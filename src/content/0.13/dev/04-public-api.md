Most of the time, you will be using Karma directly from the command line.
You can, however, call Karma programmatically from your node module. Here is the public API.


## karma.Server(options, [callback=process.exit])

### Constructor

```javascript
var Server = require('karma').Server
var server = new Server({port: 9876}, function(exitCode) {
  console.log('Karma has exited with ' + exitCode)
  process.exit(exitCode)
})
```

### **server.start()**

Equivalent of `karma start`.

```javascript
server.start()
```

### Events

The `server` object is an [`EventEmitter`](https://nodejs.org/docs/latest/api/events.html#events_class_events_eventemitter). You can simply listen to events like this:

```javascript
server.on('browser_register', function (browser) {
  console.log('A new browser was registered')
})
```

### `browser_register`
**Arguments:**

* `browser`: The browser instance

A new browser was opened, but is not ready yet.

### `browser_error`
**Arguments:**

* `browser`: The browser instance
* `error`: The error that occured

There was an error on this browser instance.

### `browser_start`
**Arguments:**

* `browser`: The browser instance
* `info`: Details about the run

A test run is beginning in this browser.

### `browser_complete`
**Arguments:**

* `browser`: The browser instance
* `result`: Test results

A test run has completed in this browser.

### `browsers_change`
**Arguments:**

* `browsers`: A collection of browser instances

The list of browers has changed.

#### `browsers_ready`

All browsers are ready for execution

### `run_start`
**Arguments:**

* `browsers`: A collection of browser instances on which tests are excuted

A test run starts.

### `run_complete`
**Arguments:**

* `browsers`: A collection of browser instances
* `results`: A list of results

A test run was completed.

## karma.runner

### **runner.run(options, [callback=process.exit])**

Equivalent of `karma run`.

```javascript
var runner = require('karma').runner
runner.run({port: 9876}, function(exitCode) {
  console.log('Karma has exited with ' + exitCode)
  process.exit(exitCode)
})
```

## Callback function notes

- If there is an error, the error code will be provided as the second parameter to the error callback.