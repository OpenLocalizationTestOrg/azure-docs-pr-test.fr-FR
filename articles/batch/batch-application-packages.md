---
title: "Installer des packages d’applications sur des nœuds de calcul - Azure Batch | Microsoft Docs"
description: "Utilisez la fonctionnalité de packages d’applications d’Azure Batch pour gérer facilement plusieurs applications et versions pour l’installation sur des nœuds de calcul Batch."
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
ms.openlocfilehash: afcc04c80ec15872a22de5d5969a7ef6a583562f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-applications-to-compute-nodes-with-batch-application-packages"></a><span data-ttu-id="e1d95-103">Déployer des applications sur les nœuds avec des packages d’applications Batch</span><span class="sxs-lookup"><span data-stu-id="e1d95-103">Deploy applications to compute nodes with Batch application packages</span></span>

<span data-ttu-id="e1d95-104">La fonctionnalité de packages d’application d’Azure Batch permet de gérer facilement les applications de tâche et leur déploiement sur les nœuds de calcul dans votre pool.</span><span class="sxs-lookup"><span data-stu-id="e1d95-104">The application packages feature of Azure Batch provides easy management of task applications and their deployment to the compute nodes in your pool.</span></span> <span data-ttu-id="e1d95-105">Grâce aux packages d’application, vous pouvez charger et gérer plusieurs versions des applications que vos tâches exécutent, notamment leurs fichiers de prise en charge.</span><span class="sxs-lookup"><span data-stu-id="e1d95-105">With application packages, you can upload and manage multiple versions of the applications your tasks run, including their supporting files.</span></span> <span data-ttu-id="e1d95-106">Vous pouvez ensuite déployer automatiquement une ou plusieurs de ces applications sur les nœuds de calcul de votre pool.</span><span class="sxs-lookup"><span data-stu-id="e1d95-106">You can then automatically deploy one or more of these applications to the compute nodes in your pool.</span></span>

<span data-ttu-id="e1d95-107">Dans cet article, vous allez apprendre à charger et gérer des packages d’application à l’aide du Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e1d95-107">In this article, you will learn how to upload and manage application packages in the Azure portal.</span></span> <span data-ttu-id="e1d95-108">Vous apprendrez ensuite à les installer sur les nœuds de calcul d’un pool au moyen de la bibliothèque [Batch .NET][api_net].</span><span class="sxs-lookup"><span data-stu-id="e1d95-108">You will then learn how to install them on a pool's compute nodes with the [Batch .NET][api_net] library.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="e1d95-109">Les packages d’applications sont pris en charge sur tous les pools Batch créés après le 5 juillet 2017.</span><span class="sxs-lookup"><span data-stu-id="e1d95-109">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="e1d95-110">Ils sont pris en charge sur les pools Batch créés entre le 10 mars 2016 et le 5 juillet 2017 uniquement si le pool a été créé à l’aide d’une configuration de service cloud.</span><span class="sxs-lookup"><span data-stu-id="e1d95-110">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if the pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="e1d95-111">Les pools Batch créés avant le 10 mars 2016 ne prennent pas en charge les packages d’applications.</span><span class="sxs-lookup"><span data-stu-id="e1d95-111">Batch pools created prior to 10 March 2016 do not support application packages.</span></span>
>
> <span data-ttu-id="e1d95-112">Les API servant à la création et la gestion des packages d’application font partie de la bibliothèque [Batch Management .NET] [[api_net_mgmt]].</span><span class="sxs-lookup"><span data-stu-id="e1d95-112">The APIs for creating and managing application packages are part of the [Batch Management .NET][[api_net_mgmt]] library.</span></span> <span data-ttu-id="e1d95-113">Les API servant à l’installation des packages d’application sur un nœud de calcul font partie de la bibliothèque [Batch .NET][api_net].</span><span class="sxs-lookup"><span data-stu-id="e1d95-113">The APIs for installing application packages on a compute node are part of the [Batch .NET][api_net] library.</span></span>  
>
> <span data-ttu-id="e1d95-114">La fonctionnalité de packages d’application décrite ici remplace la fonctionnalité d’applications Batch disponible dans les versions précédentes du service.</span><span class="sxs-lookup"><span data-stu-id="e1d95-114">The application packages feature described here supersedes the Batch Apps feature available in previous versions of the service.</span></span>
> 
> 

