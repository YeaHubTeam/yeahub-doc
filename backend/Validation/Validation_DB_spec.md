# Validation module tables

| Author  | Knyaginin Dmitry |
| ------- | ---------------- |
| Version | 0.0.1            |



### 1. Table “questions”

##### Table “questions” columns

| **Name**    | **Type**      | **Default**  | **required** | **Comment** |
| ----------- | ------------- | ------------ | ------------ | ----------- |
| id          | uuid          |              | +            | PK          |
| title       | varchar(255)  |              | +            |             |
| description | text          |              | +            |             |
| imageSrc    | varchar(255)  |              |              |             |
| longAnswer  | varchar(1000) |              |              |             |
| shortAnswer | varchar(255)  |              |              |             |
| status      | varchar(50)   |              |              |             |
| created_at  | Date          | current_date | +            |             |
| updated_at  | Date          |              |              |             |
| created_by  | uuid          |              | +            | FK          |
| updated_by  | uuid          |              |              |             |
| keywords    | text          |              |              |             |


##### Table “questions” indexes

| **Name**       | **Columns** | **Unique?** |
| -------------- | ----------- | ----------- |
| questions_ind0 | created_at  |             |
| questions_ind1 | keywords    |             |
| questions_ind2 | created_by  |             |

##### Table “questions” constraints

| **Name**      | **Columns** | **Type** |
| ------------- | ----------- | -------- |
| questions_pk0 | Id          | PK       |
| questions_fk0 | created_by  | FK       |

### 2. Table “tests”

##### Table “tests” columns

| **Name**          | **Type**     | **Default**  | **required** | **Comment**           |
| ----------------- | ------------ | ------------ | ------------ | --------------------- |
| id                | uuid         |              | +            | PK                    |
| title             | varchar(255) |              | +            |                       |
| description       | text         |              | +            |                       |
| minutes_to_pass   | int8         | 20           |              | Max time to pass test |
| type              | varchar(50)  | SELF_CHECK   |              | (1)                   |
| imageSrc          | varchar(255) |              |              |                       |
| created_at        | Date         | current_date | +            |                       |
| updated_at        | Date         |              |              |                       |
| created_by        | uuid         |              | +            | FK                    |
| updated_by        | uuid         |              |              |                       |
| keywords          | text         |              |              |                       |
| rate              | int8         |              |              |                       |
| complexity        | int4         | 5            |              |1 to 10 points         |
| specialization_id | int4         |              | +            |                       |
| approved_skill_id | int8         |              |              |for skill testing      |

- (1) - "type" column has next values "SELF_CHECK", "ONLINE_VALIDATION_CHECKLIST", "SKILL_TEST" may be Enum

##### Table “tests” indexes

| **Name**   | **Columns** | **Unique?** |
| ---------- | ----------- | ----------- |
| tests_ind0 | created_at  |             |
| tests_ind1 | keywords    |             |
| tests_ind2 | created_by  |             |
| tests_ind3 | comlexity   |             |

##### Table “tests” constraints

| **Name**  | **Columns** | **Type** |
| --------- | ----------- | -------- |
| tests_pk0 | id          | PK       |
| tests_fk0 | created_by  | FK       |


### 3. Table “tests_questions”

##### Table “tests_questions” columns

| **Name**    | **Type** | **Default**  | **required** | **Comment** |
| ----------- | -------- | ------------ | ------------ | ----------- |
| test_id     | uuid     |              | +            | PK          |
| question_id | uuid     |              | +            | PK          |
| created_at  | Date     | current_date | +            |             |

##### Table “tests_questions” indexes

| **Name**             | **Columns** | **Unique?** |
| -------------------- | ----------- | ----------- |
| tests_questions_ind0 | created_at  |             |

##### Table “tests_questions” constraints

| **Name**            | **Columns**          | **Type** |
| ------------------- | -------------------- | -------- |
| tests_questions_pk0 | test_id, question_id | PK       |


### 4. Table “tests_pass_attempts”

##### Table “tests_pass_attempts” columns

| **Name**          | **Type** | **Default**  | **required** | **Comment** |
| ----------------- | -------- | ------------ | ------------ | ----------- |
| test_id           | uuid     |              | +            | PK          |
| user_id           | uuid     |              | +            | PK          |
| begin_at          | Date     | current_date | +            |             |
| end_at            | Date     |              | +            |             |
| correct_ans_count | int4     |              |              |             |

