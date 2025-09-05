1. What is ExpressJS and its relation to NodeJS.
   ExpreeJS- It is a web application framework that runs on Node.js . It simplifies the process of building Web application by providing middleware , routing ,http etc. features.

   Relationship with NodeJS - It is designed to ehance the process of web application developement using NodeJS . NodeJS , on the other hand is a JS runtime environment that allows developers to build using JS in server side also.

2. Middleware
   Middleware acts as a bridge between incoming HTTP requests and your Express.js application, providing carious operations like parsing ,authentication ,serving static file etc.

   CODE ===>

   ```
        const express = require('express');
        const app = express();

        // Sample middleware functions
        function authenticationMiddleware(req, res, next) {
        console.log('Authenticating...');
        next();
        }

        function authorizationMiddleware(req, res, next) {
        console.log('Authorizing...');
        next();
        }

        function requestValidationMiddleware(req, res, next) {
        console.log('Validating request...');
        next();
        }

        // The actual route handler
        app.get('/my-secured-endpoint', authenticationMiddleware, authorizationMiddleware, requestValidationMiddleware, (req, res) => {
        res.send('Welcome! You are authorized.');
        });

        app.listen(3000);
   ```

3. How to serve a static file

   Express provides a built-in middleware called express.static() to serve static assets like HTML, CSS, JavaScript, images, PDFs, etc.

   ```
       const express = require("express");
       const path = require("path");

       const app = express();

       // Serve static files from "public" folder
       app.use(express.static(path.join(__dirname, "public")));

       app.listen(3000, () => console.log("Server running at http://localhost:3000"));

       http://localhost:3000/index.html → serves public/index.html
       http://localhost:3000/style.css → serves public/style.css
       http://localhost:3000/script.js → serves public/script.js
   ```

4. Serving Different Content Types in Express.js

   ```
      res.json() → sends JSON with proper headers.
      res.send() → auto-detects type (string = HTML, object = JSON).
      res.type() → manually sets content type.
      res.format() → handles content negotiation.
      res.sendFile() → serve files directly.
   ```

5. for file upload use multer

6. Implement caching in production level environment

   Bascially we can use redis here

   ```
      import express from "express";
      import { createClient } from "redis";

      const app = express();

      // Create Redis client
      const client = createClient({
      url: "redis://localhost:6379"  // default Redis URL
      });

      // Handle connection errors
      client.on("error", (err) => console.error("Redis Client Error:", err));

      // Connect to Redis
      await client.connect();

      // Set data in Redis
      app.get("/set", async (req, res) => {
      await client.set("name", "Vipul");
      res.send("Key 'name' set in Redis");
      });

      // Get data from Redis
      app.get("/get", async (req, res) => {
      const value = await client.get("name");
      res.send(`Value for 'name' is: ${value}`);
      });

      app.listen(3000, () => {
      console.log("Server running on http://localhost:3000");
      });

   ```

7. cookie
   we use cookie-parser package

   ```
      import express from "express";
      import cookieParser from "cookie-parser";

      const app = express();

      // Use cookie-parser middleware
      app.use(cookieParser());

      // ✅ Set a cookie
      app.get("/set-cookie", (req, res) => {
      res.cookie("username", "vipul", {
         maxAge: 1000 * 60 * 60, // 1 hour
         httpOnly: true,         // prevents JS access (security)
         secure: false,          // true in production with HTTPS
         sameSite: "strict"      // CSRF protection
      });
      res.send("Cookie has been set");
      });

      // ✅ Get cookies
      app.get("/get-cookie", (req, res) => {
      const { username } = req.cookies; // read cookie
      res.send(`Cookie retrieved: ${username}`);
      });

      // ✅ Clear cookie
      app.get("/clear-cookie", (req, res) => {
      res.clearCookie("username");
      res.send("Cookie cleared");
      });

      app.listen(3000, () => {
      console.log("Server running on http://localhost:3000");
      });

   ```

8. What are ways to improve the performance of Express.js applications?

   - Enable Caching(Use redis for frequently needed data)
   - Optmise middleware use
   - Try not to block event loop , do proper use of async I/o operations
   - DB optimization (indexing ,caching , pagination instead of fetching whole collection)

9. Template engines in Express.js let us generate dynamic HTML on the server. We integrate one (like EJS, Pug, or Handlebars) by setting app.set('view engine', 'ejs') and using res.render() to inject data into templates before sending them to the client.

10. DB pooling  
    Mongoose By default on connecting -
    One connection pool (default 100 connections) is opened
    Every query (User.find(), User.save(), etc.) reuses that pool.
    DB write operation is costly so we can do 100 operation without w8ing for another to finish using mongoose

11. USer Authentication
    Baically using JWT we can verify
    there is one more way session based

12. Authentication → Verifies who the user is (login/signup).
    Authorization → Determines what the user is allowed to do.  
    Interview-Worthy Summary

Passwords: Always hash (bcrypt/argon2), never store plain text.

Secrets: Store in environment variables or secret managers, not in code.

Transport: Use HTTPS + secure cookies.

Defense-in-depth: Rate limiting(for preventing brute force attempt), Helmet, input validation.

13. axios or fetch for third party API integration

14. To ensure scalability in Express.js:
    Design stateless apps (use Redis/db for session).
    Horizontally scale with PM2 + Load Balancer.
    Optimize database with pooling, indexes, caching.
    Use CDN + Redis caching to reduce load.
    Offload heavy tasks to workers/queues.
    Monitor and auto-scale in production.

15. Write an Express.js middleware function that limits requests to 100 per hour per IP address.
    locally we do it by using

```
   const rateLimiter = (req, res, next) => {
   const ip = req.ip;
   const currTime = Date.now();

   if (!ipConfig[ip]) {
      // first request from this IP
      ipConfig[ip] = { count: 1, startTime: currTime };
   } else {
      const timePassed = currTime - ipConfig[ip].startTime;

      if (timePassed > 5 * 1000) {
         // reset after 1 hour
         ipConfig[ip] = { count: 1, startTime: currTime };
      } else {
         if (ipConfig[ip].count >= 5) {
         return res.status(403).json({ message: "Rate limit exceeded" });
         }
         ipConfig[ip].count++;
      }
   }

   next();
   };
```

16. Secure API
    authentication & autherization
    hashed password
    .env
    prevention again common attacks
    CORS only with trusted ones

17. SSR
    using ejs we produce dynamic HTML page on user req good for blog content website SEO better Ecommerce
