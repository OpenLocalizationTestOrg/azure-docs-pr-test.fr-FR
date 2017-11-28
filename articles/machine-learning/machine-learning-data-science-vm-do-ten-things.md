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
# <a name="ten-things-you-can-do-on-hello-data-science-virtual-machine"></a><span data-ttu-id="1ca8b-103">Dix choses que vous pouvez effectuer sur la science des données hello Machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="1ca8b-103">Ten things you can do on hello Data science Virtual Machine</span></span>
<span data-ttu-id="1ca8b-104">Hello Machine virtuelle de science des données Microsoft (DSVM) est un environnement de développement de science des données puissant qui permet de vous tooperform diverses tâches de modélisation et exploration de données.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-104">hello Microsoft Data Science Virtual Machine (DSVM) is a powerful data science development environment that enables you tooperform various data exploration and modeling tasks.</span></span> <span data-ttu-id="1ca8b-105">Hello environnement est déjà généré et fourni avec les données courantes plusieurs outils analytique qui la rendent facile tooget rapidement en main votre analyse locale, Cloud ou hybride déploiements.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-105">hello environment comes already built and bundled with several popular data analytics tools that make it easy tooget started quickly with your analysis for On-premises, Cloud or hybrid deployments.</span></span> <span data-ttu-id="1ca8b-106">Hello DSVM travaille en étroite collaboration avec de nombreux services Azure et est en mesure de tooread et traiter des données qui sont déjà stockées sur Azure, dans l’entrepôt de données SQL Azure, Azure Data Lake, le stockage Azure, ou dans la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-106">hello DSVM works closely with many Azure services and is able tooread and process data that is already stored on Azure, in Azure SQL Data Warehouse, Azure Data Lake, Azure Storage, or in Azure Cosmos DB.</span></span> <span data-ttu-id="1ca8b-107">Elle peut également exploiter d’autres outils d’analyse tels qu’Azure Machine Learning et Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-107">It can also leverage other analytics tools such as Azure Machine Learning and Azure Data Factory.</span></span>

<span data-ttu-id="1ca8b-108">Dans cet article nous vous guident la toouse votre tooperform DSVM des tâches différentes pour la science des données et interagir avec d’autres services Azure.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-108">In this article we walk you through how toouse your DSVM tooperform various data science tasks and interact with other Azure services.</span></span> <span data-ttu-id="1ca8b-109">Voici quelques-unes des hello opérations pouvant être exécutées sur hello DSVM :</span><span class="sxs-lookup"><span data-stu-id="1ca8b-109">Here are some of hello things you can do on hello DSVM:</span></span>

1. <span data-ttu-id="1ca8b-110">Explorer les données et de développer des modèles localement sur hello DSVM à l’aide de Microsoft R Server Python</span><span class="sxs-lookup"><span data-stu-id="1ca8b-110">Explore data and develop models locally on hello DSVM using Microsoft R Server, Python</span></span>
2. <span data-ttu-id="1ca8b-111">Utilisez un tooexperiment de bloc-notes Notebook avec vos données sur un navigateur à l’aide de Python, 2, 3 de Python, Microsoft R une version d’entreprise prêt de R conçu pour l’évolutivité et performances</span><span class="sxs-lookup"><span data-stu-id="1ca8b-111">Use a Jupyter notebook tooexperiment with your data on a browser using Python 2, Python 3, Microsoft R an enterprise ready version of R designed for scalability and performance</span></span>
3. <span data-ttu-id="1ca8b-112">Rendre opérationnels des modèles créés avec R et Python sur Azure Machine Learning afin que les applications clientes puissent accéder à vos modèles à l'aide d'une interface de services web simple</span><span class="sxs-lookup"><span data-stu-id="1ca8b-112">Operationalize models built using R and Python on Azure Machine Learning so client applications can access your models using a simple web services interface</span></span>
4. <span data-ttu-id="1ca8b-113">Administrer vos ressources Azure à l’aide du portail Azure ou de PowerShell</span><span class="sxs-lookup"><span data-stu-id="1ca8b-113">Administer your Azure resources using  Azure portal or Powershell</span></span>
5. <span data-ttu-id="1ca8b-114">Augmenter votre espace de stockage et partager des jeux de données / du code à grande échelle avec toute votre équipe en créant un stockage Fichier Azure comme lecteur montable sur votre DSVM</span><span class="sxs-lookup"><span data-stu-id="1ca8b-114">Extend your storage space and share large-scale datasets / code across your whole team by creating an Azure File storage as a mountable drive on your DSVM</span></span>
6. <span data-ttu-id="1ca8b-115">Partager du code avec votre équipe à l’aide de GitHub et accéder à votre référentiel à l’aide de hello préinstallées clients Git - interpréteur de commandes Git, Git l’interface graphique utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-115">Share code with your team using GitHub and access your repository using hello pre-installed Git clients - Git Bash, Git GUI.</span></span>
7. <span data-ttu-id="1ca8b-116">Accéder aux différents services de données et d’analytique Azure tels que Stockage Blob Azure, Azure Data Lake, Azure HDInsight (Hadoop), Azure Cosmos DB, Azure SQL Data Warehouse et Database</span><span class="sxs-lookup"><span data-stu-id="1ca8b-116">Access various Azure data and analytics services like Azure blob storage, Azure Data Lake, Azure HDInsight (Hadoop), Azure Cosmos DB, Azure SQL Data Warehouse & databases</span></span>
8. <span data-ttu-id="1ca8b-117">Générer des rapports et tableau de bord à l’aide de hello préinstallé sur hello DSVM Power BI Desktop et les déployer sur le cloud de hello</span><span class="sxs-lookup"><span data-stu-id="1ca8b-117">Build reports and dashboard using hello Power BI Desktop pre-installed on hello DSVM and deploy them on hello cloud</span></span>
9. <span data-ttu-id="1ca8b-118">Évoluer dynamiquement votre toomeet DSVM qu'a besoin de votre projet</span><span class="sxs-lookup"><span data-stu-id="1ca8b-118">Dynamically scale your DSVM toomeet your project needs</span></span>
10. <span data-ttu-id="1ca8b-119">Installer des outils supplémentaires sur votre machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="1ca8b-119">Install additional tools on your virtual machine</span></span>   

