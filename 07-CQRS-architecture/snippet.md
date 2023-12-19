The Command-Query Responsibility Segregation (CQRS) architectural pattern involves separating the responsibilities for handling commands (write operations) and queries (read operations). 

In this example, let's create a simplified implementation in the context of Harry Potter with separate components for handling commands and queries.

```python
# Command Handler
class WizardCommandHandler:
    def __init__(self):
        self.wizards = []

    def handle_create_wizard(self, name, house):
        wizard = {'name': name, 'house': house}
        self.wizards.append(wizard)

# Query Handler
class WizardQueryHandler:
    def __init__(self, command_handler):
        self.command_handler = command_handler

    def get_all_wizards(self):
        return self.command_handler.wizards

# Usage
if __name__ == "__main__":
    # Create command handler
    command_handler = WizardCommandHandler()

    # Create query handler with a reference to the command handler
    query_handler = WizardQueryHandler(command_handler)

    # Command: Create Wizard
    command_handler.handle_create_wizard(name="Harry Potter", house="Gryffindor")

    # Query: Get All Wizards
    all_wizards = query_handler.get_all_wizards()

    # Display the result
    print("All Wizards:")
    for wizard in all_wizards:
        print(f"- {wizard['name']} from House {wizard['house']}")

```

In this example:

- `WizardCommandHandler` is responsible for handling commands related to wizards. It has a method `handle_create_wizard` for creating a new wizard.
`WizardQueryHandler` is responsible for handling queries related to wizards. It takes a reference to the `WizardCommandHandler` and has a method `get_all_wizards` for retrieving all wizards.

This separation allows for the segregation of responsibilities between writing and reading operations. In a real-world scenario, you might have more complex logic in both command and query handlers, and the data storage mechanisms could be different for writes and reads.