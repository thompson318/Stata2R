## Title

Code Translation using Large Language Models: What's the role Research Software Engineer?

## Abstract
[250 words.]: #
Code translation may significantly enhance the research impact of existing code by making the code accessible to a greater range of researchers.
Language choice is usually influenced by research domain, so the ability to port code written in one language to another may enable researchers to reach new users outside their own research domain.
Translation requires skills in the source and target language, and the research domain.
The combination of skills required makes it unlikely that an individual researcher or RSE will be able to perform code translation.
Large language models (LLM) can support translation between languages by amalgamating language and domain specific knowledge from many sources.
Research software engineers play a role in this by implementing best practice methods in translation and providing tools to validate the resulting code. 

We will discuss our experiences in developing a plugin for Claude Code to enable domain
experts in statistics to translate code written in Stata to R and Python packages.  
The plugin implements 4 skills that the user implements in sequence;
1. Analyse and plan: Is the package well enough documented and tested to support translation? Which language(s) to target? Create a new library or contribute to an existing library?
1. Translation to pseudocode: Intermediate translation to pseudocode to support human review without expertise in target language(s). This translation deliberately excludes any existing tests.  
1. Translation from pseudocode target language(s): Translate to the target language; add infrastructure to support ongoing opensource development (CI testing, contributing guidelines, review licenses)  
1. Port tests and documentation: Review existing Stata tests, implement in target language, and summarise test correspondce. Highlight any missing tests. Review Stata documentation (examples, papers), and translate to suitable format in target lanuguage (eg. Vignettes in R)  
 
We used the plugin in a workshop with statisticians to translate a selection of Stata 
packages. We will discuss our experiences in code translation and compare our results with the growing research body in this area. We aim to provoke informed discussion about the role of RSEs and LLMs in code translation.

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

