# Meteor Method Hooks

### Before/after hooks for Meteor methods

This package extends Meteor with four methods:
* `Meteor.beforeMethods` 
* `Meteor.afterMethods`
* `Meteor.beforeAllMethods` 
* `Meteor.afterAllMethods`

This package differs from hitchcott:method-hooks in that:
* You can add hooks for all methods
* It works on both client and server
* You can add and remove hooks at runtime. 
* After methods can change the methods result

The `beforeMethods` method can be used for securing `Meteor.methods` based on the result of a definable function.
Any `beforeMethods` that throws an error will stop the relevant method and any other hooks from executing.
If you want to prevent further execution without triggering an error, you can just return 'false' from within your hook.

Here's an example for checking user login:

```js
Meteor.beforeMethods('test',function(){
  if(!Meteor.userId()) throw new Meteor.Error(403,"Forbidden");
})
```
You can also pass an array of method names as first parameter.

Uses include:

* Security
* Logging
* [insert imaginative idea]

The before methods get the same arguments as the original method, 

The after method can get the current result from `this._result`.
If it returns a value that is not undefined, then this will replace the original result.

## TODO
* Testing

## Credits
Inspired by: [Chris Hitchcott](https://github.com/hitchcott/meteor-method-hooks), 2015