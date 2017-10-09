---
title: "aaaUse PowerShell tooget main d’Azure Data Lake Store | Documents Microsoft"
description: "Utiliser Azure PowerShell toocreate un compte Data Lake Store et effectuer des opérations de base"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: bf85f369-f9aa-4ca1-9ae7-e03a78eb7290
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 9c958bfd63e412ec0b0a4113a149f61aee026bc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-powershell"></a><span data-ttu-id="0e6ea-103">Prise en main d'Azure Data Lake Store avec Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0e6ea-103">Get started with Azure Data Lake Store using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0e6ea-104">Portail</span><span class="sxs-lookup"><span data-stu-id="0e6ea-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="0e6ea-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0e6ea-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="0e6ea-106">Kit SDK .NET</span><span class="sxs-lookup"><span data-stu-id="0e6ea-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="0e6ea-107">Kit SDK Java</span><span class="sxs-lookup"><span data-stu-id="0e6ea-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="0e6ea-108">API REST</span><span class="sxs-lookup"><span data-stu-id="0e6ea-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="0e6ea-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0e6ea-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="0e6ea-110">Node.JS</span><span class="sxs-lookup"><span data-stu-id="0e6ea-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="0e6ea-111">Python</span><span class="sxs-lookup"><span data-stu-id="0e6ea-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="0e6ea-112">Découvrez comment toouse Azure PowerShell toocreate stocker une Azure Data Lake compte et effectuer des opérations de base telles que la création de dossiers, téléchargent et téléchargement les fichiers de données, supprimez votre compte, un etc.. Pour plus d’informations sur Data Lake Store, consultez [Vue d’ensemble de Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0e6ea-112">Learn how toouse Azure PowerShell toocreate an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e6ea-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0e6ea-113">Prerequisites</span></span>
<span data-ttu-id="0e6ea-114">Avant de commencer ce didacticiel, vous devez disposer de hello :</span><span class="sxs-lookup"><span data-stu-id="0e6ea-114">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="0e6ea-115">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-115">**An Azure subscription**.</span></span> <span data-ttu-id="0e6ea-116">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0e6ea-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="0e6ea-117">**Azure PowerShell 1.0 ou version ultérieure**.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-117">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="0e6ea-118">Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0e6ea-118">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="authentication"></a><span data-ttu-id="0e6ea-119">Authentification</span><span class="sxs-lookup"><span data-stu-id="0e6ea-119">Authentication</span></span>
<span data-ttu-id="0e6ea-120">Cet article utilise une approche plus simple de l’authentification avec Data Lake Store où vous êtes invité à tooenter vos informations d’identification de compte Azure.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-120">This article uses a simpler authentication approach with Data Lake Store where you are prompted tooenter your Azure account credentials.</span></span> <span data-ttu-id="0e6ea-121">Hello accès niveau tooData Lake Store compte de système de fichiers et est ensuite régie par niveau d’accès hello Hello à l’utilisateur connecté.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-121">hello access level tooData Lake Store account and file system is then governed by hello access level of hello logged in user.</span></span> <span data-ttu-id="0e6ea-122">Toutefois, il existe d’autres approches en tant que bien tooauthenticate avec Data Lake Store, qui sont **l’authentification de l’utilisateur final** ou **l’authentification de service**.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-122">However, there are other approaches as well tooauthenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="0e6ea-123">Pour plus d’informations sur la façon d’et tooauthenticate, consultez [l’authentification de l’utilisateur final](data-lake-store-end-user-authenticate-using-active-directory.md) ou [l’authentification de service](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="0e6ea-123">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="create-an-azure-data-lake-store-account"></a><span data-ttu-id="0e6ea-124">Créer un compte Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="0e6ea-124">Create an Azure Data Lake Store account</span></span>
1. <span data-ttu-id="0e6ea-125">À partir de votre bureau, ouvrez une nouvelle fenêtre de Windows PowerShell et entrez hello suivant toolog extrait dans tooyour compte Azure, définissez hello abonnement et hello Data Lake Store fournisseur.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-125">From your desktop, open a new Windows PowerShell window, and enter hello following snippet toolog in tooyour Azure account, set hello subscription, and register hello Data Lake Store provider.</span></span> <span data-ttu-id="0e6ea-126">Toolog demandée, assurez-vous que vous connectez en tant qu’un des admininistrators/propriétaire de l’abonnement hello :</span><span class="sxs-lookup"><span data-stu-id="0e6ea-126">When prompted toolog in, make sure you log in as one of hello subscription admininistrators/owner:</span></span>

        # Log in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Azure Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"
