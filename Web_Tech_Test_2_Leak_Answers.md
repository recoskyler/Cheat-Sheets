# Web Tech Test 2

## 1

- T
- F
- T
- T
- T
- T
- T
- F
- F
- F

> https://www.w3schools.com/sql/sql_intro.asp
> SQL is a standard language for accessing and manipulating databases.

## 2

A cookie is information stored on your device by a website you visit. They are used for keeping states of personalized settings, "remember me" info. etc. on a website. They are stored as single or multiple files on your device.

## 3

```js
var timer = setInterval(() => {doSomething(p1)}, 5000);
```

## 4

**PK** is *"Primary Key"*, the ID number of the item itself.

**FK** is *"Foreign Key"*. the ID number of another item, which might be on another table. It points to another item.

**PK** and **FK** are essential for creating relational databases, as they allow us to link tables and items by their IDs.

## 5

Sessions are stored on the server, which means modifying them is difficult as you don't have access to the file(s) that store the sessions on the server. Because cookies are stored on tht device itself, the user can easily modify them.

## 6

> I'm not sure about this one :/

If a hacker somehow views the main PHP file that includes credentials for connecting to your database, s/he can easily gain access to your database.

> On the slides, it says that you should separate it so that you don't need to type it again and again.

## 7

Ajax is a method for requesting, receiving, sending data to/from a server in the background (asynchronous), and updating a page without the need of reloading. It uses REST asynchronously to perform these actions.

## 8

```js
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  printDetails() {
    console.log("Name: " + this.name + "\nAge: " + this.age);
  }
}

let atalay = new Person("Atalay", 19);

atalay.printDetails();
```

## 9

```SQL
DELETE FROM DBTEST;
```

OR

```SQL
TRUNCATE TABLE DBTEST;
```

## 10

### A

```SQL
SELECT D.ID, D.student_name, C.course_name, C.course_code, C.ects_credits, S.the_year 
  FROM declarations D, courses C, study_semesters S WHERE
  D.courses_ID = C.ID AND D.semesters_ID = S.ID AND S.the_year = 2019 AND
  C.ects_credits >= 6.00 AND C.study_semesters_ID = D.semesters_ID;
```

### B

```SQL
UPDATE courses SET old_credits = ects_credits * 1.5 WHERE ects_credits >= 6.00;
```

### C

```SQL
DELETE FROM study_semesters WHERE the_year <= 2000;
```

### If you'd ike to try it, you need to create the tables and insert items first

You can use [this](https://www.db-fiddle.com/f/8eHhQNYnQfxoT8NREP9XxU/0).

#### Create Tables

```SQL
CREATE TABLE semester_type (
  ID int NOT NULL,
  type varchar(120) NOT NULL,
  PRIMARY KEY (ID)
);

CREATE TABLE study_semesters (
  ID int NOT NULL,
  semester_type_ID int NOT NULL,
  semester_name varchar(120) NOT NULL,
  the_year year NOT NULL,
  PRIMARY KEY (ID),
  FOREIGN KEY (semester_type_ID) REFERENCES semester_type(ID)
);

CREATE TABLE courses (
  ID int NOT NULL,
  study_semesters_ID int NOT NULL,
  course_code varchar(7) NOT NULL,
  course_name varchar(120) NOT NULL,
  ects_credits decimal(2, 1) NOT NULL,
  old_credits decimal(2, 1),
  PRIMARY KEY (ID),
  FOREIGN KEY (study_semesters_ID) REFERENCES study_semesters(ID)
);

CREATE TABLE declarations (
  ID int NOT NULL,
  courses_ID int NOT NULL,
  semesters_ID int NOT NULL,
  student_code varchar(10) NOT NULL,
  student_name varchar(45) NOT NULL,
  remarks varchar(125) NOT NULL,
  PRIMARY KEY (ID),
  FOREIGN KEY (courses_ID) REFERENCES courses(ID),
  FOREIGN KEY (semesters_ID) REFERENCES study_semesters(ID)
);
```

#### Insert Items

```SQL
INSERT INTO semester_type (ID, type) VALUES (0, "a");
INSERT INTO study_semesters (ID, semester_type_ID, semester_name, the_year) VALUES (1, 0, "s1", 2019);
INSERT INTO study_semesters (ID, semester_type_ID, semester_name, the_year) VALUES (0, 0, "s0", 2018);
INSERT INTO study_semesters (ID, semester_type_ID, semester_name, the_year) VALUES (2, 0, "s2", 2020);
INSERT INTO courses (ID, study_semesters_ID, course_code, course_name, ects_credits, old_credits) VALUES (0, 1, "OK0", "COURSE OK0", 6.00, 5);
INSERT INTO courses (ID, study_semesters_ID, course_code, course_name, ects_credits, old_credits) VALUES (1, 1, "OK1", "COURSE OK1", 7.20, 5);
INSERT INTO courses (ID, study_semesters_ID, course_code, course_name, ects_credits, old_credits) VALUES (2, 0, "NO0", "COURSE NO0", 5.90, 5);
INSERT INTO courses (ID, study_semesters_ID, course_code, course_name, ects_credits, old_credits) VALUES (3, 2, "NO1", "COURSE NO1", 7.20, 5);
INSERT INTO declarations (ID, courses_ID, semesters_ID, student_code, student_name, remarks) VALUES (0, 0, 1, "SC0", "John Doe 01", "");
INSERT INTO declarations (ID, courses_ID, semesters_ID, student_code, student_name, remarks) VALUES (1, 1, 2, "SC1", "John Doe 12", "");
INSERT INTO declarations (ID, courses_ID, semesters_ID, student_code, student_name, remarks) VALUES (2, 2, 0, "SC2", "John Doe 20", "");
INSERT INTO declarations (ID, courses_ID, semesters_ID, student_code, student_name, remarks) VALUES (3, 1, 1, "SC3", "John Doe 11", "");
INSERT INTO declarations (ID, courses_ID, semesters_ID, student_code, student_name, remarks) VALUES (4, 3, 1, "SC4", "John Doe 31", "");
INSERT INTO declarations (ID, courses_ID, semesters_ID, student_code, student_name, remarks) VALUES (5, 0, 2, "SC5", "John Doe 02", "");
```
