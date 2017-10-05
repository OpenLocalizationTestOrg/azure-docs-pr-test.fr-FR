---
title: "Capacité dédiée pour les travaux du service d’exécution de lot de Machine Learning | Microsoft Docs"
description: "Vue d’ensemble du service Azure Batch pour les travaux Machine Learning."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.service: machine-learning
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 3879eb3d0c6fa9d74fff01b07f5c07d3991dfbbd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-batch-service-for-machine-learning-jobs"></a><span data-ttu-id="40133-103">Service Azure Batch pour les travaux Machine Learning</span><span class="sxs-lookup"><span data-stu-id="40133-103">Azure Batch service for Machine Learning jobs</span></span>

<span data-ttu-id="40133-104">Le traitement par pool Batch de Machine Learning utilise une échelle gérée par le client pour le service d’exécution de lot d’Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="40133-104">Machine Learning Batch Pool processing provides customer-managed scale for the Azure Machine Learning Batch Execution Service.</span></span> <span data-ttu-id="40133-105">Le traitement par lots classique pour Machine Learning a lieu dans un environnement multi-clients, qui limite le nombre de travaux simultanés que vous pouvez soumettre. Les travaux sont mis en file d’attente d’après le principe premier entré, premier sorti.</span><span class="sxs-lookup"><span data-stu-id="40133-105">Classic batch processing for machine learning takes place in a multi-tenant environment, which limits the number of concurrent jobs you can submit, and jobs are queued on a first-in-first-out basis.</span></span> <span data-ttu-id="40133-106">Cette incertitude signifie que vous ne pouvez pas prédire précisément à quel moment votre travail sera exécuté.</span><span class="sxs-lookup"><span data-stu-id="40133-106">This uncertainty means that you can't accurately predict when your job will run.</span></span>

<span data-ttu-id="40133-107">Le traitement par pool Batch vous permet de créer des pools dans lesquels vous pouvez soumettre des programmes de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="40133-107">Batch Pool processing allows you to create pools on which you can submit batch jobs.</span></span> <span data-ttu-id="40133-108">Vous contrôlez la taille du pool ainsi que le pool auquel le travail est soumis.</span><span class="sxs-lookup"><span data-stu-id="40133-108">You control the size of the pool, and to which pool the job is submitted.</span></span> <span data-ttu-id="40133-109">Le travail du service d’exécution de lot s’exécute dans son propre espace de traitement fournissant ainsi des performances de traitement prévisibles et la possibilité de créer des pools de ressources qui correspondent à la charge de traitement que vous soumettez.</span><span class="sxs-lookup"><span data-stu-id="40133-109">Your BES job runs in its own processing space providing predictable processing performance and the ability to create resource pools that correspond to the processing load that you submit.</span></span>

## <a name="how-to-use-batch-pool-processing"></a><span data-ttu-id="40133-110">Comment utiliser le traitement par pool Batch</span><span class="sxs-lookup"><span data-stu-id="40133-110">How to use Batch Pool processing</span></span>

<span data-ttu-id="40133-111">La configuration du traitement par pool Batch n’est pas disponible actuellement via le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="40133-111">Configuration of Batch Pool Processing is not currently available through the Azure portal.</span></span> <span data-ttu-id="40133-112">Pour utiliser le traitement par pool Batch, vous devez :</span><span class="sxs-lookup"><span data-stu-id="40133-112">To use Batch Pool processing, you must:</span></span>

-   <span data-ttu-id="40133-113">appeler le service CSS pour créer un compte de pool Batch et obtenir une URL de service du pool et une clé d’autorisation ;</span><span class="sxs-lookup"><span data-stu-id="40133-113">Call CSS to create a Batch Pool Account and obtain a Pool Service URL and an authorization key</span></span>
-   <span data-ttu-id="40133-114">créer un service web et un plan de facturation basés sur un nouveau Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="40133-114">Create a New Resource Manager based web service and billing plan</span></span>

<span data-ttu-id="40133-115">Pour créer votre compte, appelez le Support technique et Service clientèle Microsoft (CSS) et indiquez votre ID d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="40133-115">To create your account, call Microsoft Customer Service and Support (CSS) and provide your Subscription ID.</span></span> <span data-ttu-id="40133-116">CSS collabore avec vous pour déterminer la capacité appropriée à votre situation.</span><span class="sxs-lookup"><span data-stu-id="40133-116">CSS will work with you to determine the appropriate capacity for your scenario.</span></span> <span data-ttu-id="40133-117">CSS configure ensuite votre compte avec le nombre maximal de pools que vous pouvez créer et le nombre maximal de machines virtuelles que vous pouvez placer dans chaque pool.</span><span class="sxs-lookup"><span data-stu-id="40133-117">CSS then configures your account with the maximum number of pools you can create and the maximum number of virtual machines (VMs) that you can place in each pool.</span></span> <span data-ttu-id="40133-118">Une fois votre compte configuré, vous recevez l’URL de service du pool et une clé d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="40133-118">Once your account is configured, you are provided your Pool Service URL and an authorization key.</span></span>

