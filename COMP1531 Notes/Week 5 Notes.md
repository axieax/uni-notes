# Continuous Integration (CI)

Process of automating the integration of code changes from multiple contributors into a single software project

- Write tests (ideally for each story, broad tests: unit, integration, acceptance, UI tests) - typically run by a "runner" (queue structure on VM)
- Code coverage checkers
- Merge and integrate code as often as possible
- Ensure build always work (i.e. green)

# Authentication vs authorisation

Authentication - veryifying identity of a user

- encrypt password: hashlib to create a hash `hashlib.sha256('my_password'.encode()).hexdigest()` (.encode() converts to binary)

Authorisation - verifying an identity's access privileges

- encode information: JSON Web Token (JWT) - prevents anti-tampering - header, payload, verify signature (hashed, including secret code)
  - `SECRET_KEY = 'asdkjfhadslkjfhs'`
  - `encoded_jwt = jwt.encode({'some': 'payload'}, SECRET_KEY, algorithm='HS256').decode('utf-8')`
  - `encoded_jwt.decode()`
  - `jwt.decode(encoded_jwt.encode('utf-8'), SECRET_KEY, algorithms=['HS256'])`

# SE Principles

Design smells:

- Rigidity: tendency to be too difficult to change
- Fragility: tendency for software to break when single change is made
- Immobility: previous work is hard to reuse or move
- Viscosity: changes feel very slow to implement
- Opacity: difficult to understand
- Needless complexity: things done more complex than they should be
- Needless repetition: lack of unified structures
- Coupling: interdependence between components

Design principles - make items:

- Extensible
- Reusable
- Maintainable
- Understandable
- Testable

Often through abstraction - removing characteristics of something to reduce it to a more high level concept

DRY: Don't repeat code (yourself) - every piece of knowledge must have a single, unambiguous, authoritative representation within a system

KISS: Keep it simple, stupid, e.g. get attribute of datetime - using datetime.datetime.now().strftime(); ==argparse== (-m etc.)

Encapsulation: maintaining type abstraction by restricting direct access to internal representation of types (types include classes)

Top-down thinking: should not add functionality until it is needed - work from high levels of abstraction down to lower levels of abstraction

Why write well-designed code: Agile loops - code needs to be maintainable

Refactoring: restructuring existing code without changing its external behaviour - typically to fix code or design smells - makes code more maintainable

# Persistence

Data storage:

- Memory (non-persistent)
- File (pickle) - load data upon server start, save all changes to pickled file as well
- Database (SQL)

## Taskboard - Kanbans

## Tute: Counting tags in html

```python
import requests
url = 'google.com'
html_code = requests.get(url).content.decode('utf-8')
```

```python
import flask, request, jsonify
import requests
app = Flask(__name__)

@app.route('/gettagcount', methods=['GET'])
def get_count():
  tag = request.args.get('tag')
  url = "https://www.unsw.edu.au"
  html_code = requests.get(url).content.decode('utf-8').split('<')
  counter = 0
  for element in html_code:
    if element.startswith(tag):
      counter += 1
  return jsonify({'count': counter})
```

