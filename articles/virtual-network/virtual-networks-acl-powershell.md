---
title: "listes de contrôle d’accès de point de terminaison Azure d’aaaManage | PowerShell | Classique | Documents Microsoft"
description: "Découvrez comment toomanage ACL avec PowerShell"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: c84e40af-f351-4572-b3f0-d572d46bafe7
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: a7ca241ea108a266085bfb689b742d781e58da1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-endpoint-access-control-lists-using-powershell-in-hello-classic-deployment-model"></a><span data-ttu-id="41f7c-103">Gérer les listes de contrôle d’accès de point de terminaison à l’aide de PowerShell dans le modèle de déploiement classique de hello</span><span class="sxs-lookup"><span data-stu-id="41f7c-103">Manage endpoint access control lists using PowerShell in hello classic deployment model</span></span>
<span data-ttu-id="41f7c-104">Vous pouvez créer et gérer des listes de contrôle d’accès réseau (ACL) pour les points de terminaison à l’aide d’Azure PowerShell ou dans le portail de gestion de hello.</span><span class="sxs-lookup"><span data-stu-id="41f7c-104">You can create and manage Network Access Control Lists (ACLs) for endpoints by using Azure PowerShell or in hello Management Portal.</span></span> <span data-ttu-id="41f7c-105">Dans cette rubrique, vous trouverez des procédures pour les tâches courantes des listes de contrôle d’accès que vous pouvez effectuer à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="41f7c-105">In this topic, you'll find procedures for ACL common tasks that you can complete using PowerShell.</span></span> <span data-ttu-id="41f7c-106">Pour la liste d’Azure PowerShell hello applets de commande consultez [applets de commande Azure Management](http://go.microsoft.com/fwlink/?LinkId=317721).</span><span class="sxs-lookup"><span data-stu-id="41f7c-106">For hello list of Azure PowerShell cmdlets see [Azure Management Cmdlets](http://go.microsoft.com/fwlink/?LinkId=317721).</span></span> <span data-ttu-id="41f7c-107">Pour plus d’informations sur les listes de contrôle d’accès, consultez [Qu’est-ce qu’une liste de contrôle d’accès (ACL) réseau ?](virtual-networks-acl.md).</span><span class="sxs-lookup"><span data-stu-id="41f7c-107">For more information about ACLs, see [What is a Network Access Control List (ACL)?](virtual-networks-acl.md).</span></span> <span data-ttu-id="41f7c-108">Si vous souhaitez toomanage vos ACL à l’aide du portail de gestion de hello, consultez [comment tooSet des points de terminaison tooa Machine virtuelle](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="41f7c-108">If you want toomanage your ACLs by using hello Management Portal, see [How tooSet Up Endpoints tooa Virtual Machine](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="manage-network-acls-by-using-azure-powershell"></a><span data-ttu-id="41f7c-109">Gérer les listes de contrôle d’accès réseau à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="41f7c-109">Manage Network ACLs by using Azure PowerShell</span></span>
<span data-ttu-id="41f7c-110">Vous pouvez utiliser toocreate d’applets de commande Azure PowerShell, supprimer et configurer (set) listes de contrôle d’accès réseau (ACL).</span><span class="sxs-lookup"><span data-stu-id="41f7c-110">You can use Azure PowerShell cmdlets toocreate, remove, and configure (set) Network Access Control Lists (ACLs).</span></span> <span data-ttu-id="41f7c-111">Nous avons inclus quelques exemples de certaines façons hello que vous pouvez configurer une liste ACL à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="41f7c-111">We've included a few examples of some of hello ways you can configure an ACL using PowerShell.</span></span>

<span data-ttu-id="41f7c-112">tooretrieve une liste complète des applets de commande PowerShell de l’ACL de hello, vous pouvez utiliser de hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="41f7c-112">tooretrieve a complete list of hello ACL PowerShell cmdlets, you can use either of hello following:</span></span>

    Get-Help *AzureACL*
    Get-Command -Noun AzureACLConfig

