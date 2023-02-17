# Implement Sockets in Vue js compatible with Laravel Backend

## Summery

The Repo is about to Vue.js implementation of Sockets that is compatible with a Laravel backend. It uses the "laravel-echo" and "socket.io-client" libraries to establish a connection between the client-side Vue.js application and the server-side Laravel backend.

To use this code, first, the "laravel-echo" and "socket.io-client" libraries should be installed using npm. Then, a "socket.js" file should be created in the Vue.js project's "src" folder, which will handle the configuration and initialization of the Echo instance.

The code in the "socket.js" file initializes a new instance of Echo, sets the broadcaster to "socket.io", and provides the host of the Echo server that is used in Laravel's "broadcasting.php" configuration file. Additionally, it sends the authentication header with the user's token to the server when the connection is established.

In a Vue.js component, the "socket.js" file is imported, and the "channel" method of the Echo instance is called with the channel ID specified in the Laravel backend's event broadcasting configuration. The "listen" method is then used to register a listener for the specified channel, and a callback function is provided to handle incoming messages from the server.

The code is provided as an example and should be adjusted based on the specific needs of the project. Additionally, the version numbers of the "laravel-echo", "socket.io", and "socket.io-client" libraries should be verified to ensure compatibility.

### Installing

A step by step series of examples that tell you how to get a development

environment running

Install Laravel Eco

    npm install laravel-echo

Install socket

    npm install socket.io-client

    npm install socket.io

## Make a socket.js file in src folder

### Sample code of socket.js file

    import Echo from "laravel-echo";

    window.io = require("socket.io-client");

    const echo_instance = new Echo({

      broadcaster: "socket.io",

      host: process.env.VUE_APP_ECHO_SERVER,

      auth: {

        headers: { Authorization: "Bearer " + localStorage.getItem('token') },

      },

    });

    export default echo_instance;

### Use In component

First import socket.js in the component

     import echo_instance from "../../socket";

use this code in created method or where you want

      echo_instance

        .channel(`${this.channel_id}`)

        .listen(`.${this.channel_id}`, (response) => {

          console.log("responsesssss", response);

          if (response.report) {

            console.log("response socket", response);

          } else {

          }

        });

        * channel_id is here which laravel use in event brodcasting

        * Make sure you put "." in listen

## Acknowledgments

  - Make sure the version of packages like that in package.json file, if latest versions not work

###

      "socket.io": "^2.0.3",

      "socket.io-client": "^2.0.3",

      "laravel-echo": "^1.15.0",
