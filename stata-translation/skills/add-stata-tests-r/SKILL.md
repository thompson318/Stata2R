---
name: add-stata-tests-r
description: Iterates through each file in stata testing directory, summarises matching tests in R, adds missing tests, and summarises again. runs when user askes to "compare tests"
---

Locate a Stata executable
Using the rstata package write tests to compare results in Stata with R package results; 
1. for each test in each .do file in testing/ run with rstata and compare with a matching R test
2. Write a test summary file describing how the stata tests correspond with R tests.
3. Alert the user to any missing tests.
---
