---
name: pseudocode-to-r
description: Translate pseudocode package to an R package whilst preserving behavior and generating verification tests. Use when translating pseudocode  to R
---

# Pseudocode to R 

Prompt the user for a location to create the new package. Suggest {../package-name R}
## 1. Code translation
Translate the code in the pseudocode directory to an R package, whilst preserving behaviour, adapting idioms, and generating verification tests.
- Use the renv package to create and manage a local environment throughout. 
- Preserve original behaviour exactly
- Follow R tidyverse language idioms and conventions 
- Maintain code structure when possible.
- Add appropriate R error handling.
- Include necessary imports and dependencies

## 2. Create a Shiny GUI to recreate any dlg files in the package directory.

## 3. Generate Tests

Create tests to verify package functions:

**Test generation approach:**
1. Create new tests covering:
   - Basic functionality for each function/method
   - Edge cases (empty inputs, null values, boundary conditions)
   - Error handling and exceptions
   - Integration between components


## 4. Complete Documentation

Compare the documentation in the .sthlp and examples/ directory with the R directory. Port any missing elements from stata to the R package.

Look through the source files in the package for any additional documentation or history information and port it to the R package.

### 5. Add open source infrastructure
- Copy the license file from the original package to the r package.
- Add a contributing guide to the r package
- Add a github workflow to run r tests on push to main, pull requests, and workflow dispatch
- add a .gitignore to r package

