---
title: "Adpater"
date: 2023-06-06T16:24:24+05:30
draft: False
---

The Adapter pattern is a structural design pattern that allows objects with incompatible interfaces to work together. It acts as a bridge between two incompatible interfaces, converting the interface of one class into another interface that the client expects

```
class PaymentGateway:
    def process_payment(self, amount):
        pass

class BankPaymentGateway:
    def make_payment(self, amount):
        print(f"Making payment of ${amount} via Bank Payment Gateway")

class PayPalPaymentGateway:
    def send_payment(self, amount):
        print(f"Sending payment of ${amount} via PayPal Payment Gateway")

class PaymentGatewayAdapter(PaymentGateway):
    def __init__(self, payment_gateway):
        self.payment_gateway = payment_gateway

    def process_payment(self, amount):
        if isinstance(self.payment_gateway, BankPaymentGateway):
            self.payment_gateway.make_payment(amount)
        elif isinstance(self.payment_gateway, PayPalPaymentGateway):
            self.payment_gateway.send_payment(amount)

# Usage
bank_gateway = BankPaymentGateway()
paypal_gateway = PayPalPaymentGateway()

adapter1 = PaymentGatewayAdapter(bank_gateway)
adapter2 = PaymentGatewayAdapter(paypal_gateway)

adapter1.process_payment(100)  # Output: "Making payment of $100 via Bank Payment Gateway"
adapter2.process_payment(200)  # Output: "Sending payment of $200 via PayPal Payment Gateway"

```

In this example, we have a common PaymentGateway interface that represents the desired interface for processing payments. The PaymentGateway class defines the process_payment() method.

We also have two existing payment gateway classes: BankPaymentGateway and PayPalPaymentGateway. These classes have their own specific methods for making payments (make_payment() for the bank gateway and send_payment() for the PayPal gateway).

The PaymentGatewayAdapter class acts as an adapter that implements the PaymentGateway interface and internally holds an instance of the specific payment gateway. It adapts the specific payment gateway's method calls to the process_payment() method of the PaymentGateway interface.

In the usage section, we create instances of the specific payment gateways: bank_gateway and paypal_gateway. We then create adapter instances (adapter1 and adapter2) and pass the corresponding payment gateway instances to their constructors.

When calling the process_payment() method on the adapter objects, they internally invoke the specific methods (make_payment() or send_payment()) of the respective payment gateway objects. The adapters bridge the gap between the common PaymentGateway interface and the specific payment gateway classes.