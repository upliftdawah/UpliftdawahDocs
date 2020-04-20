# API Reference
All APIs return a structure like below where the `code` field tells you whether it succeeded or not. In case of success
`code` will be `200` and there will be a `payload` field containing the result as mentioned in each API. In case of
failure `code` be any value other than 200 and there will be an `error` field containing the error message

```
//e.g error response for get_meeting_notes api
{code: 404, error: 'could not find meeting notes'}
//e.g success response for get_meeting_notes api
{code: 200, payload: {
  id: 'kdfjskjfskdfslkfsd',
  created_by: '3234k3j4l2k3j4l32k',
  created_for: '3234k3j4l2k3j4l32k',
  created_at: 12321310,
  updated_at: 12321310,
  notes: 'Some notes'
}}
```
**Base URL:** https://us-central1-upliftdawahapp.cloudfunctions.net/ 

## Type Definitions
```
EPOCHTIME: int //milliseconds from epoch

ADD_USER_REQUEST: {
  "full_name" : <string>, //required
  "phone" : <string>,
  "email" : <string>, //required
  "address" : <string>,
  "dob" : <EPOCHTIME>,
  "role" : <int>, //required
  "zone" : <int>,
  "request_message" : <string>
}

SIGNUP_REQUEST: {
  "full_name" : <string>, //required
  "password" : <string>, //required
  "phone" : <string>,
  "email" : <string>, //required
  "address" : <string>,
  "dob" : <EPOCHTIME>,
  "role" : <int>, //required
  "zone" : <int>,
  "request_message" : <string>
}

UPDATE_USER_REQUEST: {
  "user_id" : <string>, //required
  "full_name" : <string>, //required
  "phone" : <string>,
  "address" : <string>,
  "dob" : <EPOCHTIME>,
  "zone" : <int>,
  "request_message" : <string>
}

USER_RESPONSE: {
  "id" : <string>,
  "user_id" : <string>,
  "full_name" : <string>,
  "phone" : <string>,
  "email" : <string>,
  "address" : <string>,
  "dob" : <EPOCHTIME>,
  "role" : <int>,
  "zone" : <int>,
  "request_message" : <string>,
  "photo" : <string>,
  "status" : <int>,
  "created_at" : <EPOCHTIME>,
  "updated_at" : <EPOCHTIME>,
  "last_contacted" : <EPOCHTIME>,
  "has_dummy_password": <boolean>,
  "is_email_verified": <boolean>
}

TICKET_CORRESPONDENCE: {
  created_by: <string>,
  created_by_name: <string>, //this field is only returned in get api
  timestamp: <EPOCHTIME>,
  contents: <string>
}

ADD_TICKET_REQUEST: {
  assignee: <string>, 
  contents: <string>, //required
  subject: <string>, //required
  status: <int>
}

UPDATE_TICKET_REQUEST: {
  id: <string>, //required
  assignee: <string>,
  status: <int> //required
}

TICKET_RESPONSE: {
  id: <string>,
  created_by: <string>,
  created_by_name: <string>, //this field is only returned in get api
  assignee: <string>,
  assignee_name: <string>, //this field is only returned in get api
  contents: <string>,
  subject: <string>,
  status: <int>,
  created_at: <EPOCHTIME>,
  updated_at: <EPOCHTIME>,
  correspondence: [<TICKET_CORRESPONDENCE>]
}

ADD_TASK_REQUEST: {
  assignee: <string>, //required
  contents: <string>, //required
  status: <int>
}

UPDATE_TASK_REQUEST: {
  id: <string>, //required
  status: <int> //required
}

TASK_RESPONSE: {
  id: <string>,
  created_by: <string>,
  created_by_name: <string>, //this field is only returned in get api
  assignee: <string>,
  assignee_name: <string>, //this field is only returned in get api
  contents: <string>,
  status: <int>,
  created_at: <EPOCHTIME>,
  updated_at: <EPOCHTIME>
}

ADD_MEETING_NOTES_REQUEST: {
  created_for: <string>, //required
  notes: <string> //required
}

UPDATE_MEETING_NOTES_REQUEST: {
  id: <string>, //required
  notes: <string> //required
}

MEETING_NOTES_RESPONSE: {
  id: <string>,
  created_by: <string>,
  created_by_name: <string>, //this field is only returned in get api
  created_for: <string>,
  created_for_name: <string>, //this field is only returned in get api
  notes: <string>,
  created_at: <EPOCHTIME>,
  updated_at: <EPOCHTIME>
}

ADD_EDUCATIONAL_MATERIAL_REQUEST: {
  created_for: <string>, //required
  contents: <string>, //required
  status: <int>
}

UPDATE_EDUCATIONAL_MATERIAL_REQUEST: {
  id: <string>, //required
  status: <int> //required
}

EDUCATIONAL_MATERIAL_RESPONSE: {
  id: <string>,
  created_by: <string,
  created_by_name: <string, //this field is only returned in get api
  created_for: <string>,
  created_for_name: <string>, //this field is only returned in get api
  contents: <string>,
  status: <int>,
  created_at: <EPOCHTIME>,
  updated_at: <EPOCHTIME>
}

```

