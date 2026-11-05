# Marche Gourmande — export public GitHub Pages

Ce dépôt contient l'export statique public de **Marche Gourmande**.
Le produit, son code source et sa feuille de route appartiennent à
[O-N-2950/marchegourmande](https://github.com/O-N-2950/marchegourmande).

Le domaine déclaré dans `CNAME` est `marchegourmande.ch`. Les fichiers `_next/`,
HTML, icônes, manifest et service worker sont des artefacts déployés ; ne pas
développer une deuxième application ni modifier manuellement ces bundles.

Le rattachement est aussi déclaré dans le registre de portefeuille de NEO Core.
La dernière modification fonctionnelle de cet export remonte au 29.06.2026,
source du dépôt d'export `223b8d141637259f365dc7fad45f347e234e6d1f`.

## Livraison

Une mise à jour doit provenir d'un build du dépôt source qualifié, avec sa
version et sa preuve de correspondance vers cet export. La présence d'un
fichier `api/health` statique ne prouve pas la santé d'une API ni d'une base.
La configuration GitHub Pages et le CNAME ne suffisent pas à prouver le
routage DNS actuel ou la disponibilité du domaine.

Conserver l'hébergement tant que la cible du domaine et la procédure de
remplacement ne sont pas vérifiées. Aucun retrait de site n'est autorisé
par le seul constat d'ancienneté ou de petite taille du dépôt.

[État et prochaines actions](docs/PROGRESS.md).
