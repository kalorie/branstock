# Usage

## Add as a submodule

```
git submodule add <this-url>
```

## Reference within build files

```gradle
// Root project
buildscript {
    ext {
        repo = file("branstock/repositories.gradle")
        java = file("branstock/java.gradle")
        maven = file("branstock/maven.gradle")
    }
}

subprojects {
    apply from: repo
    apply from: java
    apply from: maven
}

// Subproject, for referencing the repo
buildscript {
    apply from: "$rootDir/branstock/repositories.gradle"
    repositories artifactory
    dependencies {
        classpath "some-plugin"
    }
}
```

## Pass different params by system properties

The following system properties could be passed during gradle task execution, e.g. `-Durl=<external-url>`.

* `url`: the host of the repository contained in `rootRepo`
* `rootRepo`: FQDN of the repo, to download artifacts
* `user`: username
* `password`: password
* `releaseRepo`: FQDN of the release repo, e.g. `http://xxx/artifactory/libs-release-repo`
* `snapshotRepo`: FQDN of the snapshot repo, e.g. `http://xxx/artifactory/libs-snapshot-repo`

For the repository hosted by Nexus, the FQDN may be as follows:

* `rootRepo`: `http://x.x.x.x:8081/repository/maven-public`
* `releaseRepo`: `http://x.x.x.x:8081/repository/maven-releases`
* `snapshotRepo`: `http://x.x.x.x:8081/repository/maven-snapshots`

## Download from different repositories

* `local` - Local maven repository, typically `$USER/.m2/repository`;
* `internet` - Maven central and jcenter;
* Private maven repositories such as Artifactory and Nexus deployed within your company. 

# Attic

How to ignore specific files during merging:

```
git merge --no-ff --no-log --no-commit <merge-branch>
git reset HEAD gradle.properties
git checkout -- gradle.properties
git commit -m "<message>"
```
