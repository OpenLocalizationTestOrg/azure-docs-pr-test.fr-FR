---
title: "aaaTen opérations pouvant être exécutées sur hello Machine virtuelle de science des données | Documents Microsoft"
description: "Effectuer diverses exploration de données et les tâches de modélisation sur la science des données hello Machine virtuelle."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 145dfe3e-2bd2-478f-9b6e-99d97d789c62
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: gokuma;weig;bradsev
ms.openlocfilehash: 4dfe22f14f00208c63e26ce44b05123c9ac4b850
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="ten-things-you-can-do-on-hello-data-science-virtual-machine"></a>Dix choses que vous pouvez effectuer sur la science des données hello Machine virtuelle
Hello Machine virtuelle de science des données Microsoft (DSVM) est un environnement de développement de science des données puissant qui permet de vous tooperform diverses tâches de modélisation et exploration de données. Hello environnement est déjà généré et fourni avec les données courantes plusieurs outils analytique qui la rendent facile tooget rapidement en main votre analyse locale, Cloud ou hybride déploiements. Hello DSVM travaille en étroite collaboration avec de nombreux services Azure et est en mesure de tooread et traiter des données qui sont déjà stockées sur Azure, dans l’entrepôt de données SQL Azure, Azure Data Lake, le stockage Azure, ou dans la base de données Azure Cosmos. Elle peut également exploiter d’autres outils d’analyse tels qu’Azure Machine Learning et Azure Data Factory.

Dans cet article nous vous guident la toouse votre tooperform DSVM des tâches différentes pour la science des données et interagir avec d’autres services Azure. Voici quelques-unes des hello opérations pouvant être exécutées sur hello DSVM :

1. Explorer les données et de développer des modèles localement sur hello DSVM à l’aide de Microsoft R Server Python
2. Utilisez un tooexperiment de bloc-notes Notebook avec vos données sur un navigateur à l’aide de Python, 2, 3 de Python, Microsoft R une version d’entreprise prêt de R conçu pour l’évolutivité et performances
3. Rendre opérationnels des modèles créés avec R et Python sur Azure Machine Learning afin que les applications clientes puissent accéder à vos modèles à l'aide d'une interface de services web simple
4. Administrer vos ressources Azure à l’aide du portail Azure ou de PowerShell
5. Augmenter votre espace de stockage et partager des jeux de données / du code à grande échelle avec toute votre équipe en créant un stockage Fichier Azure comme lecteur montable sur votre DSVM
6. Partager du code avec votre équipe à l’aide de GitHub et accéder à votre référentiel à l’aide de hello préinstallées clients Git - interpréteur de commandes Git, Git l’interface graphique utilisateur.
7. Accéder aux différents services de données et d’analytique Azure tels que Stockage Blob Azure, Azure Data Lake, Azure HDInsight (Hadoop), Azure Cosmos DB, Azure SQL Data Warehouse et Database
8. Générer des rapports et tableau de bord à l’aide de hello préinstallé sur hello DSVM Power BI Desktop et les déployer sur le cloud de hello
9. Évoluer dynamiquement votre toomeet DSVM qu'a besoin de votre projet
10. Installer des outils supplémentaires sur votre machine virtuelle   

