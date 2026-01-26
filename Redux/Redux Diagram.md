[Component/UI]
   |
   |  dispatch(login(credentials))
   |
   v
[RSAA Middleware: take care of Actions]
   |---> dispatch({ type: LOGIN_REQUEST })
   |        (loading spinner ON, error reset)
   |
   |---> Makes API call
   |
   |---> API responds
   |        |
   |        | success: dispatch({ type: LOGIN_SUCCESS, payload: { user, token } })
   |        | failure: dispatch({ type: LOGIN_FAILURE, payload: error })
   v
[Reducer (authReducer)]
   |
   | case LOGIN_REQUEST:
   |     return { ...state, loading: true, error: null }
   |
   | case LOGIN_SUCCESS:
   |     return { ...state, loading: false, user: action.payload.user, token: action.payload.token, error: null }
   |
   | case LOGIN_FAILURE:
   |     return { ...state, loading: false, error: action.payload }
   |
   v
[Redux Store]
   |
   | Stores updated state immutably
   |
   v
[React Component]
   |
   | useSelector(state => state.auth)
   | { loading, user, token, error } updated automatically
   |
   v
[UI Updates Automatically]
   | - Show spinner / hide spinner
   | - Display user info
   | - Show error message if any
