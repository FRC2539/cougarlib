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