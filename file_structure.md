# 1. Frontend Directory Structure

The frontend directory structure is designed to organize the React application's codebase effectively. Here's an overview of the key directories and their purposes:

## 1.1. `frontend/cypress/`
- Contains end-to-end tests using Cypress
- Includes test specifications like `cypress/e2e/auth.cy.js` for authentication testing
- Configuration in `cypress.config.js` sets up the testing environment

## 1.2. `frontend/node_modules/`
- Contains all the npm packages and dependencies installed via `npm install`
- Managed by `npm`, not typically modified directly
- Essential for running the application and its development environment

## 1.3. `frontend/playwright/`
- Houses browser automation and testing scripts using Playwright
- Includes tests like `playwright/auth.spec.js` for cross-browser authentication testing
- Configured via `playwright.config.js` for multi-browser support

## 1.4. `frontend/public/`
- Contains static assets that are publicly accessible
- Includes `index.html`, `favicon.ico`, and other static resources
- Files here are served directly without being processed by webpack

## 1.5. `frontend/screenshots/`
- Stores screenshots taken during automated tests
- Useful for visual regression testing and debugging
- Screenshots are typically named based on the test, e.g., `auth-test-failed-1.png`

## 1.6. `frontend/src/`
The main source code directory for the React application. Contains various subdirectories:

### 1.6.1. `frontend/src/api/`
- Handles API configurations and defaults
- `axiosDefaults.js` sets up base URL and default headers for API requests

### 1.6.2. `frontend/src/assets/`
- Stores static assets like `logo.png` and `upload.png`
- Includes images and icons used throughout the application

### 1.6.3. `frontend/src/components/`
- Contains reusable React components
- Includes components like `Asset.js`, `Avatar.js`, and `NavBar.js`
- `MoreDropdown.js` provides a reusable dropdown menu component

### 1.6.4. `frontend/src/contexts/`
Holds React context providers for state management:

- `CurrentUserContext.js`: Manages user authentication state
- `ProfileDataContext.js`: Handles profile data and follow/unfollow functionality
- `PostCacheContext.js`: Implements post caching for performance
- `AnimationLoadingContext.js`: Manages animation loading states
- `ThemeContext.js`: Controls app-wide theme settings (light/dark mode)

### 1.6.5. `frontend/src/fonts/`
- Stores custom font files like `Fontspring-DEMO-coresansc65.otf`
- Ensures consistent typography across the app

### 1.6.6. `frontend/src/hooks/`
- Contains custom React hooks like `useClickOutsideToggle.js` and `useRedirect.js`
- `useWindowSize.js` provides responsive design utilities

### 1.6.7. `frontend/src/mocks/`
- Includes mock data and handlers in `handlers.js` for testing
- Simulates API responses for consistent testing environments

### 1.6.8. `frontend/src/pages/`
Contains page components organized by feature:

#### 1.6.8.1. `frontend/src/pages/auth/`
- `SignInForm.js` and `SignUpForm.js` manage user authentication

#### 1.6.8.2. `frontend/src/pages/comments/`
- `Comment.js`, `CommentCreateForm.js`, and `CommentEditForm.js` handle comment functionality

#### 1.6.8.3. `frontend/src/pages/messaging/`
- `Message.js`, `MessageList.js`, `MessageDetail.js` manage the messaging feature
- `MessageDetailSendForm.js` handles sending new messages

#### 1.6.8.4. `frontend/src/pages/posts/`
- `Post.js`, `PostCreateForm.js`, `PostEditForm.js` manage post CRUD operations
- `PostsPage.js` displays the main feed of posts

#### 1.6.8.5. `frontend/src/pages/profiles/`
- `Profile.js`, `ProfileEditForm.js` handle user profile management
- `PopularProfiles.js` showcases popular user profiles

### 1.6.9. `frontend/src/styles/`
- `variables.css` defines global CSS variables for consistent styling
- `base.css` provides base styles for the app such as fonts, colors and fallbacks

#### 1.6.9.1. `frontend/src/styles/modules/`
- Houses component-specific CSS module files
- Examples include:
  - `Post.module.css` for styling post components
  - `Profile.module.css` for profile-related styles
  - `MessageList.module.css` for message list styling
  - `NavBarDesktop.module.css` and `NavBarMobile.module.css` for responsive navigation styling
- Each module corresponds to a specific component, enabling scoped styling
- there is an `animations` folder containing CSS files for custom animations
- `LikeAnimation.module.css` defines styles for the post liking animation

### 1.6.10. `frontend/src/utils/`
- `utils.js` contains utility functions like `fetchMoreData` for infinite scrolling

## 1.7. `frontend/test-results/`
- Stores test results, often in JSON format like `test-results.json`
- Useful for analyzing test outcomes and generating reports

This structure organizes the frontend code into logical sections, promoting maintainability and scalability. Each directory and file serves a specific purpose in creating a robust React application.