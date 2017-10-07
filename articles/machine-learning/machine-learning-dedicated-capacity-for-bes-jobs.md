---
title: "aaaDedicated capacité pour les tâches d’exécution Service Machine Learning lot | Documents Microsoft"
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
ms.openlocfilehash: bba7970bb31c50e5b0b9d5f4ff4f0d2dacf942e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-batch-service-for-machine-learning-jobs"></a><span data-ttu-id="673ad-103">Service Azure Batch pour les travaux Machine Learning</span><span class="sxs-lookup"><span data-stu-id="673ad-103">Azure Batch service for Machine Learning jobs</span></span>

<span data-ttu-id="673ad-104">Le traitement du Pool de traitement par lots d’apprentissage machine prévoit hello Azure Machine Learning Batch Execution Service gérée par le client de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="673ad-104">Machine Learning Batch Pool processing provides customer-managed scale for hello Azure Machine Learning Batch Execution Service.</span></span> <span data-ttu-id="673ad-105">Lot classique pour l’apprentissage de traitement s’effectue dans une architecture mutualisée, le numéro de hello limites de travaux simultanés, vous pouvez soumettre et travaux est en attente sur une base in-first-out.</span><span class="sxs-lookup"><span data-stu-id="673ad-105">Classic batch processing for machine learning takes place in a multi-tenant environment, which limits hello number of concurrent jobs you can submit, and jobs are queued on a first-in-first-out basis.</span></span> <span data-ttu-id="673ad-106">Cette incertitude signifie que vous ne pouvez pas prédire précisément à quel moment votre travail sera exécuté.</span><span class="sxs-lookup"><span data-stu-id="673ad-106">This uncertainty means that you can't accurately predict when your job will run.</span></span>

<span data-ttu-id="673ad-107">Le traitement par lots Pool vous permet de pools toocreate sur lequel vous pouvez soumettre des traitements par lots.</span><span class="sxs-lookup"><span data-stu-id="673ad-107">Batch Pool processing allows you toocreate pools on which you can submit batch jobs.</span></span> <span data-ttu-id="673ad-108">Contrôle de taille hello du pool de hello et toowhich pool hello travail est envoyé.</span><span class="sxs-lookup"><span data-stu-id="673ad-108">You control hello size of hello pool, and toowhich pool hello job is submitted.</span></span> <span data-ttu-id="673ad-109">Votre travail BES s’exécute dans son propre traitement espace fournissant des performances de traitement prévisibles et le hello capacité toocreate pools de ressources qui correspondant la charge de traitement toohello que vous envoyez.</span><span class="sxs-lookup"><span data-stu-id="673ad-109">Your BES job runs in its own processing space providing predictable processing performance and hello ability toocreate resource pools that correspond toohello processing load that you submit.</span></span>

## <a name="how-toouse-batch-pool-processing"></a><span data-ttu-id="673ad-110">Comment le traitement du Pool de traitement par lots toouse</span><span class="sxs-lookup"><span data-stu-id="673ad-110">How toouse Batch Pool processing</span></span>

<span data-ttu-id="673ad-111">Configuration du Pool de traitement par lot n’est pas actuellement disponible via hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="673ad-111">Configuration of Batch Pool Processing is not currently available through hello Azure portal.</span></span> <span data-ttu-id="673ad-112">toouse Pool de traitement par lots de traitement, vous devez :</span><span class="sxs-lookup"><span data-stu-id="673ad-112">toouse Batch Pool processing, you must:</span></span>

-   <span data-ttu-id="673ad-113">Appelez CSS toocreate un compte de Pool de traitement par lots et obtenir une URL de Service du Pool et une clé d’autorisation</span><span class="sxs-lookup"><span data-stu-id="673ad-113">Call CSS toocreate a Batch Pool Account and obtain a Pool Service URL and an authorization key</span></span>
-   <span data-ttu-id="673ad-114">créer un service web et un plan de facturation basés sur un nouveau Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="673ad-114">Create a New Resource Manager based web service and billing plan</span></span>

