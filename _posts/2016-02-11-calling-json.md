---
layout: post
title: Show me the data
excerpt: In which our hero manages to actually get what she's looking for
---

I've started refactoring my JSON API project, and managed to get Bootstrap working. It was *entirely* down to me feeling the pressure for the first time when it comes to code and allowing my usual unflappable nature when working to a deadline to be overwhelmed by attempting to do ALL THE THINGS.

Basically, I'd remembered to include the Bootstrap script, but not the stylesheet - a complete rookie mistake that I shall not be making again!

### Bastard won't return my calls

Next to be addressed was getting the JSON data to not only display correctly in my main feed, but to pull through the correct data for a detail page that could be reached by clicking on the image or title on the main page as per the wireframes.

As I'm no longer attempting to impress a potential employer and I had two more weeks left with Bloc, and as I'd spent about three hours finding Stack Overflow posts that weren't quite helpful enough for me to solve this, I asked Mentor Ben for a bit of help. 

Below is the factory that I'd originally set up to call the JSON feed, which was displaying correctly on the main page:

{% highlight javascript %}
potato.factory('PotatoPics', function($http) {
  return {
    getPics: function(callback) {
      return $http.jsonp('https://api.flickr.com/services/feeds/photos_public.gne?tags=potato&tagmode=all&format=json&jsoncallback=JSON_CALLBACK')
      .success(function(data) {
        callback(data);
      })
      .error(function(data){
        console.log('Error');
      });
    }
  };
});
{% endhighlight %}

The above was working absolutely fine, but I was having real difficulty figuring out how to get the listing at any particular index to display when clicking through to the detail page. 

### Boo-ya, baby!

After working together with Mentor Ben, we arrived at a solution that I not only understand but will also let me proceed with everything else I want to do.

First, I need to tell my HTML exactly what to call. The link had been set up with a placeholder - `<a href="/detail">` - so that I was able to provide a click-through and I could style the detail page appropriately. As I'm using the `ui-router` function of Bootstrap, this changes to `<a ui-sref="detail({id: $index})">`. 

This is accompanied by a change to the `$stateProvider` handling the detail page, which now directs to `url: '/detail/:id'`. 

These two changes mean that when the relevant object is clicked, it should go through to the `/detail` page and pass across the object from that index.

My factory also looks completely different:

{% highlight javascript %}
potato.factory('PotatoPics', function($http) {

  var json;

  function getJSON(callback) {
    return $http.jsonp('https://api.flickr.com/services/feeds/photos_public.gne?tags=potato&tagmode=all&format=json&jsoncallback=JSON_CALLBACK')
    .success(function(data) {
      json = data;
      callback(data);
    })
    .error(function(data){
      console.log('Error');
    });
  }

  return {
    getPics: function(callback) {
      if (json) {
        return json;
      } else {
        getJSON(callback);
      }
    },
    getDetail: function(id, callback) {
      if (json) {
        return callback(json.items[id]);
      } else {
        getJSON(function() {
          return callback(json.items[id]);
        });
      }
    }
  };
});
{% endhighlight %}

Let's run through what everything is doing.

First, we set up an empty variable, `json`, that we'll be using for caching purposes. We've also split out the function, `getJSON`, that actually calls the JSON feed as we're going to need to access the data in more than one controller.

Then we tell the app what to do in `getPics` and `getDetail`. Both are essentially doing the same thing: if we've already called our data, please return that; if we haven't called our data, please get it using the `getJSON` function. The only difference is that in `getDetail` we're telling it that there is a parameter - the id, which is actually the index from the main feed - to expect, which lets us access the specific object at that index in the wider array.

This means that I'm now able to access the correct information in order to set up the click-through to the detail of each image, just as required.