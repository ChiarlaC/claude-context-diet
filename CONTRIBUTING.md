# Contributing to Claudeignore Skill

First off, thank you for considering contributing! 🎉

## How to Contribute

### 🐛 Report Bugs

Open an issue with:
- Project type (Next.js, Python, etc.)
- Command you ran
- Expected vs actual behavior
- Console output

### 💡 Suggest Features

We'd love to hear ideas for:
- New framework templates
- Better pattern matching
- Performance improvements

### 🔧 Submit Pull Requests

1. Fork the repo
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Test your changes (see [TEST-GUIDE.md](./TEST-GUIDE.md))
4. Commit with clear messages
5. Push to your fork
6. Open a Pull Request

### 📝 Add New Templates

To add a framework template:

1. Add to `SKILL.md` under `## Templates`
2. Follow this structure:
```
### Framework Name
```
# Dependencies
<package_directories>

# Build outputs
<build_directories>

# Media & Static Assets
*.png
*.jpg
*.jpeg
*.gif
*.svg
*.ico
*.webp

# Logs, cache, etc.
```
```

3. Add detection logic in Step 1
4. Test on a real project

### ✅ Code Standards

- **Safety first:** Never use `find . -type f` (can timeout)
- **Always include media filters:** `*.png`, `*.jpg`, etc.
- **Error handling:** Use `2>/dev/null` for commands
- **Performance:** Commands should complete in <1 second

## Development Setup

```bash
# Clone your fork
git clone https://github.com/ChiarlaC/claudeignore-skill.git
cd claudeignore-skill

# Create test project
mkdir test-project
cd test-project
echo '{"name":"test"}' > package.json

# Test the skill logic manually
du -sh . 2>/dev/null
```

## Testing

See [TEST-GUIDE.md](./TEST-GUIDE.md) for comprehensive testing instructions.

Quick validation:
```bash
# Check for media filters
grep -c "*.png" SKILL.md  # Should be 6+

# Check for dangerous commands
grep "find . -type f" SKILL.md  # Should only appear in warnings
```

## Questions?

Feel free to open a discussion on GitHub.

---

**Happy contributing!** 🚀
