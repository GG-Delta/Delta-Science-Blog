#### Once and for all: Save time, engergy and nerves in the long run by controlling different Python versions (using pyenv) and managing virtual environments (using virtualenvwrapper)

**Summary** (Context/Motivation/Problem/Solution)
Most people's computers have multiple Python versions installed (Macs come with Python pre-installed, often termed system Python). Keeping these versions (the pre-installed system Python version and other user-installed Python versions) separate and controlling them independently (e.g. installing or updating a given Python package for a specific Phython version only) requires an upfront solution. Working with virtual environments, i.e. having a separate workspace for each individual project, necessitates actively defining the Python version that will be used to create a specific virtual environment. Controlling Python versions is thus linked to the task of managing virtual environments. All packages installed in a specific virtual environment will not conflict with other virtual environments (all packages being contained in that particular workspace). Following the steps outlined below, your computer should be in a state where different Python versions coexist peacefully and where you can safely install, upgrade, or remove libraries without affecting other projects. In fact, a working setup that is simple to maintain.

**Introduction**

A certainty, especially in the world of programming, is that there are numerous paths to the same destination. 

As a result, there is a plethora of advice available on how to arrive at a working (and hopefully maintainable) setup of a local computer to do data science using Python. 

Speaking from personal experience, I was always too busy doing the actual work to contemplate about the "ideal" setup, so I decided for the moment to ignore any best practices that might exist somewhere. Besides, given the vast amount of information available, determining the right blueprint to follow is not an easy task (just considering the combinatorial nightmare of different operating systems, python versions, installed or assumed pre-installed software, various IDEs etc etc). In short, there are many flying pieces and thus many degrees of freedom, which inevitably leads to complexity.

However, sooner or later the day always comes when you can't afford to ignore the Python setup issue any longer simply because something broke (e.g. after installing a new Python package or upgrading an installed one). From that moment on you will be busy finding a way to continue your work. Sometimes a quick fix is possible (after consulting numerous entries at Stack Overflow or similar websites), but sometimes band-aid is not enough, so that you need a fundamental solution. 

In order to spare you time, research effort and hopefully some nerves I will consicly summarize all steps that resulted into my tested setup. Each step builds on different sources of advice that I will cite along the way (i.e. credits, attribution and thanks are given by explicit references).   

I wrote this summary using macOS (version: 12.6), but you should be able to follow equivalent steps on Linux or Windows (you might need to make some modifications). 

One last word before going into the details: I mentioned the term "fundamental solution" for a reason: in case you got totally lost with quick fixes that resulted in even more problems later on a fresh installation of the operating system is a radical approach. However, it provides a clean start from where you can begin building your new robust setup that is maintainable for all your future projects. I wrote the following lines with a fresh installation of the operating system in mind: 

**Brief overview**

We'll go through three main steps below. The following list is intended to provide you with a high-level overview. Each of the three main steps will be explained in the following paragraphs:

**1.** **Install the *homebrew* package manager** (if you are not sure if you have it check it and eventually update it)

**2.** **Install *pyenv*** (using homebrew)

- a. Running the installation command in the terminal	
- b. Configure your terminal: setup your .zsrh file for pyenv
- c. Using *pyenv* to install a new Python version (in addition to your system Python version)
- d. Switching between the availability of different Python versions

**3.** **Install *virtualenwrapper*** using your system Python version (and its associated pip version)

- a. Running the installation command in the terminal
- b. Configure your terminal to load the *virtualenvwrapper* commands
- c.  Setup a new virtual envrionment on the basis of a specific Python version



---

--- title: "Save time and nerves by controlling different Python versions (*pyenv*) and managing virtual environments (*virtualenvwrapper*)" author: "GG Supp" date: "2022-10-25" categories: [news, code, analysis] image: "image.jpg" format:  html:    code-copy: true draft: true ---

# Summary

Most people's computers have multiple Python versions installed (Macs come with Python pre-installed, often termed system Python). Keeping these versions (the pre-installed system Python version and other user-installed Python versions) separate and controlling them independently (e.g. installing or updating a given Python package for a specific Phython version only) requires an upfront solution. Working with virtual environments, i.e. having a separate workspace for each individual project, necessitates actively defining the Python version that will be used to create a specific virtual environment. Controlling Python versions is thus linked to the task of managing virtual environments. All packages installed in a specific virtual environment will not conflict with other virtual environments (all packages being contained in that particular workspace).

