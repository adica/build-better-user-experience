# How to build better user experience with “positive thinking” approach

You always want the fastest and most responsive UI.

In an attempt to optimize your product, you may have already learned how to use techniques such as minifying your CSS and JS files, compressing static resources, and utilizing caching via CDN.

But still there is much more to do - we can change our UI behavior with a few simple steps that will make our product to be much faster and better with a “positive thinking approach”.

When building UI interfaces most of the developers tend to use “worst case scenario” approach. It assumes that an exception is going to occur, therefore, the UI will not be updated until we get an OK response from the server.

“Positive thinking” approach is a method that assumes that the steps of our product flow are going to be fine 99% of the time so we should update our UI as if we got OK response from the server even before we sent our request.
In the 1% of errors that may occur, we will quietly notify the user that something has gone wrong or an exception has occurred.

Let’s see some examples:

1. “Instagram”  

	the basic scenario in Instagram includes 3 steps:

	* Choose an image and apply a filter
	* Add a caption to that image
	* Set where to share this image and press the “save” button.

	Most of the applications will start uploading the image to the server only after the “save” button is clicked, and 	        show the user the end result after the server will return that everything went fine.

	however, Instagram uploads the image immediately after the user applies the filter.
        This action gives them few seconds for uploading while the user writes his caption and chooses where to share it --          when he presses the “save” button - he sees immediately the end result without wasting time and with no “loading...”         image .

2.  “Facebook”

	when we add a comment on facebook - FB does not wait for response from the server, it updates the UI as if the      response returns OK. Only when there is a problem - FB announces the user.
This way - the user sees his comment immediately after saving it and does not have to wait (while seeing the “loading..” image) until the server responds with “success”.

----------

How can we start with this approach for our own applications immediately?
For example, lets look at the following ajax call:

```javascript
// Make AJAX request to create post for user
$.ajax("/user/post", {
  type: "POST”,
  data: { data: this.data },
  dataType: "json”,
  success: function(data) {
 	// Render new post in the UI
	renderNewPost(data);
  },
  error: function(data) {
    // Notify the user on error
  }
});

```

Let’s move up the “renderNewPost” section like this:

``` javascript
// Render new post in the UI
renderNewPost(this.data);
// Make AJAX request to create post for user
$.ajax("/user/post", {
  type: "POST”,
  data: { data: this.data },
  dataType: "json”,
  success: function(data) {
 	  },
  error: function(data) {
    // Notify the user on error
  }
});

```

This way our user will immediately see a response and  thinks that our user experience is great!

----------


### Summary

With “positive thinking” approach,  we can have a faster and more responsive product or website, even if you don’t have the best resources.

The main point to remember:
Change the UI according to your users action - assuming that the server will return “success” in most of the  scenarios.




> **Note**
This article is inspired by the “Boom Performance” lecture by Eran Zinman as hosted on #YGLF 2015 convention.

