#batch.js
batch.js is a Node.js module that defines the Batch object.

##High Level View
Batch is essentially an object that holds an animation frame and an array of jobs to be performed which may or may not change the animation frame.

Jobs can be added with `Batch.queue` (or `Batch.add` if the job requires arguments). The jobs will either be run through `Batch.sync`, which will be listening for new jobs in `Batch.jobs`, or they will be run via `Batch.request_frame` if `Batch.sync` is undefined or otherwise false.

##Batch constructor:
* Allows instantiation of `Batch` with or without the `new` keyword.
* Sets `Batch.sync` to the `sync` argument
* Binds the `Batch` object to its `run` method so the `Batch` object will be available when `Batch.run` is used as a callback.

##Batch methods:
###queue(fn)
Runs the function `fn` and all other functions in `Batch.jobs`.

###request_frame()
Has no effect if `Batch.frame` is defined, otherwise it assigns `Batch.frame`.

###run()
Runs all jobs in `Batch.jobs` and clears `Batch.jobs`.

###add(fn)
Has same effect as `Batch.queue`, but returns a function which you can pass arguments to, whereas `Batch.queue` does not support arguments.

##Other functions:
###requestAnimationFrame(callback)
`requestAnimationFrame` looks in the Node.js global namespace for several different functions that request animation frames, defaulting to an in-lined function `timeout` which calls the callback (usually `Batch.run`) after a 60th of a second. This delay can enforce a 60 fps frame rate for a animation.

##Other Notes:
This code uses a mix of snake_case and camelCase. That is, `Batch` methods are written with underscores between words like `Batch.request_frame` and the extra function `requestAnimationFrame` has no extra characters between words and instead capitalizes the first character of each additional word. This may be an intentional choice to make object methods look different than functions not associated with objects, but camelCase is the preferred convention for JavaScript so some developers might find this choice surprising.
