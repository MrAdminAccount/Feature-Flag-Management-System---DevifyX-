# Feature-Flag-Management-System - DevifyX (SQL Only)

## 📌 Overview
This project implements a **Feature Flag Management System** purely using **MySQL** — no backend or frontend involved. It was built as part of a DevifyX internship assignment and demonstrates strong SQL design, relational modeling, and trigger-based automation.

Feature flags are critical for controlling the rollout of features in different environments and to specific user segments.

## 🛠️ Features Implemented

### 🔑 Core Features
- ✅ **Feature Flags Table** with metadata
- ✅ **Enable/Disable flags** system-wide
- ✅ **User/Group targeting**
- ✅ **Environment-specific flags**
- ✅ **Audit logging** with timestamps and actor info
- ✅ **Flag expiry** support
- ✅ **Dependency management** (flag A depends on B)
- ✅ **Sample SQL query interface**

### 🌟 Bonus Features
- ✅ **Percentage rollout** of flags
- ✅ **Soft deletes** instead of hard deletions
- ✅ **Flag tagging/categorization**
- ✅ **Change history table** for all updates

## 🧱 Database Structure

- `feature_flags` – Core table for flags
- `users`, `groups`, `user_group_membership` – Targeting
- `environments` – Dev, staging, prod, etc.
- `flag_assignments` – Maps flags to users/groups
- `flag_dependencies` – Relationships between flags
- `flag_audit_logs` – Tracks changes (create, update, delete)
- `flag_history` – Full changelog (bonus)

## 🚀 Getting Started

1. Clone the repo or copy the SQL script.
2. Open your MySQL client (like MySQL Workbench or CLI).
3. Run the entire SQL file. It will:
   - Create the `feature_flag_system` database
   - Generate all tables, triggers, and views
   - Insert sample data for demo purposes
