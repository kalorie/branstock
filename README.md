# Usage

* Add as a submodule

```
git submodule add project-config <this-url>
```

* Reference within build files

```gradle
// Root project
apply from: "project-config/repositories.gradle"
apply from: "project-config/java.gradle"
apply from: "project-config/maven.gradle"

// Subproject, for referencing the repo
buildscript {
    apply from: "$rootDir/project-config/repositories.gradle"
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