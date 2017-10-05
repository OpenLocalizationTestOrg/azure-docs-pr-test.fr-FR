---
title: "Gérer les listes de contrôle d’accès de point de terminaison Azure | PowerShell | Classique | Microsoft Docs"
description: En savoir plus sur la gestion des listes ACL avec PowerShell
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
ms.openlocfilehash: c3476908447380ccd7e8b9c0f1c2a55ae763cc1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-endpoint-access-control-lists-using-powershell-in-the-classic-deployment-model"></a><span data-ttu-id="572e5-103">Gérer les listes de contrôle d’accès de point de terminaison en utilisant PowerShell dans le modèle de déploiement classique</span><span class="sxs-lookup"><span data-stu-id="572e5-103">Manage endpoint access control lists using PowerShell in the classic deployment model</span></span>
<span data-ttu-id="572e5-104">Vous pouvez créer et gérer des listes de contrôle d’accès réseau pour les points de terminaison à l’aide d’Azure PowerShell ou du portail de gestion.</span><span class="sxs-lookup"><span data-stu-id="572e5-104">You can create and manage Network Access Control Lists (ACLs) for endpoints by using Azure PowerShell or in the Management Portal.</span></span> <span data-ttu-id="572e5-105">Dans cette rubrique, vous trouverez des procédures pour les tâches courantes des listes de contrôle d’accès que vous pouvez effectuer à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="572e5-105">In this topic, you'll find procedures for ACL common tasks that you can complete using PowerShell.</span></span> <span data-ttu-id="572e5-106">Pour obtenir la liste des applets de commande Azure PowerShell, consultez [Applets de commande de gestion Azure](http://go.microsoft.com/fwlink/?LinkId=317721).</span><span class="sxs-lookup"><span data-stu-id="572e5-106">For the list of Azure PowerShell cmdlets see [Azure Management Cmdlets](http://go.microsoft.com/fwlink/?LinkId=317721).</span></span> <span data-ttu-id="572e5-107">Pour plus d’informations sur les listes de contrôle d’accès, consultez [Qu’est-ce qu’une liste de contrôle d’accès (ACL) réseau ?](virtual-networks-acl.md).</span><span class="sxs-lookup"><span data-stu-id="572e5-107">For more information about ACLs, see [What is a Network Access Control List (ACL)?](virtual-networks-acl.md).</span></span> <span data-ttu-id="572e5-108">Si vous voulez gérer vos listes de contrôle d’accès à partir du portail de gestion, consultez [Comment configurer des points de terminaison sur une machine virtuelle](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="572e5-108">If you want to manage your ACLs by using the Management Portal, see [How to Set Up Endpoints to a Virtual Machine](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="manage-network-acls-by-using-azure-powershell"></a><span data-ttu-id="572e5-109">Gérer les listes de contrôle d’accès réseau à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="572e5-109">Manage Network ACLs by using Azure PowerShell</span></span>
<span data-ttu-id="572e5-110">Vous pouvez utiliser les applets de commande Azure PowerShell pour créer, supprimer et configurer (définir) des listes de contrôle d’accès réseau.</span><span class="sxs-lookup"><span data-stu-id="572e5-110">You can use Azure PowerShell cmdlets to create, remove, and configure (set) Network Access Control Lists (ACLs).</span></span> <span data-ttu-id="572e5-111">Nous avons inclus quelques exemples qui illustrent des méthodes de configuration de listes de contrôle d’accès à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="572e5-111">We've included a few examples of some of the ways you can configure an ACL using PowerShell.</span></span>

<span data-ttu-id="572e5-112">Pour récupérer la liste complète des applets de commande PowerShell des listes ACL, utilisez l’une des opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="572e5-112">To retrieve a complete list of the ACL PowerShell cmdlets, you can use either of the following:</span></span>

    Get-Help *AzureACL*
    Get-Command -Noun AzureACLConfig

