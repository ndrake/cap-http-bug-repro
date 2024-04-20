## Created with Capacitor Create App

This app was created using [`@capacitor/create-app`](https://github.com/ionic-team/create-capacitor-app),
and comes with a very minimal shell for building an app.

## CapacitorHTTP issue with Capacitor v6

It seems that after upgrading to Capacitor 6, using Capacitor HTTP with Axios doesn't work right and the requests aren't intercepted. 


Steps to reproduce:

Cap v5.5.1 control test

* Clone this repo
* Run `npm install`
* Run `npm run build`
* Run `npx cap sync ios`
* Run `npx cap open ios`
* Run app in ios 17.4 simulator
* Open Safari Inspector for the app in the simulator
* Click "Get Data" button
* Page should update with API response (employee name or error message)
* You should NOT see an HTTP request in the Inspector Network tab
* You SHOULD see a CapacitorHttp.request message in the console with the request/response details


Cap v6 test

* Upgrade project to Capacitor v6
  * Run `npm i -D @capacitor/cli@latest`
  * Run `npx cap migrate`
    * Answer `Y`, `Y`, `NPM`
* Run `npm run build`
* Run `npx cap sync ios`
* Run `npx cap open ios`
* Open Safari Inspector for the app in the simulator
* Run app in ios 17.4 simulator
* Click "Get Data" button

Expected

* Page should update with API response (employee name or error message)
* Capacitor.Http intercepts the request and it doesn't show in the Safari inspector

Actual

* Page doesn't update
* Capacitor.Http does NOT intercept the request and it is handled by the webview

