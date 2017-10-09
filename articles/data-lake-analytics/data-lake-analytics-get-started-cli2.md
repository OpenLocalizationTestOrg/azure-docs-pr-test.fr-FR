---
title: "aaaGet main Analytique de LAC de données Azure à l’aide d’Azure CLI 2.0 | Documents Microsoft"
description: "Découvrez comment toouse hello une Interface de ligne de Azure 2.0 toocreate un compte Analytique lac de données, créez une tâche Analytique lac de données à l’aide de U-SQL et envoi de la tâche de hello. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: jgao
ms.openlocfilehash: c4e91c0d3526e4932c2948c0a326d4cedc985791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-cli-20"></a>Prise en main d’Azure Data Lake Analytics à l’aide d’Azure CLI 2.0
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

Dans ce didacticiel, vous développez un travail qui lit un fichier TSV (valeurs séparées par des tabulations) et le convertit en fichier CSV (valeurs séparées par des virgules). toogo hello même didacticiel d’autres prises en charge par le biais des outils, utiliser la liste déroulante hello haut hello de cette section.

## <a name="prerequisites"></a>Composants requis
Avant de commencer ce didacticiel, vous devez disposer des éléments suivants de hello :

* **Un abonnement Azure**. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Azure CLI 2.0**. Consultez [Installation et configuration de l’interface de ligne de commande Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).

## <a name="log-in-tooazure"></a>Connectez-vous à tooAzure

toolog dans tooyour abonnement Azure :

```
azurecli
az login
```

Vous êtes demandé toobrowse tooa URL et que vous entrez un code d’authentification.  Puis suivez hello instructions tooenter vos informations d’identification.

Une fois que vous êtes connecté, la commande de connexion hello répertorie vos abonnements.

toouse un abonnement spécifique :

```
az account set --subscription <subscription id>
```

## <a name="create-data-lake-analytics-account"></a>Créer un compte Analytique Data Lake
Vous devez disposer d’un compte Data Lake Analytics avant de pouvoir exécuter des travaux quelconques. toocreate un compte Analytique lac de données, vous devez spécifier hello éléments suivants :

* **Groupe de ressources Azure**. Un compte Data Lake Analytics doit être créé au sein d’un groupe de ressources Azure. [Le Gestionnaire de ressources Azure](../azure-resource-manager/resource-group-overview.md) vous permet de toowork avec des ressources hello dans votre application en tant que groupe. Vous pouvez déployer, mettre à jour ou supprimer toutes les ressources de hello pour votre application dans une opération unique et coordonnée.  

toolist hello des groupes de ressource sous votre abonnement :

```
az group list
```

toocreate un groupe de ressources :

```
az group create --name "<Resource Group Name>" --location "<Azure Location>"
```

* **Nom du compte Data Lake Analytics**. Chaque compte Data Lake Analytics porte un nom.
* **Emplacement**. Utilisez une des centres de données Azure hello qui prend en charge les données de LAC Analytique.
* **Compte Data Lake Store par défaut** : chaque compte Data Lake Analytics possède un compte Data Lake Store par défaut.

toolist hello Data Lake Store compte existant :

```
az dls account list
```

toocreate un nouveau compte Data Lake Store :

```azurecli
az dls account create --account "<Data Lake Store Account Name>" --resource-group "<Resource Group Name>"
```

Utilisez hello suivant de syntaxe toocreate un compte Analytique lac de données :

```
az dla account create --account "<Data Lake Analytics Account Name>" --resource-group "<Resource Group Name>" --location "<Azure location>" --default-data-lake-store "<Default Data Lake Store Account Name>"
```

Après avoir créé un compte, vous pouvez utiliser les hello suivant des comptes de commandes toolist hello et afficher les détails du compte :

```
az dla account list
az dla account show --account "<Data Lake Analytics Account Name>"            
```

## <a name="upload-data-toodata-lake-store"></a>Télécharger des données tooData Lake Store
Dans ce didacticiel, vous traitez des journaux de recherche.  journal des recherches Hello peut être stockée dans le magasin de LAC de données ou le stockage Blob Azure.

Hello portail Azure fournit une interface utilisateur pour la copie de certains exemples données fichiers toohello par défaut compte Data Lake Store, qui incluent un fichier journal de recherche. Consultez [préparer les données sources](data-lake-analytics-get-started-portal.md) compte Data Lake Store de tooupload hello données toohello par défaut.

fichiers tooupload à l’aide de la version 2.0 CLI, utilisez hello suivant les commandes :

```
az dls fs upload --account "<Data Lake Store Account Name>" --source-path "<Source File Path>" --destination-path "<Destination File Path>"
az dls fs list --account "<Data Lake Store Account Name>" --path "<Path>"
```