### <a name="create-a-network-acl-with-rules-that-permit-access-from-a-remote-subnet"></a><span data-ttu-id="41f7c-113">Créer une liste de contrôle d’accès réseau avec des règles qui autorisent l’accès à un sous-réseau distant</span><span class="sxs-lookup"><span data-stu-id="41f7c-113">Create a Network ACL with rules that permit access from a remote subnet</span></span>
<span data-ttu-id="41f7c-114">exemple Hello ci-dessous illustre un toocreate de façon une ACL contient des règles.</span><span class="sxs-lookup"><span data-stu-id="41f7c-114">hello example below illustrates a way toocreate a new ACL that contains rules.</span></span> <span data-ttu-id="41f7c-115">Cette liste ACL est ensuite appliquée tooa point de terminaison de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="41f7c-115">This ACL is then applied tooa virtual machine endpoint.</span></span> <span data-ttu-id="41f7c-116">listes de contrôle Hello dans l’exemple hello ci-dessous permettront l’accès à un sous-réseau distant.</span><span class="sxs-lookup"><span data-stu-id="41f7c-116">hello ACL rules in hello example below will allow access from a remote subnet.</span></span> <span data-ttu-id="41f7c-117">toocreate une ACL réseau avec les règles d’autorisation pour un sous-réseau distant, ouvrez Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="41f7c-117">toocreate a new Network ACL with permit rules for a remote subnet, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="41f7c-118">Copiez et collez le script hello ci-dessous, configurez le script de hello avec vos propres valeurs et puis exécutez le script de hello.</span><span class="sxs-lookup"><span data-stu-id="41f7c-118">Copy and paste hello script below, configuring hello script with your own values, and then run hello script.</span></span>

1. <span data-ttu-id="41f7c-119">Créer un nouvel objet de liste ACL réseau hello.</span><span class="sxs-lookup"><span data-stu-id="41f7c-119">Create hello new network ACL object.</span></span>
   
        $acl1 = New-AzureAclConfig
2. <span data-ttu-id="41f7c-120">Définissez une règle qui autorise l’accès depuis un sous-réseau distant.</span><span class="sxs-lookup"><span data-stu-id="41f7c-120">Set a rule that permits access from a remote subnet.</span></span> <span data-ttu-id="41f7c-121">Dans l’exemple hello ci-dessous, vous définissez la règle *100* (qui est prioritaire sur la règle 200 et versions ultérieures) sous-réseau distant de hello tooallow *10.0.0.0/8* accéder au point de terminaison de machine virtuelle toohello.</span><span class="sxs-lookup"><span data-stu-id="41f7c-121">In hello example below, you set rule *100* (which has priority over rule 200 and higher) tooallow hello remote subnet *10.0.0.0/8* access toohello virtual machine endpoint.</span></span> <span data-ttu-id="41f7c-122">Remplacez les valeurs hello par vos propres exigences de configuration.</span><span class="sxs-lookup"><span data-stu-id="41f7c-122">Replace hello values with your own configuration requirements.</span></span> <span data-ttu-id="41f7c-123">nom de Hello « SharePoint ACL config » doit être remplacé par nom convivial de hello que vous souhaitez toocall cette règle.</span><span class="sxs-lookup"><span data-stu-id="41f7c-123">hello name "SharePoint ACL config" should be replaced with hello friendly name that you want toocall this rule.</span></span>
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "SharePoint ACL config"
3. <span data-ttu-id="41f7c-124">Pour les règles supplémentaires, répétez l’applet de commande hello, en remplaçant les valeurs hello avec vos propres exigences de configuration.</span><span class="sxs-lookup"><span data-stu-id="41f7c-124">For additional rules, repeat hello cmdlet, replacing hello values with your own configuration requirements.</span></span> <span data-ttu-id="41f7c-125">Être vraiment toochange hello règle numéro tooreflect hello commande dans lequel vous souhaitez hello règles toobe est appliqué.</span><span class="sxs-lookup"><span data-stu-id="41f7c-125">Be sure toochange hello rule number Order tooreflect hello order in which you want hello rules toobe applied.</span></span> <span data-ttu-id="41f7c-126">nombre le moins élevé Hello est prioritaire sur nombre plus élevé de hello.</span><span class="sxs-lookup"><span data-stu-id="41f7c-126">hello lower rule number takes precedence over hello higher number.</span></span>
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
4. <span data-ttu-id="41f7c-127">Ensuite, vous pouvez créer un nouveau point de terminaison (Add) ou définir hello ACL pour un point de terminaison existant (Set).</span><span class="sxs-lookup"><span data-stu-id="41f7c-127">Next, you can either create a new endpoint (Add) or set hello ACL for an existing endpoint (Set).</span></span> <span data-ttu-id="41f7c-128">Dans cet exemple, nous allons ajouter qu'un nouveau point de terminaison de machine virtuelle appelé « web » et la mise à jour de terminaison de machine virtuelle hello avec hello paramètres ACL.</span><span class="sxs-lookup"><span data-stu-id="41f7c-128">In this example, we will add a new virtual machine endpoint called "web" and update hello virtual machine endpoint with hello ACL settings.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        | Update-AzureVM
5. <span data-ttu-id="41f7c-129">Ensuite, combinez les applets de commande hello et exécuter le script de hello.</span><span class="sxs-lookup"><span data-stu-id="41f7c-129">Next, combine hello cmdlets and run hello script.</span></span> <span data-ttu-id="41f7c-130">Pour cet exemple, hello combiné des applets de commande ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="41f7c-130">For this example, hello combined cmdlets would look like this:</span></span>
   
        $acl1 = New-AzureAclConfig
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "Sharepoint ACL config"
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        |Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        |Update-AzureVM

