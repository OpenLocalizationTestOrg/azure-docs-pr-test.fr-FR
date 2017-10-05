---
title: "Dix choses que vous pouvez effectuer sur la machine virtuelle Science des données | Microsoft Docs"
description: "Effectuez diverses tâches de modélisation et d'exploration des données sur la machine virtuelle pour la science des données."
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
ms.openlocfilehash: 45af1cd3a05b483429d2307659f1882ef28921f6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="ten-things-you-can-do-on-the-data-science-virtual-machine"></a><span data-ttu-id="674df-103">Dix choses que vous pouvez effectuer sur la machine virtuelle pour la science des données</span><span class="sxs-lookup"><span data-stu-id="674df-103">Ten things you can do on the Data science Virtual Machine</span></span>
<span data-ttu-id="674df-104">La machine virtuelle pour la science des données (DSVM, « Data Science Virtual Machine ») Microsoft est un environnement puissant de développement de la science des données qui vous permet d'effectuer diverses tâches de modélisation et d'exploration des données.</span><span class="sxs-lookup"><span data-stu-id="674df-104">The Microsoft Data Science Virtual Machine (DSVM) is a powerful data science development environment that enables you to perform various data exploration and modeling tasks.</span></span> <span data-ttu-id="674df-105">L’environnement est déjà généré et fourni avec plusieurs outils d’analyse de données courants qui facilitent la prise en main rapide de votre analyse pour les déploiements sur site, dans le cloud ou hybrides.</span><span class="sxs-lookup"><span data-stu-id="674df-105">The environment comes already built and bundled with several popular data analytics tools that make it easy to get started quickly with your analysis for On-premises, Cloud or hybrid deployments.</span></span> <span data-ttu-id="674df-106">La DSVM fonctionne en lien avec de nombreux services Azure et peut lire et traiter les données déjà stockées sur Azure, dans Azure SQL Data Warehouse, Azure Data Lake, Stockage Azure et Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="674df-106">The DSVM works closely with many Azure services and is able to read and process data that is already stored on Azure, in Azure SQL Data Warehouse, Azure Data Lake, Azure Storage, or in Azure Cosmos DB.</span></span> <span data-ttu-id="674df-107">Elle peut également exploiter d’autres outils d’analyse tels qu’Azure Machine Learning et Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="674df-107">It can also leverage other analytics tools such as Azure Machine Learning and Azure Data Factory.</span></span>

<span data-ttu-id="674df-108">Dans cet article, nous vous guidons dans l'utilisation de votre DSVM afin d'effectuer diverses tâches de science des données et d'interagir avec d'autres services Azure.</span><span class="sxs-lookup"><span data-stu-id="674df-108">In this article we walk you through how to use your DSVM to perform various data science tasks and interact with other Azure services.</span></span> <span data-ttu-id="674df-109">Voici quelques-unes des tâches que vous pouvez effectuer sur la DSVM :</span><span class="sxs-lookup"><span data-stu-id="674df-109">Here are some of the things you can do on the DSVM:</span></span>

1. <span data-ttu-id="674df-110">Explorer les données et développer des modèles localement sur la DSVM avec Microsoft R Server et de Python</span><span class="sxs-lookup"><span data-stu-id="674df-110">Explore data and develop models locally on the DSVM using Microsoft R Server, Python</span></span>
2. <span data-ttu-id="674df-111">Utiliser un notebook Jupyter pour faire des expériences avec vos données sur un navigateur à l'aide de Python 2, Python 3 et Microsoft R, une version d'entreprise de R conçue pour l'évolutivité et les performances</span><span class="sxs-lookup"><span data-stu-id="674df-111">Use a Jupyter notebook to experiment with your data on a browser using Python 2, Python 3, Microsoft R an enterprise ready version of R designed for scalability and performance</span></span>
3. <span data-ttu-id="674df-112">Rendre opérationnels des modèles créés avec R et Python sur Azure Machine Learning afin que les applications clientes puissent accéder à vos modèles à l'aide d'une interface de services web simple</span><span class="sxs-lookup"><span data-stu-id="674df-112">Operationalize models built using R and Python on Azure Machine Learning so client applications can access your models using a simple web services interface</span></span>
4. <span data-ttu-id="674df-113">Administrer vos ressources Azure à l’aide du portail Azure ou de PowerShell</span><span class="sxs-lookup"><span data-stu-id="674df-113">Administer your Azure resources using  Azure portal or Powershell</span></span>
5. <span data-ttu-id="674df-114">Augmenter votre espace de stockage et partager des jeux de données / du code à grande échelle avec toute votre équipe en créant un stockage Fichier Azure comme lecteur montable sur votre DSVM</span><span class="sxs-lookup"><span data-stu-id="674df-114">Extend your storage space and share large-scale datasets / code across your whole team by creating an Azure File storage as a mountable drive on your DSVM</span></span>
6. <span data-ttu-id="674df-115">Partager du code avec votre équipe à l’aide de GitHub et accéder à votre dépôt à l’aide des clients Git préinstallés : Git Bash, Git GUI.</span><span class="sxs-lookup"><span data-stu-id="674df-115">Share code with your team using GitHub and access your repository using the pre-installed Git clients - Git Bash, Git GUI.</span></span>
7. <span data-ttu-id="674df-116">Accéder aux différents services de données et d’analytique Azure tels que Stockage Blob Azure, Azure Data Lake, Azure HDInsight (Hadoop), Azure Cosmos DB, Azure SQL Data Warehouse et Database</span><span class="sxs-lookup"><span data-stu-id="674df-116">Access various Azure data and analytics services like Azure blob storage, Azure Data Lake, Azure HDInsight (Hadoop), Azure Cosmos DB, Azure SQL Data Warehouse & databases</span></span>
8. <span data-ttu-id="674df-117">Générer des rapports et des tableaux de bord à l'aide du Power BI Desktop préinstallé sur la DSVM et les déployer sur le cloud</span><span class="sxs-lookup"><span data-stu-id="674df-117">Build reports and dashboard using the Power BI Desktop pre-installed on the DSVM and deploy them on the cloud</span></span>
9. <span data-ttu-id="674df-118">Mettre à l'échelle dynamiquement votre DSVM pour répondre aux besoins de votre projet</span><span class="sxs-lookup"><span data-stu-id="674df-118">Dynamically scale your DSVM to meet your project needs</span></span>
10. <span data-ttu-id="674df-119">Installer des outils supplémentaires sur votre machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="674df-119">Install additional tools on your virtual machine</span></span>   

