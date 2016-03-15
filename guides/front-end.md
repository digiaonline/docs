# Front-end Developer’s Guide

This document is a primer on core concepts and workflows adopted by front-end developers at Nord Software.

## What is a front-end application?

A front-end application is a graphical user interface consumed by actual end users. Technically it is a standalone server-agnostic JavaScript, HTML and CSS bundle that functions independently and, if needed, communicates with back-end services via HTTP or WebSockets.

Web applications have traditionally been monolithic server-side systems (commonly written in PHP, Ruby or Python) that implemented the entire application architecture as a single server-side model. This meant that database connections, data models, business logic, HTML, CSS, JavaScript as well as any third-party integrations had to be tightly coupled under a single umbrella. Furthermore, from an end user’s point of view, it only provided a single entry into the application: through a web browser.

The emergence of mobile applications has brought forth a looser, compositional paradigm to web application architecture that separates front-end and back-end components. Creating a standalone mobile application on top of a traditional web application would require the development team to rewrite large portions of the application to support communication with external client applications because it was originally meant for a single client only: the server-side application itself.

So instead, by decoupling the presentational layer (HTML, CSS and JavaScript) entirely, the back-end application can be refined for a specific purpose: managing business-related processing and handling requests sent by front-end applications. Correspondingly, multiple consumer-facing front-end applications can be developed side-by-side against a shared back-end configuration.

As a result, consumer use cases (e.g. requesting the most popular blog posts or submitting a comment) can be abstracted out and exposed by back-end services as public API endpoints which can then be called by front-end applications. This allows developers to build an extensible ecosystem around a business.

## Tools of the trade

