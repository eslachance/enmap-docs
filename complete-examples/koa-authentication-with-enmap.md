# Koa Authentication with Enmap

In this example we'll be using Enmap to store user data in order to authenticate users on a simple Koa application. In order to make this secure, we'll be using `bcrypt` to encrypt the passwords, so of course they will not be plain text in the database. 

### Requirements

We'll be using `koa` as a web server module, along with `koa-session` in order to store the session information. Additionally, for ease of use, `koa-router` is used to simplify the route code. 

> This tutorial uses `koa-session` which, by default, is insecure since it stores the entire session data in a browser cookie. This means the password, though encrypted, would be availble in the cookie, and easy to spoof. There are many session stores available for different storage system, but using them is beyond the scope of this example.

To install those requirements, run the following in a new, empty folder for your project: 

```text
npm i enmap better-sqlite-pool koa koa-session koa-ejs koa-bodyparser koa-router bcrypt
```

Once all of those are installed, we're ready to start! We're going to create an index page, login page, and one "protected" page that requires login. Let's start with the top of the file, which is all the required modules: 

```javascript
// Native Imports
const { sep, resolve, join } = require("path");

// Enmap Imports
const Enmap = require("enmap");
const users = new Enmap({ name: "users" });

// Bcrypt's hashing system
const bcrypt = require("bcrypt");

// Koa Imports
const Koa = require("koa");
// Koa's EJS renderer for HTML views.
const render = require("koa-ejs");
// The Body Parser to accept incoming form data and file uploads.
const parser = require("koa-bodyparser");
// The default "sessions" support.
const session = require("koa-session");
// Koa's get/post/etc router to simplify routes.
const Router = require("koa-router");
// Initializing the main components.
const router = new Router();
const app = new Koa();

// Define the data directory for templates (views).
const dataDir = resolve(`${process.cwd()}${sep}`);
```

So now we have all the basics necessary. 

### Account Creation Function

Let's create a few functions specifically for the login features, related to enmap. First, a function to create a new user: 

```javascript
const newuser = (username, name, plainpw, admin = false) => {
  if (users.has(username)) throw Error(`User ${username} already exists!`);
  bcrypt.hash(plainpw, 10, (err, password) => {
    if (err) throw err;
    users.set(username, {
      username, name, password, admin, created: Date.now()
    });
  });
};
```

This function takes in the following arguments: 

* `username` which obviously is self-explanatory: it's the username entered during login.
* `name` is the "full name" or "display name", for a friendly display on the page or an email.
* `plainpw` is the password desired for this account. It has to come in as plain text, obviously, in order to be properly saved in the database. 
* `admin` is a boolean value representing whether the user should be administrator. If creating something like a blog, only an administrator could create other administrators. It's false by default.

The function first checks if the username exists and returns an error if it does. It then generates a salted, hashed version of the password which it stores in the database. Don't let the name fool you, the password is not "encrypted", which implies that it can be decrypted. Instead, it's a "cryptographic hash functions", a unidirectional function that cannot be undone. The only way to verify that a password is correct is to re-hash it again and compared the hashes.

Once the hashed password is obtained, the user itself is stored in the database with all 4 incoming arguments except the password which is the hashed version.

### Login Function

The login function takes in the username and the incoming plain password and verifies that the hashed version corresponds with the one stored in the database. 

```javascript
const login = (username, password) => {
  const user = this.users.get(username);
  if (!user) return new Promise(resp => resp(false));
  if (!password) return new Promise(resp => resp(false));
  return bcrypt.compare(password, user.password);
};
```

An important point here is that this function returns a promise in all cases. If the username doesn't exist or the password is blank, a `false` response is returned in a promise. Otherwise, the response of bcrypt's `compare` function is returned. This function returns true if the passwords match, false if they do not.

### Defining some app settings

There's a few configuration items we need to take care of. First off, the session settings: 

```javascript
app.keys = ['some secret hurr'];
app.use(session(app));
```

Then we need to setup how Koa will handle rendering EJS pages. This is one pretty awesome thing about Koa, that this can be setup automatically and globally, but don't let me gush all over this! 

```javascript
render(app, {
  root: join(__dirname, 'views'),
  layout: 'template',
  viewExt: 'html',
  cache: false,
  debug: true
});
```

### Basic Routes

So let's establish our "routes", which is the pages that can be accessed by the browser. With the help of the Router, this can be really straightforward. 

```javascript
router.get("/", async (ctx, next) => {
  // This is our static index page. It will render the views/index.js file
  await ctx.render("index");
});
```

