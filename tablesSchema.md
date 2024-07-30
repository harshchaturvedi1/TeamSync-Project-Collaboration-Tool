# TeamSync Database Schema Documentation

## Overview

The TeamSync project database schema is designed to support project management and team collaboration functionalities. It includes tables for users, projects, tasks, comments, interactions, and system logs. Each table is structured to efficiently handle the specific data and relationships required by the application.

## Tables and Schema

### **1. Users Table**

**Purpose**: Stores information about users of the system.

| Column          | Data Type                                                         | Description                               | Constraints               |
| --------------- | ----------------------------------------------------------------- | ----------------------------------------- | ------------------------- |
| `id`            | `INT AUTO_INCREMENT`                                              | Unique identifier for each user.          | `PRIMARY KEY`, `NOT NULL` |
| `name`          | `VARCHAR(255)`                                                    | Full name of the user.                    | `NOT NULL`                |
| `email`         | `VARCHAR(255) UNIQUE`                                             | Email address of the user.                | `NOT NULL`                |
| `password_hash` | `TEXT`                                                            | Hashed password for authentication.       | `NOT NULL`                |
| `role`          | `VARCHAR(50)`                                                     | Role of the user (e.g., Admin, Member).   | `NOT NULL`                |
| `created_at`    | `TIMESTAMP DEFAULT CURRENT_TIMESTAMP`                             | Timestamp when the user was created.      | `NOT NULL`                |
| `updated_at`    | `TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP` | Timestamp when the user was last updated. | `NOT NULL`                |

### **2. Projects Table**

**Purpose**: Manages project details and relationships.

| Column        | Data Type                                                         | Description                                  | Constraints                         |
| ------------- | ----------------------------------------------------------------- | -------------------------------------------- | ----------------------------------- |
| `id`          | `INT AUTO_INCREMENT`                                              | Unique identifier for each project.          | `PRIMARY KEY`, `NOT NULL`           |
| `name`        | `VARCHAR(255)`                                                    | Name of the project.                         | `NOT NULL`                          |
| `description` | `TEXT`                                                            | Detailed description of the project.         | `NULL` (optional)                   |
| `owner_id`    | `INT NULL`                                                        | Reference to the user who owns the project.  | Foreign Key referencing `users(id)` |
| `start_date`  | `DATE`                                                            | Start date of the project.                   | `NULL` (optional)                   |
| `end_date`    | `DATE`                                                            | End date of the project.                     | `NULL` (optional)                   |
| `created_at`  | `TIMESTAMP DEFAULT CURRENT_TIMESTAMP`                             | Timestamp when the project was created.      | `NOT NULL`                          |
| `updated_at`  | `TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP` | Timestamp when the project was last updated. | `NOT NULL`                          |

### **3. Project Members Table**

**Purpose**: Links users to projects and defines their membership.

| Column          | Data Type                               | Description                                  | Constraints                                        |
| --------------- | --------------------------------------- | -------------------------------------------- | -------------------------------------------------- |
| `project_id`    | `INT`                                   | Identifier for the project.                  | Foreign Key referencing `projects(id)`, `NOT NULL` |
| `user_id`       | `INT`                                   | Identifier for the user.                     | Foreign Key referencing `users(id)`, `NOT NULL`    |
| **PRIMARY KEY** | Composite Key (`project_id`, `user_id`) | Composite key for unique project-user pairs. |                                                    |

### **4. Tasks Table**

**Purpose**: Manages tasks within projects.

| Column        | Data Type                                                         | Description                                            | Constraints                                        |
| ------------- | ----------------------------------------------------------------- | ------------------------------------------------------ | -------------------------------------------------- |
| `id`          | `INT AUTO_INCREMENT`                                              | Unique identifier for each task.                       | `PRIMARY KEY`, `NOT NULL`                          |
| `project_id`  | `INT`                                                             | Reference to the project to which the task belongs.    | Foreign Key referencing `projects(id)`, `NOT NULL` |
| `name`        | `VARCHAR(255)`                                                    | Name of the task.                                      | `NOT NULL`                                         |
| `description` | `TEXT`                                                            | Detailed description of the task.                      | `NULL` (optional)                                  |
| `assigned_to` | `INT NULL`                                                        | Reference to the user assigned to the task.            | Foreign Key referencing `users(id)`                |
| `status`      | `VARCHAR(50)`                                                     | Current status of the task (e.g., Pending, Completed). | `NOT NULL`                                         |
| `priority`    | `VARCHAR(50)`                                                     | Priority level of the task (e.g., High, Medium, Low).  | `NOT NULL`                                         |
| `due_date`    | `DATE`                                                            | Due date for the task.                                 | `NULL` (optional)                                  |
| `created_at`  | `TIMESTAMP DEFAULT CURRENT_TIMESTAMP`                             | Timestamp when the task was created.                   | `NOT NULL`                                         |
| `updated_at`  | `TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP` | Timestamp when the task was last updated.              | `NOT NULL`                                         |

### **5. Task Comments Table**

**Purpose**: Stores comments made on tasks.

| Column       | Data Type                             | Description                                 | Constraints                                     |
| ------------ | ------------------------------------- | ------------------------------------------- | ----------------------------------------------- |
| `id`         | `INT AUTO_INCREMENT`                  | Unique identifier for each comment.         | `PRIMARY KEY`, `NOT NULL`                       |
| `task_id`    | `INT`                                 | Reference to the task being commented on.   | Foreign Key referencing `tasks(id)`, `NOT NULL` |
| `user_id`    | `INT`                                 | Reference to the user who made the comment. | Foreign Key referencing `users(id)`, `NOT NULL` |
| `comment`    | `TEXT`                                | Content of the comment.                     | `NOT NULL`                                      |
| `created_at` | `TIMESTAMP DEFAULT CURRENT_TIMESTAMP` | Timestamp when the comment was created.     | `NOT NULL`                                      |

### **6. User Interactions Table**

**Purpose**: Tracks actions performed by users.

| Column       | Data Type                             | Description                                     | Constraints                                     |
| ------------ | ------------------------------------- | ----------------------------------------------- | ----------------------------------------------- |
| `id`         | `INT AUTO_INCREMENT`                  | Unique identifier for each interaction.         | `PRIMARY KEY`, `NOT NULL`                       |
| `user_id`    | `INT`                                 | Reference to the user who performed the action. | Foreign Key referencing `users(id)`, `NOT NULL` |
| `action`     | `VARCHAR(255)`                        | Description of the action performed.            | `NOT NULL`                                      |
| `details`    | `TEXT`                                | Additional details about the interaction.       | `NULL` (optional)                               |
| `created_at` | `TIMESTAMP DEFAULT CURRENT_TIMESTAMP` | Timestamp when the interaction occurred.        | `NOT NULL`                                      |

### **7. System Logs Table**

**Purpose**: Stores system logs for auditing and debugging.

| Column       | Data Type                             | Description                                    | Constraints               |
| ------------ | ------------------------------------- | ---------------------------------------------- | ------------------------- |
| `id`         | `INT AUTO_INCREMENT`                  | Unique identifier for each log entry.          | `PRIMARY KEY`, `NOT NULL` |
| `level`      | `VARCHAR(50)`                         | Severity level of the log (e.g., INFO, ERROR). | `NOT NULL`                |
| `message`    | `TEXT`                                | Log message content.                           | `NOT NULL`                |
| `meta`       | `TEXT`                                | Additional metadata related to the log.        | `NULL` (optional)         |
| `created_at` | `TIMESTAMP DEFAULT CURRENT_TIMESTAMP` | Timestamp when the log entry was created.      | `NOT NULL`                |
