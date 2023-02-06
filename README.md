"# Creating-a-Simple-ETL-Package by using SSIS" 


######## Leçon 1: Créer un projet et un package de base #########


I/ Créé des gestionnaires de connexions pour les données sources et de destination
Après avoir ajouté un gestionnaire de connexions de fichiers plats pour la connexion à la source de données, vous ajoutez
un gestionnaire de connexions OLE DB pour la connexion à la destination de données.
==> Source: Fichiers Plats
==> Destination: OLE DB
###Ajouter et configurer un gestionnaire de connexions OLE DB###
À l’aide d’un gestionnaire de connexions OLE DB, vous pouvez:
1/ spécifier le serveur ==> localhost
2/ la méthode d’authentification ==> l’authentification Windows
3/ la base de données par défaut pour la connexion.==> AdventureWorksDW2012

II/ Ajoutez une tâche de flux de données à votre package
La tâche de flux de données définit le moteur de flux de données qui déplace les données entre les sources et les 
destinations et fournit la fonctionnalité grâce à laquelle il est possible de transformer, nettoyer et modifier les
données lors de leur déplacement. La tâche de flux de données est l'endroit où s'effectue la majorité du travail d'un
processus d'ETL.

III/Ajouter et configurer la source du fichier plat à votre package pour extraire les données du fichier source
(Ajouter un composant source de fichier plat)
Une source de fichier plat est un composant de flux de données qui utilise des métadonnées définies par un gestionnaire de 
connexions de fichiers plats. Ces métadonnées spécifient le format et la structure des données à extraire du fichier plat
par un processus de transformation.La source de fichier plat extrait les données d’un seul fichier plat, en utilisant les 
définitions de format indiquées dans le gestionnaire de connexions de fichiers plats.
==> glisser une source de fichier plat sur l’onglet Flux de données

IV/ Ajouter et configurer les transformations de recherche
Une transformation de recherche effectue une recherche en joignant les données dans la colonne d'entrée spécifiée à une 
colonne dans un dataset de référence. Le dataset de référence peut être une table ou une vue existante, une nouvelle table 
ou le résultat d'une instruction SQL.
Dans ce tutoriel, définissez les transformations de recherche nécessaires pour obtenir les valeurs de CurrencyKey et DateKey.
la transformation de recherche utilise un gestionnaire de connexions OLE DB pour se connecter à la base de données qui 
contient les données sources du jeu de données de référence, que j'ai créé précédemment.
==> Au cours de cette tâche, vous allez ajouter et configurer les deux composants de transformation de recherche suivants 
dans le package :

1/Ajouter et configurer la transformation Lookup "Currency Key": Une transformation qui effectue une recherche des valeurs dans la colonne CurrencyKey de la table de dimensions 
DimCurrency, en fonction de leur correspondance avec les valeurs de la colonne CurrencyID du fichier plat.
2/Ajouter et configurer la transformation Lookup "Date Key":Une transformation qui effectue une recherche des valeurs dans la colonne DateKey de la table de dimensions DimDate, en 
fonction de leur correspondance avec les valeurs de la colonne CurrencyDate du fichier plat.


V/ Ajouter et configurer la destination OLE DB
La tâche suivante consiste à charger les données transformées dans la destination. Pour charger les données, vous ajoutez 
une destination OLE DB au flux de données. La destination OLE DB peut utiliser une table de base de données, une vue ou une
commande SQL pour charger les données dans plusieurs bases de données compatibles OLE DB.
==> Au cours de cette tâche, vous allez ajouter et configurer une destination OLE DB pour utiliser le gestionnaire de 
connexions OLE DB que vous avez créé précédemment.
https://dataedo.com/samples/html/Data_warehouse/doc/AdventureWorksDW_4/modules/Currency_Rates_104/module.html

VI/ Annoter et mettre en forme le package de la leçon 1
La configuration du package de la leçon 1 étant terminée, c’est probablement le moment de mettre un peu d’ordre dans la 
disposition du package. SQL Server Data Tools fournit des outils qui facilitent la mise en forme de la disposition des 
packages. Les fonctionnalités de mise en forme offrent notamment la possibilité d’attribuer la même taille aux formes, de 
les aligner et de changer l’espace horizontal et vertical entre elles.
==> Une autre manière d'améliorer la compréhension des fonctionnalités des packages est d'ajouter des annotations 
décrivant ces fonctionnalités:
==> Exploitez les fonctionnalités de mise en forme disponibles dans SQL Server Data Tools pour "Mettre en forme la 
disposition du flux de données" et après pour "Ajouter une annotation au flux de données".
Voila l'annotation de cette situation: "Le flux de données extrait les données d'un fichier, recherche des valeurs dans 
la colonne CurrencyKey de la table DimCurrency et dans la colonne DateKey de la table DimDate, puis écrit les données 
dans la table NewFactCurrencyRate."

##Summary: 
Dans ce tutoriel, vous avez effectué les tâches suivantes :

* création d'un nouveau projet SSIS ;

* Configuration des gestionnaires de connexions pour que le package se connecte aux données sources et de destination.

* Ajout d'un flux de données qui récupère les données à partir d'une source de fichier plat, effectue les transformations 
de recherche nécessaires sur les données et configure les données pour la destination.

==>Votre package est maintenant terminé et prêt à être testé ! 
==> Vous devez Exécuter le package de la leçon 1 à traver le Démarrage de débogage.
