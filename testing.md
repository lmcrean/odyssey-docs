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
