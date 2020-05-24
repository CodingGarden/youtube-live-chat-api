# Youtube Live Chat API

* Socket.io API wrapper around the YouTube live chat API.
* Messages are stored in Mongo DB.

## Socket Events

```js
const socket = io('http://path-to-server');
// emitted when there are new messages, is an array of messages
socket.on('messages', (messages) => {
  console.log(messages);
});
```

## Endpoints

* Start listening for messages
  * `GET /listen`
    * Will start listening for chat messages and emitting socket events in for first live event found
    * Will return false if there are no live events
* Get a list of all youtube events
  * `GET /events`
* Get a list of all live chat messages
  * `GET /messages`
* Filter messages by liveChatId (obtain id from events endpoint)
  * `GET /messages?liveChatId=some-liveChatId-from-active-events-endpoint-to-filter-messages`
* Filter messages by some regex against the message
  * `GET /messages?q=any-valid-regular-expression-to-filter-messages`

## Configuration

* Copy `.env.sample` to `.env` and update accordingly

#### Required

Variables needed to listen for messages:

| Variable | Description|
| :--- | :--- |
| MONGO_URI | Mongo DB URL, used to store chat messages |
| GOOGLE_API_KEY | Google API Key, used to retrieve messages |
| YOUTUBE_CHANNEL_ID | The channel to listen for messages |

### Extra

If you would like to _send_ messages as well, the following variables are required:

| Variable | Description|
| :--- | :--- |
| GOOGLE_REFRESH_TOKEN | Oauth refresh token |
| GOOGLE_CLIENT_ID | Oauth client id |
| GOOGLE_CLIENT_SECRET | Oauth client secret |

## Client

See the [example-client](./example-client/index.html) for socket.io client usage.
