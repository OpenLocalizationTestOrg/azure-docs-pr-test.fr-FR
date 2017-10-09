---
title: "packages d’applications aaaInstall sur les nœuds de calcul - Azure Batch | Documents Microsoft"
description: "Utiliser la fonctionnalité packages application hello de traitement par lots Azure tooeasily gérer plusieurs applications et les nœuds de calcul des versions pour l’installation sur le lot."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 3b6044b7-5f65-4a27-9d43-71e1863d16cf
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 683be7b7f1bd5db7835332016f6dccb72f45c3b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-applications-toocompute-nodes-with-batch-application-packages"></a><span data-ttu-id="890a2-103">Déployer des nœuds de toocompute d’applications avec les packages d’applications de traitement par lots</span><span class="sxs-lookup"><span data-stu-id="890a2-103">Deploy applications toocompute nodes with Batch application packages</span></span>

<span data-ttu-id="890a2-104">fonctionnalité Hello de packages d’application de traitement par lots Azure fournit une gestion plus simple des applications de la tâche et leur toohello déploiement nœuds de calcul dans le pool.</span><span class="sxs-lookup"><span data-stu-id="890a2-104">hello application packages feature of Azure Batch provides easy management of task applications and their deployment toohello compute nodes in your pool.</span></span> <span data-ttu-id="890a2-105">Avec les packages d’application, vous pouvez télécharger et gérer plusieurs versions d’applications hello que vos tâches de s’exécuter, y compris leurs fichiers de support.</span><span class="sxs-lookup"><span data-stu-id="890a2-105">With application packages, you can upload and manage multiple versions of hello applications your tasks run, including their supporting files.</span></span> <span data-ttu-id="890a2-106">Vous pouvez ensuite automatiquement déployer une ou plusieurs de ces applications toohello nœuds de calcul dans le pool.</span><span class="sxs-lookup"><span data-stu-id="890a2-106">You can then automatically deploy one or more of these applications toohello compute nodes in your pool.</span></span>

<span data-ttu-id="890a2-107">Dans cet article, vous allez apprendre comment tooupload et gérer des packages d’application Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="890a2-107">In this article, you will learn how tooupload and manage application packages in hello Azure portal.</span></span> <span data-ttu-id="890a2-108">Vous apprendrez ensuite comment tooinstall sur d’un pool nœuds de calcul avec hello [Batch .NET] [ api_net] bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="890a2-108">You will then learn how tooinstall them on a pool's compute nodes with hello [Batch .NET][api_net] library.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="890a2-109">Les packages d’applications sont pris en charge sur tous les pools Batch créés après le 5 juillet 2017.</span><span class="sxs-lookup"><span data-stu-id="890a2-109">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="890a2-110">Elles sont prises en charge sur les pools de traitement par lots créés entre 10 mars 2016 et 5 juillet 2017 uniquement si le pool de hello a été créé à l’aide d’une configuration de Service Cloud.</span><span class="sxs-lookup"><span data-stu-id="890a2-110">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if hello pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="890a2-111">Les pools de lot créés too10 préalable mars 2016 ne gèrent pas les packages d’applications.</span><span class="sxs-lookup"><span data-stu-id="890a2-111">Batch pools created prior too10 March 2016 do not support application packages.</span></span>
>
> <span data-ttu-id="890a2-112">API pour créer et gérer des packages d’application Hello font partie de hello [Batch Management .NET] [[api_net_mgmt]] bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="890a2-112">hello APIs for creating and managing application packages are part of hello [Batch Management .NET][[api_net_mgmt]] library.</span></span> <span data-ttu-id="890a2-113">API pour l’installation des packages d’application sur un nœud de calcul Hello font partie de hello [Batch .NET] [ api_net] bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="890a2-113">hello APIs for installing application packages on a compute node are part of hello [Batch .NET][api_net] library.</span></span>  
>
> <span data-ttu-id="890a2-114">fonctionnalité de packages d’application Hello décrite ici remplace la fonctionnalité des applications Batch hello disponible dans les versions précédentes du service de hello.</span><span class="sxs-lookup"><span data-stu-id="890a2-114">hello application packages feature described here supersedes hello Batch Apps feature available in previous versions of hello service.</span></span>
> 
> 

## <a name="application-package-requirements"></a><span data-ttu-id="890a2-115">Configuration requise des packages d’application</span><span class="sxs-lookup"><span data-stu-id="890a2-115">Application package requirements</span></span>
<span data-ttu-id="890a2-116">toouse des packages d’applications, vous devez trop[lier un compte de stockage Azure](#link-a-storage-account) tooyour compte Batch.</span><span class="sxs-lookup"><span data-stu-id="890a2-116">toouse application packages, you need too[link an Azure Storage account](#link-a-storage-account) tooyour Batch account.</span></span>

<span data-ttu-id="890a2-117">Cette fonctionnalité a été introduite dans [API REST de traitement par lots] [ api_rest] version 2015-12-01.2.2). et hello correspondant [Batch .NET] [ api_net] version de la bibliothèque 3.1.0.</span><span class="sxs-lookup"><span data-stu-id="890a2-117">This feature was introduced in [Batch REST API][api_rest] version 2015-12-01.2.2 and hello corresponding [Batch .NET][api_net] library version 3.1.0.</span></span> <span data-ttu-id="890a2-118">Nous vous recommandons de toujours utiliser version plus récente de l’API hello lorsque vous travaillez avec un lot.</span><span class="sxs-lookup"><span data-stu-id="890a2-118">We recommend that you always use hello latest API version when working with Batch.</span></span>

> [!NOTE]
> <span data-ttu-id="890a2-119">Les packages d’applications sont pris en charge sur tous les pools Batch créés après le 5 juillet 2017.</span><span class="sxs-lookup"><span data-stu-id="890a2-119">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="890a2-120">Elles sont prises en charge sur les pools de traitement par lots créés entre 10 mars 2016 et 5 juillet 2017 uniquement si le pool de hello a été créé à l’aide d’une configuration de Service Cloud.</span><span class="sxs-lookup"><span data-stu-id="890a2-120">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if hello pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="890a2-121">Les pools de lot créés too10 préalable mars 2016 ne gèrent pas les packages d’applications.</span><span class="sxs-lookup"><span data-stu-id="890a2-121">Batch pools created prior too10 March 2016 do not support application packages.</span></span>
>
>

## <a name="about-applications-and-application-packages"></a><span data-ttu-id="890a2-122">Concernant les applications et les packages d’applications</span><span class="sxs-lookup"><span data-stu-id="890a2-122">About applications and application packages</span></span>
<span data-ttu-id="890a2-123">Dans le traitement par lots Azure, un *application* fait référence à set tooa des fichiers binaires avec version qui peuvent être des nœuds de calcul toohello automatiquement téléchargé dans votre pool de.</span><span class="sxs-lookup"><span data-stu-id="890a2-123">Within Azure Batch, an *application* refers tooa set of versioned binaries that can be automatically downloaded toohello compute nodes in your pool.</span></span> <span data-ttu-id="890a2-124">Un *package d’application* fait référence tooa *ensemble spécifique* des fichiers binaires et représente une donnée *version* de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="890a2-124">An *application package* refers tooa *specific set* of those binaries and represents a given *version* of hello application.</span></span>

<span data-ttu-id="890a2-125">![Diagramme détaillé sur les applications et les packages d’applications][1]</span><span class="sxs-lookup"><span data-stu-id="890a2-125">![High-level diagram of applications and application packages][1]</span></span>

### <a name="applications"></a><span data-ttu-id="890a2-126">Applications</span><span class="sxs-lookup"><span data-stu-id="890a2-126">Applications</span></span>
<span data-ttu-id="890a2-127">Une application dans le lot contient une ou plusieurs applications, packages et spécifie les options de configuration de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="890a2-127">An application in Batch contains one or more application packages and specifies configuration options for hello application.</span></span> <span data-ttu-id="890a2-128">Par exemple, une application peut spécifier hello par défaut application package version tooinstall sur les nœuds de calcul et si ses packages peuvent être mis à jour ou supprimées.</span><span class="sxs-lookup"><span data-stu-id="890a2-128">For example, an application can specify hello default application package version tooinstall on compute nodes and whether its packages can be updated or deleted.</span></span>

