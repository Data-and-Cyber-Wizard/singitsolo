## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Technologies Used](#technologies-used)
- [Installation](#installation)
- [Usage](#usage)
- 
- [API Documentation](#api-documentation)
- [Database Schema](#database-schema)
- [App Flow](#app-flow)

## Overview

**Sing It Solo** is a cloud-based karaoke application built to enhance the karaoke experience for both venues and patrons. Specifically designed for restaurants, bars, and other event spaces, this app provides a seamless karaoke system where users can engage in fun and competitive singing sessions. It allows users to select songs, join a queue, and interact with fellow singers and the audience. 

The application brings a unique twist to traditional karaoke by incorporating a voting system and a rewards mechanism, allowing users to earn points based on audience votes. These points can then be redeemed for various rewards within the venue, such as a free drink, side dish, or meal. 

### Key Features:
1. **User Registration & Sign-in**: Users can easily create accounts and sign in to the platform to start interacting with the karaoke system.
2. **Song Selection & Queue**: Users can browse through a comprehensive list of available songs, select their desired song, and add themselves to the "going to sing" queue.
3. **Karaoke Queue**: The app dynamically updates to show which users are currently singing, what song they are performing, and the order of upcoming singers.
4. **Karaoke Lyrics Display**: While a user is singing, the app provides a live, synchronized lyrics display in karaoke format, with words highlighted to match the rhythm of the song.
5. **Voting System**: After a singer finishes their performance, users can vote for them. Positive votes will reward the singer with points.
6. **Points & Rewards**: The points earned by users through voting can be redeemed for rewards such as drinks, food, or other items at the venue.
7. **Push Notifications**: When it's a user's turn to sing, the app sends a push notification to alert them. The user can then check in, confirm their intent to sing, and begin their performance when ready.
8. **Venue Interaction**: The app is designed to be used both on patrons' mobile devices and the venue's screen(s). The synchronized lyrics display is shown in karaoke format on the venue’s device to complement the user experience.

### App Flow:
1. **User Registration/Sign-in**: Users sign up or log into the app using their credentials.
2. **Song Selection**: Users browse the song catalog, select a song, and add themselves to the "queue" of singers.
3. **Queue Management**: The app shows users who is currently singing, and who is up next.
4. **Karaoke Performance**: When it’s their turn, users receive a push notification, check in, and tap the "Start Song" button to begin their performance.
5. **Voting**: After the performance, audience members vote on the singer's performance, allowing them to earn points.
6. **Points Redemption**: The points accumulated through voting can be used to redeem rewards at the venue.

**Sing It Solo** aims to modernize and gamify the karaoke experience, creating an engaging and interactive environment that benefits both the venue and its patrons. By offering rewards, an engaging queue system, and synchronized karaoke lyrics, it turns every karaoke session into a fun and competitive event that users will want to come back to.

### Target Audience
- **Restaurants**: Enhance the dining experience with fun karaoke nights.
- **Bars and Pubs**: Create a social environment where guests can participate in karaoke events and earn rewards.
- **Event Venues**: Perfect for venues looking to host karaoke contests or social events.

### Technologies-Used
**Technologies for "Sing It Solo"**

For building a cloud-based karaoke application like **Sing It Solo**, we need a tech stack that allows for scalability, real-time updates, push notifications, and seamless integration of mobile and venue systems. Here's a suggested tech stack for both the front-end and back-end:

#### **Frontend (User Interface)**
- **Mobile (iOS/Android)**: 
  - **React Native** or **Flutter** (for cross-platform mobile app development)
    - These frameworks allow us to write the app once and deploy it on both iOS and Android, which is ideal for a karaoke app that needs to be available across different mobile devices.
  - **Native Android** (Java/Kotlin) and **Native iOS** (Swift) (optional, if you prefer platform-specific development)
  
- **Real-Time Updates (Lyrics Synchronization, Voting, Queue Updates)**: 
  - **Socket.io** (for WebSockets in React Native or Flutter, to handle real-time communication)
    - To synchronize lyrics, voting, and queue updates across multiple users and the venue system in real-time.

#### **Backend (Server-Side)**
- **Node.js** with **Express.js**
  - **Node.js** is lightweight and scalable, ideal for real-time applications like karaoke. **Express.js** provides a fast and minimal backend framework for handling requests, user management, and communication.
  
- **Database**: 
  - **MongoDB** (for flexible, scalable, document-based storage of user data, song selections, queues, etc.)
    - MongoDB's flexible schema fits well with changing data like user profiles, song histories, and votes. It's also highly scalable, which will be important as your app grows.
  - Alternatively, **PostgreSQL** can be used if we prefer an SQL-based relational database with more structured relationships between entities.
  
- **Real-Time Event Handling**:
  - **Socket.io** (for real-time bi-directional communication between the server and mobile devices, ensuring the live lyrics, voting, and queue statuses are always updated instantly)

- **Push Notifications**:
  - **Firebase Cloud Messaging (FCM)** or **OneSignal**
    - Firebase Cloud Messaging (FCM) will allow us to send push notifications to users when it's their turn to sing or when other important events happen in the app.

- **Authentication**:
  - **Firebase Authentication** or **Auth0**
    - These provide ready-made solutions for user authentication and authorization. Firebase Authentication supports multiple login providers like Google, Facebook, and email/password.
  
- **File Storage**:
  - **Amazon S3** or **Google Cloud Storage**
    - These are used to store music files, images, or other media content (e.g., song covers, user profiles).

#### **Venue Management System (for Screens in Venues)**
- **React.js** or **Vue.js**
  - The venue system, which will run on a larger screen in the venue, can be developed using a front-end JavaScript framework like React or Vue.js. These frameworks allow for real-time updates to be pushed to the venue's screen, showing lyrics and queue management live.

#### **Cloud Infrastructure**
- **AWS** (Amazon Web Services) or **Google Cloud**
  - For hosting the backend, APIs, and real-time services (with **AWS EC2** for scalable server instances, **AWS S3** for file storage, and **AWS RDS** or **DynamoDB** for database services).
  - Alternatively, **Google Cloud Platform (GCP)** offers similar cloud infrastructure services.

#### **CI/CD and Deployment**
- **GitHub Actions**, **CircleCI**, or **Travis CI** for Continuous Integration and Continuous Deployment pipelines.
- **Docker** for containerizing the backend services, ensuring smooth and consistent deployments.
- **Heroku** or **AWS Elastic Beanstalk** for easy deployment of your backend services.

---

### Database-Schema

Below is a potential database schema for **Sing It Solo**, with collections/tables designed for users, songs, queues, votes, and rewards. We'll use **MongoDB** as an example, given its flexibility with document-based data.

#### **Users Collection**
Stores user data, authentication details, and points accumulated from votes.

```json
{
  "_id": ObjectId("unique_user_id"),
  "username": "john_doe",
  "email": "john@example.com",
  "password_hash": "hashed_password",
  "profile_picture": "url_to_profile_image",
  "points": 120,                   // Accumulated points for rewards
  "songs_sung": [
    { 
      "song_id": ObjectId("song_id"),
      "date_sung": ISODate("2025-01-22T18:00:00Z"),
      "rating": 4,                // Rating given by users after performance
    }
  ],
  "queue_position": 3,              // The user's position in the queue
  "active_song": ObjectId("song_id")  // Current song being sung
}
```

#### **Songs Collection**
Stores the songs available in the karaoke catalog.

```json
{
  "_id": ObjectId("unique_song_id"),
  "title": "Bohemian Rhapsody",
  "artist": "Queen",
  "duration_seconds": 354,         // Duration in seconds
  "lyrics": "url_to_lyrics_text_or_file",
  "song_file": "url_to_song_audio_file",
  "genre": "Rock",
  "popularity": 1500,               // Number of times sung
  "added_on": ISODate("2025-01-01T00:00:00Z")
}
```

#### **Queue Collection**
Tracks the order in which users will sing their selected songs.

```json
{
  "_id": ObjectId("unique_queue_entry_id"),
  "user_id": ObjectId("unique_user_id"),
  "song_id": ObjectId("unique_song_id"),
  "queued_at": ISODate("2025-01-22T18:05:00Z"),
  "status": "waiting"              // "waiting", "singing", "finished"
}
```

#### **Votes Collection**
Tracks votes given to singers after each performance.

```json
{
  "_id": ObjectId("unique_vote_id"),
  "user_id": ObjectId("voter_user_id"),
  "singer_user_id": ObjectId("singer_user_id"),
  "song_id": ObjectId("song_id"),
  "vote_score": 4,                 // Rating out of 5
  "timestamp": ISODate("2025-01-22T18:15:00Z")
}
```

#### **Rewards Collection**
Keeps track of rewards that can be redeemed based on points.

```json
{
  "_id": ObjectId("unique_reward_id"),
  "reward_name": "Free Drink",
  "points_required": 100,
  "redeemed_by": [
    ObjectId("user_id")            // User who redeemed the reward
  ],
  "available_at": ObjectId("venue_id")  // Which venue this reward is available at
}
```

#### **Venues Collection**
Stores information about venues that use the app.

```json
{
  "_id": ObjectId("unique_venue_id"),
  "name": "Karaoke Bar",
  "location": "123 Main St, Cityville",
  "active": true,
  "rewards": [
    { "reward_id": ObjectId("reward_id"), "quantity": 10 }
  ],
  "user_queue": [ 
    { "user_id": ObjectId("user_id"), "queue_position": 1 }
  ],
  "screen_display": {
    "lyrics_sync_url": "url_to_live_lyrics_sync_feed",
    "current_song": ObjectId("song_id")
  }
}
```

#### **Push Notifications Collection**
Stores push notification events for users.

```json
{
  "_id": ObjectId("unique_push_id"),
  "user_id": ObjectId("user_id"),
  "message": "It's your turn to sing!",
  "sent_at": ISODate("2025-01-22T18:00:00Z"),
  "status": "sent"                 // "sent", "delivered", "opened"
}
```

### Relationships Between Collections:
- **Users** can have many **songs_sung** and **votes**.
- **Songs** are selected by **users** and are associated with many **votes**.
- **Queue** entries link a **user** to a **song**.
- **Votes** are stored after each performance to provide feedback for the singer.
- **Rewards** are redeemed by **users** who have earned enough points, and the availability is tied to a specific **venue**.

### Next Steps for Implementation:
- Implement user authentication and registration.
- Set up real-time communication for syncing the song lyrics and queue status.
- Integrate the voting system and points-based rewards.
- Deploy the backend to a cloud provider like AWS or GCP.
- Build the mobile and venue UI using React Native or Flutter for mobile and React/Vue.js for the venue display.

With this architecture and schema, you're set to start building out the features and expanding them as the app grows!3
