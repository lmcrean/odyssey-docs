<center>

# **Odyssey** <!-- omit from toc -->

This

</center>

---

# 1. **Features**

## 1.1. Messaging

- **Real-Time Messaging**: Engage in instant messaging with individuals or groups.

- **Message List**: View and scroll through a list of your active conversations.

- **Detailed Conversations**: Dive into specific messages within conversations, including media sharing.
- **Message Forms**: Easily send new messages in active conversations or start new conversations with others.

## 1.2. Posts 

- Users can create posts and share them with their followers.
- They can share images and text in their posts.

## 1.3. User Authentication

- Users can sign up and log into the app to access their personalized dashboard.

## 1.4. Profiles

- Users can view detailed profiles of other users, which lists their posts
- Users can customise their own profiles with a profile picture and bio.
- The profile picture appears on posts and in the message section.

## 1.5. Follows and Likes

- Users can follow other users and like their posts.
- 

# 2. **User Experience**

## 2.1. User Stories (Strategy and Scope Plane)
The user stories are covered in the Agile Methodology.

- **As a user**, I can sign up and log into the app to access my personalized messaging dashboard.
- **As a user**, I can view a list of all my ongoing conversations and quickly access any of them.
- **As a user**, I can start a new conversation with another user by sending the first message.
- **As a user**, I can send and receive messages in real-time within an ongoing conversation.
- **As a user**, I can view detailed information about a conversation, including its history and any attached media.

## 2.2. Structure of the Application


```mermaid
flowchart TD
subgraph NavbarSignedout["NavbarSignedOut (signed out user)"]
        NC["Home Feed"]
        NA["Sign In"]
        NB["Sign Up"]
  end
 subgraph Navbar["Navbar (signed in user)"]
        A["Home Feed"]
        B["Create Post"]
        C["Messages"]
        D["Profile"]
        E["Logout"]
  end
 subgraph PostsList["Posts List"]
        F["Posts List"]
        G["Like Post"]
        I["View Post"]
        L["Popular Profiles"]
        M["User Avatar"]
  end
 subgraph PostsDetail["Posts Detail"]
        AA["Post Detail"]
        AB["Add Comment"]
        AC["View Comment"]
        AE["Like Post"]
        AF["User Avatar"]
  end
 subgraph ProfileSection["Profile Section"]
        N["Profile Page"]
        NO{"is Profile == self?"}
        NN["yes"]
        O["Edit Username"]
        P["Edit Password"]
        Q["Edit Profile"]
        R["Popular Profiles"]
        NI["no"]
        NM["message"]
        NF["follow"]
  end
 subgraph MessageList["Messages List"]
        S["Messages List"]
        T["View Message"]
  end
 subgraph MessageDetail["Message Detail"]
        V["Message Detail"]
        W["Send Message"]
        X["Unique Message"]
        Y["go back"]
  end
 subgraph PopularProfiles["Popular Profiles Component"]
        VV["User"]
        WW["Send Message"]
        XX["Follow"]
  end
    AI(("start")) --> NA & NB & NC
    NB --> NA
    NA --> A
    A & NC --> F
    B --> F
    D --> N
    C --> S
    I --> AA
    F --> G & L & M & I
    N --> NO & R
    NO --> NN & NI
    NN --> O & P & Q
    NI --> NM & NF
    AA --> AB & AC & AE & AF
    S --> T
    T --> V
    V --> W & X & Y
    L --> VV
    R --> VV
    VV --> WW & XX
    M --> N
    AF --> N
    WW --> V
    NM --> V
    Y --> S
    style AA fill:#AA00FF
    style AC fill:#AA00FF
    style X fill:#AA00FF
    style Navbar fill:#00C853,color:#000000
    style NavbarSignedout fill:#00C853,color:#000000
    style PostsList fill:#FFD600,color:#000000
    style PostsDetail fill:#FFD600,color:#000000
    style MessageList fill:#BBDEFB,color:#000000
    style MessageDetail fill:#BBDEFB,color:#000000
    style ProfileSection fill:#FFCDD2,color:#000000
    style PopularProfiles fill:#FFCDD2,color:#000000
```


Website Navigation for signed in user

Purple indicates that the user can EDIT or DELETE the content, providing they are the owner.

Authentication was omitted from the diagram for readability. To summarise:
- The signed out Navbar offers option to SIGN IN or SIGN UP.
- Once signed in, the user can sign out in the navbar.
- A signed out user
  - cannot access messages
  - cannot see options for like or follow
  - cannot create or edit a post

