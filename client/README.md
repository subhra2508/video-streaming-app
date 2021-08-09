 
### navigation with react router

### what we want 
- user want to navigate to another page in our app
- user clicks a 'link' tag
- React Router prevents the browser from navigating to the new page and fetching new index.html file !
- URL still changes
- 'History' seees updated URL,takes URL and sends it to BrowserRouter
- BrowserRouter communicates the URL to Route components
- Router components rerender to show new set of components

There are mainly 3 types of Router
- BrowserRouter -> localhost:3000/pagetwo (uses everything after the TLD .com ,.net or port as the 'path')
- HashRouter -> localhost:3000/#/pagetwo (uses everything after a # as the 'path')
- MemoryRouter -> localhost:3000/ ->Doesn't use the URL to track navigation

path -> components

/    -> streamList
/streams/new -> StreamCreate
/streams/edit -> StreamEdit
/streams/delete -> StreamDelete
/streams/show -> StreamShow


Google Oauth2 flow

### Traditional Email and Password authentication flow
- We store a record in a database with the user's email and password
- when the user tries to login, we compare email/pw with whats stored in database
- A user is 'Logged In' when they enter the correct email/pw

### OAuth Authentication flow
- User authentication with outside service provider (Google,LinkedIn,Facebook)
- User authorize our app to access their information
- Outside provider tells us about the user
- We are trusting the outside provider to correctly handle identification of a user
- OAuth can be used for (1) user identification in our app and (2) our app making actions on behalf of user


### OAuth for server
- Results in a 'token' that a server can use to make
requests on behalf of the user
- Usually used when we have an app that needs to access user data when they are not logged in
- Difficult to setup because we need to store a lot of info about the user

### OAuth for JS Browser Apps
- Results in a 'token' that a Browser app can use to make requests on behalf of the user
- Usually used when we have an app that only needs to access user data while they are logged in
- very easy to set up thanks to Google's JS lib to automate flow
