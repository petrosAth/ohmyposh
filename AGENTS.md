# Oh My Posh package

The deployable configuration at `.config/ohmyposh` is an independent Git submodule containing one prompt configuration per shared theme.

## Theme contracts

- Prompt files are named `<theme>.omp.json`; Zsh resolves them from `${SYSTEM_THEME}`.
- Keep each prompt theme paired with its local `.nvim/palettes/<theme>.lua` editing palette.
- New or renamed themes must remain consistent with `theme/AGENTS.md` and the other shared-theme consumers.
- Preserve the Oh My Posh schema declaration and the existing prompt, transient-prompt, palette, and block structure.
- Follow `.editorconfig`: JSON uses two-space indentation and a 120-column maximum. Do not manually normalize unrelated theme files.

## Repository boundary

Commit configuration work inside `.config/ohmyposh` before updating the parent dotfiles gitlink. Preserve any existing nested work.

## Verification

```sh
for file in .config/ohmyposh/*.omp.json; do jq empty "$file" || exit; done
oh-my-posh debug --config .config/ohmyposh/gruvbox.omp.json >/dev/null
git -C .config/ohmyposh status --short
```
