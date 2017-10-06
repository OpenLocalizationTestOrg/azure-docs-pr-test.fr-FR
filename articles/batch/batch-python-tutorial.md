---
title: "aaaTutorial - hello d’utilisation du SDK de traitement par lots Azure pour Python | Documents Microsoft"
description: "Découvrez les concepts de base hello de traitement par lots Azure et créer une solution simple à l’aide de Python."
services: batch
documentationcenter: python
author: tamram
manager: timlt
editor: 
ms.assetid: 42cae157-d43d-47f8-88f5-486ccfd334f4
ms.service: batch
ms.devlang: python
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c4d5152aeef31848c50a7f2aae5e7a7e0e1e9535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-batch-sdk-for-python"></a><span data-ttu-id="d52d7-103">Prise en main hello lot SDK pour Python</span><span class="sxs-lookup"><span data-stu-id="d52d7-103">Get started with hello Batch SDK for Python</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d52d7-104">.NET</span><span class="sxs-lookup"><span data-stu-id="d52d7-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="d52d7-105">Python</span><span class="sxs-lookup"><span data-stu-id="d52d7-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="d52d7-106">Node.JS</span><span class="sxs-lookup"><span data-stu-id="d52d7-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="d52d7-107">Principes fondamentaux de hello [Azure Batch] [ azure_batch] et hello [lot Python] [ py_azure_sdk] client comme une petite application de traitement par lots écrite dans Python les sujets abordés.</span><span class="sxs-lookup"><span data-stu-id="d52d7-107">Learn hello basics of [Azure Batch][azure_batch] and hello [Batch Python][py_azure_sdk] client as we discuss a small Batch application written in Python.</span></span> <span data-ttu-id="d52d7-108">Nous allons comment deux exemples scripts utilisez hello lot service tooprocess une charge de travail parallèle sur les ordinateurs virtuels Linux dans le cloud de hello et comment ils interagissent avec [Azure Storage](../storage/common/storage-introduction.md) intermédiaire de fichier et l’extraction.</span><span class="sxs-lookup"><span data-stu-id="d52d7-108">We look at how two sample scripts use hello Batch service tooprocess a parallel workload on Linux virtual machines in hello cloud, and how they interact with [Azure Storage](../storage/common/storage-introduction.md) for file staging and retrieval.</span></span> <span data-ttu-id="d52d7-109">Vous allez en savoir un flux de travail courant lot application acquérir une compréhension de base du hello principaux composants du lot telles que les travaux, les tâches, les pools et nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="d52d7-109">You'll learn a common Batch application workflow and gain a base understanding of hello major components of Batch such as jobs, tasks, pools, and compute nodes.</span></span>

<span data-ttu-id="d52d7-110">![Flux de travail de la solution Batch (de base)][11]</span><span class="sxs-lookup"><span data-stu-id="d52d7-110">![Batch solution workflow (basic)][11]</span></span><br/>

## <a name="prerequisites"></a><span data-ttu-id="d52d7-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d52d7-111">Prerequisites</span></span>
<span data-ttu-id="d52d7-112">Cet article suppose que vous avez acquis une connaissance pratique de Python et que vous êtes familiarisé avec Linux.</span><span class="sxs-lookup"><span data-stu-id="d52d7-112">This article assumes that you have a working knowledge of Python and familiarity with Linux.</span></span> <span data-ttu-id="d52d7-113">Il suppose également que vous êtes en mesure de toosatisfy hello création exigences relatives aux comptes qui sont spécifiées ci-dessous pour Azure et hello lot et les services de stockage.</span><span class="sxs-lookup"><span data-stu-id="d52d7-113">It also assumes that you're able toosatisfy hello account creation requirements that are specified below for Azure and hello Batch and Storage services.</span></span>

