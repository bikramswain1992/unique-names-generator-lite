# Unique Names Generator Lite
<!-- ALL-CONTRIBUTORS-BADGE:START - Do not remove or modify this section -->
[![All Contributors](https://img.shields.io/badge/all_contributors-10-orange.svg?style=flat-square)](#contributors-)
<!-- ALL-CONTRIBUTORS-BADGE:END -->


[![](https://img.shields.io/npm/l/unique-names-generator.svg)](https://github.com/andreasonny83/unique-names-generator/blob/main/LICENSE)


> More than 50,000,000 name combinations out of the box

## What is Unique name generator lite?

Unique name generator lite is a derivative work of the popular package Unique name generator. It provides a curated list of dictionaries to generate unique and memorable names which is lightweight and tree-shakeable.

It comes with a list of dictionaries out of the box, but you can also provide your custom ones.

## Docs

This documentation is for the `unique-names-generator-lite` v1.


## Table of contents

- [Unique Names Generator Lite](#unique-names-generator-lite)
  - [What is Unique name generator lite?](#what-is-unique-name-generator-lite)
  - [Docs](#docs)
    - [Migrating to v4](#migrating-to-v4)
  - [Table of contents](#table-of-contents)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Usage](#usage)
    - [Typescript support](#typescript-support)
  - [API](#api)
    - [uniqueNamesGenerator (options)](#uniquenamesgenerator-options)
    - [options](#options)
      - [dictionaries](#dictionaries)
      - [separator](#separator)
      - [length](#length)
      - [style](#style)
      - [seed](#seed)
  - [Dictionaries available](#dictionaries-available)
      - [Numbers](#numbers)
      - [Adjectives](#adjectives)
      - [Animals](#animals)
      - [Colors](#colors)
    - [Default dictionaries](#default-dictionaries)
    - [Custom dictionaries](#custom-dictionaries)
    - [Numbers Dictionary](#numbers-dictionary)
  - [Numbers Dictionary API](#numbers-dictionary-api)
    - [generate (options)](#generate-options)
    - [options](#options-1)
      - [min](#min)
      - [max](#max)
      - [length](#length-1)
    - [Combining custom and provided dictionaries](#combining-custom-and-provided-dictionaries)
  - [Migration guide](#migration-guide)
    - [Migration guide from version 3 to version 4](#migration-guide-from-version-3-to-version-4)
      - [Mandatory `dictionaries` config](#mandatory-dictionaries-config)
    - [Migration guide from version 1 or 2](#migration-guide-from-version-1-or-2)
      - [uniqueNamesGenerator](#uniquenamesgenerator)
      - [Separator](#separator-1)
      - [Short](#short)
  - [Contributing](#contributing)
  - [License](#license)
  - [Contributors ✨](#contributors-)

## Prerequisites

This project requires NodeJS (at least version 18) and NPM.
[Node](http://nodejs.org/) and [NPM](https://npmjs.org/) are really easy to install.
To make sure you have them available on your machine,
try running the following command.

```sh
$ node --version
v18.0.0
```

## Installation

**BEFORE YOU INSTALL:** please read the [prerequisites](#prerequisites)

Install the package using npm or Yarn

```sh
$ npm i -S unique-names-generator-lite
```

Or using Yarn

```sh
$ yarn add unique-names-generator-lite
```

## Usage

```js
import { uniqueNamesGenerator, adjectives, colors, animals } from 'unique-names-generator';

const randomName = uniqueNamesGenerator({ dictionaries: [adjectives, colors, animals] }); // big_red_donkey

const shortName = uniqueNamesGenerator({
  dictionaries: [adjectives, animals, colors], // colors can be omitted here as not used
  length: 2
}); // big-donkey
```

### Typescript support

This package export a type definition file so you can use it, out of the box,
inside your Typescript project.

```typescript
import { uniqueNamesGenerator, Config, adjectives, colors, animals } from 'unique-names-generator';

const customConfig: Config = {
  dictionaries: [adjectives, colors],
  separator: '-',
  length: 2,
};

const randomName: string = uniqueNamesGenerator({
  dictionaries: [adjectives, colors, animals]
}); // big_red_donkey

const shortName: string = uniqueNamesGenerator(customConfig); // big-donkey
```

## API

### uniqueNamesGenerator (options)

Returns a `string` with a random generated name

### options

Type: `Config`

#### dictionaries

Type: `array`

required: `true`

This is an array of dictionaries. Each dictionary is an array of strings containing the words to use for generating the string.

The [provided dictionaries](#dictionaries-available) can be imported from the library as a separate modules and provided in the desired order.

```typescript
import { uniqueNamesGenerator, adjectives, colors, animals } from 'unique-names-generator';

const shortName: string = uniqueNamesGenerator({
  dictionaries: [colors, adjectives, animals]
}); // red_big_donkey
```

Read more about the dictionaries and how to use them, in the [Dictionaries](#dictionaries-available) section.

#### separator

Type: `string`

required: `false`

Default: `_`

A string separator to be used for separate the words generated.
The default separator is set to `_`.

#### length

Type: `number`

required: `false`

Default: `3`

The default value is set to `3` and it will return a name composed of 3 words.
This values must be equal or minor to the number of [dictionaries](#dictionaries-available) defined (3 by default).
Setting the `length` to a value of `4` will throw an error when only 3 dictionaries are provided.

#### style

Type: `lowerCase | upperCase | capital`

required: `false`

Default: `lowerCase`

The default value is set to `lowerCase` and it will return a lower case name.
By setting the value to `upperCase`, the words, will be returned with all the letters in upper case format.
The `capital` option will capitalize each word of the unique name generated

```typescript
import { uniqueNamesGenerator, adjectives, colors, animals } from 'unique-names-generator';

const capitalizedName: string = uniqueNamesGenerator({
  dictionaries: [colors, adjectives, animals],
  style: 'capital'
}); // Red_Big_Donkey

const upperCaseName: string = uniqueNamesGenerator({
  dictionaries: [colors, adjectives, animals],
  style: 'upperCase'
}); // RED_BIG_DONKEY

const lowerCaseName: string = uniqueNamesGenerator({
  dictionaries: [colors, adjectives, animals],
  style: 'lowerCase'
}); // red_big_donkey
```

#### seed

Type: `number | string`

required: `false`

A seed is used when wanting to deterministically generate a name. As long as the provided seed is the same the generated name will also always be the same.

```typescript
import { uniqueNamesGenerator, adjectives, colors, animals } from 'unique-names-generator';
const config: Config = {
  dictionaries: [adjectives, colors, animals],
  separator: '-',
  seed: 120498,
};

const nameFromSeed: string = uniqueNamesGenerator(config); // continuous-gray-dragonfly
```

```typescript
import { uniqueNamesGenerator, adjectives, colors, animals } from 'unique-names-generator';
const config: Config = {
  dictionaries: [adjectives, colors, animals],
  separator: '-',
  seed: 'you can use strings as a seed',
};

const nameFromSeed: string = uniqueNamesGenerator(config); // stable-crimson-porpoise
```

## Dictionaries available

#### Numbers

This is a dynamic dictionary. Read more in the [Numbers Dictionary](#numbers-dictionary) section

#### Adjectives

A list of more than 1,400 adjectives ready for you to use

```typescript
import { uniqueNamesGenerator, Config, adjectives } from 'unique-names-generator';

const config: Config = {
  dictionaries: [adjectives]
}

const characterName: string = uniqueNamesGenerator(config); // big
```

#### Animals

A list of more than 350 animals ready to use

```typescript
import { uniqueNamesGenerator, Config, animals } from 'unique-names-generator';

const config: Config = {
  dictionaries: [animals]
}

const characterName: string = uniqueNamesGenerator(config); // donkey
```

#### Colors

A list of more than 50 different colors

```typescript
import { uniqueNamesGenerator, Config, colors } from 'unique-names-generator';

const config: Config = {
  dictionaries: [colors]
}

const characterName: string = uniqueNamesGenerator(config); // red
```


### Default dictionaries

By default, the Unique name generator library comes with 3 dictionaries out of the box, so that you can use them
straight away.
Starting from the version 4 of the library, however, you must explicitly provide the dictionaries within the
configuration object.
This is for reducing the bundle size and allowing tree shaking to remove the extra dictionaries from your bundle when
using custom ones.

The new syntax for using the default dictionaries is the following:

```typescript
import { uniqueNamesGenerator, Config, adjectives, colors, animals } from 'unique-names-generator';

const config: Config = {
  dictionaries: [adjectives, colors, animals]
}

const characterName: string = uniqueNamesGenerator(config); // red_big_donkey
```

### Custom dictionaries

You might want to provide your custom dictionaries to use for generating your unique names,
in order to meet your business requirements.

You can easily do that using the [dictionaries](#dictionaries-available) option.

```typescript
import { uniqueNamesGenerator } from 'unique-names-generator';

const starWarsCharacters = [
  'Han Solo',
  'Jabba The Hutt',
  'R2-D2',
  'Luke Skywalker',
  'Princess Leia Organa'
];
const colors = [
  'Green', 'Red', 'Yellow', 'Black'
]

const characterName: string = uniqueNamesGenerator({
  dictionaries: [colors, starWarsCharacters],
  length: 2,
  separator: ' '
}); // Green Luke Skywalker
```

### Numbers Dictionary

You can easily generate random numbers inside your unique name using the Numbers dictionary helper.

```typescript
import { uniqueNamesGenerator, NumberDictionary } from 'unique-names-generator';

const numberDictionary = NumberDictionary.generate({ min: 100, max: 999 });
const characterName: string = uniqueNamesGenerator({
dictionaries: [['Dangerous'], ['Snake'], numberDictionary],
  length: 3,
  separator: '',
  style: 'capital'
}); // DangerousSnake123
```

## Numbers Dictionary API

### generate (options)

Returns a `string` with a random generated number between 1 and 999

### options

Type: `Config`

#### min

Type: `number`

required: `false`

default: `1`

The minimum value to be returned as a random number

#### max

Type: `number`

required: `false`

default: `999`

The maximum value to be returned as a random number

#### length

Type: `number`

required: `false`

The length of the random generated number to be returned.

Setting a length of 3 will always return a random number between `100` and `999`. This is the same as setting `100` and `999` as `min` and `max` option.

**Note** If set, this will ignore any `min` and `max` options provided.


### Combining custom and provided dictionaries

You can reuse the dictionaries provided by the library.
Just import the ones that you need and use them directly in your app.

```typescript
import { uniqueNamesGenerator, adjectives, colors } from 'unique-names-generator';

const improvedAdjectives = [
  ...adjectives,
  'abrasive',
  'brash',
  'callous',
  'daft',
  'eccentric',
];
const xMen = [
'professorX',
'beast',
'colossus',
'cyclops',
'iceman',
'wolverine',
];

const characterName: string = uniqueNamesGenerator({
  dictionaries: [improvedAdjectives, color, xMen],
  length: 2,
  separator: '-'
}); // eccentric-blue-iceman
```

## Contributing

Please read [CONTRIBUTING.md](CONTRIBUTING.md) for details on our code of conduct, and the process for submitting pull requests to us.

1.  Fork it!
2.  Create your feature branch: `git checkout -b my-new-feature`
3.  Add your changes: `git add .`
4.  Commit your changes: `git commit -am 'Add some feature'`
5.  Push to the branch: `git push origin my-new-feature`
6.  Submit a pull request :sunglasses:

## License

[MIT License](https://github.com/bikramswain1992/unique-names-generator-lite/blob/main/LICENSE)

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

This project follows the [all-contributors](https://github.com/all-contributors/all-contributors) specification. Contributions of any kind welcome!
