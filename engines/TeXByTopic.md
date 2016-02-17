# Tex By Topic Notes

## Chapter1: The Structure of the TeX Processor

Chapter: Global Picture of the way the TeX processor operates.

### Four TeX Processors

TeX Processing is split into four separate units;
each acceptiong the output of the previous stage,
and delivering the input for the next stage:

* Input processor (tokenizer):
    * Input: `.tex` file
    * Output: tokens (character tokens, control sequenze tokens)
* Expansion processor (Substitution?):
    * Input: stream of tokens
    * output: stream of tokens
    * Some but not all the tokens generated in the first level
      (macros, conditionals, a number of primitive TeX commands)
      are subject to expansion.
      Expansion is the process that replaces some (sequences of tokens)
      by other (or no tokens).
* Execution processor:
    * input: 
    * output:
    * Control sequences that are not expandable are executable,
      this execution takes place on the third level of the TeX processor.
      two things happening at this stage:
      * Changes to TeX's internal state.
        example: assignments (including macro definitions)
      * construction of horizontal, vertical, mathematical lists.
* Visual processor:
      * Horizontal lists are broken into paragraphes
      * Vertical lists are broken into pages
      * formulas are build out of math mode. 


