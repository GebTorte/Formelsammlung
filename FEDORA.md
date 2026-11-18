# FEDORA

## .bashrc
```bash
# .bashrc

# Source global definitions
if [ -f /etc/bashrc ]; then
    . /etc/bashrc
fi

# User specific environment
if ! [[ "$PATH" =~ "$HOME/.local/bin:$HOME/bin:" ]]; then
    PATH="$HOME/.local/bin:$HOME/bin:$PATH"
fi
export PATH

# Uncomment the following line if you don't like systemctl's auto-paging feature:
# export SYSTEMD_PAGER=

# User specific aliases and functions
if [ -d ~/.bashrc.d ]; then
    for rc in ~/.bashrc.d/*; do
        if [ -f "$rc" ]; then
            . "$rc"
        fi
    done
fi
unset rc

echo "Hi from .bashrc"

# git access key 
ssh-add ~/.ssh/keyname

# config ldpath
export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/usr/local/lib:/usr/local/lib64"

# signal setup
alias signal='~/SignalApp/signal-desktop.AppImage'
echo "start Signal app by >signal"

# saga gis
echo "to start saga gis"
echo ">saga_gui &"

# pdf compression GS
# gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dPDFSETTINGS=/ebook \
#-dNOPAUSE -dQUIET -dBATCH -sOutputFile=output.pdf input.pdf
# 
#Summary of -dPDFSETTINGS:
 #   -dPDFSETTINGS=/screen lower quality, smaller size. (72 dpi)
 #   -dPDFSETTINGS=/ebook for better quality, but slightly larger pdfs. (150 dpi)
 #   -dPDFSETTINGS=/prepress output similar to Acrobat Distiller "Prepress Optimized" setting (300 dpi)
 #   -dPDFSETTINGS=/printer selects output similar to the Acrobat Distiller "Print Optimized" setting (300 dpi)
 #   -dPDFSETTINGS=/default selects output intended to be useful across a wide variety of uses, possibly at the expense of a larger output file

# add r to path
export PATH="$PATH:/usr/bin/R"

```

## AMD Ryzen GPU setup
> sudo dnf install rocm  // or rocm-devel 

## QGIS
### custom venv
#### install

// use system python version!!!
//> uv python pin 3.14 (use sytem )
//> uv sync


> uv add scipy scikit-learn
> uv add torch torchvision --index https://download.pytorch.org/whl/rocm10.0 

// reset index to default
> uv sync --default-index https://pypi.org/simple

> uv add geopandas pyproj shapely
> uv add remotior-sensus

##### set system site packages
toggle flat in .venv/pyvenv.cfg to true:
include-system-site-packages = true

// NOTE:

### Launch qgis from this python venv to enable SCP (semi-automatic classification plugin) toolkit
> source .venv/bin/activate
> qgis