## User APIs
### Get User
* **Path:** `/api/user?id=<user_id>`
* **Http Method:** `GET`
* **Response Body:** `{code: 200, payload: USER_RESPONSE}`

### Get User by Email
* **Path:** `/api/user_by_email?email=<email>`
* **Http Method:** `GET`
* **Response Body:** `{code: 200, payload: USER_RESPONSE}`

### Add User
* **Path:** `/api/user`
* **Http Method:** `PUT`
* **Request Body:** `ADD_USER_REQUEST`
* **Response Body:** `{code: 200, payload: USER_RESPONSE}`

### Update User
* **Path:** `/api/user`
* **Http Method:** `PATCH`
* **Request Body:** `UPDATE_USER_REQUEST`
* **Response Body:** `{code: 200, payload:USER_RESPONSE}`

### Delete User
* **Path:** `/api/user?id=<user_id>`
* **Http Method:** `DELETE`
* **Response Body:** `{code: 200, payload: '<user_id>'}`

### Update Zone
* **Path:** `/api/set_user_zone`
* **Http Method:** `PATCH`
* **Request Body:** `{id: '<id>', status: <zone_id}`
* **Response Body:** `{code: 200, payload: USER_RESPONSE}`

### Update Status
* **Path:** `/api/set_user_status`
* **Http Method:** `PATCH`
* **Request Body:** `{id: '<id>', status: <status_id>}`
* **Response Body:** `{code: 200, payload: USER_RESPONSE}`

### Approve user
* **Path:** `/api/approve_user`
* **Http Method:** `PATCH`
* **Request Body:** `{id: '<id>', role: <role_id> (optional)}`
* **Response Body:** `{code: 200, payload: USER_RESPONSE}`

### Deactivate Account
* **Path:** `/api/deactivate_account`
* **Http Method:** `PATCH`
* **Request Body:** ``
* **Response Body:** `{code: 200, payload: USER_RESPONSE}`

### Update Role
* **Path:** `/api/set_user_role`
* **Http Method:** `PATCH`
* **Request Body:** `{id: '<id>', status: <role_id}`
* **Response Body:** `{code: 200, payload: USER_RESPONSE}`

### Update Photo (This method is not ready yet)
* **Path:** `/api/set_user_photo`
* **Http Method:** `POST`
* **Request Body:** TBD
* **Response Body:** TBD

### Reset Photo (This method is not ready yet)
* **Path:** `/api/reset_user_photo`
* **Http Method:** `POST`
* **Request Body:** TBD
* **Response Body:** TBD

### List Users
* **Path:** `/api/list_users`
* **Http Method:** `POST`
* **Request Body:** 
```
{
  filters: {
    roles: [],
    zone: [],
    status: [],
    has_mentors: true/false/none
    is_email_verified: true/false/none
  },
  limit: int,
  sort: '' // e.g. 'created_at desc', following multiple sort orders are supported, to request support for new combination create an issue
  //dob asc, full_name asc

}
```
* **Response Body:** `{code: 200, payload: [USER_RESPONSE]}`

