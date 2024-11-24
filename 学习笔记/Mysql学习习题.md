**SQL Lesson 1: SELECT** **查询** **101**

1. 找到所有电影的名称title
   SELECT title FROM movies;
2. 找到所有电影的导演
   SELECT director FROM movies;
3. 找到所有电影的名称和导演
   SELECT title,director FROM movies;
4. 找到所有电影的名称和上映年份
   SELECT title,year FROM movies;
5. 找到所有电影的所有信息
   SELECT * FROM movies;
6. 找到所有电影的名称,Id和播放时长
   SELECT title,id,length_minutes FROM movies;
7. 请列出所有电影的ID,名称和出版国(即美国)
   SELECT id,title,"美国" as Country FROM movies;

**SQL Lesson 2:** **条件查询** **(constraints) (Pt. 1)**

1. 找到id为6的电影
   SELECT * FROM movies where id = 6;
2. 找到在2000-2010年间year上映的电影
   SELECT * FROM movies where year between 2000 and 2010;
3. 找到不是在2000-2010年间year上映的电影
   SELECT * FROM movies where year not between 2000 and 2010;
4. 找到头5部电影
   SELECT * FROM movies limit 5;
5. 找到2010（含）年之后的电影里片长小于两个小时的片子
   SELECT * FROM movies where year >=2010 and length_minutes < 120;
6. 找到99年和09年的电影,只要列出年份和片长看下
   SELECT year,length_minutes FROM movies where year =1999 or year =2009;

**SQL Lesson 3:** **条件查询****(constraints) (Pt. 2)**

1. 找到所有Toy Story系列电影
   SELECT * FROM movies where title like "%Toy Story%";
2. 找到所有John Lasseter导演的电影
   SELECT * FROM movies where director like "John Lasseter%";
3. 找到所有不是John Lasseter导演的电影
   SELECT * FROM movies where director not like "John Lasseter%";
4. 找到所有电影名为 "WALL-" 开头的电影
   SELECT * FROM movies where title like "%Wall%";
5. 有一部98年电影中文名《虫虫危机》请给我找出来
   SELECT * FROM movies where year =1998;
6. 找出所有Pete导演的电影,只要列出电影名,导演名和年份就可以
   SELECT title,director,year FROM movies where director like "%Pete%"
7. John Lasseter导演了两个系列，一个Car系列一个Toy Story系列,请帮我列出这John Lasseter导演两个系列千禧年之后(含千禧年)的电影
   SELECT * FROM movies where director="John Lasseter"and year>= 2000

**SQL Lesson 4:** **查询结果****Filtering****过滤** **和** **sorting****排序**

1. 按导演名排重列出所有电影(只显示导演)，并按导演名正序排列
   SELECT distinct director FROM movies order by director;
2. 列出按上映年份最新上线的4部电影
   SELECT * FROM movies order by year desc limit 4;
3. 按电影名字母序升序排列，列出前5部电影
   SELECT * FROM movies order by title asc limit 5;
4. 按电影名字母序升序排列，列出上一题之后的5部电影
   SELECT * FROM movies order by title asc limit 5 offset 5;
5. 如果按片长排列，John Lasseter导演导过片长第3长的电影是哪部，列出名字即可
   SELECT title FROM movies where director="John Lasseter" order by length_minutes desc limit 1 offset 2
6. 按导演名字母升序,如果导演名相同按年份降序,取前10部电影给我
   SELECT * FROM movies order by director asc,year desc limit 10;





**SQL Review:** **复习** **SELECT** **查询**

1. 列出所有加拿大人的Canadian信息(包括所有字段)
   SELECT * FROM north_american_cities where country="Canada";
2. 列出所有美国United States的城市按纬度从北到南排序(包括所有字段)

SELECT * FROM north_american_cities WHERE Longitude < '-87.629798' ORDER BY Longitude ASC;

1. 列出所有在Chicago西部的城市，从西到东排序(包括所有字段)
   SELECT * FROM north_american_cities where longitude<-87.629798 order by longitude asc;
