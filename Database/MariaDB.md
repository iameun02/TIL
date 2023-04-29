## SQL Programming 

<br/>

#### 1. IF문 활용 

```sql
drop procedure if exists ifproc;

delimiter $$
create procedure ifproc()
begin
	
	declare var1 int;
	set var1 = 100;
	
    if var1 =100 then
    	select '100과 일치합니다.';
    else
    	select '100이 아닙니다.';
    end if;
	
	
end $$ 
delimiter ;

call ifproc();

```
#### 2. CASE문 활용
```sql
drop procedure if exists caseproc;

delimiter $$
create procedure caseproc()
begin
	
	declare point int;
	declare grade char(1);
	set point =75;

	case 
		when point >=90 then
			set grade = 'A';
		when point >=80 then
			set grade = 'B';
		when point >=70 then
			set grade = 'C';
		when point >=60 then
			set grade = 'D';
		else set grade = 'F';
	end case;
	
	select point, grade;
	
end $$
delimiter ;

call caseproc()
```
<br/>

#### 3. While 반복문 활용
```sql
drop procedure if exists whileproc;

delimiter $$
create procedure whileproc()
begin
	
	declare i int;
	declare total int;
	
	set i = 0;
	set total = 0;

	while i < 100 do
		set i = i+1;
		set total = total +i;
	end while;
	
	select i , total;
end $$
delimiter ;

call whileproc();
```
<br/>

#### 4. Iterater, Leave문 활용
```sql
drop procedure if exists whileproc2;

delimiter $$
create procedure whileproc2()
begin
	
	declare i int;
	declare total int;
	
	set i = 0;
	set total = 0;

	mywhile: while i < 100 do
		set i = i+1;
	
		if (i%2 =0) then
			iterate mywhile;
		end if;
	
		set total = total +i;
	
		if total > 1000 then
			leave mywhile ;
		end if;
	end while;
	
	select i , total;
end $$
delimiter ;

call whileproc2();
```
#### 5. 오류처리
```sql
drop procedure if exists errorproc; 

delimiter $$
create procedure errorproc()
begin
	
	declare continue handler for sqlexception
	begin
		show errors;
		rollback;
	end;
	
	insert into 테이블명(컬럼명1, 컬럼명2, 컬럼명3)
		values(값1, 값2, 값3);
	
end $$
delimiter ;


call errorproc();
```
<br/>

#### 5. 동적 SQL문 (쿼리를 변수에 담아 실행)
```sql
prepare myQuery from 'select * from 테이블명 where 조건절';
execute myQuery 

deallocate prepare myQuery;
```

#### 5-1. userid, mobile 조건 값을 변수로 대입 
```sql
set @userid = 'KKK';  /*대화식모드에서의 변수선언 방법*/
set @mobile ='010';

prepare myQuery from 'select * from 테이블명 where userid = ? and mobile = ?';
execute myQuery using @userid, @mobile;

deallocate prepare myQuery;
```
<br><br>

## 고급 SQL 
<br/>

### 1. 동일 데이터를 다양하게 조회
#### 1) 테이블 생성
``` sql 
create table pivottbl(
 product varchar(10)
,quater varchar(10)
,amount int);
```
#### 2) 데이터 삽입
``` sql
insert into pivottbl values
('TV', '1', 10), ('TV', '2', 20), ('TV', '2', 15), ('TV' ,'4' ,25),
('세탁기', '1', 5), ('세탁기', '3', 10),('세탁기', '3', 15), ('세탁기', '4', 20),
('에어컨', 2, 20), ('에어컨', 3, 10);
```

#### 3) SELECT 조회
* #### SUM IF 문 활용
```sql
select product
 ,sum(if(quater = '1', amount, 0)) '1분기'
 ,sum(if(quater = '2', amount, 0)) '2분기'
 ,sum(if(quater = '3', amount, 0)) '3분기'
 ,sum(if(quater = '4', amount, 0)) '4분기'
from pivottbl
group by product;
```
* #### CASE WHEN 문 활용
```sql
select product
 ,case 
   when quater ='1' then "1분기"
   when quater ='2' then "2분기"	
   when quater ='3' then "3분기"	
   when quater ='4' then "4분기" end as 분기
 ,sum(amount)
from pivottbl
group by product,
  case 
   when quater ='1' then "1분기"
   when quater ='2' then "2분기"	
   when quater ='3' then "3분기"	
   when quater ='4' then "4분기"
  end ;
  ```

  * #### CASE WHEN 문 활용
