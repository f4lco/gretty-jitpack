# Gretty with Gradle 6 / 7 and JitPack

## Building

This example reproducer project applies the Gretty plugin in both Gradle 6 and Gradle 7 projects.

The following incantations should proceed without error:

```
$ gradle wrapper --gradle-version 6.9
$ ./gradlew showClasspath
$ gradle wrapper --gradle-version 7.0.2
$ ./gradlew showClasspath
```

Gretty's `showClasspath` task displays the classpath of the hypothetical webapp and is usually a good indicator if all dependencies can resolve correctly without setting up an example webapp.

## Concerns

- Because Gradle 7 ships with a never Groovy version, we need to force Geb and Spock versions which agree on the Groovy version. Otherwise, you get the error message mentioned in [this PR](https://github.com/gretty-gradle-plugin/gretty/pull/230#issue-659125035).

- Because JitPack rewrites the artifact metadata, and Gretty plugin depends on a couple auxiliary modules, we need to instruct Gradle to rewrite their metadata as well. Otherwise, the core Gretty plugin might stem from the JitPack build, but Gradle might source the ancillary projects from other repositories in the wrong version (namely, the version Gretty has been built with, and not the commit-id).
