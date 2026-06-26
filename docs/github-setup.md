# GitHub Setup

The public repository already exists at:

```text
https://github.com/an-thony350/FractalScope
```

Use these commands from the folder containing this public dossier.

## If You Have Not Cloned the GitHub Repo Locally

```bash
cd ~/Documents
git clone https://github.com/an-thony350/FractalScope.git
cd FractalScope

cp -r /path/to/FractalScope-public/. .

git add README.md docs assets .gitignore
git commit -m "Create public FractalScope technical dossier"
git push
```

## If You Already Have a Local Empty Repo

```bash
cd ~/Documents/FractalScope

cp -r /path/to/FractalScope-public/. .

git add README.md docs assets .gitignore
git commit -m "Create public FractalScope technical dossier"
git push -u origin main
```

## Files to Keep Public

- `README.md`
- `docs/`
- `assets/logo.png`
- `assets/system_diagram.png`
- `assets/simple_mandelbrot_set_visual.jpeg`
- `assets/number-format/`
- `.gitignore`

## Files Not to Add

- `fpga/rtl/`
- `fpga/tb/`
- `fpga/v*_release/`
- `ps/`
- `controller/`
- `notebooks/`
- `.github/workflows/`
- generated Vivado artefacts
- bitstreams / HWH files
- full report PDF unless redacted and approved by teammates

