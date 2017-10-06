---
title: "Didacticiel Data Factory : premier pipeline de données | Microsoft Docs"
description: "Ce didacticiel Azure Data Factory vous montre comment toocreate et la planification d’une fabrique de données qui traite les données à l’aide de la ruche de script sur un cluster Hadoop."
services: data-factory
keywords: didacticiel azure data factory, cluster hadoop, hadoop hive
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
ms.assetid: 81f36c76-6e78-4d93-a3f2-0317b413f1d0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: ed9c0ade4500d4ac1f7c2c2312c1fa675e0b1f02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-pipeline-tootransform-data-using-hadoop-cluster"></a>Didacticiel : Créer votre premier pipeline tootransform des données à l’aide de cluster Hadoop
> [!div class="op_single_selector"]
> * [Vue d’ensemble et étapes préalables requises](data-factory-build-your-first-pipeline.md)
> * [Portail Azure](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [modèle Azure Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
> * [API REST](data-factory-build-your-first-pipeline-using-rest-api.md)

Dans ce didacticiel, vous allez générer votre première fabrique de données Azure avec un pipeline de données. pipeline de Hello transforme les données d’entrée en exécutant le script Hive sur un cluster Azure HDInsight (Hadoop) tooproduce des données sortie.  

Cet article fournit la vue d’ensemble et conditions préalables requises pour le didacticiel de hello. Après avoir terminé la configuration requise de hello, vous pouvez effectuer didacticiel hello à l’aide de hello suivant outils/kits de développement logiciel : portail Azure, Visual Studio, PowerShell, le modèle de gestionnaire de ressources, les API REST. Sélectionnez une des options de hello dans la liste déroulante de hello en hello début (ou) des liens à fin hello de ce didacticiel de hello toodo article en utilisant l’une de ces options.    

## <a name="tutorial-overview"></a>Vue d’ensemble du didacticiel
Dans ce didacticiel, vous effectuez hello comme suit :

1. Création d'une **fabrique de données**. Une fabrique de données peut contenir un ou plusieurs pipelines de données qui déplacent et transforment des données. 

    Dans ce didacticiel, vous créez un pipeline dans la fabrique de données hello. 
2. Création d'un **pipeline**. Un pipeline peut avoir une ou plusieurs activités (exemples : activité de copie, activité Hive HDInsight). Cet exemple utilise hello activité HDInsight Hive qui exécute un script Hive sur un cluster HDInsight Hadoop. script de Hello crée d’abord une table de références hello des données de journal web brutes stockées dans le stockage d’objets blob Azure, puis partitions hello des données brutes par année et mois.

    Dans ce didacticiel, pipeline de hello utilise les données de tootransform d’activité de la ruche hello en exécutant une requête Hive sur un cluster Azure HDInsight Hadoop. 
3. Créer des **services liés**. Vous créez un service lié de toolink un magasin de données ou d’une fabrique de données de calcul service toohello. Un magasin de données tels que le stockage Azure conserve les données d’entrée/sortie des activités dans le pipeline de hello. Un service de calcul comme un cluster HDInsight Hadoop traite/transforme des données.

    Dans ce didacticiel, vous allez créer deux services liés : **Azure Storage** et **Azure HDInsight**. Hello le stockage Azure lié à des liens de service un compte de stockage Azure qui contient la fabrique de données toohello hello les données d’entrée/sortie. HDInsight Azure lié à des liens de service un cluster Azure HDInsight qui est la fabrique de données utilisé tootransform données toohello. 
3. Créer des **jeux de données**d’entrée et de sortie. Un jeu de données d’entrée représente une entrée hello pour une activité dans le pipeline de hello et un jeu de données de sortie sortie hello pour l’activité de hello.

    Ce didacticiel, hello d’entrée et la sortie de jeux de données spécifier des emplacements d’entrée et les données de sortie dans hello stockage d’objets Blob Azure. Hello service lié Azure Storage spécifie quel compte de stockage Azure est utilisé. Un jeu de données d’entrée spécifie où se trouvent les fichiers d’entrée hello et un jeu de données de sortie spécifie l’emplacement des fichiers de sortie hello. 


Consultez [Introduction tooAzure Data Factory](data-factory-introduction.md) article pour une présentation détaillée de la fabrique de données Azure.
  
Voici hello **affichage des diagrammes** de fabrique de données exemple hello vous générez dans ce didacticiel. **MyFirstPipeline** a une activité de type Hive qui utilise le jeu de données **AzureBlobInput** comme une entrée et génère le jeu de données **AzureBlobOutput** en tant que sortie. 

![Vue Diagramme dans le didacticiel Data Factory](media/data-factory-build-your-first-pipeline/data-factory-tutorial-diagram-view.png)


Dans ce didacticiel, **inputdata** dossier Hello **adfgetstarted** conteneur d’objets blob Azure contient un fichier nommé input.log. Ce fichier journal contient les entrées de trois mois : janvier, février et mars 2016. Voici les lignes d’exemple hello pour chaque mois dans le fichier d’entrée de hello. 

```
2016-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871 
2016-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2016-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

Lorsque le fichier de hello est traité par le pipeline hello avec activité de la ruche HDInsight, activité hello s’exécute un script Hive sur un cluster HDInsight de hello et partitions d’entrée de données par année et mois. script de Hello crée trois dossiers de sortie qui contient un fichier avec des entrées à partir de chaque mois.  

```
adfgetstarted/partitioneddata/year=2016/month=1/000000_0
adfgetstarted/partitioneddata/year=2016/month=2/000000_0
adfgetstarted/partitioneddata/year=2016/month=3/000000_0
```

À partir des lignes d’exemple hello ci-dessus, hello tout d’abord (avec 2016-01-01) est écrite toohello 000000_0 fichier dans les mois hello = 1 dossier. De même, hello deuxième écrit toohello fichier dans les mois hello = 2 dossier et hello troisième toohello fichier est écrite dans les mois hello = 3 dossier.  

## <a name="prerequisites"></a>Composants requis
Avant de commencer ce didacticiel, vous devez disposer de hello suivant des conditions préalables :

1. **Un abonnement Azure** : si vous n’en avez pas, vous pouvez créer un compte en quelques minutes pour une évaluation gratuite. Consultez hello [version d’évaluation gratuite](https://azure.microsoft.com/pricing/free-trial/) l’article sur la façon dont vous pouvez obtenir un compte d’évaluation gratuit.
2. **Le stockage Azure** : vous utilisez un compte de stockage Azure de standard à usage général pour stocker les données de hello dans ce didacticiel. Si vous n’avez pas un compte de stockage Azure de standard à usage général, consultez hello [créer un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account) l’article. Une fois que vous avez créé le compte de stockage hello, notez hello **nom de compte** et **clé d’accès**. Consultez [Affichage, copie et régénération de clés d’accès de stockage](../storage/common/storage-create-storage-account.md#view-and-copy-storage-access-keys).
3. Téléchargez et lisez le fichier de requête Hive hello (**HQL**) situé à : [https://adftutorialfiles.blob.core.windows.net/hivetutorial/partitionweblogs.hql](https://adftutorialfiles.blob.core.windows.net/hivetutorial/partitionweblogs.hql). Cette requête transforme les données de sortie de données d’entrée tooproduce. 
4. Téléchargez et lisez le fichier d’entrée d’exemple hello (**input.log**) situé à : [https://adftutorialfiles.blob.core.windows.net/hivetutorial/input.log](https://adftutorialfiles.blob.core.windows.net/hivetutorial/input.log)
5. Créez un conteneur de blobs nommé **adfgetstarted** dans votre stockage Blob Azure. 
6. Télécharger **partitionweblogs.hql** toohello de fichiers **script** dossier Bonjour **adfgetstarted** conteneur. Utilisez des outils tels que [l’Explorateur de stockage Microsoft Azure](http://storageexplorer.com/). 
7. Télécharger **input.log** toohello de fichiers **inputdata** dossier Bonjour **adfgetstarted** conteneur. 

Après avoir terminé la configuration requise de hello, sélectionnez une des hello suivant outils/kits de développement logiciel toodo hello didacticiel : 

- [Portail Azure](data-factory-build-your-first-pipeline-using-editor.md)
- [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
- [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
- [modèle Azure Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
- [API REST](data-factory-build-your-first-pipeline-using-rest-api.md)

Le portail Azure et Visual Studio proposent une méthode utilisant l’interface utilisateur graphique pour créer vos fabriques de données. Quant aux options fournies par l’API REST, le modèle Resource Manager et PowerShell, elles vous permettent de créer vos fabriques de données via des scripts et des programmes.

> [!NOTE]
> le pipeline de données Hello dans ce didacticiel transforme les données de sortie de données d’entrée tooproduce. Elle ne copie pas les données à partir d’un magasin de données de destination source données magasin tooa. Pour obtenir un didacticiel sur la façon de toocopy les données à l’aide d’Azure Data Factory, consultez [didacticiel : copier des données à partir du stockage d’objets Blob tooSQL de base de données](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> Vous pouvez chaîner les deux activités (exécutée une activité après l’autre) en définissant le dataset de sortie hello d’une activité hello d’entrée dataset Hello autre activité. Pour plus d’informations, voir [Planification et exécution dans Data Factory](data-factory-scheduling-and-execution.md). 





  
