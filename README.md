# todo app avec hasura et apollo
## difficultés:
```
mettre en place apollo et la prise en main de hasura , mais une fois compris c'est agréable à prendre en main
rafraichir les données de manière instantané (supression, ajout)
```
## Observation:
```
il y a une petite latence sur le chargement des donnés pourtant il n'y avait que 10 maximum 
ça economise pas mal de temps d'utiliser directement hasura et apollo et de se passer de vuex
Il y a une console disponible pour graphql du coup on peut faire des requetes sans ouvrir l'app(je ne pouvais pas faire ça avec pouchDB)
```
## Avantages:
```
j'ai stocké directement les requetes dans des dossier et fichier qui peuvent être appeler directement partout sur l'application , je trouve ça pratique
On peut personalisé des requetes et créer des fichier gql corespondant  ainsi les utiliser sur d'autres fichier
Il n'y pas besoin de coder le loader pour les donnés apollo s'en occupe ,  il suffira juste de faire un v-if
par rapport à pouchDb on peut limiter les argument afficher sur une requete
```
# Quasar App (todoapp)

A Quasar Framework app

## Install the dependencies
```bash
yarn
```

### Start the app in development mode (hot-code reloading, error reporting, etc.)
```bash
quasar dev
```

### Lint the files
```bash
yarn run lint
```

### Build the app for production
```bash
quasar build
```

### Customize the configuration
See [Configuring quasar.conf.js](https://quasar.dev/quasar-cli/quasar-conf-js).