### <a name="remove-a-network-acl-rule-that-permits-access-from-a-remote-subnet"></a><span data-ttu-id="41f7c-131">Supprimer une règle de liste de contrôle d’accès réseau qui autorise l’accès depuis un sous-réseau distant</span><span class="sxs-lookup"><span data-stu-id="41f7c-131">Remove a Network ACL rule that permits access from a remote subnet</span></span>
<span data-ttu-id="41f7c-132">exemple Hello ci-dessous illustre une façon de tooremove une règle de liste ACL réseau.</span><span class="sxs-lookup"><span data-stu-id="41f7c-132">hello example below illustrates a way tooremove a network ACL rule.</span></span>  <span data-ttu-id="41f7c-133">règles de tooremove une règle ACL réseau avec une autorisation pour un sous-réseau distant, ouvrez Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="41f7c-133">tooremove a Network ACL rule with permit rules for a remote subnet, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="41f7c-134">Copiez et collez le script hello ci-dessous, configurez le script de hello avec vos propres valeurs et puis exécutez le script de hello.</span><span class="sxs-lookup"><span data-stu-id="41f7c-134">Copy and paste hello script below, configuring hello script with your own values, and then run hello script.</span></span>

1. <span data-ttu-id="41f7c-135">Première étape est tooget hello ACL réseau objet point de terminaison de machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="41f7c-135">First step is tooget hello Network ACL object for hello virtual machine endpoint.</span></span> <span data-ttu-id="41f7c-136">Vous devez ensuite supprimer règle hello.</span><span class="sxs-lookup"><span data-stu-id="41f7c-136">You'll then remove hello ACL rule.</span></span> <span data-ttu-id="41f7c-137">Dans ce cas, nous la supprimons par son ID de règle.</span><span class="sxs-lookup"><span data-stu-id="41f7c-137">In this case, we are removing it by rule ID.</span></span> <span data-ttu-id="41f7c-138">Cela supprime uniquement les ID de règle hello 0 à partir de la liste ACL de hello.</span><span class="sxs-lookup"><span data-stu-id="41f7c-138">This will only remove hello rule ID 0 from hello ACL.</span></span> <span data-ttu-id="41f7c-139">Elle ne supprime pas l’objet de liste ACL hello à partir du point de terminaison de machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="41f7c-139">It does not remove hello ACL object from hello virtual machine endpoint.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Get-AzureAclConfig –EndpointName "web" `
        | Set-AzureAclConfig –RemoveRule –ID 0 –ACL $acl1
2. <span data-ttu-id="41f7c-140">Ensuite, vous devez appliquer le point de terminaison de machine virtuelle hello ACL réseau objet toohello et mettre à jour de la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="41f7c-140">Next, you must apply hello Network ACL object toohello virtual machine endpoint and update hello virtual machine.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Set-AzureEndpoint –ACL $acl1 –Name "web" `
        | Update-AzureVM

### <a name="remove-a-network-acl-from-a-virtual-machine-endpoint"></a><span data-ttu-id="41f7c-141">Supprimer une liste de contrôle d’accès réseau d’un point de terminaison de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="41f7c-141">Remove a Network ACL from a virtual machine endpoint</span></span>
<span data-ttu-id="41f7c-142">Dans certains scénarios, vous pourriez tooremove un objet ACL réseau à partir d’un point de terminaison de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="41f7c-142">In certain scenarios, you might want tooremove a Network ACL object from a virtual machine endpoint.</span></span> <span data-ttu-id="41f7c-143">toodo qui, ouvrez Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="41f7c-143">toodo that, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="41f7c-144">Copiez et collez le script hello ci-dessous, configurez le script de hello avec vos propres valeurs et puis exécutez le script de hello.</span><span class="sxs-lookup"><span data-stu-id="41f7c-144">Copy and paste hello script below, configuring hello script with your own values, and then run hello script.</span></span>

        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Remove-AzureAclConfig –EndpointName "web" `
        | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="41f7c-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="41f7c-145">Next steps</span></span>
[<span data-ttu-id="41f7c-146">Qu’est-ce qu’une liste de contrôle d’accès (ACL) réseau ?</span><span class="sxs-lookup"><span data-stu-id="41f7c-146">What is a Network Access Control List (ACL)?</span></span>](virtual-networks-acl.md)

