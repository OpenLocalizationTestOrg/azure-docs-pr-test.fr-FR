---
title: "Accès à des jeux de données grâce à la bibliothèque cliente Python Machine Learning | Microsoft Docs"
description: "Installez et utilisez la bibliothèque cliente Python pour accéder et gérer les données d'apprentissage automatique d'Azure en toute sécurité à partir d'un environnement Python local."
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
ms.openlocfilehash: e3ae712e0f8d386f637520fbbff4b348bc86f32d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="access-datasets-with-python-using-the-azure-machine-learning-python-client-library"></a><span data-ttu-id="0c866-103">Accédez aux jeux de données avec Python grâce à la bibliothèque cliente Python d'Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0c866-103">Access datasets with Python using the Azure Machine Learning Python client library</span></span>
<span data-ttu-id="0c866-104">L’aperçu de la bibliothèque cliente Python de Microsoft Azure Machine Learning offre un accès sécurisé à vos jeux de données Azure Machine Learning à partir d’un environnement Python local et permet la création et la gestion de jeux de données dans un espace de travail.</span><span class="sxs-lookup"><span data-stu-id="0c866-104">The preview of Microsoft Azure Machine Learning Python client library can enable secure access to your Azure Machine Learning datasets from a local Python environment and enables the creation and management of datasets in a workspace.</span></span>

<span data-ttu-id="0c866-105">Cette rubrique fournit des instructions pour les procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="0c866-105">This topic provides instructions on how to:</span></span>

* <span data-ttu-id="0c866-106">installation de la bibliothèque cliente Python de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0c866-106">install the Machine Learning Python client library</span></span> 
* <span data-ttu-id="0c866-107">accès et téléchargement des jeux de données, y compris des instructions sur l’obtention d’une autorisation d'accès aux jeux de données Azure Machine Learning depuis votre environnement Python local</span><span class="sxs-lookup"><span data-stu-id="0c866-107">access and upload datasets, including instructions on how to get authorization to access Azure Machine Learning datasets from your local Python environment</span></span>
* <span data-ttu-id="0c866-108">accès aux jeux de données intermédiaires à partir d'expériences</span><span class="sxs-lookup"><span data-stu-id="0c866-108">access intermediate datasets from experiments</span></span>
* <span data-ttu-id="0c866-109">utilisation de la bibliothèque cliente Python pour énumérer les jeux de données, accès aux métadonnées, lecture du contenu d'un jeu de données, création de nouveaux jeux de données et mise à jour des jeux de données existants</span><span class="sxs-lookup"><span data-stu-id="0c866-109">use the Python client library to enumerate datasets, access metadata, read the contents of a dataset, create new datasets and update existing datasets</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <span data-ttu-id="0c866-110"><a name="prerequisites"></a>Configuration requise</span><span class="sxs-lookup"><span data-stu-id="0c866-110"><a name="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="0c866-111">La bibliothèque cliente Python a été testée dans les environnements suivants :</span><span class="sxs-lookup"><span data-stu-id="0c866-111">The Python client library has been tested under the following environments:</span></span>

* <span data-ttu-id="0c866-112">Windows, Mac et Linux</span><span class="sxs-lookup"><span data-stu-id="0c866-112">Windows, Mac and Linux</span></span>
* <span data-ttu-id="0c866-113">Python 2.7, 3.3 et 3.4</span><span class="sxs-lookup"><span data-stu-id="0c866-113">Python 2.7, 3.3 and 3.4</span></span>

<span data-ttu-id="0c866-114">Il a une dépendance sur les packages suivants :</span><span class="sxs-lookup"><span data-stu-id="0c866-114">It has a dependency on the following packages:</span></span>

* <span data-ttu-id="0c866-115">requêtes</span><span class="sxs-lookup"><span data-stu-id="0c866-115">requests</span></span>
* <span data-ttu-id="0c866-116">python-dateutil</span><span class="sxs-lookup"><span data-stu-id="0c866-116">python-dateutil</span></span>
* <span data-ttu-id="0c866-117">pandas</span><span class="sxs-lookup"><span data-stu-id="0c866-117">pandas</span></span>

