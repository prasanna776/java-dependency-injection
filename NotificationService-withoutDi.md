# 📧 Notification Service Without Dependency Injection (Without DI)

 

## 🎯 Objective

Understand how a Notification Service works **without Dependency Injection (DI)**.

In this example, the Notification Service is permanently connected to the Email Service.

---

# 📖 Real-Life Analogy

Imagine a company application that sends notifications.

Currently, it can send notifications only through Email.

```text
Application
     │
     ▼
Email Service
```

If tomorrow the company wants to use:

- SMS
- WhatsApp
- Push Notifications

the NotificationService code must be modified.

This is called **Tight Coupling**.

---

# 📂 Java Code

```java
package com.example.practice;

// Email Service
class EmailService {

    public void send(String message) {
        System.out.println("Email Sent: " + message);
    }
}

// SMS Service
class SmsService {

    public void send(String message) {
        System.out.println("SMS Sent: " + message);
    }
}

// WhatsApp Service
class WhatsAppService {

    public void send(String message) {
        System.out.println("WhatsApp Sent: " + message);
    }
}

// Notification Service
class NotificationService {

    EmailService email;

    public NotificationService() {

        email = new EmailService(); // Dependency created inside
    }

    public void notifyUser(String message) {

        email.send(message);
    }
}

public class NotificationServicewithoutDi {

    public static void main(String[] args) {

        NotificationService service =
                new NotificationService();

        service.notifyUser("Welcome User");
    }
}
```

---

# 🏗 Class Diagram

```text
          +----------------+
          | EmailService   |
          +----------------+
                  ▲
                  │
                  │
          +----------------------+
          | NotificationService  |
          +----------------------+
                  ▲
                  │
                  │
          +----------------------+
          |         Main         |
          +----------------------+
```

---

# 🔍 Step-by-Step Explanation

## Step 1: Email Service

```java
class EmailService {

    public void send(String message) {
        System.out.println("Email Sent: " + message);
    }
}
```

Responsible for sending emails.

Example Output:

```text
Email Sent: Welcome User
```

---

## Step 2: SMS Service

```java
class SmsService {

    public void send(String message) {
        System.out.println("SMS Sent: " + message);
    }
}
```

Can send SMS messages.

Currently not used.

---

## Step 3: WhatsApp Service

```java
class WhatsAppService {

    public void send(String message) {
        System.out.println("WhatsApp Sent: " + message);
    }
}
```

Can send WhatsApp messages.

Currently not used.

---

## Step 4: Notification Service

```java
class NotificationService {

    EmailService email;
}
```

NotificationService depends directly on EmailService.

---

## Step 5: Dependency Creation

```java
public NotificationService() {

    email = new EmailService();
}
```

Important Point:

NotificationService creates its own dependency.

```text
NotificationService
        │
        ▼
new EmailService()
```

This is why it is called:

### Without Dependency Injection

---

## Step 6: Sending Notification

```java
public void notifyUser(String message) {

    email.send(message);
}
```

Delegates notification to EmailService.

---

## Step 7: Main Method

```java
NotificationService service =
        new NotificationService();

service.notifyUser("Welcome User");
```

Execution starts here.

---

# ▶ Program Flow

```text
Main Method
      │
      ▼
Create NotificationService
      │
      ▼
Constructor Executes
      │
      ▼
Creates EmailService Object
      │
      ▼
notifyUser()
      │
      ▼
email.send()
      │
      ▼
Message Sent
```

---

# 🖥 Output

```text
Email Sent: Welcome User
```

---

# ❌ Problem 1: Tight Coupling

Current dependency:

```java
EmailService email;
```

NotificationService is directly connected to EmailService.

```text
NotificationService
         │
         ▼
    EmailService
```

---

# ❌ Problem 2: Hard to Change

Suppose tomorrow you want SMS notifications.

Current code:

```java
email = new EmailService();
```

Must be changed to:

```java
sms = new SmsService();
```

Source code modification is required.

---

# ❌ Problem 3: Difficult Maintenance

Every time a new notification channel is added:

- SMS
- WhatsApp
- Telegram
- Push Notification

NotificationService must be modified.

---

# ❌ Problem 4: Difficult Testing

Testing becomes harder because EmailService is hardcoded.

Mock objects cannot be injected easily.

---

# ⚠ Why This Is Called Without DI

Because the dependency is created inside the class itself.

```java
email = new EmailService();
```

Instead of receiving it from outside.

---

# Without DI Structure

```text
NotificationService
        │
        ▼
new EmailService()
```

The class controls its dependency.

---

# ✅ Better Approach (Using DI)

Instead of:

```java
email = new EmailService();
```

We should inject the dependency:

```java
NotificationService service =
        new NotificationService(new EmailService());
```

or

```java
NotificationService service =
        new NotificationService(new SmsService());
```

or

```java
NotificationService service =
        new NotificationService(new WhatsAppService());
```

This provides flexibility.

---

# ⚖ Without DI vs With DI

| Without DI | With DI |
|------------|----------|
| Dependency created inside class | Dependency provided from outside |
| Tight Coupling | Loose Coupling |
| Hard to change | Easy to change |
| Difficult testing | Easy testing |
| Less flexible | More flexible |

---

# 🎤 Interview Question

### Why is this example called Without Dependency Injection?

Because NotificationService directly creates its dependency using:

```java
email = new EmailService();
```

The dependency is not supplied from outside.

Therefore, this is a **Without Dependency Injection (Without DI)** example.

---

# 🎤 Interview Answer

In this program, NotificationService directly creates an EmailService object inside its constructor:

```java
email = new EmailService();
```

Since the dependency is created internally, NotificationService becomes tightly coupled with EmailService. If we want to switch to SmsService or WhatsAppService, we must modify the source code. Therefore, this example represents **Without Dependency Injection (Without DI)**.
