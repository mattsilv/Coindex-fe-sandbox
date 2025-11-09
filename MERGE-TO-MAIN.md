# Merge Instructions for Main Branch

## Current Status

All work is on branch: `claude/photo-capture-component-011CUxmRSRAeZNcvqxDNNDza`

This branch contains:
- ✅ Complete photo upload component
- ✅ Client-side metadata stripping
- ✅ Full documentation
- ✅ Privacy requirements
- ✅ Component specifications

## To Merge to Main (From Another Machine)

### Option 1: Direct Merge
```bash
# Clone the repo (if not already cloned)
git clone https://github.com/mattsilv/Coindex-fe-sandbox.git
cd Coindex-fe-sandbox

# Fetch all branches
git fetch --all

# Create main branch from the claude branch
git checkout -b main claude/photo-capture-component-011CUxmRSRAeZNcvqxDNNDza

# Push to main
git push -u origin main
```

### Option 2: Merge via Pull Request
1. Go to: https://github.com/mattsilv/Coindex-fe-sandbox
2. Click "Pull Requests" → "New Pull Request"
3. Base: `main` (create if needed)
4. Compare: `claude/photo-capture-component-011CUxmRSRAeZNcvqxDNNDza`
5. Create and merge the PR

### Option 3: GitHub Web UI
1. Go to: https://github.com/mattsilv/Coindex-fe-sandbox
2. Click on the branch dropdown
3. Click "View all branches"
4. Find `claude/photo-capture-component-011CUxmRSRAeZNcvqxDNNDza`
5. Click "..." → "Set as default branch" (if you want)
6. Or rename the branch to `main` in settings

## After Merging

### Update GitHub Pages
1. Go to Settings → Pages
2. Change source branch from `claude/...` to `main`
3. Save
4. Wait 1-2 minutes for deployment
5. Verify at: https://mattsilv.github.io/Coindex-fe-sandbox/

### Clean Up (Optional)
```bash
# Delete the claude branch (if you want)
git branch -d claude/photo-capture-component-011CUxmRSRAeZNcvqxDNNDza
git push origin --delete claude/photo-capture-component-011CUxmRSRAeZNcvqxDNNDza
```

## What's Included

### Files
- `index.html` - Photo upload component (live demo)
- `photo-capture-mockup.html` - Original mockup (reference)
- `README.md` - Project overview and guide
- `COMPONENT-01-UPLOAD.md` - Upload component spec (10 numbered requirements)
- `PRIVACY-REQUIREMENTS.md` - Privacy feature technical documentation
- `MERGE-TO-MAIN.md` - This file

### Commits
```
e9f7ec4 Add comprehensive component documentation
1e4c57b Add client-side metadata stripping for privacy protection
cc8152f Make upload flow flexible for single or multiple coins
e4fad8d Update photo capture to show obverse and reverse sides
a8be788 Add index.html for GitHub Pages
908de91 Add photo capture component HTML mockup
```

## Next Steps After Merge

1. **Component 2: Photo Editor**
   - Create `COMPONENT-02-EDITOR.md`
   - Build crop/rotate functionality
   - Keep as separate HTML file for now

2. **Component 3: AI Analysis & Review**
   - Create `COMPONENT-03-REVIEW.md`
   - Display AI results
   - Allow user corrections

3. **Component 4: Metadata Entry**
   - Create `COMPONENT-04-METADATA.md`
   - Form for coin details
   - Validation

4. **Component 5: Catalog View**
   - Create `COMPONENT-05-CATALOG.md`
   - Grid of all coins
   - Search/filter

## Questions?

See README.md for full project documentation.

All requirements are numbered in COMPONENT-01-UPLOAD.md for easy reference.
