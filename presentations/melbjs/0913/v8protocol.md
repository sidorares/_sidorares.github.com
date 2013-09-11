### V8 protocol
  - http-like: Headers + '\r\n\r\b' + json body
  - there is (undocumented) client in node.js core


### Example:
```
> node --debug-brk program.js
```


### Example:
```
> telnet 127.0.0.1 5858
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
Type: connect
V8-Version: 3.14.5.9
Protocol-Version: 1
Embedding-Host: node v0.10.12
Content-Length: 0

Content-Length: 102

{"seq":117,"type":"request","command":"v8flags","arguments":{"flags":"--trace_gc b^@always_compact"}}
Content-Length: 95

{"seq":3,"request_seq":117,"type":"response","command":"v8flags","success":true,"running":true}
```


### What is possible with protocol:
- get script source
- get backtrace
- evaluate code on frame
- add/remove breakpoints (+ conditions and hit count)
- modify source (live edit)
- pause, step in/next/out/continue


### Using protocol client from node.js
```js
var Debugger = require('_debugger');
var client = new Debugger();
client.connect(5858);
var bp = {
  type: "scriptId",
  target: 12345,
  line: 123,
  column: 33
};
client.setBreakpoint(bp, function(err, res) {
  console.log(res);
});
```


### Using protocol client from node.js
```js
client.on('break', function(res) {
   console.log(res.body.script.id);
});
```