## <a name="application-package-requirements"></a><span data-ttu-id="e1d95-115">Configuration requise des packages d’application</span><span class="sxs-lookup"><span data-stu-id="e1d95-115">Application package requirements</span></span>
<span data-ttu-id="e1d95-116">Pour utiliser des packages d’application, vous devez [lier un compte de stockage Azure](#link-a-storage-account) à votre compte Batch.</span><span class="sxs-lookup"><span data-stu-id="e1d95-116">To use application packages, you need to [link an Azure Storage account](#link-a-storage-account) to your Batch account.</span></span>

<span data-ttu-id="e1d95-117">Cette fonctionnalité a été introduite dans la version 2015-12-01.2.2 de [l’API REST Batch][api_rest] et dans la version 3.1.0 de la bibliothèque [Batch .NET][api_net] correspondante.</span><span class="sxs-lookup"><span data-stu-id="e1d95-117">This feature was introduced in [Batch REST API][api_rest] version 2015-12-01.2.2 and the corresponding [Batch .NET][api_net] library version 3.1.0.</span></span> <span data-ttu-id="e1d95-118">Nous vous recommandons de toujours utiliser la dernière version de l’API lorsque vous utilisez Batch.</span><span class="sxs-lookup"><span data-stu-id="e1d95-118">We recommend that you always use the latest API version when working with Batch.</span></span>

> [!NOTE]
> <span data-ttu-id="e1d95-119">Les packages d’applications sont pris en charge sur tous les pools Batch créés après le 5 juillet 2017.</span><span class="sxs-lookup"><span data-stu-id="e1d95-119">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="e1d95-120">Ils sont pris en charge sur les pools Batch créés entre le 10 mars 2016 et le 5 juillet 2017 uniquement si le pool a été créé à l’aide d’une configuration de service cloud.</span><span class="sxs-lookup"><span data-stu-id="e1d95-120">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if the pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="e1d95-121">Les pools Batch créés avant le 10 mars 2016 ne prennent pas en charge les packages d’applications.</span><span class="sxs-lookup"><span data-stu-id="e1d95-121">Batch pools created prior to 10 March 2016 do not support application packages.</span></span>
>
>

## <a name="about-applications-and-application-packages"></a><span data-ttu-id="e1d95-122">Concernant les applications et les packages d’applications</span><span class="sxs-lookup"><span data-stu-id="e1d95-122">About applications and application packages</span></span>
<span data-ttu-id="e1d95-123">Dans Azure Batch, une *application* fait référence à un jeu de versions de fichiers binaires automatiquement téléchargeable sur les nœuds de calcul de votre pool.</span><span class="sxs-lookup"><span data-stu-id="e1d95-123">Within Azure Batch, an *application* refers to a set of versioned binaries that can be automatically downloaded to the compute nodes in your pool.</span></span> <span data-ttu-id="e1d95-124">Un *package d’application* désigne un *jeu spécifique* de ces fichiers binaires et représente une *version* donnée de l’application.</span><span class="sxs-lookup"><span data-stu-id="e1d95-124">An *application package* refers to a *specific set* of those binaries and represents a given *version* of the application.</span></span>

<span data-ttu-id="e1d95-125">![Diagramme détaillé sur les applications et les packages d’applications][1]</span><span class="sxs-lookup"><span data-stu-id="e1d95-125">![High-level diagram of applications and application packages][1]</span></span>

### <a name="applications"></a><span data-ttu-id="e1d95-126">Applications</span><span class="sxs-lookup"><span data-stu-id="e1d95-126">Applications</span></span>
<span data-ttu-id="e1d95-127">Dans Batch, une application contient un ou plusieurs packages d’application et spécifie les options de configuration de l’application.</span><span class="sxs-lookup"><span data-stu-id="e1d95-127">An application in Batch contains one or more application packages and specifies configuration options for the application.</span></span> <span data-ttu-id="e1d95-128">Par exemple, une application peut indiquer la version par défaut du package d’application à installer sur les nœuds de calcul, et préciser si ses packages peuvent être mis à jour ou supprimés.</span><span class="sxs-lookup"><span data-stu-id="e1d95-128">For example, an application can specify the default application package version to install on compute nodes and whether its packages can be updated or deleted.</span></span>

### <a name="application-packages"></a><span data-ttu-id="e1d95-129">packages d’application</span><span class="sxs-lookup"><span data-stu-id="e1d95-129">Application packages</span></span>
<span data-ttu-id="e1d95-130">Un package d’application est un fichier .zip contenant les fichiers binaires de l’application et les fichiers de prise en charge requis pour que vos tâches puissent exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="e1d95-130">An application package is a .zip file that contains the application binaries and supporting files that are required for your tasks to run the application.</span></span> <span data-ttu-id="e1d95-131">Chaque package d’application représente une version spécifique de l’application.</span><span class="sxs-lookup"><span data-stu-id="e1d95-131">Each application package represents a specific version of the application.</span></span>

<span data-ttu-id="e1d95-132">Vous pouvez spécifier des packages d’application aux niveaux d’un pool et d’une tâche.</span><span class="sxs-lookup"><span data-stu-id="e1d95-132">You can specify application packages at the pool and task levels.</span></span> <span data-ttu-id="e1d95-133">Lorsque vous créez un pool ou une tâche, vous pouvez spécifier un ou plusieurs de ces packages et, le cas échéant, une version.</span><span class="sxs-lookup"><span data-stu-id="e1d95-133">You can specify one or more of these packages and (optionally) a version when you create a pool or task.</span></span>

* <span data-ttu-id="e1d95-134">**Les packages d’application du pool** sont déployés sur *tous* les nœuds dans le pool.</span><span class="sxs-lookup"><span data-stu-id="e1d95-134">**Pool application packages** are deployed to *every* node in the pool.</span></span> <span data-ttu-id="e1d95-135">Les applications sont déployées lorsqu’un nœud rejoint un pool, et lorsqu’il est redémarré ou réinitialisé.</span><span class="sxs-lookup"><span data-stu-id="e1d95-135">Applications are deployed when a node joins a pool, and when it is rebooted or reimaged.</span></span>
  
    <span data-ttu-id="e1d95-136">Les packages d’application de pool sont appropriés lorsque tous les nœuds dans un pool exécutent les tâches d’un travail.</span><span class="sxs-lookup"><span data-stu-id="e1d95-136">Pool application packages are appropriate when all nodes in a pool execute a job's tasks.</span></span> <span data-ttu-id="e1d95-137">Vous pouvez spécifier un ou plusieurs packages d’application lorsque vous créez un pool, et vous pouvez ajouter ou mettre à jour les packages d’un pool existant.</span><span class="sxs-lookup"><span data-stu-id="e1d95-137">You can specify one or more application packages when you create a pool, and you can add or update an existing pool's packages.</span></span> <span data-ttu-id="e1d95-138">Si vous mettez à jour les packages d’application d’un pool existant, vous devez redémarrer ses nœuds pour installer le nouveau package.</span><span class="sxs-lookup"><span data-stu-id="e1d95-138">If you update an existing pool's application packages, you must restart its nodes to install the new package.</span></span>
* <span data-ttu-id="e1d95-139">**Les packages d’application de tâche** sont déployés uniquement sur un nœud de calcul programmé pour exécuter une tâche, juste avant d’exécuter la ligne de commande de la tâche.</span><span class="sxs-lookup"><span data-stu-id="e1d95-139">**Task application packages** are deployed only to a compute node scheduled to run a task, just before running the task's command line.</span></span> <span data-ttu-id="e1d95-140">Si le package d’application spécifié et la version sont déjà sur le nœud, il n’est pas redéployé et le package existant est utilisé.</span><span class="sxs-lookup"><span data-stu-id="e1d95-140">If the specified application package and version is already on the node, it is not redeployed and the existing package is used.</span></span>
  
    <span data-ttu-id="e1d95-141">Les packages d’application de tâche sont utiles dans les environnements de pool partagé, où différents travaux sont exécutés sur un même pool et le pool n’est pas supprimé lorsqu’un travail est terminé.</span><span class="sxs-lookup"><span data-stu-id="e1d95-141">Task application packages are useful in shared-pool environments, where different jobs are run on one pool, and the pool is not deleted when a job is completed.</span></span> <span data-ttu-id="e1d95-142">Si votre travail présente moins de tâches que le pool ne contient de nœuds, les packages d’applications au niveau des tâches peuvent réduire le transfert de données, votre application n’étant déployée que sur les nœuds exécutant les tâches.</span><span class="sxs-lookup"><span data-stu-id="e1d95-142">If your job has fewer tasks than nodes in the pool, task application packages can minimize data transfer since your application is deployed only to the nodes that run tasks.</span></span>
  
    <span data-ttu-id="e1d95-143">Les autres scénarios pouvant tirer parti des packages d’application de tâche sont les travaux qui exécutent une application lourde, mais uniquement pour un petit nombre de tâches.</span><span class="sxs-lookup"><span data-stu-id="e1d95-143">Other scenarios that can benefit from task application packages are jobs that run a large application, but for only a few tasks.</span></span> <span data-ttu-id="e1d95-144">Par exemple, une phase de prétraitement ou une tâche de fusion, où l’application de pré-traitement ou de fusion est lourde, peuvent bénéficier de l’utilisation de packages d’application de tâche.</span><span class="sxs-lookup"><span data-stu-id="e1d95-144">For example, a pre-processing stage or a merge task, where the pre-processing or merge application is heavyweight, may benefit from using task application packages.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e1d95-145">Il existe des restrictions au nombre d’applications et de packages d’application à l’intérieur d’un compte Batch, ainsi qu’à la taille maximale des packages d’application.</span><span class="sxs-lookup"><span data-stu-id="e1d95-145">There are restrictions on the number of applications and application packages within a Batch account and on the maximum application package size.</span></span> <span data-ttu-id="e1d95-146">Pour plus d’informations sur ces limites, voir [Quotas et limites pour le service Azure Batch](batch-quota-limit.md) .</span><span class="sxs-lookup"><span data-stu-id="e1d95-146">See [Quotas and limits for the Azure Batch service](batch-quota-limit.md) for details about these limits.</span></span>
> 
> 

### <a name="benefits-of-application-packages"></a><span data-ttu-id="e1d95-147">Avantages des packages d’applications</span><span class="sxs-lookup"><span data-stu-id="e1d95-147">Benefits of application packages</span></span>
<span data-ttu-id="e1d95-148">Les packages d’application peuvent simplifier le code de votre solution Batch et alléger les coûts requis par la gestion des applications exécutées par vos tâches.</span><span class="sxs-lookup"><span data-stu-id="e1d95-148">Application packages can simplify the code in your Batch solution and lower the overhead required to manage the applications that your tasks run.</span></span>

<span data-ttu-id="e1d95-149">Avec des packages d’application, la tâche de démarrage de votre pool ne doit pas nécessairement spécifier une longue liste de fichiers de ressources à installer sur les nœuds.</span><span class="sxs-lookup"><span data-stu-id="e1d95-149">With application packages, your pool's start task doesn't have to specify a long list of individual resource files to install on the nodes.</span></span> <span data-ttu-id="e1d95-150">Vous n’êtes pas obligé de gérer manuellement plusieurs versions de vos fichiers dans le stockage Azure ni sur vos nœuds.</span><span class="sxs-lookup"><span data-stu-id="e1d95-150">You don't have to manually manage multiple versions of your application files in Azure Storage, or on your nodes.</span></span> <span data-ttu-id="e1d95-151">En outre, inutile de vous soucier de la génération [d’URL SAP](../storage/common/storage-dotnet-shared-access-signature-part-1.md) pour fournir l’accès aux fichiers dans votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="e1d95-151">And, you don't need to worry about generating [SAS URLs](../storage/common/storage-dotnet-shared-access-signature-part-1.md) to provide access to the files in your Storage account.</span></span> <span data-ttu-id="e1d95-152">Batch fonctionne en arrière-plan avec le stockage Azure pour stocker des packages d’application et les déployer sur les nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="e1d95-152">Batch works in the background with Azure Storage to store application packages and deploy them to compute nodes.</span></span>

> [!NOTE] 
> <span data-ttu-id="e1d95-153">La taille totale d’une tâche de démarrage doit être inférieure ou égale à 32 768 caractères, y compris les fichiers de ressources et les variables d’environnement.</span><span class="sxs-lookup"><span data-stu-id="e1d95-153">The total size of a start task must be less than or equal to 32768 characters, including resource files and environment variables.</span></span> <span data-ttu-id="e1d95-154">Si votre tâche de démarrage dépasse cette limite, l’utilisation de packages d’application est une autre option.</span><span class="sxs-lookup"><span data-stu-id="e1d95-154">If your start task exceeds this limit, then using application packages is another option.</span></span> <span data-ttu-id="e1d95-155">Vous pouvez également créer une archive zippée contenant vos fichiers de ressources, la charger en tant qu’objet blob sur Stockage Azure, puis la décompresser à partir de la ligne de commande de votre tâche de démarrage.</span><span class="sxs-lookup"><span data-stu-id="e1d95-155">You can also create a zipped archive containing your resource files, upload it as a blob to Azure Storage, and then unzip it from the command line of your start task.</span></span> 
>
>

## <a name="upload-and-manage-applications"></a><span data-ttu-id="e1d95-156">Téléchargement et gestion des applications</span><span class="sxs-lookup"><span data-stu-id="e1d95-156">Upload and manage applications</span></span>
<span data-ttu-id="e1d95-157">Vous pouvez utiliser le [Portail Azure][portal] ou la bibliothèque [Batch Management .NET](batch-management-dotnet.md) pour gérer les packages d’application dans votre compte Batch.</span><span class="sxs-lookup"><span data-stu-id="e1d95-157">You can use the [Azure portal][portal] or the [Batch Management .NET](batch-management-dotnet.md) library to manage the application packages in your Batch account.</span></span> <span data-ttu-id="e1d95-158">Dans les sections suivantes, nous allons commencer par montrer comment lier un compte de stockage, puis nous aborderons l’ajout d’applications et de packages et leur gestion avec le portail.</span><span class="sxs-lookup"><span data-stu-id="e1d95-158">In the next few sections, we first show how to link a Storage account, then discuss adding applications and packages and managing them with the portal.</span></span>

### <a name="link-a-storage-account"></a><span data-ttu-id="e1d95-159">Liaison d’un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="e1d95-159">Link a Storage account</span></span>
<span data-ttu-id="e1d95-160">Pour utiliser les packages d’application, vous devez commencer par lier un compte Azure Storage à votre compte Batch.</span><span class="sxs-lookup"><span data-stu-id="e1d95-160">To use application packages, you must first link an Azure Storage account to your Batch account.</span></span> <span data-ttu-id="e1d95-161">Si vous n’avez pas encore configuré de compte de stockage, le portail Azure affiche un avertissement la première fois que vous cliquez sur la vignette **Applications** dans le panneau **Compte Batch**.</span><span class="sxs-lookup"><span data-stu-id="e1d95-161">If you have not yet configured a Storage account, the Azure portal displays a warning the first time you click the **Applications** tile in the **Batch account** blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e1d95-162">Batch prend actuellement en charge *uniquement* le type de compte de stockage **à usage général**, comme décrit à l’étape 5, [Créer un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account), dans [À propos des comptes de stockage Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="e1d95-162">Batch currently supports *only* the **General-purpose** storage account type as described in step 5, [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account), in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="e1d95-163">Quand vous liez un compte de stockage Azure à votre compte Batch, liez *uniquement* un compte de stockage **à usage général**.</span><span class="sxs-lookup"><span data-stu-id="e1d95-163">When you link an Azure Storage account to your Batch account, link *only* a **General-purpose** storage account.</span></span>
> 
> 

<span data-ttu-id="e1d95-164">![Avertissement « Aucun compte de stockage configuré » dans le portail Azure][9]</span><span class="sxs-lookup"><span data-stu-id="e1d95-164">!['No storage account configured' warning in Azure portal][9]</span></span>

<span data-ttu-id="e1d95-165">Le service Batch utilise le compte de stockage associé pour stocker vos packages d’application.</span><span class="sxs-lookup"><span data-stu-id="e1d95-165">The Batch service uses the associated Storage account to store your application packages.</span></span> <span data-ttu-id="e1d95-166">Une fois que vous avez lié les deux comptes, Batch peut déployer automatiquement les packages stockés dans le compte de stockage lié sur vos nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="e1d95-166">After you've linked the two accounts, Batch can automatically deploy the packages stored in the linked Storage account to your compute nodes.</span></span> <span data-ttu-id="e1d95-167">Pour lier un compte de stockage à votre compte Batch, dans le panneau **Avertissement**, cliquez sur **Paramètres du compte de stockage**, puis, dans le panneau **Compte de stockage**, cliquez sur **Compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="e1d95-167">To link a Storage account to your Batch account, click **Storage account settings** on the **Warning** blade, and then click **Storage Account** on the **Storage Account** blade.</span></span>

<span data-ttu-id="e1d95-168">![Panneau Sélectionner un compte de stockage dans le Portail Azure][10]</span><span class="sxs-lookup"><span data-stu-id="e1d95-168">![Choose storage account blade in Azure portal][10]</span></span>

<span data-ttu-id="e1d95-169">Nous vous recommandons de créer un compte de stockage *spécifiquement* destiné à être utilisé avec votre compte Batch et de le sélectionner ici.</span><span class="sxs-lookup"><span data-stu-id="e1d95-169">We recommend that you create a Storage account *specifically* for use with your Batch account, and select it here.</span></span> <span data-ttu-id="e1d95-170">Pour plus d’informations sur la création d’un compte de stockage, consultez la section « Créer un compte de stockage » dans [À propos des comptes de stockage Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="e1d95-170">For details about how to create a storage account, see "Create a Storage account" in [About Azure Storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="e1d95-171">Après avoir créé un compte de stockage, vous pouvez le lier à votre compte Batch à l’aide du panneau **Compte de stockage** .</span><span class="sxs-lookup"><span data-stu-id="e1d95-171">After you've created a Storage account, you can then link it to your Batch account by using the **Storage Account** blade.</span></span>

> [!WARNING]
> <span data-ttu-id="e1d95-172">Le service Batch utilise un stockage Azure pour stocker vos packages d’application en tant qu’objets blob de blocs.</span><span class="sxs-lookup"><span data-stu-id="e1d95-172">The Batch service uses Azure Storage to store your application packages as block blobs.</span></span> <span data-ttu-id="e1d95-173">Vous êtes [facturé comme d’habitude][storage_pricing] pour les données d’objet blob de bloc.</span><span class="sxs-lookup"><span data-stu-id="e1d95-173">You are [charged as normal][storage_pricing] for the block blob data.</span></span> <span data-ttu-id="e1d95-174">Veillez à prendre en compte la taille et le nombre de vos packages d’application, ainsi qu’à supprimer régulièrement les packages obsolètes afin de minimiser les coûts.</span><span class="sxs-lookup"><span data-stu-id="e1d95-174">Be sure to consider the size and number of your application packages, and periodically remove deprecated packages to minimize costs.</span></span>
> 
> 

### <a name="view-current-applications"></a><span data-ttu-id="e1d95-175">Affichage des applications en cours</span><span class="sxs-lookup"><span data-stu-id="e1d95-175">View current applications</span></span>
<span data-ttu-id="e1d95-176">Pour visualiser les applications dans votre compte Batch, cliquez sur l’élément de menu **Applications** dans le menu gauche pendant que vous affichez le panneau **Compte Batch**.</span><span class="sxs-lookup"><span data-stu-id="e1d95-176">To view the applications in your Batch account, click the **Applications** menu item in the left menu while viewing the **Batch account** blade.</span></span>

<span data-ttu-id="e1d95-177">![Vignette Applications][2]</span><span class="sxs-lookup"><span data-stu-id="e1d95-177">![Applications tile][2]</span></span>

<span data-ttu-id="e1d95-178">La sélection de cette option de menu a pour effet d’ouvrir le panneau **Applications** :</span><span class="sxs-lookup"><span data-stu-id="e1d95-178">Selecting this menu option opens the **Applications** blade:</span></span>

<span data-ttu-id="e1d95-179">![Liste des applications][3]</span><span class="sxs-lookup"><span data-stu-id="e1d95-179">![List applications][3]</span></span>

<span data-ttu-id="e1d95-180">Le panneau **Applications** affiche l’ID de chaque application dans votre compte et les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="e1d95-180">The **Applications** blade displays the ID of each application in your account and the following properties:</span></span>

* <span data-ttu-id="e1d95-181">**Packages** : nombre de versions associées à cette application.</span><span class="sxs-lookup"><span data-stu-id="e1d95-181">**Packages**: The number of versions associated with this application.</span></span>
* <span data-ttu-id="e1d95-182">**Version par défaut** : version d’application installée si vous n’indiquez pas de version lorsque vous spécifiez l’application pour un pool.</span><span class="sxs-lookup"><span data-stu-id="e1d95-182">**Default version**: The application version installed if you do not indicate a version when you specify the application for a pool.</span></span> <span data-ttu-id="e1d95-183">Ce paramètre est facultatif.</span><span class="sxs-lookup"><span data-stu-id="e1d95-183">This setting is optional.</span></span>
* <span data-ttu-id="e1d95-184">**Autoriser les mises à jour** : valeur spécifiant si les mises à jour, les suppressions et les ajouts de packages sont autorisés.</span><span class="sxs-lookup"><span data-stu-id="e1d95-184">**Allow updates**: The value that specifies whether package updates, deletions, and additions are allowed.</span></span> <span data-ttu-id="e1d95-185">Si ce paramètre présente la valeur **Non**, les mises à jour et les suppressions de packages sont désactivées pour l’application.</span><span class="sxs-lookup"><span data-stu-id="e1d95-185">If this is set to **No**, package updates and deletions are disabled for the application.</span></span> <span data-ttu-id="e1d95-186">Seules les nouvelles versions de package d’application pourront être ajoutées.</span><span class="sxs-lookup"><span data-stu-id="e1d95-186">Only new application package versions can be added.</span></span> <span data-ttu-id="e1d95-187">La valeur par défaut de ce paramètre est **Oui**.</span><span class="sxs-lookup"><span data-stu-id="e1d95-187">The default is **Yes**.</span></span>

### <a name="view-application-details"></a><span data-ttu-id="e1d95-188">Affichage des détails de l’application</span><span class="sxs-lookup"><span data-stu-id="e1d95-188">View application details</span></span>
<span data-ttu-id="e1d95-189">Pour ouvrir le panneau contenant les détails d’une application, dans le panneau **Applications**, sélectionnez l’application.</span><span class="sxs-lookup"><span data-stu-id="e1d95-189">To open the blade that includes the details for an application, select the application in the **Applications** blade.</span></span>

<span data-ttu-id="e1d95-190">![Détails de l’application][4]</span><span class="sxs-lookup"><span data-stu-id="e1d95-190">![Application details][4]</span></span>

<span data-ttu-id="e1d95-191">Dans le panneau des détails de l’application, vous pouvez configurer les paramètres suivants pour votre application.</span><span class="sxs-lookup"><span data-stu-id="e1d95-191">In the application details blade, you can configure the following settings for your application.</span></span>

* <span data-ttu-id="e1d95-192">**Autoriser les mises à jour** : permet de spécifier si ses packages d’application peuvent être mis à jour ou supprimés.</span><span class="sxs-lookup"><span data-stu-id="e1d95-192">**Allow updates**: Specify whether its application packages can be updated or deleted.</span></span> <span data-ttu-id="e1d95-193">Voir la section « Mettre à jour ou supprimer un package d’application » dans la suite de cet article.</span><span class="sxs-lookup"><span data-stu-id="e1d95-193">See "Update or Delete an application package" later in this article.</span></span>
* <span data-ttu-id="e1d95-194">**Version par défaut** : permet de spécifier un package d’application par défaut à déployer sur les nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="e1d95-194">**Default version**: Specify a default application package to deploy to compute nodes.</span></span>
* <span data-ttu-id="e1d95-195">**Nom d’affichage** : permet de spécifier un nom « convivial » que votre solution Batch peut utiliser pendant l’affichage d’informations sur l’application, comme dans l’interface utilisateur d’un service que vous fournissez à vos clients via Batch.</span><span class="sxs-lookup"><span data-stu-id="e1d95-195">**Display name**: Specify a friendly name that your Batch solution can use when it displays information about the application, for example, in the UI of a service that you provide to your customers through Batch.</span></span>

### <a name="add-a-new-application"></a><span data-ttu-id="e1d95-196">Ajout d’une application</span><span class="sxs-lookup"><span data-stu-id="e1d95-196">Add a new application</span></span>
<span data-ttu-id="e1d95-197">Pour créer une application, ajoutez un package d’application et spécifiez un nouvel ID d’application unique.</span><span class="sxs-lookup"><span data-stu-id="e1d95-197">To create a new application, add an application package and specify a new, unique application ID.</span></span> <span data-ttu-id="e1d95-198">Le premier package d’application que vous ajoutez avec le nouvel ID d’application crée également l’application.</span><span class="sxs-lookup"><span data-stu-id="e1d95-198">The first application package that you add with the new application ID also creates the new application.</span></span>

<span data-ttu-id="e1d95-199">Dans le panneau **Applications**, cliquez sur **Ajouter** pour ouvrir le panneau **Nouvelle application**.</span><span class="sxs-lookup"><span data-stu-id="e1d95-199">Click **Add** on the **Applications** blade to open the **New application** blade.</span></span>

<span data-ttu-id="e1d95-200">![Panneau Nouvelle application dans le Portail Azure][5]</span><span class="sxs-lookup"><span data-stu-id="e1d95-200">![New application blade in Azure portal][5]</span></span>

<span data-ttu-id="e1d95-201">Le panneau **Nouvelle application** contient les champs ci-après pour vous permettre de spécifier les paramètres de la nouvelle application et du nouveau package d’application.</span><span class="sxs-lookup"><span data-stu-id="e1d95-201">The **New application** blade provides the following fields to specify the settings of your new application and application package.</span></span>

<span data-ttu-id="e1d95-202">**ID d’application**</span><span class="sxs-lookup"><span data-stu-id="e1d95-202">**Application id**</span></span>

<span data-ttu-id="e1d95-203">Ce champ spécifie l’ID de votre nouvelle application, qui est soumis aux règles de validation des ID Azure Batch standard.</span><span class="sxs-lookup"><span data-stu-id="e1d95-203">This field specifies the ID of your new application, which is subject to the standard Azure Batch ID validation rules.</span></span> <span data-ttu-id="e1d95-204">Les règles pour la fourniture d’un ID d’application sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="e1d95-204">The rules for providing an application ID are as follows:</span></span>

* <span data-ttu-id="e1d95-205">Sur des nœuds Windows, l’ID peut contenir n’importe quelle combinaison de caractères alphanumériques, de tirets et de traits de soulignement.</span><span class="sxs-lookup"><span data-stu-id="e1d95-205">On Windows nodes, the ID can contain any combination of alphanumeric characters, hyphens, and underscores.</span></span> <span data-ttu-id="e1d95-206">Sur des nœuds Linux, seuls les caractères alphanumériques et les traits de soulignement sont autorisés.</span><span class="sxs-lookup"><span data-stu-id="e1d95-206">On Linux nodes, only alphanumeric characters and underscores are permitted.</span></span>
* <span data-ttu-id="e1d95-207">Ne peut pas contenir plus de 64 caractères.</span><span class="sxs-lookup"><span data-stu-id="e1d95-207">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="e1d95-208">Doit être unique dans le compte Batch.</span><span class="sxs-lookup"><span data-stu-id="e1d95-208">Must be unique within the Batch account.</span></span>
* <span data-ttu-id="e1d95-209">Conserve la casse et ne respecte pas la casse.</span><span class="sxs-lookup"><span data-stu-id="e1d95-209">Is case-preserving and case-insensitive.</span></span>

<span data-ttu-id="e1d95-210">**Version**</span><span class="sxs-lookup"><span data-stu-id="e1d95-210">**Version**</span></span>

<span data-ttu-id="e1d95-211">Ce champ spécifie la version du package d’application que vous chargez.</span><span class="sxs-lookup"><span data-stu-id="e1d95-211">This field specifies the version of the application package you are uploading.</span></span> <span data-ttu-id="e1d95-212">Les chaînes de version sont soumises aux règles de validation suivantes :</span><span class="sxs-lookup"><span data-stu-id="e1d95-212">Version strings are subject to the following validation rules:</span></span>

* <span data-ttu-id="e1d95-213">Sur des nœuds Windows, la chaîne de version peut contenir n’importe quelle combinaison de caractères alphanumériques, de tirets, de traits de soulignement et de points.</span><span class="sxs-lookup"><span data-stu-id="e1d95-213">On Windows nodes, the version string can contain any combination of alphanumeric characters, hyphens, underscores, and periods.</span></span> <span data-ttu-id="e1d95-214">Sur des nœuds Linux, la chaîne de version peut contenir uniquement des caractères alphanumériques et des traits de soulignement.</span><span class="sxs-lookup"><span data-stu-id="e1d95-214">On Linux nodes, the version string can contain only alphanumeric characters and underscores.</span></span>
* <span data-ttu-id="e1d95-215">Ne peut pas contenir plus de 64 caractères.</span><span class="sxs-lookup"><span data-stu-id="e1d95-215">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="e1d95-216">Doit être unique dans l’application.</span><span class="sxs-lookup"><span data-stu-id="e1d95-216">Must be unique within the application.</span></span>
* <span data-ttu-id="e1d95-217">Conservent la casse et ne respectent pas la casse.</span><span class="sxs-lookup"><span data-stu-id="e1d95-217">Are case-preserving and case-insensitive.</span></span>

<span data-ttu-id="e1d95-218">**Package d’application**</span><span class="sxs-lookup"><span data-stu-id="e1d95-218">**Application package**</span></span>

<span data-ttu-id="e1d95-219">Ce champ spécifie le fichier .zip contenant les fichiers binaires de l’application et les fichiers de prise en charge qui sont requis pour l’exécution de l’application.</span><span class="sxs-lookup"><span data-stu-id="e1d95-219">This field specifies the .zip file that contains the application binaries and supporting files that are required to execute the application.</span></span> <span data-ttu-id="e1d95-220">Cliquez sur la zone **Sélectionner un fichier** ou sur l’icône de dossier pour rechercher et sélectionner un fichier .zip contenant les fichiers de votre application.</span><span class="sxs-lookup"><span data-stu-id="e1d95-220">Click the **Select a file** box or the folder icon to browse to and select a .zip file that contains your application's files.</span></span>

<span data-ttu-id="e1d95-221">Après avoir sélectionné un fichier, cliquez sur **OK** pour commencer le chargement dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="e1d95-221">After you've selected a file, click **OK** to begin the upload to Azure Storage.</span></span> <span data-ttu-id="e1d95-222">Une fois l’opération de chargement terminée, le portail affiche une notification et ferme le panneau.</span><span class="sxs-lookup"><span data-stu-id="e1d95-222">When the upload operation is complete, the portal displays a notification and closes the blade.</span></span> <span data-ttu-id="e1d95-223">Selon la taille du fichier que vous chargez et la vitesse de votre connexion réseau, cette opération peut prendre un certain temps.</span><span class="sxs-lookup"><span data-stu-id="e1d95-223">Depending on the size of the file that you are uploading and the speed of your network connection, this operation may take some time.</span></span>

> [!WARNING]
> <span data-ttu-id="e1d95-224">Ne fermez pas le panneau **Nouvelle application** avant que l’opération de chargement soit terminée.</span><span class="sxs-lookup"><span data-stu-id="e1d95-224">Do not close the **New application** blade before the upload operation is complete.</span></span> <span data-ttu-id="e1d95-225">La fermeture du panneau met fin au processus de chargement.</span><span class="sxs-lookup"><span data-stu-id="e1d95-225">Doing so will stop the upload process.</span></span>
> 
> 

### <a name="add-a-new-application-package"></a><span data-ttu-id="e1d95-226">Ajout d’un package d’application</span><span class="sxs-lookup"><span data-stu-id="e1d95-226">Add a new application package</span></span>
<span data-ttu-id="e1d95-227">Pour ajouter une nouvelle version de package d’application pour une application existante, sélectionnez une application dans le panneau **Applications**, cliquez sur **Packages**, puis sur **Ajouter** pour ouvrir le panneau **Ajouter un package**.</span><span class="sxs-lookup"><span data-stu-id="e1d95-227">To add a new application package version for an existing application, select an application in the **Applications** blade, click **Packages**, then click **Add** to open the **Add package** blade.</span></span>

<span data-ttu-id="e1d95-228">![Panneau Ajouter un package d’application dans le Portail Azure][8]</span><span class="sxs-lookup"><span data-stu-id="e1d95-228">![Add application package blade in Azure portal][8]</span></span>

<span data-ttu-id="e1d95-229">Comme vous pouvez le voir, les champs correspondent à ceux du panneau **Nouvelle application**, mais la zone **ID d’application** est désactivée.</span><span class="sxs-lookup"><span data-stu-id="e1d95-229">As you can see, the fields match those of the **New application** blade, but the **Application id** box is disabled.</span></span> <span data-ttu-id="e1d95-230">Comme vous l’avez fait pour la nouvelle application, spécifiez la **version** de votre nouveau package, accédez au fichier .zip de votre **package d’application**, puis cliquez sur **OK** pour charger le package.</span><span class="sxs-lookup"><span data-stu-id="e1d95-230">As you did for the new application, specify the **Version** for your new package, browse to your **Application package** .zip file, then click **OK** to upload the package.</span></span>

### <a name="update-or-delete-an-application-package"></a><span data-ttu-id="e1d95-231">Mettre à jour ou supprimer un package d’application</span><span class="sxs-lookup"><span data-stu-id="e1d95-231">Update or delete an application package</span></span>
<span data-ttu-id="e1d95-232">Pour mettre à jour ou supprimer un package d’application existant, ouvrez le panneau des détails de l’application, cliquez sur **Packages** pour ouvrir le panneau **Packages**, cliquez sur les **points de suspension** dans la ligne du package d’application que vous voulez modifier, puis sélectionnez l’action à exécuter.</span><span class="sxs-lookup"><span data-stu-id="e1d95-232">To update or delete an existing application package, open the details blade for the application, click **Packages** to open the **Packages** blade, click the **ellipsis** in the row of the application package that you want to modify, and select the action that you want to perform.</span></span>

<span data-ttu-id="e1d95-233">![Mettre à jour ou supprimer un package dans le Portail Azure][7]</span><span class="sxs-lookup"><span data-stu-id="e1d95-233">![Update or delete package in Azure portal][7]</span></span>

<span data-ttu-id="e1d95-234">**Mettre à jour**</span><span class="sxs-lookup"><span data-stu-id="e1d95-234">**Update**</span></span>

<span data-ttu-id="e1d95-235">Quand vous cliquez sur **Mettre à jour**, le panneau *Mettre à jour le package* s’affiche.</span><span class="sxs-lookup"><span data-stu-id="e1d95-235">When you click **Update**, the *Update package* blade is displayed.</span></span> <span data-ttu-id="e1d95-236">Ce panneau est semblable au panneau *Nouveau package d’application* ; toutefois, seul le champ de sélection du package est activé, ce qui vous permet de spécifier un nouveau fichier ZIP à charger.</span><span class="sxs-lookup"><span data-stu-id="e1d95-236">This blade is similar to the *New application package* blade, however only the package selection field is enabled, allowing you to specify a new ZIP file to upload.</span></span>

<span data-ttu-id="e1d95-237">![Panneau Mettre à jour un package dans le Portail Azure][11]</span><span class="sxs-lookup"><span data-stu-id="e1d95-237">![Update package blade in Azure portal][11]</span></span>

<span data-ttu-id="e1d95-238">**Supprimer**</span><span class="sxs-lookup"><span data-stu-id="e1d95-238">**Delete**</span></span>

<span data-ttu-id="e1d95-239">Lorsque vous cliquez sur **Supprimer**, vous êtes invité à confirmer la suppression de la version du package, puis Batch supprime le package du stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="e1d95-239">When you click **Delete**, you are asked to confirm the deletion of the package version, and Batch deletes the package from Azure Storage.</span></span> <span data-ttu-id="e1d95-240">Si vous supprimez la version par défaut d’une application, le paramètre **Version par défaut** est supprimé de l’application.</span><span class="sxs-lookup"><span data-stu-id="e1d95-240">If you delete the default version of an application, the **Default version** setting is removed for the application.</span></span>

<span data-ttu-id="e1d95-241">![Supprimer l’application][12]</span><span class="sxs-lookup"><span data-stu-id="e1d95-241">![Delete application ][12]</span></span>

## <a name="install-applications-on-compute-nodes"></a><span data-ttu-id="e1d95-242">Installation d’applications sur des nœuds de calcul</span><span class="sxs-lookup"><span data-stu-id="e1d95-242">Install applications on compute nodes</span></span>
<span data-ttu-id="e1d95-243">Maintenant que vous avez vu comment gérer les packages d’application avec le portail Azure, nous pouvons discuter de leur déploiement sur les nœuds de calcul et leur exécution avec des tâches Batch.</span><span class="sxs-lookup"><span data-stu-id="e1d95-243">Now that you've learned how to manage application packages with the Azure portal, we can discuss how to deploy them to compute nodes and run them with Batch tasks.</span></span>

### <a name="install-pool-application-packages"></a><span data-ttu-id="e1d95-244">Installation des packages d’application de pool</span><span class="sxs-lookup"><span data-stu-id="e1d95-244">Install pool application packages</span></span>
<span data-ttu-id="e1d95-245">Pour installer un package d’application sur les nœuds de calcul d’un pool, spécifiez au moins une *référence* de package d’application pour le pool.</span><span class="sxs-lookup"><span data-stu-id="e1d95-245">To install an application package on all compute nodes in a pool, specify one or more application package *references* for the pool.</span></span> <span data-ttu-id="e1d95-246">Les packages d’applications que vous spécifiez pour un pool sont installés sur chaque nœud de calcul lorsque ce nœud rejoint le pool, et lorsque le nœud est redémarré ou réinitialisé.</span><span class="sxs-lookup"><span data-stu-id="e1d95-246">The application packages that you specify for a pool are installed on each compute node when that node joins the pool, and when the node is rebooted or reimaged.</span></span>

<span data-ttu-id="e1d95-247">Dans Batch .NET, spécifiez une ou plusieurs propriétés [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref] lorsque vous créez un pool ou pour un pool existant.</span><span class="sxs-lookup"><span data-stu-id="e1d95-247">In Batch .NET, specify one or more [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref] when you create a new pool, or for an existing pool.</span></span> <span data-ttu-id="e1d95-248">La classe [ApplicationPackageReference][net_pkgref] spécifie un ID et la version d’une application à installer sur les nœuds de calcul d’un pool.</span><span class="sxs-lookup"><span data-stu-id="e1d95-248">The [ApplicationPackageReference][net_pkgref] class specifies an application ID and version to install on a pool's compute nodes.</span></span>

```csharp
// Create the unbound CloudPool
CloudPool myCloudPool =
    batchClient.PoolOperations.CreatePool(
        poolId: "myPool",
        targetDedicatedComputeNodes: 1,
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Specify the application and version to install on the compute nodes
myCloudPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "litware",
        Version = "1.1001.2b" }
};

// Commit the pool so that it's created in the Batch service. As the nodes join
// the pool, the specified application package is installed on each.
await myCloudPool.CommitAsync();
```

> [!IMPORTANT]
> <span data-ttu-id="e1d95-249">Si un déploiement de package d’application échoue pour une raison quelconque, le service Batch marque le nœud comme [inutilisable][net_nodestate], et aucune tâche n’est planifiée sur ce nœud.</span><span class="sxs-lookup"><span data-stu-id="e1d95-249">If an application package deployment fails for any reason, the Batch service marks the node [unusable][net_nodestate], and no tasks are scheduled for execution on that node.</span></span> <span data-ttu-id="e1d95-250">Dans ce cas, vous devez **redémarrer** le nœud pour relancer le déploiement du package.</span><span class="sxs-lookup"><span data-stu-id="e1d95-250">In this case, you should **restart** the node to reinitiate the package deployment.</span></span> <span data-ttu-id="e1d95-251">Le redémarrage du nœud réactive également la planification des tâches sur celui-ci.</span><span class="sxs-lookup"><span data-stu-id="e1d95-251">Restarting the node also enables task scheduling again on the node.</span></span>
> 
> 

### <a name="install-task-application-packages"></a><span data-ttu-id="e1d95-252">Installation des packages d’application de tâche</span><span class="sxs-lookup"><span data-stu-id="e1d95-252">Install task application packages</span></span>
<span data-ttu-id="e1d95-253">À l’instar de l’installation sur un pool, vous spécifiez les *références* de package d’application pour une tâche.</span><span class="sxs-lookup"><span data-stu-id="e1d95-253">Similar to a pool, you specify application package *references* for a task.</span></span> <span data-ttu-id="e1d95-254">Lorsqu’une tâche est planifiée pour s’exécuter sur un nœud, le package est téléchargé et extrait juste avant que la ligne de commande de la tâche soit exécutée.</span><span class="sxs-lookup"><span data-stu-id="e1d95-254">When a task is scheduled to run on a node, the package is downloaded and extracted just before the task's command line is executed.</span></span> <span data-ttu-id="e1d95-255">Si une version et un package spécifiés sont déjà installés sur le nœud, le package n’est pas téléchargé et le package existant est utilisé.</span><span class="sxs-lookup"><span data-stu-id="e1d95-255">If a specified package and version is already installed on the node, the package is not downloaded and the existing package is used.</span></span>

<span data-ttu-id="e1d95-256">Pour installer un package d’application de tâche, configurer la propriété [CloudTask][net_cloudtask].[ApplicationPackageReferences][net_cloudtask_pkgref] de la tâche :</span><span class="sxs-lookup"><span data-stu-id="e1d95-256">To install a task application package, configure the task's [CloudTask][net_cloudtask].[ApplicationPackageReferences][net_cloudtask_pkgref] property:</span></span>

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

## <a name="execute-the-installed-applications"></a><span data-ttu-id="e1d95-257">Exécution des applications installées</span><span class="sxs-lookup"><span data-stu-id="e1d95-257">Execute the installed applications</span></span>
<span data-ttu-id="e1d95-258">Les packages que vous avez spécifiés pour un pool ou une tâche sont téléchargés et extraits dans un répertoire nommé au sein du `AZ_BATCH_ROOT_DIR` du nœud.</span><span class="sxs-lookup"><span data-stu-id="e1d95-258">The packages that you've specified for a pool or task are downloaded and extracted to a named directory within the `AZ_BATCH_ROOT_DIR` of the node.</span></span> <span data-ttu-id="e1d95-259">Batch crée également une variable d’environnement qui contient le chemin d’accès au répertoire nommé.</span><span class="sxs-lookup"><span data-stu-id="e1d95-259">Batch also creates an environment variable that contains the path to the named directory.</span></span> <span data-ttu-id="e1d95-260">Vos lignes de commande de tâche utilisent cette variable d’environnement lors du référencement de l’application sur le nœud.</span><span class="sxs-lookup"><span data-stu-id="e1d95-260">Your task command lines use this environment variable when referencing the application on the node.</span></span> 

<span data-ttu-id="e1d95-261">Sur des nœuds Windows, le format de la variable est le suivant :</span><span class="sxs-lookup"><span data-stu-id="e1d95-261">On Windows nodes, the variable is in the following format:</span></span>

```
Windows:
AZ_BATCH_APP_PACKAGE_APPLICATIONID#version
```

<span data-ttu-id="e1d95-262">Sur des nœuds Linux, le format est légèrement différent.</span><span class="sxs-lookup"><span data-stu-id="e1d95-262">On Linux nodes, the format is slightly different.</span></span> <span data-ttu-id="e1d95-263">Les points (.), les tirets (-) et les signes dièse (#) sont aplatis en traits de soulignement dans la variable d’environnement.</span><span class="sxs-lookup"><span data-stu-id="e1d95-263">Periods (.), hypens (-) and number signs (#) are flattened to underscores in the environment variable.</span></span> <span data-ttu-id="e1d95-264">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="e1d95-264">For example:</span></span>

```
Linux:
AZ_BATCH_APP_PACKAGE_APPLICATIONID_version
```

<span data-ttu-id="e1d95-265">`APPLICATIONID` et `version` sont des valeurs qui correspondent à la version de l’application et du package que vous avez spécifiées pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="e1d95-265">`APPLICATIONID` and `version` are values that correspond to the application and package version you've specified for deployment.</span></span> <span data-ttu-id="e1d95-266">Par exemple, si vous spécifiez que la version 2.7 de l’application *blender* doit être installée sur des nœuds Windows, vos lignes de commande de tâche utilisent cette variable d’environnement pour accéder aux fichiers de l’application :</span><span class="sxs-lookup"><span data-stu-id="e1d95-266">For example, if you specified that version 2.7 of application *blender* should be installed on Windows nodes, your task command lines would use this environment variable to access its files:</span></span>

```
Windows:
AZ_BATCH_APP_PACKAGE_BLENDER#2.7
```

<span data-ttu-id="e1d95-267">Sur des nœuds Linux, spécifiez la variable d’environnement au format suivant :</span><span class="sxs-lookup"><span data-stu-id="e1d95-267">On Linux nodes, specify the environment variable in this format:</span></span>

```
Linux:
AZ_BATCH_APP_PACKAGE_BLENDER_2_7
``` 

<span data-ttu-id="e1d95-268">Lorsque vous téléchargez un package d’application, vous pouvez spécifier une version par défaut à déployer sur vos nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="e1d95-268">When you upload an application package, you can specify a default version to deploy to your compute nodes.</span></span> <span data-ttu-id="e1d95-269">Si vous avez spécifié une version par défaut pour une application, vous pouvez omettre le suffixe de version lorsque vous faites référence à l’application.</span><span class="sxs-lookup"><span data-stu-id="e1d95-269">If you have specified a default version for an application, you can omit the version suffix when you reference the application.</span></span> <span data-ttu-id="e1d95-270">Vous pouvez spécifier la version d’application par défaut sur le portail Azure, sur le panneau Applications, tel qu’illustré dans la section [Téléchargement et gestion des applications](#upload-and-manage-applications).</span><span class="sxs-lookup"><span data-stu-id="e1d95-270">You can specify the default application version in the Azure portal, on the Applications blade, as shown in [Upload and manage applications](#upload-and-manage-applications).</span></span>

<span data-ttu-id="e1d95-271">Par exemple, si vous définissez « 2.7 » comme version par défaut pour l’application *blender*, et si vos tâches référencent la variable d’environnement suivante, vos nœuds Windows exécutent la version 2.7 :</span><span class="sxs-lookup"><span data-stu-id="e1d95-271">For example, if you set "2.7" as the default version for application *blender*, and your tasks reference the following environment variable, then your Windows nodes will execute version 2.7:</span></span>

`AZ_BATCH_APP_PACKAGE_BLENDER`

<span data-ttu-id="e1d95-272">L’extrait de code suivant montre un exemple de ligne de commande de tâche qui lance la version par défaut de l’application *blender* :</span><span class="sxs-lookup"><span data-stu-id="e1d95-272">The following code snippet shows an example task command line that launches the default version of the *blender* application:</span></span>

```csharp
string taskId = "blendertask01";
string commandLine =
    @"cmd /c %AZ_BATCH_APP_PACKAGE_BLENDER%\blender.exe -args -here";
CloudTask blenderTask = new CloudTask(taskId, commandLine);
```

> [!TIP]
> <span data-ttu-id="e1d95-273">Pour plus d’informations sur les paramètres d’environnement de nœud de calcul, voir la section [Paramètres d’environnement des tâches](batch-api-basics.md#environment-settings-for-tasks) de l’article [Présentation des fonctionnalités du service Batch pour les développeurs](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="e1d95-273">See [Environment settings for tasks](batch-api-basics.md#environment-settings-for-tasks) in the [Batch feature overview](batch-api-basics.md) for more information about compute node environment settings.</span></span>
> 
> 

## <a name="update-a-pools-application-packages"></a><span data-ttu-id="e1d95-274">Mise à jour des packages d’applications d’un pool</span><span class="sxs-lookup"><span data-stu-id="e1d95-274">Update a pool's application packages</span></span>
<span data-ttu-id="e1d95-275">Si un pool existant a déjà été configuré avec un package d’application, vous pouvez spécifier un nouveau package pour le pool.</span><span class="sxs-lookup"><span data-stu-id="e1d95-275">If an existing pool has already been configured with an application package, you can specify a new package for the pool.</span></span> <span data-ttu-id="e1d95-276">Si vous spécifiez une nouvelle référence de package pour un pool, les points suivants s’appliquent :</span><span class="sxs-lookup"><span data-stu-id="e1d95-276">If you specify a new package reference for a pool, the following apply:</span></span>

* <span data-ttu-id="e1d95-277">Le service Batch installe le package nouvellement spécifié sur tous les nouveaux nœuds rejoignant le pool, ainsi que sur tout nœud actuel redémarré ou réinitialisé.</span><span class="sxs-lookup"><span data-stu-id="e1d95-277">The Batch service installs the newly specified package on all new nodes that join the pool and on any existing node that is rebooted or reimaged.</span></span>
* <span data-ttu-id="e1d95-278">Les nœuds de calcul qui sont déjà dans le pool lorsque vous mettez à jour les références du package n’installent pas automatiquement le nouveau package d’application.</span><span class="sxs-lookup"><span data-stu-id="e1d95-278">Compute nodes that are already in the pool when you update the package references do not automatically install the new application package.</span></span> <span data-ttu-id="e1d95-279">Ces nœuds de calcul doivent être redémarrés ou réinitialisés pour recevoir le nouveau package.</span><span class="sxs-lookup"><span data-stu-id="e1d95-279">These compute nodes must be rebooted or reimaged to receive the new package.</span></span>
* <span data-ttu-id="e1d95-280">Lorsqu’un nouveau package est déployé, les variables d’environnement créées reflètent les références du nouveau package d’application.</span><span class="sxs-lookup"><span data-stu-id="e1d95-280">When a new package is deployed, the created environment variables reflect the new application package references.</span></span>

<span data-ttu-id="e1d95-281">Dans cet exemple, le pool existant comporte la version 2.7 de l’application *blender* configurée comme l’une de ses propriétés [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref].</span><span class="sxs-lookup"><span data-stu-id="e1d95-281">In this example, the existing pool has version 2.7 of the *blender* application configured as one of its [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref].</span></span> <span data-ttu-id="e1d95-282">Pour mettre à jour les nœuds du pool avec la version 2.76b, spécifiez une nouvelle classe [ApplicationPackageReference][net_pkgref] avec la nouvelle version, puis validez la modification.</span><span class="sxs-lookup"><span data-stu-id="e1d95-282">To update the pool's nodes with version 2.76b, specify a new [ApplicationPackageReference][net_pkgref] with the new version, and commit the change.</span></span>

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

<span data-ttu-id="e1d95-283">Maintenant que la nouvelle version a été configurée, le service Batch installe la version 2.76b sur tout *nouveau* nœud rejoignant le pool.</span><span class="sxs-lookup"><span data-stu-id="e1d95-283">Now that the new version has been configured, the Batch service installs version 2.76b to any *new* node that joins the pool.</span></span> <span data-ttu-id="e1d95-284">Pour installer la version 2.76b sur des nœuds qui figurent *déjà* dans le pool, redémarrez ou réinitialisez ces derniers.</span><span class="sxs-lookup"><span data-stu-id="e1d95-284">To install 2.76b on the nodes that are *already* in the pool, reboot or reimage them.</span></span> <span data-ttu-id="e1d95-285">Notez que les nœuds redémarrés conservent les fichiers des déploiements précédents du package.</span><span class="sxs-lookup"><span data-stu-id="e1d95-285">Note that rebooted nodes retain the files from previous package deployments.</span></span>

## <a name="list-the-applications-in-a-batch-account"></a><span data-ttu-id="e1d95-286">Liste des applications dans un compte Batch</span><span class="sxs-lookup"><span data-stu-id="e1d95-286">List the applications in a Batch account</span></span>
<span data-ttu-id="e1d95-287">Vous pouvez lister les applications et leurs packages dans un compte Batch à l’aide de la méthode [ApplicationOperations][net_appops].[ListApplicationSummaries][net_appops_listappsummaries].</span><span class="sxs-lookup"><span data-stu-id="e1d95-287">You can list the applications and their packages in a Batch account by using the [ApplicationOperations][net_appops].[ListApplicationSummaries][net_appops_listappsummaries] method.</span></span>

```csharp
// List the applications and their application packages in the Batch account.
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

## <a name="wrap-up"></a><span data-ttu-id="e1d95-288">Conclusion</span><span class="sxs-lookup"><span data-stu-id="e1d95-288">Wrap up</span></span>
<span data-ttu-id="e1d95-289">Grâce aux packages d’application, vous pouvez aider vos clients à sélectionner les applications pour leurs travaux et à spécifier la version exacte à utiliser lors du traitement de travaux avec votre service Batch.</span><span class="sxs-lookup"><span data-stu-id="e1d95-289">With application packages, you can help your customers select the applications for their jobs and specify the exact version to use when processing jobs with your Batch-enabled service.</span></span> <span data-ttu-id="e1d95-290">Vous pouvez également fournir à vos clients la possibilité de télécharger et d’effectuer le suivi de leurs propres applications dans votre service.</span><span class="sxs-lookup"><span data-stu-id="e1d95-290">You might also provide the ability for your customers to upload and track their own applications in your service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1d95-291">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e1d95-291">Next steps</span></span>
* <span data-ttu-id="e1d95-292">[L’API REST Batch][api_rest] prend également en charge l’utilisation de packages d’application.</span><span class="sxs-lookup"><span data-stu-id="e1d95-292">The [Batch REST API][api_rest] also provides support to work with application packages.</span></span> <span data-ttu-id="e1d95-293">Par exemple, pour plus d’informations sur la spécification des packages à installer à l’aide de l’API REST, voir l’élément [applicationPackageReferences][rest_add_pool_with_packages] de l’article [Ajouter un pool à un compte][rest_add_pool].</span><span class="sxs-lookup"><span data-stu-id="e1d95-293">For example, see the [applicationPackageReferences][rest_add_pool_with_packages] element in [Add a pool to an account][rest_add_pool] for information about how to specify packages to install by using the REST API.</span></span> <span data-ttu-id="e1d95-294">Pour plus de détails sur l’obtention d’informations sur l’application à l’aide de l’API REST Batch, consultez la page [Applications][rest_applications].</span><span class="sxs-lookup"><span data-stu-id="e1d95-294">See [Applications][rest_applications] for details about how to obtain application information by using the Batch REST API.</span></span>
* <span data-ttu-id="e1d95-295">Découvrez comment [gérer les quotas et les comptes Azure Batch avec Batch Management .NET](batch-management-dotnet.md)par programme.</span><span class="sxs-lookup"><span data-stu-id="e1d95-295">Learn how to programmatically [manage Azure Batch accounts and quotas with Batch Management .NET](batch-management-dotnet.md).</span></span> <span data-ttu-id="e1d95-296">La bibliothèque [Batch Management .NET][api_net_mgmt] peut activer les fonctionnalités de création et de suppression de compte pour votre application ou service Batch.</span><span class="sxs-lookup"><span data-stu-id="e1d95-296">The [Batch Management .NET][api_net_mgmt] library can enable account creation and deletion features for your Batch application or service.</span></span>

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
