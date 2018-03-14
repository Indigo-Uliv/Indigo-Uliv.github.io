# Admin RESTful API

* auto-gen TOC:
{:toc}

## Presentation


The [Indigo Web project](https://github.com/Indigo-Uliv/indigo-web) is a
translation layer that provides an accessible and well structured set of access
methods to the data management system. Access methods comes in the form of
RESTful services, accessible via the base url of an indigo node running indigo-web.
This Admin RESTful API allows the remote management of the system. It is
available at _**/api/admin**_ from you root URI.


## Groups

### **Get the list of existing groups**


_Synopsys_:

  To get a list of existing groups, the following request shall be performed:

  ```GET <root URI>/api/admin/groups```

  where:
  * `<root URI>` is the URL of the web server.

_Response Body_:

a JSON array of JSON String: the list of group names.

_Response Status_:

<table>
  <tr> <th>HTTP Status</th> <th>Description</th>          </tr>
  <tr> <td>200 OK</td>      <td>The list is returned</td> </tr>
</table>


_Example_:

  GET to the groups URI to list existing groups:

```
GET /api/admin/groups HTTP/1.1
Host: 192.168.12.12
```

  Response:

```
HTTP/1.1 200 OK

['group1', 'group2']
```

### **Create a new group**


_Synopsys_:

  To create a new group, the following request shall be performed:

  ```POST <root URI>/api/admin/groups```

  where:
  * `<root URI>` is the URL of the web server.


_Request Body_:

The request expects a json dictionary to provide the name of the group.
```
{ "groupname": "NewGroupName" }
````

_Response Body_:

a JSON dictionary representing the new group (uuid, name and members).

_Response Status_:

<table>
  <tr> <th>HTTP Status</th>     <th>Description</th>                               </tr>
  <tr> <td>201 Created</td>     <td>The group is created</td>                      </tr>
  <tr> <td>400 Bad Request</td> <td>The request contains invalid parameters</td>   </tr>
  <tr> <td>403 Forbidden</td>   <td>The client lacks the proper authorization</td> </tr>
  <tr> <td>409 Conflict</td>    <td>The group name is already used</td>            </tr>
</table>


_Example_:

  POST to the groups URI to create a new group:

```
POST /api/admin/groups HTTP/1.1
Host: 192.168.12.12

{ "groupname": "group2" }
```

  Response:

```
HTTP/1.1 201 Created

{
  "uuid": "43dbdc8f-b863-471f-98d1-982dd51410f1"
  "name": "group2",
  "members": [],
}
```

### **Get Information on an existing group**


_Synopsys_:

  To get information on an existing group, the following request shall be
  performed:

  ```GET <root URI>/api/admin/groups/<GroupName>```

  where:
  * `<root URI>` is the URL of the web server.
  * `<GroupName>` is the name of the group.

_Response Body_:

a JSON dictionary representing the group (uuid, name and members).

_Response Status_:

<table>
  <tr> <th>HTTP Status</th>   <th>Description</th>                 </tr>
  <tr> <td>200 OK</td>        <td>The information is returned</td> </tr>
  <tr> <td>404 Not Found</td> <td>The group doesn't exist</td>     </tr>
</table>


_Example_:

  GET to the groups URI to get information:

```
GET /api/admin/groups/group2 HTTP/1.1
Host: 192.168.12.12
```

  Response:

```
HTTP/1.1 200 OK

{
  "uuid": "43dbdc8f-b863-471f-98d1-982dd51410f1"
  "name": "group2",
  "members": [],
}
```

### **Delete an existing group**


_Synopsys_:

  To delete on an existing group, the following request shall be performed:

  ```DELETE <root URI>/api/admin/groups/<GroupName>```

  where:
  * `<root URI>` is the URL of the web server.
  * `<GroupName>` is the name of the group.

_Response Status_:

<table>
  <tr> <th>HTTP Status</th>   <th>Description</th>                               </tr>
  <tr> <td>200 OK</td>        <td>The group is deleted</td>                      </tr>
  <tr> <td>403 Forbidden</td> <td>The client lacks the proper authorization</td> </tr>
  <tr> <td>404 Not Found</td> <td>The group doesn't exist</td>                   </tr>
</table>


_Example_:

  DELETE to the groups URI to delete a group:

```
DELETE /api/admin/groups/group2 HTTP/1.1
Host: 192.168.12.12
```

  Response:

```
HTTP/1.1 200 OK
```

### **Modify an existing group**


_Synopsys_:

  To modify a group, the following request shall be performed:

  ```PUT <root URI>/api/admin/groups/<GroupName>```

  where:
  * `<root URI>` is the URL of the web server.
  * `<GroupName>` is the name of the group.


_Request Body_:

The request expects a json dictionary to provide the name of the
users to add or remove.

```
{
  "add_users": ["user1", "user2", ...] or
  "rm_users": ["user1", "user2", ...]
}
````

_Response Body_:

a message string informing which users have been added or removed.

_Response Status_:

<table>
  <tr> <th>HTTP Status</th>         <th>Description</th>                               </tr>
  <tr> <td>200 OK</td>              <td>The group has been fully modified</td>         </tr>
  <tr> <td>206 Partial Content</td> <td>Some users have been added or deleted</td>     </tr>
  <tr> <td>400 Bad Request</td>     <td>The request contains invalid parameters</td>   </tr>
  <tr> <td>403 Forbidden</td>       <td>The client lacks the proper authorization</td> </tr>
</table>


_Example 1_:

  PUT to the groups URI to add users to a group:

```
PUT /api/admin/groups/group2 HTTP/1.1
Host: 192.168.12.12

{ "add_users": ["user3", "user5"] }
```

  Response:

```
HTTP/1.1 200 OK

Added user3, user5 to the group group2
```


_Example 2_:

  PUT to the groups URI to remove users from a group:

```
PUT /api/admin/groups/group2 HTTP/1.1
Host: 192.168.12.12

{ "rm_users": ["user5"] }
```

  Response:

```
HTTP/1.1 200 OK

Removed user5 from the group group2
```


## Users

### **Get the list of existing users**


_Synopsys_:

  To get a list of existing users, the following request shall be performed:

  ```GET <root URI>/api/admin/users```

  where:
  * `<root URI>` is the URL of the web server.

_Response Body_:

a JSON array of JSON String: the list of users names.

_Response Status_:

<table>
  <tr> <th>HTTP Status</th>   <th>Description</th>              </tr>
  <tr> <td>200 OK</td>        <td>The list is returned</td>     </tr>
</table>


_Example_:

  GET to the users URI to list existing users:

```
GET /api/admin/users HTTP/1.1
Host: 192.168.12.12
```

  Response:

```
HTTP/1.1 200 OK

['user1', 'user2']
```

### **Create a new user**


_Synopsys_:

  To create a new user, the following request shall be performed:

  ```POST <root URI>/api/admin/users```

  where:
  * `<root URI>` is the URL of the web server.


_Request Body_:

The request expects a json dictionary to provide the information about the user.
```
{
  "username": "NewUserName",
  "password": "Password",
  "email": "UserEmail",
  "administrator": "is_admin"
}
```

where:
  * `NewUserName` is the name of the user
  * `Password` is its Password
  * `UserEmail` is its email
  * `IsAdmin` is a boolean to make the user an administrator

_Response Body_:

a JSON dictionary representing the new user ('uuid', 'name', 'email',
'administrator', 'active', 'groups').

_Response Status_:

<table>
  <tr> <th>HTTP Status</th>     <th>Description</th>                               </tr>
  <tr> <td>201 Created</td>     <td>The user is created</td>                      </tr>
  <tr> <td>400 Bad Request</td> <td>The request contains invalid parameters</td>   </tr>
  <tr> <td>403 Forbidden</td>   <td>The client lacks the proper authorization</td> </tr>
  <tr> <td>409 Conflict</td>    <td>The user name is already used</td>            </tr>
</table>


_Example_:

  POST to the users URI to create a new user:

```
POST /api/admin/users HTTP/1.1
Host: 192.168.12.12

{
  "username": "user1",
  "password": "userPW",
  "email": "user@indigo.com",
  "administrator": "false"
}
```

  Response:

```
HTTP/1.1 201 Created

{
  'uuid': "2f9b85ca-522b-4657-a984-493ab116424c",
  'name': "user1",
  'email': "user@indigo.com",
  'administrator': "true",
  'active': "true",
  'groups': []
}
```

### **Get Information on an existing user**


_Synopsys_:

  To get information on an existing user, the following request shall be
  performed:

  ```GET <root URI>/api/admin/users/<UserName>```

  where:
  * `<root URI>` is the URL of the web server.
  * `<UserName>` is the name of the user.

_Response Body_:

a JSON dictionary representing the user ('uuid', 'name', 'email',
'administrator', 'active', 'groups').

_Response Status_:

<table>
  <tr> <th>HTTP Status</th>   <th>Description</th>                 </tr>
  <tr> <td>200 OK</td>        <td>The information is returned</td> </tr>
  <tr> <td>404 Not Found</td> <td>The user doesn't exist</td>     </tr>
</table>


_Example_:

  GET to the users URI to get information:

```
GET /api/admin/users/user1 HTTP/1.1
Host: 192.168.12.12
```

  Response:

```
HTTP/1.1 200 OK

{
  'uuid': "2f9b85ca-522b-4657-a984-493ab116424c",
  'name': "user1",
  'email': "user@indigo.com",
  'administrator': "true",
  'active': "true",
  'groups': []
}
```

### **Delete an existing user**


_Synopsys_:

  To delete on an existing user, the following request shall be performed:

  ```DELETE <root URI>/api/admin/users/<UserName>```

  where:
  * `<root URI>` is the URL of the web server.
  * `<UserName>` is the name of the user.

_Response Status_:

<table>
  <tr> <th>HTTP Status</th>   <th>Description</th>                               </tr>
  <tr> <td>200 OK</td>        <td>The user is deleted</td>               </tr>
  <tr> <td>403 Forbidden</td> <td>The client lacks the proper authorization</td> </tr>
  <tr> <td>404 Not Found</td> <td>The user doesn't exist</td>                    </tr>
</table>


_Example_:

  DELETE to the users URI to delete a user:

```
DELETE /api/admin/user/user1 HTTP/1.1
Host: 192.168.12.12
```

  Response:

```
HTTP/1.1 200 OK
```


### **Modify an existing user**


_Synopsys_:

  To modify a user, the following request shall be performed:

  ```PUT <root URI>/api/admin/users/<UserName>```

  where:
  * `<root URI>` is the URL of the web server.
  * `<UserName>` is the name of the user.


_Request Body_:

The request expects a json dictionary to provide the fields of the user to be
modified.

```
{
  "password": password,
  "email": email,
  "administrator": is_admin,
  "active": is_active}
}
````

_Response Body_:

a JSON dictionary representing the user ('uuid', 'name', 'email',
'administrator', 'active', 'groups').

_Response Status_:

<table>
  <tr> <th>HTTP Status</th>         <th>Description</th>                               </tr>
  <tr> <td>200 OK</td>              <td>The group has been fully modified</td>         </tr>
  <tr> <td>400 Bad Request</td>     <td>The request contains invalid parameters</td>   </tr>
  <tr> <td>403 Forbidden</td>       <td>The client lacks the proper authorization</td> </tr>
</table>


_Example_:

  PUT to the users URI to modify a user:

```
PUT /api/admin/groups/user2 HTTP/1.1
Host: 192.168.12.12

{
  "email": user2@indigo.com,
  "active": "true"
 }
```


  Response:

```
HTTP/1.1 200 OK

{
  'uuid': "2f9b85ca-522b-4657-a984-493ab116424c",
  'name': "user2",
  'email': "user2@indigo.com",
  'administrator': "false",
  'active': "true",
  'groups': []
}
```
