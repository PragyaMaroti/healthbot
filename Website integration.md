Ways to do website integration:  
- Use the **Rasa Chat Widget**, a widget which we can incorporate into our existing webpage **by adding a HTML snippet**.  
- build our own chat widget.   



### Chat Widget
Once you've set up your SocketIO channel, you can use the official Rasa Chat Widget on any webpage. Just paste the following into your site HTML and paste the URL of your Rasa instance into the data-websocket-url attribute:   
```
<div id="rasa-chat-widget" data-websocket-url="https://your-rasa-url-here/"></div>
<script src="https://unpkg.com/@rasahq/rasa-chat" type="application/javascript"></script>
```   

### Websocket Channel 
The SocketIO channel uses websockets and is real-time. To use the SocketIO channel, add the credentials to your credentials.yml:   

```
socketio:
  user_message_evt: user_uttered
  bot_message_evt: bot_uttered
  session_persistence: true/false
````  
**The first two configuration values define the event names used by Rasa Open Source when sending or receiving messages over socket.io.**   
Note:  By default, the SocketIO channel uses the socket id as sender_id, which causes the session to restart at every page reload. session_persistence can be set to true to avoid that. In that case, the frontend is responsible for generating a session id and sending it to the Rasa Core server by emitting the event session_request with {session_id: [session_id]} immediately after the connect event.   

