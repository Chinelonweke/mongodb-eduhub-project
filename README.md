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


### courses Collection

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

### lessons Collection
| **Field** | **Type** | **Description**                                                      |
| ----------| -------- | -------------------------------------------------------------------- |
|'lessonId' | String   | Unique identifier for the lesson                                     |
|'courseId' | String   | References'courses.courseId' (indicates which course it belongs to)  |
|'title'    | String   | Title of the lesson                                                  |
|'content'  | String   | Body of the lesson (can be HTML or Markdown formatted)               |
|'duration' | Number   | Estimated time to complete the lesson (in minutes)                   |

### enrollments Collection
| **Field**       | **Type** | **Description**                                     |
| ----------------| -------- | --------------------------------------------------- |
|'enrollmentId'   | String   | Unique identifier for each enrollment               |
|'studentId'      | String   | References'users.userId' (the student enrolled)     |
|'courseId'       | String   | References'courses.courseId' (the enrolled course)  |
|'enrollmentDate' | Date     | Date the student enrolled in the course             |
|'lastAccessed'   | Date     | The last time the student accessed the course       |
|'progress'       | Number   | Percentage of the course completed (0–100%)         |

### assignments Collection
| **Field**     | **Type** | **Description**                                          |
| --------------| -------- | -------------------------------------------------------- |
|'assignmentId' | String   | Unique identifier for the assignment                     |
|'courseId'     | String   | References'courses.courseId' (indicates related course)  |
|'title'        | String   | Title of the assignment                                  |
|'instructions' | String   | Detailed instructions or prompt for the assignment       |
|'dueDate'      | Date     | Deadline for submitting the assignment                   |

### submissions Collection
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