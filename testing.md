# Testing


# Manual Testing 

Pass criteria includes no warning messages, no errors.

## Test 1: Testing the Navbar

| Feature | Auth status: <br> Signed in/Signed out/ Both |Expected Outcome | Testing Performed | Result | Pass/Fail |
| --- | --- | --- | --- | --- | --- |
| Sign up | Signed out | User is redirected to the sign up page | Clicked on the sign up button | User was redirected to the sign up page | Pass |
| Sign in | Signed out | User is redirected to the sign in page | Clicked on the sign in button | User was redirected to the sign in page | Pass |
| Home Feed | Signed in | User is redirected to the home feed | Clicked on the home feed button | User was redirected to the home feed | Pass |
| Add Post | Signed in | User is redirected to the add post page | Clicked on the add post button | User was redirected to the add post page | Pass |
| Messages | Signed in | User is redirected to the messages page | Clicked on the messages button | User was redirected to the messages page | Pass |
| Profile | Signed in | User is redirected to the profile page | Clicked on the profile button | User was redirected to the profile page | Pass |
| Sign Out | Signed in | User is signed out and redirected to the sign in page | Clicked on the sign out button | User was signed out and redirected to the sign in page | Pass |
| Responsive Design | Both | Navbar is responsive, will switch between a sidebar and bottom in different views, there must be no breaks particularly around the 768px where the hook activates. | Tested on different screen sizes | Navbar was responsive | Pass |

## Test 2: Testing the Home Feed

| Feature | Auth status: <br> Signed in/Signed out/ Both |Expected Outcome | Testing Performed | Result | Pass/Fail |
| --- | --- | --- | --- | --- | --- |
| Posts | Both | User is able to view posts | Viewed the posts | User was able to view the posts | Pass |
| Like Post | Signed in | User is able to like a post, updates Like Count | Liked a post, updates like count | User was able to like a post | Pass |
| Unlike Post | Signed in | User is able to unlike a post, updates Like Count | Unliked a post, updates like count | User was able to unlike a post | Pass |
| For you tab | Signed in | Displays recent posts | Clicked on the for you tab | Recent posts were displayed | Pass |
| Following tab | Signed in | Displays posts from users the user is following | Clicked on the following tab | Posts from users the user is following were displayed | Pass |
| Liked tab | Signed in | Displays posts the user has liked | Clicked on the liked tab | Posts the user has liked were displayed | Pass |


## Test 3: Testing the Post functionality

| Feature | Auth status: <br> Signed in/Signed out/ Both |Expected Outcome | Testing Performed | Result | Pass/Fail |
| --- | --- | --- | --- | --- | --- |
| Add Post | Signed in | User is able to add a post | Added a post | User was able to add a post, was visible on home feed | Pass |
| Edit Post | Signed in | User is able to edit a post | Edited a post | User was able to edit a post | Pass |
| Delete Post | Signed in | User is able to delete a post | Deleted a post | User was able to delete a post | Pass |

## Test 4: Testing the Profile Page

| Feature | Auth status: <br> Signed in/Signed out/ Both |Expected Outcome | Testing Performed | Result | Pass/Fail |
| --- | --- | --- | --- | --- | --- |
| View Profile | Both | User is able to view their profile | Viewed the profile | User was able to view their profile | Pass |
| Edit username | Signed in | User is able to edit their profile username | Edited the profile username | User was able to edit their username | Pass |
| Edit bio | Signed in | User is able to edit their profile bio | Edited the profile bio | User was able to edit their bio | Pass |
| Edit profile picture | Signed in | User is able to edit their profile picture | Edited the profile picture | User was able to edit their profile picture | FAIL$$$$$$$$$$ |
| follow user link |
| message user link | 

## Test 5: Testing the Messages Page

| Feature | Auth status: <br> Signed in/Signed out/ Both |Expected Outcome | Testing Performed | Result | Pass/Fail |
| --- | --- | --- | --- | --- | --- |
| View Messages | Signed in | User is able to view their messages | Viewed the messages | User was able to view their messages | Pass |
| Send Message with Picture | Signed in | User is able to send a message with picture | sent message with attached file | User was able to send picture, it appears in chat interface | Pass | 
| Send Message | Signed in | User is able to send a message | Sent a message | User was able to send a message | Pass |
| Delete Message | Signed in | User is able to delete a message | Deleted a message | User was able to delete a message | Pass |

## Test 6: Testing the Sign Up Page

| Feature | Auth status: <br> Signed in/Signed out/ Both |Expected Outcome | Testing Performed | Result | Pass/Fail |
| --- | --- | --- | --- | --- | --- |
| Sign Up | Signed out | User is able to sign up | Signed up | User was able to sign up | Pass |
| Sign Up Validation | Signed out | User is unable to sign up with invalid credentials | Signed up with invalid credentials | User was unable to sign up | Pass |

## Test 7: Testing the Sign In Page

| Feature | Auth status: <br> Signed in/Signed out/ Both |Expected Outcome | Testing Performed | Result | Pass/Fail |
| --- | --- | --- | --- | --- | --- |
| Sign In | Signed out | User is able to sign in | Signed in | User was able to sign in | Pass |
| Sign In Validation | Signed out | User is unable to sign in with invalid credentials | Signed in with invalid credentials | User was unable to sign in | Pass |

## Test 8: Popular profiles component

| Feature | Auth status: <br> Signed in/Signed out/ Both | Expected Outcome | Testing Performed | Result | Pass/Fail |
| --- | --- | --- | --- | --- | --- |
| Popular profiles | Both | User is able to view popular profiles | Viewed popular profiles | User was able to view popular profiles | Pass |
| Follow user | Signed in | User is able to follow a popular profile | Followed a popular profile | User was able to follow a popular profile | Pass |
| Message user | Signed in | User is able to message a popular profile | Messaged a popular profile | User was able to message a popular profile | Pass |

## Test 9: Landing Page

| Feature | Auth status: <br> Signed in/Signed out/ Both | Expected Outcome | Testing Performed | Result | Pass/Fail |
| --- | --- | --- | --- | --- | --- |
| Landing Page | Both | User is able to view the landing page | Viewed the landing page | User was able to view the landing page | Pass |
| Sign Up | Signed out | User is able to sign up from the landing page | Signed up from the landing page | User was able to sign up from the landing page | Pass |
| Sign In | Signed out | User is able to sign in from the landing page | Signed in from the landing page | User was able to sign in from the landing page | Pass |

