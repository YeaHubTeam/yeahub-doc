# Interview preparation module tables

| Author  | Knyaginin Dmitry |
| ------- | ---------------- |
| Version | 0.0.1            |



### 1. Table “inpr_profile_questions”

##### Table “inpr_profile_questions” columns

| **Name**     | **Type**      | **Default**  | **required** | **Comment** |
| ------------ | ------------- | ------------ | ------------ | ----------- |
| profile_id   | uuid          |              | +            | PK          |
| question_id  | uuid          |              | +            | PK          |
| checks_count | int4          | 1            |              |             |
| is_learned   | boolean       | false        |              |             |


##### Table “inpr_profile_questions” indexes

| **Name**                    | **Columns**                 | **Unique?** |
| --------------------------- | --------------------------- | ----------- |
|                             |                             |             |

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



### 3. Table “inpr_profile_progress”

This table caches count of fully learned questions for decrease DB load

##### Table “inpr_profile_progress” columns

| **Name**           | **Type**      | **Default**  | **required** | **Comment** |
| ------------------ | ------------- | ------------ | ------------ | ----------- |
| profile_id         | uuid          |              | +            | PK          |
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



## Dictionaries spec


## Dictionaries content


## Changes

| **Date**   | **Author**       | **Description**                                                      |
| ---------- | ---------------- | -------------------------------------------------------------------- |
| 27.04.2024 | Knyaginin Dmitry | YH-46. Create Interview preparation module DB specification          |
|            |                  |                                                                      |
|            |                  |                                                                      |
|            |                  |                                                                      |
|            |                  |                                                                      |
|            |                  |                                                                      |
