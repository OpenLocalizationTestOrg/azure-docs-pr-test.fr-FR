---
title: "plans de toorecovery aaaAdd Azure automation procédures opérationnelles dans le portail classique de hello | Documents Microsoft"
description: "Cet article décrit la façon dont Azure Site Recovery vous permet désormais de tooextend les plans de récupération à l’aide des tâches complexes Azure Automation toocomplete pendant la récupération tooAzure"
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: f24eaa62-9dea-4fce-92e1-a72513ca0289
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: 3bb7420911afbce289b656f28823b1923e8af0c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-automation-runbooks-toorecovery-plans-in-hello-classic-portal"></a><span data-ttu-id="4eecb-103">Ajouter des plans de toorecovery runbooks Azure automation dans le portail classique de hello</span><span class="sxs-lookup"><span data-stu-id="4eecb-103">Add Azure automation runbooks toorecovery plans in hello classic portal</span></span>
<span data-ttu-id="4eecb-104">Ce didacticiel explique comment Azure Site Recovery s’intègre à Azure Automation tooprovide extensibilité toorecovery plans.</span><span class="sxs-lookup"><span data-stu-id="4eecb-104">This tutorial describes how Azure Site Recovery integrates with Azure Automation tooprovide extensibility toorecovery plans.</span></span> <span data-ttu-id="4eecb-105">Récupération de vos machines virtuelles protégées à l’aide d’Azure Site Recovery pour la réplication toosecondary cloud et les scénarios de réplication tooAzure peuvent organiser les plans de récupération.</span><span class="sxs-lookup"><span data-stu-id="4eecb-105">Recovery plans can orchestrate recovery of your virtual machines protected using Azure Site Recovery for both replication toosecondary cloud and replication tooAzure scenarios.</span></span> <span data-ttu-id="4eecb-106">Ils permettent également de restauration de hello **précis et constants**, **repeatable**, et **automatisée**.</span><span class="sxs-lookup"><span data-stu-id="4eecb-106">They also help in making hello recovery **consistently accurate**, **repeatable**, and **automated**.</span></span> <span data-ttu-id="4eecb-107">Si vous basculez sur votre tooAzure de machines virtuelles, intégration à Azure Automation étend les plans de récupération et vous offre la fonctionnalité tooexecute runbooks, ce qui permet des tâches d’automatisation puissantes.</span><span class="sxs-lookup"><span data-stu-id="4eecb-107">If you are failing over your virtual machines tooAzure, integration with Azure Automation extends the recovery plans and gives you capability tooexecute runbooks, thus allowing powerful automation tasks.</span></span>

