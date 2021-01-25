# Week 1-2 Notes

## Software Development Life Cycle (SDLC)

1. Requirements analysis

   - Analyse and understand problem domain (agreement of work to be completed by all stakeholders, descriptions and constraints of a proposed system)
   - Determine functional (specific capability/service that the system should provide) and non-functional (constraint on how the system can achieve that - performance characteristic) components
     - e.g. functional: the system must send a notification to all users whenever there is a new post; non-functional: the system must send emails no later than 30 minutes after from such an activity

   - Generate userstories / use cases

2. Design

   - Producing software architecture/blueprints
   - System diagrams and schematics
   - Modelling of data flows

3. Development

   - Choosing a programming language and write the code

4. Testing

   - Use unit or behaviour tests to test your software

5. Deployment

   - "Ship it"

6. Maintenance

   - Monitor

### Requirements engineering

- Identify purpose and goal of a software system, negotiation process between stakeholders (e.g. end users, clients/businesses, design teams)

<u>Process:</u>

1. Elicitation of raw requirements from stakeholders - questions and discovery

   - Market research
   - Interviews with stakeholders
   - Focus groups
   - Asking “what if? what is?” questions

2. Analysis of requirements - building the picture

   - Identify dependencies, conflicts, risks

   - Establish relative priorities

   - Usually done through:

   - - User stories
     - Use cases - represent a dialogue between the user and the system, with the aim of helping the user achieve a business goal (black box)
       - Use case, goal in context, scope, level, preconditions, success end condition, failed end condition, primary actor, trigger
       - Steps (main success scenario)

3. Formal specification of requirements - refining the picture

   - Establishing the right sense of granularity
   - Often the stage of breaking up into functional and non-functional

4. Validation of requirements - going back to stakeholders and ensuring requirements are correct

<u>Challenges:</u>

- Requirements sometimes only understood after design/build has begun
- Clients/customers sometimes don’t know what they want
- Clients/customers sometimes change their mind
- Developers might not understand the subject domain
- Limited access to stakeholders
- Jumping into details or solutions too early (XY problem)

<u>Important:</u>

- Investigate stakeholder needs
- Expand, refine and connect specific ideas
- Understand the iterative and ongoing nature

## pytest

pytest Python library - detects any function prefixed with **test** and runs that function, processing the assertions inside - don’t need to call test functions

`import pytest`

run from cli using `pytest-3 FILE`

no file specified when running pytest-3 - automatically looks for any files in that directory in shape:

- test_*.py
- *_test.py

Run specific functions without test files using -k

e.g. test_small ; test_small_negative; test_large

`pytest-3 -k small` or `pytest-3 -k small -v`

Markers: use a range of decorators to specify tests in python, e.g. `@pytest.mark.up`



*Add to path:*

Project in ~/cs1531/project

`export PYTHONPATH="$PYTHONPATH:~/1 cs1531/project"`

Then add to `~/.bashrc` terminal



## Python Data Types

Can destructure tuples

Strings immutable

Lists - sequential containers of memory, ordered

- Integer index can be negative - count from end

- Enumerate list - has an index tracker

- - e.g. for index, element in enumerate(list):

Dictionary - associative containers of memory - string key mapped to value



Iterate over dictionary - keys e.g. for key in dict:

​	`dict.items()` - key value as tuple

​	`dict.keys()` - key

​	`dict.values()` - values



## Exceptions

> Action (error thrown) that disrupts the normal flow of a program - exceptions are ways we can elegantly recover from errors

```python
raise Exception("...")
```

This gives us more information but doesn't help us handle it.. try and catch by:

```python
try:
  pass
except Exception as e:
  pass
```

Can keep running program after resolving error - rather than exiting / crashing.

Exceptions carry data. When exceptions are thrown, normal code execution stops. 

Using with `pytest`:

1. Example 1

   ```python
   def sqrt(x):
   	if x < 0:
   		raise Exception(f"Input {x} is less than 0. Cannot sqrt a number < 0")
   	return x**0.5
   
   def test_sqrt_bad():
   	with pytest.raises(Exception, match=r"*Cannot sqrt*"):
   		sqrt(-1)
   		sqrt(-2)
   		sqrt(-3)
   		sqrt(-4)
   		sqrt(-5)
   
   ```

2. Example 2 - other basic exceptions can be caught with the 'exception' type

   ```python
   def sqrt(x):
   	if x < 0:
   		raise ValueError(f"Input {x} is less than 0. Cannot sqrt a number < 0")
   	return x**0.5
   
   def test_sqrt_bad():
   	with pytest.raises(Exception):
   		sqrt(-1)
   		sqrt(-2)
   		sqrt(-3)
   		sqrt(-4)
   		sqrt(-5)
   ```



## Project Management

Agile

Standups - what did I do, what problems did I face, What am I going to do

Sprints/iterations - time is fixed, scope is flexible; plan only for the next sprint; typically have a release at the end of each sprint

Taskboards - don’t need many columns, e.g. backlog, todo, doing, testing?, closed/done

Pair programming

Test-driven-development (TDD) - writing tests before the implementation, write only enough code to make the next text pass















