---
title: "Ajouter des Runbooks Azure Automation à des plans de récupération dans le portail Classic | Microsoft Docs"
description: "Cet article explique comment Microsoft Azure Site Recovery vous permet désormais d’étendre des plans de récupération à l’aide de Microsoft Azure Automation, afin d’effectuer des tâches complexes lors de la récupération vers Microsoft Azure"
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
ms.openlocfilehash: 0a248e7c3f39a35ac10dc6ac64e5cef7d152e033
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="add-azure-automation-runbooks-to-recovery-plans-in-the-classic-portal"></a><span data-ttu-id="e8f83-103">Ajouter des Runbooks Azure Automation à des plans de récupération dans le portail Classic</span><span class="sxs-lookup"><span data-stu-id="e8f83-103">Add Azure automation runbooks to recovery plans in the classic portal</span></span>
<span data-ttu-id="e8f83-104">Ce didacticiel explique comment Microsoft Azure Site Recovery s’intègre dans Microsoft Azure Automation pour permettre l’extensibilité des plans de récupération.</span><span class="sxs-lookup"><span data-stu-id="e8f83-104">This tutorial describes how Azure Site Recovery integrates with Azure Automation to provide extensibility to recovery plans.</span></span> <span data-ttu-id="e8f83-105">Les plans de récupération peuvent orchestrer la récupération des machines virtuelles protégées via Microsoft Azure Site Recovery, pour la réplication vers un cloud secondaire et la réplication vers Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e8f83-105">Recovery plans can orchestrate recovery of your virtual machines protected using Azure Site Recovery for both replication to secondary cloud and replication to Azure scenarios.</span></span> <span data-ttu-id="e8f83-106">Ils garantissent que le récupération est **précise et cohérente**, **répétable** et **automatisée**.</span><span class="sxs-lookup"><span data-stu-id="e8f83-106">They also help in making the recovery **consistently accurate**, **repeatable**, and **automated**.</span></span> <span data-ttu-id="e8f83-107">Si vous effectuez le basculement de vos machines virtuelles vers Microsoft Azure, l’intégration avec Microsoft Azure Automation étend les plans de récupération et vous offre la possibilité d’exécuter des Runbooks, ce qui vous donne accès à des tâches d’automatisation très puissantes.</span><span class="sxs-lookup"><span data-stu-id="e8f83-107">If you are failing over your virtual machines to Azure, integration with Azure Automation extends the recovery plans and gives you capability to execute runbooks, thus allowing powerful automation tasks.</span></span>

