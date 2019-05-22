# Gradle Dependency and Utils [![Hits-of-Code](https://hitsofcode.com/github/exozet/Android-Dependencies)](https://hitsofcode.com/view/github/exozet/Android-Dependencies)

## Introduction

Project wide handling of tested and used libraries. Also including some utility gradle tasks.

# Dependencies

The idea is to have all projects being up-to-date just by updating the dependency submodule.

## Global variables

    compileSdkVer
    buildToolsVer
    minSdkVer
    targetSdkVer
    kotlinVersion
    supportLibVer
    playServicesVer
    firebaseVer
    retrofitVersion
    robolectricVersion

## Gradle Plugins

    ext.plugin

## Gradle Library Plugins

    ext.pluginLibrary

## Gradle Libraries

    ext.libs

## Gradle Test Libraries

    ext.testLibs

## Gradle Android Test Libraries

    ext.androidTestLibs

## Gradle Configs

    ext.configs

# Utils

## Exported Tasks

### Gradle Wrapper

Mind the : in front of wrapper to execute task in root project instead of subproject.

    gradle :wrapper

### generateReleaseNotes

Meant to write end-user non technical release notes for automated store publications.

### generateChangelog

Generates a file at ${project.rootDir}/app/src/main/assets/CHANGELOG.md including a list of all git commits with VSC hash link and commit user.

    preBuild.dependsOn generateChangelogTask

### copyReadme

Copies README.md to ${project.rootDir}/app/src/main/assets/

### generateEnvironmentLog

Meant to debug build environment issues, never bundle it into a release version, due it may include build environment secrets.

Generates a file at ${project.rootDir}/app/src/main/assets/ENVIRONMENT.md including System.getenv()

    preBuild.dependsOn generateEnvironmentLogTask

### commitHash

Prints current commit hash.

### commitCount

Prints amount of commits based on current branch. (Caution when using it for versionCode: it's meant for release branches, due every branches can have a higher number.)

### simpleReleaseVersionName

Creating release version name. Format: major.minor.build.

### canonicalReleaseVersionName

Creating release version name. Format: branch/major.minor.build-commithash

### buildNumberByCI

Getting build number from Jenkins, Travis or Bitrise.

### branchName

Getting branch name from CI or from git directly.

### branchNameByCI

Getting build number from Jenkins, Travis or Bitrise.

### branchNameByGit

Basically calls:

    git rev-parse --abbrev-ref HEAD

## To add tasks to preBuild

    task('printEnvironmentTask') {
        println(System.getenv())
    }

    task('generateEnvironmentLogTask') {
         // generateEnvironmentLog() for debugging purposes
    }

    task('generateChangelogTask') {
        generateChangelog()
    }

    task('generateReleaseNotesTask') {
        generateReleaseNotes()
    }

    task copyReadme(type: Copy) {
        from "${project.rootDir}/README.md"
        into "${project.rootDir}/app/src/main/assets"
    }

    preBuild.dependsOn printEnvironmentTask
    preBuild.dependsOn generateChangelogTask
    preBuild.dependsOn generateReleaseNotesTask
    preBuild.dependsOn copyReadme

# bintray

    apply from: "${project.rootDir}/Android-Dependencies/bintray.gradle"

bintray.properties

    bintray.user=
    bintray.apikey=
    bintray.organization=
    bintray.gpg.password=

    binrtray.group =
    binrtray.repo = 'maven'
    binrtray.name =
    bintray.licenses = 'MIT'

    bintray.vcsUrl =
    bintray.websiteUrl =
    bintray.version.desc =

# javadoc

apply from: "${project.rootDir}/Android-Dependencies/javadoc.gradle"