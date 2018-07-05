
# Leetcode: Human Traffic of Stadium     :BLOG:Hard:

---

Human Traffic of Stadium  

---

Similar Problems:  

-   [Review: SQL Problems](https://code.dennyzhang.com/review-sql), [Tag: #sql](https://code.dennyzhang.com/tag/sql)

---

X city built a new stadium, each day many people visit it and the stats are saved as these columns: id, date, people  

Please write a query to display the records which have 3 or more consecutive rows and the amount of people more than 100(inclusive).  

For example, the table stadium:  

    +------+------------+-----------+
    | id   | date       | people    |
    +------+------------+-----------+
    | 1    | 2017-01-01 | 10        |
    | 2    | 2017-01-02 | 109       |
    | 3    | 2017-01-03 | 150       |
    | 4    | 2017-01-04 | 99        |
    | 5    | 2017-01-05 | 145       |
    | 6    | 2017-01-06 | 1455      |
    | 7    | 2017-01-07 | 199       |
    | 8    | 2017-01-08 | 188       |
    +------+------------+-----------+

For the sample data above, the output is:  

    +------+------------+-----------+
    | id   | date       | people    |
    +------+------------+-----------+
    | 5    | 2017-01-05 | 145       |
    | 6    | 2017-01-06 | 1455      |
    | 7    | 2017-01-07 | 199       |
    | 8    | 2017-01-08 | 188       |
    +------+------------+-----------+

Note:  
Each day only have one row record, and the dates are increasing with id increasing.  

Github: [challenges-leetcode-interesting](https://github.com/DennyZhang/challenges-leetcode-interesting/tree/master/problems/human-traffic-of-stadium)  

Credits To: [leetcode.com](https://leetcode.com/problems/human-traffic-of-stadium/description/)  

Leave me comments, if you have better ways to solve.  

---

    ## Blog link: https://code.dennyzhang.com/human-traffic-of-stadium
    SET @group_number=0;
    
    select distinct stadium.id, stadium.date, stadium.people
    from stadium inner join
        (select min(id) as min_id, max(id) as max_id, group_id
        from (select t3.*, if(below_100 != next_day_below_100 , @group_number:=@group_number+1, @group_number) as group_id
    	  from (select t1.*, t2.below_100 as next_day_below_100
    	     from
    	     (select id, date, people, if(people<100, 1, 0) as below_100
    	     from stadium) t1 left join  
    	     (select id, date, people, if(people<100, 1, 0) as below_100
    	     from stadium) t2
    	     on t1.id = t2.id + 1
    	     order by t1.id asc) t3) as t4
        group by group_id
        having count(1)>=3) as t5
    where stadium.id >= min_id and stadium.id <= max_id
    order by stadium.id asc
