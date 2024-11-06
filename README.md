# Interviews Manager


Small app that allows user to manage his job interviews.

Stack: ASP.NET WebAPI(.NET 6), AutoMapper, Entity Framework and PostgreSQL for backend; ASP.NET WebApp (Razor Pages) and vanilla JavaScript for frontend, deploying with Docker. Unit-tested with xUnit, AutoFixture and Moq.

If you want to run the app, you can use <i>docker-compose up -d </i> from project root folder, and then open http://localhost:7000/ in your browser.


# Tables


### `Companies` Table
| Column | Type     | Collation | Nullable | Default |
|--------|----------|-----------|----------|---------|
| Id     | `uuid`   |           | not null |         |
| Name   | `text`   |           | not null |         |
| Rating | `smallint` |         | not null |         |

**Indexes:**
- `PK_Companies` PRIMARY KEY, btree (Id)

**Referenced by:**
- Table `Positions`, Foreign Key `FK_Positions_Companies_CompanyId` on `CompanyId` → `Companies(Id)` (ON DELETE CASCADE)

---

### `Interviews` Table
| Column     | Type                        | Collation | Nullable | Default |
|------------|-----------------------------|-----------|----------|---------|
| Id         | `uuid`                      |           | not null |         |
| Name       | `text`                      |           | not null |         |
| Date       | `timestamp with time zone`  |           | not null |         |
| Comment    | `text`                      |           |          |         |
| PositionId | `uuid`                      |           | not null |         |

**Indexes:**
- `PK_Interviews` PRIMARY KEY, btree (Id)
- `IX_Interviews_PositionId` btree (PositionId)

**Foreign Key Constraints:**
- `FK_Interviews_Positions_PositionId` on `PositionId` → `Positions(Id)` (ON DELETE CASCADE)

---

### `Positions` Table
| Column     | Type     | Collation | Nullable | Default |
|------------|----------|-----------|----------|---------|
| Id         | `uuid`   |           | not null |         |
| Name       | `text`   |           | not null |         |
| MoneyLower | `integer`|           | not null |         |
| MoneyUpper | `integer`|           | not null |         |
| City       | `text`   |           | not null |         |
| Comment    | `text`   |           |          |         |

---

### `Users` Table
| Column    | Type     | Collation | Nullable | Default |
|-----------|----------|-----------|----------|---------|
| Id        | `uuid`   |           | not null |         |
| Name      | `text`   |           | not null |         |
| Login     | `text`   |           | not null |         |
| Password  | `text`   |           | not null |         |
| IsActive  | `boolean`|           | not null |         |
| Language  | `text`   |           |          |         |

**Indexes:**
- `PK_Users` PRIMARY KEY, btree (Id)

**Referenced by:**
- Table `Positions`, Foreign Key `FK_Positions_Users_UserId` on `UserId` → `Users(Id)` (ON DELETE CASCADE)

---

### `__EFMigrationsHistory` Table
| Column         | Type                   | Collation | Nullable | Default |
|----------------|------------------------|-----------|----------|---------|
| MigrationId    | `character varying(150)` |        | not null |         |
| ProductVersion | `character varying(32)`  |         | not null |         |

**Indexes:**
- `PK___EFMigrationsHistory` PRIMARY KEY, btree (MigrationId)

---

# Core Tables and Relationships
1.1 Companies Table

    Purpose: Stores information about companies involved in interviews or positions.
    Key Fields: Id (primary key), Name (company name), and Rating (company rating).
    Relationships: Referenced by the Positions table, meaning a position must be associated with a specific company.
    Cascade Deletion: If a company is deleted, all associated positions in the Positions table are automatically deleted.

1.2 Positions Table

    Purpose: Holds details about job positions within companies, which users can apply for.
    Key Fields: Id (primary key), Name (job title), MoneyLower and MoneyUpper (salary range), City (location of the job), and Comment (additional notes).
    Relationships:
        Associated with Companies through the CompanyId field, indicating which company offers each position.
        Likely related to the Users table to track which user posted or manages the position.
        Used by the Interviews table to link each interview to a position.

1.3 Interviews Table

    Purpose: Records details about interviews for specific positions.
    Key Fields:
        Id (primary key)
        Name (name of the interview)
        Date (scheduled date and time)
        Comment (optional notes on the interview)
        PositionId (foreign key to Positions), linking each interview to a job position.
    Relationships:
        Directly related to the Positions table by PositionId, so each interview is specific to a position.
        Cascade deletion is enabled, meaning if a position is deleted, all related interviews are removed.

1.4 Users Table

    Purpose: Stores user information, likely representing applicants, recruiters, or admin users.
    Key Fields:
        Id (primary key)
        Name (user's full name)
        Login (username or unique identifier)
        Password (hashed password)
        IsActive (boolean indicating if the user account is active)
        Language (preferred language for localization purposes).
    Relationships:
        Associated with Positions through UserId, meaning users can be responsible for positions.
        Cascade deletion on related positions if a user is deleted.

1.5 Localizations Table (not fully detailed here)

    Purpose: Likely used for managing language-specific translations for user interface elements and messages.
    Role: Supports localization features in the app by storing key-value pairs for translations. The Language field in the Users table is probably used to match users with the correct localization data.

1.6 __EFMigrationsHistory Table

    Purpose: Used by Entity Framework (EF) to track schema migrations.
    Role: Records all migrations that have been applied to the database schema. Not directly relevant to the application's business logic.