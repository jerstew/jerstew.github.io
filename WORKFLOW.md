# Personal AstroPaper Site Workflow - jerstew.github.io

## Current Setup

You have a local clone with:
- **origin**: `https://github.com/jerstew/jerstew.github.io.git` (Your personal site repo)
- **upstream**: `https://github.com/satnaing/astro-paper.git` (Original AstroPaper - for pulling updates)
- **jerstew**: Your customization branch (where your changes live, deployed to your site)
- **main**: Clean copy tracking upstream (for staying in sync with AstroPaper updates)

## Branch Strategy

```
upstream/main (Original AstroPaper)
    ↓ (fetch + merge)
origin/main (Your repo, stays in sync for pulling updates)
    ↓ (rebase or merge)
origin/jerstew (Your customizations - DEPLOYED to jerstew.github.io)
```

## Deployment

Your site is automatically deployed from the `jerstew` branch via GitHub Pages.
- **Live Site**: https://jerstew.github.io
- **Deploy Source**: `jerstew` branch (or configure in repo settings)

## Recommended Workflow

### 1. **Initial Setup** (✅ Already Done!)

Remotes are configured and branches have been pushed to jerstew.github.io. Verify with:
```bash
git remote -v
```

Expected output:
```
origin    https://github.com/jerstew/jerstew.github.io.git (fetch)
origin    https://github.com/jerstew/jerstew.github.io.git (push)
upstream  https://github.com/satnaing/astro-paper.git (fetch)
upstream  https://github.com/satnaing/astro-paper.git (no push)
```

### 2. **Configure GitHub Pages** (One-time setup in repo settings)

Go to https://github.com/jerstew/jerstew.github.io/settings/pages

- **Source**: Deploy from a branch
- **Branch**: `jerstew` (or `main` if you prefer)
- **Folder**: `/ (root)`

Your site will automatically deploy when you push changes to the selected branch.

### 3. **Your Changes Are Safe**

All your work is now in `jerstew` branch on your personal site repo:
```bash
git push origin jerstew  # Push to jerstew.github.io
```

### 3. **Daily Development**

Work on your `jerstew` branch:
```bash
git checkout jerstew
# Make your changes
git add .
git commit -m "Your changes"
git push origin jerstew  # Automatically deploys to jerstew.github.io
```

**Note**: Every push to the `jerstew` branch triggers an automatic deployment.

### 4. **Pulling Updates from AstroPaper**

When the AstroPaper repo updates, follow these steps:

#### Step 1: Fetch upstream changes
```bash
git fetch upstream
```

#### Step 2: Update your main branch with upstream
```bash
git checkout main
git merge upstream/main
git push origin main
```

#### Step 3: Rebase your jerstew branch onto updated main
```bash
git checkout jerstew
git rebase main
git push origin jerstew --force-with-lease
```

**Note**: `--force-with-lease` is safer than `--force` and ensures you don't accidentally overwrite others' work.

#### Alternative: If you prefer merges over rebases
```bash
git checkout jerstew
git merge main
git push origin jerstew
```

### 5. **Handling Merge Conflicts**

If there are conflicts when rebasing/merging:

```bash
# Conflicts will be marked in files
# Edit files to resolve conflicts
git add .
git rebase --continue  # for rebase
# OR
git commit -m "Merge upstream updates"  # for merge
```

## File Organization

**Your customizations are in:**
- `src/styles/global.css` - Windows 2000 Pro theme variables
- `src/styles/components.css` - Component styling
- `src/components/` - Custom component modifications
- `src/layouts/` - Unified page container pattern
- `src/pages/` - All pages using custom layout pattern

**AstroPaper originals:**
- Everything else (watch for conflicts)

## Deployment Recommendation

**Option A: Deploy from your jerstew branch**
```bash
# Set deployment to use jerstew branch
# In your hosting platform (Vercel, Netlify, etc.)
```

**Option B: Merge jerstew into main before deployment**
```bash
git checkout main
git merge jerstew
git push origin main
# Deploy from main
```

## Checking for Updates

To see what's new in upstream:
```bash
git log main..upstream/main --oneline
```

To see what you've changed from upstream:
```bash
git log upstream/main..jerstew --oneline
```

## Quick Reference

| Task | Command |
|------|---------|
| Check status | `git status` |
| Fetch upstream updates | `git fetch upstream` |
| View upcoming changes | `git log main..upstream/main --oneline` |
| Merge upstream to main | `git checkout main && git merge upstream/main` |
| Update jerstew from main | `git checkout jerstew && git rebase main` |
| Push changes | `git push origin jerstew` |
| Create new feature | `git checkout -b feature/my-feature` |

## Tips & Best Practices

1. **Commit message convention**: Use `type: description`
   - `feat:` New feature
   - `refactor:` Code restructuring
   - `style:` CSS/styling changes
   - `fix:` Bug fixes
   - `docs:` Documentation

2. **Keep main clean**: Never work directly on main. Always use feature branches.

3. **Regular syncs**: Fetch upstream regularly to catch conflicts early.

4. **Before major updates**: 
   - Commit all your work
   - Create a backup branch: `git branch backup-jerstew`
   - Then proceed with merge/rebase

5. **Document custom changes**: Keep track of what you've customized so updates don't break your theme.

## Troubleshooting

### I made a mistake, how do I undo?
```bash
git reset --soft HEAD~1  # Undo last commit, keep changes
git reset --hard HEAD~1  # Undo last commit, discard changes
```

### I need to switch branches safely
```bash
git stash  # Save uncommitted changes
git checkout other-branch
git stash pop  # Restore changes on new branch
```

### Upstream has changes I don't want
```bash
git fetch upstream
git log main..upstream/main --oneline  # See what's new
# Then manually review before merging
```

## Your Repository URLs

✅ **All set up!** Here are your remotes:

**Origin (Your personal site repo):**
```
https://github.com/jerstew/jerstew.github.io.git
```

**Upstream (Original AstroPaper for updates):**
```
https://github.com/satnaing/astro-paper.git
```

**Live Site:**
```
https://jerstew.github.io
```

---

**Last Updated**: October 25, 2025
**Your Current Branch**: jerstew
**Deployed**: jerstew branch → GitHub Pages
**Site URL**: https://jerstew.github.io