<span data-ttu-id="40133-119">Une fois votre compte créé, vous utilisez l’URL de service du pool et une clé d’autorisation pour effectuer des opérations de gestion de pool sur votre pool Batch.</span><span class="sxs-lookup"><span data-stu-id="40133-119">After your account is created, you use the Pool Service URL and authorization key to perform pool management operations on your Batch Pool.</span></span>

![Architecture de service du pool Batch.](media/machine-learning-dedicated-capacity-for-bes-jobs/pool-architecture.png)

<span data-ttu-id="40133-121">Créez des pools en appelant l’opération Créer un pool dans l’URL de service du pool qui vous a été fournie par CSS.</span><span class="sxs-lookup"><span data-stu-id="40133-121">You create pools by calling the Create Pool operation on the pool service URL that CSS provided to you.</span></span> <span data-ttu-id="40133-122">Lorsque vous créez un pool, spécifiez le nombre de machines virtuelles et l’URL du fichier swagger.json d’un service web Machine Learning basé sur un nouveau Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="40133-122">When you create a pool, specify the number of VMs and the URL of the swagger.json of a New Resource Manager based Machine Learning web service.</span></span> <span data-ttu-id="40133-123">Ce service web est fourni pour établir l’association de facturation.</span><span class="sxs-lookup"><span data-stu-id="40133-123">This web service is provided to establish the billing association.</span></span> <span data-ttu-id="40133-124">Le service du pool Batch utilise le fichier swagger.json pour associer le pool à un plan de facturation.</span><span class="sxs-lookup"><span data-stu-id="40133-124">The Batch Pool service uses the swagger.json to associate the pool with a billing plan.</span></span> <span data-ttu-id="40133-125">Vous pouvez exécuter n’importe quel service web du service d’exécution de lot, classique ou basé sur le nouveau Resource Manager, que vous choisissez dans le pool.</span><span class="sxs-lookup"><span data-stu-id="40133-125">You can run any BES web service, both New Resource Manager based and classic, you choose on the pool.</span></span>

<span data-ttu-id="40133-126">Vous pouvez utiliser n’importe quel service web basé sur le nouveau Resource Manager, mais sachez que la facturation correspondant aux travaux est établie par rapport au plan de facturation associé à ce service.</span><span class="sxs-lookup"><span data-stu-id="40133-126">You can use any New Resource Manager based web service, but be aware that the billing for the jobs are charged against the billing plan associated with that service.</span></span> <span data-ttu-id="40133-127">Vous pouvez créer un service web et un plan de facturation spécialement pour l’exécution des travaux du pool Batch.</span><span class="sxs-lookup"><span data-stu-id="40133-127">You may want to create a web service and new billing plan specifically for running Batch Pool jobs.</span></span>

