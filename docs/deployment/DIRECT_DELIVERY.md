# Livraison directe — export public GitHub Pages

## Périmètre et autorité

Ce dépôt contient un export statique de Marche Gourmande. Il contient des fichiers HTML, les ressources Next.js générées, les icônes, le manifeste PWA et le service worker. L'application source est `O-N-2950/marchegourmande` ; le lien est documenté dans la [PR existante no 1](https://github.com/O-N-2950/O-N-2950.github.io/pull/1). Cette PR n'est pas intégrée à `dev` au moment de l'inspection. Aucun bundle généré n'est modifié par cette mise à jour de gouvernance. Les preuves disponibles ne permettent pas d'affirmer que le domaine client sert actuellement cet export Pages.

La décision ADP-019 1.4.0 remplace l'attente de NEO CI et de la fusion préalable. Les portes locales, l'isolation du canari, les accords pour les domaines sensibles et la preuve du SHA servi restent obligatoires. Un hébergement ou un résultat inconnu ne vaut pas autorisation de bascule.

## Hébergement observé

Inspection : 12.11.2026 à 06:07:27 (Europe/Zurich ; 05:07:27 UTC).

| Élément | Preuve ou limite |
| --- | --- |
| Hébergement configuré de l'export | GitHub Pages : dépôt `has_pages=true`, quatre exécutions « pages build and deployment » sur `main` ; la cible réellement servie par le domaine reste à réconcilier |
| Dernière exécution Pages observée | Succès sur `a375f62982bea502c46110bb774fb96ce9369a14` ; cela ne prouve pas à lui seul le SHA servi sur le domaine client |
| Domaine déclaré | `marchegourmande.ch`, fichier `CNAME` inchangé |
| Nœuds | Aucun identifiant de nœud Jelastic pour cet export ; GitHub Pages ne fournit pas le modèle `ROOT` de la procédure Jelastic |
| Réglage de source Pages | Lecture directe refusée par le connecteur GitHub : endpoint `/pages` non autorisé (HTTP 400). Les exécutions observées sont toutes sur `main`, aucune sur `dev` ; réglage exact à vérifier |
| Railway | Projet `4cd80bfd-8292-4592-a36b-c4435711639d` (`marchegourmande`), environnement production `eac068bc-e709-496e-8116-bcdece316727` : aucun service ; un volume PostgreSQL détaché. Aucun service de production ni déclenchement `dev` à changer dans ce projet |
| Santé dans l'export Git | `api/health` contient seulement `status`, `service` et `mode: static`. Aucun SHA. `/health` absent de l'arbre inspecté |
| Santé sur le domaine client | GET le 12.11.2026 à 06:09:11 Europe/Zurich (05:09:11 UTC) : `https://marchegourmande.ch/health` → HTTP 404 ; `/api/health` → HTTP 200 `application/json`, `status: ok`, `service: marchegourmande`, `release: b61b57e2223cfd42ed0cb286f1bfff3eea52d0ff` |
| Identité annoncée par le domaine | `b61b57e2223cfd42ed0cb286f1bfff3eea52d0ff` est un commit du dépôt source `O-N-2950/marchegourmande`, distinct des SHA de cet export. Le corps de santé est différent du fichier statique de `dev` ; ne pas attribuer le domaine à Pages sur le seul `CNAME` |
| Nœud servant actuellement le domaine | UNKNOWN. Le ledger du dépôt source mentionne historiquement Infomaniak OpenStack ; cette mention n'est pas une preuve actuelle de routage ou de topologie |

## Préserver les apports déjà présents sur main

Au début de l'inspection, `dev@12a67cae41193f6dc15947e413cbfb5308a5432e` a deux commits propres et manque un commit de `main@a375f62982bea502c46110bb774fb96ce9369a14`.

La comparaison complète des arbres montre un seul fichier propre à `main` : `entre-elles-avant-premiere/index.html`, mode `100644`, blob `1b2ca03c0ad4ae10c64466f3943da272dc00f90d`. Aucun fichier commun ne diffère. Les instructions et le verrou NEO appartiennent à `dev` et doivent être conservés. Ce fichier Entre Elles doit être repris à l'identique avant de qualifier un export ; ne pas remplacer le site par un ancien arbre qui le supprimerait. La synchronisation a ensuite été exécutée directement sur `dev` au commit `2b38709a5d2b8927b1e90d9ebb14ff23f94efd54`, en conservant les deux parents et le blob exact ; la référence distante a été relue.

## Qualification et paquet

