Semantic Versioning with Maven
==============================

This very simple maven project demonstrates how semantically correct version number
can be inserted into the build manifest file (META-INF/MANIFEST.MF).

More info on semantic versioning can be found at http://semver.org

To validate user-specified buildVersion I used a regular expression developed by [AJ ONeal](https://github.com/coolaj86) https://gist.github.com/coolaj86/3012865

Example usage
-------------

```
# Run locally
mvn clean package
```

The above creates a package and generates a MANIFEST.MF file similar to the below:

```
  1 Manifest-Version: 1.0
  2 Build-Time: 20130321-1404
  3 Build-Java: 1.6.0_43
  4 Build-Qualifier: SNAPSHOT
  5 Built-By: janek
  6 Created-By: Apache Maven
  7 Build-Path: /Users/janek/Documents/projects/examples/simple-webapp
  8 Build-OS: Mac OS X
  9 Build-Jdk: 1.6.0_43
 10 Build-Version: 1.2.3+build
 11 Build-Maven: Maven 3.0.3
 12 Build-Label: 1.2.3-SNAPSHOT
 13 Build-User: janek
 14 Archiver-Version: Plexus Archiver
```

Note the Build-Version part: 1.2.3+build, which means "that's a current development version of 1.2.3".

To generate a version number containing the build number you can use one of the following:

```
# That's what you can run on your CI server
mvn clean package -D buildVersion=+build

mvn clean package -D buildVersion=-rc.1

mvn clean package -D buildVersion=-rc.1+build

mvn clean package -D buildVersion=-rc.1+build.1

mvn clean package -D buildVersion=+build

mvn clean package -D buildVersion=+build.69

mvn clean package -D buildVersion=+build.69.b8f12d7
```

which results in one of the following version strings:

```
 10 Build-Version: 1.2.3+build
 ...
 10 Build-Version: 1.2.3-rc.1
 ...
 10 Build-Version: 1.2.3-rc.1+build
 ...
 10 Build-Version: 1.2.3-rc.1+build.1
 ...
 10 Build-Version: 1.2.3+build
 ...
 10 Build-Version: 1.2.3+build.69
 ...
 10 Build-Version: 1.2.3+build.69.b8f12d7
```

Using VERSION_NUMBER in .jsp files
----------------------------------

This example also presents how the semantic version string can be included in .jsp files.
Any occurence of a %VERSION_NUMBER% token is replaced with an actual version number during maven's prepare-package phase.
