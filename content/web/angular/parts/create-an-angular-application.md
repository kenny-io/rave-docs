## Create an Angular Application

To create an Angular application, navigate to your terminal and input the following commands:

> **CAUTION:** This procedure assumes you are familiar with and have installed the following:

> 1. NodeJS
> 2. NPM

```
# install the angular-cli globally
    
$ npm install -g @angular/cli
    
# create a new project by running the ng new command
    
$ ng new my-rave-project
```

When you are done, your application’s folder should have a structure similar to this:


![](https://d2mxuefqeaa7sj.cloudfront.net/s_1A88A5048A37D3F6017910055D93DFE494E20830AF3E0C0CD31822B264EB7DDC_1522791241401_Screenshot+from+2018-04-03+22-33-50.png)



Your `package.json` file should include the following as dependencies:


    @angular/animations
    @angular/common
    @angular/compiler
    @angular/core
    @angular/forms
    @angular/http
    @angular/platform-browser
    @angular/platform-browser-dynamic
    @angular/router
    core-js
    rxjs
    zone.js


You may install other dependencies that you may need with `NPM`:


    $ npm install --save <NAME OF DEPENDENCY>

Alternatively,  you may use Yarn:


    $ yarn add <NAME OF DEPENDENCY>