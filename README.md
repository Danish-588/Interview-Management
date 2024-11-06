# Interviews Management System

A web application that allows users to manage their job interviews.

## Commands

- **Run**: `docker-compose up -d --build`
- **Stop**: `docker-compose down`
- **Enter Database**: `docker exec -it interviewsapp-db psql -U postgres -d interviewsappdb`

---

## Stack 

### Backend  
The backend is powered by **ASP.NET Core**, a high-performance, cross-platform framework that handles the application's business logic and API endpoints. It’s ideal for building secure, scalable web applications.

### Database  
**PostgreSQL** is used for data storage, ensuring reliability, data integrity, and efficient querying. It handles all application data, including users, companies, interviews, and positions.

### Frontend  
The frontend is server-rendered using ASP.NET Core’s **Razor views** and basic HTML/CSS/JavaScript, delivering a responsive and interactive user interface without relying on a separate JavaScript framework.

### Containerization  
The application runs in **Docker** containers, which package all dependencies for consistency across environments. **Docker Compose** manages services like the backend and database, simplifying deployment and scaling.

---

## Tables

### `Companies` Table
| Column | Type     | Nullable | Default |
|--------|----------|----------|---------|
| Id     | uuid     | not null |         |
| Name   | text     | not null |         |
| Rating | smallint | not null |         |

- **Primary Key**: `PK_Companies` on `Id`
- **Referenced by**: `Positions` table with foreign key `CompanyId` (ON DELETE CASCADE)

### `Interviews` Table
| Column     | Type                        | Nullable | Default |
|------------|-----------------------------|----------|---------|
| Id         | uuid                        | not null |         |
| Name       | text                        | not null |         |
| Date       | timestamp with time zone    | not null |         |
| Comment    | text                        |          |         |
| PositionId | uuid                        | not null |         |

- **Primary Key**: `PK_Interviews` on `Id`
- **Foreign Key**: `PositionId` references `Positions(Id)` (ON DELETE CASCADE)

### `Positions` Table
| Column     | Type     | Nullable | Default |
|------------|----------|----------|---------|
| Id         | uuid     | not null |         |
| Name       | text     | not null |         |
| MoneyLower | integer  | not null |         |
| MoneyUpper | integer  | not null |         |
| City       | text     | not null |         |
| Comment    | text     |          |         |

### `Users` Table
| Column    | Type     | Nullable | Default |
|-----------|----------|----------|---------|
| Id        | uuid     | not null |         |
| Name      | text     | not null |         |
| Login     | text     | not null |         |
| Password  | text     | not null |         |
| IsActive  | boolean  | not null |         |
| Language  | text     |          |         |

- **Primary Key**: `PK_Users` on `Id`
- **Referenced by**: `Positions` table with foreign key `UserId` (ON DELETE CASCADE)

### `__EFMigrationsHistory` Table
| Column         | Type                   | Nullable | Default |
|----------------|------------------------|----------|---------|
| MigrationId    | character varying(150) | not null |         |
| ProductVersion | character varying(32)  | not null |         |

- **Primary Key**: `PK___EFMigrationsHistory` on `MigrationId`

---

## Core Tables and Relationships

- **Companies Table**  
   Stores information about companies associated with job positions. A position must be linked to a company, and deleting a company will remove related positions.

- **Positions Table**  
   Holds job position details, linking each to a company and managed by a user. Each position can have multiple interviews scheduled for it.

- **Interviews Table**  
   Tracks interviews for specific positions with fields like name, date, and optional comments. Deleting a position also removes its related interviews.

- **Users Table**  
   Stores user profiles, including applicants, recruiters, or administrators, with fields like name, login, password, and active status. Users can manage job positions.

- **Localizations Table**  
   Manages translations and language-specific content for users based on their `Language` field.

- **__EFMigrationsHistory Table**  
   Used by Entity Framework Core to track applied migrations, ensuring database schema consistency across updates.