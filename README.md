# Explorer creation target QA

Code commit: 17b379e201d211deb8f1d061f7f222de5312cc06
Base: 83ed52669
Environment: macOS arm64, Node 24.19.0, Chromium 145 (Playwright 1.58.2).
Real isolated Paseo daemon and temporary Git projects; no request mocks for the new regression tests.

Before: select src/components, collapse it, use the toolbar to create created-file.
The old code creates at root and leaves components collapsed. The regression fails.
After: the same interaction expands components and creates the entry there.
Both file and folder tests check the real parent directory and absence at root.
The selected-file test creates sibling.txt and sibling-folder beside the selected file.

Commands:

    E2E_RECORD_VIDEO=1 npm run test:e2e --workspace=@getpaseo/app -- e2e/browser/file-explorer-context-actions.spec.ts --grep 'selected collapsed folder' --max-failures=1 --output=/private/tmp/paseo-contribute-red
    E2E_RECORD_VIDEO=1 npm run test:e2e --workspace=@getpaseo/app -- e2e/browser/file-explorer-context-actions.spec.ts --output=/private/tmp/paseo-contribute-final
    npm run typecheck
    npm run lint
    npm run format

Results: old code 1 failed / 1 not run; fixed code 9 passed (53.8s).
Typecheck, lint, formatting, and all commit hooks passed. Raw outputs are included here.

Recordings and frames show only generated test workspaces.
Web was exercised on macOS. Electron desktop, iOS, Android, Windows, and Linux were not exercised.
