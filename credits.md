
# 5. **Acknowledgement and Credits**

## 5.1. Code Institute Moments app as boilerplate

"Moments" was used as a boilerplate for the project as it contained the necessary features for a social media platform. Both the API and the React frontend were built from this code.
  - Frontend: https://github.com/Code-Institute-Solutions/moments
  - API:  https://github.com/Code-Institute-Solutions/drf-api

## 5.2. Code institute Repo unification tutorial

A key issue with the project was authnetication not working on Safari browsers, due to having seperate repositories with the frontend and API. 

- [Code Institute](https://codeinstitute.net/) provided a tutorial on how to unify the repositories, which was used to fix the issue.

## 5.3. npm Libraries for frontend

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


## 5.4. Broader Software used

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

## 5.5. Use of LLMs

LLMs were used as an AI tool to generate initial drafts which would be meticulously reviewed.

- writing detailed commit messages
- implementation of new features in Javascript, CSS or Python
- drafting readme documentation
- it could be assumed that any file or commit message might have started as an LLM draft which was extensively tested and reviewed.

The limits of LLMs tended to be that they could not generate test-proof code.

The following tools were used to generate such drafts:

- [Claude Sonnet 3.5](http://www.claude.ai/), eventually replacing the use of [GPT-4o](http://www.chatgpt.com/) with it's higher context window of 200,000 tokens.
- [Github Copilot](http://www.github.com/copilot) for inline editing suggestions.

## 5.6. Personal Acknowledgements

I would like to thank the following people for their support and guidance throughout the development of this project:

# 6. License

This project is licensed under the MIT License - see the [LICENSE](LICENSE$$$$$$) file for details.