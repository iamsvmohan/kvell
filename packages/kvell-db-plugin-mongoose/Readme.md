# Mongoose Plugin for Kvell

`Kvell-db-plugin-mongoose` wraps up [mongoose](https://mongoosejs.com/) and exposes all three values required to be exposed by a kvell database plugin.

## Install

```sh
npm i kvell-db-plugin-mongoose
```

## Configuration Variables

Internally, `kvell-db-plugin-mongoose` will instantiate the database object using `mongoose.connect` method.

[Documentation for mongoose](https://mongoosejs.com/docs/index.html)

## Usage

To use it, just install the package and add a `databasePlugin` object in `kvell.config.js` with the following fields:

- `resolve`: Name of the plugin, i.e, **kvell-db-plugin-mongoose**

- `options`: All the parameters that you need to pass in the mongoose constructor. The following key is **<u>mandatory</u>**:

  - `mongoConnectionString` (string): The connection string for the mongoose server.

- `showConnectionMessage` (boolean): If set to `true`, a success message will be logged on the console once the connection is successfully established.

By default, the following options are taken as true while instantiating the mongoose instance:

- `useNewUrlParser`
- `useUnifiedTopology`

You may choose to override it by simply adding these keys as fields in the `options` field of the object.

The plugin exports the following:

- dbLib: The `mongoose` object. Check [mongoose docs](https://mongoosejs.com/docs/index.html) for complete api reference.
- dbInstance: The instantiated `mongoose` instance. In this case, both dbLib and dbInstance will be basically the same objects.

- initHandler: (not for use)

Example Usage

- **kvell.config.js**:

```javascript
databasePlugins: [
  {
    resolve: "kvell-db-plugin-mongoose",
    options: {
      mongoConnectionString: "mongodb://localhost:27017/test",
      options: {},
      showConnectionMessage: false
    }
  }
];
```

- **userModel.js**:
```javascript
const mongoose = require("kvell-db-plugin-mongoose").dbInstance;

// Create your User model's schema here and export it.

const userSchema = new mongoose.Schema({
  name: String,
  email: String,
  password: String,
  age: Number
});

const User = mongoose.model("User", userSchema);

module.exports = User;
```
