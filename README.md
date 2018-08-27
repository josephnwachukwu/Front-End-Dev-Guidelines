# Front End Dev Guidelines 2017

## Front End Development Guidelines and Best Practices

## Introduction

### Goals

### General Standards

### Deliverables

### Development

#### NodeJs

#### Webpack, Grunt, Gulp

#### Choosing Frameworks

#### Setting up Editors

## HTML

### HTML Best Practices

## CSS

### CSS Best Practices

### Choosing frameworks

### Style Guides and Documentation

## JavaScipt

### Style Guide

Use Basic rules similar to [JavaScript Standard Stye](https://standardjs.com/) :

* 2 spaces – for indentation
* Single quotes for strings – except to avoid escaping
* No unused variables – this one catches tons of bugs!
* No semicolons
* Always use === instead of == – but obj == null is allowed to check null || undefined.
* Always handle the node.js err function parameter
* Declare browser globals with /* global */ comment at top of file Prevents accidental use of vaguely-named browser globals like open, length, event, and name. Example: /* global alert, prompt */ Exceptions are: window, document, and navigator

#### Frameworks

#### Angular vs React

### 

## Mobile

### Mobile Best Practices

## Testing

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
