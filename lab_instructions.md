# General Instructions

Like always, each Lab should have the following header:
```
"""
Author: Your Name
Date: Today's Date/Due Date
FileName: The File's Name
Purpose: What the program is about
"""
```

# Lab6a: Recursion with the Lucas Numbers

The Lucas numbers are similar to Fibonacci but start with different initial values:

$L_0 = 2, L_1 = 1$

and follows the following reccurance formula:

\[ L_n = L_{n-1} + L_{n-2} \text{ for n > 1} \]

The Lucas sequence for the first couple numbers: 2, 1, 3, 4, 7, 11, 18, 29, 47, 76, 123...

Create a file called `recursion.py` and implement recursive function called `lucas_numbers(n)`, where the user enters the nth position of the lucas sequence.

After implementing, test on the following cases:
```python
print(lucas_iterative(0))   # 2
print(lucas_iterative(1))   # 1
print(lucas_iterative(5))   # 11
print(lucas_iterative(10))  # 123
```

# Lab6b: Coffee Machine Class

Ever used a coffee machine at a café or in an office? You press a button, and it dispenses coffee, but only if there's enough water, beans, and milk. Behind the scenes, the machine keeps track of its resources, how many cups it has made, and when it needs cleaning. In this lab, you'll create a `CoffeeMachine` class that mimics this behavior.

Create a file called `coffee_machine.py` and implement a `CoffeeMachine` class.

The constructor is called when you create a new coffee machine. It initializes the machine's resources.

```python
class CoffeeMachine:
    def __init__(self, machine_name, water=1000, beans=500, milk=300):
        self.machine_name = machine_name
        self.water = water  # in mL
        self.beans = beans  # in grams
        self.milk = milk    # in mL
        self.cups_made = 0
        self.profit = 0.0
        self.maintenance_count = 0
```

### Then implement the following functions:

### Step 2: `make_coffee(self, coffee_type)` Method

Create a method `make_coffee(self, coffee_type)` that:

- Accepts any case for `coffee_type` (e.g. "Espresso", "espresso", "ESPRESSO").
- Checks if there are enough water, beans, and milk.
- **If enough resources:**
  - Deduct the required amounts from water, beans, and milk.
  - Increase `cups_made` by 1.
  - Add the price to `profit`.
  - Return: `"Here is your {coffee_type}! Enjoy!"` (use the original casing the user passed)
- **If not enough resources:**
  - Return a message like:  
    `"Insufficient resources to make latte. Not enough water, milk."`
  - List **all** missing resources (water, beans, milk).
- **If the coffee type is unknown, return:**
  `"Unknown coffee type: {coffee_type}"`

Use these exact values (store it as a dictionary):

| Coffee Type   | Water (mL) | Beans (g) | Milk (mL) | Price ($) |
|---------------|------------|-----------|-----------|-----------|
| espresso      | 50         | 18        | 0         | 2.50      |
| americano     | 100        | 18        | 0         | 3.00      |
| latte         | 100        | 18        | 100       | 4.00      |
| cappuccino    | 100        | 18        | 80        | 4.00      |


### Step 3: `refill(self, water=None, beans=None, milk=None)` Method

Create a method `refill(self, water=None, beans=None, milk=None)` that:

- Adds the specified amounts to the resources.
- If a parameter is `None`, do **not** change that resource.
- Return a string in this format:  
  `"Refilled: Water +300mL, Beans +100g, Milk +200mL"`
- Only include the resources that were actually refilled.
- Example: If only water and milk are provided → `"Refilled: Water +300mL, Milk +200mL"`
- If nothing is refilled, you may return `"Nothing to refill."`

### Step 4: `check_resources(self)` Method

Create a method `check_resources(self)` that **prints** the following exact format:

```python
====================================
Machine: Kitchen Coffee
Water: 850mL
Beans: 450g
Milk: 200mL
Cups Made: 15
Profit: $45.50
====================================
```

Then test the class, below here is a sample:
```python
from coffee_machine import CoffeeMachine

# Create a coffee machine
my_machine = CoffeeMachine("Kitchen Coffee", 500, 200, 150)

# Make some coffee
print(my_machine.make_coffee("espresso"))
print(my_machine.make_coffee("latte"))
print(my_machine.make_coffee("americano"))
print(my_machine.make_coffee("cappuccino"))

# Try making coffee when low on resources
print(my_machine.make_coffee("latte"))   # Should fail

# Check resources
my_machine.check_resources()

# Refill
print(my_machine.refill(water=300, beans=100, milk=200))

# Make more coffee
print(my_machine.make_coffee("latte"))
print(my_machine.make_coffee("cappuccino"))

# Final check
my_machine.check_resources()
```


# Lab6c: [Part 2] Design a Player class

Now that you have functions for leveling up and using items, you will refactor your code into a class called **Player**. Then, you will add two new methods for random encounters and simplified combat.

