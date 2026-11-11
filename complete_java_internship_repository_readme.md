# Java Software Engineering Internship - Complete Track & Capstone

Welcome to the central repository for the **Java Software Engineering Internship** at **Codomax Digital Solutions**. This repository contains the complete practical code, notes, modules, and projects built throughout the 30-day program.

---

## 📌 Repository Overview

* **Developer:** VALARMATHI M
* **Program:** Java Software Engineering Internship
* **Organization:** Codomax Digital Solutions
* **Tech Stack:** Java (JDK 17/21), MySQL, JDBC, Spring Boot, REST APIs, Git/GitHub, VS Code / IntelliJ IDEA

---

## 📂 Module Breakdown & Core Deliverables

---

### 🔹 Module 01: Java Fundamentals (Day 1 – Day 5)

#### Key Topics:
* Java Runtime Architecture (JDK, JRE, JVM, and compilation lifecycles)
* Variables, primitives, dynamic I/O using `Scanner`, conditional statements, and loops
* Single & multidimensional arrays, String immutability, and basic logic-building exercises
* Local IDE environment setup (`JAVA_HOME` configuration)

#### Code Implementation (Logic Building & Basic Syntax):
```java
import java.util.Scanner;

public class JavaBasicsAndLogic {
    public static void main(String[] args) {
        // Scanner I/O Example
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter a number to check parity: ");
        int num = scanner.nextInt();
        
        if (num % 2 == 0) {
            System.out.println(num + " is EVEN");
        } else {
            System.out.println(num + " is ODD");
        }
        
        // Array Traversal & Logic
        int[] numbers = {10, 25, 45, 60, 85};
        int sum = 0;
        for (int n : numbers) {
            sum += n;
        }
        System.out.println("Array Sum: " + sum);

        // String Palindrome Check
        String text = "madam";
        String reversed = new StringBuilder(text).reverse().toString();
        System.out.println("Is '" + text + "' a Palindrome? " + text.equalsIgnoreCase(reversed));

        scanner.close();
    }
}
```

---

### 🔹 Module 02: Methods, Collections & Exceptions (Day 6 – Day 10)

#### Key Topics:
* Java methods, pass-by-value semantics, method overloading, and block/local scope
* Collections Framework: `ArrayList`, `HashSet`, and `HashMap`
* Exception handling (`try-catch-finally`, `throw`, `throws`) and File I/O operations (`FileWriter`, `BufferedReader`)
* **Project:** Student Management System CLI

#### Code Implementation (Student Management System):
```java
import java.io.*;
import java.util.ArrayList;
import java.util.HashMap;

class Student {
    private int id;
    private String name;

    public Student(int id, String name) {
        this.id = id;
        this.name = name;
    }

    public int getId() { return id; }
    public String getName() { return name; }
}

public class StudentManagementSystem {
    private static ArrayList<Student> studentList = new ArrayList<>();
    private static HashMap<Integer, Student> studentMap = new HashMap<>();

    public static void addStudent(int id, String name) {
        Student s = new Student(id, name);
        studentList.add(s);
        studentMap.put(id, s);
        System.out.println("Added: " + name);
    }

    public static void main(String[] args) {
        try {
            addStudent(101, "Valarmathi M");
            addStudent(102, "Anand R");

            System.out.println("\n--- Registered Students ---");
            for (Student s : studentList) {
                System.out.println("ID: " + s.getId() + " | Name: " + s.getName());
            }

            // File Persist Example
            FileWriter writer = new FileWriter("students.txt");
            for (Student s : studentList) {
                writer.write(s.getId() + "," + s.getName() + "\n");
            }
            writer.close();
            System.out.println("\nRecords saved to students.txt successfully.");

        } catch (IOException e) {
            System.err.println("File I/O Error: " + e.getMessage());
        }
    }
}
```

---

### 🔹 Module 03: Object-Oriented Programming (Day 11 – Day 15)

#### Key Topics:
* Encapsulation, inheritance, constructors, and access modifiers (`private`, `public`, `protected`)
* Abstraction (abstract classes & interfaces) and polymorphism (method overriding vs overloading)
* **Project:** Java Banking Management System

