## 2026-10-04 - Prevent Input Box Disappearance
**Learning:** In VS Code extensions, input boxes for external data (like tokens or URLs) disappear when the user switches apps to copy the data, leading to a frustrating UX where the user loses their progress.
**Action:** Always add `ignoreFocusOut: true` to `vscode.window.showInputBox` when prompting for data that a user is likely to retrieve from an external source, such as a browser.
