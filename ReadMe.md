# Task assister

## Description

The task assister is an Ikomol Proprietery application that assist in task management allocation and resolution. The users of the application are, **Super Admin**, **Admin**, **Customer Agent** and **Technicians**


### WorkFlow

1. **Admin** can create user accounts as well as revoke access to users. The admin will also be able to create teams, pair them according to their strengths and roles. Each team will have a lead. and stat level for each member. An individual will also be treated as a team. 
2. **Customer Agent** will be able to create tasks, assign them to teams. If a task is created and assigned, its status is *active*
3. **Technicians** after being assigned tasks, can update the status of the task from *active*, to either, *inprogress*, *done*, *inprogress*, and *failed*. 

### Models
1. #### User

```sql
- ID (PK)
- fname
- lname
- username
- email
- PhoneNumber
- isAgent
- isAdmin
- isSuperAdmin
- isTechnician
- locationServing
- statLevel
- createdat
- updatedat
- password
```
2. #### Team

```sql
-ID (PK)
-Name
-createdat
-updatedat
```
3. #### TeamMembers

```sql
- ID (PK)
- TeamID (FK to Team)
- UserID (FK to User)
- isLead (Boolean)
- statLevel
- createdat
- updatedat
```
4. #### Tasks
```sql
- ID (PK)
- Description
- status
- AssignedTo (FK to Team)
- createdat
- updatedat
```
5. #### Task Comment
```sql
- ID (PK)
- TaskID (FK to Task)
- UserID (FK to User)
- Comment
- createdat
```
6. #### TaskHistory
```sql
- ID (PK)
- TaskID (FK to Task)
- Status
- Timestamp
```

6. #### Notification
```sql
- ID (PK)
- UserID (FK to User)
- Message
- Status (Read/Unread)
- createdat
````

### Relationships:

* **User** to **TeamMembers**: One-to-Many (A user can be part of multiple teams)
- **Team** to **TeamMembers**: One-to-Many (A team can have multiple members)
- **TeamMembers** to **User**: Many-to-One (A team member is a user)
- **TeamMembers** to **Team**: Many-to-One (A team member belongs to a team)
- **Task** to **Team**: Many-to-One (A task is assigned to one team)
- **TaskHistory** to **Task**: Many-to-One (A task can have multiple status updates)
- **TaskComments** to **Task**: Many-to-One (A task can have multiple comments)
- **TaskComments** to **User**: Many-to-One (A comment is made by one user)
- **Notification** to **User**: Many-to-One (A notification is for one user)


### ERD Diagrams


### summary

**Explanation**

- Users can belong to multiple teams through the TeamMembers entity.
- Teams have members and a lead determined by the stats level.
- Tasks are assigned to teams and have a status history tracked by TaskStatusHistory.
- Comments allow users to comment on tasks.
- Notifications keep users informed about task updates and other relevant information.




### Api EndPoints
A. **Users**
1. **POST /users** - Create a new user <br>
    {
        "user_key":"user_value",<br>
        .<br>
        .<br>
        .        <br>
    }
2. **GET /users** - Get all users <br>
 {
        "user_key":"user_value"*,<br>
        .<br>
        .<br>
        .  <br>      
    }
3. **GET /user/id** -Get Specific user <br>
{
    "id":"id"
}
4. **PUT /user/id** - Update user <br>
{
    "id":"id",<br>
    ["data_keys":"data_values",...]*<br>
}

B. **Team**
1. **POST /team** - Create a new team
2. **GET /teams** - Get all teams
3. **GET /teams/id** -Get Specific teams
4. **PUT /teams/id** - Update a team
5. **DELETE /teams/id** - Delete a team

C. **Task**
1. **POST /task** - Create a new task
2. **GET /tasks** - Get all tasks
3. **GET /tasks/id** -Get Specific tasks
4. **PUT /tasks/id** - Update a task
5. **DELETE /tasks/id** - Delete a task

### Other Functions 
The system should also be able to handle user router information, including serial number, and type of the router. This is to track and enable management of the router. 
It can assist to reset the oneISP user Mac or monitor routers interface on the ONT. 

### Feature Recomendations

- implement bulk sms as part of notification
- use websockets 
- perform analysis and track task progress
- instant notification on whatsapp group

