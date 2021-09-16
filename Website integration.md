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


### Rest channels:  

The RestInput and CallbackInput channels can be used for custom integrations. They provide a URL where you can post messages and **either receive response messages directly, or asynchronously via a webhook.**  

#### RestInput
**The REST channel will provide you with a REST endpoint where you can post user messages and receive the assistant's messages in response.**   

- Add the REST channel to your **credentials.yml** as:-   
 rest:
- Restart your **Rasa X or Rasa Open Source server** to make the REST channel available to receive messages.
-  You can then send messages to _http://<host>:<port>/webhooks/rest/webhook_, **replacing the host and port with the appropriate values from your running Rasa X or Rasa Open Source server**. ❗  
  ![image](https://user-images.githubusercontent.com/64036955/133624626-53a29713-daea-4871-952b-8283943ca159.png)

  #### CallbackInput:  
  The Callback channel behaves very much like the REST channel, but** instead of directly returning the bot messages to the HTTP request that sends the message, it will call a URL you can specify to send bot messages.**  
  
  - To use the callback channel, add the credentials to your credentials.yml:
```
callback:
  # URL to which Core will send the bot responses
  url: "http://localhost:5034/bot"
```
  
- Restart your Rasa X or Rasa Open Source server to make the new channel endpoint available to receive messages.  
- You can then send messages to http://<host>:<port>/webhooks/callback/webhook, replacing the host and port with the appropriate values from your running Rasa X or Rasa Open Source server. ❗
  ![image](https://user-images.githubusercontent.com/64036955/133625285-62546dc7-a9fd-4317-894e-e11785979cf9.png)
