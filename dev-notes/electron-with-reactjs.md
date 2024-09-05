---
description: Setup and basics for electron with react for desktop applications.
---

# Electron with ReactJs

### Setup

* `cd & npm init -y` to set up
* Check node js with `node -v`
* Create file `main.js`
* Add change `index.js` to `main.js` in `package.json`
* Install electron with `npm install --save electron`
* add `"start": "electron . "` to `"scripts"`
* Create a graphical interface for the application
  * In `main.js` import `const { win } = require('electron')`
  * Create window fn, initiate BrowserWindow attributes
* Create `index.html` file for window graphical interface
* Install react `npm install --save react react-dom`

### Misc

* Able to access low lever OS fns
*   Expose low lever API into the browser frame

    * `preload.js` -> inform Browser window of file
    * `const { ipcRenderer, contextBridge } = require('electron')`

    <figure><img src="../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>
