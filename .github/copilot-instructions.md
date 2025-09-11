# HERE WEX INFRA CHINA STATIC - Development Instructions

Always reference these instructions first and fallback to search or bash commands only when you encounter unexpected information that does not match the info here.

## Project Overview

HERE WEX INFRA CHINA STATIC is a static HTML/CSS/JavaScript website showcasing HERE's automotive and mapping solutions for the Chinese market. The site consists of three main pages: homepage, digital cockpit showcase, and blog article template.

## Working Effectively

### Bootstrap and Setup
- Install validation tools: `npm install -g htmlhint csslint`
- No build process required - this is a pure static website
- No package.json, dependencies, or compilation steps needed

### Local Development Server
- Start local server: `cd [repo-root] && python3 -m http.server 8080`
- Access at: `http://localhost:8080`
- Server starts in ~1 second - NEVER CANCEL
- Test all pages load: `curl -s -o /dev/null -w "%{http_code}" http://localhost:8080/index.html` (should return 200)

### File Structure
```
.
├── index.html           # Homepage with hero and feature sections
├── digital-cockpit.html # Product showcase page  
├── blog.html           # Blog article template
├── styles.css          # Single stylesheet for all pages
├── main.js            # Modal functionality JavaScript
└── src/               # Static assets directory
    ├── logo.svg       # HERE logo
    ├── hero.jpg       # Homepage hero image
    └── feature.jpg    # Homepage feature image
```

### Validation and Quality Checks
- Validate HTML: `htmlhint *.html` - takes ~1 second, should show "no errors found"
- Validate CSS: `csslint styles.css` - takes ~1 second, expect 38 style warnings (non-critical)
- Check all pages load: `for page in index.html digital-cockpit.html blog.html; do echo "Testing $page: $(curl -s -o /dev/null -w '%{http_code}' http://localhost:8080/$page)"; done`
- NEVER CANCEL validation commands - they complete in under 5 seconds

## Known Issues and Limitations

### Missing Assets
- `src/blog-image.jpg` - referenced in blog.html but file does not exist
- `src/digital-cockpit.jpg` - referenced in digital-cockpit.html but file does not exist
- Site functions normally despite missing images (will show broken image icons)

### JavaScript Function Mismatch
- HTML pages call `openMarketoModal()` but main.js defines `openModal()`
- Contact buttons on index.html will not work due to this mismatch
- Modal functionality works correctly on digital-cockpit.html and blog.html pages

### CSS Warnings
- csslint reports 38 warnings (alphabetical order, unknown properties like 'gap', qualified headings)
- All warnings are style-related, not functional errors
- Site displays and functions correctly despite warnings

## Validation Scenarios

### Complete Manual Testing
Always perform these validation steps after making changes:

1. **Start Development Server**
   - `cd [repo-root] && python3 -m http.server 8080`
   - Wait ~1 second for "Serving HTTP on" message

2. **Test All Pages Load**
   - Navigate to `http://localhost:8080/` - should show HERE homepage
   - Navigate to `http://localhost:8080/digital-cockpit.html` - should show Digital Cockpit page  
   - Navigate to `http://localhost:8080/blog.html` - should show Blog template
   - All navigation links should work between pages

3. **Test Interactive Elements**
   - On digital-cockpit.html: click "Contact Us" button - modal should appear
   - On blog.html: click "Contact Us" button - modal should appear  
   - On index.html: click contact buttons - will NOT work (known issue)
   - Modal close button should work on pages where modal appears

4. **Validate Assets**
   - Check logo displays on all pages
   - Check hero.jpg displays on homepage
   - Check feature.jpg displays on homepage
   - Expect broken images on digital-cockpit.html and blog.html (missing assets)

## Development Workflow

### Making Changes
1. Edit HTML/CSS/JS files directly - no compilation needed
2. Refresh browser to see changes immediately  
3. Run validation: `htmlhint *.html && csslint styles.css`
4. Test manual scenarios listed above
5. Always verify navigation between all three pages works

### Common Tasks
- **Add new page**: Create .html file, add CSS styles, update navigation in existing pages
- **Modify styles**: Edit styles.css directly, refresh browser
- **Fix JavaScript**: Edit main.js, ensure function names match HTML onclick attributes  
- **Add images**: Place in src/ directory, reference as `src/filename.jpg` in HTML

### Time Expectations
- Validation commands: ~1-2 seconds each - NEVER CANCEL
- Server startup: ~1 second - NEVER CANCEL  
- Page refresh: Immediate
- No build or compilation time - changes are instant

## File Contents Reference

### Repository Root Listing
```
ls -la [repo-root]:
total 36
drwxr-xr-x 4 runner runner 4096 Sep 11 10:11 .
drwxr-xr-x 3 runner runner 4096 Sep 11 10:10 ..
drwxrwxr-x 7 runner runner 4096 Sep 11 10:11 .git
-rw-rw-r-- 1 runner runner 1467 Sep 11 10:11 blog.html
-rw-rw-r-- 1 runner runner 2166 Sep 11 10:11 digital-cockpit.html  
-rw-rw-r-- 1 runner runner 2165 Sep 11 10:11 index.html
-rw-rw-r-- 1 runner runner  714 Sep 11 10:11 main.js
drwxrwxr-x 2 runner runner 4096 Sep 11 10:11 src
-rw-rw-r-- 1 runner runner 4001 Sep 11 10:11 styles.css
```

### Available Assets
```
ls -la src/:
total 1644
drwxrwxr-x 2 runner runner   4096 Sep 11 10:11 .
drwxr-xr-x 4 runner runner   4096 Sep 11 10:11 ..
-rw-rw-r-- 1 runner runner 833716 Sep 11 10:11 feature.jpg
-rw-rw-r-- 1 runner runner 833716 Sep 11 10:11 hero.jpg  
-rw-rw-r-- 1 runner runner   1868 Sep 11 10:11 logo.svg
```

## Critical Reminders
- This is a static site - NO build process exists or is needed
- Changes are immediately visible after browser refresh
- Python HTTP server is the recommended local development approach
- Always test all three pages after making changes
- Contact functionality has known issues on homepage (JavaScript mismatch)
- Missing image assets are expected - site functions despite broken images
- All validation commands complete in under 5 seconds - NEVER CANCEL