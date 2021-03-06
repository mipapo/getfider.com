<h3 id="posts">Posts</h3>

<ul>
  <li><a href="#list-posts">List Posts</a></li>
  <li><a href="#get-post">Get a Post</a></li>
  <li><a href="#create-post">Create a Post</a></li>
  <li><a href="#edit-post">Edit a Post</a></li>
  <li><a href="#delete-post">Delete a Post</a></li>
  <li><a href="#respond-post">Respond to a Post</a></li>
</ul>

A <strong>Post</strong> is new topic created by a user on the Feedback Site, while it's usually a suggestion or feature request, sometimes it might also be a bug report or a complain.

<h4 id="list-posts">List Posts</h4>

- <strong>Authentication:</strong> Optional

```
GET /api/v1/posts
```

<strong>Parameters</strong>

<table>
  <tr>
    <th width="80">Name</th>
    <th width="90">Type</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>query</code></td>
    <td><code>string</code></td>
    <td>The search keywords</td>
  </tr>
  <tr>
    <td><code>view</code></td>
    <td><code>string</code></td>
    <td>
      The filter and order to apply. Possible values are <code>all</code>, <code>recent</code>, <code>my-votes</code>, <code>most-wanted</code>, <code>most-discussed</code>, <code>planned</code>, <code>started</code>, <code>completed</code>, <code>declined</code> and <code>trending</code>. Default: <code>all</code>
    </td>
  </tr>
  <tr>
    <td><code>limit</code></td>
    <td><code>integer</code></td>
    <td>The number of entries to return. Default: <code>30</code></td>
  </tr>
  <tr>
    <td><code>tags</code></td>
    <td><code>string</code></td>
    <td>The list of tags to filter by. Separate multiple tags by <code>,</code></td>
  </tr>
</table>

<strong>Example</strong>

```
GET <baseURL>/api/v1/posts?view=completed&query=open+links&limit=50
```

<strong>Response</strong>

```
200 OK
---
[
  {
    "id": 4315,
    "number": 65,
    "title": "Open links in new tab",
    "slug": "open-links-in-new-tab",
    "description": "When somebody pastes a link in the description of an item, it has to open link in a new tab so you don't lose focus in the app",
    "createdAt": "2018-05-16T13:50:34.579281Z",
    "user": {
      "id": 45642,
      "name": "Jon Snow",
      "role": "visitor"
    },
    "hasVoted": true,
    "votesCount": 34,
    "commentsCount": 0,
    "status": "completed",
    "response": {
      "text": "This is now available on `v0.14`. Links from any markdown text will open in a new tab.",
      "respondedAt": "2018-06-13T17:48:27.073178Z",
      "user": {
        "id": 8,
        "name": "Arya Stark",
        "role": "administrator"
      },
      "original": null
    },
    "tags": ["hard","critical"]
  },
  {
    ...
  }
]
```

<h4 id="get-post">Get a Post</h4>

- <strong>Authentication:</strong> Optional

```
GET /api/v1/posts/{number}
```

<strong>Parameters</strong>

<table>
  <tr>
    <th width="80">Name</th>
    <th width="90">Type</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>number</code></td>
    <td><code>number</code></td>
    <td><strong>Required.</strong> The number of the post to retrieve.</td>
  </tr>
  <tr>
</table>

<strong>Example</strong>

```
GET <baseURL>/api/v1/posts/65
```

<strong>Response</strong>

```
200 OK
---
{
  "id": 4315,
  "number": 65,
  "title": "Open links in new tab",
  "slug": "open-links-in-new-tab",
  "description": "When somebody pastes a link in the description of an item, it has to open link in a new tab so you don't lose focus in the app",
  "createdAt": "2018-05-16T13:50:34.579281Z",
  "user": {
    "id": 45642,
    "name": "Jon Snow",
    "role": "visitor"
  },
  "hasVoted": true,
  "votesCount": 34,
  "commentsCount": 0,
  "status": "completed",
  "response": {
    "text": "This is now available on `v0.14`. Links from any markdown text will open in a new tab.",
    "respondedAt": "2018-06-13T17:48:27.073178Z",
    "user": {
      "id": 8,
      "name": "Arya Stark",
      "role": "administrator"
    },
    "original": null
  },
  "tags": ["hard","critical"]
}
```

<h4 id="create-post">Create a Post</h4>

