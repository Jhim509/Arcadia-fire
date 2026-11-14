# Zone Zéro : battle royale 3D (solo contre bots)

## Structure

```
zone-zero/
  index.html        le jeu (moteur complet, à régler dans CFG, en haut du script)
  assets/           à créer vous-même, facultatif
    player.glb      votre personnage
    bot.glb         personnage des bots
    map.glb         une carte complète (remplace le sol vert)
```

Sans fichier dans `assets/`, le jeu utilise des personnages low poly construits dans le code.

## Ajouter vos personnages et votre carte

- Formats acceptés : `.glb` (conseillé), `.fbx` (avec squelette et animations) et `.obj` (forme seule, sans animation).
- Noms cherchés : `player`, `bot`, `map` avec l'une de ces extensions, à la racine du dépôt ou dans `assets/`.
- Le modèle est redimensionné automatiquement à 1,8 m de haut et posé au sol, face vers +Z.
- S'il contient des animations, celle qui s'appelle « run » ou « walk » (sinon la première) joue quand le personnage bouge.
- Utilisez des modèles que vous avez créés, achetés avec licence ou téléchargés sur des sites libres de droits. Ne reprenez pas ceux de Free Fire ou d'autres jeux.
- Pour un gros jeu (300 Mo ou plus), compressez les textures et utilisez des modèles en Draco ou meshopt si possible, sinon le chargement sera long sur mobile.

## Tester chez vous

Les modules et les `.glb` ne se chargent pas en ouvrant le fichier directement. Lancez un petit serveur :

```
cd zone-zero
python3 -m http.server 8000
```

Puis ouvrez http://localhost:8000

## Mettre en ligne

Déposez le dossier `zone-zero` (avec `assets/`) chez un hébergeur de sites statiques : itch.io (type « HTML »), GitHub Pages, Netlify, Cloudflare Pages ou autre. Vérifiez la limite de taille de l'hébergeur choisi. Les joueurs téléchargent le jeu dans leur navigateur à la première partie.

Le jeu charge Three.js depuis le CDN jsDelivr. Pour fonctionner hors ligne ou sans dépendance externe, copiez les fichiers Three.js dans votre dossier et changez l'`importmap`.

## Réglages (CFG)

Nombre de bots, taille de la carte, vitesse et durée de la zone, dégâts : tout est dans l'objet `CFG`.

## Limites de cette version

- Solo contre bots : pas de multijoueur en ligne (il faudrait un serveur de jeu, par exemple Node.js avec WebSocket).
- Une seule arme, pas de loot ni de véhicules.
- Les balles sont bloquées par les arbres et les bâtiments, mais pas par leur hauteur : on ne peut pas tirer par-dessus.
- Non testé sur plusieurs appareils : vérifiez la fluidité sur votre téléphone et baissez `bots` ou `obstacles` si besoin.

## Carte de ville (map.glb)

`map.glb` (16 Mo) est une ville de 400 m sur 400 m, textures 2048 px, recentrée sur l'origine. Le jeu la charge automatiquement s'il la trouve à la racine ou dans `assets/`, crée les collisions à partir des bâtiments, bloque les balles derrière les murs et fait apparaître les joueurs dans les rues. Sans `map.glb`, le jeu génère un terrain avec des arbres et des blocs.
Envoyez `map.glb` avec « Téléverser des fichiers » (limite d'environ 25 Mo par fichier dans le navigateur).
Crédits : voir `CREDITS.md`.
