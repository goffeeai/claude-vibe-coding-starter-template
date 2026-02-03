# Git Workflow

## Basic Commands

```bash
# Clone repo
git clone https://github.com/user/repo.git

# Check status
git status

# Add files
git add .                    # All files
git add file.txt             # Specific file
git add src/                 # Specific folder

# Commit
git commit -m "message"

# Push
git push origin main

# Pull
git pull origin main
```

---

## Branching

```bash
# Create branch
git checkout -b feature/login

# Switch branch
git checkout main
git checkout feature/login

# List branches
git branch          # Local
git branch -r       # Remote
git branch -a       # All

# Delete branch
git branch -d feature/login        # Local
git push origin --delete feature/login  # Remote
```

---

## Common Workflows

### Feature Branch Workflow

```bash
# 1. Create feature branch
git checkout main
git pull origin main
git checkout -b feature/new-feature

# 2. Make changes and commit
git add .
git commit -m "Add new feature"

# 3. Push feature branch
git push origin feature/new-feature

# 4. Create Pull Request on GitHub

# 5. After merge, cleanup
git checkout main
git pull origin main
git branch -d feature/new-feature
```

### Hotfix Workflow

```bash
# 1. Create hotfix from main
git checkout main
git pull origin main
git checkout -b hotfix/urgent-fix

# 2. Fix and commit
git add .
git commit -m "Fix critical bug"

# 3. Push and merge quickly
git push origin hotfix/urgent-fix
# Create PR and merge

# 4. Cleanup
git checkout main
git pull origin main
git branch -d hotfix/urgent-fix
```

---

## Commit Messages

### Format
```
<type>: <description>

[optional body]
```

### Types
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation
- `style`: Formatting (no code change)
- `refactor`: Code restructure
- `test`: Tests
- `chore`: Maintenance

### Examples
```bash
git commit -m "feat: add user authentication"
git commit -m "fix: resolve login redirect issue"
git commit -m "docs: update API documentation"
git commit -m "refactor: simplify database queries"
```

---

## Undo Changes

### Unstage files
```bash
git reset HEAD file.txt
git reset HEAD .
```

### Discard changes
```bash
git checkout -- file.txt    # Specific file
git checkout -- .           # All files
```

### Undo commit
```bash
# Keep changes
git reset --soft HEAD~1

# Discard changes
git reset --hard HEAD~1
```

### Amend commit
```bash
# Change message
git commit --amend -m "new message"

# Add forgotten files
git add forgotten-file.txt
git commit --amend --no-edit
```

---

## Stash

```bash
# Save current changes
git stash

# Save with message
git stash save "work in progress"

# List stashes
git stash list

# Apply last stash
git stash pop

# Apply specific stash
git stash apply stash@{1}

# Delete stash
git stash drop stash@{0}
```

---

## Merge vs Rebase

### Merge
```bash
# Merge feature into main
git checkout main
git merge feature/login

# Creates merge commit
# Preserves complete history
```

### Rebase
```bash
# Rebase feature onto main
git checkout feature/login
git rebase main

# Linear history
# Cleaner but rewrites history
```

### When to use what?
- **Merge**: Shared branches, preserve history
- **Rebase**: Personal branches, clean history

---

## Tags

```bash
# Create tag
git tag v1.0.0
git tag -a v1.0.0 -m "Version 1.0.0"

# Push tag
git push origin v1.0.0
git push origin --tags

# List tags
git tag

# Delete tag
git tag -d v1.0.0
git push origin --delete v1.0.0
```

---

## .gitignore

```gitignore
# Dependencies
node_modules/
vendor/

# Environment
.env
.env.local
.env.*.local

# Build
dist/
build/
.next/
.nuxt/

# IDE
.vscode/
.idea/

# OS
.DS_Store
Thumbs.db

# Logs
*.log
logs/

# Local
*.local.md
```

---

## Tips

1. **Commit often** - เล็กและบ่อย
2. **Write good messages** - อธิบายสิ่งที่ทำ
3. **Pull before push** - หลีกเลี่ยง conflicts
4. **Use branches** - แยก feature แยก branch
5. **Review before commit** - `git diff`
6. **Don't commit secrets** - ใช้ .gitignore
