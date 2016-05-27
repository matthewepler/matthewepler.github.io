---
layout: post
title:  "Bugs/Fixes for 'React for Beginners' Tutorial Series"
date:   2016-05-05 12:00:00 -0500
summary: "Errors I encountered + fixes, in case you're having the same issues while following the videos."
---
<!-- YO MATT - If you're getting an error related to kramdown, use this command to build or serve : 'bundle exec jekyll serve' -->

![React For Beginners Webpage Screenshot]({{site.url}}/images/react4Beginners/react4Beginners.png) 


## Summary
I purchased the [React for Beginners](https://reactforbeginners.com/) video tutorial series and have found it to be a great resource for learning React. Videos, unfortunately, don't automagically update everytime React updates. So when something changes in React, and you try to do it the way the video shows you to do it, you get an error.

I've put some of the errors and fixes I found below in case anyone else finds them useful. I could be blind, but I didn't see a users forum for the tutorial series - so here's a place to keep notes. If you have one I should add, just email me!

### Video 7 - 'createBrowserHistory' Warning

At the top of your file, the video says to do this:

var createBrowserHistory = require('history/lib/createBrowserHistory');

Change that line to look like this:

```javascript
import { browserHistory } from 'react-router';
```

Note = the Navigation object really isn't needed. It's a mixin and as of 1.0 is used. 

Your Router should look like this:

```jsx
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

### Video 14 - Firebase Warning (and fail)

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

### Video 17 - Warning: Encountered two children with the same key...

This happened a little over half-way through the video for me once I was using the linkState method from the mixin. 

![Error screengrab]({{site.url}}/images/react4Beginners/17.png) 

Notice the right panel (Inventory) does not look like his. It doesn't list all the "fishes" like the video. This leads me to believe it's running into an issue somewhere as it's running through the fishes state array. The warning error is worthless in terms of leading me to the exact cause.

This was confirmed by commenting out this line in the Inventory component's render function:

```jsx
	{Object.keys(this.props.fishes).map(this.renderInventory)}
```

Looking back at the renderInventory function, I realized I had this:

```jsx
<div className="fish-edit" key="{key}">
```

I removed the quotation marks from {key} and it everything was fixed. Dumb mistake but easy to do over and over. This was the third time I made that mistake so I figured I'd put it in here. Jeez. (*face palm)

# Video 19 -  Styling issue

There was no space between "lbs" and the fish name when I finished the video. I compared my style.styl file to the one provided, and the 'span' class inside ul.order was not given a class name. 

See line #140 in 'style.styl'
```css
span.count
      position relative
      overflow hidden
      float left // only works if it's floated?!
      span
        display inline-block
        // transition all 0.5s      
```


