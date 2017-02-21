
## NubeIO modifcations

In order to test or install the project, you need to set up two components together.

The first step is obviously to **clone the project**. Then, please follow the instructions below to install both components.

# Net-persistence-bundle #
To install the net-persistence bundle:

*  Copy the `net-persistence-bundle` directory from the repository into the main OpenMCT folder, where there is files like `app.js` and `index.html`.
*  Edit the `index.html` file.
*  Find the `<script>` tag with `require(['openmct', ` inside it;
*  Right before `], function (openmct) {`, add the following:
```
#!javascript

, 'net-persistence/bundle'
```
*  Right before `].forEach(`, add a new line with this inside it:
```
#!javascript

'net-persistence'
```
*  In the line just above the `'net-persistence'` line, add a comma at the end of that line.
*  Please comment the line `'platform/persistence/local'` by prepending it with two slashes.
*  In the end, it should look like this:
```
#!html

    <script>
        require([
            'openmct',
            'net-persistence/bundle'
        ], function (openmct) {
            [
                'example/imagery',
                'example/eventGenerator',
                'example/generator',
                'platform/features/my-items',
                // 'platform/persistence/local',
                'net-persistence'
            ].forEach(
                openmct.legacyRegistry.enable.bind(openmct.legacyRegistry)
            );
            openmct.start();
        });
    </script>
```
*  Now you are good to go.

# Net-persistence-server #
Time to make the server installed and running.
The server has to run on the same machine where OpenMCT resides.

*  Open a terminal (or command line prompt, command prompt, etc.).
*  Inside the terminal, navigate to the directory where `net-persistence-server` resides.
*  Type the following command for the first time. It will install dependencies needed for the server to run:
```
#!shell

npm install
```
*  Then, to run the server, type this command:
```
#!shell

npm start
```

There you go! Now, if you open OpenMCT, you should be up & running while using the net-persistence-server's storage, and not your browser local storage.


## Start of openmct read me














# Open MCT [![license](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](http://www.apache.org/licenses/LICENSE-2.0)

Open MCT is a next-generation mission control framework for visualization of data on desktop and mobile devices. It is developed at NASA's Ames Research Center, and is being used by NASA for data analysis of spacecraft missions, as well as planning and operation of experimental rover systems. As a generalizable and open source framework, Open MCT could be used as the basis for building applications for planning, operation, and analysis of any systems producing telemetry data.

