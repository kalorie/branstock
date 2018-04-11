# Usage

* Add as a submodule

```
git submodule add <this-url>
```

* Reference within build files

```gradle
// Root project
apply from: file("branstock/repositories.gradle")
apply from: file("branstock/java.gradle")
apply from: file("branstock/maven.gradle")

// Subproject, for referencing the repo
buildscript {
    apply from: "$rootDir/branstock/repositories.gradle"
    repositories artifactory
    dependencies {
        classpath "some-plugin"
    }
}
```

# Attic

How to ignore specific files during merging:

```
git merge --no-ff --no-log --no-commit <merge-branch>
git reset HEAD gradle.properties
git checkout -- gradle.properties
git commit -m "<message>"
```
