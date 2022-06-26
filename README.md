# Cougar Library

This is the library that contains the common code required to get a robot up-and-running. 

## Usage

Begin by adding this project as a git submodule.

Run (**in the root directory of your project**):

```
git submodule add https://github.com/FRC2539/cougarlib.git cougarlib

cd cougarlib

git submodule update --init
```

## Keeping The Libraries Updated
We recommend using the source control page in VSCode to pull any library changes from GitHub. 

The same results can be achieved using `git submodule ...`, but the source control panel is easier with a complex library like this.

### Importing The Library

In `build.gradle` add the following at the end of the dependencies list:

_Note: the cougar-swerve-lib section is optional. Import only `:cougarlib` if desired._

```
implementation project(':cougarlib:cougar-swerve-lib')
```

In `settings.gradle` add the following to the end of the file:

```
include ':cougarlib'
include ':cougarlib:cougar-swerve-lib'
project(':cougarlib').projectDir = new File('./cougarlib')
project(':cougarlib:cougar-swerve-lib').projectDir = new File('./cougarlib/cougar-swerve-lib')
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