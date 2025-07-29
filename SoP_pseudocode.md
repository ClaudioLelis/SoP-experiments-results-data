### High-Level Logic of the SoP Search Controller

The Spectrum of Prompts (SoP) controller is responsible for adaptively exploring prompt variations in order to find the most effective remediation.

The high-level logic operates as follows:

1. **Initialize** the search with a root prompt and set its score as the current best.
2. **While the search tree has capacity:**
   - Select the next prompt node to evaluate.
   - Run the Patch-Compile-Test State Machine (PCT-SM) on this prompt.
   - Compute a quality score `f(x)` for the result.
   - If this score is better than the current best, update the best prompt and its score.
   - Decide whether to explore further by generating two prompt variations:
     - A **concise** version (left branch)
     - A **verbose** version (right branch)
   - Add these new prompts as child nodes in the tree.

3. **Terminate** when the maximum number of prompt nodes is reached or no further improvements are expected.

Each prompt variation is created using controlled meta-prompting strategies and evaluated based on real remediation outcomes. The controller ensures that deeper variations are only explored if justified by the scoring heuristic `f(x)` and within the predefined search budget.

