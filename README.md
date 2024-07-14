# OJ-Project
# High Level Design
| Date: 10.07.2024 - 13.07.2024
| By: Shaivi Sinha
| Project Name: Logic Room - Online Judge
## FRONTEND
1. Home Page
    - Provide an introduction to the platform and navigation to key areas.
    - Overview of platform, featured challenges, login/signup links.
2. Login/Sign Up Page
    - Enable user authentication and account creation.
    - Forms for username, email, password; options to login or Sign Up.
        - Log In
            - Input: Username, Password
            - E-mail direction for forgot password
            - Link to Sign Up page
        - Sign Up
            - Input: username, password, password confirmation, e-mail
            - Third party sign up: google, apple, github
            - Link to Log in page
3. Dashboard
    - Central hub for user-specific data and actions.
        - User Profile
        - Notifs
        - Stats
        - Steak score
    - Overview of
        - solved problems
        - current rank + badge
        - most solved topics
        - topics for revision
        - Streak calendar
        - save questions
4. Problem List
    - displays all available coding challenges
        - List of problems with title
        - difficulty
        - acceptance
        - rating (user rating)
        - solutions (opened after a passing a certain test cases (75%) in multiple submission/ after acceptance of your code
    - also displays
        - the problems to improve rank
        - streak calendar
5. Problem Page
    - Displays the details of a specific problem and facilitate code submission.
    - Includes:
        - Problem statement
        - input/output examples
        - code editor
        - run button
        - submit button
    - Also Include:
        - Hint Section
        - Constraint Section
        - Leaderboard
            - Highlights top performers on the platform
            - Rankings based on problems solved and performance metrics (time complexity, test cases passed)
6. Admin Dashboard
    - Provides administrators with tools to manage the platform.
    - Overview of user activities, problem management, user management, submission reviews, and system monitoring.
7. Contest Page
    - to be added sooon!!
8.  Discussion Forums
    - Allows the users to discuss problems, and help each other
    - Threads for each problem, user comments, upvote/downvote system
9.  User Settings
    - Allows the users to manage their account settings
    - Update email, change password, manage notification preferences, and delete account.
10.  Achievements and Badges
    - Gamifying the platform and encourage user engagement
    - badges earned by users
    - progress tracking
11.  FAQ section
    - Provides users with assistance and answers to common questions

<aside>
💡 Figma File for Low-Fidelity Prototype attached below

https://www.figma.com/design/50WUElJaoYFnUWYgtI7Nwd/OJ?node-id=0-1&t=x9ryRLCk6YgcNUsV-1

</aside>

## BACKEND

to be done using Express.js and Node.js

## REST API ENDPOINTS

- Authentication
    - POST /api/auth/register: registers a new user
    - POST /api/auth/login: authenticates a user
- User Profile APIs
    - GET /api/user/profile: retrieves the authenticated user's profile
    - PUT /api/user/profile: Updates the authenticated user's profile
- Problem Management APIs
    - GET /api/problems: retrieves a list of all problems
    - GET /api/problems/: retrieves a specific problem by its ID
    - POST /api/problems: creates a new problem (Admin only)
- Submission APIs
    - POST /api/submissions: submits a solution for a problem
    - GET /api/submissions: retrieves all submissions by the authenticated user
- Leaderboard APIs
    - GET /api/leaderboard: retrieves the leaderboard data
- Reporting System APIs
    - POST /api/contest/log-violation: logs a potential cheating incident
    - GET /api/admin/violation-reports: retrieves the violation reports for admin review

## DATABASES

1. **Users**
    - userId
    - username
    - email
    - passwordHash
    - solvedProblems
    - submissions
    - createdAt
    - updatedAt
2. **Problems**
    - problemId
    - title
    - description
    - difficulty
    - testCases
    - solutionCode
    - topic tags
    - createdAt
    - updatedAt
3. **Submissions**
    - submissionId
    - userId
    - problemId
    - code
    - language
    - status
    - executionTime
    - memory
    - submittedAt
4. **Leaderboard**
    - userId
    - score
    - rank
    - updatedAt

## DOCKER

Containers:

1. Frontend Container (React.js)
2. Backend Container (Node.js & Express.js)
3. Database Container (MongoDB)
4. Judge Container (Code execution and evaluation)

Purpose

- Ensures consistency across environments
- Simplifies deployment
- Isolates the code execution for security

## SECURITY MEASURES

1. Using Docker containers to run user-submitted code in a secure, isolated environment
2. Implementing CPU and memory usage limits for code execution to prevent resource abuse
3. Thoroughly validating all user inputs, especially in code submissions
4. Ensures all API communications use HTTPS for secure data transfer
5. Ensures API connect at time of authentication and authorization

## CODE EVALUATION SYSTEM

1. Execute code written in various programming languages
2. Compare program output with expected results to determine correctness
3. Provide feedback on code performance and correctness (test cases passed or not)


## ANTI-CHEATING MEASURE

1. limit copy-paste actions within the code editor
2. Ensuring the user remains engaged with the coding environment.


## REPORTING SYSTEM

### 1. Features

- Logging the details of potential cheating incidents
- display warnings for minor violations
- using flag for severe or repeated violations for manual review
- user agreement page explaining anti-cheating measures before starting the contest

### 2. API Endpoints

- POST /api/contest/log-violation: to log the potential cheating incidents
- GET /api/admin/violation-reports: to retrieve the violation reports for admin review


## CHALLENGES

- Providing instant feedback on code submissions while handling multiple concurrent users can be resource-intensive and complex
    - Soltion: Using lightweight Docker containers to run code execution processes, as containers can be spun up and down quickly, ensuring scalability and isolation
- Supporting multiple programming languages with varying runtime environments and requirements
    - Solution: Developing a modular execution framework where each programming language has a dedicated Docker image configured with the necessary environment
- Scaling the platform to handle peak loads during user traffic without degrading performance
    - Solution: Deploying the application on a cloud platform (AWS) with auto-scaling capabilities to dynamically adjust resources based on demand.
- Executing the user-submitted code securely to prevent malicious activities and resource abuse
    - Solution: Implementing code sandboxing techniques to isolate code execution from the main system, thereby preventing any harmful code from accessing sensitive system resources
