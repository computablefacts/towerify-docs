# Towerify docs

Cette repo contient la documentation de Towerify.

Elle est écrite dans des fichiers en MarkDown et elle est générée grâce à [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/getting-started/).

## Modifier la documentation en local

Commencer, bien sûr, par cloner cette repo.

``` bash
git clone https://github.com/computablefacts/towerify-docs.git
```

Installer Material for MkDocs (MkDocs nécessite python `v3.x`) :

``` bash
pip install mkdocs-material
```

Lancer le serveur pour voir la documentation dans son navigateur :

``` bash
mkdocs serve
```

Si tout se passe bien, MkDocs affiche ceci :

``` bash
INFO    -  Building documentation...
INFO    -  Cleaning site directory
INFO    -  Documentation built in 0.47 seconds
INFO    -  [23:06:06] Watching paths for changes: 'docs', 'mkdocs.yml'
INFO    -  [23:06:06] Serving on http://127.0.0.1:8000/
```

Accéder à l'URL affichée dans son navigateur permet de voir la documentation.

Si on affiche une page de la doc dans son navigateur et qu'on modifie le fichier correspondant
de la doc depuis son IDE, la page du navigateur se met à jour au fur et à mesure sans avoir
besoin de la rafraîchir.

Pratique si on possède deux écrans : IDE pour modifier la doc sur le premier et navigateur pour 
voir les modifications sur le deuxième.
