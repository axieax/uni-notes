# User stories

User Stories are a method of requirements engineering used to inform the development process and what features to build with the user at the centre.

As a < type of user >, I want < some goal > so that < some reason >

User stories are written in non-technical language and are user-goal focused, not product-feature focused. User stories inform feature decisions.

Why do we care? They keep customers at the centre - keep it problem focused, not solution focused

Epic user stories

How do we know we've met the user story requirement?

- **I**ndependent: user story could be developed independently and delivered separately
- **N**egotiable: avoid too much detail
- **V**aluable: must hold some value to the client
- **E**stimable: we'll get to this in a later lecture
- **S**mall: user story should be small
- **T**estable

## User Acceptance Criteria (Rule-based)

Break down a user story into criteria that must be met for the user, or customer, to accept

e.g. As a user, I want to use a search field to type a city, name, or street, so that I can find matching hotel options.

--> As a user, I want to use a search field to type a city, name, or street, so that I can find matching hotel options. The search field is placed on the top bar Search starts once the user clicks “Search” The field contains a placeholder with a grey-colored text: “Where are you going?” The placeholder disappears once the user starts typing Search is performed if a user types in a city, hotel name, street, or all combined The user can’t type more than 200 symbols

## Acceptance Tests

Acceptance tests are black-box tests that are performed to ensure acceptance criteria have been met. 

## Scenario Oriented Acceptance Criteria

**Given** some precondition, **When** I do some action, Then I expect some result

## Overview

- Rule-based acceptance criteria are simpler and generally work for all sorts of stories
- Scenario-based AC work for stories that imply specific user actions, but don't work for higher-level system properties (e.g. design)
- Scenario-based AC are more likely to be implementable as tests

# System Modelling

## Conceptual Modelling

e.g. for software engineering: Data models, Mathematical models, Domain models, Data flow models, State transition models

Models used to convey the fundamental principles and basic functionality of systems (communication)

- Structural - highlight the static structure of the system (e.g. UML class diagrams, ER diagrams)
- Behavioural - highlight the dynamic behaviour (e.g. State diagrams - states are circles, transitions are labelled arrows connecting them)

# Git reset --hard vs --soft; git commit --amend