### <a name="application-packages"></a><span data-ttu-id="890a2-129">packages d’application</span><span class="sxs-lookup"><span data-stu-id="890a2-129">Application packages</span></span>
<span data-ttu-id="890a2-130">Un package d’application est un fichier .zip qui contient les fichiers binaires d’application hello et les fichiers de prise en charge qui sont requises pour votre application de hello toorun tâches.</span><span class="sxs-lookup"><span data-stu-id="890a2-130">An application package is a .zip file that contains hello application binaries and supporting files that are required for your tasks toorun hello application.</span></span> <span data-ttu-id="890a2-131">Chaque package d’application représente une version spécifique de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="890a2-131">Each application package represents a specific version of hello application.</span></span>

<span data-ttu-id="890a2-132">Vous pouvez spécifier les packages d’applications au niveau hello pool et des tâches.</span><span class="sxs-lookup"><span data-stu-id="890a2-132">You can specify application packages at hello pool and task levels.</span></span> <span data-ttu-id="890a2-133">Lorsque vous créez un pool ou une tâche, vous pouvez spécifier un ou plusieurs de ces packages et, le cas échéant, une version.</span><span class="sxs-lookup"><span data-stu-id="890a2-133">You can specify one or more of these packages and (optionally) a version when you create a pool or task.</span></span>

* <span data-ttu-id="890a2-134">**Les packages d’applications du pool** sont déployés trop*chaque* nœud dans le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="890a2-134">**Pool application packages** are deployed too*every* node in hello pool.</span></span> <span data-ttu-id="890a2-135">Les applications sont déployées lorsqu’un nœud rejoint un pool, et lorsqu’il est redémarré ou réinitialisé.</span><span class="sxs-lookup"><span data-stu-id="890a2-135">Applications are deployed when a node joins a pool, and when it is rebooted or reimaged.</span></span>
  
    <span data-ttu-id="890a2-136">Les packages d’application de pool sont appropriés lorsque tous les nœuds dans un pool exécutent les tâches d’un travail.</span><span class="sxs-lookup"><span data-stu-id="890a2-136">Pool application packages are appropriate when all nodes in a pool execute a job's tasks.</span></span> <span data-ttu-id="890a2-137">Vous pouvez spécifier un ou plusieurs packages d’application lorsque vous créez un pool, et vous pouvez ajouter ou mettre à jour les packages d’un pool existant.</span><span class="sxs-lookup"><span data-stu-id="890a2-137">You can specify one or more application packages when you create a pool, and you can add or update an existing pool's packages.</span></span> <span data-ttu-id="890a2-138">Si vous mettez à jour les packages d’applications d’un pool existant, vous devez redémarrer ses nœuds tooinstall hello nouveau package.</span><span class="sxs-lookup"><span data-stu-id="890a2-138">If you update an existing pool's application packages, you must restart its nodes tooinstall hello new package.</span></span>
* <span data-ttu-id="890a2-139">**Les packages d’applications de tâches** sont déployées uniquement le nœud de calcul tooa planifiée toorun une tâche, juste avant d’exécuter la ligne de commande de la tâche hello.</span><span class="sxs-lookup"><span data-stu-id="890a2-139">**Task application packages** are deployed only tooa compute node scheduled toorun a task, just before running hello task's command line.</span></span> <span data-ttu-id="890a2-140">Si hello spécifié version et le package d’application est déjà sur le nœud de hello, il n’est pas redéployé et hello les package existant est utilisé.</span><span class="sxs-lookup"><span data-stu-id="890a2-140">If hello specified application package and version is already on hello node, it is not redeployed and hello existing package is used.</span></span>
  
    <span data-ttu-id="890a2-141">Packages d’applications de tâche sont utiles dans les environnements de pool partagé, où différentes tâches sont exécutées sur un pool et pool de hello n’est pas supprimé lorsqu’un travail est terminé.</span><span class="sxs-lookup"><span data-stu-id="890a2-141">Task application packages are useful in shared-pool environments, where different jobs are run on one pool, and hello pool is not deleted when a job is completed.</span></span> <span data-ttu-id="890a2-142">Si votre travail comporte moins de tâches que les nœuds dans le pool de hello, packages d’applications de tâche peuvent réduire le transfert de données depuis votre application est déployée toohello uniquement les nœuds qui exécutent des tâches.</span><span class="sxs-lookup"><span data-stu-id="890a2-142">If your job has fewer tasks than nodes in hello pool, task application packages can minimize data transfer since your application is deployed only toohello nodes that run tasks.</span></span>
  
    <span data-ttu-id="890a2-143">Les autres scénarios pouvant tirer parti des packages d’application de tâche sont les travaux qui exécutent une application lourde, mais uniquement pour un petit nombre de tâches.</span><span class="sxs-lookup"><span data-stu-id="890a2-143">Other scenarios that can benefit from task application packages are jobs that run a large application, but for only a few tasks.</span></span> <span data-ttu-id="890a2-144">Par exemple, une étape de prétraitement ou une tâche de fusion, où les application de pré-traitement ou de fusion hello est lourd, peut-être bénéficier à l’aide de packages d’applications Office.</span><span class="sxs-lookup"><span data-stu-id="890a2-144">For example, a pre-processing stage or a merge task, where hello pre-processing or merge application is heavyweight, may benefit from using task application packages.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="890a2-145">Il existe des restrictions de nombre de hello des applications et des packages d’applications au sein d’un compte de traitement par lots et de la taille du package maximale application hello.</span><span class="sxs-lookup"><span data-stu-id="890a2-145">There are restrictions on hello number of applications and application packages within a Batch account and on hello maximum application package size.</span></span> <span data-ttu-id="890a2-146">Consultez [Quotas et limites pour hello service Azure Batch](batch-quota-limit.md) pour plus d’informations sur ces limites.</span><span class="sxs-lookup"><span data-stu-id="890a2-146">See [Quotas and limits for hello Azure Batch service](batch-quota-limit.md) for details about these limits.</span></span>
> 
> 

### <a name="benefits-of-application-packages"></a><span data-ttu-id="890a2-147">Avantages des packages d’applications</span><span class="sxs-lookup"><span data-stu-id="890a2-147">Benefits of application packages</span></span>
<span data-ttu-id="890a2-148">Les packages d’applications peuvent simplifier le code hello dans votre solution de traitement par lots et des inférieur hello généraux toomanage requis hello applications vos tâches.</span><span class="sxs-lookup"><span data-stu-id="890a2-148">Application packages can simplify hello code in your Batch solution and lower hello overhead required toomanage hello applications that your tasks run.</span></span>

<span data-ttu-id="890a2-149">Avec les packages d’application, tâche de démarrage de votre pool n’est toospecify une longue liste de tooinstall des fichiers de ressources individuels sur les nœuds hello.</span><span class="sxs-lookup"><span data-stu-id="890a2-149">With application packages, your pool's start task doesn't have toospecify a long list of individual resource files tooinstall on hello nodes.</span></span> <span data-ttu-id="890a2-150">Vous n’avez pas toomanually gérer plusieurs versions de vos fichiers d’application dans le stockage Azure, ou sur les nœuds.</span><span class="sxs-lookup"><span data-stu-id="890a2-150">You don't have toomanually manage multiple versions of your application files in Azure Storage, or on your nodes.</span></span> <span data-ttu-id="890a2-151">Et vous n’avez pas besoin de tooworry sur la génération de [URL de SAP](../storage/common/storage-dotnet-shared-access-signature-part-1.md) tooprovide toohello accéder aux fichiers de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="890a2-151">And, you don't need tooworry about generating [SAS URLs](../storage/common/storage-dotnet-shared-access-signature-part-1.md) tooprovide access toohello files in your Storage account.</span></span> <span data-ttu-id="890a2-152">Fonctionne en arrière-plan hello avec les packages d’applications Azure Storage toostore du lot et les déployer toocompute nœuds.</span><span class="sxs-lookup"><span data-stu-id="890a2-152">Batch works in hello background with Azure Storage toostore application packages and deploy them toocompute nodes.</span></span>

