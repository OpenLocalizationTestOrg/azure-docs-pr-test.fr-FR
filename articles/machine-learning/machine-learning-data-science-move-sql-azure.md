---
title: "aaaMove données tooan base de données SQL Azure pour Azure Machine Learning | Documents Microsoft"
description: "Créer la Table SQL et charger des données tooSQL Table"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 50f8b862-4d32-44b2-a1e2-4fbc8024acaa
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: b33ef836f42c17a56794baf763281e9998b16bef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooan-azure-sql-database-for-azure-machine-learning"></a>Déplacer les données tooan base de données SQL Azure pour Azure Machine Learning
Cette rubrique décrit les options de hello pour déplacer des données à partir de fichiers plats (formats CSV ou TSV) ou à partir des données stockées dans une base de données locale SQL Server tooan SQL Azure. Ces tâches pour les données mobile dans le cloud toohello font partie de hello processus de science des données équipe.

Pour une rubrique qui décrit les options de hello de déplacement tooan de données locale SQL Server pour l’apprentissage, consultez [déplacer les données tooSQL Server sur une machine virtuelle Azure](machine-learning-data-science-move-sql-server-virtual-machine.md).

suivant de Hello **menu** lie tootopics qui décrivent comment les données de tooingest dans les environnements cibles où les données de salutation peuvent être stockées et traitées au cours de hello processus de science des données équipe (TDSP).

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

Hello tableau suivant résume les options hello pour Mobile tooan de données base de données SQL Azure.

| <b>SOURCE</b> | <b>DESTINATION : base de données SQL Azure</b> |
| --- | --- |
| <b>Fichier plat (mise en forme CSV ou TSV)</b> |<a href="#bulk-insert-sql-query">Requête SQL Bulk Insert |
| <b>Serveur SQL Server local</b> |1. <a href="#export-flat-file">TooFlat d’exportation de fichier<br> 2. <a href="#insert-tables-bcp">Assistant Migration de la base de données SQL<br> 3. <a href="#db-migration">Sauvegarde et restauration de base de données<br> 4. <a href="#adf">Azure Data Factory |

## <a name="prereqs"></a>Configuration requise
les procédures de Hello décrites ici nécessitent que vous avez :

* Un **abonnement Azure**. Si vous n’avez pas d’abonnement, vous pouvez vous inscrire à un [essai gratuit](https://azure.microsoft.com/pricing/free-trial/).
* Un **compte de stockage Azure**. Vous utilisez un compte de stockage Azure pour stocker les données de hello dans ce didacticiel. Si vous n’avez pas un compte de stockage Azure, consultez hello [créer un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account) l’article. Une fois que vous avez créé le compte de stockage hello, vous devez le compte de hello tooobtain clé utilisé le stockage de hello tooaccess. Voir [Gérer vos clés d’accès de stockage](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).
* Accès tooan **base de données SQL Azure**. Si vous devez configurer une base de données SQL Azure, [prise en main de Microsoft Azure SQL Database](../sql-database/sql-database-get-started.md) fournit des informations sur la façon de tooprovision une nouvelle instance de la base de données SQL Azure.
* **Azure PowerShell** installé et configuré localement. Pour obtenir des instructions, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).

