# rpg-character-generator

A lightweight Python module that builds a simple RPG character sheet. The `create_character` function validates the character's name and three core stats (strength, intelligence, charisma), then returns a formatted sheet with each stat drawn as a row of filled and empty dots.

## Contents

| File           | Description                                                     |
| -------------- | --------------------------------------------------------------- |
| `main.py`      | Defines the `create_character` function.                        |
| `LICENSE`      | CC0 1.0 Universal public domain dedication.                     |
| `.gitignore`   | Standard Python ignore rules for version control.               |

## Getting started

1. Make sure you have Python 3 installed.
2. Import and call the function from your own code:

   ```bash
   python -c "from main import create_character; print(create_character('Hero',3,2,2))"
   ```

## How it works

The module uses two marker characters and a single `create_character` function:

```python
full_dot = '●'
empty_dot = '○'

def create_character(name, strength, intelligence, charisma):

    if type(name) is not str:
        return "The character name should be a string"
    if name == "":
        return "The character should have a name"
    if len(name) > 10:
        return "The character name is too long"
    if " " in name:
        return "The character name should not contain spaces"

    if type(strength) is not int or type(intelligence) is not int or type(charisma) is not int:
        return "All stats should be integers"

    if strength < 1 or intelligence < 1 or charisma < 1:
        return "All stats should be no less than 1"
    if strength > 4 or intelligence > 4 or charisma > 4:
        return "All stats should be no more than 4"

    if strength + intelligence + charisma != 7:
        return "The character should start with 7 points"

    str_line = f"STR {full_dot * strength}{empty_dot * (10 - strength)}"
    int_line = f"INT {full_dot * intelligence}{empty_dot * (10 - intelligence)}"
    cha_line = f"CHA {full_dot * charisma}{empty_dot * (10 - charisma)}"

    return f"{name}\n{str_line}\n{int_line}\n{cha_line}"
```

### Validation rules

Before building the sheet, the function returns a friendly error string when a
rule is broken:

- `name` must be a `str` → otherwise `"The character name should be a string"`.
- `name` must not be empty → `"The character should have a name"`.
- `name` must be at most 10 characters → `"The character name is too long"`.
- `name` must not contain spaces →
  `"The character name should not contain spaces"`.
- `strength`, `intelligence`, and `charisma` must all be `int` →
  `"All stats should be integers"`.
- Each stat must be at least `1` → `"All stats should be no less than 1"`.
- Each stat must be at most `4` → `"All stats should be no more than 4"`.
- The three stats must sum to exactly `7` →
  `"The character should start with 7 points"`.

When every check passes, each stat is rendered as `STR`/`INT`/`CHA` followed by
`strength` filled dots and `10 - strength` empty dots, producing a 10-cell bar
per stat.

### Example usage

```python
from main import create_character

print(create_character("Hero", 3, 2, 2))
# Hero
# STR ●●●○○○○○○○
# INT ●●○○○○○○○○
# CHA ●●○○○○○○○○

print(create_character("A", 1, 1, 1))
# The character should start with 7 points
```

> Note: the module only defines the function — it has no top-level `print`
> calls, so running `python main.py` produces no output. Import it as shown
> above to use it.

## Key concepts

- Validate several inputs with early-return guard clauses.
- Use `type(x) is not int` / `is not str` for strict type checks.
- Build a string with f-strings and repeat characters with the `*` operator.
- Return either a formatted result or a clear error message.

## License

Released under [CC0 1.0](LICENSE), placing the work in the public domain.