### <a name="create-a-network-acl-with-rules-that-permit-access-from-a-remote-subnet"></a><span data-ttu-id="572e5-113">Créer une liste de contrôle d’accès réseau avec des règles qui autorisent l’accès à un sous-réseau distant</span><span class="sxs-lookup"><span data-stu-id="572e5-113">Create a Network ACL with rules that permit access from a remote subnet</span></span>
<span data-ttu-id="572e5-114">L’exemple suivant illustre un moyen de créer une liste ACL contenant des règles.</span><span class="sxs-lookup"><span data-stu-id="572e5-114">The example below illustrates a way to create a new ACL that contains rules.</span></span> <span data-ttu-id="572e5-115">Cette liste ACL est ensuite appliquée à un point de terminaison de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="572e5-115">This ACL is then applied to a virtual machine endpoint.</span></span> <span data-ttu-id="572e5-116">Les règles ACL dans l’exemple ci-dessous autorisent l’accès à un sous-réseau distant.</span><span class="sxs-lookup"><span data-stu-id="572e5-116">The ACL rules in the example below will allow access from a remote subnet.</span></span> <span data-ttu-id="572e5-117">Pour créer une liste de contrôle d’accès réseau avec des règles Permit pour un sous-réseau distant, ouvrez un environnement d’écriture de scripts intégré d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="572e5-117">To create a new Network ACL with permit rules for a remote subnet, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="572e5-118">Copiez et collez le script ci-dessous, en configurant le script avec vos propres valeurs, puis exécutez le script.</span><span class="sxs-lookup"><span data-stu-id="572e5-118">Copy and paste the script below, configuring the script with your own values, and then run the script.</span></span>

1. <span data-ttu-id="572e5-119">Créez l’objet de liste de contrôle d’accès réseau.</span><span class="sxs-lookup"><span data-stu-id="572e5-119">Create the new network ACL object.</span></span>
   
        $acl1 = New-AzureAclConfig
2. <span data-ttu-id="572e5-120">Définissez une règle qui autorise l’accès depuis un sous-réseau distant.</span><span class="sxs-lookup"><span data-stu-id="572e5-120">Set a rule that permits access from a remote subnet.</span></span> <span data-ttu-id="572e5-121">Dans l’exemple ci-dessous, vous définissez la règle *100* (qui est prioritaire sur la règle 200 et au-delà) pour autoriser le sous-réseau distant *10.0.0.0/8* à accéder au point de terminaison de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="572e5-121">In the example below, you set rule *100* (which has priority over rule 200 and higher) to allow the remote subnet *10.0.0.0/8* access to the virtual machine endpoint.</span></span> <span data-ttu-id="572e5-122">Remplacez les valeurs en fonction de votre propre configuration.</span><span class="sxs-lookup"><span data-stu-id="572e5-122">Replace the values with your own configuration requirements.</span></span> <span data-ttu-id="572e5-123">Le nom « SharePoint ACL config » doit être remplacé par le nom convivial que vous attribuez à cette règle.</span><span class="sxs-lookup"><span data-stu-id="572e5-123">The name "SharePoint ACL config" should be replaced with the friendly name that you want to call this rule.</span></span>
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "SharePoint ACL config"
3. <span data-ttu-id="572e5-124">Pour les règles supplémentaires, répétez l’applet de commande, en remplaçant les valeurs en fonction de votre propre configuration.</span><span class="sxs-lookup"><span data-stu-id="572e5-124">For additional rules, repeat the cmdlet, replacing the values with your own configuration requirements.</span></span> <span data-ttu-id="572e5-125">Veillez à modifier l’ordre des numéros de règle pour qu’il reflète l’ordre dans lequel vous souhaitez que les règles soient appliquées.</span><span class="sxs-lookup"><span data-stu-id="572e5-125">Be sure to change the rule number Order to reflect the order in which you want the rules to be applied.</span></span> <span data-ttu-id="572e5-126">Le numéro de règle le plus bas est prioritaire sur le numéro supérieur.</span><span class="sxs-lookup"><span data-stu-id="572e5-126">The lower rule number takes precedence over the higher number.</span></span>
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
4. <span data-ttu-id="572e5-127">Ensuite, vous pouvez créer un point de terminaison (Add) ou définir la liste ACL d’un point de terminaison existant (Set).</span><span class="sxs-lookup"><span data-stu-id="572e5-127">Next, you can either create a new endpoint (Add) or set the ACL for an existing endpoint (Set).</span></span> <span data-ttu-id="572e5-128">Dans cet exemple, nous ajoutons un nouveau point de terminaison de machine virtuelle appelé « web » et nous mettons à jour le point de terminaison de machine virtuelle avec les paramètres ACL.</span><span class="sxs-lookup"><span data-stu-id="572e5-128">In this example, we will add a new virtual machine endpoint called "web" and update the virtual machine endpoint with the ACL settings.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        | Update-AzureVM
5. <span data-ttu-id="572e5-129">Ensuite, combinez les applets de commande et exécutez le script.</span><span class="sxs-lookup"><span data-stu-id="572e5-129">Next, combine the cmdlets and run the script.</span></span> <span data-ttu-id="572e5-130">Pour cet exemple, les applets de commande combinées ressemblent à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="572e5-130">For this example, the combined cmdlets would look like this:</span></span>
   
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

