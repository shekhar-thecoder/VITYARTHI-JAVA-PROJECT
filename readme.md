# Student Management System

A robust and modular Java CLI Application developed for 
CSE2006: Programming in Java. 
The project implements a academic record management workflow which uses oops(object-oriented programming ) principles, dynamic Collections, custom exceptions.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------

# 1. Overview of the Project

In professional and educational institutes including university, schools and academic labs, management of records heavily
depends on physical papers and unvalidated spreadsheets entries.

The **Student Management System** provides a lightweight and persisitat local cli that runs int the terminal.
The project is completed using 6 modular java files which strictly sticks to the core OOP design principles:

- **`myUserfile.java` (Abstract Base Class):** Contains fundamental user attributes (`idofUser`, `nameofUser`, `emailofUser`) and an abstract method named as `displayUserDetails()`.
- **`myStudentFile.java` (Derived Class):** Extends `myUserfile` using inheritance, adds student-specific attributes (`courseofStudent`, `cgpaofStudent`), and overrides `displayUserDetails()` for polymorphic display.
- **`invalidStudentDataException.java` (Custom Exception):** Extends `java.lang.Exception` to guard against duplicate IDs, malformed emails, and invalid CGPAs.
- **`myStudentOperations.java` (Java Interface):** Declares the standard CRUD and File I/O operational contracts.
- **`myStudentManager.java` (Operational Engine):** Implements `myStudentOperations`, managing an in-memory `ArrayList<myStudentFile>` and streaming data to and from disk via `BufferedReader` and `BufferedWriter`.
- **`Main.java` (Interactive CLI Controller):** Executes a user-friendly console menu loop with defensive input handling to prevent runtime crashes.

--------------------------------------------------

# 2. Features

- **1. Student Enrollment (Create):** Adds new student records with real-time field validation and duplicate roll number ID prevention.
- **2. Display All Records (Read):** Iterates over the student registry and formats output using runtime polymorphism.
- **3. Instant Search by Roll ID (Read):** Performs linear scans over in-memory collections for quick profile lookups.
- **4. In-Place Record Modification (Update):** Updates name, email, course, and CGPA for an existing student while checking its validity.
- **5. Remove Record (Delete):** Deletes specific student entries from memory.
- **6. Automated File Persistence (File Input/Output):** 
  - Automatically loads existing records from `students_data.txt` after request.
  - IN case of program exit it automatically writes and saves all records.
- **7. Defensive Error Shielding:** Handles `NumberFormatException` on numerical menu inputs and catches custom `invalidStudentDataException` without crashing the system.

---------------------------------------------------------------------------------------------------------------------------------------------------

# 3. Technologies & Tools Used

| Category | Component / Tool | Application in Project |
| :--- | :--- | :--- |
| **Language** | Java (JDK 8+ / JDK 17 / JDK 21 / JDK 26) | Core Java runtime and complation environment |
| **Collections** | `java.util.ArrayList` | Dynamic in-memory list (`studentRecordsList`) replacing static arrays |
| **Exception Handling** | Custom Checked Exception | `invalidStudentDataException` extending `Exception` |
| **File I/O Streams** | `BufferedReader`, `BufferedWriter`, `FileReader`, `FileWriter` | Stream-based disk persistence to `students_data.txt` |
| **User Input** | `java.util.Scanner` | Console reading and buffer management |
| **Build & Run Tools** | `javac`, `java` | Command-line compilation and execution via PowerShell / CMD |
| **OOP Concepts** | Abstraction, Inheritance, Encapsulation, Polymorphism | Modular class hierarchy (`myUserfile` $\rightarrow$ `myStudentFile`) |



--------------------------------------------------------------------------------------------------------------------------------------------------

# 4. Steps to Install & Run the Project

# Prerequisites
Make sure Java is installed on your system. You can verify this by running:
```powershell
java -version
javac -version
Installation & Execution Steps
1. Clone or Navigate to the Project Directory:
cd "filePath"

2. Verify Project Files: Ensure all of the 6 source files are present in the mentioned folder:

myUserfile.java
myStudentFile.java
invalidStudentDataException.java
myStudentOperations.java
myStudentManager.java
Main.java

3. Compile all Java Files:

javac *.java


4. Launch the CLI Console Application:

java Main

5. Instructions for Testing
Follow these test scenarios in the CLI to verify all functional requirements and defensive constraints:

Test Case 1: Standard Student Insertion & Display
Select Menu Option 1 (Add Student).
Enter valid details:
Roll ID: 101
Name: Aman Sharma
Email: aman@vitstudent.ac.in
Course: B.Tech CSE
CGPA: 8.75
Select Menu Option 2 (View All) to confirm the student profile displays correctly.
Test Case 2: Custom Exception Handling (Invalid Inputs)
Negative Roll ID: Select 1, enter ID -5.
Expected Result: >> Validation Failed: Student ID hamesha positive integer honi chahiye!
Out-of-Range CGPA: Select 1, enter ID 103, Name Rahul, Email rahul@test.com, Course B.Tech, CGPA 11.5.
Expected Result: >> Validation Failed: CGPA 0.0 se 10.0 ke beech hona chahiye!
Malformed Email: Select 1, enter Email rahulgmailcom (missing @ or .).
Expected Result: >> Validation Failed: Invalid email address! Kripya proper email address dalein.
Test Case 3: Duplicate Primary Key Detection
Select Option 1 and enter Roll ID 101 (already added in Test Case 1).
Expected Result: >> Validation Failed: Student ID 101 pehle se system me exist karti hai!
Test Case 4: Search & In-Place Update
Select Option 3, enter ID 101 
→
→ verifies student profile is displayed.
Select Option 4, enter ID 101, and provide updated details (e.g. new CGPA 9.10).
Select Option 2 
→
→ verifies modified data is active in memory.
Test Case 5: File Persistence & Cold-Start Verification
Select Option 7 (Exit). The system automatically saves records to students_data.txt.
Inspect the file in notepad or terminal:
powershell


type students_data.txt
Relaunch the program (java Main).
Notice the startup log: >> File I/O: File se records successfully load ho gaye.
Select Option 2 
→
→ verifies all previous data was restored into memory without data loss.
