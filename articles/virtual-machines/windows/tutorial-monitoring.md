---
title: aaaAzure analyse et les Machines virtuelles Windows | Documents Microsoft
description: Didacticiel - Surveiller une machine virtuelle Windows avec Azure PowerShell
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/04/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 191dc5a30d41c25a9e38f8ec2a32efdc05e03015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-windows-virtual-machine-with-azure-powershell"></a><span data-ttu-id="30703-103">Surveiller une machine virtuelle Windows avec Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="30703-103">Monitor a Windows Virtual Machine with Azure PowerShell</span></span>

<span data-ttu-id="30703-104">Surveillance Azure utilise des agents de démarrage de toocollect et les données de performances à partir de machines virtuelles Azure, stocker ces données dans le stockage Azure et le rendre accessible via le portail, module Azure PowerShell de hello et hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="30703-104">Azure monitoring uses agents toocollect boot and performance data from Azure VMs, store this data in Azure storage, and make it accessible through portal, hello Azure PowerShell module, and hello Azure CLI.</span></span> <span data-ttu-id="30703-105">Ce didacticiel vous montre comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="30703-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="30703-106">Activer les diagnostics de démarrage sur une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="30703-106">Enable boot diagnostics on a VM</span></span>
> * <span data-ttu-id="30703-107">Afficher les diagnostics de démarrage</span><span class="sxs-lookup"><span data-stu-id="30703-107">View boot diagnostics</span></span>
> * <span data-ttu-id="30703-108">Afficher les métriques de l’hôte de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="30703-108">View VM host metrics</span></span>
> * <span data-ttu-id="30703-109">Installer l’extension de diagnostics hello</span><span class="sxs-lookup"><span data-stu-id="30703-109">Install hello diagnostics extension</span></span>
> * <span data-ttu-id="30703-110">Afficher les métriques de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="30703-110">View VM metrics</span></span>
> * <span data-ttu-id="30703-111">Créer une alerte</span><span class="sxs-lookup"><span data-stu-id="30703-111">Create an alert</span></span>
> * <span data-ttu-id="30703-112">Configurer la surveillance avancée</span><span class="sxs-lookup"><span data-stu-id="30703-112">Set up advanced monitoring</span></span>

<span data-ttu-id="30703-113">Ce didacticiel nécessite hello Azure PowerShell version 3.6 ou version ultérieure du module.</span><span class="sxs-lookup"><span data-stu-id="30703-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="30703-114">Exécutez ` Get-Module -ListAvailable AzureRM` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="30703-114">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="30703-115">Si vous avez besoin de tooupgrade, consultez [installez Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="30703-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

<span data-ttu-id="30703-116">exemple de hello toocomplete dans ce didacticiel, vous devez disposer d’un ordinateur virtuel existant.</span><span class="sxs-lookup"><span data-stu-id="30703-116">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="30703-117">Si nécessaire, cet [exemple de script](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) peut en créer une pour vous.</span><span class="sxs-lookup"><span data-stu-id="30703-117">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="30703-118">Lors de l’utilisation de didacticiel de hello, remplacez le groupe de ressources hello, nom de la machine virtuelle et l’emplacement si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="30703-118">When working through hello tutorial, replace hello resource group, VM name, and location where needed.</span></span>

## <a name="view-boot-diagnostics"></a><span data-ttu-id="30703-119">Afficher les diagnostics de démarrage</span><span class="sxs-lookup"><span data-stu-id="30703-119">View boot diagnostics</span></span>

<span data-ttu-id="30703-120">Comme les machines virtuelles Windows démarre, agent de Diagnostics de démarrage hello capture de texte qui peut être utilisé pour la résolution des problèmes d’objectif.</span><span class="sxs-lookup"><span data-stu-id="30703-120">As Windows virtual machines boot up, hello boot diagnostic agent captures screen output that can be used for troubleshooting purpose.</span></span> <span data-ttu-id="30703-121">Cette fonctionnalité est activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="30703-121">This capability is enabled by default.</span></span> <span data-ttu-id="30703-122">Hello capturées écran captures sont stockés dans un compte de stockage Azure, qui est également créé par défaut.</span><span class="sxs-lookup"><span data-stu-id="30703-122">hello captured screen shots are stored in an Azure storage account, which is also created by default.</span></span> 

