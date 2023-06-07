---
title: "Bridge"
date: 2023-06-07T08:24:20+05:30
draft: False
---

The Bridge pattern is a structural design pattern that decouples an abstraction from its implementation, allowing them to vary independently. It provides a way to separate the interface and implementation of a class hierarchy, enabling them to evolve independently.

```
class Device:
    def __init__(self):
        self.state = False

    def is_enabled(self):
        return self.state

    def enable(self):
        self.state = True

    def disable(self):
        self.state = False


class RemoteControl:
    def __init__(self, device):
        self.device = device

    def toggle_power(self):
        if self.device.is_enabled():
            self.device.disable()
        else:
            self.device.enable()

    def volume_up(self):
        pass

    def volume_down(self):
        pass


class TV(Device):
    def __init__(self):
        super().__init__()
        self.volume = 50

    def volume_up(self):
        if self.volume < 100:
            self.volume += 10

    def volume_down(self):
        if self.volume > 0:
            self.volume -= 10

    def get_volume(self):
        return self.volume


class Radio(Device):
    def __init__(self):
        super().__init__()
        self.volume = 30

    def volume_up(self):
        if self.volume < 100:
            self.volume += 5

    def volume_down(self):
        if self.volume > 0:
            self.volume -= 5

    def get_volume(self):
        return self.volume


# Usage
tv = TV()
remote_control = RemoteControl(tv)

remote_control.toggle_power()
remote_control.volume_up()
remote_control.volume_up()
print(tv.is_enabled())  # Output: True
print(tv.get_volume())  # Output: 70

radio = Radio()
remote_control = RemoteControl(radio)

remote_control.toggle_power()
remote_control.volume_down()
print(radio.is_enabled())  # Output: True
print(radio.get_volume())  # Output: 25
```

In this example, we have the Device class hierarchy, which represents different entertainment devices such as TVs and radios. Each device has its own implementation of enabling/disabling and adjusting volume.

The RemoteControl class acts as the abstraction and holds a reference to a Device object. It provides methods for toggling power, increasing volume, and decreasing volume. These methods delegate the operations to the respective methods of the assigned device.

The TV and Radio classes are concrete implementations of the Device class. They provide specific implementations for enabling/disabling and adjusting volume. In this example, they have additional methods get_volume() to retrieve the current volume.

In the usage section, we create instances of the TV and Radio classes. Then, we create instances of the RemoteControl class, passing the respective device objects. We can then use the remote control to toggle power and adjust the volume, and we can retrieve the current state and volume of the devices.

By using the Bridge pattern, we separate the abstraction (remote control) from its implementation (device). This allows us to independently extend and modify both the remote controls and the entertainment devices, and easily switch between different combinations of remote controls and devices.
