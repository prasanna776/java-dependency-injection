# 📱 Dependency Injection Without DI Example in Java

 

## 🎯 Objective

Understand what happens when a class creates its own dependency instead of receiving it from outside.

This example demonstrates **Without Dependency Injection (Without DI)**.

---

# 📖 Real-Life Analogy

Imagine a mobile phone manufacturer permanently installs an **Airtel SIM** inside the phone.

- You cannot remove it.
- You cannot insert Jio.
- You cannot insert Idea.
- The mobile is tightly connected to Airtel.

This is called **Tight Coupling**.

---

# 📂 Java Code

```java
package com.example.practice;

// Real-Life Analogy 📱
//
// Without DI:
//
// Mobile manufacturer permanently installs Airtel SIM.
//
// You cannot easily switch.
//

class AirtelSim {
    public void call() {
        System.out.println("Calling using Airtel SIM");
    }
}

class IdeaSim {
    public void call() {
        System.out.println("Calling using Idea SIM");
    }
}

class JioSim {
    public void call() {
        System.out.println("Calling using Jio SIM");
    }
}

class Mobile {

    AirtelSim sim;

    public Mobile() {
        sim = new AirtelSim(); // Mobile creates its own dependency
    }

    void camera() {
        System.out.println("Camera Opened");
    }

    public void makeCall() {
        sim.call();
    }
}

public class PrasannaWithoutDI {

    public static void main(String[] args) {

        Mobile mobile = new Mobile();

        mobile.camera();

        mobile.sim.call();
    }
}
```

---

# 🏗 Class Diagram

```text
            +------------+
            | AirtelSim  |
            +------------+
                   ▲
                   |
                   |
            +------------+
            |   Mobile   |
            +------------+
                   ▲
                   |
                   |
     +--------------------------+
     | PrasannaWithoutDI(Main)   |
     +--------------------------+
```

---

# 🔍 Code Explanation

## Step 1: AirtelSim Class

```java
class AirtelSim {
    public void call() {
        System.out.println("Calling using Airtel SIM");
    }
}
```

This class provides calling functionality.

Output:

```text
Calling using Airtel SIM
```

---

## Step 2: IdeaSim Class

```java
class IdeaSim {
    public void call() {
        System.out.println("Calling using Idea SIM");
    }
}
```

Another SIM provider.

---

## Step 3: JioSim Class

```java
class JioSim {
    public void call() {
        System.out.println("Calling using Jio SIM");
    }
}
```

Another SIM provider.

---

## Step 4: Mobile Class

```java
class Mobile {

    AirtelSim sim;

    public Mobile() {
        sim = new AirtelSim();
    }
}
```

Here the Mobile creates its own Airtel SIM.

This is the main problem.

The Mobile class directly depends on AirtelSim.

```text
Mobile → AirtelSim
```

---

## Step 5: Camera Method

```java
void camera() {
    System.out.println("Camera Opened");
}
```

Displays:

```text
Camera Opened
```

---

## Step 6: Calling Feature

```java
public void makeCall() {
    sim.call();
}
```

Uses Airtel SIM for calling.

---

## Step 7: Main Method

```java
public static void main(String[] args) {

    Mobile mobile = new Mobile();

    mobile.camera();

    mobile.sim.call();
}
```

Execution starts here.

---

# ▶ Program Flow

```text
Main Method
      │
      ▼
Create Mobile Object
      │
      ▼
Mobile Constructor Executes
      │
      ▼
Creates AirtelSim Object
      │
      ▼
Camera Method Executes
      │
      ▼
AirtelSim Call Method Executes
```

---

# 🖥 Output

```text
Camera Opened
Calling using Airtel SIM
```

---

# ❌ Problems Without DI

Because Mobile creates AirtelSim internally:

```java
sim = new AirtelSim();
```

You cannot easily switch to:

```java
new JioSim();
```

or

```java
new IdeaSim();
```

Every time you want another SIM:

1. Open Mobile class
2. Modify source code
3. Recompile application

This violates the **Open/Closed Principle**.

---

# ⚠ Tight Coupling

```text
Mobile
   │
   ▼
AirtelSim
```

Mobile is tightly connected to AirtelSim.

Changing SIM requires changing Mobile code.

---

# ✅ Why Dependency Injection is Better

With Dependency Injection:

```text
Mobile
   ▲
   │
Airtel / Jio / Idea
```

Any SIM can be injected from outside.

Benefits:

- Loose Coupling
- Easy Maintenance
- Easy Testing
- Better Flexibility
- Reusable Code

---

# 📌 Key Interview Question

### Why is this example called "Without DI"?

Because the dependency is created inside the class itself.

```java
sim = new AirtelSim();
```

Instead of receiving the dependency from outside.

---

# 📌 Interview Answer

**Dependency Injection Without DI Example**

In this program, the Mobile class directly creates an AirtelSim object using:

```java
sim = new AirtelSim();
```

Since the dependency is created inside the class, Mobile is tightly coupled with AirtelSim. If we want to use JioSim or IdeaSim, we must modify the Mobile class. Therefore, this is called a **Without Dependency Injection** example.
