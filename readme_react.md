
# **Odyssey**

This Readme Documents the Frontend of the Odyssey Messaging App. The Backend is documented in the [Odyssey API Readme]($$$$$$$$$$$).

## **Introduction**
This is a messaging application built with React and integrated with a robust backend API. The app enables users to engage in one-on-one and group conversations, share multimedia, and stay connected with friends and colleagues. The app emphasizes real-time messaging, ease of use, and clean UI, making it ideal for a wide variety of users.

## **Table of Contents** <!--omit from TOC--->
- [**Odyssey**](#odyssey)
  - [**Introduction**](#introduction)
  - [**Table of Contents** \<!--omit from TOC---\>](#table-of-contents---omit-from-toc---)
    - [**1. Features**](#1-features)
    - [**2. User Stories**](#2-user-stories)
    - [**3. Automatic Testing**](#3-automatic-testing)
    - [**4. Installation**](#4-installation)
    - [**5. Usage**](#5-usage)
    - [**6. Acknowledgement and Credits**](#6-acknowledgement-and-credits)

---

### **1. Features**
- **Real-Time Messaging**: Engage in instant messaging with individuals or groups.
- **Message List**: View and scroll through a list of your active conversations.
- **Detailed Conversations**: Dive into specific messages within conversations, including media sharing.
- **Message Forms**: Easily send new messages in active conversations or start new conversations with others.
- **Responsive Design**: Built using `react-bootstrap`, ensuring the app looks great on any device.
- **Profile and Posts**: In addition to messaging, the app includes features for user profiles and posts, creating a social experience.

### **2. User Stories**
- **As a user**, I can sign up and log into the app to access my personalized messaging dashboard.
- **As a user**, I can view a list of all my ongoing conversations and quickly access any of them.
- **As a user**, I can start a new conversation with another user by sending the first message.
- **As a user**, I can send and receive messages in real-time within an ongoing conversation.
- **As a user**, I can view detailed information about a conversation, including its history and any attached media.

### **3. Automatic Testing**
- The app includes automatic tests for core components and functionality using testing frameworks like Jest. 
- To run tests, use the following command:
  ```bash
  npm test
  ```
- Tests cover components like message forms, message lists, and detail views to ensure the integrity of the app's messaging functionality.

### **4. Installation**
To get the app up and running locally, follow these steps:

1. **Clone the repository**:
   ```bash
   git clone <repository-url>
   ```
2. **Install dependencies**:
   Navigate to the project directory and install the required dependencies:
   ```bash
   npm install
   ```
3. **Install correct node version**:
   Run the following command to start the React app locally:
   ```bash
   nvm install 16
   ```
4. **Run build**:
   Run the following command to build the React app locally:
   ```bash
   npm run build
   ```
5. **Start the development server**:
   Run the following command to start the React app locally:
   ```bash
   npm start
   ```

### **5. Usage**
Once the app is running, navigate to the messaging section where you can:
- **View Message Lists**: Access all your conversations in a list format.
- **View Message Details**: Click on any conversation to see the detailed messages.
- **Send New Messages**: Use the provided forms to send new messages in ongoing conversations or to start a new chat.
- **Responsive Interface**: The app adjusts seamlessly across devices due to the usage of `react-bootstrap`.

### **6. Acknowledgement and Credits**
- Special thanks to the contributors to React and Bootstrap for providing an excellent development framework.
- Thanks to [Axios](https://github.com/axios/axios) for handling HTTP requests and enabling smooth API interactions.
