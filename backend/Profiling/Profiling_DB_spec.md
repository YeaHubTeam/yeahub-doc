# Profilling module tables

| Author  | Knyaginin Dmitry |
| ------- | ---------------- |
| Version | 0.0.3            |



### 1. Table “profiles”

For specify user concrete type. Now by “profile_type” column (see comment)

##### Table “profiles” columns

| **Name**          | **Type** | **Default** | **required** | **Comment**                                                        |
| ----------------- | -------- | ----------- | ------------ | -------------------------------------------------------------------|
| id                | uuid     |             | +            | PK                                                                 |
| user_id           | uuid     |             | +            | FK                                                                 |
| profile_type      | int4     | 1           | +            | 1 – candidate, 2 – member,   3 - HR                                |
| specialization_id | int4     |             | +            | FK for specializations.id                                 |
| marking_weight    | int4     | 1           |              | For candidate only: weight in rating_points “like” from this  user |

##### Table “profiles” indexes

| **Name**      | **Columns**           | **Unique?** |
| ------------- | --------------------- | ----------- |
| profiles_ind0 | user_id, profile_type | +           |

##### Table “profiles” constraints

| **Name**     | **Columns**                | **Type** |
| ------------ | -------------------------- | -------- |
| profiles_pk1 | id                         | PK       |
| profiles_uk1 | user_id, specialization_id | UK       |
| profiles_fk1 | user_id                    | FK       |
| profiles_fk2 | specialization_id          | FK       |


### 2. Table “profile_rate”

For separate rating process  for every profile. 

##### Table “profile_rate” columns

| **Name**           | **Type** | **Default** | **required** | **Comment**       |
| ------------------ | -------- | ----------- | ------------ | ----------------- |
| id                 | uuid     |             | +            | PK                |
| profile_id         | uuid     |             | +            | FK                |
| rating_points      | int8     | 0           | +            | 0 – for candidate |
| achievements_count | int8     | 0           |              | Only for caching! |

##### Table “profile_rate” indexes

| **Name**          | **Columns**   | **Unique?** |
| ----------------- | ------------- | ----------- |
| profile_rate_ind0 | rating_points |             |

##### Table “profile_rate” constraints

| **Name**         | **Columns** | **Type** |
| ---------------- | ----------- | -------- |
| profile_rate_pk1 | id          | PK       |
| profile_rate_uk1 | profile_id  | UK       |


### 3. Table “profile_skills”

For profile skills mapping

##### Table “profile_skills” columns

| **Name**   | **Type** | **Default** | **required** | **Comment** |
| ---------- | -------- | ----------- | ------------ | ----------- |
| profile_id | uuid     |             | +            | FK          |
| skill_id   | int8     |             | +            | FK          |

##### Table “profile_skills” indexes

| **Name** | **Columns** | **Unique?** |
| -------- | ----------- | ----------- |
|          |             |             |

##### Table “profile_skills” constraints

| **Name**           | **Columns**          | **Type** |
| ------------------ | -------------------- | -------- |
| profile_skills_pk1 | profile_id, skill_id | PK       |


### 4. Table “profile_achievements”

Hold profile achievement

##### Table “profile_achievements” columns

| **Name**       | **Type** | **Default**  | **required** | **Comment** |
| -------------- | -------- | ------------ | ------------ | ----------- |
| profile_id     | uuid     |              | +            | FK          |
| achievement_id | int8     |              | +            | FK          |
| getting_at     | Date     | current_date | +            |             |

##### Table “profile_achievements” indexes

| **Name**                  | **Columns** | **Unique?** |
| ------------------------- | ----------- | ----------- |
| profile_achievements_ind0 | getting_at  |             |

##### Table “profile_achievements” constraints

| **Name**                 | **Columns**                | **Type** |
| ------------------------ | -------------------------- | -------- |
| profile_achievements_pk1 | profile_id, achievement_id | PK       |


### 5. Table “profile_rates”

Hold profile to profile marking events

##### Table “profile_rates” columns

| **Name**       | **Type** | **Default**  | **required** | **Comment** |
| -------------- | -------- | ------------ | ------------ | ----------- |
| profile_id     | uuid     |              | +            | FK          |
| user_marked_id | uuid     |              | +            | FK          |
| mark           | int8     |              | +            |             |
| getting_at     | Date     | current_date | +            |             |

##### Table “profile_rates” indexes

| **Name**                  | **Columns** | **Unique?** |
| ------------------------- | ----------- | ----------- |
| profile_rates_ind0        | getting_at  |             |

##### Table “profile_rate” constraints

| **Name**         | **Columns**                | **Type** |
| ---------------- | -------------------------- | -------- |
| profile_rate_pk1 | profile_id, achievement_id | PK       |


### 6. Table “specialization_skills”

Skills to specializations relation table

##### Table “specialization_skills” columns

| **Name**          | **Type** | **Default**  | **required** | **Comment** |
| --------------    | -------- | ------------ | ------------ | ----------- |
| specialization_id | int8     |              | +            | FK          |
| skill_id          | int8     |              | +            | FK          |
| added_at          | Date     | current_date | +            |             |

##### Table “specialization_skills” indexes

| **Name**                      | **Columns** | **Unique?** |
| ----------------------------- | ----------- | ----------- |
| specialization_skills_ind0    | added_at    |             |

##### Table “specialization_skills” constraints

| **Name**                     | **Columns**                 | **Type** |
| ---------------------------- | --------------------------- | -------- |
| specialization_skills_pk1    | specialization_id, skill_id | PK       |


### 7. Table “jobs”

Resume jobs

##### Table “jobs” columns

