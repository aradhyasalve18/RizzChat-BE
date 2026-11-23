# RizzChatzz — Backend
Backend server for **RizzChatzz**, a real-time chat and photo-sharing web application.
The backend provides REST APIs for uploading, retrieving and deleting photos, along with real-time messaging and message history using Socket.IO.

## Tech Stack
Technology and its Purpose
Node.js for JavaScript runtime
Express.js for REST API server
MongoDB for Message and photo metadata storage
Socket.IO for Real-time messaging
Cloudinary for Image upload and cloud storage
Multer for Multipart file upload handling
CORS for Cross-origin frontend communication

## Features
- Real-time messaging between connected users
- Retrieve previously stored messages
- Store chat messages in MongoDB
- Upload photos with captions and usernames
- Store uploaded images using Cloudinary
- Retrieve uploaded photo details
- Delete photo records and associated Cloudinary assets

## Architecture
```text
React Frontend
      |
      | REST API
      | Socket.IO
      |
Express.js Backend
      |
      ├── MongoDB
      │    ├── messages
      │    └── files
      │
      ├── Socket.IO
      │    └── Real-time messaging
      │
      └── Cloudinary
           └── Image uploads
```
## API Endpoints
### Photo Upload
**POST `/uploads`**
Uploads an image to Cloudinary and stores its metadata in MongoDB.
Request type: `multipart/form-data`
Field and Description
`file`  Image file 
`username`  Username of the uploader 
`caption`  Photo caption
Supported image formats include JPG, JPEG, PNG, GIF and WebP.
### Get Uploaded Photos
**GET `/files`**
Returns the stored photo records from the MongoDB `files` collection.
### Delete Photo
**DELETE `/delete/:id`**
Deletes a photo record from MongoDB and requests deletion of the corresponding image from Cloudinary.
## Socket.IO Events
The backend uses Socket.IO for real-time communication.
| Event | Direction | Description 
|---|---|---|
| `connection` | Client → Server | Establishes a socket connection |
| `getHistory` | Client → Server | Requests stored chat messages |
| `history` | Server → Client | Returns message history |
| `message` | Client ↔ Server | Sends and broadcasts a chat message |
| `disconnect` | Client → Server | Handles socket disconnection |
Messages received through the `message` event are stored in MongoDB and broadcast to connected clients.

## Database
MongoDB database: `project1`
Collections:
- `messages` — stores chat messages.
- `files` — stores uploaded photo metadata, including username, caption, Cloudinary URL and file identifier.
## Getting Started
### Prerequisites
- Node.js
- npm
- MongoDB database
- Cloudinary account
### Installation
Clone the repository:
```bash
git clone https://github.com/aradhyasalve18/RizzChat-BE.git
```
Navigate to the backend directory:
```bash
cd RizzChat-BE
```
Install dependencies:
```bash
npm install
```
Create a `.env` file in the backend root directory:
```env
MONGO_URL=your_mongodb_connection_string
CLOUDINARY_CLOUD_NAME=your_cloudinary_cloud_name
CLOUDINARY_API_KEY=your_cloudinary_api_key
CLOUDINARY_API_SECRET=your_cloudinary_api_secret
```
Start the server:
```bash
npm run dev
```
The backend runs on port `3000`.
## Environment Variables
| Variable | Description |
|---|---|
| `MONGO_URL` | MongoDB connection string |
| `CLOUDINARY_CLOUD_NAME` | Cloudinary cloud name |
| `CLOUDINARY_API_KEY` | Cloudinary API key |
| `CLOUDINARY_API_SECRET` | Cloudinary API secret |
Never commit `.env` files or expose credentials in public repositories.
## Frontend Integration
The backend is designed to work with the RizzChatzz React frontend.
Frontend repository:
https://github.com/aradhyasalve18/RizzChat-FE
Live application:
https://rizzchatzz.web.app
The frontend communicates with the backend through HTTP requests and Socket.IO connections.
## Future Improvements
- Add authentication and user authorisation
- Validate and sanitise incoming requests
- Restrict CORS to trusted frontend origins
- Improve error handling and API response consistency
- Add message pagination
- Add environment-based server configuration
- Improve file deletion reliability

**Developed as part of the RizzChatzz full-stack web application.**
