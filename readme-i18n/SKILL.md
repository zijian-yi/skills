---
name: readme-i18n
description: Use when the user wants to translate a README into a new language, sync existing translated READMEs after the original changes, or manage multilingual README files in a repository.
---

# README i18n

Keep translated READMEs in sync with the main README. Supports creating new translations and updating existing ones when the original changes.

## Two Modes

| Mode | Trigger | What happens |
|------|---------|--------------|
| **Create** | "translate README to Japanese", "add Chinese README" | Translate the full main README into a new language |
| **Sync** | "sync READMEs", "update translations" | Diff the main README, update only changed sections in each translation |

## Workflow

### Step 0: Detect files and conventions

1. Find the main README — the one without a language suffix (usually `README.md`)
2. Glob for other files with "README" in the name to discover existing translations
3. Infer the naming pattern from existing translations (e.g., `README.zh.md`, `README-ja.md`, `README_fr.md`)
4. If no translations exist yet and you're creating one, ask the user what naming convention to use

### Step 1: Determine mode

If the user asked to add/translate a new language → **Create mode**
If the user asked to sync/update → **Sync mode**
If ambiguous, ask.

---

## Create Mode

### Step 2c: Read and translate

1. Read the main README in full
2. Confirm the target language with the user if not already clear
3. Translate the entire document, preserving:
   - All markdown formatting, headings, and structure
   - Code blocks unchanged (do not translate code)
   - Links and URLs unchanged
   - Image references unchanged
   - Badge URLs unchanged

### Step 3c: Preview and write

1. Show the user the full translated README
2. Ask for approval before writing
3. Write the file using the detected (or chosen) naming convention

---

## Sync Mode

### Step 2s: Identify changes

1. Use `git diff` on the main README to find what changed
   - First try: diff against the commit when translations were last modified
   - Fallback: diff against HEAD~1, or ask the user for the commit range
2. Summarize the changes to the user (e.g., "Sections 'Installation' and 'Usage' were updated, 'FAQ' section was added")

### Step 3s: Update each translation

For each translated README:

1. Read the translated file
2. Identify sections that correspond to the changed parts of the main README
3. Translate only the changed/added sections
4. **Preserve language-specific content** — any sections in the translation that don't have a counterpart in the main README must be left untouched
5. For deleted sections: remove the corresponding translated section, but flag this to the user

### Step 4s: Preview and write

For each translated file:

1. Show the user what will change (original vs proposed, or a clear summary of edits)
2. Ask for approval before writing
3. Apply the edits only after approval

Repeat for each translation. Do not batch — handle one file at a time.

---

## Translation Guidelines

When translating:

- **Do not translate**: code blocks, terminal commands, CLI flags, variable names, URLs, file paths, brand names, project names
- **Do translate**: prose, headings, list items (descriptive text), comments in code only if they are part of the explanation
- **Preserve tone**: match the original's tone (formal/informal, technical level)
- **Use conventional terminology**: prefer established translations for technical terms in the target language (e.g., use the standard term for "pull request" in that language's developer community, even if it's the English word)

## Important Rules

- **Always preview before writing.** Never write a translated file without showing the user first.
- **Preserve language-specific extras.** Sections in a translation that don't exist in the main README are intentional — do not remove them during sync.
- **No hardcoded naming patterns.** Detect from existing files. If no pattern exists, ask.
- **One file at a time during sync.** Present changes per file, get approval, then move to the next.
- **Code blocks are sacred.** Never translate content inside code fences.