Following the steps outlined here below, your computer should be in a state where different Python versions coexist peacefully and where you can safely install, upgrade, or remove libraries without affecting other projects. In fact, a working setup that is simple to maintain.

# Introduction

A certainty, especially in the world of programming, is that there are numerous paths to the same destination. As a result, there is a plethora of advice available on how to arrive at a working (and hopefully maintainable) setup of a local computer to do data science using Python.

Speaking from personal experience, I was always too busy doing the actual work to contemplate about the "ideal" setup, so I decided for the moment to ignore any best practices that might exist somewhere. Besides, given the vast amount of information available, determining the right blueprint to follow is not an easy task (just considering the combinatorial nightmare of different operating systems, python versions, installed or assumed pre-installed software, various IDEs etc etc). In short, there are many flying pieces and thus many degrees of freedom, which inevitably leads to complexity.

However, sooner or later the day always comes when you can't afford to ignore the Python setup issue any longer simply because something broke (e.g. after installing a new Python package or upgrading an installed one). From that moment on you will be busy finding a way to continue your work. Sometimes a quick fix is possible (after consulting numerous entries at Stack Overflow or similar websites), but sometimes band-aid is not enough, so that you need a fundamental solution.

In order to spare you time, research effort and hopefully some nerves I will consicly summarize all steps that resulted into my tested setup. Each step builds on different sources of advice that I will cite along the way (i.e. credits, attribution and thanks are given by explicit references).

I used the phrase "fundamental solution" above for a reason: in case you got totally lost with quick fixes that resulted in even more problems later on a fresh installation of the operating system is certainly a radical approach. However, it provides a clean start from where you can begin building your new robust setup that is maintainable for all your future projects. I wrote the following lines with a fresh installation of the operating system in mind.

I wrote this summary using macOS (version: 12.6), but you should be able to follow equivalent steps on Linux or Windows (you might need to make some modifications).

# Overview

We'll go through three main steps. The list below is intended to provide you with a high-level overview. Each of the three main steps will be explained in the following paragraphs:

1. **Install the** ***homebrew*** **package manager** (macOS/Linux) (if you are not sure if you have please check and eventually update it: see details below)
2. **Install** ***pyenv*** (using *homebrew*)
   1. Running the installation command in the terminal
   2. Configure your terminal (setup your .zsrh file for *pyenv*)
   3. Using *pyenv* to install a new Python version (in addition to your system Python version)
   4. Switching between the availability of different Python versions

3. **Install** ***virtualenvwrapper*** using your system Python version (and its associated *pip* version)
   1. Running the installation command in the terminal
   2. Configure your terminal to load the *virtualenvwrapper* commands
   3. Setup a new virtual environment on the basis of a specific Python version

# Details

## 1. Install the *homebrew* package manager

