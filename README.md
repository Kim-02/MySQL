## MySQL

개발 환경으로는 VS코드에서 지원하는 Explor을 사용하였다.

![VS코드](https://user-images.githubusercontent.com/80444565/123954566-852c2b00-d9e3-11eb-9a79-8a6bfc452afe.PNG)
--
위와 같이 간단한 인터페이스로 데이터베이스를 생성하고 지우고 테이블을 관리할 수 있다.
따라서 CREATE DATABASE, USE와 같은 데이터베이스를 생성하는 명령어를 사용할 필요가 없다는 장점을 가지고 있다.

SQL문법은 다음과 같다.
- CREATE TABLE, 말그대로 테이블 하나를 생성한다. 

![image](https://user-images.githubusercontent.com/80444565/123956434-a9890700-d9e5-11eb-8f33-141173f343c7.png)
--
후에 실행을 해보면 
> ![image](https://user-images.githubusercontent.com/80444565/123957418-b823ee00-d9e6-11eb-8d4f-ba2a86efd84a.png)

이런 형식으로 실행이 된다.
이로써 우리는 각 요소들로 인해 네이밍을 할 수 있고 그 뒤에 형식을 지정해서 데이터베이스를 입력할 수 있도록 만들 수 있다는 것을 알 수 있다.

Table
--
테이블 조작에 관한 설명이다.
- Alter   
테이블을 조작할 수 있는 성질을 가지고 있다.   
사용 방식은 아래와 같다.   
![image](https://user-images.githubusercontent.com/80444565/123962627-a1809580-d9ec-11eb-8b99-320d543f2414.png)   
형식을 살펴보면 ALTER TABLE [테이블명] ADD 필드이름 필드타입   
이런 형식으로 추가를 한다.   
테이블을 어떤것을 변경할지 선택한 후 뒤에 입력을 해준다.   
사용할 수 있는 명령어는    
- ADD 필드이름 필드타입 
- DROP 필드이름
- MODIFY COLUMN 필드이름 필드타입   

Drop
--   
삭제에 관한 설명이다    
사용 방식은 아래와 같다   
![image](https://user-images.githubusercontent.com/80444565/124071759-d0dde380-da7a-11eb-976b-7f6ef4627e74.png)   
Drop 이후 삭제할 요소를 입력한다   
   
TRUNCATE
--   
Drop으로 요소를 삭제하면 당연하게도 모든 데이터가 소실된다.   
이 때 저장된 데이터만 날리고 요소는 남겨두고 싶을 때 Truncate을 사용한다. 방법은 아래와 같다    
![image](https://user-images.githubusercontent.com/80444565/124072974-747bc380-da7c-11eb-9ed6-33f10771eae0.png)     
테이블에 있는 데이터만 날아가고 다시작성할 수 있는 상태가 된다.   

if exist문을 이용한다면 테이블이 없어 발생하는 애러를 막을 수 있다.   
![image](https://user-images.githubusercontent.com/80444565/124073218-d3d9d380-da7c-11eb-89bb-52fb995c9a15.png)    

INSERT
--    
insert INTO문과 VLAUES절을 사용하여 테이블에 새로운 레코드를 추가할 수 있다.   
지정되있는 테이블요소에 데이터값을 집어넣는 것이다. 사용방법은 아래와 같다.   
![image](https://user-images.githubusercontent.com/80444565/124074745-e81ed000-da7e-11eb-94d1-7c3c4360bc9c.png)   
필드에 지정할 값을 정하고 그 값의 순서에 맞춰서 VALUSE()에 지정을 해주면된다. 유의할 점은 문자열일 경우에 ''로 묶어줘야 한다는 점이다.   
