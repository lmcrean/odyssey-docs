## Issues with cloudinary connecting to server

expecting a cloudinary picture to be apparent in this url localhost:3000/posts/11, instead it is not showing up.

Troubleshooting steps taken so far

1. Checked the cloudinary account to see if the picture was uploaded - no
2. Checked the server to see if the picture was being sent to the server (github.com/lmcrean/drf-clone) - no

My theory is that I am missing a .env file.

I have an axios post

```
import axios from "axios";

axios.defaults.baseURL = "https://project5-lmcrean-1b4c7e21126b.herokuapp.com/";
axios.defaults.headers.post["Content-Type"] = "multipart/form-data";
axios.defaults.withCredentials = true;

export const axiosReq = axios.create();
export const axiosRes = axios.create();
```