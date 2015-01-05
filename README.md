Gohunt
========

A golang client library for the official Product Hunt API.

## Usage

### Gohunt Client

Interaction with the Product Hunt API is facilitated by the Gohunt Client. The client can be generated in three ways:


Client-Only Authentication by OAuth2
```go
client, err := gohunt.NewOAuthClient(clientID, clientSecret)
```

User-Authentication by Developer Token
```go
client := gohunt.NewUserClient(phToken)
```

User-Authentication by OAuth2
```go
func HandleLogin() {
   err := gohunt.RequestUserOAuthCode(clientID, redirectUrl, state)
}

func HandleRedirect(data) {
   client, err := gohunt.NewUserOAuthClient(clientID, clientSecret, redirectUrl, data.code)
}
```

### Client Interface

`[param]` indicates an optional parameter; use "" or -1 to exclude them in the request.

```go
// Posts
client.GetPost(id int)
client.GetPosts()
client.GetPreviousPosts(daysAgo int)
client.GetPostsOnDay(day string) // Formatted YYYY-MM-DD
client.GetAllPosts([searchUrl string], [olderThanID int], [newerThanID int], [count int])

// Users
client.GetUser(username string)  // id or username
client.GetAllUsers([olderThanID int], [newerThanID int], [count int], [order string])  // order is "asc" or "desc"

// Votes
client.GetPostVotes(postID int, [olderThanID int], [newerThanID int], [count int], [order string])
client.GetUserVotes(userID int, [olderThanID int], [newerThanID int], [count int], [order string])

// Notifications
client.GetNotifications([olderThanID int], [newerThanID int], [count int], [order string])
```