# Lab 10: Building and Packaging Java Applications with Maven

## Objective
In this lab, we build and package a Java application using **Maven**, run unit tests, generate the artifact, and verify the application is working.

---

## Steps

### 1. Install Maven
Follow the official Maven installation guide:  
[https://maven.apache.org/install.html](https://maven.apache.org/install.html)

Verify installation:
```
mvn -v
```
### 2. Clone the Source Code
```
git clone https://github.com/IbrahimAdel15/build2.git
cd build2
```
### 3. Run Unit Tests
```
mvn test
```
### 4. Build the Application
```
mvn package
```
This will generate the .jar file inside:
```
target/hello-ivolve-1.0-SNAPSHOT.jar
```
### 5. Run the Application
```
java -jar target/hello-ivolve-1.0-SNAPSHOT.jar
```
### 6. Verify Application Output
You should see the expected output in the terminal (e.g., application greeting message).

Directory Structure
```
build2/
├── pom.xml
├── src/
└── target/
    └── hello-ivolve-1.0-SNAPSHOT.jar
```
Notes
-  If you face permission issues, ensure Java is installed and added to PATH.

-  To clean previous builds:
```
mvn clean
```