Then we have the login route, which does a lot of the bulk of our work. It checks for login, and adds everything it needs to the session in Koa if the authentication is successful: 

```javascript
// we obviously need a route to show the login page itself, too!
router.get("/login", async (ctx) => {
  await ctx.render("login");  
});

router.post("/login", async (ctx) => {
  // Fail if there is no username and password. 
  // This relies on koa-bodyparser
  if (!ctx.request.body.username || !ctx.request.body.password) {
    ctx.throw(400, "Missing Username or Password");
  }
  // Use our login function to verify the username/password is correct
  const success = await login(ctx.request.body.username, ctx.request.body.password);
  if (success) {
    // get the user's information
    const user = users.get(ctx.request.body.username);
    // Set all our session parameters:
    ctx.session.logged = true;
    ctx.session.username = ctx.request.body.username;
    ctx.session.admin = user.admin;
    ctx.session.name = user.name;
    // Save the session itself. This sets the cookie in the browser, 
    // as well as save into the sessions in memory.
    ctx.session.save();
    console.log(`User authenticated: ${user.username}`);
    // Once logged in, redirect to the secret page.
    ctx.redirect("/secret");
  } else {
    console.log("Authentication Failed");
    // Throw if the above login returns false.
    ctx.throw(403, "Nope. Not allowed, mate.");
  }
});
```

Let's also create a logout function, that simply destroys the current session and returns the user to the index: 

```javascript
router.get("/logout", async (ctx) => {
  ctx.session = null;
  ctx.redirect("/");
});
```

This one is pretty straightforward, so I don't think I need to get into the details, right? ;\)

Lastly, we have the route for our "private" page. the one that only works if you're logged in. Now, there are "better" ways to establish protected routes, but let's go with the simplest one for now. We're just going to check for the `logged` property of the session to determine if the user is logged in.

```javascript
router.get("/secret", async (ctx) => {
  if(!ctx.session.logged) ctx.throw(403, "Unauthorized to view this page");
  await ctx.render("secret");
});
```

### The End of the File

At the very end of our file we still have a bit of stuff to add. Mainly starting the server, but also telling the parser and routers to initialize. This would be how it's done: 

```javascript
app
  .use(parser())
  .use(router.routes())
  .use(router.allowedMethods());

app.on('error', (err, ctx) => {
  console.error('server error', err, ctx)
});

app.listen(3000);
```

### Creating Templates

While templating is slightly beyond the scope of an authentication tutorial, I would be remiss to ignore the fact that logging in without a page would be... let's say a little hard. 

Koa's EJS templating configuration, that we did above, means that templates need to appear in the `views` folder. There will be a few template files: 

* `template.html` will be the "main" template. It will have the header, footer, and whatever else we want to appear on every page. 
* `index.html` will be the main page everyone can access. 
* `login.html` contains the login page and form
* `secret.html` has a little secret about something. 

Let's start with the `template.html` file.

{% code title="views/template.html" %}
```markup
<!DOCTYPE html>
<html lang="en">
	<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
		<title>A Page</title>
	</head>
  <body>
    <nav>
     <ul>
      <li><a href="/">Home</a></li>
      <li><a href="/login">Login</a></li>
      <li><a href="/secret">Secret</a></li>
     </ul>
    </nav>
  <%- body %>
  </body>
</html>
```
{% endcode %}

The `<%- body %>` tag is where the contents of the other pages appear.

The `index.html` is just some welcome thingy that we aren't concerned about: 

{% code title="views/index.html" %}
```markup
<h1>Index</h1>
<p>Lorem Ipsum Carrots</p>
```
{% endcode %}

Then we have the `login.html` page which has our form. The form simply posts back to itself, so it'll trigger the `.post` endpoint:

{% code title="views/login.html" %}
```markup
<h1>Login</h1>
<form method="POST">
 <p>Username: <input type="text" name="username" id="username"></p>
 <p>Password: <input type="password" name="password" id="password"></p>
 <p><button type="submit">Login</button></p>
</form>
```
{% endcode %}

And, finally, the `secret.html` page we've all been waiting for. Nothing that you haven't heard before, though: 

{% code title="views/secret.html" %}
```markup
<h1>Some Secret</h1>
<p>Han Shot First.</p>

```
{% endcode %}

With all said and done, [This should be your project](https://gist.github.com/eslachance/fdc5992534489f1b3b30b8c367e8fba9). Want a more "advanced" version of this project? Check out [My full blogging platform, Koarrots](https://github.com/eslachance/koarrots).

