### Vim netbeans protocol
  - text/line based
  - vim is client
  - attemts to connect to port 3219 when started as `vim -nb` (or `:nbs` from vim command mode)
  - node.js server: https://github.com/clehner/node-vim-netbeans


### What is possible with netbeans protocol:
- open new buffer (empty/with text/file from fs)
- listen keystrokes
- show/hide line marker
- move cursor to line
- listen for hover events (GUI only) and display bubble/tooltip


### Using protocol client from node.js
```js

var nb = require('vim-netbeans');
var server = new nb.VimServer();
server.on("clientAuthed", function (vim) {
  vim.editFile('test.js', function(buff) {
    buff.setDot(10, 20); // move to line/col
  }
  vim.key("C-i", function (buffer, offset, lnum, col) {
    console.log('Ctrl-i clicked');
  });
});
```
