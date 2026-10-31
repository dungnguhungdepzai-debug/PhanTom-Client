name: Build Phantom Client

on:
  push:
    branches: [ main, master ]
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Extract source
        run: |
          unzip phantom-client-fixed.zip
          cp -r phantom-client/* .
          rm -f build.gradle settings.gradle
          sed -i 's/gradle-8.10/gradle-8.14/g' gradle/wrapper/gradle-wrapper.properties

      - name: Setup Java 25
        uses: actions/setup-java@v5
        with:
          distribution: 'oracle'
          java-version: '25'
          cache: 'gradle'

      - name: Build
        run: |
          chmod +x gradlew
          ./gradlew build --no-daemon

      - name: Upload JAR
        uses: actions/upload-artifact@v4
        with:
          name: phantom-client-jar
          path: build/libs/phantom-client-1.0.0.jar
          retention-days: 30
