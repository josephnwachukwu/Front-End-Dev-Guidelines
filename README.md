# Front End Development Guidelines and Best Practices 2018


## Introduction

This document contains the guidelines and best practices for a front-end web development team. It was created by compiling the most common best practices among the best development firms spanning many industry and company sizes.

This document is not intended to replace common sense, conventions requested by particular clients, teams, or prevent expressive or creative solutions to problems. Team or project-specific agreements or client requests will always supersede this document's content.

Each item here represents either:

1. A reminder to follow existing standards or industry conventions,
2. guidance on what constitutes professional patterns and organization, or
3. a decision made favoring one method over its alternatives.

### Goals

Our motivations in creating this document are to:

1. Foster code consistency across our projects.
2. Facilitate ease of maintenance.
3. Ensure we create professional quality Web sites.
4. Guide staff on-boarding or educate new developers.


### General Standards

### Deliverables

### Development

#### NodeJs


#### Setting up Editors

## HTML

### HTML Markup Best Practices

Please follow conventions established for a given project so all team members can have the same expectations around document structure and markup.

Structural consistency is critical when talking about the types of pages being used on a site or in a Web app. The markup structure provides all the necessary hooks for scripting and behavior, so it's important that the appropriate hooks are in place.

A clear, clean, and concise HTML structure is also necessary for semantics, flexibility, and a reliable deployment environment. Do not deviate from established templates or patterns without architect approval.

## CSS

### CSS Best Practices

### Choosing frameworks