2. 用人口数population排序,列出墨西哥Mexico最大的2个城市(包括所有字段)

SELECT * FROM North_american_cities where Country = 'Mexico' order by population desc limit 2;

1. 列出美国United States人口3-4位的两个城市和他们的人口(包括所有字段)
   SELECT * FROM north_american_cities where country='United States' order by population desc limit 2 offset 2;
2. 北美所有城市,请按国家名字母序从A-Z再按人口从多到少排列看下前10位的城市(包括所有字段)
   SELECT * FROM north_american_cities order by country asc,population desc limit 10;

**SQL Lesson 6:** **用****JOINs****进行多表联合查询**

1. 找到所有电影的国内Domestic_sales和国际销售额
   SELECT * FROM Movies left join Boxoffice on Movies.Id = Boxoffice.Movie_id;
2. 找到所有国际销售额比国内销售大的电影
   SELECT * FROM Movies left join Boxoffice on Movies.Id = Boxoffice.Movie_id where demostic_sales < international_sales;
3. 找出所有电影按市场占有率rating倒序排列
   SELECT * FROM Movies left join Boxoffice on Movies.Id = Boxoffice.Movie_id where demostic_sales < international_sales order by rating asc;
4. John Lasseter导演的每部电影每分钟值多少钱,告诉我最高的3个电影名和价值就可以
   SELECT director,international_sales FROM Movies left join Boxoffice on Movies.Id = Boxoffice.Movie_id order by international_sales limit 1;

**SQL Lesson 7:** **外连接（****OUTER JOINs****）**

1. 找到所有有雇员的办公室(buildings)名字
   SELECT distinct building FROM employees where building is not null;
2. 找到所有办公室和他们的最大容量
   SELECT * FROM buildings;
3. 找到所有办公室里的所有角色（包含没有雇员的）,并做唯一输出(DISTINCT)
   SELECT distinct buildings.building_name,employees.role FROM buildings left join employees on employees.building=buildings.building_name;
4. 找到所有有雇员的办公室(buildings)和对应的容量
   SELECT distinct building,capacity FROM employees left join buildings on employees.building=buildings.building_name where employees.building is not null;

**SQL Lesson 8:** **关于特殊关键字** **NULLs**

1. 找到雇员里还没有分配办公室的(列出名字和角色就可以)
   SELECT name,role FROM employees where Building is null;
2. 找到还没有雇员的办公室
   SELECT Building_name FROM Buildings left join Employees on Buildings.Building_name = Employees.Building where name is null;

**SQL Lesson 9:** **在查询中使用表达式**

1. 列出所有的电影ID,名字和销售总额(以百万美元为单位计算)
   SELECT id,title,(domestic_sales+international_sales)/1000000 as "销售总额" FROM Movies left join Boxoffice on Movies.Id = Boxoffice.Movie_id;
2. 列出所有的电影ID,名字和市场指数(Rating的10倍为市场指数)
   SELECT id,title,rating*100 as "市场指数" FROM Movies left join Boxoffice on Movies.Id = Boxoffice.Movie_id;
3. 列出所有偶数年份的电影，需要电影ID,名字和年份
   SELECT id,title,year from Movies left join Boxoffice on Movies.Id = Boxoffice.Movie_id where year%2=0;
4. John Lasseter导演的每部电影每分钟值多少钱,告诉我最高的3个电影名和价值就可以
   SELECT title,(domestic_sales+international_sales)/length_minutes as “价值” from Movies left join Boxoffice on Movies.Id = Boxoffice.Movie_id where director = “Jhon Lasseter” order by “价值” limit 3;
5. 电影名最长的3部电影和他们的总销量是多少
   SELECT，length(title) as title_len,title,(domestic_sales + international_sales) as “总销量” from Movies left join Boxoffice on Movies.Id = Boxoffice.Movie_id order by title_len desc limit 3;

**SQL Lesson 10:** **在查询中进行统计****I (Pt. 1)**

