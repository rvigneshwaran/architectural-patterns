
The Event-Driven architectural pattern involves components (or services) communicating with each other by emitting and listening to events. Events represent significant changes in the system, and services can react to these events. In this example, let's create a simple Event-Driven system in the context of Harry Potter using Python's built-in `queue` module for event handling.

```python
import queue
import threading

# Event Bus
class EventBus:
    def __init__(self):
        self.events = queue.Queue()

    def publish(self, event):
        self.events.put(event)

    def subscribe(self, callback):
        while True:
            event = self.events.get()
            callback(event)

# Wizard Service
class WizardService:
    def __init__(self, event_bus):
        self.event_bus = event_bus

    def create_wizard(self, name, house):
        wizard = {'name': name, 'house': house}
        self.event_bus.publish({'event_type': 'wizard_created', 'data': wizard})

# Spell Service
class SpellService:
    def __init__(self, event_bus):
        self.event_bus = event_bus

    def cast_spell(self, wizard_name, spell_name):
        spell_cast = {'wizard_name': wizard_name, 'spell_name': spell_name}
        self.event_bus.publish({'event_type': 'spell_cast', 'data': spell_cast})

# Event Handlers
def handle_wizard_created(event):
    print(f"New wizard created: {event['data']['name']} from House {event['data']['house']}")

def handle_spell_cast(event):
    print(f"Wizard {event['data']['wizard_name']} casts {event['data']['spell_name']}!")

# Usage
if __name__ == "__main__":
    event_bus = EventBus()

    # Subscribe event handlers
    event_bus.subscribe(handle_wizard_created)
    event_bus.subscribe(handle_spell_cast)

    # Create services
    wizard_service = WizardService(event_bus)
    spell_service = SpellService(event_bus)

    # Create a wizard and cast a spell
    wizard_service.create_wizard(name="Harry Potter", house="Gryffindor")
    spell_service.cast_spell(wizard_name="Harry Potter", spell_name="Expelliarmus")

```

In this example:

- The `EventBus` class acts as a central event dispatcher. It has methods for publishing events (`publish`) and subscribing to events (`subscribe`).
- The `WizardService` and `SpellService` classes represent two services that can create wizards and cast spells, respectively.
- The `handle_wizard_created` and `handle_spell_cast` functions are event handlers that react to specific event types.

When you run this script, you'll see output messages indicating the creation of a wizard and the casting of a spell, demonstrating the Event-Driven nature of the system. 

In a real-world scenario, services could be more complex, and events might trigger various actions in different parts of the system.