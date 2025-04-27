const express = require('express');
const app = express();
const http = require('http').createServer(app);
const io = require('socket.io')(http);

app.use(express.static('public')); // Nơi chứa file game HTML + JS

io.on('connection', (socket) => {
  console.log('A user connected');

  socket.on('move', (data) => {
    socket.broadcast.emit('move', data);
  });

  socket.on('disconnect', () => {
    console.log('A user disconnected');
  });
});

http.listen(3000, () => {
  console.log('Server running on http://localhost:3000');
});
