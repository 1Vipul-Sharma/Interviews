====================================================================================================================================================

-                                                            REACT ROUTER

=====================================================================================================================================================

1. How do you implement private/protected routes with React Router DOM?

Answer:

```
   const PrivateRoute = ({ children }) => {
   const isAuth = localStorage.getItem("token");
   return isAuth ? children : <Navigate to="/login" />;
   };

   // usage
   <Route path="/dashboard" element={<PrivateRoute><Dashboard /></PrivateRoute>} />
```

Explanation:
We wrap the protected component with a guard (PrivateRoute). If the user is not authenticated, redirect them to /login.

2. What is lazy loading in React Router v6 and how do you implement it?

Answer:

```
   import { lazy, Suspense } from "react";
   const Products = lazy(() => import("./Products"));

   <Route
   path="/products"
   element={
      <Suspense fallback={<h1>Loading...</h1>}>
         <Products />
      </Suspense>
   }
   />
```

Explanation:
Lazy loading splits code into chunks. React Router supports React.lazy + Suspense to only load the component when that route is visited → reduces bundle size.

3. How do you pass props through <Route> in React Router v6?

Answer:

```
   <Route path="/profile" element={<Profile user={user} />} />
```

Explanation:
Unlike v5, v6 doesn’t use render or component props. Instead, you directly pass JSX with props into element.

4. What is the difference between relative and absolute paths in nested routing?

Answer:

```
   Relative Path: Does not start with /, appended to the parent route.

   Absolute Path: Starts with /, resolves from the root.

   Example:

   <Route path="dashboard" element={<Dashboard />}>
   <Route path="stats" element={<Stats />} />   {/* /dashboard/stats */}
   <Route path="/settings" element={<Settings />} /> {/* /settings */}
   </Route>
```

Explanation:
Relative keeps context inside parent routes, while absolute ignores nesting.

5. How does useNavigate() differ from useHistory() in older versions?

Answer:

```
   React Router v5 → useHistory() for pushing/replacing routes.

   React Router v6 → useNavigate() replaced it.

   const navigate = useNavigate();
   navigate("/login"); // push
   navigate(-1);       // go back
```

Explanation:
useNavigate is more intuitive, handles back/forward navigation, and works better with modern APIs.

6. How can you handle 404 Not Found routes in React Router?

Answer:

```
   <Route path="*" element={<NotFound />} />
```

Explanation:
path="\*" is a catch-all route that matches anything not defined. Always place it last in the <Routes> block.

7. How do you share layouts (like a navbar or sidebar) across multiple routes in React Router v6?

Answer:

```
   const Layout = () => (
   <>
      <Navbar />
      <Outlet />  {/* child route renders here */}
   </>
   );

   <Route path="/" element={<Layout />}>
   <Route index element={<Home />} />
   <Route path="products" element={<Products />} />
   </Route>

```

Explanation:
React Router v6 uses <Outlet> to render nested child routes inside a shared parent layout.

8. How do you differentiate between replace and push navigation in React Router?

Answer:

```
   const navigate = useNavigate();
   navigate("/dashboard", { replace: true }); // replaces current entry


   push (default): Adds a new entry to the history stack.

   replace: Replaces the current entry, preventing back navigation.
```

Explanation:
Use replace for redirects (like after login), so the user can’t go back to /login with the browser back button.