### get_user_status
* **Path:** `/get_user_status?uid=<user_id>`
* **Http Method:** `GET`
* **Request Body:** ``
* **Response Body:** `{code: 200, payload: USER_RESPONSE}` //everything other than status and email verification flag will be null

### List New Shahadahs
* **Path:** `/api/list_new_shahadahs?r=detailed`
* **Http Method:** `POST`
* **Response Body:** `{code: 200, payload: [USER_RESPONSE]}`

### List Unattended Muslims
* **Path:** `/api/list_unattended_muslims?r=detailed`
* **Http Method:** `POST`
* **Response Body:** `{code: 200, payload: [USER_RESPONSE]}`

### Notifications API
* **Path:** `/api/notifications`
* **Http Method:** `GET`
* **Response Body:**
For Admin:
```
{code: 200, payload: {
  unattended_muslims: [USER_RESPONSE],
  total_unattended_muslims: <int>,
  new_shahadahs: [USER_RESPONSE],
  total_new_shahadahs: <int>,
  pending_membership_requests: [USER_RESPONSE],
  total_pending_membership_requests: <int>,
  unassigned_tickets: [TICKET_RESPONSE],
  total_unassigned_tickets: <int>,
}}
}
```

For Volunteer:
```
{code: 200, payload: {
  unattended_muslims: [USER_RESPONSE],
  total_unattended_muslims: <int>,
  newly_assigned_muslims: [USER_RESPONSE], //right now this is being returned as empty
  total_newly_assigned_muslims: <int>,
  unacknowledged_tasks: [TASK_RESPONSE],
  total_unacknowledged_tasks: <int>
}}
}
```

For New Muslims:
```
{code: 200, payload: {
  new_educational_material: [EDUCATIONAL_MATERIAL_RESPONSE],
  total_new_educational_material: <int>
}}
}
```

### Notification batch counts API
* **Path:** `/api/notification_counts`
* **Http Method:** `GET`
* **Response Body:**
For Admin:
```
{code: 200, payload: {
  unattended_muslims: <int>,
  new_shahadahs: <int>,
  pending_membership_requests: <int>,
  unassigned_tickets: <int>
}}
}
```

For Volunteer:
```
{code: 200, payload: {
  unattended_muslims: <int>,
  newly_assigned_muslims: <int>,
  unacknowledged_tasks: <int>
}}
}
```

For New Muslims:
```
{code: 200, payload: {
  new_educational_material: <int>
}}
}
```

### Assign Mentors
* **Path:** `/api/assign_mentors`
* **Http Method:** `POST`
* **Request Body:**
```
{
  user_id: '<mentee_id>',
  mentors: [] //mentors user id
}
```
* **Response Body:**
```
{code: 200, payload: {
  user_id: '<mentee_id>',
  mentors: [] //mentors user id
 }
}
```

### Assign Mentees
* **Path:** `/api/assign_mentees`
* **Http Method:** `POST`
* **Request Body:** 
```
{
  user_id: '<mentor_id>',
  mentees: [] //mentees user id
}
```
* **Response Body:** 
```
{code: 200, payload: {
  user_id: '<mentee_id>',
  mentors: [] //mentors user id
 }
}
```

### List Mentees
* **Path:** `/api/list_mentees?id=<user_id>`
* **Http Method:** `GET`
* **Response Body:** `{code: 200, payload: [] //list of mentees user id}`

### List Mentees with details
* **Path:** `/api/list_mentees?id=<user_id>&r=detailed`
* **Http Method:** `GET`
* **Response Body:** `{code: 200, payload: [USER_RESPONSE]}`

### List Mentors
* **Path:** `/api/list_mentors?id=<user_id>`
* **Http Method:** `GET`
* **Response Body:** `{code: 200, payload: [] //list of mentors user id}`

### List Mentors with details
* **Path:** `/api/list_mentors?id=<user_id>&r=detailed`
* **Http Method:** `GET`
* **Response Body:** `{code: 200, payload: [USER_RESPONSE]}`

## Misc APIs
All these APIs can be called without auth token.