### Style Guides and Documentation
Aside from any branding guides that may be already avaialbe, It is suggested that you document your code with something like [Compodoc](https://github.com/compodoc/compodoc).

## JavaScript

### Style Guide

Use Basic rules similar to [JavaScript Standard Stye](https://standardjs.com/) :

* 2 spaces – for indentation
* Single quotes for strings – except to avoid escaping
* No unused variables – this one catches tons of bugs!
* No semicolons
* Always use === instead of == – but obj == null is allowed to check null || undefined.
* Always handle the node.js err function parameter
* Declare browser globals with /* global */ comment at top of file Prevents accidental use of vaguely-named browser globals like open, length, event, and name. Example: /* global alert, prompt */ Exceptions are: window, document, and navigator


### Code Commenting 

Use JSDoc Method for code commenting. You can learn more about JSDoc [here](http://usejsdoc.org/).

JSDoc enables developers to generate documentation from comments within a Javascript codebase. It also forces a commenting style
throughout a codebase as an added benefit.

#### Table of Contents
* [Intro](#intro)
* [Installation](#installation)
* [Files](#files)
* [Namespaces](#namespaces)
* [Modules](#modules)
* [Functions](#functions)
* [Classes](#classes)
* [Variables and Constants](#variables-and-constants)
* [Links](#links)
* [Examples](#examples)
* [Tips](#tips)

All JSDoc comments are of the forms:

*Single line:*
```js
/** jsdoc comment here */
```

*Multiple lines:*
```js
/** 
 *  jsdoc comment here
 *  and here
 *  and even here
 */
```

JSDoc leverages tags preceeded with the @ symbol in order to
keep track of relationships within the comments. For example
one can describe a function like this:

```js
/**
 * Takes 2 numbers and returns their sum.
 * @param   {number} a the first number
 * @param   {number} b the second number
 *
 * @returns {number} the sum of a and b
 */
function addNumbers(a, b) {
  return a + b;
}
```
Notice how different types of tags are separated by an empty
comment line. This helps with the readability of JSDoc tags.
Note, the untagged description line isn't separated by an 
empty line from the first tag.

The first * of each line is vertically aligned. The type,
parameter name, and descriptions are vertically aligned
as well.

In the following section, we'll go over how to leverage and
group tags throughout a javascript code base.

#### Installation
Prerequisite: Install and setup [npm](http://www.npmjs.com/) 
and [gulp](http://gulpjs.com/).

Open up your shell in your project's root directory.

Install the most stable version of **JSDoc** and save into your 
package.json file using the following command:

```sh
npm install git+git+https://github.com/jsdoc3/jsdoc.git -s
```
Also install and add **gulp-shell** to your package.json file:

```sh
npm install gulp-shell -s
```

Create a file named **conf.json** with the following inside of
it in your main directory:

```json
{
    "tags": {
        "allowUnknownTags": true
    },
    "source": {
        "include": ["lib"],
        "exclude": [],
        "includePattern": ".+\\.js(doc)?$",
        "excludePattern": "(^|\\/|\\\\)_"
    },
    "plugins": [],
    "templates": {
        "cleverLinks": false,
        "monospaceLinks": false
    },
    "opts": {
        "recurse": true,
        "private": true
    }
}
```

In the **include** array, add the relative paths to
any folders or files you would like JSDoc to create 
documentation for. Here, recurse is set to true, so 
adding a folder will add all files within the folder 
with the extensions ".js" or ".jsdoc". 

You can also **exclude** folders and files by adding 
their relative paths to the exclude array.

Now, open your gulpfile (usally **gulpfile.js**) and add 
**gulp** and **gulp-shell** as requirements. Also, add a 
taskto recompile the JSDocs:

```js
var gulp = require('gulp');
var shell = require('gulp-shell');

gulp.task('createDocs', shell.task([
  'rm -rf out',
  './node_modules/.bin/jsdoc -c conf.json'
]));
```

You can now compile the JSDoc documents by opening up 
the project folder and running the **createDocs** command
with gulp:

```sh
gulp createDocs
```

The **"out"** folder in the project directory will now
have the generated docs. Open up the **index.html**
file in the "out" folder to see the generated docs.

It's good practice to add the "createDocs" command to 
any watch tasks you may have setup in gulp. Also, 
remember to add the "out" folder to your **.gitignore**
if you would not like to check in the docs to your
repo.

#### Files

Document the top of files using the following style:
```js
/** 
 *  @fileOverview Write what's going on in the file here.
 *
 *  @author       Shri Ganeshram
 *  @author       Jack Hanford
 *
 *  @requires     NPM:npm_module_1
 *  @requires     BOWER:bower_module_1
 *  @requires     EXTERNAL:@link{http://url.com module_name}
 *  @requires     path/to/file:your_module_2
 */
```
 **@fileOverview** is followed by a simple description of
 the contents of the file. If it's too difficult to fit 
 a description within a line or two, it probably means
 the file needs to be broken into multiple files.
 
 **@author** is followed by the name of an author. To add
 multiple authors, use @author multiple times on 
 separate lines as seen above.
 
 **@requires** uses the source followed by the module name.
 Valid sources include (NPM, BOWER, EXTERNAL, and paths):
 
 **NPM** -- used for NPM modules, followed by :module_name
 
 
 **EXTERNAL** -- used for External Links, followed by the
 @link tag with a url to the module followed by its
 name in curly braces, e.g. 
 @link{https://github.com/twbs/bootstrap Bootstrap}
 
 **paths** -- used for modules within the codebase, use a 
 path to the module from the root directory of the 
 code base to the module file followed by :module_name
 e.g. /toolbar/api_panel.js:API Panel

#### Namespaces

In javascript, you can simulate a namespace using
a javascript object.

Use the **@namespace** tag to label a namespace:

```js
/**
 *  Description of namespace here.
 *  @namespace
 */
var Utils = {
  getUserName: function...
};
```

JSDoc will take care of the rest, creating a namespace
named Utils with member function getUserName.

You can add member functions to a namespace if they are
located outside of the namespace definition using
**@memberOf**:

```js
/**
 * Takes 2 numbers and returns their sum.
 * @memberOf Utils
 *
 * @param   {number} a the first number
 * @param   {number} b the second number
 *
 * @returns {number} the sum of a and b
 */
function addNumbers(a, b) {
  return a + b;
}

Utils.addNumbers = addNumbers;
```
Just follow the **@memberOf** tag with the name of
the namespace the function is a member of.

#### Modules

Modules can be documented using the **@module**
tag in JSDoc:

```js
/**
 * description of module here
 * @module ModuleName
 */

module.exports = new(function () {
...
```

JSDoc is smart about figuring out that the member
functions of module.exports belong to the module.

To add a **private method or variable** to a module, 
use the **@member** tag.
```js
/** @member MemberName */
```

For functions, you'll need to add an **@function** tag
as well.
```js
/** 
 * @member MemberName 
 * @function
 */
```

Make sure the function tag comes after the member tag!

If for some reason JSDoc doesn't pick up the
module, you can use the **@exports** tag:

```js
/** @exports ModuleName */
```

#### Functions

Functions use the following comment style in
JSDoc:

```js
/**
 * Takes 2 numbers and returns their sum.
 * @param   {number} a     the first number
 * @param   {number} b     the second number
 * @param   {number} [c=0] the optional third number
 *
 * @returns {number} the sum of a and b
 */
function addNumbers(a, b, c) {
  if (typeof c === "undefined") {
    c = 0;
  }
  return a + b + c;
}
```

The first line in the comment is a succinct
description of what the function does.

The **@param** tag is used to define parameters
the function takes as input. In this case
the function takes 3 parameters, a, b, and c.

The structure of the param tag for a **required
parameter** is:
```js
 *  @param {type} paramname param description
```
'type' is the javascript type of the parameter
which can take values of string, number, boolean,
or Class, where Class represents the type of a
user defined class.

'paramname' is the name of the parameter.

'param description' is a description of what the 
parameter represents.

The structure of an **optional parameter** is the
same with the paramname in square brackets:

```js
 *  @param {type} [paramname] param description
```

The structure of an **optional parameter with a
default value** is the same as an optional 
parameter's with an = followed by the default
value for the param:

```js
 *  @param {type} [paramname=default_value] param description
```

Optional tags **@throws** and **@constructor** can be used
as well.

**@throws** defines a possible exception:
```js
 *  @throws {exceptionName}
```

**@constructor** is used to label functions that
are class constructors:
```js
*  @constructor
```
#### Classes

Classes are defined similarly to functions with 
different tags.

```js
/**
 * A class to represent user's cars.
 * @class
 *
 * @constructor
 *
 * @property licensePlate the car's license plate number
 * @property vehicleType  the type of car
 */
function Car(licensePlate) {
  this.licensePlate = licensePlate;
  this.vehicleType = "sedan";
}
```
For classes, we use the first line to provide
a description of the class.

The **@class** tag is used to label the function
as a class.

The **@constructor** tag is used to label the 
function as a constructor for the class.

The **@property** tag is used to define class 
properties and is followed by the property name
and the description of the property.

## Variables and Constants

Variables can be documented using JSDoc. 
For example:

```js
/**
 * The current environment we're running in.
 * @type {string}
 */
 var currentEnvironment = getEnvironment();
```
The comment consists of a description in the 
first line followed by a **@type** tag in the 
second line.

Constants can be documented the same way as 
variables except with a **@constant** tag:

```js
/**
 * The environment we're running in.
 * @constant
 *
 * @type {string}
 */
 var ENVIRONMENT = "production";
```

#### Links

External links can be used in various comments
by using the **@link** tag:

```js
/** Stolen from {http://stackoverflow.com/questions/11919065/sort-an-array-by-the-levenshtein-distance-with-best-performance-in-javascript Stackoverflow Levenshtein Distance}*/
```
The **@link** tag is followed by the url and its
caption in curly braces.

#### Examples

To include an example in the code base, use the 
**@example** tag:

```js
/**
 * Takes 2 numbers and returns their sum.
 * @example 
 * var a = 5,
 *     b = 6;
 *
 * var sum = addNumbers(5, 6); // sum is set to 11
 *
 * @param   {number} a the first number
 * @param   {number} b the second number
 *
 * @returns {number} the sum of a and b
 */
function addNumbers(a, b) {
  return a + b;
}
```

Use the **@example** tag within the comment block
used to define a function, class, or constructor.

#### Tips

Sublime Text users, check out 
[DocBlockr](https://github.com/spadgos/sublime-jsdocs) in 
[Package Control](http://wbond.net/sublime_packages/package_control)
for autocomplete of JSDoc comments.

### Code Coverage

Code coverage of 70-80% is a reasonable goal for system test of most projects with most coverage metrics. Use a higher goal for projects specifically organized for high testability or that have high failure costs. Minimum code coverage for unit testing can be 10-20% higher than for system testing.

Introduction
Empirical studies of real projects found that increasing code coverage above 70-80% is time consuming and therefore leads to a relatively slow bug detection rate. Your goal should depend on the risk assessment and economics of the project.

### Full Coverage Generally Impractical
Although 100% code coverage may appear like a best possible effort, even 100% code coverage is estimated to only expose about half the faults in a system. Low code coverage indicates inadequate testing, but high code coverage guarantees nothing.

In a large system, achieving 100% code coverage is generally not cost effective. Some reasons are listed below.

Some test cases are expensive to reproduce but are highly improbable. The cost to benefit ratio does not justify repeating these tests simply to record the code coverage.
Checks may exist for unexpected error conditions. Layers of code might obscure whether errors in low-level code propagate up to higher level code. An engineer might decide that handling all errors creates a more robust solution than tracing the possible errors.

Unreachable code in the current version might become reachable in a future version. An engineer might address uncertainty about future development by investing a little more effort to add some capability that is not currently needed.
Code shared among several projects is only partially utilized by the project under test.
Generally, the tester should stop increasing code coverage when the tests become contrived. When you focus more and more on making the coverage numbers better, your motivation shifts away from finding bugs.
