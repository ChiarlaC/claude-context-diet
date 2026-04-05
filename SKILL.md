# claudeignore

Generate optimized `.claudeignore` files to reduce token usage and costs in AI coding assistants.

## What it does

Creates a `.claudeignore` file in your project root to prevent Claude Code from loading unnecessary files (node_modules, build artifacts, etc.). This can reduce token consumption by 90%+ in large projects.

## Usage

```bash
/claudeignore [template]
```

**Examples:**
- `/claudeignore` - Auto-detect project type and generate
- `/claudeignore nextjs` - Generate for Next.js project
- `/claudeignore python` - Generate for Python project
- `/claudeignore go` - Generate for Go project

## Available Templates

- `nextjs` - Next.js/React projects
- `react` - React (CRA, Vite) projects
- `vue` - Vue.js projects
- `python` - Python projects with pip/poetry
- `go` - Go projects
- `rust` - Rust projects
- `node` - Generic Node.js projects
- `full` - Comprehensive template (all common patterns)

---

**Step 1: Detect Project Type**

First, analyze the project structure to determine the framework/language:

<bash>
ls -la
</bash>

Look for key indicators:
- `package.json` → Check for next/react/vue in dependencies
- `requirements.txt` or `pyproject.toml` → Python
- `go.mod` → Go
- `Cargo.toml` → Rust

**Step 2: Choose Base Template**

Based on detection, select the appropriate template. If user specified a template, use that instead.

**Step 3: Generate .claudeignore**

Create the `.claudeignore` file with the selected template. Use the templates below:

## Templates

### Next.js / React
```
# Dependencies
node_modules/
.pnp/
.pnp.js

# Build outputs
.next/
out/
build/
dist/

# Cache
.cache/
.turbo/
.swc/

# Testing
coverage/

# Environment
.env*.local

# Logs
*.log
logs/

# OS
.DS_Store
Thumbs.db

# IDE
.vscode/
.idea/
*.swp
*.swo

# Package manager
.yarn/
.pnpm-store/
package-lock.json
yarn.lock
pnpm-lock.yaml

# Media & Static Assets
*.png
*.jpg
*.jpeg
*.gif
*.svg
*.ico
*.webp
*.woff
*.woff2
*.ttf
*.eot
*.mp4
*.mp3
*.webm
public/images/
public/videos/
assets/images/
```

### Python
```
# Virtual environments
venv/
env/
ENV/
.venv/

# Python cache
__pycache__/
*.py[cod]
*$py.class
.pytest_cache/

# Distribution
dist/
build/
*.egg-info/
.eggs/

# Testing
.coverage
htmlcov/
.tox/

# Jupyter
.ipynb_checkpoints/
*.ipynb

# Environment
.env
.env.local

# Logs
*.log

# IDE
.vscode/
.idea/
*.swp

# OS
.DS_Store

# Media & Static Assets
*.png
*.jpg
*.jpeg
*.gif
*.svg
*.ico
*.webp
static/images/
media/
```

### Go
```
# Binaries
*.exe
*.exe~
*.dll
*.so
*.dylib
bin/

# Test coverage
*.out
coverage.txt

# Go workspace
go.work
go.work.sum

# Vendor
vendor/

# IDE
.vscode/
.idea/
*.swp

# OS
.DS_Store

# Logs
*.log

# Media & Static Assets
*.png
*.jpg
*.jpeg
*.gif
*.svg
*.ico
*.webp
static/
public/
```

### Rust
```
# Build outputs
target/
Cargo.lock

# Backup files
**/*.rs.bk

# IDE
.vscode/
.idea/
*.swp

# OS
.DS_Store

# Logs
*.log

# Media & Static Assets
*.png
*.jpg
*.jpeg
*.gif
*.svg
*.ico
*.webp
static/
assets/
```

### Generic Node.js
```
# Dependencies
node_modules/

# Build
dist/
build/

# Logs
*.log
logs/

# Environment
.env
.env*.local

# OS
.DS_Store
Thumbs.db

# IDE
.vscode/
.idea/
*.swp

# Media & Static Assets
*.png
*.jpg
*.jpeg
*.gif
*.svg
*.ico
*.webp
*.woff
*.woff2
*.ttf
public/
static/
assets/images/
```

### Full (Comprehensive)
```
# Dependencies
node_modules/
vendor/
.pnp/

# Build outputs
dist/
build/
out/
.next/
target/
*.egg-info/

# Cache
.cache/
.turbo/
.swc/
__pycache__/

# Virtual environments
venv/
.venv/
env/

# Package manager locks
package-lock.json
yarn.lock
pnpm-lock.yaml
Cargo.lock

# Testing
coverage/
.coverage
.pytest_cache/
*.test
*.out

# Logs
*.log
logs/

# Environment
.env
.env*.local

# IDE
.vscode/
.idea/
*.swp
*.swo

# OS
.DS_Store
Thumbs.db

# Git
.git/

# Media & Static Assets
*.png
*.jpg
*.jpeg
*.gif
*.svg
*.ico
*.webp
*.woff
*.woff2
*.ttf
*.eot
*.mp4
*.mp3
*.webm
*.pdf
public/
static/
assets/images/
media/
uploads/
```

**Step 4: Calculate Savings**

After creating the file, estimate token savings by checking sizes of major ignored directories:

<bash>
du -sh . 2>/dev/null && echo "---" && du -sh node_modules .next target build dist venv __pycache__ 2>/dev/null | head -10
</bash>

Calculate percentage based on directory sizes. Present results:
```
✅ Created .claudeignore with [template] template

📊 Estimated Impact:
- Ignored directories: ~XXX MB (node_modules, build outputs, etc.)
- Total project size: ~XXX MB
- Estimated exclusion: ~XX% of project
- Token savings: ~90-95% per conversation
- Cost savings: ~$15-20 per 1M tokens

💡 Tip: Run 'claude --refresh' to apply changes to current session.
```

**Important:** Never use `find . -type f` as it can timeout on large projects with millions of files. Always use `du -sh` on specific directories instead.

**Step 5: Offer Customization**

Ask if user wants to:
- Add custom patterns
- Exclude specific directories
- See what files will still be included

## Example Output

```
✅ Created .claudeignore for Next.js project

📊 Impact:
- 15,847 files excluded (node_modules, .next, etc.)
- ~450 MB removed from context
- Estimated 92% token reduction
- Save ~$18 per 1M tokens

💡 Your conversations will now be faster and cheaper!

Would you like to:
1. Add custom ignore patterns
2. Review what's still included
3. Done
```

## Notes

- Always create in project root (where package.json/go.mod/etc. exists)
- If `.claudeignore` exists, ask before overwriting
- Suggest reviewing with `cat .claudeignore` after creation
- For mono-repos, consider multiple .claudeignore files in subdirectories