<span data-ttu-id="30703-123">Vous pouvez obtenir des données de diagnostic de démarrage hello avec hello [Get-AzureRmVMBootDiagnosticsData](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmbootdiagnosticsdata) commande.</span><span class="sxs-lookup"><span data-stu-id="30703-123">You can get hello boot diagnostic data with hello [Get-AzureRmVMBootDiagnosticsData](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmbootdiagnosticsdata) command.</span></span> <span data-ttu-id="30703-124">Bonjour l’exemple suivant, les diagnostics de démarrage sont téléchargés toohello racine hello * c:\* lecteur.</span><span class="sxs-lookup"><span data-stu-id="30703-124">In hello following example, boot diagnostics are downloaded toohello root of hello *c:\* drive.</span></span> 

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup -Name myVM -Windows -LocalPath "c:\"
```

## <a name="view-host-metrics"></a><span data-ttu-id="30703-125">Afficher les métriques de l’hôte</span><span class="sxs-lookup"><span data-stu-id="30703-125">View host metrics</span></span>

<span data-ttu-id="30703-126">Une machine virtuelle Windows possède une machine virtuelle hôte dédiée dans Azure, avec qui elle interagit.</span><span class="sxs-lookup"><span data-stu-id="30703-126">A Windows VM has a dedicated Host VM in Azure that it interacts with.</span></span> <span data-ttu-id="30703-127">Métriques sont automatiquement collectées pour hello hôte et peuvent être consultées dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="30703-127">Metrics are automatically collected for hello Host and can be viewed in hello Azure portal.</span></span>

1. <span data-ttu-id="30703-128">Bonjour portail Azure, cliquez sur **groupes de ressources**, sélectionnez **myResourceGroup**, puis sélectionnez **myVM** dans la liste des ressources hello.</span><span class="sxs-lookup"><span data-stu-id="30703-128">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="30703-129">Cliquez sur **métriques** sur hello Panneau de machine virtuelle, puis sélectionnez une des métriques d’hôte hello sous **métriques disponibles** toosee fonctionne hello machine virtuelle d’hôte.</span><span class="sxs-lookup"><span data-stu-id="30703-129">Click **Metrics** on hello VM blade, and then select any of hello Host metrics under **Available metrics** toosee how hello Host VM is performing.</span></span>

    ![Afficher les métriques de l’hôte](./media/tutorial-monitoring/tutorial-monitor-host-metrics.png)

## <a name="install-diagnostics-extension"></a><span data-ttu-id="30703-131">Installer l’extension Diagnostics</span><span class="sxs-lookup"><span data-stu-id="30703-131">Install diagnostics extension</span></span>

<span data-ttu-id="30703-132">métriques de base hôte Hello sont disponibles, mais toosee plus précis et des mesures spécifiques à la machine virtuelle, vous tooneed tooinstall hello extension Azure diagnostics sur hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="30703-132">hello basic host metrics are available, but toosee more granular and VM-specific metrics, you tooneed tooinstall hello Azure diagnostics extension on hello VM.</span></span> <span data-ttu-id="30703-133">Hello extension Azure diagnostics permet une analyse supplémentaire et diagnostics toobe de données récupérées à partir de la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="30703-133">hello Azure diagnostics extension allows additional monitoring and diagnostics data toobe retrieved from hello VM.</span></span> <span data-ttu-id="30703-134">Vous pouvez afficher ces métriques de performances et créer des alertes basées sur le fonctionnement de hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="30703-134">You can view these performance metrics and create alerts based on how hello VM performs.</span></span> <span data-ttu-id="30703-135">extension de diagnostic Hello est installée via hello portail Azure comme suit :</span><span class="sxs-lookup"><span data-stu-id="30703-135">hello diagnostic extension is installed through hello Azure portal as follows:</span></span>

1. <span data-ttu-id="30703-136">Bonjour portail Azure, cliquez sur **groupes de ressources**, sélectionnez **myResourceGroup**, puis sélectionnez **myVM** dans la liste des ressources hello.</span><span class="sxs-lookup"><span data-stu-id="30703-136">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="30703-137">Cliquez sur **Paramètres de diagnostic**.</span><span class="sxs-lookup"><span data-stu-id="30703-137">Click **Diagnosis settings**.</span></span> <span data-ttu-id="30703-138">liste de Hello montre que *diagnostics de démarrage* sont déjà activés à partir de la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="30703-138">hello list shows that *Boot diagnostics* are already enabled from hello previous section.</span></span> <span data-ttu-id="30703-139">Cliquez sur la case à cocher pour hello *les audits de base*.</span><span class="sxs-lookup"><span data-stu-id="30703-139">Click hello check box for *Basic metrics*.</span></span>
3. <span data-ttu-id="30703-140">Cliquez sur hello **activer l’analyse au niveau invité** bouton.</span><span class="sxs-lookup"><span data-stu-id="30703-140">Click hello **Enable guest-level monitoring** button.</span></span>

    ![Afficher les métriques de diagnostic](./media/tutorial-monitoring/enable-diagnostics-extension.png)

## <a name="view-vm-metrics"></a><span data-ttu-id="30703-142">Afficher les métriques de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="30703-142">View VM metrics</span></span>

<span data-ttu-id="30703-143">Vous pouvez afficher les métriques de machine virtuelle hello Bonjour même façon que vous avez affiché les métriques de machine virtuelle hôte hello :</span><span class="sxs-lookup"><span data-stu-id="30703-143">You can view hello VM metrics in hello same way that you viewed hello host VM metrics:</span></span>

1. <span data-ttu-id="30703-144">Bonjour portail Azure, cliquez sur **groupes de ressources**, sélectionnez **myResourceGroup**, puis sélectionnez **myVM** dans la liste des ressources hello.</span><span class="sxs-lookup"><span data-stu-id="30703-144">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="30703-145">toosee effectue hello machine virtuelle, cliquez sur **métriques** sur hello Panneau de machine virtuelle, puis sélectionnez une des métriques de diagnostic hello sous **métriques disponibles**.</span><span class="sxs-lookup"><span data-stu-id="30703-145">toosee how hello VM is performing, click **Metrics** on hello VM blade, and then select any of hello diagnostics metrics under **Available metrics**.</span></span>

    ![Afficher les métriques de la machine virtuelle](./media/tutorial-monitoring/monitor-vm-metrics.png)

## <a name="create-alerts"></a><span data-ttu-id="30703-147">Créez des alertes</span><span class="sxs-lookup"><span data-stu-id="30703-147">Create alerts</span></span>

<span data-ttu-id="30703-148">Vous pouvez créer des alertes en fonction de métriques de performances spécifiques.</span><span class="sxs-lookup"><span data-stu-id="30703-148">You can create alerts based on specific performance metrics.</span></span> <span data-ttu-id="30703-149">Les alertes peuvent être utilisé toonotify vous lors de l’utilisation moyenne du processeur dépasse un seuil ou une espace disque disponible devient inférieur à un certain montant, par exemple.</span><span class="sxs-lookup"><span data-stu-id="30703-149">Alerts can be used toonotify you when average CPU usage exceeds a certain threshold or available free disk space drops below a certain amount, for example.</span></span> <span data-ttu-id="30703-150">Les alertes sont affichent dans hello portail Azure ou peuvent être envoyés par courrier électronique.</span><span class="sxs-lookup"><span data-stu-id="30703-150">Alerts are displayed in hello Azure portal or can be sent via email.</span></span> <span data-ttu-id="30703-151">Vous pouvez également déclencher des runbooks Azure Automation ou Azure Logic Apps dans tooalerts de réponse en cours de génération.</span><span class="sxs-lookup"><span data-stu-id="30703-151">You can also trigger Azure Automation runbooks or Azure Logic Apps in response tooalerts being generated.</span></span>

<span data-ttu-id="30703-152">Hello exemple suivant crée une alerte pour l’utilisation moyenne du processeur.</span><span class="sxs-lookup"><span data-stu-id="30703-152">hello following example creates an alert for average CPU usage.</span></span>

1. <span data-ttu-id="30703-153">Bonjour portail Azure, cliquez sur **groupes de ressources**, sélectionnez **myResourceGroup**, puis sélectionnez **myVM** dans la liste des ressources hello.</span><span class="sxs-lookup"><span data-stu-id="30703-153">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="30703-154">Cliquez sur **règles d’alerte** sur le panneau de la machine virtuelle hello, puis cliquez sur **ajouter une alerte métrique** haut hello du panneau des alertes hello.</span><span class="sxs-lookup"><span data-stu-id="30703-154">Click **Alert rules** on hello VM blade, then click **Add metric alert** across hello top of hello alerts blade.</span></span>
4. <span data-ttu-id="30703-155">Spécifiez un **Nom** pour votre alerte, comme *myAlertRule*</span><span class="sxs-lookup"><span data-stu-id="30703-155">Provide a **Name** for your alert, such as *myAlertRule*</span></span>
5. <span data-ttu-id="30703-156">tootrigger une alerte lorsque le pourcentage de l’UC dépasse 1.0 pendant cinq minutes, laissez hello toutes les autres valeurs par défaut sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="30703-156">tootrigger an alert when CPU percentage exceeds 1.0 for five minutes, leave all hello other defaults selected.</span></span>
6. <span data-ttu-id="30703-157">Si vous le souhaitez, case hello pour *propriétaires, collaborateurs et les lecteurs de messagerie* toosend la notification par e-mail.</span><span class="sxs-lookup"><span data-stu-id="30703-157">Optionally, check hello box for *Email owners, contributors, and readers* toosend email notification.</span></span> <span data-ttu-id="30703-158">action par défaut de Hello est toopresent une notification dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="30703-158">hello default action is toopresent a notification in hello portal.</span></span>
7. <span data-ttu-id="30703-159">Cliquez sur hello **OK** bouton.</span><span class="sxs-lookup"><span data-stu-id="30703-159">Click hello **OK** button.</span></span>

## <a name="advanced-monitoring"></a><span data-ttu-id="30703-160">Surveillance avancée</span><span class="sxs-lookup"><span data-stu-id="30703-160">Advanced monitoring</span></span> 

<span data-ttu-id="30703-161">Vous pouvez faire une surveillance plus avancée de votre machine virtuelle en utilisant [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span><span class="sxs-lookup"><span data-stu-id="30703-161">You can do more advanced monitoring of your VM by using [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span></span> <span data-ttu-id="30703-162">Si vous ne l’avez pas déjà fait, vous pouvez vous inscrire pour une [version d’évaluation gratuite](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) d’Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="30703-162">If you haven't already done so, you can sign up for a [free trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) of Operations Management Suite.</span></span>

<span data-ttu-id="30703-163">Lorsque vous avez accès toohello OMS portail, vous pouvez trouver l’identificateur de clé et l’espace de travail du espace de travail hello sur le panneau des paramètres hello.</span><span class="sxs-lookup"><span data-stu-id="30703-163">When you have access toohello OMS portal, you can find hello workspace key and workspace identifier on hello Settings blade.</span></span> <span data-ttu-id="30703-164">Hello d’utilisation [Set-AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) commande tootooadd hello OMS extension toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="30703-164">Use hello [Set-AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) cmmand tootooadd hello OMS extension toohello VM.</span></span> <span data-ttu-id="30703-165">Mise à jour hello valeurs Bonjour ci-dessous exemple tooreflect vous clé d’espace de travail OMS et l’ID de l’espace de travail</span><span class="sxs-lookup"><span data-stu-id="30703-165">Update hello variable values in hello below sample tooreflect you OMS workspace key and workspace Id.</span></span>  

```powershell
$omsId = "<Replace with your OMS Id>"
$omsKey = "<Replace with your OMS key>"

