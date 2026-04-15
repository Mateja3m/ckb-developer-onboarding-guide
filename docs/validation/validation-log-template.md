# Validation Log Template

Use one copy of this template for each test attempt.

```md
# Validation Log

## Metadata

- Date:
- Tester:
- Section being validated:
- Source used:
- Operating system:

## Command Executed

```bash
<paste the exact command you ran>
```

## Observed Output

```text
<paste the full output or the most relevant part>
```

## Failure Cases

- Did the command fail? If yes, how?
- Did it partially work?
- Was the output incomplete, misleading, or different from expectations?

## Confusion Points

- What would a beginner likely not understand here?
- Was any term, dependency, or expected precondition unclear?
- Did the step assume hidden knowledge?

## Possible Root Cause (Optional)

- Missing dependency
- Wrong version
- Wrong directory
- Missing configuration
- Permission issue
- Network issue
- Unclear documentation
- Other:

## Notes

- What would improve this step?
- What should be added to future docs?
- Should this become a troubleshooting entry later?
```

## Short Form Version

Use this when you want a faster capture format:

```md
## Command Executed
```bash
<command>
```

## Observed Output
```text
<output>
```

## Failure Cases
- None / describe failure

## Confusion Points
- None / describe confusion

## Possible Root Cause (Optional)
- N/A / describe cause

## Notes
- Additional notes
```
