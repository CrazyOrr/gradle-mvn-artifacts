# gradle-mvn-artifacts
Helper to config Gradle Artifacts for publishing to Maven repositories.

Supports:
- Java
- Android (working with [Android Gradle plugin](https://developer.android.com/studio/releases/gradle-plugin))
- Android with Kotlin (javadoc generated by [dokka](https://github.com/Kotlin/dokka))

## Usage

### 1. Have a working Gradle build
This is up to you.

### 2. Apply the script from each sub-modules build.gradle where you want to create sources and javadoc jars
```gradle
android {
    // ...
}
dependencies {
    // ...
}
// after android and dependencies configurations

apply from: 'https://raw.githubusercontent.com/CrazyOrr/gradle-mvn-artifacts/master/gradle-mvn-artifacts.gradle'

// before publishing configurations
publishing {
    publications {
        // ...
    }
}
```
Note: You must apply this script after `android` and `dependencies` configurations, before `publishing` configuration,
so that this script can create `sourcesJar` and `javadocJar` 2 tasks for you to reference in `publishing` configuration.

### 3. Use added tasks
```gradle
publishing {
    publications {
        myPub(MavenPublication) {
            artifact sourcesJar
            artifact javadocJar
        }
    }
}
```
Or
```
./gradlew sourcesJar javadocJar
```

## Credits
- [chrisbanes/gradle-mvn-push](https://github.com/chrisbanes/gradle-mvn-push)
- [square/leakcanary](https://github.com/square/leakcanary/blob/master/gradle/gradle-mvn-push.gradle)
- [JakeWharton/timber](https://github.com/JakeWharton/timber/blob/master/gradle/gradle-mvn-push.gradle)