``` sql
select product 
,sum(case when quater ='1' then amount else 0 end)"1분기"
,sum(case when quater ='2' then amount else 0 end) "2분기"
,sum(case when quater ='3' then amount else 0 end)"3분기"
,sum(case when quater ='4' then amount else 0 end) "4분기"
from pivottbl
group by product;
```
<br/>

### 2. Trigger
#### 1) 백업 테이블 생성
```sql
create table 백업테이블명
(속성1 char(10)
,속성2 char(20)
,속성3 char(20)
,속성4 date
);
```
#### 2) 트리거 생성
```sql
delimiter //
create trigger 트리거명
after|before insert|update|delete on 원테이블명
for each row
begin
    insert into 백업테이블명
    values (old.속성1, old.속성2, old.속성3, curdate());

end //
delimiter ;
```
#### 3) 트리거 확인
```sql
select * from 원테이블명;
select * from 백업테이블명;
```
<br><br>

## SQL을 활용한 텍스트 내 키워드 검색
<br/>

### 0. DB 생성 
```sql
create database fulltextdb;
use fulltextdb;
```
<br/>

### 1. 테이블 생성
```sql
create table fulltexttbl
(id 	int auto_increment primary key
,section	varchar(15) not null
,description varchar(1000)
);
```
<br/>

### 2. 데이터 삽입

```sql
insert into fulltexttbl values
(NULL, N'경제', N'수도권 아파트도 3곳 중 1곳은 깡통전세..집값급락'),
(NULL, N'사회', N'백화점 천장 균열 알고도 11시간 영업... 폐점 뒤에야 보수'),
(NULL, N'생활', N'밤사이 중부 눈... 내일 아침, 빙판길 주의'),
(NULL, N'정치', N'원전으로 마중나온 만수르.. UAE와 MOU 48건 체결'),
(NULL, N'세계', N'한국인 2명 탑승 네팔 추락여객기 실종자 수색 재게');
```
:bulb: SQL Server에서 유니코드 문자열 상수를 다룰 때는 모든 유니코드 문자열 앞에 대문자 N이 와야한다.
<br/>

### 3. 전체 텍스트 인덱스 생성 
```sql
create fulltext index idx_fulltxttbl
on fulltexttbl(description); -- description 컬럼에 대해 인덱스 생성

/*확인*/
show index from fulltexttbl;
```
<br/>

### 4. 인덱스 생성 규칙 설정
+ 인덱스 생성 최소 길이 확인
+ 전체 텍스트 인덱스 테이블 데이터 확인 
```sql
set global innodb_ft_aux_table ='fulltextdb/fulltexttbl'; -- 디비명/테이블명 

select * from information_schema.INNODB_FT_INDEX_TABLE; -- 생성된 단어 확인
```
<br/>

### *Mac 생성 최소 길이 설정 (Default : 3) 
1) 터미널에서 my.cnf 파일을 연다.
2) 아래 구문을 작성하여 입력 후 저장하고 닫는다.
``` sql
[mysqld]
ft_min_word_len = 2
innodb_ft_min_token_size = 2
```
3. Mariadb 연결을 끊었다가 재기동한다.
   - brew services stop mariadb
   - brew services restart mariadb

4. 설정이 잘 바뀌었는지 확인한다.
   - show variables like  'innodb_ft_min_token_size';
   - show variables like 'ft_min%'

<br/>

### 5. 전체 텍스트 검색 
- in natural mode (정확한 단어 검색)
```sql
select * from fulltexttbl
where match(description) against('내일 한국인'); -- or 연산자 적용됨 (내일 or 한국인)
```

- in boolean mode (- : 제외, * : 부분포함, + : 정확히 포함)
```sql
select * from fulltexttbl
 where match(description) against('-아파트* +한국인' in boolean mode);
```

