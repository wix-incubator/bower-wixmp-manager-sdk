# Events

## wixmp.events.on(eventName, listener)
Subscribe listener to event
```js
wixmp.events.on(wixmp.events.FOLDERS.LIST, myListener)
```

### eventName {String}
Name of event for subscribing. All events names you can find at **wixmp.events**
```js
wixmp.events.FOLDERS.LIST
```

### listener(promise, event) {Function}
Event listener is invoked when the corresponding method is called. Listener receives promise of the future result
and the event object.

```js
function(promise, event){

  // code before action

  promise.then(
    function (data) {
       // success
    },
    function (reason) {
       // fail
    }
  )
}
```


#### promise {Promise}
Promise that will be resolved or rejected on action complete.<br>
For more documentation visit [BlueBird Promise library](https://github.com/petkaantonov/bluebird/blob/master/API.md)

##### promise.then(success, fail) {Function}

###### success(data) {Function}
Function will be called when action was completed successfully
```js
/**
* @param data {Object|Array}
*/
function (data) {
  // do something
}
```

###### fail(error) {Function}
Function will be called when action was failed
```js
/**
* @param error {Object}
*/
function (error) {
  // do something
}
```
###### error {Object}
Error object contains `code`, `message` and additional `data` regarding the error event.

| code |        message           | meaning
|------|--------------------------|--------
| -200 | Internal JS Error        |
| -201 | Internal JS Error        | The request failed by network failure
| -406 | Internal JS Error        | File is invalid
| -100 | Abort                    | Activity is canceled by user
| 400  | Bad Request              |
| 401  | Unauthorized             | The request implemented by non-authorized user
| 403  | Forbidden                | The request is not allowed for the current user
| 404  | Not Found                | The request resource or data is not found
| 408  | Timeout                  | The request was failed by timeout
| 500  | Internal Server Error    |

For example:
```js
{
  code:  404,
  message: 'Not Found',
  data: {
    guid: 'Can not find category by guid or legacy key.'
  }

}
```



#### event {Object}
Event data

If you write your own Source, you can add additional attributes there by **params** object:

```js
emit(this, wixmp.events.FOLDERS.LIST, params)
```

The structure of the `event` object in the callback will be the following:

```js
{
  eventName:   'folders.list',  // {String} name of event
  eventTarget: privateSource,   // {Object} where event was emitted
  arguments:   ['123']          // {Arguments} arguments of source method. For sources only
}
```


## wixmp.events.off(eventName, listener)
Unsubscribe listener from an event
```js
wixmp.events.off(wixmp.events.FOLDERS.LIST, myListener)
```
### eventName {String}
Name of event for unsubscribing. All events names you can find at **wixmp.events**
```js
wixmp.events.FOLDERS.LIST // 'folders.list'
```

### listener {Function}
Event listener that was subscribed before


## emit(eventTarget, eventName, params) {resolve: resolve, reject: reject}
This function allows to emit events from custom Source. It is passed to the source constructor as an argument.

```js
function CustomSource (customSettings, emit, http) {

  this.loadSomeData = function () {
    // generate event
    var event = emit(this, wixmp.events.FOLDERS.LIST);

    // do something

    // resolve event
    event.resolve(data)
  }
}
```

### eventTarget {Object}
From where event was emitted. It is an instance of the source.

### eventName {String}
Name of event for emitting.

All predefined events names you can find at **wixmp.events**<br>
Also, you can emit your own event.

```js
wixmp.events.FOLDERS.LIST
```

### params {Object}
Additional params that need to be passed to [event](#event-object)
```js
{
  attribute: 'value'
}
```

### returns {Object} {resolve: resolve, reject: reject}

#### resolve(data) {Function}
Resolve event with specified data

#### reject(error) {Function}
Resolve event with error. See [error](#error-object)


## wixmp.events {Object}
List of events names by namespaces

```js
{
  FOLDERS: {
    LIST:   'folders.list',
    REMOVE: 'folders.remove'
  },
  FOLDER: {
    CREATE: 'folder.create',
    UPDATE: 'folder.update',
    REMOVE: 'folder.remove'
  },
  ITEMS: {
    LIST:   'items.list',
    SEARCH: 'items.search',
    REMOVE: 'items.remove',
    UPLOAD: 'items.upload',
    UPLOAD_BY_URL: 'items.uploadByUrl'
  },
  ITEM: {
    GET: 'item.get',
    UPDATE: 'item.update',
    REMOVE: 'item.remove',
    UPLOAD: 'item.upload',
    UPLOAD_BY_URL: 'item.uploadByUrl'
  }
}
```