#### Code Implementation (Banking System):
```java
interface BankOperations {
    void deposit(double amount);
    void withdraw(double amount);
    void checkBalance();
}

abstract class Account {
    protected String accountNumber;
    protected double balance;

    public Account(String accountNumber, double initialBalance) {
        this.accountNumber = accountNumber;
        this.balance = initialBalance;
    }
}

class SavingsAccount extends Account implements BankOperations {
    public SavingsAccount(String accountNumber, double initialBalance) {
        super(accountNumber, initialBalance);
    }

    @Override
    public void deposit(double amount) {
        balance += amount;
        System.out.println("Deposited $" + amount + ". New Balance: $" + balance);
    }

    @Override
    public void withdraw(double amount) {
        if (amount <= balance) {
            balance -= amount;
            System.out.println("Withdrew $" + amount + ". Remaining Balance: $" + balance);
        } else {
            System.out.println("Insufficient funds!");
        }
    }

    @Override
    public void checkBalance() {
        System.out.println("Account: " + accountNumber + " | Balance: $" + balance);
    }
}

public class MainBank {
    public static void main(String[] args) {
        SavingsAccount acc = new SavingsAccount("SAV-9876", 1000.00);
        acc.checkBalance();
        acc.deposit(500.00);
        acc.withdraw(300.00);
    }
}
```

---

### 🔹 Module 04: Java Database & JDBC (Day 16 – Day 20)

#### Key Topics:
* Relational database concepts, SQL fundamentals, schema normalization, and MySQL setup
* JDBC Architecture: Driver loading, `DriverManager`, `Connection`, `PreparedStatement`, and `ResultSet`
* Executing parameterized CRUD transactions safely to prevent SQL injection
* **Project:** Java + MySQL CLI Management System

#### Code Implementation (JDBC Database Service):
```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;

public class DatabaseService {
    private static final String URL = "jdbc:mysql://localhost:3306/internship_db";
    private static final String USER = "root";
    private static final String PASSWORD = "password";

    public static Connection getConnection() throws Exception {
        return DriverManager.getConnection(URL, USER, PASSWORD);
    }

    public static void createRecord(int id, String name, String email) {
        String sql = "INSERT INTO users (id, name, email) VALUES (?, ?, ?)";
        try (Connection conn = getConnection(); PreparedStatement pstmt = conn.prepareStatement(sql)) {
            pstmt.setInt(1, id);
            pstmt.setString(2, name);
            pstmt.setString(3, email);
            pstmt.executeUpdate();
            System.out.println("Database record inserted successfully.");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    public static void main(String[] args) {
        createRecord(1, "Valarmathi", "valarmathi@example.com");
    }
}
```

---

### 🔹 Module 05: Java Web & REST API Development (Day 21 – Day 25)

#### Key Topics:
* HTTP protocols, status codes, and Spring Boot web services initialization
* Layered MVC Architecture: Controllers (`@RestController`), Services (`@Service`), Repositories (`@Repository`)
* Spring Data JPA / Hibernate database mapping and custom REST exception handlers
* API verification using Postman

#### Code Implementation (Spring Boot Controller):
```java
package com.codomax.demo.controller;

import org.springframework.web.bind.annotation.*;
import java.util.HashMap;
import java.util.Map;

@RestController
@RequestMapping("/api/v1/users")
public class UserController {

    @GetMapping("/{id}")
    public Map<String, Object> getUserById(@PathVariable Long id) {
        Map<String, Object> response = new HashMap<>();
        response.put("id", id);
        response.put("name", "Valarmathi M");
        response.put("role", "Java Backend Developer");
        response.put("status", "Active");
        return response;
    }

    @PostMapping
    public Map<String, String> createUser(@RequestBody Map<String, String> payload) {
        Map<String, String> response = new HashMap<>();
        response.put("message", "User created successfully!");
        response.put("userName", payload.get("name"));
        return response;
    }
}
```

---

### 🔹 Module 06: Java Capstone Project (Day 26 – Day 30)

#### Project Overview:
Full-stack enterprise backend application implementing a multi-tiered architecture with Spring Boot, JPA, MySQL, and secure endpoint routing.

#### Key Features Built:
1. **Multi-tiered Architecture:** Decoupled Controller, Service, and Repository layers.
2. **Relational Database Schema:** Normalized tables with `@OneToMany` and `@ManyToOne` entity mappings.
3. **Data Validation & Error Handling:** Intercepting validation failures using `@ControllerAdvice`.
4. **API Testing & Documentation:** Tested endpoints via Postman and documented schemas using Swagger/OpenAPI.

---

## 🛠️ How to Clone & Run Locally

```bash
# 1. Clone the repository
git clone https://github.com/<YOUR_USERNAME>/<YOUR_REPOSITORY_NAME>.git

# 2. Navigate to project root
cd <YOUR_REPOSITORY_NAME>

# 3. Compile standard Java files
javac StudentManagementSystem.java
java StudentManagementSystem

# 4. Run Spring Boot application (if using Maven wrapper)
./mvnw spring-boot:run
```

---

## 📜 Recognition & Certification
* **MSME Govt. Verified Credential:** Completed all 6 modules and evaluations.
* **Organization:** Codomax Digital Solutions