### 2.2.1. Inputs and Validation

| Feature | Input Fields | Frontend Validation | Backend Validation |
|---------|--------------|---------------------|---------------------|
| Sign Up | - Username (required)<br>- Password (required)<br>- Password confirmation (required) | File: `frontend/src/pages/auth/SignUpForm.js`<br>- Checks for field completion<br>- Displays server-side errors <br>- Field may not be blank <br> -Username cannot contain spaces <br> - displays Bootstrap Alerts such as `{errors.non_field_errors?.map((message, idx) => ( <Alert key={idx} > {message} </Alert> ))}` | Files: `drf_api/settings.py`, `drf_api/serializers.py`<br>- Uses default dj-rest-auth registration validators with `AUTH_PASSWORD_VALIDATORS`<br>- Creates profile via signal in drf_api app<br>- Django's default password validators apply, quoted here from docs: <br><br> - **UserAttributeSimilarityValidator**: Checks the similarity between the password and a set of attributes of the user.<br>- **MinimumLengthValidator**: Checks whether the password meets a minimum length. This validator is configured with a custom option: it now requires the minimum length to be nine characters, instead of the default eight.<br>- **CommonPasswordValidator**: Checks whether the password occurs in a list of common passwords. By default, it compares to an included list of 20,000 common passwords.<br>- **NumericPasswordValidator**: Checks whether the password isn’t entirely numeric.|
| Sign In | - Username (required)<br>- Password (required) | File: `frontend/src/pages/auth/SignInForm.js`<br>- Checks for field completion<br>- Handles authentication errors that may arise from `dj-rest-auth` in the API | File: `drf_api/urls.py`<br>- Uses dj-rest-auth for login<br>-`dj-rest-auth` framework uses Django's [`authenticate()` method](https://docs.djangoproject.com/en/5.1/topics/auth/default/#django.contrib.auth.authenticate) to ensure username and password match the database.
| Create Post | - Title (required)<br>- Content (optional)<br>- Image (optional) | File: `frontend/src/pages/posts/PostCreateForm.js`<br>- Checks title is not empty<br>- Client-side image preview | Files: `posts/serializers.py`, `posts/models.py`<br>- Validates image size (max 2MB) and dimensions (max 4096px in width or height)<br>- Handles image upload to Cloudinary<br>- Uses function to get default image if none provided |
| Send Message | - Content (required for text)<br>- Image (optional) | File: `frontend/src/pages/messaging/MessageDetailSendForm.js`<br>- Ensures content or image is present<br>- Handles image upload | Files: `messaging/views/message_detail_send_view.py`, `messaging/serializers.py`<br>- Validates message creation and recipient existence<br>- Validates content is not blank when no image<br>- Validates image upload (max 5MB, file type) |
| Update Profile | - Name (optional)<br>- Content/Bio (optional)<br>- Image (optional) | File: `frontend/src/pages/profiles/ProfileEditForm.js`<br>- Handles image upload and preview | File: `profiles/serializers.py`<br>- Validates image upload to Cloudinary<br>- No explicit validation on name and content fields |
| Like/Unlike Post | - No input (toggle action) | File: `frontend/src/pages/posts/Post.js`<br>- UI toggle for like/unlike<br>- Updates like count | Files: `likes/models.py`, `likes/serializers.py`, `likes/views.py`<br>- Ensures uniqueness with `unique_together` in model<br>- `LikeSerializer` handles uniqueness in create method<br>- Handles creation and deletion of Like objects |
| Follow/Unfollow User | - No input (toggle action) | File: `frontend/src/pages/profiles/Profile.js`<br>- UI toggle for follow/unfollow | Files: `followers/models.py`, `followers/serializers.py`, `followers/views.py`<br>- Ensures uniqueness with `unique_together` in model<br>- `FollowerSerializer` handles uniqueness in create method<br>- Manages Follower object creation and deletion |
| Update Username | - New Username (required) | File: `frontend/src/pages/profiles/UsernameForm.js`<br>- Checks new username is not empty<br>- Displays server-side errors | File: `drf_api/urls.py`<br>- Uses dj-rest-auth for username update<br>- Django's built-in uniqueness validation applies |
| Update Password | - Current Password (required)<br>- New Password (required)<br>- Confirm New Password | File: `frontend/src/pages/profiles/UserPasswordForm.js`<br>- Ensures all fields are filled<br>- Checks new passwords match | File: `drf_api/urls.py`<br>- Uses dj-rest-auth for password change<br>- Django's built-in password validators apply |

