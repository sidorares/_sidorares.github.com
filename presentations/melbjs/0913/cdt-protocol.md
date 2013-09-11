### Webkit DevTools protocol
  - JSON-RPC over websocket
  - list of websocket endpoints available at http://localhost:9222/json
  - node.js clients:

  https://github.com/cyrus-and/chrome-remote-interface
  https://github.com/admazely/inspector
  http://sokolovstas.github.io/SublimeWebInspector/


### Start
```
> google-chrome --remote-debugging-port=9222```


### What is possible with CDT remote protocol:
- Everything as in V8 protocol
- get sourcemaps
- restart frame
- run to location
- set breakoint on DOM node update
- listen console messages (with stack)
- set breakpoint on XHR request
- emulate mouse/keyboard/touch events
- override geolocation and orientation info
- and much more (Canvas, Workers, Memory, Profile...)


### Using protocol client from node.js
```js
var Chrome = require('chrome-remote-interface');
Chrome(function(chrome) {
   chrome.Debugger.enable();
   chrome.on('Debugger.paused', function(res) {
      // stack, script info, break reason etc
   })
})
```