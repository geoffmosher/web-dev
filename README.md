# web-dev
**Code samples and tutorials**

**1. Google OAuth Login API for Squarespace - basic NodeJS example **

const express = require("express");
const passport = require("passport");
const GoogleStrategy = require("passport-google-oauth20").Strategy;

const app = express();

// Configure the Google OAuth strategy
passport.use(new GoogleStrategy({
  clientID: "YOUR_GOOGLE_CLIENT_ID",
  clientSecret: "YOUR_GOOGLE_CLIENT_SECRET",
  callbackURL: "http://localhost:3000/auth/google/callback",
}, (accessToken, refreshToken, profile, done) => {
  return done(null, profile);
}));

// Serialize user for the session
passport.serializeUser((user, done) => done(null, user));
passport.deserializeUser((obj, done) => done(null, obj));

// Google OAuth routes
app.get('/auth/google', passport.authenticate('google', { scope: ['profile', 'email'] }));
app.get('/auth/google/callback',
  passport.authenticate('google', { failureRedirect: '/' }),
  (req, res) => res.send('Login Successful!'));

app.listen(3000, () => console.log("Server running on http://localhost:3000"));

**package.json**
{
  "name": "google-login-sample",
  "version": "1.0.0",
  "main": "app.js",
  "scripts": {
    "start": "node app.js"
  },
  "dependencies": {
    "express": "^4.18.0",
    "passport": "^0.6.0",
    "passport-google-oauth20": "^2.0.0"
  }
}

**Instructions**
Replace YOUR_GOOGLE_CLIENT_ID and YOUR_GOOGLE_CLIENT_SECRET with credentials from the Google Developer Console. 
Install dependencies using npm install.
Run the app with npm start.
