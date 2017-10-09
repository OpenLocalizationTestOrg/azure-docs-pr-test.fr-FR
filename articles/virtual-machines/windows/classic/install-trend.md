---
title: aaaInstall Trend Micro Deep Security sur une machine virtuelle | Documents Microsoft
description: "Cet article décrit comment tooinstall et configurer Trend Micro security sur un ordinateur virtuel créé avec le modèle de déploiement classique hello dans Azure."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: e991b635-f1e2-483f-b7ca-9d53e7c22e2a
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: iainfou
ms.openlocfilehash: dc5492db07a37a2296df5da673183a14c6d5b1f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-trend-micro-deep-security-as-a-service-on-a-windows-vm"></a><span data-ttu-id="ce43f-103">Comment tooinstall et configurer Trend Micro Deep Security en tant que Service sur une machine virtuelle Windows</span><span class="sxs-lookup"><span data-stu-id="ce43f-103">How tooinstall and configure Trend Micro Deep Security as a Service on a Windows VM</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ce43f-104">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ce43f-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ce43f-105">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="ce43f-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="ce43f-106">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="ce43f-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="ce43f-107">Cet article vous montre comment tooinstall et configurer Trend Micro Deep Security en tant que Service sur un nouveau ou existant ordinateur virtuel (VM) exécutant Windows Server.</span><span class="sxs-lookup"><span data-stu-id="ce43f-107">This article shows you how tooinstall and configure Trend Micro Deep Security as a Service on a new or existing virtual machine (VM) running Windows Server.</span></span> <span data-ttu-id="ce43f-108">Deep Security inclut une protection anti-programmes malveillants, un pare-feu, un système de prévention contre les intrusions et une surveillance de l’intégrité.</span><span class="sxs-lookup"><span data-stu-id="ce43f-108">Deep Security as a Service includes anti-malware protection, a firewall, an intrusion prevention system, and integrity monitoring.</span></span>

<span data-ttu-id="ce43f-109">client de Hello est installé comme une extension de sécurité via hello Agent de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ce43f-109">hello client is installed as a security extension via hello VM Agent.</span></span> <span data-ttu-id="ce43f-110">Sur une machine virtuelle, vous installez hello Deep Security Agent, en tant que hello Qu'agent de machine virtuelle est automatiquement créé par hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ce43f-110">On a new virtual machine, you install hello Deep Security Agent, as hello VM Agent is created automatically by hello Azure portal.</span></span>

<span data-ttu-id="ce43f-111">Une machine virtuelle existante, créée à l’aide du portail classique de hello, hello CLI d’Azure ou PowerShell n’est peut-être pas un agent de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ce43f-111">An existing VM created using hello classic portal, hello Azure CLI, or PowerShell might not have a VM agent.</span></span> <span data-ttu-id="ce43f-112">Pour un ordinateur virtuel existant qui n’a pas hello Agent de machine virtuelle, vous devez toodownload et installez en premier.</span><span class="sxs-lookup"><span data-stu-id="ce43f-112">For an existing virtual machine that doesn't have hello VM Agent, you need toodownload and install it first.</span></span> <span data-ttu-id="ce43f-113">Cet article aborde ces deux situations.</span><span class="sxs-lookup"><span data-stu-id="ce43f-113">This article covers both situations.</span></span>

<span data-ttu-id="ce43f-114">Si vous avez un abonnement en cours à partir de Trend Micro pour une solution sur site, vous pouvez l’utiliser toohelp protéger vos machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="ce43f-114">If you have a current subscription from Trend Micro for an on-premises solution, you can use it toohelp protect your Azure virtual machines.</span></span> <span data-ttu-id="ce43f-115">Si vous n’êtes pas encore client, vous pouvez vous inscrire pour une version d’évaluation.</span><span class="sxs-lookup"><span data-stu-id="ce43f-115">If you're not a customer yet, you can sign up for a trial subscription.</span></span> <span data-ttu-id="ce43f-116">Pour plus d’informations sur cette solution, consultez hello Trend Micro blog [Microsoft Azure VM Extension pour approfondie sécurité de l’Agent](http://go.microsoft.com/fwlink/p/?LinkId=403945).</span><span class="sxs-lookup"><span data-stu-id="ce43f-116">For more information about this solution, see hello Trend Micro blog post [Microsoft Azure VM Agent Extension For Deep Security](http://go.microsoft.com/fwlink/p/?LinkId=403945).</span></span>

