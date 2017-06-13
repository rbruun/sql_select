1)

mysql> select first_name, last_name from student;
+------------+-----------+
| first_name | last_name |
+------------+-----------+
| Eric       | Ephram    |
| Greg       | Gould     |
| Adam       | Ant       |
| Howard     | Hess      |
| Charles    | Caldwell  |
| James      | Joyce     |
| Doug       | Dumas     |
| Kevin      | Kraft     |
| Frank      | Fountain  |
| Brian      | Biggs     |
+------------+-----------+
10 rows in set (0.00 sec)

2)

mysql> select * from student where years_of_experience < 8;
+------------+------------+-----------+---------------------+------------+
| student_id | first_name | last_name | years_of_experience | start_date |
+------------+------------+-----------+---------------------+------------+
|          1 | Eric       | Ephram    |                   2 | 2016-03-31 |
|          2 | Greg       | Gould     |                   6 | 2016-09-30 |
|          3 | Adam       | Ant       |                   5 | 2016-06-02 |
|          4 | Howard     | Hess      |                   1 | 2016-02-28 |
|          5 | Charles    | Caldwell  |                   7 | 2016-05-07 |
|          8 | Kevin      | Kraft     |                   3 | 2016-04-15 |
|         10 | Brian      | Biggs     |                   4 | 2015-12-25 |
+------------+------------+-----------+---------------------+------------+
7 rows in set (0.00 sec)

3)

mysql> select last_name, start_date, student_id from student order by last_name;
+-----------+------------+------------+
| last_name | start_date | student_id |
+-----------+------------+------------+
| Ant       | 2016-06-02 |          3 |
| Biggs     | 2015-12-25 |         10 |
| Caldwell  | 2016-05-07 |          5 |
| Dumas     | 2016-07-04 |          7 |
| Ephram    | 2016-03-31 |          1 |
| Fountain  | 2016-01-31 |          9 |
| Gould     | 2016-09-30 |          2 |
| Hess      | 2016-02-28 |          4 |
| Joyce     | 2016-08-27 |          6 |
| Kraft     | 2016-04-15 |          8 |
+-----------+------------+------------+
10 rows in set (0.00 sec)

4)

mysql> select * from student where first_name in ('Adam', 'James', 'Frank')
    -> order by last_name desc;
+------------+------------+-----------+---------------------+------------+
| student_id | first_name | last_name | years_of_experience | start_date |
+------------+------------+-----------+---------------------+------------+
|          6 | James      | Joyce     |                   9 | 2016-08-27 |
|          9 | Frank      | Fountain  |                   8 | 2016-01-31 |
|          3 | Adam       | Ant       |                   5 | 2016-06-02 |
+------------+------------+-----------+---------------------+------------+
3 rows in set (0.00 sec)

5)

mysql> select * from student where start_date between '2016-01-01' and '2016-06-30';
+------------+------------+-----------+---------------------+------------+
| student_id | first_name | last_name | years_of_experience | start_date |
+------------+------------+-----------+---------------------+------------+
|          1 | Eric       | Ephram    |                   2 | 2016-03-31 |
|          3 | Adam       | Ant       |                   5 | 2016-06-02 |
|          4 | Howard     | Hess      |                   1 | 2016-02-28 |
|          5 | Charles    | Caldwell  |                   7 | 2016-05-07 |
|          8 | Kevin      | Kraft     |                   3 | 2016-04-15 |
|          9 | Frank      | Fountain  |                   8 | 2016-01-31 |
+------------+------------+-----------+---------------------+------------+
6 rows in set (0.01 sec)

------------------- Medium Challenge ------------------------------

mysql> explain assignment;
+----------------+------------------+------+-----+---------+----------------+
| Field          | Type             | Null | Key | Default | Extra          |
+----------------+------------------+------+-----+---------+----------------+
| assignment_id  | int(11) unsigned | NO   | PRI | NULL    | auto_increment |
| student_id     | int(11)          | NO   |     | NULL    |                |
| assignment_nbr | int(11)          | NO   |     | NULL    |                |
| class_id       | int(11)          | YES  |     | NULL    |                |
| grade_id       | int(11) unsigned | YES  | MUL | NULL    |                |
+----------------+------------------+------+-----+---------+----------------+
5 rows in set (0.00 sec)

mysql> select * from assignment;
+---------------+------------+----------------+----------+----------+
| assignment_id | student_id | assignment_nbr | class_id | grade_id |
+---------------+------------+----------------+----------+----------+
|             1 |          3 |              1 |        2 |        1 |
|             2 |          2 |              1 |        2 |        2 |
|             3 |          4 |              1 |        1 |        2 |
|             4 |          4 |              1 |        1 |        1 |
|             5 |          5 |              1 |        1 |        5 |
|             8 |          5 |              3 |        1 |        1 |
|             9 |          6 |              3 |        1 |        2 |
|            10 |          7 |              3 |        1 |        2 |
|            11 |          8 |              3 |        1 |        2 |
+---------------+------------+----------------+----------+----------+
9 rows in set (0.00 sec)

mysql> explain grade;
+-------------------+------------------+------+-----+---------+----------------+
| Field             | Type             | Null | Key | Default | Extra          |
+-------------------+------------------+------+-----+---------+----------------+
| grade_id          | int(11) unsigned | NO   | PRI | NULL    | auto_increment |
| grade_description | char(30)         | YES  |     | NULL    |                |
+-------------------+------------------+------+-----+---------+----------------+
2 rows in set (0.00 sec)

mysql> select * from grade;
+----------+-----------------------------+
| grade_id | grade_description           |
+----------+-----------------------------+
|        1 | Incomplete                  |
|        2 | Complete and unsatisfactory |
|        3 | Complete and Satisfactory   |
|        4 | Exceeds expectations        |
|        5 | Not graded                  |
+----------+-----------------------------+
5 rows in set (0.00 sec)

-------------------------   Hard Challenge  ------------------------

| assignment | CREATE TABLE `assignment` (
  `assignment_id` int(11) unsigned NOT NULL AUTO_INCREMENT,
  `student_id` int(11) unsigned NOT NULL,
  `assignment_nbr` int(11) NOT NULL,
  `class_id` int(11) DEFAULT NULL,
  `grade_id` int(11) unsigned DEFAULT NULL,
  PRIMARY KEY (`assignment_id`),
  KEY `idx_grade_id` (`grade_id`),
  KEY `idx_student_id` (`student_id`),
  CONSTRAINT `fk_grade_id` FOREIGN KEY (`grade_id`) REFERENCES `grade` (`grade_id`),
  CONSTRAINT `fk_student_id` FOREIGN KEY (`student_id`) REFERENCES `student` (`student_id`)
) ENGINE=InnoDB AUTO_INCREMENT=13 DEFAULT CHARSET=utf8 |