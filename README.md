# Cougar Library

This is the library that contains the common code required to get a robot up-and-running. 

# Usage

To use this library, add the following to your `build.gradle`:

```
repositories {
    mavenCentral()
}
```

This allows the project to fetch modules from the Maven Central Repository.

Next, add the following to the end of the `dependencies` list:

```
implementation 'com.team2539:cougarlib:2022.0.2'
```

**Replace 2022.0.2 with the most recent version available.**

You may have to build once, but now you can import any files you need from the library.

Example:

```
import com.team2539.cougarlib.controller.LogitechController;
```

# Development

To develop this library, make a local clone, preferably in the same parent folder as a robot project.

For example, if you have the javabot repository in the `code` folder on your computer, you would also clone this library into the `code` folder.

## Workflow

Given the plugin conflicts and the changes to imports in robot projects, it is necessary to follow the steps below when testing this library. 

When you are ready to publish a new version, make sure to undo these changes.

## Resolving Plugin Conflicts

Certain plugins, like the spotless formatter, will create conflicts. 

We use spotless in our robot code, which will cause a conflict, because only the parent project (robot project becomes parent during this whole process) should declare a plugin version.

All you need to do is comment out the plugin import for spotless, and the section labeled `spotless`. 

## Importing into a Robot Project

_In order to test the code in the library, it is easiest to import the library into an existing codebase, like javabot._

To do this, comment out the `implementation` line for this libary in the robot project's dependencies (in `build.gradle`).

Below that line, add `implementation project(":cougarlib")`.

Now, go to the `settings.gradle` file, and add the following to the bottom:

```gradle
include ":cougarlib"
project(":cougarlib").projectDir = file("../cougarlib")
```

**Make sure to run the `Build Robot Command` in this library, and then only after doing so will the build command work in the robot project.**

_You may need to run the `Reload Window` command in the robot project for the language server to recognize the new library source._

## Undoing These Changes

Make sure to undo all the commenting out and import changes that we just made before you commit or publish the robot code or this library. 

Also, make sure to run the spotless formatter on this library before publishing the new version.