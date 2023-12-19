The Pipe-and-Filter architectural pattern involves breaking down a system into a series of processing elements (filters) connected by channels (pipes). 

Each filter performs a specific operation on the input data and produces output that is passed through the pipes to the next filter. 

In the context of Harry Potter, let's create a simplified example with filters for creating wizards and casting spells.


```python
# Filter: Create Wizard
def create_wizard(data):
    name = data['name']
    house = data['house']
    return {'name': name, 'house': house}

# Filter: Cast Spell
def cast_spell(data):
    wizard_name = data['wizard_name']
    spell_name = data['spell_name']
    return f"Wizard {wizard_name} casts {spell_name}!"

# Pipe-and-Filter System
def pipe_and_filter_system(data, *filters):
    result = data
    for filter_func in filters:
        result = filter_func(result)
    return result

if __name__ == "__main__":
    # Input data
    input_data = {'name': 'Harry Potter', 'house': 'Gryffindor', 'spell_name': 'Expelliarmus'}

    # Define the filters
    filters = [create_wizard, cast_spell]

    # Run the Pipe-and-Filter system
    output = pipe_and_filter_system(input_data, *filters)

    # Display the result
    print(output)

```

In this example:

- `create_wizard` is a filter that takes input data containing a wizard's name and house, and it produces a wizard object.
- `cast_spell` is another filter that takes a wizard's name and a spell's name, producing a string indicating the spell casting.
- The `pipe_and_filter_system` function takes input data and a series of filters, applies each filter sequentially, and returns the final result.

When you run this script, it creates a wizard using the create_wizard filter and then casts a spell using the cast_spell filter, demonstrating the sequential processing of filters in a Pipe-and-Filter system. In a real-world scenario, filters might perform more complex operations, and the system could involve additional filters connected through pipes.