# Cougar Library

This is the library that contains the common code required to get a robot up-and-running. 

## Usage

Begin by adding this project as a git submodule.

Run (**in the root directory of your project**):

`git submodule add https://github.com/FRC2539/cougarlib.git cougarlib`

### Importing The Library

In `build.gradle` add the following at the end of the dependencies list:

```
implementation project(':cougarlib')
```

In `settings.gradle` add the following to the end of the file:

```
include ':cougarlib'
project(':cougarlib').projectDir = new File('./cougarlib')
```

### Preventing Formatting Errors

If your project uses spotless or another formatter that runs checks during a build, you'll need to ignore the submodule folder.

For spotless, change your configuration from something like this:

```
spotless {
   java {
      target fileTree('.') {
            include '**/*.java'
            exclude '**/build/**', '**/build-*/**'
      }
      toggleOffOn()
      palantirJavaFormat()
      removeUnusedImports()
      trimTrailingWhitespace()
      endWithNewline()
   }
}
```

to something like this (exclusion added):

```
spotless {
   java {
      target fileTree('.') {
            include '**/*.java'
            exclude '**/build/**', '**/build-*/**'
            exclude 'cougarlib'
      }
      toggleOffOn()
      palantirJavaFormat()
      removeUnusedImports()
      trimTrailingWhitespace()
      endWithNewline()
   }
}
```