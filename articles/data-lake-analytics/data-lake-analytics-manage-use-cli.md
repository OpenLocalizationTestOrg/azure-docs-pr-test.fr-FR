---
title: "aaaManage Analytique de LAC de données Azure à l’aide d’une Interface de ligne Azure | Documents Microsoft"
description: "Découvrez comment les comptes toomanage Analytique lac de données, sources de données, des travaux et des utilisateurs à l’aide de CLI d’Azure"
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: 4e5a3a0a-6d7f-43ed-aeb5-c3b3979a1e0a
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 0af1f89080739b39f6980989b7694734cc135715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-command-line-interface-cli"></a>Gestion de Azure Data Lake Analytics à l’aide de l’interface de ligne de commande Azure (CLI)
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

Découvrez comment des comptes toomanage Analytique de LAC de données Azure, des sources de données, des utilisateurs et des travaux à l’aide de hello CLI d’Azure. les rubriques de gestion toosee à l’aide d’autres outils, cliquez sur l’onglet hello ci-dessus, sélectionnez.


**Configuration requise**

Avant de commencer ce didacticiel, vous devez disposer de hello :

* **Un abonnement Azure**. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Interface de ligne de commande Azure**. Consultez [Installation et configuration de l’interface de ligne de commande Azure](../cli-install-nodejs.md).
  * Téléchargez et installez hello **préliminaires** [outils CLI d’Azure](https://github.com/MicrosoftBigData/AzureDataLake/releases) commander toocomplete cette démonstration.
* **Authentification**, à l’aide hello la commande suivante :
  
        azure login
    Pour plus d’informations sur l’authentification à l’aide d’un compte professionnel ou scolaire, consultez [connecter tooan abonnement Azure à partir de hello CLI d’Azure](../xplat-cli-connect.md).
* **Passez en mode Azure Resource Manager de toohello**, à l’aide hello la commande suivante :
  
        azure config mode arm

**toolist hello Data Lake Store et Analytique lac de données de commandes :**

    azure datalake store
    azure datalake analytics

<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-accounts"></a>Gérer les comptes
Avant d'exécuter des travaux Data Lake Analytics, vous devez avoir un compte Data Lake Analytics. Contrairement à Azure HDInsight, vous ne payez pas pour un compte Analytics lorsque celui-ci n'exécute aucun travail.  Vous payez uniquement pour fois hello lorsqu’il exécute un travail.  Pour plus d'informations, consultez [Présentation d'Azure Data Lake Analytics](data-lake-analytics-overview.md).  

### <a name="create-accounts"></a>Création de comptes
      azure datalake analytics account create "<Data Lake Analytics Account Name>" "<Azure Location>" "<Resource Group Name>" "<Default Data Lake Account Name>"


### <a name="update-accounts"></a>Mise à jour de comptes
Hello commande suivante met à jour les propriétés de hello d’un compte d’Analytique Data Lake existant

    azure datalake analytics account set "<Data Lake Analytics Account Name>"


### <a name="list-accounts"></a>Énumérer les comptes
Énumérer les comptes Data Lake Analytics 

    azure datalake analytics account list

Répertorier les comptes Data Lake Analytics dans un groupe de ressources spécifique

    azure datalake analytics account list -g "<Azure Resource Group Name>"

Obtenir des détails sur un compte Data Lake Analytics spécifique

    azure datalake analytics account show -g "<Azure Resource Group Name>" -n "<Data Lake Analytics Account Name>"

### <a name="delete-data-lake-analytics-accounts"></a>Supprimer les comptes Data Lake Analytics
      azure datalake analytics account delete "<Data Lake Analytics Account Name>"


<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-account-data-sources"></a>Gestion des sources de données du compte
Analytique lac de données prend en charge actuellement les hello les sources de données suivantes :

* [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md)
* [Azure Storage](../storage/common/storage-introduction.md)

Lorsque vous créez un compte Analytique, vous devez désigner un compte de stockage par défaut de stockage de LAC de données Azure compte toobe hello. Hello compte de stockage par défaut ADL sert toostore métadonnée de la tâche et le travail de journaux d’audit. Après la création d'un compte Analytics, vous pouvez ajouter des comptes Data Lake Storage et/ou des comptes Azure Storage supplémentaires. 

### <a name="find-hello-default-adl-storage-account"></a>Recherchez le compte de stockage ADL hello par défaut
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

valeur de Hello est répertorié sous propriétés : datalakeStoreAccount:name.

### <a name="add-additional-azure-blob-storage-accounts"></a>Ajouter des comptes de stockage d'objets Blob Azure supplémentaires
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -b "<Azure Blob Storage Account Short Name>" -k "<Azure Storage Account Key>"

> [!NOTE]
> Seuls les noms courts Blob Storage sont pris en charge.  N'utilisez pas de nom de domaine complet, comme « myblob.blob.core.windows.net ».
> 
> 

