# Most Common Web Security Attacks

# Cross-Site Scripting (XSS)

1. Cross-Site Scripting is also called XSS for short. And the idea is that a hacker can inject their own custom JavaScript into a webpage. It's used to trick users into running their custom JavaScript code. And they can also be used to steal cookies. And if they steal cookies they can steal the cookies data as well as potentially session data, which has been linked with a cookie.

2. Let's imagine that we have a URL that's going to be coming in from a GET request and it's going to contain an email address. What we're going to do is take that email address, whatever string has been given to us and output it on the HTML page. So in my code I would have email colon and then a place for the dynamic text would get dropped in. So when that outputs in this case, it's going to put email : Kevin@nowhere.com.

3. That's going to appear in my HTML Now let me show you the evil example. We have the exact same thing, but instead of the email address, being an actual email address, now its a bit of JavaScript. So, when that gets dropped in, in that dynamic spot for email, now it gets output to my HTML, is email colon, and that JavaScript gets executed by the users browser. Now this example just pops up a harmless alert box that says, Gotcha! But when ever you see me use that kind of JavaScript alert realize that, that could be any arbitrary JavaScript that the hacker wanted.

4. In real life the hacker would write a script that could access the browser's cookie data or send data to another server that they controlled. 

5. Now this time, instead of working with something that comes from the URL, I want us to look at the database data. Let's imagine that there's an email address in our database data which is fake@email.com and then a specially crafted string at the end, backslash, double-quote, closing curly brace, and semicolon. What that does is it tells the JSON that you're done. It says here's the end of the field, because here's the double quote, and here's the curly brace and semicolon to end all the JSON. We're done with the user's JSON. What comes after it then, is JavaScript.

So it runs its JavaScript alert and then right at the very end of that we've got the forward slash, forward slash. Which is a comment in JavaScript and it basically says ignore everything after that. You see what that does? It prematurely truncates our JSON and then runs JavaScript and then ignores anything else that would come after it. So this is called cross-site scripting because the scripting is done via another website. And it's successful because the browser trusts the JavaScript. Whatever JavaScript is handed to it, the browser just simply executes it. The browser doesn't have a mechanism for knowing which JavaScript is trustworthy or not trustworthy.

And the browser will even let the JavaScript access the cookie data. But how do we protect against it? The main way is that you want to sanitize any dynamic text that gets output to the browser. Make sure that it's safe. Turn it into something that's harmless before you put it on the page. So that means your HTML, your JavaScript, JSON, XML, anything else that you output. You want to make sure that it gets rendered harmless, especially data that comes from URL or forms. That's our primary way that we interact with our users, right. They either are typing a URL, clicking a link or filling out a web form.

That's the data that's easiest to send to us. But, we also have to be careful about database data, cookie data and session data. Even though it may not seem like that's coming directly from the users, it may be coming from them indirectly. They may have sent in a value to our database. It was never sanitized. Now we're pulling it back out to use it. We can't trust it just because it's in our database. We still have to sanitize it again. We saw that back in the JSON example. Now I realize, that sometimes, you do want to let some HTML tags go through unsanitized.

You may even want to let some JavaScript through unsanitized. If you're working with a content management system, that may be the case. You may need your users to be able to style the content using HTML. If so, then you want to use a white list to determine which HTML tags ought to be valid and you should then sanitize everything else. One you successfully sanitize all the dynamic content on your site, cross-site scripting won't be a threat.