> [!NOTE] 
> <span data-ttu-id="890a2-153">Hello taille totale d’une tâche de démarrage doit être inférieur ou égal too32768 caractères, y compris les fichiers de ressources et les variables d’environnement.</span><span class="sxs-lookup"><span data-stu-id="890a2-153">hello total size of a start task must be less than or equal too32768 characters, including resource files and environment variables.</span></span> <span data-ttu-id="890a2-154">Si votre tâche de démarrage dépasse cette limite, l’utilisation de packages d’application est une autre option.</span><span class="sxs-lookup"><span data-stu-id="890a2-154">If your start task exceeds this limit, then using application packages is another option.</span></span> <span data-ttu-id="890a2-155">Vous pouvez également créer une archive ZIP qui contient vos fichiers de ressources, télécharger sous la forme d’un objet blob de tooAzure stockage, puis décompressez-le à partir de la ligne de commande hello de votre tâche de démarrage.</span><span class="sxs-lookup"><span data-stu-id="890a2-155">You can also create a zipped archive containing your resource files, upload it as a blob tooAzure Storage, and then unzip it from hello command line of your start task.</span></span> 
>
>

## <a name="upload-and-manage-applications"></a><span data-ttu-id="890a2-156">Téléchargement et gestion des applications</span><span class="sxs-lookup"><span data-stu-id="890a2-156">Upload and manage applications</span></span>
<span data-ttu-id="890a2-157">Vous pouvez utiliser hello [portail Azure] [ portal] ou hello [Batch Management .NET](batch-management-dotnet.md) packages d’application bibliothèque toomanage hello dans votre compte Batch.</span><span class="sxs-lookup"><span data-stu-id="890a2-157">You can use hello [Azure portal][portal] or hello [Batch Management .NET](batch-management-dotnet.md) library toomanage hello application packages in your Batch account.</span></span> <span data-ttu-id="890a2-158">Dans hello ensuite des sections suivantes, nous montrer tout d’abord comment toolink un compte de stockage, puis discutez ajoutant des applications et packages et les gérer avec hello portal.</span><span class="sxs-lookup"><span data-stu-id="890a2-158">In hello next few sections, we first show how toolink a Storage account, then discuss adding applications and packages and managing them with hello portal.</span></span>

