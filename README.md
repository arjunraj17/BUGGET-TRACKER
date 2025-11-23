# BUGGET-TRACKER
Budget Tracker Model: BudgetEntry.java

This file provides the technical documentation for the core data model (BudgetEntry) used within the budgettracker.model package of the Budget Tracker application.

1. Technical Overview

The BudgetEntry class is an immutable model object (a POJO - Plain Old Java Object) designed to encapsulate the details of a single financial transaction (Income or Expense).

It adheres to the principle of encapsulation by keeping all its fields private and exposing them only through public getter methods. Since there are no setter methods, once a BudgetEntry object is created, its data cannot be modified, which enhances data integrity.

1.1. Core Class Structure

Element                Type                     Purpose

description            String                   Textual description of the transaction (e.g., "Monthly Salary," "Electric Bill").

amount                 double                   The monetary value of the transaction.

date                   LocalDate                The date of the transaction (from java.time package).

type                   String                   The category of the transaction, typically "Income" or "Expense".

1.2. Key Methods

Method                      Return Type                         Description

BudgetEntry(...)            Constructor                         Initializes a new entry with all required data fields.

getAmount()                   double                            Retrieves the numeric value of the transaction.

getDate()                    LocalDate                          Retrieves the transaction date.

toString()                     String                          Provides a formatted string representation of the entry, ensuring 
                                                               the amount is displayed with two decimal places.

2. Setup and Integration

This model is written in Java and requires a standard Java Development Kit (JDK) environment to compile and run.

2.1. Prerequisites

Java Development Kit (JDK): Version 8 or newer is recommended.

Build Tool (Optional but Recommended): Maven or Gradle.

2.2. Project Structure

If integrating this model into a larger project, ensure the file is placed within the correct package structure:

src/
└── budgettracker/
    └── model/
        └── BudgetEntry.java


2.3. Compilation

To compile the class manually from the root of the src directory:

javac budgettracker/model/BudgetEntry.java


3. Code Details and Usage

3.1. Code Snippet

The class source code (located at budgettracker/model/BudgetEntry.java):

package budgettracker.model;

import java.time.LocalDate;

public class BudgetEntry {
    private String description;
    private double amount;
    private LocalDate date;
    private String type;

    // Constructor: Requires all four parameters to create an instance
    public BudgetEntry(String description, double amount, String type, LocalDate date) {
        this.description = description;
        this.amount = amount;
        this.type = type;
        this.date = date;
    }

    // Getters for immutable access
    public String getDescription() {
        return description;
    }

    public double getAmount() {
        return amount;
    }

    public LocalDate getDate() {
        return date;
    }

    public String getType() {
        return type;
    }

    // Overridden toString for clean output
    @Override
    public String toString() {
        return String.format("[%s] %s: %.2f (on %s)", 
                            type, description, amount, date.toString());
    }
}


3.2. Example Usage

This example demonstrates how to create instances of BudgetEntry and use the getter methods:

import budgettracker.model.BudgetEntry;
import java.time.LocalDate;

public class BudgetTrackerDemo {
    public static void main(String[] args) {
        // 1. Create an Income entry
        BudgetEntry income = new BudgetEntry(
            "Monthly Salary", 
            4500.00, 
            "Income", 
            LocalDate.of(2025, 11, 1)
        );

        // 2. Create an Expense entry
        BudgetEntry expense = new BudgetEntry(
            "Groceries", 
            85.50, 
            "Expense", 
            LocalDate.now()
        );

        // 3. Accessing data using getters
        System.out.println("--- Transaction Details ---");
        System.out.println("Description: " + expense.getDescription()); // Output: Groceries
        System.out.println("Amount: $" + expense.getAmount());         // Output: $85.5
        System.out.println("Type: " + income.getType());             // Output: Income
        
        // 4. Using the formatted toString()
        System.out.println("\n--- Formatted Output ---");
        System.out.println(income.toString());   // Output: [Income] Monthly Salary: 4500.00 (on 2025-11-01)
        System.out.println(expense.toString());  // Output: [Expense] Groceries: 85.50 (on 2025-11-23)
    }
}
