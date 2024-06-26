# Users module tables

| Author  | Knyaginin Dmitry |
| ------- | ---------------- |
| Version | 0.0.2            |


### 1. Table “users”

Table for common users information 

##### Table “users” columns

| **Name**      | **Type**     | **Default**      | **required** | **Comment**            |
| ------------- | ------------ | ---------------- | ------------ | ---------------------- |
| id            | uuid         |                  | +            | PK                     |
| first_name    | varchar(255) |                  | +            |                        |
| last_name     | varchar(255) |                  | +            |                        |
| password_hash | varchar(255) |                  | +            | May be should separate |
| phone         | varchar(50)  |                  | +            |                        |
| email         | varchar(255) |                  | +            |                        |
| links         | text         |'[]'              |              | JSON struct for front  |
| country       | varchar(255) |                  |              |                        |
| city          | varchar(255) |                  |              |                        |
| birthday      | Date         |                  |              |                        |
| address       | varchar(255) |                  |              | Is it needed?          |
| avatarurl     | varchar(255) | DefaultAvatarUrl | +            | Add default!           |
| refresh_token | varchar(255) |                  |              | May be should separate |
| profile       | Uuid         |                  | +            | FK                     |
| created_at    | Date         | current_date     | +            |                        |
| updated_at    | Date         |                  |              |                        |
| version       | int8         | 0                |              | Optional!              |

##### Table “users” indexes

| **Name**   | **Columns** | **Unique?** |
| ---------- | ----------- | ----------- |
| users_ind0 | phone       | +           |
| users_ind1 | email       | +           |
| users_ind2 | created_at  |             |

##### Table “users” constraints

| **Name**          | **Columns**                 | **Type**               |
| ----------------- | --------------------------- | ---------------------- |
| users_pk1         | id                          | PK                     |
| users_uk1         | email                       | UK                     |
| users_uk2         | phone                       | UK                     |
| users_profile_fk1 | profiles.id → users.profile | FK (Cascade on delete) |


### 2. Table “user_role”

Table for readonly for users!! Rows may be not exist for candidate! Default role - **candidate** 

##### Table “user_role” columns

| **Name**       | **Type** | **Default** | **required** | **Comment** |
| -------------- | -------- | ----------- | ------------ | ----------- |
| user_id        | uuid     |             | +            |             |
| user_role_id   | int4     |             | +            |             |
| setted_by      | uuid     |             | +            |             |

##### Table “user_role” constraints

| **Name**      | **Columns**            | **Type** |
| ------------- | ---------------------- | -------- |
| user_role_pk0 | role_id, permission_id | PK       |


## Dictionaries spec


### 1. Dictionary table “role”

Table for readonly for users!!

##### Table “role” columns

| **Name** | **Type**    | **Default** | **required** | **Comment** |
| -------- | ----------- | ----------- | ------------ | ----------- |
| id       | int4        |             | +            | PK          |
| name     | varchar(50) |             | +            |             |

##### Table “role” constraints

| **Name** | **Columns** | **Type** |
| -------- | ----------- | -------- |
| role_pk0 | id          | PK       |


### 2. Dictionary table “permission”

Table for readonly for users!!

##### Table “permission” columns

| **Name** | **Type**     | **Default** | **required** | **Comment** |
| -------- | ------------ | ----------- | ------------ | ----------- |
| id       | int4         |             | +            | PK          |
| name     | varchar(255) |             | +            |             |

##### Table “permission” constraints

| **Name**       | **Columns** | **Type** |
| -------------- | ----------- | -------- |
| permission_pk0 | id          | PK       |

### 3. Dictionary table “role_permission”

Table for readonly for users!!

##### Table “role” columns

| **Name**      | **Type** | **Default** | **required** | **Comment** |
| ------------- | -------- | ----------- | ------------ | ----------- |
| role_id       | int4     |             | +            | PK          |
| permission_id | int4     |             | +            | PK          |

##### Table “role” constraints

| **Name** | **Columns**            | **Type** |
| -------- | ---------------------- | -------- |
| role_pk0 | role_id, permission_id | PK       |


## 					Dictionaries content

### 1. Role

| **id** | **name**  |
| ------ | --------- |
| 1      | guest     |
| 2      | candidate |
| 3      | member    |
| 4      | admin     |
| 5      | HR        |
| 6      | client    |

### 2. Permission

| **id** | **name**                     |
| ------ | ---------------------------- |
|    1   | View members list/profile    |
|    2   | View candidates list/profile |
|    3   | Edit own profile             |
|    4   | Edit user profiles           |
|    5   | Add (edit own) vacancy       |
|    6   | View vacancies               |
|    7   | Edit user roles              |
|    8   | Edit user rate               |
|    9   | Add articles/blog            |
|   10   | Edit own articles/blog       |
|   11   | Edit user articles/blog      |
|   12   | Edit system dictionaries     |


### 3. Role_permission

| **role_id** | **permission_id (as list)**           |
| ----------- | ------------------------------------- |
| 1           | 1, 6                                  |
| 2           | 1, 2, 3, 6                            |
| 3           | 1, 2, 3, 6, 8, 9, 10                  |
| 4           | 1, 2, 3. 4, 5, 6, 7, 8, 9, 10, 11, 12 |
| 5           | 1, 5                                  |


## Changes

| **Date**   | **Author**       | **Description**                            |
| ---------- | ---------------- | ------------------------------------------ |
| 06.03.2024 | Knyaginin Dmitry | YH-46. Create User module DB specification |
| 01.04.2024 | Knyaginin Dmitry | YH-46. Add links field to Users table      |
|            |                  |                                            |
|            |                  |                                            |
|            |                  |                                            |
|            |                  |                                            |
|            |                  |                                            |
|            |                  |                                            |
|            |                  |                                            |
|            |                  |                                            |


 