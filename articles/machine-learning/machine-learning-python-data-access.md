---
title: "jeux de données aaaAccess avec la bibliothèque cliente de Machine Learning Python | Documents Microsoft"
description: "Installer et utiliser hello tooaccess de bibliothèque cliente de Python et gérer les données d’Azure Machine Learning en toute sécurité à partir d’un environnement local de Python."
services: machine-learning
documentationcenter: python
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 9ab42272-c30c-4b7e-8e66-d64eafef22d0
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: huvalo;bradsev
ms.openlocfilehash: f55067118f13c52bf677930a20836ce6989f8187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="access-datasets-with-python-using-hello-azure-machine-learning-python-client-library"></a><span data-ttu-id="20be1-103">Accès de jeux de données avec Python à l’aide de la bibliothèque cliente de hello Azure Machine Learning Python</span><span class="sxs-lookup"><span data-stu-id="20be1-103">Access datasets with Python using hello Azure Machine Learning Python client library</span></span>
<span data-ttu-id="20be1-104">afficher un aperçu de Hello de bibliothèque cliente de Microsoft Azure Machine Learning Python permettre un accès sécurisé tooyour jeux de données Azure Machine Learning à partir d’un environnement local de Python et permet la création de hello et la gestion de jeux de données dans un espace de travail.</span><span class="sxs-lookup"><span data-stu-id="20be1-104">hello preview of Microsoft Azure Machine Learning Python client library can enable secure access tooyour Azure Machine Learning datasets from a local Python environment and enables hello creation and management of datasets in a workspace.</span></span>

<span data-ttu-id="20be1-105">Cette rubrique fournit des instructions pour les procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="20be1-105">This topic provides instructions on how to:</span></span>

* <span data-ttu-id="20be1-106">installer la bibliothèque cliente de Machine Learning Python hello</span><span class="sxs-lookup"><span data-stu-id="20be1-106">install hello Machine Learning Python client library</span></span> 
* <span data-ttu-id="20be1-107">accéder à et de jeux de données, y compris des instructions sur la façon de télécharger tooget d’autorisation tooaccess jeux de données Azure Machine Learning à partir de votre environnement local de Python</span><span class="sxs-lookup"><span data-stu-id="20be1-107">access and upload datasets, including instructions on how tooget authorization tooaccess Azure Machine Learning datasets from your local Python environment</span></span>
* <span data-ttu-id="20be1-108">accès aux jeux de données intermédiaires à partir d'expériences</span><span class="sxs-lookup"><span data-stu-id="20be1-108">access intermediate datasets from experiments</span></span>
* <span data-ttu-id="20be1-109">utiliser des datasets tooenumerate bibliothèque hello Python client accéder aux métadonnées, lire le contenu d’un dataset hello, créer de nouveaux datasets et mettre à jour des jeux de données existants</span><span class="sxs-lookup"><span data-stu-id="20be1-109">use hello Python client library tooenumerate datasets, access metadata, read hello contents of a dataset, create new datasets and update existing datasets</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <span data-ttu-id="20be1-110"><a name="prerequisites"></a>Configuration requise</span><span class="sxs-lookup"><span data-stu-id="20be1-110"><a name="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="20be1-111">bibliothèque cliente de Python Hello a été testé sous hello suivant environnements :</span><span class="sxs-lookup"><span data-stu-id="20be1-111">hello Python client library has been tested under hello following environments:</span></span>

* <span data-ttu-id="20be1-112">Windows, Mac et Linux</span><span class="sxs-lookup"><span data-stu-id="20be1-112">Windows, Mac and Linux</span></span>
* <span data-ttu-id="20be1-113">Python 2.7, 3.3 et 3.4</span><span class="sxs-lookup"><span data-stu-id="20be1-113">Python 2.7, 3.3 and 3.4</span></span>

<span data-ttu-id="20be1-114">Il a une dépendance sur hello suivant des packages :</span><span class="sxs-lookup"><span data-stu-id="20be1-114">It has a dependency on hello following packages:</span></span>

* <span data-ttu-id="20be1-115">requêtes</span><span class="sxs-lookup"><span data-stu-id="20be1-115">requests</span></span>
* <span data-ttu-id="20be1-116">python-dateutil</span><span class="sxs-lookup"><span data-stu-id="20be1-116">python-dateutil</span></span>
* <span data-ttu-id="20be1-117">pandas</span><span class="sxs-lookup"><span data-stu-id="20be1-117">pandas</span></span>

