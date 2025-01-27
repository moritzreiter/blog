---
title: "Config for New Angular Project"
date: 2025-01-27T16:49:59+01:00
---

Some configuration steps I want to remember for setting up a new Angular
project.

Create a new project:

```shell
ng new my-project --defaults
```

Omit the `--defaults` option to interactively choose some configuration options.

## Prettier

Angular automatically adds an `.editorconfig`. Open it and add

```ini
max_line_length = 80
```

Install and configure prettier:

```shell
npm install --save-dev prettier prettier-plugin-organize-imports
```

Create `.prettierrc` in the project root and add:

```json
{
  "plugins": ["prettier-plugin-organize-imports"]
}
```

Prettier will pick up the `.editorconfig` and thus formats everything with a
maximum line length of 80 characters when applied, [which is objectively how it
should be](https://laprade.blog/80-char-line-limit).

Format everything with prettier:

```shell
npx prettier . --write
```

Open the IntelliJ IDEA settings, go to _Langugages & Frameworks / JavaScript /
Prettier_ (or just search for _prettier_) and activate _Automatic Prettier
configuration_, so that the Prettier configuration from the project gets used
for code formatting. Also, on the same settings page, add `css` and `html` to
the file types in the _Run for files_ input field.

## ESLint

Install ESLint:

```shell
ng add @angular-eslint/schematics --skip-confirmation
```

And make IntelliJ IDEA aware of it by navigating to the settings at _Languages &
Frameworks / JavaScript / Code Quality Tools / ESLint_ and choosing _Automatic
ESLint configuration_. Now ESLint errors get reported right in the editor.

