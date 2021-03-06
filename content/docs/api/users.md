<h3 id="users">Users</h3>

<ul>
  <li><a href="#list-users">List Users</a></li>
  <li><a href="#create-user">Create a User</a></li>
</ul>

<h4 id="list-users">List Users</h4>

- <strong>Authentication:</strong> Required
- <strong>Required Role:</strong> Collaborator or Administrator

```
GET /api/v1/users
```

<strong>Example</strong>

```
GET <baseURL>/api/v1/users
```

<strong>Response</strong>

```
200 OK
---
[
  {
    "id": 3,
    "name": "Arya Stark",
    "role": "administrator",
    "status": "active",
  },
  {
    "id": 5,
    "name": "Jon Snow",
    "role": "visitor",
    "status": "active"
  },
  {
    "id": 24,
    "name": "The Queen",
    "role": "collaborator",
    "status": "blocked"
  },
  {
    ...
  }
]
```

<h4 id="create-user">Create a User</h4>

- <strong>Authentication:</strong> Required
- <strong>Required Role:</strong> Administrator

```
POST /api/v1/users
```

The Create User API will only create a new user if it cannot find an existing user with given email or reference ID. If the user already exists on Fider, the ID of the existing user is returned instead of creating a new user.

The ID returned by this API can be used to impersonate that user. Read more about <a href="#impersonation">impersonation</a>.

<strong>Parameters</strong>

<table>
  <tr>
    <th width="120">Name</th>
    <th width="90">Type</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>name</code></td>
    <td><code>string</code></td>
    <td><strong>Required.</strong> The name of the user.</td>
  </tr>
  <tr>
    <td><code>email</code></td>
    <td><code>string</code></td>
    <td>The email of the user.</td>
  </tr>
  <tr>
    <td><code>reference</code></td>
    <td><code>string</code></td>
    <td>A unique ID for the user in another system.</td>
  </tr>
</table>

<strong>Example</strong>

```
POST <baseURL>/api/v1/users
---
{
  "name": "Jon Snow",
  "email": "jon.snow@got.com",
  "reference": "CRM-817453"
}
```

<strong>Response</strong>

```
200 OK
---
{
  "id": 6332
}
```