#### Why a class?

So far, you’ve passed a player dictionary into functions. A class allows you to:

- Store the player’s data and actions together
- Avoid passing the dictionary repeatedly
- Add behavior like `gain_exp()`, `take_damage()`, etc.

### Step 1: Create the `Player` class

Define a class `Player` with a `__init__` method that takes the starting attributes.

Constructor:
`__init__(self, class_name, level, current_exp, health, attributes, inventory)`

or you can use the dictionary
Constructor:
`__init__(self, player_dictionary)`

Then also must do the following:

- Store all parameters as instance variables.
- Also store max_health (set equal to starting health).
- Store a dictionary for item effects (see Part 1):
    - `"apple"`: restores 50 HP
    - `"health potion"`: restores 100 HP + 10% of max health


### Step 2: Migrate your Part 1 functions into methods

#### Method `level_manager(self)`
- Same logic as Part 1’s level_manager(player), but:
    - Use self.level, self.current_exp, self.attributes, etc.
    - Ask the user which attribute to increase (STR/INT/DEX/VIT/CON/CHR).
    - Extra credit (if done): Handle multiple level-ups in one call.

#### Method `use_item(self, item_name)`
- Same logic as Part 1’s use_item(player, item_name), but:
    - Use self.inventory, self.health, self.max_health.
    - Return the message string as before.
    - Reduce the item count. Remove item if count reaches 0.

### Step 3: New methods for Part 2

#### Method `random_encounter(self)`
- Randomly determines if the player finds an enemy.
- **Logic**:
  - Generate a random number between 1 and 4.
  - If the number is 1, return `True` (encounter happens).
  - Otherwise, return `False`.
- **Print**:  
  `"You venture deeper... (roll) ... Nothing here."` (if no encounter)  
  Or just return `True` silently if encounter.

#### Method `combat(self, enemy_name, enemy_hp, enemy_damage)`
Simplified turn-based combat.

**Steps**:
1. Print: `"A {enemy_name} appears! HP: {enemy_hp}"`
2. While both player and enemy are alive:
   - Show player status:  
     `"Your HP: {self.health}/{self.max_health}"`
   - Ask user: `"Action? (attack / use item): "`
   - If `"attack"`:
     - Deal damage equal to player's STR attribute × 2.
     - Reduce enemy HP by that amount.
     - Print: `"You hit the {enemy_name} for {damage} damage!"`
   - If `"use item"`:
     - Ask `"Which item? (apple / health potion): "`
     - Call `self.use_item(item_name)` and print the result.
   - If enemy HP > 0, enemy attacks:
     - Reduce player's health by `enemy_damage`.
     - Print: `"{enemy_name} hits you for {enemy_damage} damage!"`
   - If player dies (health ≤ 0), print `"You have been defeated..."` and break.
3. If player wins (enemy HP ≤ 0):
   - Gain EXP equal to `enemy_hp × 2`.
   - Print: `"You defeated {enemy_name}! Gained {exp_gained} EXP."`
   - Call `self.level_manager()` to handle possible level-ups.

Please use the following skeleton:
```python
import random

class Player:
    def __init__(self, class_name, level, current_exp, health, attributes, inventory):
        # TODO: Set up instance variables
        # example, self.class_name = class_name

        # if you are doing a dictionary, you may do
        # self.class_name = player_dictionary['class']
        pass 
        # pass is here to allow for the function to be defined
        # you may remove them after you implement everything
    
    def level_manager(self):
        # TODO: Your Part 1 logic here
        pass
    
    def use_item(self, item_name):
        # TODO: Your Part 1 logic here
        pass
    
    def random_encounter(self):
        # TODO: Return True 25% of the time
        pass
    
    def combat(self, enemy_name, enemy_hp, enemy_damage):
        # TODO: Battle logic
        pass
```

### Sidenote:
Please note that there are many ways to create this player class. Some future suggestions is to create seperate classes for the RPG elements, and pass in a Player Object!

For example, instead of the current structure:

```python
class Player:
    def level_manager(self)
    def use_item(self)
    def random_encounter(self)
    def combat(self)
```

We can instead seperate them into the following:
```python
class Player:
    # Only player stats and basic actions
    def take_damage(self, amount)
    def heal(self, amount)
    def gain_exp(self, amount)
    def level_up(self)

class Inventory:
    # Manages items separately
    def add_item(self, item, quantity)
    def remove_item(self, item)
    def use_item(self, item_name, player)

class CombatSystem:
    # Handles battle logic
    def start_combat(self, player, enemy)
    def player_turn(self, player, enemy)
    def enemy_turn(self, player, enemy)

class EncounterSystem:
    # Manages random encounters
    def check_encounter(self)
    def generate_enemy(self, player_level)
```

But for the purposes of this course, we will put them all together (or you could be a project idea :3).