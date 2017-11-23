# Table of contents

* [About Munchie Zone](#about-munchiezone)
* [Installation](#installation)
* [Application design](#application-design)
  * [Directory structure](#directory-structure)
  * [Import conventions](#import-conventions)
  * [Naming conventions](#naming-conventions)
  * [Data model](#data-model)
  * [CSS](#css)
  * [Routing](#routing)
  * [Authentication](#authentication)
  * [Authorization](#authorization)
  * [Configuration](#configuration)
  * [Quality Assurance](#quality-assurance)
    * [ESLint](#eslint)
    * [Data model unit tests](#data-model-unit-tests)
* [Development history](#development-history)
  * [Milestone 1](#milestone-1)
  * [Milestone 2](#milestone-2)
* [Contact Us](#contact-us)


# About Munchie Zone

[Munchie Zone](https://github.com/munchiezone) is a meteor application which allows users to combine food orders in order to avoid expensive delivery charges. Users are also able to set dietary restrictions while searching through orders, and can also be pinged on their phone whenever a new order with their favorite food or restaurant is involved. Anyone with a University of Hawaii account is able to access this product after logging in. The application can be viewed [here](http://munchiezone.meteorapp.com/). 

# Installation

1) Download a copy of the code which can be found [here](https://github.com/munchiezone/munchiezone).
2) Install Meteor
3) cd into the app/ directory and run the following command:

```
$ meteor npm install
```

4) Run the code using the following command:

```
$ meteor npm run start
```

5) Access the application at [http://localhost:3000](http://localhost:3000)

# Application Design

## Directory structure

The top-level directory structure contains:

```
app/		# holds the Meteor application sources
config/		# holds configuration files.
.gitignore	#

```
The app/ directory has this top-level structure:

```
client/
  lib/           # holds Semantic UI files.
  head.html      # the <head>
  main.js        # import all the client-side html and js files. 

imports/
  api/           # Define collection processing code (client + server side)
    base/      	# contains Base collection
    interest/	# contains Interests collection
    profile/ 	# contains Profile collection
  startup/       # Define code to run when system starts up (client-only, server-only)
    client/        
    server/        
  ui/
    components/  # templates that appear inside a page template.
    layouts/     # Layouts contain common elements to all pages (i.e. menubar and footer)
    pages/       # Pages are navigated to by FlowRouter routes.
    stylesheets/ # CSS customizations, if any.

node_modules/    # managed by Meteor

private/
  database/      # holds the JSON file used to initialize the database on startup.

public/          
  images/        # holds static images for landing page and predefined sample users.
  
server/
   main.js       # import all the server-side js files.
```

## Import conventions
This system makes use of the Meteor 1.4 guideline.
In which, all application code is placed in the imports/ directory, and client/main.js and server/main.js imports the all the directories containing necessary code. The contents of client/main.js:
```
import '/imports/startup/client';
import '/imports/ui/components/form-controls';
import '/imports/ui/components/directory';
import '/imports/ui/components/user';
import '/imports/ui/components/landing';
import '/imports/ui/layouts/directory';
import '/imports/ui/layouts/landing';
import '/imports/ui/layouts/shared';
import '/imports/ui/layouts/user';
import '/imports/ui/pages/directory';
import '/imports/ui/pages/filter';
import '/imports/ui/pages/landing';
import '/imports/ui/pages/user';
import '/imports/ui/pages/create';
import '/imports/ui/pages/home';
import '/imports/ui/stylesheets/style.css';
import '/imports/api/base';
import '/imports/api/profile';
import '/imports/api/interest';

```
All imports (except the style.css) invoke the index.js file in the specified directory. Imports are found in either main.js files in client/ and server/ or the index.js files in import subdirectories.


## Naming conventions

The following naming conventions are used…

<ul>
    <li> Files and directories are named in lower cases and words are separated by hyphens. Ex: home-page.html </li>
    <li> “Global” Javascript variables, like collections are capitalized. Ex. Profiles </li>
    <li>Non-Global variables are written in camel-case. Ex. allProfiles</li>
    <li> Templates representing pages are capitalized and words are separated by underscores. Ex. Home_Page.</li>
    <li> Files for templates are lowercase and words are separated with underscore. Ex. home-page.html, home-page.js </li>
    <li>Routes to pages are named the same as their corresponding page. Ex. Home_Page</li>
</ul>


## Data model

The Munchie Zone data model currently uses two Javascript classes, ProfileCollection and InterestCollection. Both classes export a single variable that provides access to that collection. To alter Munchie Zone data that uses variables from the collections, uses methods in that collection to get or set data. The ProfileCollection and BaseCollection inherits from BaseCollection class, in which contains functions that can be used for both classes. Both collections also have Mocha unit tests in ProfileCollection.test.js and InterestCollection.test.js.

In the future, more collections will be implemented as needed, such as OrderCollection.

## CSS
This application was built using the Semantic UI CSS framework. Its files can be found in app/client/lib/semantic-ui. This framework does not need to be explicitly imported, as it is located in the client/ directory rather than the imports/ directory.

## Routing
Munchie Zone uses Flow Router to navigate around the app. The router can be found in imports/startup/client/router.js

<ul>
    <li> `/` leads the user to the landing page</li>
    <li> `/home` routes to the home page</li>
    <li> `/profile` leads the user to the user’s profile page</li>
    <li> `/filter` routes to the view order page</li>
    <li> `/create` brings the user to the create order page</li>
</ul>


## Authentication

Users have their accounts authenticated through the University of Hawaii CAS test server. Thus, any user with a University of Hawaii account can access and use Munchie Zone.

## Authorization

The landing page can be accessed by anyone. However, pages that require authorization are the profile, order requests, create order, and home pages. The user must be logged in through the UH test CAS server to be authorized.
Template based authorization is used to prevent unauthorized users from accessing private pages; and If_Authorized template is used, which is defined in If_Authorized.html and If_Authorized.js 

## Configuration

The config directory contains settings files, namely config/settings.development.json. The directory also contains the .gitignore file, which makes sure that the settings.production file is not uploaded in the GitHub repository. Upon startup if the database is empty, Munchie Zone will load settings.development.json.

## Quality Assurance

### ESLint

Munchie Zone includes a .eslintrc file to define the coding style. It can be invoked with the command:

```
meteor npm run lint
```

This command outputs the results onto the console.

### Data model unit tests

Invoking the script named ‘test’ runs the unit test on the data model. This is defined in the package.json file.

```
meteor npm run test
```

# Development History

## Milestone 1

This milestone started on November 7, 2017 and was completed on November 22, 2017. In it, mockups of the landing, home, profile, view order, and create order pages were created using Semantic UI, HTML, and CSS. Meteor, templates, and FlowRouter were used as well. Issue Driven Project Management practices were also followed.  The project’s completed issues can be viewed [here](https://github.com/munchiezone/munchiezone/projects/1). 

First the user is brought to the landing page, which introduces the website and prompts the user to log in at the bottom of the page. 
[Landing Page](http://munchiezone.meteorapp.com/)
![Alt text](https://github.com/munchiezone/munchiezone.github.io/blob/master/images/landing.png?raw=true)

Upon logging in, the user is brought to the home page. Here, the user can view orders they are currently participating in as well as orders from their favorited restaurants. In order to view this page and the other pages, one must log in via the landing page and change “<user>” in the link to their own username.
[Home Page](http://munchiezone.meteorapp.com/<user>/home)
![Alt text](https://github.com/munchiezone/munchiezone.github.io/blob/master/images/home.png?raw=true)

The user is able to edit his/her profile in the profile page. This is where the user can put in information such as favorite restaurants, dietary information, contact information, and etc.
[Profile Page](http://munchiezone.meteorapp.com/<user>/profile)
![Alt text](https://github.com/munchiezone/munchiezone.github.io/blob/master/images/profile.png?raw=true)

The order page contains current pending food requests, in which the user can join in on the order. Orders that contain the user’s favorite restaurants are at the top of the page.
[View Order Page](http://munchiezone.meteorapp.com/<user>/filter)
![Alt text](https://github.com/munchiezone/munchiezone.github.io/blob/master/images/view_orders.png?raw=true) 

The user can create their own order on the create order page. There are various fields that must be filled out so that orders can be filtered by other users.
[Create Order Page](http://munchiezone.meteorapp.com/<user>/create)
![Alt text](https://github.com/munchiezone/munchiezone.github.io/blob/master/images/create_orders.png?raw=true)

## Milestone 2

Milestone 2 started on November 23, 2017 and will be completed on December 9, 2017. The goal of this milestone is to improve the quality and functionality of the site and also to implement backend processes such as favoriting orders and sending phone notifications. The list of issues for milestone 2 can be viewed [here](https://github.com/munchiezone/munchiezone/projects/4).

# Contact Us

The developers of Munchie Zone can be contacted via DM on Slack or via email.
<ul>
    <li>Angela Zheng: awy@hawaii.edu</li>
    <li>Wendy Chen: wchen9@hawaii.edu</li>
    <li>Gary Wong: garyjw@hawaii.edu</li>
</ul>



