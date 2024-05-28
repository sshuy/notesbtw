# General Notes

Consider when you are doing conditions check how to approach the checking. If we are doing checks for specific items, instead of handling all of the other potential cases.
Instead just handle the cases you are looking for and raise an exception otherwise, especially if when the case we are looking for returns early.

- Bad Example:
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

- Good Example:
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
