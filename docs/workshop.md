# Workshop on Using Large Language Models to Translate Stata packages to other programming Languages.

## Target Audience
This workshop is aimed at researchers and data scientists familiar with Stata. 

## Workshop Aims
The workshop aims to develop skills in translating code from Stata to other languages. Stata has a significantly smaller user base compared to languages like R and Python, so enabling translation of existing Stata code may lead to greater research impact. 

During the workshop we will translate the code including any grapichical user interfaces, documentation and examples. In addition we will implement support for best practice in open source development, including continuous integration tests and code coverage metrics.  

## Workshop format
This is intended to be run as a 2 to 4 hour workshop where participants will
interactively translate Stata code, discuss the various outputs, and assess the 
suitability of any resulting packages.

During the workshop we will use a Claude Code plugin developed for Stata translation [Stata2R](https://github.com/stata-translations/Stata2R). The plugin 
contains a set of `skills` that guide Claude Code in creating a well structured code translation. We will work through each skill in sequence. As we do this
Claude will prompt for our input and we will discuss what approaches to take. 

Depending on the size of the Stata package to be translated, several of the skills used may take a significant amount of time (~20 minutes) to process. 

## Pre-requisites
Before attending the workshop you should have ... 

### Essential
 - installed Claude Code and have a subscription see [quickstart](https://code.claude.com/docs/en/quickstart)
 - Stata installed [if you're based at UCL](https://swdb.ucl.ac.uk/package/view/id/326)
 - an R installation [r-project](https://www.r-project.org/)
 - a Stata package that you are interested in translating. It doesn't have to be one you wrote, but you should be familiar with what it does. 
 - software version control, we recommend [git](https://git-scm.com/install/). 

### Optional
 - a Python installation [Python](https://www.python.org/downloads/)
 - access to a remote repository for storing source code and running tests, eg. [github](https://www.github.com).
 
## Considerations before the workshop
These are strategy items you should think about before the workshop as they will impact the translation approach. They can be finalised during the workshop. 
 - Is the Stata package currently maintained? Is it likely to be updated in the future?
 - Is there a strategy for on going maintenance or development? e.g. will future changes in the Stata package require porting to the R package or vice versa?
 - Where is the Stata package currently hosted (e.g. github)? Will the translated package be hosted and maintained in the same place (as a sub package) or will we create a new software repository for it?
 - Are we aiming to distribute the new software through existing infrastructire (e.g. CRAN for R, or PyPi for Python).

## During the Workshop

### Setup and Installation
If you haven't already done so, create a local copy of the Stata package you 
intend to work on. Navigate to this directory and start [Claude Code](https://code.claude.com/docs/en/quickstart).

From the Claude Code prompt, install the `stata-translation` plugin.

```
/plugins marketplace add https://github.com/stata-translations/Stata2R.git
/plugin install stata-translation
/reload-plugins
```

You can confirm that this has worked with
```
/stata-translation:hello
```

### Determine the Code Translation Strategy
The first skill we will use will inform our approach for the rest of the session. 
```
/stata-translation:translation-strategy 
```

Claude will write output to the terminal as it works and also should create the following new files recording the results. 

```
Analysis/
└── stata.md
Stata2R
├── recommendation.md
└── r-landscape.md
Stata2Python/
├── python-landscape.md
└── recommendation.md
```

### Stata.md
We start by looking at `stata.md` which contains a summary of the current Stata package. 

#### Important Questions
 - Has Claude provided an accurate summary of what the Stata package does. If not then it may be possible to interactively improve this by prompting Claude.
 - We asked Claude to assess the completeness of the Stata package. A package missing documentation, tests, and examples is going to result in a less accurate translation.
 - You can then look in more detail at the algorithm details to see if Claude has correctly summarised these.

### Stata2R and Stata2Python
We then asked Claude to look at options for code translation. We explicitly 
requested looking at the R and Python languages as these are widely used by 
researchers, but we also asked Claude to recommend other relevant languages.

The `-landscape.md` files summarises what other packages and libraries already 
exist in that ecosystem. 
- If there is already a widely used library that does what our Stata package does then there isn't much point proceeding with the translating the code. 
- Perhaps there is an existing library that we could contribute to rather than creating a new library. 

The `-recommendation.md` files contain Claude's recommendation as to whether we should translate the code and what form any translation should take. Do the recommendations make sense? 

The rest of this workshop assumes that the recommendation was to create a stand alone R package. You may need to tailor the approach based on the recommendations. 

## Translating R code to pseudo code. 
Whether there is an optimal way to perform code translation is currently unknown 
and likely to be specific to a particular use case. Given the rate of change 
in coding agents and the large language models that underpin them it is likely the 
optimal approach will change anyway. 

We have chosen to follow a strategy of converting the Stata code to pseudocode, 
deliberately excluding the test directory and including any documentation/examples.
The pseudocode step is used for three reasons:
 - It has been shown to increase the likelihood of code comprehension, see [Chen et al.](https://doi.org/10.1145/3790101).
 - It enables statisticians without R expertise to review the code before proceeding.
 - It supports the translation to multiple target languages of we elect to do that.

Excluding the test 
directory enables us to use the tests to validate the translation in a subsequent step.  
Run the `stata-to-pseudocode` skill
```
/stata-translation:translation-strategy
```
This skill will create a `pseudocode` directory containing Markdown file/s describing the 
Stata code in pseudocode. Take the time to review this code for correctness before proceeding.

## Pseudocode to R

Run
```
/stata-translation:pseudocode-to-r
```
You should be prompted for a directory location to create the new R-package. You may 
want this to a subdirectory of the current directory, which may be useful if you want to keep
everything in the same repository. Alternatively you can create a separate directory if you 
want to create a new repository for the R package.

The translation will attempt to translate the package code, replace any Stata dialog boxes with 
a R-Shiny GUI, and port any documentation and examples to R. 
A suite of tests should also be generated. Note that these are not based on the original tests from 
the Stata package, but are Claude's own invention. 

Finally the R directory should be populated with infrastructure files to support an opensource package and
submission to CRAN if appropriate.

Explore the R directory structure. Pay particular attention to the vignettes directory which should have 
replicated any usage examples from Stata. Does the package still purport to do what you think it should? 
Start rstudio and see if you can follow the vignette successfully.

The translation should have also created a `.github/workflows` directory. If you host the repository on GitHub these will run automatically each time you push updates to GitHub. Try this now.

## Add in original Stata tests.
In this step we return to the original Stata tests. We can run them from R using the rstata package, and compare their output to those from R. The `add-stata-tests-r` can do this for us.
```
/stata-translation:add-stata-tests-r
```
Depending on where your Stata executable is located Claude may need you help to find it. It is quite likely at this stage that some small errors may be found in the translation, so pay close attention to Claude's output and any prompts.

At the end of the process there should be new tests in the tests directory along with a document named `test-correspondence.md`. Read through the test correspondence document. Are you confident that all the original tests written in Stata have a corresponding test in R? Which tests are missing? 

# Next Steps

You should now have a translation of the Stata package in R. Try using it. Keep a note of any bugs or discrepancies with the Stata package you find. Discuss the process with others and ask questions. 

# Todo

If the recommendation was translate to a different language we could try that. There is a `pseudocode-to-python` skill [here](https://github.com/ArabelaTso/Skills-4-SE/tree/main/skills/pseudocode-to-python-code) which may be a good place to start. 
Agent based coding and code translation is a very fast moving field, so it would be worth reviewing any 
new developments. 


