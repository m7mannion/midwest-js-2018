# MidwestJS 2018 Notes
## Day 1

### React Workshop
_Dustin Schau & Travis Martensen_

[Workshop and Labs](https://react-training.objectpartners.com)

## Day 2 

### Automated Testing with Cypress
_Mike Plummer_

[Slides](https://mike-plummer.github.io/cypress-presentation/#/)

* Common Problems
  * Require manual intervention
  * Non-idempotent
  * Interdependent
  * External Dependencies
  * cross-browser compatibility
    * With Selenium they don't really work the same way
* Tests are flaky, hard to maintain and hard to setup
* Cypress runs inside the browser and replaces the browser app interface
* Uses well-know stack: Mocha + Chai + Sinon
* Auto-waiting to reduce flake. Selenium doesn't do this, it doesn't wait.
* Runs in the browser so it's debuggable
* Time Travel - automatically snapshots at every stage of the test
* Supports headless testing (CI)
* Improved browser control
* Able to mock network requests and the clock (i.e. Session timeout)
* Limitations:
  * single browser instance/tab
  * Each test can only access a single domain
  * More difficult to use existing common/server-side code like you could in Selenium
  * Currently only supports Chromium/Chrome but that's changing
* Setup/Config
  * Node, Common OS packages for headless browser support
  * No special IDE tools required
* Install: `yarn add cypress --dev` or `npm install cypress --save-dev`
* Setup: `yarn cypress open` or `npx cypress open`
> Directory structure
```
cypress.json
/cypress
  /fixtures
    - *.json

  /integration
    - *.spec.js

  /plugins
    - index.js

  /support
    - commands.js
    - index.js
```
* Plugins is an advanced topic we won't cover
* `/support` common commands can go here
* `yarn cypress run` runs all tests, `cypress open` is the interactive test runner. Includes it's own Chromium browser but allows you to choose one from your system that it automatically searches for.
* May not currently have test suite capabilities - presenter didn't know.
* See [online docs](https://docs.cypress.io/guides/overview/why-cypress.html#) for API details
  * Tests use Mocha + Chai
  * `context` is a stylistic feature for grouping
  * All Cypress actions start with `cy`
  * Cypress is promise-based. Actions are executed asynchronously
  * `Record` Videos automatically recorded during `cypress run`. Screenshots automatically taken on failure.
  * _Selector builder_ (playground on CLI) for `get` which uses jQuery style selectors to target specific elements. Waits for them and will timeout after default time that can be modified before erroring out.
  * Can alias element selectors
  * Interactions
  * Viewport for scrolling into view, moving things around, resize, etc. Can be used for responsive design.
  * Eventing
  * Assertions: Supports Chai, Chai-jQuery and Sinon assertions. Can use arrow functions
  * Control cookies and storage
  * Control Time!!!
  * Can make XHR requests
  * Commands is a way to extract steps and create a custom Cypress API entry for re-use.
* Test runner live updates as you write tests
* Roadmap: multi-browser but **never IE**. Sauce Labs integration.



### Modern JavaScript Tools
_Mark Volkmann_

[Slides](https://github.com/mvolkmann/talks/blob/master/ModernJSTools.key.pdf)

* He runs everything from node/npm.
* `npx` See https://www.npmjs.com/package/npx
* See cross-environment scripts for commands defined in package.json.
* `ESLint` instead of older jslint
  * Has `--fix` mode that modifies source files for some common errors
  * See also `babel-eslint`
* Prettier
* Babel. Use configuration `.babelrc` to control browsers and Node versions supported.
* Skipped Jest and Flow slides
* Istanbul comes with Jest for coverage but can be used standalone
* See [Parcel](https://parceljs.org) which he uses over Webpack or Rollup. Transpiles using Babel. Enables use of ES6 import/export syntax rathr than adding a script tag for each .js file in main html.
  * Has a watch/reload capability
* Browsersync
* Husky: Git hooks made easy. 
* Likes [Flow.js](https://flow.org) over TypeScript for various reasons noted in the slides. Facebook team is focusing on [ReasonML](https://reasonml.github.io) instead of flow. It compiles to JS.


### Room with a Vue - Introduction to Vue.js
_Zachary Klein_

* Vue is a library, not a framework. Falls between Angular and React. Focuses on the "view" portion of MVC.
* Install from NPM. Latest is v3 which is not GA.
* Easiest way is to source in library from CDN.
* Starts when you create `new Vue({...})` instance. You pass an object where you identify what in the DOM it will manage/render.
* `data` Object describing the state of the app/component. Add's watchers to manage state.
* `method` Object containing functions. Can access/manipulate data. Can be called from templates.
* Vue creates getters/setters for all data properties
* `computed` Properties. Functions that return dynamic values.
* `templates` HTML based templating syntax using Mustache syntax.
* `directives` Vue-specific element attributes
* `components` Nested component hierarchy. Each renders either a template or returns `createElement()` calls (JSX is supported). Single file components (*.vue files)


### Rapid REST API Development with Node and SailsJS
_[Justin James](https://digitaldrummerj.me)_

[Slides](https://www.slideshare.net/digitaldrummerj/rapid-api-development-with-node-and-sails)

[Code](TBD)

* Auto-generated REST APIs
* Any database
* Flexible and configurable
* Security policies, simple yes/no checks. Wiring done for you. Setup via configurations
* Built on top of _Express_
* Ridiculously fast and it just works
* Does not hide the magic
* Getting started
  * Install Node
  * `npm install -g sails` Generates new project, comes with a server and generates models, actions and controllers
  * Has the Vue engine installed
* `sails new [project name]` Choose option 2 blank app
* `sails lift` Start Sails server
* `sails inspect` Chrome debugger
* `sails console` 
* `sails generate [type] [name]`
* API generates both model and controller. Model represents a record. Usually maps to db. Attributes map to columns.
* Controllers are dictionary of actions. Responds to requests. Bound to routes
* Actions respond to requests, bound to routes, structured way to create an action. 1 file per action
* Does not have a live reload
* Presenter was somehow running REST calls from JS code in VSCode editor
* Helpers are reusable bits of code available to the whole app
* Handles custom responses
* Node-env determines production which won't return data for 500 errors. In dev it will to assist with troubleshooting.
* CORS under config/security.js
* Recommend for production that you explicitly define your routes


### E2E testing your SEO with headless chrome and puppeteer
_Tristan Sokol_

[Slides](https://blog.tristansokol.com/Presentations/seo-testing/index.html#/)

* Options for different outputs - PDF, images.
* Image diffing - see pixelmatch link on slides
* Puppeteer - Node.js bindings for headless Chrome
* Almost every command is asynchronous. Async await is common with puppeteer
* Can have handlers for requests/responses
* Typing allows you to slow it down so type-ahead events can occur


## Day 3

### Accessibility for Web Apps
_Aaron Cannon_

* Speakers from Accessible360 in Minneapolis. They specialize in A11Y.
1. What is it?
2. Getting Started
3. Example Scenarios
4. Screen Reader
5. Development Strategies
* It's not simply a checkbox. It's a process improvement program. Plan, Do, Check, Act cycle
* **IS** the practice of removing barriers that prevent equal access to your digital content for everyone.
* Assistive Technology - some you'll spend more time (i.e. screen readers)
* **IS NOT** a formidable* effort that only helps a small amount of people
* 1 in 5 Americans ~56.7 million
  * 4 categories: vision, physical, auditory, cognitive
* Legal issues. Mostly public facing stuff. Moving towards applications behind firewalls that affect job accessibility.
* **IS** a standards-based process. Published by W3C. Currently version 2.1. **WCAG**.
* Use the features of the tools you have - for example in Word use headings instead of large bold fonts.
* Getting Started
  * Process improvement
  * Determine most common issues
  * Stay educated
* Process Improvement
  * Design - designers send the Invision files. Color contrast issues are most common.
  * Development
  * IT/Infrastructure
  * Content
* Most Common Issues
  * Audit your stuff
  * Prioritize within your roadmap
  * Think about fixes globally
  * Headings & Lists (use 'em correctly)
  * Icons (aria-hidden with sr-only text)
  * Color Contrast
  * Skip To Content links
  * Focus indicators
* Stay Educated
  * Continually monitor your app
  * Watch for trends in design, the law, libraries
  * New hires!
* Example Functionality
  * Easiest to test
  * Good indicator of overall a11y
  * Skip to Content link
  * Easily identifiable focus indicator
* Screen Readers
  * Most unknown to developers
  * Ignore more styling/css
  * Element order almost always follows the DOM and not visual layout
  * Live example on Duolingo showed how difficult it is for a11y user to understand what the page is providing you. Speech is a 1-dimensional view, you don't have the concept of above/below, etc.
* Development Strategies
  * \#1 Rule! Always, always use semantic HTML
  * See General Guidelines slide
  * Structuring text
  * Text Color Contrast
  * Menus and Navigation
  mailto:aaron@accessible360.com
  * Headings & Landmarks - HTML5 Semantic Elements
  * Images & `alt` attributes
  * Icons
  * Forms
  * Other elements - Tables (understand thead, th and scopes), Frames, Video
  * Modal/Dialog windows
  * Tabs
  * Single Page Apps
* JAWS or NVDA tools. Good idea to bring in someone who uses a screen reader for QA testing and important to have someone in the organization who understands what a11y is and how to do it.
* JIRA broker their entire page recently causing screen readers to not read anything.

### Modern JavaScript in the Java-only Enterprise
_Bruce Coddington_

Bruce Coddington - works at Mutual of Omaha. Modernizing their applications from the 70's.
* Didn't trust JavaScript. They were using GWT. Tons of Java to build small amounts of JavaScript.
* Years invested in a component library in GWT.
* **Goal**: slowly introduce modern JS frameworks. Select teams started using React and Vue. Designers wanted Vue because they use Laravel. Devs wanted React.
  * Experiences sparked curiosity which lead to more teams building JS applications.
* **Challenge**: was build tools were based on JVM - Gradle builds. Enterprise repo was only setup for Maven-style libs.
* **Goal**: to make JS a first class citizen
  * Code quality tools (Sonar) modified to support JS
* **Challenge**: JS existed in scripts tags in JSPs or single large file
  * Code copy/pasted everywhere across multiple JSPs - this made testing JS impossible
* Created internal JS User Group
  * Front End Developers Community of Practice
  * Presentations from teams on shared libraries
  * Workshops on development process via templates
  * Became an inspiration of other COP's
* **Challenge**: Server infrastructure only supported deploying web app via WAR
* **Goal:** Containerize deployments via build pipeline
* Moving to Nginx
* **Challenge**: NodeJS was not authorized to be installed on development workstations
  * Only JVM technologies were approved
  * There was fear that teams would try to build APIs with Node
  * Management was unaware that Node wasn't just for building apps
* **Goal**: Educate on multiple uses of Node.js
  * Initial workaround was to install gradle-node plugin
  * POC to prove to management
  * Special admin privileges granted to devs
  * Multiple blogs posts on workstation setup were created
* **Challenge**: most dev teams were unaware of modern JS tooling
  * Infrastructure team had no exposure
  * Many teams didn't know where to start
  * Architecture team was suspicious of adding additional technologies
* **Goal**: Create multiple project templates - react, vue, etc.
  * Multiple collaboration sessions with infra team
  * Webpack and Jest configurations setup
  * NPM tasks preset specifically for Continuous Integration platform
  * Gradle task that delegate to NPM tasks automatically. Java footprint reduced
* Don't get hung up on best practices. Collaborate and share. Best practices are in their templates.
* Be willing to accept the tradeoffs during the transition but don't paint yourself into a corner
* Let the code do the talking for you. Build projects and demo, demo, demo.
* Don't try to do it alone. Build a community


### Hello Real World of Legacy Code: Story of Yelp's Migrate to React
_Tanvi_

* Why is legacy code a concern?
  * Architectural decisions
    * Scalability
    * Reusability
    * Tight coupling
    * Ownership
  * Maintenance
  * Testing
  * Performance
* Recognize the problem
* Forsee the future - requires some experience
* See **Bugsnag.com** tool for monitoring application stability

### Building a GraphQL Client in JavaScript
_Joe Karlsson_

* JavaScript, GraphQL, Apollo and React
* https://github.com/JoeKarlsson/graphql-apollo-demo
* GraphQL is a REST killer. Instead of hitting separate REST endpoints you hit a single endpoint. GraphQL does the work for you.
* You describe the shape you need the data in.
* Get back what you ask for. Does away with the need to work with the "data" team to update/create their service for you for new/udpated data.
* Why use it?
  * Declarative
  * De-coupled from storage. Nothing to do with graphs or databases
  * Validated and structured. Strongly typed so you have a schema
  * Facilitates collaboration
  * Super fast
  * No more API versioning
* Query language for schema is a little odd but the docs are good to explain details
* GraphQL has a playground to trial queries
* Can create code snippets
* graphqlhub.com
* Appollo is a view agnostic wrapper for your GrpahQL components
  * Declarative data fetching
  * zero-config caching
  * Combines local & remote data
  * Vibrant ecosystem
* Can connecct to back-end via websockets
* Can combine front-end and back-end state
* How to get better at it since it can be intimidating - just try it, play around with graphqlhub.com, howtographql.com
* Very actively being changed so be aware if you build for production is may change! 

### Using JavaScript to write Native Application/SDKs for iOS, Android and the web
_Siddharth Malkireddy/Derek Anderson_

[OpenSource Site](https://syr.js.org)

* Speakers from PayPal
* Slow cycle to update SDK when you just want to change the UI to keep it up to date with the latest. They want dynamically updatable UIs. Needed to be simple for merchants to integrate.
* Less friction with merchants
* Goals
  * Easy to integrate. PayPal was known for not being easy to integrate.
  * Light
  * Complete
  * Dynamic
* Cordova was not an option because they wanted a native experience
* React Native was chosen
  * Large ecosystem and community
  * Multi-platform friendly (iOS, Android, Windows)
  * Common JavaScript Design (ES Classes, JSX via Babel)
  * Easily extendable
  * Dynamically updatable (Without the need for rebuilding native code)
* What didn't work
  * Moved really fast, we made no decisions
  * Things changed a lot
  * Integration as an SDK wasn't the best
  * Already big, grew heavier over time
* What was painful
  * 2nd and 3rd party devs were apprehensive
  * Goals
    * Too many libs, hard to internalize, required NPM to distribute
    * Ambitious, bloated SDK
* ...and SYR was born - Light Dynamic UI Engine for Everywhere
* Borrowed the best from React
* 100% code compatibility
* Easy to write and integrate native modules
* Dynamically updatable
* No more JSC - hello native JS engine
* Reduced surface area of code
* Debugging tools
* No React in the codebase