<span data-ttu-id="673ad-115">toocreate votre compte, appelez le Support technique et Service clientèle Microsoft et fournir votre ID d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="673ad-115">toocreate your account, call Microsoft Customer Service and Support (CSS) and provide your Subscription ID.</span></span> <span data-ttu-id="673ad-116">CSS fonctionneront avec vous toodetermine hello capacité appropriée pour votre scénario.</span><span class="sxs-lookup"><span data-stu-id="673ad-116">CSS will work with you toodetermine hello appropriate capacity for your scenario.</span></span> <span data-ttu-id="673ad-117">CSS configure ensuite votre compte avec un nombre maximal de pools, vous pouvez créer et nombre maximal de machines virtuelles (VM) que vous pouvez placer dans chaque pool de hello hello.</span><span class="sxs-lookup"><span data-stu-id="673ad-117">CSS then configures your account with hello maximum number of pools you can create and hello maximum number of virtual machines (VMs) that you can place in each pool.</span></span> <span data-ttu-id="673ad-118">Une fois votre compte configuré, vous recevez l’URL de service du pool et une clé d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="673ad-118">Once your account is configured, you are provided your Pool Service URL and an authorization key.</span></span>

<span data-ttu-id="673ad-119">Après la création de votre compte, vous utiliser hello URL du Service de Pool et l’autorisation tooperform clé pool opérations de gestion sur votre Pool de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="673ad-119">After your account is created, you use hello Pool Service URL and authorization key tooperform pool management operations on your Batch Pool.</span></span>

![Architecture de service du pool Batch.](media/machine-learning-dedicated-capacity-for-bes-jobs/pool-architecture.png)

<span data-ttu-id="673ad-121">Pour créer des pools par l’appel d’opération de créer un Pool de hello d’URL de service du pool hello que tooyou CSS fourni.</span><span class="sxs-lookup"><span data-stu-id="673ad-121">You create pools by calling hello Create Pool operation on hello pool service URL that CSS provided tooyou.</span></span> <span data-ttu-id="673ad-122">Lorsque vous créez un pool, spécifiez le nombre hello de machines virtuelles et les URL de hello de hello swagger.json d’un nouveau gestionnaire de ressources en fonction de service web Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="673ad-122">When you create a pool, specify hello number of VMs and hello URL of hello swagger.json of a New Resource Manager based Machine Learning web service.</span></span> <span data-ttu-id="673ad-123">Ce service web est fourni association de facturation tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="673ad-123">This web service is provided tooestablish hello billing association.</span></span> <span data-ttu-id="673ad-124">Hello service du Pool de traitement par lots utilise le pool de hello hello swagger.json tooassociate avec un plan de facturation.</span><span class="sxs-lookup"><span data-stu-id="673ad-124">hello Batch Pool service uses hello swagger.json tooassociate hello pool with a billing plan.</span></span> <span data-ttu-id="673ad-125">Vous pouvez exécuter n’importe quel BES service web, les deux nouveau gestionnaire de ressources en fonction et classique, cliquez sur le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="673ad-125">You can run any BES web service, both New Resource Manager based and classic, you choose on hello pool.</span></span>

<span data-ttu-id="673ad-126">Vous pouvez utiliser n’importe quel service web d’en fonction du nouveau gestionnaire de ressources, mais sachez que facturation hello pour les travaux de hello sont facturées par rapport au plan de facturation hello associé au service.</span><span class="sxs-lookup"><span data-stu-id="673ad-126">You can use any New Resource Manager based web service, but be aware that hello billing for hello jobs are charged against hello billing plan associated with that service.</span></span> <span data-ttu-id="673ad-127">Vous souhaiterez toocreate un service web et la facturation nouveau plan spécialement pour l’exécution des travaux du Pool de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="673ad-127">You may want toocreate a web service and new billing plan specifically for running Batch Pool jobs.</span></span>

