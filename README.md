The project demonstrates a problem of ajoberstart/gradle-git release plugin:  https://github.com/ajoberstar/gradle-git/issues/181

### Problem description 
When being applied to a project with native components (C/C++), the plugin somehow disables/removes buildType variant of the name 'release':
```
buildTypes {
    debug
    release 
}
```

### how to run 
$ ./gradlew clean collectExecutables -Prelease.version=1.0.0-SNAPSHOT

this gives the following:
```
$ ./gradlew clean collectExecutables -Prelease.version=1.0.0-SNAPSHOT
bin[executable] is of buildType: debug
:clean
:compileHelloExecutableHelloC
:linkHelloExecutable
:helloExecutable
:collectExecutables

BUILD SUCCESSFUL
```

As you can see there is only one build variant (of type 'debug')
  
### workaround & correct output
As a workaround, you can rename 'release' buildType e.g. 'xrelease':

```
buildTypes {
    debug
    xrelease // <-- renamed buildType 
}
```

You can then see both variants (debug * xrelease)

```
 $ ./gradlew clean collectExecutables -Prelease.version=1.0.0-SNAPSHOT
bin[debugExecutable] is of buildType: debug
bin[xreleaseExecutable] is of buildType: xrelease
:clean
:compileHelloDebugExecutableHelloC
:linkHelloDebugExecutable
:helloDebugExecutable
:compileHelloXreleaseExecutableHelloC
:linkHelloXreleaseExecutable
:helloXreleaseExecutable
:collectExecutables

BUILD SUCCESSFUL
```
  
 



