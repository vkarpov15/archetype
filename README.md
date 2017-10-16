# archetype

<img src="https://i.imgur.com/TW4rq2f.png">

Archetype is a library for casting and validating objects. It has exceptional support for deeply nested objects, type composition, custom types, and geoJSON.

[![CircleCI](https://circleci.com/gh/boosterfuels/archetype.svg?style=svg)](https://circleci.com/gh/boosterfuels/archetype)

```javascript
const { ObjectId } = require('mongodb');
const moment = require('moment');

// `Person` is now a constructor
const Person = new Archetype({
  name: 'string',
  bandId: {
    $type: ObjectId,
    $required: true
  },
  createdAt: {
    $type: moment,
    $default: () => moment()
  }
}).compile('Person');

const test = new Person({
  name: 'test',
  bandId: '507f191e810c19729de860ea'
});

test.bandId; // Now a mongodb ObjectId
test.createdAt; // moment representing now
```

If casting fails, archetype throws a nice clean exception:

```javascript
try {
  Person({ // <-- calling with `new` is optional
    name: 'test',
    bandId: 'ImNotAValidObjectId'
  });
} catch(error) {
  error.errors['bandId'].message; // Mongodb ObjectId error
}
```

[Archetypes are composable, inspectable, and extendable via `extends`.](http://thecodebarbarian.com/casting-mongodb-queries-with-archetype.html)

## Connect

Follow [archetype on Twitter](https://twitter.com/archetype_js) for updates, including our gists of the week. Here's some older gists of the week:

* [20171013](https://gist.github.com/vkarpov15/1520cfb604972e81198db028e4606809)
* [20171006](https://gist.github.com/vkarpov15/e03dafb2ac478cb38ff3fbe4c36139d6)
