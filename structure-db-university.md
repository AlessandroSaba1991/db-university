# DB University

## Departments

- id:                           BIGINT          PK NOTNULL UNIQUE INDEX AUTOINCREMENTAL
- name:                         VARCHAR(50)     NOTNULL

## Graduation_Courses

- id:                           BIGINT          PK NOTNULL UNIQUE INDEX AUTOINCREMENTAL
- name:                         VARCHAR(50)     NOTNULL 
- duration:                     DATETIME        NOTNULL
- ?department_id?
- ?student_id?

## Courses

- id:                           BIGINT          PK NOTNULL UNIQUE INDEX AUTOINCREMENTAL
- name:                         VARCHAR(50)     NOTNULL 
- seats:                        SMALLINT        NOTNULL  
- start_date:                   DATETIME        NOTNULL
- end_date:                     DATETIME        NOTNULL
- ?graduation_course_id?

## COURSE_TEACHER

- course_id:
- teacher_id:

## Teachers

- id:                           BIGINT          PK NOTNULL UNIQUE INDEX AUTOINCREMENTAL
- name:                         VARCHAR(50)     NOTNULL 
- lastname:                     VARCHAR(50)     NOTNULL  
- email:                        VARCHAR(50)     NOTNULL UNIQUE
- tel_nr:                       VARCHAR(15)     NULL
- address:                      VARCHAR(50)     NOTNULL

## EXAM_SESSION_STUDENT

- exam_session_id:
- student_id:
- vote:                         TINYINT         NULL  

## Exam_sessions

- id:                           BIGINT          PK NOTNULL UNIQUE INDEX AUTOINCREMENTAL
- name:                         VARCHAR(50)     NOTNULL 
- date:                         DATETIME        NOTNULL
- ?course_id?

## Students

- id:                           BIGINT          PK NOTNULL UNIQUE INDEX AUTOINCREMENTAL
- name:                         VARCHAR(50)     NOTNULL  
- lastname:                     VARCHAR(50)     NOTNULL 
- age:                          TINYINT         NULL  
- email:                        VARCHAR(50)     NOTNULL UNIQUE
- tel_nr:                       VARCHAR(15)     NULL
- address:                      VARCHAR(50)     NOTNULL