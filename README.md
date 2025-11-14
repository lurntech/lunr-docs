# Lunr Documentation

This is a documentation site built with [Zensical](https://zensical.org) - a modern static site generator by the creators of Material for MkDocs.

## 🚀 Setup

### Windows (PowerShell)
```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
pip install --upgrade pip
pip install -r requirements.txt
```

### Unix/Linux/Mac
```bash
bash setup.sh
```

## Development

Serve the documentation locally:
```bash
zensical serve -f zensical.toml
```

Access at http://localhost:8000

## Build

Build the static site:
```bash
zensical build
```

## Deploy

Deploy to GitHub Pages:
```bash
zensical gh-deploy
```

## About Zensical

Zensical is fully compatible with Material for MkDocs configurations, providing:

- ⚡ **Faster builds** - Built with Rust for performance
- 🎨 **Modern design** - Clean, professional interface
- 🔧 **Full compatibility** - Drop-in replacement for MkDocs
- 🚀 **Active development** - Regular updates and improvements
