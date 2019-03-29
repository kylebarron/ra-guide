---
author: Kyle Barron
title: Code as Programs
---

## Introduction

When learning to code, you might start off just entering lines of code directly into a [REPL](../glossary.md#repl). After a while, you learn that entering code directly into such a console is lacking in reproducibility. You might arrive at a final dataset but not remember all the commands needed to recreate it. This is why it's important for code to be written in files.

Still, many researchers write code linearly at the top level of the script, like the following:
```stata
// Example script as top-level code
// Load example dataset
sysuse auto, clear
// Run commands that modify data in memory
histogram mpg
regress price mpg
```

I prefer to write in terms of _programs_ — pieces of reusable code inside larger files — for two reasons:

- Ability to reuse code without copying and pasting
- Better mental segmentation

!!! note
    This document will explain programs in the context of Stata, but most of the context here transfers to writing programs in other languages like R, Python, or Julia.

## What are programs?

Programs are named pieces of code within a file. For example, you might rewrite the simple example above as:

```stata
// Example script as program
program summarize_data
    // Load example dataset
    sysuse auto, clear
    // Run commands that modify data in memory
    histogram mpg
    regress price mpg
end
```

The code to describe the `auto` dataset is now contained in the `summarize_data` command. This means that to run the code you'd type `summarize_data` at the Stata prompt, similar to any built-in program.

### What's wrong with copy and paste?

Let's say that in addition to seeing how `mpg` impacts price, you also wanted to describe how `weight` and `length` impact price. The "simplest" solution to that is to copy and paste the top-level code twice, replacing `mpg` with `weight` and with `length` in the two copies.

But then if you decide you want to change the histogram to a scatter plot, or add fixed effects to the regression, you'd need to make sure to remember to change each instance of the code. That's really easy to forget.

Programs help because they're _abstractions_. You can write the code once and easily modify it to run with any sort of combinations you'd like.


### The `syntax` command

The `syntax` command lets programs take _parameters_, or starting values.

```stata
program summarize_data
    // Store parameter
    syntax, independent_var(str)

    display "The independent variable is `independent_var'"
    histogram `independent_var'
    regress price `independent_var'
end
```



### `main`

If all the code in a file is contained in programs, then when the file is run in Stata, the programs are only _defined_, and not _called_. The way to fix this is to define one master program that calls all other programs, then on the last line of the file, . Traditionally this is called `main`.

```stata
program main
    summarize_data, independent_var(mpg)
    summarize_data, independent_var(weight)
    summarize_data, independent_var(length)
end
```

### Dual duty script and program

Explain `if main`.


## Full example

```stata
args __name__
version 13
clear all
set more off
set varabbrev off
capture log close _all

program main
    summarize_data, independent_var(mpg)
    summarize_data, independent_var(weight)
    summarize_data, independent_var(length)
end

program summarize_data
    // Store parameter
    syntax, independent_var(str)

    display "The independent variable is `independent_var'"
    histogram `independent_var'
    regress price `independent_var'
end

if ("`__name__'" == "__main__") {
    main, email cap noi
}
```

## Helpful Tips

- In my own code, I always use `capture program drop` on the line before a program starts. This helps with debugging because Stata won't let you redefine a program that already exists. Instead you must first clear the program definition from memory and then define it again from scratch.

    For example
