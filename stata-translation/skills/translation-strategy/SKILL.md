---
name: translation-strategy
description: Decide whether it is worth translating a Stata package to other programming languages. Use before performing any translation.
---

### 1. Analyse the Stata Package.

-- Is the source code a complete Stata package, including certification tests.?
-- List imports, external libraries and dependencies
-- Analyse the test in testing/ to understand the expected package behaviour.
-- Export results to Analysis/stata.md

### 2. R Landscape
-- Identify any existing equivalent packages in R and export the results to Stata2R/r-landscape.md
-- do you recommend creating a new r package or contributing these changes to one of the existing packages.
-- export results to Stata2R/recommendation.md

### 3. Python Landscape
-- Identify any existing equivalent packages in python and export the results to Stata2Python/python-landscape.md
-- do you recommend creating a new python package or contributing these changes to one of the existing packages.
-- Export results to Stata2Python/recommendation.md

### 4. Other Languages.
-- Are there any other relevant target programming languages? 
