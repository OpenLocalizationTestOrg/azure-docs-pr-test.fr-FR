---
title: "Outils d’ingestion de données de la machine virtuelle DSVM - Azure | Microsoft Docs"
description: "Outils d’ingestion de données de la machine virtuelle DSVM"
keywords: "outils de science des données, machine virtuelle science des données, outils pour la science des données, science des données linux"
services: machine-learning
documentationcenter: 
author: bradsev
manager: cgronlun
editor: cgronlun
ms.assetid: 
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/11/2017
ms.author: gokuma;bradsev
ms.openlocfilehash: 564c06c5017a77431b7d6fed7b43c47141b12252
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="data-science-virtual-machine-data-ingestion-tools"></a>Outils d’ingestion de données de la machine virtuelle DSVM

L’une des premières étapes techniques dans un projet de science de données ou d’intelligence artificielle consiste à identifier les jeux de données à utiliser, puis à les importer dans votre environnement analytique. La machine virtuelle DSVM (Data Science Virtual Machine) fournit des outils et des bibliothèques pour importer des données de différentes sources dans un stockage de données analytiques sur la machine DSVM ou dans une plateforme de données sur le cloud ou localement. 

Voici quelques outils de déplacement de données que nous vous avons fournis sur la machine virtuelle DSVM. 

## <a name="adlcopy"></a>AdlCopy

|    |           |
| ------------- | ------------- |
| Qu’est-ce que c’est ?   | Outil permettant de copier des données d’objets blob du stockage Azure vers Azure Data Lake Store. Il peut également copier des données entre deux comptes Azure Data Lake Store.      |
| Versions DSVM prises en charge      | Windows      |
| Utilisations classiques      | Importation de plusieurs objets blob du stockage Azure vers Azure Data Lake Store.      |
|  Comment l’utiliser/l’exécuter ?    |   Ouvrez une invite de commandes et tapez `adlcopy` pour obtenir de l’aide.    |
| Liens vers des exemples      | [À l’aide d’AdlCopy]https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-copy-data-azure-storage-blob)      |
| Outils connexes sur la machine virtuelle DSVM      | AzCopy, ligne de commande Azure     |

## <a name="azure-command-line"></a>Ligne de commande Azure

|    |           |
| ------------- | ------------- |
| Qu’est-ce que c’est ?   | Outil de gestion pour Azure. Il contient également des verbes de commande pour déplacer des données à partir de plateformes de données Azure, telles que les objets blob de stockage Azure, Azure Data Lake Storage.     |
| Versions DSVM prises en charge      | Windows, Linux     |
| Utilisations classiques      | Importation/exportation de données vers et depuis le stockage Azure, Azure Data Lake Store      |
|  Comment l’utiliser/l’exécuter ?    |   Ouvrez une invite de commandes et tapez `az` pour obtenir de l’aide.    |
| Liens vers des exemples      | [Utilisation de l’interface de ligne de commande Azure](https://docs.microsoft.com/cli/azure/?viee-cli-latest)     |
| Outils connexes sur la machine virtuelle DSVM      | AzCopy, AdlCopy      |


## <a name="azcopy"></a>AzCopy

|    |           |
| ------------- | ------------- |
| Qu’est-ce que c’est ?   | Outil permettant de copier des données vers et depuis des fichiers locaux, des objets blob, des fichiers et des tables de stockage Azure.      |
| Versions DSVM prises en charge      | Windows      |
| Utilisations classiques      | Copie de fichiers vers le stockage d’objets blob, copie d’objets blob entre plusieurs comptes.      |
|  Comment l’utiliser/l’exécuter ?    |   Ouvrez une invite de commandes et tapez `azcopy` pour obtenir de l’aide.    |
| Liens vers des exemples      | [AzCopy sur Windows](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy)      |
| Outils connexes sur la machine virtuelle DSVM      | AdlCopy     |


## <a name="azure-cosmos-db-documentdb-api-data-migration-tool"></a>Azure Cosmos DB : API DocumentDB (outil de migration de données)

|    |           |
| ------------- | ------------- |
| Qu’est-ce que c’est ?   | Outil permettant d’importer des données dans Azure Cosmos DB ou Azure DocumentDB à partir de différentes sources, notamment des fichiers JSON, des fichiers CSV, SQL, MongoDB, Stockage Table Azure, Amazon DynamoDB et les collections d’API Azure Cosmos DB DocumentDB.      |
| Versions DSVM prises en charge      | Windows      |
| Utilisations classiques      | Importation de fichiers à partir d’une machine virtuelle vers CosmosDB, importation de données à partir du stockage Table Azure vers CosmosDB ou importation de données à partir d’une base de données SQL Server vers CosmosDB.     |
|  Comment l’utiliser/l’exécuter ?    |   Pour utiliser la version en ligne de commande, ouvrez une invite de commandes et tapez `dt`. Pour utiliser l’outil GUI, ouvrez une invite de commandes et tapez `dtui`.    |
| Liens vers des exemples      | [Importation de données dans CosmosDB](https://docs.microsoft.com/en-us/azure/cosmos-db/import-data)      |
| Outils connexes sur la machine virtuelle DSVM      | AzCopy, AdlCopy      |


## <a name="bcp"></a>bcp

|    |           |
| ------------- | ------------- |
| Qu’est-ce que c’est ?   | Outil SQL Server permettant de copier des données entre SQL Server et un fichier de données.      |
| Versions DSVM prises en charge      | Windows      |
| Utilisations classiques      | Importation d’un fichier CSV dans une table SQL Server, exportation d’une table SQL Server dans un fichier.      |
|  Comment l’utiliser/l’exécuter ?    |   Ouvrez une invite de commandes et tapez `bcp` pour obtenir de l’aide.    |
| Liens vers des exemples      | [Utilitaire de copie en bloc](https://docs.microsoft.com/en-us/sql/tools/bcp-utility)      |
| Outils connexes sur la machine virtuelle DSVM      | SQL Server, sqlcmd      |


## <a name="microsoft-data-management-gateway"></a>Passerelle de gestion des données de Microsoft

|    |           |
| ------------- | ------------- |
| Qu’est-ce que c’est ?   | Outil permettant de connecter des sources de données locales à des services cloud en vue de leur consommation.      |
| Versions DSVM prises en charge      | Windows      |
| Utilisations classiques      | Connexion d’une machine virtuelle à une source de données locale      |
|  Comment l’utiliser/l’exécuter ?    |   Démarrez « Passerelle de gestion des données Microsoft » à partir du menu Démarrer.    |
| Liens vers des exemples      | [Passerelle de gestion de données](https://msdn.microsoft.com/library/dn879362.aspx)      |
| Outils connexes sur la machine virtuelle DSVM      | AzCopy, AdlCopy, bcp    |
