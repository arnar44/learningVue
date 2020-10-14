# Learning Vue
The purpose of this project was to get familiar with the Vue syntax. It is a simple app that can GET and POST to the https://jsonplaceholder.typicode.com/ API.

## App
There are two functionalities on the app. The user can make a GET request to the API, it gets all "posts" from the API and lists them for the user.
The user can also POST to the API. Since this is only a test API, the posts will not be saved to the server, only faked as if. This means that if a post is successful it will appear in the posts lists, but when a users requests the posts his/her posts will not be a part of the response nor the listed posts. 

## Project setup
```
git clone https://github.com/arnar44/learningVue.git
```

```
cd learningVue
```

```
yarn install
```

```
yarn run serve
```
App will be run on the localhost.
