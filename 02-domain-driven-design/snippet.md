Domain-Driven Design (DDD) is more of a design philosophy than a specific architectural pattern. It emphasizes building software systems that closely align with the business domain they are intended to serve. In DDD, the core building blocks are Entities, Value Objects, Aggregates, Repositories, Services, and Domain Events.

```python
from typing import List

# Entity
class Wizard:
    def __init__(self, wizard_id: int, name: str, house: str):
        self.wizard_id = wizard_id
        self.name = name
        self.house = house

# Value Object
class Spell:
    def __init__(self, name: str, power_level: int):
        self.name = name
        self.power_level = power_level

# Repository
class WizardRepository:
    def __init__(self):
        self.wizards: List[Wizard] = []

    def add_wizard(self, wizard: Wizard):
        self.wizards.append(wizard)

    def get_wizard_by_id(self, wizard_id: int) -> Wizard:
        for wizard in self.wizards:
            if wizard.wizard_id == wizard_id:
                return wizard
        raise ValueError("Wizard not found")

# Usage
if __name__ == "__main__":
    # Create a wizard
    harry = Wizard(wizard_id=1, name="Harry Potter", house="Gryffindor")

    # Create spells (value objects)
    expelliarmus = Spell(name="Expelliarmus", power_level=10)
    patronus = Spell(name="Expecto Patronum", power_level=15)

    # Assign spells to the wizard
    harry.spells = [expelliarmus, patronus]

    # Create a wizard repository
    wizard_repository = WizardRepository()

    # Add the wizard to the repository
    wizard_repository.add_wizard(harry)

    # Retrieve the wizard from the repository
    retrieved_wizard = wizard_repository.get_wizard_by_id(1)

    # Print wizard information
    print(f"Name: {retrieved_wizard.name}, House: {retrieved_wizard.house}")
    print("Spells:")
    for spell in retrieved_wizard.spells:
        print(f"- {spell.name} (Power Level: {spell.power_level})")
```

In this example:

- `Wizard` is an entity representing a wizard with an ID, name, house, and a list of spells.
- `Spell` is a value object representing a magical spell with a name and power level.
- `WizardRepository` is a repository responsible for adding wizards and retrieving wizards by their ID.

This is a simplified illustration, and in a real-world scenario, you would typically have more complex domain models and might involve other DDD concepts like Aggregates, Services, and Domain Events depending on the complexity of your domain.