<span data-ttu-id="0c866-118">Nous vous invitons à utiliser une distribution Python telle qu’[Anaconda](http://continuum.io/downloads#all) ou [Canopy](https://store.enthought.com/downloads/), qui est fournie avec Python, IPython et les trois packages listés ci-dessus installés.</span><span class="sxs-lookup"><span data-stu-id="0c866-118">We recommend using a Python distribution such as [Anaconda](http://continuum.io/downloads#all) or [Canopy](https://store.enthought.com/downloads/), which come with Python, IPython and the three packages listed above installed.</span></span> <span data-ttu-id="0c866-119">Bien que IPython n'est pas formellement requis, il s'agit d'un environnement idéal pour la manipulation et la visualisation interactive des données.</span><span class="sxs-lookup"><span data-stu-id="0c866-119">Although IPython is not strictly required, it is a great environment for manipulating and visualizing data interactively.</span></span>

### <span data-ttu-id="0c866-120"><a name="installation"></a>Installation de la bibliothèque cliente Python d'Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0c866-120"><a name="installation"></a>How to install the Azure Machine Learning Python client library</span></span>
<span data-ttu-id="0c866-121">La bibliothèque cliente Python d’Azure Machine Learning doit également être installée pour effectuer les tâches décrites dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="0c866-121">The Azure Machine Learning Python client library must also be installed to complete the tasks outlined in this topic.</span></span> <span data-ttu-id="0c866-122">Elle est disponible depuis le [Python Package Index](https://pypi.python.org/pypi/azureml).</span><span class="sxs-lookup"><span data-stu-id="0c866-122">It is available from the [Python Package Index](https://pypi.python.org/pypi/azureml).</span></span> <span data-ttu-id="0c866-123">Pour l'installer dans votre environnement Python, exécutez la commande suivante à partir de votre environnement Python local :</span><span class="sxs-lookup"><span data-stu-id="0c866-123">To install it in your Python environment, run the following command from your local Python environment:</span></span>

    pip install azureml

<span data-ttu-id="0c866-124">Autrement, vous pouvez la télécharger et l'installer à partir des sources sur [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).</span><span class="sxs-lookup"><span data-stu-id="0c866-124">Alternatively, you can download and install from the sources on [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).</span></span>

    python setup.py install

<span data-ttu-id="0c866-125">Si vous avez installé git sur votre ordinateur, vous pouvez utiliser pip pour l'installer directement à partir du référentiel git :</span><span class="sxs-lookup"><span data-stu-id="0c866-125">If you have git installed on your machine, you can use pip to install directly from the git repository:</span></span>

    pip install git+https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python.git


## <span data-ttu-id="0c866-126"><a name="datasetAccess"></a>Utilisation des extraits de code Studio pour accéder aux jeux de données</span><span class="sxs-lookup"><span data-stu-id="0c866-126"><a name="datasetAccess"></a>Use Studio Code snippets to access datasets</span></span>
<span data-ttu-id="0c866-127">La bibliothèque cliente Python vous offre un accès par programme à vos jeux de données existants à partir des expériences qui ont été exécutées.</span><span class="sxs-lookup"><span data-stu-id="0c866-127">The Python client library gives you programmatic access to your existing datasets from experiments that have been run.</span></span>

<span data-ttu-id="0c866-128">Depuis l'interface web Studio, vous pouvez générer des extraits de code qui incluent toutes les informations nécessaires pour télécharger et désérialiser des jeux de données en tant qu'objets DataFrame de Pandas sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="0c866-128">From the Studio web interface, you can generate code snippets that include all the necessary information to download and deserialize datasets as Pandas DataFrame objects on your location machine.</span></span>

### <span data-ttu-id="0c866-129"><a name="security"></a>Sécurité relative à l'accès aux données</span><span class="sxs-lookup"><span data-stu-id="0c866-129"><a name="security"></a>Security for data access</span></span>
<span data-ttu-id="0c866-130">Les extraits de code fournis par Studio pour une utilisation avec la bibliothèque cliente Python incluent l'ID de votre d'espace de travail et le jeton d'autorisation.</span><span class="sxs-lookup"><span data-stu-id="0c866-130">The code snippets provided by Studio for use with the Python client library includes your workspace id and authorization token.</span></span> <span data-ttu-id="0c866-131">Ceux-ci vous permettent un accès complet à votre espace de travail et doivent être protégés, par exemple avec un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="0c866-131">These provide full access to your workspace and must be protected, like a password.</span></span>

<span data-ttu-id="0c866-132">Pour des raisons de sécurité, la fonctionnalité d'extrait de code est uniquement disponible pour les utilisateurs qui ont leur rôle défini en tant que **Propriétaire** de l'espace de travail.</span><span class="sxs-lookup"><span data-stu-id="0c866-132">For security reasons, the code snippet functionality is only available to users that have their role set as **Owner** for the workspace.</span></span> <span data-ttu-id="0c866-133">Votre rôle s’affiche dans Azure Machine Learning Studio sur la page **UTILISATEURS** sous **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="0c866-133">Your role is displayed in Azure Machine Learning Studio on the **USERS** page under **Settings**.</span></span>

![Sécurité][security]

<span data-ttu-id="0c866-135">Si votre rôle n’est pas défini en tant que **Propriétaire**, vous pouvez demander à être invité à nouveau en tant que propriétaire ou demander au propriétaire de l’espace de travail de vous fournir l’extrait de code.</span><span class="sxs-lookup"><span data-stu-id="0c866-135">If your role is not set as **Owner**, you can either request to be reinvited as an owner, or ask the owner of the workspace to provide you with the code snippet.</span></span>

<span data-ttu-id="0c866-136">Pour obtenir le jeton d'autorisation, vous pouvez effectuer l'une des opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="0c866-136">To obtain the authorization token, you can do one of the following:</span></span>

* <span data-ttu-id="0c866-137">Demander un jeton à un propriétaire.</span><span class="sxs-lookup"><span data-stu-id="0c866-137">Ask for a token from an owner.</span></span> <span data-ttu-id="0c866-138">Les propriétaires peuvent accéder à leurs jetons d'autorisation à partir de la page Paramètres de leur espace de travail dans Studio.</span><span class="sxs-lookup"><span data-stu-id="0c866-138">Owners can access their authorization tokens from the Settings page of their workspace in Studio.</span></span> <span data-ttu-id="0c866-139">Sélectionnez **Paramètres** dans le volet gauche puis cliquez sur **JETONS D’AUTORISATION** pour voir les jetons principaux et secondaires.</span><span class="sxs-lookup"><span data-stu-id="0c866-139">Select **Settings** from the left pane and click **AUTHORIZATION TOKENS** to see the primary and secondary tokens.</span></span>  <span data-ttu-id="0c866-140">Bien que les jetons d'autorisation principaux ou secondaires puissent être utilisés dans l'extrait de code, il est recommandé aux propriétaires de ne partager que les jetons d'autorisation secondaires.</span><span class="sxs-lookup"><span data-stu-id="0c866-140">Although either the primary or the secondary authorization tokens can be used in the code snippet, it is recommended that owners only share the secondary authorization tokens.</span></span>

![Jetons d’autorisation](./media/machine-learning-python-data-access/ml-python-access-settings-tokens.png)

* <span data-ttu-id="0c866-142">Demander à être promu au rôle de propriétaire.</span><span class="sxs-lookup"><span data-stu-id="0c866-142">Ask to be promoted to role of owner.</span></span>  <span data-ttu-id="0c866-143">Pour cela, un propriétaire actuel de l'espace de travail doit tout d'abord vous supprimer de l'espace de travail puis vous y inviter à nouveau en tant que propriétaire.</span><span class="sxs-lookup"><span data-stu-id="0c866-143">To do this, a current owner of the workspace needs to first remove you from the workspace then re-invite you to it as an owner.</span></span>

<span data-ttu-id="0c866-144">Une fois que les développeurs ont obtenu l’ID de l’espace de travail et les jetons d’autorisation, ils peuvent accéder à l’espace de travail à l’aide de l’extrait de code, quel que soit leur rôle.</span><span class="sxs-lookup"><span data-stu-id="0c866-144">Once developers have obtained the workspace id and authorization token, they are able to access the workspace using the code snippet regardless of their role.</span></span>

<span data-ttu-id="0c866-145">Les jetons d’autorisation sont gérés sur la page **JETONS D’AUTORISATION** sous **PARAMÈTRES**.</span><span class="sxs-lookup"><span data-stu-id="0c866-145">Authorization tokens are managed on the **AUTHORIZATION TOKENS** page under **SETTINGS**.</span></span> <span data-ttu-id="0c866-146">Vous pouvez les régénérer, mais cette procédure entraîne la révocation de l’accès au jeton précédent.</span><span class="sxs-lookup"><span data-stu-id="0c866-146">You can regenerate them, but this procedure revokes access to the previous token.</span></span>

### <span data-ttu-id="0c866-147"><a name="accessingDatasets"></a>Accès aux jeux de données depuis une application Python locale</span><span class="sxs-lookup"><span data-stu-id="0c866-147"><a name="accessingDatasets"></a>Access datasets from a local Python application</span></span>
1. <span data-ttu-id="0c866-148">Dans Machine Learning Studio, cliquez sur **JEUX DE DONNÉES** dans la barre de navigation à gauche.</span><span class="sxs-lookup"><span data-stu-id="0c866-148">In Machine Learning Studio, click **DATASETS** in the navigation bar on the left.</span></span>
2. <span data-ttu-id="0c866-149">Sélectionnez le jeu de données auquel vous souhaitez accéder.</span><span class="sxs-lookup"><span data-stu-id="0c866-149">Select the dataset you would like to access.</span></span> <span data-ttu-id="0c866-150">Vous pouvez sélectionner un des jeux de données depuis la liste **MES JEUX DE DONNÉES** ou **EXEMPLES**.</span><span class="sxs-lookup"><span data-stu-id="0c866-150">You can select any of the datasets from the **MY DATASETS** list or from the **SAMPLES** list.</span></span>
3. <span data-ttu-id="0c866-151">Dans la barre d’outils inférieure, cliquez sur **Générer un code d’accès aux données**.</span><span class="sxs-lookup"><span data-stu-id="0c866-151">From the bottom toolbar, click **Generate Data Access Code**.</span></span> <span data-ttu-id="0c866-152">Ce bouton est désactivé si les données sont dans un format incompatible avec la bibliothèque cliente Python.</span><span class="sxs-lookup"><span data-stu-id="0c866-152">If the data is in a format incompatible with the Python client library, this button is disabled.</span></span>
   
    ![JEUX DE DONNÉES][datasets]
4. <span data-ttu-id="0c866-154">Sélectionnez l'extrait de code dans la fenêtre qui s'affiche et copiez-le dans votre presse-papiers.</span><span class="sxs-lookup"><span data-stu-id="0c866-154">Select the code snippet from the window that appears and copy it to your clipboard.</span></span>
   
    ![Code d'accès][dataset-access-code]
5. <span data-ttu-id="0c866-156">Collez le code dans le bloc-notes de votre application Python locale.</span><span class="sxs-lookup"><span data-stu-id="0c866-156">Paste the code into the notebook of your local Python application.</span></span>
   
    ![Bloc-notes][ipython-dataset]

## <span data-ttu-id="0c866-158"><a name="accessingIntermediateDatasets"></a>Accès aux jeux de données intermédiaires à partir d'expériences de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0c866-158"><a name="accessingIntermediateDatasets"></a>Access intermediate datasets from Machine Learning experiments</span></span>
<span data-ttu-id="0c866-159">Après l'exécution d'une expérience dans Machine Learning Studio, il est possible d'accéder aux jeux de données intermédiaires depuis les nœuds de modules de sortie.</span><span class="sxs-lookup"><span data-stu-id="0c866-159">After an experiment is run in the Machine Learning Studio, it is possible to access the intermediate datasets from the output nodes of modules.</span></span> <span data-ttu-id="0c866-160">Les jeux de données intermédiaires sont des données qui ont été créées et utilisées pour les étapes intermédiaires lorsqu'un outil de modèle a été exécuté.</span><span class="sxs-lookup"><span data-stu-id="0c866-160">Intermediate datasets are data that has been created and used for intermediate steps when a model tool has been run.</span></span>

<span data-ttu-id="0c866-161">Les jeux de données intermédiaires sont accessibles tant que le format de données est compatible avec la bibliothèque cliente Python.</span><span class="sxs-lookup"><span data-stu-id="0c866-161">Intermediate datasets can be accessed as long as the data format is compatible with the Python client library.</span></span>

<span data-ttu-id="0c866-162">Les formats suivants sont pris en charge (ces constantes sont dans la classe `azureml.DataTypeIds` ) :</span><span class="sxs-lookup"><span data-stu-id="0c866-162">The following formats are supported (constants for these are in the `azureml.DataTypeIds` class):</span></span>

* <span data-ttu-id="0c866-163">Texte brut</span><span class="sxs-lookup"><span data-stu-id="0c866-163">PlainText</span></span>
* <span data-ttu-id="0c866-164">CSV générique</span><span class="sxs-lookup"><span data-stu-id="0c866-164">GenericCSV</span></span>
* <span data-ttu-id="0c866-165">TSV générique</span><span class="sxs-lookup"><span data-stu-id="0c866-165">GenericTSV</span></span>
* <span data-ttu-id="0c866-166">CSV générique sans en-tête</span><span class="sxs-lookup"><span data-stu-id="0c866-166">GenericCSVNoHeader</span></span>
* <span data-ttu-id="0c866-167">TSV générique sans en-tête</span><span class="sxs-lookup"><span data-stu-id="0c866-167">GenericTSVNoHeader</span></span>

<span data-ttu-id="0c866-168">Vous pouvez déterminer le format en pointant sur un nœud de sortie de module.</span><span class="sxs-lookup"><span data-stu-id="0c866-168">You can determine the format by hovering over a module output node.</span></span> <span data-ttu-id="0c866-169">Celui-ci s'affiche avec le nom de nœud dans une infobulle.</span><span class="sxs-lookup"><span data-stu-id="0c866-169">It is displayed along with the node name, in a tooltip.</span></span>

<span data-ttu-id="0c866-170">Certains des modules, tels que le module [Fractionner][split], ont un format de sortie appelé `Dataset`, qui n’est pas pris en charge par la bibliothèque cliente Python.</span><span class="sxs-lookup"><span data-stu-id="0c866-170">Some of the modules, such as the [Split][split] module, output to a format named `Dataset`, which is not supported by the Python client library.</span></span>

![Format de jeu de données][dataset-format]

<span data-ttu-id="0c866-172">Vous devez utiliser un module de conversion, tel que [Convertir en CSV][convert-to-csv], afin d’obtenir un format de sortie pris en charge.</span><span class="sxs-lookup"><span data-stu-id="0c866-172">You need to use a conversion module, such as [Convert to CSV][convert-to-csv], to get an output into a supported format.</span></span>

![Format CSV générique][csv-format]

<span data-ttu-id="0c866-174">Les étapes suivantes proposent un exemple qui créé une expérience, l'exécute et accède au jeu de données intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="0c866-174">The following steps show an example that creates an experiment, runs it and accesses the intermediate dataset.</span></span>

1. <span data-ttu-id="0c866-175">Création d'une nouvelle expérience.</span><span class="sxs-lookup"><span data-stu-id="0c866-175">Create a new experiment.</span></span>
2. <span data-ttu-id="0c866-176">Insérez un module **Jeu de données Adult Census Income Binary Classification** .</span><span class="sxs-lookup"><span data-stu-id="0c866-176">Insert an **Adult Census Income Binary Classification dataset** module.</span></span>
3. <span data-ttu-id="0c866-177">Insérez un module [Fractionner][split] puis connectez son entrée à une sortie de module de jeu de données.</span><span class="sxs-lookup"><span data-stu-id="0c866-177">Insert a [Split][split] module, and connect its input to the dataset module output.</span></span>
4. <span data-ttu-id="0c866-178">Insérez un module [Convertir en CSV][convert-to-csv], puis connectez son entrée à l’une des sorties du module [Fractionner][split].</span><span class="sxs-lookup"><span data-stu-id="0c866-178">Insert a [Convert to CSV][convert-to-csv] module and connect its input to one of the [Split][split] module outputs.</span></span>
5. <span data-ttu-id="0c866-179">Enregistrez l'expérience, exécutez-la et attendez qu'elle ait fini de s'exécuter.</span><span class="sxs-lookup"><span data-stu-id="0c866-179">Save the experiment, run it, and wait for it to finish running.</span></span>
6. <span data-ttu-id="0c866-180">Cliquez sur le nœud de sortie du module [Convertir en CSV][convert-to-csv].</span><span class="sxs-lookup"><span data-stu-id="0c866-180">Click the output node on the [Convert to CSV][convert-to-csv] module.</span></span>
7. <span data-ttu-id="0c866-181">Lorsque le menu contextuel s’affiche, sélectionnez **Générer un code d’accès aux données**.</span><span class="sxs-lookup"><span data-stu-id="0c866-181">When the context menu appears, select **Generate Data Access Code**.</span></span>
   
    ![Menu contextuel][experiment]
8. <span data-ttu-id="0c866-183">Sélectionnez l’extrait de code dans la fenêtre qui s’affiche et copiez-le dans votre presse-papiers.</span><span class="sxs-lookup"><span data-stu-id="0c866-183">Select the code snippet and copy it to your clipboard from the window that appears.</span></span>
   
    ![Code d'accès][intermediate-dataset-access-code]
9. <span data-ttu-id="0c866-185">Collez le code dans votre bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="0c866-185">Paste the code in your notebook.</span></span>
   
    ![Bloc-notes][ipython-intermediate-dataset]
10. <span data-ttu-id="0c866-187">Vous pouvez visualiser les données à l'aide de matplotlib.</span><span class="sxs-lookup"><span data-stu-id="0c866-187">You can visualize the data using matplotlib.</span></span> <span data-ttu-id="0c866-188">Cela les affiche dans un histogramme pour la colonne âge :</span><span class="sxs-lookup"><span data-stu-id="0c866-188">This displays in a histogram for the age column:</span></span>
    
    ![Histogramme][ipython-histogram]

## <span data-ttu-id="0c866-190"><a name="clientApis"></a>Utilisation de la bibliothèque cliente Python de Machine Learning pour accéder, lire, créer et gérer des jeux de données</span><span class="sxs-lookup"><span data-stu-id="0c866-190"><a name="clientApis"></a>Use the Machine Learning Python client library to access, read, create, and manage datasets</span></span>
### <a name="workspace"></a><span data-ttu-id="0c866-191">Espace de travail</span><span class="sxs-lookup"><span data-stu-id="0c866-191">Workspace</span></span>
<span data-ttu-id="0c866-192">L'espace de travail est le point d'entrée de la bibliothèque cliente Python.</span><span class="sxs-lookup"><span data-stu-id="0c866-192">The workspace is the entry point for the Python client library.</span></span> <span data-ttu-id="0c866-193">Il fournit la classe `Workspace` avec l'ID de votre espace de travail et le jeton d'autorisation pour créer une instance :</span><span class="sxs-lookup"><span data-stu-id="0c866-193">Provide the `Workspace` class with your workspace id and authorization token to create an instance:</span></span>

    ws = Workspace(workspace_id='4c29e1adeba2e5a7cbeb0e4f4adfb4df',
                   authorization_token='f4f3ade2c6aefdb1afb043cd8bcf3daf')


### <a name="enumerate-datasets"></a><span data-ttu-id="0c866-194">Énumérer les jeux de données</span><span class="sxs-lookup"><span data-stu-id="0c866-194">Enumerate datasets</span></span>
<span data-ttu-id="0c866-195">Pour énumérer tous les jeux de données dans un espace de travail donné :</span><span class="sxs-lookup"><span data-stu-id="0c866-195">To enumerate all datasets in a given workspace:</span></span>

    for ds in ws.datasets:
        print(ds.name)

<span data-ttu-id="0c866-196">Pour énumérer uniquement les jeux de données créés par l'utilisateur :</span><span class="sxs-lookup"><span data-stu-id="0c866-196">To enumerate just the user-created datasets:</span></span>

    for ds in ws.user_datasets:
        print(ds.name)

<span data-ttu-id="0c866-197">Pour énumérer uniquement les exemples de jeux de données :</span><span class="sxs-lookup"><span data-stu-id="0c866-197">To enumerate just the example datasets:</span></span>

    for ds in ws.example_datasets:
        print(ds.name)

<span data-ttu-id="0c866-198">Vous pouvez accéder à un jeu de données par son nom (qui respecte la casse) :</span><span class="sxs-lookup"><span data-stu-id="0c866-198">You can access a dataset by name (which is case-sensitive):</span></span>

    ds = ws.datasets['my dataset name']

<span data-ttu-id="0c866-199">Vous pouvez également y accéder par l'index :</span><span class="sxs-lookup"><span data-stu-id="0c866-199">Or you can access it by index:</span></span>

    ds = ws.datasets[0]


### <a name="metadata"></a><span data-ttu-id="0c866-200">Metadata</span><span class="sxs-lookup"><span data-stu-id="0c866-200">Metadata</span></span>
<span data-ttu-id="0c866-201">Les jeux de données ont des métadonnées, en plus du contenu.</span><span class="sxs-lookup"><span data-stu-id="0c866-201">Datasets have metadata, in addition to content.</span></span> <span data-ttu-id="0c866-202">(Les jeux de données intermédiaires sont une exception à cette règle et n'ont pas de métadonnées.)</span><span class="sxs-lookup"><span data-stu-id="0c866-202">(Intermediate datasets are an exception to this rule and do not have any metadata.)</span></span>

<span data-ttu-id="0c866-203">Certaines valeurs de métadonnées sont affectées par l'utilisateur lors de la création :</span><span class="sxs-lookup"><span data-stu-id="0c866-203">Some metadata values are assigned by the user at creation time:</span></span>

    print(ds.name)
    print(ds.description)
    print(ds.family_id)
    print(ds.data_type_id)

<span data-ttu-id="0c866-204">D'autres sont des valeurs affectées par Azure ML :</span><span class="sxs-lookup"><span data-stu-id="0c866-204">Others are values assigned by Azure ML:</span></span>

    print(ds.id)
    print(ds.created_date)
    print(ds.size)

<span data-ttu-id="0c866-205">Consultez la classe `SourceDataset` pour plus d'informations sur les métadonnées disponibles.</span><span class="sxs-lookup"><span data-stu-id="0c866-205">See the `SourceDataset` class for more on the available metadata.</span></span>

### <a name="read-contents"></a><span data-ttu-id="0c866-206">Lire le contenu</span><span class="sxs-lookup"><span data-stu-id="0c866-206">Read contents</span></span>
<span data-ttu-id="0c866-207">Les extraits de code fournis par Machine Learning Studio téléchargent automatiquement et désérialisent le jeu de données vers un objet DataFrame de Pandas.</span><span class="sxs-lookup"><span data-stu-id="0c866-207">The code snippets provided by Machine Learning Studio automatically download and deserialize the dataset to a Pandas DataFrame object.</span></span> <span data-ttu-id="0c866-208">Cette opération est effectuée à l'aide de la méthode `to_dataframe` :</span><span class="sxs-lookup"><span data-stu-id="0c866-208">This is done with the `to_dataframe` method:</span></span>

    frame = ds.to_dataframe()

<span data-ttu-id="0c866-209">Si vous préférez télécharger les données brutes et procéder vous-même à la désérialisation, cela est possible.</span><span class="sxs-lookup"><span data-stu-id="0c866-209">If you prefer to download the raw data, and perform the deserialization yourself, that is an option.</span></span> <span data-ttu-id="0c866-210">Pour le moment, il s'agit de la seule option pour les formats tels que « ARFF » que la bibliothèque cliente Python ne peut pas désérialiser.</span><span class="sxs-lookup"><span data-stu-id="0c866-210">At the moment, this is the only option for formats such as 'ARFF', which the Python client library cannot deserialize.</span></span>

<span data-ttu-id="0c866-211">Pour lire le contenu en texte :</span><span class="sxs-lookup"><span data-stu-id="0c866-211">To read the contents as text:</span></span>

    text_data = ds.read_as_text()

<span data-ttu-id="0c866-212">Pour lire le contenu en binaire :</span><span class="sxs-lookup"><span data-stu-id="0c866-212">To read the contents as binary:</span></span>

    binary_data = ds.read_as_binary()

<span data-ttu-id="0c866-213">Vous pouvez également ouvrir un simple flux vers le contenu :</span><span class="sxs-lookup"><span data-stu-id="0c866-213">You can also just open a stream to the contents:</span></span>

    with ds.open() as file:
        binary_data_chunk = file.read(1000)


### <a name="create-a-new-dataset"></a><span data-ttu-id="0c866-214">Créer un nouveau jeu de données</span><span class="sxs-lookup"><span data-stu-id="0c866-214">Create a new dataset</span></span>
<span data-ttu-id="0c866-215">La bibliothèque cliente Python vous permet de télécharger des jeux de données depuis votre programme Python.</span><span class="sxs-lookup"><span data-stu-id="0c866-215">The Python client library allows you to upload datasets from your Python program.</span></span> <span data-ttu-id="0c866-216">Ces jeux de données sont alors disponibles pour une utilisation dans votre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="0c866-216">These datasets are then available for use in your workspace.</span></span>

<span data-ttu-id="0c866-217">Si vous avez vos données dans un DataFrame de Pandas, utilisez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="0c866-217">If you have your data in a Pandas DataFrame, use the following code:</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_dataframe(
        dataframe=frame,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

<span data-ttu-id="0c866-218">Si vos données sont déjà sérialisées, vous pouvez utiliser :</span><span class="sxs-lookup"><span data-stu-id="0c866-218">If your data is already serialized, you can use:</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_raw_data(
        raw_data=raw_data,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

<span data-ttu-id="0c866-219">La bibliothèque cliente Python est en mesure de sérialiser une trame de données Pandas aux formats suivants (ces constantes sont dans la classe `azureml.DataTypeIds` ) :</span><span class="sxs-lookup"><span data-stu-id="0c866-219">The Python client library is able to serialize a Pandas DataFrame to the following formats (constants for these are in the `azureml.DataTypeIds` class):</span></span>

* <span data-ttu-id="0c866-220">Texte brut</span><span class="sxs-lookup"><span data-stu-id="0c866-220">PlainText</span></span>
* <span data-ttu-id="0c866-221">CSV générique</span><span class="sxs-lookup"><span data-stu-id="0c866-221">GenericCSV</span></span>
* <span data-ttu-id="0c866-222">TSV générique</span><span class="sxs-lookup"><span data-stu-id="0c866-222">GenericTSV</span></span>
* <span data-ttu-id="0c866-223">CSV générique sans en-tête</span><span class="sxs-lookup"><span data-stu-id="0c866-223">GenericCSVNoHeader</span></span>
* <span data-ttu-id="0c866-224">TSV générique sans en-tête</span><span class="sxs-lookup"><span data-stu-id="0c866-224">GenericTSVNoHeader</span></span>

### <a name="update-an-existing-dataset"></a><span data-ttu-id="0c866-225">Mettre à jour un jeu de données existant</span><span class="sxs-lookup"><span data-stu-id="0c866-225">Update an existing dataset</span></span>
<span data-ttu-id="0c866-226">Si vous essayez de télécharger un nouveau jeu de données avec un nom qui correspond à un jeu de données existant, vous devriez obtenir une erreur de conflit.</span><span class="sxs-lookup"><span data-stu-id="0c866-226">If you try to upload a new dataset with a name that matches an existing dataset, you should get a conflict error.</span></span>

<span data-ttu-id="0c866-227">Pour mettre à jour un jeu de données existant, vous devez d'abord obtenir la référence d'un jeu de données existant :</span><span class="sxs-lookup"><span data-stu-id="0c866-227">To update an existing dataset, you first need to get a reference to the existing dataset:</span></span>

    dataset = ws.datasets['existing dataset']

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up to jan 2015'

<span data-ttu-id="0c866-228">Utilisez ensuite `update_from_dataframe` pour sérialiser et remplacer le contenu du jeu de données sur Azure :</span><span class="sxs-lookup"><span data-stu-id="0c866-228">Then use `update_from_dataframe` to serialize and replace the contents of the dataset on Azure:</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(frame2)

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up to jan 2015'

<span data-ttu-id="0c866-229">Si vous souhaitez sérialiser les données dans un format différent, spécifiez une valeur pour le paramètre en option `data_type_id` .</span><span class="sxs-lookup"><span data-stu-id="0c866-229">If you want to serialize the data to a different format, specify a value for the optional `data_type_id` parameter.</span></span>

    from azureml import DataTypeIds

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        data_type_id=DataTypeIds.GenericTSV,
    )

    print(dataset.data_type_id) # 'GenericTSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up to jan 2015'

<span data-ttu-id="0c866-230">Vous pouvez éventuellement définir une nouvelle description en spécifiant une valeur pour le paramètre `description` .</span><span class="sxs-lookup"><span data-stu-id="0c866-230">You can optionally set a new description by specifying a value for the `description` parameter.</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        description='data up to feb 2015',
    )

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up to feb 2015'

<span data-ttu-id="0c866-231">Vous pouvez éventuellement définir un nouveau nom en spécifiant une valeur pour le paramètre `name` .</span><span class="sxs-lookup"><span data-stu-id="0c866-231">You can optionally set a new name by specifying a value for the `name` parameter.</span></span> <span data-ttu-id="0c866-232">À partir de maintenant, vous allez récupérer le jeu de données uniquement à l'aide du nouveau nom.</span><span class="sxs-lookup"><span data-stu-id="0c866-232">From now on, you'll retrieve the dataset using the new name only.</span></span> <span data-ttu-id="0c866-233">Le code suivant met à jour les données, le nom et la description.</span><span class="sxs-lookup"><span data-stu-id="0c866-233">The following code updates the data, name and description.</span></span>

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        name='existing dataset v2',
        description='data up to feb 2015',
    )

    print(dataset.data_type_id)                    # 'GenericCSV'
    print(dataset.name)                            # 'existing dataset v2'
    print(dataset.description)                     # 'data up to feb 2015'

    print(ws.datasets['existing dataset v2'].name) # 'existing dataset v2'
    print(ws.datasets['existing dataset'].name)    # IndexError

<span data-ttu-id="0c866-234">Les paramètres `data_type_id`, `name` et `description` sont facultatifs. Par défaut, ils indiquent leur valeur précédente.</span><span class="sxs-lookup"><span data-stu-id="0c866-234">The `data_type_id`, `name` and `description` parameters are optional and default to their previous value.</span></span> <span data-ttu-id="0c866-235">Le paramètre `dataframe` est toujours requis.</span><span class="sxs-lookup"><span data-stu-id="0c866-235">The `dataframe` parameter is always required.</span></span>

<span data-ttu-id="0c866-236">Si vos données sont déjà sérialisées, utilisez `update_from_raw_data` au lieu de `update_from_dataframe`.</span><span class="sxs-lookup"><span data-stu-id="0c866-236">If your data is already serialized, use `update_from_raw_data` instead of `update_from_dataframe`.</span></span> <span data-ttu-id="0c866-237">Si vous transmettez simplement `raw_data` au lieu de `dataframe`, cela fonctionne de la même manière.</span><span class="sxs-lookup"><span data-stu-id="0c866-237">If you just pass in `raw_data` instead of  `dataframe`, it works in a similar way.</span></span>

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

