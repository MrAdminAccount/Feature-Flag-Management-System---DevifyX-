# Feature Flag Management System (SQL-Only)

This is a complete **Feature Flag Management System** implemented using **pure MySQL**, submitted as part of the DevifyX internship assignment. It is designed to manage the rollout of new features in a structured, controlled, and testable way—supporting user targeting, environments, flag dependencies, audits, soft deletes, and more.

---

## 📌 Project Objective

To design and implement a robust Feature Flag system **without any frontend/backend code**, using **only MySQL constructs** like:

* DDL (Data Definition Language)
* DML (Data Manipulation Language)
* Views
* Triggers
* Constraints
* Sample queries

---

## 🧠 Key Concepts

A **Feature Flag System** allows developers to:

* Toggle features **on/off** without deploying new code
* Control visibility based on **user, group, or environment**
* Gradually roll out new features
* Maintain **audit trails** and history
* Cleanly manage expired or dependent features

---

## 🧱 Database Design Overview

| Table                   | Purpose                                                               |
| ----------------------- | --------------------------------------------------------------------- |
| `feature_flags`         | Stores core flag metadata and status                                  |
| `users`                 | Represents end users                                                  |
| `groups`                | User groups (e.g., QA, DevOps)                                        |
| `user_group_membership` | Many-to-many relationship between users and groups                    |
| `environments`          | Lists available environments (e.g., development, production)          |
| `flag_assignments`      | Links flags to specific users/groups and handles percentage rollout   |
| `flag_dependencies`     | Manages dependency relationships between flags                        |
| `flag_audit_logs`       | Tracks changes (create, update, delete) with actor info and timestamp |
| `flag_history`          | Full state change history (bonus feature)                             |

---

## ✅ Features Implemented

### Core Features

* [x] Create/read/update/delete feature flags
* [x] Toggle flags per environment (e.g., dev, prod)
* [x] User- and group-based flag assignment
* [x] Flag expiry with timestamp
* [x] Dependency management between flags
* [x] Logging using triggers
* [x] Views for active flags

### Bonus Features

* [x] Percentage-based rollout
* [x] Categorization of flags
* [x] Soft deletes (no data loss)
* [x] Full history table with changes tracked

---

## 🧪 Sample Queries

### Active flags for a user in an environment:

```sql
SELECT ff.*
FROM feature_flags ff
JOIN environments e ON ff.environment_id = e.environment_id
JOIN flag_assignments fa ON ff.flag_id = fa.flag_id
LEFT JOIN user_group_membership ugm ON fa.group_id = ugm.group_id
WHERE e.name = 'development'
AND (fa.user_id = 1 OR ugm.user_id = 1)
AND ff.is_enabled = TRUE
AND (ff.expiry_date IS NULL OR ff.expiry_date > NOW())
AND ff.deleted = FALSE;
```

### View flag dependencies:

```sql
SELECT f1.name AS Flag, f2.name AS Depends_On
FROM flag_dependencies fd
JOIN feature_flags f1 ON fd.flag_id = f1.flag_id
JOIN feature_flags f2 ON fd.depends_on_flag_id = f2.flag_id;
```

### Insert and update operations with audit and history logging:

```sql
UPDATE feature_flags SET description = 'Improved UI rollout' WHERE flag_id = 1;
SELECT * FROM flag_audit_logs ORDER BY action_time DESC;
SELECT * FROM flag_history ORDER BY changed_at DESC;
```

---

## 🧰 How to Run Locally

1. **Install MySQL 8.0+**
2. Open MySQL CLI or MySQL Workbench
3. Run the full `feature_flag_system.sql` file provided in this repo
4. You’re ready to run the queries listed above or explore the data

✅ Alternatively, you can watch the attached screen recording (`demo.mp4`) to see a complete walk-through.

---

## 📹 Screen Recording

A screen-recorded demonstration of the entire system running on MySQL CLI is available under [`/demo.mp4`](./demo.mp4).

It walks through:

* Creating the database
* Creating tables
* Inserting data
* Trigger-based logging
* Live queries on active flags and dependencies

---

## 🙋 Author

**Pranav Raghavan**
SQL | DevifyX Internship Applicant

---

## 📝 License

This project is submitted as a technical demonstration for internship purposes. Feel free to fork, learn, and adapt with attribution.

---

Feel free to reach out for collaboration, improvements, or feedback!
