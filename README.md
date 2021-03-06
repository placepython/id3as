# Id3as: boite à idée de projets

Ce projet implémente une application de boîte à idée permettant de collecter des idées de projet via leur titre et une description courte optionnelle, de leurs affecter éventuellement des tags et des catégories, et de permettre à un utilisateur d'aimer (éventuellement DownVoter) ou de ne pas aimer (éventuellement UpVoter) pour manifester leur motivation ou non motivation pour le projet proposé.

Cette application utilise le framework django dans sa dernière version 3.2. L'idée est d'utiliser le moteur de template de django pour la réalisation du front-end avec Bootstrap pour apporter des styles simples.

## Installation

Les dépendances de ce projet sont gérée avec *pipenv* comme recommandé dans la [documentation officielle](https://packaging.python.org/tutorials/managing-dependencies/) sur le packaging python. Pour ceux qui ne l'ont pas installé (si la commande `pipenv --version` vous donne une erreur), n'hésitez pas à l'installer à l'aide de pipx comme décrit dans [cette documentation](./docs/installer-pipenv.md). En plus de pipenv, vous aurez besoin de travailler avec la **version 3.9 de Python**. 

Les dépendance pour le front-end sont gérées à l'aide de node et de son package manager, npm. Il est donc nécessaire d'installer node
sur votre ordinateur, si ce n'est pas déjà fait. Pour le savoir, exécuter la commande `npm --version` dans
un terminal. Si vous obtenez une erreur, rendez-vous sur le [site web de node.js](https://nodejs.org/en/download/)
et suivez les indications d'installation pour votre système.

Une fois que pipenv est installé sur votre système, vous pouvez commencer le développement de ce projet en suivant les instruction ci-dessous:

1. Forkez le projet sur votre propre compte github
2. Cloner votre fork avec git pour obtenir une version locale
3. Ouvrez un terminal à la racine du projet
4. Installer les dépendances du projet avec `$ pipenv install --dev`
5. Exécutez les migrations avec `$ pipenv run python manage.py migrate`. La version de développement utiliser sqlite comme base de données. La version de production utilise postgresql.
6. Générer les fichiers front avec `$ pipenv run python manage.py webpack`
6. Démarrez le serveur de développement avec `$ pipenv run python manage.py runserver`
7. Accédez à l'application sur [http://localhost:8000](http://localhost:8000)

Vous pouvez éviter d'avoir à exécuter pipenv run à chaque fois en activant l'environnement
virtuel à l'aide de la commande `pipenv shell`.

## Structure générale du projet

Ce projet utilise une variation de la structure proposée dans le ouvrage [Two
Scoops of Django](https://www.feldroy.com/books/two-scoops-of-django-3-x), de Audrey et Daniel Greenfield, reconnu pour 
ses bonnes pratiques. Cette structure s'articule autour d'un répertoire de configuration
nommé **config** et un répertoire d'applications nommé ici **id3as**. Les templates
se trouve dans le répertoire templates à la racine du projet et les fichiers
front dans le répertoire assets (lire [ce README](./assets/README.md) pour le développement du front-end)

## Applications django

Pour ceux qui s'occupent du front-end, n'hésitez pas à lire la documentation dans 
[ce REAMDE dédié.](./assets/README.md)

La structure du projet n'est pas celle par défaut produite par django-admin. Elle
découpe le projet de la manière suivante:

- **assets** accueille les fichiers javascript et scss dans le sous-répertoire src. On utilise webpack pour compiler les assets finaux avec la commande `npm run dev` ou `npm run dev:watch`.
- **config/settings** accueille tous les fichiers de configuration pour le développement (local.py) pour le déploiement (heroku.py et production.py)
- **id3as** accueille toutes les apps django composant le projet
- **media** est le répertoire dans lequel sont éventuellement rangés les fichiers uploadés par l'utilisateur (p.ex. une image associée à l'idée de projet).
- **tests** réunit les tests unitaires, d'intégration et fonctionnels

Le projet a lui-même déjà été découpé en applications django comme suit:

- **id3as/projects** implémente les idées de projets
- **id3as/pages** implémente les pages statiques du site
- **id3as/users** implémente le modèle utilisateur et le système d'authentification
- **id3as/profiles** implémente le profil utilisateur avec la posibilité de gérer les idées de projet qu'il a proposées
- **id3as/votes** implémente le système de vote sur les idées de projets
- **id3as/categories** implémente le système de catégories
- **id3as/tags** implémente le système de tags et utilise la biblithèque taggit pour son implémentation

Ces différentes applications ont été préconfigurées dans le squellette de départ.

