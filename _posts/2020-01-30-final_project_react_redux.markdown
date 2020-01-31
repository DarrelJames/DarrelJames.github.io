---
layout: post
title:      "FINAL PROJECT!! React/Redux"
date:       2020-01-31 00:10:39 +0000
permalink:  final_project_react_redux
---


Github:
[client](https://github.com/DarrelJames/calorie-tracker-client)
[backend](https://github.com/DarrelJames/calorie-tracker-api)

I created a calorie tracker that'll track the foods you consumed on a daily basis and persist your data into Rails API.

I started off by creating the backend by generating a rails app with the `--api` flag. Also with deployment in mind, I specified which database to use by adding `-d postgresql`. So the final command to create the app is:

`rails new NAME --api -d postgresql`

For user Authentication I used JSON web tokens. I used devise to handle the creation of user and tokens. I followed a video tutorial by a Flatiron instructor [here](https://youtu.be/qjtht03t7z4)

After getting authentication going and stubbed out all the model resources. I generated my react app by running

`npx create-react-app NAME`

Libraries Used:
* [axios](https://github.com/axios/axios): Used to make http requests to API
* [moment](https://github.com/moment/moment): Mainly formatting
* [react-redux](https://react-redux.js.org/): State container
* [redux-form](https://redux-form.com/8.2.2/): Easily connect forms to store and have tons more features, Instant validations for example
* [redux-thunk](https://github.com/reduxjs/redux-thunk): dispatch asynchronously
* [react-datepicker](https://reactdatepicker.com/): Simple Date picker, used to select log by date

I really enjoyed building this app with react. React makes it really easy to get going. Having a solid file structure makes the development process fluid. That was something I struggled with in my last project, JS/Rails. I definitely will go back and learn more about vanilla javascript design patterns.