### <a name="link-a-storage-account"></a><span data-ttu-id="890a2-159">Liaison d’un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="890a2-159">Link a Storage account</span></span>
<span data-ttu-id="890a2-160">toouse des packages d’applications, vous devez d’abord lier un tooyour de compte de stockage Azure du compte Batch.</span><span class="sxs-lookup"><span data-stu-id="890a2-160">toouse application packages, you must first link an Azure Storage account tooyour Batch account.</span></span> <span data-ttu-id="890a2-161">Si vous n’avez pas encore configuré un compte de stockage, hello portail Azure affiche un avertissement hello première fois que vous cliquez sur hello **Applications** vignette Bonjour **compte Batch** panneau.</span><span class="sxs-lookup"><span data-stu-id="890a2-161">If you have not yet configured a Storage account, hello Azure portal displays a warning hello first time you click hello **Applications** tile in hello **Batch account** blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="890a2-162">Prend en charge du lot actuellement *uniquement* hello **à usage général** type de compte de stockage comme décrit à l’étape 5, [créer un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account), dans [sur Azure comptes de stockage](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="890a2-162">Batch currently supports *only* hello **General-purpose** storage account type as described in step 5, [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account), in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="890a2-163">Lorsque vous liez un tooyour de compte de stockage Azure du compte Batch, *uniquement* un **à usage général** compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="890a2-163">When you link an Azure Storage account tooyour Batch account, link *only* a **General-purpose** storage account.</span></span>
> 
> 

<span data-ttu-id="890a2-164">![Avertissement « Aucun compte de stockage configuré » dans le portail Azure][9]</span><span class="sxs-lookup"><span data-stu-id="890a2-164">!['No storage account configured' warning in Azure portal][9]</span></span>

<span data-ttu-id="890a2-165">Hello lot service utilise hello associés toostore de compte de stockage vos packages d’application.</span><span class="sxs-lookup"><span data-stu-id="890a2-165">hello Batch service uses hello associated Storage account toostore your application packages.</span></span> <span data-ttu-id="890a2-166">Une fois que vous avez lié des deux comptes de hello, lot peut déployer automatiquement des packages de hello stockées dans les nœuds de calcul hello lié stockage compte tooyour.</span><span class="sxs-lookup"><span data-stu-id="890a2-166">After you've linked hello two accounts, Batch can automatically deploy hello packages stored in hello linked Storage account tooyour compute nodes.</span></span> <span data-ttu-id="890a2-167">toolink un tooyour de compte de stockage du compte Batch, cliquez sur **les paramètres de compte de stockage** sur hello **avertissement** panneau, puis cliquez sur **compte de stockage** sur hello **Compte de stockage** panneau.</span><span class="sxs-lookup"><span data-stu-id="890a2-167">toolink a Storage account tooyour Batch account, click **Storage account settings** on hello **Warning** blade, and then click **Storage Account** on hello **Storage Account** blade.</span></span>

<span data-ttu-id="890a2-168">![Panneau Sélectionner un compte de stockage dans le Portail Azure][10]</span><span class="sxs-lookup"><span data-stu-id="890a2-168">![Choose storage account blade in Azure portal][10]</span></span>

<span data-ttu-id="890a2-169">Nous vous recommandons de créer un compte de stockage *spécifiquement* destiné à être utilisé avec votre compte Batch et de le sélectionner ici.</span><span class="sxs-lookup"><span data-stu-id="890a2-169">We recommend that you create a Storage account *specifically* for use with your Batch account, and select it here.</span></span> <span data-ttu-id="890a2-170">Pour plus d’informations sur la façon toocreate un compte de stockage, consultez la section « Créer un compte de stockage » dans [les comptes sur le stockage Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="890a2-170">For details about how toocreate a storage account, see "Create a Storage account" in [About Azure Storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="890a2-171">Une fois que vous avez créé un compte de stockage, vous pouvez ensuite lier il tooyour lot compte à l’aide de hello **compte de stockage** panneau.</span><span class="sxs-lookup"><span data-stu-id="890a2-171">After you've created a Storage account, you can then link it tooyour Batch account by using hello **Storage Account** blade.</span></span>

> [!WARNING]
> <span data-ttu-id="890a2-172">Hello service Batch utilise le stockage Azure toostore vos packages d’application en tant qu’objets BLOB de blocs.</span><span class="sxs-lookup"><span data-stu-id="890a2-172">hello Batch service uses Azure Storage toostore your application packages as block blobs.</span></span> <span data-ttu-id="890a2-173">Vous êtes [facturé comme d’habitude] [ storage_pricing] pour les données blob de bloc hello.</span><span class="sxs-lookup"><span data-stu-id="890a2-173">You are [charged as normal][storage_pricing] for hello block blob data.</span></span> <span data-ttu-id="890a2-174">Être sûr de taille de hello tooconsider et nombre de vos packages d’application et supprimer régulièrement les coûts de toominimize déconseillées de packages.</span><span class="sxs-lookup"><span data-stu-id="890a2-174">Be sure tooconsider hello size and number of your application packages, and periodically remove deprecated packages toominimize costs.</span></span>
> 
> 

### <a name="view-current-applications"></a><span data-ttu-id="890a2-175">Affichage des applications en cours</span><span class="sxs-lookup"><span data-stu-id="890a2-175">View current applications</span></span>
<span data-ttu-id="890a2-176">applications de hello tooview dans votre compte de traitement par lots, cliquez sur hello **Applications** élément de menu dans le menu de gauche hello lors de l’affichage hello **compte Batch** panneau.</span><span class="sxs-lookup"><span data-stu-id="890a2-176">tooview hello applications in your Batch account, click hello **Applications** menu item in hello left menu while viewing hello **Batch account** blade.</span></span>

<span data-ttu-id="890a2-177">![Vignette Applications][2]</span><span class="sxs-lookup"><span data-stu-id="890a2-177">![Applications tile][2]</span></span>

<span data-ttu-id="890a2-178">Cette option de menu ouvre hello **Applications** panneau :</span><span class="sxs-lookup"><span data-stu-id="890a2-178">Selecting this menu option opens hello **Applications** blade:</span></span>

<span data-ttu-id="890a2-179">![Liste des applications][3]</span><span class="sxs-lookup"><span data-stu-id="890a2-179">![List applications][3]</span></span>

<span data-ttu-id="890a2-180">Hello **Applications** panneau affiche hello ID de chaque application dans votre compte et hello les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="890a2-180">hello **Applications** blade displays hello ID of each application in your account and hello following properties:</span></span>

* <span data-ttu-id="890a2-181">**Packages**: hello le nombre de versions associées à cette application.</span><span class="sxs-lookup"><span data-stu-id="890a2-181">**Packages**: hello number of versions associated with this application.</span></span>
* <span data-ttu-id="890a2-182">**Version par défaut**: version de l’application hello installée si vous n’indiquez pas une version lorsque vous spécifiez l’application hello pour un pool.</span><span class="sxs-lookup"><span data-stu-id="890a2-182">**Default version**: hello application version installed if you do not indicate a version when you specify hello application for a pool.</span></span> <span data-ttu-id="890a2-183">Ce paramètre est facultatif.</span><span class="sxs-lookup"><span data-stu-id="890a2-183">This setting is optional.</span></span>
* <span data-ttu-id="890a2-184">**Autoriser les mises à jour**: valeur hello qui spécifie si le package met à jour, suppressions et les ajouts sont autorisés.</span><span class="sxs-lookup"><span data-stu-id="890a2-184">**Allow updates**: hello value that specifies whether package updates, deletions, and additions are allowed.</span></span> <span data-ttu-id="890a2-185">Si la valeur est trop**non**, mises à jour de package et les suppressions sont désactivées pour l’application hello.</span><span class="sxs-lookup"><span data-stu-id="890a2-185">If this is set too**No**, package updates and deletions are disabled for hello application.</span></span> <span data-ttu-id="890a2-186">Seules les nouvelles versions de package d’application pourront être ajoutées.</span><span class="sxs-lookup"><span data-stu-id="890a2-186">Only new application package versions can be added.</span></span> <span data-ttu-id="890a2-187">valeur par défaut Hello est **Oui**.</span><span class="sxs-lookup"><span data-stu-id="890a2-187">hello default is **Yes**.</span></span>

### <a name="view-application-details"></a><span data-ttu-id="890a2-188">Affichage des détails de l’application</span><span class="sxs-lookup"><span data-stu-id="890a2-188">View application details</span></span>
<span data-ttu-id="890a2-189">panneau hello tooopen qui inclut des détails de hello pour une application, sélectionnez hello Bonjour **Applications** panneau.</span><span class="sxs-lookup"><span data-stu-id="890a2-189">tooopen hello blade that includes hello details for an application, select hello application in hello **Applications** blade.</span></span>

<span data-ttu-id="890a2-190">![Détails de l’application][4]</span><span class="sxs-lookup"><span data-stu-id="890a2-190">![Application details][4]</span></span>

<span data-ttu-id="890a2-191">Dans le panneau des détails de l’application hello, vous pouvez configurer hello suivant les paramètres de votre application.</span><span class="sxs-lookup"><span data-stu-id="890a2-191">In hello application details blade, you can configure hello following settings for your application.</span></span>

* <span data-ttu-id="890a2-192">**Autoriser les mises à jour** : permet de spécifier si ses packages d’application peuvent être mis à jour ou supprimés.</span><span class="sxs-lookup"><span data-stu-id="890a2-192">**Allow updates**: Specify whether its application packages can be updated or deleted.</span></span> <span data-ttu-id="890a2-193">Voir la section « Mettre à jour ou supprimer un package d’application » dans la suite de cet article.</span><span class="sxs-lookup"><span data-stu-id="890a2-193">See "Update or Delete an application package" later in this article.</span></span>
* <span data-ttu-id="890a2-194">**Version par défaut**: spécifiez une valeur par défaut package toodeploy toocompute des nœuds d’applications.</span><span class="sxs-lookup"><span data-stu-id="890a2-194">**Default version**: Specify a default application package toodeploy toocompute nodes.</span></span>
* <span data-ttu-id="890a2-195">**Nom d’affichage**: spécifiez un nom convivial votre solution peut utiliser lorsqu’il affiche plus d’informations sur l’application hello, par exemple, Bonjour l’interface utilisateur d’un service que vous fournissez tooyour des clients via le traitement de lot.</span><span class="sxs-lookup"><span data-stu-id="890a2-195">**Display name**: Specify a friendly name that your Batch solution can use when it displays information about hello application, for example, in hello UI of a service that you provide tooyour customers through Batch.</span></span>

### <a name="add-a-new-application"></a><span data-ttu-id="890a2-196">Ajout d’une application</span><span class="sxs-lookup"><span data-stu-id="890a2-196">Add a new application</span></span>
<span data-ttu-id="890a2-197">toocreate une nouvelle application, ajoutez un package d’application et spécifier un ID d’application des nouveaux et uniques.</span><span class="sxs-lookup"><span data-stu-id="890a2-197">toocreate a new application, add an application package and specify a new, unique application ID.</span></span> <span data-ttu-id="890a2-198">Hello premier package d’application que vous ajoutez à un nouvel ID d’application hello crée également la nouvelle application de hello.</span><span class="sxs-lookup"><span data-stu-id="890a2-198">hello first application package that you add with hello new application ID also creates hello new application.</span></span>

<span data-ttu-id="890a2-199">Cliquez sur **ajouter** sur hello **Applications** hello tooopen de panneau **nouvelle application** panneau.</span><span class="sxs-lookup"><span data-stu-id="890a2-199">Click **Add** on hello **Applications** blade tooopen hello **New application** blade.</span></span>

<span data-ttu-id="890a2-200">![Panneau Nouvelle application dans le Portail Azure][5]</span><span class="sxs-lookup"><span data-stu-id="890a2-200">![New application blade in Azure portal][5]</span></span>

<span data-ttu-id="890a2-201">Hello **nouvelle application** panneau fournit des paramètres de hello toospecify de votre package d’application et la nouvelle application de champs de suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="890a2-201">hello **New application** blade provides hello following fields toospecify hello settings of your new application and application package.</span></span>

<span data-ttu-id="890a2-202">**ID d’application**</span><span class="sxs-lookup"><span data-stu-id="890a2-202">**Application id**</span></span>

<span data-ttu-id="890a2-203">Ce champ spécifie l’ID hello de votre nouvelle application, qui est le sujet toohello standard ID de lot Azure des règles de validation.</span><span class="sxs-lookup"><span data-stu-id="890a2-203">This field specifies hello ID of your new application, which is subject toohello standard Azure Batch ID validation rules.</span></span> <span data-ttu-id="890a2-204">règles de Hello pour fournir un ID d’application sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="890a2-204">hello rules for providing an application ID are as follows:</span></span>

* <span data-ttu-id="890a2-205">Sur les nœuds de Windows hello ID peut contenir n’importe quelle combinaison de caractères alphanumériques, des traits d’union et des traits de soulignement.</span><span class="sxs-lookup"><span data-stu-id="890a2-205">On Windows nodes, hello ID can contain any combination of alphanumeric characters, hyphens, and underscores.</span></span> <span data-ttu-id="890a2-206">Sur des nœuds Linux, seuls les caractères alphanumériques et les traits de soulignement sont autorisés.</span><span class="sxs-lookup"><span data-stu-id="890a2-206">On Linux nodes, only alphanumeric characters and underscores are permitted.</span></span>
* <span data-ttu-id="890a2-207">Ne peut pas contenir plus de 64 caractères.</span><span class="sxs-lookup"><span data-stu-id="890a2-207">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="890a2-208">Doit être unique au sein de hello compte Batch.</span><span class="sxs-lookup"><span data-stu-id="890a2-208">Must be unique within hello Batch account.</span></span>
* <span data-ttu-id="890a2-209">Conserve la casse et ne respecte pas la casse.</span><span class="sxs-lookup"><span data-stu-id="890a2-209">Is case-preserving and case-insensitive.</span></span>

<span data-ttu-id="890a2-210">**Version**</span><span class="sxs-lookup"><span data-stu-id="890a2-210">**Version**</span></span>

<span data-ttu-id="890a2-211">Ce champ spécifie la version de hello du package d’application hello que vous téléchargez.</span><span class="sxs-lookup"><span data-stu-id="890a2-211">This field specifies hello version of hello application package you are uploading.</span></span> <span data-ttu-id="890a2-212">Chaînes de version sont toohello sujet suivant les règles de validation :</span><span class="sxs-lookup"><span data-stu-id="890a2-212">Version strings are subject toohello following validation rules:</span></span>

* <span data-ttu-id="890a2-213">Sur les nœuds de Windows, chaîne de version hello peut contenir n’importe quelle combinaison de caractères alphanumériques, des traits d’union, des traits de soulignement et des points.</span><span class="sxs-lookup"><span data-stu-id="890a2-213">On Windows nodes, hello version string can contain any combination of alphanumeric characters, hyphens, underscores, and periods.</span></span> <span data-ttu-id="890a2-214">Des nœuds Linux, la chaîne de version hello peut contenir uniquement des caractères alphanumériques et des traits de soulignement.</span><span class="sxs-lookup"><span data-stu-id="890a2-214">On Linux nodes, hello version string can contain only alphanumeric characters and underscores.</span></span>
* <span data-ttu-id="890a2-215">Ne peut pas contenir plus de 64 caractères.</span><span class="sxs-lookup"><span data-stu-id="890a2-215">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="890a2-216">Doit être unique au sein de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="890a2-216">Must be unique within hello application.</span></span>
* <span data-ttu-id="890a2-217">Conservent la casse et ne respectent pas la casse.</span><span class="sxs-lookup"><span data-stu-id="890a2-217">Are case-preserving and case-insensitive.</span></span>

<span data-ttu-id="890a2-218">**Package d’application**</span><span class="sxs-lookup"><span data-stu-id="890a2-218">**Application package**</span></span>

<span data-ttu-id="890a2-219">Ce champ spécifie le fichier .zip hello qui contient les fichiers binaires d’application hello et fichiers de prise en charge l’application hello tooexecute requis.</span><span class="sxs-lookup"><span data-stu-id="890a2-219">This field specifies hello .zip file that contains hello application binaries and supporting files that are required tooexecute hello application.</span></span> <span data-ttu-id="890a2-220">Cliquez sur hello **sélectionner un fichier** zone ou hello tooand de toobrowse icône de dossier sélectionner un fichier .zip qui contient les fichiers de votre application.</span><span class="sxs-lookup"><span data-stu-id="890a2-220">Click hello **Select a file** box or hello folder icon toobrowse tooand select a .zip file that contains your application's files.</span></span>

<span data-ttu-id="890a2-221">Une fois que vous avez sélectionné un fichier, cliquez sur **OK** toobegin hello téléchargement tooAzure stockage.</span><span class="sxs-lookup"><span data-stu-id="890a2-221">After you've selected a file, click **OK** toobegin hello upload tooAzure Storage.</span></span> <span data-ttu-id="890a2-222">Lors de l’opération de téléchargement de hello est terminée, portail de hello affiche une notification et ferme le panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="890a2-222">When hello upload operation is complete, hello portal displays a notification and closes hello blade.</span></span> <span data-ttu-id="890a2-223">Selon la taille de hello du fichier hello que vous êtes hello et téléchargement de la vitesse de votre connexion réseau, cette opération peut prendre un certain temps.</span><span class="sxs-lookup"><span data-stu-id="890a2-223">Depending on hello size of hello file that you are uploading and hello speed of your network connection, this operation may take some time.</span></span>

> [!WARNING]
> <span data-ttu-id="890a2-224">Ne fermez pas hello **nouvelle application** panneau avant de l’opération de téléchargement de hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="890a2-224">Do not close hello **New application** blade before hello upload operation is complete.</span></span> <span data-ttu-id="890a2-225">Cela arrête les processus de téléchargement hello.</span><span class="sxs-lookup"><span data-stu-id="890a2-225">Doing so will stop hello upload process.</span></span>
> 
> 

### <a name="add-a-new-application-package"></a><span data-ttu-id="890a2-226">Ajout d’un package d’application</span><span class="sxs-lookup"><span data-stu-id="890a2-226">Add a new application package</span></span>
<span data-ttu-id="890a2-227">tooadd une nouvelle version de package d’application pour une application existante, sélectionnez une application Bonjour **Applications** panneau, cliquez sur **Packages**, puis cliquez sur **ajouter** tooopen Hello **un package** panneau.</span><span class="sxs-lookup"><span data-stu-id="890a2-227">tooadd a new application package version for an existing application, select an application in hello **Applications** blade, click **Packages**, then click **Add** tooopen hello **Add package** blade.</span></span>

<span data-ttu-id="890a2-228">![Panneau Ajouter un package d’application dans le Portail Azure][8]</span><span class="sxs-lookup"><span data-stu-id="890a2-228">![Add application package blade in Azure portal][8]</span></span>

<span data-ttu-id="890a2-229">Comme vous pouvez le voir, les champs hello correspondent à celles de hello **nouvelle application** panneau mais hello **id de l’Application** à cocher est désactivée.</span><span class="sxs-lookup"><span data-stu-id="890a2-229">As you can see, hello fields match those of hello **New application** blade, but hello **Application id** box is disabled.</span></span> <span data-ttu-id="890a2-230">Comme vous l’avez fait pour application hello, spécifiez hello **Version** pour votre nouveau package, parcourir tooyour **package d’Application** .zip de fichier, puis cliquez sur **OK** hello de tooupload package.</span><span class="sxs-lookup"><span data-stu-id="890a2-230">As you did for hello new application, specify hello **Version** for your new package, browse tooyour **Application package** .zip file, then click **OK** tooupload hello package.</span></span>

### <a name="update-or-delete-an-application-package"></a><span data-ttu-id="890a2-231">Mettre à jour ou supprimer un package d’application</span><span class="sxs-lookup"><span data-stu-id="890a2-231">Update or delete an application package</span></span>
<span data-ttu-id="890a2-232">tooupdate ou supprimer un package d’application, panneau de détails hello ouvert pour l’application hello, cliquez sur **Packages** tooopen hello **Packages** panneau, cliquez sur hello **sélection**dans la ligne hello hello du package d’application que vous souhaitez toomodify et sélectionnez l’action hello que vous souhaitez tooperform.</span><span class="sxs-lookup"><span data-stu-id="890a2-232">tooupdate or delete an existing application package, open hello details blade for hello application, click **Packages** tooopen hello **Packages** blade, click hello **ellipsis** in hello row of hello application package that you want toomodify, and select hello action that you want tooperform.</span></span>

<span data-ttu-id="890a2-233">![Mettre à jour ou supprimer un package dans le Portail Azure][7]</span><span class="sxs-lookup"><span data-stu-id="890a2-233">![Update or delete package in Azure portal][7]</span></span>

<span data-ttu-id="890a2-234">**Mettre à jour**</span><span class="sxs-lookup"><span data-stu-id="890a2-234">**Update**</span></span>

<span data-ttu-id="890a2-235">Lorsque vous cliquez sur **mise à jour**, hello *package de mise à jour* panneau s’affiche.</span><span class="sxs-lookup"><span data-stu-id="890a2-235">When you click **Update**, hello *Update package* blade is displayed.</span></span> <span data-ttu-id="890a2-236">Ce panneau est similaire toohello *nouveau package d’application* panneau toutefois seul champ de sélection de package de hello est activé, ce qui vous toospecify une nouvelle tooupload de fichier ZIP.</span><span class="sxs-lookup"><span data-stu-id="890a2-236">This blade is similar toohello *New application package* blade, however only hello package selection field is enabled, allowing you toospecify a new ZIP file tooupload.</span></span>

<span data-ttu-id="890a2-237">![Panneau Mettre à jour un package dans le Portail Azure][11]</span><span class="sxs-lookup"><span data-stu-id="890a2-237">![Update package blade in Azure portal][11]</span></span>

<span data-ttu-id="890a2-238">**Supprimer**</span><span class="sxs-lookup"><span data-stu-id="890a2-238">**Delete**</span></span>

<span data-ttu-id="890a2-239">Lorsque vous cliquez sur **supprimer**, vous êtes invité à la suppression hello tooconfirm de version du package hello et lot supprime le package de hello depuis le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="890a2-239">When you click **Delete**, you are asked tooconfirm hello deletion of hello package version, and Batch deletes hello package from Azure Storage.</span></span> <span data-ttu-id="890a2-240">Si vous supprimez la version par défaut de hello d’une application, hello **version par défaut** paramètre est supprimé pour l’application hello.</span><span class="sxs-lookup"><span data-stu-id="890a2-240">If you delete hello default version of an application, hello **Default version** setting is removed for hello application.</span></span>

<span data-ttu-id="890a2-241">![Supprimer l’application][12]</span><span class="sxs-lookup"><span data-stu-id="890a2-241">![Delete application ][12]</span></span>

## <a name="install-applications-on-compute-nodes"></a><span data-ttu-id="890a2-242">Installation d’applications sur des nœuds de calcul</span><span class="sxs-lookup"><span data-stu-id="890a2-242">Install applications on compute nodes</span></span>
<span data-ttu-id="890a2-243">Maintenant que vous avez appris comment toomanage application packages avec hello portail Azure, nous pouvons voir comment toodeploy les nœuds de toocompute et de les exécuter avec les tâches de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="890a2-243">Now that you've learned how toomanage application packages with hello Azure portal, we can discuss how toodeploy them toocompute nodes and run them with Batch tasks.</span></span>

### <a name="install-pool-application-packages"></a><span data-ttu-id="890a2-244">Installation des packages d’application de pool</span><span class="sxs-lookup"><span data-stu-id="890a2-244">Install pool application packages</span></span>
<span data-ttu-id="890a2-245">tooinstall un package d’application sur tous les nœuds de calcul dans un pool, spécifiez au moins un package d’application *références* pour le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="890a2-245">tooinstall an application package on all compute nodes in a pool, specify one or more application package *references* for hello pool.</span></span> <span data-ttu-id="890a2-246">les packages d’applications Hello que vous spécifiez pour un pool sont installés sur chaque nœud de calcul lorsque ce nœud rejoint le pool de hello et lorsque le nœud de hello est redémarré ou la réinitialisation.</span><span class="sxs-lookup"><span data-stu-id="890a2-246">hello application packages that you specify for a pool are installed on each compute node when that node joins hello pool, and when hello node is rebooted or reimaged.</span></span>

<span data-ttu-id="890a2-247">Dans Batch .NET, spécifiez une ou plusieurs propriétés [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref] lorsque vous créez un pool ou pour un pool existant.</span><span class="sxs-lookup"><span data-stu-id="890a2-247">In Batch .NET, specify one or more [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref] when you create a new pool, or for an existing pool.</span></span> <span data-ttu-id="890a2-248">Hello [ApplicationPackageReference] [ net_pkgref] classe spécifie un ID d’application et la version tooinstall sur d’un pool nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="890a2-248">hello [ApplicationPackageReference][net_pkgref] class specifies an application ID and version tooinstall on a pool's compute nodes.</span></span>

```csharp
// Create hello unbound CloudPool
CloudPool myCloudPool =
    batchClient.PoolOperations.CreatePool(
        poolId: "myPool",
        targetDedicatedComputeNodes: 1,
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Specify hello application and version tooinstall on hello compute nodes
myCloudPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "litware",
        Version = "1.1001.2b" }
};

// Commit hello pool so that it's created in hello Batch service. As hello nodes join
// hello pool, hello specified application package is installed on each.
await myCloudPool.CommitAsync();
```

> [!IMPORTANT]
> <span data-ttu-id="890a2-249">Si un déploiement de package d’application échoue pour une raison quelconque, les marques de service de traitement par lots hello hello nœud [inutilisable][net_nodestate], et aucune tâche est planifiée pour l’exécution sur ce nœud.</span><span class="sxs-lookup"><span data-stu-id="890a2-249">If an application package deployment fails for any reason, hello Batch service marks hello node [unusable][net_nodestate], and no tasks are scheduled for execution on that node.</span></span> <span data-ttu-id="890a2-250">Dans ce cas, vous devez **redémarrer** hello de déploiement de package de nœud tooreinitiate hello.</span><span class="sxs-lookup"><span data-stu-id="890a2-250">In this case, you should **restart** hello node tooreinitiate hello package deployment.</span></span> <span data-ttu-id="890a2-251">Nœud de hello redémarrage vous permet également de planification des tâches à nouveau sur le nœud de hello.</span><span class="sxs-lookup"><span data-stu-id="890a2-251">Restarting hello node also enables task scheduling again on hello node.</span></span>
> 
> 

### <a name="install-task-application-packages"></a><span data-ttu-id="890a2-252">Installation des packages d’application de tâche</span><span class="sxs-lookup"><span data-stu-id="890a2-252">Install task application packages</span></span>
<span data-ttu-id="890a2-253">Pool de tooa similaire, spécifiez de package d’application *références* pour une tâche.</span><span class="sxs-lookup"><span data-stu-id="890a2-253">Similar tooa pool, you specify application package *references* for a task.</span></span> <span data-ttu-id="890a2-254">Lorsqu’une tâche est planifiée toorun sur un nœud, le package de hello est téléchargé et extrait juste avant l’exécution de la ligne de commande de la tâche hello.</span><span class="sxs-lookup"><span data-stu-id="890a2-254">When a task is scheduled toorun on a node, hello package is downloaded and extracted just before hello task's command line is executed.</span></span> <span data-ttu-id="890a2-255">Si une version et le package spécifié est déjà installé sur le nœud de hello, package de hello n’est pas téléchargé et hello les package existant est utilisé.</span><span class="sxs-lookup"><span data-stu-id="890a2-255">If a specified package and version is already installed on hello node, hello package is not downloaded and hello existing package is used.</span></span>

<span data-ttu-id="890a2-256">tooinstall un package d’application Office, configurez la tâche hello [CloudTask][net_cloudtask].[ ApplicationPackageReferences] [ net_cloudtask_pkgref] propriété :</span><span class="sxs-lookup"><span data-stu-id="890a2-256">tooinstall a task application package, configure hello task's [CloudTask][net_cloudtask].[ApplicationPackageReferences][net_cloudtask_pkgref] property:</span></span>

```csharp
CloudTask task =
    new CloudTask(
        "litwaretask001",
        "cmd /c %AZ_BATCH_APP_PACKAGE_LITWARE%\\litware.exe -args -here");

task.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference
    {
        ApplicationId = "litware",
        Version = "1.1001.2b"
    }
};
```

## <a name="execute-hello-installed-applications"></a><span data-ttu-id="890a2-257">Exécuter des applications de hello installé</span><span class="sxs-lookup"><span data-stu-id="890a2-257">Execute hello installed applications</span></span>
<span data-ttu-id="890a2-258">Hello packages que vous avez spécifié pour un pool ou une tâche sont téléchargés et extrait tooa nommé répertoire hello `AZ_BATCH_ROOT_DIR` du nœud de hello.</span><span class="sxs-lookup"><span data-stu-id="890a2-258">hello packages that you've specified for a pool or task are downloaded and extracted tooa named directory within hello `AZ_BATCH_ROOT_DIR` of hello node.</span></span> <span data-ttu-id="890a2-259">Traitement par lots crée également une variable d’environnement qui contient toohello de chemin d’accès hello nommé active.</span><span class="sxs-lookup"><span data-stu-id="890a2-259">Batch also creates an environment variable that contains hello path toohello named directory.</span></span> <span data-ttu-id="890a2-260">Les lignes de commande de tâche utiliser cette variable d’environnement pour référencer l’application hello sur le nœud de hello.</span><span class="sxs-lookup"><span data-stu-id="890a2-260">Your task command lines use this environment variable when referencing hello application on hello node.</span></span> 

<span data-ttu-id="890a2-261">Sur les nœuds de Windows, variable de hello est Bonjour suivant le format :</span><span class="sxs-lookup"><span data-stu-id="890a2-261">On Windows nodes, hello variable is in hello following format:</span></span>

```
Windows:
AZ_BATCH_APP_PACKAGE_APPLICATIONID#version
```

<span data-ttu-id="890a2-262">Des nœuds Linux, le format de hello est légèrement différente.</span><span class="sxs-lookup"><span data-stu-id="890a2-262">On Linux nodes, hello format is slightly different.</span></span> <span data-ttu-id="890a2-263">Points (.), des tirets (-) et des signes dièse (#) sont mis à plat toounderscores dans la variable d’environnement hello.</span><span class="sxs-lookup"><span data-stu-id="890a2-263">Periods (.), hypens (-) and number signs (#) are flattened toounderscores in hello environment variable.</span></span> <span data-ttu-id="890a2-264">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="890a2-264">For example:</span></span>

```
Linux:
AZ_BATCH_APP_PACKAGE_APPLICATIONID_version
```

<span data-ttu-id="890a2-265">`APPLICATIONID`et `version` sont des valeurs qui correspondent toohello application et la version du package que vous avez spécifié pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="890a2-265">`APPLICATIONID` and `version` are values that correspond toohello application and package version you've specified for deployment.</span></span> <span data-ttu-id="890a2-266">Par exemple, si vous avez spécifié cette version 2.7 d’application *blender* doit être installé sur les nœuds de Windows, les lignes de commande de tâche utiliseriez cette tooaccess de variable d’environnement ses fichiers :</span><span class="sxs-lookup"><span data-stu-id="890a2-266">For example, if you specified that version 2.7 of application *blender* should be installed on Windows nodes, your task command lines would use this environment variable tooaccess its files:</span></span>

```
Windows:
AZ_BATCH_APP_PACKAGE_BLENDER#2.7
```

<span data-ttu-id="890a2-267">Des nœuds Linux, spécifiez la variable d’environnement hello dans ce format :</span><span class="sxs-lookup"><span data-stu-id="890a2-267">On Linux nodes, specify hello environment variable in this format:</span></span>

```
Linux:
AZ_BATCH_APP_PACKAGE_BLENDER_2_7
``` 

<span data-ttu-id="890a2-268">Lorsque vous téléchargez un package d’application, vous pouvez spécifier un tooyour toodeploy de version par défaut des nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="890a2-268">When you upload an application package, you can specify a default version toodeploy tooyour compute nodes.</span></span> <span data-ttu-id="890a2-269">Si vous avez spécifié une version par défaut pour une application, vous pouvez omettre suffixe de version hello lorsque vous faites référence application hello.</span><span class="sxs-lookup"><span data-stu-id="890a2-269">If you have specified a default version for an application, you can omit hello version suffix when you reference hello application.</span></span> <span data-ttu-id="890a2-270">Vous pouvez spécifier la version de l’application par défaut hello Bonjour portail Azure, dans le panneau des Applications hello, comme indiqué dans [télécharger et gérer des applications](#upload-and-manage-applications).</span><span class="sxs-lookup"><span data-stu-id="890a2-270">You can specify hello default application version in hello Azure portal, on hello Applications blade, as shown in [Upload and manage applications](#upload-and-manage-applications).</span></span>

<span data-ttu-id="890a2-271">Par exemple, si vous définissez « 2.7 » en tant que version par défaut de hello pour application *blender*, vos tâches référencent hello suivant la variable d’environnement, puis les nœuds de Windows seront exécute la version 2.7 :</span><span class="sxs-lookup"><span data-stu-id="890a2-271">For example, if you set "2.7" as hello default version for application *blender*, and your tasks reference hello following environment variable, then your Windows nodes will execute version 2.7:</span></span>

`AZ_BATCH_APP_PACKAGE_BLENDER`

<span data-ttu-id="890a2-272">Hello extrait de code suivant montre un exemple de ligne de commande tâche qui lance la version par défaut de hello Hello *blender* application :</span><span class="sxs-lookup"><span data-stu-id="890a2-272">hello following code snippet shows an example task command line that launches hello default version of hello *blender* application:</span></span>

```csharp
string taskId = "blendertask01";
string commandLine =
    @"cmd /c %AZ_BATCH_APP_PACKAGE_BLENDER%\blender.exe -args -here";
CloudTask blenderTask = new CloudTask(taskId, commandLine);
```

> [!TIP]
> <span data-ttu-id="890a2-273">Consultez [paramètres d’environnement pour les tâches](batch-api-basics.md#environment-settings-for-tasks) Bonjour [vue d’ensemble de lot](batch-api-basics.md) pour plus d’informations sur les paramètres d’environnement de nœud de calcul.</span><span class="sxs-lookup"><span data-stu-id="890a2-273">See [Environment settings for tasks](batch-api-basics.md#environment-settings-for-tasks) in hello [Batch feature overview](batch-api-basics.md) for more information about compute node environment settings.</span></span>
> 
> 

## <a name="update-a-pools-application-packages"></a><span data-ttu-id="890a2-274">Mise à jour des packages d’applications d’un pool</span><span class="sxs-lookup"><span data-stu-id="890a2-274">Update a pool's application packages</span></span>
<span data-ttu-id="890a2-275">Si un pool existant a déjà été configuré avec un package d’application, vous pouvez spécifier un nouveau package pour le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="890a2-275">If an existing pool has already been configured with an application package, you can specify a new package for hello pool.</span></span> <span data-ttu-id="890a2-276">Si vous spécifiez une nouvelle référence de package pour un pool, suivants de hello s’appliquent :</span><span class="sxs-lookup"><span data-stu-id="890a2-276">If you specify a new package reference for a pool, hello following apply:</span></span>

* <span data-ttu-id="890a2-277">Hello service Batch installe package nouvellement spécifié de hello sur tous les nœuds nouveau joindre le pool de hello et sur n’importe quel nœud existant qui est redémarré ou la réinitialisation.</span><span class="sxs-lookup"><span data-stu-id="890a2-277">hello Batch service installs hello newly specified package on all new nodes that join hello pool and on any existing node that is rebooted or reimaged.</span></span>
* <span data-ttu-id="890a2-278">Calcul des nœuds qui sont déjà dans le pool de hello lorsque vous mettez à jour les références de package hello n’installent pas automatiquement le nouveau package d’application hello.</span><span class="sxs-lookup"><span data-stu-id="890a2-278">Compute nodes that are already in hello pool when you update hello package references do not automatically install hello new application package.</span></span> <span data-ttu-id="890a2-279">Ces nœuds doivent être redémarrés ou réinitialisé tooreceive hello nouveau package de calcul.</span><span class="sxs-lookup"><span data-stu-id="890a2-279">These compute nodes must be rebooted or reimaged tooreceive hello new package.</span></span>
* <span data-ttu-id="890a2-280">Lorsqu’un nouveau package est déployé, hello créé des variables d’environnement reflètent les nouvelles références de package d’application hello.</span><span class="sxs-lookup"><span data-stu-id="890a2-280">When a new package is deployed, hello created environment variables reflect hello new application package references.</span></span>

<span data-ttu-id="890a2-281">Dans cet exemple, un pool existant hello a la version 2.7 de hello *blender* application configurée comme l’un de ses [CloudPool][net_cloudpool].[ ApplicationPackageReferences][net_cloudpool_pkgref].</span><span class="sxs-lookup"><span data-stu-id="890a2-281">In this example, hello existing pool has version 2.7 of hello *blender* application configured as one of its [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref].</span></span> <span data-ttu-id="890a2-282">nœuds du pool tooupdate hello avec la version 2.76b, spécifiez un nouveau [ApplicationPackageReference] [ net_pkgref] avec la nouvelle version de hello et validation hello modification.</span><span class="sxs-lookup"><span data-stu-id="890a2-282">tooupdate hello pool's nodes with version 2.76b, specify a new [ApplicationPackageReference][net_pkgref] with hello new version, and commit hello change.</span></span>

```csharp
string newVersion = "2.76b";
CloudPool boundPool = await batchClient.PoolOperations.GetPoolAsync("myPool");
boundPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "blender",
        Version = newVersion }
};
await boundPool.CommitAsync();
```

<span data-ttu-id="890a2-283">Maintenant que hello nouvelle version a été configurée, hello service Batch installe la version 2.76b tooany *nouveau* nœud qui rejoint hello pool.</span><span class="sxs-lookup"><span data-stu-id="890a2-283">Now that hello new version has been configured, hello Batch service installs version 2.76b tooany *new* node that joins hello pool.</span></span> <span data-ttu-id="890a2-284">tooinstall 2.76b sur nœuds hello *déjà* dans le pool de hello, redémarrez ou les réinitialiser.</span><span class="sxs-lookup"><span data-stu-id="890a2-284">tooinstall 2.76b on hello nodes that are *already* in hello pool, reboot or reimage them.</span></span> <span data-ttu-id="890a2-285">Notez que les nœuds redémarrés conservent fichiers hello à partir des déploiements de package précédents.</span><span class="sxs-lookup"><span data-stu-id="890a2-285">Note that rebooted nodes retain hello files from previous package deployments.</span></span>

## <a name="list-hello-applications-in-a-batch-account"></a><span data-ttu-id="890a2-286">Liste des applications hello dans un compte Batch</span><span class="sxs-lookup"><span data-stu-id="890a2-286">List hello applications in a Batch account</span></span>
<span data-ttu-id="890a2-287">Vous pouvez répertorier les applications hello et les packages dans un compte de traitement par lots à l’aide de hello [ApplicationOperations][net_appops].[ ListApplicationSummaries] [ net_appops_listappsummaries] (méthode).</span><span class="sxs-lookup"><span data-stu-id="890a2-287">You can list hello applications and their packages in a Batch account by using hello [ApplicationOperations][net_appops].[ListApplicationSummaries][net_appops_listappsummaries] method.</span></span>

```csharp
// List hello applications and their application packages in hello Batch account.
List<ApplicationSummary> applications = await batchClient.ApplicationOperations.ListApplicationSummaries().ToListAsync();
foreach (ApplicationSummary app in applications)
{
    Console.WriteLine("ID: {0} | Display Name: {1}", app.Id, app.DisplayName);

    foreach (string version in app.Versions)
    {
        Console.WriteLine("  {0}", version);
    }
}
```

## <a name="wrap-up"></a><span data-ttu-id="890a2-288">Conclusion</span><span class="sxs-lookup"><span data-stu-id="890a2-288">Wrap up</span></span>
<span data-ttu-id="890a2-289">Avec les packages d’application, vous pouvez aider vos clients sélectionnez applications hello pour leurs tâches et spécifiez hello version exacte toouse lors du traitement des travaux avec votre service de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="890a2-289">With application packages, you can help your customers select hello applications for their jobs and specify hello exact version toouse when processing jobs with your Batch-enabled service.</span></span> <span data-ttu-id="890a2-290">Vous pouvez également permettre de hello pour votre tooupload clients et effectuer le suivi de leurs propres applications dans votre service.</span><span class="sxs-lookup"><span data-stu-id="890a2-290">You might also provide hello ability for your customers tooupload and track their own applications in your service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="890a2-291">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="890a2-291">Next steps</span></span>
* <span data-ttu-id="890a2-292">Hello [API REST de traitement par lots] [ api_rest] fournit également la prise en charge toowork avec les packages d’applications.</span><span class="sxs-lookup"><span data-stu-id="890a2-292">hello [Batch REST API][api_rest] also provides support toowork with application packages.</span></span> <span data-ttu-id="890a2-293">Par exemple, consultez hello [applicationPackageReferences] [ rest_add_pool_with_packages] élément [ajouter un compte du pool de tooan] [ rest_add_pool] pour plus d’informations sur la façon toospecify tooinstall de packages à l’aide des API REST de hello.</span><span class="sxs-lookup"><span data-stu-id="890a2-293">For example, see hello [applicationPackageReferences][rest_add_pool_with_packages] element in [Add a pool tooan account][rest_add_pool] for information about how toospecify packages tooinstall by using hello REST API.</span></span> <span data-ttu-id="890a2-294">Consultez [Applications] [ rest_applications] pour plus d’informations sur comment informations à l’aide de l’application tooobtain hello API REST de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="890a2-294">See [Applications][rest_applications] for details about how tooobtain application information by using hello Batch REST API.</span></span>
* <span data-ttu-id="890a2-295">Découvrez comment tooprogrammatically [gérer les quotas avec Batch Management .NET et des comptes Azure Batch](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="890a2-295">Learn how tooprogrammatically [manage Azure Batch accounts and quotas with Batch Management .NET](batch-management-dotnet.md).</span></span> <span data-ttu-id="890a2-296">Hello [Batch Management .NET][api_net_mgmt] bibliothèque peut activer des fonctionnalités de création et la suppression de compte pour votre application de traitement ou d’un service.</span><span class="sxs-lookup"><span data-stu-id="890a2-296">hello [Batch Management .NET][api_net_mgmt] library can enable account creation and deletion features for your Batch application or service.</span></span>

[api_net]: https://docs.microsoft.com/dotnet/api/overview/azure/batch/client?view=azure-dotnet
[api_net_mgmt]: https://docs.microsoft.com/dotnet/api/overview/azure/batch/management?view=azure-dotnet
[api_rest]: https://docs.microsoft.com/en-us/rest/api/batchservice/
[batch_mgmt_nuget]: https://www.nuget.org/packages/Microsoft.Azure.Management.Batch/
[github_samples]: https://github.com/Azure/azure-batch-samples
[storage_pricing]: https://azure.microsoft.com/pricing/details/storage/
[net_appops]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationoperations.aspx
[net_appops_listappsummaries]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationoperations.listapplicationsummaries.aspx
[net_cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_cloudpool_pkgref]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.applicationpackagereferences.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudtask.aspx
[net_cloudtask_pkgref]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudtask.applicationpackagereferences.aspx
[net_nodestate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.state.aspx
[net_pkgref]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationpackagereference.aspx
[portal]: https://portal.azure.com
[rest_applications]: https://msdn.microsoft.com/library/azure/mt643945.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[rest_add_pool_with_packages]: https://msdn.microsoft.com/library/azure/dn820174.aspx#bk_apkgreference

[1]: ./media/batch-application-packages/app_pkg_01.png "Diagramme détaillée des packages d’applications"
[2]: ./media/batch-application-packages/app_pkg_02.png "Vignette Applications dans le Portail Azure"
[3]: ./media/batch-application-packages/app_pkg_03.png "Panneau Application dans le Portail Azure"
[4]: ./media/batch-application-packages/app_pkg_04.png "Panneau Détails de l’application dans le Portail Azure"
[5]: ./media/batch-application-packages/app_pkg_05.png "Panneau Nouvelle application dans le Portail Azure"
[7]: ./media/batch-application-packages/app_pkg_07.png "Liste déroulante Mettre à jour ou supprimer des packages dans le Portail Azure"
[8]: ./media/batch-application-packages/app_pkg_08.png "Panneau Nouveau package d’application dans le Portail Azure"
[9]: ./media/batch-application-packages/app_pkg_09.png "Alerte Aucun compte de stockage lié"
[10]: ./media/batch-application-packages/app_pkg_10.png "Panneau Sélectionner un compte de stockage dans le Portail Azure"
[11]: ./media/batch-application-packages/app_pkg_11.png "Panneau Mettre à jour un package dans le Portail Azure"
[12]: ./media/batch-application-packages/app_pkg_12.png "Boîte de dialogue de confirmation de la suppression d’un package dans le Portail Azure"