## <a name="install-hello-deep-security-agent-on-a-new-vm"></a><span data-ttu-id="ce43f-117">Installer hello Deep Security Agent sur un nouvel ordinateur virtuel</span><span class="sxs-lookup"><span data-stu-id="ce43f-117">Install hello Deep Security Agent on a new VM</span></span>

<span data-ttu-id="ce43f-118">Hello [portail Azure](http://portal.azure.com) vous permet d’installer l’extension de sécurité Trend Micro hello lorsque vous utilisez une image à partir de hello **Marketplace** toocreate hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="ce43f-118">hello [Azure portal](http://portal.azure.com) lets you install hello Trend Micro security extension when you use an image from hello **Marketplace** toocreate hello virtual machine.</span></span> <span data-ttu-id="ce43f-119">Si vous créez une machine virtuelle unique, à l’aide du portail de hello est une protection de tooadd facilement à partir de Trend Micro.</span><span class="sxs-lookup"><span data-stu-id="ce43f-119">If you're creating a single virtual machine, using hello portal is an easy way tooadd protection from Trend Micro.</span></span>

<span data-ttu-id="ce43f-120">À l’aide d’une entrée à partir de hello **Marketplace** ouvre un Assistant qui vous permet de configurer la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="ce43f-120">Using an entry from hello **Marketplace** opens a wizard that helps you set up hello virtual machine.</span></span> <span data-ttu-id="ce43f-121">Vous utilisez hello **paramètres** panneau, panneau de configuration troisième hello d’Assistant hello, tooinstall hello extension de sécurité Trend Micro.</span><span class="sxs-lookup"><span data-stu-id="ce43f-121">You use hello **Settings** blade, hello third panel of hello wizard, tooinstall hello Trend Micro security extension.</span></span>  <span data-ttu-id="ce43f-122">Pour plus d’informations, consultez [créer une machine virtuelle exécutant Windows Bonjour Azure portal](tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="ce43f-122">For general instructions, see [Create a virtual machine running Windows in hello Azure portal](tutorial.md).</span></span>

<span data-ttu-id="ce43f-123">Si vous obtenez les toohello **paramètres** Panneau de l’Assistant de hello, procédez comme hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="ce43f-123">When you get toohello **Settings** blade of hello wizard, do hello following steps:</span></span>

1. <span data-ttu-id="ce43f-124">Cliquez sur **Extensions**, puis cliquez sur **ajouter une extension** dans le volet suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="ce43f-124">Click **Extensions**, then click **Add extension** in hello next pane.</span></span>

   ![Démarrer l’ajout de l’extension de hello][1]

2. <span data-ttu-id="ce43f-126">Sélectionnez **Deep Security Agent** Bonjour **nouvelle ressource** volet.</span><span class="sxs-lookup"><span data-stu-id="ce43f-126">Select **Deep Security Agent** in hello **New resource** pane.</span></span> <span data-ttu-id="ce43f-127">Dans le volet de Deep Security Agent hello, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="ce43f-127">In hello Deep Security Agent pane, click **Create**.</span></span>

   ![Identifier le Deep Security Agent][2]

3. <span data-ttu-id="ce43f-129">Entrez hello **identificateur du locataire** et **mot de passe d’Activation client** pour l’extension de hello.</span><span class="sxs-lookup"><span data-stu-id="ce43f-129">Enter hello **Tenant Identifier** and **Tenant Activation Password** for hello extension.</span></span> <span data-ttu-id="ce43f-130">Vous pouvez également entrer un **identificateur de stratégie de sécurité**.</span><span class="sxs-lookup"><span data-stu-id="ce43f-130">Optionally, you can enter a **Security Policy Identifier**.</span></span> <span data-ttu-id="ce43f-131">Ensuite, cliquez sur **OK** client de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="ce43f-131">Then, click **OK** tooadd hello client.</span></span>

   ![Fournir les détails de l’extension][3]

## <a name="install-hello-deep-security-agent-on-an-existing-vm"></a><span data-ttu-id="ce43f-133">Installer hello Deep Security Agent sur un ordinateur virtuel existant</span><span class="sxs-lookup"><span data-stu-id="ce43f-133">Install hello Deep Security Agent on an existing VM</span></span>
<span data-ttu-id="ce43f-134">tooinstall hello l’agent sur un ordinateur virtuel existant, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ce43f-134">tooinstall hello agent on an existing VM, you need hello following items:</span></span>

* <span data-ttu-id="ce43f-135">module d’Azure PowerShell Hello, version 0.8.2 ou plus récente, installée sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="ce43f-135">hello Azure PowerShell module, version 0.8.2 or newer, installed on your local computer.</span></span> <span data-ttu-id="ce43f-136">Vous pouvez vérifier la version de hello d’Azure PowerShell que vous avez installés à l’aide de hello **azure de Get-Module | version de format-table** commande.</span><span class="sxs-lookup"><span data-stu-id="ce43f-136">You can check hello version of Azure PowerShell that you have installed by using hello **Get-Module azure | format-table version** command.</span></span> <span data-ttu-id="ce43f-137">Pour obtenir des instructions et une version plus récente de lien toohello, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ce43f-137">For instructions and a link toohello latest version, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="ce43f-138">Ouvrez une session à l’aide d’abonnement Azure tooyour `Add-AzureAccount`.</span><span class="sxs-lookup"><span data-stu-id="ce43f-138">Log in tooyour Azure subscription using `Add-AzureAccount`.</span></span>
* <span data-ttu-id="ce43f-139">Hello Agent de machine virtuelle installé sur la machine virtuelle cible hello.</span><span class="sxs-lookup"><span data-stu-id="ce43f-139">hello VM Agent installed on hello target virtual machine.</span></span>

<span data-ttu-id="ce43f-140">Tout d’abord, vérifiez que hello Qu'agent de machine virtuelle est déjà installé.</span><span class="sxs-lookup"><span data-stu-id="ce43f-140">First, verify that hello VM Agent is already installed.</span></span> <span data-ttu-id="ce43f-141">Renseignez nom du service cloud hello et nom de machine virtuelle et exécutez hello suivant de commandes à partir d’une invite de commandes de niveau administrateur Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ce43f-141">Fill in hello cloud service name and virtual machine name, and then run hello following commands at an administrator-level Azure PowerShell command prompt.</span></span> <span data-ttu-id="ce43f-142">Remplacez tout le contenu du devis hello, y compris hello < et >.</span><span class="sxs-lookup"><span data-stu-id="ce43f-142">Replace everything within hello quotes, including hello < and > characters.</span></span>

    $CSName = "<cloud service name>"
    $VMName = "<virtual machine name>"
    $vm = Get-AzureVM -ServiceName $CSName -Name $VMName
    write-host $vm.VM.ProvisionGuestAgent

<span data-ttu-id="ce43f-143">Si vous ne connaissez pas le service cloud hello et nom d’ordinateur virtuel, exécutez **Get-AzureVM** toodisplay que les informations pour tous les hello des machines virtuelles dans votre abonnement actuel.</span><span class="sxs-lookup"><span data-stu-id="ce43f-143">If you don't know hello cloud service and virtual machine name, run **Get-AzureVM** toodisplay that information for all hello virtual machines in your current subscription.</span></span>

<span data-ttu-id="ce43f-144">Si hello **écriture-host** commande **True**, hello l’Agent VM est installé.</span><span class="sxs-lookup"><span data-stu-id="ce43f-144">If hello **write-host** command returns **True**, hello VM Agent is installed.</span></span> <span data-ttu-id="ce43f-145">Si elle retourne **False**, consultez les instructions hello et un toohello lien Télécharger Bonjour billet de blog Azure [Agent de machine virtuelle et Extensions - partie 2](http://go.microsoft.com/fwlink/p/?LinkId=403947).</span><span class="sxs-lookup"><span data-stu-id="ce43f-145">If it returns **False**, see hello instructions and a link toohello download in hello Azure blog post [VM Agent and Extensions - Part 2](http://go.microsoft.com/fwlink/p/?LinkId=403947).</span></span>

<span data-ttu-id="ce43f-146">Si hello Agent de machine virtuelle est installé, exécutez ces commandes.</span><span class="sxs-lookup"><span data-stu-id="ce43f-146">If hello VM Agent is installed, run these commands.</span></span>

    $Agent = Get-AzureVMAvailableExtension TrendMicro.DeepSecurity -ExtensionName TrendMicroDSA

    Set-AzureVMExtension -Publisher TrendMicro.DeepSecurity –Version $Agent.Version -ExtensionName TrendMicroDSA -VM $vm | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="ce43f-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ce43f-147">Next steps</span></span>
<span data-ttu-id="ce43f-148">Il prend quelques minutes pour hello toostart de l’agent en cours d’exécution lorsqu’il est installé.</span><span class="sxs-lookup"><span data-stu-id="ce43f-148">It takes a few minutes for hello agent toostart running when it is installed.</span></span> <span data-ttu-id="ce43f-149">Après cela, vous devez tooactivate Deep Security sur l’ordinateur virtuel de hello afin qu’il puisse être gérée par un gestionnaire de sécurité approfondie.</span><span class="sxs-lookup"><span data-stu-id="ce43f-149">After that, you need tooactivate Deep Security on hello virtual machine so it can be managed by a Deep Security Manager.</span></span> <span data-ttu-id="ce43f-150">Hello suivant des articles pour en savoir plus, consultez :</span><span class="sxs-lookup"><span data-stu-id="ce43f-150">See hello following articles for additional instructions:</span></span>

* <span data-ttu-id="ce43f-151">L’article de Trend sur cette solution, [Sécurité cloud instantanée pour Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=404101)</span><span class="sxs-lookup"><span data-stu-id="ce43f-151">Trend's article about this solution, [Instant-On Cloud Security for Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=404101)</span></span>
* <span data-ttu-id="ce43f-152">A [exemple de script Windows PowerShell](http://go.microsoft.com/fwlink/?LinkId=404100) tooconfigure hello virtual machine</span><span class="sxs-lookup"><span data-stu-id="ce43f-152">A [sample Windows PowerShell script](http://go.microsoft.com/fwlink/?LinkId=404100) tooconfigure hello virtual machine</span></span>
* <span data-ttu-id="ce43f-153">[Instructions](http://go.microsoft.com/fwlink/?LinkId=404099) pour l’exemple hello</span><span class="sxs-lookup"><span data-stu-id="ce43f-153">[Instructions](http://go.microsoft.com/fwlink/?LinkId=404099) for hello sample</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ce43f-154">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="ce43f-154">Additional resources</span></span>
<span data-ttu-id="ce43f-155">[Comment toolog sur l’ordinateur virtuel de tooa exécutant Windows Server]</span><span class="sxs-lookup"><span data-stu-id="ce43f-155">[How toolog on tooa virtual machine running Windows Server]</span></span>

<span data-ttu-id="ce43f-156">[Fonctionnalités et extensions de machine virtuelle Azure]</span><span class="sxs-lookup"><span data-stu-id="ce43f-156">[Azure VM Extensions and features]</span></span>

<!-- Image references -->
[1]: ./media/install-trend/new_vm_Blade3.png
[2]: ./media/install-trend/find_SecurityAgent.png
[3]: ./media/install-trend/SecurityAgentDetails.png

<!-- Link references -->
[Comment toolog sur l’ordinateur virtuel de tooa exécutant Windows Server]:connect-logon.md
[Fonctionnalités et extensions de machine virtuelle Azure]: http://go.microsoft.com/fwlink/p/?linkid=390493&clcid=0x409