Both frontend and backend implement validation to ensure data integrity and security. The frontend provides immediate feedback to users, while the backend performs thorough checks before processing the data. Error messages from the server are caught by the frontend and displayed to the user for a seamless experience.

## 2.3. Skeleton

To make the app, `react-bootstrap` was used for an efficient workflow.

Where possible the app was designed with a mobile-first approach, ensuring that the app is responsive and accessible across devices.

### 2.3.1. UiZard Wireframe

The following UiZard wireframe was used as a starting point for the app's design:

![UiZard Wireframe - Mobile](https://res.cloudinary.com/$$$$$$$$$$$$$$$$$)
Mobile Design

![UiZard Wireframe](https://res.cloudinary.com/$$$$$$$$$$$$$$$$$)
Desktop Design

The wireframe shows the basic layout of the app, including the navbar, message list, and message detail components. The final design was based on this wireframe, with additional features and styling added to enhance the user experience.




### 2.3.2. Responsive Navbar for Mobile and Desktop

for the Navbar a desktop and mobile component was created to ensure a seamless experience across devices. Then through a hook the Navbar would switch according to screenwidth.

## 2.4. Surface

Global vars were used to efficently manage the color scheme and typography.

### 2.4.1. NavBar Design

Figma was used to create a more detailed wireframe for the app, due to time constraints certain components were focused on.

![](assets/media/2024-09-15-20-42-57.png)

### 2.4.2. Color Scheme and Typefaces with Root vars

![](assets/media/2024-09-15-20-44-48.png)

these were used to create a consistent and visually appealing design for the app, as shown in the image the variables stylesheet was used to set the color scheme and typography for the app. This provided an efficient workflow.

### 2.4.3. Light and Dark Mode with ThemeContext

Odyssey implements a dynamic theme switching feature using React Context. This system allows for seamless toggling between light and dark modes across the application. Let's dive into how this is implemented.

The theming system is primarily implemented in the `frontend/src/contexts/ThemeContext.js` file. Here's a breakdown of its key components:

### 2.4.4. ThemeContext

The `ThemeContext` is created using React's `createContext` function:

```javascript
export const ThemeContext = createContext();
```

This context will hold the current theme state and provide a method to toggle it.

### 2.4.5. ThemeProvider

The `ThemeProvider` component is responsible for managing the theme state and providing it to the rest of the application:

```javascript
export const ThemeProvider = ({ children }) => {
  const [lightMode, setLightMode] = useState(() => {
    const savedMode = localStorage.getItem('lightMode');
    return savedMode ? JSON.parse(savedMode) : false;
  });

  const applyTheme = useCallback((isLight) => {
    const root = document.documentElement;

    if (isLight) {
      root.style.setProperty('--color-background', '#FFFFFF');
      root.style.setProperty('--color-secondary-background', '#F0F0F0');
      root.style.setProperty('--color-primary-text', '#333333');
      root.style.setProperty('--color-secondary-text', '#666666');
    } else {
      root.style.setProperty('--color-background', '#121212');
      root.style.setProperty('--color-secondary-background', '#1F1F1F');
      root.style.setProperty('--color-primary-text', '#f0e7e7');
      root.style.setProperty('--color-secondary-text', '#B3B3B3');
    }
  }, []);

  useEffect(() => {
    localStorage.setItem('lightMode', JSON.stringify(lightMode));
    applyTheme(lightMode);
  }, [lightMode, applyTheme]);

  return (
    <ThemeContext.Provider value={{ lightMode, setLightMode }}>
      {children}
    </ThemeContext.Provider>
  );
};
```

Key points:
- The initial theme state is retrieved from localStorage, defaulting to dark mode if not set.
- The `applyTheme` function updates CSS custom properties based on the current theme.
- Theme changes are persisted to localStorage and applied immediately.

**useThemeTransition Hook**

This custom hook provides a way to apply theme transition effects:

```javascript
export const useThemeTransition = () => {
  return { 'data-theme-transition': true };
};
```

**Theme Application**

The theme is applied using CSS custom properties defined in `frontend/src/styles/themeTransitions.css`:

```css
[data-theme-transition] {
  transition: background-color 0.3s ease, color 0.3s ease;
}

:root {
  --color-background: #121212;
  --color-secondary-background: #1F1F1F;
  --color-primary-text: #f0e7e7;
  --color-secondary-text: #B3B3B3;
}
```

These CSS variables are dynamically updated by the `applyTheme` function in the `ThemeProvider`.

Components can access and toggle the theme using the `ThemeContext`. For example, in `frontend/src/components/NavBarDesktop.js`:

```javascript
import React, { useContext } from "react";
import { ThemeContext } from "../contexts/ThemeContext";
import { FontAwesomeIcon } from '@fortawesome/react-fontawesome';
import { faSun, faMoon } from '@fortawesome/free-solid-svg-icons';

const NavBarDesktop = () => {
  const { lightMode, setLightMode } = useContext(ThemeContext);

  const toggleTheme = () => {
    setLightMode(!lightMode);
  };

  return (
    // ... other nav elements ...
    <button onClick={toggleTheme} className={styles.ThemeToggle}>
      <FontAwesomeIcon icon={lightMode ? faMoon : faSun} />
    </button>
    // ... other nav elements ...
  );
};
```

</details>

This implementation allows for a seamless theme switching experience across the Odyssey application, with the current theme persisting between sessions.

# 4. **Installation**

It would be advisable to use the [Gitpod IDE](http://gitpod.io) for the installation process, as it is pre-configured with the necessary tools and dependencies, especially around `nvm` and linking to the API.

To get the frontend app up and running locally, follow these steps:

1. **Clone the repository**:
   ```bash
   git clone http://github.com/lmcrean/odyssey_react.git
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

## 4.1. Note on compiling static files

You will need to re-run this command any time you want to deploy changes to the static files in your project, including the React code. To do this, you need to delete the existing `build` folder and rebuild it.

This command will delete the old folder and replace it with the new one: 

```bash
npm run build && rm -rf ../staticfiles/build && mv build ../staticfiles/.
```

# 5. Agile Methodology

As seperate Readme file is created to cover the Agile Methodology. 

# 6. **Acknowledgement and Credits**

## 6.1. Code Institute Moments app as boilerplate

"Moments" was used as a boilerplate for the project as it contained the necessary features for a social media platform. Both the API and the React frontend were built from this code.
  - Frontend: https://github.com/Code-Institute-Solutions/moments
  - API:  https://github.com/Code-Institute-Solutions/drf-api

## 6.2. Code institute Repo unification tutorial

A key issue with the project was authnetication not working on Safari browsers, due to having seperate repositories with the frontend and API. 

- [Code Institute](https://codeinstitute.net/) provided a tutorial on how to unify the repositories, which was used to fix the issue.

## 6.3. Libraries

Below is a table listing the key dependencies and devDependencies used in this project, along with brief descriptions and links to the documentation that may have been refered.

| Dependency & Version                                          | Description                                                                                                                                                          |
|---------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **@fortawesome/fontawesome-svg-core==^6.6.0**                 | [@fortawesome/fontawesome-svg-core](https://www.npmjs.com/package/@fortawesome/fontawesome-svg-core) is the core package that enables FontAwesome icons in your project. |
| **@fortawesome/free-solid-svg-icons==^6.6.0**                 | [@fortawesome/free-solid-svg-icons](https://www.npmjs.com/package/@fortawesome/free-solid-svg-icons) provides solid style icons from FontAwesome.                     |
| **@fortawesome/react-fontawesome==^0.2.2**                    | [@fortawesome/react-fontawesome](https://www.npmjs.com/package/@fortawesome/react-fontawesome) is a React component library for FontAwesome icons.                    |
| **@testing-library/jest-dom==^5.14.1**                        | [@testing-library/jest-dom](https://www.npmjs.com/package/@testing-library/jest-dom) provides custom jest matchers for DOM node assertions.                           |
| **@testing-library/react==^11.2.7**                           | [@testing-library/react](https://www.npmjs.com/package/@testing-library/react) is a testing utility for React components.                                             |
| **@testing-library/user-event==^12.8.3**                      | [@testing-library/user-event](https://www.npmjs.com/package/@testing-library/user-event) simulates user interactions for testing purposes.                            |
| **axios==^0.21.4**                                            | [axios](https://www.npmjs.com/package/axios) is a promise-based HTTP client for making requests to servers.                                                           |
| **bootstrap==^4.6.0**                                         | [bootstrap](https://www.npmjs.com/package/bootstrap) is a popular front-end framework for building responsive, mobile-first sites.                                    |
| **heroku==^9.1.0**                                            | [heroku](https://www.npmjs.com/package/heroku) is a CLI for interacting with the Heroku platform.                                                                     |
| **jwt-decode==^3.1.2**                                        | [jwt-decode](https://www.npmjs.com/package/jwt-decode) is a small library for decoding JSON Web Tokens (JWT).                                                         |
| **react==^17.0.2**                                            | [react](https://www.npmjs.com/package/react) is a JavaScript library for building user interfaces.                                                                    |
| **react-bootstrap==^1.6.3**                                   | [react-bootstrap](https://www.npmjs.com/package/react-bootstrap) provides Bootstrap components built with React.                                                     |
| **react-dom==^17.0.2**                                        | [react-dom](https://www.npmjs.com/package/react-dom) is the entry point to the DOM and server renderers for React.                                                    |
| **react-infinite-scroll-component==^6.1.0**                   | [react-infinite-scroll-component](https://www.npmjs.com/package/react-infinite-scroll-component) helps implement infinite scrolling in React.                         |
| **react-router-dom==^5.3.0**                                  | [react-router-dom](https://www.npmjs.com/package/react-router-dom) is a library for handling routing in React applications.                                           |
| **react-scripts==4.0.3**                                      | [react-scripts](https://www.npmjs.com/package/react-scripts) provides scripts and configuration used by Create React App.                                             |
| **web-vitals==^1.1.2**                                        | [web-vitals](https://www.npmjs.com/package/web-vitals) is a library for measuring essential web performance metrics.                                                  |
| **@babel/plugin-proposal-private-property-in-object==^7.21.11** | [@babel/plugin-proposal-private-property-in-object](https://www.npmjs.com/package/@babel/plugin-proposal-private-property-in-object) adds support for private properties in objects. This cleared a warning message in the console. |
| **msw==^0.35.0**                                              | [msw](https://www.npmjs.com/package/msw) is a mocking library for intercepting network requests during testing.                                                       |


## 6.4. Broader Software used

| Software & Version | Description                                                                                   |
|--------------------|-----------------------------------------------------------------------------------------------|
| **Node.js**        | [Node.js](https://nodejs.org/en/) is a JavaScript runtime built on Chrome's V8 JavaScript engine. |
| **npm**            | [npm](https://www.npmjs.com/) is the package manager for JavaScript and the world's largest software registry. |
| **nvm**            | [nvm](https://github.com/nvm-sh/nvm) is a version manager for Node.js, allowing you to install and switch between multiple versions of Node.js. |
| **VSCode**         | [VSCode](https://code.visualstudio.com/) is a popular code editor that provides a range of features for efficient coding. |
| **Git**            | [Git](https://git-scm.com/) is a distributed version control system for tracking changes in source code during software development. |
| **GitHub**         | [GitHub](https://github.com/) is a platform for hosting and collaborating on Git repositories, providing tools for version control and project management. |
| **Heroku**         | [Heroku](https://www.heroku.com/) is a cloud platform that enables developers to build, deliver, monitor, and scale applications. |
| **Cloudinary**     | [Cloudinary](https://cloudinary.com/) is a cloud-based image and video management service that provides storage, optimization, and delivery solutions. |
| **PostgreSQL**     | [PostgreSQL](https://www.postgresql.org/) is a powerful, open-source object-relational database system. |
| **Gitpod**         | [Gitpod](https://www.gitpod.io/) is an online IDE that provides a fully equipped workspace for development. |

## 6.5. Use of LLMs

LLMs were used as an AI tool to generate initial drafts which would be meticulously reviewed.

- writing detailed commit messages
- implementation of new features in Javascript, CSS or Python
- drafting readme documentation
- it could be assumed that any file or commit message might have started as an LLM draft which was extensively tested and reviewed.

The limits of LLMs tended to be that they could not generate test-proof code.

The following tools were used to generate such drafts:

- [Claude Sonnet 3.5](http://www.claude.ai/), eventually replacing the use of [GPT-4o](http://www.chatgpt.com/) with it's higher context window of 200,000 tokens.
- [Github Copilot](http://www.github.com/copilot) for inline editing suggestions.

## 6.6. Personal Acknowledgements

I would like to thank the following people for their support and guidance throughout the development of this project:

# 7. License

This project is licensed under the MIT License - see the [LICENSE](LICENSE$$$$$$) file for details.
