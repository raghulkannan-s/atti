# AI-Powered Realtime Communication Platform (Mobile + Backend)

## Goal

Build a production-style mobile application with:

* Authentication
* 1-to-1 Chat
* Group Chat
* Audio Calls
* Video Calls
* AI Meeting Summaries
* AI Task Extraction
* Notifications
* Admin Controls

---

# Tech Stack

## Frontend

```text
React Native
Expo
TypeScript
Socket.IO Client
React Navigation
```

## Backend

```text
Java
Spring Boot

Spring Security
JWT Authentication
Spring Data JPA
Spring WebSocket
```

## Database

```text
PostgreSQL
```

## Realtime

```text
WebSocket
Socket.IO (or STOMP WebSocket)
```

## Calls

```text
WebRTC
```

## AI

```text
Gemini API
or
OpenAI API

Whisper (Speech-To-Text)
```

## Storage

```text
AWS S3
or
Cloudinary
or
MinIO
```

---

# High Level Architecture

```text
┌─────────────────────┐
│   React Native App  │
└──────────┬──────────┘
           │
           │ REST API
           │ WebSocket
           ▼
┌─────────────────────┐
│    Spring Boot      │
│                     │
│ Authentication      │
│ Chat Service        │
│ Group Service       │
│ Call Service        │
│ AI Service          │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│    PostgreSQL       │
└─────────────────────┘

           │
           ▼

┌─────────────────────┐
│ Gemini / OpenAI     │
│ Whisper             │
└─────────────────────┘
```

---

# Database Modules

## User

```text
id
name
email
password
avatar
createdAt
```

---

## Conversation

```text
id
type

PRIVATE
GROUP

createdAt
```

---

## ConversationMember

```text
id
conversationId
userId
role

ADMIN
MEMBER
```

---

## Message

```text
id
conversationId
senderId

TEXT
IMAGE
FILE
AI_SUMMARY

content

createdAt
```

---

## Call

```text
id
conversationId

AUDIO
VIDEO

startedAt
endedAt
duration
```

---

## CallRecording

```text
id
callId
audioUrl
```

---

## AiSummary

```text
id
callId
summary
actionItems
createdAt
```

---

# PHASE 1

# Authentication Module

## Features

```text
Register
Login
Logout

JWT Authentication
Refresh Token
Profile
```

## APIs

```text
POST /auth/register

POST /auth/login

GET /user/me

PUT /user/profile
```

---

# PHASE 2

# Chat Module

## Features

```text
1-to-1 Chat

Send Message

Receive Message

Message History

Typing Indicator

Online Status
```

## Flow

```text
User A
    |
    |
WebSocket
    |
    |
User B
```

## APIs

```text
GET /conversations

GET /messages

POST /messages
```

---

# PHASE 3

# Group Module

## Features

```text
Create Group

Add Members

Remove Members

Group Admin

Group Avatar

Group Information
```

## Flow

```text
Admin
   |
Create Group
   |
Add Members
   |
Realtime Updates
```

---

# PHASE 4

# Media Module

## Features

```text
Image Upload

File Upload

Download Files

Preview Media
```

## Storage

```text
Cloudinary

or

S3
```

---

# PHASE 5

# Notifications

## Features

```text
Push Notification

Message Notification

Call Notification
```

## Stack

```text
Firebase Cloud Messaging
```

---

# PHASE 6

# Audio Calling

## Features

```text
1-to-1 Audio Call

Accept Call

Reject Call

Mute

End Call
```

## Flow

```text
Caller
   |
Offer
   |
Spring Boot Signaling
   |
Answer
   |
Receiver
```

```text
Media

User A ←→ User B
```

---

# PHASE 7

# Video Calling

## Features

```text
1-to-1 Video Call

Camera Toggle

Mic Toggle

Speaker Toggle

Switch Camera
```

## Flow

```text
WebRTC

Offer
Answer
ICE Candidate

Peer Connection
```

---

# PHASE 8

# Group Video Calls

## Features

```text
Multiple Participants

Join Call

Leave Call

Mute

Camera Control
```

## Architecture

```text
Participants

       SFU

A ──┐
B ──┼── Media Server
C ──┘
```

Use later:

```text
LiveKit

or

Jitsi
```

Do NOT build SFU yourself.

---

# PHASE 9

# Call Recording

## Features

```text
Record Audio

Store Recording

Attach To Call
```

## Flow

```text
Call

↓

Recording

↓

Storage
```

---

# PHASE 10

# AI Meeting Summary

## Goal

Generate summary after call.

## Flow

```text
Call Ends

↓

Audio Recording

↓

Whisper

↓

Transcript

↓

Gemini/OpenAI

↓

Summary

↓

Store Summary

↓

Send To Chat
```

## Output

```text
Meeting Summary

Topics:
- Authentication
- Chat Module

Action Items:
- Raghul -> Build Login
- Client -> Provide Assets
```

---

# PHASE 11

# AI Task Extraction

## Goal

Extract tasks automatically.

## Flow

```text
Transcript

↓

AI

↓

Tasks
```

## Example

```text
Raghul:
I will complete login tomorrow

↓

Task Created

Title:
Login Module

Owner:
Raghul

Due:
Tomorrow
```

---

# PHASE 12

# AI Chat Assistant

## Features

```text
@ai summarize

@ai explain

@ai create tasks

@ai generate meeting notes
```

## Flow

```text
User

↓

Message

↓

AI Service

↓

Response
```

---

# PHASE 13

# AI Chat Summaries

## Goal

Summarize long group discussions.

## Example

```text
500 Messages

↓

AI

↓

Summary
```

Output:

```text
Topics Discussed

Pending Tasks

Important Decisions
```

---

# PHASE 14

# Admin Module

## Features

```text
Block User

Delete Group

Manage Reports

Monitor Usage
```

---

# Final Folder Structure

```text
backend

src/main/java

├── auth
│
├── user
│
├── chat
│
├── conversation
│
├── group
│
├── websocket
│
├── call
│
├── recording
│
├── notification
│
├── ai
│
├── storage
│
├── common
│
└── config
```

---

# Build Order

```text
1. Authentication

2. Chat

3. Group Chat

4. Media Upload

5. Notifications

6. Audio Calls

7. Video Calls

8. Call Recording

9. AI Summary

10. AI Task Extraction

11. AI Assistant

12. AI Chat Summary

13. Admin Module
```
