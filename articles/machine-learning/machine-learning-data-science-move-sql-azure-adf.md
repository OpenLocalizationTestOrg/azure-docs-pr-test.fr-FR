---
title: "aaaMove des données à partir d’un tooSQL de SQL Server sur site Azure avec Azure Data Factory | Documents Microsoft"
description: "Configurer un pipeline de définition d’application qui se compose de deux activités de migration de données qui déplacent les données entre eux sur une base quotidienne entre bases de données locale et dans le cloud de hello."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 36837c83-2015-48be-b850-c4346aa5ae8a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 7f7e78c7a84a259539221d3235b76bb5a3cf9866
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-on-premises-sql-server-toosql-azure-with-azure-data-factory"></a>Déplacement des données à partir d’un ordinateur local SQL server tooSQL Azure avec Azure Data Factory
Cette rubrique montre comment toomove des données à partir d’un tooa de base de données SQL Server locale base de données SQL Azure via à l’aide du stockage d’objets Blob Azure hello fabrique de données Azure (ADF).

Pour une table qui résume les différentes options de déplacement tooan de données base de données SQL Azure, consultez [déplacer les données tooan base de données SQL Azure pour Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).

## <a name="intro"></a>Présentation : Nouveautés ADF et quand il doit être utilisé toomigrate données ?
Azure Data Factory est un service d’intégration des données cloud entièrement géré qui orchestre et automatise le déplacement de hello et la transformation de données. concept clé de Hello dans le modèle de définition d’application hello est le pipeline. Un pipeline est un regroupement logique des activités, chacune définissant hello actions tooperform sur les données de hello contenues dans les jeux de données. Services liés sont des informations de hello toodefine utilisé nécessaires pour les ressources de données de Data Factory tooconnect toohello.

Avec la définition d’application, les services de traitement de données existants peuvent être composées dans des pipelines de données qui sont hautement disponible et gérée dans le cloud de hello. Ces pipelines de données peuvent être planifiée tooingest, préparer, transformer, analyser et publier des données et ADF gère et orchestre les données complexes hello et le traitement des dépendances. Solutions peuvent être cloud hello rapidement générées et déployées dans, la connexion d’un nombre croissant de locaux et cloud des sources de données.

Utilisez plutôt ADF :

* Lorsque besoins toobe migré en permanence dans un scénario hybride qui accède à la fois des données sur site et ressources de cloud
* Lorsque les données de salutation sont traitées ou besoins toobe modifiée ou avoir une logique métier ajouté tooit en cours de migration.

ADF permet hello de planification et de surveillance des travaux à l’aide de simples scripts JSON qui gèrent le déplacement de hello des données sur une base périodique. ADF dispose également d'autres fonctionnalités comme la prise en charge des opérations complexes. Pour plus d’informations sur la définition d’application, consultez documentation hello [fabrique de données Azure (ADF)](https://azure.microsoft.com/services/data-factory/).

## <a name="scenario"></a>Hello scénario
Nous allons configurer un pipeline ADF qui se compose de deux activités de migration de données. Ensemble, ils passent données quotidiennement entre une base de données SQL locale et une base de données SQL Azure dans le cloud de hello. Hello deux activités sont :

* copier des données d’une tooan de base de données SQL Server sur site compte de stockage d’objets Blob Azure
* copier des données à partir de tooan de compte de stockage d’objets Blob Azure hello base de données SQL Azure.

> [!NOTE]
> Hello les étapes indiquées ici ont été adaptées à partir de hello plus didacticiel fourni par l’équipe ADF hello : [déplacement des données entre des sources locales et cloud avec la passerelle de gestion des données](../data-factory/data-factory-move-data-between-onprem-and-cloud.md) toohello les sections correspondantes de cette rubrique de référence Vous trouverez lorsque cela est approprié.
>
>

## <a name="prereqs"></a>Configuration requise
Ce didacticiel part du principe que vous disposez de :

* Un **abonnement Azure**. Si vous n’avez pas d’abonnement, vous pouvez vous inscrire à un [essai gratuit](https://azure.microsoft.com/pricing/free-trial/).
* Un **compte de stockage Azure**. Vous utilisez un compte de stockage Azure pour stocker les données de hello dans ce didacticiel. Si vous n’avez pas un compte de stockage Azure, consultez hello [créer un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account) l’article. Une fois que vous avez créé le compte de stockage hello, vous devez le compte de hello tooobtain clé utilisé le stockage de hello tooaccess. Voir [Gérer vos clés d’accès de stockage](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).
* Accès tooan **base de données SQL Azure**. Si vous devez configurer une base de données SQL Azure, hello phrase sujet [prise en main de Microsoft Azure SQL Database ](../sql-database/sql-database-get-started.md) fournit des informations sur la façon de tooprovision une nouvelle instance de la base de données SQL Azure.
* **Azure PowerShell** installé et configuré localement. Pour obtenir des instructions, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).

