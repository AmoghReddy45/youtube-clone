# YouTube Clone Design Document

## Introduction
This document outlines the design of a simplified YouTube clone, created as part of a Full Stack Development course. The objective is not to replicate YouTube in its entirety but to construct a basic version that incorporates YouTube's core functionalities. The focus is on simplicity and learning, rather than creating a production-ready system.

## Background
YouTube is a video-sharing platform enabling users to upload, view, rate, share, and comment on videos. Due to its vast scale and complex features, this project will primarily concentrate on video uploading and viewing.

## Requirements
- Users can sign in/out using their Google account.
- Users can upload videos while signed in.
- Videos should be transcoded to multiple formats (e.g., 360p, 720p).
- Users can view a list and individual videos, regardless of sign-in status.

## High-Level Design
### Components:
1. **Video Storage**: Utilizing Google Cloud Storage for hosting raw and processed videos.
2. **Video Upload Events**: Employing Cloud Pub/Sub for managing video upload events, enhancing durability, and allowing asynchronous video processing.
3. **Video Processing Workers**: Using Cloud Run for transcoding videos with ffmpeg and handling variable workloads.
4. **Video Metadata**: Storing video metadata in Firestore for display purposes.
5. **Video API**: Developing a simple API with Firebase Functions for video uploads and metadata retrieval.
6. **Web Client**: Creating a user interface with Next.js, hosted on Cloud Run, for video uploads and sign-in.
7. **Authentication**: Integrating Firebase Auth for user authentication, particularly with Google Sign-In.

## Detailed Design
### 1. User Sign Up
- Integration of Firebase Auth for Google account sign-ups.
- Creation of Firestore documents for each user, containing additional information.
- Use of Firebase Auth triggers for reliable user document creation.

### 2. Video Upload
- Restricting uploads to authenticated users.
- Generating signed URLs through Firebase Functions for secure uploads to Google Cloud Storage.

### 3. Video Processing
- Implementing Cloud Pub/Sub for managing high-volume uploads and decoupling upload and processing stages.
- Utilizing Cloud Run workers for processing and Firestore for storing video metadata.

## Limitations & Future Work
- Handling of request timeouts and message redelivery limits in Cloud Run and Pub/Sub.
- Absence of checks for illegal content in uploaded videos.
- Detailed exploration of these limitations and potential future enhancements is suggested.

## References
- [Firebase Auth Documentation](https://firebase.google.com/docs/auth)
- [Cloud Storage Signed URLs](https://cloud.google.com/storage/docs/access-control/signed-urls)
- [Pub/Sub Push Subscriptions](https://cloud.google.com/pubsub/docs/push)
- [Integrating Pub/Sub with Cloud Storage](https://cloud.google.com/storage/docs/pubsub-notifications)
- [Using Pub/Sub with Cloud Run](https://cloud.google.com/run/docs/tutorials/pubsub)
