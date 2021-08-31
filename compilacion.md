
# Generación de HTML

## Compilación local de la documentación

Documentación y dispositivas:

    [conda activate dai]
    [cd docs]
    make

Sin diapositivas:

    [conda activate dai]
    [cd docs]
    make html & make open

Paso a paso:

    [conda activate dai]
    cd slides
    make
    cd ../docs
    make slides
    make html
    make open

## Subir al repo

    [git add newfiles]
    [cd docs]
    make push

## Subir páginas estáticas

    [cd docs]
    make clean && make push && make && make pages
    [git checkout master]

## Instalación de miniconda

    conda=Miniconda3-latest-Linux-x86_64.sh 
    curl -O https://repo.anaconda.com/miniconda/$conda
    bash $conda

## Configuración del entorno

    conda create --name dai python=3.7.7
    conda activate dai
    conda install -c conda-forge pandoc=2.9.2.1
    python -m pip install sphinx==3.0.3 sphinx_rtd_theme==0.4.3
    conda deactivate
