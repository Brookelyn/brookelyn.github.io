---
layout: post
title: Filtering JSON data
excerpt: In which our hero parses some strings
---

One of the requirements of the [JSON API project]({% post_url 2016-02-04-first-test %}) that I've been working on is for the author of the photo and the image's publish date to display in a specific format - the author's name should display only their username, and the published date should read like the following: 'Published: 11 Feb 2016 at 11:06'.

This means that both need to be modified from what they originally pull in as from the JSON feed - where author comes across something like `nobody@flickr.com (IlikePotatoes!)` and the date comes across looking like `2016-02-22T10:23:17Z` - which I'm going to use Angular's filter functionality to do.

### Say my name

Getting the author's name to display correctly was my first step. This was fairly straightforward, as all I wanted to do was to take the string being fed in and get just the text between the parentheses:

{% highlight javascript %}
potato.filter('authorFilter', function() {
  return function(author) {
    var string = author;
    var authorString = string.substring(string.lastIndexOf("(")+1,string.lastIndexOf(")"));
    return authorString;
  }
});
{% endhighlight %}

As you can see, my filter is pulling in the author data then splitting the returned string at the `lastIndexOf` the opening parenthesis plus one, in order to ensure the character itself isn't pulled in, and ending at the `lastIndexOf` the closing parenthesis.

### Date and time

Displaying the date and time according to the spec was a bit more challenging. I'm sure there's a more elegant way to do it, but what I came up with fulfills the most important criteria of all: *it works*.

{% highlight javascript %}
potato.filter('pubDate', function() {
  return function(published){
    var fullDate = published;
    var year = fullDate.substring(0,4);
    var month = parseInt(fullDate.substring(5,7));
    var day = fullDate.substring(8,10);
    var time = fullDate.substring(fullDate.lastIndexOf("T")+1,fullDate.lastIndexOf(":"));

    var dayLast = day.charAt(day.length - 1);
    var timeFirst = time.charAt(0);

    // Removes superfluous '0' from published time
    if (timeFirst === "0") {
      time = time.replace("0", "");
    }

    // Adds suffix to day
    if (dayLast === 1){
      day = day + "st";
    } else if (dayLast === 2) {
      day = day + "nd";
    } else {
      day = day + "th";
    }

    // Converts month number to month name
    if (month === 01) {
      month = "Jan";
    } else if (month === 02){
      month = "Feb";
    } else if (month === 03){
      month = "Mar";
    } else if (month === 04){
      month = "Apr";
    } else if (month === 05){
      month = "May";
    } else if (month === 06){
      month = "Jun";
    } else if (month === 07){
      month = "Jul";
    } else if (month === 08){
      month = "Aug";
    } else if (month === 09){
      month = "Sep";
    } else if (month === 10){
      month = "Oct";
    } else if (month === 11){
      month = "Nov";
    } else if (month === 12){
      month = "Dec";
    }

    return day + " " + month + " " + year + " at " + time;
  }
});
{% endhighlight %}

As you can see, I'm again pulling in a string that I need to split into different parts. 

Most of the numbers in the string are fine to remain as strings as far as JavaScript is concerned - there's no reason, for example, that 2016 needs to be recognised as integers instead of a string. To display the month, however, I felt it was easier to convert the string into integers before converting the display to a three-letter string for the month (for example, 'Feb').

My filter is also removing any '0's for published times before 10:00, and adding a suffix to the date in order to achieve '22nd' instead of just '22'.

### Next steps

I've tweaked the styles of things a bit now and am much happier with how it's looking:

{:.center}
![]({{ site.baseurl }}/img/potato/potato-list-view-22-feb.png)

I still need to create a filter for the tags in my detail page, seperating them out and adding links so that clicking on each tag takes you to a search for that tag on Flickr. 

And there's a bit more functionality to add, too - but it finally feels like it's really beginning to get somewhere.