<span data-ttu-id="4eecb-108">Si vous n’avez pas encore entendu parler de Microsoft Azure Automation, connectez-vous [ici](https://azure.microsoft.com/services/automation/) et téléchargez [ici](https://azure.microsoft.com/documentation/scripts/) des exemples de scripts.</span><span class="sxs-lookup"><span data-stu-id="4eecb-108">If you have not heard about Azure Automation yet, sign up [here](https://azure.microsoft.com/services/automation/) and download their sample scripts [here](https://azure.microsoft.com/documentation/scripts/).</span></span> <span data-ttu-id="4eecb-109">En savoir plus sur [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) et comment tooorchestrate tooAzure de récupération à l’aide de la récupération des plans [ici](https://azure.microsoft.com/blog/?p=166264).</span><span class="sxs-lookup"><span data-stu-id="4eecb-109">Read more about [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) and how tooorchestrate recovery tooAzure using recovery plans [here](https://azure.microsoft.com/blog/?p=166264).</span></span>

<span data-ttu-id="4eecb-110">Dans ce bref didacticiel, nous allons voir comment intégrer des Runbooks Microsoft Azure dans des plans de récupération.</span><span class="sxs-lookup"><span data-stu-id="4eecb-110">In this short tutorial, we will look at how you can integrate Azure Automation runbooks into recovery plans.</span></span> <span data-ttu-id="4eecb-111">Nous automatiser des tâches simples qui précédemment requis une intervention manuelle et voir comment tooconvert un multi étape de récupération dans une action de récupération d’un simple clic.</span><span class="sxs-lookup"><span data-stu-id="4eecb-111">We will automate simple tasks that earlier required manual intervention and see how tooconvert a multi step recovery into a single-click recovery action.</span></span> <span data-ttu-id="4eecb-112">Nous verrons également comment dépanner un script simple en cas de problème.</span><span class="sxs-lookup"><span data-stu-id="4eecb-112">We will also look at how you can troubleshoot a simple script if it goes wrong.</span></span>

## <a name="protect-hello-application-tooazure"></a><span data-ttu-id="4eecb-113">Protéger hello application tooAzure</span><span class="sxs-lookup"><span data-stu-id="4eecb-113">Protect hello application tooAzure</span></span>
<span data-ttu-id="4eecb-114">Commençons par une application simple, constituée de deux machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="4eecb-114">Let us begin with a simple application consisting of two virtual machines.</span></span> <span data-ttu-id="4eecb-115">Voici l’application HRweb de Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="4eecb-115">Here, we have a HRweb application of Fabrikam.</span></span> <span data-ttu-id="4eecb-116">Fabrikam-HRweb-frontend et Fabrikam-Hrweb-principaux sont hello deux des ordinateurs virtuels protégés tooAzure à l’aide d’Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="4eecb-116">Fabrikam-HRweb-frontend and Fabrikam-Hrweb-backend are hello two virtual machines protected tooAzure using Azure Site Recovery.</span></span> <span data-ttu-id="4eecb-117">machines virtuelles de tooprotect hello à l’aide d’Azure Site Recovery, suivez les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="4eecb-117">tooprotect hello virtual machines using Azure Site Recovery, follow hello steps below.</span></span>

1. <span data-ttu-id="4eecb-118">Activez la protection de vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="4eecb-118">Enable protection for your virtual machines.</span></span>
2. <span data-ttu-id="4eecb-119">Assurez-vous que les machines virtuelles de hello ont terminé la réplication initiale et sont répliqués.</span><span class="sxs-lookup"><span data-stu-id="4eecb-119">Ensure that hello virtual machines have completed initial replication and are replicating.</span></span>
3. <span data-ttu-id="4eecb-120">Attendez que hello la réplication initiale se termine et hello état de réplication est protégé.</span><span class="sxs-lookup"><span data-stu-id="4eecb-120">Wait till hello initial replication completes and hello Replication status says Protected.</span></span>

## ![](media/site-recovery-runbook-automation/01.png)
<span data-ttu-id="4eecb-121">Dans ce didacticiel, nous allons créer un plan de récupération pour hello Fabrikam HRweb application toofailover hello application tooAzure.</span><span class="sxs-lookup"><span data-stu-id="4eecb-121">In this tutorial, we will create a recovery plan for hello Fabrikam HRweb application toofailover hello application tooAzure.</span></span> <span data-ttu-id="4eecb-122">Puis nous sera l’intégrer à un runbook qui créera un point de terminaison sur hello a échoué sur une machine virtuelle Azure tooserve des pages web sur le port 80.</span><span class="sxs-lookup"><span data-stu-id="4eecb-122">Then we will integrate it with a runbook that will create an endpoint on hello failed over Azure virtual machine tooserve web pages at port 80.</span></span>

<span data-ttu-id="4eecb-123">Commençons par créer un plan de récupération pour notre application.</span><span class="sxs-lookup"><span data-stu-id="4eecb-123">First, let's create a recovery plan for our application.</span></span>

## <a name="create-hello-recovery-plan"></a><span data-ttu-id="4eecb-124">Créer le plan de récupération hello</span><span class="sxs-lookup"><span data-stu-id="4eecb-124">Create hello recovery plan</span></span>
<span data-ttu-id="4eecb-125">toorecover hello application tooAzure, vous devez toocreate un plan de récupération.</span><span class="sxs-lookup"><span data-stu-id="4eecb-125">toorecover hello application tooAzure, you need toocreate a recovery plan.</span></span>
<span data-ttu-id="4eecb-126">À l’aide d’un plan de récupération que vous pouvez spécifier la commande hello de la récupération des ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="4eecb-126">Using a recovery plan you can specify hello order of recovery of the virtual machines.</span></span> <span data-ttu-id="4eecb-127">machine virtuelle de Hello placé dans le groupe 1 se récupérer démarrage initial et suivez de machine virtuelle de hello dans le groupe 2.</span><span class="sxs-lookup"><span data-stu-id="4eecb-127">hello virtual machine placed in group 1 will recover and start first, and then hello virtual machine in group 2 will follow.</span></span>

<span data-ttu-id="4eecb-128">Créez un plan de récupération ressemblant à ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="4eecb-128">Create a Recovery Plan that looks like below.</span></span>

![](media/site-recovery-runbook-automation/12.png)

<span data-ttu-id="4eecb-129">plus d’informations sur les plans de récupération, lisez la documentation de tooread [ici](https://msdn.microsoft.com/library/azure/dn788799.aspx "ici").</span><span class="sxs-lookup"><span data-stu-id="4eecb-129">tooread more about recovery plans, read documentation [here](https://msdn.microsoft.com/library/azure/dn788799.aspx "here").</span></span>

<span data-ttu-id="4eecb-130">Ensuite, nous allons créer hello artefacts nécessaires dans Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="4eecb-130">Next, let's create hello necessary artifacts in Azure Automation.</span></span>

## <a name="create-hello-automation-account-and-its-assets"></a><span data-ttu-id="4eecb-131">Créer le compte d’automatisation hello et ses composants</span><span class="sxs-lookup"><span data-stu-id="4eecb-131">Create hello automation account and its assets</span></span>
<span data-ttu-id="4eecb-132">Vous avez besoin d’un runbook toocreate du compte Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="4eecb-132">You need an Azure Automation account toocreate runbooks.</span></span> <span data-ttu-id="4eecb-133">Si vous n’avez pas déjà un compte, accédez à onglet d’Automation tooAzure dénoté par ![](media/site-recovery-runbook-automation/02.png)et créer un nouveau compte.</span><span class="sxs-lookup"><span data-stu-id="4eecb-133">If you do not already have an account, navigate tooAzure Automation tab denoted by ![](media/site-recovery-runbook-automation/02.png)and create a new account.</span></span>

1. <span data-ttu-id="4eecb-134">Donner le compte de hello un tooidentify nom avec.</span><span class="sxs-lookup"><span data-stu-id="4eecb-134">Give hello account a name tooidentify with.</span></span>
2. <span data-ttu-id="4eecb-135">Spécifiez une région géographique dans laquelle vous souhaitez que le compte de hello de tooplace.</span><span class="sxs-lookup"><span data-stu-id="4eecb-135">Specify a geographical region where you want tooplace hello account.</span></span>

<span data-ttu-id="4eecb-136">Il est recommandé de compte de hello tooplace Bonjour même région que le coffre hello ASR.</span><span class="sxs-lookup"><span data-stu-id="4eecb-136">It is recommended tooplace hello account in hello same region as hello ASR vault.</span></span>

![](media/site-recovery-runbook-automation/03.png)

<span data-ttu-id="4eecb-137">Ensuite, créez hello suivant actifs Bonjour compte.</span><span class="sxs-lookup"><span data-stu-id="4eecb-137">Next, create hello following assets in hello Account.</span></span>

### <a name="add-a-subscription-name-as-asset"></a><span data-ttu-id="4eecb-138">Ajouter un nom d’abonnement en tant que ressource</span><span class="sxs-lookup"><span data-stu-id="4eecb-138">Add a subscription name as asset</span></span>
1. <span data-ttu-id="4eecb-139">Ajouter un nouveau paramètre ![](media/site-recovery-runbook-automation/04.png) dans hello actifs d’automatisation Azure et sélectionnez trop![](media/site-recovery-runbook-automation/05.png)</span><span class="sxs-lookup"><span data-stu-id="4eecb-139">Add a new setting ![](media/site-recovery-runbook-automation/04.png) in hello Azure Automation Assets and select too![](media/site-recovery-runbook-automation/05.png)</span></span>
2. <span data-ttu-id="4eecb-140">Sélectionnez le type de variable hello en tant que **chaîne**</span><span class="sxs-lookup"><span data-stu-id="4eecb-140">Select hello variable type as **String**</span></span>
3. <span data-ttu-id="4eecb-141">Spécifiez le nom de variable **AzureSubscriptionName**</span><span class="sxs-lookup"><span data-stu-id="4eecb-141">Specify variable name as **AzureSubscriptionName**</span></span>

   ![](media/site-recovery-runbook-automation/06.png)
4. <span data-ttu-id="4eecb-142">Spécifiez le nom de votre abonnement Azure réel en tant que valeur de la variable hello.</span><span class="sxs-lookup"><span data-stu-id="4eecb-142">Specify your actual Azure Subscription name as hello variable value.</span></span>

   ![](media/site-recovery-runbook-automation/07_1.png)

<span data-ttu-id="4eecb-143">Vous pouvez identifier le nom hello de votre abonnement à partir de la page des paramètres de votre compte sur hello portail Azure hello.</span><span class="sxs-lookup"><span data-stu-id="4eecb-143">You can identify hello name of your subscription from hello settings page of your account on hello Azure portal.</span></span>

### <a name="add-an-azure-login-credential-as-asset"></a><span data-ttu-id="4eecb-144">Ajouter des informations d’identification de connexion Microsoft Azure en tant que ressources</span><span class="sxs-lookup"><span data-stu-id="4eecb-144">Add an Azure login credential as asset</span></span>
<span data-ttu-id="4eecb-145">Azure Automation utilise Azure PowerShell tooconnect toothe abonnement et fonctionne sur les artefacts hello il.</span><span class="sxs-lookup"><span data-stu-id="4eecb-145">Azure Automation uses Azure PowerShell tooconnect toothe subscription and operates on hello artifacts there.</span></span> <span data-ttu-id="4eecb-146">Pour cela, vous devez vous authentifier à l’aide de votre compte Microsoft ou d’un compte professionnel ou scolaire.</span><span class="sxs-lookup"><span data-stu-id="4eecb-146">For this, you need to authenticate using your Microsoft account or a work or school account.</span></span>
<span data-ttu-id="4eecb-147">Vous pouvez stocker des informations d’identification du compte hello dans un toobe asset utilisée en toute sécurité par hello runbook.</span><span class="sxs-lookup"><span data-stu-id="4eecb-147">You can store hello account credentials in an asset toobe used securely by hello runbook.</span></span>

1. <span data-ttu-id="4eecb-148">Ajouter un nouveau paramètre ![](media/site-recovery-runbook-automation/04.png) dans hello actifs d’automatisation Azure, puis sélectionnez![](media/site-recovery-runbook-automation/09.png)</span><span class="sxs-lookup"><span data-stu-id="4eecb-148">Add a new setting ![](media/site-recovery-runbook-automation/04.png) in hello Azure Automation Assets and select ![](media/site-recovery-runbook-automation/09.png)</span></span>
2. <span data-ttu-id="4eecb-149">Sélectionner le type d’informations d’identification hello en tant que **informations d’identification de Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="4eecb-149">Select hello Credential type as **Windows PowerShell Credential**</span></span>
3. <span data-ttu-id="4eecb-150">Nommez hello **AzureCredential**</span><span class="sxs-lookup"><span data-stu-id="4eecb-150">Specify hello name as **AzureCredential**</span></span>

   ![](media/site-recovery-runbook-automation/10.png)
4. <span data-ttu-id="4eecb-151">Spécifiez le nom d’utilisateur hello et un mot de passe toosign à l’aide de.</span><span class="sxs-lookup"><span data-stu-id="4eecb-151">Specify hello username and password toosign-in with.</span></span>

<span data-ttu-id="4eecb-152">Désormais, ces deux paramètres sont disponibles dans vos ressources.</span><span class="sxs-lookup"><span data-stu-id="4eecb-152">Now both these settings are available in your assets.</span></span>

![](media/site-recovery-runbook-automation/11.png)

<span data-ttu-id="4eecb-153">Plus d’informations sur comment abonnement de tooyour tooconnect via PowerShell est donné [ici](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4eecb-153">More information about how tooconnect tooyour subscription via PowerShell is given [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="4eecb-154">Ensuite, vous allez créer un runbook dans Azure Automation que vous pouvez ajouter un point de terminaison pour la machine virtuelle frontal de hello après le basculement.</span><span class="sxs-lookup"><span data-stu-id="4eecb-154">Next, you will create a runbook in Azure Automation that can add an endpoint for hello front-end virtual machine after failover.</span></span>

## <a name="azure-automation-context"></a><span data-ttu-id="4eecb-155">Contexte Microsoft Automation</span><span class="sxs-lookup"><span data-stu-id="4eecb-155">Azure automation context</span></span>
<span data-ttu-id="4eecb-156">ASR transmet un toohelp de runbook de variable toohello de contexte vous écrivez des scripts déterministes.</span><span class="sxs-lookup"><span data-stu-id="4eecb-156">ASR passes a context variable toohello runbook toohelp you write deterministic scripts.</span></span> <span data-ttu-id="4eecb-157">Disent que noms hello de hello Service Cloud et hello Machine virtuelle sont prévisibles, mais se produit qu’il n’est pas toujours les cas de hello en raison de toocertain scénarios hello une où nom hello du nom d’ordinateur virtuel hello peut avoir modifié en raison d' caractères toounsupported dans Azure.</span><span class="sxs-lookup"><span data-stu-id="4eecb-157">One could argue that hello names of hello Cloud Service and hello Virtual Machine are predictable, but happens that it is not always hello case owing toocertain scenarios such as hello one where hello name of hello virtual machine name might have changed due toounsupported characters in Azure.</span></span> <span data-ttu-id="4eecb-158">Par conséquent, cette information est transmise de plan de récupération toohello ASR dans le cadre de hello *contexte*.</span><span class="sxs-lookup"><span data-stu-id="4eecb-158">Hence this information is passed toohello ASR recovery plan as part of hello *context*.</span></span>

<span data-ttu-id="4eecb-159">Voici un exemple de l’aspect de la variable de contexte hello.</span><span class="sxs-lookup"><span data-stu-id="4eecb-159">Below is an example of how hello context variable looks.</span></span>

        {"RecoveryPlanName":"hrweb-recovery",

        "FailoverType":"Test",

        "FailoverDirection":"PrimaryToSecondary",

        "GroupId":"1",

        "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                {"CloudServiceName":"pod02hrweb-Chicago-test",

                "RoleName":"Fabrikam-Hrweb-frontend-test"}

                }

        }


<span data-ttu-id="4eecb-160">tableau Hello ci-dessous contient le nom et une description pour chaque variable dans le contexte de hello.</span><span class="sxs-lookup"><span data-stu-id="4eecb-160">hello table below contains name and description for each variable in hello context.</span></span>

| <span data-ttu-id="4eecb-161">**Nom de la variable**</span><span class="sxs-lookup"><span data-stu-id="4eecb-161">**Variable name**</span></span> | <span data-ttu-id="4eecb-162">**Description**</span><span class="sxs-lookup"><span data-stu-id="4eecb-162">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="4eecb-163">RecoveryPlanName</span><span class="sxs-lookup"><span data-stu-id="4eecb-163">RecoveryPlanName</span></span> |<span data-ttu-id="4eecb-164">Nom du plan en cours d'exécution.</span><span class="sxs-lookup"><span data-stu-id="4eecb-164">Name of plan being run.</span></span> <span data-ttu-id="4eecb-165">Vous aide à vous entreprendre une action basée sur l’utilisation de nom hello même script</span><span class="sxs-lookup"><span data-stu-id="4eecb-165">Helps you take action based on name using hello same script</span></span> |
| <span data-ttu-id="4eecb-166">FailoverType</span><span class="sxs-lookup"><span data-stu-id="4eecb-166">FailoverType</span></span> |<span data-ttu-id="4eecb-167">Spécifie si hello basculement test, planifié ou non.</span><span class="sxs-lookup"><span data-stu-id="4eecb-167">Specifies whether hello failover is test, planned, or unplanned.</span></span> |
| <span data-ttu-id="4eecb-168">FailoverDirection</span><span class="sxs-lookup"><span data-stu-id="4eecb-168">FailoverDirection</span></span> |<span data-ttu-id="4eecb-169">Spécifiez si la récupération est tooprimary ou la base de données secondaire</span><span class="sxs-lookup"><span data-stu-id="4eecb-169">Specify whether recovery is tooprimary or secondary</span></span> |
| <span data-ttu-id="4eecb-170">GroupID</span><span class="sxs-lookup"><span data-stu-id="4eecb-170">GroupID</span></span> |<span data-ttu-id="4eecb-171">Identifier le numéro de groupe hello dans le plan de récupération hello lorsque le plan de hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="4eecb-171">Identify hello group number within hello recovery plan when hello plan is running</span></span> |
| <span data-ttu-id="4eecb-172">VmMap</span><span class="sxs-lookup"><span data-stu-id="4eecb-172">VmMap</span></span> |<span data-ttu-id="4eecb-173">Tableau de tous les ordinateurs virtuels hello dans le groupe de hello</span><span class="sxs-lookup"><span data-stu-id="4eecb-173">Array of all hello virtual machines in hello group</span></span> |
| <span data-ttu-id="4eecb-174">Clé VMMap</span><span class="sxs-lookup"><span data-stu-id="4eecb-174">VMMap key</span></span> |<span data-ttu-id="4eecb-175">Clé unique (GUID) pour chaque machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="4eecb-175">Unique key (GUID) for each VM.</span></span> <span data-ttu-id="4eecb-176">Il a hello identique hello ID VMM de machine virtuelle de hello, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="4eecb-176">It's hello same as hello VMM ID of hello virtual machine where applicable.</span></span> |
| <span data-ttu-id="4eecb-177">RoleName</span><span class="sxs-lookup"><span data-stu-id="4eecb-177">RoleName</span></span> |<span data-ttu-id="4eecb-178">Nom de machine virtuelle Azure qui est en cours de récupération de hello</span><span class="sxs-lookup"><span data-stu-id="4eecb-178">Name of hello Azure VM that's being recovered</span></span> |
| <span data-ttu-id="4eecb-179">CloudServiceName</span><span class="sxs-lookup"><span data-stu-id="4eecb-179">CloudServiceName</span></span> |<span data-ttu-id="4eecb-180">Nom du Service Cloud Azure sous le hello machine virtuelle est créée.</span><span class="sxs-lookup"><span data-stu-id="4eecb-180">Azure Cloud Service name under which hello virtual machine is created.</span></span> |

<span data-ttu-id="4eecb-181">tooidentify hello VmMap Key dans le contexte de hello, vous pouvez également atteindre la page de propriétés de machine virtuelle toohello dans ASR et examinez hello propriété VM GUID.</span><span class="sxs-lookup"><span data-stu-id="4eecb-181">tooidentify hello VmMap Key in hello context you could also go toohello VM properties page in ASR and look at hello VM GUID property.</span></span>

![](media/site-recovery-runbook-automation/13.png)

## <a name="author-an-automation-runbook"></a><span data-ttu-id="4eecb-182">Créer un Runbook Automation</span><span class="sxs-lookup"><span data-stu-id="4eecb-182">Author an Automation runbook</span></span>
<span data-ttu-id="4eecb-183">Créer maintenant hello runbook tooopen port80 sur l’ordinateur virtuel frontal de hello.</span><span class="sxs-lookup"><span data-stu-id="4eecb-183">Now create hello runbook tooopen port 80 on hello front-end virtual machine.</span></span>

1. <span data-ttu-id="4eecb-184">Créer un runbook Bonjour compte Azure Automation avec le nom de hello **OpenPort80**</span><span class="sxs-lookup"><span data-stu-id="4eecb-184">Create a new runbook in hello Azure Automation account with hello name **OpenPort80**</span></span>

   ![](media/site-recovery-runbook-automation/14.png)
2. <span data-ttu-id="4eecb-185">Accédez toohello vue auteur de runbook de hello et entrer en mode brouillon hello.</span><span class="sxs-lookup"><span data-stu-id="4eecb-185">Navigate toohello Author view of hello runbook and enter hello draft mode.</span></span>
3. <span data-ttu-id="4eecb-186">Tout d’abord spécifier toouse de variable hello comme contexte de plan de récupération hello</span><span class="sxs-lookup"><span data-stu-id="4eecb-186">First specify hello variable toouse as hello recovery plan context</span></span>

   ```
       param (
           [Object]$RecoveryPlanContext
       )

   ```
4. <span data-ttu-id="4eecb-187">Prochaine connexion abonnement toohello à l’aide du nom d’abonnement et les informations d’identification hello</span><span class="sxs-lookup"><span data-stu-id="4eecb-187">Next connect toohello subscription using hello credential and subscription name</span></span>

   ```
       $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

       # Connect tooAzure
       $AzureAccount = Add-AzureAccount -Credential $Cred
       $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
       Select-AzureSubscription -SubscriptionName $AzureSubscriptionName
   ```

   <span data-ttu-id="4eecb-188">Notez que vous utilisez hello Azure actifs – **AzureCredential** et **AzureSubscriptionName** ici.</span><span class="sxs-lookup"><span data-stu-id="4eecb-188">Note that you use hello Azure assets – **AzureCredential** and **AzureSubscriptionName** here.</span></span>
5. <span data-ttu-id="4eecb-189">Maintenant, spécifiez les détails du point de terminaison hello et hello GUID de l’ordinateur virtuel de hello pour lequel vous souhaitez le point de terminaison tooexpose hello.</span><span class="sxs-lookup"><span data-stu-id="4eecb-189">Now specify hello endpoint details and hello GUID of hello virtual machine for which you want tooexpose hello endpoint.</span></span> <span data-ttu-id="4eecb-190">Dans cet ordinateur virtuel frontal de cas hello.</span><span class="sxs-lookup"><span data-stu-id="4eecb-190">In this case hello front-end virtual machine.</span></span>

   ```
       # Specify hello parameters toobe used by hello script
       $AEProtocol = "TCP"
       $AELocalPort = 80
       $AEPublicPort = 80
       $AEName = "Port 80 for HTTP"
       $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"
   ```

   <span data-ttu-id="4eecb-191">Cela indique hello protocole de point de terminaison Azure, port local sur la machine virtuelle de hello et son port public mappé.</span><span class="sxs-lookup"><span data-stu-id="4eecb-191">This specifies hello Azure endpoint protocol, local port on hello VM and its mapped public port.</span></span> <span data-ttu-id="4eecb-192">Ces variables sont les paramètres requis par hello commandes Azure qui ajoutent des points de terminaison tooVMs.</span><span class="sxs-lookup"><span data-stu-id="4eecb-192">These variables are parameters     required by hello Azure commands that add endpoints tooVMs.</span></span> <span data-ttu-id="4eecb-193">Hello VMGUID conserve hello GUID de l’ordinateur virtuel de hello sur que vous devez toooperate.</span><span class="sxs-lookup"><span data-stu-id="4eecb-193">hello VMGUID holds hello GUID of hello virtual machine you need toooperate on.</span></span>
6. <span data-ttu-id="4eecb-194">script de Hello maintenant extraire contexte hello pour hello donné VM GUID et créer un point de terminaison sur l’ordinateur virtuel de hello référencée par lui.</span><span class="sxs-lookup"><span data-stu-id="4eecb-194">hello script will now extract hello context for hello given VM GUID and create an endpoint on hello virtual machine referenced by it.</span></span>

   ```
       #Read hello VM GUID from hello context
       $VM = $RecoveryPlanContext.VmMap.$VMGUID

       if ($VM -ne $null)
       {
           # Invoke pipeline commands within an InlineScript

           $EndpointStatus = InlineScript {
               # Invoke hello necessary pipeline commands tooadd a Azure Endpoint tooa specified Virtual Machine
               # Commands include: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including parameters)

               $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                   Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                   Update-AzureVM
               Write-Output $Status
           }
       }
   ```
7. <span data-ttu-id="4eecb-195">Une fois cette opération terminée, atteint publier ![](media/site-recovery-runbook-automation/20.png) tooallow votre toobe script disponible pour l’exécution.</span><span class="sxs-lookup"><span data-stu-id="4eecb-195">Once this is complete, hit Publish ![](media/site-recovery-runbook-automation/20.png) tooallow your script toobe available for execution.</span></span>

<span data-ttu-id="4eecb-196">script complet de Hello est donné ci-dessous pour des références</span><span class="sxs-lookup"><span data-stu-id="4eecb-196">hello complete script is given below for your reference</span></span>

```
  workflow OpenPort80
  {
    param (
        [Object]$RecoveryPlanContext
    )

    $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

    # Connect tooAzure
    $AzureAccount = Add-AzureAccount -Credential $Cred
    $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
    Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

    # Specify hello parameters toobe used by hello script
    $AEProtocol = "TCP"
    $AELocalPort = 80
    $AEPublicPort = 80
    $AEName = "Port 80 for HTTP"
    $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"

    #Read hello VM GUID from hello context
    $VM = $RecoveryPlanContext.VmMap.$VMGUID

    if ($VM -ne $null)
    {
        # Invoke pipeline commands within an InlineScript

        $EndpointStatus = InlineScript {
            # Invoke hello necessary pipeline commands tooadd an Azure Endpoint tooa specified Virtual Machine
            # This set of commands includes: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including necessary parameters)

            $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                Update-AzureVM
            Write-Output $Status
        }
    }
  }
```

## <a name="add-hello-script-toohello-recovery-plan"></a><span data-ttu-id="4eecb-197">Ajouter un plan de récupération hello script toohello</span><span class="sxs-lookup"><span data-stu-id="4eecb-197">Add hello script toohello recovery plan</span></span>
<span data-ttu-id="4eecb-198">Une fois le script de hello est prêt, vous pouvez l’ajouter plan de récupération toohello que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="4eecb-198">Once hello script is ready, you can add it toohello recovery plan that you created earlier.</span></span>

1. <span data-ttu-id="4eecb-199">Dans le plan de récupération hello que vous avez créé, choisissez tooadd un script après le groupe 2.</span><span class="sxs-lookup"><span data-stu-id="4eecb-199">In hello recovery plan you created, choose tooadd a script after the group 2.</span></span> ![](media/site-recovery-runbook-automation/15.png)
2. <span data-ttu-id="4eecb-200">Spécifiez un nom de script.</span><span class="sxs-lookup"><span data-stu-id="4eecb-200">Specify a script name.</span></span> <span data-ttu-id="4eecb-201">Il s’agit simplement d’un nom convivial pour ce script pour l’affichage dans le plan de récupération hello.</span><span class="sxs-lookup"><span data-stu-id="4eecb-201">This is just a friendly name for this script for showing within hello Recovery plan.</span></span>
3. <span data-ttu-id="4eecb-202">Dans le script de hello basculement tooAzure – sélectionnez le nom de compte Azure Automation hello.</span><span class="sxs-lookup"><span data-stu-id="4eecb-202">In hello failover tooAzure script – Select hello Azure Automation Account name.</span></span>
4. <span data-ttu-id="4eecb-203">Hello Runbooks d’Azure, sélectionnez runbook hello que vous avez créés.</span><span class="sxs-lookup"><span data-stu-id="4eecb-203">In hello Azure Runbooks, select hello runbook you authored.</span></span>

![](media/site-recovery-runbook-automation/16.png)

## <a name="primary-side-scripts"></a><span data-ttu-id="4eecb-204">Scripts côté principal</span><span class="sxs-lookup"><span data-stu-id="4eecb-204">Primary side scripts</span></span>
<span data-ttu-id="4eecb-205">Lorsque vous exécutez un tooAzure de basculement, vous pouvez également choisir tooexecute scripts du côté primaire.</span><span class="sxs-lookup"><span data-stu-id="4eecb-205">When you are executing a failover tooAzure, you can also choose tooexecute primary side scripts.</span></span> <span data-ttu-id="4eecb-206">Ces scripts s’exécutent sur le serveur VMM de hello pendant le basculement.</span><span class="sxs-lookup"><span data-stu-id="4eecb-206">These scripts will run on hello VMM server during failover.</span></span>
<span data-ttu-id="4eecb-207">Les scripts côté principal ne sont disponibles que pour les phases précédant et suivant l’arrêt.</span><span class="sxs-lookup"><span data-stu-id="4eecb-207">Primary side scripts are only available only for pre-shutdown and post shutdown stages.</span></span> <span data-ttu-id="4eecb-208">Il s’agit, car nous pensons que hello site principal toobe généralement pas disponible lorsqu’un incident ne survienne.</span><span class="sxs-lookup"><span data-stu-id="4eecb-208">This is because we expect hello primary site toobe typically unavailable when a disaster strikes.</span></span>
<span data-ttu-id="4eecb-209">Pendant un basculement non planifié, uniquement si vous choisissez cette option pour les opérations de site principal, il tente les scripts côté principal toorun hello.</span><span class="sxs-lookup"><span data-stu-id="4eecb-209">During an unplanned failover, only if you opt in for primary site operations, it will attempt toorun hello primary side scripts.</span></span> <span data-ttu-id="4eecb-210">Si elles ne sont pas accessibles ou continuera de délai d’attente, hello basculement toorecover hello des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="4eecb-210">If they are not reachable or timeout, hello failover will continue toorecover hello virtual machines.</span></span>
<span data-ttu-id="4eecb-211">Les scripts côté principal sont non disponibles pour les Sites de VMware/physiques/Hyper-v sans tooAzure VMM protégé - tout en vous tooAzure de basculement.</span><span class="sxs-lookup"><span data-stu-id="4eecb-211">Primary side scripts are un-available for VMware/Physical/Hyper-v Sites without VMM protected tooAzure - while you failover tooAzure.</span></span>
<span data-ttu-id="4eecb-212">Toutefois, lorsque la restauration automatique à partir d’Azure tooon local, les scripts côté principal (Runbooks) peut servir pour toutes les cibles à l’exception de VMware.</span><span class="sxs-lookup"><span data-stu-id="4eecb-212">However, when you failback from Azure tooon-premises, primary side scripts (Runbooks) can be used for all targets except VMware.</span></span>

## <a name="test-hello-recovery-plan"></a><span data-ttu-id="4eecb-213">Plan de récupération test hello</span><span class="sxs-lookup"><span data-stu-id="4eecb-213">Test hello recovery plan</span></span>
<span data-ttu-id="4eecb-214">Une fois que vous avez ajouté le plan de toohello hello runbook, vous pouvez lancer un test de basculement et voir en action.</span><span class="sxs-lookup"><span data-stu-id="4eecb-214">Once you have added hello runbook toohello plan you can initiate a test failover and see it in action.</span></span> <span data-ttu-id="4eecb-215">Il est toujours recommandé toorun un tootest de basculement de test de votre tooensure plan de récupération d’application et hello qu’il n’y a aucune erreur.</span><span class="sxs-lookup"><span data-stu-id="4eecb-215">It is always recommended toorun a test failover tootest your application and hello recovery plan tooensure that there are no errors.</span></span>

1. <span data-ttu-id="4eecb-216">Sélectionnez le plan de récupération hello et lancer un test de basculement.</span><span class="sxs-lookup"><span data-stu-id="4eecb-216">Select hello recovery plan and initiate a test failover.</span></span>
2. <span data-ttu-id="4eecb-217">Pendant l’exécution de plan hello, vous pouvez voir si hello runbook a été exécutée ou non par l’intermédiaire de son état.</span><span class="sxs-lookup"><span data-stu-id="4eecb-217">During hello plan execution, you can see whether hello runbook has executed or not via its status.</span></span>

   ![](media/site-recovery-runbook-automation/17.png)
3. <span data-ttu-id="4eecb-218">Vous pouvez également voir hello l’état de l’exécution de runbook sur page de tâches Azure Automation hello pour hello runbook détaillé.</span><span class="sxs-lookup"><span data-stu-id="4eecb-218">You can also see hello detailed runbook execution status on hello Azure Automation jobs page for hello runbook.</span></span>

   ![](media/site-recovery-runbook-automation/18.png)
4. <span data-ttu-id="4eecb-219">Une fois hello basculement terminé, indépendamment des résultats de l’exécution de runbook hello, vous pouvez voir si l’exécution de hello a réussi ou non en visitant la page de machine virtuelle Azure hello et en examinant les points de terminaison hello.</span><span class="sxs-lookup"><span data-stu-id="4eecb-219">After hello failover completes, apart from hello runbook execution result, you can see whether hello execution is successful or not by visiting hello Azure virtual machine page and looking at hello endpoints.</span></span>

![](media/site-recovery-runbook-automation/19.png)

## <a name="sample-scripts"></a><span data-ttu-id="4eecb-220">Exemples de scripts</span><span class="sxs-lookup"><span data-stu-id="4eecb-220">Sample scripts</span></span>
<span data-ttu-id="4eecb-221">Pendant que nous avons passé en revue une automatisation couramment utilisé de tâche d’ajout d’un point de terminaison de tooan machine virtuelle Azure dans ce didacticiel, vous pourriez effectuer plusieurs autres tâches d’automatisation puissantes à l’aide d’Azure automation.</span><span class="sxs-lookup"><span data-stu-id="4eecb-221">While we walked through automating one commonly used task of adding an endpoint tooan Azure virtual machine in this tutorial, you could do a number of other powerful automation tasks using Azure automation.</span></span> <span data-ttu-id="4eecb-222">Microsoft et hello Communauté d’Azure Automation fournissent des exemples de runbooks qui peuvent vous aider à commencer à créer vos propres solutions et les runbooks d’utilitaire, que vous pouvez utiliser comme blocs de construction de plus grandes tâches d’automatisation.</span><span class="sxs-lookup"><span data-stu-id="4eecb-222">Microsoft and hello Azure Automation community provide sample runbooks which can help you get started creating your own solutions, and utility runbooks, which you can use as building blocks for larger automation tasks.</span></span> <span data-ttu-id="4eecb-223">Commencer à les utiliser à partir de la galerie de hello et créer des plans de récupération d’un seul clic puissantes pour vos applications à l’aide d’Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="4eecb-223">Start using them from hello gallery and build  powerful one-click recovery plans for your applications using Azure Site Recovery.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4eecb-224">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="4eecb-224">Additional Resources</span></span>
[<span data-ttu-id="4eecb-225">Vue d’ensemble de Microsoft Azure Automation</span><span class="sxs-lookup"><span data-stu-id="4eecb-225">Azure Automation Overview</span></span>](http://msdn.microsoft.com/library/azure/dn643629.aspx "Vue d’ensemble de Microsoft Azure Automation")

[<span data-ttu-id="4eecb-226">Exemples de scripts Microsoft Azure Automation</span><span class="sxs-lookup"><span data-stu-id="4eecb-226">Sample Azure Automation Scripts</span></span>](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Exemples de scripts Microsoft Azure Automation")