### <a name="remove-a-network-acl-rule-that-permits-access-from-a-remote-subnet"></a><span data-ttu-id="572e5-131">Supprimer une règle de liste de contrôle d’accès réseau qui autorise l’accès depuis un sous-réseau distant</span><span class="sxs-lookup"><span data-stu-id="572e5-131">Remove a Network ACL rule that permits access from a remote subnet</span></span>
<span data-ttu-id="572e5-132">L’exemple ci-dessous illustre une méthode de suppression d’une règle de liste de contrôle d’accès réseau.</span><span class="sxs-lookup"><span data-stu-id="572e5-132">The example below illustrates a way to remove a network ACL rule.</span></span>  <span data-ttu-id="572e5-133">Pour supprimer une liste de contrôle d’accès réseau avec des règles Permit pour un sous-réseau distant, ouvrez un environnement d’écriture de scripts intégré d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="572e5-133">To remove a Network ACL rule with permit rules for a remote subnet, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="572e5-134">Copiez et collez le script ci-dessous, en configurant le script avec vos propres valeurs, puis exécutez le script.</span><span class="sxs-lookup"><span data-stu-id="572e5-134">Copy and paste the script below, configuring the script with your own values, and then run the script.</span></span>

1. <span data-ttu-id="572e5-135">La première étape consiste à obtenir l’objet de liste de contrôle d’accès réseau du point de terminaison de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="572e5-135">First step is to get the Network ACL object for the virtual machine endpoint.</span></span> <span data-ttu-id="572e5-136">Ensuite, vous supprimez la règle ACL.</span><span class="sxs-lookup"><span data-stu-id="572e5-136">You'll then remove the ACL rule.</span></span> <span data-ttu-id="572e5-137">Dans ce cas, nous la supprimons par son ID de règle.</span><span class="sxs-lookup"><span data-stu-id="572e5-137">In this case, we are removing it by rule ID.</span></span> <span data-ttu-id="572e5-138">Seul l’ID de règle 0 est supprimé de la liste ACL.</span><span class="sxs-lookup"><span data-stu-id="572e5-138">This will only remove the rule ID 0 from the ACL.</span></span> <span data-ttu-id="572e5-139">L’objet ACL n’est pas supprimé du point de terminaison de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="572e5-139">It does not remove the ACL object from the virtual machine endpoint.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Get-AzureAclConfig –EndpointName "web" `
        | Set-AzureAclConfig –RemoveRule –ID 0 –ACL $acl1
2. <span data-ttu-id="572e5-140">Ensuite, vous devez appliquer l’objet de liste de contrôle d’accès réseau au point de terminaison de machine virtuelle et mettre à jour la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="572e5-140">Next, you must apply the Network ACL object to the virtual machine endpoint and update the virtual machine.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Set-AzureEndpoint –ACL $acl1 –Name "web" `
        | Update-AzureVM

### <a name="remove-a-network-acl-from-a-virtual-machine-endpoint"></a><span data-ttu-id="572e5-141">Supprimer une liste de contrôle d’accès réseau d’un point de terminaison de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="572e5-141">Remove a Network ACL from a virtual machine endpoint</span></span>
<span data-ttu-id="572e5-142">Dans certains scénarios, vous voudrez peut-être supprimer un objet de liste de contrôle d’accès réseau d’un point de terminaison de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="572e5-142">In certain scenarios, you might want to remove a Network ACL object from a virtual machine endpoint.</span></span> <span data-ttu-id="572e5-143">Pour ce faire, ouvrez un environnement d’écriture de scripts intégré d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="572e5-143">To do that, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="572e5-144">Copiez et collez le script ci-dessous, en configurant le script avec vos propres valeurs, puis exécutez le script.</span><span class="sxs-lookup"><span data-stu-id="572e5-144">Copy and paste the script below, configuring the script with your own values, and then run the script.</span></span>

        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Remove-AzureAclConfig –EndpointName "web" `
        | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="572e5-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="572e5-145">Next steps</span></span>
[<span data-ttu-id="572e5-146">Qu’est-ce qu’une liste de contrôle d’accès (ACL) réseau ?</span><span class="sxs-lookup"><span data-stu-id="572e5-146">What is a Network Access Control List (ACL)?</span></span>](virtual-networks-acl.md)

