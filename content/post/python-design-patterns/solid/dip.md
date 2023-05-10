---
title: "Dependency Inversion Principle"
date: 2023-05-09T16:37:02+05:30
draft: False
---

The Dependency Inversion Principle (DIP) is a principle in object-oriented design that states that high-level modules should not depend on low-level modules. Instead, both should depend on abstractions. It promotes decoupling and flexibility in the codebase



## Example - 1 [ Violation ]

```
class PaymentProcessor:
    def process_payment(self, amount):
        print(f"Processing payment of ${amount}")

class PaymentService:
    def __init__(self):
        self.payment_processor = PaymentProcessor()

    def perform_payment(self, amount):
        self.payment_processor.process_payment(amount)

# Usage
payment_service = PaymentService()
payment_service.perform_payment(100)  # Output: "Processing payment of $100"

```

`PaymentService` class directory depends on the `PaymentProcessor`, creating an instance insite its consyructor there by, establishing a strong coupling between the two classes, violating `Dependency Inversion Principle`

## Example - 2 [ Fixing ]

```
from abc import ABC, abstractmethod

class PaymentProcessor(ABC):
    @abstractmethod
    def process_payment(self, amount):
        pass

class CreditCardPaymentProcessor(PaymentProcessor):
    def process_payment(self, amount):
        print(f"processing credit card payment {amount}")

class PaypalPaymentProcessor(PaymentProcessor):
    def process_payment(self, amount):
        print(f"processing paypal payment {amount}")

class PaymentServices:
    def __init__(self, payment_processor):
        self.payment_processor=payment_processor

    def perform_payment(self, amount):
        self.payment_processor.process_payment(amount)

creditcard_processor=CreditCardPaymentProcessor()
paypal_processor=PaypalPaymentProcessor()

payment_service=PaymentServices(creditcard_processor)
payment_service.perform_payment(100)

payment_service=PaymentServices(paypal_processor)
payment_service.perform_payment(200)
```

the `PaymentProcessor` abstract class, which serves as the abstraction that both the `PaymentService` and the concrete payment processors (`CreditCardPaymentProcessor and PayPalPaymentProcessor`) depend on

By introducing the abstraction and decoupling the high-level and low-level modules, we adhere to the Dependency Inversion Principle, promoting flexibility, maintainability, and easier integration of new payment processors in the future