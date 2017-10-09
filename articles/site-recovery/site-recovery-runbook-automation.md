---
title: plans de toorecovery runbooks aaaAdd Azure Automation dans Azure Site Recovery | Documents Microsoft
description: "Découvrez comment Azure Site Recovery peut vous aider à étendre des plans de récupération à l’aide d’Azure Automation. Découvrez comment toocomplete complexe tâches pendant la récupération tooAzure."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: ecece14d-5f92-4596-bbaf-5204addb95c2
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/23/2017
ms.author: ruturajd@microsoft.com
ms.openlocfilehash: 90d517200cec5527e98a0d00da466bace587b70b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-automation-runbooks-toorecovery-plans"></a><span data-ttu-id="6a9a6-104">Ajouter des plans de toorecovery runbooks Azure Automation</span><span class="sxs-lookup"><span data-stu-id="6a9a6-104">Add Azure Automation runbooks toorecovery plans</span></span>
<span data-ttu-id="6a9a6-105">Dans cet article, nous décrivons comment Azure Site Recovery s’intègre à Azure Automation toohelp vous étendez vos plans de récupération.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-105">In this article, we describe how Azure Site Recovery integrates with Azure Automation toohelp you extend your recovery plans.</span></span> <span data-ttu-id="6a9a6-106">Des plans de récupération peuvent orchestrer la récupération de machines virtuelles protégées par Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-106">Recovery plans can orchestrate recovery of VMs that are protected with Site Recovery.</span></span> <span data-ttu-id="6a9a6-107">Plans de récupération fonctionnent aussi bien pour le cloud secondaire tooa de réplication et tooAzure de réplication.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-107">Recovery plans work both for replication tooa secondary cloud, and for replication tooAzure.</span></span> <span data-ttu-id="6a9a6-108">Plans de récupération également aider à effectuer la récupération de hello **précis et constants**, **repeatable**, et **automatisée**.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-108">Recovery plans also help make hello recovery **consistently accurate**, **repeatable**, and **automated**.</span></span> <span data-ttu-id="6a9a6-109">Si vous basculez votre tooAzure de machines virtuelles, l’intégration avec Azure Automation étend vos plans de récupération.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-109">If you fail over your VMs tooAzure, integration with Azure Automation extends your recovery plans.</span></span> <span data-ttu-id="6a9a6-110">Vous pouvez l’utiliser tooexecute runbooks, qui offrent des tâches d’automatisation puissantes.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-110">You can use it tooexecute runbooks, which offer powerful automation tasks.</span></span>

