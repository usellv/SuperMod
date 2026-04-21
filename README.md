.github/workflows/build.yml
{
  "schemaVersion": 1,
  "id": "super_mod",
  "version": "1.0.0",
  "name": "Super Mod",
  "description": "Visuals by usellv",
  "authors": [ "usellv" ],
  "contact": {},
  "license": "MIT",
  "icon": "assets/super_mod/icon.png",
  "environment": "*",
  "entrypoints": {
    "main": [ "com.example.SuperMod" ],
    "client": [ "com.example.SuperMod" ]
  },
  "depends": {
    "fabricloader": ">=0.15.0",
    "minecraft": "1.21",
    "java": ">=21",
    "fabric-api": "*"
  }
}
name: Build Mod
on:
  push:
    branches: [ "main", "master" ]
  workflow_dispatch: # Позволяет запустить вручную кнопкой

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Set up JDK 21
        uses: actions/setup-java@v4
        with:
          java-version: '21'
          distribution: 'temurin'
      - name: Make gradlew executable
        run: chmod +x gradlew
      - name: Build with Gradle
        run: ./gradlew build
      - name: Upload Artifact
        uses: actions/upload-artifact@v4
        with:
          name: SuperMod-JAR
          path: build/libs/*.jar