Analytique Data Lake peut également accéder au stockage d’objets blobs Azure.  Pour télécharger le stockage d’objets Blob de données tooAzure, consultez [Using hello CLI d’Azure avec le stockage Azure](../storage/common/storage-azure-cli.md).

## <a name="submit-data-lake-analytics-jobs"></a>Envoyer des travaux Analytique Data Lake
travaux de Hello Analytique lac de données est écrites dans hello langage U-SQL. toolearn en savoir plus sur U-SQL, consultez [prise en main langage U-SQL](data-lake-analytics-u-sql-get-started.md) et [U-SQL language eence](http://go.microsoft.com/fwlink/?LinkId=691348).

**toocreate un script de travail Analytique lac de données**

Créez un fichier texte avec le script U-SQL suivant, enregistrez la station de travail hello texte fichier tooyour :

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

Ce script U-SQL lit le fichier de données source hello via **Extractors.Tsv()**, puis crée un fichier csv en utilisant **Outputters.Csv()**.

Ne modifiez pas deux chemins d’accès de hello, sauf si vous copiez le fichier de source de hello dans un autre emplacement.  Analytique de LAC de données crée le dossier de sortie hello si elle n’existe pas.

Il est plus simples toouse chemins d’accès relatifs pour les fichiers stockés sur les comptes Data Lake Store par défaut. Vous pouvez également utiliser des chemins d’accès absolus.  Par exemple :

```
adl://<Data LakeStorageAccountName>.azuredatalakestore.net:443/Samples/Data/SearchLog.tsv
```

Vous devez utiliser des chemins d’accès absolus des fichiers de tooaccess dans les comptes de stockage liés.  syntaxe de Hello pour les fichiers stockés dans le compte de stockage Azure associé est la suivante :

```
wasb://<BlobContainerName>@<StorageAccountName>.blob.core.windows.net/Samples/Data/SearchLog.tsv
```

> [!NOTE]
> Conteneur d’objets Blob Azure avec des objets Blob publics ne sont pas pris en charge.      
> Le conteneur d’objets Blob Azure avec des conteneurs publics n’est pas pris en charge.      
>

**travaux de toosubmit**

Utilisez hello suivant de syntaxe toosubmit un travail.

```
az dla job submit --account "<Data Lake Analytics Account Name>" --job-name "<Job Name>" --script "<Script Path and Name>"
```

Par exemple :

```
az dla job submit --account "myadlaaccount" --job-name "myadlajob" --script @"C:\DLA\myscript.txt"
```

**travaux de toolist et afficher les détails de travail**

```
azurecli
az dla job list --account "<Data Lake Analytics Account Name>"
az dla job show --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

**travaux de toocancel**

```
az dla job cancel --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

## <a name="retrieve-job-results"></a>Récupérer les résultats de travaux

Lorsqu’un travail est terminé, vous pouvez utiliser hello suivant des fichiers de sortie de commandes toolist hello et télécharger les fichiers de hello :

```
az dls fs list --account "<Data Lake Store Account Name>" --source-path "/Output" --destination-path "<Destintion>"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv" --length 128 --offset 0
az dls fs downlod --account "<Data Lake Store Account Name>" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "<Destination Path and File Name>"
```

Par exemple :

```
az dls fs downlod --account "myadlsaccount" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "C:\DLA\myfile.csv"
```

## <a name="pipelines-and-recurrences"></a>Pipelines et récurrences

**Obtenir des informations sur les pipelines et les récurrences**

Hello d’utilisation `az dla job pipeline` commandes informations de pipeline toosee hello envoyés précédemment des travaux.

```
az dla job pipeline list --account "<Data Lake Analytics Account Name>"

az dla job pipeline show --account "<Data Lake Analytics Account Name>" --pipeline-identity "<Pipeline ID>"
```

Hello d’utilisation `az dla job recurrence` commandes d’informations sur la périodicité toosee hello pour les travaux soumis précédemment.

```
az dla job recurrence list --account "<Data Lake Analytics Account Name>"

az dla job recurrence show --account "<Data Lake Analytics Account Name>" --recurrence-identity "<Recurrence ID>"
```

## <a name="next-steps"></a>Étapes suivantes

* toosee hello Data Lake Analytique CLI 2.0 de document de référence, consultez [Analytique lac de données](https://docs.microsoft.com/cli/azure/dla).
* toosee hello Data Lake Store CLI 2.0 de document de référence, consultez [Data Lake Store](https://docs.microsoft.com/cli/azure/dls).
* toosee une requête plus complexe, consultez [site Web d’analyse se connecte à l’aide d’Analytique de LAC de données Azure](data-lake-analytics-analyze-weblogs.md).
