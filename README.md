# Site de Rempart de Miel

Le petit site du jeu, prévu pour https://theochuzeville-create.github.io (dépôt GitHub `theochuzeville-create.github.io`). Rien n'est encore en ligne.

## Contenu

- `index.html` : présentation en français ; `en/index.html` : la même en anglais.
- `confidentialite.html` et `en/privacy.html` : politique de confidentialité (adresse à donner à la Play Console).
- `app-ads.txt` : la ligne AdMob, qui doit rester à la racine du site.
- `.nojekyll` : GitHub Pages sert les fichiers tels quels.
- `style.css` : clair et sombre selon le téléphone, aucune ressource externe.
- `images/` : l'icône 192 px et six captures réduites (432 px de large), tirées de `jeu-abeilles/captures/`.

## Avant la mise en ligne

- L'adresse de contact est theochuzeville@gmail.com, sur toutes les pages.
- Une fois le jeu publié, mettre le lien Play Store à l'endroit repéré par le commentaire `LIEN PLAY STORE` (FR) et `PLAY STORE LINK` (EN).
- Quand le nom anglais sera choisi, le mettre dans `en/` (commentaire `ENGLISH NAME TO BE CHOSEN`).
- Si le jeu change sa façon de traiter les données (classement en ligne, par exemple), mettre à jour les deux politiques et leur date avant la sortie de la version.

## Publication (plus tard)

Le jeton GitHub est déposé par Théo avec `ssh -t … /srv/theo/perso/outils/deposer-cle.sh github`, qui l'écrit dans `/srv/theo/config/github.env` (variable `GITHUB_TOKEN`, chmod 600). Il ne s'affiche jamais, ne va ni dans ce dossier ni dans git.

Première fois (le dépôt `theochuzeville-create.github.io` doit exister sur GitHub, public, branche `main`) :

```bash
cd /srv/theo/perso/creations/site-rempart-de-miel
git init -b main
git add -A && git commit -m "Site de Rempart de Miel"
set -a; source /srv/theo/config/github.env; set +a   # le fichier n'a pas d'export
git -c credential.helper= \
    -c "credential.helper=!f() { echo username=x-access-token; echo password=\$GITHUB_TOKEN; }; f" \
    push https://github.com/theochuzeville-create/theochuzeville-create.github.io.git main
```

Le jeton passe par un assistant d'identification ponctuel : il n'est écrit ni dans l'URL, ni dans `.git/config`, ni dans l'historique. Pour les mises à jour suivantes, même commande `push` après un `git commit`.

Ensuite, dans GitHub, Settings > Pages : source « Deploy from a branch », branche `main`, dossier `/`. Le site répond en général en une ou deux minutes.

## Vérifications après la mise en ligne

- https://theochuzeville-create.github.io/app-ads.txt affiche la ligne AdMob, en texte brut.
- https://theochuzeville-create.github.io/confidentialite.html et `/en/privacy.html` s'ouvrent sans connexion à un compte.
- Dans la Play Console, le champ « Site Web » de la fiche doit être exactement `https://theochuzeville-create.github.io` : AdMob cherche `app-ads.txt` à la racine de ce domaine. La vérification dans AdMob peut prendre jusqu'à 24 heures après la publication du jeu.
