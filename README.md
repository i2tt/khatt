# Khatt

Khatt is an agent skill that rewrites code which reads as AI-generated so that it reads as if the codebase's own developers wrote it while keeping everything the code does

The skill is a single file named SKILL.md with no plugins and no build step

## Before and after 

Before

```python
def process_data(data):
    """
    Processes the input data by normalizing each item.

    Args:
        data (list): The list of items to process.

    Returns:
        list: The processed data.
    """
    try:
        # Step 1: Initialize the result list
        processed_data = []
        # Step 2: Loop through each item
        for item in data:
            # Normalize the item
            result = item.strip().lower()
            processed_data.append(result)
        # Step 3: Return the result
        return processed_data
    except Exception as e:
        print(f"❌ An error occurred: {e}")
        return []
```

After

```python
def normalize_tags(tags):
    return [t.strip().lower() for t in tags]
```

The rewrite removes the docstring that repeats the signature, the step comments, the comments that restate each line, the broad except that hid errors behind an empty list, and the emoji. It renames the function after what it does. It keeps the one thing the code does

## What it does not do

- It never adds bugs, typos, or sloppy formatting to make code look human
- It never changes behavior without saying so. It records public names, return values, errors, and side effects before editing and checks the rewrite against them
- It never invents an API, config key, dependency, or a reason for a comment

## Installation

For Claude Code on Windows PowerShell

    git clone https://github.com/i2tt/khatt.git "$env:USERPROFILE\.claude\skills\khatt"

For Claude Code on macOS or Linux

    git clone https://github.com/i2tt/khatt.git ~/.claude/skills/khatt

For any other agent that supports skills, place SKILL.md inside a folder named khatt in the skills folder that your agent reads from

## Usage

- Pasted code: write "use khatt on this code" and paste the code
- A file or folder: write "use khatt on src/billing.py"
- Check only: write "check this code with khatt without editing"
- While writing new code: write "use khatt while you write this" and the skill applies silently
- To match a style: point at a file you like and the skill will follow it over the default rules

## Modes

- Pasted code returns the rewritten code, a list of changes with pattern numbers, and a line confirming behavior did not change
- File mode reads the whole file and its neighbors, edits in place, runs the project's tests or linter when it has them, and reports which parts it reviewed and which it did not cover
- Embedded mode applies the rules silently when another task writes code, a commit message, or a pull request
- Review mode returns each tell with its file, line, pattern number, and strength, without editing

## Method

1. Record the behavior that must not change, then mark each AI pattern, strongest first
2. Read neighboring files for the team's conventions and existing helpers
3. Write a draft that removes the tells and matches the neighbors
4. Compare the draft with the behavior ledger, run tests if there are any, and look for remaining patterns
5. Write the final version

## Patterns

Patterns are sorted from strongest to weakest inside each section. Patterns 1 to 6, 25, and 29 are enough on their own to justify an edit.

The skill also warns against overcorrecting: code with every comment stripped, every edge polished, and every function named in the same verb_noun shape reads as generated too.

### A. Narration

1. Comments that restate the code
2. Step-numbered and outline comments
3. Comments addressed to the reader
4. Change notes inside the code
5. Docstrings on everything
6. Emoji and decoration in code

### B. Defense by rule

7. Error handling around everything
8. Checks for states that cannot happen
9. Fallbacks that hide missing data
10. Logging every step

### C. Structure by rule

11. Abstractions with one use
12. Names written for a stranger
13. Verbose forms of simple logic
14. Demo and scaffold blocks
15. Constants for every literal

### D. Inflation

16. Marketing words in code
17. Error messages written as a reply

### E. Leftovers

18. Placeholders and elisions
19. Commented-out alternatives
20. Unused imports and variables

### F. Wrong codebase

21. Style drift from the neighbors
22. Reinventing what the repository has

### G. Tests, commits, and pull requests

23. Test names and tests that restate the code
24. Commit messages and PR descriptions

### H. Assembled from parts

25. Primitives from the wrong concurrency model, such as a threading lock inside asyncio
26. Two libraries for one job, such as colorama and pystyle in one script
27. Portability guards nobody asked for
28. Terminal layouts measured by hand
29. Timers that measure the wrong span, such as a ping clock started before the semaphore

## When the skill does not act

- When the repository's own conventions call for the pattern, such as required docstrings or a lint rule
- Generated code, vendored code, migrations, and lockfiles
- Public APIs that callers outside the change depend on
- Comments that explain why, license headers, and links to issues
- Validation at a trust boundary such as user input, network data, or files
- Tutorial code where the explanation is the point

## Repository layout

- SKILL.md is the skill itself
- README.md is this file
- CHANGELOG.md is the version history
- LICENSE is the MIT license

## License

Khatt is released under the MIT License. See [LICENSE](LICENSE)

## Credits
<p align="center">
  <a href="https://github.com/i2tt"><img src="https://img.shields.io/badge/i2tt-GitHub-181717?style=for-the-badge&logo=github&logoColor=white" alt="i2tt" /></a>
  <a href="https://soar-team.xyz/"><img src="https://img.shields.io/badge/Website-soar--team.xyz-111111?style=for-the-badge&logo=googlechrome&logoColor=white" alt="Website" /></a>
</p>