L'arbre `dev` inspecté ne comporte ni `package.json`, ni sources applicatives, ni commande de construction, ni suite de tests d'application. `docs/NORTH_STAR.md` n'est pas présent sur cette branche ; le contrat technique est proposé dans la PR no 1 et l'autorité métier reste le dépôt source. Il faut qualifier le build dans le dépôt source et conserver la correspondance source → export ; aucun test d'application réussi n'est revendiqué pour ce dépôt d'artefacts. Le navigateur local a réellement été lancé par l'agent : Chromium s'arrête avec `process_singleton_posix.cc: socket() failed: Operation not permitted` puis `SIGABRT`. Les deux passes navigateur et les captures du candidat ne sont donc pas exécutées, et la livraison est bloquée.

Avant de construire le paquet, obtenir une copie complète des ressources, notamment les polices et images, et vérifier l'identité du commit exact :

```bash
git status --porcelain=v1 --untracked-files=all
git rev-parse HEAD
git diff --check
git diff --exit-code origin/main HEAD -- entre-elles-avant-premiere/index.html
```

La première commande doit être vide ; la dernière doit confirmer la préservation de l'avant-première, sauf évolution explicitement qualifiée. Exécuter ensuite les contrôles et tests du dépôt source et deux passes complètes des parcours navigateur sur le même build. Leurs commandes exactes et sorties doivent être recueillies dans le dépôt source, pas inventées ici.

L'utilitaire `scripts/deliver/artifact.py` prépare et vérifie le paquet. Une fois `/tmp/release` construit et qualifié depuis la source exacte, les commandes sont :

```bash
python scripts/deliver/artifact.py seal --repo . --source /tmp/release --output /tmp/release.tar.gz
python scripts/deliver/artifact.py verify --archive /tmp/release.tar.gz --expected-sha "$RELEASE_SHA" --archive-sha256 "$ARCHIVE_SHA256" --manifest-sha256 "$MANIFEST_SHA256"
```

Les trois variables sont les identifiants complets issus de la qualification et du scellement, pas des secrets. Ces commandes ne réalisent ni l'envoi, ni le canari, ni une bascule. Le paquet de l'export complet doit contenir :

1. l'identité complète du commit d'export et celle du commit source réellement construit ;
2. un `/health` JSON généré lors de l'empaquetage contenant le SHA complet de l'export qualifié, le SHA source et `mode: static` ; une santé statique n'est pas une preuve de santé d'une API ou d'une base ;
3. le SHA-256 de chaque fichier, puis du manifeste et de l'archive ;
4. les preuves des deux passages navigateur et la liste exacte des fichiers envoyés.

Ne pas écrire le SHA supposé de production dans les bundles versionnés. Le SHA est estampillé dans l'artefact après qualification du commit, puis le contenu servi doit être comparé à cet artefact.

## Envoi, canari, bascule et retour arrière

**État : non exécutables avec les seules preuves actuellement disponibles.** Le transport, la vérification des fichiers chez l'hébergeur et une méthode de canari séparé pour GitHub Pages ne sont pas établis. L'API Pages et l'historique des déploiements ne sont pas exposés par le connecteur GitHub disponible. Ne pas inventer un nœud Jelastic ni utiliser un nœud d'une autre application pour servir cet export. Si la cible réelle devient un serveur Infomaniak, les opérations serveur passent par le connecteur NEO Infomaniak MCP.

Avant toute bascule, le responsable de l'hébergement doit établir une méthode de livraison du paquet exact, sa vérification distante, un canari distinct préservant les données de production et une commande de restauration testée. Le canari n'utilise ni base de production, ni Stripe live, ni envoi réel. Conserver le déploiement/paquet précédent, ses empreintes et sa configuration de domaine.

Le retour arrière doit restaurer le paquet précédent identifié et vérifier de nouveau `/health` sur `marchegourmande.ch`. À cette date, aucun identifiant de déploiement restaurable ni commande de retour arrière vérifiée n'est disponible : le retour arrière reste **non prouvé**, et une bascule est interdite. Aucune migration n'est incluse dans cette mise à jour ; une future migration nécessite accord d'Olivier, sauvegarde hors dépôt avant migration, schéma additif et rejouable.

Après livraison effective seulement : vérifier le SHA exact sur le domaine client, les parcours sur téléphone et ordinateur, conserver les captures, actualiser `docs/PROGRESS.md`, réutiliser la PR de livraison `dev → main` et lancer NEO CI sur ce SHA. Un échec impose correctif ou retour arrière immédiat. Aucun secret dans le dépôt, cette documentation ou les sorties de commande.
