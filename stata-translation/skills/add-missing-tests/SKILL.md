---
name: add-missing-tests
description: Iterates through each file in stata testing directory, summarises matching tests in R, adds missing tests, and summarises again. runs when user askes to "compare tests"
---

1. **Compare**: for each test in each .do file in testing/ compare with matching R test, then ask user if they want to add missing tests
2. **Add missing tests**: For each test that is missing in R add a test using separate file to match the file structure in testing/
3. **Compare**: for each test in each .do file in testing/ compare with matching R test and write a markdown summary document
