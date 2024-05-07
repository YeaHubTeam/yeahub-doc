# Verification module tables

| Author  | Knyaginin Dmitry |
| ------- | ---------------- |
| Version | 0.0.3            |



### 1. Table “tests”

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

- (1) - "type" column has next values "SELF_CHECK", "ONLINE_Verification_CHECKLIST", "" may be Enum

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


### 2. Table “tests_questions”

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


### 3. Table “tests_pass_attempts”

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


### 4. Table “verification_online_session_requests”

##### Table “verification_online_session_requests” columns

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

##### Table “verification_online_session_requests” indexes

| **Name**                                  | **Columns**       | **Unique?** |
| ----------------------------------------- | ----------------- | ----------- |
| verification_online_session_requests_ind0 | created_at        |             |
| verification_online_session_requests_ind0 | specialization_id |             |

##### Table “verification_online_session_requests” constraints

| **Name**                                 | **Columns**                                          | **Type** |
| ---------------------------------------- | ---------------------------------------------------- | -------- |
| verification_online_session_requests_pk0 | id                                                   | PK       |
| verification_online_session_requests_fk0 | user_id                                              | FK       |
| verification_online_session_requests_fk1 | verification_online_request_states.specialization_id | FK       |


### 5. Table “verification_online_session_attempts”

Map attempts to slots by specialization_id of request and slot related profile

##### Table “verification_online_session_attempts” columns

| **Name**           | **Type** | **Default** | **required** | **Comment** |
| ------------------ | -------- | ----------- | ------------ | ----------- |
| id                 | uuid     |             | +            | PK          |
| verification_reqid | uuid     |             | +            | FK          |
| slot_id            | uuid     |             |              | FK          |
| isSuccess          | boolean  |             |              |             |
| feedback           | text     |             |              |             |

##### Table “verification_online_session_attempts” indexes

| **Name**                                  | **Columns** | **Unique?** |
| ----------------------------------------- | ----------- | ----------- |
| verification_online_session_attempts_ind0 | plan_date   |             |
| verification_online_session_attempts_ind1 | slot_id     |             |

##### Table “verification_online_session_attempts” constraints

| **Name**                                 | **Columns**        | **Type** |
| --------------------------------------   | ------------------ | -------- |
| verification_online_session_attempts_pk0 | id                 | PK       |
| verification_online_session_attempts_fk0 | verification_reqid | FK       |


### 6. Table “verification_offline_tasks”

##### Table “verification_offline_tasks” columns

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

##### Table “verification_offline_tasks” indexes

| **Name**                        | **Columns**       | **Unique?** |
| ------------------------------- | -----------       | ----------- |
| verification_offline_tasks_ind0 | rate              |             |
| verification_offline_tasks_ind1 | created_at        |             |
| verification_offline_tasks_ind2 | specialization_id |             |

##### Table “verification_offline_tasks” constraints

| **Name**                       | **Columns**       | **Type** |
| ------------------------------ | ----------------- | -------- |
| verification_offline_tasks_pk0 | id                | PK       |
| verification_offline_tasks_fk0 | created_by        | FK       |
| verification_offline_tasks_fk1 | specialization_id | FK       |


### 7. Table “verification_offline_task_executions”

##### Table “verification_offline_task_executions” columns

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

##### Table “verification_offline_task_executions” indexes

| **Name**                                | **Columns** | **Unique?** |
| --------------------------------------- | ----------- | ----------- |
|                                         |             |             |

##### Table “verification_offline_task_executions” constraints

| **Name**                                 | **Columns**      | **Type** |
| ---------------------------------------- | ---------------- | -------- |
| verification_offline_task_executions_pk0 | id               | PK       |
| verification_offline_task_executions_fk0 | task_id          | FK       |
| verification_offline_task_executions_fk0 | executor_id      | FK       |


### 8. Table “verification_online_session_slots”  

##### Table “verification_online_session_slots” columns

| **Name**           | **Type** | **Default** | **required** | **Comment** |
| ------------------ | -------- | ----------- | ------------ | ----------- |
| id                 | uuid     |             | +            | PK          |
| profile_id         | uuid     |             | +            | FK          |
| begin_at           | Date     |             |              |             |
| end_at             | Date     |             |              |             |
| busy               | Boolean  | false       |              |             |

##### Table “verification_online_session_slots” indexes

| **Name**                                  | **Columns** | **Unique?** |
| ----------------------------------------- | ----------- | ----------- |
| verification_online_session_slots_ind0    | plan_date   |             |

##### Table “verification_online_session_slots” constraints

| **Name**                                 | **Columns**        | **Type** |
| --------------------------------------   | ------------------ | -------- |
| verification_online_session_slots_pk0    | id                 | PK       |
| verification_online_session_slots_fk0    | profile_id         | FK       |


## Dictionaries spec


### 1. Dictionary table “verification_online_request_states”

Table for readonly for users!!

##### Table “verification_online_request_states” columns

| **Name** | **Type**     | **Default** | **required** | **Comment** |
| -------- | ------------ | ----------- | ------------ | ----------- |
| id       | int4         |             | +            | PK          |
| title    | varchar(255) |             | +            |             |
| code     | varchar(50)  |             | +            |             |

##### Table “verification_online_request_states” indexes

| **Name** | **Columns** | **Unique?** |
| -------- | ----------- | ----------- |
|          |             |             |

##### Table “verification_online_request_states” constraints

| **Name**                               | **Columns** | **Type** |
| -------------------------------------- | ----------- | -------- |
| verification_online_request_states_pk0 | id          | PK       |

### 2. Dictionary table “verification_online_session_types”

Table for readonly for users!!

##### Table “verification_online_session_types” columns

| **Name** | **Type**     | **Default** | **required** | **Comment** |
| -------- | ------------ | ----------- | ------------ | ----------- |
| id       | int4         |             | +            | PK          |
| title    | varchar(255) |             | +            |             |
| code     | varchar(50)  |             | +            |             |

##### Table “verification_online_session_types” indexes

| **Name** | **Columns** | **Unique?** |
| -------- | ----------- | ----------- |
|          |             |             |

##### Table “verification_online_session_types” constraints

| **Name**                               | **Columns** | **Type** |
| -------------------------------------- | ----------- | -------- |
| verification_online_session_types_pk0  | id          | PK       |

## Dictionaries content

### 1. verification_online_request_states

| **id** | **title** | **code** |
| ------ | --------- | -------- |
|        |           |          |

Content of this dictionary stored as ./csv/verification_online_request_states.csv

### 2. verification_online_session_types

| **id** | **title** | **code** |
| ------ | --------- | -------- |
|        |           |          |

Content of this dictionary stored as ./csv/verification_online_session_types.csv

## Changes

| **Date**   | **Author**       | **Description**                                                      |
| ---------- | ---------------- | -------------------------------------------------------------------- |
| 11.03.2024 | Knyaginin Dmitry | YH-46. Create Verification module DB specification                   |
| 01.04.2024 | Knyaginin Dmitry | YH-46. Add offline tasks, testing details, online verification types |
| 16.04.2024 | Knyaginin Dmitry | YH-46. Add slots for online verification attempts                    |
| 07.05.2024 | Knyaginin Dmitry | YH-46. Separate module Knowledge base added                          |
|            |                  |                                                                      |
|            |                  |                                                                      |
|            |                  |                                                                      |
|            |                  |                                                                      |
|            |                  |                                                                      |