### List Roles
* **Path:** `/roles`
* **Http Method:** `GET`
* **Response Body:** `{code: 200, payload:[{'id': <int>, 'Value': <string>}]}` [see this for possible values](https://github.com/naveedahmedsiddiqui/UpliftDawah/blob/master/functions/misc.js#L13-L16)

### List Zones
* **Path:** `/zones`
* **Http Method:** `GET`
* **Response Body:** `{code: 200, payload:[{'id': <int>, 'Value': <string>}]}` [see this for possible values](https://github.com/naveedahmedsiddiqui/UpliftDawah/blob/master/functions/misc.js#L32-L37)

### List User Statuses
* **Path:** `/user_statuses`
* **Http Method:** `GET`
* **Response Body:** `{code: 200, payload:[{'id': <int>, 'Value': <string>}]}` [see this for possible values](https://github.com/naveedahmedsiddiqui/UpliftDawah/blob/master/functions/misc.js#L23-L25)

### Signup
* **Path:** `/signup`
* **Http Method:** `PUT`
* **Request Body:** `SIGNUP_REQUEST`
* **Response Body:** `{code: 200, payload: USER_RESPONSE}`

### send_password_reset_email
* **Path:** `/send_password_reset_email`
* **Http Method:** `PUT`
* **Request Body:** `{email: <string> //required}`
* **Response Body:** `{code: 200, payload: <email>}`

### send_verification_email
* **Path:** `/send_verification_email`
* **Http Method:** `PUT`
* **Request Body:** `{email: <string> //required, password: <string> //required}`
* **Response Body:** `{code: 200, payload: <email>}`

### is_email_verified
* **Path:** `/is_email_verified?uid=<user_id>`
* **Http Method:** `GET`
* **Request Body:** ``
* **Response Body:** `{code: 200, payload: true/false}`

### List Ticket Statuses
* **Path:** `/ticket_statuses`
* **Http Method:** `GET`
* **Response Body:** `{code: 200, payload:[{'id': <int>, 'Value': <string>}]}` [see this for possible values](https://github.com/naveedahmedsiddiqui/UpliftDawah/blob/master/functions/misc.js#L44-L46)

### List Task Statuses
* **Path:** `/task_statuses`
* **Http Method:** `GET`
* **Response Body:** `{code: 200, payload:[{'id': <int>, 'Value': <string>}]}` [see this for possible values](https://github.com/naveedahmedsiddiqui/UpliftDawah/blob/master/functions/misc.js#L53-L57)

### Educational Material Statuses
* **Path:** `/educational_material_statuses`
* **Http Method:** `GET`
* **Response Body:** `{code: 200, payload:[{'id': <int>, 'Value': <string>}]}` [see this for possible values](https://github.com/naveedahmedsiddiqui/UpliftDawah/blob/master/functions/misc.js#L64-L65)


## Tickets APIs

### Get Ticket
* **Path:** `/api/ticket?id=<ticket_id>`
* **Http Method:** `GET`
* **Response Body:** `{code: 200, payload: TICKET_RESPONSE}`

### Add Ticket
* **Path:** `/api/ticket`
* **Http Method:** `PUT`
* **Request Body:** `ADD_TICKET_REQUEST`
* **Response Body:** `{code: 200, payload: TICKET_RESPONSE}`

### Update Ticket
* **Path:** `/api/ticket`
* **Http Method:** `PATCH`
* **Request Body:** `UPDATE_TICKET_REQUEST`
* **Response Body:** `{code: 200, payload: TICKET_RESPONSE}`

### Delete Ticket
* **Path:** `/api/ticket?id=<ticket_id>`
* **Http Method:** `DELETE`
* **Response Body:** `{code: 200, payload: '<ticket_id>'}`

### Update Status
* **Path:** `/api/set_ticket_status`
* **Http Method:** `PATCH`
* **Request Body:** `{id: '<id>', status: <status>}`
* **Response Body:** `{code: 200, payload: TICKET_RESPONSE}`

### Add Ticket Correspondence
* **Path:** `/api/ticket_correspondence?id=<ticket_id>`
* **Http Method:** `PUT`
* **Request Body:** `{'contents': '<text>'}`
* **Response Body:** `{code: 200, payload: TICKET_RESPONSE}`

### List Tickets
By default this api will not include ticket correspondence in the result, use the path mentioned below to include correspondence
* **Path:** `/api/list_tickets` (use `/api/list_tickets?r=detailed` to include correspondence )
* **Http Method:** `POST`
* **Request Body:** 
```
{
  filters: {
    created_by: [<user_id>],
    assignee: [<user_id>],
    status: []
  },
  limit: int,
  sort: '' // e.g. 'created_at desc', to request new multi-sort combination create an issue
}
```
* **Response Body:** `{code: 200, payload: [TICKET_RESPONSE]}`

### List Unassigned Tickets
* **Path:** `/api/list_tickets?r=detailed`
* **Response Body:** `{code: 200, payload: [TICKET_RESPONSE]}`

## Tasks APIs

### Get Task
* **Path:** `/api/task?id=<task_id>`
* **Http Method:** `GET`
* **Response Body:** `{code: 200, payload: TASK_RESPONSE}`

### Add Task
* **Path:** `/api/task`
* **Http Method:** `PUT`
* **Request Body:** `ADD_TASK_REQUEST`
* **Response Body:** `{code: 200, payload: TASK_RESPONSE}`

### Update Task
* **Path:** `/api/task`
* **Http Method:** `PATCH`
* **Request Body:** `UPDATE_TASK_REQUEST`
* **Response Body:** `{code: 200, payload: TASK_RESPONSE}`

### Delete Task
* **Path:** `/api/task?id=<task_id>`
* **Http Method:** `DELETE`
* **Response Body:** `{code: 200, payload: '<task_id>'}`

### Update Status
* **Path:** `/api/set_task_status`
* **Http Method:** `PATCH`
* **Request Body:** `{id: '<id>', status: <status>}`
* **Response Body:** `{code: 200, payload: TASK_RESPONSE}`

### List Tasks
* **Path:** `/api/list_tasks`
* **Http Method:** `POST`
* **Request Body:** 
```
{
  filters: {
    assignee: [<user_id>],
    status: []
  },
  limit: int,
  sort: '' // e.g. 'created_at desc', following multiple sort orders are supported, to request support for new combination create an issue
}
```
* **Response Body:** `{code: 200, payload: [TASK_RESPONSE]}`

## Meeting Notes APIs

### Get Meeting Note
* **Path:** `/api/meeting_note?id=<meeting_note_id>`
* **Http Method:** `GET`
* **Response Body:** `{code: 200, payload: MEETING_NOTES_RESPONSE}`

### Add Meeting Note
* **Path:** `/api/meeting_note`
* **Http Method:** `PUT`
* **Request Body:** `ADD_MEETING_NOTES_REQUEST`
* **Response Body:** `{code: 200, payload: MEETING_NOTES_RESPONSE}`

### Update Meeting Note
* **Path:** `/api/meeting_note`
* **Http Method:** `PATCH`
* **Request Body:** `UPDATE_MEETING_NOTES_REQUEST`
* **Response Body:** `{code: 200, payload: MEETING_NOTES_RESPONSE}`

### Delete Meeting Note
* **Path:** `/api/meeting_note?id=<meeting_note_id>`
* **Http Method:** `DELETE`
* **Response Body:** `{code: 200, payload: '<meeting_note_id>'}`

### List Meeting Notes
* **Path:** `/api/list_meeting_notes`
* **Http Method:** `POST`
* **Request Body:** 
```
{
  filters: {
    created_by: [<user_id>],
    created_for: [<user_id>]
  },
  limit: int,
  sort: '' // e.g. 'created_at desc', following multiple sort orders are supported, to request support for new combination create an issue
}
```
* **Response Body:** `{code: 200, payload: [MEETING_NOTES_RESPONSE]}`

## Educational Material APIs

### Get Educational Material
* **Path:** `/api/educational_material?id=<educational_material_id>`
* **Http Method:** `GET`
* **Response Body:** `{code: 200, payload: EDUCATIONAL_MATERIAL_RESPONSE}`

### Add Educational Material
* **Path:** `/api/educational_material`
* **Http Method:** `PUT`
* **Request Body:** `ADD_EDUCATIONAL_MATERIAL_REQUEST`
* **Response Body:** `{code: 200, payload: EDUCATIONAL_MATERIAL_RESPONSE}`

### Update Educational Material
* **Path:** `/api/educational_material`
* **Http Method:** `PATCH`
* **Request Body:** `UPDATE_EDUCATIONAL_MATERIAL_REQUEST`
* **Response Body:** `{code: 200, payload: EDUCATIONAL_MATERIAL_RESPONSE}`

### Update Status
* **Path:** `/api/set_educational_material_status`
* **Http Method:** `PATCH`
* **Request Body:** `{id: '<id>', status: <status>}`
* **Response Body:** `{code: 200, payload: EDUCATIONAL_MATERIAL_RESPONSE}`

### Delete Educational Material
* **Path:** `/api/educational_material?id=<educational_material_id>`
* **Http Method:** `DELETE`
* **Response Body:** `{code: 200, payload: '<educational_material_id>'}`

### List Educational Materials
* **Path:** `/api/list_educational_materials`
* **Http Method:** `POST`
* **Request Body:** 
```
{
  filters: {
    status: []
  },
  limit: int,
  sort: '' // e.g. 'created_at desc', following multiple sort orders are supported, to request support for new combination create an issue
}
```
* **Response Body:** `{code: 200, payload: [EDUCATIONAL_MATERIAL_RESPONSE]}`

## Notification/Home Page APIs
All the below APIs are combined into single API `notifications` (see above) which can called for all the user types without any parameter to get the designed data
All the below APIs are still available which can be called to get the detailed information

Admin:
Admin notification screen will show the following 4 lists:
1. New Shahadahs:
API: list_new_shahadahs, when user will click 'more...' option, a new page will be open and the same api can be called like list_new_shahadahs?r=detailed to get full list

2. Un attended muslims:
API: list_unattended_muslims, when user will click 'more...' option, a new page will be open and the same api can be called like list_unattended_muslims?r=detailed to get full list

3. Pending membership requests
API: list_users, with param: {filters: {status: [3], sort: 'created_at desc, fullname asc', limit: 5, is_email_verified: true}}, when 'more' is clicked the same api can be called without limit provided

4. Unanswered/incomplete tickets
API: list_unassigned_tickets, when user will click 'more...' option, a new page will be open and the same api can be called like list_unassigned_tickets?r=detailed to get full list

Volunteers:
Volunteers notification screen will show following 3 lists:
1. Newly assigned muslims //this should be implemented with push notification

2. Unack'd tasks
API: list_tasks, with param: {filters: {status: [1], sort: 'created_at desc', limit: 5}}, when 'more' is clicked the same api can be called without limit provided

3. Un attended muslims
API: list_unattended_muslims, when user will click 'more...' option, a new page will be open and the same api can be called like list_unattended_muslims?r=detailed to get full list

# Sign-up flows
There are two possible scenarios for sign-up:
1. A user is signing up which doesn't exist in the system
2. A user is signing up which was already added in the system by another user

## Scenario 1: A user is signing up which doesn't exist in the system
In this scenario, the user will be added in the system with 'Unapproved' status. A verification email will be sent to the user. Until the
email is verified the user will not show up in admin's list for approval. The email sent to the user will contain a link to verify the email address.
While the email addrsss is not verified if the user try to use app it should show that the email verification is pending and give option to the user
to send verification email again by entering email address and password again. Once the email is verified but not yet approved, user will be
shown appropriate message and there will be no other option.

APIs to be used: signup, GET api/user, send_verification_email

## Scenario 2: A user is signing up which was already added in the system by another user
In this case user will be created with dummy password and status 'Active' if created by Admin or 'Unapproved' otherwise. If the user being
created is a NewMuslim role, the status will be 'Unclaimed' regardless of who is creating it. Since the password is dummy no one would
be able to login as that user even if its status is 'Active'. When the actual user try to signup using that email address, the
signup api will return error code 409, indicating that the email already exists. The user then should be shown appropriate message
with option to claim that account by sending password reset email. Once the user resets the password, the account will show to admin
in pending approval list. The workflow is the same from this point onwards.

APIs to be used: PUT api/user, signup, send_password_reset_email, GET api/user