##### Table “tests_pass_attempts” indexes

| **Name**                 | **Columns** | **Unique?** |
| ------------------------ | ----------- | ----------- |
| tests_pass_attempts_ind0 | begin_at    |             |

##### Table “tests_pass_attempts” constraints

| **Name**                | **Columns**      | **Type** |
| ----------------------- | ---------------- | -------- |
| tests_pass_attempts_pk0 | test_id, user_id | PK       |


### 5. Table “validation_online_session_requests”

##### Table “validation_online_session_requests” columns

| **Name**          | **Type** | **Default**  | **required** | **Comment** |
| ----------------- | -------- | ------------ | ------------ | ----------- |
| id                | uuid     |              | +            | PK          |
| user_id           | uuid     |              | +            | FK          |
| state_id          | int4     | 10 (CREATED) | +            |             |
| specialization_id | int4     |              | +            | FK          |
| session_type      | int4     |              | +            | FK          |
| user_message      | text     |              |              |             |
| created_at        | Date     | current_date | +            |             |
| updated_at        | Date     |              |              |             |

##### Table “validation_online_session_requests” indexes

| **Name**                                | **Columns**       | **Unique?** |
| --------------------------------------- | ----------------- | ----------- |
| validation_online_session_requests_ind0 | created_at        |             |
| validation_online_session_requests_ind0 | specialization_id |             |

##### Table “validation_online_session_requests” constraints

| **Name**                               | **Columns**                                        | **Type** |
| -------------------------------------- | -------------------------------------------------- | -------- |
| validation_online_session_requests_pk0 | id                                                 | PK       |
| validation_online_session_requests_fk0 | user_id                                            | FK       |
| validation_online_session_requests_fk1 | validation_online_request_states.specialization_id | FK       |


### 6. Table “validation_online_session_attempts”

##### Table “validation_online_session_attempts” columns

| **Name**         | **Type** | **Default** | **required** | **Comment** |
| ---------------- | -------- | ----------- | ------------ | ----------- |
| id               | uuid     |             | +            | PK          |
| validation_reqid | uuid     |             | +            | FK          |
| plan_date        | Date     |             | +            |             |
| begin_at         | Date     |             |              |             |
| end_at           | Date     |             |              |             |
| isSuccess        | boolean  |             |              |             |
| feedback         | text     |             |              |             |

##### Table “validation_online_session_attempts” indexes

| **Name**                                | **Columns** | **Unique?** |
| --------------------------------------- | ----------- | ----------- |
| validation_online_session_attempts_ind0 | plan_date   |             |

##### Table “validation_online_session_attempts” constraints

| **Name**                               | **Columns**      | **Type** |
| -------------------------------------- | ---------------- | -------- |
| validation_online_session_attempts_pk0 | id               | PK       |
| validation_online_session_attempts_fk0 | validation_reqid | FK       |


### 7. Table “validation_offline_tasks”

##### Table “validation_offline_tasks” columns

| **Name**          | **Type**     | **Default**  | **required** | **Comment** |
| ----------------- | ------------ | ------------ | ------------ | ----------- |
| id                | uuid         |              | +            | PK          |
| title             | varchar(255) |              | +            |             |
| description       | text         |              | +            |             |
| criteria          | text         |              | +            |             |
| duration          | varchar(50)  |              |              |             |
| recomendation     | text         |              |              |             |
| imageSrc          | text         |              |              |             |
| url               | text         |              |              |             |
| file              | bytea        |              |              |             |
| rate              | int4         | 10           | +            |             |
| specialization_id | int4         |              | +            | FK          |
| created_by        | uuid         |              | +            | FK          |
| updated_by        | uuid         |              |              |             |
| created_at        | Date         | current_date | +            |             |
| updated_at        | Date         |              |              |             |

##### Table “validation_offline_tasks” indexes

| **Name**                      | **Columns**       | **Unique?** |
| ----------------------------- | -----------       | ----------- |
| validation_offline_tasks_ind0 | rate              |             |
| validation_offline_tasks_ind1 | created_at        |             |
| validation_offline_tasks_ind2 | specialization_id |             |

