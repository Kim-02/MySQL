개요
--
많은 데이터를 가지고 있는 엑셀 데이터를 미리 구성해 놓은 MySQL로 빠르게 옮기기 위한 작업이다.   
pymysql을 사용하며 엑셀에서 데이터를 가져오는 방식으로는 openpyxl을 사용하였다.   

전체코드
--
```python
import pymysql
from openpyxl import load_workbook

main_user_list =[]
def alter_str(value):
    x = str(value)
    return x
def alter_date(value):
    x = f"20{value[0:2]}-{value[3:5]}-{value[6:]}"
    return x

range_1 = int(input("입력데이터 범위를 입력하세요: "))
for x in range(range_1):
    main_user_list.append([])

wb= load_workbook("C:\\Users\\김승환\\Desktop\\Python_Workspace\\test_xlsx.xlsx")
ws = wb.active

for down in range(range_1):
    for length in range(6):
        if length+1 == 4 or length+1 == 6:
            main_user_list[down].append(alter_date(ws.cell(down+2,length+1).value))
        else:
            main_user_list[down].append(ws.cell(down+2,length+1).value)
print(main_user_list)

conn = pymysql.connect(host='localhost',user='root',db='developer',password='best0804',charset='utf8')

cursor = conn.cursor()

# sql = '''INSERT INTO user (number,name,sex,day_end) VALUES (%s, %s, %s, %s) '''
for value in range(range_1):
    cursor.execute(f'''INSERT INTO user (number,name,phone_num,birth,sex,day_end) 
    VALUES ({main_user_list[value][0]},'{main_user_list[value][1]}','{main_user_list[value][2]}','{main_user_list[value][3]}','{main_user_list[value][4]}','{main_user_list[value][5]}')''')

conn.commit()
conn.close()
```    


함수설정
--
```python
main_user_list =[]
def alter_str(value):
    x = str(value)
    return x
def alter_date(value):
    x = f"20{value[0:2]}-{value[3:5]}-{value[6:]}"
    return x
```   
리스트에 담아 관리할 main_user_list라는 리스트를 하나 만들어준다.    
sql데이터에 들어갈 때는 평소에 사용하지 않는 date라는 형태가 있다.   
엑셀 데이터에 날짜 표기 형식이 02.01.02이런식으로 표현되어 있어 2002-01-25형태로 바꿔주기 위해 각 부분을 따와서 바꿔주는 함수를 작성하였다.   

데이터 인서트 범위 설정
--
```python
range_1 = int(input("입력데이터 범위를 입력하세요: "))
for x in range(range_1):
    main_user_list.append([])
```   
인서트 범위를 설정해주기 위해 범위를 받는 변수를 만들었다.    
이렇게 한 이유는 범위를 일일히 지정하면 전체 코드에서 찾아 바꿔야 하는데, 쉽지않다.    
따라서 애초부터 입력 범위를 받아서 입력을 하면 데이터를 변경할 필요가 없기 때문에 이런 방식을 채택하였다.     
이중 리스트를 사용하여 인자들을 받을 예정이기 때문에 리스트를 원하는 값만큼 만들어서 인서트해준다.   

엑셀데이터 열기
--
```python
wb= load_workbook("C:\\Users\\김승환\\Desktop\\Python_Workspace\\test_xlsx.xlsx")
ws = wb.active
```   
간단하게 openpyxl에 있는 메소드인 load_workbook을 가져와 엑셀파일을 열어준다.   

엑셀 데이터 읽기
--
가져온 엑셀 데이터를 읽어준다.   
pandas를 이용하지 않고 openpyxl을 채용한 이유는 pandas는 한줄 한줄 긴 데이터를 읽어올 때 편리한 기능을 가지고 있다.   
하지만 현제 해야하는 방식은 하나하나의 셀에 들어가 값을 리스트에 넣어줘야 하기 때문에 한줄을 가져오는 것은 별로 의미가 없다.    
따라서 openpyxl을 활용하여 각각의 셀에 접근하였다.   
```python
for down in range(range_1):
    for length in range(6):
        if length+1 == 4 or length+1 == 6:
            main_user_list[down].append(alter_date(ws.cell(down+2,length+1).value))
        else:
            main_user_list[down].append(ws.cell(down+2,length+1).value)
```   
하나하나 살펴보면   
```python
for down in range(range_1):
```   
openpyxl에서 셀을 읽는 방식을 먼저 알아야한다.   
ws.cell(y,x).value이런 형식으로 데이터를 읽어오게 된다.   
따라서 이중 for문을 활용하여 이차원 형식의 데이터를 가져올 수 있도록 할 것이다.    
먼저 어디까지 긁어올 지 사용자에게 입력하도록 한 후 range값을 넣어 그만큼 반복하도록 한다.     
```python
for length in range(6):
```   
읽어올 데이터의 종류가 몇개인지 지정하는 코드이다.   
현제 읽어올 데이터는 총 6종류임으로 총 6번 반복하면 되기 때문에 range값을 6을 주었다.   
때에 따라 제어하기 위해 input문으로 사용자에게 직접입력받는 방법도 있다.   

```python
if length+1 == 4 or length+1 == 6:
    main_user_list[down].append(alter_date(ws.cell(down+2,length+1).value))
else:
    main_user_list[down].append(ws.cell(down+2,length+1).value)
```   