2. <span data-ttu-id="0e6ea-127">Un compte Azure Data Lake Store est associé à un groupe de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-127">An Azure Data Lake Store account is associated with an Azure Resource Group.</span></span> <span data-ttu-id="0e6ea-128">Commencez par créer un groupe de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-128">Start by creating an Azure Resource Group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="0e6ea-129">![Créer un groupe de ressources Azure](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Créer un groupe de ressources Azure")</span><span class="sxs-lookup"><span data-stu-id="0e6ea-129">![Create an Azure Resource Group](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Create an Azure Resource Group")</span></span>
3. <span data-ttu-id="0e6ea-130">Créer un compte Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-130">Create an Azure Data Lake Store account.</span></span> <span data-ttu-id="0e6ea-131">nom Hello que vous spécifiez doit uniquement contenir des lettres minuscules et chiffres.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-131">hello name you specify must only contain lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="0e6ea-132">![Créer un compte Azure Data Lake Store](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Créer un compte Azure Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="0e6ea-132">![Create an Azure Data Lake Store account](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Create an Azure Data Lake Store account")</span></span>
4. <span data-ttu-id="0e6ea-133">Vérifiez que le compte de hello a été créé.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-133">Verify that hello account is successfully created.</span></span>

        Test-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

    <span data-ttu-id="0e6ea-134">Hello pour cela doit être de sortie **True**.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-134">hello output for this should be **True**.</span></span>

## <a name="create-directory-structures-in-your-azure-data-lake-store"></a><span data-ttu-id="0e6ea-135">Créer des structures de répertoires dans votre Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="0e6ea-135">Create directory structures in your Azure Data Lake Store</span></span>
<span data-ttu-id="0e6ea-136">Vous pouvez créer des répertoires sous votre toomanage de compte Azure Data Lake Store et stocker des données.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-136">You can create directories under your Azure Data Lake Store account toomanage and store data.</span></span>

1. <span data-ttu-id="0e6ea-137">Spécifiez un répertoire racine.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-137">Specify a root directory.</span></span>

        $myrootdir = "/"
2. <span data-ttu-id="0e6ea-138">Créer un nouveau répertoire nommé **mynewdirectory** sous la racine spécifiée de hello.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-138">Create a new directory called **mynewdirectory** under hello specified root.</span></span>

        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/mynewdirectory
3. <span data-ttu-id="0e6ea-139">Vérifiez que ce répertoire hello est créé avec succès.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-139">Verify that hello new directory is successfully created.</span></span>

        Get-AzureRmDataLakeStoreChildItem -AccountName $dataLakeStoreName -Path $myrootdir

    <span data-ttu-id="0e6ea-140">Il doit afficher une sortie semblable à hello suivante :</span><span class="sxs-lookup"><span data-stu-id="0e6ea-140">It should show an output like hello following:</span></span>

    <span data-ttu-id="0e6ea-141">![Vérifier le répertoire](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "Vérifier le répertoire")</span><span class="sxs-lookup"><span data-stu-id="0e6ea-141">![Verify Directory](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "Verify Directory")</span></span>

## <a name="upload-data-tooyour-azure-data-lake-store"></a><span data-ttu-id="0e6ea-142">Télécharger des données tooyour Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="0e6ea-142">Upload data tooyour Azure Data Lake Store</span></span>
<span data-ttu-id="0e6ea-143">Vous pouvez télécharger votre tooData de data Lake Store directement dans le répertoire de niveau ou tooa de racine hello que vous avez créé dans le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-143">You can upload your data tooData Lake Store directly at hello root level or tooa directory that you created within hello account.</span></span> <span data-ttu-id="0e6ea-144">Hello d’extraits de code ci-dessous montrent comment tooupload un répertoire toohello de données exemple (**mynewdirectory**) vous avez créé dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-144">hello snippets below demonstrate how tooupload some sample data toohello directory (**mynewdirectory**) you created in hello previous section.</span></span>

<span data-ttu-id="0e6ea-145">Si vous recherchez des tooupload de données d’exemple, vous pouvez obtenir hello **Ambulance données** dossier hello [référentiel Git de LAC de données Azure](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="0e6ea-145">If you are looking for some sample data tooupload, you can get hello **Ambulance Data** folder from hello [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span> <span data-ttu-id="0e6ea-146">Télécharger le fichier de hello et stockez-le dans un répertoire local sur votre ordinateur, telles que C:\sampledata\.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-146">Download hello file and store it in a local directory on your computer, such as  C:\sampledata\.</span></span>

    Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\sampledata\vehicle1_09142014.csv" -Destination $myrootdir\mynewdirectory\vehicle1_09142014.csv


## <a name="rename-download-and-delete-data-from-your-data-lake-store"></a><span data-ttu-id="0e6ea-147">Renommer, télécharger et supprimer des données de votre Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="0e6ea-147">Rename, download, and delete data from your Data Lake Store</span></span>
<span data-ttu-id="0e6ea-148">toorename un fichier, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="0e6ea-148">toorename a file, use hello following command:</span></span>

    Move-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014.csv -Destination $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

<span data-ttu-id="0e6ea-149">toodownload un fichier, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="0e6ea-149">toodownload a file, use hello following command:</span></span>

    Export-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv -Destination "C:\sampledata\vehicle1_09142014_Copy.csv"

<span data-ttu-id="0e6ea-150">toodelete un fichier, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="0e6ea-150">toodelete a file, use hello following command:</span></span>

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

<span data-ttu-id="0e6ea-151">Lorsque vous y êtes invité, entrez **Y** élément hello de toodelete.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-151">When prompted, enter **Y** toodelete hello item.</span></span> <span data-ttu-id="0e6ea-152">Si vous avez plusieurs fichiers toodelete, vous pouvez fournir tous les chemins d’accès de hello séparés par des virgules.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-152">If you have more than one file toodelete, you can provide all hello paths separated by comma.</span></span>

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014.csv, $myrootdir\mynewdirectoryvehicle1_09142014_Copy.csv

## <a name="delete-your-azure-data-lake-store-account"></a><span data-ttu-id="0e6ea-153">Supprimer votre compte Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="0e6ea-153">Delete your Azure Data Lake Store account</span></span>
<span data-ttu-id="0e6ea-154">Utilisez hello suivant commande toodelete votre compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-154">Use hello following command toodelete your Data Lake Store account.</span></span>

    Remove-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

<span data-ttu-id="0e6ea-155">Lorsque vous y êtes invité, entrez **Y** compte de hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-155">When prompted, enter **Y** toodelete hello account.</span></span>

## <a name="performance-guidance-while-using-powershell"></a><span data-ttu-id="0e6ea-156">Guide des performances lors de l’utilisation de PowerShell</span><span class="sxs-lookup"><span data-stu-id="0e6ea-156">Performance guidance while using PowerShell</span></span>

<span data-ttu-id="0e6ea-157">Voici les paramètres importants qui peuvent être analysées tooget hello meilleures performances lors de l’utilisation de PowerShell toowork avec Data Lake Store hello :</span><span class="sxs-lookup"><span data-stu-id="0e6ea-157">Below are hello most important settings that can be tuned tooget hello best performance while using PowerShell toowork with Data Lake Store:</span></span>

| <span data-ttu-id="0e6ea-158">Propriété</span><span class="sxs-lookup"><span data-stu-id="0e6ea-158">Property</span></span>            | <span data-ttu-id="0e6ea-159">Default</span><span class="sxs-lookup"><span data-stu-id="0e6ea-159">Default</span></span> | <span data-ttu-id="0e6ea-160">Description</span><span class="sxs-lookup"><span data-stu-id="0e6ea-160">Description</span></span> |
|---------------------|---------|-------------|
| <span data-ttu-id="0e6ea-161">PerFileThreadCount</span><span class="sxs-lookup"><span data-stu-id="0e6ea-161">PerFileThreadCount</span></span>  | <span data-ttu-id="0e6ea-162">10</span><span class="sxs-lookup"><span data-stu-id="0e6ea-162">10</span></span>      | <span data-ttu-id="0e6ea-163">Ce paramètre vous permet de nombre de hello toochoose de threads parallèles pour le chargement ou téléchargement de chaque fichier.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-163">This parameter enables you toochoose hello number of parallel threads for uploading or downloading each file.</span></span> <span data-ttu-id="0e6ea-164">Ce nombre représente hello nombre max. de threads qui peut être alloués par fichier, mais vous risquez d’obtenir moins de threads en fonction de votre scénario (par exemple, si vous téléchargez un fichier de 1 Ko, vous obtiendrez un thread même si vous demander de 20 threads).</span><span class="sxs-lookup"><span data-stu-id="0e6ea-164">This number represents hello max threads that can be allocated per file, but you may get less threads depending on your scenario (e.g. if you are uploading a 1KB file, you will get one thread even if you ask for 20 threads).</span></span>  |
| <span data-ttu-id="0e6ea-165">ConcurrentFileCount</span><span class="sxs-lookup"><span data-stu-id="0e6ea-165">ConcurrentFileCount</span></span> | <span data-ttu-id="0e6ea-166">10</span><span class="sxs-lookup"><span data-stu-id="0e6ea-166">10</span></span>      | <span data-ttu-id="0e6ea-167">Ce paramètre est spécifique au chargement ou au téléchargement des dossiers.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-167">This parameter is specifically for uploading or downloading folders.</span></span> <span data-ttu-id="0e6ea-168">Ce paramètre détermine le nombre hello des fichiers simultanées qui peuvent être téléchargés ou téléchargé.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-168">This parameter determines hello number of concurrent files that can be uploaded or downloaded.</span></span> <span data-ttu-id="0e6ea-169">Ce nombre représente le nombre maximal de hello des fichiers simultanées qui peuvent être téléchargés ou téléchargé en même temps, mais vous risquez d’obtenir moins d’accès concurrentiel en fonction de votre scénario (par exemple, si vous téléchargez les deux fichiers, vous obtiendrez deux téléchargements de fichier simultanées même si vous demandez 15).</span><span class="sxs-lookup"><span data-stu-id="0e6ea-169">This number represents hello maximum number of concurrent files that can be uploaded or downloaded at one time, but you may get less concurrency depending on your scenario (e.g. if you are uploading two files, you will get two concurrent file uploads even if you ask for 15).</span></span> |

<span data-ttu-id="0e6ea-170">**Exemple**</span><span class="sxs-lookup"><span data-stu-id="0e6ea-170">**Example**</span></span>

<span data-ttu-id="0e6ea-171">Cette commande télécharge les fichiers de disque local de l’utilisateur d’Azure Data Lake Store toohello à l’aide de 20 threads par fichier et 100 fichiers simultanées.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-171">This command downloads files from Azure Data Lake Store toohello user's local drive using 20 threads per file and 100 concurrent files.</span></span>

    Export-AzureRmDataLakeStoreItem -AccountName <Data Lake Store account name> -PerFileThreadCount 20-ConcurrentFileCount 100 -Path /Powershell/100GB/ -Destination C:\Performance\ -Force -Recurse

### <a name="how-do-i-determine-hello-value-tooset-for-these-parameters"></a><span data-ttu-id="0e6ea-172">Comment déterminer les tooset de valeur hello pour ces paramètres ?</span><span class="sxs-lookup"><span data-stu-id="0e6ea-172">How do I determine hello value tooset for these parameters?</span></span>

<span data-ttu-id="0e6ea-173">Voici quelques conseils à suivre.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-173">Here's some guidance that you can use.</span></span>

* <span data-ttu-id="0e6ea-174">**Étape 1 : Déterminer le nombre total de threads de hello** -vous devez commencer par le calcul toouse de nombre total de threads hello.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-174">**Step 1: Determine hello total thread count** - You should start by calculating hello total thread count toouse.</span></span> <span data-ttu-id="0e6ea-175">En règle générale, vous devez utiliser 6 threads pour chaque noyau physique.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-175">As a general guideline, you should use 6 threads for each physical core.</span></span>

        Total thread count = total physical cores * 6

    <span data-ttu-id="0e6ea-176">**Exemple**</span><span class="sxs-lookup"><span data-stu-id="0e6ea-176">**Example**</span></span>

    <span data-ttu-id="0e6ea-177">En supposant que Hello PowerShell sont en cours d’exécution des commandes à partir d’une machine virtuelle D14 qui possède 16 cœurs</span><span class="sxs-lookup"><span data-stu-id="0e6ea-177">Assuming you are running hello PowerShell commands from a D14 VM that has 16 cores</span></span>

        Total thread count = 16 cores * 6 = 96 threads


* <span data-ttu-id="0e6ea-178">**Étape 2 : Calculer PerFileThreadCount** -nous calculons notre PerFileThreadCount en fonction de taille hello des fichiers de hello.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-178">**Step 2: Calculate PerFileThreadCount**  - We calculate our PerFileThreadCount based on hello size of hello files.</span></span> <span data-ttu-id="0e6ea-179">Pour les fichiers inférieures à 2,5 Go, n’est pas toochange besoin de ce paramètre car hello comme valeur par défaut 10 est suffisante.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-179">For files smaller than 2.5GB, there is no need toochange this parameter because hello default of 10 is sufficient.</span></span> <span data-ttu-id="0e6ea-180">Pour les fichiers de plus de 2,5 Go, vous devez utiliser 10 threads base hello pour hello première 2,5 Go et ajouter 1 thread de chaque augmentation de 256 Mo supplémentaires pour une taille de fichier.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-180">For files larger than 2.5GB, you should use 10 threads as hello base for hello first 2.5GB and add 1 thread for each additional 256MB increase in file size.</span></span> <span data-ttu-id="0e6ea-181">Si vous copiez un dossier contenant différentes tailles de fichiers, envisagez de regrouper ces fichiers par tailles similaires.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-181">If you are copying a folder with a large range of file sizes, consider grouping them into similar file sizes.</span></span> <span data-ttu-id="0e6ea-182">Les différentes tailles de fichiers ne permettent pas d’obtenir des performances optimales.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-182">Having dissimilar file sizes may cause non-optimal performance.</span></span> <span data-ttu-id="0e6ea-183">Si cela est possible toogroup les tailles de fichiers similaires, vous devez définir PerFileThreadCount selon la taille de fichier maximale hello.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-183">If that's not possible toogroup similar file sizes, you should set PerFileThreadCount based on hello largest file size.</span></span>

        PerFileThreadCount = 10 threads for hello first 2.5GB + 1 thread for each additional 256MB increase in file size

    <span data-ttu-id="0e6ea-184">**Exemple**</span><span class="sxs-lookup"><span data-stu-id="0e6ea-184">**Example**</span></span>

    <span data-ttu-id="0e6ea-185">En supposant que vous avez 100 fichiers allant de 1 Go too10GB, nous utilisons hello 10 Go comme hello plus grande taille de l’équation, ce qui indiquerait hello suivante du fichier.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-185">Assuming you have 100 files ranging from 1GB too10GB, we use hello 10GB as hello largest file size for equation, which would read like hello following.</span></span>

        PerFileThreadCount = 10 + ((10GB - 2.5GB) / 256MB) = 40 threads

* <span data-ttu-id="0e6ea-186">**Étape 3 : Calculer ConcurrentFilecount** -utiliser le nombre total de threads hello et PerFileThreadCount toocalculate ConcurrentFileCount selon hello suivant l’équation.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-186">**Step 3: Calculate ConcurrentFilecount** - Use hello total thread count and PerFileThreadCount toocalculate ConcurrentFileCount based on hello following equation.</span></span>

        Total thread count = PerFileThreadCount * ConcurrentFileCount

    <span data-ttu-id="0e6ea-187">**Exemple**</span><span class="sxs-lookup"><span data-stu-id="0e6ea-187">**Example**</span></span>

    <span data-ttu-id="0e6ea-188">Selon les valeurs de l’exemple hello que nous avons utilisé</span><span class="sxs-lookup"><span data-stu-id="0e6ea-188">Based on hello example values we have been using</span></span>

        96 = 40 * ConcurrentFileCount

    <span data-ttu-id="0e6ea-189">Par conséquent, **ConcurrentFileCount** est **2.4**, ce qui nous pouvons arrondir trop**2**.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-189">So, **ConcurrentFileCount** is **2.4**, which we can round off too**2**.</span></span>

### <a name="further-tuning"></a><span data-ttu-id="0e6ea-190">Paramétrage supplémentaire</span><span class="sxs-lookup"><span data-stu-id="0e6ea-190">Further tuning</span></span>

<span data-ttu-id="0e6ea-191">Vous pouvez avoir besoin de davantage de paramétrage, car il existe une plage de toowork de tailles de fichier avec.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-191">You might require further tuning because there is a range of file sizes toowork with.</span></span> <span data-ttu-id="0e6ea-192">Hello au-dessus de calcul fonctionne bien si toutes ou la plupart des fichiers de hello est la plage de 10 Go toohello et que le plus proche.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-192">hello above calculation works well if all or most of hello files are larger and closer toohello 10GB range.</span></span> <span data-ttu-id="0e6ea-193">Par contre, s’il y a beaucoup de tailles de fichiers différentes et que la plupart des fichiers sont parmi les plus petits, vous pouvez réduire PerFileThreadCount.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-193">If instead, there are many different files sizes with many files being smaller, then you could reduce PerFileThreadCount.</span></span> <span data-ttu-id="0e6ea-194">En réduisant hello PerFileThreadCount, nous pouvons augmenter ConcurrentFileCount.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-194">By reducing hello PerFileThreadCount, we can increase ConcurrentFileCount.</span></span> <span data-ttu-id="0e6ea-195">Par conséquent, si nous partons du principe que la plupart de ses fichiers est plus petite dans la plage de 5 Go hello, nous pouvons refaire la notre calcul :</span><span class="sxs-lookup"><span data-stu-id="0e6ea-195">So, if we assume that most of our files are smaller in hello 5GB range, we can re-do our calculation:</span></span>

    PerFileThreadCount = 10 + ((5GB - 2.5GB) / 256MB) = 20

<span data-ttu-id="0e6ea-196">Par conséquent, **ConcurrentFileCount** sera désormais 96/20, ce qui est 4.8, arrondie trop**4**.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-196">So, **ConcurrentFileCount** will now be 96/20, which is 4.8, rounded off too**4**.</span></span>

<span data-ttu-id="0e6ea-197">Vous pouvez continuer tootune ces paramètres en modifiant hello **PerFileThreadCount** haut et bas en fonction de distribution hello votre de tailles de fichier.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-197">You can continue tootune these settings by changing hello **PerFileThreadCount** up and down depending on hello distribution of your file sizes.</span></span>

### <a name="limitation"></a><span data-ttu-id="0e6ea-198">Limitation</span><span class="sxs-lookup"><span data-stu-id="0e6ea-198">Limitation</span></span>

* <span data-ttu-id="0e6ea-199">**Nombre de fichiers est inférieure à ConcurrentFileCount**: si le nombre de hello de fichiers que vous chargez est inférieure à hello **ConcurrentFileCount** que vous avez calculé, puis vous devez réduire  **ConcurrentFileCount** nombre égal toohello de toobe de fichiers.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-199">**Number of files is less than ConcurrentFileCount**: If hello number of files you are uploading is smaller than hello **ConcurrentFileCount** that you calculated, then you should reduce **ConcurrentFileCount** toobe equal toohello number of files.</span></span> <span data-ttu-id="0e6ea-200">Vous pouvez utiliser n’importe quel tooincrease de threads restants **PerFileThreadCount**.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-200">You can use any remaining threads tooincrease **PerFileThreadCount**.</span></span>

* <span data-ttu-id="0e6ea-201">**Trop de threads**: Si vous augmentez le thread trop sans augmenter la taille de votre cluster, vous courez risque hello de dégradation des performances.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-201">**Too many threads**: If you increase thread count too much without increasing your cluster size, you run hello risk of degraded performance.</span></span> <span data-ttu-id="0e6ea-202">Il peut y avoir des problèmes de contention lors du basculement de contexte sur hello du processeur.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-202">There can be contention issues when context-switching on hello CPU.</span></span>

* <span data-ttu-id="0e6ea-203">**Concurrence insuffisante**: si la concurrence de hello n’est pas suffisante, puis votre cluster est peut-être trop faible.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-203">**Insufficient concurrency**: If hello concurrency is not sufficient, then your cluster may be too small.</span></span> <span data-ttu-id="0e6ea-204">Vous pouvez augmenter le nombre de hello de nœuds dans votre cluster qui vous donne plus de concurrence.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-204">You can increase hello number of nodes in your cluster which will give you more concurrency.</span></span>

* <span data-ttu-id="0e6ea-205">**Erreurs de limitation** : il se peut que vous rencontriez des erreurs de limitation si le nombre d’accès concurrentiels est trop élevé.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-205">**Throttling errors**: You may see throttling errors if your concurrency is too high.</span></span> <span data-ttu-id="0e6ea-206">Si vous rencontrez le problème de limitation, vous devez réduire d’accès concurrentiel hello ou nous contacter.</span><span class="sxs-lookup"><span data-stu-id="0e6ea-206">If you are seeing throttling errors, you should either reduce hello concurrency or contact us.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e6ea-207">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0e6ea-207">Next steps</span></span>
* [<span data-ttu-id="0e6ea-208">Sécuriser les données dans Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="0e6ea-208">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="0e6ea-209">Utiliser Azure Data Lake Analytics avec Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="0e6ea-209">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="0e6ea-210">Utiliser Azure HDInsight avec Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="0e6ea-210">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

