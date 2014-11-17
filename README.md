# prompt-server

Webserver for the Prompt social network.

## Install

We always have Prompt servers up at [TODO](#TODO), but to install your own, just follow these steps:

    npm install -g prompt-social-server
    prompt-server

On first run, the server will try to find the config values it needs in the following places:

* `~/.prompt-serverrc`
* environment variables
* stdin, by prompting you

If it lacks necessary config values, or any credentials are faulty, prompt-server will quit before it can begin.

Otherwise, it will kick up a web server at the default location of <http://localhost:3000>.

## Resources

prompt-server exposes the following API for interacting with the social network.

**N.B.: What follows is a very rough draft.**

### Summary

```
## AUTHENTICATION

HEAD    /auth               # return whether the given credentials are currently logged in
PUT     /auth               # sign up a user with the given credentials
POST    /auth               # log in the user matching the given credentials
DELETE  /auth               # logout the user with the given credentials

## USER FEED

GET     /timeline           # retrieve your friends' latest posts
GET     /notifications      # retrieve your latest notifications

## BLOCKING AND HIDING USERS

GET     /blocked            # list the users you have blocked from your content
PUT     /block/:user_id     # block the given user
DELETE  /block/:user_id     # unblock the given user

GET     /hidden             # list the users you have hidden from your timeline
PUT     /hide/:user_id      # hide the given user from your timeline
DELETE  /hide/:user_id      # unhide the given user from your timeline

## SEARCHING

GET     /search             # executes a search, using the query string for options
POST    /search             # executes a search, using the request body for options

## MESSAGES

GET     /messages           # list messages sent to you, chronologically
GET     /message/:msg_id    # get a specific message, optionally with the rest of the conversation
POST    /messages           # send a new message

## POSTS

GET     /posts              # retrieve your posts, chronologically
POST    /posts              # create a new post
GET     /post/:post_id      
PUT     /post/:post_id      # update a post
DELETE  /post/:post_id      # delete a post

## LIKES

GET     /likes              # lists every post you've liked
POST    /like/:post_id      # like a post
DELETE  /like/:post_id      # unlike a post

## FRIENDS

GET     /friends            # list your friends
GET     /friend/:user_id    # get your friend's info, ex: name, pronouns
POST    /friend/:user_id    # friend a user
DELETE  /friend/:user_id    # unfriend a user

## EVENTS

GET     /events             # list events you created or were invited to
POST    /events             # create an event
GET     /event/:event_id    # get info about a specific event
PUT     /event/:event_id    # update an event
DELETE  /event/:event_id    # delete an event
POST    /event/:event_id/invite
                            # invite multiple users to an event
PUT     /event/:event_id/invite/:user_id
                            # invite a user to an event
PUT     /rsvp/:event_id/{going,maybe,not-going}
                            # indicate or update your RSVP

## UPLOADS

GET     /uploads            # list the files you've uploaded
POST    /uploads            # uploads a new file
GET     /upload/:file_id    # returns the raw file
PUT     /upload/:file_id    # updates an uploaded file
DELETE  /upload/:file_id    # deletes an uploaded file

## PERMISSIONS

GET /permissions                   # show default permissions inherited by all resources.
PUT /permissions                   # set default permissions for all resources.
GET /permissions/:resource         # show default permissions inherited by a specific resources.
                                   # (including inherited rules)
PUT /permissions/:resource         # set default permissions for a specific resource.
                                   # (supercedes user defaults)
GET /permissions/:resource>/:id    # show permissions for a specific object.
                                   # (including inherited rules)
PUT /permissions/:resource/:id     # set permissions for a specific object.
                                   # (supercedes resource defaults)

## SETTINGS

GET  /settings                     # lists your current settings
POST /settings                     # sets values according to the JSON in the request body
                                   # (values not changed go untouched)
PUT  /settings/{setting}/{value}   # update a specific setting with a new value
```

For more info, see inside the `/docs` folder.

## Testing

    git clone https://github.com/prompt-project/server.git prompt-server
    cd prompt-server
    npm install
    npm test

## License

[GPLv3](http://opensource.org/licenses/GPL-3.0)
