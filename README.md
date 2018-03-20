OnixJS Software Development Kit
================
![alt text](https://raw.githubusercontent.com/onixjs/core/master/onix-splash.png "OnixJS")
A High-Performance NodeJS SOA Framework designed to address goals like flexibility, stability and connectivity.

> **Disclaimer**: This framework is in active development and won't be ready for production until we reach release candidate.
> **Alpha release date**: Feb 2018
> **Estimated date for beta release**: March ~ Apr 2018
> **Estimated date for release candidate**: 2Q/2018

## Installation

````sh
$ npm install --save @onixjs/sdk
````

## Phylosophy
The OnixJS phylosophy is to empower developers to decide which dependencies they want to install and maintain in their projects.

We strongly believe that staging or deploying your project, now or in a year... MUST NOT be affected by the framework or any of its dependencies, and that is the reason of why we decided to use practically zero dependencies.

All of this while providing with cool and modern features and mechanisms to build a better communicated, more stable and scalable product.

## Examples

```js
import { OnixClient, AppReference} from "@onixjs/sdk";
import { Browser } from '@onixjs/sdk/dist/core/browser.adapters';
// Create SDK Instance (Hint: Use NodeJS Adapters for NodeJS Clients)
const SDK: OnixClient = new OnixClient({
    host: '127.0.0.1',
    port: 80,
    adapters: {
        http: Browser.HTTP,
        websocket: Browser.WebSocket
    }
});
// Init SDK
await SDK.init();
// Create a TodoApp Reference
const TodoAppRef: AppReference | Error = await SDK.AppReference('TodoApp');
// Verify we actually got a Reference and not an Error
if (TodoAppRef instanceof AppReference) {
    const result = await TodoAppRef.Module('TodoModule')
                                   .Component('TodoComponent')
                                   .Method('addTodo')
                                   .call({ text: 'Hello SDK World' });
} else {
    throw TodoAppRef;
}
```

## Core Documentation

````sh
$ git clone git@github.com:onixjs/sdk.git
$ cd sdk
$ npm install && npm run serve:docs
````

Documents will be served on [http://127.0.0.1:3000](http://127.0.0.1:3000)

Note: This documentation is not final dev oriented.

## Test

````sh
$ git clone git@github.com:onixjs/core.git
$ cd core
$ npm install && npm run test
````



















import { Component } from '@angular/core';
import { OnixClient, ComponentReference, AppReference} from '@onixjs/sdk';
import { Browser } from '@onixjs/sdk/dist/core/browser.adapters';
import { Observable } from 'rxjs/Observable';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {

  private sdk: OnixClient = new OnixClient({
    host: 'http://127.0.0.1',
    port: 3000,
    adapters: {
      http: Browser.HTTP,
      websocket: Browser.WebSocket
    }
  });
