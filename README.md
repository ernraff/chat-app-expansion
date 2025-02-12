# Multi-Chat Implementation Plan

## Overview
This project aims to extend an existing ai moderated single-chatroom application into a multi-chatroom system, allowing users to join or create different chat rooms, similar to modern chat applications like WhatsApp, Discord, or Slack.

## Goals
- Users can create, join, and leave multiple chat rooms.
- A home screen where users can see a list of available chat rooms.
- Each chat room functions independently, with its own message history and participants.
- Messages are stored and retrieved for each chat room separately.

---

## Architecture
### Backend (Node.js + Express + MongoDB)
1. **User Authentication**
   - Users authenticate via JWT tokens.
   - User information is stored in MongoDB.

2. **Chat Rooms Management**
   - A `ChatRoom` model will be introduced with:
     ```js
     {
       _id: ObjectId,
       name: String,
       members: [userId],
       createdAt: Date,
       updatedAt: Date
     }
     ```
   - Users can create and join rooms, and a user can be in multiple rooms.

3. **Message Storage**
   - Messages will reference a specific chat room:
     ```js
     {
       _id: ObjectId,
       roomId: ObjectId,
       senderId: ObjectId,
       content: String,
       timestamp: Date
     }
     ```
   - Messages are only retrieved for the room a user is currently in.

4. **Socket.io for Real-Time Messaging**
   - Emit and receive messages based on the `roomId`.
   - Broadcast only to users in the same room.

### Frontend (React + Next.js + Socket.io-client)
1. **Home Screen**
   - Displays a list of available chat rooms.
   - Allows users to create new rooms.

2. **Chat Room UI**
   - Displays messages relevant to the selected room.
   - Users can send messages in the active chat room.

3. **Navigation Between Chats**
   - Users can switch between different chat rooms seamlessly.

---

## Implementation Plan
### Phase 1: Setup Backend for Multi-Room Support
- Modify database schema to include `ChatRoom` model.
- Update user model to store joined rooms.
- Update message storage to reference `roomId`.
- Adjust WebSocket (Socket.io) logic to handle multiple rooms.

### Phase 2: Update Frontend UI
- Create a home screen displaying available chat rooms.
- Implement navigation between chat rooms.
- Allow users to create or join chat rooms.
- Update the chat UI to show messages for the selected room.

### Phase 3: Secure & Optimize
- Add authentication checks for chat access.
- Optimize database queries for message retrieval.
- Implement basic UI improvements for usability.

---

## Future Enhancements
- Implement private chat rooms.
- Allow direct messages between users.
- Enable push notifications for new messages.
- Improve UI/UX with animations and themes.

---

## Repository Information
This repository is meant for planning and documentation purposes. The actual implementation will be pushed to the original repo.
