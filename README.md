C1. Create a maven projects with all dependencies required for the application
in CI/CD pipeline.
To run CI/CD pipeline in GitHub
I. Install required tools
II. Install Java (JDK 11 or higher)
o Download from Oracle JDK or OpenJDK
o Set environment variable:
▪ JAVA_HOME = C:\Program Files\Java\jdk-XX
▪ Add %JAVA_HOME%\bin to PATH

III. Install Apache Maven
o Download and extract
o Set:
▪ MAVEN_HOME = C:\apache-maven
▪ Add %MAVEN_HOME%\bin to PATH

IV. Install Visual Studio Code
V. Install VS Code Extensions:
o Extension Pack for Java
o Maven for Java
o Debugger for Java
II. Create Maven Project in VS Code

Open VS Code
Press Ctrl + Shift + P
Type: Java: Create Java Project
Select Maven create from archetype
Choose:
Archetype → maven-archetype-quickstart
Enter details:
Group Id: com.example
Artifact Id: demo (Give any name)
Choose folder → Project will be created automatically

Push the folder to git repository
III. For CI/CD Pipeline (GitHub Actions)

In the local folder
Create a folder by name .github and inside that create worflows folder

and in that create a file maven.yml

Structure:
Localfoldername
-demo
-.github/workflows/maven.yml

Push this to Github repo

IV. Check the actions tab in github for the CI working

maven.yml
name: Java CI/CD Pipeline
on:
push:
branches: [ "main" ]
jobs:
build:
runs-on: windows-latest
env:
FORCE_JAVASCRIPT_ACTIONS_TO_NODE24: true
steps:
- uses: actions/checkout@v4
- uses: actions/setup-java@v4
with:
distribution: 'temurin'
java-version: '11'
- name: Build using Maven
run: mvn clean install
working-directory: demo
