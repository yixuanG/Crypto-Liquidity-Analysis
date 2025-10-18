# GitHub Setup Guide

This document guides you through publishing this project to GitHub.

## Pre-Publication Checklist

### ✅ Already Completed
- [x] Project structure reorganized
- [x] Old files archived in `_archive/`
- [x] `.gitignore` configured to exclude data
- [x] `README.md` created with comprehensive documentation
- [x] `requirements.txt` added with dependencies
- [x] `LICENSE` file added (MIT License)
- [x] `CHANGELOG.md` documenting all changes
- [x] `CONTRIBUTING.md` for collaboration guidelines
- [x] `.gitattributes` for proper file handling

### ⚠️ Before Publishing - Action Required

1. **Review Notebooks for Sensitive Information**
   ```bash
   # Check all notebooks for:
   # - Personal information
   # - API keys or passwords
   # - Absolute paths that reveal your directory structure
   # - Email addresses (unless you want them public)
   
   grep -r "password\|api_key\|secret" notebooks/
   ```

2. **Update README.md with Your Information**
   - Add your name and contact information
   - Add your institution name
   - Add your GitHub username to the clone URL
   - (Optional) Add links to your LinkedIn, personal website

3. **Review and Test Archive**
   ```bash
   # Verify _archive is gitignored
   git status | grep _archive
   # Should return nothing
   
   # Check archive size
   du -sh _archive/
   # Note: Archive is ~1GB+ and won't be uploaded
   ```

4. **Optional: Add Sample Data or Examples**
   - Consider adding small sample datasets
   - Or add screenshots of expected outputs
   - Update README with where to get data

## Step-by-Step GitHub Publication

### 1. Initialize Git Repository

```bash
cd "/Users/ivan/FSFM/01_Courses/2nd Semester/Financial Management/Crypto_Liquidity"

# Initialize git (if not already)
git init

# Check git status
git status
```

### 2. Review What Will Be Committed

```bash
# See what will be included
git add --dry-run .

# Verify data files are ignored
git status | grep -i "csv\|xlsx\|png"
# Should see: "nothing to commit" or only show .gitignore entries
```

### 3. Make Initial Commit

```bash
# Add all files (data excluded by .gitignore)
git add .

# Check what's staged
git status

# Make initial commit
git commit -m "Initial commit: Cryptocurrency Liquidity Analysis project

- Complete analysis pipeline from data processing to statistical analysis
- 10 well-documented Jupyter notebooks
- Comprehensive README and documentation
- Organized by workflow stages (event filter → analysis)
- Excludes proprietary data (gitignored)
"
```

### 4. Create GitHub Repository

**Option A: Via GitHub Website**
1. Go to https://github.com/new
2. Repository name: `Crypto-Liquidity-Analysis`
3. Description: "Analysis of cryptocurrency market liquidity response to major events"
4. Choose: Public (for showcase) or Private
5. **DO NOT** initialize with README (you already have one)
6. Click "Create repository"

**Option B: Via GitHub CLI** (if installed)
```bash
gh repo create Crypto-Liquidity-Analysis --public --source=. --remote=origin
```

### 5. Push to GitHub

```bash
# Add remote (use URL from GitHub)
git remote add origin https://github.com/YOUR_USERNAME/Crypto-Liquidity-Analysis.git

# Verify remote
git remote -v

# Push to GitHub
git branch -M main
git push -u origin main
```

### 6. Verify Upload

1. Go to your repository on GitHub
2. Check that:
   - ✅ README displays properly
   - ✅ No CSV/data files are present
   - ✅ All notebooks are in `notebooks/` directory
   - ✅ `_archive/` is not present (gitignored)
   - ✅ Documentation files are readable

## Post-Publication

### Add Repository Description & Topics

On GitHub repository page:
1. Click ⚙️ (settings icon) next to "About"
2. Add description: "Quantitative analysis of cryptocurrency liquidity response to major economic, regulatory, and technical events using high-frequency trading data"
3. Add topics/tags:
   - `cryptocurrency`
   - `liquidity`
   - `financial-markets`
   - `event-study`
   - `python`
   - `jupyter-notebook`
   - `quantitative-finance`
   - `market-microstructure`

### Optional: Add README Badges

Add to top of README.md:
```markdown
![Python](https://img.shields.io/badge/python-3.8+-blue.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)
![Status](https://img.shields.io/badge/status-active-success.svg)
```

### Optional: Create GitHub Pages

If you want a website for your project:
1. Go to repository Settings → Pages
2. Source: Deploy from branch → main → /docs
3. Create a `docs/` folder with `index.md`

### Optional: Add Screenshots

Create `images/` folder with:
- Sample workflow diagram
- Example visualizations
- Results screenshots

Update README to include:
```markdown
## Sample Results
![Sample Visualization](images/sample_chart.png)
```

## Maintenance

### Updating the Repository

```bash
# Make changes
git add <files>
git commit -m "Description of changes"
git push

# Or update all
git add .
git commit -m "Update analysis with new findings"
git push
```

### Creating Releases

For significant milestones:
```bash
# Tag a release
git tag -a v1.0.0 -m "First complete version"
git push origin v1.0.0

# Create release on GitHub
# Go to Releases → Draft a new release
# Select tag → Add release notes
```

## Troubleshooting

### Problem: Data files accidentally committed

```bash
# Remove from git (keep local file)
git rm --cached <filename>.csv

# Update .gitignore if needed
echo "<pattern>" >> .gitignore

# Commit the change
git commit -m "Remove data file from tracking"
git push
```

### Problem: Repository too large

```bash
# Check size
du -sh .git

# If too large, check what's tracked
git ls-files | grep -E "csv|png|xlsx"

# Remove large files from history (use with caution)
# git filter-branch --tree-filter 'rm -rf path/to/large/files' HEAD
```

### Problem: Merge conflicts

```bash
# Pull latest changes first
git pull origin main

# Resolve conflicts
# Edit files, then:
git add <resolved-files>
git commit
git push
```

## Security Best Practices

- ✅ Never commit API keys or passwords
- ✅ Never commit proprietary data without permission
- ✅ Review each commit before pushing
- ✅ Use `.gitignore` liberally
- ✅ Consider using `.env` files for sensitive config (add to .gitignore)

## Sharing Your Project

### For Your Portfolio
- Add link to resume/CV
- Add to LinkedIn projects section
- Include in personal website portfolio

### For Academic Purposes
- Share with professors and peers
- Include in course assignments (if allowed)
- Reference in research papers

### For Job Applications
- Demonstrate coding skills
- Show data analysis capabilities
- Highlight quantitative research experience

## Resources

- [GitHub Docs](https://docs.github.com/)
- [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)
- [Markdown Guide](https://www.markdownguide.org/)
- [Jupyter Notebook Best Practices](https://jupyter-notebook.readthedocs.io/)

---

**Ready to publish?** Follow the steps above and showcase your work! 🚀

