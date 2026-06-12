# Dependency Injection (DI) Example in Java

## Program Name

Notification Service using Constructor Dependency Injection

---

## Objective

To understand Dependency Injection (DI) by injecting different notification services into a client class.

---

## Source Code

```java
package com.example.practice;

// Common Interface
interface NotificationService {
    void send(String message);
}

// Email Service
class EmailService implements NotificationService {

    @Override
    public void send(String message) {
        System.out.println("Email Sent: " + message);
    }
}

// SMS Service
class SmsService implements NotificationService {

    @Override
    public void send(String message) {
        System.out.println("SMS Sent: " + message);
    }
}

// WhatsApp Service
class WhatsAppService implements NotificationService {

    @Override
    public void send(String message) {
        System.out.println("WhatsApp Sent: " + message);
    }
}

// Client Class
class NotificationManager {

    private NotificationService service;

    // Constructor Injection
    public NotificationManager(NotificationService service) {
        this.service = service;
    }

    public void notifyUser(String message) {
        service.send(message);
    }
}

// Main Class
public class Prasanna {

    public static void main(String[] args) {

        // Inject Email Service
        NotificationService email = new EmailService();

        NotificationManager manager =
                new NotificationManager(email);

        manager.notifyUser("Welcome User");
    }
}
```

---

## Output

```text
Email Sent: Welcome User
```

---

## Class Explanation

### 1. NotificationService Interface

```java
interface NotificationService {
    void send(String message);
}
```

This is the common contract for all notification services.

---

### 2. EmailService Class

```java
class EmailService implements NotificationService
```

Sends notifications through Email.

---

### 3. SmsService Class

```java
class SmsService implements NotificationService
```

Sends notifications through SMS.

---

### 4. WhatsAppService Class

```java
class WhatsAppService implements NotificationService
```

Sends notifications through WhatsApp.

---

### 5. NotificationManager Class

```java
public NotificationManager(NotificationService service)
```

Receives the dependency through the constructor.

This is called Constructor Injection.

---

### 6. Prasanna Class

```java
public class Prasanna
```

Contains the main method and starts the program execution.

---

## Dependency Injection Flow

```text
EmailService
      │
      ▼
NotificationManager
      │
      ▼
notifyUser("Welcome User")
      │
      ▼
Email Sent: Welcome User
```

---

## Advantages of Dependency Injection

1. Loose Coupling
2. Easy Maintenance
3. Better Code Reusability
4. Easy Testing
5. Easy to Switch Services

Example:

```java
NotificationService service = new SmsService();
```

or

```java
NotificationService service = new WhatsAppService();
```

No changes are required in NotificationManager.

---

## Conclusion

Dependency Injection allows dependencies to be provided from outside the class instead of creating them inside the class. This makes the application flexible, maintainable, and scalable.
