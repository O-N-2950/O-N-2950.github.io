## 2026-11-12 — ADP-019, export Pages et absence de régression
- Utilitaire de scellement : **29 tests de contrat réussis** sur la version commune réellement exécutée et relue ; empreinte `artifact.py` `d6600e3862db736820c6c38f9ebd6d472ec503443f8ee95771c1864376d8235f`. Chaque copie installée est comparée à cette empreinte. Ces tests ne sont ni des tests navigateur ni une preuve de réception du paquet de cette application.


- Politique : bloc NEO 1.4.0 épinglé dans `AGENTS.md` et `CLAUDE.md`, verrou aligné sur `6c564f02f3b8ae1cae047653bc77bd6514e71725` et empreinte canonique `dbc9a0a0887b4ba6e4725064d3067ebc4c9d42653e6ad8fea9bf094b27d79a0b`. Règle locale enregistrée : « On progresse toujours, on ne régresse jamais ».
- Inspection : 12.11.2026 à 06:07:27 (Europe/Zurich ; 05:07:27 UTC). Base lue `dev@12a67cae41193f6dc15947e413cbfb5308a5432e` ; GitHub Pages configuré, domaine déclaré `marchegourmande.ch`, hébergeur réellement servi à réconcilier. Projet Railway homonyme sans service. Voir `docs/deployment/DIRECT_DELIVERY.md`.
- Anti-régression : synchronisation de `main` dans `dev` effectuée au commit `2b38709a5d2b8927b1e90d9ebb14ff23f94efd54`, avec les deux parents Git conservés. Le fichier `entre-elles-avant-premiere/index.html` est repris à l’identique (blob `1b2ca03c0ad4ae10c64466f3943da272dc00f90d`) ; les instructions propres à `dev` sont préservées. Aucun fichier commun ne présentait de conflit.
- Contrôles locaux : identité du bloc, marqueurs, source et empreinte, syntaxe du verrou et préservation des règles vérifiées sur les fichiers préparés. Aucun build ni suite applicative fournis dans ce dépôt d'export. Lancement réel du navigateur local impossible : Chromium `socket() failed: Operation not permitted`, puis `SIGABRT` ; deux passes navigateur non exécutées, aucune capture candidate.
- Livraison : **NON EFFECTUÉE** ; heure de livraison : sans objet. GET domaine client le 12.11.2026 à 06:09:11 Europe/Zurich (05:09:11 UTC) : `/health` HTTP 404 ; `/api/health` HTTP 200 annonce `release: b61b57e2223cfd42ed0cb286f1bfff3eea52d0ff`. Ce SHA appartient au dépôt source Marche Gourmande, pas à cet export. SHA servi par `/health` : **UNKNOWN**. Le run Pages réussi sur `main@a375f629…` ne prouve pas le déploiement sur ce domaine. Aucun paquet envoyé, canari ou bascule exécuté ; aucune migration ni sauvegarde de base effectuée.
- Blocages techniques avant livraison : source/build → export non qualifiés ; `docs/NORTH_STAR.md` absent de `dev` (contrat proposé dans PR no 1) ; `/health` estampillé absent ; deux passes navigateur manquantes ; réglage Pages, vérification distante du paquet, canari et méthode de retour arrière non établis. Propriétaires : responsable du produit Marche Gourmande et responsable de l'hébergement ; reprise après accès à ces preuves et moyens.
- Retour arrière : version `main` identifiée dans Git mais restauration opérationnelle **non prouvée**. Ne pas assimiler un commit à un déploiement réinstallable.

### À prouver sur le terrain

| Quoi | Par qui | Quand |
| --- | --- | --- |
| Vérifier sur téléphone et ordinateur les pages publiques, ressources PWA et avant-première Entre Elles de l'export livré | Agent de livraison et responsable Marche Gourmande | Après bascule vérifiée au SHA exact ; captures conservées avant compte rendu |
| Confirmer les parcours réellement utilisés et l'absence de régression avec des utilisateurs autorisés | Responsable du produit / utilisateurs pilotes désignés | Après livraison technique ; avant déclaration 100 % ou confirmation commerciale |

Les contrôles techniques manquants ci-dessus ne sont pas des essais terrain différables.

## 2026-11-09 — Livraison progressive et preuves terrain

- Fait : décision d’Olivier du 09.11.2026 diffusée dans les instructions épinglées NEO Core 1.3.0.
- Règle historique remplacée le 12.11.2026 : l’attente de NEO CI avant livraison ne s’applique plus. ADP-019 exige les portes locales sur le SHA exact, le canari et les preuves de service ; NEO CI intervient après livraison. Les seuls essais terrain manquants restent différables.
- Contrôles maintenus avant livraison : sécurité, migrations, facturation, paiements et envois à de vrais clients. Aucun échec technique ni contrôle sensible manquant n’est reclassé en preuve terrain.
- Prouvé : présence du bloc et du pin contrôlée lors de la diffusion ; cela ne prouve ni la réception par les agents ni une nouvelle version en production.
- Propriétaire : responsable du produit et NEO Factory. Prochaine action : distinguer les blocages techniques des essais terrain, puis livrer le prochain candidat utile qualifié localement selon ADP-019.

### À prouver sur le terrain

| Quoi | Par qui | Quand |
| --- | --- | --- |
| Inventorier les essais avec utilisateurs et preuves d’usage réel restant à réaliser pour cette application, sans les déclarer acquis | Responsable du produit | Après livraison de l’étape concernée ; avant toute déclaration 100 % North Star ou confirmation commerciale finale |

