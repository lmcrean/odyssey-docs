# Unable to Fetch Conversations in React App Using Axios - tokens not being sent correctly in GET request

I'm working on a React app where I am expecting to fetch a list of conversations for the logged-in user. This has been achieved already with Postman on the production API.

However, in the API-connected front-end, the GET request to fetch conversations is not executing properly. I have documented in my code where tests are failing, particularly in the `MessageList` component, where the access tokens don't appear to be fetched correctly. I've learnt that the token might not be sent correctly or is invalid.  

# relevant files

1. AxiosDefaults
```
// src/api/axiosDefaults.js

import axios from "axios";

axios.defaults.baseURL = "https://odyssey-api-f3455553b29d.herokuapp.com/";
axios.defaults.headers.post["Content-Type"] = "multipart/form-data";
axios.defaults.withCredentials = true;

export const axiosReq = axios.create();
export const axiosRes = axios.create();
```

2. CurrentUserContext

This appears to enable to login the user succesfully
```
// src/contexts/CurrentUserContext.js

import { createContext, useContext, useEffect, useMemo, useState } from "react";
import axios from "axios";
import { axiosReq, axiosRes } from "../api/axiosDefaults";
import { useHistory } from "react-router";
import { removeTokenTimestamp, shouldRefreshToken } from "../utils/utils";

export const CurrentUserContext = createContext();
export const SetCurrentUserContext = createContext();

export const useCurrentUser = () => useContext(CurrentUserContext);
export const useSetCurrentUser = () => useContext(SetCurrentUserContext);

export const CurrentUserProvider = ({ children }) => {
  const [currentUser, setCurrentUser] = useState(null);
  const history = useHistory();

  const handleMount = async () => {
    try {
      const { data } = await axiosRes.get("dj-rest-auth/user/");
      setCurrentUser(data);
      console.log('Current user data:', data); // PASS. Current user data: { pk: 13, username: "user1", email: "", first_name: "", last_name: "", ... }
    } catch (err) {
      console.error('Failed to fetch current user data:', err); // Not registering
    }
  };

  useEffect(() => {
    handleMount();
  }, []);

  useMemo(() => {
    axiosReq.interceptors.request.use(
      async (config) => {
        if (shouldRefreshToken()) {
          try {
            const response = await axios.post("/dj-rest-auth/token/refresh/");
            console.log('Token refreshed:', response.data); // PASS. Token refreshed: { access: 'eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9...', ... }
          } catch (err) {
            setCurrentUser((prevCurrentUser) => {
              if (prevCurrentUser) {
                history.push("/signin");
              }
              return null;
            });
            removeTokenTimestamp();
            return config;
          }
        }
        return config;
      },
      (err) => {
        return Promise.reject(err);
      }
    );

    axiosRes.interceptors.response.use(
      (response) => response,
      async (err) => {
        if (err.response?.status === 401) {
          try {
            const response = await axios.post("/dj-rest-auth/token/refresh/");
            console.log('Token refreshed after 401:', response.data); // Token refreshed after 401: { access: 'eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9...', ... }
          } catch (err) {
            setCurrentUser((prevCurrentUser) => {
              if (prevCurrentUser) {
                history.push("/signin");
              }
              return null;
            });
            removeTokenTimestamp();
          }
          return axios(err.config);
        }
        return Promise.reject(err);
      }
    );
  }, [history]);

  return (
    <CurrentUserContext.Provider value={currentUser}>
      <SetCurrentUserContext.Provider value={setCurrentUser}>
        {children}
      </SetCurrentUserContext.Provider>
    </CurrentUserContext.Provider>
  );
};
```

3. MessageList

trying to call this array from GET `https://odyssey-api-f3455553b29d.herokuapp.com/conversations/?Authorization=eyJ0eXAiOiJ....`
to retrive
`[{"id": 15,"username": "user3" }, {"id": 14,"username": "user2"},{"id": 16,"username": "user4"}]`

The above was retrieved successfully as a GET request with Postman API handler after POST login details `https://odyssey-api-f3455553b29d.herokuapp.com/dj-rest-auth/login/`
with body: `{"username": "user1","password": "*****"}`

note the console.logs that are NOT registering.

```
// pages/messaging/MessageList.js


import React, { useEffect, useState, useContext } from 'react';
import { axiosReq } from '../../api/axiosDefaults';
import { CurrentUserContext } from '../../contexts/CurrentUserContext';

const MessageList = () => {
  const [conversations, setConversations] = useState([]);
  const { currentUser } = useContext(CurrentUserContext);

  useEffect(() => {
    const fetchConversations = async () => {
      if (!currentUser || !currentUser.token) {
        console.error('Token is missing or current user is not set'); // Not registering
        return;
      }

      console.log('Current user (MessageList):', currentUser); // FAIL. Not registering
      console.log('Current user token (MessageList):', currentUser.token); // FAIL. Not registering

      try {
        const response = await axiosReq.get('/conversations/', {
          headers: {
            Authorization: `Token ${currentUser.token}`,
            'Content-Type': 'application/json', // Specify Content-Type for this request
          },
        });
        console.log('Fetched conversations:', response.data); // FAIL. Not registering
        setConversations(response.data);
      } catch (error) {
        console.error('Failed to fetch conversations:', error); // FAIL. Not registering
      }
    };

    if (currentUser && currentUser.token) {
      console.log('Fetching conversations...'); // FAIL. Not registering
      fetchConversations();
    } else {
      console.log('Current user or token is missing:', currentUser); // Current user or token is missing: undefined
    }
  }, [currentUser]);

  console.log('Conversations state:', conversations); // Conversations state: []

  return (
    <div>
      <h1>Conversations</h1>
      <ul>
        {conversations.length > 0 ? (
          conversations.map((conversation) => (
            <li key={conversation.id}>{conversation.username}</li>
          ))
        ) : (
          <p>No conversations found.</p>
        )}
      </ul>
    </div>
  );
};

export default MessageList;


```

# Debugging Steps Taken

1. Verified that the GET request URL is correct and matches the successful Postman request.

2.  Verified that tokens are being retrieved successfully after login using Postman:
`[{"id": 15,"username": "user3" }, {"id": 14,"username": "user2"},{"id": 16,"username": "user4"}]`

3. Added extensive console logs to check if the current user and token are being set correctly:

4. Current user data logged correctly in ```
console.log('Current user data:', data); // Current user data: { pk: 13, username: "user1", email: "", first_name: "", last_name: "", ... }```

5. Current user data logged correctly in MessageList 
   - `console.log ('Current user:', currentUser); // Current user: Object { pk: 13, username: "user1", email: "", first_name: "", last_name: "", ... }`
   - `console.log('Current user token:', currentUser.token); // Token refreshed: { access: 'eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9...', ... }`

6. tried setting the Content-Type header to application/json for the GET request.

 # Observations

 - The 401 Unauthorized error suggests that the token might not be sent correctly or is invalid. 
 - Despite logging in and getting tokens, the request to fetch conversations is not being executed properly. The console logs in the MessageList component are not registering the fetched data.
 - Nework tab in Devtools shows that the GET request is being made with the correct token. [![Network in Devtools][1]][1]


# Resources:

github.com/lmcrean/odyssey-react


  [1]: https://i.sstatic.net/8MPOzzRT.png