[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

# User Manager
This repo shows how to set up application (node) and database (mongodb) on different nodes communicating using docker containers technology.

### Development
This application was developed using [ExpressJS](http://expressjs.com/). MongoDB was used for persisting data with [Mongoose](https://mongoosejs.com/) as [ORM](https://en.wikipedia.org/wiki/Object-relational_mapping).

### Installation
* Start up your terminal (or Command Prompt on Windows OS).
* Ensure that you've `node` installed on your PC.
* Clone the repository by entering the command `git clone https://github.com/Onakomaiya/UserManager.git` in the terminal.
* Navigate to the project folder using `cd UserManager` on your terminal (or command prompt)
* Create a `.env` file in your root directory and copy content from `.env.sample` file. Variables such as DB_URL (which must be a mongoDB URL) and PORT are defined in the .env file and it is essential you create this file before running the application.
```
PORT=3000
DB_URL='mongodb://Ona:123@mongo:27017/databaseName'
```
##### Create your app and mongo images
* Launch your docker terminal navigate to the location of your app using `cd c:/path/to/your/UserManager`.
* Note the `IP` address at the launch of docker terminal. You will need it to access the app through the browser  
* Run `docker-compose up -d --no-deps --build app`
* Confirm your mongo and app containers are fully running using `docker container ls` or `docker ps` 
```x-form-url-encoded
$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                      NAMES
6dbd01404dc4        usermanager2_app    "npm start"              3 hours ago         Up 21 minutes       0.0.0.0:3000->3000/tcp     app
b481cb7f513f        mongo               "docker-entrypoint..."   3 hours ago         Up 21 minutes       0.0.0.0:27017->27017/tcp   mongo
```
##### Create mongo database with user access
* Launch the mongo shell within docker using `$ docker exec -it mongo mongo`
* Create database and user with access
```x-form-url-encoded
  > show dbs
  admin   0.000GB
  config  0.000GB
  local   0.000GB
  > use andela_microsoft
  switched to db andela_microsoft
  > db.createUser(
  ...    {
  ...      user: "Ona",
  ...      pwd: "123",
  ...      roles: [{ role:"readWrite", db:"andela_microsoft;" }]
  ...    }
  ... );
```

### Testing
To ensure that your installation is successful you'll need to run tests.
Using the `IP` you noted earlier, go to `IP:PORT/users` like `192.168.xx.xx:3000/users`

### API Documentation
The API only has one endpoint which is the `/users` endpoint for saving users to the database. The endpoint works with the HTTP verbs: `POST`, `GET`, `PUT`, `DELETE`.

###### POST HTTP Request
-   `POST` /users
-   INPUT:
```x-form-url-encoded
name: John Doe
email: john.doe@gmail.com
password: johndoe
```

###### HTTP Response

-   HTTP Status: `201: created`
-   JSON data
```json
{
  "_id": "59071791b0lkscm2325794",
  "name": "John Doe",
  "email": "john.doe@gmail.com",
  "password": "johndoe",
  "__v": 0
}
```

###### GET HTTP Response
-   `GET` /users

```json
[
    {
        "_id": "59071791b0lkscm2325794",
        "name": "John Doe",
        "email": "john.doe@gmail.com",
        "password": "johndoe",
        "__v": 0
    }
]
```

###### GET HTTP Response
-   `GET` /users/:id

```json
{
    "_id": "59071791b0lkscm2325794",
    "name": "John Doe",
    "email": "john.doe@gmail.com",
    "password": "johndoe",
    "__v": 0
}
```

###### DELETE HTTP Response
-   `DELETE` /users/:id

```x-form-url-encoded
User John Doe was deleted
```

###### POST HTTP Request
-   `PUT` /users/:id
-   INPUT:
```x-form-url-encoded
name: Jane Doe
email: jane.doe@gmail.com
password: janedoe
```

###### HTTP Response

-   HTTP Status: `200: OK`
-   JSON data
```json
{
  "_id": "59071791b0lkscm2325794",
  "name": "Jane Doe",
  "email": "jane.doe@gmail.com",
  "password": "janedoe",
  "__v": 0
}
```


### Author
**Olajide Bolaji 'Nuel** - Software Developer at Andela
