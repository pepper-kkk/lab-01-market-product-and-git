## Product Choice

- **Product:** Telegram
- **Website:** <https://telegram.org/>
- **Description:** Telegram is a cross-platform messaging app for private chats, groups, channels, media sharing, and bots.

## Main components

![Telegram Component Diagram](diagrams/out/telegram/component-diagram/Component%20Diagram.svg)

- [Telegram Component Diagram Code](diagrams/src/telegram/component-diagram.puml)

Select at least 5 components from the diagram and describe them:

1. **Mobile/Web Client** — User-facing app that displays chats and sends requests to the backend.
2. **API Gateway** — Entry point for client requests; routes calls to internal services and applies basic validation.
3. **Auth Service** — Handles login, session management, and user/device authentication.
4. **Messaging Service** — Core chat logic: send/receive messages, read status, chat history.
5. **Media Service** — Upload/download of photos/videos/files; manages media metadata and delivery links.
6. **Notifications Service** — Sends push notifications and manages delivery preferences.  
*(You only need 5 — you can keep 5–6.)*

## Data flow

![Telegram Sequence Diagram](diagrams/out/telegram/sequence-diagram/Sequence%20Diagram.svg)

- [Telegram Sequence Diagram Code](diagrams/src/telegram/sequence-diagram.puml)

### Chosen flow/group: 2. Send Message (with File Ref)

This group describes how a user sends a message that references an already uploaded media file.

- **Mobile App → MTProto Gateway:** `sendMessage(peer=Bob, input_file=file_id_A)` — sends recipient (Bob), message metadata, and a reference to the uploaded media (`file_id_A`) plus session/auth data.
- **MTProto Gateway → Auth Service:** validates the user session/device (auth token, session id).
- **Auth Service → MTProto Gateway:** returns **OK** if the session is valid.
- **MTProto Gateway → Message Service:** forwards the validated send request (peer id + file reference + message content/metadata).
- **Message Service → Sharded DB:** persists the message in inbox/outbox and updates chat state; increments the sequence/counter (**pts**) so clients can sync state consistently.
- **Message Service → MTProto Gateway:** responds **Message Accepted** and assigns a server-side `message_id`.
- **MTProto Gateway → Mobile App:** returns RPC response so the client can render the message as sent and show the final id/status.
- **Mobile App:** updates UI (message appears in the chat).

**Components involved and exchanged data**

- Client/Gateway exchange: `peer_id`, `file_id` reference, message payload/metadata, auth/session data, and response with `message_id` + status.
- Gateway/Auth exchange: session/device identifiers and validation result.
- Message Service/DB exchange: message record, chat state updates, and sequence counter (`pts`).

*Note:* `file_id_A` comes from the previous group **1. Media Upload (Encrypted Parts)** where the media is uploaded in chunks and saved with metadata before being referenced in `sendMessage`

## Deployment

![Telegram Deployment Diagram](diagrams/out/telegram/deployment-diagram/Deployment%20Diagram.svg)

- [Telegram Deployment Diagram Code](diagrams/src/telegram/deployment-diagram.puml)

Briefly describe where the components are deployed:

- **Clients** run on users’ devices (mobile/desktop/web).
- **Gateway/edge** receives traffic and routes it to backend services.
- **Backend services** (auth, messaging, media, notifications) run on server infrastructure and scale horizontally.
- **Datastores** (DB/caches/object storage) are deployed separately with replication for reliability.

## Assumptions

- I assume the API Gateway applies rate limiting and abuse/spam protection before requests reach core services.
- I assume the Media Service relies on caching/CDN and possibly deduplication to optimize delivery and storage costs.

## Open questions

- How exactly is load balancing and service discovery implemented between Telegram’s internal services in production?
- How does the data flow differ for end-to-end encrypted secret chats compared to regular cloud chats?
