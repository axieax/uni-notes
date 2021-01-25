# Decorators

Wrappers

```python
def authorise(function):
  def wrapper(*args, **kwargs):
    # Before
    auth_token = kwargs['auth_token']
    if auth_token != 'secret':
      raise Exception
    del kwargs['auth_token']
    # Function call
    return_value = function(*args, **kwargs)
    # After
    update_data()
    return return_value
  return wrapper

@authorise
def send_message(channel_id, message_body)
	pass

@authorise
def create_channel(channel_name, is_private):
  pass

if __name__ == '__main__':
  token = 'test'
  send_message(1, 'Hello', auth_token=token)
  create_channel('Channel', False, auth_token=token)  
```

# Property-based testing

Use Hypothesis to generate inputs for general tests

```python
from hypothesis import given, strategies, Verbosity, settings

def echo(x):
  return x

def is_even(l):
  return [x % 2 == 0 for x in l]

@given(strategies.integers(min_value=0, max_value=100))
def test_int(i):
  assert i == echo(i)

@given(strategies.text())
def test_str(x):
  assert x == echo(x)
  
@given(strategies.lists(strategies.integers()))
def test_even(old_list):
  original_length = len(old_list)
  new_list = is_even(old_list)
  new_length = len(new_list)
  assert original_length == new_length
  for i in range(new_length):
    if old_list[i] % 2 == 0:
      assert new_list[i] == 1
    else:
      assert new_list[i] == 0
```

https://hypothesis.readthedocs.io/en/latest/data.html

# SDLC Deployment

Continuous Integration - practice of automating the integration of code changes from multiple contributors into a single software project

Deployment - activities relating to making a software system available for use

Movement from software as an asset (disc), to software as a service (subscription for software updates) --> transition of deployment being more frequent

## Modern deployment - heavily integrated and automated

<img src="https://miro.medium.com/max/3536/1*ixosClL_dPysk9sYaJxrHg.png" alt="Beginner-Friendly Introduction to GitLab CI/CD | by Zuri Hunter | FAUN |  Medium" style="zoom:40%;" />

Continuous delivery (CD) - allows accepted code changes to be deployed to customers quickly and sustainably - involves the automation of the release process such that releases can be done in a 'button push' (still requires manual approval)

Three common tiers:

- dev - released often, available to developers to see their changes in deployment
- test - as close to release as possible, ideally identical to prod
- prod - released to customers, ideally as quickly as possible

Continuous delivery is concerned with automatically pushing code out to dev, test, prod.

<img src="https://edge.siriuscom.com/_wss/clients/509/assets/503/CI-CD-graphic.PNG" alt="Continuous Integration and Continuous Delivery: Beyond the Conveyor Belt  Mentality" style="zoom:20%;" />

## Flighting

Term used predominantly in larger software projects to describe moving builds out of particular slices of users, beyond the simplicity of 'dev', 'test', 'prod', e.g. Windows Insider Program

## Continuous deployment

Continuous deployment - extension of continuous delivery whereby changes attempt to flight toward production automatically, and the only thing stopping them is a failed test

## A/B Testing

Randomised scientific experiment with multiple variants (typically two) - consists of one independent variable with all other variables controlled

Consists of having two "versions" randomly distributed to end-users, then monitoring the results. These versions can be managed within the same instance, or sent to different instances via a load balancer.

## DevOps

Modern DevOps Roles:

- Product owner
- Team lead
- Cloud architect
- Site reliability engineer
- DevOps system administrator

## Maintenance

After deployment, the use of analytics and monitoring tools to ensure that as the platform is used and remains in a healthy state (e.g. 4XX 5XX errors, ensuring disk, memory, cpu and network is not overloaded - often aren't actively monitored, but through alerts and triggers)

- to preserve user experience (warnings, errors, performance/uptime issues)
- to enhance user experience (analytical tools to monitor users or understand their interactions --> customer interviews and user stories)



Deployment to Heroku / AWS





