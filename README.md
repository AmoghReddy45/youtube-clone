# YouTube Clone Design Document

## Introduction
This document details the design of a simplified YouTube clone, developed as part of a Full Stack Development course. The project aims to create a basic version of YouTube, focusing on core functionalities and user interaction, emphasizing learning and simplicity.

## Background
YouTube is a vast video-sharing platform that allows for uploading, viewing, rating, sharing, and commenting on videos. This project extends the initial focus on video uploading and viewing to include user engagement features like Likes/Dislikes and a Comment Section.

## Requirements
- Users can sign in/out using their Google account.
- Users can upload videos while signed in.
- Videos are transcoded to multiple formats (e.g., 360p, 720p).
- Users can view a list of uploaded videos and individual videos, with or without signing in.
- Users can like or dislike videos (signed in users).
- Users can comment on videos (signed in users).

## High-Level Design
### Components:
- **Video Storage:** Google Cloud Storage for hosting raw and processed videos.
- **Video Upload Events:** Cloud Pub/Sub manages video upload events for enhanced durability and asynchronous processing.
- **Video Processing Workers:** Cloud Run for transcoding videos using ffmpeg.
- **Video Metadata:** Firestore for storing video metadata.
- **Video API:** Firebase Functions to handle video uploads and metadata retrieval.
- **Web Client:** Next.js-based UI, hosted on Cloud Run, for video uploads and user interactions.
- **Authentication:** Firebase Auth for user authentication with Google Sign-In.
- **Likes/Dislikes System:** A system to manage user likes and dislikes on videos.
- **Comments System:** A platform for users to post and view comments on videos.

## Detailed Design
### 1. User Sign Up
- Integration of Firebase Auth for Google account sign-ups.
- Creation of Firestore documents for each user.

### 2. Video Upload
- Restriction to authenticated users for video uploads.
- Secure upload URLs generated through Firebase Functions.

### 3. Video Processing
- Cloud Pub/Sub for managing high-volume uploads.
- Cloud Run workers for video processing and Firestore for metadata storage.

### 4. Likes and Dislikes
- Implementation of a user interaction system for liking or disliking videos.
- Firestore schema updated to track like and dislike counts.
- API endpoints created for processing likes/dislikes.

### 5. Comment Section
- System for users to post and view comments on videos.
- Extension of Firestore schema to include comments, linked to users and videos.
- Updated API and frontend for comment management.

## Limitations & Future Work
- Timeouts and message redelivery limits in Cloud Run and Pub/Sub.
- No current system to check for illegal content in uploaded videos.
- Future enhancements to explore: advanced comment moderation and refined likes/dislikes system.

## References
- [Firebase Auth Documentation](https://firebase.google.com/docs/auth)
- [Cloud Storage Signed URLs](https://cloud.google.com/storage/docs/access-control/signed-urls)
- [Pub/Sub Push Subscriptions](https://cloud.google.com/pubsub/docs/push)
- [Using Pub/Sub with Cloud Storage](https://cloud.google.com/storage/docs/pubsub-notifications)
- [Using Pub/Sub with Cloud Run](https://cloud.google.com/run/docs/tutorials/pubsub)