### <a name="accounts"></a><span data-ttu-id="d52d7-114">Comptes</span><span class="sxs-lookup"><span data-stu-id="d52d7-114">Accounts</span></span>
* <span data-ttu-id="d52d7-115">**Compte Azure** : si vous ne possédez pas encore d’abonnement Azure, [créez un compte Azure gratuit][azure_free_account].</span><span class="sxs-lookup"><span data-stu-id="d52d7-115">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account][azure_free_account].</span></span>
* <span data-ttu-id="d52d7-116">**Compte Batch**: une fois que vous disposez d’un abonnement Azure, [créez un compte Azure Batch](batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d52d7-116">**Batch account**: Once you have an Azure subscription, [create an Azure Batch account](batch-account-create-portal.md).</span></span>
* <span data-ttu-id="d52d7-117">**Compte de stockage** : voir la section [Créer un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account) de l’article [À propos des comptes de stockage Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="d52d7-117">**Storage account**: See [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

### <a name="code-sample"></a><span data-ttu-id="d52d7-118">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="d52d7-118">Code sample</span></span>
<span data-ttu-id="d52d7-119">didacticiel de Python Hello [exemple de code] [ github_article_samples] est un des hello de nombreux exemples de code de lot trouvés dans hello [exemples de traitement par lots azure] [ github_samples] référentiel sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="d52d7-119">hello Python tutorial [code sample][github_article_samples] is one of hello many Batch code samples found in hello [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="d52d7-120">Vous pouvez télécharger tous les exemples de hello en cliquant sur **Clone ou téléchargement > ZIP de téléchargement** sur la page d’accueil de référentiel hello, ou en cliquant sur hello [azure-lot-exemples-master.zip] [ github_samples_zip]lien direct.</span><span class="sxs-lookup"><span data-stu-id="d52d7-120">You can download all hello samples by clicking **Clone or download > Download ZIP** on hello repository home page, or by clicking hello [azure-batch-samples-master.zip][github_samples_zip] direct download link.</span></span> <span data-ttu-id="d52d7-121">Une fois que vous avez extrait le contenu hello du fichier ZIP de hello, scripts hello deux pour ce didacticiel sont trouvent dans hello `article_samples` active :</span><span class="sxs-lookup"><span data-stu-id="d52d7-121">Once you've extracted hello contents of hello ZIP file, hello two scripts for this tutorial are found in hello `article_samples` directory:</span></span>

`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_client.py`<br/>
`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_task.py`

### <a name="python-environment"></a><span data-ttu-id="d52d7-122">Environnement Python</span><span class="sxs-lookup"><span data-stu-id="d52d7-122">Python environment</span></span>
<span data-ttu-id="d52d7-123">toorun hello *python_tutorial_client.py* exemple de script sur votre station de travail locale, vous devez un **interpréteur Python** compatible avec la version **2.7** ou **3.3 +**.</span><span class="sxs-lookup"><span data-stu-id="d52d7-123">toorun hello *python_tutorial_client.py* sample script on your local workstation, you need a **Python interpreter** compatible with version **2.7** or **3.3+**.</span></span> <span data-ttu-id="d52d7-124">script de Hello a été testé sur Linux et Windows.</span><span class="sxs-lookup"><span data-stu-id="d52d7-124">hello script has been tested on both Linux and Windows.</span></span>

### <a name="cryptography-dependencies"></a><span data-ttu-id="d52d7-125">dépendances de chiffrement</span><span class="sxs-lookup"><span data-stu-id="d52d7-125">cryptography dependencies</span></span>
<span data-ttu-id="d52d7-126">Vous devez installer les dépendances hello pour hello [cryptographie] [ crypto] bibliothèque, requis par hello `azure-batch` et `azure-storage` packages Python.</span><span class="sxs-lookup"><span data-stu-id="d52d7-126">You must install hello dependencies for hello [cryptography][crypto] library, required by hello `azure-batch` and `azure-storage` Python packages.</span></span> <span data-ttu-id="d52d7-127">Effectuez l’une des hello suit les opérations appropriées pour votre plateforme, ou consultez toohello [installation de chiffrement] [ crypto_install] pour plus d’informations :</span><span class="sxs-lookup"><span data-stu-id="d52d7-127">Perform one of hello following operations appropriate for your platform, or refer toohello [cryptography installation][crypto_install] details for more information:</span></span>

* <span data-ttu-id="d52d7-128">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="d52d7-128">Ubuntu</span></span>

    `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython-dev python-dev`
* <span data-ttu-id="d52d7-129">CentOS</span><span class="sxs-lookup"><span data-stu-id="d52d7-129">CentOS</span></span>

    `yum update && yum install -y gcc openssl-devel libffi-devel python-devel`
* <span data-ttu-id="d52d7-130">SLES/OpenSUSE</span><span class="sxs-lookup"><span data-stu-id="d52d7-130">SLES/OpenSUSE</span></span>

    `zypper ref && zypper -n in libopenssl-dev libffi48-devel python-devel`
* <span data-ttu-id="d52d7-131">Windows</span><span class="sxs-lookup"><span data-stu-id="d52d7-131">Windows</span></span>

    `pip install cryptography`

> [!NOTE]
> <span data-ttu-id="d52d7-132">Si l’installation de Python 3.3 + sur Linux, utilisez équivalents de python3 hello pour les dépendances de Python hello.</span><span class="sxs-lookup"><span data-stu-id="d52d7-132">If installing for Python 3.3+ on Linux, use hello python3 equivalents for hello Python dependencies.</span></span> <span data-ttu-id="d52d7-133">Par exemple, sur Ubuntu : `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython3-dev python3-dev`</span><span class="sxs-lookup"><span data-stu-id="d52d7-133">For example, on Ubuntu: `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython3-dev python3-dev`</span></span>
>
>

### <a name="azure-packages"></a><span data-ttu-id="d52d7-134">Packages Azure</span><span class="sxs-lookup"><span data-stu-id="d52d7-134">Azure packages</span></span>
<span data-ttu-id="d52d7-135">Ensuite, installez hello **Azure Batch** et **Azure Storage** packages Python.</span><span class="sxs-lookup"><span data-stu-id="d52d7-135">Next, install hello **Azure Batch** and **Azure Storage** Python packages.</span></span> <span data-ttu-id="d52d7-136">Vous pouvez installer les deux packages à l’aide de **pip** et hello *requirements.txt* est disponible ici :</span><span class="sxs-lookup"><span data-stu-id="d52d7-136">You can install both packages by using **pip** and hello *requirements.txt* found here:</span></span>

`/azure-batch-samples/Python/Batch/requirements.txt`

<span data-ttu-id="d52d7-137">Problème suivant **pip** les packages tooinstall hello lot et le stockage de la commande :</span><span class="sxs-lookup"><span data-stu-id="d52d7-137">Issue following **pip** command tooinstall hello Batch and Storage packages:</span></span>

`pip install -r requirements.txt`

<span data-ttu-id="d52d7-138">Vous pouvez également installer hello [par lots azure] [ pypi_batch] et [le stockage azure] [ pypi_storage] Python packages manuellement :</span><span class="sxs-lookup"><span data-stu-id="d52d7-138">Or, you can install hello [azure-batch][pypi_batch] and [azure-storage][pypi_storage] Python packages manually:</span></span>

`pip install azure-batch`<br/>
`pip install azure-storage`

> [!TIP]
> <span data-ttu-id="d52d7-139">Si vous utilisez un compte non privilégié, vous devrez peut-être tooprefix vos commandes avec `sudo`.</span><span class="sxs-lookup"><span data-stu-id="d52d7-139">If you are using an unprivileged account, you may need tooprefix your commands with `sudo`.</span></span> <span data-ttu-id="d52d7-140">Par exemple, `sudo pip install -r requirements.txt`.</span><span class="sxs-lookup"><span data-stu-id="d52d7-140">For example, `sudo pip install -r requirements.txt`.</span></span> <span data-ttu-id="d52d7-141">Pour plus d’informations sur l’installation des packages Python, voir [Installing Packages][pypi_install] (Installation des packages) sur python.org.</span><span class="sxs-lookup"><span data-stu-id="d52d7-141">For more information on installing Python packages, see [Installing Packages][pypi_install] on python.org.</span></span>
>
>

## <a name="batch-python-tutorial-code-sample"></a><span data-ttu-id="d52d7-142">Exemple de code de didacticiel Python Batch</span><span class="sxs-lookup"><span data-stu-id="d52d7-142">Batch Python tutorial code sample</span></span>
<span data-ttu-id="d52d7-143">exemple de code du didacticiel Hello Python de lot se compose de deux scripts Python et plusieurs fichiers de données.</span><span class="sxs-lookup"><span data-stu-id="d52d7-143">hello Batch Python tutorial code sample consists of two Python scripts and a few data files.</span></span>

* <span data-ttu-id="d52d7-144">**python_tutorial_client.py**: interagit avec tooexecute de services de stockage et de traitement par lots hello une charge de travail parallèle sur les nœuds de calcul (machines virtuelles).</span><span class="sxs-lookup"><span data-stu-id="d52d7-144">**python_tutorial_client.py**: Interacts with hello Batch and Storage services tooexecute a parallel workload on compute nodes (virtual machines).</span></span> <span data-ttu-id="d52d7-145">Hello *python_tutorial_client.py* script s’exécute sur votre station de travail locale.</span><span class="sxs-lookup"><span data-stu-id="d52d7-145">hello *python_tutorial_client.py* script runs on your local workstation.</span></span>
* <span data-ttu-id="d52d7-146">**python_tutorial_task.py**: script hello qui s’exécute sur les nœuds de calcul dans Azure tooperform travail hello.</span><span class="sxs-lookup"><span data-stu-id="d52d7-146">**python_tutorial_task.py**: hello script that runs on compute nodes in Azure tooperform hello actual work.</span></span> <span data-ttu-id="d52d7-147">Dans l’exemple hello, *python_tutorial_task.py* analyse hello texte dans un fichier téléchargé depuis le stockage Azure (fichier d’entrée de hello).</span><span class="sxs-lookup"><span data-stu-id="d52d7-147">In hello sample, *python_tutorial_task.py* parses hello text in a file downloaded from Azure Storage (hello input file).</span></span> <span data-ttu-id="d52d7-148">Ensuite, il génère un fichier texte (fichier de sortie hello) qui contient une liste de mots de trois premières hello qui s’affichent dans le fichier d’entrée de hello.</span><span class="sxs-lookup"><span data-stu-id="d52d7-148">Then it produces a text file (hello output file) that contains a list of hello top three words that appear in hello input file.</span></span> <span data-ttu-id="d52d7-149">Une fois qu’il crée le fichier de sortie hello, *python_tutorial_task.py* téléchargements hello fichier tooAzure stockage.</span><span class="sxs-lookup"><span data-stu-id="d52d7-149">After it creates hello output file, *python_tutorial_task.py* uploads hello file tooAzure Storage.</span></span> <span data-ttu-id="d52d7-150">Cela rend disponible pour le script de client toohello de téléchargement en cours d’exécution sur votre station de travail.</span><span class="sxs-lookup"><span data-stu-id="d52d7-150">This makes it available for download toohello client script running on your workstation.</span></span> <span data-ttu-id="d52d7-151">Hello *python_tutorial_task.py* script s’exécute en parallèle sur plusieurs nœuds de calcul dans hello service Batch.</span><span class="sxs-lookup"><span data-stu-id="d52d7-151">hello *python_tutorial_task.py* script runs in parallel on multiple compute nodes in hello Batch service.</span></span>
* <span data-ttu-id="d52d7-152">**./Data/taskdata\*.txt**: ces trois fichiers texte fournissent une entrée de hello pour les nœuds de calcul tâches hello qui s’exécutent sur hello.</span><span class="sxs-lookup"><span data-stu-id="d52d7-152">**./data/taskdata\*.txt**: These three text files provide hello input for hello tasks that run on hello compute nodes.</span></span>

<span data-ttu-id="d52d7-153">Hello suivant schéma illustre les opérations principales hello qui sont effectuées par les scripts de client et de la tâche hello.</span><span class="sxs-lookup"><span data-stu-id="d52d7-153">hello following diagram illustrates hello primary operations that are performed by hello client and task scripts.</span></span> <span data-ttu-id="d52d7-154">Ce flux de travail de base est caractéristique de nombreuses solutions de calcul créées avec Batch.</span><span class="sxs-lookup"><span data-stu-id="d52d7-154">This basic workflow is typical of many compute solutions that are created with Batch.</span></span> <span data-ttu-id="d52d7-155">Pendant qu’il ne présente pas toutes les fonctionnalités disponibles dans hello service Batch, presque tous les scénarios de traitement par lots inclut des parties de ce flux de travail.</span><span class="sxs-lookup"><span data-stu-id="d52d7-155">While it does not demonstrate every feature available in hello Batch service, nearly every Batch scenario includes portions of this workflow.</span></span>

<span data-ttu-id="d52d7-156">![Exemple de flux de travail Batch][8]</span><span class="sxs-lookup"><span data-stu-id="d52d7-156">![Batch example workflow][8]</span></span><br/>

[<span data-ttu-id="d52d7-157">**Étape 1.**</span><span class="sxs-lookup"><span data-stu-id="d52d7-157">**Step 1.**</span></span>](#step-1-create-storage-containers) <span data-ttu-id="d52d7-158">Créer des **conteneurs** dans le Stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="d52d7-158">Create **containers** in Azure Blob Storage.</span></span><br/><span data-ttu-id="d52d7-159">
[**Étape 2.**](#step-2-upload-task-script-and-data-files)</span><span class="sxs-lookup"><span data-stu-id="d52d7-159">
[**Step 2.**](#step-2-upload-task-script-and-data-files)</span></span> <span data-ttu-id="d52d7-160">Téléchargez toocontainers de fichiers de script et d’entrée de tâche.</span><span class="sxs-lookup"><span data-stu-id="d52d7-160">Upload task script and input files toocontainers.</span></span><br/><span data-ttu-id="d52d7-161">
[**Étape 3.**](#step-3-create-batch-pool)</span><span class="sxs-lookup"><span data-stu-id="d52d7-161">
[**Step 3.**](#step-3-create-batch-pool)</span></span> <span data-ttu-id="d52d7-162">Créer un **pool** Batch.</span><span class="sxs-lookup"><span data-stu-id="d52d7-162">Create a Batch **pool**.</span></span><br/>
  <span data-ttu-id="d52d7-163">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span><span class="sxs-lookup"><span data-stu-id="d52d7-163">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span></span> <span data-ttu-id="d52d7-164">Hello pool **StartTask** téléchargements hello tâche script (python_tutorial_task.py) toonodes dès qu’ils rejoignent le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="d52d7-164">hello pool **StartTask** downloads hello task script (python_tutorial_task.py) toonodes as they join hello pool.</span></span><br/><span data-ttu-id="d52d7-165">
[**Étape 4.**](#step-4-create-batch-job)</span><span class="sxs-lookup"><span data-stu-id="d52d7-165">
[**Step 4.**](#step-4-create-batch-job)</span></span> <span data-ttu-id="d52d7-166">Créer un **travail** Batch.</span><span class="sxs-lookup"><span data-stu-id="d52d7-166">Create a Batch **job**.</span></span><br/><span data-ttu-id="d52d7-167">
[**Étape 5.**](#step-5-add-tasks-to-job)</span><span class="sxs-lookup"><span data-stu-id="d52d7-167">
[**Step 5.**](#step-5-add-tasks-to-job)</span></span> <span data-ttu-id="d52d7-168">Ajouter **tâches** toohello travail.</span><span class="sxs-lookup"><span data-stu-id="d52d7-168">Add **tasks** toohello job.</span></span><br/>
  <span data-ttu-id="d52d7-169">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span><span class="sxs-lookup"><span data-stu-id="d52d7-169">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span></span> <span data-ttu-id="d52d7-170">les tâches de Hello sont planifiée tooexecute sur les nœuds.</span><span class="sxs-lookup"><span data-stu-id="d52d7-170">hello tasks are scheduled tooexecute on nodes.</span></span><br/>
    <span data-ttu-id="d52d7-171">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span><span class="sxs-lookup"><span data-stu-id="d52d7-171">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span></span> <span data-ttu-id="d52d7-172">Chaque tâche télécharge ses données d’entrée depuis Stockage Azure, puis commence l’exécution.</span><span class="sxs-lookup"><span data-stu-id="d52d7-172">Each task downloads its input data from Azure Storage, then begins execution.</span></span><br/><span data-ttu-id="d52d7-173">
[**Étape 6.**](#step-6-monitor-tasks)</span><span class="sxs-lookup"><span data-stu-id="d52d7-173">
[**Step 6.**](#step-6-monitor-tasks)</span></span> <span data-ttu-id="d52d7-174">Surveiller les tâches.</span><span class="sxs-lookup"><span data-stu-id="d52d7-174">Monitor tasks.</span></span><br/>
  <span data-ttu-id="d52d7-175">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span><span class="sxs-lookup"><span data-stu-id="d52d7-175">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span></span> <span data-ttu-id="d52d7-176">Comme les tâches sont effectuées, ils téléchargent leur tooAzure de données de sortie stockage.</span><span class="sxs-lookup"><span data-stu-id="d52d7-176">As tasks are completed, they upload their output data tooAzure Storage.</span></span><br/><span data-ttu-id="d52d7-177">
[**Étape 7.**](#step-7-download-task-output)</span><span class="sxs-lookup"><span data-stu-id="d52d7-177">
[**Step 7.**](#step-7-download-task-output)</span></span> <span data-ttu-id="d52d7-178">Télécharger la sortie des tâches à partir de Storage.</span><span class="sxs-lookup"><span data-stu-id="d52d7-178">Download task output from Storage.</span></span>

<span data-ttu-id="d52d7-179">Comme indiqué précédemment, certaines solutions Batch ne suivent pas exactement cette procédure et peuvent exécuter de nombreuses autres opérations ; toutefois, cet exemple illustre les processus fréquemment inclus dans une solution Batch.</span><span class="sxs-lookup"><span data-stu-id="d52d7-179">As mentioned, not every Batch solution performs these exact steps, and may include many more, but this sample demonstrates common processes found in a Batch solution.</span></span>

## <a name="prepare-client-script"></a><span data-ttu-id="d52d7-180">Préparer le script client</span><span class="sxs-lookup"><span data-stu-id="d52d7-180">Prepare client script</span></span>
<span data-ttu-id="d52d7-181">Avant d’exécuter les exemples hello, ajoutez vos informations d’identification de compte de stockage et de traitement par lots trop*python_tutorial_client.py*.</span><span class="sxs-lookup"><span data-stu-id="d52d7-181">Before you run hello sample, add your Batch and Storage account credentials too*python_tutorial_client.py*.</span></span> <span data-ttu-id="d52d7-182">Si vous n’avez pas déjà fait, ouvrez les fichier hello dans votre hello Favoris d’éditeur et de mise à jour de lignes avec vos informations d’identification suivantes.</span><span class="sxs-lookup"><span data-stu-id="d52d7-182">If you have not done so already, open hello file in your favorite editor and update hello following lines with your credentials.</span></span>

```python
# Update hello Batch and Storage account credential strings below with hello values
# unique tooyour accounts. These are used when constructing connection strings
# for hello Batch and Storage client objects.

# Batch account credentials
BATCH_ACCOUNT_NAME = ""
BATCH_ACCOUNT_KEY = ""
BATCH_ACCOUNT_URL = ""

# Storage account credentials
STORAGE_ACCOUNT_NAME = ""
STORAGE_ACCOUNT_KEY = ""
```

<span data-ttu-id="d52d7-183">Vous pouvez trouver vos informations d’identification compte Batch et de stockage dans le panneau de compte hello de chaque service Bonjour [portail Azure][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="d52d7-183">You can find your Batch and Storage account credentials within hello account blade of each service in hello [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="d52d7-184">![Traitement par lots les informations d’identification dans le portail de hello][9]
![informations d’identification de stockage dans le portail de hello][10]</span><span class="sxs-lookup"><span data-stu-id="d52d7-184">![Batch credentials in hello portal][9]
![Storage credentials in hello portal][10]</span></span><br/>

<span data-ttu-id="d52d7-185">Bonjour les sections suivantes, nous analysons les étapes hello utilisés par hello scripts tooprocess une charge de travail Bonjour service Batch.</span><span class="sxs-lookup"><span data-stu-id="d52d7-185">In hello following sections, we analyze hello steps used by hello scripts tooprocess a workload in hello Batch service.</span></span> <span data-ttu-id="d52d7-186">Nous vous encourageons toorefer régulièrement toohello des scripts dans votre éditeur pendant que vous progressez via rest hello d’article de hello.</span><span class="sxs-lookup"><span data-stu-id="d52d7-186">We encourage you toorefer regularly toohello scripts in your editor while you work your way through hello rest of hello article.</span></span>

<span data-ttu-id="d52d7-187">Accédez toohello ligne dans **python_tutorial_client.py** toostart à l’étape 1 :</span><span class="sxs-lookup"><span data-stu-id="d52d7-187">Navigate toohello following line in **python_tutorial_client.py** toostart with Step 1:</span></span>

```python
if __name__ == '__main__':
```

## <a name="step-1-create-storage-containers"></a><span data-ttu-id="d52d7-188">Étape 1 : créer des conteneurs de stockage</span><span class="sxs-lookup"><span data-stu-id="d52d7-188">Step 1: Create Storage containers</span></span>
<span data-ttu-id="d52d7-189">![Créer des conteneurs dans le service Stockage Azure][1]
</span><span class="sxs-lookup"><span data-stu-id="d52d7-189">![Create containers in Azure Storage][1]
</span></span><br/>

<span data-ttu-id="d52d7-190">Batch prend en charge l’interaction avec Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="d52d7-190">Batch includes built-in support for interacting with Azure Storage.</span></span> <span data-ttu-id="d52d7-191">Les conteneurs dans votre compte de stockage fournissent des fichiers de hello requis par les tâches de hello qui s’exécutent dans votre compte Batch.</span><span class="sxs-lookup"><span data-stu-id="d52d7-191">Containers in your Storage account will provide hello files needed by hello tasks that run in your Batch account.</span></span> <span data-ttu-id="d52d7-192">les conteneurs de Hello fournissent également des données de sortie de hello toostore sur place qui produisent des tâches de hello.</span><span class="sxs-lookup"><span data-stu-id="d52d7-192">hello containers also provide a place toostore hello output data that hello tasks produce.</span></span> <span data-ttu-id="d52d7-193">Hello première hello *python_tutorial_client.py* du script est créer trois conteneurs dans [stockage d’objets Blob Azure](../storage/common/storage-introduction.md#blob-storage):</span><span class="sxs-lookup"><span data-stu-id="d52d7-193">hello first thing hello *python_tutorial_client.py* script does is create three containers in [Azure Blob Storage](../storage/common/storage-introduction.md#blob-storage):</span></span>

* <span data-ttu-id="d52d7-194">**application**: ce conteneur stockera hello Python script exécuté par les tâches de hello, *python_tutorial_task.py*.</span><span class="sxs-lookup"><span data-stu-id="d52d7-194">**application**: This container will store hello Python script run by hello tasks, *python_tutorial_task.py*.</span></span>
* <span data-ttu-id="d52d7-195">**d’entrée**: tâches téléchargera tooprocess de fichiers de données hello hello *d’entrée* conteneur.</span><span class="sxs-lookup"><span data-stu-id="d52d7-195">**input**: Tasks will download hello data files tooprocess from hello *input* container.</span></span>
* <span data-ttu-id="d52d7-196">**sortie**: lorsque les tâches de terminer le traitement du fichier d’entrée, ils téléchargeront hello résultats toohello *sortie* conteneur.</span><span class="sxs-lookup"><span data-stu-id="d52d7-196">**output**: When tasks complete input file processing, they will upload hello results toohello *output* container.</span></span>

<span data-ttu-id="d52d7-197">Dans l’ordre des toointeract avec un stockage de compte et de créer des conteneurs, nous utilisons hello [le stockage azure] [ pypi_storage] package toocreate un [BlockBlobService] [ py_blockblobservice] objet : hello « client de l’objet blob. »</span><span class="sxs-lookup"><span data-stu-id="d52d7-197">In order toointeract with a Storage account and create containers, we use hello [azure-storage][pypi_storage] package toocreate a [BlockBlobService][py_blockblobservice] object--hello "blob client."</span></span> <span data-ttu-id="d52d7-198">Ensuite, nous créons trois conteneurs hello compte de stockage à l’aide du client de blob hello.</span><span class="sxs-lookup"><span data-stu-id="d52d7-198">We then create three containers in hello Storage account using hello blob client.</span></span>

```python
import azure.storage.blob as azureblob

# Create hello blob client, for use in obtaining references to
# blob storage containers and uploading files toocontainers.
blob_client = azureblob.BlockBlobService(
    account_name=STORAGE_ACCOUNT_NAME,
    account_key=STORAGE_ACCOUNT_KEY)

# Use hello blob client toocreate hello containers in Azure Storage if they
# don't yet exist.
APP_CONTAINER_NAME = 'application'
INPUT_CONTAINER_NAME = 'input'
OUTPUT_CONTAINER_NAME = 'output'
blob_client.create_container(APP_CONTAINER_NAME, fail_on_exist=False)
blob_client.create_container(INPUT_CONTAINER_NAME, fail_on_exist=False)
blob_client.create_container(OUTPUT_CONTAINER_NAME, fail_on_exist=False)
```

<span data-ttu-id="d52d7-199">Une fois que les conteneurs hello ont été créées, application hello peut maintenant télécharger des fichiers de hello qui seront utilisés par les tâches hello.</span><span class="sxs-lookup"><span data-stu-id="d52d7-199">Once hello containers have been created, hello application can now upload hello files that will be used by hello tasks.</span></span>

> [!TIP]
> <span data-ttu-id="d52d7-200">[Comment toouse le stockage Blob Azure à partir de Python](../storage/blobs/storage-python-how-to-use-blob-storage.md) fournit une bonne vue d’ensemble de l’utilisation de conteneurs Azure Storage et les objets BLOB.</span><span class="sxs-lookup"><span data-stu-id="d52d7-200">[How toouse Azure Blob storage from Python](../storage/blobs/storage-python-how-to-use-blob-storage.md) provides a good overview of working with Azure Storage containers and blobs.</span></span> <span data-ttu-id="d52d7-201">Il doit être haut hello de votre liste de lecture commencer à utiliser avec le lot.</span><span class="sxs-lookup"><span data-stu-id="d52d7-201">It should be near hello top of your reading list as you start working with Batch.</span></span>
>
>

## <a name="step-2-upload-task-script-and-data-files"></a><span data-ttu-id="d52d7-202">Étape 2 : charger les scripts de tâche et les fichiers de données</span><span class="sxs-lookup"><span data-stu-id="d52d7-202">Step 2: Upload task script and data files</span></span>
<span data-ttu-id="d52d7-203">![Tâche de chargement d’application et d’entrée (données) des fichiers toocontainers][2]
</span><span class="sxs-lookup"><span data-stu-id="d52d7-203">![Upload task application and input (data) files toocontainers][2]
</span></span><br/>

<span data-ttu-id="d52d7-204">Dans le fichier de hello Téléchargez opération, *python_tutorial_client.py* définit tout d’abord les collections de **application** et **d’entrée** chemins d’accès de fichiers tels qu’ils existent sur l’ordinateur local de hello.</span><span class="sxs-lookup"><span data-stu-id="d52d7-204">In hello file upload operation, *python_tutorial_client.py* first defines collections of **application** and **input** file paths as they exist on hello local machine.</span></span> <span data-ttu-id="d52d7-205">Puis il les télécharge ces conteneurs toohello de fichiers que vous avez créé à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="d52d7-205">Then it uploads these files toohello containers that you created in hello previous step.</span></span>

```python
# Paths toohello task script. This script will be executed by hello tasks that
# run on hello compute nodes.
application_file_paths = [os.path.realpath('python_tutorial_task.py')]

# hello collection of data files that are toobe processed by hello tasks.
input_file_paths = [os.path.realpath('./data/taskdata1.txt'),
                    os.path.realpath('./data/taskdata2.txt'),
                    os.path.realpath('./data/taskdata3.txt')]

# Upload hello application script tooAzure Storage. This is hello script that
# will process hello data files, and is executed by each of hello tasks on the
# compute nodes.
application_files = [
    upload_file_to_container(blob_client, APP_CONTAINER_NAME, file_path)
    for file_path in application_file_paths]

# Upload hello data files. This is hello data that will be processed by each of
# hello tasks executed on hello compute nodes in hello pool.
input_files = [
    upload_file_to_container(blob_client, INPUT_CONTAINER_NAME, file_path)
    for file_path in input_file_paths]
```

<span data-ttu-id="d52d7-206">À l’aide de la compréhension de la liste, hello `upload_file_to_container` fonction est appelée pour chaque fichier dans les collections de hello et deux [ResourceFile] [ py_resource_file] collections sont remplies.</span><span class="sxs-lookup"><span data-stu-id="d52d7-206">Using list comprehension, hello `upload_file_to_container` function is called for each file in hello collections, and two [ResourceFile][py_resource_file] collections are populated.</span></span> <span data-ttu-id="d52d7-207">Hello `upload_file_to_container` fonction apparaît ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="d52d7-207">hello `upload_file_to_container` function appears below:</span></span>

```python
def upload_file_to_container(block_blob_client, container_name, path):
    """
    Uploads a local file tooan Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param str container_name: hello name of hello Azure Blob storage container.
    :param str file_path: hello local path toohello file.
    :rtype: `azure.batch.models.ResourceFile`
    :return: A ResourceFile initialized with a SAS URL appropriate for Batch
    tasks.
    """

    import datetime
    import azure.storage.blob as azureblob
    import azure.batch.models as batchmodels

    blob_name = os.path.basename(path)

    print('Uploading file {} toocontainer [{}]...'.format(path,
                                                          container_name))

    block_blob_client.create_blob_from_path(container_name,
                                            blob_name,
                                            file_path)

    sas_token = block_blob_client.generate_blob_shared_access_signature(
        container_name,
        blob_name,
        permission=azureblob.BlobPermissions.READ,
        expiry=datetime.datetime.utcnow() + datetime.timedelta(hours=2))

    sas_url = block_blob_client.make_blob_url(container_name,
                                              blob_name,
                                              sas_token=sas_token)

    return batchmodels.ResourceFile(file_path=blob_name,
                                    blob_source=sas_url)
```

### <a name="resourcefiles"></a><span data-ttu-id="d52d7-208">Objets ResourceFile</span><span class="sxs-lookup"><span data-stu-id="d52d7-208">ResourceFiles</span></span>
<span data-ttu-id="d52d7-209">A [ResourceFile] [ py_resource_file] fournit des tâches dans un lot avec fichier de tooa hello URL dans le stockage Azure qui est téléchargé tooa nœud de calcul avant l’exécution de cette tâche.</span><span class="sxs-lookup"><span data-stu-id="d52d7-209">A [ResourceFile][py_resource_file] provides tasks in Batch with hello URL tooa file in Azure Storage that is downloaded tooa compute node before that task is run.</span></span> <span data-ttu-id="d52d7-210">Hello [ResourceFile][py_resource_file]. **blob_source** propriété spécifie une URL complète du fichier de hello hello telle qu’elle existe dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="d52d7-210">hello [ResourceFile][py_resource_file].**blob_source** property specifies hello full URL of hello file as it exists in Azure Storage.</span></span> <span data-ttu-id="d52d7-211">URL de Hello peut-être également inclure une signature d’accès partagé (SAS) qui fournit un accès sécurisé toohello fichier.</span><span class="sxs-lookup"><span data-stu-id="d52d7-211">hello URL may also include a shared access signature (SAS) that provides secure access toohello file.</span></span> <span data-ttu-id="d52d7-212">La propriété *ResourceFiles* est utilisée par la plupart des types de tâches dans Batch :</span><span class="sxs-lookup"><span data-stu-id="d52d7-212">Most task types in Batch include a *ResourceFiles* property, including:</span></span>

* <span data-ttu-id="d52d7-213">[CloudTask][py_task]</span><span class="sxs-lookup"><span data-stu-id="d52d7-213">[CloudTask][py_task]</span></span>
* <span data-ttu-id="d52d7-214">[StartTask][py_starttask]</span><span class="sxs-lookup"><span data-stu-id="d52d7-214">[StartTask][py_starttask]</span></span>
* <span data-ttu-id="d52d7-215">[JobPreparationTask][py_jobpreptask]</span><span class="sxs-lookup"><span data-stu-id="d52d7-215">[JobPreparationTask][py_jobpreptask]</span></span>
* <span data-ttu-id="d52d7-216">[JobReleaseTask][py_jobreltask]</span><span class="sxs-lookup"><span data-stu-id="d52d7-216">[JobReleaseTask][py_jobreltask]</span></span>

<span data-ttu-id="d52d7-217">Cet exemple n’utilise pas de type hello JobPreparationTask ou JobReleaseTask les types de tâches, mais vous pouvez en savoir plus sur les [nœuds de calcul des tâches de préparation et l’achèvement de projet sur Azure Batch exécuter](batch-job-prep-release.md).</span><span class="sxs-lookup"><span data-stu-id="d52d7-217">This sample does not use hello JobPreparationTask or JobReleaseTask task types, but you can read more about them in [Run job preparation and completion tasks on Azure Batch compute nodes](batch-job-prep-release.md).</span></span>

### <a name="shared-access-signature-sas"></a><span data-ttu-id="d52d7-218">Signature d’accès partagé (SAP)</span><span class="sxs-lookup"><span data-stu-id="d52d7-218">Shared access signature (SAS)</span></span>
<span data-ttu-id="d52d7-219">Signatures d’accès partagé sont des chaînes qui fournissent un accès sécurisé toocontainers et objets BLOB dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="d52d7-219">Shared access signatures are strings that provide secure access toocontainers and blobs in Azure Storage.</span></span> <span data-ttu-id="d52d7-220">Hello *python_tutorial_client.py* script utilise les deux objets blob et les signatures d’accès partagé de conteneur et montre comment tooobtain ces partagés accéder aux chaînes de signature à partir de hello service de stockage.</span><span class="sxs-lookup"><span data-stu-id="d52d7-220">hello *python_tutorial_client.py* script uses both blob and container shared access signatures, and demonstrates how tooobtain these shared access signature strings from hello Storage service.</span></span>

* <span data-ttu-id="d52d7-221">**Signatures d’accès partagé d’objets BLOB**: utilise des StartTask du pool hello blob signatures d’accès partagé lorsqu’il télécharge hello tâche script et l’entrée des fichiers de données à partir du stockage (voir [étape 3](#step-3-create-batch-pool) ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="d52d7-221">**Blob shared access signatures**: hello pool's StartTask uses blob shared access signatures when it downloads hello task script and input data files from Storage (see [Step #3](#step-3-create-batch-pool) below).</span></span> <span data-ttu-id="d52d7-222">Hello `upload_file_to_container` fonctionner dans *python_tutorial_client.py* contient le code hello qui obtient la signature d’accès partagé de l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="d52d7-222">hello `upload_file_to_container` function in *python_tutorial_client.py* contains hello code that obtains each blob's shared access signature.</span></span> <span data-ttu-id="d52d7-223">Il le fait en appelant [BlockBlobService.make_blob_url] [ py_make_blob_url] dans le module de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="d52d7-223">It does so by calling [BlockBlobService.make_blob_url][py_make_blob_url] in hello Storage module.</span></span>
* <span data-ttu-id="d52d7-224">**Signature d’accès partagé de conteneur**: que chaque tâche a terminé son travail sur le nœud de calcul hello, il télécharge sa toohello de fichier de sortie *sortie* conteneur dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="d52d7-224">**Container shared access signature**: As each task finishes its work on hello compute node, it uploads its output file toohello *output* container in Azure Storage.</span></span> <span data-ttu-id="d52d7-225">toodo, *python_tutorial_task.py* utilise une signature d’accès partagé de conteneur qui fournit un accès en écriture toohello conteneur.</span><span class="sxs-lookup"><span data-stu-id="d52d7-225">toodo so, *python_tutorial_task.py* uses a container shared access signature that provides write access toohello container.</span></span> <span data-ttu-id="d52d7-226">Hello `get_container_sas_token` fonctionner dans *python_tutorial_client.py* Obtient la signature d’accès partagé du conteneur hello, qui est ensuite passée en tant que tâches de toohello un argument de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="d52d7-226">hello `get_container_sas_token` function in *python_tutorial_client.py* obtains hello container's shared access signature, which is then passed as a command-line argument toohello tasks.</span></span> <span data-ttu-id="d52d7-227">Étape 5 de #, [travail de tooa tâches ajouter](#step-5-add-tasks-to-job), traite de l’utilisation de hello de SAP de conteneur hello.</span><span class="sxs-lookup"><span data-stu-id="d52d7-227">Step #5, [Add tasks tooa job](#step-5-add-tasks-to-job), discusses hello usage of hello container SAS.</span></span>

> [!TIP]
> <span data-ttu-id="d52d7-228">Extraction de série en deux parties hello sur les signatures d’accès partagé, [partie 1 : modèle de présentation hello SAP](../storage/common/storage-dotnet-shared-access-signature-part-1.md) et [partie 2 : créer et utiliser une SAP avec hello service Blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn plus de fournir un accès sécurisé toodata dans votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="d52d7-228">Check out hello two-part series on shared access signatures, [Part 1: Understanding hello SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) and [Part 2: Create and use a SAS with hello Blob service](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn more about providing secure access toodata in your Storage account.</span></span>
>
>

## <a name="step-3-create-batch-pool"></a><span data-ttu-id="d52d7-229">Étape 3 : créer le pool Batch</span><span class="sxs-lookup"><span data-stu-id="d52d7-229">Step 3: Create Batch pool</span></span>
<span data-ttu-id="d52d7-230">![Créer un pool Batch][3]
</span><span class="sxs-lookup"><span data-stu-id="d52d7-230">![Create a Batch pool][3]
</span></span><br/>

<span data-ttu-id="d52d7-231">Un **pool** Batch est une collection de nœuds de calcul (machines virtuelles) sur lequel Batch exécute les tâches d’un travail.</span><span class="sxs-lookup"><span data-stu-id="d52d7-231">A Batch **pool** is a collection of compute nodes (virtual machines) on which Batch executes a job's tasks.</span></span>

<span data-ttu-id="d52d7-232">Une fois qu’il télécharge hello tâche script et les données de fichiers toohello compte de stockage, *python_tutorial_client.py* démarre son interaction avec le service de traitement par lots hello à l’aide du module de traitement par lots Python hello.</span><span class="sxs-lookup"><span data-stu-id="d52d7-232">After it uploads hello task script and data files toohello Storage account, *python_tutorial_client.py* starts its interaction with hello Batch service by using hello Batch Python module.</span></span> <span data-ttu-id="d52d7-233">toodo, un [BatchServiceClient] [ py_batchserviceclient] est créé :</span><span class="sxs-lookup"><span data-stu-id="d52d7-233">toodo so, a [BatchServiceClient][py_batchserviceclient] is created:</span></span>

```python
# Create a Batch service client. We'll now be interacting with hello Batch
# service in addition tooStorage.
credentials = batchauth.SharedKeyCredentials(BATCH_ACCOUNT_NAME,
                                             BATCH_ACCOUNT_KEY)

batch_client = batch.BatchServiceClient(
    credentials,
    base_url=BATCH_ACCOUNT_URL)
```

<span data-ttu-id="d52d7-234">Ensuite, un pool de nœuds de calcul est créé dans hello compte Batch avec un appel trop`create_pool`.</span><span class="sxs-lookup"><span data-stu-id="d52d7-234">Next, a pool of compute nodes is created in hello Batch account with a call too`create_pool`.</span></span>

```python
def create_pool(batch_service_client, pool_id,
                resource_files, publisher, offer, sku):
    """
    Creates a pool of compute nodes with hello specified OS settings.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str pool_id: An ID for hello new pool.
    :param list resource_files: A collection of resource files for hello pool's
    start task.
    :param str publisher: Marketplace image publisher
    :param str offer: Marketplace image offer
    :param str sku: Marketplace image sku
    """
    print('Creating pool [{}]...'.format(pool_id))

    # Create a new pool of Linux compute nodes using an Azure Virtual Machines
    # Marketplace image. For more information about creating pools of Linux
    # nodes, see:
    # https://azure.microsoft.com/documentation/articles/batch-linux-nodes/

    # Specify hello commands for hello pool's start task. hello start task is run
    # on each node as it joins hello pool, and when it's rebooted or re-imaged.
    # We use hello start task tooprep hello node for running our task script.
    task_commands = [
        # Copy hello python_tutorial_task.py script toohello "shared" directory
        # that all tasks that run on hello node have access to.
        'cp -r $AZ_BATCH_TASK_WORKING_DIR/* $AZ_BATCH_NODE_SHARED_DIR',
        # Install pip and hello dependencies for cryptography
        'apt-get update',
        'apt-get -y install python-pip',
        'apt-get -y install build-essential libssl-dev libffi-dev python-dev',
        # Install hello azure-storage module so that hello task script can access
        # Azure Blob storage
        'pip install azure-storage']

    # Get hello node agent SKU and image reference for hello virtual machine
    # configuration.
    # For more information about hello virtual machine configuration, see:
    # https://azure.microsoft.com/documentation/articles/batch-linux-nodes/
    sku_to_use, image_ref_to_use = \
        common.helpers.select_latest_verified_vm_image_with_node_agent_sku(
            batch_service_client, publisher, offer, sku)

    new_pool = batch.models.PoolAddParameter(
        id=pool_id,
        virtual_machine_configuration=batchmodels.VirtualMachineConfiguration(
            image_reference=image_ref_to_use,
            node_agent_sku_id=sku_to_use),
        vm_size=_POOL_VM_SIZE,
        target_dedicated=_POOL_NODE_COUNT,
        start_task=batch.models.StartTask(
            command_line=
            common.helpers.wrap_commands_in_shell('linux', task_commands),
            run_elevated=True,
            wait_for_success=True,
            resource_files=resource_files),
        )

    try:
        batch_service_client.pool.add(new_pool)
    except batchmodels.batch_error.BatchErrorException as err:
        print_batch_exception(err)
        raise
```

<span data-ttu-id="d52d7-235">Lorsque vous créez un pool, vous définissez un [PoolAddParameter] [ py_pooladdparam] qui spécifie plusieurs propriétés pour le pool de hello :</span><span class="sxs-lookup"><span data-stu-id="d52d7-235">When you create a pool, you define a [PoolAddParameter][py_pooladdparam] that specifies several properties for hello pool:</span></span>

* <span data-ttu-id="d52d7-236">**ID** de pool de hello (*id* - requis)</span><span class="sxs-lookup"><span data-stu-id="d52d7-236">**ID** of hello pool (*id* - required)</span></span><p/><span data-ttu-id="d52d7-237">Comme pour la plupart des entités dans Batch, votre nouveau pool doit avoir un ID unique au sein de votre compte Batch.</span><span class="sxs-lookup"><span data-stu-id="d52d7-237">As with most entities in Batch, your new pool must have a unique ID within your Batch account.</span></span> <span data-ttu-id="d52d7-238">Votre code fait référence à l’aide de son ID de pool de toothis, et c’est la façon dont vous identifiez pool hello Bonjour Azure [portal][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="d52d7-238">Your code refers toothis pool using its ID, and it's how you identify hello pool in hello Azure [portal][azure_portal].</span></span>
* <span data-ttu-id="d52d7-239">**Nombre de nœuds de calcul** (*target_dedicated* - obligatoire)</span><span class="sxs-lookup"><span data-stu-id="d52d7-239">**Number of compute nodes** (*target_dedicated* - required)</span></span><p/><span data-ttu-id="d52d7-240">Cette propriété spécifie le nombre de machines virtuelles doivent être déployés dans le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="d52d7-240">This property specifies how many VMs should be deployed in hello pool.</span></span> <span data-ttu-id="d52d7-241">Il est important toonote que tous les comptes de traitement par lots ont une valeur par défaut **quota** que limites hello nombre de **cœurs** (et par conséquent, les nœuds de calcul) dans un compte de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="d52d7-241">It is important toonote that all Batch accounts have a default **quota** that limits hello number of **cores** (and thus, compute nodes) in a Batch account.</span></span> <span data-ttu-id="d52d7-242">Vous trouverez les quotas par défaut hello et obtenir des instructions sur la façon de trop[un quota de](batch-quota-limit.md#increase-a-quota) (par exemple, le nombre maximal de hello de cœurs dans votre compte Batch) dans [Quotas et limites pour hello service Azure Batch](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="d52d7-242">You can find hello default quotas and instructions on how too[increase a quota](batch-quota-limit.md#increase-a-quota) (such as hello maximum number of cores in your Batch account) in [Quotas and limits for hello Azure Batch service](batch-quota-limit.md).</span></span> <span data-ttu-id="d52d7-243">Si vous vous demandez pourquoi votre pool n’atteint pas plus de X nœuds,</span><span class="sxs-lookup"><span data-stu-id="d52d7-243">If you find yourself asking "Why won't my pool reach more than X nodes?"</span></span> <span data-ttu-id="d52d7-244">Ce quota de base peut être la cause de hello.</span><span class="sxs-lookup"><span data-stu-id="d52d7-244">this core quota may be hello cause.</span></span>
* <span data-ttu-id="d52d7-245">**Système d’exploitation** pour les nœuds (*virtual_machine_configuration***ou***cloud_service_configuration* - obligatoire)</span><span class="sxs-lookup"><span data-stu-id="d52d7-245">**Operating system** for nodes (*virtual_machine_configuration* **or** *cloud_service_configuration* - required)</span></span><p/><span data-ttu-id="d52d7-246">Dans *python_tutorial_client.py*, nous créons un pool de nœuds Linux à l’aide de [VirtualMachineConfiguration][py_vm_config].</span><span class="sxs-lookup"><span data-stu-id="d52d7-246">In *python_tutorial_client.py*, we create a pool of Linux nodes using a [VirtualMachineConfiguration][py_vm_config].</span></span> <span data-ttu-id="d52d7-247">Hello `select_latest_verified_vm_image_with_node_agent_sku` fonctionner dans `common.helpers` simplifie l’utilisation de [Azure Marketplace de Machines virtuelles] [ vm_marketplace] images.</span><span class="sxs-lookup"><span data-stu-id="d52d7-247">hello `select_latest_verified_vm_image_with_node_agent_sku` function in `common.helpers` simplifies working with [Azure Virtual Machines Marketplace][vm_marketplace] images.</span></span> <span data-ttu-id="d52d7-248">Pour plus d’informations sur l’utilisation des images du Marketplace, voir [Configurer des nœuds de calcul Linux dans des pools Azure Batch](batch-linux-nodes.md) .</span><span class="sxs-lookup"><span data-stu-id="d52d7-248">See [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) for more information about using Marketplace images.</span></span>
* <span data-ttu-id="d52d7-249">**Taille des nœuds de calcul** (*vm_size* - obligatoire)</span><span class="sxs-lookup"><span data-stu-id="d52d7-249">**Size of compute nodes** (*vm_size* - required)</span></span><p/><span data-ttu-id="d52d7-250">Étant donné que nous spécifions des nœuds Linux pour notre [VirtualMachineConfiguration][py_vm_config], nous spécifions une taille de machine virtuelle (`STANDARD_A1` dans cet exemple) parmi les [tailles des machines virtuelles dans Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d52d7-250">Since we're specifying Linux nodes for our [VirtualMachineConfiguration][py_vm_config], we specify a VM size (`STANDARD_A1` in this sample) from [Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="d52d7-251">Pour plus d’informations, voir [Configurer des nœuds de calcul Linux dans des pools Azure Batch](batch-linux-nodes.md) .</span><span class="sxs-lookup"><span data-stu-id="d52d7-251">Again, see [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) for more information.</span></span>
* <span data-ttu-id="d52d7-252">**Tâche de démarrage** (*start_task* : non obligatoire)</span><span class="sxs-lookup"><span data-stu-id="d52d7-252">**Start task** (*start_task* - not required)</span></span><p/><span data-ttu-id="d52d7-253">En même temps que hello au-dessus des propriétés d’un nœud physique, vous pouvez également spécifier un [StartTask] [ py_starttask] pour le pool hello (il n’est pas obligatoire).</span><span class="sxs-lookup"><span data-stu-id="d52d7-253">Along with hello above physical node properties, you may also specify a [StartTask][py_starttask] for hello pool (it is not required).</span></span> <span data-ttu-id="d52d7-254">Hello StartTask s’exécute sur chaque nœud de ce nœud rejoint le pool de hello, chaque fois qu’un nœud est redémarré.</span><span class="sxs-lookup"><span data-stu-id="d52d7-254">hello StartTask executes on each node as that node joins hello pool, and each time a node is restarted.</span></span> <span data-ttu-id="d52d7-255">Hello StartTask est particulièrement utile pour la préparation des nœuds de calcul pour l’exécution de hello de tâches, telles que l’installation d’applications hello qui exécutent des tâches.</span><span class="sxs-lookup"><span data-stu-id="d52d7-255">hello StartTask is especially useful for preparing compute nodes for hello execution of tasks, such as installing hello applications that your tasks run.</span></span><p/><span data-ttu-id="d52d7-256">Dans cet exemple d’application, hello StartTask copie les fichiers de hello qu’il télécharge à partir du stockage (qui sont spécifié à l’aide de hello StartTask **resource_files** propriété) à partir de hello StartTask *répertoire de travail* toohello *partagé* Active toutes les tâches en cours d’exécution sur le nœud de hello peuvent accéder.</span><span class="sxs-lookup"><span data-stu-id="d52d7-256">In this sample application, hello StartTask copies hello files that it downloads from Storage (which are specified by using hello StartTask's **resource_files** property) from hello StartTask *working directory* toohello *shared* directory that all tasks running on hello node can access.</span></span> <span data-ttu-id="d52d7-257">Pour l’essentiel, cette copie `python_tutorial_task.py` toohello répertoire partagé sur chaque nœud comme nœud de hello rejoint le pool de hello, afin que toutes les tâches qui s’exécutent sur le nœud de hello puissent y accéder.</span><span class="sxs-lookup"><span data-stu-id="d52d7-257">Essentially, this copies `python_tutorial_task.py` toohello shared directory on each node as hello node joins hello pool, so that any tasks that run on hello node can access it.</span></span>

<span data-ttu-id="d52d7-258">Vous pouvez remarquer hello appel toohello `wrap_commands_in_shell` fonction d’assistance.</span><span class="sxs-lookup"><span data-stu-id="d52d7-258">You may notice hello call toohello `wrap_commands_in_shell` helper function.</span></span> <span data-ttu-id="d52d7-259">Cette fonction prend une collection de commandes distinctes et crée une ligne de commande unique adaptée à la propriété de ligne de commande d’une tâche.</span><span class="sxs-lookup"><span data-stu-id="d52d7-259">This function takes a collection of separate commands and creates a single command line appropriate for a task's command-line property.</span></span>

<span data-ttu-id="d52d7-260">Remarquables dans l’extrait de code hello ci-dessus est également utiliser deux variables d’environnement Bonjour hello **lettre** propriété Hello StartTask : `AZ_BATCH_TASK_WORKING_DIR` et `AZ_BATCH_NODE_SHARED_DIR`.</span><span class="sxs-lookup"><span data-stu-id="d52d7-260">Also notable in hello code snippet above is hello use of two environment variables in hello **command_line** property of hello StartTask: `AZ_BATCH_TASK_WORKING_DIR` and `AZ_BATCH_NODE_SHARED_DIR`.</span></span> <span data-ttu-id="d52d7-261">Chaque nœud de calcul au sein d’un pool de traitement par lots est automatiquement configuré avec plusieurs variables d’environnement qui sont tooBatch spécifique.</span><span class="sxs-lookup"><span data-stu-id="d52d7-261">Each compute node within a Batch pool is automatically configured with several environment variables that are specific tooBatch.</span></span> <span data-ttu-id="d52d7-262">Tout processus qui est exécutée par une tâche a des variables d’environnement toothese accès.</span><span class="sxs-lookup"><span data-stu-id="d52d7-262">Any process that is executed by a task has access toothese environment variables.</span></span>

> [!TIP]
> <span data-ttu-id="d52d7-263">toofind plus d’informations sur les variables d’environnement hello qui sont disponibles sur les nœuds de calcul dans un pool de traitement par lots, ainsi que les informations sur les répertoires de travail tâche, consultez **paramètres d’environnement pour les tâches** et **fichiers et répertoires**  Bonjour [vue d’ensemble des fonctionnalités de traitement par lots Azure](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="d52d7-263">toofind out more about hello environment variables that are available on compute nodes in a Batch pool, as well as information on task working directories, see **Environment settings for tasks** and **Files and directories** in hello [overview of Azure Batch features](batch-api-basics.md).</span></span>
>
>

## <a name="step-4-create-batch-job"></a><span data-ttu-id="d52d7-264">Étape 4 : créer un travail Batch</span><span class="sxs-lookup"><span data-stu-id="d52d7-264">Step 4: Create Batch job</span></span>
<span data-ttu-id="d52d7-265">![Créer un travail Batch][4]</span><span class="sxs-lookup"><span data-stu-id="d52d7-265">![Create Batch job][4]</span></span><br/>

<span data-ttu-id="d52d7-266">Un **travail** Batch constitue un ensemble de tâches et est associé à un pool de nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="d52d7-266">A Batch **job** is a collection of tasks, and is associated with a pool of compute nodes.</span></span> <span data-ttu-id="d52d7-267">tâches de Hello dans un travail s’exécutent sur les nœuds de calcul du pool hello associé.</span><span class="sxs-lookup"><span data-stu-id="d52d7-267">hello tasks in a job execute on hello associated pool's compute nodes.</span></span>

<span data-ttu-id="d52d7-268">Vous pouvez utiliser une tâche pour l’organisation et le suivi des tâches dans les charges de travail, mais également pour imposer certaines contraintes--par exemple hello durée d’exécution pour le travail de hello (et par extension, ses tâches) et priorité des travaux dans les tâches de tooother de relation dans hello compte Batch.</span><span class="sxs-lookup"><span data-stu-id="d52d7-268">You can use a job not only for organizing and tracking tasks in related workloads, but also for imposing certain constraints--such as hello maximum runtime for hello job (and by extension, its tasks) and job priority in relation tooother jobs in hello Batch account.</span></span> <span data-ttu-id="d52d7-269">Dans cet exemple, toutefois, les travaux de hello est associé uniquement à pool hello qui a été créé à l’étape 3 de #.</span><span class="sxs-lookup"><span data-stu-id="d52d7-269">In this example, however, hello job is associated only with hello pool that was created in step #3.</span></span> <span data-ttu-id="d52d7-270">Aucune propriété supplémentaire n’est configurée.</span><span class="sxs-lookup"><span data-stu-id="d52d7-270">No additional properties are configured.</span></span>

<span data-ttu-id="d52d7-271">Tous les travaux Batch sont associés à un pool spécifique.</span><span class="sxs-lookup"><span data-stu-id="d52d7-271">All Batch jobs are associated with a specific pool.</span></span> <span data-ttu-id="d52d7-272">Cette association indique les nœuds d’exécutent des tâches du travail hello sur.</span><span class="sxs-lookup"><span data-stu-id="d52d7-272">This association indicates which nodes hello job's tasks execute on.</span></span> <span data-ttu-id="d52d7-273">Vous spécifiez un pool de hello à l’aide de hello [PoolInformation] [ py_poolinfo] propriété, comme indiqué dans l’extrait de code hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d52d7-273">You specify hello pool by using hello [PoolInformation][py_poolinfo] property, as shown in hello code snippet below.</span></span>

```python
def create_job(batch_service_client, job_id, pool_id):
    """
    Creates a job with hello specified ID, associated with hello specified pool.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello ID for hello job.
    :param str pool_id: hello ID for hello pool.
    """
    print('Creating job [{}]...'.format(job_id))

    job = batch.models.JobAddParameter(
        job_id,
        batch.models.PoolInformation(pool_id=pool_id))

    try:
        batch_service_client.job.add(job)
    except batchmodels.batch_error.BatchErrorException as err:
        print_batch_exception(err)
        raise
```

<span data-ttu-id="d52d7-274">Maintenant qu’un travail a été créé, les tâches sont ajoutées travail hello de tooperform.</span><span class="sxs-lookup"><span data-stu-id="d52d7-274">Now that a job has been created, tasks are added tooperform hello work.</span></span>

## <a name="step-5-add-tasks-toojob"></a><span data-ttu-id="d52d7-275">Étape 5 : Ajouter des tâches toojob</span><span class="sxs-lookup"><span data-stu-id="d52d7-275">Step 5: Add tasks toojob</span></span>
<span data-ttu-id="d52d7-276">![Ajouter des tâches toojob][5]</span><span class="sxs-lookup"><span data-stu-id="d52d7-276">![Add tasks toojob][5]</span></span><br/><span data-ttu-id="d52d7-277">
*(1) tâches sont ajoutés toohello travail, tâches de hello (2) sont planifiée toorun sur les nœuds et les tâches hello (3) téléchargement tooprocess de fichiers de données hello*</span><span class="sxs-lookup"><span data-stu-id="d52d7-277">
*(1) Tasks are added toohello job, (2) hello tasks are scheduled toorun on nodes, and (3) hello tasks download hello data files tooprocess*</span></span>

<span data-ttu-id="d52d7-278">Lot **tâches** sont des nœuds de calcul hello unités de travail individuelles qui s’exécutent sur hello.</span><span class="sxs-lookup"><span data-stu-id="d52d7-278">Batch **tasks** are hello individual units of work that execute on hello compute nodes.</span></span> <span data-ttu-id="d52d7-279">Une tâche a une ligne de commande et exécute les scripts hello ou exécutables que vous spécifiez dans cette ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="d52d7-279">A task has a command line and runs hello scripts or executables that you specify in that command line.</span></span>

<span data-ttu-id="d52d7-280">tooactually effectuer un travail, de tâches doivent être ajoutées à une tâche tooa.</span><span class="sxs-lookup"><span data-stu-id="d52d7-280">tooactually perform work, tasks must be added tooa job.</span></span> <span data-ttu-id="d52d7-281">Chaque [CloudTask] [ py_task] est configuré avec une propriété de ligne de commande et [ResourceFiles] [ py_resource_file] (comme avec la tâche de début du pool hello) que hello tâche télécharge toohello nœud avant sa ligne de commande est exécutée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="d52d7-281">Each [CloudTask][py_task] is configured with a command-line property and [ResourceFiles][py_resource_file] (as with hello pool's StartTask) that hello task downloads toohello node before its command line is automatically executed.</span></span> <span data-ttu-id="d52d7-282">Dans l’exemple hello, chaque tâche traite un seul fichier.</span><span class="sxs-lookup"><span data-stu-id="d52d7-282">In hello sample, each task processes only one file.</span></span> <span data-ttu-id="d52d7-283">Par conséquent, sa collection ResourceFiles contient un seul élément.</span><span class="sxs-lookup"><span data-stu-id="d52d7-283">Thus, its ResourceFiles collection contains a single element.</span></span>

```python
def add_tasks(batch_service_client, job_id, input_files,
              output_container_name, output_container_sas_token):
    """
    Adds a task for each input file in hello collection toohello specified job.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello ID of hello job toowhich tooadd hello tasks.
    :param list input_files: A collection of input files. One task will be
     created for each input file.
    :param output_container_name: hello ID of an Azure Blob storage container to
    which hello tasks will upload their results.
    :param output_container_sas_token: A SAS token granting write access to
    hello specified Azure Blob storage container.
    """

    print('Adding {} tasks toojob [{}]...'.format(len(input_files), job_id))

    tasks = list()

    for input_file in input_files:

        command = ['python $AZ_BATCH_NODE_SHARED_DIR/python_tutorial_task.py '
                   '--filepath {} --numwords {} --storageaccount {} '
                   '--storagecontainer {} --sastoken "{}"'.format(
                    input_file.file_path,
                    '3',
                    _STORAGE_ACCOUNT_NAME,
                    output_container_name,
                    output_container_sas_token)]

        tasks.append(batch.models.TaskAddParameter(
                'topNtask{}'.format(input_files.index(input_file)),
                wrap_commands_in_shell('linux', command),
                resource_files=[input_file]
                )
        )

    batch_service_client.task.add_collection(job_id, tasks)
```

> [!IMPORTANT]
> <span data-ttu-id="d52d7-284">Lorsque leur accès aux variables d’environnement telles que `$AZ_BATCH_NODE_SHARED_DIR` ou exécuter une application introuvable dans du nœud hello `PATH`, lignes de commande de tâche doit appeler hello interface explicitement, comme avec `/bin/sh -c MyTaskApplication $MY_ENV_VAR`.</span><span class="sxs-lookup"><span data-stu-id="d52d7-284">When they access environment variables such as `$AZ_BATCH_NODE_SHARED_DIR` or execute an application not found in hello node's `PATH`, task command lines must invoke hello shell explicitly, such as with `/bin/sh -c MyTaskApplication $MY_ENV_VAR`.</span></span> <span data-ttu-id="d52d7-285">Cette exigence n’est pas nécessaire si vos tâches exécutent une application dans du nœud hello `PATH` et ne font pas référence à des variables d’environnement.</span><span class="sxs-lookup"><span data-stu-id="d52d7-285">This requirement is unnecessary if your tasks execute an application in hello node's `PATH` and do not reference any environment variables.</span></span>
>
>

<span data-ttu-id="d52d7-286">Au sein de hello `for` boucle dans l’extrait de code hello ci-dessus, vous pouvez voir que la ligne de commande hello pour la tâche hello est construite avec cinq arguments de ligne de commande qui sont passés trop*python_tutorial_task.py*:</span><span class="sxs-lookup"><span data-stu-id="d52d7-286">Within hello `for` loop in hello code snippet above, you can see that hello command line for hello task is constructed with five command-line arguments that are passed too*python_tutorial_task.py*:</span></span>

1. <span data-ttu-id="d52d7-287">**FilePath**: il s’agit hello chemin d’accès local toohello fichier tel qu’il existe sur le nœud de hello.</span><span class="sxs-lookup"><span data-stu-id="d52d7-287">**filepath**: This is hello local path toohello file as it exists on hello node.</span></span> <span data-ttu-id="d52d7-288">Lorsque hello objet ResourceFile dans `upload_file_to_container` a été créé à l’étape 2 ci-dessus, le nom de fichier hello a été utilisée pour cette propriété (hello `file_path` paramètre hello ResourceFile constructeur).</span><span class="sxs-lookup"><span data-stu-id="d52d7-288">When hello ResourceFile object in `upload_file_to_container` was created in Step 2 above, hello file name was used for this property (hello `file_path` parameter in hello ResourceFile constructor).</span></span> <span data-ttu-id="d52d7-289">Cela indique que hello fichier se trouve dans hello même nœud hello en tant que répertoire *python_tutorial_task.py*.</span><span class="sxs-lookup"><span data-stu-id="d52d7-289">This indicates that hello file can be found in hello same directory on hello node as *python_tutorial_task.py*.</span></span>
2. <span data-ttu-id="d52d7-290">**NUMWORDS**: haut de hello *N* mots doivent être écrits en fichier de sortie toohello.</span><span class="sxs-lookup"><span data-stu-id="d52d7-290">**numwords**: hello top *N* words should be written toohello output file.</span></span>
3. <span data-ttu-id="d52d7-291">**storageaccount**: nom hello Hello compte de stockage qui est propriétaire du résultat de la tâche hello conteneur toowhich hello doit être téléchargé.</span><span class="sxs-lookup"><span data-stu-id="d52d7-291">**storageaccount**: hello name of hello Storage account that owns hello container toowhich hello task output should be uploaded.</span></span>
4. <span data-ttu-id="d52d7-292">**storagecontainer**: nom de hello Hello de toowhich de conteneur de stockage hello sortie de fichiers doivent être téléchargés.</span><span class="sxs-lookup"><span data-stu-id="d52d7-292">**storagecontainer**: hello name of hello Storage container toowhich hello output files should be uploaded.</span></span>
5. <span data-ttu-id="d52d7-293">**sastoken**: signature hello accès partagé (SAP) qui fournit un accès en écriture toohello **sortie** conteneur dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="d52d7-293">**sastoken**: hello shared access signature (SAS) that provides write access toohello **output** container in Azure Storage.</span></span> <span data-ttu-id="d52d7-294">Hello *python_tutorial_task.py* script utilise cette signature d’accès partagé lorsque crée sa référence BlockBlobService.</span><span class="sxs-lookup"><span data-stu-id="d52d7-294">hello *python_tutorial_task.py* script uses this shared access signature when creates its BlockBlobService reference.</span></span> <span data-ttu-id="d52d7-295">Cela fournit un accès en écriture toohello conteneur sans nécessiter une clé d’accès pour le compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="d52d7-295">This provides write access toohello container without requiring an access key for hello storage account.</span></span>

```python
# NOTE: Taken from python_tutorial_task.py

# Create hello blob client using hello container's SAS token.
# This allows us toocreate a client that provides write
# access only toohello container.
blob_client = azureblob.BlockBlobService(account_name=args.storageaccount,
                                         sas_token=args.sastoken)
```

## <a name="step-6-monitor-tasks"></a><span data-ttu-id="d52d7-296">Étape 6 : surveiller les tâches</span><span class="sxs-lookup"><span data-stu-id="d52d7-296">Step 6: Monitor tasks</span></span>
<span data-ttu-id="d52d7-297">![Surveiller les tâches][6]</span><span class="sxs-lookup"><span data-stu-id="d52d7-297">![Monitor tasks][6]</span></span><br/><span data-ttu-id="d52d7-298">
*Hello tâches hello moniteurs (1) pour l’état d’achèvement et les tâches hello (2) téléchargement tooAzure de données de résultat stockage*</span><span class="sxs-lookup"><span data-stu-id="d52d7-298">
*hello script (1) monitors hello tasks for completion status, and (2) hello tasks upload result data tooAzure Storage*</span></span>

<span data-ttu-id="d52d7-299">Lorsque les tâches sont ajoutées tooa travail, ils sont en file d’attente et planifiés pour l’exécution sur des nœuds de calcul dans le pool hello associé hello travail automatiquement.</span><span class="sxs-lookup"><span data-stu-id="d52d7-299">When tasks are added tooa job, they are automatically queued and scheduled for execution on compute nodes within hello pool associated with hello job.</span></span> <span data-ttu-id="d52d7-300">Selon les paramètres que vous spécifiez hello, lot gère queuing à toutes les tâches, la planification, une nouvelle tentative et autres tâches d’administration de tâche pour vous.</span><span class="sxs-lookup"><span data-stu-id="d52d7-300">Based on hello settings you specify, Batch handles all task queuing, scheduling, retrying, and other task administration duties for you.</span></span>

<span data-ttu-id="d52d7-301">Il existe de nombreuses approches toomonitoring exécution de la tâche.</span><span class="sxs-lookup"><span data-stu-id="d52d7-301">There are many approaches toomonitoring task execution.</span></span> <span data-ttu-id="d52d7-302">Hello `wait_for_tasks_to_complete` fonctionner dans *python_tutorial_client.py* fournit un exemple simple de tâches de surveillance pour un certain état, dans ce cas, hello [terminé] [ py_taskstate] état.</span><span class="sxs-lookup"><span data-stu-id="d52d7-302">hello `wait_for_tasks_to_complete` function in *python_tutorial_client.py* provides a simple example of monitoring tasks for a certain state, in this case, hello [completed][py_taskstate] state.</span></span>

```python
def wait_for_tasks_to_complete(batch_service_client, job_id, timeout):
    """
    Returns when all tasks in hello specified job reach hello Completed state.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello id of hello job whose tasks should be toomonitored.
    :param timedelta timeout: hello duration toowait for task completion. If all
    tasks in hello specified job do not reach Completed state within this time
    period, an exception will be raised.
    """
    timeout_expiration = datetime.datetime.now() + timeout

    print("Monitoring all tasks for 'Completed' state, timeout in {}..."
          .format(timeout), end='')

    while datetime.datetime.now() < timeout_expiration:
        print('.', end='')
        sys.stdout.flush()
        tasks = batch_service_client.task.list(job_id)

        incomplete_tasks = [task for task in tasks if
                            task.state != batchmodels.TaskState.completed]
        if not incomplete_tasks:
            print()
            return True
        else:
            time.sleep(1)

    print()
    raise RuntimeError("ERROR: Tasks did not reach 'Completed' state within "
                       "timeout period of " + str(timeout))
```

## <a name="step-7-download-task-output"></a><span data-ttu-id="d52d7-303">Étape 7 : télécharger la sortie des tâches</span><span class="sxs-lookup"><span data-stu-id="d52d7-303">Step 7: Download task output</span></span>
<span data-ttu-id="d52d7-304">![Télécharger la sortie des tâches à partir du service Stockage][7]</span><span class="sxs-lookup"><span data-stu-id="d52d7-304">![Download task output from Storage][7]</span></span><br/>

<span data-ttu-id="d52d7-305">Maintenant que hello tâche terminée, sortie hello des tâches de hello peut être téléchargé depuis le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="d52d7-305">Now that hello job is completed, hello output from hello tasks can be downloaded from Azure Storage.</span></span> <span data-ttu-id="d52d7-306">Cette opération s’effectue avec un appel trop`download_blobs_from_container` dans *python_tutorial_client.py*:</span><span class="sxs-lookup"><span data-stu-id="d52d7-306">This is done with a call too`download_blobs_from_container` in *python_tutorial_client.py*:</span></span>

```python
def download_blobs_from_container(block_blob_client,
                                  container_name, directory_path):
    """
    Downloads all blobs from hello specified Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param container_name: hello Azure Blob storage container from which to
     download files.
    :param directory_path: hello local directory toowhich toodownload hello files.
    """
    print('Downloading all files from container [{}]...'.format(
        container_name))

    container_blobs = block_blob_client.list_blobs(container_name)

    for blob in container_blobs.items:
        destination_file_path = os.path.join(directory_path, blob.name)

        block_blob_client.get_blob_to_path(container_name,
                                           blob.name,
                                           destination_file_path)

        print('  Downloaded blob [{}] from container [{}] too{}'.format(
            blob.name,
            container_name,
            destination_file_path))

    print('  Download complete!')
```

> [!NOTE]
> <span data-ttu-id="d52d7-307">Hello appel trop`download_blobs_from_container` dans *python_tutorial_client.py* Spécifie que les fichiers hello doivent être téléchargé tooyour répertoire de base.</span><span class="sxs-lookup"><span data-stu-id="d52d7-307">hello call too`download_blobs_from_container` in *python_tutorial_client.py* specifies that hello files should be downloaded tooyour home directory.</span></span> <span data-ttu-id="d52d7-308">Pensez toomodify libre cette sortie d’emplacement.</span><span class="sxs-lookup"><span data-stu-id="d52d7-308">Feel free toomodify this output location.</span></span>
>
>

## <a name="step-8-delete-containers"></a><span data-ttu-id="d52d7-309">Étape 8 : supprimer les conteneurs</span><span class="sxs-lookup"><span data-stu-id="d52d7-309">Step 8: Delete containers</span></span>
<span data-ttu-id="d52d7-310">Vous êtes facturé pour les données qui résident dans le stockage Azure, il est toujours un tooremove recommandé que tous les objets BLOB qui ne sont plus nécessaires pour vos traitements par lots.</span><span class="sxs-lookup"><span data-stu-id="d52d7-310">Because you are charged for data that resides in Azure Storage, it is always a good idea tooremove any blobs that are no longer needed for your Batch jobs.</span></span> <span data-ttu-id="d52d7-311">Dans *python_tutorial_client.py*, cette opération s’effectue avec trois appels trop[BlockBlobService.delete_container][py_delete_container]:</span><span class="sxs-lookup"><span data-stu-id="d52d7-311">In *python_tutorial_client.py*, this is done with three calls too[BlockBlobService.delete_container][py_delete_container]:</span></span>

```python
# Clean up storage resources
print('Deleting containers...')
blob_client.delete_container(app_container_name)
blob_client.delete_container(input_container_name)
blob_client.delete_container(output_container_name)
```

## <a name="step-9-delete-hello-job-and-hello-pool"></a><span data-ttu-id="d52d7-312">Étape 9 : Supprimer le travail de hello et pool de hello</span><span class="sxs-lookup"><span data-stu-id="d52d7-312">Step 9: Delete hello job and hello pool</span></span>
<span data-ttu-id="d52d7-313">À l’étape finale de hello, vous êtes le pool de travail et hello de hello toodelete demandées qui ont été créés par hello *python_tutorial_client.py* script.</span><span class="sxs-lookup"><span data-stu-id="d52d7-313">In hello final step, you are prompted toodelete hello job and hello pool that were created by hello *python_tutorial_client.py* script.</span></span> <span data-ttu-id="d52d7-314">Bien que vous ne soyez pas facturé pour les travaux et les tâches à proprement parler, les nœuds de calcul vous *sont* facturés.</span><span class="sxs-lookup"><span data-stu-id="d52d7-314">Although you are not charged for jobs and tasks themselves, you *are* charged for compute nodes.</span></span> <span data-ttu-id="d52d7-315">Par conséquent, nous vous conseillons d’affecter les nœuds uniquement en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="d52d7-315">Thus, we recommend that you allocate nodes only as needed.</span></span> <span data-ttu-id="d52d7-316">La suppression des pools inutilisés peut être incluse dans votre processus de maintenance.</span><span class="sxs-lookup"><span data-stu-id="d52d7-316">Deleting unused pools can be part of your maintenance process.</span></span>

<span data-ttu-id="d52d7-317">Hello BatchServiceClient [JobOperations] [ py_job] et [PoolOperations] [ py_pool] ont tous deux des méthodes de suppression correspondantes, qui sont appelé si vous confirmez la suppression :</span><span class="sxs-lookup"><span data-stu-id="d52d7-317">hello BatchServiceClient's [JobOperations][py_job] and [PoolOperations][py_pool] both have corresponding deletion methods, which are called if you confirm deletion:</span></span>

```python
# Clean up Batch resources (if hello user so chooses).
if query_yes_no('Delete job?') == 'yes':
    batch_client.job.delete(_JOB_ID)

if query_yes_no('Delete pool?') == 'yes':
    batch_client.pool.delete(_POOL_ID)
```

> [!IMPORTANT]
> <span data-ttu-id="d52d7-318">N’oubliez pas que les ressources de calcul vous sont facturées et que la suppression des pools inutilisés vous permet de réduire les coûts.</span><span class="sxs-lookup"><span data-stu-id="d52d7-318">Keep in mind that you are charged for compute resources--deleting unused pools will minimize cost.</span></span> <span data-ttu-id="d52d7-319">En outre, n’oubliez pas que la suppression d’un pool supprime tous les nœuds de calcul dans ce pool, et que toutes les données sur les nœuds hello seront irrécupérables après la suppression d’un pool de hello.</span><span class="sxs-lookup"><span data-stu-id="d52d7-319">Also, be aware that deleting a pool deletes all compute nodes within that pool, and that any data on hello nodes will be unrecoverable after hello pool is deleted.</span></span>
>
>

## <a name="run-hello-sample-script"></a><span data-ttu-id="d52d7-320">Exécutez le script d’exemple hello</span><span class="sxs-lookup"><span data-stu-id="d52d7-320">Run hello sample script</span></span>
<span data-ttu-id="d52d7-321">Lorsque vous exécutez hello *python_tutorial_client.py* script à partir du didacticiel de hello [exemple de code][github_article_samples], la sortie de console hello est similaire toohello suivant.</span><span class="sxs-lookup"><span data-stu-id="d52d7-321">When you run hello *python_tutorial_client.py* script from hello tutorial [code sample][github_article_samples], hello console output is similar toohello following.</span></span> <span data-ttu-id="d52d7-322">Il existe une pause à `Monitoring all tasks for 'Completed' state, timeout in 0:20:00...` tandis que les nœuds de calcul du pool hello sont créés, démarré, et la tâche de démarrage du pool hello hello commandes est exécutées.</span><span class="sxs-lookup"><span data-stu-id="d52d7-322">There is a pause at `Monitoring all tasks for 'Completed' state, timeout in 0:20:00...` while hello pool's compute nodes are created, started, and hello commands in hello pool's start task are executed.</span></span> <span data-ttu-id="d52d7-323">Hello d’utilisation [portail Azure] [ azure_portal] toomonitor votre pool, nœuds de calcul, tâche et pendant et après l’exécution des tâches.</span><span class="sxs-lookup"><span data-stu-id="d52d7-323">Use hello [Azure portal][azure_portal] toomonitor your pool, compute nodes, job, and tasks during and after execution.</span></span> <span data-ttu-id="d52d7-324">Hello d’utilisation [portail Azure] [ azure_portal] ou hello [Microsoft Azure Storage Explorer] [ storage_explorer] tooview les ressources de stockage hello (conteneurs et objets BLOB) qui sont créés par l’application hello.</span><span class="sxs-lookup"><span data-stu-id="d52d7-324">Use hello [Azure portal][azure_portal] or hello [Microsoft Azure Storage Explorer][storage_explorer] tooview hello Storage resources (containers and blobs) that are created by hello application.</span></span>

> [!TIP]
> <span data-ttu-id="d52d7-325">Exécutez hello *python_tutorial_client.py* script à partir de hello `azure-batch-samples/Python/Batch/article_samples` active.</span><span class="sxs-lookup"><span data-stu-id="d52d7-325">Run hello *python_tutorial_client.py* script from within hello `azure-batch-samples/Python/Batch/article_samples` directory.</span></span> <span data-ttu-id="d52d7-326">Il utilise un chemin d’accès relatif pour hello `common.helpers` importation du module, vous voyez `ImportError: No module named 'common'` si vous n’exécutez pas script hello à partir de ce répertoire.</span><span class="sxs-lookup"><span data-stu-id="d52d7-326">It uses a relative path for hello `common.helpers` module import, so you might see `ImportError: No module named 'common'` if you don't run hello script from within this directory.</span></span>
>
>

<span data-ttu-id="d52d7-327">Temps d’exécution par défaut est **environ 5 à 7 minutes** lorsque vous exécutez exemple hello dans sa configuration par défaut.</span><span class="sxs-lookup"><span data-stu-id="d52d7-327">Typical execution time is **approximately 5-7 minutes** when you run hello sample in its default configuration.</span></span>

```
Sample start: 2016-05-20 22:47:10

Uploading file /home/user/py_tutorial/python_tutorial_task.py toocontainer [application]...
Uploading file /home/user/py_tutorial/data/taskdata1.txt toocontainer [input]...
Uploading file /home/user/py_tutorial/data/taskdata2.txt toocontainer [input]...
Uploading file /home/user/py_tutorial/data/taskdata3.txt toocontainer [input]...
Creating pool [PythonTutorialPool]...
Creating job [PythonTutorialJob]...
Adding 3 tasks toojob [PythonTutorialJob]...
Monitoring all tasks for 'Completed' state, timeout in 0:20:00..........................................................................
  Success! All tasks reached hello 'Completed' state within hello specified timeout period.
Downloading all files from container [output]...
  Downloaded blob [taskdata1_OUTPUT.txt] from container [output] too/home/user/taskdata1_OUTPUT.txt
  Downloaded blob [taskdata2_OUTPUT.txt] from container [output] too/home/user/taskdata2_OUTPUT.txt
  Downloaded blob [taskdata3_OUTPUT.txt] from container [output] too/home/user/taskdata3_OUTPUT.txt
  Download complete!
Deleting containers...

Sample end: 2016-05-20 22:53:12
Elapsed time: 0:06:02

Delete job? [Y/n]
Delete pool? [Y/n]

Press ENTER tooexit...
```

## <a name="next-steps"></a><span data-ttu-id="d52d7-328">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d52d7-328">Next steps</span></span>
<span data-ttu-id="d52d7-329">Estimez les modifications toomake libre trop*python_tutorial_client.py* et *python_tutorial_task.py* tooexperiment avec différents scénarios de calcul.</span><span class="sxs-lookup"><span data-stu-id="d52d7-329">Feel free toomake changes too*python_tutorial_client.py* and *python_tutorial_task.py* tooexperiment with different compute scenarios.</span></span> <span data-ttu-id="d52d7-330">Par exemple, essayez d’ajouter un délai d’exécution trop*python_tutorial_task.py* toosimulate longue des tâches et les surveiller dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="d52d7-330">For example, try adding an execution delay too*python_tutorial_task.py* toosimulate long-running tasks and monitor them in hello portal.</span></span> <span data-ttu-id="d52d7-331">Essayez d’ajouter des tâches plus ou en ajustant de nombre hello de nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="d52d7-331">Try adding more tasks or adjusting hello number of compute nodes.</span></span> <span data-ttu-id="d52d7-332">Ajouter toocheck logique pour autoriser l’utilisation de hello de durée d’exécution de toospeed pool existant</span><span class="sxs-lookup"><span data-stu-id="d52d7-332">Add logic toocheck for and allow hello use of an existing pool toospeed execution time.</span></span>

<span data-ttu-id="d52d7-333">Maintenant que vous êtes familiarisé avec les flux de travail de base hello d’une solution de traitement par lots, il est toodig de temps dans toohello des fonctionnalités supplémentaires de hello service Batch.</span><span class="sxs-lookup"><span data-stu-id="d52d7-333">Now that you're familiar with hello basic workflow of a Batch solution, it's time toodig in toohello additional features of hello Batch service.</span></span>

* <span data-ttu-id="d52d7-334">Hello de révision [les fonctionnalités de présentation d’Azure Batch](batch-api-basics.md) article, nous vous recommandons de si vous êtes de nouveau service toohello.</span><span class="sxs-lookup"><span data-stu-id="d52d7-334">Review hello [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new toohello service.</span></span>
* <span data-ttu-id="d52d7-335">Démarrer sur hello autres articles de développement de lot sous **développement approfondie** Bonjour [cursus lot][batch_learning_path].</span><span class="sxs-lookup"><span data-stu-id="d52d7-335">Start on hello other Batch development articles under **Development in-depth** in hello [Batch learning path][batch_learning_path].</span></span>
* <span data-ttu-id="d52d7-336">Extraire une implémentation différente du traitement de charge de travail hello « N premiers mots » traitement par lots Bonjour [TopNWords] [ github_topnwords] exemple.</span><span class="sxs-lookup"><span data-stu-id="d52d7-336">Check out a different implementation of processing hello "top N words" workload with Batch in hello [TopNWords][github_topnwords] sample.</span></span>

[azure_batch]: https://azure.microsoft.com/services/batch/
[azure_free_account]: https://azure.microsoft.com/free/
[azure_portal]: https://portal.azure.com
[batch_learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[blog_linux]: http://blogs.technet.com/b/windowshpc/archive/2016/03/30/introducing-linux-support-on-azure-batch.aspx
[crypto]: https://cryptography.io/en/latest/
[crypto_install]: https://cryptography.io/en/latest/installation/
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[github_topnwords]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/TopNWords
[github_article_samples]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch/article_samples

[nuget_packagemgr]: https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c
[nuget_restore]: https://docs.nuget.org/consume/package-restore/msbuild-integrated#enabling-package-restore-during-build

[py_account_ops]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations
[py_azure_sdk]: https://pypi.python.org/pypi/azure
[py_batch_docs]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.html
[py_batch_package]: https://pypi.python.org/pypi/azure-batch
[py_batchserviceclient]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.html#azure.batch.BatchServiceClient
[py_blockblobservice]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.blockblobservice.html#azure.storage.blob.blockblobservice.BlockBlobService
[py_cloudtask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudTask
[py_computenodeuser]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.models.html#azure.batch.models.ComputeNodeUser
[py_cs_config]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudServiceConfiguration
[py_delete_container]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.delete_container
[py_gen_blob_sas]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.generate_blob_shared_access_signature
[py_gen_container_sas]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.generate_container_shared_access_signature
[py_image_ref]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_imagereference]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_job]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.JobOperations
[py_jobpreptask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.JobPreparationTask
[py_jobreltask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.JobReleaseTask
[py_list_skus]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations.list_node_agent_skus
[py_make_blob_url]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.make_blob_url
[py_pool]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.PoolOperations
[py_pooladdparam]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.PoolAddParameter
[py_poolinfo]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.PoolInformation
[py_resource_file]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.ResourceFile
[py_samples_github]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch/
[py_starttask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.StartTask
[py_starttask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.StartTask
[py_task]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudTask
[py_taskstate]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.TaskState
[py_vm_config]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.VirtualMachineConfiguration
[pypi_batch]: https://pypi.python.org/pypi/azure-batch
[pypi_storage]: https://pypi.python.org/pypi/azure-storage
[pypi_install]: https://packaging.python.org/installing/
[storage_explorer]: http://storageexplorer.com/
[visual_studio]: https://www.visualstudio.com/products/vs-2015-product-editions
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/

[1]: ./media/batch-python-tutorial/batch_workflow_01_sm.png "Créer des conteneurs dans le Stockage Azure"
[2]: ./media/batch-python-tutorial/batch_workflow_02_sm.png "Tâche de chargement d’application et d’entrée (données) des fichiers toocontainers"
[3]: ./media/batch-python-tutorial/batch_workflow_03_sm.png "Créer un pool Batch"
[4]: ./media/batch-python-tutorial/batch_workflow_04_sm.png "Créer un travail Batch"
[5]: ./media/batch-python-tutorial/batch_workflow_05_sm.png "Ajouter des tâches toojob"
[6]: ./media/batch-python-tutorial/batch_workflow_06_sm.png "Surveiller les tâches"
[7]: ./media/batch-python-tutorial/batch_workflow_07_sm.png "Télécharger la sortie des tâches à partir de Storage"
[8]: ./media/batch-python-tutorial/batch_workflow_sm.png "Flux de travail de la solution Batch (diagramme complet)"
[9]: ./media/batch-python-tutorial/credentials_batch_sm.png "Informations d’identification de compte Batch dans le portail"
[10]: ./media/batch-python-tutorial/credentials_storage_sm.png "Informations d’identification de compte de stockage dans le portail"
[11]: ./media/batch-python-tutorial/batch_workflow_minimal_sm.png "Flux de travail de la solution Batch (diagramme minimal)"
