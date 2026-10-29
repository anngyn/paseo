# Chat file links and Explorer selection QA

Source commit: 831f00a8e098b9d5a15ab35dd27bb5449006572d

Web Chromium 145 on macOS arm64, Playwright 1.58.2. Real isolated daemon and temporary Git repositories; the supported mock agent provider supplies deterministic chat text. No request interception in these new tests. Electron and native/mobile platforms were not run. Production daemon was untouched.

- Before: source 17b379e20 opens the file tab but leaves Explorer hidden. The regression fails on the visible-tree assertion. before.png is a frame from the unmodified recording after clicking the link.
- After: nested ancestors expand, Files is shown, and the linked row is selected. Hiding hidden files then clicking a hidden sibling reveals and selects it.
- Large tree: 150 preceding files originally leave the selected target outside the rendered window. The fix scrolls it into view, allows manual scrolling, and scrolls back on reopening the same link. A subsequent New file draft remains in view.
- Outside workspace: the real absolute external file opens without changing Explorer visibility or the previous workspace selection.

The combined related specs passed 13 tests (1.4m). The final chat spec passed 4 tests (36.2s), including the consumed-scroll-request change and new-file-draft visibility assertion. Commit hooks passed format, lint and typecheck on the final source. Raw output and videos are included. Earlier successful Explorer creation evidence remains at the branch root.
