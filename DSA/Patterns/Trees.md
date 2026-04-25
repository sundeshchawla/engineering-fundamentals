POSTORDER DFS — BOTTOM UP TEMPLATE

Use when: answer at a node depends on results from both children
          (depth, diameter, path sum, subtree properties)

Pattern:
  1. Base case: return identity value for null node
  2. Recurse left, recurse right — get their results
  3. Compute this node's contribution using left + right
  4. Update global answer (often via a reference/instance variable)
  5. Return what parent needs — NOT necessarily the global answer

The split between step 4 and step 5 is the entire difficulty
of hard tree problems. Always ask: "what does my parent need
vs what is the actual answer at this node?"