# irc.js

## Example usage

Add to the head of the document:

```html
<script src="https://cdn.jsdelivr.net/gh/matheusfillipe/irc.js@0.0.1/irc.min.js"></script>
```

Use it like this:

```javascript
// You can change these defaults
// WsIrcClient.default_username = 'username'
// WsIrcClient.default_nick_prefix = 'web-'

let irc_client = new WsIrcClient({
  server: "irc.someircwebsocket.com",
  port: 7669,
  is_ssl: true,
  debug: true
})
  .onmessage(function (channel, from, message) {
    console.log(`${channel} -> ${from}: ${message}`)
    this.send(channel, "${from}: I'm running on someone's browser")
  })
  .onconnect(function () {
    this.join(irc_channel)
    this.send(channel, "Hello folks!")
  })
  .onjoin(function (channel) {
    console.log(`Joined ${channel}`)
  })
  .onpart(function (channel) {
    console.log(`Leaving ${channel}`)
  })
  .onnames(function (channel, names) {
    console.log(channel + " - Names: " + names.join(" "))
  })
  .onnickinuse(function () {
    console.log("That nickname is already in use!")
  })
  .onnickchange(function (nick) {
    console.log(`You are now know as: ${nick}`)
  })
  .connect()

  // You can keep using client methods from here...
```
