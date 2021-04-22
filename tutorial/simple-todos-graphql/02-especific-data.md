---
title: "2: Loading Specific Data to the Minimongo"
---

Before doing our queries and mutations with GraphQL, we'll first load fewer data to the Minimongo and the rest of the data we'll fetch with GraphQL later.

## 2.1 Meteor Livedata

Meteor is great to use with reactive data. That's why it's so easy to create an app like our to-do that exchange data between client and server without any problems in a fast way. But, when our app starts to scaling up and bringing more and more data from the server or sending to it, the application can get slower. 

That doesn't mean a problem with Meteor. Meteor's DDP protocol is a super-fast method to send and receive data, but as expected, the bigger the data, the longer will take to transport it. You can learn more about DDP [here](https://github.com/meteor/meteor/blob/devel/packages/ddp/DDP.md).

So, as uncle Ben said: "With great power comes great responsibility". Meteor's DDP protocol is a really powerful tool, but if you don't use it right, you can make your app slow.

## 2.2 Filtering Data

GraphQL is a different approach of Meteor's DPP on how to exchange data between server and client, but with Meteor, you can use both approaches together, and this is exactly what we'll do.

So, in [this step](https://react-tutorial.meteor.com/simple-todos/09-publications.html#9-2-Tasks-Publication) on the Simple Todo tutorial we created a publication the expose all the task data to be used in the client.

We'll keep using the subscription just to keep track in changes on the state of tasks when they're finished or not. So, from all that data, we in keep just the props `_id`, `isChecked`, and `userId`.


Go ahead and change the update the `Meteor.publish` inside the `tasksPublication`.

`import/api/tasksPublication.js`

```js
..
Meteor.publish('tasks', function publishTasks() {
  return TasksCollection.find(
    { userId: this.userId },
    { fields: { _id: 1, isChecked: 1, userId: 1 } }
  );
});
```

Your app should look like this now:

<img width="300px" src="/simple-todos-graphql/assets/step02-tasks-no-name.png"/>


This is happening because we're not getting the text data anymore. You can check, all the data that you have in the client, on you Minimongo:


<img width="600px" src="/simple-todos-graphql/assets/step02-minimongo.png"/>


As you can see, we just have what we asked for: `_id`, `isChecked`, and `userId`.

> Review: you can check how your code should be in the end of this step [here](https://github.com/meteor/react-tutorial/tree/master/src/simple-todos-graphql/step02)

In the next step we'll create our first query and using GraphQL.