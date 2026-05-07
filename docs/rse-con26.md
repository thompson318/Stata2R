## Title

Code Translation using Large Language Models: What's the role Research Software Engineer?

## Abstract
[250 words.]: #
Translating research code to other programming language enables
 researchers to reach beyond their own domain, increasing research impact and 
guarding against software obsolescence.
Translation requires skills in the source and target language, and the research domain making it unlikely
 that any individual will be able to perform translation.
Large language models (LLM) support translation by amalgamating language and domain specific knowledge from many sources.
RSEs play a role in this by implementing best practice methods and providing validation tools.

We will discuss our experiences in developing a Clause Code plugin that supports domain
experts in statistics in translating Stata packages to R and Python.  
The plugin implements 4 skills;
1. Analyse and plan: Is the package well documented? Which target language(s)? Create a new library or contribute to an existing library?
1. Translation to pseudocode: Translate to pseudocode to support human review without language expertise. Excludes any existing tests.  
1. Pseudocode to target language(s): Translate; add infrastructure to support ongoing opensource development (CI testing, contributing guidelines, licenses)  
1. Tests and documentation: Implement any existing Stata tests in target language; summarise test correspondence; highlight missing tests. Review documentation (examples, papers), and translate to target language (eg. Vignettes in R)  
 
We used the plugin in workshops with statisticians to translate a selection of Stata 
packages. We will discuss our experiences in code translation and compare our results with existing research in code translation. We aim to provoke informed discussion about the role of RSEs and LLMs in code translation.

## Prerequisates
[150 words.]: #
The talk/poster will focus on general software engineering methods so should be comprehensible to 
most participants at RSECon. 
We assume no knowledge of the programming languages used, nor the inner workings of the 
LLMs used for translation. The interest is in the developer and user experience of using large 
language models for translation.

## Outcomes
[150 words.]: #
Use of coding agents built on large language models is becoming an integral part of the 
research software engineering process. This talk aims to present a disinterested review of
our experience, collating not just our experiences but also the experiences of our users. 
Whilst seeking to avoid giving simple answers to complex questions, the talk will contribute
 to participants understanding of the ever evolving role of research software engineering.

