```python
# Model
class Character:
    def __init__(self, name, house, role):
        self.name = name
        self.house = house
        self.role = role

# View
class CharacterView:
    def display_character(self, character):
        print(f"Name: {character.name}, House: {character.house}, Role: {character.role}")

# Controller
class CharacterController:
    def __init__(self, model, view):
        self.model = model
        self.view = view

    def set_character_name(self, name):
        self.model.name = name

    def set_character_house(self, house):
        self.model.house = house

    def set_character_role(self, role):
        self.model.role = role

    def update_view(self):
        self.view.display_character(self.model)

# Usage
if __name__ == "__main__":
    # Create a Harry Potter character
    harry = Character(name="Harry Potter", house="Gryffindor", role="Wizard")

    # Create a view and a controller
    view = CharacterView()
    controller = CharacterController(model=harry, view=view)

    # Display the initial character information
    controller.update_view()

    # Update the character information through the controller
    controller.set_character_house("Hogwarts")
    controller.set_character_role("Seeker")

    # Display the updated character information
    controller.update_view()
```

In this example:

- The `Character` class represents the model, defining the attributes of a Harry Potter character.
- The `CharacterView` class handles the presentation of character information.
- The `CharacterController` class acts as an intermediary between the model and the view, updating the model and notifying the view to display the updated information.