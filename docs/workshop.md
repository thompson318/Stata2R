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

We start by looking at `stata.md` which contains a summary of the current Stata package. 
