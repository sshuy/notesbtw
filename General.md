# General Notes

## Handling control flow
Consider when you are doing conditions check how to approach the checking. If we are doing checks for specific items, instead of handling all of the other potential cases.
Instead just handle the cases you are looking for and raise an exception otherwise, especially if when the case we are looking for returns early.

### Return all possible results before raising an exception. (Not 100% sure how I feel but oh well.)
**Bad Example:**

**Note:** *It's important to fail early, but here I think having the exception at the end after checking all cases, works better, than having to provide all the cases required to raise an exception/failure.*
```python
# Bad :(
class Sword:
    def __init__(self, sword_type):
        self.sword_type = sword_type

    def __add__(self, other):
        if self.sword_type == "steel" or other.sword_type == "steel" or self.sword_type != other.sword_type:
            raise Exception("can not craft")

        if self.sword_type == "bronze" and other.sword_type == "bronze":
            return Sword("iron")
        else:
            return Sword("steel")
```

**Good Example:**
```python
# Good :)
class Sword:
    def __init__(self, sword_type):
        self.sword_type = sword_type

    def __add__(self, other):
        if self.sword_type == "bronze" and other.sword_type == "bronze":
            return Sword("iron")
        if self.sword_type == "iron" and other.sword_type == "iron":
            return Sword("steel")
    raise Exception("can not craft")
```
### Ordering is so VERY FUCKING IMPORTANT when it comes to control flow, like seriously...
Okay so we have a task where we are implemented overloads on operators on our custom class type, lets build this example.
- Class called 'Card'
    - Members
        - Rank [2, 3, 4... Jack, Queen, King, Ace] (Strings btw)
        - Rank Index - Position in the rank array
        - Suit [Clubs, Diamonds, Hearts, Spades] (Strings btw)
        - Suit Index - Position in the rank array

Now we want to implement three operator overloads.
- Add [+]
- Less Than [<]
- Greater Than [>]

The evaluation of each of these overloads depend on this implementation
> A card is "greater than" another card if it has a higher rank. However, if the ranks are the same, the card with the higher suit is "greater than" the other card. This same logic applies to the "less than" operator. The "equal to" operator should check that the rank AND suit are equal.

Now initially reading that implementation how would you implement the solution? Do you start by
- Checking if the card rank is greater than the other card rank?
- Checking if the card ranks are equal to eachother?
- Checking if the card suit is greater than the other card suit?

The answer is...

*Checking if the card ranks are equal to eachother*.

The other choices if chosen will result in you scratching your head going, man this works on like 90% of the cases, but two keep failing. Why??? Well checking if the card is greater than the other, should be the final check right? Because if that check is true then you're good and you can return out YAY, but doing so results in you missing a lot of edge cases. Trust me...

**Working Example**
```python
import random

SUITS = ["Clubs", "Diamonds", "Hearts", "Spades"]

RANKS = ["2", "3", "4", "5", "6", "7", "8", "9", "10", "Jack", "Queen", "King", "Ace"]


class Card:
    def __init__(self, rank, suit):
        self.rank = rank
        self.suit = suit
        self.rank_index = RANKS.index(rank)
        self.suit_index = SUITS.index(suit)

    def __eq__(self, other):
        return(self.rank_index == other.rank_index and self.suit_index == other.suit_index)

    def __lt__(self, other):
        if self.rank_index == other.rank_index and self.suit_index < other.suit_index:
            return True
        elif self.rank_index < other.rank_index:
            return True
        return False

    def __gt__(self, other):
        if self.rank_index == other.rank_index and self.suit_index > other.suit_index:
            return True
        elif self.rank_index > other.rank_index:
            return True
        return False

    def __str__(self):
        return f"{self.rank} of {self.suit}"
```
**Broken Example**
```python
import random

SUITS = ["Clubs", "Diamonds", "Hearts", "Spades"]

RANKS = ["2", "3", "4", "5", "6", "7", "8", "9", "10", "Jack", "Queen", "King", "Ace"]


class Card:
    def __init__(self, rank, suit):
        self.rank = rank
        self.suit = suit
        self.rank_index = RANKS.index(rank)
        self.suit_index = SUITS.index(suit)

    def __eq__(self, other):
        return(self.rank_index == other.rank_index and self.suit_index == other.suit_index)

    def __lt__(self, other):
        if self.rank_index < other.rank_index:
            return True
        elif self.suit.index < other.suit_index:
            return True
        return False

    def __gt__(self, other):
        if self.rank_index < other.rank_index:
            return True
        elif self.suit.index < other.suit_index:
            return True
        return False

    def __str__(self):
        return f"{self.rank} of {self.suit}"

# So getting the order wrong, like we've done above we end up saying Queen < Jack (FALSE) then we move to suit evaluate DIAMOND < SPADES (TRUE). uh, oh we've returned an errorenous result.
# Rank Inputs: Queen     Jack
# Suit Inputs: Diamonds  Spades
#
# Expected:
# - Equal: False
# - Greater than: True
# - Less than: False
#
# Actual:
# - Equal: False
# - Greater than: True
# - Less than: True
```
