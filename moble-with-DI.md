# 📱 Dependency Injection (DI) Example in Java
 

## 🎯 Objective

Understand how **Dependency Injection (DI)** works using a Mobile and SIM Card example.

This example demonstrates **Constructor Injection**, one of the most common forms of Dependency Injection.

---

# 📖 Real-Life Analogy

Imagine you buy a new mobile phone.

The mobile does not come permanently attached to a specific SIM.

You can insert:

- Airtel SIM
- Jio SIM
- Idea SIM
- BSNL SIM
- Vi SIM

The mobile works with any SIM.

This is called **Loose Coupling**.

---

# 📂 Java Code

```java
package com.example.practice;

import java.util.Scanner;

interface Sim
{
    void call();
}

class AirtelSim implements Sim
{
    public void call()
    {
        System.out.println("Calling with Airtel");
    }
}

class JioSim implements Sim
{
    public void call()
    {
        System.out.println("Calling with Jio");
    }
}

class IdeaSim implements Sim
{
    public void call()
    {
        System.out.println("Calling with Idea");
    }
}

class Mobile
{
    Sim sim;

    Mobile(Sim sim)
    {
        this.sim = sim;
    }

    void makeCall()
    {
        sim.call();
    }
}

public class Prasanna
{
    public static void main(String[] args)
    {
        AirtelSim ar = new AirtelSim();

        Mobile m1 = new Mobile(ar);
        m1.makeCall();

        // Mobile m2 = new Mobile(new JioSim());
        // m2.makeCall();

        // Mobile m3 = new Mobile(new IdeaSim());
        // m3.makeCall();
    }
}
```

---

# 🏗 Class Diagram

```text
                  +---------+
                  |   Sim   |
                  +---------+
                       ▲
       ┌───────────────┼───────────────┐
       │               │               │
       ▼               ▼               ▼

 +-----------+   +-----------+   +-----------+
 | AirtelSim |   |  JioSim   |   | IdeaSim   |
 +-----------+   +-----------+   +-----------+

                       ▲
                       │
                       │
                 +-----------+
                 |  Mobile   |
                 +-----------+

                       ▲
                       │
                       │
                 +-----------+
                 |   Main    |
                 +-----------+
```

---

# 🔍 Step-by-Step Explanation

## Step 1: Create Interface

```java
interface Sim
{
    void call();
}
```

The interface defines a common rule.

Every SIM provider must implement:

```java
void call();
```

---

## Step 2: Airtel Implementation

```java
class AirtelSim implements Sim
{
    public void call()
    {
        System.out.println("Calling with Airtel");
    }
}
```

Output:

```text
Calling with Airtel
```

---

## Step 3: Jio Implementation

```java
class JioSim implements Sim
{
    public void call()
    {
        System.out.println("Calling with Jio");
    }
}
```

Output:

```text
Calling with Jio
```

---

## Step 4: Idea Implementation

```java
class IdeaSim implements Sim
{
    public void call()
    {
        System.out.println("Calling with Idea");
    }
}
```

Output:

```text
Calling with Idea
```

---

## Step 5: Mobile Class

```java
class Mobile
{
    Sim sim;

    Mobile(Sim sim)
    {
        this.sim = sim;
    }
}
```

Notice:

```java
Sim sim;
```

Mobile depends on the interface, not a specific SIM company.

This is the key idea of Dependency Injection.

---

## Step 6: Constructor Injection

```java
Mobile(Sim sim)
{
    this.sim = sim;
}
```

The dependency is supplied from outside.

The Mobile class does not create:

```java
new AirtelSim();
```

or

```java
new JioSim();
```

Instead, it receives the dependency.

This is called:

### Constructor Injection

---

## Step 7: Calling Feature

```java
void makeCall()
{
    sim.call();
}
```

The Mobile delegates the calling functionality to whichever SIM is inserted.

---

## Step 8: Main Method

```java
AirtelSim ar = new AirtelSim();

Mobile m1 = new Mobile(ar);

m1.makeCall();
```

Execution Flow:

```text
Create AirtelSim
        │
        ▼
Pass AirtelSim to Mobile
        │
        ▼
Mobile stores dependency
        │
        ▼
makeCall()
        │
        ▼
AirtelSim.call()
```

---

# ▶ Using Jio SIM

```java
Mobile m2 = new Mobile(new JioSim());

m2.makeCall();
```

Output:

```text
Calling with Jio
```

---

# ▶ Using Idea SIM

```java
Mobile m3 = new Mobile(new IdeaSim());

m3.makeCall();
```

Output:

```text
Calling with Idea
```

---

# 🔄 Program Flow

```text
Main Method
      │
      ▼
Create SIM Object
      │
      ▼
Pass SIM to Mobile Constructor
      │
      ▼
Mobile Stores SIM
      │
      ▼
makeCall()
      │
      ▼
SIM call() Method Executes
```

---

# 🖥 Output

For Airtel:

```text
Calling with Airtel
```

For Jio:

```text
Calling with Jio
```

For Idea:

```text
Calling with Idea
```

---

# ✅ Advantages of Dependency Injection

### 1. Loose Coupling

```text
Mobile
   │
   ▼
 Interface (Sim)
```

Mobile does not depend on Airtel, Jio, or Idea directly.

---

### 2. Easy to Change

Switching SIM:

```java
new AirtelSim()
```

to

```java
new JioSim()
```

requires no changes inside Mobile.

---

### 3. Easy Maintenance

Changes in SIM classes do not affect Mobile.

---

### 4. Better Reusability

One Mobile class works with many SIM providers.

---

### 5. Easy Testing

Mock SIM objects can be injected during testing.

---

# ⚖ Without DI vs With DI

| Without DI | With DI |
|------------|----------|
| Mobile creates AirtelSim | SIM provided from outside |
| Tight Coupling | Loose Coupling |
| Hard to change | Easy to change |
| Less flexible | More flexible |
| Difficult testing | Easy testing |

---

# 📌 Why This Is Dependency Injection?

Because the dependency is injected from outside:

```java
Mobile m1 = new Mobile(ar);
```

The Mobile class does not create its dependency.

It receives it through the constructor.

Therefore, this is called:

### Constructor-Based Dependency Injection

---

# 🎤 Interview Answer

In this example, the Mobile class depends on the Sim interface rather than a specific implementation like AirtelSim or JioSim. The dependency is supplied through the constructor:

```java
Mobile(Sim sim)
{
    this.sim = sim;
}
```

Since the object receives its dependency from outside instead of creating it internally, this is called **Dependency Injection (DI)**. Specifically, it is **Constructor Injection**, and it promotes loose coupling, flexibility, maintainability, and testability.
