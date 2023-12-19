
 The Layered architectural pattern involves organizing the application into distinct layers, where each layer has a specific responsibility. Typically, the layers include Presentation (or UI), Business Logic, and Data Access layers. In this example, we'll create a simple implementation in the context of Harry Potter with three layers: Presentation, Business Logic, and Data Access.

```python
# Data Access Layer
class WizardRepository:
    def __init__(self):
        self.wizards = []

    def add_wizard(self, wizard):
        self.wizards.append(wizard)

    def get_wizards(self):
        return self.wizards

# Business Logic Layer
class WizardService:
    def __init__(self, wizard_repository):
        self.wizard_repository = wizard_repository

    def create_wizard(self, name, house):
        wizard = {'name': name, 'house': house}
        self.wizard_repository.add_wizard(wizard)

    def get_all_wizards(self):
        return self.wizard_repository.get_wizards()

# Presentation Layer
class WizardConsoleApp:
    def __init__(self, wizard_service):
        self.wizard_service = wizard_service

    def run(self):
        while True:
            print("\n1. Create Wizard")
            print("2. Display All Wizards")
            print("3. Exit")

            choice = input("Enter your choice: ")

            if choice == '1':
                name = input("Enter wizard name: ")
                house = input("Enter wizard house: ")
                self.wizard_service.create_wizard(name, house)
                print(f"Wizard {name} created in House {house}.")
            elif choice == '2':
                wizards = self.wizard_service.get_all_wizards()
                print("\nAll Wizards:")
                for wizard in wizards:
                    print(f"- {wizard['name']} from House {wizard['house']}")
            elif choice == '3':
                print("Exiting.")
                break
            else:
                print("Invalid choice. Please try again.")

if __name__ == "__main__":
    # Create instances of each layer
    wizard_repository = WizardRepository()
    wizard_service = WizardService(wizard_repository)
    wizard_app = WizardConsoleApp(wizard_service)

    # Run the application
    wizard_app.run()

```

In this example:

- The Data Access Layer (`WizardRepository`) is responsible for storing and retrieving wizard data.
- The Business Logic Layer (`WizardService`) contains the application's business logic, including the creation and retrieval of wizards.
- The Presentation Layer (`WizardConsoleApp`) is a simple console application that interacts with the user, taking input and displaying output.

This structure demonstrates the separation of concerns and responsibilities among the layers. In a more complex system, you might have additional layers, such as Service or Domain layers, depending on the application's requirements.