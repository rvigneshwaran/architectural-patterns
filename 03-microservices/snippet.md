The Microservices architectural pattern involves building a system as a collection of loosely coupled and independently deployable services. 

Each microservice represents a specific business capability and communicates with others through well-defined APIs. In the context of Harry Potter, let's create a simple example with two microservices: one for managing wizards and another for handling spells.


```python
from flask import Flask, jsonify, request

app_wizards = Flask(__name__)
app_spells = Flask(__name__)

# Wizards Microservice
wizards = []

@app_wizards.route('/wizards', methods=['GET'])
def get_wizards():
    return jsonify({'wizards': wizards})

@app_wizards.route('/wizards', methods=['POST'])
def create_wizard():
    data = request.get_json()
    wizard = {
        'name': data['name'],
        'house': data['house']
    }
    wizards.append(wizard)
    return jsonify({'wizard': wizard}), 201

# Spells Microservice
spells = []

@app_spells.route('/spells', methods=['GET'])
def get_spells():
    return jsonify({'spells': spells})

@app_spells.route('/spells', methods=['POST'])
def create_spell():
    data = request.get_json()
    spell = {
        'name': data['name'],
        'power_level': data['power_level']
    }
    spells.append(spell)
    return jsonify({'spell': spell}), 201

# Run Microservices
if __name__ == "__main__":
    app_wizards.run(port=5000)
    app_spells.run(port=5001)

```
In this example:

- The `app_wizards` and app_spells Flask applications represent two microservices, one for managing wizards and another for handling spells.
- Each microservice has endpoints (`/wizards` and `/spells`) for retrieving existing records and creating new ones.
- The `get_wizards` and `get_spells` endpoints return the list of wizards and spells, respectively.
- The `create_wizard` and `create_spell` endpoints allow the addition of new wizards and spells.

You can run this script, and the microservices will be accessible at `http://127.0.0.1:5000/wizards` and `http://127.0.0.1:5001/spells`.