1. 找出就职年份最高的雇员(列出雇员名字+年份）
   SELECT name,max(years_employed) from employees;
2. 按角色(Role)统计一下每个角色的平均就职年份
   SELECT role,avg(years_employed) from employees group by role;
3. 按办公室名字总计一下就职年份总和
   SELECT building,sum(years_employed) from employees group by building
4. 每栋办公室按人数排名,不要统计无办公室的雇员
   SELECT building,count(*) as count from employees where building is not null group by building
5. 就职1,3,5,7年的人分别占总人数的百分比率是多少(给出年份和比率"50%" 记为 50)
   SELECT years_employed,count(*)*100/(select count(*) from employees) as rating from employees where years_employed in (1,3,5,7) group by years_employed

**SQL Lesson 11:** **在查询中进行统计****I (Pt. 2)**

1. 统计一下Artist角色的雇员数量
   SELECT count(*) from employees where role = “Artist”;
2. 按角色统计一下每个角色的雇员数量
   SELECT role,count(*) from employees where group by role;
3. 算出Engineer角色的就职年份总计
   SELECT sum(Years_employed) FROM employees where role = "Engineer";
4. 每栋办公室按人数排名,不要统计无办公室的雇员
   SELECT count(*) as count,Role,building is not null as bn FROM employees group by Role,bn
5. 就职1,3,5,7年的人分别占总人数的百分比率是多少(给出年份和比率"50%" 记为 50)
   SELECT Role,Years_employed/3 as year_3,count(*) as count FROM employees group by Role,year_3 order by count desc

**SQL Lesson 12:** **在查询中进行统计****I (Pt. 2)**

1. 统计出每一个导演的电影数量（列出导演名字和数量）
   SELECT director,count(*) FROM movies group by director
2. 统计一下每个导演的销售总额(列出导演名字和销售总额)
   SELECT director,sum(domestic_sales+international_sales) as "总销售额" FROM movies left join boxoffice on movies.id=boxoffice.movie_id group by director
3. 按导演分组计算销售总额,求出平均销售额冠军（统计结果过滤掉只有单部电影的导演，列出导演名，总销量，电影数量，平均销量)
   SELECT director,sum(Domestic_sales + International_sales) AS sum_sales,count(director),sum(Domestic_sales + International_sales)/count(director) AS avg_sales FROM movies LEFT JOIN boxoffice ON movies.id = boxoffice.movie_id group by director having count(director) > 1 ORDER BY avg_sales DESC LIMIT 1
4. 找出每部电影和单部电影销售冠军之间的销售差，列出电影名，销售额差额
   select title ,(select max(international_sales+domestic_sales) from boxoffice)-(international_sales+domestic_sales) AS Margin from movies left join boxoffice on movies.id=boxoffice.movie_id

## 运营想要将用户划分为25岁以下和25岁及以上两个年龄段，分别查看这两个年龄段用户数量

```mysql
--用if函数的写法。
SELECT IF(age>=25,"25岁及以上","25岁以下") AS age_cut,count(*) AS number
FROM user_profile
GROUP BY age_cut;


--用case的写法。
select case when age <25 or age is null then '25岁以下'
when age>= 25 then '25岁及以上'
end age_cut,count(*)number from user_profile group by age_cut;

```

判断成绩的等级，85-100为“优”，70-84为“良”，60-69为“及格”，60以下为“不及格”，并统计每一等级的人数。



```mysql
SELECT
CASE
WHEN GRADE BETWEEN 85 AND 100 THEN '优'
WHEN GRADE BETWEEN 70 AND 84 THEN '良'
WHEN GRADE BETWEEN 60 AND 69 THEN '及格'
ELSE '不及格'
END 等级, COUNT(*) 人数
FROM SC
GROUP BY
CASE
WHEN GRADE BETWEEN 85 AND 100 THEN '优'
WHEN GRADE BETWEEN 70 AND 84 THEN '良'
WHEN GRADE BETWEEN 60 AND 69 THEN '及格'
ELSE '不及格'
END
```