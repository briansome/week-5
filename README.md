# week-5
# Assignment 1: Design Your Own Class! 🏗️

class Smartphone:
    """
    Represents a generic smartphone.
    Demonstrates attributes, a constructor, and methods.
    """

    def __init__(self, brand, model, storage_gb, os="Android", price=0.0):
        """
        Constructor to initialize a new Smartphone object.

        Args:
            brand (str): The brand of the smartphone (e.g., "Samsung", "Apple").
            model (str): The specific model name (e.g., "Galaxy S23", "iPhone 15 Pro").
            storage_gb (int): The storage capacity in gigabytes.
            os (str, optional): The operating system. Defaults to "Android".
            price (float, optional): The price of the smartphone. Defaults to 0.0.
        """
        self.brand = brand
        self.model = model
        self.storage_gb = storage_gb
        self.os = os
        self.price = price
        self.__is_on = False  # Encapsulation: private attribute

        print(f"'{self.brand} {self.model}' created.")

    def turn_on(self):
        """Turns the smartphone on."""
        if not self.__is_on:
            self.__is_on = True
            print(f"{self.brand} {self.model} is now ON.")
        else:
            print(f"{self.brand} {self.model} is already on.")

    def turn_off(self):
        """Turns the smartphone off."""
        if self.__is_on:
            self.__is_on = False
            print(f"{self.brand} {self.model} is now OFF.")
        else:
            print(f"{self.brand} {self.model} is already off.")

    def make_call(self, number):
        """
        Simulates making a call if the phone is on.

        Args:
            number (str): The phone number to call.
        """
        if self.__is_on:
            print(f"{self.brand} {self.model} calling {number}...")
        else:
            print(f"{self.brand} {self.model} is off. Cannot make call.")

    def send_message(self, recipient, message):
        """
        Simulates sending a message if the phone is on.

        Args:
            recipient (str): The recipient of the message.
            message (str): The message content.
        """
        if self.__is_on:
            print(f"{self.brand} {self.model} sending message to {recipient}: '{message[:20]}...'")
        else:
            print(f"{self.brand} {self.model} is off. Cannot send message.")

    def install_app(self, app_name):
        """
        Simulates installing an app.

        Args:
            app_name (str): The name of the app to install.
        """
        if self.__is_on:
            print(f"{self.brand} {self.model} installing '{app_name}'...")
            print(f"'{app_name}' installed successfully.")
        else:
            print(f"{self.brand} {self.model} is off. Cannot install app.")

    def get_info(self):
        """Returns a string with basic information about the smartphone."""
        status = "On" if self.__is_on else "Off"
        return (f"Brand: {self.brand}, Model: {self.model}, "
                f"Storage: {self.storage_gb}GB, OS: {self.os}, "
                f"Price: ${self.price:,.2f}, Status: {status}")

# Inheritance Layer: PremiumSmartphone
class PremiumSmartphone(Smartphone):
    """
    Represents a premium smartphone, inheriting from Smartphone.
    Adds specific features like advanced camera and wireless charging.
    """

    def __init__(self, brand, model, storage_gb, os="iOS", price=1000.0, camera_megapixels=48):
        """
        Constructor for PremiumSmartphone, calls the parent constructor.

        Args:
            brand (str): The brand.
            model (str): The model.
            storage_gb (int): Storage capacity.
            os (str, optional): Operating system. Defaults to "iOS".
            price (float, optional): Price. Defaults to 1000.0.
            camera_megapixels (int, optional): Camera resolution in megapixels. Defaults to 48.
        """
        super().__init__(brand, model, storage_gb, os, price) # Call parent constructor
        self.camera_megapixels = camera_megapixels
        self.__has_wireless_charging = True # Encapsulation specific to premium

        print(f"  --> (Premium features added for '{self.model}')")

    def take_photo(self):
        """Simulates taking a high-quality photo."""
        if self._Smartphone__is_on: # Accessing encapsulated parent attribute (for demonstration)
            print(f"{self.model} taking a {self.camera_megapixels}MP photo! ✨")
        else:
            print(f"{self.model} is off. Cannot take photo.")

    def activate_wireless_charging(self):
        """Activates wireless charging if available."""
        if self.__has_wireless_charging:
            print(f"{self.model} is now wirelessly charging... ⚡")
        else:
            print(f"{self.model} does not support wireless charging.")

    # Polymorphism: Overriding a method (optional, but demonstrates polymorphism)
    def get_info(self):
        """Overrides parent's get_info to include premium details."""
        parent_info = super().get_info()
        return (f"{parent_info}, Camera: {self.camera_megapixels}MP, "
                f"Wireless Charging: {'Yes' if self.__has_wireless_charging else 'No'}")


# --- Creating and using objects ---
print("--- Demonstrating Smartphone Class ---")
my_phone = Smartphone("Xiaomi", "Redmi Note 12", 128, os="Android", price=250.00)
print(my_phone.get_info())
my_phone.turn_on()
my_phone.make_call("555-1234")
my_phone.install_app("TikTok")
my_phone.send_message("Alice", "Hey, what's up? Long time no see!")
my_phone.turn_off()
my_phone.make_call("999-8888") # Should not work when off
print("\n")

print("--- Demonstrating PremiumSmartphone Class (Inheritance & Polymorphism) ---")
premium_phone = PremiumSmartphone("Apple", "iPhone 15 Pro Max", 512, os="iOS", price=1499.99, camera_megapixels=64)
print(premium_phone.get_info()) # Calls the overridden get_info
premium_phone.turn_on()
premium_phone.make_call("111-2222")
premium_phone.take_photo()
premium_phone.activate_wireless_charging()
premium_phone.turn_off()
print("\n")

# Demonstrating encapsulation (attempting to access private attributes directly)
# This will raise an AttributeError if uncommented:
# print(my_phone.__is_on)
# Correct (though generally not recommended for private attributes):
# print(my_phone._Smartphone__is_on)
