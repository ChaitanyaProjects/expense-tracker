# Expense Sharing Application (Splitwise-like)

---

## 1. Overview of the Design

The UML diagram represents the **backend design** of a simplified expense-sharing application similar to Splitwise.

The design focuses on:

- Group-based expense sharing
- Multiple expense split types
- Accurate balance tracking
- Simplification of debts

The system is **modular, extensible, and easy to maintain**, following good object-oriented design principles.

---

## 2. Core Components

### 2.1 Splitwise (Singleton)

The `Splitwise` class acts as the **central controller** of the system.

**Responsibilities:**

- Maintains records of all users, groups, and expenses
- Acts as the single entry point for adding expenses and settling payments

**Why Singleton?**

- Ensures only one instance manages the entire system state
- Prevents duplication of users or groups

---

### 2.2 User

The `User` class represents an individual user of the application.

**Key Attributes:**

- `userId`, `name`, `email`
- `balances`: stores how much the user owes to or is owed by other users

**Responsibilities:**

- Track net balances with other users
- Update balances after expenses or settlements

Each user can clearly see:

- How much they owe
- How much others owe them

---

### 2.3 Group

The `Group` class represents a collection of users sharing expenses.

**Key Attributes:**

- Group details (ID, name)
- Members of the group
- Group expenses
- Group-level balances

**Responsibilities:**

- Add or remove members
- Add expenses to the group
- Update balances for group members
- Settle payments between users
- Simplify group debts

The `Group` class contains the **main business logic** of the application.

---

### 2.4 Expense

The `Expense` class models a single expense entry.

**Key Attributes:**

- Expense ID, description, amount
- User who paid the expense
- List of splits
- Associated group ID

Each expense knows **who paid** and **how the amount is split** among participants.

---

### 2.5 Split

The `Split` class represents an individual user’s share of an expense.

**Attributes:**

- User ID
- Amount owed by that user

This allows precise tracking of how much each participant owes for an expense.

---

## 3. Expense Splitting Logic (Strategy Pattern)

### 3.1 SplitStrategy (Abstract)

The `SplitStrategy` defines a common interface for all split calculations.

**Method:**

- `calculateSplit(...)`

---

### 3.2 Concrete Split Strategies

The design supports multiple split types using separate classes:

- `EqualSplit`
- `ExactSplit`
- `PercentageSplit`

Each class implements its own logic for calculating user shares.

**Benefits:**

- Clean separation of responsibilities
- Easy to add new split types in the future
- Avoids complex conditional logic

---

### 3.3 SplitFactory

The `SplitFactory` returns the appropriate split strategy based on the selected `SplitType`.

This hides object creation logic and improves maintainability.

---

## 4. Balance Simplification

### DebtSimplifier

The `DebtSimplifier` class is responsible for **simplifying balances**.

**Purpose:**

- Reduce the number of transactions required to settle dues
- Convert indirect debts into direct ones

---

## 5. Balance Tracking

Balances are stored as **net pairwise balances** between users.

- Positive balance → others owe the user
- Negative balance → user owes others

This ensures:

- Clear visibility of dues
- Minimal transactions during settlement

---

|  |  |
| --- | --- |
|  |  |
|  |  |
|  |  |
|  |  |

---

##
