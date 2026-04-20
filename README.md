A Claude plugin to aid translation of Stata packages to R packages

Based on https://github.com/ArabelaTso/Skills-4-SE/blob/main/skills/module-level-code-translator/SKILL.md

```
# start claude code with path to plugin
claude --plugin-dir $filepath
```

run a specific skill
```
/stata-translation:stata-to-r-translator
```

It took two prompts to get this to work properly 

```
/stata-translation:stata-to-r-translator
#followed by
why did you not follow the instructions in stata-to-r-translator/SKILL.md  
```

There is also a run-stata skill which can be used to create directly comparable tests between stata and R
```
/run-stata testing/artbin_testing_1.do
```
Some coercion may be required to install stata librarys.

``` 
use /run-stata to run testing/artbin_testing_1.do using "ssc install ssi" to add ssi      
  command 
```
and a new test file that compare stata with R
```
use /run-stata to create new R tests to compare r package with niss and ssi results
use rstata within test-artbin-ssi-niss.R to replace hard coded values in expect_equal     
  calls 
update test-correspondence.md now that we have test-artbin-ssi-niss.R
``` 

There is a second skill `stata-to-r-translator_pc` which does the translation step via pseudocode as suggested by [Chen et al. 2026](https://ucl-arc.slack.com/files/U060G4B3M7C/F0ALJ6HE2BW/can_emulating_semantic_translation_help_llms_with_code_translation.pdf). Inspecting the code created shows differences between the two approaches, however these may be unrelated to the pseudocode method.