<span data-ttu-id="673ad-128">Pour plus d’informations sur la création de services web, consultez [Déploiement d’un service web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="673ad-128">For more information on creating web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="673ad-129">Une fois que vous avez créé un pool, vous envoyez hello BES à l’aide de la tâche hello URL des demandes de lot pour le service web de hello.</span><span class="sxs-lookup"><span data-stu-id="673ad-129">Once you have created a pool, you submit hello BES job using hello Batch Requests URL for hello web service.</span></span> <span data-ttu-id="673ad-130">Vous pouvez choisir toosubmit il tooa pool ou tooclassic le traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="673ad-130">You can choose toosubmit it tooa pool or tooclassic batch processing.</span></span> <span data-ttu-id="673ad-131">toosubmit un tooBatch Pool de traitement, vous ajoutez hello suivant le corps de la demande du travail envoi de paramètre toohello :</span><span class="sxs-lookup"><span data-stu-id="673ad-131">toosubmit a job tooBatch Pool processing, you add hello following parameter toohello job submission request body:</span></span>

<span data-ttu-id="673ad-132">« AzureBatchPoolId »:« &lt;ID du pool&gt; »</span><span class="sxs-lookup"><span data-stu-id="673ad-132">"AzureBatchPoolId":"&lt;pool ID&gt;"</span></span>

<span data-ttu-id="673ad-133">Si vous n’ajoutez pas de paramètre hello, travail de hello est exécuté dans un environnement de processus de lot classique hello.</span><span class="sxs-lookup"><span data-stu-id="673ad-133">If you do not add hello parameter, hello job is run in hello classic batch process environment.</span></span> <span data-ttu-id="673ad-134">Si le pool de hello a des ressources disponibles, hello commence immédiatement.</span><span class="sxs-lookup"><span data-stu-id="673ad-134">If hello pool has available resources, hello job starts running immediately.</span></span> <span data-ttu-id="673ad-135">Si le pool de hello n’a pas de libérer des ressources, votre travail est en file d’attente jusqu'à ce qu’une ressource est disponible.</span><span class="sxs-lookup"><span data-stu-id="673ad-135">If hello pool does not have free resources, your job is queued until a resource is available.</span></span>

<span data-ttu-id="673ad-136">Si vous trouvez que vous atteignez régulièrement vos pools de capacité hello, et que vous devez augmenter sa capacité, vous pouvez appeler CSS et manipuler un tooincrease représentatif de vos quotas.</span><span class="sxs-lookup"><span data-stu-id="673ad-136">If you find that you regularly reach hello capacity of your pools, and you need increased capacity, you can call CSS and work with a representative tooincrease your quotas.</span></span>

<span data-ttu-id="673ad-137">Exemple de demande :</span><span class="sxs-lookup"><span data-stu-id="673ad-137">Example Request:</span></span>

<span data-ttu-id="673ad-138">https://ussouthcentral.services.azureml.net/subscriptions/80c77c7674ba4c8c82294c3b2957990c/services/9fe659022c9747e3b9b7b923c3830623/jobs?api-version=2.0</span><span class="sxs-lookup"><span data-stu-id="673ad-138">https://ussouthcentral.services.azureml.net/subscriptions/80c77c7674ba4c8c82294c3b2957990c/services/9fe659022c9747e3b9b7b923c3830623/jobs?api-version=2.0</span></span>

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

## <a name="considerations-when-using-batch-pool-processing"></a><span data-ttu-id="673ad-139">Considérations relatives à l’utilisation du traitement par pool Batch</span><span class="sxs-lookup"><span data-stu-id="673ad-139">Considerations when using Batch Pool processing</span></span>

<span data-ttu-id="673ad-140">Pool de traitement par lot est un service facturable toujours actif et qu’elle vous tooassociate il avec un gestionnaire de ressources en fonction de plan de facturation.</span><span class="sxs-lookup"><span data-stu-id="673ad-140">Batch Pool Processing is an always-on billable service and that requires you tooassociate it with a Resource Manager based billing plan.</span></span> <span data-ttu-id="673ad-141">Vous êtes facturé uniquement pour nombre de hello d’heures de calcul pool de hello est en cours d’exécution ; quel que soit le nombre de hello des tâches exécutées au cours de ce pool de temps.</span><span class="sxs-lookup"><span data-stu-id="673ad-141">You are only billed for hello number of compute hours hello pool is running; regardless of hello number of jobs run during that time pool.</span></span> <span data-ttu-id="673ad-142">Si vous créez un pool, vous êtes facturé pour les heures de calcul hello de chaque ordinateur virtuel dans le pool de hello jusqu'à ce que le pool de hello est supprimé, même si aucune tâche de traitement par lots n’est en cours d’exécution dans le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="673ad-142">If you create a pool, you are billed for hello compute hours of each virtual machine in hello pool until hello pool is deleted, even if no batch jobs are running in hello pool.</span></span> <span data-ttu-id="673ad-143">Facturation des machines virtuelles de hello démarre lorsqu’ils ont terminé la mise en service et s’arrête lorsqu’ils ont été supprimés.</span><span class="sxs-lookup"><span data-stu-id="673ad-143">Billing for hello virtual machines starts when they have finished provisioning and stops when they have been deleted.</span></span> <span data-ttu-id="673ad-144">Vous pouvez utiliser un des plans hello trouvés sur hello [page de tarification de Machine Learning](https://azure.microsoft.com/pricing/details/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="673ad-144">You can use any of hello plans found on hello [Machine Learning Pricing page](https://azure.microsoft.com/pricing/details/machine-learning/).</span></span>

<span data-ttu-id="673ad-145">Exemple de facturation :</span><span class="sxs-lookup"><span data-stu-id="673ad-145">Billing example:</span></span>

<span data-ttu-id="673ad-146">Si vous créez un pool Batch comprenant 2 machines virtuelles et le supprimez après 24 heures, votre plan de facturation est débité de 48 heures de calcul quel que soit le nombre de travaux exécutés pendant cette période.</span><span class="sxs-lookup"><span data-stu-id="673ad-146">If you create a Batch Pool with 2 virtual machines and delete it after 24 hours your billing plan is debited 48 compute hours; regardless of how many jobs were run during that period.</span></span>

<span data-ttu-id="673ad-147">Si vous créez un pool Batch comportant 4 machines virtuelles et le supprimez après 12 heures, votre plan de facturation est également débité de 48 heures de calcul.</span><span class="sxs-lookup"><span data-stu-id="673ad-147">If you create a Batch Pool with 4 virtual machines and delete it after 12 hours, your billing plan is also debited 48 compute hours.</span></span>

<span data-ttu-id="673ad-148">Nous vous recommandons d’interroger les hello travail état toodetermine lors de l’achèvement des travaux.</span><span class="sxs-lookup"><span data-stu-id="673ad-148">We recommend that you poll hello job status toodetermine when jobs complete.</span></span> <span data-ttu-id="673ad-149">Lorsque tous vos travaux terminés, appelez hello redimensionnement d’un Pool opération tooset hello nombre de machines virtuelles dans hello pool toozero.</span><span class="sxs-lookup"><span data-stu-id="673ad-149">When all your jobs have finished running, call hello Resize Pool operation tooset hello number of virtual machines in hello pool toozero.</span></span> <span data-ttu-id="673ad-150">Si vous êtes court sur des ressources et vous devez toocreate un nouveau pool, par exemple toobill par rapport à un autre plan de facturation, vous pouvez supprimer le pool de hello à la place lorsque tous vos travaux de l’exécution est terminée.</span><span class="sxs-lookup"><span data-stu-id="673ad-150">If you are short on pool resources and you need toocreate a new pool, for example toobill against a different billing plan, you can delete hello pool instead when all your jobs have finished running.</span></span>


| <span data-ttu-id="673ad-151">**Utilisez le traitement par pool Batch si**</span><span class="sxs-lookup"><span data-stu-id="673ad-151">**Use Batch Pool Processing when**</span></span>    | <span data-ttu-id="673ad-152">**Utilisez le traitement par lots classique si**</span><span class="sxs-lookup"><span data-stu-id="673ad-152">**Use classic batch processing when**</span></span>  |
|---|---|
|<span data-ttu-id="673ad-153">Vous devez toorun un grand nombre de travaux</span><span class="sxs-lookup"><span data-stu-id="673ad-153">You need toorun a large number of jobs</span></span><br><span data-ttu-id="673ad-154">Ou</span><span class="sxs-lookup"><span data-stu-id="673ad-154">Or</span></span><br/><span data-ttu-id="673ad-155">Vous devez tooknow vos tâches s’exécutent immédiatement</span><span class="sxs-lookup"><span data-stu-id="673ad-155">You need tooknow that your jobs will run immediately</span></span><br/><span data-ttu-id="673ad-156">Ou</span><span class="sxs-lookup"><span data-stu-id="673ad-156">Or</span></span><br/><span data-ttu-id="673ad-157">Vous avez besoin d’un débit garanti.</span><span class="sxs-lookup"><span data-stu-id="673ad-157">You need guaranteed throughput.</span></span> <span data-ttu-id="673ad-158">Par exemple, vous devez toorun un nombre de travaux dans un laps de temps donné et devez tooscale votre toomeet de ressources de calcul des besoins.</span><span class="sxs-lookup"><span data-stu-id="673ad-158">For example, you need toorun a number of jobs in a given time frame, and want tooscale out your compute resources toomeet your needs.</span></span>    | <span data-ttu-id="673ad-159">Vous exécutez quelques travaux</span><span class="sxs-lookup"><span data-stu-id="673ad-159">You are running just a few jobs</span></span><br/><span data-ttu-id="673ad-160">and</span><span class="sxs-lookup"><span data-stu-id="673ad-160">And</span></span><br/> <span data-ttu-id="673ad-161">Vous n’avez pas besoin hello travaux toorun immédiatement</span><span class="sxs-lookup"><span data-stu-id="673ad-161">You don’t need hello jobs toorun immediately</span></span> |
