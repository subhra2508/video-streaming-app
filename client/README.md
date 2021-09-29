 
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

```jsx
class GoogleAuth extends React.Component{
    state = {isSignedIn:null};


    componentDidMount(){
        window.gapi.load('client:auth2',() => {
            window.gapi.client.init({
                clientId:'YOUR_CLIENT_ID',
                scope:'email'
            }).then(()=>{
                this.auth = window.gapi.auth2.getAuthInstance();
                this.setState({isSignedIn:this.auth.isSignedIn.get()});
                this.auth.isSignedIn.listen(this.onAuthChange);
            });
        });
    }
    onAuthChange = (isSignedIn) =>{
         if(isSignedIn){
             this.props.signIn();
         }
         else{
             this.props.signOut();
         }
    }

    onSignInClick = () => {
        this.auth.signIn();
    }

    onSignOutClick = ()=>{
        this.auth.signOut();
    }

    renderAuthButton(){
        if(this.state.isSignedIn === null){
            return null;
        }
        else if(this.state.isSignedIn){
             return (
             <button onClick={this.onSignOutClick} className = "ui red google button">
                 <i className="google icon"/>
                 sign out
             </button>)
        }
        else{
            return (
                <button onClick={this.onSignInClick} className="ui red google button">
                    <i className="google icon"/>
                    sign in with google
                </button>
            )
        }
    }

    render(){
        return <div>{this.renderAuthButton()}</div>
    }
};
```
BAD PRACTISE :
- state.pop()
- state.push()
- state[0] = 'hi'
- state.name = 'Sam'
- state.age = 30
- delete state.name

GOOD PRACTISE :
- state.filter(element => element!=='hi')
- [...state,'hi']
- state.map(el => el === 'hi'?'bye':el)
- {...state,name:'Sam'}
- {...state,age:30}
- {...state,age:undefined}
- _.omit(state,'age')


- Intentional Navigation : User clicks on a 'Link' component
- programmatic navigation : We run code to forcibly navigate the user through our app


sequence of steps:
- User submits the form
- we make request to backend API to create stream
- we navigate user back to the list of streams
 Time passes....
- API responds with error,stream wasn't created and user doesn't know!
- we either show error to the user or navigate them back to list of streams


<img src="../images/programmatic_navigation.png">


Getting access to the history object is a pain so we are using different approach

<img src="../images/programmatic_navigation_historyobj.png">

selection procedures :
- selection reducers
- url-based selection

<img src="./../images/url_based_selection">