---
id: 2025-11-04-add-ds_store-to-global-gitignore
aliases: []
tags: []
---

# Add .DS_Store to Your Global .gitignore

`.DS_Store` is a macOS Finder metadata file that shouldn’t be committed. Add it
to your global `.gitignore` so it’s ignored in all repositories.

## 1) Create or open your global ignore file

  ```bash
  touch ~/.gitignore_global
  ```

## 2) Tell Git to use it (if not already)

```bash    
  git config --global core.excludesfile ~/.gitignore_global
  ```

## 3) Add the pattern

Open the file and add:
```text
.DS_Store
```

Optional additional macOS patterns:
```text
.AppleDouble
.LSOverride
Icon?
.Spotlight-V100
.Trashes
```

## 4) Clean existing tracked .DS_Store files (per repo)

If any repos already track `.DS_Store`, run inside each repo:

```bash
git rm --cached -r .DS_Store
git commit -m "Remove .DS_Store from version control"
```

That’s it `.DS_Store` will be ignored across all your Git repositories.