- [Atom](https://atom.io), [PHPStorm](https://www.jetbrains.com/phpstorm) (optional), or [Sublime Text](http://www.sublimetext.com/2)
- [SourceTree](https://www.sourcetreeapp.com)
- [iTerm 2](https://www.iterm2.com)
- Node.js (install with [nvm](https://github.com/creationix/nvm))
- [Postman](https://www.getpostman.com)
- [Gmail](http://www.gmail.com)
- [Slack](https://nordsoftware.slack.com)
- [Toggl](https://www.toggl.com)
- [GitHub](https://github.com)
- [Trello](https://trello.com)
- [1Password](https://agilebits.com/onepassword)
- [Vagrant](https://www.vagrantup.com)
- [VirtualBox](https://www.virtualbox.org/wiki/Downloads)

## Accounts and licenses

Please ask Niklas to create the following accounts for you:

- Gmail
- Slack
- Toggl
- 1Password (license)

Optional:

- PHPStorm (license)

## Readme

Every project **must** contain a README.md file that succinctly details the purpose of the project and the exact steps a new contributor should take in order to make the application run.

Ideally, installing an application should be as simple as running

```
git clone git@github.com:nordsoftware/their-project.git .
cd their-project
npm install
npm start
```

Although these commands may seem self-explanatory to experienced front-end developers, having a clear set of step-by-step instructions reduces the time and cognitive load it takes for a new contributor to get up to speed.

Any additional steps should be clearly outlined in the readme. Before sharing the project with other developers, the project creator should test and make sure the installation guide works.

As a project evolves, every contributor is responsible for ensuring the readme reflects the current state of the application.

Remember to keep the readme concise and readable. Include what is absolutely necessary and omit everything else.

## Creating a new project

```
mkdir my-project
cd my-project
npm init
npm shrinkwrap
npm install lodash --save
npm install gulp --save-dev
```

## Project structure

```
.
├── assets
│   ├── background.jpg
│   └── logo.png
├── dist
│   ├── bundle.css
│   ├── bundle.js
│   └── index.html
├── src
|   ├── common
|   │   ├── services
|   │   │   └── auth-service.js
|   │   └── styles
|   │       └── _typography.scss
|   ├── components
|   │   ├── login-page
|   │   │   ├── _login-page.scss
|   │   │   └── login-page.js
|   │   └── navbar
|   │       ├── _navbar.scss
|   │       └── navbar.js
|   ├── config
|   │   └── api.js
|   ├── index.js
|   └── index.scss
├── .editorconfig
├── .eslintrc
├── .gitignore
├── package.json
└── README.md
```

A front-end project should contain at least two key directories: `src` and `dist`, referring to *source* and *distribution*, respectively. The source directory is where we save the code we’ve written, whereas the distribution directory contains the final executable code after compiling and building the application from source. You should not add `dist` to version control. An additional `assets` directory may be created to house images, fonts, audio files, and other presentational resources.

Files and directories in src should be written in kebab-case and all lowercase letters (e.g. `auth-service.js` but not `AuthService.js`), with the exception of partial SCSS files that require a leading underscore. Naming all files and directories in all lowercase letters eliminates conflicts when renaming versioned files and switching between lowercase and uppercase characters.

## Bower vs npm

Bower was traditionally used by front-end projects.

npm is used by Node and Webpack-based projects.

Generally speaking, Bower is used by older JavaScript applications where separate source files are simply concatenated to form a single bundle. Bower modules utilize global variables to communicate with each other. Please use Bower only if you’re working on an existing project that’s built on top of Bower. Also note that Bower-based applications typically also contain a package.json file (npm’s manifest) for managing developer tool dependencies.

## Typical development workflow

```
git pull --rebase
npm install
npm start
git add .
git commit -m "Add feature"
git push origin master
npm run deploy
```

## Starting the development server

Every project should include a *start* script that lifts up a development environment when a developer executes `npm start` on the command-line.

Scripts should only reference local npm modules that are included as dependencies (avoid referencing globally installed packages):

package.json

```json
{
  "scripts": {
    "start": "node node_modules/webpack-dev-server/bin/webpack-dev-server"
  },
  "devDependencies": {
    "webpack-dev-server": "^1.14.1"
  }
}
```

## Dependencies

Dependencies are stored in a `package.json` file (older projects may have a bower.json file for application dependencies). There are two types of dependencies: *application* and *development* dependencies.

Application dependencies are essential packages that are necessary for an application to function. At build time, these dependencies are woven into the distributable bundles to be run on consumer devices. For example, a React-powered website needs the React module in order to render the pages properly, making it an application dependency. Such libraries should be installed with the `--save` flag.

While development dependencies such as Webpack and Gulp may be required for an application to be correctly compiled, built and deployed, they do not affect application-level logic or implementations. Swapping them out should not alter the end product. Development dependencies are placed in `devDependencies` with the `--save-dev` option.

## Environments

An environment is the context an application is running in. Typically, an application runs in at least two environments: a *development* environment (also referred to as a local environment), and a *production* environment.

The development environment is an isolated instance of the application that runs on the developer’s own computer. This is where all the programming happens. The developer has the freedom to extensively test his implementations without having to worry about real-world repercussions.

The production environment is the real, published state of the application running on a dedicated platform. This is the product that end users interact with. The production environment is a sacred domain that must be kept in a working condition at all times.

Each environment shares the same front-end codebase but has its own set of back-end services like databases, email dispatchers, and third-party APIs. This is why we need a clean way to declare separate configurations for each environment.

It should work like so:

- Load the development configuration when lifting up the development environment (development build).
- Load the production configuration when deploying to production (production build).

Most configurations also contain various types of sensitive data such as database passwords and API keys. It’s important that not a single piece of sensitive information should ever end up in a repository. The decision to open-source a codebase may entail unintentionally publishing a set of credentials and compromising an entire service and the privacy of customers.

Configuration data should be stored in environment variables (or in unversioned local configuration files) that can be accessed by build tools (e.g. Webpack or Gulp) to assemble the application. The build tool will then pull out the correct variables depending on whether you’re creating a local or production build. Front-end applications typically use an `.env` file for declaring environment variables.

## Version control

Version control (or source control) brings organizational sanity to programmers. First and foremost, version control systems like Git establish a chronological timeline for your codebase, describing what was modified, added or removed by whom and for what reason.

Issuing a commit is like taking a snapshot of the changes you’ve made. You handpick the changes you wish to include in your commit, write a concise message (e.g. “Decrease navbar font size”), and push it onto the timeline. Other collaborators may then pull your commit and receive your changes.

Commits can be browsed and “time-traveled” to when needed. So instead of arbitrarily modifying a shared folder in Dropbox, you’ll be able to preserve and visualize the entire history and evolution of your codebase since its inception.

Another therapeutic feature of version control systems is that they allow you to create branches. Branches are used for isolating portions of code and preventing them from causing side effects in other parts of the codebase while still in development.
While projects may employ various branching models, the general idea is to have a stable branch called the *master* branch. This is the main branch that contains the most up-to-date stable version of the project. All unfinished bits of code must be kept out of the master branch, and every contributor should strive to keep it in a working (i.e. unbroken) state. Unfinished code should reside in a separate topic branch.

I advise you to keep your commits compact. Bugs are harder to isolate and debug when time-traveling between massive commits. Smaller and more focused commit messages are also easier to scan visually. A lengthier and more descriptive timeline usually beats a shorter and nebulous one.

## Code readability and commenting

Ideally, the best kind of code documentation is self-documenting code. In practice, it means that your code reads naturally.

When writing a docblock comment for a function, ask yourself whether the function really needs a description, or any other written documentation for that matter. Could the function be refactored (restructured and reorganized) to make such comments obsolete?

Consider the following function variations:

```javascript
/**
 * Fetches blog posts by a user.
 */
function blogPosts(id) {
  // Fetches blog posts from the API where the user ID is ‘id’
  return service.posts(id);
}

/**
 * @param {string} userId
 * @return {Promise}
 */
function fetchBlogPostsByUserId(userId) {
  return blogPostApi.findAll({userId});
}
```

Both functions are supposed to fetch blog posts from the API with the given user ID. The only difference is how the functions have been laid out.

First, let’s look at the function `blogPosts`. There I’ve explicitly described the behavior of the function lest other developers misinterpret it. It takes `id` as an argument, but we’re not quite sure if it’s a blog post ID or a user ID. The description vaguely suggests the function accepts a user IDs since we’re fetching blog posts by a user, but it’s not 100% clear until we dive in read the comment inside the function. This problem becomes more apparent when reading calls to the function: `blogPosts(someId).then()...` because *users* may not be mentioned at all, forcing you to dig up the function declaration and read the comments. Also, the function’s internal operation is equally ambiguous since it refers to a `posts` method declared on an arbitrary `service` object which, again, takes a mysterious ID as an argument.

Now, if we inspect the second, refactored function, you’ll notice that we’ve renamed the function and omitted the description. But we’ve added param and return sections to the docblock. They’ve been added so contributors can reference what data types are given to and returned by the function. I’ve also renamed the internals to clarify how the operation works as a whole.

Just don’t go overboard with detail: `fetchBlogPostsByUserIdAndReturnPromise` may also hinder readability since most developers already know that making an HTTP fetch request is asynchronous in nature and should always return a promise object. Let’s keep our names intuitive and also pleasing to look at.

## Deployment

Deployment is the process of publishing an application in a given environment (typically production).

Deployment processes vary depending on the type of application, its dependencies, configuration, hosting services, third-party integrations, and any other characteristics that contribute to its complexity. There really is no one-size-fits-all method. Ideally, deploying an application (especially updating it) should not be made more complicated than executing a single terminal command.

The reason why simplicity matters is that it encourages developers to deploy more often. Frequent deploys means releasing bite-sized features on a more regular basis. While deploying more often does result in introducing bugs more frequently, it reduces the number of large-scale bugs and regressions. From a developer’s point of view, it’s more desirable to fix minor bugs here and there than tackle large ones that break the entire application. Much like focused Git commits, smaller releases will be easier to debug as well. It’s also worth noting that clients and stakeholders will appreciate being able to see new updates more regularly.

TL;DR: Deploy often. Deploy small. Fix more often but on a smaller scale.

## Hosting a front-end application

A front-end application should be a server-agnostic bundle that can be served by any HTTP server or service.

Hosting is a decision that should take the rest of the application architecture into consideration. Most of our front-end applications are served statically over a CDN like Amazon S3.
