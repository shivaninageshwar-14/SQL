# SQL
This Repository consist of all my sql codes
create database W;
use W;
create table sailor(sid integer not null,sname varchar(32),rating integer,age real,CONSTRAINT PK_sailor PRIMARY KEY(sid));
insert into sailor values(22,"dustin",7,45);
insert into sailor values(29,"Brutus",1,33);
insert into sailor values(31,"Lubber",8,55.5);
insert into sailor values(32,"Andy",8,25.5);
insert into sailor values(58,"Rusty",10,35);
insert into sailor values(64,"Horatio",7,35);
insert into sailor values(71,"Zorba",10,16);
insert into sailor values(74,"Horatio",9,40);
insert into sailor values(85,"Art",3,25.5);
insert into sailor values(95,"Bob",3,63.5);
create table boat(bid int,bname varchar(10),color varchar(10),CONSTRAINT PK_BOAT PRIMARY KEY(bid));
select s.sname from sailor s where s.rating > 8;
select b.bname, b.color from boat b;
select b.bname from boat b where b.color = 'red';
select b.bname from boat b where b.color = 'red';
select s.sname from sailor s, reserves r where s.sid = r.sid and r.bid = 103;
select s.sid from sailor s, boat b, reserves r where s.sid = r.sid and b.bid = r.bid and b.color = 'pink';
select s.sid from sailor s, boat b, reserves r where s.sid = r.sid and b.bid = r.bid and b.color = 'pink';
select s.sname from sailor s, boat b, reserves r where s.sid = r.sid and b.bid = r.bid and b.color = 'red';
select distinct b.color from sailor s, boat b, reserves r where s.sid = r.sid and b.bid = r.bid and s.sname = 'Lubber';
select distinct s.sname from sailor s, reserves r where s.sid = r.sid;



select s.sname, s.age from sailor s;
select s.sname from sailor s where s.rating > 7 and s.age > 25;




insert into boat values(101,"Intertake","blue");
insert into boat values(102,"Intertake","red");
insert into boat values(103,"Clipper","green");
insert into boat values(104,"Marine","red");
create table reserves(sid integer not null,bid integer not null,day datetime not null,CONSTRAINT PK_reserves PRIMARY KEY(sid,bid,day),FOREIGN KEY(sid)REFERENCES sailor(sid),FOREIGN KEY(bid) REFERENCES boat(bid));
insert into reserves values(22,101,"1998-10-10");
insert into reserves values(22,102,"1998-10-10");
insert into reserves values(22,103,"1998-10-8");
insert into reserves values(22,104,"1998-10-7");
insert into reserves values(31,103,"1998-11-6");
insert into reserves values(31,104,"1998-11-12");
insert into reserves values(64,101,"1998-9-5");
insert into reserves values(64,102,"1998-9-8");
insert into reserves values(74,103,"1998-9-8");
select s.sname,s.age from sailor s;
select s.sname from sailor s, boat b, reserves r where s.sid = r.sid and b.bid = r.bid and b.color = 'red'
union

select s.sname from sailor s, boat b, reserves r where s.sid = r.sid and b.bid = r.bid and b.color = 'green';
select s.sname from sailor s where s.sid in (select r.sid from reserves r where r.bid = 103);
select s.sname from sailor s where s.sid in (select r.sid from reserves r, boat b where r.bid = b.bid and b.color = 'red'); 
select s.sname from sailor s where s.sid not in (select r.sid from reserves r, boat b where r.bid = b.bid and b.color = 'red');  
select s.sname from sailor s where exists (select * from reserves r where r.bid = 103 and r.sid = s.sid);
select s1.sname from sailor s1 where s1.rating > any (select s2.rating from sailor s2 where s2.sname = 'Dustin');
select s1.sname from sailor s1 where s1.rating > all (select s2.rating from sailor s2 where s2.sname = 'Bob');
select s.sname from sailor s where s.rating = (select max(s2.rating) from sailor s2);
select avg(s.age) as average_age from sailor s;
select avg(s.age) as average_age from sailor s where s.rating = 10;
select count(*) as sailor_count from sailor s;
select count(distinct s.rating) as rating_count from sailor s;


select s.sname from sailor s where s.age > (select max(s2.age) from sailor s2 where s2.rating = 10);



select s.rating, min(s.age) as youngest_age from sailor s group by s.rating;
select s.rating, min(s.age) as youngest_voting_age from sailor s where s.age >= 18 group by s.rating having count(*) >= 2;
select b.bid, b.bname, count(r.sid) as reservation_count from boat b join reserves r on b.bid = r.bid where b.color = 'red' group by b.bid, b.bname;
select s.sname from sailor s order by s.sname;
select * from sailor s order by s.rating;
select * from sailor s order by s.rating desc, s.age;






