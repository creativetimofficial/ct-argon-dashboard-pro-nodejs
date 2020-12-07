# [Argon Dashboard Pro Nodejs](https://argon-dashboard-pro-nodejs.creative-tim.com/?ref=adnp-readme) [![Tweet](https://img.shields.io/twitter/url/http/shields.io.svg?style=social&logo=twitter)](https://twitter.com/home?status=Argon%20Dashboard%20Pro%20Node.js%20is%20a%20Premium%20Frontend%20Preset%20for%20Node.js%20%E2%9D%A4%EF%B8%8F%0Ahttps%3A//argon-dashboard-pro-nodejs.creative-tim.com/%20%23bootstrap%20%23argon%20%23design%20%23dashboard%20%23nodejs%20%23premium%20via%20%40CreativeTim)

![version](https://img.shields.io/badge/version-1.0.0-blue.svg)  ![license](https://img.shields.io/badge/license-MIT-blue.svg) [![GitHub issues open](https://img.shields.io/github/issues/creativetimofficial/ct-argon-dashboard-pro-nodejs.svg?maxAge=2592000)](https://github.com/creativetimofficial/ct-argon-dashboard-pro-nodejs/issues?q=is%3Aopen+is%3Aissue) [![GitHub issues closed](https://img.shields.io/github/issues-closed-raw/creativetimofficial/ct-argon-dashboard-pro-nodejs.svg?maxAge=2592000)](https://github.com/creativetimofficial/ct-argon-dashboard-pro-nodejs/issues?q=is%3Aissue+is%3Aclosed)

![Product Image](https://github.com/creativetimofficial/public-assets/blob/master/argon-dashboard-pro-nodejs/argon-dashboard-pro-nodejs.gif?raw=true)

Start your development with a Bootstrap 4 Admin Dashboard built for Node.js framework, the newest go-to technology for top companies. [Creative Tim](https://www.creative-tim.com/) partnered with [Udevoffice](https://udevoffice.com/) to provide a fully coded “frontend + backend” solution for you. It features a huge number of components that can help you create amazing websites and brings with itself innumerable advantages: lightweight, fast, scalable and modern way to execute your next top app.

**FULLY CODED COMPONENTS**

Argon Dashboard Pro Node is built with over frontend 200 individual components, giving you the freedom of choosing and combining. All components can take variations in colour, that you can easily modify using SASS files.
You will save a lot of time going from prototyping to full-functional code, because all elements are implemented. This Dashboard is coming with prebuilt examples, so the development process is seamless, switching from our pages to the real website is very easy to be done.
Every element has multiple states for colors, styles, hover, focus, that you can easily access and use.
View all components [here](https://argon-dashboard-pro-nodejs.creative-tim.com/docs/components/alerts?ref=adnp-readme)

**COMPLEX DOCUMENTATION**

Each element is well presented in a very complex documentation. You can check the components [here](https://argon-dashboard-pro-nodejs.creative-tim.com/docs/components/alerts?ref=adnp-readme) and the foundation [here](https://argon-dashboard-pro-nodejs.creative-tim.com/docs/foundation/colors?ref=adnp-readme)

**Example Pages**

If you want to get inspiration or just show something directly to your clients, you can jump start your development with our pre-built example pages. You will be able to quickly set up the basic structure for your web project.
View example pages [here](https://argon-dashboard-pro-nodejs.creative-tim.com/?ref=adnp-readme)


## Installation

1. You need `Node.js` (at least 10.x version) installed on your machine, if you don't have it, you should install it - download [link](https://nodejs.org/en/download/)
3. `cd` to your downloaded Argon Dashboard Pro Nodejs app
2. Install necessary dependencies:
    - **Via node `npm` package manager** - Run `npm install` on the project root
    - **Via `yarn` package manager** - Run `yarn install` on the project root

## Configuration for PostgreSQL database and Redis data structure store

##### Via Docker

1. Install **Docker** on your machine
2. Run `docker-compose up -d` in a terminal on the project root. This will start 3 containers:
    - database(PostgreSQL) container;
    - redis container - required for session management;
    - haproxy container - required only for a staging/production setup;

##### Via another chosen solution.

1. Install your **PostgreSQL** database
2. Install your **Redis** server
3. Change connection configuration, from your root `cd` to `env-files` folder and change the following configurations with your own:

###### **For PostgreSQL connection:**
1. Database connection via URL
```bash
DATABASE_URL=http://creativeTim:creativeTim@127.0.0.1:5432/creativeTim
# Example: DATABASE_URL=http://<user>:<password>@<host>/<database_name>
```
2. Database connection via credentials
```bash
DATABASE_HOST=127.0.0.1
DATABASE_PORT=5432
DATABASE_NAME=creativeTim
DATABASE_USER=creativeTim
DATABASE_PASSWORD=creativeTim
```

######  **For Redis connection:**
1. REDIS connection via URL
```bash
REDIS_URL=redis://:@127.0.0.1:6379
# Example: redis://:<password>@<host>:<port>
```
2. REDIS connection via credentials
```bash
REDIS_HOST=127.0.0.1
REDIS_PORT=6379
REDIS_PASSWORD=
```

## Migrations and seeds

1. For database tables structure, in the project root run: `npm run knex migrate:latest` or `yarn knex migrate:latest` if you are using `yarn` as the default package manager
2. To create a default user, run: `npm run knex seed:run` or `yarn knex seed:run` if you are using `yarn` as the default package manager

## Run the application

1. For starting the application, the following script (defined in `package.json` under `scripts`) must be called:
    - via **npm**: `npm run start` or `npm run dev` for starting the development environment, which has livereload enabled;
    - via **yarn**: `yarn start` or `yarn dev` for starting the development environment, which has livereload enabled;


## Usage

Register a user or login with three types of credentials **admin@argon.com**:**secret**, **creator@argon.com**:**secret** and **member@argon.com**:**secret** and start testing the preset (make sure to run the migrations and seeds for these credentials to be available).

Besides the dashboard and the auth pages this preset also has an edit profile page.
**NOTE**: _Keep in mind that all available features can be viewed once you login using the credentials provided above or by registering your own user._

## Features

In order to see the available features `cd` into `features` folder, and you will then find a folder for each of the available features, mostly each folder containing:

- A `routes.js` file that usually contains the `GET` and `POST` requests, for example, the profile router looks like this:

```javascript
const { wrap } = require('async-middleware');

const requestBodyValidation = require('./commands/verify-request-body');
const updateUserInfo = require('./commands/update-user-info');
const { loadPage } = require('./commands/profile');

module.exports = (router, middlewares = []) => {
  router.get('/profile', middlewares.map(middleware => wrap(middleware)), wrap(loadPage));
  router.post('/update-profile-info', wrap(requestBodyValidation), wrap(updateUserInfo));

  return router;
};
```

- A `repository.js` file that contains feature database queries
- A `commands` folder where you can find all feature functionality functions, for example the login template rendering which looks like this:

```javascript
function loadPage(req, res) {
  debug('login:loadPage', req, res);
  res.render('pages/login');
}
```
- A `constants.js` file, to store all your static variables, for eg:

```
const USERNAME_PASSWORD_COMBINATION_ERROR = 'These credentials do not match our records.';
const INTERNAL_SERVER_ERROR = 'Something went wrong! Please try again.';
```

All feature routes are mounted in `routes/index.js` from the project root.

## For the Front-end side:

##### Templates

- You can find all the templates in `views` folder where you will find:
1. The `layout.ejs` file, the main template layout.
2. A `pages` folder with all the page templates
3. A `partials` folder with the common components (header, footer, sidebar)

## Table of Contents

* [Versions](#versions)
* [Demo](#demo)
* [Documentation](#documentation)
* [File Structure](#file-structure)
* [Browser Support](#browser-support)
* [Resources](#resources)
* [Reporting Issues](#reporting-issues)
* [Licensing](#licensing)
* [Useful Links](#useful-links)

## Versions

[<img src="https://github.com/creativetimofficial/public-assets/blob/master/logos/html-logo.jpg?raw=true" width="60" height="60" />](https://demos.creative-tim.com/argon-dashboard-pro/pages/dashboards/dashboard.html?ref=adnp-readme)
[<img src="https://github.com/creativetimofficial/public-assets/blob/master/logos/nodejs-logo.jpg?raw=true" width="60" height="60" />](https://argon-dashboard-pro-nodejs.creative-tim.com/?ref=adnp-readme)
[<img src="https://github.com/creativetimofficial/public-assets/blob/master/logos/laravel_logo.png?raw=true" width="60" height="60" />](https://argon-dashboard-pro-laravel.creative-tim.com/?ref=adnp-readme)

| HTML | NODEJS | LARAVEL |
| --- | --- | --- |
| [![Argon Dashboard Pro HTML](https://s3.amazonaws.com/creativetim_bucket/products/137/original/opt_adp_thumbnail.jpg)](https://demos.creative-tim.com/argon-dashboard-pro/pages/dashboards/dashboard.html?ref=adnp-readme) | [![Argon Dashboard Pro Nodejs](https://s3.amazonaws.com/creativetim_bucket/products/153/original/opt_adp_node_thumbnail.jpg)](https://argon-dashboard-pro-nodejs.creative-tim.com/?ref=adnp-readme) | [![Argon Dashboard Pro Laravel](https://s3.amazonaws.com/creativetim_bucket/products/146/original/opt_adp_laravel_thumbnail.jpg)](https://argon-dashboard-pro-laravel.creative-tim.com/?ref=adnp-readme)

## Demo

| Register | Login | Dashboard |
| --- | --- | ---  |
| [![Register](https://github.com/creativetimofficial/public-assets/blob/master/argon-dashboard-pro-nodejs/argon-nodejs-pro-register.png?raw=true)](https://argon-dashboard-pro-nodejs.creative-tim.com/register?ref=adnp-readme)  | [![Login](https://github.com/creativetimofficial/public-assets/blob/master/argon-dashboard-pro-nodejs/argon-nodejs-pro-login.png?raw=true)](https://argon-dashboard-pro-nodejs.creative-tim.com/login?ref=adnp-readme)  | [![Dashboard](https://github.com/creativetimofficial/public-assets/blob/master/argon-dashboard-pro-nodejs/argon-nodejs-pro-dashboard%20.png?raw=true)](https://argon-dashboard-pro-nodejs.creative-tim.com/?ref=adnp-readme)

| Profile Page | Users Page | Tables Page  |
| --- | --- | ---  |
| [![Profile Page](https://github.com/creativetimofficial/public-assets/blob/master/argon-dashboard-pro-nodejs/argon-nodejs-pro-profile.png?raw=true)](https://argon-dashboard-pro-nodejs.creative-tim.com/profile?ref=adnp-readme)  | [![Users Page](https://github.com/creativetimofficial/public-assets/blob/master/argon-dashboard-pro-nodejs/argon-nodejs-pro-users.png?raw=true)](https://argon-dashboard-nodejs.creative-tim.com/user-management?ref=adnp-readme)  | [![Tables Page](https://github.com/creativetimofficial/public-assets/blob/master/argon-dashboard-pro-nodejs/argon-nodejs-pro-tables.png?raw=true)](https://argon-dashboard-pro-nodejs.creative-tim.com/tables?ref=adnp-readme)
[View More](https://argon-dashboard-pro-nodejs.creative-tim.com/?ref=adnp-readme)

## Documentation
The documentation for the Argon Dashboard Pro Nodejs is hosted at our [website](https://argon-dashboard-pro-nodejs.creative-tim.com/docs/getting-started/overview.html?ref=adn-readme).

## File Structure

```
├── CHANGELOG.md
├── ISSUES_TEMPLATE.md
├── LICENSE.md
├── README.md
│   .editorconfig
│   .eslintrc.js
│   .gitignore
│   .prettierrc
│   docker-compose.yml
│   ecosystem.config.js
│   gulpfile.js
│   haproxy.cfg
│   logger.js
│   package.json
│   app.js
│
├───bin
│       www
│
├───config
│       index.js
│
├───db
│   │   index.js
│   │   knexfile.js
│   │
│   ├───migrations
│   │       20190213122702_create-roles-table.js
│   │       20190315141435_create-users-table.js
│   │       20190315155223_create-posts-table.js
│   │       20190318161927_create_tags_table.js
│   │       20190318161939_create_categories_table.js
│   │       20190318161947_create_posts_tags_table.js
│   │       20190318162859_create_posts_categories_table.js
│   │
│   └───seeds
│           01-insert-default-roles.js
│           02-create-default-users.js
│           03-create-default-tags.js
│           04-create-default-categories.js
│
├───docsÂ
│       documentation.html
│
├───env-files
│       development.env
│       production.env
│       staging.env
│
├── public
│   ├── css
│   │   ├── argon.css
│   │   └── argon.min.css
│   ├── fonts
│   │   └── nucleo
│   ├── img
│   │   ├── brand
│   │   ├── icons
│   │   └── theme
│   ├── js
│   │   ├── argon.js
│   │   └── argon.min.js
│   ├── scss
│   │   ├── argon.scss
│   │   ├── bootstrap
│   │   ├── core
│   │   └── custom
│   └── vendor
├───features
│   ├───category-management
│   │   │   constants.js
│   │   │   repository.js
│   │   │   routes.js
│   │   │
│   │   └───commands
│   │           add-category.js
│   │           delete-category.js
│   │           load-page.js
│   │           update-category.js
│   │           verify-request-body.js
│   │
│   ├───login
│   │   │   constants.js
│   │   │   init-auth-middleware.js
│   │   │   repository.js
│   │   │   routes.js
│   │   │
│   │   └───commands
│   │           load-page.js
│   │           login.js
│   │           redirect-to-dashboard.js
│   │           verify-request-body.js
│   │
│   ├───logout
│   │   │   routes.js
│   │   │
│   │   └───commands
│   │           logout.js
│   │
│   ├───posts
│   │   │   constants.js
│   │   │   repository.js
│   │   │   routes.js
│   │   │
│   │   └───commands
│   │           add-post.js
│   │           delete-post.js
│   │           edit-post.js
│   │           load-page.js
│   │           verify-request-body.js
│   │
│   ├───profile
│   │   │   constants.js
│   │   │   repository.js
│   │   │   routes.js
│   │   │
│   │   └───commands
│   │           change-password.js
│   │           load-page.js
│   │           update-user-info.js
│   │           verify-request-body.js
│   │
│   ├───register
│   │   │   constants.js
│   │   │   repository.js
│   │   │   routes.js
│   │   │
│   │   └───commands
│   │           create-user.js
│   │           load-page.js
│   │           verify-request-body.js
│   │
│   ├───reset-password
│   │   │   routes.js
│   │   │
│   │   └───commands
│   │           load-page.js
│   │
│   ├───tag-management
│   │   │   constants.js
│   │   │   repository.js
│   │   │   routes.js
│   │   │
│   │   └───commands
│   │           add-tag.js
│   │           delete-tag.js
│   │           load-page.js
│   │           update-tag.js
│   │           verify-request-body.js
│   │
│   └───user-management
│       │   constants.js
│       │   repository.js
│       │   routes.js
│       │
│       └───commands
│               load-edit-page.js
│               load-page.js
│               update-user.js
│               verify-request-body.js
│
├───helpers
│       role-guard.js
│
├───resources
│       user-roles.json
│
├───routes
│       index.js
│
├───screens
│       Dashboard.png
│       Login.png
│       Profile.png
│       Users.png
│
└───views
    │   layout.ejs
    │
    ├───pages
    │   │   404.ejs
    │   │   calendar.ejs
    │   │   charts.ejs
    │   │   homepage.ejs
    │   │   reset-password.ejs
    │   │   widgets.ejs
    │   │
    │   ├───components
    │   │       buttons.ejs
    │   │       cards.ejs
    │   │       grid.ejs
    │   │       icons.ejs
    │   │       notifications.ejs
    │   │       typography.ejs
    │   │
    │   ├───dashboards
    │   │       alternative.ejs
    │   │       dashboard.ejs
    │   │
    │   ├───examples
    │   │       add-category.ejs
    │   │       add-post.ejs
    │   │       add-tag.ejs
    │   │       category-management.ejs
    │   │       display-posts.ejs
    │   │       edit-category.ejs
    │   │       edit-post.ejs
    │   │       edit-tag.ejs
    │   │       edit-user.ejs
    │   │       lock.ejs
    │   │       login.ejs
    │   │       post-management.ejs
    │   │       pricing.ejs
    │   │       profile.ejs
    │   │       register.ejs
    │   │       tag-management.ejs
    │   │       timeline.ejs
    │   │       user-management.ejs
    │   │
    │   ├───forms
    │   │       components.ejs
    │   │       elements.ejs
    │   │       validation.ejs
    │   │
    │   ├───maps
    │   │       google.ejs
    │   │       vector.ejs
    │   │
    │   └───tables
    │           datatables.ejs
    │           sortable.ejs
    │           tables.ejs
    │
    └───partials
        │   dropdown.ejs
        │   footer.ejs
        │   header.ejs
        │   navbar.ejs
        │   scripts.ejs
        │   sidebar.ejs
        │
        └───auth
                footer.ejs
                header.ejs
                navbar.ejs
```
## Browser Support

At present, we officially aim to support the last two versions of the following browsers:

<img src="https://github.com/creativetimofficial/public-assets/blob/master/logos/chrome-logo.png?raw=true" width="64" height="64"> <img src="https://raw.githubusercontent.com/creativetimofficial/public-assets/master/logos/firefox-logo.png" width="64" height="64"> <img src="https://raw.githubusercontent.com/creativetimofficial/public-assets/master/logos/edge-logo.png" width="64" height="64"> <img src="https://raw.githubusercontent.com/creativetimofficial/public-assets/master/logos/safari-logo.png" width="64" height="64"> <img src="https://raw.githubusercontent.com/creativetimofficial/public-assets/master/logos/opera-logo.png" width="64" height="64">


## Resources
- Demo: <https://argon-dashboard-pro-nodejs.creative-tim.com/?ref=adnp-readme>
- Download Page: <https://www.creative-tim.com/product/argon-dashboard-pro-nodejs?ref=adnp-readme>
- Documentation: <https://argon-dashboard-pro-nodejs.creative-tim.com/docs/getting-started/overview.html?ref=adnp-readme>
- License Agreement: <https://www.creative-tim.com/license>
- Support: <https://www.creative-tim.com/contact-us>
- Issues: [Github Issues Page](https://github.com/creativetimofficial/ct-argon-dashboard-pro-nodejs/issues)
- **Dashboards:**

| HTML | NODEJS | LARAVEL |
| --- | --- | --- |
| [![Argon Dashboard Pro HTML](https://s3.amazonaws.com/creativetim_bucket/products/137/original/opt_adp_thumbnail.jpg)](https://demos.creative-tim.com/argon-dashboard-pro/pages/dashboards/dashboard.html?ref=adnp-readme) | [![Argon Dashboard Pro Nodejs](https://s3.amazonaws.com/creativetim_bucket/products/153/original/opt_adp_node_thumbnail.jpg)](https://argon-dashboard-pro-nodejs.creative-tim.com/?ref=adnp-readme) | [![Argon Dashboard Pro Laravel](https://s3.amazonaws.com/creativetim_bucket/products/146/original/opt_adp_laravel_thumbnail.jpg)](https://argon-dashboard-pro-laravel.creative-tim.com/?ref=adnp-readme)

## Change log

Please see the [changelog](CHANGELOG.md) for more information on what has changed recently.

## Credits

- [Creative Tim](https://creative-tim.com/)
- [Under Development Office](https://udevoffice.com/)

## Reporting Issues

We use GitHub Issues as the official bug tracker for the Argon Dashboard Pro Nodejs. Here are some advices for our users that want to report an issue:

1. Make sure that you are using the latest version of the Argon Dashboard Pro Nodejs. Check the CHANGELOG from your dashboard on our [website](https://www.creative-tim.com/).
2. Providing us reproducible steps for the issue will shorten the time it takes for it to be fixed.
3. Some issues may be browser specific, so specifying in what browser you encountered the issue might help.

## Licensing

- Copyright 2019 Creative Tim (https://www.creative-tim.com/?ref=adnp-readme)
- [Creative Tim License](https://www.creative-tim.com/license).


## Useful Links

- [Tutorials](https://www.youtube.com/channel/UCVyTG4sCw-rOvB9oHkzZD1w)
- [Affiliate Program](https://www.creative-tim.com/affiliates/new) (earn money)
- [Blog Creative Tim](http://blog.creative-tim.com/)
- [Free Products](https://www.creative-tim.com/bootstrap-themes/free) from Creative Tim
- [Premium Products](https://www.creative-tim.com/bootstrap-themes/premium?ref=adn-readme) from Creative Tim
- [React Products](https://www.creative-tim.com/bootstrap-themes/react-themes?ref=adn-readme) from Creative Tim
- [Angular Products](https://www.creative-tim.com/bootstrap-themes/angular-themes?ref=adn-readme) from Creative Tim
- [VueJS Products](https://www.creative-tim.com/bootstrap-themes/vuejs-themes?ref=adn-readme) from Creative Tim
- [More products](https://www.creative-tim.com/bootstrap-themes?ref=adn-readme) from Creative Tim
- Check our Bundles [here](https://www.creative-tim.com/bundles??ref=adn-readme)

### Social Media

Twitter: <https://twitter.com/CreativeTim?ref=adnp-readme>

Facebook: <https://www.facebook.com/CreativeTim?ref=adnp-readme>

Dribbble: <https://dribbble.com/creativetim?ref=adnp-readme>

Instagram: <https://www.instagram.com/CreativeTimOfficial?ref=adnp-readme>

## Credits

- [Creative Tim](https://creative-tim.com/?ref=adnp-readme)
- [Under Development Office](https://udevoffice.com/ref=creativetim)
