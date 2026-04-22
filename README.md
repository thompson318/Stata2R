A Claude plugin to aid translation of Stata packages to other software languages. 
The aim is to increase the impact of well written and tested Stata packages by 
translating them to more widely used programming languages. Primarily R and Python. 
The plugin consists of multiple skills that can either be run in isolation or as a 
complete workflow.

# start claude code with path to plugin
claude --plugin-dir $filepath/stata-translation
```

# Strategy

## 1. Start by examining the Stata package and ask whether it is worth translating to R, Python or other languages
```
/stata-translation:translation-strategy
```

## 2. Convert source code to pseudo code. 

[Chen et al. 2026](https://ucl-arc.slack.com/files/U060G4B3M7C/F0ALJ6HE2BW/can_emulating_semantic_translation_help_llms_with_code_translation.pdf) report than translating code through a pseudocode intermediate step results in code that better fits the target langiage idioms, resulting in easier to maintain code. The pseudocode step also supports translating to multiple target langauges.

```
/stata-translation:stata-to-pseudocode
```

```
/stata-translation:pseudocode-to-r
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

Based on https://github.com/ArabelaTso/Skills-4-SE/blob/main/skills/module-level-code-translator/SKILL.md