As a first step you should install [homebrew](https://brew.sh/) which is a very useful and straightforward package manager (for macOS/Linux). In order to enter the code below open a terminal window (you can do this by opening macOS spotlight - or via your keyboard: just hit both keys *command* plus *space* at once - type "terminal" and open this application).

Now that you have your terminal window open, you can enter the following commands shown below:

## Install homebrew

To install *homebrew* on your computer: paste this command in your terminal window and hit *enter.* After hitting *enter* the script will explain what it will do and then pauses before it does it:

{default} /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

## Check homebrew (installed/version)

To verify and check whether you have *homebrew* already installed you can the following command. In case you have homebrew installed the output will tell you which version it is. If you don't have it installed yet, the output will tell you something like `command not found`.

{default} brew --version 

Example output in case your computer has *homebrew* installed (your version might differ):

{default} Homebrew 3.6.6 Homebrew/homebrew-core (git revision 7ec3c2d24e8; last commit 2022-10-24) Homebrew/homebrew-cask (git revision c3048a8013; last commit 2022-10-24)

## Update homebrew

After having verified that your computer has *homebrew installed*, update it to make sure you have the latest version. Just enter the following command in your terminal window and hit enter [[*](https://docs.brew.sh/FAQ)].

{default}

## 2. Install *pyenv* (via *homebrew*)





-----

Total OLD

--- title: "Save time and nerves by controlling different Python versions (*pyenv*) and managing virtual environments (*virtualenvwrapper*)" author: "GG Supp" date: "2022-10-25" categories: [news, code, analysis] image: "image.jpg" draft: true ---

# Summary

Most people's computers have multiple Python versions installed (Macs come with Python pre-installed, often termed system Python). Keeping these versions (the pre-installed system Python version and other user-installed Python versions) separate and controlling them independently (e.g. installing or updating a given Python package for a specific Phython version only) requires an upfront solution. Working with virtual environments, i.e. having a separate workspace for each individual project, necessitates actively defining the Python version that will be used to create a specific virtual environment. Controlling Python versions is thus linked to the task of managing virtual environments. All packages installed in a specific virtual environment will not conflict with other virtual environments (all packages being contained in that particular workspace).

Following the steps outlined here below, your computer should be in a state where different Python versions coexist peacefully and where you can safely install, upgrade, or remove libraries without affecting other projects. In fact, a working setup that is simple to maintain.

# Introduction

A certainty, especially in the world of programming, is that there are numerous paths to the same destination. As a result, there is a plethora of advice available on how to arrive at a working (and hopefully maintainable) setup of a local computer to do data science using Python.

Speaking from personal experience, I was always too busy doing the actual work to contemplate about the "ideal" setup, so I decided for the moment to ignore any best practices that might exist somewhere. Besides, given the vast amount of information available, determining the right blueprint to follow is not an easy task (just considering the combinatorial nightmare of different operating systems, python versions, installed or assumed pre-installed software, various IDEs etc etc). In short, there are many flying pieces and thus many degrees of freedom, which inevitably leads to complexity.

However, sooner or later the day always comes when you can't afford to ignore the Python setup issue any longer simply because something broke (e.g. after installing a new Python package or upgrading an installed one). From that moment on you will be busy finding a way to continue your work. Sometimes a quick fix is possible (after consulting numerous entries at Stack Overflow or similar websites), but sometimes band-aid is not enough, so that you need a fundamental solution.

In order to spare you time, research effort and hopefully some nerves I will consicly summarize all steps that resulted into my tested setup. Each step builds on different sources of advice that I will cite along the way (i.e. credits, attribution and thanks are given by explicit references).

I used the phrase "fundamental solution" above for a reason: in case you got totally lost with quick fixes that resulted in even more problems later on a fresh installation of the operating system is certainly a radical approach. However, it provides a clean start from where you can begin building your new robust setup that is maintainable for all your future projects. I wrote the following lines with a fresh installation of the operating system in mind.

I wrote this summary using macOS (version: 12.6), but you should be able to follow equivalent steps on Linux or Windows (you might need to make some modifications).

# Overview

We'll go through three main steps. The list below is intended to provide you with a high-level overview. Each of the three main steps will be explained in the following paragraphs:

1. **Install the** ***homebrew*** **package manager** (macOS/Linux) (if you are not sure if you have please check and eventually update it: see details below)
2. **Install** ***pyenv*** (using *homebrew*)
   1. Running the installation command in the terminal
   2. Configure your terminal (setup your .zsrh file for *pyenv*)
   3. Using *pyenv* to install a new Python version (in addition to your system Python version)
   4. Switching between the availability of different Python versions

3. **Install** ***virtualenvwrapper*** using your system Python version (and its associated *pip* version)
   1. Running the installation command in the terminal
   2. Configure your terminal to load the *virtualenvwrapper* commands
   3. Setup a new virtual environment on the basis of a specific Python version

# Details

## 1. Install the *homebrew* package manager

As a first step you should install [homebrew](https://brew.sh/) which is a very useful and straightforward package manager (for macOS/Linux). In order to enter the code below open a terminal window (you can do this by opening macOS spotlight - or via your keyboard: just hit both keys *command* plus *space* at once - type "terminal" and open this application).

Now that you have your terminal window open, you can enter the following commands shown below:

## Install homebrew

To install *homebrew* on your computer: paste this command in your terminal window and hit *enter.* After hitting *enter* the script will explain what it will do and then pauses before it does it:

{default} /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

## Check homebrew (installed/version)

To verify and check whether you have *homebrew* already installed you can the following command. In case you have homebrew installed the output will tell you which version it is. If you don't have it installed yet, the output will tell you something like `command not found`.

{default} brew --version 

Example output in case your computer has *homebrew* installed (your version might differ):

{default} Homebrew 3.6.6 Homebrew/homebrew-core (git revision 7ec3c2d24e8; last commit 2022-10-24) Homebrew/homebrew-cask (git revision c3048a8013; last commit 2022-10-24)

## Update homebrew

After having verified that your computer has *homebrew installed*, update it to make sure you have the latest version. Just enter the following command in your terminal window and hit enter [[*](https://docs.brew.sh/FAQ)].

{default}

## 2. Install *pyenv* (via *homebrew*)