### <a name="add-additional-data-lake-store-accounts"></a>Ajouter des comptes Data Lake Store supplémentaires
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -l "<Data Lake Store Account Name>" [-d]

[-d] est un tooindicate commutateur facultatif si hello lac de données ajouté est le compte Data Lake n’hello par défaut. 

### <a name="update-existing-data-source"></a>Mettre à jour la source de données existante
tooset une valeur par défaut de hello toobe existante Data Lake Store compte :

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -l "<Azure Data Lake Store Account Name>" -d

tooupdate une clé de compte de stockage Blob :

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -b "<Blob Storage Account Name>" -k "<New Blob Storage Account Key>"

### <a name="list-data-sources"></a>Répertorier les sources de données :
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

![Data Lake Analytics : énumérer les sources de données](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-data-source.png)

### <a name="delete-data-sources"></a>Supprimer des sources de données :
toodelete un compte Data Lake Store :

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Azure Data Lake Store Account Name>"

toodelete un compte de stockage d’objets Blob :

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Blob Storage Account Name>"

## <a name="manage-jobs"></a>Gestion des travaux
Vous devez disposer d'un compte Data Lake Analytics avant de pouvoir créer un travail.  Pour plus d'informations, consultez [Gestion des comptes Data Lake Analytics](#manage-accounts).

### <a name="list-jobs"></a>Répertorier les travaux
      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"

![Data Lake Analytics : énumérer les sources de données](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-jobs.png)

### <a name="get-job-details"></a>Obtenir les détails du travail
      azure datalake analytics job show -n "<Data Lake Analytics Account Name>" -j "<Job ID>"

### <a name="submit-jobs"></a>Soumettre les travaux
> [!NOTE]
> priorité par défaut de Hello d’une tâche est comprise entre 1000 et hello par défaut de parallélisme pour un travail est 1.
> 
> 

    azure datalake analytics job create  "<Data Lake Analytics Account Name>" "<Job Name>" "<Script>"

### <a name="cancel-jobs"></a>Annuler les travaux
Utilisez l’id de tâche hello liste commande toofind hello et utilisez annulation du travail toocancel hello.

      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"
      azure datalake analytics job cancel "<Data Lake Analytics Account Name>" "<Job ID>"

## <a name="manage-catalog"></a>Gestion du catalogue
catalogue de Hello U-SQL est utilisé toostructure données et le code afin qu’ils peuvent être partagés par les scripts U-SQL. catalogue de Hello permet hello performances maximales des données dans Azure Data Lake. Pour plus d'informations, consultez [Utilisation du catalogue U-SQL](data-lake-analytics-use-u-sql-catalog.md).

### <a name="list-catalog-items"></a>Répertorier les éléments du catalogue
    #List databases
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t database

    #List tables
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t table

les types de Hello incluent la base de données, schéma, assembly, source de données externe, table, fonction table ou des statistiques de table.

<!-- ################################ -->
<!-- ################################ -->
## <a name="use-arm-groups"></a>Utilisez des groupes ARM
Les applications sont généralement constituées de nombreux composants, par exemple une application web, base de données, serveur de base de données, stockage et services tiers. Azure Resource Manager (ARM) vous permet de toowork avec des ressources dans votre application comme une tooas de groupe, ou un groupe de ressources Azure hello. Vous pouvez déployer, mettre à jour, analyser ou supprimer toutes les ressources de hello pour votre application dans une opération unique et coordonnée. Vous utilisez un modèle de déploiement pouvant fonctionner avec différents environnements (environnements de test, intermédiaire et de production). Vous pouvez de clarifier la facturation pour votre organisation en consultant les coûts de hello reportées pour l’ensemble du groupe hello. Pour plus d'informations, consultez [Présentation d'Azure Resource Manager](../azure-resource-manager/resource-group-overview.md). 

Un service de données Lake Analytique peut inclure hello suivant des composants :

* Compte Azure Data Lake Analytics
* Compte Azure Data Lake Storage par défaut requis
* Comptes Azure Data Lake Storage supplémentaires
* Comptes Azure Storage supplémentaires

Vous pouvez créer tous ces composants sous un toomake de groupe ARM les toomanage plus facile.

![Compte et stockage Azure Data Lake Analytics](./media/data-lake-analytics-manage-use-portal/data-lake-analytics-arm-structure.png)

Un compte Analytique lac de données et les comptes de stockage dépendant de hello doivent être placés dans hello même centre de données Azure.
groupe de Hello ARM peut cependant se trouver dans un autre centre de données.  

## <a name="see-also"></a>Voir aussi
* [Vue d'ensemble de Microsoft Azure Data Lake Analytics](data-lake-analytics-overview.md)
* [Prise en main des analyses Data Lake à l’aide du portail Azure](data-lake-analytics-get-started-portal.md)
* [Gérer les analyses Azure Data Lake à l’aide du portail Azure](data-lake-analytics-manage-use-portal.md)
* [Surveiller et résoudre les problèmes des tâches d’analyse Azure Data Lake à l’aide du portail Azure](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)

