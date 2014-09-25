# prompt-server

Webserver for the Prompt social network.

## Install

We always have Prompt servers up at [TODO](#TODO), but to install your own, just follow these steps:

    npm install -g prompt-server
    prompt-server

On first run, the server will try to find the config values it needs in the following places:

* `~/.prompt-serverrc`
* environment variables
* stdin, by prompting you

If it lacks necessary config values, or any credentials are faulty, prompt-server will quit before it can begin.

Otherwise, it will kick up a web server at the default location of <http://localhost:3000>.

## Resources

prompt-server exposes the following API for interacting with the social network.

**N.B.: What follows is an incredible rough draft.**

### auth

Signup, login, and account deletion.

* `HEAD /auth`: returns whether the given credentials are valid for login.
* `POST /auth/signup`: signs up, creating a user for you.
* `POST /auth/login`: logs in an existing user.

### timeline

Show your timeline. This includes posts from your friends, and any new messages since you last checked.

* `GET /timeline`: retrieves your timeline

TODO: long-polling, streaming

### block

Block a user from seeing or interacting with your content.

* `GET /block`: lists users you have blocked.
* `PUT /block/<user_id>`: block a user.

### search

Search for posts, users, and other information:

* `GET /search`: executes a search.
* `POST /search`: executes a search, using the request body instead of query parameters.

TODO: long-polling, streaming

### messages

Send messages to other users.

* `GET /messages`: lists messages you've received, chronologically.
* `GET /messages/sent`: lists your sent messages, chronologically.
* `POST /messages/<user_id>`: sends a user the request body as a message.

N.B.: Messages cannot be deleted or updated.

### posts

Posts are content: text, images, links, documents, video, etc.

* `GET /posts`: lists your posts chronologically.
* `POST /posts`: create a new post.
* `PUT /posts/<post_id>`: update a post, using the request's message body as the post's new content.
* `DELETE /posts/<post_id>`: delete a post.

### likes

TODO

### comments

TODO

### friends

Friendship is a two way street. Marking people as friends allows them to see posts you list as friends-only, even if they don't list you as a friend.

* `GET /friends`: lists your friends.
* `POST /friends`: add multiple friends by passing their user IDs as a JSON array in the request body.
* `PUT /friends/<user_id>`: add someone as a friend.
* `DELETE /friends/<user_id>`: remove someone as a friend.

### lists

Lists group your friends, so you can share with and view content from specific groups in your life.

* `GET /lists`: lists your lists.
* `POST /lists`: creates a new list using the request body.
* `PUT /lists/<list_id>`: update a list using the request body. Overwrites existing values.
* `PUT /lists/<list_id>/<user_id>,<user_id>,<user_id>...`: add users to a list.
* `DELETE /lists/<list_id>`: delete a list.
* `DELETE /lists/<list_id>/<user_id>,<user_id>`: deletes specific users from a list.

### settings

Your account settings.

* `GET /settings`: lists your current settings.
* `POST /settings`: sets values according to the JSON in the request body. Values not changed go untouched.

## Testing

    git clone https://github.com/prompt-project/server.git prompt-server
    cd prompt-server
    npm install
    npm test

## License

[GPLv3](http://opensource.org/licenses/GPL-3.0)
