# Export Pages — contrat technique propre

Servir l'export qualifié du produit Marche Gourmande, sans créer de logique
métier parallèle. L'autorité métier reste O-N-2950/marchegourmande.

| ID | Critère technique |
|---|---|
| PAGE-01 | Le domaine et le routage HTTPS aboutissent à la cible déclarée |
| PAGE-02 | Chaque export est lié au SHA source et au build réellement qualifié |
| PAGE-03 | Manifest, ressources et parcours publics correspondent à cet export |
| PAGE-04 | La procédure de remplacement/restauration maintient le service et prouve l'artefact servi |

Le dépôt de juin et une réponse HTTP 200 ne prouvent pas PAGE-02 à PAGE-04.
Suivi dans PROGRESS.md. Aucun score métier du produit n'est dupliqué.