Please visit our [Official Site](https://nasa.github.io/openmct/) and [Getting Started Guide](https://nasa.github.io/openmct/getting-started/)

## See Open MCT in Action

Try Open MCT now with our [live demo](https://openmct-demo.herokuapp.com/).
![Demo](https://nasa.github.io/openmct/static/res/images/Open-MCT.Browse.Layout.Mars-Weather-1.jpg)

## New API

A simpler, [easier-to-use API](https://nasa.github.io/openmct/docs/api/)
has been added to Open MCT. Changes in this
API include a move away from a declarative system of JSON configuration files
towards an imperative system based on function calls. Developers will be able
to extend and build on Open MCT by making direct function calls to a public
API. Open MCT is also being refactored to minimize the dependencies that using
Open MCT imposes on developers, such as the current requirement to use
AngularJS.

This new API has not yet been heavily used and is likely to contain defects.
You can help by trying it out, and reporting any issues you encounter
using our GitHub issue tracker. Such issues may include bugs, suggestions,
missing documentation, or even just requests for help if you're having
trouble.

We want Open MCT to be as easy to use, install, run, and develop for as
possible, and your feedback will help us get there!

## Building and Running Open MCT Locally

Building and running Open MCT in your local dev environment is very easy. Be sure you have [Git](https://git-scm.com/downloads) and [Node.js](https://nodejs.org/) installed, then follow the directions below. Need additional information? Check out the [Getting Started](https://nasa.github.io/openmct/getting-started/) page on our website.
(These instructions assume you are installing as a non-root user; developers have [reported issues](https://github.com/nasa/openmct/issues/1151) running these steps with root privileges.)

1. Clone the source code

 `git clone https://github.com/nasa/openmct.git`

2. Install development dependencies

 `npm install`

3. Run a local development server

 `npm start`

Open MCT is now running, and can be accessed by pointing a web browser at [http://localhost:8080/](http://localhost:8080/)

## Documentation

Documentation is available on the [Open MCT website](https://nasa.github.io/openmct/documentation/). The documentation can also be built locally.

### Examples

The clearest examples for developing Open MCT plugins are in the
[tutorials](https://nasa.github.io/openmct/docs/tutorials/) provided in
our documentation.

For a practical example of a telemetry adapter, see David Hudson's
[Kerbal Space Program plugin](https://github.com/hudsonfoo/kerbal-openmct),
which allows [Kerbal Space Program](https://kerbalspaceprogram.com) players
to build and use displays for their own missions in Open MCT.

Additional examples are available in the `examples` hierarchy of this
repository; however, be aware that these examples are
[not fully-documented](https://github.com/nasa/openmct/issues/846), so
the tutorials will likely serve as a better starting point.

### Building the Open MCT Documentation Locally
Open MCT's documentation is generated by an
[npm](https://www.npmjs.com/)-based build.  It has additional dependencies that
may not be available on every platform and thus is not covered in the standard
npm install.  Ensure your system has [libcairo](http://cairographics.org/)
installed and then run the following commands:

* `npm install`
* `npm install canvas nomnoml`
* `npm run docs`

Documentation will be generated in `target/docs`.

## Deploying Open MCT

Open MCT is built using [`npm`](http://npmjs.com/)
and [`gulp`](http://gulpjs.com/).

To build Open MCT for deployment:

`npm run prepublish`

This will compile and minify JavaScript sources, as well as copy over assets.
The contents of the `dist` folder will contain a runnable Open MCT
instance (e.g. by starting an HTTP server in that directory), including:

* A `main.js` file containing Open MCT source code.
* Various assets in the `example` and `platform` directories.
* An `index.html` that runs Open MCT in its default configuration.

Additional `gulp` tasks are defined in [the gulpfile](gulpfile.js).

## Bundles

A bundle is a group of software components (including source code, declared
as AMD modules, as well as resources such as images and HTML templates)
that is intended to be added or removed as a single unit. A plug-in for
Open MCT will be expressed as a bundle; platform components are also
expressed as bundles.

A bundle is also just a directory which contains a file `bundle.json`,
which declares its contents.

The file `bundles.json` (note the plural), at the top level of the
repository, is a JSON file containing an array of all bundles (expressed as
directory names) to include in a running instance of Open MCT. Adding or
removing paths from this list will add or remove bundles from the running
application.

## Tests

Tests are written for [Jasmine 1.3](http://jasmine.github.io/1.3/introduction.html)
and run by [Karma](http://karma-runner.github.io). To run:

`npm test`

The test suite is configured to load any scripts ending with `Spec.js` found
in the `src` hierarchy. Full configuration details are found in
`karma.conf.js`. By convention, unit test scripts should be located
alongside the units that they test; for example, `src/foo/Bar.js` would be
tested by `src/foo/BarSpec.js`. (For legacy reasons, some existing tests may
be located in separate `test` folders near the units they test, but the
naming convention is otherwise the same.)

### Test Reporting

When `npm test` is run, test results will be written as HTML to
`target/tests`. Code coverage information is written to `target/coverage`.


### Functional Testing

The tests described above are all at the unit-level; an additional
test suite using [Protractor](https://angular.github.io/protractor/)
is under development, in the `protractor` folder.

To run:

* Install protractor following the instructions above.
* `cd protractor`
* `npm install`
* `npm run all`

# Glossary

Certain terms are used throughout Open MCT with consistent meanings
or conventions. Any deviations from the below are issues and should be
addressed (either by updating this glossary or changing code to reflect
correct usage.) Other developer documentation, particularly in-line
documentation, may presume an understanding of these terms.

* _bundle_: A bundle is a removable, reusable grouping of software elements.
  The application is composed of bundles. Plug-ins are bundles. For more
  information, refer to framework documentation (under `platform/framework`.)
* _capability_: An object which exposes dynamic behavior or non-persistent
  state associated with a domain object.
* _composition_: In the context of a domain object, this refers to the set of
  other domain objects that compose or are contained by that object. A domain
  object's composition is the set of domain objects that should appear
  immediately beneath it in a tree hierarchy. A domain object's composition is
  described in its model as an array of id's; its composition capability
  provides a means to retrieve the actual domain object instances associated
  with these identifiers asynchronously.
* _description_: When used as an object property, this refers to the human-readable
  description of a thing; usually a single sentence or short paragraph.
  (Most often used in the context of extensions, domain
  object models, or other similar application-specific objects.)
* _domain object_: A meaningful object to the user; a distinct thing in
  the work support by Open MCT. Anything that appears in the left-hand
  tree is a domain object.
* _extension_: An extension is a unit of functionality exposed to the
  platform in a declarative fashion by a bundle. For more
  information, refer to framework documentation (under `platform/framework`.)
* _id_: A string which uniquely identifies a domain object.
* _key_: When used as an object property, this refers to the machine-readable
  identifier for a specific thing in a set of things. (Most often used in the
  context of extensions or other similar application-specific object sets.)
* _model_: The persistent state associated with a domain object. A domain
  object's model is a JavaScript object which can be converted to JSON
  without losing information (that is, it contains no methods.)
* _name_: When used as an object property, this refers to the human-readable
  name for a thing. (Most often used in the context of extensions, domain
  object models, or other similar application-specific objects.)
* _navigation_: Refers to the current state of the application with respect
  to the user's expressed interest in a specific domain object; e.g. when
  a user clicks on a domain object in the tree, they are _navigating_ to
  it, and it is thereafter considered the _navigated_ object (until the
  user makes another such choice.)
* _space_: A name used to identify a persistence store. Interactions with
  persistence will generally involve a `space` parameter in some form, to
  distinguish multiple persistence stores from one another (for cases
  where there are multiple valid persistence locations available.)