- <strong>Authentication:</strong> Required

```
POST /api/v1/posts
```

<strong>Parameters</strong>

<table>
  <tr>
    <th width="120">Name</th>
    <th width="90">Type</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>title</code></td>
    <td><code>string</code></td>
    <td><strong>Required.</strong> The title of the post.</td>
  </tr>
  <tr>
    <td><code>description</code></td>
    <td><code>string</code></td>
    <td>The description of the post.</td>
  </tr>
</table>

<strong>Example</strong>

```
POST <baseURL>/api/v1/posts
---
{
  "title": "Allow users to edit any comment",
  "description": "This is useful to fix some minor typos or introduce more details"
}
```

<strong>Response</strong>

```
200 OK
---
{
  "id": 6848,
  "number": 47,
  "title": "Allow users to edit any comment",
  "slug": "allow-users-to-edit-any-comment"
}
```

<h4 id="edit-post">Edit a Post</h4>

- <strong>Authentication:</strong> Required
- <strong>Required Role:</strong> Collaborator or Administrator

```
PUT /api/v1/posts/{number}
```

<strong>Parameters</strong>

<table>
  <tr>
    <th width="120">Name</th>
    <th width="90">Type</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>number</code></td>
    <td><code>number</code></td>
    <td><strong>Required.</strong> The number of the post to be edited.</td>
  </tr>
  <tr>
    <td><code>title</code></td>
    <td><code>string</code></td>
    <td><strong>Required.</strong> The title of the post.</td>
  </tr>
  <tr>
    <td><code>description</code></td>
    <td><code>string</code></td>
    <td>The description of the post.</td>
  </tr>
</table>

<strong>Example</strong>

```
POST <baseURL>/api/v1/posts/47
---
{
  "title": "Allow users to edit their own comments",
  "description": "This is useful to fix some minor typos or introduce more details"
}
```

<strong>Response</strong>

```
200 OK
---
{}
```

<h4 id="delete-post">Delete a Post</h4>

- <strong>Authentication:</strong> Required
- <strong>Required Role:</strong> Administrator

```
DELETE /api/v1/posts/{number}
```

<strong>Parameters</strong>

<table>
  <tr>
    <th width="120">Name</th>
    <th width="90">Type</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>number</code></td>
    <td><code>number</code></td>
    <td><strong>Required.</strong> The number of the post to be deleted.</td>
  </tr>
  <tr>
    <td><code>text</code></td>
    <td><code>string</code></td>
    <td>The reason why this post is being deleted.</td>
  </tr>
</table>

<strong>Example</strong>

```
DELETE <baseURL>/api/v1/posts/47
---
{
  "text": "this is spam!"
}
```

<strong>Response</strong>

```
200 OK
---
{}
```

<h4 id="respond-post">Respond to a Post</h4>

- <strong>Authentication:</strong> Required
- <strong>Required Role:</strong> Collaborator or Administrator

```
PUT /api/v1/posts/{number}/status
```

<strong>Parameters</strong>

<table>
  <tr>
    <th width="140">Name</th>
    <th width="90">Type</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>number</code></td>
    <td><code>number</code></td>
    <td><strong>Required.</strong> The number of the post to add a response.</td>
  </tr>
  <tr>
    <td><code>status</code></td>
    <td><code>string</code></td>
    <td><strong>Required.</strong>The new status of the post. Possible values are <code>open</code>, <code>planned</code>, <code>started</code>, <code>completed</code>, <code>declined</code> and <code>duplicate</code></td>
  </tr>
  <tr>
    <td><code>text</code></td>
    <td><code>string</code></td>
    <td>An optional description of what is the status on this post. This is made visible to all visitors on the website.</td>
  </tr>
  <tr>
    <td><code>originalNumber</code></td>
    <td><code>number</code></td>
    <td>The number of the post to merge this into. This parameter <strong>Required</strong> when status is <code>duplicate</code>.</td>
  </tr>
</table>

<strong>Example #1</strong>

```
PUT <baseURL>/api/v1/posts/47/status
---
{
  "status": "declined",
  "text": "this is spam!"
}
```

<strong>Example #2</strong>

```
PUT <baseURL>/api/v1/posts/47/status
---
{
  "status": "duplicate",
  "originalNumber": 84
}
```

<strong>Response</strong>

```
200 OK
---
{}
```
