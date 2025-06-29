## Overview
The EduHub project is a robust backend database solution designed using MongoDB to support an online e-learning platform. Developed as part of the AltSchool of Data Engineering Tinyuka 2024 Second Semester Project Exam, this project demonstrates essential MongoDB expertise, including data modeling, database architecture, CRUD operations, aggregation pipelines, and query optimization techniques. It encompasses key functionalities such as managing users, courses, enrollments, assessments, comprehensive data analysis, and advanced search capabilities.

## Project Goals
- Build a scalable NoSQL database architecture tailored specifically for online learning platforms.
- Maintain data integrity through robust schema validation rules.
- Enable efficient and high-performance querying for real-time responsiveness.
- Provide comprehensive documentation and practical code demonstrations to enhance understanding and implementation.

## Key Features
- User Management: Facilitates account creation, authentication, and profile customization for both students and instructors.
- Course Management: Enables instructors to design, structure, and publish interactive educational content.
- Enrollment Monitoring: Tracks student participation, course registration, and progress throughout the learning journey.
- Assignment Workflow: Supports the creation, submission, and evaluation of assignments with integrated grading features.
- Analytics & Reporting: Generates actionable insights, performance metrics, and learning trends through data-driven reports.
- Intelligent Search & Filters: Offers dynamic course discovery using keyword searches, category filters, and sorting options.

## Setup Instructions
Prerequisites
MongoDB v8.0 or higher 
Python 3.8+
Required Python libraries: pymongo, pandas, datetime

##  Installation
#### 1. Clone the Repository
git clone: https://github.com/Chinelonweke/mongodb-eduhub-project.git
cd mongodb-eduhub-project

#### 2. Set Up MongoDB
Create a MongoDB Atlas Account and Cluster
 Create a Database User
 Configure Network Access (IP Whitelist)
 Get Your Connection String
 Install MongoDB and start the service.
Database is name Eduhub_db

#### 3. Install Dependencies
setup the requirement.txt file
pymongo

#### 4. Run the Jupyter Notebook
Open notebooks/eduhub_mongodb_project.ipynb in Jupyter Notebook.
Execute all cells to set up the database and run queries.

#### 5. Import Sample Data
Data imported in data/sample_data.json.

## Database Schema

#### Collections

### users Collection

Represents all user accounts (students, instructors, admins).

| **Field**    | **Type** | **Description**                                      |
| ------------ | -------- | -----------------------------------------------------|
|'userId'     | String   | Unique user identifier                                |
|'email'      | String   | User's email address (**indexed** for quick lookup)   |
|'firstName'  | String   | First name of the user                                |
|'lastName'   | String   | Last name of the user                                 |
|'role'       | String   | User role:"student" or "instructor"                   |
|'dateJoined' | Date     | The date the user registered on the platform          |
|'isActive'   | Boolean  | Indicates if the account is active (for soft deletes) |
|'profile'    | Object   | User’s bio, skills, and additional profile details    |


### Courses Collection

| **Field**     | **Type** | **Description**                                   |
| --------------| -------- | ------------------------------------------------- |
|'courseId'     | String   | Unique identifier for the course                  |
|'title'        | String   | Course name or title                              |
|'description'  | String   | Overview of the course content                    |
|'category'     | String   | Category label (e.g.,'"Data"','"AI"', etc.)       |
|'instructorId' | String   | References the instructor (linked via userId)     |
|'createdAt'    | Date     | Timestamp of when the course was created          |
|'updatedAt'    | Date     | Timestamp of the last course update               |
|'tags'         | Array    | List of tags/keywords for filtering and discovery |
|'price'        | Number   | Course price in USD                               |
|'isPublished'  | Boolean  | Indicates if the course is live/publicly visible  |

### Lessons Collection
| **Field** | **Type** | **Description**                                                      |
| ----------| -------- | -------------------------------------------------------------------- |
|'lessonId' | String   | Unique identifier for the lesson                                     |
|'courseId' | String   | References'courses.courseId' (indicates which course it belongs to)  |
|'title'    | String   | Title of the lesson                                                  |
|'content'  | String   | Body of the lesson (can be HTML or Markdown formatted)               |
|'duration' | Number   | Estimated time to complete the lesson (in minutes)                   |

### Enrollments Collection
| **Field**       | **Type** | **Description**                                     |
| ----------------| -------- | --------------------------------------------------- |
|'enrollmentId'   | String   | Unique identifier for each enrollment               |
|'studentId'      | String   | References'users.userId' (the student enrolled)     |
|'courseId'       | String   | References'courses.courseId' (the enrolled course)  |
|'enrollmentDate' | Date     | Date the student enrolled in the course             |
|'lastAccessed'   | Date     | The last time the student accessed the course       |
|'progress'       | Number   | Percentage of the course completed (0–100%)         |