<span data-ttu-id="20be1-118">Nous recommandons d’utiliser une distribution de Python comme [Anaconda](http://continuum.io/downloads#all) ou [Canopy](https://store.enthought.com/downloads/), qui sont fournis avec Python, notebooks et d’installer les packages hello trois répertoriés ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="20be1-118">We recommend using a Python distribution such as [Anaconda](http://continuum.io/downloads#all) or [Canopy](https://store.enthought.com/downloads/), which come with Python, IPython and hello three packages listed above installed.</span></span> <span data-ttu-id="20be1-119">Bien que IPython n'est pas formellement requis, il s'agit d'un environnement idéal pour la manipulation et la visualisation interactive des données.</span><span class="sxs-lookup"><span data-stu-id="20be1-119">Although IPython is not strictly required, it is a great environment for manipulating and visualizing data interactively.</span></span>

### <span data-ttu-id="20be1-120"><a name="installation"></a>Comment tooinstall hello bibliothèque cliente de Azure Machine Learning Python</span><span class="sxs-lookup"><span data-stu-id="20be1-120"><a name="installation"></a>How tooinstall hello Azure Machine Learning Python client library</span></span>
<span data-ttu-id="20be1-121">bibliothèque cliente de Azure Machine Learning Python Hello doit également être installé toocomplete des tâches hello présentées dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="20be1-121">hello Azure Machine Learning Python client library must also be installed toocomplete hello tasks outlined in this topic.</span></span> <span data-ttu-id="20be1-122">Il est disponible à partir de hello [Python Package Index](https://pypi.python.org/pypi/azureml).</span><span class="sxs-lookup"><span data-stu-id="20be1-122">It is available from hello [Python Package Index](https://pypi.python.org/pypi/azureml).</span></span> <span data-ttu-id="20be1-123">tooinstall dans votre environnement de Python, exécutez hello après une commande à partir de votre environnement de Python local :</span><span class="sxs-lookup"><span data-stu-id="20be1-123">tooinstall it in your Python environment, run hello following command from your local Python environment:</span></span>

    pip install azureml

<span data-ttu-id="20be1-124">Ou bien, vous pouvez télécharger et installer à partir de sources de hello sur [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).</span><span class="sxs-lookup"><span data-stu-id="20be1-124">Alternatively, you can download and install from hello sources on [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).</span></span>

    python setup.py install

<span data-ttu-id="20be1-125">Si vous avez git installé sur votre ordinateur, vous pouvez utiliser pip tooinstall directement à partir de référentiel git de hello :</span><span class="sxs-lookup"><span data-stu-id="20be1-125">If you have git installed on your machine, you can use pip tooinstall directly from hello git repository:</span></span>

    pip install git+https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python.git


## <span data-ttu-id="20be1-126"><a name="datasetAccess"></a>Utiliser des datasets tooaccess Studio Code des extraits de code</span><span class="sxs-lookup"><span data-stu-id="20be1-126"><a name="datasetAccess"></a>Use Studio Code snippets tooaccess datasets</span></span>
<span data-ttu-id="20be1-127">bibliothèque cliente de Python Hello vous donne un accès par programmation tooyour jeux de données existante à partir d’expériences qui ont été exécutées.</span><span class="sxs-lookup"><span data-stu-id="20be1-127">hello Python client library gives you programmatic access tooyour existing datasets from experiments that have been run.</span></span>

<span data-ttu-id="20be1-128">À partir d’une interface web hello Studio, vous pouvez générer des extraits de code qui incluent toutes les toodownload d’informations nécessaires hello et désérialiser des jeux de données en tant qu’objets Pandas la trame de données sur votre ordinateur de l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="20be1-128">From hello Studio web interface, you can generate code snippets that include all hello necessary information toodownload and deserialize datasets as Pandas DataFrame objects on your location machine.</span></span>

### <span data-ttu-id="20be1-129"><a name="security"></a>Sécurité relative à l'accès aux données</span><span class="sxs-lookup"><span data-stu-id="20be1-129"><a name="security"></a>Security for data access</span></span>
<span data-ttu-id="20be1-130">extraits de code fournis par Studio pour utilisation avec la bibliothèque cliente de Python hello inclut votre id d’espace de travail et l’autorisation de Hello jeton.</span><span class="sxs-lookup"><span data-stu-id="20be1-130">hello code snippets provided by Studio for use with hello Python client library includes your workspace id and authorization token.</span></span> <span data-ttu-id="20be1-131">Ces fournissent l’espace de travail tooyour un accès complet et doivent être protégés comme un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="20be1-131">These provide full access tooyour workspace and must be protected, like a password.</span></span>

<span data-ttu-id="20be1-132">Pour des raisons de sécurité, fonctionnalité d’extrait de code hello est uniquement disponible toousers qui ont leur rôle défini en tant que **propriétaire** pour l’espace de travail hello.</span><span class="sxs-lookup"><span data-stu-id="20be1-132">For security reasons, hello code snippet functionality is only available toousers that have their role set as **Owner** for hello workspace.</span></span> <span data-ttu-id="20be1-133">Votre rôle est affiché dans Azure Machine Learning Studio sur hello **utilisateurs** page sous **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="20be1-133">Your role is displayed in Azure Machine Learning Studio on hello **USERS** page under **Settings**.</span></span>

![Sécurité][security]

<span data-ttu-id="20be1-135">Si votre rôle n’est pas défini en tant que **propriétaire**, vous pouvez soit demander toobe nouvelle en tant que propriétaire, ou demandez au propriétaire de tooprovide d’espace de travail hello hello vous avec l’extrait de code hello.</span><span class="sxs-lookup"><span data-stu-id="20be1-135">If your role is not set as **Owner**, you can either request toobe reinvited as an owner, or ask hello owner of hello workspace tooprovide you with hello code snippet.</span></span>

<span data-ttu-id="20be1-136">jeton d’autorisation de hello tooobtain, vous pouvez effectuer hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="20be1-136">tooobtain hello authorization token, you can do one of hello following:</span></span>

* <span data-ttu-id="20be1-137">Demander un jeton à un propriétaire.</span><span class="sxs-lookup"><span data-stu-id="20be1-137">Ask for a token from an owner.</span></span> <span data-ttu-id="20be1-138">Propriétaires peuvent accéder à leurs jetons d’autorisation à partir de la page des paramètres de leur espace de travail dans Studio hello.</span><span class="sxs-lookup"><span data-stu-id="20be1-138">Owners can access their authorization tokens from hello Settings page of their workspace in Studio.</span></span> <span data-ttu-id="20be1-139">Sélectionnez **paramètres** de hello gauche du volet et cliquez sur **jetons d’autorisation** toosee hello les jetons principaux et secondaires.</span><span class="sxs-lookup"><span data-stu-id="20be1-139">Select **Settings** from hello left pane and click **AUTHORIZATION TOKENS** toosee hello primary and secondary tokens.</span></span>  <span data-ttu-id="20be1-140">Bien hello principal ou jetons d’autorisation secondaire hello peuvent être utilisés dans l’extrait de code hello, il est recommandé que les propriétaires uniquement partagent les jetons d’autorisation secondaire hello.</span><span class="sxs-lookup"><span data-stu-id="20be1-140">Although either hello primary or hello secondary authorization tokens can be used in hello code snippet, it is recommended that owners only share hello secondary authorization tokens.</span></span>

![Jetons d’autorisation](./media/machine-learning-python-data-access/ml-python-access-settings-tokens.png)

* <span data-ttu-id="20be1-142">Demandez à toorole toobe promue du propriétaire.</span><span class="sxs-lookup"><span data-stu-id="20be1-142">Ask toobe promoted toorole of owner.</span></span>  <span data-ttu-id="20be1-143">toodo cela, un propriétaire actuel du toofirst de besoins d’espace de travail hello vous supprimer à partir de l’espace de travail hello puis ré-vous inviter tooit en tant que propriétaire.</span><span class="sxs-lookup"><span data-stu-id="20be1-143">toodo this, a current owner of hello workspace needs toofirst remove you from hello workspace then re-invite you tooit as an owner.</span></span>

<span data-ttu-id="20be1-144">Une fois que les développeurs ont obtenu les id d’espace de travail hello et l’autorisation jetons, ils sont en mesure de tooaccess espace de travail de hello à l’aide d’extrait de code hello, quelle que soit leur rôle.</span><span class="sxs-lookup"><span data-stu-id="20be1-144">Once developers have obtained hello workspace id and authorization token, they are able tooaccess hello workspace using hello code snippet regardless of their role.</span></span>

<span data-ttu-id="20be1-145">Jetons d’autorisation sont gérés sur hello **jetons d’autorisation** page sous **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="20be1-145">Authorization tokens are managed on hello **AUTHORIZATION TOKENS** page under **SETTINGS**.</span></span> <span data-ttu-id="20be1-146">Vous pouvez régénérer les, mais cette procédure révoque le jeton précédent d’accès toohello.</span><span class="sxs-lookup"><span data-stu-id="20be1-146">You can regenerate them, but this procedure revokes access toohello previous token.</span></span>

### <span data-ttu-id="20be1-147"><a name="accessingDatasets"></a>Accès aux jeux de données depuis une application Python locale</span><span class="sxs-lookup"><span data-stu-id="20be1-147"><a name="accessingDatasets"></a>Access datasets from a local Python application</span></span>
1. <span data-ttu-id="20be1-148">Dans la Machine Learning Studio, cliquez sur **jeux de données** dans la barre de navigation hello sur hello gauche.</span><span class="sxs-lookup"><span data-stu-id="20be1-148">In Machine Learning Studio, click **DATASETS** in hello navigation bar on hello left.</span></span>
2. <span data-ttu-id="20be1-149">Sélectionnez le dataset hello tooaccess voulue.</span><span class="sxs-lookup"><span data-stu-id="20be1-149">Select hello dataset you would like tooaccess.</span></span> <span data-ttu-id="20be1-150">Vous pouvez sélectionner un des jeux de données hello hello **mes DATASETS** liste ou à partir de hello **exemples** liste.</span><span class="sxs-lookup"><span data-stu-id="20be1-150">You can select any of hello datasets from hello **MY DATASETS** list or from hello **SAMPLES** list.</span></span>
3. <span data-ttu-id="20be1-151">Dans la barre d’outils du bas hello, cliquez sur **Code d’accès aux données générer**.</span><span class="sxs-lookup"><span data-stu-id="20be1-151">From hello bottom toolbar, click **Generate Data Access Code**.</span></span> <span data-ttu-id="20be1-152">Si les données de salutation sont dans un format incompatible avec la bibliothèque cliente de Python hello, ce bouton est désactivé.</span><span class="sxs-lookup"><span data-stu-id="20be1-152">If hello data is in a format incompatible with hello Python client library, this button is disabled.</span></span>
   
    ![JEUX DE DONNÉES][datasets]
4. <span data-ttu-id="20be1-154">Sélectionnez l’extrait de code hello à partir de la fenêtre hello qui s’affiche et copiez-le tooyour Presse-papiers.</span><span class="sxs-lookup"><span data-stu-id="20be1-154">Select hello code snippet from hello window that appears and copy it tooyour clipboard.</span></span>
   
    ![Code d'accès][dataset-access-code]
5. <span data-ttu-id="20be1-156">Collez les code hello dans Bloc-notes hello de votre application Python locale.</span><span class="sxs-lookup"><span data-stu-id="20be1-156">Paste hello code into hello notebook of your local Python application.</span></span>
   
    ![Bloc-notes][ipython-dataset]

## <span data-ttu-id="20be1-158"><a name="accessingIntermediateDatasets"></a>Accès aux jeux de données intermédiaires à partir d'expériences de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="20be1-158"><a name="accessingIntermediateDatasets"></a>Access intermediate datasets from Machine Learning experiments</span></span>
<span data-ttu-id="20be1-159">Après l’exécution d’une expérience Bonjour Machine Learning Studio, il est possible tooaccess hello intermédiaire des groupes de données à partir des nœuds de sortie hello des modules.</span><span class="sxs-lookup"><span data-stu-id="20be1-159">After an experiment is run in hello Machine Learning Studio, it is possible tooaccess hello intermediate datasets from hello output nodes of modules.</span></span> <span data-ttu-id="20be1-160">Les jeux de données intermédiaires sont des données qui ont été créées et utilisées pour les étapes intermédiaires lorsqu'un outil de modèle a été exécuté.</span><span class="sxs-lookup"><span data-stu-id="20be1-160">Intermediate datasets are data that has been created and used for intermediate steps when a model tool has been run.</span></span>

<span data-ttu-id="20be1-161">Jeux de données intermédiaires sont accessibles tant que format de données hello est compatible avec la bibliothèque cliente de Python hello.</span><span class="sxs-lookup"><span data-stu-id="20be1-161">Intermediate datasets can be accessed as long as hello data format is compatible with hello Python client library.</span></span>

<span data-ttu-id="20be1-162">Hello formats suivants sont pris en charge (dans ce cas, les constantes sont Bonjour `azureml.DataTypeIds` classe) :</span><span class="sxs-lookup"><span data-stu-id="20be1-162">hello following formats are supported (constants for these are in hello `azureml.DataTypeIds` class):</span></span>

* <span data-ttu-id="20be1-163">Texte brut</span><span class="sxs-lookup"><span data-stu-id="20be1-163">PlainText</span></span>
* <span data-ttu-id="20be1-164">CSV générique</span><span class="sxs-lookup"><span data-stu-id="20be1-164">GenericCSV</span></span>
* <span data-ttu-id="20be1-165">TSV générique</span><span class="sxs-lookup"><span data-stu-id="20be1-165">GenericTSV</span></span>
* <span data-ttu-id="20be1-166">CSV générique sans en-tête</span><span class="sxs-lookup"><span data-stu-id="20be1-166">GenericCSVNoHeader</span></span>
* <span data-ttu-id="20be1-167">TSV générique sans en-tête</span><span class="sxs-lookup"><span data-stu-id="20be1-167">GenericTSVNoHeader</span></span>

<span data-ttu-id="20be1-168">Vous pouvez déterminer le format de hello en pointant sur un nœud de sortie de module.</span><span class="sxs-lookup"><span data-stu-id="20be1-168">You can determine hello format by hovering over a module output node.</span></span> <span data-ttu-id="20be1-169">Il s’affiche avec le nom du nœud hello, dans une info-bulle.</span><span class="sxs-lookup"><span data-stu-id="20be1-169">It is displayed along with hello node name, in a tooltip.</span></span>

<span data-ttu-id="20be1-170">Certains des modules hello, par exemple hello [fractionnement] [ split] module, le format de sortie de tooa nommé `Dataset`, qui n’est pas pris en charge par la bibliothèque cliente de Python hello.</span><span class="sxs-lookup"><span data-stu-id="20be1-170">Some of hello modules, such as hello [Split][split] module, output tooa format named `Dataset`, which is not supported by hello Python client library.</span></span>

![Format de jeu de données][dataset-format]

<span data-ttu-id="20be1-172">Vous devez toouse un module de conversion, tel que [convertir tooCSV][convert-to-csv], tooget une sortie dans un format pris en charge.</span><span class="sxs-lookup"><span data-stu-id="20be1-172">You need toouse a conversion module, such as [Convert tooCSV][convert-to-csv], tooget an output into a supported format.</span></span>

![Format CSV générique][csv-format]

<span data-ttu-id="20be1-174">Hello étapes suivantes montrent un exemple qui crée une expérience, exécute et accède au jeu de données intermédiaire hello.</span><span class="sxs-lookup"><span data-stu-id="20be1-174">hello following steps show an example that creates an experiment, runs it and accesses hello intermediate dataset.</span></span>

1. <span data-ttu-id="20be1-175">Création d'une nouvelle expérience.</span><span class="sxs-lookup"><span data-stu-id="20be1-175">Create a new experiment.</span></span>
2. <span data-ttu-id="20be1-176">Insérez un module **Jeu de données Adult Census Income Binary Classification** .</span><span class="sxs-lookup"><span data-stu-id="20be1-176">Insert an **Adult Census Income Binary Classification dataset** module.</span></span>
3. <span data-ttu-id="20be1-177">Insérer un [fractionnement] [ split] module et vous connecter à sa sortie de module d’entrée toohello jeu de données.</span><span class="sxs-lookup"><span data-stu-id="20be1-177">Insert a [Split][split] module, and connect its input toohello dataset module output.</span></span>
4. <span data-ttu-id="20be1-178">Insérer un [convertir tooCSV] [ convert-to-csv] module et se connecter à son tooone d’entrée de hello [fractionnement] [ split] module génère.</span><span class="sxs-lookup"><span data-stu-id="20be1-178">Insert a [Convert tooCSV][convert-to-csv] module and connect its input tooone of hello [Split][split] module outputs.</span></span>
5. <span data-ttu-id="20be1-179">Enregistrer l’expérience de hello, exécuter et attendez qu’elle toofinish en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="20be1-179">Save hello experiment, run it, and wait for it toofinish running.</span></span>
6. <span data-ttu-id="20be1-180">Cliquez sur le nœud de sortie hello sur hello [convertir tooCSV] [ convert-to-csv] module.</span><span class="sxs-lookup"><span data-stu-id="20be1-180">Click hello output node on hello [Convert tooCSV][convert-to-csv] module.</span></span>
7. <span data-ttu-id="20be1-181">Menu contextuel de hello, sélectionnez **Code d’accès aux données générer**.</span><span class="sxs-lookup"><span data-stu-id="20be1-181">When hello context menu appears, select **Generate Data Access Code**.</span></span>
   
    ![Menu contextuel][experiment]
8. <span data-ttu-id="20be1-183">Sélectionnez l’extrait de code hello et copier tooyour Presse-papiers à partir de la fenêtre hello qui s’affiche.</span><span class="sxs-lookup"><span data-stu-id="20be1-183">Select hello code snippet and copy it tooyour clipboard from hello window that appears.</span></span>
   
    ![Code d'accès][intermediate-dataset-access-code]
9. <span data-ttu-id="20be1-185">Collez le code de hello dans le bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="20be1-185">Paste hello code in your notebook.</span></span>
   
    ![Bloc-notes][ipython-intermediate-dataset]
10. <span data-ttu-id="20be1-187">Vous pouvez visualiser les données de salutation avec matplotlib ;.</span><span class="sxs-lookup"><span data-stu-id="20be1-187">You can visualize hello data using matplotlib.</span></span> <span data-ttu-id="20be1-188">Cela affiche dans un histogramme pour la colonne d’âge hello :</span><span class="sxs-lookup"><span data-stu-id="20be1-188">This displays in a histogram for hello age column:</span></span>
    
    ![Histogramme][ipython-histogram]

## <span data-ttu-id="20be1-190"><a name="clientApis"></a>Utilisez tooaccess de bibliothèque client hello Machine Learning Python, lire, créer et gérer des jeux de données</span><span class="sxs-lookup"><span data-stu-id="20be1-190"><a name="clientApis"></a>Use hello Machine Learning Python client library tooaccess, read, create, and manage datasets</span></span>
### <a name="workspace"></a><span data-ttu-id="20be1-191">Espace de travail</span><span class="sxs-lookup"><span data-stu-id="20be1-191">Workspace</span></span>
<span data-ttu-id="20be1-192">espace de travail Hello est le point d’entrée hello pour la bibliothèque cliente de Python hello.</span><span class="sxs-lookup"><span data-stu-id="20be1-192">hello workspace is hello entry point for hello Python client library.</span></span> <span data-ttu-id="20be1-193">Fournir hello `Workspace` classe avec votre espace de travail un id et l’autorisation toocreate jeton une instance :</span><span class="sxs-lookup"><span data-stu-id="20be1-193">Provide hello `Workspace` class with your workspace id and authorization token toocreate an instance:</span></span>

    ws = Workspace(workspace_id='4c29e1adeba2e5a7cbeb0e4f4adfb4df',
                   authorization_token='f4f3ade2c6aefdb1afb043cd8bcf3daf')


### <a name="enumerate-datasets"></a><span data-ttu-id="20be1-194">Énumérer les jeux de données</span><span class="sxs-lookup"><span data-stu-id="20be1-194">Enumerate datasets</span></span>
<span data-ttu-id="20be1-195">tooenumerate tous les jeux de données dans un espace de travail donné :</span><span class="sxs-lookup"><span data-stu-id="20be1-195">tooenumerate all datasets in a given workspace:</span></span>

    for ds in ws.datasets:
        print(ds.name)

<span data-ttu-id="20be1-196">tooenumerate hello simplement créés par l’utilisateur des groupes de données :</span><span class="sxs-lookup"><span data-stu-id="20be1-196">tooenumerate just hello user-created datasets:</span></span>

    for ds in ws.user_datasets:
        print(ds.name)

<span data-ttu-id="20be1-197">jeux de données tooenumerate hello simplement exemple :</span><span class="sxs-lookup"><span data-stu-id="20be1-197">tooenumerate just hello example datasets:</span></span>

    for ds in ws.example_datasets:
        print(ds.name)

<span data-ttu-id="20be1-198">Vous pouvez accéder à un jeu de données par son nom (qui respecte la casse) :</span><span class="sxs-lookup"><span data-stu-id="20be1-198">You can access a dataset by name (which is case-sensitive):</span></span>

    ds = ws.datasets['my dataset name']

<span data-ttu-id="20be1-199">Vous pouvez également y accéder par l'index :</span><span class="sxs-lookup"><span data-stu-id="20be1-199">Or you can access it by index:</span></span>

    ds = ws.datasets[0]


### <a name="metadata"></a><span data-ttu-id="20be1-200">Metadata</span><span class="sxs-lookup"><span data-stu-id="20be1-200">Metadata</span></span>
<span data-ttu-id="20be1-201">Jeux de données des métadonnées, dans toocontent d’addition.</span><span class="sxs-lookup"><span data-stu-id="20be1-201">Datasets have metadata, in addition toocontent.</span></span> <span data-ttu-id="20be1-202">(Les jeux de données intermédiaires sont une règle d’exception toothis et n’ont pas toutes les métadonnées.)</span><span class="sxs-lookup"><span data-stu-id="20be1-202">(Intermediate datasets are an exception toothis rule and do not have any metadata.)</span></span>

<span data-ttu-id="20be1-203">Certaines valeurs de métadonnées sont affectés par l’utilisateur de hello lors de la création :</span><span class="sxs-lookup"><span data-stu-id="20be1-203">Some metadata values are assigned by hello user at creation time:</span></span>

    print(ds.name)
    print(ds.description)
    print(ds.family_id)
    print(ds.data_type_id)

<span data-ttu-id="20be1-204">D'autres sont des valeurs affectées par Azure ML :</span><span class="sxs-lookup"><span data-stu-id="20be1-204">Others are values assigned by Azure ML:</span></span>

    print(ds.id)
    print(ds.created_date)
    print(ds.size)

<span data-ttu-id="20be1-205">Consultez hello `SourceDataset` classe pour les métadonnées disponibles plus on hello.</span><span class="sxs-lookup"><span data-stu-id="20be1-205">See hello `SourceDataset` class for more on hello available metadata.</span></span>

### <a name="read-contents"></a><span data-ttu-id="20be1-206">Lire le contenu</span><span class="sxs-lookup"><span data-stu-id="20be1-206">Read contents</span></span>
<span data-ttu-id="20be1-207">extraits de code Hello fournis automatiquement par Machine Learning Studio, téléchargement et désérialiser l’objet de trame de données Pandas tooa hello dataset.</span><span class="sxs-lookup"><span data-stu-id="20be1-207">hello code snippets provided by Machine Learning Studio automatically download and deserialize hello dataset tooa Pandas DataFrame object.</span></span> <span data-ttu-id="20be1-208">Cette opération s’effectue par hello `to_dataframe` méthode :</span><span class="sxs-lookup"><span data-stu-id="20be1-208">This is done with hello `to_dataframe` method:</span></span>

    frame = ds.to_dataframe()

<span data-ttu-id="20be1-209">Si vous préférez des données brutes toodownload hello et procédez vous-même à la désérialisation de hello, qui est une option.</span><span class="sxs-lookup"><span data-stu-id="20be1-209">If you prefer toodownload hello raw data, and perform hello deserialization yourself, that is an option.</span></span> <span data-ttu-id="20be1-210">Au moment de hello, il s’agit de hello seule option de formats tels que 'ARFF', Impossible de désérialiser la bibliothèque client Python hello.</span><span class="sxs-lookup"><span data-stu-id="20be1-210">At hello moment, this is hello only option for formats such as 'ARFF', which hello Python client library cannot deserialize.</span></span>

<span data-ttu-id="20be1-211">contenu de hello tooread sous forme de texte :</span><span class="sxs-lookup"><span data-stu-id="20be1-211">tooread hello contents as text:</span></span>

    text_data = ds.read_as_text()

<span data-ttu-id="20be1-212">contenu de hello tooread sous forme binaire :</span><span class="sxs-lookup"><span data-stu-id="20be1-212">tooread hello contents as binary:</span></span>

    binary_data = ds.read_as_binary()

<span data-ttu-id="20be1-213">Vous pouvez également ouvrir un contenu toohello :</span><span class="sxs-lookup"><span data-stu-id="20be1-213">You can also just open a stream toohello contents:</span></span>

    with ds.open() as file:
        binary_data_chunk = file.read(1000)


### <a name="create-a-new-dataset"></a><span data-ttu-id="20be1-214">Créer un nouveau jeu de données</span><span class="sxs-lookup"><span data-stu-id="20be1-214">Create a new dataset</span></span>
<span data-ttu-id="20be1-215">bibliothèque cliente de Python Hello vous permet de tooupload des jeux de données à partir de votre programme Python.</span><span class="sxs-lookup"><span data-stu-id="20be1-215">hello Python client library allows you tooupload datasets from your Python program.</span></span> <span data-ttu-id="20be1-216">Ces jeux de données sont alors disponibles pour une utilisation dans votre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="20be1-216">These datasets are then available for use in your workspace.</span></span>

<span data-ttu-id="20be1-217">Si vous disposez de vos données dans une trame de données Pandas, utilisez hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="20be1-217">If you have your data in a Pandas DataFrame, use hello following code:</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_dataframe(
        dataframe=frame,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

<span data-ttu-id="20be1-218">Si vos données sont déjà sérialisées, vous pouvez utiliser :</span><span class="sxs-lookup"><span data-stu-id="20be1-218">If your data is already serialized, you can use:</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_raw_data(
        raw_data=raw_data,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

<span data-ttu-id="20be1-219">la bibliothèque cliente Python Hello est en mesure de tooserialize met en forme une suivant de toohello Pandas de trame de données (dans ce cas, les constantes sont Bonjour `azureml.DataTypeIds` classe) :</span><span class="sxs-lookup"><span data-stu-id="20be1-219">hello Python client library is able tooserialize a Pandas DataFrame toohello following formats (constants for these are in hello `azureml.DataTypeIds` class):</span></span>

* <span data-ttu-id="20be1-220">Texte brut</span><span class="sxs-lookup"><span data-stu-id="20be1-220">PlainText</span></span>
* <span data-ttu-id="20be1-221">CSV générique</span><span class="sxs-lookup"><span data-stu-id="20be1-221">GenericCSV</span></span>
* <span data-ttu-id="20be1-222">TSV générique</span><span class="sxs-lookup"><span data-stu-id="20be1-222">GenericTSV</span></span>
* <span data-ttu-id="20be1-223">CSV générique sans en-tête</span><span class="sxs-lookup"><span data-stu-id="20be1-223">GenericCSVNoHeader</span></span>
* <span data-ttu-id="20be1-224">TSV générique sans en-tête</span><span class="sxs-lookup"><span data-stu-id="20be1-224">GenericTSVNoHeader</span></span>

### <a name="update-an-existing-dataset"></a><span data-ttu-id="20be1-225">Mettre à jour un jeu de données existant</span><span class="sxs-lookup"><span data-stu-id="20be1-225">Update an existing dataset</span></span>
<span data-ttu-id="20be1-226">Si vous essayez tooupload un nouveau dataset avec un nom qui correspond à un dataset existant, vous devez obtenir une erreur de conflit.</span><span class="sxs-lookup"><span data-stu-id="20be1-226">If you try tooupload a new dataset with a name that matches an existing dataset, you should get a conflict error.</span></span>

<span data-ttu-id="20be1-227">tooupdate un dataset existant, vous devez tout d’abord tooget un jeu de données référence toohello existant :</span><span class="sxs-lookup"><span data-stu-id="20be1-227">tooupdate an existing dataset, you first need tooget a reference toohello existing dataset:</span></span>

    dataset = ws.datasets['existing dataset']

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

<span data-ttu-id="20be1-228">Utilisez ensuite `update_from_dataframe` tooserialize et remplacer contenu hello du jeu de données hello sur Azure :</span><span class="sxs-lookup"><span data-stu-id="20be1-228">Then use `update_from_dataframe` tooserialize and replace hello contents of hello dataset on Azure:</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(frame2)

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

<span data-ttu-id="20be1-229">Si vous souhaitez autre format tooserialize hello données tooa, spécifiez une valeur pour hello facultatif `data_type_id` paramètre.</span><span class="sxs-lookup"><span data-stu-id="20be1-229">If you want tooserialize hello data tooa different format, specify a value for hello optional `data_type_id` parameter.</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        data_type_id=DataTypeIds.GenericTSV,
    )

    print(dataset.data_type_id) # 'GenericTSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

<span data-ttu-id="20be1-230">Vous pouvez éventuellement définir une nouvelle description en spécifiant une valeur pour hello `description` paramètre.</span><span class="sxs-lookup"><span data-stu-id="20be1-230">You can optionally set a new description by specifying a value for hello `description` parameter.</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        description='data up toofeb 2015',
    )

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toofeb 2015'

<span data-ttu-id="20be1-231">Vous pouvez éventuellement définir un nouveau nom en spécifiant une valeur pour hello `name` paramètre.</span><span class="sxs-lookup"><span data-stu-id="20be1-231">You can optionally set a new name by specifying a value for hello `name` parameter.</span></span> <span data-ttu-id="20be1-232">Dès lors, vous allez récupérer hello le jeu de données à l’aide du nouveau nom uniquement hello.</span><span class="sxs-lookup"><span data-stu-id="20be1-232">From now on, you'll retrieve hello dataset using hello new name only.</span></span> <span data-ttu-id="20be1-233">Hello suivant code met à jour la description, nom et les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="20be1-233">hello following code updates hello data, name and description.</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        name='existing dataset v2',
        description='data up toofeb 2015',
    )

    print(dataset.data_type_id)                    # 'GenericCSV'
    print(dataset.name)                            # 'existing dataset v2'
    print(dataset.description)                     # 'data up toofeb 2015'

    print(ws.datasets['existing dataset v2'].name) # 'existing dataset v2'
    print(ws.datasets['existing dataset'].name)    # IndexError

<span data-ttu-id="20be1-234">Hello `data_type_id`, `name` et `description` paramètres sont facultatifs et la valeur précédente de tootheir par défaut.</span><span class="sxs-lookup"><span data-stu-id="20be1-234">hello `data_type_id`, `name` and `description` parameters are optional and default tootheir previous value.</span></span> <span data-ttu-id="20be1-235">Hello `dataframe` paramètre est toujours requis.</span><span class="sxs-lookup"><span data-stu-id="20be1-235">hello `dataframe` parameter is always required.</span></span>

<span data-ttu-id="20be1-236">Si vos données sont déjà sérialisées, utilisez `update_from_raw_data` au lieu de `update_from_dataframe`.</span><span class="sxs-lookup"><span data-stu-id="20be1-236">If your data is already serialized, use `update_from_raw_data` instead of `update_from_dataframe`.</span></span> <span data-ttu-id="20be1-237">Si vous transmettez simplement `raw_data` au lieu de `dataframe`, cela fonctionne de la même manière.</span><span class="sxs-lookup"><span data-stu-id="20be1-237">If you just pass in `raw_data` instead of  `dataframe`, it works in a similar way.</span></span>

<!-- Images -->
[security]:./media/machine-learning-python-data-access/security.png
[dataset-format]:./media/machine-learning-python-data-access/dataset-format.png
[csv-format]:./media/machine-learning-python-data-access/csv-format.png
[datasets]:./media/machine-learning-python-data-access/datasets.png
[dataset-access-code]:./media/machine-learning-python-data-access/dataset-access-code.png
[ipython-dataset]:./media/machine-learning-python-data-access/ipython-dataset.png
[experiment]:./media/machine-learning-python-data-access/experiment.png
[intermediate-dataset-access-code]:./media/machine-learning-python-data-access/intermediate-dataset-access-code.png
[ipython-intermediate-dataset]:./media/machine-learning-python-data-access/ipython-intermediate-dataset.png
[ipython-histogram]:./media/machine-learning-python-data-access/ipython-histogram.png


<!-- Module References -->
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/