<span data-ttu-id="40133-128">Pour plus d’informations sur la création de services web, consultez [Déploiement d’un service web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="40133-128">For more information on creating web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="40133-129">Une fois que vous avez créé un pool, soumettez le travail du service d’exécution de lot à l’aide de l’URL des requêtes de lots du service web.</span><span class="sxs-lookup"><span data-stu-id="40133-129">Once you have created a pool, you submit the BES job using the Batch Requests URL for the web service.</span></span> <span data-ttu-id="40133-130">Vous pouvez choisir de le soumettre à un traitement par lots classique ou par pool.</span><span class="sxs-lookup"><span data-stu-id="40133-130">You can choose to submit it to a pool or to classic batch processing.</span></span> <span data-ttu-id="40133-131">Pour soumettre un travail au traitement par pool Batch, ajoutez le paramètre suivant dans le corps de la demande de soumission de travail :</span><span class="sxs-lookup"><span data-stu-id="40133-131">To submit a job to Batch Pool processing, you add the following parameter to the job submission request body:</span></span>

<span data-ttu-id="40133-132">« AzureBatchPoolId »:« &lt;ID du pool&gt; »</span><span class="sxs-lookup"><span data-stu-id="40133-132">"AzureBatchPoolId":"&lt;pool ID&gt;"</span></span>

<span data-ttu-id="40133-133">Si vous n’ajoutez pas le paramètre, le travail est exécuté dans l’environnement du processus classique de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="40133-133">If you do not add the parameter, the job is run in the classic batch process environment.</span></span> <span data-ttu-id="40133-134">Si le pool possède des ressources disponibles, le travail démarre immédiatement.</span><span class="sxs-lookup"><span data-stu-id="40133-134">If the pool has available resources, the job starts running immediately.</span></span> <span data-ttu-id="40133-135">S’il n’en possède pas, votre travail est mis en file d’attente jusqu’à ce qu’une ressource soit disponible.</span><span class="sxs-lookup"><span data-stu-id="40133-135">If the pool does not have free resources, your job is queued until a resource is available.</span></span>

<span data-ttu-id="40133-136">Si vous estimez que vous atteignez régulièrement la limite de la capacité de vos pools et que vous devez l’augmenter, vous pouvez appeler CSS et demander à un représentant d’accroître vos quotas.</span><span class="sxs-lookup"><span data-stu-id="40133-136">If you find that you regularly reach the capacity of your pools, and you need increased capacity, you can call CSS and work with a representative to increase your quotas.</span></span>

<span data-ttu-id="40133-137">Exemple de demande :</span><span class="sxs-lookup"><span data-stu-id="40133-137">Example Request:</span></span>

<span data-ttu-id="40133-138">https://ussouthcentral.services.azureml.net/subscriptions/80c77c7674ba4c8c82294c3b2957990c/services/9fe659022c9747e3b9b7b923c3830623/jobs?api-version=2.0</span><span class="sxs-lookup"><span data-stu-id="40133-138">https://ussouthcentral.services.azureml.net/subscriptions/80c77c7674ba4c8c82294c3b2957990c/services/9fe659022c9747e3b9b7b923c3830623/jobs?api-version=2.0</span></span>

```json
{

    "Input":{
    
        "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpoint
        =https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://zhguim
        l.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;;",
        
        "BaseLocation":null,
        
        "RelativeLocation":"testint/AdultCensusIncomeBinaryClassificationDataset.csv",
        
        "SasBlobToken":null
    
    },
    
    "GlobalParameters":{ },
    
    "Outputs":{
    
        "output1":{
        
            "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpo
            int=https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://sampleaccount.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;",
            "BaseLocation":null,
            "RelativeLocation":"testintoutput/testint\_results.csv",
            
            "SasBlobToken":null
        
        }
    
    },
    
    "AzureBatchPoolId":"8dfc151b0d3e446497b845f3b29ef53b"

}
```

## <a name="considerations-when-using-batch-pool-processing"></a><span data-ttu-id="40133-139">Considérations relatives à l’utilisation du traitement par pool Batch</span><span class="sxs-lookup"><span data-stu-id="40133-139">Considerations when using Batch Pool processing</span></span>

<span data-ttu-id="40133-140">Le traitement par pool Batch est un service toujours facturable qui vous oblige à l’associer à un plan de facturation basé sur un Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="40133-140">Batch Pool Processing is an always-on billable service and that requires you to associate it with a Resource Manager based billing plan.</span></span> <span data-ttu-id="40133-141">Vous êtes facturé uniquement pour le nombre d’heures de calcul d’exécution du pool, quel que soit le nombre de travaux exécutés au cours de ce temps.</span><span class="sxs-lookup"><span data-stu-id="40133-141">You are only billed for the number of compute hours the pool is running; regardless of the number of jobs run during that time pool.</span></span> <span data-ttu-id="40133-142">Si vous créez un pool, vous êtes facturé pour les heures de calcul de chaque machine virtuelle du pool jusqu’à ce qu’il soit supprimé, même si aucun travail de traitement par lots ne s’exécute dans le pool.</span><span class="sxs-lookup"><span data-stu-id="40133-142">If you create a pool, you are billed for the compute hours of each virtual machine in the pool until the pool is deleted, even if no batch jobs are running in the pool.</span></span> <span data-ttu-id="40133-143">La facturation des machines virtuelles démarre lorsque leur approvisionnement est terminé et s’arrête lorsqu’elles ont été supprimées.</span><span class="sxs-lookup"><span data-stu-id="40133-143">Billing for the virtual machines starts when they have finished provisioning and stops when they have been deleted.</span></span> <span data-ttu-id="40133-144">Vous pouvez utiliser l’un des plans indiqués dans la [Machine Learning Tarification](https://azure.microsoft.com/pricing/details/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="40133-144">You can use any of the plans found on the [Machine Learning Pricing page](https://azure.microsoft.com/pricing/details/machine-learning/).</span></span>

<span data-ttu-id="40133-145">Exemple de facturation :</span><span class="sxs-lookup"><span data-stu-id="40133-145">Billing example:</span></span>

<span data-ttu-id="40133-146">Si vous créez un pool Batch comprenant 2 machines virtuelles et le supprimez après 24 heures, votre plan de facturation est débité de 48 heures de calcul quel que soit le nombre de travaux exécutés pendant cette période.</span><span class="sxs-lookup"><span data-stu-id="40133-146">If you create a Batch Pool with 2 virtual machines and delete it after 24 hours your billing plan is debited 48 compute hours; regardless of how many jobs were run during that period.</span></span>

<span data-ttu-id="40133-147">Si vous créez un pool Batch comportant 4 machines virtuelles et le supprimez après 12 heures, votre plan de facturation est également débité de 48 heures de calcul.</span><span class="sxs-lookup"><span data-stu-id="40133-147">If you create a Batch Pool with 4 virtual machines and delete it after 12 hours, your billing plan is also debited 48 compute hours.</span></span>

<span data-ttu-id="40133-148">Nous vous recommandons d’interroger l’état des travaux pour déterminer leur achèvement.</span><span class="sxs-lookup"><span data-stu-id="40133-148">We recommend that you poll the job status to determine when jobs complete.</span></span> <span data-ttu-id="40133-149">Lorsque l’exécution de tous vos travaux est terminée, appelez l’opération de redimensionnement du pool pour définir le nombre de machines virtuelles du pool sur zéro.</span><span class="sxs-lookup"><span data-stu-id="40133-149">When all your jobs have finished running, call the Resize Pool operation to set the number of virtual machines in the pool to zero.</span></span> <span data-ttu-id="40133-150">Si vous manquez de ressources de pool et que vous devez créer un pool, par exemple pour facturer sur un autre plan de facturation, il est préférable de supprimer le pool lorsque l’exécution de tous les travaux est terminée.</span><span class="sxs-lookup"><span data-stu-id="40133-150">If you are short on pool resources and you need to create a new pool, for example to bill against a different billing plan, you can delete the pool instead when all your jobs have finished running.</span></span>


| <span data-ttu-id="40133-151">**Utilisez le traitement par pool Batch si**</span><span class="sxs-lookup"><span data-stu-id="40133-151">**Use Batch Pool Processing when**</span></span>    | <span data-ttu-id="40133-152">**Utilisez le traitement par lots classique si**</span><span class="sxs-lookup"><span data-stu-id="40133-152">**Use classic batch processing when**</span></span>  |
|---|---|
|<span data-ttu-id="40133-153">Vous devez exécuter un grand nombre de travaux</span><span class="sxs-lookup"><span data-stu-id="40133-153">You need to run a large number of jobs</span></span><br><span data-ttu-id="40133-154">Ou</span><span class="sxs-lookup"><span data-stu-id="40133-154">Or</span></span><br/><span data-ttu-id="40133-155">Vos travaux doivent s’exécuter immédiatement</span><span class="sxs-lookup"><span data-stu-id="40133-155">You need to know that your jobs will run immediately</span></span><br/><span data-ttu-id="40133-156">Ou</span><span class="sxs-lookup"><span data-stu-id="40133-156">Or</span></span><br/><span data-ttu-id="40133-157">Vous avez besoin d’un débit garanti.</span><span class="sxs-lookup"><span data-stu-id="40133-157">You need guaranteed throughput.</span></span> <span data-ttu-id="40133-158">Par exemple, vous devez exécuter plusieurs travaux dans un laps de temps donné et souhaitez augmenter la taille des instances de vos ressources de calcul pour satisfaire à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="40133-158">For example, you need to run a number of jobs in a given time frame, and want to scale out your compute resources to meet your needs.</span></span>    | <span data-ttu-id="40133-159">Vous exécutez quelques travaux</span><span class="sxs-lookup"><span data-stu-id="40133-159">You are running just a few jobs</span></span><br/><span data-ttu-id="40133-160">and</span><span class="sxs-lookup"><span data-stu-id="40133-160">And</span></span><br/> <span data-ttu-id="40133-161">Vous n’avez pas besoin que les travaux s’exécutent immédiatement</span><span class="sxs-lookup"><span data-stu-id="40133-161">You don’t need the jobs to run immediately</span></span> |
