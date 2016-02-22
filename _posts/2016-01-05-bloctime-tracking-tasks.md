---
layout: post
title: Bloctime - Tracking tasks
---
The next and final step in the Bloctime project - bar the extra credit stories - is to allow the user to add and keep track of the tasks they're using the app to time.

### Handling tasks

In the Blocitoff project, we were given the option of using either a factory or directive to control the addition of information to Firebase. In that instance I used a directive, as at the time it seemed the simplest way to handle it.

This time, having a better understanding how Firebase works and how it interacts with Angular, I decided to use a factory. `Task` sets up an array to keep track of adding, removing and displaying tasks:

{% highlight javascript linenos %}
bloctime.factory('Task', ['$firebaseArray', function($firebaseArray) {
  var fbRef = new Firebase("https://brookelyn-bloctime.firebaseio.com/tasks");
  var tasks = $firebaseArray(fbRef);

  return {
    add: function(task) {
      var addTask = tasks.$add({
        name: task.text,
        date: Firebase.ServerValue.TIMESTAMP,
        completed: false
      });
      return addTask;
    },
    delete: function(task) {
      return tasks.$remove(task);
    },
    all: function() {
      return tasks;
    }
  }
}]);
{% endhighlight %}

This is then referred to in the directive controlling the page when adding or deleting a task from the list:

{% highlight javascript linenos %}
$scope.addTask = function() {
  Task.add($scope.task);
  $scope.task = {};
}

$scope.deleteTask = function(task) {
  Task.delete(task).then(function(ref) {
    if (ref.key() === task.$id) {
      // success
    } else {
      // failure
    }
  })
};
{% endhighlight %}

Tasks are displayed from oldest to newest using a filter in `ngRepeat` in the HTML.

###What next for Bloctime?
I'm at the stage in my Bloc apprenticeship where I need to start creating a portfolio and sorting out my CV in order to start applying for, you know, a real job.

For this reason, I'm going to be setting aside Bloctime at this point, although there's quite a lot that I'd like to add to the app - for example, setting it up so that to use it you need to sign in so that it can handle multiple users, displaying completed tasks under a second tab and linking up the tasks with the countdown timer so that selecting a task from your list starts the timer for you.

So just a few things, then... :)