##### Table “validation_offline_tasks” constraints

| **Name**                     | **Columns**       | **Type** |
| ---------------------------- | ----------------- | -------- |
| validation_offline_tasks_pk0 | id                | PK       |
| validation_offline_tasks_fk0 | created_by        | FK       |
| validation_offline_tasks_fk1 | specialization_id | FK       |


### 8. Table “validation_offline_task_executions”

##### Table “validation_offline_task_executions” columns

| **Name**         | **Type** | **Default** | **required** | **Comment** |
| ---------------- | -------- | ----------- | ------------ | ----------- |
| id               | uuid     |             | +            | PK          |
| task_id          | uuid     |             | +            | FK          |
| executor_id      | uuid     |             | +            | FK          |
| begin_at         | Date     |             |              |             |
| end_at           | Date     |             |              |             |
| isSuccess        | boolean  |             |              |             |
| review_rate      | int4     |             |              | 0...100     |
| feedback         | text     |             |              |             |

##### Table “validation_offline_task_executions” indexes

| **Name**                                | **Columns** | **Unique?** |
| --------------------------------------- | ----------- | ----------- |
|                                         |             |             |

##### Table “validation_offline_task_executions” constraints

| **Name**                               | **Columns**      | **Type** |
| -------------------------------------- | ---------------- | -------- |
| validation_offline_task_executions_pk0 | id               | PK       |
| validation_offline_task_executions_fk0 | task_id          | FK       |
| validation_offline_task_executions_fk0 | executor_id      | FK       |


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

### 2. Dictionary table “validation_online_request_states”

Table for readonly for users!!

##### Table “validation_online_request_states” columns

| **Name** | **Type**     | **Default** | **required** | **Comment** |
| -------- | ------------ | ----------- | ------------ | ----------- |
| id       | int4         |             | +            | PK          |
| title    | varchar(255) |             | +            |             |
| code     | varchar(50)  |             | +            |             |

##### Table “validation_online_request_states” indexes

| **Name** | **Columns** | **Unique?** |
| -------- | ----------- | ----------- |
|          |             |             |

##### Table “validation_online_request_states” constraints

| **Name**                             | **Columns** | **Type** |
| ------------------------------------ | ----------- | -------- |
| validation_online_request_states_pk0 | id          | PK       |

### 3. Dictionary table “validation_online_session_types”

Table for readonly for users!!

##### Table “validation_online_session_types” columns

| **Name** | **Type**     | **Default** | **required** | **Comment** |
| -------- | ------------ | ----------- | ------------ | ----------- |
| id       | int4         |             | +            | PK          |
| title    | varchar(255) |             | +            |             |
| code     | varchar(50)  |             | +            |             |

##### Table “validation_online_session_types” indexes

| **Name** | **Columns** | **Unique?** |
| -------- | ----------- | ----------- |
|          |             |             |

##### Table “validation_online_session_types” constraints

| **Name**                             | **Columns** | **Type** |
| ------------------------------------ | ----------- | -------- |
| validation_online_session_types_pk0  | id          | PK       |

## Dictionaries content

### 1. Specializations

| **id** | **title** | **decriprion** |
| ------ | --------- | -------------- |
|        |           |                |

Content of this dictionary stored as ./csv/specializations.csv

### 2. validation_online_request_states

| **id** | **title** | **code** |
| ------ | --------- | -------- |
|        |           |          |

Content of this dictionary stored as ./csv/validation_online_request_states.csv

### 3. validation_online_session_types

| **id** | **title** | **code** |
| ------ | --------- | -------- |
|        |           |          |

Content of this dictionary stored as ./csv/validation_online_session_types.csv

## Changes

| **Date**   | **Author**       | **Description**                                                    |
| ---------- | ---------------- | ------------------------------------------------------------------ |
| 11.03.2024 | Knyaginin Dmitry | YH-46. Create Validation module DB specification                   |
| 01.04.2024 | Knyaginin Dmitry | YH-46. Add offline tasks, testing details, online validation types |
|            |                  |                                                                    |
|            |                  |                                                                    |
|            |                  |                                                                    |
|            |                  |                                                                    |
|            |                  |                                                                    |
