# Export Marche Gourmande — 05.11.2026

| Élément | État |
|---|---|
| Produit propriétaire | O-N-2950/marchegourmande |
| Rôle | Hébergement d'un export statique, 52 fichiers dans l'arbre initial |
| GitHub Pages | Activé dans les métadonnées GitHub observées |
| Domaine déclaré | marchegourmande.ch, fichier CNAME |
| Dernière source de l'export | 223b8d141637259f365dc7fad45f347e234e6d1f, 29.06.2026 |
| Build source → export servi | Correspondance non prouvée |
| Nouvelle livraison dans ce lot | Aucune : documentation et rattachement seulement |
| HTTPS observé le 05.11 depuis un hôte NEO | marchegourmande.ch répond 200 ; o-n-2950.github.io aboutit au même domaine, réponse 200 |

L'observation HTTPS établit que le domaine répond et sert du contenu Marche
Gourmande ; elle ne certifie ni le parcours métier ni l'identité exacte du build.
L'hébergement est donc à conserver pendant la qualification du dépôt source.

## Suite à traiter dans le produit propriétaire

1. Relever DNS, réponse HTTPS et version publique réellement servie ; conserver
   les résultats, y compris erreurs réseau, sans les transformer en panne produit.
2. Rendre traçable le build source et l'export exact, sans modifier les bundles à
   la main. L'export de juin ne certifie pas la version actuelle du produit.
3. Mettre à jour depuis le produit source après qualification, ou retirer cet
   hébergement après migration et contrôle du domaine. Ne pas archiver à l'aveugle.

La North Star métier reste celle du dépôt source. Ce dépôt d'artefacts ne crée
pas de second objectif métier ni de pourcentage de readiness indépendant.