Set-AzureRmVMExtension -ResourceGroupName myResourceGroup `
  -ExtensionName "Microsoft.EnterpriseCloud.Monitoring" `
  -VMName myVM `
  -Publisher "Microsoft.EnterpriseCloud.Monitoring" `
  -ExtensionType "MicrosoftMonitoringAgent" `
  -TypeHandlerVersion 1.0 `
  -Settings @{"workspaceId" = $omsId} `
  -ProtectedSettings @{"workspaceKey" = $omsKey} `
  -Location eastus
```

<span data-ttu-id="30703-166">Après quelques minutes, vous devez voir hello nouvelle machine virtuelle dans l’espace de travail OMS hello.</span><span class="sxs-lookup"><span data-stu-id="30703-166">After a few minutes, you should see hello new VM in hello OMS workspace.</span></span> 

![Panneau OMS](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a><span data-ttu-id="30703-168">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="30703-168">Next steps</span></span>
<span data-ttu-id="30703-169">Dans ce didacticiel, vous avez configuré et examiné des machines virtuelles avec Azure Security Center.</span><span class="sxs-lookup"><span data-stu-id="30703-169">In this tutorial, you configured and reviewed VMs with Azure Security Center.</span></span> <span data-ttu-id="30703-170">Vous avez appris à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="30703-170">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="30703-171">Créez un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="30703-171">Create a virtual network</span></span>
> * <span data-ttu-id="30703-172">Créer un groupe de ressources et une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="30703-172">Create a resource group and VM</span></span> 
> * <span data-ttu-id="30703-173">Activer les diagnostics de démarrage sur hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="30703-173">Enable boot diagnostics on hello VM</span></span>
> * <span data-ttu-id="30703-174">Afficher les diagnostics de démarrage</span><span class="sxs-lookup"><span data-stu-id="30703-174">View boot diagnostics</span></span>
> * <span data-ttu-id="30703-175">Afficher les métriques de l’hôte</span><span class="sxs-lookup"><span data-stu-id="30703-175">View host metrics</span></span>
> * <span data-ttu-id="30703-176">Installer l’extension de diagnostics hello</span><span class="sxs-lookup"><span data-stu-id="30703-176">Install hello diagnostics extension</span></span>
> * <span data-ttu-id="30703-177">Afficher les métriques de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="30703-177">View VM metrics</span></span>
> * <span data-ttu-id="30703-178">Créer une alerte</span><span class="sxs-lookup"><span data-stu-id="30703-178">Create an alert</span></span>
> * <span data-ttu-id="30703-179">Configurer la surveillance avancée</span><span class="sxs-lookup"><span data-stu-id="30703-179">Set up advanced monitoring</span></span>

<span data-ttu-id="30703-180">Avance toohello toolearn de didacticiel suivant sur le centre de sécurité Azure.</span><span class="sxs-lookup"><span data-stu-id="30703-180">Advance toohello next tutorial toolearn about Azure security center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="30703-181">Gérer la sécurité des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="30703-181">Manage VM security</span></span>](./tutorial-azure-security.md)