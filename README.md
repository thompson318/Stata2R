A Claude plugin to aid translation of Stata packages to other software languages. 
The aim is to increase the impact of well written and tested Stata packages by 
translating them to more widely used programming languages. Primarily R and Python. 
The plugin consists of multiple skills that can either be run in isolation or as a 
complete workflow.

# Installation
```
/plugins marketplace add https://github.com/stata-translations/Stata2R.git
/plugin install stata-translation
/reload-plugins
```

# Translation

## 1. Examine the Stata package.
```
/stata-translation:translation-strategy
```

## 2. Convert Stata code to pseudo code. 

```
/stata-translation:stata-to-pseudocode

## 3. Pseducode To R
```
/stata-translation:pseudocode-to-r
```

## 4. Confirm test correspondence
```
/stata-translation:add-stata-tests-r
```
