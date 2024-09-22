## This project is a comprehensive suite of convention plugins that drastically simplify gradle management in multi module applications.

## It includes plugins for the following configuration applications:
- Android application config
- Android application compose config
- Android Wear os application config
- Android library config
- Android library compose config
- Android dynamic feature config
- Android feature UI config
- Android Room database config
- JVM library config
- JVM library with Ktor config

## These plugins simplify gradle management by:
- Allowing you to consolidate the configuration logic of the `build.gradle` file in the relevant module into a couple lines of code
- Preventing version inconsistencies in your dependencies since all plugins reference the version catalog directly
- Ensuring consistency in your projects gradle setup across all modules
- Easing the automation of build tasks

  
## How to use:

This repository contains the `build-logic` module by itself as well as a sample project that you can use as a reference during the set up process.

## Step 1:
  Clone the repository

## Step 2:
  Copy the `build-logic` module and paste it into your projects root directory

## Step 3:
  Add the necessary dependencies
  The `build-logic` module contains a variety of plugins by default and this setup guide assumes you want to keep / use all of them for the sake of simplicity. 
  The sample projects version catalog contains all of the needed dependencies along with versions that are guaranteed to work with each other. 

  Note that in order to access other modules using dot notation when adding them as a dependency like this:
  `implementation(projects.auth.domain)`
 
  You will need to add this line to your projects `settings.gradle` file:
  
 `enableFeaturePreview("TYPESAFE_PROJECT_ACCESSORS")`
  
  

## Step 4:
  Add the convention plugins to your version catalog:

  `yourapp-android-application = { id = "yourapp.android.application", version = "unspecified" }`
  
  `yourapp-android-application-compose = { id = "yourapp.android.application.compose", version = "unspecified" }`
  
  `yourapp-android-library = { id = "yourapp.android.library", version = "unspecified" }`
  
  `yourapp-android-library-compose = { id = "yourapp.android.library.compose", version = "unspecified" }`
  
  `yourapp-android-feature-ui = { id = "yourapp.android.feature.ui", version = "unspecified" }`
  
  `yourapp-android-room = { id = "yourapp.android.room", version = "unspecified" }`
  
  `yourapp-android-dynamic-feature = { id = "yourapp.android.dynamic.feature", version = "unspecified" }`
  
  `yourapp-jvm-library = { id = "yourapp.jvm.library", version = "unspecified" }`
  
  `yourapp-jvm-ktor = { id = "yourapp.jvm.ktor", version = "unspecified" }`
  
  `yourapp-android-application-wear-compose = { id="yourapp.android.application.wear.compose", version="unspecified"}`

  <br>
  

  If you don't already have them added to your version catalog you will also need these plugins:

  <br>

  `android-application = { id = "com.android.application", version.ref = "agp" }`
  
  `android-library = { id = "com.android.library", version.ref = "agp" }`
  
  `jetbrainsKotlinAndroid = { id = "org.jetbrains.kotlin.android", version.ref = "kotlin" }`
  
 `ksp = { id = "com.google.devtools.ksp", version.ref = "ksp" }`
 
 `kotlin-serialization = { id = "org.jetbrains.kotlin.plugin.serialization", version.ref = "kotlin" }`
 
 `room = { id = "androidx.room", version.ref = "room" }`
 
 `org-jetbrains-kotlin-jvm = { id = "org.jetbrains.kotlin.jvm", version.ref = "org-jetbrains-kotlin-jvm" }`
 
 `androidDynamicFeature = { id = "com.android.dynamic-feature", version.ref = "agp" }`
 
 `compose-compiler = { id = "org.jetbrains.kotlin.plugin.compose", version.ref = "kotlin" }`

 <br>

  As well as these gradle dependencies:

  <br>

  `android-gradlePlugin = { group = "com.android.tools.build", name = "gradle", version.ref = "agp" }`
  
  `android-tools-common = { group = "com.android.tools", name = "common", version.ref = "androidTools" }`
 
  `kotlin-gradlePlugin = { group = "org.jetbrains.kotlin", name = "kotlin-gradle-plugin", version.ref = "kotlin" }`
  
  `ksp-gradlePlugin = { group = "com.google.devtools.ksp", name = "com.google.devtools.ksp.gradle.plugin", version.ref = "ksp" }`
  
  `room-gradlePlugin = { group = "androidx.room", name = "room-gradle-plugin", version.ref = "room" }`

<br>

  You will also need to add these to your projects class path by adding them to your project level `build.gradle` file like this: 
  
  ```kotlin
    plugins {
    alias(libs.plugins.android.application) apply false
    alias(libs.plugins.jetbrainsKotlinAndroid) apply false
    alias(libs.plugins.kotlin.serialization) apply false
    alias(libs.plugins.ksp) apply false
    alias(libs.plugins.room) apply false
    alias(libs.plugins.android.library) apply false
    alias(libs.plugins.org.jetbrains.kotlin.jvm) apply false
    alias(libs.plugins.androidDynamicFeature) apply false
    alias(libs.plugins.compose.compiler) apply false
  }
``` 

  
## Step 5:

  To make your project recognize the `build-logic` module as a special build configuration module make sure it doesn't get added to your projects `settings.gradle` file
  
  You might encounter issues when rebuilding your project if you do not add this line to your projects `settings.gradle` file:

  `gradle.startParameter.excludedTaskNames.addAll(listOf(":build-logic:convention:testClasses"))`

  
  
  
  
  
