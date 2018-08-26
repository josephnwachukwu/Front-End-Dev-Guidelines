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

### Javascipt Best Practices

#### Frameworks

#### Angular vs React

### 

## Mobile

### Mobile Best Practices

### Testing

## Code Coverage

### Full Coverage Generally Impractical
Although 100% code coverage may appear like a best possible effort, even 100% code coverage is estimated to only expose about half the faults in a system. Low code coverage indicates inadequate testing, but high code coverage guarantees nothing.

In a large system, achieving 100% code coverage is generally not cost effective. Some reasons are listed below.

Some test cases are expensive to reproduce but are highly improbable. The cost to benefit ratio does not justify repeating these tests simply to record the code coverage.
Checks may exist for unexpected error conditions. Layers of code might obscure whether errors in low-level code propagate up to higher level code. An engineer might decide that handling all errors creates a more robust solution than tracing the possible errors.

Unreachable code in the current version might become reachable in a future version. An engineer might address uncertainty about future development by investing a little more effort to add some capability that is not currently needed.
Code shared among several projects is only partially utilized by the project under test.
Generally, the tester should stop increasing code coverage when the tests become contrived. When you focus more and more on making the coverage numbers better, your motivation shifts away from finding bugs.