**Données**: processus de migration hello sont illustrées à l’aide de hello [NYC Taxi dataset](http://chriswhong.com/open-data/foil_nyc_taxi/). contient des informations sur les données du voyage et salons Hello NYC Taxi dataset et est disponible sur le stockage d’objets blob Azure : [NYC Taxi données](http://www.andresmh.com/nyctaxitrips/). Un échantillon et une description de ces fichiers sont fournis dans la [description du jeu de données des voyages NYC Taxi](machine-learning-data-science-process-sql-walkthrough.md#dataset).

Vous pouvez adapter hello procédures tooa ici décrit ensemble de vos propres données ou suivez les étapes de hello comme décrit à l’aide de hello NYC Taxi le jeu de données. hello de tooupload NYC Taxi le jeu de données dans votre base de données SQL Server locale, procédez comme procédure hello [importer en bloc des données dans la base de données SQL Server](machine-learning-data-science-process-sql-walkthrough.md#dbload). Ces instructions concernent un serveur SQL Server sur une Machine virtuelle de Azure, mais la procédure hello pour le téléchargement toohello local SQL Server est hello identiques.

## <a name="file-to-azure-sql-database"></a>Déplacement des données d’une base de données de fichier plat source tooan SQL Azure
Données de fichiers plats (CSV ou TSV au format) peuvent être déplacés tooan SQL Azure à l’aide d’une requête SQL d’insertion en bloc.

### <a name="bulk-insert-sql-query"></a> Requête SQL Bulk Insert
des étapes de Hello de procédure hello à l’aide de hello Bulk Insert la requête SQL sont similaires toothose traité dans les sections hello pour le déplacement des données à partir d’un tooSQL de source de fichier plat Server sur une machine virtuelle Azure. Pour plus d’informations, consultez [Requête SQL Bulk Insert](machine-learning-data-science-move-sql-server-virtual-machine.md#insert-tables-bulkquery).

## <a name="sql-on-prem-to-sazure-sql-database"></a>Déplacement des données à partir de la base de données locale SQL Server tooan SQL Azure
Si la source de données hello est stocké dans un local SQL Server, il existe différentes possibilités pour Mobile hello tooan SQL Azure base de données :

1. [TooFlat d’exportation de fichier](#export-flat-file)
2. [Assistant Migration de la base de données SQL](#insert-tables-bcp)
3. [Sauvegarde et restauration de base de données](#db-migration)
4. [Azure Data Factory](#adf)

étapes de hello trois premières Hello sont très similaires sections toothose dans [déplacer les données tooSQL Server sur une machine virtuelle Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) qui couvrent les mêmes procédures. Sections appropriées de liens toohello dans cette rubrique sont fournies dans hello suivant les instructions.

### <a name="export-flat-file"></a>TooFlat d’exportation de fichier
étapes Hello pour cet exportation du fichier plat tooa sont similaires toothose couvert dans [exporter tooFlat fichier](machine-learning-data-science-move-sql-server-virtual-machine.md#export-flat-file).

### <a name="insert-tables-bcp"></a>Assistant Migration de la base de données SQL
Hello étapes pour utiliser hello Assistant de Migration de base de données SQL sont similaires toothose couvert dans [l’Assistant Migration de base de données SQL](machine-learning-data-science-move-sql-server-virtual-machine.md#sql-migration).

### <a name="db-migration"></a>Sauvegarde et restauration de base de données
étapes Hello pour l’utilisation de base de données de sauvegarde et de restauration sont similaires toothose traitée dans [base de données principale et de restauration](machine-learning-data-science-move-sql-server-virtual-machine.md#sql-backup).

### <a name="adf"></a>Azure Data Factory
procédure de Hello pour Mobile données tooan Azure SQL database avec fabrique de données Azure (ADF) est fourni dans la rubrique de hello [déplacer des données à partir d’un ordinateur local SQL server tooSQL Azure avec Azure Data Factory](machine-learning-data-science-move-sql-azure-adf.md). Cette rubrique montre comment toomove des données à partir d’un tooan de base de données SQL Server locale SQL Azure de base de données via le stockage d’objets Blob Azure à l’aide de la définition d’application.

Envisagez d’utiliser ADF lorsque toobe des besoins de données migrées en permanence dans un scénario hybride qui accède à la fois localement et ressources de cloud et lorsque les données de salutation sont traitées ou a besoin toobe modifié ou avez ajouté de logique métier des tooit quand en cours de migration. ADF permet hello de planification et de surveillance des travaux à l’aide de simples scripts JSON qui gèrent le déplacement de hello des données sur une base périodique. ADF dispose également d'autres fonctionnalités comme la prise en charge des opérations complexes.
