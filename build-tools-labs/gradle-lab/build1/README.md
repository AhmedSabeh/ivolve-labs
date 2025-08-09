# Lab 9: Building and Packaging Java Applications with Gradle
-    Install Gradle
-    Clone source code https:// github.com/Ibrahim Adel15/build1.git
-    Run Unit test.
-    Build App [ generate artifact in build/libs/ivolve app.jar
-    Run App.
-    Verify App is working.
---

## Steps

### 1. Install Gradle
Follow the official Gradle installation guide:  
[https://gradle.org/install/](https://gradle.org/install/)

Verify installation:
```
gradle -v
```
### 2. Clone the Source Code
```
git clone https://github.com/IbrahimAdel15/build1.git
cd build1
```
### 3. Run Unit Tests
```
gradle test
```
### 4. Build the Application
```
gradle build
```
This will generate the .jar file inside:
```
build/libs/ivolve-app.jar
```
### 5. Run the Application
```
java -jar build/libs/ivolve-app.jar
```
### 6. Verify Application Output
You should see the expected output in the terminal (Hello iVolve Trainee).
<img width="1366" height="99" alt="Screenshot (144)" src="https://github.com/user-attachments/assets/17b4c75a-9459-4382-b8e0-74660581d9a6" />

Directory Structure
```
build1/
├── build.gradle
├── settings.gradle
├── src/
└── build/
    └── libs/
        └── ivolve-app.jar
```
Notes
-  If you face permission issues, ensure Java is installed and added to PATH.

-  To clean previous builds:
```
gradle clean
```