> [!NOTE]
> Cette procédure utilise hello [portail Azure](https://portal.azure.com/).
>
>

## <a name="upload-data"></a>Téléchargement hello données tooyour local SQL Server
Nous utilisons hello [NYC Taxi dataset](http://chriswhong.com/open-data/foil_nyc_taxi/) processus de migration toodemonstrate hello. Hello NYC Taxi dataset est disponible, comme indiqué dans cette publication, sur le stockage d’objets blob Azure [NYC Taxi données](http://www.andresmh.com/nyctaxitrips/). les données de salutation possède deux fichiers, fichier hello trip_data.csv, qui contient les détails de voyage, et fichier hello trip_far.csv, qui contient les détails des prix hello payé pour chaque sortie. Un échantillon et une description de ces fichiers sont fournis dans la [description du jeu de données des voyages NYC Taxi](machine-learning-data-science-process-sql-walkthrough.md#dataset).

Vous pouvez adapter procédure hello fourni ici ensemble tooa de vos propres données ou suivez les étapes de hello comme décrit à l’aide de hello NYC Taxi le jeu de données. hello de tooupload NYC Taxi le jeu de données dans votre base de données SQL Server locale, procédez comme procédure hello [importer en bloc des données dans la base de données SQL Server](machine-learning-data-science-process-sql-walkthrough.md#dbload). Ces instructions concernent un serveur SQL Server sur une Machine virtuelle de Azure, mais la procédure hello pour le téléchargement toohello local SQL Server est hello identiques.

## <a name="create-adf"></a> Création d’une Azure Data Factory
Hello des instructions sur la création d’une fabrique de données Azure et un groupe de ressources Bonjour [portail Azure](https://portal.azure.com/) sont fournies [créer une fabrique de données Azure](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory). Nom hello nouvelle ADF instance *adfdsp* et nom du groupe de ressources hello créé *adfdsprg*.

## <a name="install-and-configure-up-hello-data-management-gateway"></a>Installer et configurer des hello passerelle de gestion des données
tooenable vos pipelines dans un toowork de fabrique de données Azure avec un serveur de SQL Server locale, vous devez tooadd sous la forme d’une fabrique de données toohello Service lié. toocreate un Service lié pour un ordinateur local SQL Server, vous devez :

* Téléchargez et installez la passerelle de gestion des données de Microsoft sur l’ordinateur local de hello.
* configurer service hello lié pour passerelle hello toouse des source de données hello localement.

Hello passerelle de gestion des données sérialise et désérialise les données source et le récepteur de hello sur ordinateur hello où il est hébergé.

Pour obtenir des détails et des instructions d’installation sur la passerelle de gestion des données, consultez [Déplacement de données entre des sources locales et le cloud à l’aide de la passerelle de gestion des données](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)

## <a name="adflinkedservices"></a>Créer des ressources de données de services liés tooconnect toohello
Un service lié définit les informations de hello nécessaires pour la ressource de données Azure Data Factory tooconnect tooa. procédure pas à pas de Hello pour la création de services liés est fourni dans [créer des services liés](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services).

Dans ce scénario, nous avons trois ressources pour lesquelles les services liés sont nécessaires.

1. [Service lié pour SQL Server local](#adf-linked-service-onprem-sql)
2. [Service lié pour Azure Blob Storage](#adf-linked-service-blob-store)
3. [Service lié pour base de données Azure SQL](#adf-linked-service-azure-sql)

### <a name="adf-linked-service-onprem-sql"></a>Service lié pour base de données SQL Server locale
service de hello lié toocreate pour hello local SQL Server :

* Cliquez sur hello **magasin de données** dans la page d’accueil hello ADF sur le portail Azure Classic
* Sélectionnez **SQL** et entrez hello *nom d’utilisateur* et *mot de passe* les informations d’identification pour hello local SQL Server. Vous devez servername de hello tooenter comme un **nom de l’instance complet servername barre oblique inverse (nomserveur\nominstance)**. Hello du nom de service lié *adfonpremsql*.

### <a name="adf-linked-service-blob-store"></a>Service lié pour les objets blob
toocreate hello service lié pour le compte de stockage d’objets Blob Azure hello :

* Cliquez sur hello **magasin de données** dans la page d’accueil hello ADF sur le portail Azure Classic
* Sélectionnez **Azure Storage Account**.
* entrez hello du compte clé et le conteneur du nom du stockage d’objets Blob Azure. Hello du nom du Service lié *adfds*.

### <a name="adf-linked-service-azure-sql"></a>Service lié pour la base de données SQL Azure
toocreate hello service lié pour hello de base de données SQL Azure :

* Cliquez sur hello **magasin de données** dans la page d’accueil hello ADF sur le portail Azure Classic
* Sélectionnez **SQL Azure** et entrez hello *nom d’utilisateur* et *mot de passe* informations d’identification pour hello de base de données SQL Azure. Hello *nom d’utilisateur* doit être spécifié en tant que  *user@servername* .   

## <a name="adf-tables"></a>Définir et créer des tables toospecify comment tooaccess hello des jeux de données
Créer des tables qui spécifient la structure de hello, l’emplacement et la disponibilité de jeux de données hello avec hello script basé sur les procédures suivantes. Fichiers JSON sont des tables de hello toodefine utilisé. Pour plus d’informations sur la structure hello de ces fichiers, consultez [jeux de données](../data-factory/data-factory-create-datasets.md).

> [!NOTE]
> Vous devez exécuter hello `Add-AzureAccount` applet de commande avant d’exécuter hello [New-AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx) tooconfirm d’applet de commande qui hello abonnement Azure à droite est sélectionné pour l’exécution de la commande hello. Pour obtenir la documentation de cette applet de commande, consultez [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0).
>
>

définitions Hello JSON dans les tables de hello utilisent hello nom :

* Hello **nom de la table** Bonjour local SQL server est *nyctaxi_data*
* Hello **nom du conteneur** Bonjour Azure Blob Storage est compte *containername*  

Trois définitions de table sont nécessaires pour ce pipeline ADF :

1. [Table SQL locale](#adf-table-onprem-sql)
2. [Table d'objets blob ](#adf-table-blob-store)
3. [Table SQL Azure](#adf-table-azure-sql)

> [!NOTE]
> Ces procédures utilisent Azure PowerShell toodefine et créer des activités ADF hello. Mais ces tâches peuvent également être accomplies à l’aide de hello portail Azure. Pour plus d’informations, consultez [Créer des jeux de données](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets).
>
>

### <a name="adf-table-onprem-sql"></a>Table SQL locale
définition de la table Hello pour hello local SQL Server est spécifié dans hello le fichier JSON suivant :

        {
            "name": "OnPremSQLTable",
            "properties":
            {
                "location":
                {
                "type": "OnPremisesSqlServerTableLocation",
                "tableName": "nyctaxi_data",
                "linkedServiceName": "adfonpremsql"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1,   
                "waitOnExternal":
                {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
                }

                }
            }
        }

les noms de colonne Hello n’étaient pas inclus ici. Vous pouvez sélectionner des noms de colonne hello en les incluant ici (pour plus d’informations, consultez hello [documentation d’ADF](../data-factory/data-factory-data-movement-activities.md) rubrique.

Copier la définition de JSON hello de table de hello dans un fichier appelé *onpremtabledef.json* de fichier et l’enregistrer tooa connus d’emplacement (ici supposé toobe *C:\temp\onpremtabledef.json*). Créer les table hello dans ADF par hello suivant l’applet de commande PowerShell de Azure :

    New-AzureDataFactoryTable -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp –File C:\temp\onpremtabledef.json


### <a name="adf-table-blob-store"></a>Table d'objets blob
Définition de table hello pour hello de sortie blob emplacement est suivante hello (cela mappe les données de hello ingéré à partir de l’objet blob de tooAzure local) :

        {
            "name": "OutputBlobTable",
            "properties":
            {
                "location":
                {
                "type": "AzureBlobLocation",
                "folderPath": "containername",
                "format":
                {
                "type": "TextFormat",
                "columnDelimiter": "\t"
                },
                "linkedServiceName": "adfds"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1
                }
            }
        }

Copier la définition de JSON hello de table de hello dans un fichier appelé *bloboutputtabledef.json* de fichier et l’enregistrer tooa connus d’emplacement (ici supposé toobe *C:\temp\bloboutputtabledef.json*). Créer les table hello dans ADF par hello suivant l’applet de commande PowerShell de Azure :

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\bloboutputtabledef.json  

### <a name="adf-table-azure-sq"></a>Table SQL Azure
Définition de table hello pour hello de sortie SQL Azure est suivante hello (ce schéma mappe les données hello provenant d’un objet blob de hello) :

    {
        "name": "OutputSQLAzureTable",
        "properties":
        {
            "structure":
            [
                { "name": "column1", type": "String"},
                { "name": "column2", type": "String"}                
            ],
            "location":
            {
                "type": "AzureSqlTableLocation",
                "tableName": "your_db_name",
                "linkedServiceName": "adfdssqlazure_linked_servicename"
            },
            "availability":
            {
                "frequency": "Day",
                "interval": 1            
            }
        }
    }

Copier la définition de JSON hello de table de hello dans un fichier appelé *AzureSqlTable.json* de fichier et l’enregistrer tooa connus d’emplacement (ici supposé toobe *C:\temp\AzureSqlTable.json*). Créer les table hello dans ADF par hello suivant l’applet de commande PowerShell de Azure :

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\AzureSqlTable.json  


## <a name="adf-pipeline"></a>Définir et créer le pipeline de hello
Spécifiez les activités de hello appartenant toohello de pipeline et créer un pipeline de hello avec hello script basé sur les procédures suivantes. Un fichier JSON est propriétés de pipeline utilisé toodefine hello.

* Hello script suppose que hello **nom du pipeline** est *AMLDSProcessPipeline*.
* Notez également que nous périodicité hello de hello pipeline toobe est exécutée sur tous les jours base et utilisez hello durée par défaut d’exécution pour le travail hello (0 h 00 UTC).

> [!NOTE]
> Bonjour procédures suivantes utilisent Azure PowerShell toodefine et créer hello ADF pipeline. Toutefois, cette tâche peut également être accomplie à l’aide du portail Azure. Pour plus d’informations, consultez [Création d’un pipeline](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline).
>
>

À l’aide des définitions de table hello fournies précédemment, définition de pipeline hello pour hello QU'ADF est spécifiée comme suit :

        {
            "name": "AMLDSProcessPipeline",
            "properties":
            {
                "description" : "This pipeline has one Copy activity that copies data from an on-premises SQL tooAzure blob",
                 "activities":
                [
                    {
                        "name": "CopyFromSQLtoBlob",
                        "description": "Copy data from on-premises SQL server tooblob",     
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OnPremSQLTable"} ],
                        "outputs": [ {"name": "OutputBlobTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "SqlSource",
                                "sqlReaderQuery": "select * from nyctaxi_data"
                            },
                            "sink":
                            {
                                "type": "BlobSink"
                            }   
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 0,
                            "timeout": "01:00:00"
                        }       

                     },

                    {
                        "name": "CopyFromBlobtoSQLAzure",
                        "description": "Push data tooSql Azure",        
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OutputBlobTable"} ],
                        "outputs": [ {"name": "OutputSQLAzureTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "BlobSource"
                            },
                            "sink":
                            {
                                "type": "SqlSink",
                                "WriteBatchTimeout": "00:5:00",                
                            }            
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 2,
                            "timeout": "02:00:00"
                        }
                     }
                ]
            }
        }

Copiez cette définition JSON de pipeline de hello dans un fichier appelé *pipelinedef.json* de fichier et l’enregistrer tooa connus d’emplacement (ici supposé toobe *C:\temp\pipelinedef.json*). Créer le pipeline de hello dans ADF avec hello suivant l’applet de commande PowerShell de Azure :

    New-AzureDataFactoryPipeline  -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\pipelinedef.json

Vérifiez que vous pouvez voir les pipeline hello sur hello ADF Bonjour portail classique Azure s’affichent comme suit (si vous cliquez sur le diagramme de hello)

![Pipeline ADF](media/machine-learning-data-science-move-sql-azure-adf/DJP1kji.png)

## <a name="adf-pipeline-start"></a>Démarrer hello Pipeline
pipeline de Hello peut maintenant être exécuté à l’aide de hello de commande suivante :

    Set-AzureDataFactoryPipelineActivePeriod -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp -StartDateTime startdateZ –EndDateTime enddateZ –Name AMLDSProcessPipeline

Hello *startdate* et *enddate* toobe remplacée par les dates réelles hello entre lesquels vous souhaitez hello pipeline toorun est nécessaire que les valeurs de paramètre.

Une fois que le pipeline de hello s’exécute, vous devez être en mesure de toosee hello données qui s’affichent dans le conteneur hello sélectionné pour l’objet blob hello, un seul fichier par jour.

Notez que nous n’avons pas réutilisé fonctionnalité hello fournie par les données de toopipe ADF incrémentielle. Pour plus d’informations sur comment toodo cela et autres fonctionnalités fournies par le chargeur automatique, consultez hello [documentation d’ADF](https://azure.microsoft.com/services/data-factory/).
