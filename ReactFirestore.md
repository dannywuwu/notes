# [Redux and Firestore](https://react-redux-firebase.com/docs/firestore)


### `npm install react-redux-firebase redux-firestore`

```js
//index.js
import { ..., compose } from 'redux'
import { reduxFirestore, getFirestore, createFirestoreInstance } from 'redux-firestore'
import { ReactReduxFirebaseProvider, getFirebase } from 'react-redux-firebase'
import fbConfig from './config/fb'
import firebase from "firebase/app"

const store = createStore(rootReducer, 
  compose (
    applyMiddleware(thunk.withExtraArgument({ getFirebase, getFirestore })),
    //store enhancers, pass in firebase config
    reduxFirestore(fbConfig),
  )
);

const reactReduxFirebaseProps = {
  firebase,
  config: fbConfig,
  dispatch: store.dispatch,
  createFirestoreInstance
};
```

### `withExtraArgument`

- Takes in an object
- Pass in different properties

## Adding Data to Firestore

### React-Plan

```js
//CreateProject.js
import { connect } from 'react-redux'
import { createProject } from '../../store/actions/projectActions'

this.props.createProject(this.state);

const mapDispatchToProps = dispatch => {
    return {
        createProject: project => dispatch(createProject(project))
    }
}

export default connect(null, mapDispatchToProps)(CreateProject)
```

```js
//projectActions.js

export const createProject = (project) => {
    // pause, make async db call
    return (dispatch, getState, { getFirebase, getFirestore}) => {
        const firestore = getFirestore();
        firestore.collection('projects').add({
            ...project, //project, content
            authorFirst: 'gang',
            authorLast: 'yong',
            authordId: 123,
            createdAt: new Date()
        }).then(() => {
            dispatch({ type: 'CREATE_PROJECT', project });
        }).catch((error) => {
            dispatch({ type: 'CREATE_PROJECT_ERROR', error });
        })
    }
};
```

```js
//reducer
const projectReducer = (state = initState, action) => {
    switch(action.type){
        case 'CREATE_PROJECT':
           ...
            return state;
        default:
            return state;
    }
}
```

## Syncing data with Firestore

- Grab Firestore data and render it in the app
    - Sync Redux state with Firestore data

```js
// rootReducer.js

//  this reducer is made for syncing firestore data with state
// it has access to the fbConfig passed in through index.js
import { firestoreReducer } from 'redux-firestore'

//firestoreReducer syncs properties in the state to the data in the database
const rootReducer = combineReducers ({
    auth: authReducer,
    project: projectReducer,
    firestore: firestoreReducer
})
```

```js
// Dashboard.js
const mapStateToProps = state => {
    return{
        projects: state.firestore.ordered.projects
    }
}
// compose: multiple HOC
export default compose(
    connect(mapStateToProps),
    firestoreConnect(() => ['projects']),
    )(Dashboard)
// firestore connect takes array of collections
// induces firestore reducer above to sync data
```

## Connecting to State + Firebase

```js
import { connect } from 'react-redux'
import { firestoreConnect } from 'react-redux-firebase'
import { compose } from 'redux'

export default compose (
  connect(mapStateToProps),
  firestoreConnect([
      { collection: 'projects' }
  ])
)(ProjectDetails)
```

## Firebase Authentication + Redux

```js
// rootReducer
import { firebaseReducer } from 'react-redux-firebase'

const rootReducer = combineReducers ({
    // which reducers we want to combine and what we want to call them
    ...
    firebase: firebaseReducer,
})
```

```js
// authAction
import firebase from 'firebase/app'
import 'firebase/auth'

export const signIn = (credentials) => {
    return (dispatch, getState) => {
        firebase.auth().signInWithEmailAndPassword(
            credentials.email,
            credentials.password
        ).then(() => {
            dispatch({ type: 'LOGIN_SUCCESS' })
        }).catch((err) => {
            dispatch({ type: 'LOGIN_ERROR', err })
        });
    }
}
```

## Authentication Status

```js
// navbar
function Navbar(props) {
    const { auth } = props;
    const links = auth.uid ? <SignInLinks></SignInLinks> : <SignOutLinks></SignOutLinks>
    ...
}
const mapStateToProps = (state) => {
    return {
        auth: state.firebase.auth
    }
}
```

### `auth.isLoaded`

- Check if Firebase is loaded

## Route Guarding

```js
import { Redirect } from 'react-router-dom'

const { auth } = this.props;
    if(!auth.uid){
      return <Redirect to='/signin'></Redirect
    }

const mapStateToProps = dispatch => {
    return {
        auth: state.firebase.auth
    }
}
```