<span data-ttu-id="6a9a6-111">Si vous êtes de nouveau tooAzure Automation, vous pouvez [inscrire](https://azure.microsoft.com/services/automation/) et [télécharger des exemples de scripts](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="6a9a6-111">If you are new tooAzure Automation, you can [sign up](https://azure.microsoft.com/services/automation/) and [download sample scripts](https://azure.microsoft.com/documentation/scripts/).</span></span> <span data-ttu-id="6a9a6-112">Pour plus d’informations, toolearn comment tooAzure de récupération tooorchestrate à l’aide de [plans de récupération](https://azure.microsoft.com/blog/?p=166264), consultez [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="6a9a6-112">For more information, and toolearn how tooorchestrate recovery tooAzure by using [recovery plans](https://azure.microsoft.com/blog/?p=166264), see [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/).</span></span>

<span data-ttu-id="6a9a6-113">Cet article explique comment intégrer des runbooks Azure Automation dans vos plans de récupération.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-113">In this article, we describe how you can integrate Azure Automation runbooks into your recovery plans.</span></span> <span data-ttu-id="6a9a6-114">Nous utilisons des exemples tooautomate tâches de base qui nécessitaient auparavant une intervention manuelle.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-114">We use examples tooautomate basic tasks that previously required manual intervention.</span></span> <span data-ttu-id="6a9a6-115">Nous expliquons également comment tooconvert un tooa de récupération en plusieurs étapes par simple clic action de récupération.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-115">We also describe how tooconvert a multi-step recovery tooa single-click recovery action.</span></span>

## <a name="customize-hello-recovery-plan"></a><span data-ttu-id="6a9a6-116">Personnaliser le plan de récupération hello</span><span class="sxs-lookup"><span data-stu-id="6a9a6-116">Customize hello recovery plan</span></span>
1. <span data-ttu-id="6a9a6-117">Accédez toohello **Site Recovery** panneau des ressources plan de récupération.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-117">Go toohello **Site Recovery** recovery plan resource blade.</span></span> <span data-ttu-id="6a9a6-118">Pour cet exemple, le plan de récupération hello a deux tooit ajouté machines virtuelles pour la récupération.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-118">For this example, hello recovery plan has two VMs added tooit, for recovery.</span></span> <span data-ttu-id="6a9a6-119">toobegin Ajout d’un runbook, cliquez sur hello **personnaliser** onglet.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-119">toobegin adding a runbook, click hello **Customize** tab.</span></span>

    ![Cliquez sur le bouton de personnaliser hello](media/site-recovery-runbook-automation-new/essentials-rp.png)


2. <span data-ttu-id="6a9a6-121">Cliquez avec le bouton droit sur **Group 1: Start**, puis sélectionnez **Ajouter une action postérieure**.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-121">Right-click **Group 1: Start**, and then select **Add post action**.</span></span>

    ![Cliquer avec le bouton droit sur Group 1: Start, puis ajouter une action postérieure](media/site-recovery-runbook-automation-new/customize-rp.png)

3. <span data-ttu-id="6a9a6-123">Cliquez sur **Choisir un script**.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-123">Click **Choose a script**.</span></span>

4. <span data-ttu-id="6a9a6-124">Sur hello **action mettre à jour** panneau, le script de nom hello **Hello World**.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-124">On hello **Update action** blade, name hello script **Hello World**.</span></span>

    ![panneau d’action Hello mise à jour](media/site-recovery-runbook-automation-new/update-rp.png)

5. <span data-ttu-id="6a9a6-126">Choisissez un nom de compte Automation.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-126">Enter an Automation account name.</span></span>
    >[!NOTE]
    > <span data-ttu-id="6a9a6-127">Hello compte Automation peut être dans n’importe quelle région Azure.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-127">hello Automation account can be in any Azure region.</span></span> <span data-ttu-id="6a9a6-128">Hello compte Automation doit être Bonjour même abonnement que le coffre Azure Site Recovery hello.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-128">hello Automation account must be in hello same subscription as hello Azure Site Recovery vault.</span></span>

6. <span data-ttu-id="6a9a6-129">Dans votre compte Automation, sélectionnez un runbook.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-129">In your Automation account, select a runbook.</span></span> <span data-ttu-id="6a9a6-130">Ce runbook est hello du script qui s’exécute pendant l’exécution de hello hello du plan de récupération, après la récupération hello du premier groupe de hello.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-130">This runbook is hello script that runs during hello execution of hello recovery plan, after hello recovery of hello first group.</span></span>

7. <span data-ttu-id="6a9a6-131">script de hello toosave, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-131">toosave hello script, click **OK**.</span></span> <span data-ttu-id="6a9a6-132">script de Hello est ajouté trop**groupe 1 : POST-étapes**.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-132">hello script is added too**Group 1: Post-steps**.</span></span>

    ![Action postérieure Group 1:Start](media/site-recovery-runbook-automation-new/addedscript-rp.PNG)


## <a name="considerations-for-adding-a-script"></a><span data-ttu-id="6a9a6-134">Considérations relatives à l’ajout d’un script</span><span class="sxs-lookup"><span data-stu-id="6a9a6-134">Considerations for adding a script</span></span>

* <span data-ttu-id="6a9a6-135">Pour les options trop**supprimer une étape** ou **mettre à jour hello script**, avec le bouton droit de script de hello.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-135">For options too**delete a step** or **update hello script**, right-click hello script.</span></span>
* <span data-ttu-id="6a9a6-136">Un script peut s’exécuter sur Azure pendant le basculement à partir d’un tooAzure d’ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-136">A script can run on Azure during failover from an on-premises machine tooAzure.</span></span> <span data-ttu-id="6a9a6-137">Il peut s’exécutent également sur Azure en tant que site principal script avant l’arrêt, pendant la restauration à partir de l’ordinateur local, Azure tooan.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-137">It also can run on Azure as a primary-site script before shutdown, during failback from Azure tooan on-premises machine.</span></span>
* <span data-ttu-id="6a9a6-138">Lorsqu’un script s’exécute, il injecte un contexte de plan de récupération.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-138">When a script runs, it injects a recovery plan context.</span></span> <span data-ttu-id="6a9a6-139">Bonjour à l’exemple suivant montre une variable de contexte :</span><span class="sxs-lookup"><span data-stu-id="6a9a6-139">hello following example shows a context variable:</span></span>

    ```
            {"RecoveryPlanName":"hrweb-recovery",

            "FailoverType":"Test",

            "FailoverDirection":"PrimaryToSecondary",

            "GroupId":"1",

            "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                    { "SubscriptionId":"7a1111111-c1d6-49c5-8c5d-111ce8dd183",

                    "ResourceGroupName":"ContosoRG",

                    "CloudServiceName":"pod02hrweb-Chicago-test",

                    "RoleName":"Fabrikam-Hrweb-frontend-test",

                    "RecoveryPointId":"TimeStamp"}

                    }

            }
    ```

    <span data-ttu-id="6a9a6-140">Hello tableau suivant répertorie le nom de hello et une description de chaque variable dans le contexte de hello.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-140">hello following table lists hello name and description of each variable in hello context.</span></span>

    | <span data-ttu-id="6a9a6-141">**Nom de la variable**</span><span class="sxs-lookup"><span data-stu-id="6a9a6-141">**Variable name**</span></span> | <span data-ttu-id="6a9a6-142">**Description**</span><span class="sxs-lookup"><span data-stu-id="6a9a6-142">**Description**</span></span> |
    | --- | --- |
    | <span data-ttu-id="6a9a6-143">RecoveryPlanName</span><span class="sxs-lookup"><span data-stu-id="6a9a6-143">RecoveryPlanName</span></span> |<span data-ttu-id="6a9a6-144">nom de Hello du plan hello en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-144">hello name of hello plan being run.</span></span> <span data-ttu-id="6a9a6-145">Cette variable vous permet de prendre des mesures différentes selon le nom de plan de récupération hello.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-145">This variable helps you take different actions based on hello recovery plan name.</span></span> <span data-ttu-id="6a9a6-146">Vous pouvez également réutiliser le script de hello.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-146">You also can reuse hello script.</span></span> |
    | <span data-ttu-id="6a9a6-147">FailoverType</span><span class="sxs-lookup"><span data-stu-id="6a9a6-147">FailoverType</span></span> |<span data-ttu-id="6a9a6-148">Spécifie si le basculement de hello est un test, planifié ou non planifié.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-148">Specifies whether hello failover is a test, planned, or unplanned.</span></span> |
    | <span data-ttu-id="6a9a6-149">FailoverDirection</span><span class="sxs-lookup"><span data-stu-id="6a9a6-149">FailoverDirection</span></span> |<span data-ttu-id="6a9a6-150">Spécifie si la récupération est le site principal ou secondaire de tooa.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-150">Specifies whether recovery is tooa primary or secondary site.</span></span> |
    | <span data-ttu-id="6a9a6-151">GroupID</span><span class="sxs-lookup"><span data-stu-id="6a9a6-151">GroupID</span></span> |<span data-ttu-id="6a9a6-152">Identifie le numéro de groupe hello dans le plan de récupération hello lorsque le plan de hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-152">Identifies hello group number in hello recovery plan when hello plan is running.</span></span> |
    | <span data-ttu-id="6a9a6-153">VmMap</span><span class="sxs-lookup"><span data-stu-id="6a9a6-153">VmMap</span></span> |<span data-ttu-id="6a9a6-154">Un tableau de tous les ordinateurs virtuels dans le groupe de hello.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-154">An array of all VMs in hello group.</span></span> |
    | <span data-ttu-id="6a9a6-155">Clé VMMap</span><span class="sxs-lookup"><span data-stu-id="6a9a6-155">VMMap key</span></span> |<span data-ttu-id="6a9a6-156">Clé unique (GUID) pour chaque machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-156">A unique key (GUID) for each VM.</span></span> <span data-ttu-id="6a9a6-157">Son hello identique hello ID Azure Virtual Machine Manager (VMM) de hello machine virtuelle, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-157">It's hello same as hello Azure Virtual Machine Manager (VMM) ID of hello VM, where applicable.</span></span> |
    | <span data-ttu-id="6a9a6-158">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="6a9a6-158">SubscriptionId</span></span> |<span data-ttu-id="6a9a6-159">ID d’abonnement Azure Hello dans lequel hello machine virtuelle a été créé.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-159">hello Azure subscription ID in which hello VM was created.</span></span> |
    | <span data-ttu-id="6a9a6-160">RoleName</span><span class="sxs-lookup"><span data-stu-id="6a9a6-160">RoleName</span></span> |<span data-ttu-id="6a9a6-161">nom Hello Hello machine virtuelle Azure qui est en cours de récupération.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-161">hello name of hello Azure VM that's being recovered.</span></span> |
    | <span data-ttu-id="6a9a6-162">CloudServiceName</span><span class="sxs-lookup"><span data-stu-id="6a9a6-162">CloudServiceName</span></span> |<span data-ttu-id="6a9a6-163">nom du service cloud Azure Hello que sous lequel hello machine virtuelle a été créé.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-163">hello Azure cloud service name under which hello VM was created.</span></span> |
    | <span data-ttu-id="6a9a6-164">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="6a9a6-164">ResourceGroupName</span></span>|<span data-ttu-id="6a9a6-165">nom de groupe de ressources Azure Hello que sous lequel hello machine virtuelle a été créé.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-165">hello Azure resource group name under which hello VM was created.</span></span> |
    | <span data-ttu-id="6a9a6-166">RecoveryPointId</span><span class="sxs-lookup"><span data-stu-id="6a9a6-166">RecoveryPointId</span></span>|<span data-ttu-id="6a9a6-167">horodateur de Hello pour lorsque hello machine virtuelle est récupérée.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-167">hello timestamp for when hello VM is recovered.</span></span> |

* <span data-ttu-id="6a9a6-168">Vérifiez que ce compte Automation hello a hello suivant des modules :</span><span class="sxs-lookup"><span data-stu-id="6a9a6-168">Ensure that hello Automation account has hello following modules:</span></span>
    * <span data-ttu-id="6a9a6-169">AzureRM.profile</span><span class="sxs-lookup"><span data-stu-id="6a9a6-169">AzureRM.profile</span></span>
    * <span data-ttu-id="6a9a6-170">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="6a9a6-170">AzureRM.Resources</span></span>
    * <span data-ttu-id="6a9a6-171">AzureRM.Automation</span><span class="sxs-lookup"><span data-stu-id="6a9a6-171">AzureRM.Automation</span></span>
    * <span data-ttu-id="6a9a6-172">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="6a9a6-172">AzureRM.Network</span></span>
    * <span data-ttu-id="6a9a6-173">AzureRM.Compute</span><span class="sxs-lookup"><span data-stu-id="6a9a6-173">AzureRM.Compute</span></span>

<span data-ttu-id="6a9a6-174">Les versions de tous les modules doivent être compatibles.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-174">All modules should be of compatible versions.</span></span> <span data-ttu-id="6a9a6-175">Un tooensure facilement que tous les modules sont compatibles est toouse hello dernières versions de tous les modules hello.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-175">An easy way tooensure that all modules are compatible is toouse hello latest versions of all hello modules.</span></span>

### <a name="access-all-vms-of-hello-vmmap-in-a-loop"></a><span data-ttu-id="6a9a6-176">Accéder à tous les ordinateurs virtuels de hello VMMap dans une boucle</span><span class="sxs-lookup"><span data-stu-id="6a9a6-176">Access all VMs of hello VMMap in a loop</span></span>
<span data-ttu-id="6a9a6-177">Utilisez hello les de code tooloop sur tous les ordinateurs virtuels de hello Microsoft VMMap :</span><span class="sxs-lookup"><span data-stu-id="6a9a6-177">Use hello following code tooloop across all VMs of hello Microsoft VMMap:</span></span>

```
$VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
$vmMap = $RecoveryPlanContext.VmMap
 foreach($VMID in $VMinfo)
 {
     $VM = $vmMap.$VMID                
             if( !(($VM -eq $Null) -Or ($VM.ResourceGroupName -eq $Null) -Or ($VM.RoleName -eq $Null))) {
         #this check is tooensure that we skip when some data is not available else it will fail
 Write-output "Resource group name ", $VM.ResourceGroupName
 Write-output "Rolename " = $VM.RoleName
     }
 }

```

> [!NOTE]
> <span data-ttu-id="6a9a6-178">Hello ressource groupe nom et le rôle de valeurs de nom sont vides quand le script de hello est un groupe de démarrage pré tooa.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-178">hello resource group name and role name values are empty when hello script is a pre-action tooa boot group.</span></span> <span data-ttu-id="6a9a6-179">les valeurs Hello sont remplies uniquement si hello machine virtuelle de ce groupe réussit au basculement.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-179">hello values are populated only if hello VM of that group succeeds in failover.</span></span> <span data-ttu-id="6a9a6-180">script de Hello est une post-action du groupe de démarrage hello.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-180">hello script is a post-action of hello boot group.</span></span>

## <a name="use-hello-same-automation-runbook-in-multiple-recovery-plans"></a><span data-ttu-id="6a9a6-181">Utilisez hello même runbook Automation dans plusieurs plans de récupération</span><span class="sxs-lookup"><span data-stu-id="6a9a6-181">Use hello same Automation runbook in multiple recovery plans</span></span>

<span data-ttu-id="6a9a6-182">Vous pouvez utiliser un même script dans plusieurs plans de récupération à l’aide de variables externes.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-182">You can use a single script in multiple recovery plans by using external variables.</span></span> <span data-ttu-id="6a9a6-183">Vous pouvez utiliser [variables Azure Automation](../automation/automation-variables.md) toostore les paramètres que vous pouvez passer d’une récupération de l’exécution du plan.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-183">You can use [Azure Automation variables](../automation/automation-variables.md) toostore parameters that you can pass for a recovery plan execution.</span></span> <span data-ttu-id="6a9a6-184">En ajoutant le nom de plan de récupération hello en tant que préfixe toohello variable, vous pouvez créer des variables individuelles pour chaque plan de récupération.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-184">By adding hello recovery plan name as a prefix toohello variable, you can create individual variables for each recovery plan.</span></span> <span data-ttu-id="6a9a6-185">Ensuite, utilisez les variables hello en tant que paramètres.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-185">Then, use hello variables as parameters.</span></span> <span data-ttu-id="6a9a6-186">Vous pouvez modifier un paramètre sans modifier le script de hello, mais toujours modifier hello hello façon script fonctionne.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-186">You can change a parameter without changing hello script, but still change hello way hello script works.</span></span>

### <a name="use-a-simple-string-variable-in-a-runbook-script"></a><span data-ttu-id="6a9a6-187">Utiliser une variable chaîne simple dans un script de runbook</span><span class="sxs-lookup"><span data-stu-id="6a9a6-187">Use a simple string variable in a runbook script</span></span>

<span data-ttu-id="6a9a6-188">Dans cet exemple, un script accepte l’entrée d’un groupe de sécurité réseau (NSG) hello et elle applique des machines virtuelles de toohello d’un plan de récupération.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-188">In this example, a script takes hello input of a Network Security Group (NSG) and applies it toohello VMs of a recovery plan.</span></span>

<span data-ttu-id="6a9a6-189">Pour toodetect de script hello le plan de récupération est en cours d’exécution, utilisez le contexte hello du plan de récupération :</span><span class="sxs-lookup"><span data-stu-id="6a9a6-189">For hello script toodetect which recovery plan is running, use hello recovery plan context:</span></span>

```
workflow AddPublicIPAndNSG {
    param (
          [parameter(Mandatory=$false)]
          [Object]$RecoveryPlanContext
    )

    $RPName = $RecoveryPlanContext.RecoveryPlanName
```

<span data-ttu-id="6a9a6-190">tooapply un groupe de sécurité réseau existant, vous devez connaître les nom de groupe de sécurité réseau hello et le nom de groupe de ressources de groupe de sécurité réseau hello.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-190">tooapply an existing NSG, you must know hello NSG name and hello NSG resource group name.</span></span> <span data-ttu-id="6a9a6-191">Utilisez ces variables en tant qu’entrées pour les scripts de plan de récupération.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-191">Use these variables as inputs for recovery plan scripts.</span></span> <span data-ttu-id="6a9a6-192">toodo, créez deux variables Bonjour ressources du compte Automation.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-192">toodo this, create two variables in hello Automation account assets.</span></span> <span data-ttu-id="6a9a6-193">Ajouter le nom hello hello du plan de récupération que vous créez des paramètres hello pour qu’un nom de variable toohello préfixe.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-193">Add hello name of hello recovery plan that you are creating hello parameters for as a prefix toohello variable name.</span></span>

1. <span data-ttu-id="6a9a6-194">Créer un nom de groupe de sécurité réseau toostore variable hello.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-194">Create a variable toostore hello NSG name.</span></span> <span data-ttu-id="6a9a6-195">Ajouter un nom de variable toohello préfixe à l’aide du nom hello hello du plan de récupération.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-195">Add a prefix toohello variable name by using hello name of hello recovery plan.</span></span>

    ![Créer la variable du nom de groupe de sécurité réseau](media/site-recovery-runbook-automation-new/var1.png)

2. <span data-ttu-id="6a9a6-197">Créer un nom de groupe de ressources d’un NSG hello toostore variable.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-197">Create a variable toostore hello NSG's resource group name.</span></span> <span data-ttu-id="6a9a6-198">Ajouter un nom de variable toohello préfixe à l’aide du nom hello hello du plan de récupération.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-198">Add a prefix toohello variable name by using hello name of hello recovery plan.</span></span>

    ![Créer un nom de groupe de ressources de groupe de sécurité réseau](media/site-recovery-runbook-automation-new/var2.png)


3.  <span data-ttu-id="6a9a6-200">Dans le script de hello, utilisez hello référence code tooget hello variable valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="6a9a6-200">In hello script, use hello following reference code tooget hello variable values:</span></span>

    ```
    $NSGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSG"
    $NSGRGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSGRG"

    $NSGnameVar = Get-AutomationVariable -Name $NSGValue
    $RGnameVar = Get-AutomationVariable -Name $NSGRGValue
    ```

4.  <span data-ttu-id="6a9a6-201">Utilisez les variables hello dans hello runbook tooapply hello NSG toohello interface réseau de hello basculéent machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="6a9a6-201">Use hello variables in hello runbook tooapply hello NSG toohello network interface of hello failed-over VM:</span></span>

    ```
    InlineScript {
    if (($Using:NSGname -ne $Null) -And ($Using:NSGRGname -ne $Null)) {
            $NSG = Get-AzureRmNetworkSecurityGroup -Name $Using:NSGname -ResourceGroupName $Using:NSGRGname
            Write-output $NSG.Id
            #Apply hello NSG tooa network interface
            #$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
            #Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
            #  -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $NSG
        }
    }
    ```

<span data-ttu-id="6a9a6-202">Pour chaque plan de récupération, créez des variables indépendantes afin que vous puissiez réutiliser les script hello.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-202">For each recovery plan, create independent variables so that you can reuse hello script.</span></span> <span data-ttu-id="6a9a6-203">Ajouter un préfixe à l’aide du nom de plan de récupération hello.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-203">Add a prefix by using hello recovery plan name.</span></span> <span data-ttu-id="6a9a6-204">Pour obtenir un script complète, de bout en bout pour ce scénario, consultez [ajouter un tooVMs publique de l’adresse IP et le groupe de sécurité réseau pendant le test de basculement d’un plan de récupération de Site Recovery](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).</span><span class="sxs-lookup"><span data-stu-id="6a9a6-204">For a complete, end-to-end script for this scenario, see [Add a public IP and NSG tooVMs during test failover of a Site Recovery recovery plan](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).</span></span>


### <a name="use-a-complex-variable-toostore-more-information"></a><span data-ttu-id="6a9a6-205">Utilisez une variable complexe de toostore plus d’informations</span><span class="sxs-lookup"><span data-stu-id="6a9a6-205">Use a complex variable toostore more information</span></span>

<span data-ttu-id="6a9a6-206">Considérez un scénario dans lequel vous souhaitez un tooturn script unique sur une adresse IP publique sur des machines virtuelles spécifiques.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-206">Consider a scenario in which you want a single script tooturn on a public IP on specific VMs.</span></span> <span data-ttu-id="6a9a6-207">Dans un autre scénario, vous pourriez tooapply différents groupes de sécurité réseau sur différentes machines virtuelles (et non sur tous les ordinateurs virtuels).</span><span class="sxs-lookup"><span data-stu-id="6a9a6-207">In another scenario, you might want tooapply different NSGs on different VMs (not on all VMs).</span></span> <span data-ttu-id="6a9a6-208">Vous pouvez créer un script réutilisable pour tout plan de récupération.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-208">You can make a script that is reusable for any recovery plan.</span></span> <span data-ttu-id="6a9a6-209">Chaque plan de récupération peut avoir un nombre variable de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-209">Each recovery plan can have a variable number of VMs.</span></span> <span data-ttu-id="6a9a6-210">Par exemple, une récupération SharePoint a deux serveurs frontaux.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-210">For example, a SharePoint recovery has two front ends.</span></span> <span data-ttu-id="6a9a6-211">Une application métier n’a qu’un seul serveur frontal.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-211">A basic line-of-business (LOB) application has only one front end.</span></span> <span data-ttu-id="6a9a6-212">Vous ne pouvez pas créer des variables distinctes pour chaque plan de récupération.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-212">You cannot create separate variables for each recovery plan.</span></span> 

<span data-ttu-id="6a9a6-213">Bonjour l’exemple suivant, nous utiliser une technique de nouveau et créer un [variable complexe](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) dans les ressources de compte Azure Automation hello.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-213">In hello following example, we use a new technique and create a [complex variable](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) in hello Azure Automation account assets.</span></span> <span data-ttu-id="6a9a6-214">Pour ce faire, spécifiez plusieurs valeurs.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-214">You do this by specifying multiple values.</span></span> <span data-ttu-id="6a9a6-215">Vous devez utiliser Azure PowerShell toocomplete hello est comme suit :</span><span class="sxs-lookup"><span data-stu-id="6a9a6-215">You must use Azure PowerShell toocomplete hello following steps:</span></span>

1. <span data-ttu-id="6a9a6-216">Dans PowerShell, la connexion tooyour abonnement Azure :</span><span class="sxs-lookup"><span data-stu-id="6a9a6-216">In PowerShell, sign in tooyour Azure subscription:</span></span>

    ```
    login-azurermaccount
    $sub = Get-AzureRmSubscription -Name <SubscriptionName>
    $sub | Select-AzureRmSubscription
    ```

2. <span data-ttu-id="6a9a6-217">paramètres de hello toostore, créer hello complexe variable à l’aide du nom hello hello du plan de récupération :</span><span class="sxs-lookup"><span data-stu-id="6a9a6-217">toostore hello parameters, create hello complex variable by using hello name of hello recovery plan:</span></span>

    ```
    $VMDetails = @{"VMGUID"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"};"VMGUID2"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"}}
        New-AzureRmAutomationVariable -ResourceGroupName <RG of Automation Account> -AutomationAccountName <AA Name> -Name <RecoveryPlanName> -Value $VMDetails -Encrypted $false
    ```

3. <span data-ttu-id="6a9a6-218">Dans cette variable complexe, **VMDetails** est hello ID de machine virtuelle pour hello protégé la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-218">In this complex variable, **VMDetails** is hello VM ID for hello protected VM.</span></span> <span data-ttu-id="6a9a6-219">tooget hello ID de machine virtuelle, Bonjour portail Azure, afficher les propriétés de machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-219">tooget hello VM ID, in hello Azure portal, view hello VM properties.</span></span> <span data-ttu-id="6a9a6-220">Hello capture d’écran suivante montre une variable qui stocke les détails de hello de deux machines virtuelles :</span><span class="sxs-lookup"><span data-stu-id="6a9a6-220">hello following screenshot shows a variable that stores hello details of two VMs:</span></span>

    ![Utilisez hello ID de machine virtuelle comme hello GUID](media/site-recovery-runbook-automation-new/vmguid.png)

4. <span data-ttu-id="6a9a6-222">Utilisez cette variable dans votre runbook.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-222">Use this variable in your runbook.</span></span> <span data-ttu-id="6a9a6-223">Si hello indiqué que VM GUID se trouve dans le contexte du plan de récupération hello, appliquez hello NSG sur hello machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="6a9a6-223">If hello indicated VM GUID is found in hello recovery plan context, apply hello NSG on hello VM:</span></span>

    ```
    $VMDetailsObj = Get-AutomationVariable -Name $RecoveryPlanContext.RecoveryPlanName
    ```

4. <span data-ttu-id="6a9a6-224">Dans votre runbook, parcourir les ordinateurs virtuels de hello du contexte du plan de récupération hello.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-224">In your runbook, loop through hello VMs of hello recovery plan context.</span></span> <span data-ttu-id="6a9a6-225">Vérifier l’existence de hello VM dans **$VMDetailsObj**.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-225">Check whether hello VM exists in **$VMDetailsObj**.</span></span> <span data-ttu-id="6a9a6-226">Si elle existe, accéder aux propriétés de hello Hello de variable tooapply hello groupe de sécurité réseau :</span><span class="sxs-lookup"><span data-stu-id="6a9a6-226">If it exists, access hello properties of hello variable tooapply hello NSG:</span></span>

    ```
        $VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
        $vmMap = $RecoveryPlanContext.VmMap

        foreach($VMID in $VMinfo) {
            Write-output $VMDetailsObj.value.$VMID

            if ($VMDetailsObj.value.$VMID -ne $Null) { #If hello VM exists in hello context, this will not b Null
                $VM = $vmMap.$VMID
                # Access hello properties of hello variable
                $NSGname = $VMDetailsObj.value.$VMID.'NSGName'
                $NSGRGname = $VMDetailsObj.value.$VMID.'NSGResourceGroupName'

                # Add code tooapply hello NSG properties toohello VM
            }
        }
    ```

<span data-ttu-id="6a9a6-227">Vous pouvez utiliser hello même générer un script pour les plans de récupération différent.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-227">You can use hello same script for different recovery plans.</span></span> <span data-ttu-id="6a9a6-228">Entrez des paramètres différents en stockant la valeur hello qui correspond le plan de récupération tooa dans des variables différentes.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-228">Enter different parameters by storing hello value that corresponds tooa recovery plan in different variables.</span></span>

## <a name="sample-scripts"></a><span data-ttu-id="6a9a6-229">Exemples de scripts</span><span class="sxs-lookup"><span data-stu-id="6a9a6-229">Sample scripts</span></span>

<span data-ttu-id="6a9a6-230">toodeploy exemple scripts tooyour compte Automation, cliquez sur hello **déployer tooAzure** bouton.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-230">toodeploy sample scripts tooyour Automation account, click hello **Deploy tooAzure** button.</span></span>

<span data-ttu-id="6a9a6-231">[![Déployer tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span><span class="sxs-lookup"><span data-stu-id="6a9a6-231">[![Deploy tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)</span></span>

<span data-ttu-id="6a9a6-232">Pour un autre exemple, consultez hello suivant vidéo.</span><span class="sxs-lookup"><span data-stu-id="6a9a6-232">For another example, see hello following video.</span></span> <span data-ttu-id="6a9a6-233">Il montre comment toorecover un tooAzure d’application de WordPress à deux niveaux :</span><span class="sxs-lookup"><span data-stu-id="6a9a6-233">It demonstrates how toorecover a two-tier WordPress application tooAzure:</span></span>


> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/One-click-failover-of-a-2-tier-WordPress-application-using-Azure-Site-Recovery/player]



## <a name="additional-resources"></a><span data-ttu-id="6a9a6-234">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="6a9a6-234">Additional resources</span></span>
* [<span data-ttu-id="6a9a6-235">Documentation Automation</span><span class="sxs-lookup"><span data-stu-id="6a9a6-235">Azure Automation service Run As account</span></span>](../automation/automation-sec-configure-azure-runas-account.md)
* [<span data-ttu-id="6a9a6-236">Vue d’ensemble d’Azure Automation</span><span class="sxs-lookup"><span data-stu-id="6a9a6-236">Azure Automation overview</span></span>](http://msdn.microsoft.com/library/azure/dn643629.aspx "Vue d’ensemble d’Azure Automation")
* [<span data-ttu-id="6a9a6-237">Ressources de script pour les professionnels de l'informatique</span><span class="sxs-lookup"><span data-stu-id="6a9a6-237">Azure Automation sample scripts</span></span>](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Ressources de script pour les professionnels de l'informatique")
