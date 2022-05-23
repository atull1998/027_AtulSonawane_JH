#----------------------------------------------------------------------------------------------
                       #SECTION 1 :-
#-----------------------------------------------------------------------------------------------
create database exam;
use exam;

create table DEPT7(
DEPTNO int (2),
DNAME varchar(15),
LOC Varchar (10));


select * from DEPT7;

insert into DEPT7
values(10,'ACCOUNTING','NEWYORK'),
(20,'RESEARCH','DALLAS'),
(30,'SALES','CHICAGO'),
(40,'OPERATIONS','BOSTON');

create table EMP4(
EMPNO int (4),
ENAME varchar(10),
JOB varbinary(9),
HIREDATE date,
SAL float(7,2),
COMM float(7,2),
DEPTNO int(2));

insert into EMP values
(7839,'KING','MANAGER','1991-11-17',5000,NULL,10),
(7698,'BLAKE','CLERK','1981-05-01',2850,NULL,30),
(7782,'CLARK','MANAGER','1981-06-09',2450,NULL,10),
(7566,'JONES','CLERK','1981-04-02',2975,NULL,20),
(7654,'MARTIN','SALESMAN','1981-09-28',1250,1400,30),
(7499,'ALLEN','SALESMAN','1981-02-20',1600,300,30);



#3. Display all the employees where SAL between 2500 and 5000 (inclusive of both)
select * from EMP where SAL between 
2500 and 5000;

#4. Display all the ENAMEs in descending order of ENAME.
select ENAME from emp 
order by Ename desc;

#5. Display all the JOBs in lowercase.
select lower(JOB)
from emp;

#6. Display the ENAMEs and the lengths of the ENAMEs.
select ENAME,length(ENAME)as length
from EMP;

#7. Display the DEPTNO and the count of employees who belong to that DEPTNO .
select d.DEPTNO,count(e.DEPTNO)from
dept d inner join emp e group by
d.DEPTNO;

#8. Display the DNAMEs and the ENAMEs who belong to that DNAME.
select DNAME,ENAME from EMP join DEPT
on emp.DEPTNO = DEPT.DEPTNO;


#9. Display the position at which the string ‘AR’ occurs in the ename.
select ENAME,instr(ENAME,'AR')from EMP;

#10. Display the HRA for each employee given that HRA is 20% of SAL.
select ename , sal*0.20 as HRA from EMP;



#---------------------------------------------------------------------------------------------------------------
                          #section 2:-
#----------------------------------------------------------------------------------------------------------------
                                     # VALID TRIANGLE 
delimiter //
create function valid_triangle(s1 float, s2 float, s3 float)
returns boolean
deterministic
begin	
	 if (s1+s2>s3) and (s1+s3>s2) and (s2+s3>s1) then
     return true ;
     else
     return false;
     end if ;
end ; //
delimiter ;

delimiter //
create procedure abc(s1 float, s2 float, s3 float)
begin
	if valid_triangle(s1,s2,s3) then
		insert into tempp values (s1,s2,s3,'Valid triangle');
	else 
		insert into tempp values (s1,s2,s3,'Invalid triangle');
	end if ;
end ;//
delimiter ;

call abc (7,10,5) ;

create table tempp (
side1 float,
side2 float,
side3 float,
triangle_status varchar(20));

#---------------------------------------------------------------------------------------------------------------------------------
                                             #TWO CHAR STRING 
create table temp
(
  s1 char (10),
  s2 char(20),
  ans char(10)
  );
  
  delimiter //
  create procedure abc(s1 char(20), s2 char (20))
  begin
       
       declare a int(4);
       set a=locate(s1,s2);
       if(a != 0) then
       insert into temp values (s1,s2,'present');
       else
       insert into temp values (s1,s2,'absent');
       end if;
end; //
delimiter ;

call abc('amey','ameypatekar');
call abc('abc','wogigabksdf');
call abc('abc','abdc');
call abc('abc','abcdef');


select * from temp;
drop procedure abc;
drop table temp;