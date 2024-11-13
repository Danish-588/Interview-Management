# Interview Management System

## Overview

The Interview Management System (IMS) is a web application designed to streamline the interview process for organizations. Authorized users can add, view, assess, and update candidate information, enter test scores, and leave feedback. The IMS generates final reports that assist in making selection decisions for each candidate.

## Features

- **Candidate Management**: Add, view, update, and remove candidate profiles with details such as contact information, qualifications, test scores, and performance comments.
- **User Authentication**: Secure login for different user roles with access managed by unique `user_id` and password credentials.
- **Question Management**: Create, edit, and categorize interview questions, assign marks, and link them to specific candidates.
- **Evaluation and Reporting**: Record feedback on candidates, generate reports based on test scores and comments, and use final assessments to determine candidate selection.

## Core Functionalities

1. **Add Candidate Information**: Register new candidates and assign them a unique `cand_id`.
2. **Question Management**: Interviewers can create and manage questions and assign marks.
3. **Generate Reports**: Based on feedback and test scores, reports help determine candidate selection or rejection.
4. **CRUD Operations**: Easily perform Create, Read, Update, and Delete actions on candidate data.

## Problem Statement

IMS aims to facilitate efficient management of candidate interviews by allowing authorized users to handle various aspects of the interview process. Each candidate is assigned a unique identifier (`cand_id`) and can have multiple comments and test scores recorded, with each assessment linked via `cand_id`. The system stores critical information, such as candidate contact details, qualifications, and departmental association, ensuring data integrity and ease of access.

## Tech Stack

- **XAMPP**: 
  - **Apache**: Provides the web server.
  - **MySQL**: Relational database to manage candidates, users, questions, and interview data.
  - **PHP**: Backend logic, linking the frontend with the database.
  - **Perl**: Simplifies backend scripting tasks.

## Advantages of the System

- **Organized Data**: Efficiently store and retrieve candidate information.
- **Efficient Workflow**: Streamlined interview process, reducing time and manual effort.
- **Data Integrity**: Accurate and reliable data for informed hiring decisions.

## Installation

1. Download and install [XAMPP](https://www.apachefriends.org/index.html).
2. Start Apache and MySQL from the XAMPP Control Panel.
3. Import the IMS database via phpMyAdmin.
4. Place the project files in the `htdocs` directory in the XAMPP installation folder.
5. Access the system via `http://localhost/your-project-folder-name`.

## Usage

1. **Login/Register**: Authorized users login to access the system.
2. **Manage Candidates**: Add, update, or delete candidate profiles.
3. **Manage Questions**: Create interview questions and assign them to candidates.
4. **Generate Reports**: View feedback reports and make selection decisions based on candidate performance.
