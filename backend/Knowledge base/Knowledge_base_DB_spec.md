# Verification module tables

| Author  | Knyaginin Dmitry |
| ------- | ---------------- |
| Version | 0.0.1            |



### 1. Table “questions”

##### Table “questions” columns

| **Name**          | **Type**      | **Default**  | **required** | **Comment** |
| ----------------- | ------------- | ------------ | ------------ | ----------- |
| id                | uuid          |              | +            | PK          |
| title             | varchar(255)  |              | +            |             |
| description       | text          |              | +            |             |
| imageSrc          | varchar(255)  |              |              |             |
| longAnswer        | varchar(1000) |              |              |             |
| shortAnswer       | varchar(255)  |              |              |             |
| status            | varchar(50)   |              |              |             |
| created_at        | Date          | current_date | +            |             |
| updated_at        | Date          |              |              |             |
| created_by        | uuid          |              | +            | FK          |
| updated_by        | uuid          |              |              |             |
| keywords          | text          |              |              |             |


##### Table “questions” indexes

| **Name**       | **Columns**       | **Unique?** |
| -------------- | ----------------- | ----------- |
| questions_ind0 | created_at        |             |
| questions_ind1 | keywords          |             |
| questions_ind2 | created_by        |             |

##### Table “questions” constraints

| **Name**      | **Columns** | **Type** |
| ------------- | ----------- | -------- |
| questions_pk0 | Id          | PK       |
| questions_fk0 | created_by  | FK       |


### 2. Table “question_specializations”

##### Table “question_specializations” columns

| **Name**          | **Type**      | **Default**  | **required** | **Comment** |
| ----------------- | ------------- | ------------ | ------------ | ----------- |
| question_id       | uuid          |              | +            | PK          |
| specialization_id | int4          |              | +            | PK          |


##### Table “question_specializations” indexes

| **Name**                      | **Columns**       | **Unique?** |
| ----------------------------- | ----------------- | ----------- |
|                               |                   |             |

##### Table “question_specializations” constraints

| **Name**                     | **Columns**                     | **Type** |
| ---------------------------- | ------------------------------- | -------- |
| question_specializations_pk0 | question_id, specialization_id  | PK       |


### 3. Table “question_skills”

For relation to skills checked by question

##### Table “question_skills” columns

| **Name**    | **Type** | **Default** | **required** | **Comment** |
| ----------- | -------- | ----------- | ------------ | ----------- |
| question_id | uuid     |             | +            | FK          |
| skill_id    | int8     |             | +            | FK          |

##### Table “question_skills” indexes

| **Name** | **Columns** | **Unique?** |
| -------- | ----------- | ----------- |
|          |             |             |

##### Table “question_skills” constraints

| **Name**            | **Columns**           | **Type** |
| ------------------- | --------------------- | -------- |
| question_skills_pk1 | question_id, skill_id | PK       |


## Dictionaries spec


### 1. Dictionary table “Specializations”

Table for readonly for users!!

##### Table “specializations” columns

| **Name**    | **Type**     | **Default**  | **required** | **Comment** |
| ----------- | ------------ | ------------ | ------------ | ----------- |
| id          | int4         |              | +            | PK          |
| title       | varchar(255) |              | +            |             |
| description | text         |              | +            |             |
| imageSrc    | varchar(255) |              |              |             |
| created_at  | Date         | current_date | +            |             |
| updated_at  | Date         |              |              |             |

##### Table “specializations” indexes

| **Name**             | **Columns** | **Unique?** |
| -------------------- | ----------- | ----------- |
| specializations_ind0 | title       | +           |

##### Table “specializations” constraints

| **Name**            | **Columns** | **Type** |
| ------------------- | ----------- | -------- |
| specializations_pk0 | id          | PK       |


## Dictionaries content

### 1. Specializations

| **id** | **title** | **decriprion** |
| ------ | --------- | -------------- |
|        |           |                |

Content of this dictionary stored as ./csv/specializations.csv


## Changes

| **Date**   | **Author**       | **Description**                                                      |
| ---------- | ---------------- | -------------------------------------------------------------------- |
| 07.05.2024 | Knyaginin Dmitry | YH-46. Separate module Knowledge base added                          |
|            |                  |                                                                      |
|            |                  |                                                                      |
|            |                  |                                                                      |
|            |                  |                                                                      |
|            |                  |                                                                      |
