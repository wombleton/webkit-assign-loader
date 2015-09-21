# webkit-assign-loader

Due to [WebKit issue #138038][], assigning to a property on an object created
with `Object.create` may result in the error `TypeError: Attempted to assign to
readonly property.`. This bug is known to affect iOS 8 users and is particularly
likely to happen in recent versions of [Angular.js][] (at least version
`1.4.2`).

This utility rewrites the following code

```js
object.$$a = 5;
```

to this

```js
var __webkitAssign__$$a = '$$a';
object[__webkitAssign__$$a] = 5;
```

as a workaround to prevent a `TypeError`.

(Copied from https://github.com/StoryCloud/webkit-assign/blob/master/README.md)

## Usage

    npm i -D webkit-assign-loader

    // webpackConfig.js (an excerpt)

    {
      module: {
        loaders: [
          {
            test: /angular\.js$/,
            loader: 'webkit-assign-loader'
          }
        ]
      }
    }