| **Name**          | **Type**    | **Default** | **required** | **Comment**                                                        |
| --------------    | ----------- | ----------- | ------------ | -------------------------------------------------------------------|
| id                | uuid        |             | +            | PK                                                                 |
| profile_id        | uuid        |             | +            | FK                                                                 |
| title             | varchar(250)|             |              |                                                                    |
| information       | text        |             |              |                                                                    |
| start_date        | Date        |             | +            | start working date                                                 |
| end_date          | Date        |             |              | end date (optional)                                                |


##### Table “jobs” indexes

| **Name**      | **Columns**            | **Unique?** |
| ------------- | ---------------------- | ----------- |
| jobs_ind0     | profile_id             |             |

##### Table “jobs” constraints

| **Name**     | **Columns**           | **Type** |
| ------------ | --------------------- | -------- |
| jobs_pk1     | id                    | PK       |
| jobs_fk1     | profile_id            | FK       |


### 8. Table “educations”

Profile educations

##### Table “educations” columns

| **Name**          | **Type**    | **Default** | **required** | **Comment**                                                        |
| --------------    | ----------- | ----------- | ------------ | -------------------------------------------------------------------|
| id                | uuid        |             | +            | PK                                                                 |
| profile_id        | uuid        |             | +            | FK                                                                 |
| title             | varchar(250)|             |              |                                                                    |
| information       | text        |             |              |                                                                    |
| start_date        | Date        |             | +            | start working date                                                 |
| end_date          | Date        |             |              | end date (optional)                                                |


##### Table “educations” indexes

| **Name**         | **Columns**            | **Unique?** |
| ---------------- | ---------------------- | ----------- |
| educations_ind0  | profile_id             |             |

##### Table “educations” constraints

| **Name**        | **Columns**           | **Type** |
| --------------- | --------------------- | -------- |
| educations_pk1  | id                    | PK       |
| educations_fk1  | profile_id            | FK       |


### 9. Table “projects”

Resume projects

##### Table “projects” columns

| **Name**          | **Type**    | **Default** | **required** | **Comment**                                                        |
| --------------    | ----------- | ----------- | ------------ | -------------------------------------------------------------------|
| id                | uuid        |             | +            | PK                                                                 |
| profile_id        | uuid        |             | +            | FK                                                                 |
| title             | varchar(250)|             |              |                                                                    |
| information       | text        |             |              |                                                                    |
| url               | text        |             |              | remote project url                                                 |
| file              | bytea       |             |              | project file content (bytes)                                       |
| imageSrc          | text        |             |              | preview image for project (optional)                              |

##### Table “projects” indexes

| **Name**         | **Columns**            | **Unique?** |
| ---------------- | ---------------------- | ----------- |
| projects_ind0    | profile_id             |             |

##### Table “projects” constraints

| **Name**        | **Columns**           | **Type** |
| --------------- | --------------------- | -------- |
| projects_pk1    | id                    | PK       |
| projects_fk1    | profile_id            | FK       |


## Dictionaries spec

### 1. Dictionary table “skills”

Table for readonly for users!!

##### Table “skills” columns

| **Name**    | **Type**     | **Default**  | **required** | **Comment** |
| ----------- | ------------ | ------------ | ------------ | ----------- |
| id          | int8         |              | +            | PK          |
| title       | varchar(255) |              | +            |             |
| description | text         |              | +            |             |
| imageSrc    | varchar(255) |              |              |             |
| created_at  | Date         | current_date | +            |             |
| updated_at  | Date         |              |              |             |

##### Table “skills” indexes

| **Name**    | **Columns** | **Unique?** |
| ----------- | ----------- | ----------- |
| skills_ind0 | title       | +           |

##### Table “skills” constraints

| **Name**   | **Columns** | **Type** |
| ---------- | ----------- | -------- |
| skills_pk0 | id          | PK       |


### 2. Dictionary table “achievements”

Table for readonly for users!!

##### Table “achievements” columns

| **Name**    | **Type**     | **Default**  | **required** | **Comment** |
| ----------- | ------------ | ------------ | ------------ | ----------- |
| id          | int8         |              | +            | PK          |
| title       | varchar(255) |              | +            |             |
| description | text         |              | +            |             |
| imageSrc    | varchar(255) |              |              |             |
| created_at  | Date         | current_date | +            |             |
| updated_at  | Date         |              |              |             |

##### Table “achievements” indexes

| **Name**          | **Columns** | **Unique?** |
| ----------------- | ----------- | ----------- |
| achievements_ind0 | title       | +           |

##### Table “achievements” constraints

| **Name**         | **Columns** | **Type** |
| ---------------- | ----------- | -------- |
| achievements_pk0 | id          | PK       |


## Dictionaries content

### 1. Skills

| **id** | **title** | **decriprion** |
| ------ | --------- | -------------- |
|        |           |                |

Content of this dictionary stored as ./csv/skills.csv

### 2. Achievements

| **id** | **title** | **decriprion** |
| ------ | --------- | -------------- |
|        |           |                |

Content of this dictionary stored as ./csv/achievements.csv


## Changes

| **Date**   | **Author**       | **Description**                                         |
| ---------- | ---------------- | ------------------------------------------------------- |
| 06.03.2024 | Knyaginin Dmitry | YH-46. Create Profiling module DB specification         |
| 08.03.2024 | Knyaginin Dmitry | YH-46. Add ratings and achievements to Profiling module |
| 01.04.2024 | Knyaginin Dmitry | YH-46. Add jobs, educations e.t.c to Profiling module   |
|            |                  |                                                         |
|            |                  |                                                         |
|            |                  |                                                         |
|            |                  |                                                         |
|            |                  |                                                         |
|            |                  |                                                         |

