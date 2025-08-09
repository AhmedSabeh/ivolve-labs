# Lab 10: Building and Packaging Java Applications with Maven
-    Install maven.
-    Clone source code https:// github.com/Ibrahim Adel15/build2.git
-    Run Unit test.
-    Build App [ generate a rtifact in target / hello ivolve 1.0 SNAPSHOT.jar
-    Run App.
-    Verify App is working
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
You should see the expected output in the terminal (Hello Ivolve Trainee).
<img width="1272" height="94" alt="Screenshot (146)" src="https://github.com/user-attachments/assets/650e2b9e-4d6f-4868-bac8-868280efa73f" />

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