### Assignments Collection
| **Field**     | **Type** | **Description**                                          |
| --------------| -------- | -------------------------------------------------------- |
|'assignmentId' | String   | Unique identifier for the assignment                     |
|'courseId'     | String   | References'courses.courseId' (indicates related course)  |
|'title'        | String   | Title of the assignment                                  |
|'instructions' | String   | Detailed instructions or prompt for the assignment       |
|'dueDate'      | Date     | Deadline for submitting the assignment                   |

### Submissions Collection
| **Field**      | **Type** | **Description**                                            |
| ---------------| -------- | -----------------------------------------------------------|
|'submissionId'  | String   | Unique identifier for the submission                       |
|'assignmentId'  | String   | References'assignments.assignmentId'                       |
|'studentId'     | String   | References'users.userId' (student who made the submission) |
|'submittedDate' | Date     | Timestamp when the submission was made                     |
|'grade'         | Number   | Score or mark awarded to the submission                    |
|'isGraded'      | Boolean  | Indicates whether the submission has been graded           |

## Usage
Launch the Jupyter Notebook to perform CRUD operations, aggregation queries, and performance benchmarking.
Refer to src/eduhub_queries.py for standalone Python script implementations.
Modify sample_data.json to add or update data as needed.

## Data Import Utility – Code Overview
This section of the project features helper functions designed to load and insert data from the sample_data.json file into MongoDB. Below is a breakdown of its key components.

## convert_date_strings_to_datetime(data, date_fields)
Function Purpose: Converts specific fields containing ISO-formatted date strings into proper datetime objects.
Why it's used:  MongoDB requires actual Date objects—not plain strings—for accurate date-based operations such as sorting, filtering, and comparisons. This transformation ensures the data is stored in a query-friendly format.

## CRUD Operations Summary
All core Create, Read, Update, and Delete (CRUD) functionalities required for the EduHub project have been fully implemented and demonstrated in the main notebook: eduhub_mongodb_project.ipynb.

## Task 3.1: Create Operations
Added a new student user
Created a new course
Enrolled a student in a course
Added a new lesson to an existing course

## Task 3.2: Read Operations
Queried all active students
Retrieved course details with instructor info
Listed all courses in a specific category
Found students enrolled in a given course
Implemented case-insensitive course title search

## Task 3.3: Update Operations
Updated user profile data
Marked a course as published
Modified assignment grades
Added new tags to an existing course

## Task 3.4: Delete Operations
Soft-deleted a user (set isActive to false)
Deleted an enrollment document
Removed a lesson from a course
Refer to eduhub_mongodb_project.ipynb for code implementations and execution results.

## Performance Optimization
Indexes created on:
- users.email for unique lookups.
- courses.title and courses.category for search.
- assignments.dueDate for deadline queries.
- enrollments.studentId and enrollments.courseId for enrollment lookups.
Query performance analyzed using explain() and optimized with timing comparisons.

## Challenges Faced and Solutions
Challenges Faced During the EduHub MongoDB Project & Solutions:

### 1. Dealing with Nested JSON Structures

#### Issue: 
The sample_data.json file included nested elements and date strings that weren't directly compatible with MongoDB.

#### Resolution:
Created helper functions like convert_date_strings_to_datetime and convert_dates_in_collections to transform ISO date strings into Python datetime objects.Applied the conversion logic across entire collections to ensure reliable data import.

### 2. Setting Up the Development Environment

#### Issue: 
Missing libraries and package conflicts in Jupyter Notebook or VS Code environments.

#### Resolution:
Documented all required dependencies (e.g., pymongo, pandas, bson) in the README to make environment setup straightforward.

### 3. Ensuring Referential Integrity Between Collections

#### Issue: 
Maintaining valid relationships between entities like users-enrollments and courses-lessons using fields like userId and courseId.

#### Resolution:
Designed data creation logic that cross-references valid IDs.
Used unique constraints and validation checks to prevent duplicates and mismatched links.

### 4. Handling Errors During Data Import

#### Issue: 
Data import processes would fail silently due to incorrect file paths or malformed JSON.

#### Resolution:
Added try-except blocks to catch and report errors during file loading, JSON decoding, and MongoDB insertion.
Provided meaningful error messages to simplify troubleshooting.

### 5. Connecting to the collection in Mongodb
#### issue: 
The connection to collection  was difficult becuase of the  ip address.

#### Resolution: 
Added a new ip address that accepts connection from anywhere.

## License
This project is licensed under the MIT License.
Feel free to use, modify, and distribute this project in accordance with the terms of the license.

## Contributors
Chinelo Nweke

## Submission Details
Due Date: Sunday, June 15, 2025, 11:59 PM WAT.

## Resources
MongoDB Documentation: https://docs.mongodb.com/











