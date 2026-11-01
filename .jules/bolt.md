## 2024-10-03 - Cache validation regular expressions
**Learning:** Instantiating `RegExp` objects inside tight loops for file parsing degraded language server responsiveness.
**Action:** Caching validation regexes and manually resetting `lastIndex = 0` prior to `.exec()` avoids the expensive recompilation of the same regex over and over. Make sure to reset `lastIndex` when using global regexes to prevent state leakage across loop iterations.
