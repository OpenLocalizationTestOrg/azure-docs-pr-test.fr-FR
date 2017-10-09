---
title: "Migrer : utilitaire de migration de l’entrepôt de données | Microsoft Docs"
description: "Migrer tooSQL l’entrepôt de données."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 4d7ad981-ef31-4513-b337-50bdc4709c09
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: c89909883fb42b0b04dd87a9973e5ee3e30d8f0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="data-warehouse-migration-utility-preview"></a>Utilitaire de migration de l’entrepôt de données (version préliminaire)
> [!div class="op_single_selector"]
> * [Télécharger l’utilitaire de migration][Download Migration Utility]
> 
> 

Hello utilitaire de Migration de l’entrepôt de données est qu'un outil conçu toomigrate schéma et les données à partir de SQL Server et la base de données SQL Azure tooAzure SQL Data Warehouse. Pendant la migration du schéma, outil de hello mappe automatiquement schéma correspondant de hello à partir de la source toodestination. Une fois le schéma de hello a été migré, les outils hello fournit des données de toomove d’option hello avec les scripts générés automatiquement.

En outre, tooschema et migration de données, cela donne outil hello de rapports de compatibilité toogenerate option qui résument les incompatibilités entre les instances source et cible hello qui empêcheraient rationalisé migration.

## <a name="get-started"></a>Prise en main
Comme condition préalable pour l’installation, vous devez scripts de migration hello toorun de l’utilitaire de ligne de commande BCP et rapport de compatibilité Office tooview hello. Après le lancement de hello exécutable qui est téléchargé vous seront demandée tooaccept CLUF standard avant de l’outil de hello sera installé.

En outre, toorun hello Utiliy de Migration, vous serez peut-être hello une suivant les autorisations de base de données hello que vous cherchez toomigrate : CREATE DATABASE, ALTER ANY DATABASE ou VIEW ANY DEFINITION.

### <a name="launching-hello-tool-and-connecting"></a>Lancer l’outil de hello et connexion
Outil de lancement de hello en cliquant sur l’icône du bureau hello qui apparaît après installation. Lors de l’ouverture d’outil de hello, vous êtes invité à une page de connexion initiale dans laquelle vous pouvez choisir les sources et destination pour l’outil de migration hello. À ce stade, nous prenons en charge SQL Server et la base de données SQL Azure en tant que sources et SQL Data Warehouse en tant que destination. Après avoir sélectionné cette vous demandera serveur de source de tooyour tooconnect par remplissage dans le nom du serveur et l’authentification, puis en cliquant sur « Se connecter ».

Après avoir authentifié, hello outil affiche une liste des bases de données qui sont présents dans le serveur hello dont vous êtes connecté. Vous pouvez commencer la migration de hello en sélectionnant une base de données que vous aimeriez toomigrate et puis en cliquant sur « Migrer sélectionné ».

## <a name="migration-report"></a>Rapport de migration
En sélectionnant « Vérifier la compatibilité de base de données » dans l’outil de hello génère un rapport de synthèse de toutes les incompatibilités d’objet de base de données hello toomigrate demandé. Vous trouverez une liste plus large de certaines hello des fonctionnalités de SQL Server qui ne sont pas présente dans l’entrepôt de données SQL dans notre [documentation de migration][migration documentation]. Une fois le rapport de hello est généré, vous serez en mesure de toosave et rapport hello ouvert dans Excel.

Notez que lors de la génération de schéma de migration hello, la plupart des problèmes identifiés comme 'Object' soient ajustées dans la commande tooallow immédiatement la migration de ces données. Passez en revue tooensure de modifications hello vous ne souhaitez pas toomake des modifications supplémentaires avant d’appliquer le schéma de hello.

## <a name="migrate-schema"></a>Migration du schéma
Une fois connecté, en sélectionnant « Migrer le schéma » génère un script de migration de schéma pour les tables de hello sélectionné. Cette structure de hello des ports de script de table de hello, mappe les formulaires de données incompatibles types toomore compatibles et crée le schéma et les informations d’identification de sécurité si cela est indiqué par l’utilisateur hello dans les paramètres de migration hello. Ce code peut être exécuté sur l’instance de SQL Data Warehouse hello ciblé, tooa fichier enregistré, copié tooyour Presse-papiers ou même modifié en ligne avant d’entreprendre une action supplémentaire.  

Comme indiqué ci-dessus, lorsque la migration migration de hello de révision de schéma modifié que hello outil a effectué dans l’ordre tooensure qui que vous comprenez les.  

## <a name="migrate-data"></a>Migration des données
En cliquant sur « Migrer des données » hello, vous pouvez générer des scripts BCP qui déplacement les fichiers tooflat première de données sur votre serveur, puis directement dans votre entrepôt de données SQL. Nous vous recommandons de ce processus pour le déplacement des petites quantités de données et, en tant que nouvelles tentatives ne sont pas intégrés et erreurs peuvent se produire s’il existe une perte de connexion de réseau hello. Dans commande toorun cela, vous devez toohave utilitaire hello BCP de ligne de commande installé et schéma hello pour les données de salutation doit déjà avoir été créé.

Une fois que vous avez rempli les paramètres hello ci-dessus, vous devez tooclick exécutez simplement la migration et un ensemble de deux packages ne sera généré tooyour l’emplacement spécifié. Exécuter le fichier d’exportation hello dans les données de tooexport de commande à partir de votre source de migration dans des fichiers plats et exécuter les fichier d’importation hello dans l’ordre tooimport vos données dans SQL Data Warehouse.

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez effectué la migration des données, consultez Procédure trop[développer][develop].

<!--Image references-->

<!--Article references-->
[migration documentation]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md

<!--Other Web references--> 
[Download Migration Utility]: https://migrhoststorage.blob.core.windows.net/sqldwsample/DataWarehouseMigrationUtility.zip