> [!NOTE]
> <span data-ttu-id="1ca8b-120">Frais d’utilisation supplémentaires s’appliquent pour de nombreux hello supplémentaires de stockage et analytique des services de données répertoriées dans cet article.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-120">Additional usage charges apply for many of hello additional data storage and analytics services listed in this article.</span></span> <span data-ttu-id="1ca8b-121">Reportez-vous toohello [tarification Azure](https://azure.microsoft.com/pricing/) page pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-121">Please refer toohello [Azure Pricing](https://azure.microsoft.com/pricing/) page for details.</span></span>
> 
> 

<span data-ttu-id="1ca8b-122">**Configuration requise**</span><span class="sxs-lookup"><span data-stu-id="1ca8b-122">**Prerequisites**</span></span>

* <span data-ttu-id="1ca8b-123">Vous avez besoin d’un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-123">You need an Azure subscription.</span></span> <span data-ttu-id="1ca8b-124">Vous pouvez vous inscrire à un essai gratuit [ici](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="1ca8b-124">You can sign up for a free trial [here](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="1ca8b-125">Les instructions pour la configuration d’un ordinateur de virtuel de science des données sur hello portail Azure sont disponibles au [création d’une machine virtuelle](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm).</span><span class="sxs-lookup"><span data-stu-id="1ca8b-125">Instructions for provisioning a Data Science Virtual Machine on hello Azure portal are available at [Creating a virtual machine](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm).</span></span>

## <a name="1-explore-data-and-develop-models-using-microsoft-r-server-or-python"></a><span data-ttu-id="1ca8b-126">1. Explorer les données et développer des modèles à l'aide de Microsoft R Server ou de Python</span><span class="sxs-lookup"><span data-stu-id="1ca8b-126">1. Explore data and develop models using Microsoft R Server or Python</span></span>
<span data-ttu-id="1ca8b-127">Vous pouvez utiliser des langages tels que R et Python toodo analytique de vos données à droite sur hello DSVM.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-127">You can use languages like R and Python toodo your data analytics right on hello DSVM.</span></span>

<span data-ttu-id="1ca8b-128">Pour R, vous pouvez utiliser un bus IDE appelé « Revolution R Enterprise 8.0 » qui se trouvent sur le menu Démarrer de hello ou bureau de hello.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-128">For R, you can use an IDE called "Revolution R Enterprise 8.0" that can be found on hello start menu or hello desktop.</span></span> <span data-ttu-id="1ca8b-129">Microsoft a fourni des bibliothèques supplémentaires par-dessus hello Open source/CRAN-R tooenable analytique et hello capacité tooanalyze données évolutive supérieure à la taille de la mémoire hello autorisé en effectuant une analyse mémorisé en bloc parallèle.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-129">Microsoft has provided additional libraries on top of hello Open source/CRAN-R tooenable scalable analytics and hello ability tooanalyze data larger than hello memory size allowed by doing parallel chunked analysis.</span></span> <span data-ttu-id="1ca8b-130">Vous pouvez également installer l’IDE R de votre choix, par exemple [RStudio](https://www.rstudio.com/products/rstudio-desktop/).</span><span class="sxs-lookup"><span data-stu-id="1ca8b-130">You can also install an R IDE of your choice like [RStudio](https://www.rstudio.com/products/rstudio-desktop/).</span></span>

<span data-ttu-id="1ca8b-131">Pour Python, vous pouvez utiliser un IDE comme Visual Studio Community Edition qui a hello outils Python pour l’extension de Visual Studio (PTVS) préinstallée.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-131">For Python, you can use an IDE like Visual Studio Community Edition which has hello Python Tools for Visual Studio (PTVS) extension pre-installed.</span></span> <span data-ttu-id="1ca8b-132">Par défaut, seule une version de base de Python 2.7 est configurée sur PTVS (sans aucune bibliothèque d’analyse comme SciKit, Pandas).</span><span class="sxs-lookup"><span data-stu-id="1ca8b-132">By default, only a basic Python 2.7 is configured on PTVS (without any analytics library like SciKit, Pandas).</span></span> <span data-ttu-id="1ca8b-133">Dans l’ordre tooenable Anaconda Python 2.7 et 3.5, vous toodo hello éléments suivants sont nécessaires :</span><span class="sxs-lookup"><span data-stu-id="1ca8b-133">In order tooenable Anaconda Python 2.7 and 3.5, you need toodo hello following:</span></span>

* <span data-ttu-id="1ca8b-134">Créer des environnements personnalisés pour chaque version en naviguant trop**outils** -> **outils Python** -> **environnements Python** , puis en cliquant sur » **+ Personnalisé**« dans hello Visual Studio 2015 Community Edition</span><span class="sxs-lookup"><span data-stu-id="1ca8b-134">Create custom environments for each version by navigating too**Tools** -> **Python Tools** -> **Python Environments** and then clicking "**+ Custom**" in hello Visual Studio 2015 Community Edition</span></span>
* <span data-ttu-id="1ca8b-135">Donner une description et définir l’environnement de hello préfixe les chemins d’accès en tant que *c:\anaconda* Anaconda Python 2.7 ou *c:\anaconda\envs\py35* Anaconda Python 3.5</span><span class="sxs-lookup"><span data-stu-id="1ca8b-135">Give a description and set hello environment prefix paths as *c:\anaconda* for Anaconda Python 2.7 OR *c:\anaconda\envs\py35* for Anaconda Python 3.5</span></span>
* <span data-ttu-id="1ca8b-136">Cliquez sur **la détection automatique** , puis **appliquer** environnement de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-136">Click **Auto Detect** and then **Apply** toosave hello environment.</span></span>

<span data-ttu-id="1ca8b-137">Voici la configuration de l’environnement personnalisée hello ressemble dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-137">Here is what hello custom environment setup looks like in Visual Studio.</span></span>

![Installation PTVS](./media/machine-learning-data-science-vm-do-ten-things/PTVSSetup.png)

<span data-ttu-id="1ca8b-139">Consultez hello [documentation de PTVS](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) pour plus d’informations sur la façon de toocreate environnements Python.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-139">See hello [PTVS documentation](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) for additional details on how toocreate Python Environments.</span></span>

<span data-ttu-id="1ca8b-140">Maintenant vous configurer toocreate un nouveau projet de Python.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-140">Now you are set up toocreate a new Python project.</span></span> <span data-ttu-id="1ca8b-141">Accédez trop**fichier** -> **nouveau** -> **projet** -> **Python** et sélectionnez le type hello de Vous générez l’application Python.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-141">Navigate too**File** -> **New** -> **Project** -> **Python** and select hello type of Python application you are building.</span></span> <span data-ttu-id="1ca8b-142">Vous pouvez définir l’environnement Python hello hello projet toohello souhaitée version actuelle (Anaconda 2.7 ou 3.5) : avec le bouton hello **environnement de Python**, sélectionnez **ajouter/supprimer des environnements Python**, et puis sélectionnez hello souhaité tooassociate environnement avec un projet de hello.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-142">You can set hello Python environment for hello current project toohello desired version (Anaconda 2.7 or 3.5): right-click hello **Python environment**, select **Add/Remove Python Environments**, and then select hello desired environment tooassociate with hello project.</span></span> <span data-ttu-id="1ca8b-143">Vous trouverez plus d’informations sur l’utilisation de PTVS sur les produits hello [documentation](https://github.com/Microsoft/PTVS/wiki) page.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-143">You can find more information about working with PTVS on hello product [documentation](https://github.com/Microsoft/PTVS/wiki) page.</span></span>

## <a name="2-using-a-jupyter-notebook-tooexplore-and-model-your-data-with-python-or-r"></a><span data-ttu-id="1ca8b-144">2. En utilisant un modèle et un bloc-notes Jupyter tooexplore vos données avec Python ou R</span><span class="sxs-lookup"><span data-stu-id="1ca8b-144">2. Using a Jupyter Notebook tooexplore and model your data with Python or R</span></span>
<span data-ttu-id="1ca8b-145">Hello bloc-notes Jupyter est un environnement puissant qui fournit une basée sur navigateur « IDE » pour la modélisation et exploration de données.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-145">hello Jupyter Notebook is a powerful environment that provides a browser-based "IDE" for data exploration and modeling.</span></span> <span data-ttu-id="1ca8b-146">Vous pouvez utiliser Python 2, 3 de Python ou R (Open Source et hello Microsoft R Server) dans un bloc-notes Jupyter.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-146">You can use Python 2, Python 3 or R (both Open Source and hello Microsoft R Server) in a Jupyter Notebook.</span></span>

<span data-ttu-id="1ca8b-147">toolaunch hello bloc-notes Jupyter sur l’icône de menu de démarrage hello / bureau icône intitulée **bloc-notes Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-147">toolaunch hello Jupyter Notebook click on hello start menu icon / desktop icon titled **Jupyter Notebook**.</span></span> <span data-ttu-id="1ca8b-148">Sur hello DSVM vous pouvez également parcourir trop « https://localhost:9999 / « tooaccess hello Jupiter bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-148">On hello DSVM you can also browse too"https://localhost:9999/" tooaccess hello Jupiter Notebook.</span></span> <span data-ttu-id="1ca8b-149">S’il vous demande un mot de passe, suivez les instructions fournies dans hello ***comment toocreate un mot de passe fort sur le serveur de jupyter Notebook hello*** section Hello [hello d’approvisionner la Machine virtuelle Microsoft données Science](machine-learning-data-science-provision-vm.md)rubrique toocreate un bloc-notes jupyter de mot de passe fort tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-149">If it prompts you for a password, use instructions provided in hello ***How toocreate a strong password on hello Jupyter notebook server*** section of hello [Provision hello Microsoft Data Science Virtual Machine](machine-learning-data-science-provision-vm.md) topic toocreate a strong password tooaccess hello Jupyter notebook.</span></span> 

<span data-ttu-id="1ca8b-150">Une fois que vous avez ouvert le bloc-notes de hello, vous devez voir un répertoire qui contient les quelques ordinateurs portables d’exemple qui sont intégrées dans hello DSVM.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-150">Once you have opened hello notebook, you should see a directory that contains a few example notebooks that are pre-packaged into hello DSVM.</span></span> <span data-ttu-id="1ca8b-151">Vous pouvez désormais :</span><span class="sxs-lookup"><span data-stu-id="1ca8b-151">Now you can:</span></span>

* <span data-ttu-id="1ca8b-152">Cliquez sur le code de hello toosee hello bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-152">click on hello notebook toosee hello code.</span></span>
* <span data-ttu-id="1ca8b-153">exécuter chaque cellule en appuyant sur **MAJ-ENTRÉE**;</span><span class="sxs-lookup"><span data-stu-id="1ca8b-153">execute each cell by pressing **SHIFT-ENTER**.</span></span>
* <span data-ttu-id="1ca8b-154">exécuter le bloc-notes hello en cliquant sur **cellule** -> **exécuter**</span><span class="sxs-lookup"><span data-stu-id="1ca8b-154">run hello entire notebook by clicking on **Cell** -> **Run**</span></span>
* <span data-ttu-id="1ca8b-155">créer un bloc-notes en cliquant sur hello Notebook icône (coin supérieur gauche) et en cliquant sur **nouveau** sur bouton hello droit, puis en choisissant le langage de bloc-notes hello (également appelé noyaux).</span><span class="sxs-lookup"><span data-stu-id="1ca8b-155">create a new notebook by clicking on hello Jupyter Icon (left top corner) and then clicking **New** button on hello right and then choosing hello notebook language (also known as kernels).</span></span>   

> [!NOTE]
> <span data-ttu-id="1ca8b-156">Nous prenons en charge les Python 2.7 actuellement, de noyau de hello R Python 3.5 et R. prend en charge la programmation dans R Open source ainsi que les entreprise hello évolutive Microsoft R Server.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-156">Currently we support Python 2.7, Python 3.5 and R. hello R kernel supports programming in both Open source R as well as hello enterprise scalable Microsoft R Server.</span></span>   
> 
> 

<span data-ttu-id="1ca8b-157">Une fois que vous êtes dans le bloc-notes de hello Explorer vos données, générer le modèle de hello, modèle hello à l’aide de votre choix des bibliothèques de test.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-157">Once you are in hello notebook you can explore your data, build hello model, test hello model using your choice of libraries.</span></span>

## <a name="3-build-models-using-r-or-python-and-operationalize-them-using-azure-machine-learning"></a><span data-ttu-id="1ca8b-158">3. Générer des modèles avec R ou Python et les rendre opérationnels à l’aide d’Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1ca8b-158">3. Build models using R or Python and Operationalize them using Azure Machine Learning</span></span>
<span data-ttu-id="1ca8b-159">Une fois que vous avez créé et validé votre modèle hello étape suivante consiste généralement toodeploy en production.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-159">Once you have built and validated your model hello next step is usually toodeploy it into production.</span></span> <span data-ttu-id="1ca8b-160">Ainsi, votre client de prédictions du modèle applications tooinvoke hello sur un en temps réel ou sur une base de mode de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-160">This allows your client applications tooinvoke hello model predictions on a real time or on a batch mode basis.</span></span> <span data-ttu-id="1ca8b-161">Azure Machine Learning fournit un mécanisme toooperationalize un modèle intégré dans R ou Python.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-161">Azure Machine Learning provides a mechanism toooperationalize a model built in either R or Python.</span></span>

<span data-ttu-id="1ca8b-162">Lorsque vous rendez opérationnel de votre modèle dans Azure Machine Learning, qui permet aux clients les appels REST toomake passer des paramètres d’entrée et de recevoir des prédictions à partir du modèle de hello en tant que sorties est exposé par un service web.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-162">When you operationalize your model in Azure Machine Learning, a web service is exposed that allows clients toomake REST calls that pass in input parameters and receive predictions from hello model as outputs.</span></span>   

> [!NOTE]
> <span data-ttu-id="1ca8b-163">Si vous n'êtes pas encore inscrit pour Azure Machine Learning, vous pouvez obtenir un espace de travail disponible ou un espace de travail standard en visitant hello [Azure Machine Learning Studio](https://studio.azureml.net/) page d’accueil et en cliquant sur « Démarrer ».</span><span class="sxs-lookup"><span data-stu-id="1ca8b-163">If you have not yet signed up for Azure Machine Learning, you can obtain a free workspace or a standard workspace by visiting hello [Azure Machine Learning Studio](https://studio.azureml.net/) home page and clicking on "Get Started".</span></span>   
> 
> 

### <a name="build-and-operationalize-python-models"></a><span data-ttu-id="1ca8b-164">Générer et rendre opérationnels des modèles Python</span><span class="sxs-lookup"><span data-stu-id="1ca8b-164">Build and Operationalize Python models</span></span>
<span data-ttu-id="1ca8b-165">Voici un extrait de code développé dans un bloc-notes Jupyter de Python qui génère un modèle simple à l’aide de la bibliothèque de hello SciKit-en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-165">Here is a snippet of code developed in a Python Jupyter Notebook that builds a simple model using hello SciKit-learn library.</span></span>

    #IRIS classification
    from sklearn import datasets
    from sklearn import svm
    clf = svm.SVC()
    iris = datasets.load_iris()
    X, y = iris.data, iris.target
    clf.fit(X, y)

<span data-ttu-id="1ca8b-166">méthode Hello utilisé toodeploy votre tooAzure de modèles python apprentissage encapsule hello prédiction de modèle de hello dans une fonction et qu’il décore avec des attributs fournis par hello préinstallées Azure Machine Learning python bibliothèque qui indiquent votre ordinateur Azure ID d’espace de travail de formation, la clé d’API et hello d’entrée et retournent des paramètres.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-166">hello method used toodeploy your python models tooAzure Machine Learning wraps hello prediction of hello model into a function and decorates it with attributes provided by hello pre-installed Azure Machine Learning python library that denote your Azure Machine Learning workspace ID, API Key, and hello input and return parameters.</span></span>  

    from azureml import services
    @services.publish(workspaceid, auth_token)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(int) #0, or 1, or 2
    def predictIris(sep_l, sep_w, pet_l, pet_w):
     inputArray = [sep_l, sep_w, pet_l, pet_w]
    return clf.predict(inputArray)

<span data-ttu-id="1ca8b-167">Un client peut maintenant faire des appels toohello web service.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-167">A client can now make calls toohello web service.</span></span> <span data-ttu-id="1ca8b-168">Il n’y a plus de commodité les wrappers qui génèrent des requêtes d’API REST hello.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-168">There are convenience wrappers that construct hello REST API requests.</span></span> <span data-ttu-id="1ca8b-169">Voici un exemple code tooconsume hello de service web.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-169">Here is a sample code tooconsume hello web service.</span></span>

    # Consume through web service URL and keys
    from azureml import services
    @services.service(url, api_key)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(float)
    def IrisPredictor(sep_l, sep_w, pet_l, pet_w):
    pass

    IrisPredictor(3,2,3,4)


> [!NOTE]
> <span data-ttu-id="1ca8b-170">bibliothèque d’Azure Machine Learning Hello est uniquement pris en charge Python 2.7 actuellement.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-170">hello Azure Machine Learning library is only supported on Python 2.7 currently.</span></span>   
> 
> 

### <a name="build-and-operationalize-r-models"></a><span data-ttu-id="1ca8b-171">Générer et rendre opérationnels des modèles R</span><span class="sxs-lookup"><span data-stu-id="1ca8b-171">Build and Operationalize R models</span></span>
<span data-ttu-id="1ca8b-172">Vous pouvez déployer des modèles R construits hello Machine virtuelle de science des données ou un autre emplacement sur Azure Machine Learning d’une manière toohow similaires, qu'il est fait pour Python.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-172">You can deploy R models built on hello Data Science Virtual Machine or elsewhere onto Azure Machine Learning in a manner that is similar toohow it is done for Python.</span></span> <span data-ttu-id="1ca8b-173">Son hello étapes :</span><span class="sxs-lookup"><span data-stu-id="1ca8b-173">Her are hello steps:</span></span>

* <span data-ttu-id="1ca8b-174">créer un tooprovide de fichier settings.json votre ID d’espace de travail et l’authentification des jetons comme indiqué dans hello suivant l’exemple de code.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-174">create a settings.json file tooprovide your workspace ID and auth token as shown in hello following code sample.</span></span>
* <span data-ttu-id="1ca8b-175">écrire un wrapper pour le modèle hello predict (fonction).</span><span class="sxs-lookup"><span data-stu-id="1ca8b-175">write a wrapper for hello model's predict function.</span></span>
* <span data-ttu-id="1ca8b-176">Appelez ```publishWebService``` Bonjour toopass de bibliothèque Azure Machine Learning dans un wrapper de fonction hello.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-176">call ```publishWebService``` in hello Azure Machine Learning library toopass in hello function wrapper.</span></span>  

<span data-ttu-id="1ca8b-177">Voici les extraits de code et de la procédure hello qui peuvent être utilisé tooset up, générer, publier et consommer un modèle comme un service web dans Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-177">Here is hello procedure and code snippets that can be used tooset up, build, publish, and consume a model as a web service in Azure Machine Learning.</span></span>

#### <a name="setup"></a><span data-ttu-id="1ca8b-178">Paramétrage</span><span class="sxs-lookup"><span data-stu-id="1ca8b-178">Setup</span></span>
1. <span data-ttu-id="1ca8b-179">Installez le package de Machine Learning R hello en tapant ```install.packages("AzureML")``` dans l’IDE de Revolution R Enterprise 8.0 ou votre IDE R.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-179">Install hello Machine Learning R package by typing ```install.packages("AzureML")``` in Revolution R Enterprise 8.0 IDE or your R IDE.</span></span>
2. <span data-ttu-id="1ca8b-180">Téléchargez RTools [ici](https://cran.r-project.org/bin/windows/Rtools/).</span><span class="sxs-lookup"><span data-stu-id="1ca8b-180">Download RTools from [here](https://cran.r-project.org/bin/windows/Rtools/).</span></span> <span data-ttu-id="1ca8b-181">Vous devez hello zip dans le chemin d’accès hello (et nommée zip.exe) toooperationalize de votre package de R dans l’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-181">You need hello zip utility in hello path (and named zip.exe) toooperationalize your R package into Machine Learning.</span></span>
3. <span data-ttu-id="1ca8b-182">Créer un fichier settings.json sous un répertoire appelé ```.azureml``` sous votre répertoire de base et entrez les paramètres de hello à partir de votre espace de travail Azure Machine Learning :</span><span class="sxs-lookup"><span data-stu-id="1ca8b-182">Create a settings.json file under a directory called ```.azureml``` under your home directory and enter hello parameters from your Azure Machine Learning workspace:</span></span>

<span data-ttu-id="1ca8b-183">Structure du fichier settings.json :</span><span class="sxs-lookup"><span data-stu-id="1ca8b-183">settings.json File structure:</span></span>

    {"workspace":{
    "id"                  : "ENTER YOUR AZUREML WORKSPACE ID",
    "authorization_token" : "ENTER YOUR AZUREML AUTH TOKEN"
    }}


#### <a name="build-a-model-in-r-and-publish-it-in-azure-machine-learning"></a><span data-ttu-id="1ca8b-184">Générer un modèle dans R et le publier dans Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1ca8b-184">Build a model in R and publish it in Azure Machine Learning</span></span>
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

#### <a name="consume-hello-model-deployed-in-azure-machine-learning"></a><span data-ttu-id="1ca8b-185">Consommer modèle hello déployé dans Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1ca8b-185">Consume hello model deployed in Azure Machine Learning</span></span>
<span data-ttu-id="1ca8b-186">modèle de hello tooconsume à partir d’une application cliente, nous utilisons hello Azure Machine Learning bibliothèque toolook des hello service web publié par un nom à l’aide de hello `services` point de terminaison API appel toodetermine hello.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-186">tooconsume hello model from a client application, we use hello Azure Machine Learning library toolook up hello published web service by name using hello `services` API call toodetermine hello endpoint.</span></span> <span data-ttu-id="1ca8b-187">Puis vous appelez simplement hello `consume` de fonction et passez hello données frame toobe prédit.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-187">Then you just call hello `consume` function and pass in hello data frame toobe predicted.</span></span>
<span data-ttu-id="1ca8b-188">Hello suivant le code est modèle de hello de tooconsume utilisé publié sous la forme d’un service web Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-188">hello following code is used tooconsume hello model published as an Azure Machine Learning web service.</span></span>

    library(AzureML)
    library(lme4)
    ws <- workspace(config="~/.azureml/settings.json")

    s <-  services(ws, name = "sleepy lm")
    s <- tail(s, 1) # use hello last published function, in case of duplicate function names

    ep <- endpoints(ws, s)

    # OK, try this out, and compare with raw data
    ans = consume(ep, sleepstudy)$ans

<span data-ttu-id="1ca8b-189">Plus d’informations sur la bibliothèque d’Azure Machine Learning R hello trouverez [ici](https://cran.r-project.org/web/packages/AzureML/AzureML.pdf).</span><span class="sxs-lookup"><span data-stu-id="1ca8b-189">More information about hello Azure Machine Learning R library can be found [here](https://cran.r-project.org/web/packages/AzureML/AzureML.pdf).</span></span>

## <a name="4-administer-your-azure-resources-using-azure-portal-or-powershell"></a><span data-ttu-id="1ca8b-190">4. Administrer vos ressources Azure à l’aide du Portail Azure ou de PowerShell</span><span class="sxs-lookup"><span data-stu-id="1ca8b-190">4. Administer your Azure resources using Azure portal or Powershell</span></span>
<span data-ttu-id="1ca8b-191">Hello DSVM vous permet non seulement toobuild votre solution analytique localement sur hello d’ordinateur virtuel, mais vous permet également de tooaccess les services sur le cloud Azure de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-191">hello DSVM not only allows you toobuild your analytics solution locally on hello virtual machine, but also allows you tooaccess services on Microsoft's Azure cloud.</span></span> <span data-ttu-id="1ca8b-192">Azure fournit plusieurs services de calcul, de stockage, d'analyse de données et autres que vous pouvez administrer et auxquels vous pouvez accéder à partir de votre DSVM.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-192">Azure provides several compute, storage, data analytics services and other services that you can administer and access from your DSVM.</span></span>

<span data-ttu-id="1ca8b-193">tooadminister vos ressources cloud et d’abonnement Azure, vous pouvez utiliser votre navigateur et le point de toothe [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1ca8b-193">tooadminister your Azure subscription and cloud resources you can use your browser and point toothe [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="1ca8b-194">Vous pouvez également utiliser Azure Powershell tooadminister votre abonnement Azure et les ressources à l’aide d’un script.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-194">You can also use Azure Powershell tooadminister your Azure subscription and resources via a script.</span></span>
<span data-ttu-id="1ca8b-195">Vous pouvez exécuter Azure Powershell à partir d’un raccourci sur le bureau de hello ou à partir de hello démarrer menu intitulé « Microsoft Azure Powershell ».</span><span class="sxs-lookup"><span data-stu-id="1ca8b-195">You can run Azure Powershell from a shortcut on hello desktop or from hello start menu titled "Microsoft Azure Powershell".</span></span> <span data-ttu-id="1ca8b-196">Reportez-vous à la [documentation Microsoft Azure PowerShell](../powershell-azure-resource-manager.md) pour plus d’informations sur l’administration de votre abonnement Azure et de vos ressources à l’aide de scripts Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-196">Refer to [Microsoft Azure Powershell documentation](../powershell-azure-resource-manager.md) for more information on how you can administer your Azure subscription and resources using Windows Powershell scripts.</span></span>

## <a name="5-extend-your-storage-space-with-a-shared-file-system"></a><span data-ttu-id="1ca8b-197">5. Augmenter votre espace de stockage avec un système de fichiers partagés</span><span class="sxs-lookup"><span data-stu-id="1ca8b-197">5. Extend your storage space with a shared file system</span></span>
<span data-ttu-id="1ca8b-198">Les chercheurs de données peuvent partager des jeux de données volumineux, de code ou d’autres ressources au sein de l’équipe de hello.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-198">Data scientists can share large datasets, code or other resources within hello team.</span></span> <span data-ttu-id="1ca8b-199">Hello DSVM lui-même a environ 70 Go d’espace disponible.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-199">hello DSVM itself has about 70GB of space available.</span></span> <span data-ttu-id="1ca8b-200">tooextend votre stockage, vous pouvez utiliser hello Azure File Service et montez-le sur hello DSVM ou y accéder via une API REST.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-200">tooextend your storage, you can use hello Azure File Service and either mount it on hello DSVM or access it via a REST API.</span></span>   

> [!NOTE]
> <span data-ttu-id="1ca8b-201">espace maximal de Hello du partage de Service de fichiers Azure hello est de 5 To et limite de taille de fichier est de 1 To.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-201">hello maximum space of hello Azure File Service share is 5TB and individual file size limit is 1TB.</span></span>   
> 
> 

<span data-ttu-id="1ca8b-202">Vous pouvez utiliser Azure Powershell toocreate un partage Azure File Service.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-202">You can use Azure Powershell toocreate an Azure File Service share.</span></span> <span data-ttu-id="1ca8b-203">Voici toorun de script hello sous Azure PowerShell toocreate un partage de service de fichiers Azure.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-203">Here is hello script toorun under Azure PowerShell toocreate an Azure File service share.</span></span>

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


<span data-ttu-id="1ca8b-204">Maintenant que vous avez créé un partage de fichiers Azure, vous pouvez l’installer sur n’importe quelle machine virtuelle d’Azure.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-204">Now that you have created an Azure file share, you can mount it in any virtual machine in Azure.</span></span> <span data-ttu-id="1ca8b-205">Il est fortement recommandé que hello machine virtuelle est dans le même centre de données Azure en tant que la latence de tooavoid de compte de stockage hello et les données des frais de transfert.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-205">It is highly recommended that hello VM is in same Azure data center as hello storage account tooavoid latency and data transfer charges.</span></span> <span data-ttu-id="1ca8b-206">Voici le lecteur de hello hello commandes toomount sur hello DSVM que vous pouvez exécuter sur Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-206">Here are hello commands toomount hello drive on hello DSVM that you can run on Azure Powershell.</span></span>

    # Get storage key of hello storage account that has hello Azure file share from Azure portal. Store it securely on hello VM tooavoid prompted in next command.
    cmdkey /add:<<mydatadisk>>.file.core.windows.net /user:<<mydatadisk>> /pass:<storage key>

    # Mount hello Azure file share as Z: drive on hello VM. You can chose another drive letter if you wish
    net use z:  \\<mydatadisk>.file.core.windows.net\<<teamsharename>>


<span data-ttu-id="1ca8b-207">Maintenant vous pouvez accéder à ce lecteur comme vous le feriez pour n’importe quel lecteur normale sur hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-207">Now you can access this drive as you would any normal drive on hello VM.</span></span>

## <a name="6-share-code-with-your-team-using-github"></a><span data-ttu-id="1ca8b-208">6. Partager du code avec votre équipe à l’aide de GitHub</span><span class="sxs-lookup"><span data-stu-id="1ca8b-208">6. Share code with your team using GitHub</span></span>
<span data-ttu-id="1ca8b-209">GitHub est un référentiel de code où vous trouverez un grand nombre d’exemples de code et des sources pour les différents outils à l’aide de différentes technologies partagées par la Communauté de développeurs hello.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-209">GitHub is a code repository where you can find a lot of sample code and sources for different tools using various technologies shared by hello developer community.</span></span> <span data-ttu-id="1ca8b-210">Elle utilise Git hello technologie tootrack magasin de versions et des fichiers de code hello.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-210">It uses Git as hello technology tootrack and store versions of hello code files.</span></span> <span data-ttu-id="1ca8b-211">GitHub est également une plateforme où vous pouvez créer votre propre toostore référentiel de code partagé et la documentation de votre équipe implémenter le contrôle de version et également contrôle qui ont accès tooview et de contribuer du code.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-211">GitHub is also a platform where you can create your own repository toostore your team's shared code and documentation, implement version control and also control who have access tooview and contribute code.</span></span> <span data-ttu-id="1ca8b-212">Visitez hello [des pages d’aide GitHub](https://help.github.com/) pour plus d’informations sur l’utilisation de Git.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-212">Please visit hello [GitHub help pages](https://help.github.com/) for more information on using Git.</span></span> <span data-ttu-id="1ca8b-213">Vous pouvez utiliser GitHub comme hello façons toocollaborate avec votre équipe, utilisez du code développé par la Communauté de hello et contribuer du code précédent toohello Communauté.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-213">You can use GitHub as one of hello ways toocollaborate with your team, use code developed by hello community and contribute code back toohello community.</span></span>

<span data-ttu-id="1ca8b-214">Hello DSVM déjà est livré avec des outils clients sur les deux de la ligne de commande en tant que bien GUI tooaccess référentiel GitHub.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-214">hello DSVM already comes loaded with client tools on both command-line as well GUI tooaccess GitHub repository.</span></span> <span data-ttu-id="1ca8b-215">toowork d’outil de ligne de commande Hello avec Git et GitHub est appelé l’interpréteur de commandes Git.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-215">hello command-line tool toowork with Git and GitHub is called Git Bash.</span></span> <span data-ttu-id="1ca8b-216">Visual Studio installée sur hello DSVM possède des extensions de Git hello.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-216">Visual Studio installed on hello DSVM has hello Git extensions.</span></span> <span data-ttu-id="1ca8b-217">Vous pouvez trouver des icônes de démarrage de ces outils sur le menu Démarrer de hello et le bureau de hello.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-217">You can find start-up icons for these tools on hello start menu and hello desktop.</span></span>

<span data-ttu-id="1ca8b-218">code de toodownload à partir d’un référentiel GitHub, vous utilisez hello ```git clone``` commande.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-218">toodownload code from a GitHub repository you use hello ```git clone``` command.</span></span> <span data-ttu-id="1ca8b-219">Par exemple référentiel de science des données toodownload publié par Microsoft dans le répertoire en cours de hello vous pouvez exécuter hello commande suivante une fois que vous êtes dans ```git-bash```.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-219">For example toodownload data science repository published by Microsoft into hello current directory you can run hello following command once you are in ```git-bash```.</span></span>

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

<span data-ttu-id="1ca8b-220">Dans Visual Studio, vous pouvez effectuer hello même opération de clonage.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-220">In Visual Studio, you can do hello same clone operation.</span></span> <span data-ttu-id="1ca8b-221">Hello suivant capture d’écran montre comment tooaccess Git et GitHub outils dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-221">hello  following screen-shot shows how tooaccess Git and GitHub tools in Visual Studio.</span></span>

![Git dans Visual Studio](./media/machine-learning-data-science-vm-do-ten-things/VSGit.PNG)

<span data-ttu-id="1ca8b-223">Vous trouverez plus d’informations sur l’utilisation de Git toowork avec votre référentiel GitHub à partir de plusieurs ressources disponibles sur github.com. Hello [aide-mémoire](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf) est une référence utile.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-223">You can find more information on using Git toowork with your GitHub repository from several resources available on github.com. hello [cheat sheet](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf) is a useful reference.</span></span>

## <a name="7-access-various-azure-data-and-analytics-services"></a><span data-ttu-id="1ca8b-224">7. Accéder à divers services de données et d'analyse Azure</span><span class="sxs-lookup"><span data-stu-id="1ca8b-224">7. Access various Azure data and analytics services</span></span>
### <a name="azure-blob"></a><span data-ttu-id="1ca8b-225">Objets blob Azure</span><span class="sxs-lookup"><span data-stu-id="1ca8b-225">Azure Blob</span></span>
<span data-ttu-id="1ca8b-226">Les objets blob Azure constituent un stockage fiable et économique dans le cloud pour tous les types de données.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-226">Azure blob is a reliable, economical cloud storage for data big and small.</span></span> <span data-ttu-id="1ca8b-227">Examinons comment vous pouvez déplacer les données tooAzure Blob et accéder aux données stockées dans un objet Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-227">Let us look at how you can move data tooAzure Blob and access data stored in an Azure Blob.</span></span>

<span data-ttu-id="1ca8b-228">**Configuration requise**</span><span class="sxs-lookup"><span data-stu-id="1ca8b-228">**Prerequisite**</span></span>

* <span data-ttu-id="1ca8b-229">**Créez votre compte de stockage d’objets blob Azure sur le [Portail Azure](https://portal.azure.com).**</span><span class="sxs-lookup"><span data-stu-id="1ca8b-229">**Create your Azure Blob storage account from [Azure portal](https://portal.azure.com).**</span></span>

![Create_Azure_Blob](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* <span data-ttu-id="1ca8b-231">Confirmer cet outil de ligne de commande préinstallé AzCopy hello n’est trouvé dans ```C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy.exe```.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-231">Confirm that hello pre-installed command-line AzCopy tool is found at ```C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy.exe```.</span></span> <span data-ttu-id="1ca8b-232">Vous pouvez ajouter hello répertoire conteneur hello azcopy.exe tooyour chemin d’accès environnement tooavoid variable en tapant hello commande complète chemin lors de l’exécution de cet outil.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-232">You can add hello directory containing hello azcopy.exe tooyour PATH environment variable tooavoid typing hello full command path when running this tool.</span></span> <span data-ttu-id="1ca8b-233">Pour plus d’informations sur l’outil AzCopy reportez-vous trop[AzCopy documentation](../storage/common/storage-use-azcopy.md)</span><span class="sxs-lookup"><span data-stu-id="1ca8b-233">For more info on AzCopy tool please refer too[AzCopy documentation](../storage/common/storage-use-azcopy.md)</span></span>
* <span data-ttu-id="1ca8b-234">Démarrez l’outil d’Explorateur de stockage Azure hello.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-234">Start hello Azure Storage Explorer tool.</span></span> <span data-ttu-id="1ca8b-235">Vous pouvez le télécharger sur le site [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="1ca8b-235">It can be downloaded from [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span> 

![AzureStorageExplorer_v4](./media/machine-learning-data-science-vm-do-ten-things/AzureStorageExplorer_v4.png)

<span data-ttu-id="1ca8b-237">**Déplacer les données à partir de la machine virtuelle tooAzure Blob : AzCopy**</span><span class="sxs-lookup"><span data-stu-id="1ca8b-237">**Move data from VM tooAzure Blob: AzCopy**</span></span>

<span data-ttu-id="1ca8b-238">données toomove entre vos fichiers locaux et le stockage d’objets blob, vous pouvez utiliser AzCopy dans la ligne de commande ou de PowerShell :</span><span class="sxs-lookup"><span data-stu-id="1ca8b-238">toomove data between your local files and blob storage, you can use AzCopy in command-line or PowerShell:</span></span>

    AzCopy /Source:C:\myfolder /Dest:https://<mystorageaccount>.blob.core.windows.net/<mycontainer> /DestKey:<storage account key> /Pattern:abc.txt

<span data-ttu-id="1ca8b-239">Remplacez **C:\myfolder** où se trouve votre fichier, du chemin d’accès de toohello **mystorageaccount** nom de compte de stockage des objets blob tooyour, **mycontainer** toohello nom du conteneur, **clé de compte de stockage** clé d’accès tooyour blob.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-239">Replace **C:\myfolder** toohello path where your file is stored, **mystorageaccount** tooyour blob storage account name, **mycontainer** toohello container name, **storage account key** tooyour blob storage access key.</span></span> <span data-ttu-id="1ca8b-240">Vous trouverez les informations d’identification de votre compte de stockage sur le [Portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1ca8b-240">You can find your storage account credentials in [Azure portal](https://portal.azure.com).</span></span>

![StorageAccountCredential_v2](./media/machine-learning-data-science-vm-do-ten-things/StorageAccountCredential_v2.png)

<span data-ttu-id="1ca8b-242">Exécutez la commande AzCopy dans PowerShell ou à partir d’une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-242">Run AzCopy command in PowerShell or from a command prompt.</span></span> <span data-ttu-id="1ca8b-243">Voici un exemple d'utilisation de la commande AzCopy :</span><span class="sxs-lookup"><span data-stu-id="1ca8b-243">Here is some example usage of AzCopy command:</span></span>

    # Copy *.sql from local machine tooa Azure Blob
    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:"c:\Aaqs\Data Science Scripts" /Dest:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /DestKey:[ENTER STORAGE KEY] /S /Pattern:*.sql

    # Copy back all files from Azure Blob container tooLocal machine

    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Dest:"c:\Aaqs\Data Science Scripts\temp" /Source:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /SourceKey:[ENTER STORAGE KEY] /S



<span data-ttu-id="1ca8b-244">Une fois que vous exécutez votre tooan de toocopy commande AzCopy objets blob Azure, vous voyez votre fichier s’affiche dans l’Explorateur de stockage Azure dans quelques instants.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-244">Once you run your AzCopy command toocopy tooan Azure blob you see your file shows up in Azure Storage Explorer shortly.</span></span>

![AzCopy_run_finshed_Storage_Explorer_v3](./media/machine-learning-data-science-vm-do-ten-things/AzCopy_run_finshed_Storage_Explorer_v3.png)

<span data-ttu-id="1ca8b-246">**Déplacer les données à partir de la machine virtuelle tooAzure Blob : Explorateur de stockage Azure**</span><span class="sxs-lookup"><span data-stu-id="1ca8b-246">**Move data from VM tooAzure Blob: Azure Storage Explorer**</span></span>

<span data-ttu-id="1ca8b-247">Vous pouvez également télécharger des données à partir de fichiers local de hello dans votre machine virtuelle à l’aide de l’Explorateur de stockage Azure :</span><span class="sxs-lookup"><span data-stu-id="1ca8b-247">You can also upload data from hello local file in your VM using Azure Storage Explorer:</span></span>

* <span data-ttu-id="1ca8b-248">conteneur de données de tooa tooupload, hello de conteneur et cliquez sur la cible du hello sélectionnez **télécharger** bouton.![ Télécharger dans l’Explorateur de stockage](./media/machine-learning-data-science-vm-do-ten-things/storage-accounts.png)</span><span class="sxs-lookup"><span data-stu-id="1ca8b-248">tooupload data tooa container, select hello target container and click hello **Upload** button.![Upload in Storage Explorer](./media/machine-learning-data-science-vm-do-ten-things/storage-accounts.png)</span></span>
* <span data-ttu-id="1ca8b-249">Cliquez sur hello **...**  toohello à droite de hello **fichiers** , sélectionnez un ou plusieurs tooupload de fichiers à partir du système de fichiers hello puis cliquez sur **télécharger** toobegin de téléchargement de fichiers de hello.![ Télécharger les fichiers tooblob](./media/machine-learning-data-science-vm-do-ten-things/upload-files-to-blob.png)</span><span class="sxs-lookup"><span data-stu-id="1ca8b-249">Click on hello **...** toohello right of hello **Files** box, select one or multiple files tooupload from hello file system and click **Upload** toobegin uploading hello files.![Upload files tooblob](./media/machine-learning-data-science-vm-do-ten-things/upload-files-to-blob.png)</span></span>

<span data-ttu-id="1ca8b-250">**Lire des données à partir d'Azure Blob : module lecteur Machine Learning**</span><span class="sxs-lookup"><span data-stu-id="1ca8b-250">**Read data from Azure Blob: Machine Learning reader module**</span></span>

<span data-ttu-id="1ca8b-251">Dans Azure Machine Learning Studio, vous pouvez utiliser un **module d’importer des données** tooread des données à partir de votre objet blob.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-251">In Azure Machine Learning Studio you can use an **Import Data module** tooread data from your blob.</span></span>

![AML_ReaderBlob_Module_v3](./media/machine-learning-data-science-vm-do-ten-things/AML_ReaderBlob_Module_v3.png)

<span data-ttu-id="1ca8b-253">**Lire des données à partir d'Azure Blob : Python ODBC**</span><span class="sxs-lookup"><span data-stu-id="1ca8b-253">**Read data from Azure Blob: Python ODBC**</span></span>

<span data-ttu-id="1ca8b-254">Vous pouvez utiliser **BlobService** données tooread de bibliothèque directement à partir de l’objet blob dans un programme bloc-notes Jupyter ou Python.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-254">You can use **BlobService** library tooread data directly from blob in a Jupyter Notebook or Python program.</span></span>

<span data-ttu-id="1ca8b-255">Commencez par importer les packages requis :</span><span class="sxs-lookup"><span data-stu-id="1ca8b-255">First, import required packages:</span></span>

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

<span data-ttu-id="1ca8b-256">Puis entrez les informations d'identification de votre compte d'objets blob Azure et lisez les données de l'objet Blob :</span><span class="sxs-lookup"><span data-stu-id="1ca8b-256">Then plug in your Azure Blob account credentials and read data from Blob:</span></span>

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

<span data-ttu-id="1ca8b-257">les données de salutation sont lu comme une trame de données :</span><span class="sxs-lookup"><span data-stu-id="1ca8b-257">hello data is read in as a data frame:</span></span>

![IPNB_data_readin](./media/machine-learning-data-science-vm-do-ten-things/IPNB_data_readin.PNG)

### <a name="azure-data-lake"></a><span data-ttu-id="1ca8b-259">Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="1ca8b-259">Azure Data Lake</span></span>
<span data-ttu-id="1ca8b-260">Azure Data Lake Storage est un référentiel hyperscale pour les charges de travail d’analyse des Big Data, compatible avec le système de fichiers HDFS (Hadoop Distributed File System).</span><span class="sxs-lookup"><span data-stu-id="1ca8b-260">Azure Data Lake Storage is a hyper-scale repository for big data analytics workloads and compatible with Hadoop Distributed File System (HDFS).</span></span> <span data-ttu-id="1ca8b-261">Il fonctionne avec l’écosystème de Hadoop hello et hello Analytique de LAC de données Azure.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-261">It works with both hello Hadoop ecosystem and hello Azure Data Lake Analytics.</span></span> <span data-ttu-id="1ca8b-262">Nous montrent comment vous pouvez déplacer des données dans Azure Data Lake Store de hello et exécuter l’analytique à l’aide d’Analytique de LAC de données Azure.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-262">We show how you can move data into hello Azure Data Lake Store and run analytics using Azure Data Lake Analytics.</span></span>

<span data-ttu-id="1ca8b-263">**Configuration requise**</span><span class="sxs-lookup"><span data-stu-id="1ca8b-263">**Prerequisite**</span></span>

* <span data-ttu-id="1ca8b-264">Créez votre Azure Data Lake Analytics dans le [Portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1ca8b-264">Create your Azure Data Lake Analytics in [Azure portal](https://portal.azure.com).</span></span>

![Azure_Data_Lake_Create_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_Create_v2.png)

* <span data-ttu-id="1ca8b-266">Hello **Azure Data Lake Tools** dans **Visual Studio** trouvé sur ce [lien](https://www.microsoft.com/download/details.aspx?id=49504) est déjà installé sur hello Visual Studio Community Edition qui se trouve sur l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-266">hello  **Azure Data Lake Tools** in **Visual Studio** found at this  [link](https://www.microsoft.com/download/details.aspx?id=49504) is already installed on hello Visual Studio Community Edition which is on hello virtual machine.</span></span> <span data-ttu-id="1ca8b-267">Après avoir démarré Visual Studio et de journalisation dans votre abonnement Azure, vous devez voir votre compte de l’Analytique des données Azure et de stockage dans le volet gauche de hello de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-267">After starting Visual Studio and logging in your Azure subscription, you should see your Azure Data Analytics account and storage in hello left panel of Visual Studio.</span></span>

![Azure_Data_Lake_PlugIn_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_PlugIn_v2.PNG)

<span data-ttu-id="1ca8b-269">**Déplacer les données à partir de la machine virtuelle tooData Lake : Explorateur de LAC de données Azure**</span><span class="sxs-lookup"><span data-stu-id="1ca8b-269">**Move data from VM tooData Lake: Azure Data Lake Explorer**</span></span>

<span data-ttu-id="1ca8b-270">Vous pouvez utiliser **Explorateur lac de données Azure** données tooupload à partir de fichiers local de hello dans votre stockage de l’ordinateur virtuel tooData Lake.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-270">You can use **Azure Data Lake Explorer** tooupload data from hello local files in your Virtual Machine tooData Lake storage.</span></span>

![Azure_Data_Lake_UploadData](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_UploadData.PNG)

<span data-ttu-id="1ca8b-272">Vous pouvez également générer un tooproductionize de pipeline de données votre tooor de déplacement des données à partir d’Azure Data Lake à l’aide de hello [Factory(ADF) de données Azure](https://azure.microsoft.com/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="1ca8b-272">You can also build a data pipeline tooproductionize your data movement tooor from Azure Data Lake using hello [Azure Data Factory(ADF)](https://azure.microsoft.com/services/data-factory/).</span></span> <span data-ttu-id="1ca8b-273">Nous vous appellerons toothis [article](https://azure.microsoft.com/blog/creating-big-data-pipelines-using-azure-data-lake-and-azure-data-factory/) tooguide vous guide dans les données de salutation hello étapes toobuild pipelines.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-273">We refer you toothis [article](https://azure.microsoft.com/blog/creating-big-data-pipelines-using-azure-data-lake-and-azure-data-factory/) tooguide you through hello steps toobuild hello data pipelines.</span></span>

<span data-ttu-id="1ca8b-274">**Lire des données à partir d’Azure Blob tooData Lake : U-SQL**</span><span class="sxs-lookup"><span data-stu-id="1ca8b-274">**Read data from Azure Blob tooData Lake: U-SQL**</span></span>

<span data-ttu-id="1ca8b-275">Si vos données se trouvent dans Stockage Blob Azure, vous pouvez les lire directement à partir de l'objet blob de stockage Azure dans la requête SQL-U.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-275">If your data resides in Azure Blob storage, you can directly read data from Azure storage blob in U-SQL query.</span></span> <span data-ttu-id="1ca8b-276">Avant de composer votre requête U-SQL, assurez-vous que votre compte de stockage d’objets blob est lié tooyour Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-276">Before composing your U-SQL query, make sure your blob storage account is linked tooyour Azure Data Lake.</span></span> <span data-ttu-id="1ca8b-277">Accédez trop**portail Azure**, votre tableau de bord Analytique de LAC de données Azure, cliquez sur **ajouter une Source de données**, sélectionnez le type de stockage trop**Azure Storage** et de brancher votre stockage Azure Nom de compte et la clé.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-277">Go too**Azure portal**, find your Azure Data Lake Analytics dashboard, click **Add Data Source**, select storage type too**Azure Storage** and plug in your Azure Storage Account Name and Key.</span></span> <span data-ttu-id="1ca8b-278">Vous êtes tooreference en mesure de hello présentes dans le compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-278">Then you are able tooreference hello data stored in hello storage account.</span></span>

![Saisie d'un compte de stockage et d'une clé](./media/machine-learning-data-science-vm-do-ten-things/Link_Blob_to_ADLA_v2.PNG)

<span data-ttu-id="1ca8b-280">Dans Visual Studio, vous pouvez lire les données de stockage d’objets blob, certaines manipulation de données, l’ingénierie de fonctionnalité et la sortie hello résultant données tooeither Azure Data Lake ou les stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-280">In Visual Studio, you can read data from blob storage, do some data manipulation, feature engineering, and output hello resulting data tooeither Azure Data Lake or Azure Blob Storage.</span></span> <span data-ttu-id="1ca8b-281">Lorsque vous référencez des données hello dans le stockage blob, utilisez **wasb : / /**; lorsque vous faites référence dans Azure Data Lake, utilisez les données de salutation **swbhdfs : / /**</span><span class="sxs-lookup"><span data-stu-id="1ca8b-281">When you reference hello data in blob storage, use **wasb://**; when you reference hello data in Azure Data Lake, use **swbhdfs://**</span></span>

![Trame de données](./media/machine-learning-data-science-vm-do-ten-things/USQL_Read_Blob_v2.PNG)

<span data-ttu-id="1ca8b-283">Vous pouvez utiliser hello requêtes U-SQL dans Visual Studio suivantes :</span><span class="sxs-lookup"><span data-stu-id="1ca8b-283">You may use hello following U-SQL queries in Visual Studio:</span></span>

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



<span data-ttu-id="1ca8b-284">Une fois votre requête soumise toohello server, un diagramme montrant l’état hello de votre travail s’affiche.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-284">After your query is submitted toohello server, a diagram showing hello status of your job is displayed.</span></span>

![Diagramme d’état du travail](./media/machine-learning-data-science-vm-do-ten-things/USQL_Job_Status.PNG)

<span data-ttu-id="1ca8b-286">**Interroger des données dans Data Lake : U-SQL**</span><span class="sxs-lookup"><span data-stu-id="1ca8b-286">**Query data in Data Lake: U-SQL**</span></span>

<span data-ttu-id="1ca8b-287">Une fois le jeu de données hello est intégré dans Azure Data Lake, vous pouvez utiliser [langage U-SQL](../data-lake-analytics/data-lake-analytics-u-sql-get-started.md) tooquery et Explorer les données de hello.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-287">After hello dataset is ingested into Azure Data Lake, you can use [U-SQL language](../data-lake-analytics/data-lake-analytics-u-sql-get-started.md) tooquery and explore hello data.</span></span> <span data-ttu-id="1ca8b-288">Langage U-SQL est similaire tooT-SQL, mais il combine certaines fonctionnalités de c# afin que les utilisateurs peuvent écrire, etc., les fonctions définies par l’utilisateur et les modules personnalisés. Vous pouvez utiliser des scripts de hello à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-288">U-SQL language is similar tooT-SQL, but combines some features from C# so that users can write customized modules, user-defined functions, and etc. You can use hello scripts in hello previous step.</span></span>

<span data-ttu-id="1ca8b-289">Une fois la requête de hello tooserver soumis, tripdata_summary. Volume partagé de cluster se trouvent sous peu dans **Explorateur lac de données Azure**, peuvent afficher un aperçu des données hello par le fichier avec le bouton hello.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-289">After hello query is submitted tooserver, tripdata_summary.CSV can be found shortly in **Azure Data Lake Explorer**, you may preview hello data by right-click hello file.</span></span>

![Fichier dans Azure Data Lake Explorer](./media/machine-learning-data-science-vm-do-ten-things/USQL_create_summary.png)

<span data-ttu-id="1ca8b-291">informations sur les fichiers toosee hello :</span><span class="sxs-lookup"><span data-stu-id="1ca8b-291">toosee hello file information:</span></span>

![Résumé du fichier](./media/machine-learning-data-science-vm-do-ten-things/USQL_tripdata_summary.png)

### <a name="hdinsight-hadoop-clusters"></a><span data-ttu-id="1ca8b-293">Clusters HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="1ca8b-293">HDInsight Hadoop Clusters</span></span>
<span data-ttu-id="1ca8b-294">HDInsight Azure est un service géré de Apache Hadoop, Spark, HBase et Storm sur le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-294">Azure HDInsight is a managed Apache Hadoop, Spark, HBase, and Storm service on hello cloud.</span></span> <span data-ttu-id="1ca8b-295">Vous pouvez travailler facilement avec les clusters Azure HDInsight à partir de la machine virtuelle de hello données scientifiques.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-295">You can work easily with Azure HDInsight clusters from hello data science virtual machine.</span></span>

<span data-ttu-id="1ca8b-296">**Configuration requise**</span><span class="sxs-lookup"><span data-stu-id="1ca8b-296">**Prerequisite**</span></span>

* <span data-ttu-id="1ca8b-297">Créez votre compte de stockage d’objets blob Azure sur le [Portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1ca8b-297">Create your Azure Blob storage account from [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="1ca8b-298">Ce compte de stockage est données toostore utilisés pour des clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-298">This storage account is used toostore data for HDInsight clusters.</span></span>

![Créer un compte de stockage d’objets blob Azure](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* <span data-ttu-id="1ca8b-300">Personnalisez les clusters Hadoop Azure HDInsight sur le [Portail Azure](machine-learning-data-science-customize-hadoop-cluster.md)</span><span class="sxs-lookup"><span data-stu-id="1ca8b-300">Customize Azure HDInsight Hadoop Clusters from [Azure portal](machine-learning-data-science-customize-hadoop-cluster.md)</span></span>
  
  * <span data-ttu-id="1ca8b-301">Vous devez lier le compte de stockage hello créé avec votre cluster HDInsight lors de sa création.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-301">You must link hello storage account created with your HDInsight cluster when it is created.</span></span> <span data-ttu-id="1ca8b-302">Ce compte de stockage est utilisé pour accéder aux données qui peuvent être traitées au sein du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-302">This storage account is used for accessing data that can be processed within hello cluster.</span></span>

![Lier le compte toostorage créé avec le cluster HDInsight](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_v4.PNG)

* <span data-ttu-id="1ca8b-304">Vous devez activer **l’accès à distance** toohello le nœud principal du cluster hello après sa création.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-304">You must enable **Remote Access** toohello head node of hello cluster after it is created.</span></span> <span data-ttu-id="1ca8b-305">N’oubliez pas d’informations d’identification de l’accès à distance hello vous spécifiez ici (différents de ceux spécifiés pour le cluster hello lors de sa création) : vous avez besoin dans la suite de la procédure hello.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-305">Remember hello remote access credentials you specify here (different from those specified for hello cluster at its creation): you need them in hello subsequent procedure.</span></span>

![Activer l'accès à distance](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_dashboard_v3.PNG)

* <span data-ttu-id="1ca8b-307">Créez un espace de travail Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-307">Create an Azure Machine Learning workspace.</span></span> <span data-ttu-id="1ca8b-308">Vos expériences Machine Learning sont stockées dans cet espace de travail Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-308">Your Machine Learning Experiments are stored in this Machine Learning workspace.</span></span> <span data-ttu-id="1ca8b-309">Sélectionnez les options hello mis en surbrillance dans le portail, comme indiqué dans hello suivant capture d’écran :</span><span class="sxs-lookup"><span data-stu-id="1ca8b-309">Select hello highlighted options in Portal as shown in hello following screenshot:</span></span>

![Création d’un espace de travail Microsoft Azure Machine Learning](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space.PNG)

* <span data-ttu-id="1ca8b-311">Puis entrez les paramètres hello pour votre espace de travail</span><span class="sxs-lookup"><span data-stu-id="1ca8b-311">Then enter hello parameters for your workspace</span></span>

![Entrer les paramètres de l'espace de travail Machine Learning](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space_step2_v2.PNG)

* <span data-ttu-id="1ca8b-313">Téléchargez des données à l’aide d’IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-313">Upload data using IPython Notebook.</span></span> <span data-ttu-id="1ca8b-314">Tout d’abord importer les packages requis, incorporer des informations d’identification, créer une base de données dans votre compte de stockage, puis charge des clusters tooHDI de données.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-314">First import required packages, plug in credentials, create a db in your storage account, then load data tooHDI clusters.</span></span>

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


* <span data-ttu-id="1ca8b-315">Ou bien, vous pouvez suivre cette [procédure pas à pas](machine-learning-data-science-process-hive-walkthrough.md) tooupload cluster de tooHDI NYC Taxi données.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-315">Alternately,  you can follow this [walkthrough](machine-learning-data-science-process-hive-walkthrough.md) tooupload NYC Taxi data tooHDI cluster.</span></span> <span data-ttu-id="1ca8b-316">Voici les grandes étapes :</span><span class="sxs-lookup"><span data-stu-id="1ca8b-316">Major steps include:</span></span>
  
  * <span data-ttu-id="1ca8b-317">AzCopy : téléchargement compressé CSV à partir du dossier local blob publics tooyour</span><span class="sxs-lookup"><span data-stu-id="1ca8b-317">AzCopy: download zipped CSV's from public blob tooyour local folder</span></span>
  * <span data-ttu-id="1ca8b-318">AzCopy : télécharger décompressé CSV à partir du cluster de tooHDI dossier local</span><span class="sxs-lookup"><span data-stu-id="1ca8b-318">AzCopy: upload unzipped CSV's from local folder tooHDI cluster</span></span>
  * <span data-ttu-id="1ca8b-319">Connectez-vous à un nœud de tête hello de cluster Hadoop et préparer pour l’analyse exploratoire des données</span><span class="sxs-lookup"><span data-stu-id="1ca8b-319">Log into hello head node of Hadoop cluster and prepare for exploratory data analysis</span></span>

<span data-ttu-id="1ca8b-320">Une fois les données de salutation tooHDI chargé cluster, vous pouvez vérifier vos données dans l’Explorateur de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-320">After hello data is loaded tooHDI cluster, you can check your data in Azure Storage Explorer.</span></span> <span data-ttu-id="1ca8b-321">Et vous disposez d'une base de données nyctaxidb créée dans le cluster HDI.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-321">And you have a database nyctaxidb created in HDI cluster.</span></span>

<span data-ttu-id="1ca8b-322">**Exploration des données : requêtes Hive dans Python**</span><span class="sxs-lookup"><span data-stu-id="1ca8b-322">**Data exploration: Hive Queries in Python**</span></span>

<span data-ttu-id="1ca8b-323">Les données hello étant dans le cluster Hadoop, vous pouvez utiliser hello pyodbc package tooconnect tooHadoop Clusters et des requêtes de base de données à l’aide de la ruche toodo exploration et l’ingénierie de fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-323">Since hello data is in Hadoop cluster, you can use hello pyodbc package tooconnect tooHadoop Clusters and query database using Hive toodo exploration and feature engineering.</span></span> <span data-ttu-id="1ca8b-324">Vous pouvez afficher les tables existantes hello que nous avons créé à l’étape de configuration requise hello.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-324">You can view hello existing tables we created in hello prerequisite step.</span></span>

    queryString = """
        show tables in nyctaxidb2;
        """
    pd.read_sql(queryString,connection)


![Afficher les tables existantes](./media/machine-learning-data-science-vm-do-ten-things/Python_View_Existing_Tables_Hive_v3.PNG)

<span data-ttu-id="1ca8b-326">Examinons le nombre de hello d’enregistrements dans chaque mois et hello les fréquences de pourboires ou non dans la table de voyage hello :</span><span class="sxs-lookup"><span data-stu-id="1ca8b-326">Let's look at hello number of records in each month and hello frequencies of tipped or not in hello trip table:</span></span>

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

<span data-ttu-id="1ca8b-329">Nous pouvons également calculer la distance entre l’emplacement de collecte et l’emplacement de cette chute hello, puis les comparer toohello distance de déclenchement.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-329">We can also compute hello distance between pickup location and dropoff location and then compare it toohello trip distance.</span></span>

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

<span data-ttu-id="1ca8b-332">Nous allons maintenant préparer le jeu de données sous-échantillonné (1 %) pour la modélisation.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-332">Now let's prepare a down-sampled (1%) set of data for modeling.</span></span> <span data-ttu-id="1ca8b-333">Nous pouvons utiliser ces données dans le module lecteur Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-333">We can use this data in Machine Learning reader module.</span></span>

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

<span data-ttu-id="1ca8b-334">Après un certain temps, vous pouvez voir les données de salutation a été chargées dans les clusters Hadoop :</span><span class="sxs-lookup"><span data-stu-id="1ca8b-334">After a while, you can see hello data has been loaded in Hadoop clusters:</span></span>

    queryString = """
        select * from nyctaxi_downsampled_dataset limit 10;
        """
    cursor.execute(queryString)
    pd.read_sql(queryString,connection)


![Table de données](./media/machine-learning-data-science-vm-do-ten-things/DownSample_Data_For_Modeling_v2.PNG)

<span data-ttu-id="1ca8b-336">**Lire des données à partir de HDI en utilisant le module lecteur Machine Learning**</span><span class="sxs-lookup"><span data-stu-id="1ca8b-336">**Read data from HDI using Machine Learning: reader module**</span></span>

<span data-ttu-id="1ca8b-337">Vous pouvez également utiliser hello **lecteur** module Machine Learning Studio tooaccess hello base de données de cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-337">You may also use hello **reader** module in Machine Learning Studio tooaccess hello database in Hadoop cluster.</span></span> <span data-ttu-id="1ca8b-338">Informations d’identification hello vos clusters HDI plug-in et tooenable de compte de stockage Azure générer des modèles à l’aide de la base de données dans les clusters HDI d’apprentissage effectue une opération.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-338">Plug in hello credentials of your HDI clusters and Azure Storage Account tooenable build ing machine learning models using database in HDI clusters.</span></span>

![Propriétés du module lecteur](./media/machine-learning-data-science-vm-do-ten-things/AML_Reader_Hive.PNG)

<span data-ttu-id="1ca8b-340">Hello jeu de données au score calculé peut alors être affiché :</span><span class="sxs-lookup"><span data-stu-id="1ca8b-340">hello scored dataset can then be viewed:</span></span>

![Affichage du jeu de données évalué](./media/machine-learning-data-science-vm-do-ten-things/AML_Model_Results.PNG)

### <a name="azure-sql-data-warehouse--databases"></a><span data-ttu-id="1ca8b-342">Azure SQL Data Warehouse et bases de données</span><span class="sxs-lookup"><span data-stu-id="1ca8b-342">Azure SQL Data Warehouse & databases</span></span>
<span data-ttu-id="1ca8b-343">Azure SQL Data Warehouse est un entrepôt de données élastique en tant que service offrant une expérience SQL Server professionnelle.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-343">Azure SQL Data Warehouse is an elastic data warehouse as a service with enterprise-class SQL Server experience.</span></span>

<span data-ttu-id="1ca8b-344">Vous pouvez configurer votre entrepôt de données SQL Azure en suivant les instructions hello fournies dans cette [article](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md).</span><span class="sxs-lookup"><span data-stu-id="1ca8b-344">You can provision your Azure SQL Data Warehouse by following hello instructions provided in this [article](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md).</span></span> <span data-ttu-id="1ca8b-345">Une fois que vous configurez votre entrepôt de données SQL Azure, vous pouvez utiliser cette [procédure pas à pas](machine-learning-data-science-process-sqldw-walkthrough.md) toodo données télécharger, exploration et modélisation à l’aide des données au sein de hello SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-345">Once you provision your Azure SQL Data Warehouse, you can use this [walkthrough](machine-learning-data-science-process-sqldw-walkthrough.md) toodo data upload, exploration and modeling using data within hello SQL Data Warehouse.</span></span>

#### <a name="azure-cosmos-db"></a><span data-ttu-id="1ca8b-346">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="1ca8b-346">Azure Cosmos DB</span></span>
<span data-ttu-id="1ca8b-347">Base de données Cosmos Azure est une base de données NoSQL dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-347">Azure Cosmos DB is a NoSQL database in hello cloud.</span></span> <span data-ttu-id="1ca8b-348">Il vous permet de toowork avec des documents comme JSON et vous permet des documents hello toostore et la requête.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-348">It allows you toowork with documents like JSON and allows you toostore and query hello documents.</span></span>

<span data-ttu-id="1ca8b-349">Vous devez hello toodo suivant par requis étapes tooaccess base de données Azure Cosmos hello DSVM.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-349">You need toodo hello following per-requisites steps tooaccess Azure Cosmos DB from hello DSVM.</span></span>

1. <span data-ttu-id="1ca8b-350">Installez le Kit de développement logiciel (SDK) Python DocumentDB (exécutez ```pip install pydocumentdb``` à partir de l’invite de commandes)</span><span class="sxs-lookup"><span data-stu-id="1ca8b-350">Install DocumentDB Python SDK (Run ```pip install pydocumentdb``` from command prompt)</span></span>
2. <span data-ttu-id="1ca8b-351">Créez un compte Azure Cosmos DB et une base de données à partir du [portail Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="1ca8b-351">Create an Azure Cosmos DB account and a database from [Azure portal](https://portal.azure.com)</span></span>
3. <span data-ttu-id="1ca8b-352">Télécharger « Azure Cosmos DB Migration Tool » à partir de [ici](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d) et extraire le répertoire tooa de votre choix</span><span class="sxs-lookup"><span data-stu-id="1ca8b-352">Download "Azure Cosmos DB Migration Tool" from [here](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d) and extract tooa directory of your choice</span></span>
4. <span data-ttu-id="1ca8b-353">Importer des données JSON (données îles) stockées sur un [objet blob public](https://cahandson.blob.core.windows.net/samples/volcano.json) dans base de données Cosmos avec suivant commande paramètres toohello outil de migration de (dtui.exe à partir du répertoire hello où vous avez installé hello Cosmos outil de Migration de base de données).</span><span class="sxs-lookup"><span data-stu-id="1ca8b-353">Import JSON data (volcano data) stored on a [public blob](https://cahandson.blob.core.windows.net/samples/volcano.json) into Cosmos DB with following command parameters toohello migration tool (dtui.exe from hello directory where you installed hello Cosmos DB Migration Tool).</span></span> <span data-ttu-id="1ca8b-354">Entrez les emplacements source et cible de hello avec ces paramètres :</span><span class="sxs-lookup"><span data-stu-id="1ca8b-354">Enter hello source and target location with these parameters:</span></span>
   
    <span data-ttu-id="1ca8b-355">/s:JsonFile /s.Files:https://cahandson.blob.core.windows.net/samples/volcano.json /t:DocumentDBBulk /t.ConnectionString:AccountEndpoint=https://[DocDBAccountName].documents.azure.com:443/;AccountKey=[[KEY];Database=volcano /t.Collection:volcano1</span><span class="sxs-lookup"><span data-stu-id="1ca8b-355">/s:JsonFile /s.Files:https://cahandson.blob.core.windows.net/samples/volcano.json /t:DocumentDBBulk /t.ConnectionString:AccountEndpoint=https://[DocDBAccountName].documents.azure.com:443/;AccountKey=[[KEY];Database=volcano /t.Collection:volcano1</span></span>

<span data-ttu-id="1ca8b-356">Une fois que vous importez des données de hello, vous pouvez accéder tooJupyter et portable hello ouvrir intitulée *DocumentDBSample* qui contient les python tooaccess DocumentDB du code et effectuer des requêtes de base.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-356">Once you import hello data, you can go tooJupyter and open hello notebook titled *DocumentDBSample* which contains python code tooaccess DocumentDB and do some basic querying.</span></span> <span data-ttu-id="1ca8b-357">Vous pouvez en savoir plus sur Cosmos DB en visitant le service de hello [page de documentation](https://docs.microsoft.com/azure/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="1ca8b-357">You can learn more about Cosmos DB by visiting hello service [documentation page](https://docs.microsoft.com/azure/cosmos-db/).</span></span>

## <a name="8-build-reports-and-dashboard-using-hello-power-bi-desktop"></a><span data-ttu-id="1ca8b-358">8. Générer des rapports et tableau de bord à l’aide de hello Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="1ca8b-358">8. Build reports and dashboard using hello Power BI Desktop</span></span>
<span data-ttu-id="1ca8b-359">Nous permet de visualiser fichier îles JSON hello que nous avons vu dans hello précédant l’exemple de base de données Cosmos dans Power BI toogain visual connaître les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-359">Let us visualize hello Volcano JSON file that we saw in hello preceding Cosmos DB example in Power BI toogain visual insights into hello data.</span></span> <span data-ttu-id="1ca8b-360">Les étapes détaillées sont disponibles dans hello [article de Power BI](../cosmos-db/powerbi-visualize.md).</span><span class="sxs-lookup"><span data-stu-id="1ca8b-360">Detailed steps are available in hello [Power BI article](../cosmos-db/powerbi-visualize.md).</span></span> <span data-ttu-id="1ca8b-361">Voici les étapes principales hello :</span><span class="sxs-lookup"><span data-stu-id="1ca8b-361">Here are hello high-level steps:</span></span>

1. <span data-ttu-id="1ca8b-362">Ouvrez Power BI Desktop et cliquez sur « obtenir les données ».</span><span class="sxs-lookup"><span data-stu-id="1ca8b-362">Open Power BI Desktop and do "Get Data".</span></span> <span data-ttu-id="1ca8b-363">Spécifiez l’URL hello : https://cahandson.blob.core.windows.net/samples/volcano.json</span><span class="sxs-lookup"><span data-stu-id="1ca8b-363">Specify hello URL as: https://cahandson.blob.core.windows.net/samples/volcano.json</span></span>
2. <span data-ttu-id="1ca8b-364">Vous devez voir les enregistrements JSON hello importés sous forme de liste</span><span class="sxs-lookup"><span data-stu-id="1ca8b-364">You should see hello JSON records imported as a list</span></span>
3. <span data-ttu-id="1ca8b-365">Convertir la table de tooa de liste de hello pour Power BI peut manipuler hello même</span><span class="sxs-lookup"><span data-stu-id="1ca8b-365">Convert hello list tooa table so Power BI can work with hello same</span></span>
4. <span data-ttu-id="1ca8b-366">Développez l’icône (hello une icône de « flèche gauche et flèche vers la droite » hello sur hello à droite de la colonne de hello) de développement de colonnes hello en cliquant sur hello</span><span class="sxs-lookup"><span data-stu-id="1ca8b-366">Expand hello columns by clicking on hello expand icon (hello one with hello "left arrow and a right arrow" icon on hello right of hello column)</span></span>
5. <span data-ttu-id="1ca8b-367">Notez que cet emplacement est un champ « Enregistrement ».</span><span class="sxs-lookup"><span data-stu-id="1ca8b-367">Notice that location is a "Record" field.</span></span> <span data-ttu-id="1ca8b-368">Développez hello enregistrement et sélectionnez uniquement les coordonnées hello.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-368">Expand hello record and select only hello coordinates.</span></span> <span data-ttu-id="1ca8b-369">Une coordonnée est une colonne de liste</span><span class="sxs-lookup"><span data-stu-id="1ca8b-369">Coordinate is a list column</span></span>
6. <span data-ttu-id="1ca8b-370">Ajouter une nouvelle colonne tooconvert hello liste coordonnée de colonnes dans une colonne LatLong séparée virgules concaténation éléments hello deux dans le champ de liste de coordonnées hello à l’aide de la formule de hello ```Text.From([coordinates]{1})&","&Text.From([coordinates]{0})```.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-370">Add a new column tooconvert hello list coordinate column into a comma separate LatLong column concatenating hello two elements in hello coordinate list field using hello formula ```Text.From([coordinates]{1})&","&Text.From([coordinates]{0})```.</span></span>
7. <span data-ttu-id="1ca8b-371">Convertissez hello ```Elevation``` tooDecimal de colonne et sélectionnez hello **fermer** et **appliquer**.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-371">Finally convert hello ```Elevation``` column tooDecimal and select hello **Close** and **Apply**.</span></span>

<span data-ttu-id="1ca8b-372">Au lieu d’étapes précédentes, vous pouvez coller hello suivant code étapes hello utilisée dans les scripts hello éditeur avancé dans Power BI qui vous permet de transformations de données toowrite hello dans un langage de requête.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-372">Instead of preceding steps, you can paste hello following code that scripts out hello steps used in hello Advanced Editor in Power BI that allows you toowrite hello data transformations in a query language.</span></span>

    let
        Source = Json.Document(Web.Contents("https://cahandson.blob.core.windows.net/samples/volcano.json")),
        #"Converted tooTable" = Table.FromList(Source, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
        #"Expanded Column1" = Table.ExpandRecordColumn(#"Converted tooTable", "Column1", {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}, {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}),
        #"Expanded Location" = Table.ExpandRecordColumn(#"Expanded Column1", "Location", {"coordinates"}, {"coordinates"}),
        #"Added Custom" = Table.AddColumn(#"Expanded Location", "LatLong", each Text.From([coordinates]{1})&","&Text.From([coordinates]{0})),
        #"Changed Type" = Table.TransformColumnTypes(#"Added Custom",{{"Elevation", type number}})
    in
        #"Changed Type"



<span data-ttu-id="1ca8b-373">Vous avez maintenant les données de salutation dans votre modèle de données Power BI.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-373">You now have hello data in your Power BI data model.</span></span> <span data-ttu-id="1ca8b-374">Votre Power BI Desktop doit apparaître comme suit :</span><span class="sxs-lookup"><span data-stu-id="1ca8b-374">Your Power BI desktop should appear as follows:</span></span>

![Power BI Desktop](./media/machine-learning-data-science-vm-do-ten-things/PowerBIVolcanoData.png)

<span data-ttu-id="1ca8b-376">Vous pouvez démarrer la création de rapports et des visualisations à l’aide du modèle de données hello.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-376">You can start building reports and visualizations using hello data model.</span></span> <span data-ttu-id="1ca8b-377">Vous pouvez suivre les étapes de hello dans ce [article de Power BI](../cosmos-db/powerbi-visualize.md#build-the-reports) toobuild un rapport.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-377">You can follow hello steps in this [Power BI article](../cosmos-db/powerbi-visualize.md#build-the-reports) toobuild a report.</span></span> <span data-ttu-id="1ca8b-378">résultat final de Hello est un rapport qui ressemble à hello suivant.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-378">hello end result is a report that looks like hello following.</span></span>

![Power BI Desktop - Vue Rapport - Connecteur Power BI](./media/machine-learning-data-science-vm-do-ten-things/power_bi_connector_pbireportview2.png)

## <a name="9-dynamically-scale-your-dsvm-toomeet-your-project-needs"></a><span data-ttu-id="1ca8b-380">9. Évoluer dynamiquement votre toomeet DSVM qu'a besoin de votre projet</span><span class="sxs-lookup"><span data-stu-id="1ca8b-380">9. Dynamically scale your DSVM toomeet your project needs</span></span>
<span data-ttu-id="1ca8b-381">Vous pouvez évoluez toomeet DSVM hello qu'a besoin de votre projet.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-381">You can scale up and down hello DSVM toomeet your project needs.</span></span> <span data-ttu-id="1ca8b-382">Si vous n’avez pas besoin toouse hello machine virtuelle dans le soir hello ou les week-ends, vous pouvez simplement arrêté hello machine virtuelle à partir de hello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1ca8b-382">If you don't need toouse hello VM in hello evening or weekends, you can just shut down hello VM from hello [Azure portal](https://portal.azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="1ca8b-383">Vous encourez des frais de calcul si vous utilisez simplement les bouton d’arrêt de système d’exploitation hello sur hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-383">You incur compute charges if you use just hello Operating system shutdown button on hello VM.</span></span>  
> 
> 

<span data-ttu-id="1ca8b-384">Si vous devez toohandle des analyses à grande échelle et que vous avez besoin de plus de capacité du processeur et/ou de mémoire et de disque, vous trouverez un grand choix de tailles de machine virtuelle en termes de cœurs du processeur, la capacité de mémoire et types de disques (y compris les disques SSD) qui répondent à vos besoins budgétaires et le calcul.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-384">If you need toohandle some large-scale analysis and need more CPU and/or memory and/or disk capacity you can find a large choice of VM sizes in terms of CPU cores, memory capacity and disk types (including Solid state drives) that meet your compute and budgetary needs.</span></span> <span data-ttu-id="1ca8b-385">Bonjour la liste complète des ordinateurs virtuels en même temps que leur tarification toutes les heures de calcul est disponible sur hello [tarification des Machines virtuelles Azure](https://azure.microsoft.com/pricing/details/virtual-machines/) page.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-385">hello full list of VMs along with their hourly compute pricing is available on hello [Azure Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/) page.</span></span>

<span data-ttu-id="1ca8b-386">De même, si vos besoins en capacité de traitement de machine virtuelle réduit (par exemple : vous avez déplacé une tooa principales charges de travail Hadoop ou un cluster Spark), vous pouvez monter en puissance parallèle cluster hello de hello [portail Azure](https://portal.azure.com) et toohello les paramètres de votre machine virtuelle instance.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-386">Similarly, if your need for VM processing capacity reduces (for example: you moved a major workload tooa Hadoop or a Spark cluster), you can scale down hello cluster from hello [Azure portal](https://portal.azure.com) and going toohello settings of your VM instance.</span></span> <span data-ttu-id="1ca8b-387">Voici une capture d'écran.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-387">Here is a screenshot.</span></span>

![Paramètres de l'instance de machine virtuelle](./media/machine-learning-data-science-vm-do-ten-things/VMScaling.PNG)

## <a name="10-install-additional-tools-on-your-virtual-machine"></a><span data-ttu-id="1ca8b-389">10. Installer des outils supplémentaires sur votre machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="1ca8b-389">10. Install additional tools on your virtual machine</span></span>
<span data-ttu-id="1ca8b-390">Nous avons empaqueté plusieurs outils que nous pensons tooaddress en mesure de la plupart des besoins de hello courants données analytique et qui doivent vous permettre de gagner du temps en évitant d’avoir tooinstall et configurer vos environnements un par un et économiser de l’argent en payant uniquement pour les ressources que vous avez à utiliser.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-390">We have packaged several tools that we believe are able tooaddress many of hello common data analytics needs and that should save you time by avoiding having tooinstall and configure your environments one by one and save you money by paying only for resources that you use.</span></span>

<span data-ttu-id="1ca8b-391">Vous pouvez tirer parti des autres données Azure et les services analytique profilé dans cet article de tooenhance votre environnement analytique.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-391">You can leverage other Azure data and analytics services profiled in this article tooenhance your analytics environment.</span></span> <span data-ttu-id="1ca8b-392">Nous comprenons que, dans certains cas, vos besoins puissent nécessiter des outils supplémentaires, notamment des outils tiers propriétaires.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-392">We understand that in some cases your needs may require additional tools, including some proprietary third-party tools.</span></span> <span data-ttu-id="1ca8b-393">Vous avez un accès administrateur complet sur les nouveaux outils hello machine virtuelle tooinstall que vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-393">You have full administrative access on hello virtual machine tooinstall new tools you need.</span></span> <span data-ttu-id="1ca8b-394">Vous pouvez également installer des packages supplémentaires non préinstallés en Python et R.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-394">You can also install additional packages in Python and R that are not pre-installed.</span></span> <span data-ttu-id="1ca8b-395">Pour Python, vous pouvez utiliser soit ```conda```, soit ```pip```.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-395">For Python you can use either ```conda``` or ```pip```.</span></span> <span data-ttu-id="1ca8b-396">Pour R, vous pouvez utiliser hello ```install.packages()``` Bonjour R de la console ou utilisez hello IDE et choisissez «**Packages** -> **Packages d’installation...** ".</span><span class="sxs-lookup"><span data-stu-id="1ca8b-396">For R you can use hello ```install.packages()``` in hello R console or use hello IDE and choose "**Packages** -> **Install Packages...**".</span></span>

## <a name="summary"></a><span data-ttu-id="1ca8b-397">Résumé</span><span class="sxs-lookup"><span data-stu-id="1ca8b-397">Summary</span></span>
<span data-ttu-id="1ca8b-398">Voici quelques-uns des hello opérations pouvant être exécutées sur hello Machine virtuelle de science des données Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-398">These are just some of hello things you can do on hello Microsoft Data Science Virtual Machine.</span></span> <span data-ttu-id="1ca8b-399">Il existe bien d’autres choses que vous pouvez effectuer toomake il un environnement efficace analytique.</span><span class="sxs-lookup"><span data-stu-id="1ca8b-399">There are many more things you can do toomake it an effective analytics environment.</span></span>

