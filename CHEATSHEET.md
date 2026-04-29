# Superpowers — Local Fork Cheat Sheet

## Setup

```
~/dev/open-source/superpowers/          ← your fork (editable)
~/dev/zsh-config/ai/skills/             ← symlinked to ~/.cursor/skills
  brainstorming/                        ← symlink → superpowers/skills/brainstorming/
  writing-plans/                        ← symlink → superpowers/skills/writing-plans/
  create-plan/                          ← your own skill (not symlinked)
  ...
```

## Git Remotes

| Remote     | Points to                              |
|------------|----------------------------------------|
| `origin`   | Your fork (`piers109uk/superpowers`)   |
| `upstream` | Original (`obra/superpowers`)          |

## Day-to-Day

### Edit a skill

```bash
cd ~/dev/open-source/superpowers
# edit directly
vim skills/brainstorming/SKILL.md
# commit
git add -A && git commit -m "tweak brainstorming skill"
git push origin main
```

### Pull latest from upstream

```bash
cd ~/dev/open-source/superpowers
git fetch upstream
git merge upstream/main
# resolve any conflicts — your version wins when in doubt
git push origin main
```

### Add a new upstream skill (if obra adds one)

After pulling, symlink the new skill:

```bash
ln -s ~/dev/open-source/superpowers/skills/NEW_SKILL \
      ~/dev/zsh-config/ai/skills/NEW_SKILL
```

### Check symlink health

```bash
for link in ~/dev/zsh-config/ai/skills/*/; do
  name=$(basename "$link")
  if [ -L "${link%/}" ] || [ -L ~/dev/zsh-config/ai/skills/"$name" ]; then
    [ -f "$link/SKILL.md" ] && echo "OK: $name" || echo "BROKEN: $name"
  fi
done
```

## Skills Reference

### Workflow (typical order)

| #  | Skill                           | When                                                     |
|----|---------------------------------|----------------------------------------------------------|
| 1  | **brainstorming**               | Before any creative work — explores intent before code   |
| 2  | **using-git-worktrees**         | Isolate feature work on a new branch                     |
| 3  | **writing-plans**               | Break a spec into bite-sized implementation tasks         |
| 4  | **subagent-driven-development** | Execute plan tasks via subagents in current session       |
| 4b | **executing-plans**             | Execute plan in a separate session with checkpoints       |
| 4c | **dispatching-parallel-agents** | Run 2+ independent tasks concurrently                    |
| 5  | **test-driven-development**     | RED-GREEN-REFACTOR during implementation                 |
| 6  | **requesting-code-review**      | Review work against plan between tasks                   |
| 7  | **finishing-a-development-branch** | Merge/PR/discard when tasks are done                  |

### Supporting

| Skill                            | When                                                          |
|----------------------------------|---------------------------------------------------------------|
| **systematic-debugging**         | Any bug, test failure, or unexpected behavior                 |
| **verification-before-completion** | Before claiming work is done — run checks, show evidence    |
| **receiving-code-review**        | Responding to review feedback with rigor, not blind agreement |

### Meta

| Skill                | When                                                 |
|----------------------|------------------------------------------------------|
| **using-superpowers** | Session bootstrap — makes agent check skills first  |
| **writing-skills**   | Creating or editing skills                           |