<span data-ttu-id="e8f83-108">Si vous n’avez pas encore entendu parler de Microsoft Azure Automation, connectez-vous [ici](https://azure.microsoft.com/services/automation/) et téléchargez [ici](https://azure.microsoft.com/documentation/scripts/) des exemples de scripts.</span><span class="sxs-lookup"><span data-stu-id="e8f83-108">If you have not heard about Azure Automation yet, sign up [here](https://azure.microsoft.com/services/automation/) and download their sample scripts [here](https://azure.microsoft.com/documentation/scripts/).</span></span> <span data-ttu-id="e8f83-109">Lisez plus d’informations sur [Microsoft Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) et découvrez [ici](https://azure.microsoft.com/blog/?p=166264) comment orchestrer la récupération vers Microsoft Azure à l’aide de plans de récupération.</span><span class="sxs-lookup"><span data-stu-id="e8f83-109">Read more about [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) and how to orchestrate recovery to Azure using recovery plans [here](https://azure.microsoft.com/blog/?p=166264).</span></span>

<span data-ttu-id="e8f83-110">Dans ce bref didacticiel, nous allons voir comment intégrer des Runbooks Microsoft Azure dans des plans de récupération.</span><span class="sxs-lookup"><span data-stu-id="e8f83-110">In this short tutorial, we will look at how you can integrate Azure Automation runbooks into recovery plans.</span></span> <span data-ttu-id="e8f83-111">Nous allons automatiser des tâches simples, qui nécessitaient auparavant une intervention manuelle, et voir comment convertir une opération de récupération en plusieurs étapes en une seule action, impliquant un seul clic.</span><span class="sxs-lookup"><span data-stu-id="e8f83-111">We will automate simple tasks that earlier required manual intervention and see how to convert a multi step recovery into a single-click recovery action.</span></span> <span data-ttu-id="e8f83-112">Nous verrons également comment dépanner un script simple en cas de problème.</span><span class="sxs-lookup"><span data-stu-id="e8f83-112">We will also look at how you can troubleshoot a simple script if it goes wrong.</span></span>

## <a name="protect-the-application-to-azure"></a><span data-ttu-id="e8f83-113">Protéger l’application dans Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="e8f83-113">Protect the application to Azure</span></span>
<span data-ttu-id="e8f83-114">Commençons par une application simple, constituée de deux machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="e8f83-114">Let us begin with a simple application consisting of two virtual machines.</span></span> <span data-ttu-id="e8f83-115">Voici l’application HRweb de Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="e8f83-115">Here, we have a HRweb application of Fabrikam.</span></span> <span data-ttu-id="e8f83-116">« Fabrikam-HRweb-frontend » et « Fabrikam-Hrweb-backend » sont deux machines virtuelles protégées sur Microsoft Azure, via Microsoft Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="e8f83-116">Fabrikam-HRweb-frontend and Fabrikam-Hrweb-backend are the two virtual machines protected to Azure using Azure Site Recovery.</span></span> <span data-ttu-id="e8f83-117">Pour protéger les machines virtuelles via Microsoft Azure Site Recovery, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="e8f83-117">To protect the virtual machines using Azure Site Recovery, follow the steps below.</span></span>

1. <span data-ttu-id="e8f83-118">Activez la protection de vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="e8f83-118">Enable protection for your virtual machines.</span></span>
2. <span data-ttu-id="e8f83-119">Assurez-vous que les machines virtuelles ont terminé la réplication initiale et que leur réplication est en cours.</span><span class="sxs-lookup"><span data-stu-id="e8f83-119">Ensure that the virtual machines have completed initial replication and are replicating.</span></span>
3. <span data-ttu-id="e8f83-120">Attendez que la réplication initiale soit terminée et que l’état de la réplication soit Protégé.</span><span class="sxs-lookup"><span data-stu-id="e8f83-120">Wait till the initial replication completes and the Replication status says Protected.</span></span>

## ![](media/site-recovery-runbook-automation/01.png)
<span data-ttu-id="e8f83-121">Dans ce didacticiel, nous allons créer un plan de récupération pour l’application Fabrikam HRweb, afin de la faire basculer vers Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e8f83-121">In this tutorial, we will create a recovery plan for the Fabrikam HRweb application to failover the application to Azure.</span></span> <span data-ttu-id="e8f83-122">Ensuite, nous l’intégrerons dans un Runbook destiné à créer un point de terminaison sur la machine virtuelle Microsoft, afin de fournir des pages web au niveau du port 80.</span><span class="sxs-lookup"><span data-stu-id="e8f83-122">Then we will integrate it with a runbook that will create an endpoint on the failed over Azure virtual machine to serve web pages at port 80.</span></span>

<span data-ttu-id="e8f83-123">Commençons par créer un plan de récupération pour notre application.</span><span class="sxs-lookup"><span data-stu-id="e8f83-123">First, let's create a recovery plan for our application.</span></span>

## <a name="create-the-recovery-plan"></a><span data-ttu-id="e8f83-124">Créer un plan de récupération</span><span class="sxs-lookup"><span data-stu-id="e8f83-124">Create the recovery plan</span></span>
<span data-ttu-id="e8f83-125">Pour récupérer l’application dans Microsoft Azure, vous devez créer un plan de récupération.</span><span class="sxs-lookup"><span data-stu-id="e8f83-125">To recover the application to Azure, you need to create a recovery plan.</span></span>
<span data-ttu-id="e8f83-126">Au moyen de ce plan, nous pouvons spécifier l’ordre de récupération des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="e8f83-126">Using a recovery plan you can specify the order of recovery of the virtual machines.</span></span> <span data-ttu-id="e8f83-127">La machine virtuelle placée dans le groupe 1 récupère suite à l’erreur et démarre en premier. Cela fait, celle du groupe 2 prend la relève.</span><span class="sxs-lookup"><span data-stu-id="e8f83-127">The virtual machine placed in group 1 will recover and start first, and then the virtual machine in group 2 will follow.</span></span>

<span data-ttu-id="e8f83-128">Créez un plan de récupération ressemblant à ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="e8f83-128">Create a Recovery Plan that looks like below.</span></span>

![](media/site-recovery-runbook-automation/12.png)

<span data-ttu-id="e8f83-129">Pour en savoir plus sur les plans de récupération, lisez la documentation [ici](https://msdn.microsoft.com/library/azure/dn788799.aspx "ici").</span><span class="sxs-lookup"><span data-stu-id="e8f83-129">To read more about recovery plans, read documentation [here](https://msdn.microsoft.com/library/azure/dn788799.aspx "here").</span></span>

<span data-ttu-id="e8f83-130">Ensuite, nous allons créer les artefacts nécessaires dans Microsoft  Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="e8f83-130">Next, let's create the necessary artifacts in Azure Automation.</span></span>

## <a name="create-the-automation-account-and-its-assets"></a><span data-ttu-id="e8f83-131">Créer le compte Automatisation et ses ressources</span><span class="sxs-lookup"><span data-stu-id="e8f83-131">Create the automation account and its assets</span></span>
<span data-ttu-id="e8f83-132">Vous avez besoin d’un compte Microsoft Azure Automation pour créer des Runbooks.</span><span class="sxs-lookup"><span data-stu-id="e8f83-132">You need an Azure Automation account to create runbooks.</span></span> <span data-ttu-id="e8f83-133">Si vous ne disposez pas déjà d’un compte, accédez à l’onglet Azure Automation indiqué par l’élément ![](media/site-recovery-runbook-automation/02.png)et créez un compte.</span><span class="sxs-lookup"><span data-stu-id="e8f83-133">If you do not already have an account, navigate to Azure Automation tab denoted by ![](media/site-recovery-runbook-automation/02.png)and create a new account.</span></span>

1. <span data-ttu-id="e8f83-134">Donnez à ce compte un nom permettant de l’identifier.</span><span class="sxs-lookup"><span data-stu-id="e8f83-134">Give the account a name to identify with.</span></span>
2. <span data-ttu-id="e8f83-135">Spécifiez la région géographique dans laquelle placer le compte.</span><span class="sxs-lookup"><span data-stu-id="e8f83-135">Specify a geographical region where you want to place the account.</span></span>

<span data-ttu-id="e8f83-136">Il est recommandé de placer le compte dans la même région que le coffre ASR.</span><span class="sxs-lookup"><span data-stu-id="e8f83-136">It is recommended to place the account in the same region as the ASR vault.</span></span>

![](media/site-recovery-runbook-automation/03.png)

<span data-ttu-id="e8f83-137">Ensuite, créez les ressources ci-après dans le compte.</span><span class="sxs-lookup"><span data-stu-id="e8f83-137">Next, create the following assets in the Account.</span></span>

### <a name="add-a-subscription-name-as-asset"></a><span data-ttu-id="e8f83-138">Ajouter un nom d’abonnement en tant que ressource</span><span class="sxs-lookup"><span data-stu-id="e8f83-138">Add a subscription name as asset</span></span>
1. <span data-ttu-id="e8f83-139">Ajoutez un nouveau paramètre (![](media/site-recovery-runbook-automation/04.png)) dans la zone des ressources Microsoft Azure Automatisation et choisissez l’option ![](media/site-recovery-runbook-automation/05.png).</span><span class="sxs-lookup"><span data-stu-id="e8f83-139">Add a new setting ![](media/site-recovery-runbook-automation/04.png) in the Azure Automation Assets and select to ![](media/site-recovery-runbook-automation/05.png)</span></span>
2. <span data-ttu-id="e8f83-140">Sélectionnez le type de variable **String**</span><span class="sxs-lookup"><span data-stu-id="e8f83-140">Select the variable type as **String**</span></span>
3. <span data-ttu-id="e8f83-141">Spécifiez le nom de variable **AzureSubscriptionName**</span><span class="sxs-lookup"><span data-stu-id="e8f83-141">Specify variable name as **AzureSubscriptionName**</span></span>

   ![](media/site-recovery-runbook-automation/06.png)
4. <span data-ttu-id="e8f83-142">Comme valeur de la variable, spécifiez votre nom d’abonnement Azure réel.</span><span class="sxs-lookup"><span data-stu-id="e8f83-142">Specify your actual Azure Subscription name as the variable value.</span></span>

   ![](media/site-recovery-runbook-automation/07_1.png)

<span data-ttu-id="e8f83-143">Vous pouvez identifier le nom de votre abonnement à partir de la page des paramètres de votre compte, sur le Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e8f83-143">You can identify the name of your subscription from the settings page of your account on the Azure portal.</span></span>

### <a name="add-an-azure-login-credential-as-asset"></a><span data-ttu-id="e8f83-144">Ajouter des informations d’identification de connexion Microsoft Azure en tant que ressources</span><span class="sxs-lookup"><span data-stu-id="e8f83-144">Add an Azure login credential as asset</span></span>
<span data-ttu-id="e8f83-145">Azure Automation utilise Azure PowerShell pour se connecter à l’abonnement et agit sur les artefacts à ce niveau.</span><span class="sxs-lookup"><span data-stu-id="e8f83-145">Azure Automation uses Azure PowerShell to connect to the subscription and operates on the artifacts there.</span></span> <span data-ttu-id="e8f83-146">Pour cela, vous devez vous authentifier à l’aide de votre compte Microsoft ou d’un compte professionnel ou scolaire.</span><span class="sxs-lookup"><span data-stu-id="e8f83-146">For this, you need to authenticate using your Microsoft account or a work or school account.</span></span>
<span data-ttu-id="e8f83-147">Vous pouvez stocker les informations d’identification de compte dans une ressource, afin qu’elles soient utilisées par le Runbook en toute sécurité.</span><span class="sxs-lookup"><span data-stu-id="e8f83-147">You can store the account credentials in an asset to be used securely by the runbook.</span></span>

1. <span data-ttu-id="e8f83-148">Ajoutez un nouveau paramètre (![](media/site-recovery-runbook-automation/04.png)) dans la zone des ressources Microsoft Azure Automatisation et choisissez l’option ![](media/site-recovery-runbook-automation/09.png).</span><span class="sxs-lookup"><span data-stu-id="e8f83-148">Add a new setting ![](media/site-recovery-runbook-automation/04.png) in the Azure Automation Assets and select ![](media/site-recovery-runbook-automation/09.png)</span></span>
2. <span data-ttu-id="e8f83-149">Sélectionnez le type d’information d’identification suivant : **Information d’identification Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="e8f83-149">Select the Credential type as **Windows PowerShell Credential**</span></span>
3. <span data-ttu-id="e8f83-150">Spécifiez le nom ci-après : **AzureCredential**</span><span class="sxs-lookup"><span data-stu-id="e8f83-150">Specify the name as **AzureCredential**</span></span>

   ![](media/site-recovery-runbook-automation/10.png)
4. <span data-ttu-id="e8f83-151">Indiquez le nom d’utilisateur et le mot de passe avec lesquels vous connecter.</span><span class="sxs-lookup"><span data-stu-id="e8f83-151">Specify the username and password to sign-in with.</span></span>

<span data-ttu-id="e8f83-152">Désormais, ces deux paramètres sont disponibles dans vos ressources.</span><span class="sxs-lookup"><span data-stu-id="e8f83-152">Now both these settings are available in your assets.</span></span>

![](media/site-recovery-runbook-automation/11.png)

<span data-ttu-id="e8f83-153">Pour en savoir plus sur la connexion à votre abonnement avec PowerShell, cliquez [ici](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e8f83-153">More information about how to connect to your subscription via PowerShell is given [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="e8f83-154">Ensuite, vous allez créer un Runbook dans Microsoft Azure Automation, capable d’ajouter un point de terminaison pour la machine virtuelle frontale après le basculement.</span><span class="sxs-lookup"><span data-stu-id="e8f83-154">Next, you will create a runbook in Azure Automation that can add an endpoint for the front-end virtual machine after failover.</span></span>

## <a name="azure-automation-context"></a><span data-ttu-id="e8f83-155">Contexte Microsoft Automation</span><span class="sxs-lookup"><span data-stu-id="e8f83-155">Azure automation context</span></span>
<span data-ttu-id="e8f83-156">ASR passe une variable de contexte au Runbook, afin de vous aider à écrire des scripts déterministes.</span><span class="sxs-lookup"><span data-stu-id="e8f83-156">ASR passes a context variable to the runbook to help you write deterministic scripts.</span></span> <span data-ttu-id="e8f83-157">On pourrait arguer que les noms du service cloud et de la machine virtuelle sont assez prévisibles. Or, ce n’est pas toujours le cas, à cause de certains scénarios (comme celui selon lequel le nom de la machine virtuelle a pu être modifié suite à la présence de caractères non pris en charge par Microsoft Azure).</span><span class="sxs-lookup"><span data-stu-id="e8f83-157">One could argue that the names of the Cloud Service and the Virtual Machine are predictable, but happens that it is not always the case owing to certain scenarios such as the one where the name of the virtual machine name might have changed due to unsupported characters in Azure.</span></span> <span data-ttu-id="e8f83-158">Par conséquent, ces informations sont passées au plan de récupération ASR en tant qu’éléments du *contexte*.</span><span class="sxs-lookup"><span data-stu-id="e8f83-158">Hence this information is passed to the ASR recovery plan as part of the *context*.</span></span>

<span data-ttu-id="e8f83-159">Voici à quoi ressemble la variable de contexte.</span><span class="sxs-lookup"><span data-stu-id="e8f83-159">Below is an example of how the context variable looks.</span></span>

        {"RecoveryPlanName":"hrweb-recovery",

        "FailoverType":"Test",

        "FailoverDirection":"PrimaryToSecondary",

        "GroupId":"1",

        "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                {"CloudServiceName":"pod02hrweb-Chicago-test",

                "RoleName":"Fabrikam-Hrweb-frontend-test"}

                }

        }


<span data-ttu-id="e8f83-160">Le tableau ci-dessous contient le nom et la description de chaque variable dans le contexte.</span><span class="sxs-lookup"><span data-stu-id="e8f83-160">The table below contains name and description for each variable in the context.</span></span>

| <span data-ttu-id="e8f83-161">**Nom de la variable**</span><span class="sxs-lookup"><span data-stu-id="e8f83-161">**Variable name**</span></span> | <span data-ttu-id="e8f83-162">**Description**</span><span class="sxs-lookup"><span data-stu-id="e8f83-162">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="e8f83-163">RecoveryPlanName</span><span class="sxs-lookup"><span data-stu-id="e8f83-163">RecoveryPlanName</span></span> |<span data-ttu-id="e8f83-164">Nom du plan en cours d'exécution.</span><span class="sxs-lookup"><span data-stu-id="e8f83-164">Name of plan being run.</span></span> <span data-ttu-id="e8f83-165">Vous permet d'entreprendre une action basée sur le nom à l'aide du même script</span><span class="sxs-lookup"><span data-stu-id="e8f83-165">Helps you take action based on name using the same script</span></span> |
| <span data-ttu-id="e8f83-166">FailoverType</span><span class="sxs-lookup"><span data-stu-id="e8f83-166">FailoverType</span></span> |<span data-ttu-id="e8f83-167">Indique si le basculement est un test, planifié ou non planifié.</span><span class="sxs-lookup"><span data-stu-id="e8f83-167">Specifies whether the failover is test, planned, or unplanned.</span></span> |
| <span data-ttu-id="e8f83-168">FailoverDirection</span><span class="sxs-lookup"><span data-stu-id="e8f83-168">FailoverDirection</span></span> |<span data-ttu-id="e8f83-169">Indique si la récupération est principale ou secondaire</span><span class="sxs-lookup"><span data-stu-id="e8f83-169">Specify whether recovery is to primary or secondary</span></span> |
| <span data-ttu-id="e8f83-170">GroupID</span><span class="sxs-lookup"><span data-stu-id="e8f83-170">GroupID</span></span> |<span data-ttu-id="e8f83-171">Identifie le numéro de groupe dans le plan de récupération lorsque le plan est en cours d'exécution.</span><span class="sxs-lookup"><span data-stu-id="e8f83-171">Identify the group number within the recovery plan when the plan is running</span></span> |
| <span data-ttu-id="e8f83-172">VmMap</span><span class="sxs-lookup"><span data-stu-id="e8f83-172">VmMap</span></span> |<span data-ttu-id="e8f83-173">Tableau de toutes les machines virtuelles du groupe.</span><span class="sxs-lookup"><span data-stu-id="e8f83-173">Array of all the virtual machines in the group</span></span> |
| <span data-ttu-id="e8f83-174">Clé VMMap</span><span class="sxs-lookup"><span data-stu-id="e8f83-174">VMMap key</span></span> |<span data-ttu-id="e8f83-175">Clé unique (GUID) pour chaque machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e8f83-175">Unique key (GUID) for each VM.</span></span> <span data-ttu-id="e8f83-176">Ce GUID est identique à l’ID VMM de la machine virtuelle, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="e8f83-176">It's the same as the VMM ID of the virtual machine where applicable.</span></span> |
| <span data-ttu-id="e8f83-177">RoleName</span><span class="sxs-lookup"><span data-stu-id="e8f83-177">RoleName</span></span> |<span data-ttu-id="e8f83-178">Nom de la machine virtuelle Azure qui est en cours de récupération</span><span class="sxs-lookup"><span data-stu-id="e8f83-178">Name of the Azure VM that's being recovered</span></span> |
| <span data-ttu-id="e8f83-179">CloudServiceName</span><span class="sxs-lookup"><span data-stu-id="e8f83-179">CloudServiceName</span></span> |<span data-ttu-id="e8f83-180">Nom Azure Cloud Service sous lequel la machine virtuelle est créée.</span><span class="sxs-lookup"><span data-stu-id="e8f83-180">Azure Cloud Service name under which the virtual machine is created.</span></span> |

<span data-ttu-id="e8f83-181">Pour identifier la valeur du paramètre « VmMap Key » dans le contexte, vous pouvez également accéder à la page des propriétés de la machine virtuelle dans ASR et examiner la propriété GUID VM.</span><span class="sxs-lookup"><span data-stu-id="e8f83-181">To identify the VmMap Key in the context you could also go to the VM properties page in ASR and look at the VM GUID property.</span></span>

![](media/site-recovery-runbook-automation/13.png)

## <a name="author-an-automation-runbook"></a><span data-ttu-id="e8f83-182">Créer un Runbook Automation</span><span class="sxs-lookup"><span data-stu-id="e8f83-182">Author an Automation runbook</span></span>
<span data-ttu-id="e8f83-183">À présent, créez le Runbook pour ouvrir le port 80 sur la machine virtuelle frontale.</span><span class="sxs-lookup"><span data-stu-id="e8f83-183">Now create the runbook to open port 80 on the front-end virtual machine.</span></span>

1. <span data-ttu-id="e8f83-184">Créez un Runbook dans le compte Microsoft Azure Automation, en lui donnant le nom **OpenPort80**</span><span class="sxs-lookup"><span data-stu-id="e8f83-184">Create a new runbook in the Azure Automation account with the name **OpenPort80**</span></span>

   ![](media/site-recovery-runbook-automation/14.png)
2. <span data-ttu-id="e8f83-185">Accédez à la vue Auteur du Runbook et optez pour le mode brouillon.</span><span class="sxs-lookup"><span data-stu-id="e8f83-185">Navigate to the Author view of the runbook and enter the draft mode.</span></span>
3. <span data-ttu-id="e8f83-186">Commencez par spécifier la variable à utiliser en tant que contexte du plan de récupération.</span><span class="sxs-lookup"><span data-stu-id="e8f83-186">First specify the variable to use as the recovery plan context</span></span>

   ```
       param (
           [Object]$RecoveryPlanContext
       )

   ```
4. <span data-ttu-id="e8f83-187">Ensuite, connectez-vous à l’abonnement avec le nom d’abonnement et les informations d’identification adéquats.</span><span class="sxs-lookup"><span data-stu-id="e8f83-187">Next connect to the subscription using the credential and subscription name</span></span>

   ```
       $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

       # Connect to Azure
       $AzureAccount = Add-AzureAccount -Credential $Cred
       $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
       Select-AzureSubscription -SubscriptionName $AzureSubscriptionName
   ```

   <span data-ttu-id="e8f83-188">Remarque : vous pouvez utiliser ici les ressources Microsoft Azure intitulées **AzureCredential** et **AzureSubscriptionName**.</span><span class="sxs-lookup"><span data-stu-id="e8f83-188">Note that you use the Azure assets – **AzureCredential** and **AzureSubscriptionName** here.</span></span>
5. <span data-ttu-id="e8f83-189">À présent, indiquez les informations relatives au point de terminaison et au GUID de la machine virtuelle pour laquelle vous souhaitez exposer le point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="e8f83-189">Now specify the endpoint details and the GUID of the virtual machine for which you want to expose the endpoint.</span></span> <span data-ttu-id="e8f83-190">Dans ce cas, la machine virtuelle frontale.</span><span class="sxs-lookup"><span data-stu-id="e8f83-190">In this case the front-end virtual machine.</span></span>

   ```
       # Specify the parameters to be used by the script
       $AEProtocol = "TCP"
       $AELocalPort = 80
       $AEPublicPort = 80
       $AEName = "Port 80 for HTTP"
       $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"
   ```

   <span data-ttu-id="e8f83-191">Cela permet de spécifier le protocole du point de terminaison Microsoft Azure, le port local sur la machine virtuelle et le port public mappé qui lui est associé.</span><span class="sxs-lookup"><span data-stu-id="e8f83-191">This specifies the Azure endpoint protocol, local port on the VM and its mapped public port.</span></span> <span data-ttu-id="e8f83-192">Ces variables sont les paramètres requis par les commandes Microsoft Azure qui ajoutent des points de terminaison aux machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="e8f83-192">These variables are parameters     required by the Azure commands that add endpoints to VMs.</span></span> <span data-ttu-id="e8f83-193">La valeur VMGUID conserve le GUID de la machine virtuelle sur laquelle vous devez agir.</span><span class="sxs-lookup"><span data-stu-id="e8f83-193">The VMGUID holds the GUID of the virtual machine you need to operate on.</span></span>
6. <span data-ttu-id="e8f83-194">Le script va maintenant extraire le contexte de la valeur VMGUID donnée et créer un point de terminaison sur la machine virtuelle qu’il référence.</span><span class="sxs-lookup"><span data-stu-id="e8f83-194">The script will now extract the context for the given VM GUID and create an endpoint on the virtual machine referenced by it.</span></span>

   ```
       #Read the VM GUID from the context
       $VM = $RecoveryPlanContext.VmMap.$VMGUID

       if ($VM -ne $null)
       {
           # Invoke pipeline commands within an InlineScript

           $EndpointStatus = InlineScript {
               # Invoke the necessary pipeline commands to add a Azure Endpoint to a specified Virtual Machine
               # Commands include: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including parameters)

               $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                   Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                   Update-AzureVM
               Write-Output $Status
           }
       }
   ```
7. <span data-ttu-id="e8f83-195">Une fois cette opération terminée, appuyez sur l’option Publier ( ![](media/site-recovery-runbook-automation/20.png) ) pour autoriser la mise à disponibilité de votre script pour l’exécution.</span><span class="sxs-lookup"><span data-stu-id="e8f83-195">Once this is complete, hit Publish ![](media/site-recovery-runbook-automation/20.png) to allow your script to be available for execution.</span></span>

<span data-ttu-id="e8f83-196">Le script complet est indiqué ci-dessous, à titre de référence.</span><span class="sxs-lookup"><span data-stu-id="e8f83-196">The complete script is given below for your reference</span></span>

```
  workflow OpenPort80
  {
    param (
        [Object]$RecoveryPlanContext
    )

    $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

    # Connect to Azure
    $AzureAccount = Add-AzureAccount -Credential $Cred
    $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
    Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

    # Specify the parameters to be used by the script
    $AEProtocol = "TCP"
    $AELocalPort = 80
    $AEPublicPort = 80
    $AEName = "Port 80 for HTTP"
    $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"

    #Read the VM GUID from the context
    $VM = $RecoveryPlanContext.VmMap.$VMGUID

    if ($VM -ne $null)
    {
        # Invoke pipeline commands within an InlineScript

        $EndpointStatus = InlineScript {
            # Invoke the necessary pipeline commands to add an Azure Endpoint to a specified Virtual Machine
            # This set of commands includes: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including necessary parameters)

            $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                Update-AzureVM
            Write-Output $Status
        }
    }
  }
```

## <a name="add-the-script-to-the-recovery-plan"></a><span data-ttu-id="e8f83-197">Ajouter le script au plan de récupération</span><span class="sxs-lookup"><span data-stu-id="e8f83-197">Add the script to the recovery plan</span></span>
<span data-ttu-id="e8f83-198">Une fois que le script est prêt, vous pouvez l’ajouter au plan de récupération créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="e8f83-198">Once the script is ready, you can add it to the recovery plan that you created earlier.</span></span>

1. <span data-ttu-id="e8f83-199">Dans le plan de récupération que vous avez créé, optez pour l’ajout d’un script après le groupe 2.</span><span class="sxs-lookup"><span data-stu-id="e8f83-199">In the recovery plan you created, choose to add a script after the group 2.</span></span> ![](media/site-recovery-runbook-automation/15.png)
2. <span data-ttu-id="e8f83-200">Spécifiez un nom de script.</span><span class="sxs-lookup"><span data-stu-id="e8f83-200">Specify a script name.</span></span> <span data-ttu-id="e8f83-201">Il s’agit simplement d’un nom convivial pour ce script, qui doit s’afficher dans le plan de récupération.</span><span class="sxs-lookup"><span data-stu-id="e8f83-201">This is just a friendly name for this script for showing within the Recovery plan.</span></span>
3. <span data-ttu-id="e8f83-202">Lors du basculement vers le script Microsoft Azure, sélectionnez le nom de compte Microsoft Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="e8f83-202">In the failover to Azure script – Select the Azure Automation Account name.</span></span>
4. <span data-ttu-id="e8f83-203">Dans la liste des Runbooks Microsoft Azure, sélectionnez le Runbook que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="e8f83-203">In the Azure Runbooks, select the runbook you authored.</span></span>

![](media/site-recovery-runbook-automation/16.png)

## <a name="primary-side-scripts"></a><span data-ttu-id="e8f83-204">Scripts côté principal</span><span class="sxs-lookup"><span data-stu-id="e8f83-204">Primary side scripts</span></span>
<span data-ttu-id="e8f83-205">Lorsque vous exécutez un basculement vers Azure, vous pouvez également choisir d'exécuter des scripts côté principal.</span><span class="sxs-lookup"><span data-stu-id="e8f83-205">When you are executing a failover to Azure, you can also choose to execute primary side scripts.</span></span> <span data-ttu-id="e8f83-206">Ces scripts seront exécutés sur le serveur VMM pendant le basculement.</span><span class="sxs-lookup"><span data-stu-id="e8f83-206">These scripts will run on the VMM server during failover.</span></span>
<span data-ttu-id="e8f83-207">Les scripts côté principal ne sont disponibles que pour les phases précédant et suivant l’arrêt.</span><span class="sxs-lookup"><span data-stu-id="e8f83-207">Primary side scripts are only available only for pre-shutdown and post shutdown stages.</span></span> <span data-ttu-id="e8f83-208">En effet, nous prévoyons que le site principal ne sera généralement pas disponible lors des incidents.</span><span class="sxs-lookup"><span data-stu-id="e8f83-208">This is because we expect the primary site to be typically unavailable when a disaster strikes.</span></span>
<span data-ttu-id="e8f83-209">Pendant un basculement non planifié, et uniquement si vous optez pour les opérations de site principal, il tentera d'exécuter les scripts côté principal.</span><span class="sxs-lookup"><span data-stu-id="e8f83-209">During an unplanned failover, only if you opt in for primary site operations, it will attempt to run the primary side scripts.</span></span> <span data-ttu-id="e8f83-210">S’ils ne sont pas accessibles ou si le délai d'attente est dépassé, le basculement continuera de récupérer les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="e8f83-210">If they are not reachable or timeout, the failover will continue to recover the virtual machines.</span></span>
<span data-ttu-id="e8f83-211">Les scripts côté principal ne sont pas disponibles pour les sites VMware/physiques/Hyper-V sans VMM protégé vers Azure - lors du basculement vers Azure.</span><span class="sxs-lookup"><span data-stu-id="e8f83-211">Primary side scripts are un-available for VMware/Physical/Hyper-v Sites without VMM protected to Azure - while you failover to Azure.</span></span>
<span data-ttu-id="e8f83-212">Toutefois, lors de la restauration à partir d’Azure vers un serveur local, les scripts côté principal (Runbook) peuvent être utilisés pour toutes les cibles à l’exception de VMware.</span><span class="sxs-lookup"><span data-stu-id="e8f83-212">However, when you failback from Azure to on-premises, primary side scripts (Runbooks) can be used for all targets except VMware.</span></span>

## <a name="test-the-recovery-plan"></a><span data-ttu-id="e8f83-213">Tester le plan de récupération</span><span class="sxs-lookup"><span data-stu-id="e8f83-213">Test the recovery plan</span></span>
<span data-ttu-id="e8f83-214">Une fois que vous avez ajouté le Runbook au plan, vous pouvez lancer un test de basculement et le voir s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="e8f83-214">Once you have added the runbook to the plan you can initiate a test failover and see it in action.</span></span> <span data-ttu-id="e8f83-215">Nous vous recommandons d’exécuter systématiquement un basculement de test pour tester l’application et le plan de récupération, afin de vérifier qu’ils ne présentent aucune erreur.</span><span class="sxs-lookup"><span data-stu-id="e8f83-215">It is always recommended to run a test failover to test your application and the recovery plan to ensure that there are no errors.</span></span>

1. <span data-ttu-id="e8f83-216">Sélectionnez le plan de récupération et démarrez un test de basculement.</span><span class="sxs-lookup"><span data-stu-id="e8f83-216">Select the recovery plan and initiate a test failover.</span></span>
2. <span data-ttu-id="e8f83-217">Pendant l’exécution du plan, vous pouvez voir si le Runbook s’est exécuté ou non, en consultant son état.</span><span class="sxs-lookup"><span data-stu-id="e8f83-217">During the plan execution, you can see whether the runbook has executed or not via its status.</span></span>

   ![](media/site-recovery-runbook-automation/17.png)
3. <span data-ttu-id="e8f83-218">Vous pouvez également voir le détail de l’état d’exécution du Runbook sur la page des tâches Microsoft Azure Automation pour le Runbook.</span><span class="sxs-lookup"><span data-stu-id="e8f83-218">You can also see the detailed runbook execution status on the Azure Automation jobs page for the runbook.</span></span>

   ![](media/site-recovery-runbook-automation/18.png)
4. <span data-ttu-id="e8f83-219">Une fois le basculement terminé, mis à part le résultat de l’exécution du Runbook, vous pouvez voir si l’exécution a abouti en consultant la page relative à la machine virtuelle Microsoft Azure et en examinant les points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="e8f83-219">After the failover completes, apart from the runbook execution result, you can see whether the execution is successful or not by visiting the Azure virtual machine page and looking at the endpoints.</span></span>

![](media/site-recovery-runbook-automation/19.png)

## <a name="sample-scripts"></a><span data-ttu-id="e8f83-220">Exemples de scripts</span><span class="sxs-lookup"><span data-stu-id="e8f83-220">Sample scripts</span></span>
<span data-ttu-id="e8f83-221">Dans ce didacticiel, nous avons passé en revue la procédure d’automatisation d’une tâche fréquemment exécutée, qui inclut l’ajout d’un point de terminaison à une machine virtuelle Microsoft Azure. Cependant, Microsoft Azure Automation vous permet d’effectuer d’autres tâches d’automatisation très puissantes.</span><span class="sxs-lookup"><span data-stu-id="e8f83-221">While we walked through automating one commonly used task of adding an endpoint to an Azure virtual machine in this tutorial, you could do a number of other powerful automation tasks using Azure automation.</span></span> <span data-ttu-id="e8f83-222">Microsoft et la communauté Microsoft Azure Automation proposent des exemples de Runbooks qui peuvent vous aider à créer vos propres solutions, ainsi que des Runbooks utilitaires, que vous pouvez ensuite utiliser en tant que composantes pour des tâches d’automatisation plus importantes.</span><span class="sxs-lookup"><span data-stu-id="e8f83-222">Microsoft and the Azure Automation community provide sample runbooks which can help you get started creating your own solutions, and utility runbooks, which you can use as building blocks for larger automation tasks.</span></span> <span data-ttu-id="e8f83-223">Vous pouvez les utiliser à partir de la galerie et créer des plans de récupération puissants pour vos applications, en un seul clic à l’aide d’Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="e8f83-223">Start using them from the gallery and build  powerful one-click recovery plans for your applications using Azure Site Recovery.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e8f83-224">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="e8f83-224">Additional Resources</span></span>
[<span data-ttu-id="e8f83-225">Vue d’ensemble de Microsoft Azure Automation</span><span class="sxs-lookup"><span data-stu-id="e8f83-225">Azure Automation Overview</span></span>](http://msdn.microsoft.com/library/azure/dn643629.aspx "Vue d’ensemble de Microsoft Azure Automation")

[<span data-ttu-id="e8f83-226">Exemples de scripts Microsoft Azure Automation</span><span class="sxs-lookup"><span data-stu-id="e8f83-226">Sample Azure Automation Scripts</span></span>](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Exemples de scripts Microsoft Azure Automation")
