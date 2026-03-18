---
name: stata-to-r-translator
description: Translare a Stata package to an R package whilst preserving behavior and generating verification tests. Use when translating Stata to R
---

# Stata to R Translator

Translate a stata package to an R package, whilst preserving behaviour, adapting idioms, and generating verification tests. 

## Translation Workflow

Follow this sequential process for code translation.

### 1. Analyse the Stata Package.

-- Is the source code a complete Stata package, including certification tests.?
-- List imports, external libraries and dependencies
-- Analyse the test in testing/ to understand the expected package behaviour.
-- Identify any existing equivalent packages in R and export the results to Stata2R/r-landscape.md

### 2. Plan Translation Strategy

-- Plan how to translate language-specific patterns (see references/language_mappings.md)  

### 3. Translate Code

Implement the translation following target language conventions:

**Core principles:**
- Preserve original behaviour exactly
- Follow R tidyverse language idioms and conventions 
- Maintain code structure when possible.
- Add appropriate R error handling.
- Include necessary imports and dependencies

### 4. Do the GUI

### 5. Generate Tests

Create comprehensive tests to verify translation correctness:

**Test generation approach:**
1. Use appropriate test template from `assets/` directory
2. Port existing tests from the testing/ directory to corresponding R test files and create a document summarising the test correspondence.
3. Create new tests covering:
   - Basic functionality for each function/method
   - Edge cases (empty inputs, null values, boundary conditions)
   - Error handling and exceptions
   - Integration between components

**Test equivalence:**
- Ensure tests verify the same behavior as original code
- Use equivalent assertions
- Maintain test structure and organization
- Add setup/teardown as needed for target framework

### 6. Complete Documentation

Compare the documentation in the .sthlp and examples/ directory with the R directory. Port any missing elements from stata to the R package.

Look through the source files for any additional documentation or history information and port it to the R package.
