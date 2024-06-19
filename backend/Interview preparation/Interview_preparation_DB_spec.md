# Interview preparation module tables

| Author  | Knyaginin Dmitry |
| ------- | ---------------- |
| Version | 0.0.2            |



### 1. Table “inpr_profile_questions”

##### Table “inpr_profile_questions” columns

| **Name**     | **Type**      | **Default**  | **required** | **Comment** |
| ------------ | ------------- | ------------ | ------------ | ----------- |
| profile_id   | uuid          |              | +            | PK          |
| question_id  | uuid          |              | +            | PK          |
| checks_count | int4          | 1            |              |             |
| is_learned   | boolean       | false        |              |             |
| last_update  | date          | current_date |              |             |


##### Table “inpr_profile_questions” indexes

| **Name**                    | **Columns**                 | **Unique?** |
| --------------------------- | --------------------------- | ----------- |
| inpr_profile_questions_ind0 | last_update                 |             |

##### Table “inpr_profile_questions” constraints

| **Name**                   | **Columns**                  | **Type** |
| -------------------------- | ---------------------------- | -------- |
| inpr_profile_questions_pk0 | profile_id, question_id      | PK       |
| inpr_profile_questions_fk0 | profile_id (profiles.id)     | FK       |
| inpr_profile_questions_fk1 | question_id (questuins.id)   | FK       |


### 2. Table “inpr_profile_progress”

This table caches count of fully learned questions for decrease DB load

##### Table “inpr_profile_progress” columns

| **Name**           | **Type**      | **Default**  | **required** | **Comment** |
| ------------------ | ------------- | ------------ | ------------ | ----------- |
| profile_id         | uuid          |              | +            | PK          |
| specialization_id  | int4          |              |              |             |   
| learned_count      | int4          |              |              |             |   


##### Table “inpr_profile_progress” indexes

| **Name**                    | **Columns**                 | **Unique?** |
| --------------------------- | --------------------------- | ----------- |
|                             |                             |             |

##### Table “inpr_profile_progress” constraints

| **Name**                   | **Columns**                  | **Type** |
| -------------------------- | ---------------------------- | -------- |
| inpr_profile_progress_pk0  | profile_id                   | PK       |
| inpr_profile_progress_fk0  | profile_id (profiles.id)     | FK       |



### 3. Table “inpr_questions_count” 

This table caches count of questions for specializations for decrease DB load

##### Table “inpr_questions_count”  columns

| **Name**           | **Type**      | **Default**  | **required** | **Comment** |
| ------------------ | ------------- | ------------ | ------------ | ----------- |
| specialization_id  | int4          |              | +            | PK          |
| questions_count    | int4          |              |              |             |


##### Table “inpr_questions_count”  indexes

| **Name**                    | **Columns**                 | **Unique?** |
| --------------------------- | --------------------------- | ----------- |
|                             |                             |             |

##### Table “inpr_questions_count”  constraints

| **Name**                   | **Columns**                  | **Type** |
| -------------------------- | ---------------------------- | -------- |
| inpr_questions_count_pk0   | specialization_id            | PK       |


### 4. Table “inpr_profile_quizzes”  

##### Table “inpr_profile_quizzes” columns

| **Name**       | **Type**      | **Default**  | **required** | **Comment** |
| -------------- | ------------- | ------------ | ------------ | ----------- |
| id             | uuid          |              | +            | PK          |
| profile_id     | uuid          |              | +            | FK          |
| start_date     | timestamp     | current_date | +            |             |
| end_date       | timestamp     |              |              |             |
| full_count     | int4          |              |              |             |
| success_count  | int4          |              |              |             |
| skills         | text[]        |              |              |             |
| response       | text          |              |              | JSON        |


##### Table “inpr_profile_quizzes” indexes

| **Name**                    | **Columns**                 | **Unique?** |
| --------------------------- | --------------------------- | ----------- |
| inpr_profile_quizzes_ind0   | start_date                  |             |

##### Table “inpr_profile_quizzes” constraints

| **Name**                   | **Columns**                  | **Type** |
| -------------------------- | ---------------------------- | -------- |
| inpr_profile_quizzes_pk0   | id                           | PK       |
| inpr_profile_quizzes_fk0   | profile_id (profiles.id)     | FK       |


## Dictionaries spec


## Dictionaries content


## Changes

| **Date**   | **Author**       | **Description**                                                      |
| ---------- | ---------------- | -------------------------------------------------------------------- |
| 27.04.2024 | Knyaginin Dmitry | YH-46. Create Interview preparation module DB specification          |
| 09.05.2024 | Knyaginin Dmitry | YH-46. Add table “inpr_profile_quizzes”                              |
|            |                  |                                                                      |
|            |                  |                                                                      |
|            |                  |                                                                      |
|            |                  |                                                                      |
|            |                  |                                                                      |