> [!NOTE]
> <span data-ttu-id="674df-120">Des frais d’utilisation supplémentaires s’appliquent pour la plupart des services supplémentaires de stockage et d’analyse des données figurant dans cet article.</span><span class="sxs-lookup"><span data-stu-id="674df-120">Additional usage charges apply for many of the additional data storage and analytics services listed in this article.</span></span> <span data-ttu-id="674df-121">Pour plus d’informations, consultez la page sur la [tarification Azure](https://azure.microsoft.com/pricing/) .</span><span class="sxs-lookup"><span data-stu-id="674df-121">Please refer to the [Azure Pricing](https://azure.microsoft.com/pricing/) page for details.</span></span>
> 
> 

<span data-ttu-id="674df-122">**Configuration requise**</span><span class="sxs-lookup"><span data-stu-id="674df-122">**Prerequisites**</span></span>

* <span data-ttu-id="674df-123">Vous avez besoin d’un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="674df-123">You need an Azure subscription.</span></span> <span data-ttu-id="674df-124">Vous pouvez vous inscrire à un essai gratuit [ici](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="674df-124">You can sign up for a free trial [here](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="674df-125">Des instructions d’approvisionnement d’une machine virtuelle pour la science des données sur le Portail Azure sont disponibles dans [Création d’une machine virtuelle](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm).</span><span class="sxs-lookup"><span data-stu-id="674df-125">Instructions for provisioning a Data Science Virtual Machine on the Azure portal are available at [Creating a virtual machine](https://portal.azure.com/#create/microsoft-ads.standard-data-science-vmstandard-data-science-vm).</span></span>

## <a name="1-explore-data-and-develop-models-using-microsoft-r-server-or-python"></a><span data-ttu-id="674df-126">1. Explorer les données et développer des modèles à l'aide de Microsoft R Server ou de Python</span><span class="sxs-lookup"><span data-stu-id="674df-126">1. Explore data and develop models using Microsoft R Server or Python</span></span>
<span data-ttu-id="674df-127">Vous pouvez utiliser des langages tels que R et Python pour effectuer des analyses de données directement sur la DSVM.</span><span class="sxs-lookup"><span data-stu-id="674df-127">You can use languages like R and Python to do your data analytics right on the DSVM.</span></span>

<span data-ttu-id="674df-128">Pour R, vous pouvez utiliser un IDE appelé « Revolution R Enterprise 8.0 » qui se trouve dans le menu Démarrer ou sur le bureau.</span><span class="sxs-lookup"><span data-stu-id="674df-128">For R, you can use an IDE called "Revolution R Enterprise 8.0" that can be found on the start menu or the desktop.</span></span> <span data-ttu-id="674df-129">Microsoft a fourni des bibliothèques supplémentaires en plus d'Open source/CRAN-R pour permettre de mettre à l'échelle les analyses et d'analyser des volumes de données plus importants que la taille de mémoire autorisée en effectuant une analyse parallèle par blocs.</span><span class="sxs-lookup"><span data-stu-id="674df-129">Microsoft has provided additional libraries on top of the Open source/CRAN-R to enable scalable analytics and the ability to analyze data larger than the memory size allowed by doing parallel chunked analysis.</span></span> <span data-ttu-id="674df-130">Vous pouvez également installer l’IDE R de votre choix, par exemple [RStudio](https://www.rstudio.com/products/rstudio-desktop/).</span><span class="sxs-lookup"><span data-stu-id="674df-130">You can also install an R IDE of your choice like [RStudio](https://www.rstudio.com/products/rstudio-desktop/).</span></span>

<span data-ttu-id="674df-131">Pour Python, vous pouvez utiliser un IDE comme Visual Studio Community Edition qui contient l'extension Outils Python pour Visual Studio (PTVS) préinstallée.</span><span class="sxs-lookup"><span data-stu-id="674df-131">For Python, you can use an IDE like Visual Studio Community Edition which has the Python Tools for Visual Studio (PTVS) extension pre-installed.</span></span> <span data-ttu-id="674df-132">Par défaut, seule une version de base de Python 2.7 est configurée sur PTVS (sans aucune bibliothèque d’analyse comme SciKit, Pandas).</span><span class="sxs-lookup"><span data-stu-id="674df-132">By default, only a basic Python 2.7 is configured on PTVS (without any analytics library like SciKit, Pandas).</span></span> <span data-ttu-id="674df-133">Pour activer Anaconda Python 2.7 et 3.5, vous devez effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="674df-133">In order to enable Anaconda Python 2.7 and 3.5, you need to do the following:</span></span>

* <span data-ttu-id="674df-134">Créez des environnements personnalisés pour chaque version en accédant à **Outils** -> **Outils Python** -> **Environnements Python**, puis en cliquant sur « **+ Personnalisé** » dans Visual Studio 2015 Community Edition</span><span class="sxs-lookup"><span data-stu-id="674df-134">Create custom environments for each version by navigating to **Tools** -> **Python Tools** -> **Python Environments** and then clicking "**+ Custom**" in the Visual Studio 2015 Community Edition</span></span>
* <span data-ttu-id="674df-135">Donnez une description et définissez le préfixe du chemin d’accès de l’environnement comme *c:\anaconda* pour Anaconda Python 2.7 OU *c:\anaconda\envs\py35* pour Anaconda Python 3.5</span><span class="sxs-lookup"><span data-stu-id="674df-135">Give a description and set the environment prefix paths as *c:\anaconda* for Anaconda Python 2.7 OR *c:\anaconda\envs\py35* for Anaconda Python 3.5</span></span>
* <span data-ttu-id="674df-136">Cliquez sur **Détection automatique**, puis sur **Appliquer** pour enregistrer l’environnement.</span><span class="sxs-lookup"><span data-stu-id="674df-136">Click **Auto Detect** and then **Apply** to save the environment.</span></span>

<span data-ttu-id="674df-137">Voici à quoi ressemble la configuration de l'environnement personnalisé dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="674df-137">Here is what the custom environment setup looks like in Visual Studio.</span></span>

![Installation PTVS](./media/machine-learning-data-science-vm-do-ten-things/PTVSSetup.png)

<span data-ttu-id="674df-139">Consultez la page [Documentation de PTVS](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) pour plus d’informations sur la création d’environnements Python.</span><span class="sxs-lookup"><span data-stu-id="674df-139">See the [PTVS documentation](https://github.com/Microsoft/PTVS/wiki/Selecting-and-Installing-Python-Interpreters#hey-i-already-have-an-interpreter-on-my-machine-but-ptvs-doesnt-seem-to-know-about-it) for additional details on how to create Python Environments.</span></span>

<span data-ttu-id="674df-140">Vous êtes maintenant prêt à créer un nouveau projet Python.</span><span class="sxs-lookup"><span data-stu-id="674df-140">Now you are set up to create a new Python project.</span></span> <span data-ttu-id="674df-141">Accédez à **Fichier** -> **Nouveau** -> **Projet** -> **Python** et sélectionnez le type d’application Python que vous créez.</span><span class="sxs-lookup"><span data-stu-id="674df-141">Navigate to **File** -> **New** -> **Project** -> **Python** and select the type of Python application you are building.</span></span> <span data-ttu-id="674df-142">Vous pouvez définir l’environnement Python pour le projet actuel sur la version souhaitée (Anaconda 2.7 ou 3.5) : cliquez avec le bouton droit sur l’**environnement Python**, sélectionnez **Ajouter/supprimer des environnements Python**, puis sélectionnez l’environnement que vous souhaitez associer au projet.</span><span class="sxs-lookup"><span data-stu-id="674df-142">You can set the Python environment for the current project to the desired version (Anaconda 2.7 or 3.5): right-click the **Python environment**, select **Add/Remove Python Environments**, and then select the desired environment to associate with the project.</span></span> <span data-ttu-id="674df-143">Vous trouverez plus d’informations sur l’utilisation de PTVS sur la page de [documentation](https://github.com/Microsoft/PTVS/wiki) produit.</span><span class="sxs-lookup"><span data-stu-id="674df-143">You can find more information about working with PTVS on the product [documentation](https://github.com/Microsoft/PTVS/wiki) page.</span></span>

## <a name="2-using-a-jupyter-notebook-to-explore-and-model-your-data-with-python-or-r"></a><span data-ttu-id="674df-144">2. Utiliser un Notebook Jupyter pour explorer et modéliser vos données avec Python ou R</span><span class="sxs-lookup"><span data-stu-id="674df-144">2. Using a Jupyter Notebook to explore and model your data with Python or R</span></span>
<span data-ttu-id="674df-145">Le Notebook Jupyter est un environnement puissant qui fournit un « IDE » de modélisation et d'exploration de données sur navigateur.</span><span class="sxs-lookup"><span data-stu-id="674df-145">The Jupyter Notebook is a powerful environment that provides a browser-based "IDE" for data exploration and modeling.</span></span> <span data-ttu-id="674df-146">Vous pouvez utiliser Python 2, Python 3 ou R (Open Source et Microsoft R Server) dans le notebook Jupyter.</span><span class="sxs-lookup"><span data-stu-id="674df-146">You can use Python 2, Python 3 or R (both Open Source and the Microsoft R Server) in a Jupyter Notebook.</span></span>

<span data-ttu-id="674df-147">Pour lancer le notebook Jupyter, cliquez sur l’icône du menu Démarrer ou du bureau intitulée **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="674df-147">To launch the Jupyter Notebook click on the start menu icon / desktop icon titled **Jupyter Notebook**.</span></span> <span data-ttu-id="674df-148">Sur la DSVM vous pouvez également aller à « https://localhost:9999/ » pour accéder au notebook Jupyter.</span><span class="sxs-lookup"><span data-stu-id="674df-148">On the DSVM you can also browse to "https://localhost:9999/" to access the Jupiter Notebook.</span></span> <span data-ttu-id="674df-149">Si un mot de passe vous est demandé, suivez les instructions fournies dans la section ***Création d’un mot de passe sur le serveur Jupyter Notebook*** de la rubrique [Approvisionner la machine virtuelle pour la science des données Microsoft](machine-learning-data-science-provision-vm.md) pour créer un mot de passe fort et ainsi accéder au Notebook Jupyter.</span><span class="sxs-lookup"><span data-stu-id="674df-149">If it prompts you for a password, use instructions provided in the ***How to create a strong password on the Jupyter notebook server*** section of the [Provision the Microsoft Data Science Virtual Machine](machine-learning-data-science-provision-vm.md) topic to create a strong password to access the Jupyter notebook.</span></span> 

<span data-ttu-id="674df-150">Une fois le notebook ouvert, vous devriez voir un répertoire contenant quelques exemples de notebooks pré-intégrés à la DSVM.</span><span class="sxs-lookup"><span data-stu-id="674df-150">Once you have opened the notebook, you should see a directory that contains a few example notebooks that are pre-packaged into the DSVM.</span></span> <span data-ttu-id="674df-151">Vous pouvez désormais :</span><span class="sxs-lookup"><span data-stu-id="674df-151">Now you can:</span></span>

* <span data-ttu-id="674df-152">cliquer sur le notebook pour visualiser le code ;</span><span class="sxs-lookup"><span data-stu-id="674df-152">click on the notebook to see the code.</span></span>
* <span data-ttu-id="674df-153">exécuter chaque cellule en appuyant sur **MAJ-ENTRÉE**;</span><span class="sxs-lookup"><span data-stu-id="674df-153">execute each cell by pressing **SHIFT-ENTER**.</span></span>
* <span data-ttu-id="674df-154">exécuter le bloc-notes entier en cliquant sur **Cellule** -> **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="674df-154">run the entire notebook by clicking on **Cell** -> **Run**</span></span>
* <span data-ttu-id="674df-155">créer un nouveau notebook en cliquant sur l’icône Jupyter (coin supérieur gauche), puis sur le bouton **Nouveau** sur la droite et en sélectionnant la langue du notebook (également appelé noyau).</span><span class="sxs-lookup"><span data-stu-id="674df-155">create a new notebook by clicking on the Jupyter Icon (left top corner) and then clicking **New** button on the right and then choosing the notebook language (also known as kernels).</span></span>   

> [!NOTE]
> <span data-ttu-id="674df-156">Actuellement, nous prenons en charge Python 2.7, Python 3.5 et R. Le noyau R prend en charge la programmation dans Open source R ainsi que Microsoft R Server, évolutif à l'échelle de l'entreprise.</span><span class="sxs-lookup"><span data-stu-id="674df-156">Currently we support Python 2.7, Python 3.5 and R. The R kernel supports programming in both Open source R as well as the enterprise scalable Microsoft R Server.</span></span>   
> 
> 

<span data-ttu-id="674df-157">Une fois dans le notebook, vous pouvez explorer vos données, générer le modèle et le tester avec les bibliothèques de votre choix.</span><span class="sxs-lookup"><span data-stu-id="674df-157">Once you are in the notebook you can explore your data, build the model, test the model using your choice of libraries.</span></span>

## <a name="3-build-models-using-r-or-python-and-operationalize-them-using-azure-machine-learning"></a><span data-ttu-id="674df-158">3. Générer des modèles avec R ou Python et les rendre opérationnels à l’aide d’Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="674df-158">3. Build models using R or Python and Operationalize them using Azure Machine Learning</span></span>
<span data-ttu-id="674df-159">Une fois que vous avez créé et validé votre modèle, l'étape suivante consiste généralement à le déployer en production.</span><span class="sxs-lookup"><span data-stu-id="674df-159">Once you have built and validated your model the next step is usually to deploy it into production.</span></span> <span data-ttu-id="674df-160">Cela permet à vos applications clientes d’appeler les prédictions de modèle en temps réel ou par lots.</span><span class="sxs-lookup"><span data-stu-id="674df-160">This allows your client applications to invoke the model predictions on a real time or on a batch mode basis.</span></span> <span data-ttu-id="674df-161">Azure Machine Learning fournit un mécanisme permettant de faire fonctionner un modèle généré avec R ou Python.</span><span class="sxs-lookup"><span data-stu-id="674df-161">Azure Machine Learning provides a mechanism to operationalize a model built in either R or Python.</span></span>

<span data-ttu-id="674df-162">Lorsque vous rendez votre modèle opérationnel dans Azure Machine Learning, un service web est exposé. Il permet aux clients d'effectuer des appels REST qui transmettent des paramètres d'entrée et reçoivent des prédictions du modèle en tant que sorties.</span><span class="sxs-lookup"><span data-stu-id="674df-162">When you operationalize your model in Azure Machine Learning, a web service is exposed that allows clients to make REST calls that pass in input parameters and receive predictions from the model as outputs.</span></span>   

> [!NOTE]
> <span data-ttu-id="674df-163">Si vous n’êtes pas encore inscrit à Azure Machine Learning, vous pouvez obtenir un espace de travail gratuit ou standard en vous rendant sur la page d’accueil [Azure Machine Learning Studio](https://studio.azureml.net/) et en cliquant sur « Démarrer ».</span><span class="sxs-lookup"><span data-stu-id="674df-163">If you have not yet signed up for Azure Machine Learning, you can obtain a free workspace or a standard workspace by visiting the [Azure Machine Learning Studio](https://studio.azureml.net/) home page and clicking on "Get Started".</span></span>   
> 
> 

### <a name="build-and-operationalize-python-models"></a><span data-ttu-id="674df-164">Générer et rendre opérationnels des modèles Python</span><span class="sxs-lookup"><span data-stu-id="674df-164">Build and Operationalize Python models</span></span>
<span data-ttu-id="674df-165">Voici un extrait de code développé dans un notebook Jupyter Python qui génère un modèle simple à l’aide de la bibliothèque SciKit-learn.</span><span class="sxs-lookup"><span data-stu-id="674df-165">Here is a snippet of code developed in a Python Jupyter Notebook that builds a simple model using the SciKit-learn library.</span></span>

    #IRIS classification
    from sklearn import datasets
    from sklearn import svm
    clf = svm.SVC()
    iris = datasets.load_iris()
    X, y = iris.data, iris.target
    clf.fit(X, y)

<span data-ttu-id="674df-166">La méthode utilisée pour déployer vos modèles Python sur Azure Machine Learning inclut la prédiction du modèle dans une fonction et lui ajoute des attributs fournis par la bibliothèque Python Azure Machine Learning préinstallée. Celle-ci dépend de l’ID, de la clé API et des paramètres d’entrée et de retour de votre espace de travail Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="674df-166">The method used to deploy your python models to Azure Machine Learning wraps the prediction of the model into a function and decorates it with attributes provided by the pre-installed Azure Machine Learning python library that denote your Azure Machine Learning workspace ID, API Key, and the input and return parameters.</span></span>  

    from azureml import services
    @services.publish(workspaceid, auth_token)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(int) #0, or 1, or 2
    def predictIris(sep_l, sep_w, pet_l, pet_w):
     inputArray = [sep_l, sep_w, pet_l, pet_w]
    return clf.predict(inputArray)

<span data-ttu-id="674df-167">Un client peut désormais effectuer des appels au service web.</span><span class="sxs-lookup"><span data-stu-id="674df-167">A client can now make calls to the web service.</span></span> <span data-ttu-id="674df-168">Il existe des wrappers tout préparés qui construisent les demandes d'API REST.</span><span class="sxs-lookup"><span data-stu-id="674df-168">There are convenience wrappers that construct the REST API requests.</span></span> <span data-ttu-id="674df-169">Voici un exemple de code pour utiliser le service web.</span><span class="sxs-lookup"><span data-stu-id="674df-169">Here is a sample code to consume the web service.</span></span>

    # Consume through web service URL and keys
    from azureml import services
    @services.service(url, api_key)
    @services.types(sep_l = float, sep_w = float, pet_l=float, pet_w=float)
    @services.returns(float)
    def IrisPredictor(sep_l, sep_w, pet_l, pet_w):
    pass

    IrisPredictor(3,2,3,4)


> [!NOTE]
> <span data-ttu-id="674df-170">Actuellement, la bibliothèque Azure Machine Learning est uniquement prise en charge par Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="674df-170">The Azure Machine Learning library is only supported on Python 2.7 currently.</span></span>   
> 
> 

### <a name="build-and-operationalize-r-models"></a><span data-ttu-id="674df-171">Générer et rendre opérationnels des modèles R</span><span class="sxs-lookup"><span data-stu-id="674df-171">Build and Operationalize R models</span></span>
<span data-ttu-id="674df-172">Vous pouvez déployer des modèles R générés sur la machine virtuelle pour la science des données ou ailleurs sur Azure Machine Learning de la même façon que pour Python.</span><span class="sxs-lookup"><span data-stu-id="674df-172">You can deploy R models built on the Data Science Virtual Machine or elsewhere onto Azure Machine Learning in a manner that is similar to how it is done for Python.</span></span> <span data-ttu-id="674df-173">Voici la procédure à suivre :</span><span class="sxs-lookup"><span data-stu-id="674df-173">Her are the steps:</span></span>

* <span data-ttu-id="674df-174">Créez un fichier settings.json pour fournir votre ID d’espace de travail et votre jeton d’authentification, comme le montre l’exemple de code suivant.</span><span class="sxs-lookup"><span data-stu-id="674df-174">create a settings.json file to provide your workspace ID and auth token as shown in the following code sample.</span></span>
* <span data-ttu-id="674df-175">Écrivez ensuite un wrapper pour la fonction de prédiction du modèle.</span><span class="sxs-lookup"><span data-stu-id="674df-175">write a wrapper for the model's predict function.</span></span>
* <span data-ttu-id="674df-176">Appelez ```publishWebService``` dans la bibliothèque Azure Machine Learning pour transmettre le wrapper de la fonction.</span><span class="sxs-lookup"><span data-stu-id="674df-176">call ```publishWebService``` in the Azure Machine Learning library to pass in the function wrapper.</span></span>  

<span data-ttu-id="674df-177">Voici la procédure et les extraits de code qui peuvent être utilisés pour configurer, créer, publier et utiliser un modèle tel qu’un service web dans Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="674df-177">Here is the procedure and code snippets that can be used to set up, build, publish, and consume a model as a web service in Azure Machine Learning.</span></span>

#### <a name="setup"></a><span data-ttu-id="674df-178">Paramétrage</span><span class="sxs-lookup"><span data-stu-id="674df-178">Setup</span></span>
1. <span data-ttu-id="674df-179">Installez le package Machine Learning R en tapant ```install.packages("AzureML")``` dans l’IDE Revolution R Enterprise 8.0 ou dans votre IDE R.</span><span class="sxs-lookup"><span data-stu-id="674df-179">Install the Machine Learning R package by typing ```install.packages("AzureML")``` in Revolution R Enterprise 8.0 IDE or your R IDE.</span></span>
2. <span data-ttu-id="674df-180">Téléchargez RTools [ici](https://cran.r-project.org/bin/windows/Rtools/).</span><span class="sxs-lookup"><span data-stu-id="674df-180">Download RTools from [here](https://cran.r-project.org/bin/windows/Rtools/).</span></span> <span data-ttu-id="674df-181">L’utilitaire zip doit se trouver dans le dossier (et porter le nom zip.exe) pour rendre votre package R opérationnel dans Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="674df-181">You need the zip utility in the path (and named zip.exe) to operationalize your R package into Machine Learning.</span></span>
3. <span data-ttu-id="674df-182">Créez un fichier settings.json dans un répertoire appelé ```.azureml``` dans votre répertoire de base, puis entrez les paramètres de votre espace de travail Azure Machine Learning :</span><span class="sxs-lookup"><span data-stu-id="674df-182">Create a settings.json file under a directory called ```.azureml``` under your home directory and enter the parameters from your Azure Machine Learning workspace:</span></span>

<span data-ttu-id="674df-183">Structure du fichier settings.json :</span><span class="sxs-lookup"><span data-stu-id="674df-183">settings.json File structure:</span></span>

    {"workspace":{
    "id"                  : "ENTER YOUR AZUREML WORKSPACE ID",
    "authorization_token" : "ENTER YOUR AZUREML AUTH TOKEN"
    }}


#### <a name="build-a-model-in-r-and-publish-it-in-azure-machine-learning"></a><span data-ttu-id="674df-184">Générer un modèle dans R et le publier dans Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="674df-184">Build a model in R and publish it in Azure Machine Learning</span></span>
    library(AzureML)
    ws <- workspace(config="~/.azureml/settings.json")

    if(!require("lme4")) install.packages("lme4")
    library(lme4)
    set.seed(1)
    train <- sleepstudy[sample(nrow(sleepstudy), 120),]
    m <- lm(Reaction ~ Days + Subject, data = train)

    # Define a prediction function to publish based on the model:
    sleepyPredict <- function(newdata){
          predict(m, newdata=newdata)
    }

    ep <- publishWebService(ws, fun = sleepyPredict, name="sleepy lm", inputSchema = sleepstudy, data.frame=TRUE)

#### <a name="consume-the-model-deployed-in-azure-machine-learning"></a><span data-ttu-id="674df-185">Utiliser le modèle déployé dans Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="674df-185">Consume the model deployed in Azure Machine Learning</span></span>
<span data-ttu-id="674df-186">Pour utiliser le modèle à partir d’une application cliente, nous utilisons la bibliothèque Azure Machine Learning pour rechercher le service web publié par nom à l’aide de l’appel d’API `services` afin de déterminer le point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="674df-186">To consume the model from a client application, we use the Azure Machine Learning library to look up the published web service by name using the `services` API call to determine the endpoint.</span></span> <span data-ttu-id="674df-187">Il vous suffit ensuite d’appeler la fonction `consume` et de transmettre la trame de données à prédire.</span><span class="sxs-lookup"><span data-stu-id="674df-187">Then you just call the `consume` function and pass in the data frame to be predicted.</span></span>
<span data-ttu-id="674df-188">Le code suivant permet d’utiliser le modèle publié comme service web Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="674df-188">The following code is used to consume the model published as an Azure Machine Learning web service.</span></span>

    library(AzureML)
    library(lme4)
    ws <- workspace(config="~/.azureml/settings.json")

    s <-  services(ws, name = "sleepy lm")
    s <- tail(s, 1) # use the last published function, in case of duplicate function names

    ep <- endpoints(ws, s)

    # OK, try this out, and compare with raw data
    ans = consume(ep, sleepstudy)$ans

<span data-ttu-id="674df-189">Vous trouverez plus d’informations sur la bibliothèque R Azure Machine Learning [ici](https://cran.r-project.org/web/packages/AzureML/AzureML.pdf).</span><span class="sxs-lookup"><span data-stu-id="674df-189">More information about the Azure Machine Learning R library can be found [here](https://cran.r-project.org/web/packages/AzureML/AzureML.pdf).</span></span>

## <a name="4-administer-your-azure-resources-using-azure-portal-or-powershell"></a><span data-ttu-id="674df-190">4. Administrer vos ressources Azure à l’aide du Portail Azure ou de PowerShell</span><span class="sxs-lookup"><span data-stu-id="674df-190">4. Administer your Azure resources using Azure portal or Powershell</span></span>
<span data-ttu-id="674df-191">La DSVM vous permet non seulement de développer votre solution d'analyse localement sur la machine virtuelle, mais également d'accéder aux services sur le cloud Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="674df-191">The DSVM not only allows you to build your analytics solution locally on the virtual machine, but also allows you to access services on Microsoft's Azure cloud.</span></span> <span data-ttu-id="674df-192">Azure fournit plusieurs services de calcul, de stockage, d'analyse de données et autres que vous pouvez administrer et auxquels vous pouvez accéder à partir de votre DSVM.</span><span class="sxs-lookup"><span data-stu-id="674df-192">Azure provides several compute, storage, data analytics services and other services that you can administer and access from your DSVM.</span></span>

<span data-ttu-id="674df-193">Pour gérer vos ressources cloud et votre abonnement Azure, vous pouvez utiliser votre navigateur et pointer vers le [Portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="674df-193">To administer your Azure subscription and cloud resources you can use your browser and point to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="674df-194">Vous pouvez également utiliser Azure PowerShell pour administrer votre abonnement Azure et vos ressources à l’aide d’un script.</span><span class="sxs-lookup"><span data-stu-id="674df-194">You can also use Azure Powershell to administer your Azure subscription and resources via a script.</span></span>
<span data-ttu-id="674df-195">Vous pouvez exécuter Azure PowerShell à partir d'un raccourci sur le bureau ou dans le menu Démarrer intitulé « Microsoft Azure PowerShell ».</span><span class="sxs-lookup"><span data-stu-id="674df-195">You can run Azure Powershell from a shortcut on the desktop or from the start menu titled "Microsoft Azure Powershell".</span></span> <span data-ttu-id="674df-196">Reportez-vous à la [documentation Microsoft Azure PowerShell](../powershell-azure-resource-manager.md) pour plus d’informations sur l’administration de votre abonnement Azure et de vos ressources à l’aide de scripts Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="674df-196">Refer to [Microsoft Azure Powershell documentation](../powershell-azure-resource-manager.md) for more information on how you can administer your Azure subscription and resources using Windows Powershell scripts.</span></span>

## <a name="5-extend-your-storage-space-with-a-shared-file-system"></a><span data-ttu-id="674df-197">5. Augmenter votre espace de stockage avec un système de fichiers partagés</span><span class="sxs-lookup"><span data-stu-id="674df-197">5. Extend your storage space with a shared file system</span></span>
<span data-ttu-id="674df-198">Les scientifiques des données peuvent partager des jeux de données volumineux, du code ou d’autres ressources au sein de leur équipe.</span><span class="sxs-lookup"><span data-stu-id="674df-198">Data scientists can share large datasets, code or other resources within the team.</span></span> <span data-ttu-id="674df-199">La DSVM elle-même a environ 70 Go d'espace disponible.</span><span class="sxs-lookup"><span data-stu-id="674df-199">The DSVM itself has about 70GB of space available.</span></span> <span data-ttu-id="674df-200">Pour étendre votre espace de stockage, vous pouvez utiliser le service Azure File Service et l’installer sur la DSVM ou y accéder via l’API REST.</span><span class="sxs-lookup"><span data-stu-id="674df-200">To extend your storage, you can use the Azure File Service and either mount it on the DSVM or access it via a REST API.</span></span>   

> [!NOTE]
> <span data-ttu-id="674df-201">L'espace maximal du partage Azure File Service est de 5 To et la limite de taille par fichier est de 1 To.</span><span class="sxs-lookup"><span data-stu-id="674df-201">The maximum space of the Azure File Service share is 5TB and individual file size limit is 1TB.</span></span>   
> 
> 

<span data-ttu-id="674df-202">Vous pouvez utiliser Azure PowerShell pour créer un partage Azure File Service.</span><span class="sxs-lookup"><span data-stu-id="674df-202">You can use Azure Powershell to create an Azure File Service share.</span></span> <span data-ttu-id="674df-203">Voici le script à exécuter sous Azure PowerShell pour créer un partage Azure File Service.</span><span class="sxs-lookup"><span data-stu-id="674df-203">Here is the script to run under Azure PowerShell to create an Azure File service share.</span></span>

    # Authenticate to Azure.
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
    # Create a directory under the FIle share. You can give it any name
    New-AzureStorageDirectory -Share $s -Path <directory name>
    # List the share to confirm that everything worked
    Get-AzureStorageFile -Share $s


<span data-ttu-id="674df-204">Maintenant que vous avez créé un partage de fichiers Azure, vous pouvez l’installer sur n’importe quelle machine virtuelle d’Azure.</span><span class="sxs-lookup"><span data-stu-id="674df-204">Now that you have created an Azure file share, you can mount it in any virtual machine in Azure.</span></span> <span data-ttu-id="674df-205">Il est vivement recommandé que la machine virtuelle soit dans le même centre de données Azure que le compte de stockage pour éviter des frais de transfert de données et la latence.</span><span class="sxs-lookup"><span data-stu-id="674df-205">It is highly recommended that the VM is in same Azure data center as the storage account to avoid latency and data transfer charges.</span></span> <span data-ttu-id="674df-206">Voici les commandes pour installer le lecteur sur la DSVM que vous pouvez exécuter sur Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="674df-206">Here are the commands to mount the drive on the DSVM that you can run on Azure Powershell.</span></span>

    # Get storage key of the storage account that has the Azure file share from Azure portal. Store it securely on the VM to avoid prompted in next command.
    cmdkey /add:<<mydatadisk>>.file.core.windows.net /user:<<mydatadisk>> /pass:<storage key>

    # Mount the Azure file share as Z: drive on the VM. You can chose another drive letter if you wish
    net use z:  \\<mydatadisk>.file.core.windows.net\<<teamsharename>>


<span data-ttu-id="674df-207">Vous pouvez désormais accéder à ce lecteur comme à n’importe quel lecteur normal sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="674df-207">Now you can access this drive as you would any normal drive on the VM.</span></span>

## <a name="6-share-code-with-your-team-using-github"></a><span data-ttu-id="674df-208">6. Partager du code avec votre équipe à l’aide de GitHub</span><span class="sxs-lookup"><span data-stu-id="674df-208">6. Share code with your team using GitHub</span></span>
<span data-ttu-id="674df-209">GitHub est un référentiel de code dans lequel vous trouverez beaucoup d’exemples de code et de sources de différents outils utilisant diverses technologies et partagés par la communauté des développeurs.</span><span class="sxs-lookup"><span data-stu-id="674df-209">GitHub is a code repository where you can find a lot of sample code and sources for different tools using various technologies shared by the developer community.</span></span> <span data-ttu-id="674df-210">Il utilise la technologie Git pour suivre et stocker les versions des fichiers de code.</span><span class="sxs-lookup"><span data-stu-id="674df-210">It uses Git as the technology to track and store versions of the code files.</span></span> <span data-ttu-id="674df-211">GitHub est également une plateforme qui vous permet de créer votre propre référentiel pour stocker le code et la documentation partagés de votre équipe, d’implémenter le contrôle de version et de contrôler les accès pour afficher le code et y contribuer.</span><span class="sxs-lookup"><span data-stu-id="674df-211">GitHub is also a platform where you can create your own repository to store your team's shared code and documentation, implement version control and also control who have access to view and contribute code.</span></span> <span data-ttu-id="674df-212">Visitez les [pages d’aide GitHub](https://help.github.com/) pour plus d’informations sur l’utilisation de Git.</span><span class="sxs-lookup"><span data-stu-id="674df-212">Please visit the [GitHub help pages](https://help.github.com/) for more information on using Git.</span></span> <span data-ttu-id="674df-213">Vous pouvez utiliser GitHub pour collaborer avec votre équipe, utiliser le code développé par la communauté et apporter une contribution au code pour la communauté.</span><span class="sxs-lookup"><span data-stu-id="674df-213">You can use GitHub as one of the ways to collaborate with your team, use code developed by the community and contribute code back to the community.</span></span>

<span data-ttu-id="674df-214">La DSVM est déjà livrée avec des outils clients en ligne de commande et avec une interface graphique utilisateur pour accéder au dépôt GitHub.</span><span class="sxs-lookup"><span data-stu-id="674df-214">The DSVM already comes loaded with client tools on both command-line as well GUI to access GitHub repository.</span></span> <span data-ttu-id="674df-215">L’outil de ligne de commande pour utiliser Git et GitHub est appelé Git Bash.</span><span class="sxs-lookup"><span data-stu-id="674df-215">The command-line tool to work with Git and GitHub is called Git Bash.</span></span> <span data-ttu-id="674df-216">La version de Visual Studio installée sur la DSVM comprend les extensions Git.</span><span class="sxs-lookup"><span data-stu-id="674df-216">Visual Studio installed on the DSVM has the Git extensions.</span></span> <span data-ttu-id="674df-217">Vous pouvez trouver les icônes de démarrage de ces outils dans le menu Démarrer et sur le bureau.</span><span class="sxs-lookup"><span data-stu-id="674df-217">You can find start-up icons for these tools on the start menu and the desktop.</span></span>

<span data-ttu-id="674df-218">Pour télécharger du code à partir d’un dépôt GitHub, utilisez la commande ```git clone```.</span><span class="sxs-lookup"><span data-stu-id="674df-218">To download code from a GitHub repository you use the ```git clone``` command.</span></span> <span data-ttu-id="674df-219">Par exemple, pour télécharger le dépôt de science des données publié par Microsoft dans le répertoire actif, vous pouvez exécuter la commande suivante une fois dans ```git-bash```.</span><span class="sxs-lookup"><span data-stu-id="674df-219">For example to download data science repository published by Microsoft into the current directory you can run the following command once you are in ```git-bash```.</span></span>

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

<span data-ttu-id="674df-220">Dans Visual Studio, vous pouvez effectuer la même opération de clonage.</span><span class="sxs-lookup"><span data-stu-id="674df-220">In Visual Studio, you can do the same clone operation.</span></span> <span data-ttu-id="674df-221">La capture d’écran suivante indique comment accéder aux outils Git et GitHub dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="674df-221">The  following screen-shot shows how to access Git and GitHub tools in Visual Studio.</span></span>

![Git dans Visual Studio](./media/machine-learning-data-science-vm-do-ten-things/VSGit.PNG)

<span data-ttu-id="674df-223">Vous trouverez plus d’informations sur l’utilisation de Git pour travailler avec votre dépôt GitHub dans plusieurs ressources disponibles sur github.com. L’ [aide-mémoire](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf) constitue une référence utile.</span><span class="sxs-lookup"><span data-stu-id="674df-223">You can find more information on using Git to work with your GitHub repository from several resources available on github.com. The [cheat sheet](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf) is a useful reference.</span></span>

## <a name="7-access-various-azure-data-and-analytics-services"></a><span data-ttu-id="674df-224">7. Accéder à divers services de données et d'analyse Azure</span><span class="sxs-lookup"><span data-stu-id="674df-224">7. Access various Azure data and analytics services</span></span>
### <a name="azure-blob"></a><span data-ttu-id="674df-225">Objets blob Azure</span><span class="sxs-lookup"><span data-stu-id="674df-225">Azure Blob</span></span>
<span data-ttu-id="674df-226">Les objets blob Azure constituent un stockage fiable et économique dans le cloud pour tous les types de données.</span><span class="sxs-lookup"><span data-stu-id="674df-226">Azure blob is a reliable, economical cloud storage for data big and small.</span></span> <span data-ttu-id="674df-227">Étudions comment vous pouvez procéder pour déplacer des données d’objets blob Azure et accéder aux données stockées dans un objet blob Azure.</span><span class="sxs-lookup"><span data-stu-id="674df-227">Let us look at how you can move data to Azure Blob and access data stored in an Azure Blob.</span></span>

<span data-ttu-id="674df-228">**Configuration requise**</span><span class="sxs-lookup"><span data-stu-id="674df-228">**Prerequisite**</span></span>

* <span data-ttu-id="674df-229">**Créez votre compte de stockage d’objets blob Azure sur le [Portail Azure](https://portal.azure.com).**</span><span class="sxs-lookup"><span data-stu-id="674df-229">**Create your Azure Blob storage account from [Azure portal](https://portal.azure.com).**</span></span>

![Create_Azure_Blob](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* <span data-ttu-id="674df-231">Vérifiez que l’outil de ligne de commande AzCopy préinstallé se trouve ici : ```C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy.exe```.</span><span class="sxs-lookup"><span data-stu-id="674df-231">Confirm that the pre-installed command-line AzCopy tool is found at ```C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy.exe```.</span></span> <span data-ttu-id="674df-232">Vous pouvez ajouter le répertoire contenant le fichier azcopy.exe à votre variable d’environnement PATH pour éviter d’avoir à saisir tout le chemin d’accès à la commande lors de l’exécution de cet outil.</span><span class="sxs-lookup"><span data-stu-id="674df-232">You can add the directory containing the azcopy.exe to your PATH environment variable to avoid typing the full command path when running this tool.</span></span> <span data-ttu-id="674df-233">Pour plus d’informations sur l’outil AzCopy, consultez la [documentation AzCopy](../storage/common/storage-use-azcopy.md)</span><span class="sxs-lookup"><span data-stu-id="674df-233">For more info on AzCopy tool please refer to [AzCopy documentation](../storage/common/storage-use-azcopy.md)</span></span>
* <span data-ttu-id="674df-234">Lancez l’outil Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="674df-234">Start the Azure Storage Explorer tool.</span></span> <span data-ttu-id="674df-235">Vous pouvez le télécharger sur le site [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="674df-235">It can be downloaded from [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span> 

![AzureStorageExplorer_v4](./media/machine-learning-data-science-vm-do-ten-things/AzureStorageExplorer_v4.png)

<span data-ttu-id="674df-237">**Déplacer des données de la machine virtuelle vers Azure Blob : AzCopy**</span><span class="sxs-lookup"><span data-stu-id="674df-237">**Move data from VM to Azure Blob: AzCopy**</span></span>

<span data-ttu-id="674df-238">Pour déplacer des données entre vos fichiers locaux et le stockage d’objets blob, vous pouvez utiliser AzCopy en ligne de commande ou PowerShell :</span><span class="sxs-lookup"><span data-stu-id="674df-238">To move data between your local files and blob storage, you can use AzCopy in command-line or PowerShell:</span></span>

    AzCopy /Source:C:\myfolder /Dest:https://<mystorageaccount>.blob.core.windows.net/<mycontainer> /DestKey:<storage account key> /Pattern:abc.txt

<span data-ttu-id="674df-239">Remplacez **C:\myfolder** par le chemin d’accès où se trouve votre fichier, **mystorageaccount** par le nom de votre compte de stockage blob, **mycontainer** par le nom du conteneur et **storage account key** par votre clé d’accès de stockage blob.</span><span class="sxs-lookup"><span data-stu-id="674df-239">Replace **C:\myfolder** to the path where your file is stored, **mystorageaccount** to your blob storage account name, **mycontainer** to the container name, **storage account key** to your blob storage access key.</span></span> <span data-ttu-id="674df-240">Vous trouverez les informations d’identification de votre compte de stockage sur le [Portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="674df-240">You can find your storage account credentials in [Azure portal](https://portal.azure.com).</span></span>

![StorageAccountCredential_v2](./media/machine-learning-data-science-vm-do-ten-things/StorageAccountCredential_v2.png)

<span data-ttu-id="674df-242">Exécutez la commande AzCopy dans PowerShell ou à partir d’une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="674df-242">Run AzCopy command in PowerShell or from a command prompt.</span></span> <span data-ttu-id="674df-243">Voici un exemple d'utilisation de la commande AzCopy :</span><span class="sxs-lookup"><span data-stu-id="674df-243">Here is some example usage of AzCopy command:</span></span>

    # Copy *.sql from local machine to a Azure Blob
    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:"c:\Aaqs\Data Science Scripts" /Dest:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /DestKey:[ENTER STORAGE KEY] /S /Pattern:*.sql

    # Copy back all files from Azure Blob container to Local machine

    "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Dest:"c:\Aaqs\Data Science Scripts\temp" /Source:https://[ENTER STORAGE ACCOUNT].blob.core.windows.net/[ENTER CONTAINER] /SourceKey:[ENTER STORAGE KEY] /S



<span data-ttu-id="674df-244">Une fois que vous avez exécuté la commande AzCopy pour copier vers un objet blob Azure, votre fichier s'affiche dans Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="674df-244">Once you run your AzCopy command to copy to an Azure blob you see your file shows up in Azure Storage Explorer shortly.</span></span>

![AzCopy_run_finshed_Storage_Explorer_v3](./media/machine-learning-data-science-vm-do-ten-things/AzCopy_run_finshed_Storage_Explorer_v3.png)

<span data-ttu-id="674df-246">**Déplacer des données de la machine virtuelle vers Azure Blob : Azure Storage Explorer**</span><span class="sxs-lookup"><span data-stu-id="674df-246">**Move data from VM to Azure Blob: Azure Storage Explorer**</span></span>

<span data-ttu-id="674df-247">Vous pouvez également télécharger des données du fichier local vers votre machine virtuelle à l'aide d'Azure Storage Explorer :</span><span class="sxs-lookup"><span data-stu-id="674df-247">You can also upload data from the local file in your VM using Azure Storage Explorer:</span></span>

* <span data-ttu-id="674df-248">Pour charger des données dans un conteneur, sélectionnez le conteneur cible, puis cliquez sur le bouton **Charger**.![Charger dans l'Explorateur de stockage](./media/machine-learning-data-science-vm-do-ten-things/storage-accounts.png)</span><span class="sxs-lookup"><span data-stu-id="674df-248">To upload data to a container, select the target container and click the **Upload** button.![Upload in Storage Explorer](./media/machine-learning-data-science-vm-do-ten-things/storage-accounts.png)</span></span>
* <span data-ttu-id="674df-249">Cliquez sur **...** à droite de la zone **Fichiers**, sélectionnez un ou plusieurs fichiers à charger à partir du système de fichiers, puis cliquez sur **Charger** pour lancer le chargement des fichiers.![Charger les fichiers dans le blob](./media/machine-learning-data-science-vm-do-ten-things/upload-files-to-blob.png)</span><span class="sxs-lookup"><span data-stu-id="674df-249">Click on the **...** to the right of the **Files** box, select one or multiple files to upload from the file system and click **Upload** to begin uploading the files.![Upload files to blob](./media/machine-learning-data-science-vm-do-ten-things/upload-files-to-blob.png)</span></span>

<span data-ttu-id="674df-250">**Lire des données à partir d'Azure Blob : module lecteur Machine Learning**</span><span class="sxs-lookup"><span data-stu-id="674df-250">**Read data from Azure Blob: Machine Learning reader module**</span></span>

<span data-ttu-id="674df-251">Dans Azure Machine Learning Studio, vous pouvez utiliser un **module Importer les données** pour lire des données à partir de votre objet blob.</span><span class="sxs-lookup"><span data-stu-id="674df-251">In Azure Machine Learning Studio you can use an **Import Data module** to read data from your blob.</span></span>

![AML_ReaderBlob_Module_v3](./media/machine-learning-data-science-vm-do-ten-things/AML_ReaderBlob_Module_v3.png)

<span data-ttu-id="674df-253">**Lire des données à partir d'Azure Blob : Python ODBC**</span><span class="sxs-lookup"><span data-stu-id="674df-253">**Read data from Azure Blob: Python ODBC**</span></span>

<span data-ttu-id="674df-254">Vous pouvez utiliser la bibliothèque **BlobService** pour lire les données directement à partir de l’objet blob dans un Notebook Jupyter ou un programme Python.</span><span class="sxs-lookup"><span data-stu-id="674df-254">You can use **BlobService** library to read data directly from blob in a Jupyter Notebook or Python program.</span></span>

<span data-ttu-id="674df-255">Commencez par importer les packages requis :</span><span class="sxs-lookup"><span data-stu-id="674df-255">First, import required packages:</span></span>

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

<span data-ttu-id="674df-256">Puis entrez les informations d'identification de votre compte d'objets blob Azure et lisez les données de l'objet Blob :</span><span class="sxs-lookup"><span data-stu-id="674df-256">Then plug in your Azure Blob account credentials and read data from Blob:</span></span>

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
    print(("It takes %s seconds to download "+BLOBNAME) % (t2 - t1))

    #unzipping downloaded files if needed
    #with zipfile.ZipFile(ZIPPEDLOCALFILE, "r") as z:
    #    z.extractall(LOCALDIRECTORY)

    df1 = pd.read_csv(LOCALFILE, header=0)
    df1.columns = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime','passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude']
    print 'the size of the data is: %d rows and  %d columns' % df1.shape

<span data-ttu-id="674df-257">Les données sont lues comme une trame de données :</span><span class="sxs-lookup"><span data-stu-id="674df-257">The data is read in as a data frame:</span></span>

![IPNB_data_readin](./media/machine-learning-data-science-vm-do-ten-things/IPNB_data_readin.PNG)

### <a name="azure-data-lake"></a><span data-ttu-id="674df-259">Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="674df-259">Azure Data Lake</span></span>
<span data-ttu-id="674df-260">Azure Data Lake Storage est un référentiel hyperscale pour les charges de travail d’analyse des Big Data, compatible avec le système de fichiers HDFS (Hadoop Distributed File System).</span><span class="sxs-lookup"><span data-stu-id="674df-260">Azure Data Lake Storage is a hyper-scale repository for big data analytics workloads and compatible with Hadoop Distributed File System (HDFS).</span></span> <span data-ttu-id="674df-261">Il fonctionne avec l’écosystème Hadoop et avec Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="674df-261">It works with both the Hadoop ecosystem and the Azure Data Lake Analytics.</span></span> <span data-ttu-id="674df-262">Nous vous montrons comment déplacer les données dans le magasin d’Azure Data Lake et exécuter l’analyse à l’aide d’Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="674df-262">We show how you can move data into the Azure Data Lake Store and run analytics using Azure Data Lake Analytics.</span></span>

<span data-ttu-id="674df-263">**Configuration requise**</span><span class="sxs-lookup"><span data-stu-id="674df-263">**Prerequisite**</span></span>

* <span data-ttu-id="674df-264">Créez votre Azure Data Lake Analytics dans le [Portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="674df-264">Create your Azure Data Lake Analytics in [Azure portal](https://portal.azure.com).</span></span>

![Azure_Data_Lake_Create_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_Create_v2.png)

* <span data-ttu-id="674df-266">Les **outils Azure Data Lake** dans **Visual Studio** disponibles sur ce [lien](https://www.microsoft.com/download/details.aspx?id=49504) sont déjà installés dans Visual Studio Community Edition sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="674df-266">The  **Azure Data Lake Tools** in **Visual Studio** found at this  [link](https://www.microsoft.com/download/details.aspx?id=49504) is already installed on the Visual Studio Community Edition which is on the virtual machine.</span></span> <span data-ttu-id="674df-267">Après avoir lancé Visual Studio et vous être connecté à votre abonnement Azure, vous devriez voir votre compte et votre stockage Azure Data Analytics dans le volet gauche de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="674df-267">After starting Visual Studio and logging in your Azure subscription, you should see your Azure Data Analytics account and storage in the left panel of Visual Studio.</span></span>

![Azure_Data_Lake_PlugIn_v2](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_PlugIn_v2.PNG)

<span data-ttu-id="674df-269">**Déplacer des données de la machine virtuelle vers Data Lake : Azure Data Lake Explorer**</span><span class="sxs-lookup"><span data-stu-id="674df-269">**Move data from VM to Data Lake: Azure Data Lake Explorer**</span></span>

<span data-ttu-id="674df-270">Vous pouvez utiliser **Azure Data Lake Explorer** pour charger des données à partir des fichiers locaux de votre machine virtuelle vers Data Lake Storage.</span><span class="sxs-lookup"><span data-stu-id="674df-270">You can use **Azure Data Lake Explorer** to upload data from the local files in your Virtual Machine to Data Lake storage.</span></span>

![Azure_Data_Lake_UploadData](./media/machine-learning-data-science-vm-do-ten-things/Azure_Data_Lake_UploadData.PNG)

<span data-ttu-id="674df-272">Vous pouvez également créer un pipeline de données pour déplacer les données vers ou à partir d’Azure Data Lake à l’aide [d’Azure Data Factory (ADF)](https://azure.microsoft.com/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="674df-272">You can also build a data pipeline to productionize your data movement to or from Azure Data Lake using the [Azure Data Factory(ADF)](https://azure.microsoft.com/services/data-factory/).</span></span> <span data-ttu-id="674df-273">Nous vous renvoyons à cet [article](https://azure.microsoft.com/blog/creating-big-data-pipelines-using-azure-data-lake-and-azure-data-factory/) pour vous guider à travers les étapes de création des pipelines de données.</span><span class="sxs-lookup"><span data-stu-id="674df-273">We refer you to this [article](https://azure.microsoft.com/blog/creating-big-data-pipelines-using-azure-data-lake-and-azure-data-factory/) to guide you through the steps to build the data pipelines.</span></span>

<span data-ttu-id="674df-274">**Lire des données à partir d'Azure Blob vers Data Lake : U-SQL**</span><span class="sxs-lookup"><span data-stu-id="674df-274">**Read data from Azure Blob to Data Lake: U-SQL**</span></span>

<span data-ttu-id="674df-275">Si vos données se trouvent dans Stockage Blob Azure, vous pouvez les lire directement à partir de l'objet blob de stockage Azure dans la requête SQL-U.</span><span class="sxs-lookup"><span data-stu-id="674df-275">If your data resides in Azure Blob storage, you can directly read data from Azure storage blob in U-SQL query.</span></span> <span data-ttu-id="674df-276">Avant de composer votre requête SQL-U, assurez-vous que votre compte de stockage d'objets blob soit lié à votre Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="674df-276">Before composing your U-SQL query, make sure your blob storage account is linked to your Azure Data Lake.</span></span> <span data-ttu-id="674df-277">Accédez au **portail Azure**, recherchez votre tableau de bord Azure Data Lake Analytics, cliquez sur **Ajouter une source de données**, sélectionnez le type de stockage **Azure Storage** et entrez votre nom et votre clé de compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="674df-277">Go to **Azure portal**, find your Azure Data Lake Analytics dashboard, click **Add Data Source**, select storage type to **Azure Storage** and plug in your Azure Storage Account Name and Key.</span></span> <span data-ttu-id="674df-278">Vous pouvez ensuite référencer les données stockées dans le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="674df-278">Then you are able to reference the data stored in the storage account.</span></span>

![Saisie d'un compte de stockage et d'une clé](./media/machine-learning-data-science-vm-do-ten-things/Link_Blob_to_ADLA_v2.PNG)

<span data-ttu-id="674df-280">Dans Visual Studio, vous pouvez lire les données à partir d’un stockage d’objets blob, effectuer certaines manipulations de données et extractions de paramètres et envoyer les données résultantes vers Azure Data Lake ou un stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="674df-280">In Visual Studio, you can read data from blob storage, do some data manipulation, feature engineering, and output the resulting data to either Azure Data Lake or Azure Blob Storage.</span></span> <span data-ttu-id="674df-281">Lorsque vous référencez les données Stockage Blob, utilisez **wasb://**. Lorsque vous référencez les données d’Azure Data Lake, utilisez **swbhdfs://**.</span><span class="sxs-lookup"><span data-stu-id="674df-281">When you reference the data in blob storage, use **wasb://**; when you reference the data in Azure Data Lake, use **swbhdfs://**</span></span>

![Trame de données](./media/machine-learning-data-science-vm-do-ten-things/USQL_Read_Blob_v2.PNG)

<span data-ttu-id="674df-283">Vous pouvez utiliser les requêtes U-SQL suivantes dans Visual Studio :</span><span class="sxs-lookup"><span data-stu-id="674df-283">You may use the following U-SQL queries in Visual Studio:</span></span>

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
    TO "swebhdfs://<Azure Data Lake Storage Account Name>.azuredatalakestore.net/<Folder Name>/<Output Data File Name>"
    USING Outputters.Csv();

    OUTPUT @b   
    TO "wasb://<Container name>@<Azure Blob Storage Account Name>.blob.core.windows.net/<Output Data File Name>"
    USING Outputters.Csv();



<span data-ttu-id="674df-284">Une fois votre requête envoyée au serveur, un diagramme indiquant l'état de votre travail s'affiche.</span><span class="sxs-lookup"><span data-stu-id="674df-284">After your query is submitted to the server, a diagram showing the status of your job is displayed.</span></span>

![Diagramme d’état du travail](./media/machine-learning-data-science-vm-do-ten-things/USQL_Job_Status.PNG)

<span data-ttu-id="674df-286">**Interroger des données dans Data Lake : U-SQL**</span><span class="sxs-lookup"><span data-stu-id="674df-286">**Query data in Data Lake: U-SQL**</span></span>

<span data-ttu-id="674df-287">Une fois le jeu de données réceptionné dans Azure Data Lake, vous pouvez utiliser le [langage U-SQL](../data-lake-analytics/data-lake-analytics-u-sql-get-started.md) pour interroger et explorer les données.</span><span class="sxs-lookup"><span data-stu-id="674df-287">After the dataset is ingested into Azure Data Lake, you can use [U-SQL language](../data-lake-analytics/data-lake-analytics-u-sql-get-started.md) to query and explore the data.</span></span> <span data-ttu-id="674df-288">Le langage U-SQL est similaire à T-SQL, mais combine certaines fonctionnalités de C# afin de permettre aux utilisateurs d'écrire des modules personnalisés, des fonctions définies par l'utilisateur, etc. Vous pouvez utiliser les scripts de l'étape précédente.</span><span class="sxs-lookup"><span data-stu-id="674df-288">U-SQL language is similar to T-SQL, but combines some features from C# so that users can write customized modules, user-defined functions, and etc. You can use the scripts in the previous step.</span></span>

<span data-ttu-id="674df-289">Une fois la requête envoyée au serveur, tripdata_summary.CSV est créé dans **Azure Data Lake Explorer**. Vous pouvez prévisualiser les données en cliquant avec le bouton droit sur le fichier.</span><span class="sxs-lookup"><span data-stu-id="674df-289">After the query is submitted to server, tripdata_summary.CSV can be found shortly in **Azure Data Lake Explorer**, you may preview the data by right-click the file.</span></span>

![Fichier dans Azure Data Lake Explorer](./media/machine-learning-data-science-vm-do-ten-things/USQL_create_summary.png)

<span data-ttu-id="674df-291">Pour afficher les informations du fichier :</span><span class="sxs-lookup"><span data-stu-id="674df-291">To see the file information:</span></span>

![Résumé du fichier](./media/machine-learning-data-science-vm-do-ten-things/USQL_tripdata_summary.png)

### <a name="hdinsight-hadoop-clusters"></a><span data-ttu-id="674df-293">Clusters HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="674df-293">HDInsight Hadoop Clusters</span></span>
<span data-ttu-id="674df-294">Azure HDInsight est un service Apache Hadoop, Spark, HBase et Storm géré dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="674df-294">Azure HDInsight is a managed Apache Hadoop, Spark, HBase, and Storm service on the cloud.</span></span> <span data-ttu-id="674df-295">Vous pouvez travailler facilement avec les clusters Azure HDInsight à partir de la machine virtuelle pour la science des données.</span><span class="sxs-lookup"><span data-stu-id="674df-295">You can work easily with Azure HDInsight clusters from the data science virtual machine.</span></span>

<span data-ttu-id="674df-296">**Configuration requise**</span><span class="sxs-lookup"><span data-stu-id="674df-296">**Prerequisite**</span></span>

* <span data-ttu-id="674df-297">Créez votre compte de stockage d’objets blob Azure sur le [Portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="674df-297">Create your Azure Blob storage account from [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="674df-298">Ce compte de stockage est utilisé pour stocker les données des clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="674df-298">This storage account is used to store data for HDInsight clusters.</span></span>

![Créer un compte de stockage d’objets blob Azure](./media/machine-learning-data-science-vm-do-ten-things/Create_Azure_Blob.PNG)

* <span data-ttu-id="674df-300">Personnalisez les clusters Hadoop Azure HDInsight sur le [Portail Azure](machine-learning-data-science-customize-hadoop-cluster.md)</span><span class="sxs-lookup"><span data-stu-id="674df-300">Customize Azure HDInsight Hadoop Clusters from [Azure portal](machine-learning-data-science-customize-hadoop-cluster.md)</span></span>
  
  * <span data-ttu-id="674df-301">Vous devez lier le compte de stockage créé à votre cluster HDInsight, une fois sa création terminée.</span><span class="sxs-lookup"><span data-stu-id="674df-301">You must link the storage account created with your HDInsight cluster when it is created.</span></span> <span data-ttu-id="674df-302">Ce compte de stockage est utilisé pour accéder aux données qui peuvent être traitées au sein du cluster.</span><span class="sxs-lookup"><span data-stu-id="674df-302">This storage account is used for accessing data that can be processed within the cluster.</span></span>

![Liaison d'un compte de stockage créé avec un cluster HDInsight](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_v4.PNG)

* <span data-ttu-id="674df-304">Vous devez activer **l’accès à distance** au nœud principal du cluster une fois celui-ci créé.</span><span class="sxs-lookup"><span data-stu-id="674df-304">You must enable **Remote Access** to the head node of the cluster after it is created.</span></span> <span data-ttu-id="674df-305">N’oubliez pas les informations d’identification de l’accès à distance que vous spécifiez ici (différentes de celles qui sont spécifiées pour le cluster lors de sa création) : elles sont nécessaires pour effectuer les procédures suivantes.</span><span class="sxs-lookup"><span data-stu-id="674df-305">Remember the remote access credentials you specify here (different from those specified for the cluster at its creation): you need them in the subsequent procedure.</span></span>

![Activer l'accès à distance](./media/machine-learning-data-science-vm-do-ten-things/Create_HDI_dashboard_v3.PNG)

* <span data-ttu-id="674df-307">Créez un espace de travail Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="674df-307">Create an Azure Machine Learning workspace.</span></span> <span data-ttu-id="674df-308">Vos expériences Machine Learning sont stockées dans cet espace de travail Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="674df-308">Your Machine Learning Experiments are stored in this Machine Learning workspace.</span></span> <span data-ttu-id="674df-309">Sélectionnez les options en surbrillance sur le portail, comme indiqué dans la capture d’écran suivante :</span><span class="sxs-lookup"><span data-stu-id="674df-309">Select the highlighted options in Portal as shown in the following screenshot:</span></span>

![Création d’un espace de travail Microsoft Azure Machine Learning](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space.PNG)

* <span data-ttu-id="674df-311">Entrez ensuite les paramètres pour votre espace de travail</span><span class="sxs-lookup"><span data-stu-id="674df-311">Then enter the parameters for your workspace</span></span>

![Entrer les paramètres de l'espace de travail Machine Learning](./media/machine-learning-data-science-vm-do-ten-things/Create_ML_Space_step2_v2.PNG)

* <span data-ttu-id="674df-313">Téléchargez des données à l’aide d’IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="674df-313">Upload data using IPython Notebook.</span></span> <span data-ttu-id="674df-314">Importez d’abord les packages requis, saisissez vos informations d’identification, créez une base de données dans votre compte de stockage, puis chargez les données dans les clusters HDI.</span><span class="sxs-lookup"><span data-stu-id="674df-314">First import required packages, plug in credentials, create a db in your storage account, then load data to HDI clusters.</span></span>

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


        #Create the connection to Hive using ODBC
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


        #Upload data from blob storage to HDI cluster
        for i in range(1,13):
            queryString = "LOAD DATA INPATH 'wasb:///nyctaxitripraw2/trip_data_%d.csv' INTO TABLE nyctaxidb2.trip PARTITION (month=%d);"%(i,i)
            cursor.execute(queryString)
            queryString = "LOAD DATA INPATH 'wasb:///nyctaxifareraw2/trip_fare_%d.csv' INTO TABLE nyctaxidb2.fare PARTITION (month=%d);"%(i,i)  
            cursor.execute(queryString)


* <span data-ttu-id="674df-315">Vous pouvez également suivre cette [procédure pas à pas](machine-learning-data-science-process-hive-walkthrough.md) pour charger les données NYC Taxi vers le cluster HDI.</span><span class="sxs-lookup"><span data-stu-id="674df-315">Alternately,  you can follow this [walkthrough](machine-learning-data-science-process-hive-walkthrough.md) to upload NYC Taxi data to HDI cluster.</span></span> <span data-ttu-id="674df-316">Voici les grandes étapes :</span><span class="sxs-lookup"><span data-stu-id="674df-316">Major steps include:</span></span>
  
  * <span data-ttu-id="674df-317">AzCopy : téléchargez les CSV compressés de l'objet blob public vers votre dossier local</span><span class="sxs-lookup"><span data-stu-id="674df-317">AzCopy: download zipped CSV's from public blob to your local folder</span></span>
  * <span data-ttu-id="674df-318">AzCopy : téléchargez les CSV décompressés de votre dossier local vers le cluster HDI</span><span class="sxs-lookup"><span data-stu-id="674df-318">AzCopy: upload unzipped CSV's from local folder to HDI cluster</span></span>
  * <span data-ttu-id="674df-319">Connectez-vous au nœud principal du cluster Hadoop et préparez une analyse exploratoire des données</span><span class="sxs-lookup"><span data-stu-id="674df-319">Log into the head node of Hadoop cluster and prepare for exploratory data analysis</span></span>

<span data-ttu-id="674df-320">Une fois les données chargées dans le cluster HDI, vous pouvez les vérifier dans Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="674df-320">After the data is loaded to HDI cluster, you can check your data in Azure Storage Explorer.</span></span> <span data-ttu-id="674df-321">Et vous disposez d'une base de données nyctaxidb créée dans le cluster HDI.</span><span class="sxs-lookup"><span data-stu-id="674df-321">And you have a database nyctaxidb created in HDI cluster.</span></span>

<span data-ttu-id="674df-322">**Exploration des données : requêtes Hive dans Python**</span><span class="sxs-lookup"><span data-stu-id="674df-322">**Data exploration: Hive Queries in Python**</span></span>

<span data-ttu-id="674df-323">Les données se trouvant dans le cluster Hadoop, vous pouvez utiliser le package pyodbc pour vous connecter aux clusters Hadoop et envoyer des requêtes à la base de données avec Hive pour l’exploration et l’extraction de paramètres.</span><span class="sxs-lookup"><span data-stu-id="674df-323">Since the data is in Hadoop cluster, you can use the pyodbc package to connect to Hadoop Clusters and query database using Hive to do exploration and feature engineering.</span></span> <span data-ttu-id="674df-324">Vous pouvez afficher les tables existantes que nous avons créées à l'étape des conditions préalables.</span><span class="sxs-lookup"><span data-stu-id="674df-324">You can view the existing tables we created in the prerequisite step.</span></span>

    queryString = """
        show tables in nyctaxidb2;
        """
    pd.read_sql(queryString,connection)


![Afficher les tables existantes](./media/machine-learning-data-science-vm-do-ten-things/Python_View_Existing_Tables_Hive_v3.PNG)

<span data-ttu-id="674df-326">Nous allons examiner le nombre d'enregistrements chaque mois et la fréquence des pourboires dans la table de trajet :</span><span class="sxs-lookup"><span data-stu-id="674df-326">Let's look at the number of records in each month and the frequencies of tipped or not in the trip table:</span></span>

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

<span data-ttu-id="674df-329">Nous pouvons également calculer la distance entre les lieux de départ et d'arrivée, puis les comparer à la distance de la course.</span><span class="sxs-lookup"><span data-stu-id="674df-329">We can also compute the distance between pickup location and dropoff location and then compare it to the trip distance.</span></span>

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


![Traçage de la distance des départs/arrivées à la distance des trajets](./media/machine-learning-data-science-vm-do-ten-things/Exploration_direct_distance_trip_distance_v2.PNG)

<span data-ttu-id="674df-332">Nous allons maintenant préparer le jeu de données sous-échantillonné (1 %) pour la modélisation.</span><span class="sxs-lookup"><span data-stu-id="674df-332">Now let's prepare a down-sampled (1%) set of data for modeling.</span></span> <span data-ttu-id="674df-333">Nous pouvons utiliser ces données dans le module lecteur Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="674df-333">We can use this data in Machine Learning reader module.</span></span>

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

        --- now insert contents of the join into the preceding internal table

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

<span data-ttu-id="674df-334">Après un certain temps, vous pouvez voir que les données ont été chargées dans les clusters Hadoop :</span><span class="sxs-lookup"><span data-stu-id="674df-334">After a while, you can see the data has been loaded in Hadoop clusters:</span></span>

    queryString = """
        select * from nyctaxi_downsampled_dataset limit 10;
        """
    cursor.execute(queryString)
    pd.read_sql(queryString,connection)


![Table de données](./media/machine-learning-data-science-vm-do-ten-things/DownSample_Data_For_Modeling_v2.PNG)

<span data-ttu-id="674df-336">**Lire des données à partir de HDI en utilisant le module lecteur Machine Learning**</span><span class="sxs-lookup"><span data-stu-id="674df-336">**Read data from HDI using Machine Learning: reader module**</span></span>

<span data-ttu-id="674df-337">Vous pouvez également utiliser le module **lecteur** Machine Learning Studio pour accéder à la base de données dans le cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="674df-337">You may also use the **reader** module in Machine Learning Studio to access the database in Hadoop cluster.</span></span> <span data-ttu-id="674df-338">Entrez les informations d'identification de votre compte Azure Storage et de vos clusters HDI pour pouvoir générer des modèles d'apprentissage automatique à l'aide de la base de données des clusters HDI.</span><span class="sxs-lookup"><span data-stu-id="674df-338">Plug in the credentials of your HDI clusters and Azure Storage Account to enable build ing machine learning models using database in HDI clusters.</span></span>

![Propriétés du module lecteur](./media/machine-learning-data-science-vm-do-ten-things/AML_Reader_Hive.PNG)

<span data-ttu-id="674df-340">Le jeu de données évalué peut ensuite être affiché :</span><span class="sxs-lookup"><span data-stu-id="674df-340">The scored dataset can then be viewed:</span></span>

![Affichage du jeu de données évalué](./media/machine-learning-data-science-vm-do-ten-things/AML_Model_Results.PNG)

### <a name="azure-sql-data-warehouse--databases"></a><span data-ttu-id="674df-342">Azure SQL Data Warehouse et bases de données</span><span class="sxs-lookup"><span data-stu-id="674df-342">Azure SQL Data Warehouse & databases</span></span>
<span data-ttu-id="674df-343">Azure SQL Data Warehouse est un entrepôt de données élastique en tant que service offrant une expérience SQL Server professionnelle.</span><span class="sxs-lookup"><span data-stu-id="674df-343">Azure SQL Data Warehouse is an elastic data warehouse as a service with enterprise-class SQL Server experience.</span></span>

<span data-ttu-id="674df-344">Vous pouvez approvisionner votre Azure SQL Data Warehouse en suivant les instructions fournies dans cet [article](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md).</span><span class="sxs-lookup"><span data-stu-id="674df-344">You can provision your Azure SQL Data Warehouse by following the instructions provided in this [article](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md).</span></span> <span data-ttu-id="674df-345">Une fois votre Azure SQL Data Warehouse approvisionné, vous pouvez utiliser cette [procédure pas à pas](machine-learning-data-science-process-sqldw-walkthrough.md) pour le chargement de données, mais aussi pour l’exploration et la modélisation à l’aide de données dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="674df-345">Once you provision your Azure SQL Data Warehouse, you can use this [walkthrough](machine-learning-data-science-process-sqldw-walkthrough.md) to do data upload, exploration and modeling using data within the SQL Data Warehouse.</span></span>

#### <a name="azure-cosmos-db"></a><span data-ttu-id="674df-346">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="674df-346">Azure Cosmos DB</span></span>
<span data-ttu-id="674df-347">Azure Cosmos DB est une base de données NoSQL sur le cloud.</span><span class="sxs-lookup"><span data-stu-id="674df-347">Azure Cosmos DB is a NoSQL database in the cloud.</span></span> <span data-ttu-id="674df-348">Elle vous permet de travailler avec des documents comme JSON, de les stocker et de les interroger.</span><span class="sxs-lookup"><span data-stu-id="674df-348">It allows you to work with documents like JSON and allows you to store and query the documents.</span></span>

<span data-ttu-id="674df-349">Vous devez suivre les étapes préalables suivantes pour accéder à Azure Cosmos DB à partir de la DSVM.</span><span class="sxs-lookup"><span data-stu-id="674df-349">You need to do the following per-requisites steps to access Azure Cosmos DB from the DSVM.</span></span>

1. <span data-ttu-id="674df-350">Installez le Kit de développement logiciel (SDK) Python DocumentDB (exécutez ```pip install pydocumentdb``` à partir de l’invite de commandes)</span><span class="sxs-lookup"><span data-stu-id="674df-350">Install DocumentDB Python SDK (Run ```pip install pydocumentdb``` from command prompt)</span></span>
2. <span data-ttu-id="674df-351">Créez un compte Azure Cosmos DB et une base de données à partir du [portail Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="674df-351">Create an Azure Cosmos DB account and a database from [Azure portal](https://portal.azure.com)</span></span>
3. <span data-ttu-id="674df-352">Téléchargez [ici](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d) « l’outil de migration Azure Cosmos DB » et extrayez-le dans le répertoire de votre choix</span><span class="sxs-lookup"><span data-stu-id="674df-352">Download "Azure Cosmos DB Migration Tool" from [here](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d) and extract to a directory of your choice</span></span>
4. <span data-ttu-id="674df-353">Importez les données JSON (données sur le volcan) stockées sur un [objet blob public](https://cahandson.blob.core.windows.net/samples/volcano.json) dans Cosmos DB avec les paramètres de commande suivants pour l’outil de migration (dtui.exe à partir du répertoire où vous avez installé l’outil de migration Cosmos DB).</span><span class="sxs-lookup"><span data-stu-id="674df-353">Import JSON data (volcano data) stored on a [public blob](https://cahandson.blob.core.windows.net/samples/volcano.json) into Cosmos DB with following command parameters to the migration tool (dtui.exe from the directory where you installed the Cosmos DB Migration Tool).</span></span> <span data-ttu-id="674df-354">Entrez les paramètres d'emplacement source et cible suivant :</span><span class="sxs-lookup"><span data-stu-id="674df-354">Enter the source and target location with these parameters:</span></span>
   
    <span data-ttu-id="674df-355">/s:JsonFile /s.Files:https://cahandson.blob.core.windows.net/samples/volcano.json /t:DocumentDBBulk /t.ConnectionString:AccountEndpoint=https://[DocDBAccountName].documents.azure.com:443/;AccountKey=[[KEY];Database=volcano /t.Collection:volcano1</span><span class="sxs-lookup"><span data-stu-id="674df-355">/s:JsonFile /s.Files:https://cahandson.blob.core.windows.net/samples/volcano.json /t:DocumentDBBulk /t.ConnectionString:AccountEndpoint=https://[DocDBAccountName].documents.azure.com:443/;AccountKey=[[KEY];Database=volcano /t.Collection:volcano1</span></span>

<span data-ttu-id="674df-356">Une fois les données importées, vous pouvez accéder à Jupyter et ouvrir le Notebook intitulé *DocumentDBSample* qui contient le code Python pour accéder à DocumentDB et effectuer des requêtes de base.</span><span class="sxs-lookup"><span data-stu-id="674df-356">Once you import the data, you can go to Jupyter and open the notebook titled *DocumentDBSample* which contains python code to access DocumentDB and do some basic querying.</span></span> <span data-ttu-id="674df-357">Pour en savoir plus sur Cosmos DB, consultez la [page de documentation](https://docs.microsoft.com/azure/cosmos-db/) du service.</span><span class="sxs-lookup"><span data-stu-id="674df-357">You can learn more about Cosmos DB by visiting the service [documentation page](https://docs.microsoft.com/azure/cosmos-db/).</span></span>

## <a name="8-build-reports-and-dashboard-using-the-power-bi-desktop"></a><span data-ttu-id="674df-358">8. Générer des rapports et des tableaux de bord à l'aide de Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="674df-358">8. Build reports and dashboard using the Power BI Desktop</span></span>
<span data-ttu-id="674df-359">Nous allons visualiser le fichier Volcan JSON, que nous avons vu dans l’exemple Cosmos DB ci-dessus, dans Power BI afin d’obtenir un aperçu visuel des données.</span><span class="sxs-lookup"><span data-stu-id="674df-359">Let us visualize the Volcano JSON file that we saw in the preceding Cosmos DB example in Power BI to gain visual insights into the data.</span></span> <span data-ttu-id="674df-360">Les étapes détaillées sont présentées dans [l’article Power BI](../cosmos-db/powerbi-visualize.md).</span><span class="sxs-lookup"><span data-stu-id="674df-360">Detailed steps are available in the [Power BI article](../cosmos-db/powerbi-visualize.md).</span></span> <span data-ttu-id="674df-361">Les étapes principales sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="674df-361">Here are the high-level steps:</span></span>

1. <span data-ttu-id="674df-362">Ouvrez Power BI Desktop et cliquez sur « obtenir les données ».</span><span class="sxs-lookup"><span data-stu-id="674df-362">Open Power BI Desktop and do "Get Data".</span></span> <span data-ttu-id="674df-363">Spécifiez l’URL comme : https://cahandson.blob.core.windows.net/samples/volcano.json</span><span class="sxs-lookup"><span data-stu-id="674df-363">Specify the URL as: https://cahandson.blob.core.windows.net/samples/volcano.json</span></span>
2. <span data-ttu-id="674df-364">Vous devez voir les enregistrements JSON importés sous forme de liste</span><span class="sxs-lookup"><span data-stu-id="674df-364">You should see the JSON records imported as a list</span></span>
3. <span data-ttu-id="674df-365">Convertissez la liste en table afin que Power BI puisse l’utiliser</span><span class="sxs-lookup"><span data-stu-id="674df-365">Convert the list to a table so Power BI can work with the same</span></span>
4. <span data-ttu-id="674df-366">Développez les colonnes en cliquant sur l’icône Développer (celle avec l’icône « flèche gauche et flèche droite » à droite de la colonne)</span><span class="sxs-lookup"><span data-stu-id="674df-366">Expand the columns by clicking on the expand icon (the one with the "left arrow and a right arrow" icon on the right of the column)</span></span>
5. <span data-ttu-id="674df-367">Notez que cet emplacement est un champ « Enregistrement ».</span><span class="sxs-lookup"><span data-stu-id="674df-367">Notice that location is a "Record" field.</span></span> <span data-ttu-id="674df-368">Développez l'enregistrement et sélectionnez uniquement les coordonnées.</span><span class="sxs-lookup"><span data-stu-id="674df-368">Expand the record and select only the coordinates.</span></span> <span data-ttu-id="674df-369">Une coordonnée est une colonne de liste</span><span class="sxs-lookup"><span data-stu-id="674df-369">Coordinate is a list column</span></span>
6. <span data-ttu-id="674df-370">Ajoutez une nouvelle colonne pour convertir la colonne coordonnée de liste en une colonne LatLong séparée par des virgules et concaténant les deux éléments dans le champ de liste de coordonnées à l’aide de la formule ```Text.From([coordinates]{1})&","&Text.From([coordinates]{0})```.</span><span class="sxs-lookup"><span data-stu-id="674df-370">Add a new column to convert the list coordinate column into a comma separate LatLong column concatenating the two elements in the coordinate list field using the formula ```Text.From([coordinates]{1})&","&Text.From([coordinates]{0})```.</span></span>
7. <span data-ttu-id="674df-371">Enfin, convertissez la colonne ```Elevation``` en Decimal et sélectionnez **Fermer** et **Appliquer**.</span><span class="sxs-lookup"><span data-stu-id="674df-371">Finally convert the ```Elevation``` column to Decimal and select the **Close** and **Apply**.</span></span>

<span data-ttu-id="674df-372">À la place de la procédure précédente, vous pouvez coller le code suivant qui exécute ces étapes dans l'éditeur avancé de Power BI, qui vous permet d'écrire les transformations de données dans un langage de requête.</span><span class="sxs-lookup"><span data-stu-id="674df-372">Instead of preceding steps, you can paste the following code that scripts out the steps used in the Advanced Editor in Power BI that allows you to write the data transformations in a query language.</span></span>

    let
        Source = Json.Document(Web.Contents("https://cahandson.blob.core.windows.net/samples/volcano.json")),
        #"Converted to Table" = Table.FromList(Source, Splitter.SplitByNothing(), null, null, ExtraValues.Error),
        #"Expanded Column1" = Table.ExpandRecordColumn(#"Converted to Table", "Column1", {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}, {"Volcano Name", "Country", "Region", "Location", "Elevation", "Type", "Status", "Last Known Eruption", "id"}),
        #"Expanded Location" = Table.ExpandRecordColumn(#"Expanded Column1", "Location", {"coordinates"}, {"coordinates"}),
        #"Added Custom" = Table.AddColumn(#"Expanded Location", "LatLong", each Text.From([coordinates]{1})&","&Text.From([coordinates]{0})),
        #"Changed Type" = Table.TransformColumnTypes(#"Added Custom",{{"Elevation", type number}})
    in
        #"Changed Type"



<span data-ttu-id="674df-373">Vous disposez maintenant des données dans votre modèle de données Power BI.</span><span class="sxs-lookup"><span data-stu-id="674df-373">You now have the data in your Power BI data model.</span></span> <span data-ttu-id="674df-374">Votre Power BI Desktop doit apparaître comme suit :</span><span class="sxs-lookup"><span data-stu-id="674df-374">Your Power BI desktop should appear as follows:</span></span>

![Power BI Desktop](./media/machine-learning-data-science-vm-do-ten-things/PowerBIVolcanoData.png)

<span data-ttu-id="674df-376">Vous pouvez commencer à créer des rapports et des visualisations à l'aide du modèle de données.</span><span class="sxs-lookup"><span data-stu-id="674df-376">You can start building reports and visualizations using the data model.</span></span> <span data-ttu-id="674df-377">Vous pouvez suivre la procédure décrite dans cet [article Power BI](../cosmos-db/powerbi-visualize.md#build-the-reports) pour générer un rapport.</span><span class="sxs-lookup"><span data-stu-id="674df-377">You can follow the steps in this [Power BI article](../cosmos-db/powerbi-visualize.md#build-the-reports) to build a report.</span></span> <span data-ttu-id="674df-378">Le résultat final sera un rapport similaire à ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="674df-378">The end result is a report that looks like the following.</span></span>

![Power BI Desktop - Vue Rapport - Connecteur Power BI](./media/machine-learning-data-science-vm-do-ten-things/power_bi_connector_pbireportview2.png)

## <a name="9-dynamically-scale-your-dsvm-to-meet-your-project-needs"></a><span data-ttu-id="674df-380">9. Mettre à l'échelle dynamiquement votre DSVM pour répondre aux besoins de votre projet</span><span class="sxs-lookup"><span data-stu-id="674df-380">9. Dynamically scale your DSVM to meet your project needs</span></span>
<span data-ttu-id="674df-381">Vous pouvez mettre à l'échelle la DSVM pour répondre aux besoins de votre projet.</span><span class="sxs-lookup"><span data-stu-id="674df-381">You can scale up and down the DSVM to meet your project needs.</span></span> <span data-ttu-id="674df-382">Si vous n’avez pas besoin d’utiliser la machine virtuelle le soir ou le week-end, vous pouvez simplement arrêter la machine virtuelle à partir du [Portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="674df-382">If you don't need to use the VM in the evening or weekends, you can just shut down the VM from the [Azure portal](https://portal.azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="674df-383">Vous encourez des frais de calcul si vous utilisez simplement le bouton d’arrêt du système d’exploitation sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="674df-383">You incur compute charges if you use just the Operating system shutdown button on the VM.</span></span>  
> 
> 

<span data-ttu-id="674df-384">Si vous devez gérer une analyse à grande échelle et avez besoin de davantage de capacité de processeur, de mémoire et/ou de disque, vous trouverez un grand choix de tailles de machine virtuelle en termes de cœurs de processeur, de capacité de mémoire et de types de disques (y compris les disques SSD) qui répondent à vos besoins budgétaires et de calcul.</span><span class="sxs-lookup"><span data-stu-id="674df-384">If you need to handle some large-scale analysis and need more CPU and/or memory and/or disk capacity you can find a large choice of VM sizes in terms of CPU cores, memory capacity and disk types (including Solid state drives) that meet your compute and budgetary needs.</span></span> <span data-ttu-id="674df-385">La liste complète des machines virtuelles, ainsi que leur tarif horaire de calcul, sont disponibles sur la page [Tarification des machines virtuelles Azure](https://azure.microsoft.com/pricing/details/virtual-machines/) .</span><span class="sxs-lookup"><span data-stu-id="674df-385">The full list of VMs along with their hourly compute pricing is available on the [Azure Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/) page.</span></span>

<span data-ttu-id="674df-386">De même, si vos besoins en matière de capacité de traitement de la machine virtuelle diminuent (par exemple : vous avez déplacé une charge de travail importante vers un cluster Hadoop ou Spark), vous pouvez descendre en puissance le cluster à partir du [Portail Azure](https://portal.azure.com) en accédant aux paramètres de votre instance de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="674df-386">Similarly, if your need for VM processing capacity reduces (for example: you moved a major workload to a Hadoop or a Spark cluster), you can scale down the cluster from the [Azure portal](https://portal.azure.com) and going to the settings of your VM instance.</span></span> <span data-ttu-id="674df-387">Voici une capture d'écran.</span><span class="sxs-lookup"><span data-stu-id="674df-387">Here is a screenshot.</span></span>

![Paramètres de l'instance de machine virtuelle](./media/machine-learning-data-science-vm-do-ten-things/VMScaling.PNG)

## <a name="10-install-additional-tools-on-your-virtual-machine"></a><span data-ttu-id="674df-389">10. Installer des outils supplémentaires sur votre machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="674df-389">10. Install additional tools on your virtual machine</span></span>
<span data-ttu-id="674df-390">Nous avons empaqueté plusieurs outils dont nous pensons qu’ils seront en mesure de répondre à une grande partie des besoins d’analyse de données courants et de vous faire gagner du temps en évitant l’installation et la configuration de vos environnements un par un et de l’argent en ne payant que pour les ressources que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="674df-390">We have packaged several tools that we believe are able to address many of the common data analytics needs and that should save you time by avoiding having to install and configure your environments one by one and save you money by paying only for resources that you use.</span></span>

<span data-ttu-id="674df-391">Vous pouvez tirer parti des autres services de données et d’analyse Azure présentés dans cet article pour améliorer votre environnement d’analyse.</span><span class="sxs-lookup"><span data-stu-id="674df-391">You can leverage other Azure data and analytics services profiled in this article to enhance your analytics environment.</span></span> <span data-ttu-id="674df-392">Nous comprenons que, dans certains cas, vos besoins puissent nécessiter des outils supplémentaires, notamment des outils tiers propriétaires.</span><span class="sxs-lookup"><span data-stu-id="674df-392">We understand that in some cases your needs may require additional tools, including some proprietary third-party tools.</span></span> <span data-ttu-id="674df-393">Vous avez un accès administratif total à la machine virtuelle pour installer les nouveaux outils dont vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="674df-393">You have full administrative access on the virtual machine to install new tools you need.</span></span> <span data-ttu-id="674df-394">Vous pouvez également installer des packages supplémentaires non préinstallés en Python et R.</span><span class="sxs-lookup"><span data-stu-id="674df-394">You can also install additional packages in Python and R that are not pre-installed.</span></span> <span data-ttu-id="674df-395">Pour Python, vous pouvez utiliser soit ```conda```, soit ```pip```.</span><span class="sxs-lookup"><span data-stu-id="674df-395">For Python you can use either ```conda``` or ```pip```.</span></span> <span data-ttu-id="674df-396">Pour R, vous pouvez utiliser ```install.packages()``` dans la console R ou utiliser l’IDE et choisir « **Packages** -> **Installer les packages...** ».</span><span class="sxs-lookup"><span data-stu-id="674df-396">For R you can use the ```install.packages()``` in the R console or use the IDE and choose "**Packages** -> **Install Packages...**".</span></span>

## <a name="summary"></a><span data-ttu-id="674df-397">Résumé</span><span class="sxs-lookup"><span data-stu-id="674df-397">Summary</span></span>
<span data-ttu-id="674df-398">Ce sont quelques-unes des actions possibles sur la machine virtuelle pour la science des données Microsoft.</span><span class="sxs-lookup"><span data-stu-id="674df-398">These are just some of the things you can do on the Microsoft Data Science Virtual Machine.</span></span> <span data-ttu-id="674df-399">Il existe bien d'autres actions que vous pouvez effectuer pour en faire un environnement d'analyse efficace.</span><span class="sxs-lookup"><span data-stu-id="674df-399">There are many more things you can do to make it an effective analytics environment.</span></span>

