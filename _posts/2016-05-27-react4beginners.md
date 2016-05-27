---
layout: post
title:  "Bugs/Fixes for 'React for Beginners' Tutorial Series"
date:   2016-05-05 12:00:00 -0500
summary: "Errors I encountered + fixes, in case you're having the same issues while following the videos."
---

![React For Beginners Webpage Screenshot]({{site.url}}/images/react4Beginners/react4Beginners.png) 


## Summary
I purchased the "React for Beginners" video tutorial series and have found it to be a great resource for learning React. Videos, unfortunately, don't automagically update everytime React updates. So when something changes in React, and you try to do it the way the video shows you to do it, you get an error.

I've put some of the errors and fixes I found below in case anyone else finds them useful. I could be blind, but I didn't see a users forum for the tutorial series - so here's a place to keep notes. If you have one I should add, just email me!

### Video 7 - deprecated error for history stuff

At the top of your file, the video says to do this:

var createBrowserHistory = require('history/lib/createBrowserHistory');

Change that line to look like this:

```javascript
import { browserHistory } from 'react-router';
```

Note = the Navigation object really isn't needed. It's a mixin and as of 1.0 is used. 

Your Router should look like this:

```javascript
/* 
	Routes
*/
var routes = (
	<Router history={browserHistory}>
		<Route path="/" component={StorePicker} />
		<Route path="/store/:storeId" component={App} />
		<Route path="*" component={NotFound} />
	</Router>
)
```

more info here: [react-router README.md on github](https://github.com/reactjs/react-router)

### Video 14 - ERROR in console reads: FIREBASE WARNING....blah...permissions...blah
To fix, go into your firebase database by clicking the "database" link on the left-side menu of the Firebase site. At the top, in the blue area, click the "Rules" link. Change the rule to read:

```javascript
{
  "rules": {
    ".read": true,
    ".write": true
  }
}
```

Click "Publish" to save your changes. Refresh your app page. Click "Load Sample Fishes" button. It should work and you should see the fish objects appear in Firebase.

For more info on security and authorization, see [this Firebase documentation on security rules](https://firebase.google.com/docs/database/security/quickstart#numbered)