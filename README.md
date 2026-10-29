# BiblioCampus

## Présentation

BiblioCampus est une application de gestion des prêts de livres pour une
bibliothèque de campus. Elle permet de consulter les livres, d'enregistrer les
emprunts et les retours, puis de voir quelques statistiques.

Le projet utilise une architecture composée de plusieurs services. Chaque
service gère ses propres données. Les autres services reçoivent les informations
dont ils ont besoin grâce à des événements, au lieu de lire directement dans la
base de données d'un autre service.

## Équipe

Le projet est prévu pour une équipe de 2 à 4 personnes. Les noms des membres
seront ajoutés après confirmation de l'équipe.

**À faire :** inviter `charroux` dans le dépôt GitHub. Cette invitation doit
être envoyée par un propriétaire ou un administrateur du dépôt.

## Services

- **Catalogue** : ajoute les livres et met à jour leurs informations et le
  nombre d'exemplaires.
- **Membres** : crée et met à jour les comptes des lecteurs.
- **Emprunts** : enregistre les emprunts et les retours. Il garde une copie
  locale des informations nécessaires sur le livre et le membre.
- **Statistiques** : transforme les informations répliquées sur les emprunts en
  données simples à consulter.

Les services et leurs commandes sont décrits dans
[docs/services.json](docs/services.json).

## Agrégats et événements

Les agrégats principaux et les copies conservées par les autres services sont
décrits dans [docs/aggregates.json](docs/aggregates.json). Les événements entre
services, notamment ceux qui créent et mettent à jour ces copies, sont décrits
dans [docs/events.json](docs/events.json).

Un événement contient son service émetteur, son service récepteur, l'agrégat
concerné, le champ modifié et sa nouvelle valeur. Le service Emprunts peut ainsi
continuer à traiter un prêt avec ses copies locales, sans dépendre d'une lecture
directe du Catalogue ou du service Membres.

## Projection des données

Le service Statistiques utilise la copie locale des emprunts pour calculer le
nombre d'emprunts par mois. La structure projetée et une requête d'agrégation
MongoDB sont dans [docs/projections.json](docs/projections.json). Les
événements d'emprunt permettent de mettre à jour cette projection.

## Organisation des fichiers

```text
README.md
docs/
  services.json
  aggregates.json
  events.json
  projections.json
```

Les fichiers JSON sont des exemples de conception pour le projet. Ils ne
décrivent pas encore une application exécutable.