> [!NOTE]
> Frais d’utilisation supplémentaires s’appliquent pour de nombreux hello supplémentaires de stockage et analytique des services de données répertoriées dans cet article. Reportez-vous toohello [tarification Azure](https://azure.microsoft.com/pricing/) page pour plus d’informations.
> 
> 

**Configuration requise**

* Vous avez besoin d’un abonnement Azure. Vous pouvez vous inscrire à un essai gratuit [ici](https://azure.microsoft.com/free/).
* Les instructions pour la configuration d’un ordinateur de virtuel de science des données sur hello portail Azure sont disponibles au [création d’une machine virtuelle](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm).

## <a name="1-explore-data-and-develop-models-using-microsoft-r-server-or-python"></a>1. Explorer les données et développer des modèles à l'aide de Microsoft R Server ou de Python
Vous pouvez utiliser des langages tels que R et Python toodo analytique de vos données à droite sur hello DSVM.

Pour R, vous pouvez utiliser un bus IDE appelé « Revolution R Enterprise 8.0 » qui se trouvent sur le menu Démarrer de hello ou bureau de hello. Microsoft a fourni des bibliothèques supplémentaires par-dessus hello Open source/CRAN-R tooenable analytique et hello capacité tooanalyze données évolutive supérieure à la taille de la mémoire hello autorisé en effectuant une analyse mémorisé en bloc parallèle. Vous pouvez également installer l’IDE R de votre choix, par exemple [RStudio](https://www.rstudio.com/products/rstudio-desktop/).

Pour Python, vous pouvez utiliser un IDE comme Visual Studio Community Edition qui a hello outils Python pour l’extension de Visual Studio (PTVS) préinstallée. Par défaut, seule une version de base de Python 2.7 est configurée sur PTVS (sans aucune bibliothèque d’analyse comme SciKit, Pandas). Dans l’ordre tooenable Anaconda Python 2.7 et 3.5, vous toodo hello éléments suivants sont nécessaires :

* Créer des environnements personnalisés pour chaque version en naviguant trop**outils** -> **outils Python** -> **environnements Python** , puis en cliquant sur » **+ Personnalisé**« dans hello Visual Studio 2015 Community Edition
* Donner une description et définir l’environnement de hello préfixe les chemins d’accès en tant que *c:\anaconda* Anaconda Python 2.7 ou *c:\anaconda\envs\py35* Anaconda Python 3.5
* Cliquez sur **la détection automatique** , puis **appliquer** environnement de hello toosave.

Voici la configuration de l’environnement personnalisée hello ressemble dans Visual Studio.

![Installation PTVS](./media/machine-learning-data-science-vm-do-ten-things/PTVSSetup.png)

Consultez hello [documentation de PTVS](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) pour plus d’informations sur la façon de toocreate environnements Python.

Maintenant vous configurer toocreate un nouveau projet de Python. Accédez trop**fichier** -> **nouveau** -> **projet** -> **Python** et sélectionnez le type hello de Vous générez l’application Python. Vous pouvez définir l’environnement Python hello hello projet toohello souhaitée version actuelle (Anaconda 2.7 ou 3.5) : avec le bouton hello **environnement de Python**, sélectionnez **ajouter/supprimer des environnements Python**, et puis sélectionnez hello souhaité tooassociate environnement avec un projet de hello. Vous trouverez plus d’informations sur l’utilisation de PTVS sur les produits hello [documentation](https://github.com/Microsoft/PTVS/wiki) page.

## <a name="2-using-a-jupyter-notebook-tooexplore-and-model-your-data-with-python-or-r"></a>2. En utilisant un modèle et un bloc-notes Jupyter tooexplore vos données avec Python ou R
Hello bloc-notes Jupyter est un environnement puissant qui fournit une basée sur navigateur « IDE » pour la modélisation et exploration de données. Vous pouvez utiliser Python 2, 3 de Python ou R (Open Source et hello Microsoft R Server) dans un bloc-notes Jupyter.

toolaunch hello bloc-notes Jupyter sur l’icône de menu de démarrage hello / bureau icône intitulée **bloc-notes Jupyter**. Sur hello DSVM vous pouvez également parcourir trop « https://localhost:9999 / « tooaccess hello Jupiter bloc-notes. S’il vous demande un mot de passe, suivez les instructions fournies dans hello ***comment toocreate un mot de passe fort sur le serveur de jupyter Notebook hello*** section Hello [hello d’approvisionner la Machine virtuelle Microsoft données Science](machine-learning-data-science-provision-vm.md)rubrique toocreate un bloc-notes jupyter de mot de passe fort tooaccess hello. 

Une fois que vous avez ouvert le bloc-notes de hello, vous devez voir un répertoire qui contient les quelques ordinateurs portables d’exemple qui sont intégrées dans hello DSVM. Vous pouvez désormais :

* Cliquez sur le code de hello toosee hello bloc-notes.
* exécuter chaque cellule en appuyant sur **MAJ-ENTRÉE**;
* exécuter le bloc-notes hello en cliquant sur **cellule** -> **exécuter**
* créer un bloc-notes en cliquant sur hello Notebook icône (coin supérieur gauche) et en cliquant sur **nouveau** sur bouton hello droit, puis en choisissant le langage de bloc-notes hello (également appelé noyaux).   

> [!NOTE]
> Nous prenons en charge les Python 2.7 actuellement, de noyau de hello R Python 3.5 et R. prend en charge la programmation dans R Open source ainsi que les entreprise hello évolutive Microsoft R Server.   
> 
> 

Une fois que vous êtes dans le bloc-notes de hello Explorer vos données, générer le modèle de hello, modèle hello à l’aide de votre choix des bibliothèques de test.

## <a name="3-build-models-using-r-or-python-and-operationalize-them-using-azure-machine-learning"></a>3. Générer des modèles avec R ou Python et les rendre opérationnels à l’aide d’Azure Machine Learning
Une fois que vous avez créé et validé votre modèle hello étape suivante consiste généralement toodeploy en production. Ainsi, votre client de prédictions du modèle applications tooinvoke hello sur un en temps réel ou sur une base de mode de traitement par lots. Azure Machine Learning fournit un mécanisme toooperationalize un modèle intégré dans R ou Python.

Lorsque vous rendez opérationnel de votre modèle dans Azure Machine Learning, qui permet aux clients les appels REST toomake passer des paramètres d’entrée et de recevoir des prédictions à partir du modèle de hello en tant que sorties est exposé par un service web.   

> [!NOTE]
> Si vous n'êtes pas encore inscrit pour Azure Machine Learning, vous pouvez obtenir un espace de travail disponible ou un espace de travail standard en visitant hello [Azure Machine Learning Studio](https://studio.azureml.net/) page d’accueil et en cliquant sur « Démarrer ».   
> 
> 

### <a name="build-and-operationalize-python-models"></a>Générer et rendre opérationnels des modèles Python
Voici un extrait de code développé dans un bloc-notes Jupyter de Python qui génère un modèle simple à l’aide de la bibliothèque de hello SciKit-en savoir plus.

    #IRIS classification
    from sklearn import datasets
    from sklearn import svm
    clf = svm.SVC()
    iris = datasets.load_iris()
    X, y = iris.data, iris.target
    clf.fit(X, y)

méthode Hello utilisé toodeploy votre tooAzure de modèles python apprentissage encapsule hello prédiction de modèle de hello dans une fonction et qu’il décore avec des attributs fournis par hello préinstallées Azure Machine Learning python bibliothèque qui indiquent votre ordinateur Azure ID d’espace de travail de formation, la clé d’API et hello d’entrée et retournent des paramètres.  

    from azureml import services
    @services.publish(workspaceid, auth_token)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(int) #0, or 1, or 2
    def predictIris(sep_l, sep_w, pet_l, pet_w):
     inputArray = [sep_l, sep_w, pet_l, pet_w]
    return clf.predict(inputArray)

Un client peut maintenant faire des appels toohello web service. Il n’y a plus de commodité les wrappers qui génèrent des requêtes d’API REST hello. Voici un exemple code tooconsume hello de service web.

    # Consume through web service URL and keys
    from azureml import services
    @services.service(url, api_key)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(float)
    def IrisPredictor(sep_l, sep_w, pet_l, pet_w):
    pass

    IrisPredictor(3,2,3,4)


> [!NOTE]
> bibliothèque d’Azure Machine Learning Hello est uniquement pris en charge Python 2.7 actuellement.   
> 
> 

### <a name="build-and-operationalize-r-models"></a>Générer et rendre opérationnels des modèles R
Vous pouvez déployer des modèles R construits hello Machine virtuelle de science des données ou un autre emplacement sur Azure Machine Learning d’une manière toohow similaires, qu'il est fait pour Python. Son hello étapes :

* créer un tooprovide de fichier settings.json votre ID d’espace de travail et l’authentification des jetons comme indiqué dans hello suivant l’exemple de code.
* écrire un wrapper pour le modèle hello predict (fonction).
* Appelez ```publishWebService``` Bonjour toopass de bibliothèque Azure Machine Learning dans un wrapper de fonction hello.  

Voici les extraits de code et de la procédure hello qui peuvent être utilisé tooset up, générer, publier et consommer un modèle comme un service web dans Azure Machine Learning.

#### <a name="setup"></a>Paramétrage
1. Installez le package de Machine Learning R hello en tapant ```install.packages("AzureML")``` dans l’IDE de Revolution R Enterprise 8.0 ou votre IDE R.
2. Téléchargez RTools [ici](https://cran.r-project.org/bin/windows/Rtools/). Vous devez hello zip dans le chemin d’accès hello (et nommée zip.exe) toooperationalize de votre package de R dans l’apprentissage.
3. Créer un fichier settings.json sous un répertoire appelé ```.azureml``` sous votre répertoire de base et entrez les paramètres de hello à partir de votre espace de travail Azure Machine Learning :

Structure du fichier settings.json :

    {"workspace":{
    "id"                  : "ENTER YOUR AZUREML WORKSPACE ID",
    "authorization_token" : "ENTER YOUR AZUREML AUTH TOKEN"
    }}


#### <a name="build-a-model-in-r-and-publish-it-in-azure-machine-learning"></a>Générer un modèle dans R et le publier dans Azure Machine Learning
    library(AzureML)
    ws <- workspace(config="~/.azureml/settings.json")

    if(!require("lme4")) install.packages("lme4")
    library(lme4)
    set.seed(1)
    train <- sleepstudy[sample(nrow(sleepstudy), 120),]
    m <- lm(Reaction ~ Days + Subject, data = train)

    # Define a prediction function toopublish based on hello model:
    sleepyPredict <- function(newdata){
          predict(m, newdata=newdata)
    }

    ep <- publishWebService(ws, fun = sleepyPredict, name="sleepy lm", inputSchema = sleepstudy, data.frame=TRUE)

#### <a name="consume-hello-model-deployed-in-azure-machine-learning"></a>Consommer modèle hello déployé dans Azure Machine Learning
modèle de hello tooconsume à partir d’une application cliente, nous utilisons hello Azure Machine Learning bibliothèque toolook des hello service web publié par un nom à l’aide de hello `services` point de terminaison API appel toodetermine hello. Puis vous appelez simplement hello `consume` de fonction et passez hello données frame toobe prédit.
Hello suivant le code est modèle de hello de tooconsume utilisé publié sous la forme d’un service web Azure Machine Learning.

    library(AzureML)
    library(lme4)
    ws <- workspace(config="~/.azureml/settings.json")

    s <-  services(ws, name = "sleepy lm")
    s <- tail(s, 1) # use hello last published function, in case of duplicate function names

    ep <- endpoints(ws, s)

    # OK, try this out, and compare with raw data
    ans = consume(ep, sleepstudy)$ans

Plus d’informations sur la bibliothèque d’Azure Machine Learning R hello trouverez [ici](https://cran.r-project.org/web/packages/AzureML/AzureML.pdf).

## <a name="4-administer-your-azure-resources-using-azure-portal-or-powershell"></a>4. Administrer vos ressources Azure à l’aide du Portail Azure ou de PowerShell
Hello DSVM vous permet non seulement toobuild votre solution analytique localement sur hello d’ordinateur virtuel, mais vous permet également de tooaccess les services sur le cloud Azure de Microsoft. Azure fournit plusieurs services de calcul, de stockage, d'analyse de données et autres que vous pouvez administrer et auxquels vous pouvez accéder à partir de votre DSVM.

tooadminister vos ressources cloud et d’abonnement Azure, vous pouvez utiliser votre navigateur et le point de toothe [portail Azure](https://portal.azure.com). Vous pouvez également utiliser Azure Powershell tooadminister votre abonnement Azure et les ressources à l’aide d’un script.
Vous pouvez exécuter Azure Powershell à partir d’un raccourci sur le bureau de hello ou à partir de hello démarrer menu intitulé « Microsoft Azure Powershell ». Reportez-vous à la [documentation Microsoft Azure PowerShell](../powershell-azure-resource-manager.md) pour plus d’informations sur l’administration de votre abonnement Azure et de vos ressources à l’aide de scripts Windows PowerShell.

## <a name="5-extend-your-storage-space-with-a-shared-file-system"></a>5. Augmenter votre espace de stockage avec un système de fichiers partagés
Les chercheurs de données peuvent partager des jeux de données volumineux, de code ou d’autres ressources au sein de l’équipe de hello. Hello DSVM lui-même a environ 70 Go d’espace disponible. tooextend votre stockage, vous pouvez utiliser hello Azure File Service et montez-le sur hello DSVM ou y accéder via une API REST.   

> [!NOTE]
> espace maximal de Hello du partage de Service de fichiers Azure hello est de 5 To et limite de taille de fichier est de 1 To.   
> 
> 

Vous pouvez utiliser Azure Powershell toocreate un partage Azure File Service. Voici toorun de script hello sous Azure PowerShell toocreate un partage de service de fichiers Azure.

    # Authenticate tooAzure.
    Login-AzureRmAccount
    # Select your subscription
    Get-AzureRmSubscription –SubscriptionName "<your subscription name>" | Select-AzureRmSubscription
    # Create a new resource group.
    New-AzureRmResourceGroup -Name <dsvmdatarg>
    # Create a new storage account. You can reuse existing storage account if you wish.
    New-AzureRmStorageAccount -Name <mydatadisk> -ResourceGroupName <dsvmdatarg> -Location "<Azure Data Center Name For eg. South Central US>" -Type "Standard_LRS"
    # Set your current working storage account
    Set-AzureRmCurrentStorageAccount –ResourceGroupName "<dsvmdatarg>" –StorageAccountName <mydatadisk>

    # Create a Azure File Service Share
    $s = New-AzureStorageShare <<teamsharename>>
    # Create a directory under hello FIle share. You can give it any name
    New-AzureStorageDirectory -Share $s -Path <directory name>
    # List hello share tooconfirm that everything worked
    Get-AzureStorageFile -Share $s


Maintenant que vous avez créé un partage de fichiers Azure, vous pouvez l’installer sur n’importe quelle machine virtuelle d’Azure. Il est fortement recommandé que hello machine virtuelle est dans le même centre de données Azure en tant que la latence de tooavoid de compte de stockage hello et les données des frais de transfert. Voici le lecteur de hello hello commandes toomount sur hello DSVM que vous pouvez exécuter sur Azure Powershell.

    # Get storage key of hello storage account that has hello Azure file share from Azure portal. Store it securely on hello VM tooavoid prompted in next command.
    cmdkey /add:<<mydatadisk>>.file.core.windows.net /user:<<mydatadisk>> /pass:<storage key>

    # Mount hello Azure file share as Z: drive on hello VM. You can chose another drive letter if you wish
    net use z:  \\<mydatadisk>.file.core.windows.net\<<teamsharename>>


Maintenant vous pouvez accéder à ce lecteur comme vous le feriez pour n’importe quel lecteur normale sur hello machine virtuelle.

## <a name="6-share-code-with-your-team-using-github"></a>6. Partager du code avec votre équipe à l’aide de GitHub
GitHub est un référentiel de code où vous trouverez un grand nombre d’exemples de code et des sources pour les différents outils à l’aide de différentes technologies partagées par la Communauté de développeurs hello. Elle utilise Git hello technologie tootrack magasin de versions et des fichiers de code hello. GitHub est également une plateforme où vous pouvez créer votre propre toostore référentiel de code partagé et la documentation de votre équipe implémenter le contrôle de version et également contrôle qui ont accès tooview et de contribuer du code. Visitez hello [des pages d’aide GitHub](https://help.github.com/) pour plus d’informations sur l’utilisation de Git. Vous pouvez utiliser GitHub comme hello façons toocollaborate avec votre équipe, utilisez du code développé par la Communauté de hello et contribuer du code précédent toohello Communauté.

Hello DSVM déjà est livré avec des outils clients sur les deux de la ligne de commande en tant que bien GUI tooaccess référentiel GitHub. toowork d’outil de ligne de commande Hello avec Git et GitHub est appelé l’interpréteur de commandes Git. Visual Studio installée sur hello DSVM possède des extensions de Git hello. Vous pouvez trouver des icônes de démarrage de ces outils sur le menu Démarrer de hello et le bureau de hello.

code de toodownload à partir d’un référentiel GitHub, vous utilisez hello ```git clone``` commande. Par exemple référentiel de science des données toodownload publié par Microsoft dans le répertoire en cours de hello vous pouvez exécuter hello commande suivante une fois que vous êtes dans ```git-bash```.

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

Dans Visual Studio, vous pouvez effectuer hello même opération de clonage. Hello suivant capture d’écran montre comment tooaccess Git et GitHub outils dans Visual Studio.

![Git dans Visual Studio](./media/machine-learning-data-science-vm-do-ten-things/VSGit.PNG)

Vous trouverez plus d’informations sur l’utilisation de Git toowork avec votre référentiel GitHub à partir de plusieurs ressources disponibles sur github.com. Hello [aide-mémoire](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf) est une référence utile.

## <a name="7-access-various-azure-data-and-analytics-services"></a>7. Accéder à divers services de données et d'analyse Azure
### <a name="azure-blob"></a>Objets blob Azure
Les objets blob Azure constituent un stockage fiable et économique dans le cloud pour tous les types de données. Examinons comment vous pouvez déplacer les données tooAzure Blob et accéder aux données stockées dans un objet Blob Azure.

**Configuration requise**

* **Créez votre compte de stockage d’objets blob Azure sur le [Portail Azure](https://portal.azure.com).**

![Create_Azure_Blob](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* Confirmer cet outil de ligne de commande préinstallé AzCopy hello n’est trouvé dans ```C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy.exe```. Vous pouvez ajouter hello répertoire conteneur hello azcopy.exe tooyour chemin d’accès environnement tooavoid variable en tapant hello commande complète chemin lors de l’exécution de cet outil. Pour plus d’informations sur l’outil AzCopy reportez-vous trop[AzCopy documentation](../storage/common/storage-use-azcopy.md)
* Démarrez l’outil d’Explorateur de stockage Azure hello. Vous pouvez le télécharger sur le site [Microsoft Azure Storage Explorer](http://storageexplorer.com/). 

![AzureStorageExplorer_v4](./media/machine-learning-data-science-vm-do-ten-things/AzureStorageExplorer_v4.png)

**Déplacer les données à partir de la machine virtuelle tooAzure Blob : AzCopy**

données toomove entre vos fichiers locaux et le stockage d’objets blob, vous pouvez utiliser AzCopy dans la ligne de commande ou de PowerShell :

    AzCopy /Source:C:\myfolder /Dest:https://<mystorageaccount>.blob.core.windows.net/<mycontainer> /DestKey:<storage account key> /Pattern:abc.txt

Remplacez **C:\myfolder** où se trouve votre fichier, du chemin d’accès de toohello **mystorageaccount** nom de compte de stockage des objets blob tooyour, **mycontainer** toohello nom du conteneur, **clé de compte de stockage** clé d’accès tooyour blob. Vous trouverez les informations d’identification de votre compte de stockage sur le [Portail Azure](https://portal.azure.com).

![StorageAccountCredential_v2](./media/machine-learning-data-science-vm-do-ten-things/StorageAccountCredential_v2.png)

Exécutez la commande AzCopy dans PowerShell ou à partir d’une invite de commandes. Voici un exemple d'utilisation de la commande AzCopy :

    # Copy *.sql from local machine tooa Azure Blob
    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:"c:\Aaqs\Data Science Scripts" /Dest:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /DestKey:[ENTER STORAGE KEY] /S /Pattern:*.sql

    # Copy back all files from Azure Blob container tooLocal machine

    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Dest:"c:\Aaqs\Data Science Scripts\temp" /Source:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /SourceKey:[ENTER STORAGE KEY] /S



Une fois que vous exécutez votre tooan de toocopy commande AzCopy objets blob Azure, vous voyez votre fichier s’affiche dans l’Explorateur de stockage Azure dans quelques instants.

![AzCopy_run_finshed_Storage_Explorer_v3](./media/machine-learning-data-science-vm-do-ten-things/AzCopy_run_finshed_Storage_Explorer_v3.png)

**Déplacer les données à partir de la machine virtuelle tooAzure Blob : Explorateur de stockage Azure**

Vous pouvez également télécharger des données à partir de fichiers local de hello dans votre machine virtuelle à l’aide de l’Explorateur de stockage Azure :

* conteneur de données de tooa tooupload, hello de conteneur et cliquez sur la cible du hello sélectionnez **télécharger** bouton.![ Télécharger dans l’Explorateur de stockage](./media/machine-learning-data-science-vm-do-ten-things/storage-accounts.png)
* Cliquez sur hello **...**  toohello à droite de hello **fichiers** , sélectionnez un ou plusieurs tooupload de fichiers à partir du système de fichiers hello puis cliquez sur **télécharger** toobegin de téléchargement de fichiers de hello.![ Télécharger les fichiers tooblob](./media/machine-learning-data-science-vm-do-ten-things/upload-files-to-blob.png)

**Lire des données à partir d'Azure Blob : module lecteur Machine Learning**

Dans Azure Machine Learning Studio, vous pouvez utiliser un **module d’importer des données** tooread des données à partir de votre objet blob.

![AML_ReaderBlob_Module_v3](./media/machine-learning-data-science-vm-do-ten-things/AML_ReaderBlob_Module_v3.png)

**Lire des données à partir d'Azure Blob : Python ODBC**

Vous pouvez utiliser **BlobService** données tooread de bibliothèque directement à partir de l’objet blob dans un programme bloc-notes Jupyter ou Python.

Commencez par importer les packages requis :

    import pandas as pd
    from pandas import Series, DataFrame
    import numpy as np
    import matplotlib.pyplot as plt
    from time import time
    import pyodbc
    import os
    from azure.storage.blob import BlobService
    import tables
    import time
    import zipfile
    import random

Puis entrez les informations d'identification de votre compte d'objets blob Azure et lisez les données de l'objet Blob :

    CONTAINERNAME = 'xxx'
    STORAGEACCOUNTNAME = 'xxxx'
    STORAGEACCOUNTKEY = 'xxxxxxxxxxxxxxxx'
    BLOBNAME = 'nyctaxidataset/nyctaxitrip/trip_data_1.csv'
    localfilename = 'trip_data_1.csv'
    LOCALDIRECTORY = os.getcwd()
    LOCALFILE =  os.path.join(LOCALDIRECTORY, localfilename)

    #download from blob
    t1 = time.time()
    blob_service = BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
    blob_service.get_blob_to_path(CONTAINERNAME,BLOBNAME,LOCALFILE)
    t2 = time.time()
    print(("It takes %s seconds toodownload "+BLOBNAME) % (t2 - t1))

    #unzipping downloaded files if needed
    #with zipfile.ZipFile(ZIPPEDLOCALFILE, "r") as z:
    #    z.extractall(LOCALDIRECTORY)

    df1 = pd.read_csv(LOCALFILE, header=0)
    df1.columns = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime','passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude']
    print 'hello size of hello data is: %d rows and  %d columns' % df1.shape

les données de salutation sont lu comme une trame de données :

![IPNB_data_readin](./media/machine-learning-data-science-vm-do-ten-things/IPNB_data_readin.PNG)

### <a name="azure-data-lake"></a>Azure Data Lake
Azure Data Lake Storage est un référentiel hyperscale pour les charges de travail d’analyse des Big Data, compatible avec le système de fichiers HDFS (Hadoop Distributed File System). Il fonctionne avec l’écosystème de Hadoop hello et hello Analytique de LAC de données Azure. Nous montrent comment vous pouvez déplacer des données dans Azure Data Lake Store de hello et exécuter l’analytique à l’aide d’Analytique de LAC de données Azure.

**Configuration requise**

* Créez votre Azure Data Lake Analytics dans le [Portail Azure](https://portal.azure.com).

![Azure_Data_Lake_Create_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_Create_v2.png)

* Hello **Azure Data Lake Tools** dans **Visual Studio** trouvé sur ce [lien](https://www.microsoft.com/download/details.aspx?id=49504) est déjà installé sur hello Visual Studio Community Edition qui se trouve sur l’ordinateur virtuel de hello. Après avoir démarré Visual Studio et de journalisation dans votre abonnement Azure, vous devez voir votre compte de l’Analytique des données Azure et de stockage dans le volet gauche de hello de Visual Studio.

![Azure_Data_Lake_PlugIn_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_PlugIn_v2.PNG)

**Déplacer les données à partir de la machine virtuelle tooData Lake : Explorateur de LAC de données Azure**

Vous pouvez utiliser **Explorateur lac de données Azure** données tooupload à partir de fichiers local de hello dans votre stockage de l’ordinateur virtuel tooData Lake.

![Azure_Data_Lake_UploadData](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_UploadData.PNG)

Vous pouvez également générer un tooproductionize de pipeline de données votre tooor de déplacement des données à partir d’Azure Data Lake à l’aide de hello [Factory(ADF) de données Azure](https://azure.microsoft.com/services/data-factory/). Nous vous appellerons toothis [article](https://azure.microsoft.com/blog/creating-big-data-pipelines-using-azure-data-lake-and-azure-data-factory/) tooguide vous guide dans les données de salutation hello étapes toobuild pipelines.

**Lire des données à partir d’Azure Blob tooData Lake : U-SQL**

Si vos données se trouvent dans Stockage Blob Azure, vous pouvez les lire directement à partir de l'objet blob de stockage Azure dans la requête SQL-U. Avant de composer votre requête U-SQL, assurez-vous que votre compte de stockage d’objets blob est lié tooyour Azure Data Lake. Accédez trop**portail Azure**, votre tableau de bord Analytique de LAC de données Azure, cliquez sur **ajouter une Source de données**, sélectionnez le type de stockage trop**Azure Storage** et de brancher votre stockage Azure Nom de compte et la clé. Vous êtes tooreference en mesure de hello présentes dans le compte de stockage hello.

![Saisie d'un compte de stockage et d'une clé](./media/machine-learning-data-science-vm-do-ten-things/Link_Blob_to_ADLA_v2.PNG)

Dans Visual Studio, vous pouvez lire les données de stockage d’objets blob, certaines manipulation de données, l’ingénierie de fonctionnalité et la sortie hello résultant données tooeither Azure Data Lake ou les stockage d’objets Blob Azure. Lorsque vous référencez des données hello dans le stockage blob, utilisez **wasb : / /**; lorsque vous faites référence dans Azure Data Lake, utilisez les données de salutation **swbhdfs : / /**

![Trame de données](./media/machine-learning-data-science-vm-do-ten-things/USQL_Read_Blob_v2.PNG)

Vous pouvez utiliser hello requêtes U-SQL dans Visual Studio suivantes :

    @a =
        EXTRACT medallion string,
                hack_license string,
                vendor_id string,
                rate_code string,
                store_and_fwd_flag string,
                pickup_datetime string,
                dropoff_datetime string,
                passenger_count int,
                trip_time_in_secs double,
                trip_distance double,
                pickup_longitude string,
                pickup_latitude string,
                dropoff_longitude string,
                dropoff_latitude string

        FROM "wasb://<Container name>@<Azure Blob Storage Account Name>.blob.core.windows.net/<Input Data File Name>"
        USING Extractors.Csv();

    @b =
        SELECT vendor_id,
        COUNT(medallion) AS cnt_medallion,
        SUM(passenger_count) AS cnt_passenger,
        AVG(trip_distance) AS avg_trip_dist,
        MIN(trip_distance) AS min_trip_dist,
        MAX(trip_distance) AS max_trip_dist,
        AVG(trip_time_in_secs) AS avg_trip_time
        FROM @a
        GROUP BY vendor_id;

    OUTPUT @b   
    too"swebhdfs://<Azure Data Lake Storage Account Name>.azuredatalakestore.net/<Folder Name>/<Output Data File Name>"
    USING Outputters.Csv();

    OUTPUT @b   
    too"wasb://<Container name>@<Azure Blob Storage Account Name>.blob.core.windows.net/<Output Data File Name>"
    USING Outputters.Csv();



Une fois votre requête soumise toohello server, un diagramme montrant l’état hello de votre travail s’affiche.

![Diagramme d’état du travail](./media/machine-learning-data-science-vm-do-ten-things/USQL_Job_Status.PNG)

**Interroger des données dans Data Lake : U-SQL**

Une fois le jeu de données hello est intégré dans Azure Data Lake, vous pouvez utiliser [langage U-SQL](../data-lake-analytics/data-lake-analytics-u-sql-get-started.md) tooquery et Explorer les données de hello. Langage U-SQL est similaire tooT-SQL, mais il combine certaines fonctionnalités de c# afin que les utilisateurs peuvent écrire, etc., les fonctions définies par l’utilisateur et les modules personnalisés. Vous pouvez utiliser des scripts de hello à l’étape précédente de hello.

Une fois la requête de hello tooserver soumis, tripdata_summary. Volume partagé de cluster se trouvent sous peu dans **Explorateur lac de données Azure**, peuvent afficher un aperçu des données hello par le fichier avec le bouton hello.

![Fichier dans Azure Data Lake Explorer](./media/machine-learning-data-science-vm-do-ten-things/USQL_create_summary.png)

informations sur les fichiers toosee hello :

![Résumé du fichier](./media/machine-learning-data-science-vm-do-ten-things/USQL_tripdata_summary.png)

### <a name="hdinsight-hadoop-clusters"></a>Clusters HDInsight Hadoop
HDInsight Azure est un service géré de Apache Hadoop, Spark, HBase et Storm sur le cloud de hello. Vous pouvez travailler facilement avec les clusters Azure HDInsight à partir de la machine virtuelle de hello données scientifiques.

**Configuration requise**

* Créez votre compte de stockage d’objets blob Azure sur le [Portail Azure](https://portal.azure.com). Ce compte de stockage est données toostore utilisés pour des clusters HDInsight.

![Créer un compte de stockage d’objets blob Azure](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* Personnalisez les clusters Hadoop Azure HDInsight sur le [Portail Azure](machine-learning-data-science-customize-hadoop-cluster.md)
  
  * Vous devez lier le compte de stockage hello créé avec votre cluster HDInsight lors de sa création. Ce compte de stockage est utilisé pour accéder aux données qui peuvent être traitées au sein du cluster de hello.

![Lier le compte toostorage créé avec le cluster HDInsight](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_v4.PNG)

* Vous devez activer **l’accès à distance** toohello le nœud principal du cluster hello après sa création. N’oubliez pas d’informations d’identification de l’accès à distance hello vous spécifiez ici (différents de ceux spécifiés pour le cluster hello lors de sa création) : vous avez besoin dans la suite de la procédure hello.

![Activer l'accès à distance](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_dashboard_v3.PNG)

* Créez un espace de travail Machine Learning. Vos expériences Machine Learning sont stockées dans cet espace de travail Machine Learning. Sélectionnez les options hello mis en surbrillance dans le portail, comme indiqué dans hello suivant capture d’écran :

![Création d’un espace de travail Microsoft Azure Machine Learning](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space.PNG)

* Puis entrez les paramètres hello pour votre espace de travail

![Entrer les paramètres de l'espace de travail Machine Learning](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space_step2_v2.PNG)

* Téléchargez des données à l’aide d’IPython Notebook. Tout d’abord importer les packages requis, incorporer des informations d’identification, créer une base de données dans votre compte de stockage, puis charge des clusters tooHDI de données.

        #Import required Packages
        import pyodbc
        import time as time
        import json
        import os
        import urllib
        import urllib2
        import warnings
        import re
        import pandas as pd
        import matplotlib.pyplot as plt
        from azure.storage.blob import BlobService
        warnings.filterwarnings("ignore", category=UserWarning, module='urllib2')


        #Create hello connection tooHive using ODBC
        SERVER_NAME='xxx.azurehdinsight.net'
        DATABASE_NAME='nyctaxidb'
        USERID='xxx'
        PASSWORD='xxxx'
        DB_DRIVER='Microsoft Hive ODBC Driver'
        driver = 'DRIVER={' + DB_DRIVER + '}'
        server = 'Host=' + SERVER_NAME + ';Port=443'
        database = 'Schema=' + DATABASE_NAME
        hiveserv = 'HiveServerType=2'
        auth = 'AuthMech=6'
        uid = 'UID=' + USERID
        pwd = 'PWD=' + PASSWORD
        CONNECTION_STRING = ';'.join([driver,server,database,hiveserv,auth,uid,pwd])
        connection = pyodbc.connect(CONNECTION_STRING, autocommit=True)
        cursor=connection.cursor()


        #Create Hive database and tables
        queryString = "create database if not exists nyctaxidb;"
        cursor.execute(queryString)

        queryString = """
                        create external table if not exists nyctaxidb.trip
                        (
                            medallion string,
                            hack_license string,
                            vendor_id string,
                            rate_code string,
                            store_and_fwd_flag string,
                            pickup_datetime string,
                            dropoff_datetime string,
                            passenger_count int,
                            trip_time_in_secs double,
                            trip_distance double,
                            pickup_longitude double,
                            pickup_latitude double,
                            dropoff_longitude double,
                            dropoff_latitude double)  
                        PARTITIONED BY (month int)
                        ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\\n'
                        STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/trip' TBLPROPERTIES('skip.header.line.count'='1');
                    """
        cursor.execute(queryString)

        queryString = """
                        create external table if not exists nyctaxidb.fare
                        (
                            medallion string,
                            hack_license string,
                            vendor_id string,
                            pickup_datetime string,
                            payment_type string,
                            fare_amount double,
                            surcharge double,
                            mta_tax double,
                            tip_amount double,
                            tolls_amount double,
                            total_amount double)
                        PARTITIONED BY (month int)
                        ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\\n'
                        STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/fare' TBLPROPERTIES('skip.header.line.count'='1');
                    """
        cursor.execute(queryString)


        #Upload data from blob storage tooHDI cluster
        for i in range(1,13):
            queryString = "LOAD DATA INPATH 'wasb:///nyctaxitripraw2/trip_data_%d.csv' INTO TABLE nyctaxidb2.trip PARTITION (month=%d);"%(i,i)
            cursor.execute(queryString)
            queryString = "LOAD DATA INPATH 'wasb:///nyctaxifareraw2/trip_fare_%d.csv' INTO TABLE nyctaxidb2.fare PARTITION (month=%d);"%(i,i)  
            cursor.execute(queryString)


* Ou bien, vous pouvez suivre cette [procédure pas à pas](machine-learning-data-science-process-hive-walkthrough.md) tooupload cluster de tooHDI NYC Taxi données. Voici les grandes étapes :
  
  * AzCopy : téléchargement compressé CSV à partir du dossier local blob publics tooyour
  * AzCopy : télécharger décompressé CSV à partir du cluster de tooHDI dossier local
  * Connectez-vous à un nœud de tête hello de cluster Hadoop et préparer pour l’analyse exploratoire des données

Une fois les données de salutation tooHDI chargé cluster, vous pouvez vérifier vos données dans l’Explorateur de stockage Azure. Et vous disposez d'une base de données nyctaxidb créée dans le cluster HDI.

**Exploration des données : requêtes Hive dans Python**

Les données hello étant dans le cluster Hadoop, vous pouvez utiliser hello pyodbc package tooconnect tooHadoop Clusters et des requêtes de base de données à l’aide de la ruche toodo exploration et l’ingénierie de fonctionnalité. Vous pouvez afficher les tables existantes hello que nous avons créé à l’étape de configuration requise hello.

    queryString = """
        show tables in nyctaxidb2;
        """
    pd.read_sql(queryString,connection)


![Afficher les tables existantes](./media/machine-learning-data-science-vm-do-ten-things/Python_View_Existing_Tables_Hive_v3.PNG)

Examinons le nombre de hello d’enregistrements dans chaque mois et hello les fréquences de pourboires ou non dans la table de voyage hello :

    queryString = """
        select month, count(*) from nyctaxidb.trip group by month;
        """
    results = pd.read_sql(queryString,connection)

    %matplotlib inline

    results.columns = ['month', 'trip_count']
    df = results.copy()
    df.index = df['month']
    df['trip_count'].plot(kind='bar')


![Tracer le nombre d’enregistrements de chaque mois](./media/machine-learning-data-science-vm-do-ten-things/Exploration_Number_Records_by_Month_v3.PNG)

    queryString = """
        SELECT tipped, COUNT(*) AS tip_freq
        FROM
        (
            SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
            FROM nyctaxidb.fare
        )tc
        GROUP BY tipped;
        """
    results = pd.read_sql(queryString,connection)

    results.columns = ['tipped', 'trip_count']
    df = results.copy()
    df.index = df['tipped']
    df['trip_count'].plot(kind='bar')


![Traçage des fréquences de pourboires](./media/machine-learning-data-science-vm-do-ten-things/Exploration_Frequency_tip_or_not_v3.PNG)

Nous pouvons également calculer la distance entre l’emplacement de collecte et l’emplacement de cette chute hello, puis les comparer toohello distance de déclenchement.

    queryString = """
                    select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude, trip_distance, trip_time_in_secs,
                        3959*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
                        *radians(180)/180/2),2)-cos(pickup_latitude*radians(180)/180)
                        *cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2)))
                        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*radians(180)/180/2),2)
                        +cos(pickup_latitude*radians(180)/180)*cos(dropoff_latitude*radians(180)/180)*
                        pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2))) as direct_distance
                        from nyctaxidb.trip
                        where month=1
                            and pickup_longitude between -90 and -30
                            and pickup_latitude between 30 and 90
                            and dropoff_longitude between -90 and -30
                            and dropoff_latitude between 30 and 90;
                """
    results = pd.read_sql(queryString,connection)
    results.head(5)


![Table des départs et arrivées](./media/machine-learning-data-science-vm-do-ten-things/Exploration_compute_pickup_dropoff_distance_v2.PNG)

    results.columns = ['pickup_longitude', 'pickup_latitude', 'dropoff_longitude',
                       'dropoff_latitude', 'trip_distance', 'trip_time_in_secs', 'direct_distance']
    df = results.loc[results['trip_distance']<=100] #remove outliers
    df = df.loc[df['direct_distance']<=100] #remove outliers
    plt.scatter(df['direct_distance'], df['trip_distance'])


![Traçage de la distance collecte/cette chute distance tootrip](./media/machine-learning-data-science-vm-do-ten-things/Exploration_direct_distance_trip_distance_v2.PNG)

Nous allons maintenant préparer le jeu de données sous-échantillonné (1 %) pour la modélisation. Nous pouvons utiliser ces données dans le module lecteur Machine Learning.

        queryString = """
        create  table if not exists nyctaxi_downsampled_dataset_testNEW (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        pickup_hour string,
        pickup_week string,
        weekday string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double,
        direct_distance double,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double,
        tipped string,
        tip_class string
        )
        row format delimited fields terminated by ','
        lines terminated by '\\n'
        stored as textfile;
        """
        cursor.execute(queryString)

        --- now insert contents of hello join into hello preceding internal table

        queryString = """
        insert overwrite table nyctaxi_downsampled_dataset_testNEW
        select
        t.medallion,
        t.hack_license,
        t.vendor_id,
        t.rate_code,
        t.store_and_fwd_flag,
        t.pickup_datetime,
        t.dropoff_datetime,
        hour(t.pickup_datetime) as pickup_hour,
        weekofyear(t.pickup_datetime) as pickup_week,
        from_unixtime(unix_timestamp(t.pickup_datetime, 'yyyy-MM-dd HH:mm:ss'),'u') as weekday,
        t.passenger_count,
        t.trip_time_in_secs,
        t.trip_distance,
        t.pickup_longitude,
        t.pickup_latitude,
        t.dropoff_longitude,
        t.dropoff_latitude,
        t.direct_distance,
        f.payment_type,
        f.fare_amount,
        f.surcharge,
        f.mta_tax,
        f.tip_amount,
        f.tolls_amount,
        f.total_amount,
        if(tip_amount>0,1,0) as tipped,
        if(tip_amount=0,0,
        if(tip_amount>0 and tip_amount<=5,1,
        if(tip_amount>5 and tip_amount<=10,2,
        if(tip_amount>10 and tip_amount<=20,3,4)))) as tip_class
        from
        (
        select
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        pickup_datetime,
        dropoff_datetime,
        passenger_count,
        trip_time_in_secs,
        trip_distance,
        pickup_longitude,
        pickup_latitude,
        dropoff_longitude,
        dropoff_latitude,
        3959*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
        radians(180)/180/2),2)-cos(pickup_latitude*radians(180)/180)
        *cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2)))
        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*radians(180)/180/2),2)
        +cos(pickup_latitude*radians(180)/180)*cos(dropoff_latitude*radians(180)/180)*pow(sin((dropoff_longitude-pickup_longitude)*radians(180)/180/2),2))) as direct_distance,
        rand() as sample_key

        from trip
        where pickup_latitude between 30 and 90
            and pickup_longitude between -90 and -30
            and dropoff_latitude between 30 and 90
            and dropoff_longitude between -90 and -30
        )t
        join
        (
        select
        medallion,
        hack_license,
        vendor_id,
        pickup_datetime,
        payment_type,
        fare_amount,
        surcharge,
        mta_tax,
        tip_amount,
        tolls_amount,
        total_amount
        from fare
        )f
        on t.medallion=f.medallion and t.hack_license=f.hack_license and t.pickup_datetime=f.pickup_datetime
        where t.sample_key<=0.01
        """
        cursor.execute(queryString)

Après un certain temps, vous pouvez voir les données de salutation a été chargées dans les clusters Hadoop :

    queryString = """
        select * from nyctaxi_downsampled_dataset limit 10;
        """
    cursor.execute(queryString)
    pd.read_sql(queryString,connection)


![Table de données](./media/machine-learning-data-science-vm-do-ten-things/DownSample_Data_For_Modeling_v2.PNG)

**Lire des données à partir de HDI en utilisant le module lecteur Machine Learning**

Vous pouvez également utiliser hello **lecteur** module Machine Learning Studio tooaccess hello base de données de cluster Hadoop. Informations d’identification hello vos clusters HDI plug-in et tooenable de compte de stockage Azure générer des modèles à l’aide de la base de données dans les clusters HDI d’apprentissage effectue une opération.

![Propriétés du module lecteur](./media/machine-learning-data-science-vm-do-ten-things/AML_Reader_Hive.PNG)

Hello jeu de données au score calculé peut alors être affiché :

![Affichage du jeu de données évalué](./media/machine-learning-data-science-vm-do-ten-things/AML_Model_Results.PNG)

### <a name="azure-sql-data-warehouse--databases"></a>Azure SQL Data Warehouse et bases de données
Azure SQL Data Warehouse est un entrepôt de données élastique en tant que service offrant une expérience SQL Server professionnelle.

Vous pouvez configurer votre entrepôt de données SQL Azure en suivant les instructions hello fournies dans cette [article](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md). Une fois que vous configurez votre entrepôt de données SQL Azure, vous pouvez utiliser cette [procédure pas à pas](machine-learning-data-science-process-sqldw-walkthrough.md) toodo données télécharger, exploration et modélisation à l’aide des données au sein de hello SQL Data Warehouse.

#### <a name="azure-cosmos-db"></a>Azure Cosmos DB
Base de données Cosmos Azure est une base de données NoSQL dans le cloud de hello. Il vous permet de toowork avec des documents comme JSON et vous permet des documents hello toostore et la requête.

Vous devez hello toodo suivant par requis étapes tooaccess base de données Azure Cosmos hello DSVM.

1. Installez le Kit de développement logiciel (SDK) Python DocumentDB (exécutez ```pip install pydocumentdb``` à partir de l’invite de commandes)
2. Créez un compte Azure Cosmos DB et une base de données à partir du [portail Azure](https://portal.azure.com)
3. Télécharger « Azure Cosmos DB Migration Tool » à partir de [ici](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d) et extraire le répertoire tooa de votre choix
4. Importer des données JSON (données îles) stockées sur un [objet blob public](https://cahandson.blob.core.windows.net/samples/volcano.json) dans base de données Cosmos avec suivant commande paramètres toohello outil de migration de (dtui.exe à partir du répertoire hello où vous avez installé hello Cosmos outil de Migration de base de données). Entrez les emplacements source et cible de hello avec ces paramètres :
   
    /s:JsonFile /s.Files:https://cahandson.blob.core.windows.net/samples/volcano.json /t:DocumentDBBulk /t.ConnectionString:AccountEndpoint=https://[DocDBAccountName].documents.azure.com:443/;AccountKey=[[KEY];Database=volcano /t.Collection:volcano1

Une fois que vous importez des données de hello, vous pouvez accéder tooJupyter et portable hello ouvrir intitulée *DocumentDBSample* qui contient les python tooaccess DocumentDB du code et effectuer des requêtes de base. Vous pouvez en savoir plus sur Cosmos DB en visitant le service de hello [page de documentation](https://docs.microsoft.com/azure/cosmos-db/).

## <a name="8-build-reports-and-dashboard-using-hello-power-bi-desktop"></a>8. Générer des rapports et tableau de bord à l’aide de hello Power BI Desktop
Nous permet de visualiser fichier îles JSON hello que nous avons vu dans hello précédant l’exemple de base de données Cosmos dans Power BI toogain visual connaître les données de salutation. Les étapes détaillées sont disponibles dans hello [article de Power BI](../cosmos-db/powerbi-visualize.md). Voici les étapes principales hello :

1. Ouvrez Power BI Desktop et cliquez sur « obtenir les données ». Spécifiez l’URL hello : https://cahandson.blob.core.windows.net/samples/volcano.json
2. Vous devez voir les enregistrements JSON hello importés sous forme de liste
3. Convertir la table de tooa de liste de hello pour Power BI peut manipuler hello même
4. Développez l’icône (hello une icône de « flèche gauche et flèche vers la droite » hello sur hello à droite de la colonne de hello) de développement de colonnes hello en cliquant sur hello
5. Notez que cet emplacement est un champ « Enregistrement ». Développez hello enregistrement et sélectionnez uniquement les coordonnées hello. Une coordonnée est une colonne de liste
6. Ajouter une nouvelle colonne tooconvert hello liste coordonnée de colonnes dans une colonne LatLong séparée virgules concaténation éléments hello deux dans le champ de liste de coordonnées hello à l’aide de la formule de hello ```Text.From([coordinates]{1})&","&Text.From([coordinates]{0})```.
7. Convertissez hello ```Elevation``` tooDecimal de colonne et sélectionnez hello **fermer** et **appliquer**.

Au lieu d’étapes précédentes, vous pouvez coller hello suivant code étapes hello utilisée dans les scripts hello éditeur avancé dans Power BI qui vous permet de transformations de données toowrite hello dans un langage de requête.

    let
        Source = Json.Document(Web.Contents("https://cahandson.blob.core.windows.net/samples/volcano.json")),
        #"Converted tooTable" = Table.FromList(Source, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
        #"Expanded Column1" = Table.ExpandRecordColumn(#"Converted tooTable", "Column1", {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}, {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}),
        #"Expanded Location" = Table.ExpandRecordColumn(#"Expanded Column1", "Location", {"coordinates"}, {"coordinates"}),
        #"Added Custom" = Table.AddColumn(#"Expanded Location", "LatLong", each Text.From([coordinates]{1})&","&Text.From([coordinates]{0})),
        #"Changed Type" = Table.TransformColumnTypes(#"Added Custom",{{"Elevation", type number}})
    in
        #"Changed Type"



Vous avez maintenant les données de salutation dans votre modèle de données Power BI. Votre Power BI Desktop doit apparaître comme suit :

![Power BI Desktop](./media/machine-learning-data-science-vm-do-ten-things/PowerBIVolcanoData.png)

Vous pouvez démarrer la création de rapports et des visualisations à l’aide du modèle de données hello. Vous pouvez suivre les étapes de hello dans ce [article de Power BI](../cosmos-db/powerbi-visualize.md#build-the-reports) toobuild un rapport. résultat final de Hello est un rapport qui ressemble à hello suivant.

![Power BI Desktop - Vue Rapport - Connecteur Power BI](./media/machine-learning-data-science-vm-do-ten-things/power_bi_connector_pbireportview2.png)

## <a name="9-dynamically-scale-your-dsvm-toomeet-your-project-needs"></a>9. Évoluer dynamiquement votre toomeet DSVM qu'a besoin de votre projet
Vous pouvez évoluez toomeet DSVM hello qu'a besoin de votre projet. Si vous n’avez pas besoin toouse hello machine virtuelle dans le soir hello ou les week-ends, vous pouvez simplement arrêté hello machine virtuelle à partir de hello [portail Azure](https://portal.azure.com).

> [!NOTE]
> Vous encourez des frais de calcul si vous utilisez simplement les bouton d’arrêt de système d’exploitation hello sur hello machine virtuelle.  
> 
> 

Si vous devez toohandle des analyses à grande échelle et que vous avez besoin de plus de capacité du processeur et/ou de mémoire et de disque, vous trouverez un grand choix de tailles de machine virtuelle en termes de cœurs du processeur, la capacité de mémoire et types de disques (y compris les disques SSD) qui répondent à vos besoins budgétaires et le calcul. Bonjour la liste complète des ordinateurs virtuels en même temps que leur tarification toutes les heures de calcul est disponible sur hello [tarification des Machines virtuelles Azure](https://azure.microsoft.com/pricing/details/virtual-machines/) page.

De même, si vos besoins en capacité de traitement de machine virtuelle réduit (par exemple : vous avez déplacé une tooa principales charges de travail Hadoop ou un cluster Spark), vous pouvez monter en puissance parallèle cluster hello de hello [portail Azure](https://portal.azure.com) et toohello les paramètres de votre machine virtuelle instance. Voici une capture d'écran.

![Paramètres de l'instance de machine virtuelle](./media/machine-learning-data-science-vm-do-ten-things/VMScaling.PNG)

## <a name="10-install-additional-tools-on-your-virtual-machine"></a>10. Installer des outils supplémentaires sur votre machine virtuelle
Nous avons empaqueté plusieurs outils que nous pensons tooaddress en mesure de la plupart des besoins de hello courants données analytique et qui doivent vous permettre de gagner du temps en évitant d’avoir tooinstall et configurer vos environnements un par un et économiser de l’argent en payant uniquement pour les ressources que vous avez à utiliser.

Vous pouvez tirer parti des autres données Azure et les services analytique profilé dans cet article de tooenhance votre environnement analytique. Nous comprenons que, dans certains cas, vos besoins puissent nécessiter des outils supplémentaires, notamment des outils tiers propriétaires. Vous avez un accès administrateur complet sur les nouveaux outils hello machine virtuelle tooinstall que vous avez besoin. Vous pouvez également installer des packages supplémentaires non préinstallés en Python et R. Pour Python, vous pouvez utiliser soit ```conda```, soit ```pip```. Pour R, vous pouvez utiliser hello ```install.packages()``` Bonjour R de la console ou utilisez hello IDE et choisissez «**Packages** -> **Packages d’installation...** ".

## <a name="summary"></a>Résumé
Voici quelques-uns des hello opérations pouvant être exécutées sur hello Machine virtuelle de science des données Microsoft. Il existe bien d’autres choses que vous pouvez effectuer toomake il un environnement efficace analytique.

