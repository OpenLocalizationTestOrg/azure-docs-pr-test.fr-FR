---
title: "Azure Active Directory Domain Services : guide d’administration | Microsoft Docs"
description: "Joindre un domaine géré tooa machine virtuelle Windows Azure PowerShell et le modèle de déploiement classique hello."
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 9143b843-7327-43c3-baab-6e24a18db25e
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 21bc5930d84c5368a120f9d81f09320e2a0168fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-windows-server-virtual-machine-tooa-managed-domain-using-powershell"></a><span data-ttu-id="0ff92-103">Joindre un domaine géré tooa machine virtuelle Windows Server à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="0ff92-103">Join a Windows Server virtual machine tooa managed domain using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0ff92-104">Portail Azure Classic - Windows</span><span class="sxs-lookup"><span data-stu-id="0ff92-104">Azure classic portal - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
> * [<span data-ttu-id="0ff92-105">PowerShell - Windows</span><span class="sxs-lookup"><span data-stu-id="0ff92-105">PowerShell - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

> [!IMPORTANT]
> <span data-ttu-id="0ff92-106">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="0ff92-106">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="0ff92-107">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="0ff92-107">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="0ff92-108">Les Services de domaine Active Directory Azure ne prend pas en charge modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="0ff92-108">Azure AD Domain Services does not currently support hello Resource Manager model.</span></span>
>
>

<span data-ttu-id="0ff92-109">Ces étapes montrent le fonctionnement des commandes toocustomize un ensemble d’Azure PowerShell qui créer et préconfigurer une machine virtuelle Azure Windows à l’aide d’une approche de bloc de construction.</span><span class="sxs-lookup"><span data-stu-id="0ff92-109">These steps show you how toocustomize a set of Azure PowerShell commands that create and preconfigure a Windows-based Azure virtual machine by using a building block approach.</span></span> <span data-ttu-id="0ff92-110">Ces étapes vous permettent de créer une machine virtuelle Azure Windows et de joindre le domaine géré de tooan des Services de domaine Active Directory de Azure.</span><span class="sxs-lookup"><span data-stu-id="0ff92-110">These steps help you build a Windows-based Azure virtual machine and join it tooan Azure AD Domain Services managed domain.</span></span>

<span data-ttu-id="0ff92-111">Ces étapes utilisent une méthode de cases à remplir pour créer des jeux de commandes Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0ff92-111">These steps follow a fill-in-the-blanks approach for creating Azure PowerShell command sets.</span></span> <span data-ttu-id="0ff92-112">Cette approche peut être utile si vous tooPowerShell nouveau ou vous souhaitez tooknow le toospecify de valeurs pour la configuration réussie.</span><span class="sxs-lookup"><span data-stu-id="0ff92-112">This approach can be useful if you are new tooPowerShell or you want tooknow what values toospecify for successful configuration.</span></span> <span data-ttu-id="0ff92-113">Les utilisateurs expérimentés PowerShell peuvent prendre les commandes hello et remplacer leurs propres valeurs pour les variables de hello (lignes hello commençant par « $»).</span><span class="sxs-lookup"><span data-stu-id="0ff92-113">Advanced PowerShell users can take hello commands and substitute their own values for hello variables (hello lines beginning with "$").</span></span>

<span data-ttu-id="0ff92-114">Si vous n’avez pas déjà fait, suivez les instructions de hello de [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="0ff92-114">If you haven't done so already, use hello instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell on your local computer.</span></span> <span data-ttu-id="0ff92-115">Puis ouvrez une invite de commandes Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0ff92-115">Then, open a Windows PowerShell command prompt.</span></span>

## <a name="step-1-add-your-account"></a><span data-ttu-id="0ff92-116">Étape 1 : Ajouter votre compte</span><span class="sxs-lookup"><span data-stu-id="0ff92-116">Step 1: Add your account</span></span>
1. <span data-ttu-id="0ff92-117">À l’invite de commandes PowerShell hello, tapez **Add-AzureAccount** et cliquez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="0ff92-117">At hello PowerShell prompt, type **Add-AzureAccount** and click **Enter**.</span></span>
2. <span data-ttu-id="0ff92-118">Tapez hello adresse de messagerie associée à votre abonnement Azure et cliquez sur **continuer**.</span><span class="sxs-lookup"><span data-stu-id="0ff92-118">Type in hello email address associated with your Azure subscription and click **Continue**.</span></span>
3. <span data-ttu-id="0ff92-119">Tapez hello de mot de passe pour votre compte.</span><span class="sxs-lookup"><span data-stu-id="0ff92-119">Type in hello password for your account.</span></span>
4. <span data-ttu-id="0ff92-120">Cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="0ff92-120">Click **Sign in**.</span></span>

## <a name="step-2-set-your-subscription-and-storage-account"></a><span data-ttu-id="0ff92-121">Étape 2 : Configurer votre abonnement et votre compte de stockage</span><span class="sxs-lookup"><span data-stu-id="0ff92-121">Step 2: Set your subscription and storage account</span></span>
<span data-ttu-id="0ff92-122">Définissez votre abonnement Azure et le compte de stockage en exécutant ces commandes à l’invite de commandes Windows PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="0ff92-122">Set your Azure subscription and storage account by running these commands at hello Windows PowerShell command prompt.</span></span> <span data-ttu-id="0ff92-123">Tous les éléments entre guillemets hello, notamment hello < et >, remplacez les noms corrects hello.</span><span class="sxs-lookup"><span data-stu-id="0ff92-123">Replace everything within hello quotes, including hello < and > characters, with hello correct names.</span></span>

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

<span data-ttu-id="0ff92-124">Vous pouvez obtenir les nom d’abonnement approprié hello de hello propriété SubscriptionName de sortie hello Hello **Get-AzureSubscription** commande.</span><span class="sxs-lookup"><span data-stu-id="0ff92-124">You can get hello correct subscription name from hello SubscriptionName property of hello output of hello **Get-AzureSubscription** command.</span></span> <span data-ttu-id="0ff92-125">Vous pouvez obtenir nom de compte de stockage correct hello de hello propriété Label du résultat hello de hello **Get-AzureStorageAccount** commande une fois que vous exécutez hello **Select-AzureSubscription** commande.</span><span class="sxs-lookup"><span data-stu-id="0ff92-125">You can get hello correct storage account name from hello Label property of hello output of hello **Get-AzureStorageAccount** command after you run hello **Select-AzureSubscription** command.</span></span>

## <a name="step-3-step-by-step-walkthrough---provision-hello-virtual-machine-and-join-it-toohello-managed-domain"></a><span data-ttu-id="0ff92-126">Étape 3 : Procédure pas à pas : configurer l’ordinateur virtuel de hello et joindre le domaine géré de toohello</span><span class="sxs-lookup"><span data-stu-id="0ff92-126">Step 3: Step-by-step walkthrough - provision hello virtual machine and join it toohello managed domain</span></span>
<span data-ttu-id="0ff92-127">Voici toocreate Azure PowerShell correspondante du jeu de commande hello cet ordinateur virtuel, des lignes vides entre chaque bloc pour une meilleure lisibilité.</span><span class="sxs-lookup"><span data-stu-id="0ff92-127">Here is hello corresponding Azure PowerShell command set toocreate this virtual machine, with blank lines between each block for readability.</span></span>

<span data-ttu-id="0ff92-128">Indiquez les informations toobe de machine virtuelle Windows hello configuré.</span><span class="sxs-lookup"><span data-stu-id="0ff92-128">Specify information about hello Windows virtual machine toobe provisioned.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

<span data-ttu-id="0ff92-129">Pour les valeurs de InstanceSize hello pour D, DS ou machines virtuelles de série G, consultez [Machine virtuelle et les tailles de Service Cloud pour Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="0ff92-129">For hello InstanceSize values for D-, DS-, or G-series virtual machines, see [Virtual Machine and Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span>

<span data-ttu-id="0ff92-130">Fournissent des informations sur le domaine géré de hello.</span><span class="sxs-lookup"><span data-stu-id="0ff92-130">Provide information about hello managed domain.</span></span>

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

<span data-ttu-id="0ff92-131">Spécifiez le nom hello du service de cloud hello.</span><span class="sxs-lookup"><span data-stu-id="0ff92-131">Specify hello name of hello cloud service.</span></span>

    $svcname="Contoso100-test"

<span data-ttu-id="0ff92-132">Spécifiez nom hello Hello de toowhich de réseau virtuel hello que machine virtuelle doit être joint.</span><span class="sxs-lookup"><span data-stu-id="0ff92-132">Specify hello name of hello virtual network toowhich hello VM should be joined.</span></span> <span data-ttu-id="0ff92-133">Vérifiez que ce domaine d’AAD-DS gérés hello est disponible dans ce réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="0ff92-133">Ensure that hello AAD-DS managed domain is available in this virtual network.</span></span>

    $vnetname="MyPreviewVnet"

<span data-ttu-id="0ff92-134">Sélectionnez hello VM image toobe utilisé tooprovision hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0ff92-134">Select hello VM image toobe used tooprovision hello VM.</span></span>

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

<span data-ttu-id="0ff92-135">Configurer hello VM - nom de machine virtuelle de jeu, instance toobe taille et de l’image utilisée.</span><span class="sxs-lookup"><span data-stu-id="0ff92-135">Configure hello VM - set VM name, instance size & image toobe used.</span></span>

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

<span data-ttu-id="0ff92-136">Obtenir des informations d’identification d’administrateur local pour hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0ff92-136">Obtain local administrator credentials for hello VM.</span></span> <span data-ttu-id="0ff92-137">Choisissez un mot de passe administrateur fort.</span><span class="sxs-lookup"><span data-stu-id="0ff92-137">Choose a strong local administrator password.</span></span>

    $localadmincred=Get-Credential –Message "Type hello name and password of hello local administrator account."

<span data-ttu-id="0ff92-138">Obtenir des informations d’identification pour un compte d’utilisateur qui appartiennent à toojoin VM toohello managé domaine du groupe des administrateurs de contrôleur de domaine too'AAD de.</span><span class="sxs-lookup"><span data-stu-id="0ff92-138">Obtain credentials for a user account belonging too'AAD DC Administrators' group toojoin VM toohello managed domain.</span></span> <span data-ttu-id="0ff92-139">Ne spécifiez nom de domaine hello - pour l’instance, dans notre exemple, nous spécifions « bob » comme nom d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="0ff92-139">Do not specify hello domain name - for instance, in our example, we specify 'bob' as hello user name.</span></span>

    $domainadmincred=Get-Credential –Message "Now type hello name (DO NOT INCLUDE hello DOMAIN) and password of an account in hello AAD DC Administrators group, that has permission tooadd hello machine toohello domain."

<span data-ttu-id="0ff92-140">Configurer hello VM - spécifier la condition de jointure de domaine et les informations d’identification requises.</span><span class="sxs-lookup"><span data-stu-id="0ff92-140">Configure hello VM - specify domain join requirement & required credentials.</span></span>

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

<span data-ttu-id="0ff92-141">Définissez un sous-réseau pour hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0ff92-141">Set a subnet for hello VM.</span></span>

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

<span data-ttu-id="0ff92-142">Facultatif : Point toohello adresse du domaine de hello.</span><span class="sxs-lookup"><span data-stu-id="0ff92-142">Optional: Point toohello IP address of hello domain.</span></span> <span data-ttu-id="0ff92-143">Si vous définissez des serveurs DNS pour le réseau virtuel de hello adresses IP de hello Hello de toobe domaine géré hello des Services de domaine Active Directory de Azure, cette étape n’est pas requise.</span><span class="sxs-lookup"><span data-stu-id="0ff92-143">If you set hello IP addresses of hello Azure AD Domain Services managed domain toobe hello DNS servers for hello virtual network, this step is not required.</span></span>

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

<span data-ttu-id="0ff92-144">Maintenant, hello de disposition appartenant au domaine machine virtuelle Windows.</span><span class="sxs-lookup"><span data-stu-id="0ff92-144">Now, provision hello domain-joined Windows VM.</span></span>

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="script-tooprovision-a-windows-vm-and-automatically-join-it-tooan-aad-domain-services-managed-domain"></a><span data-ttu-id="0ff92-145">Script tooprovision une machine virtuelle Windows et le joindre automatiquement domaine géré de Services de domaine AAD tooan</span><span class="sxs-lookup"><span data-stu-id="0ff92-145">Script tooprovision a Windows VM and automatically join it tooan AAD Domain Services managed domain</span></span>
<span data-ttu-id="0ff92-146">Cette commande PowerShell crée une machine virtuelle pour un serveur métier qui :</span><span class="sxs-lookup"><span data-stu-id="0ff92-146">This PowerShell command set creates a virtual machine for a line-of-business server that:</span></span>

* <span data-ttu-id="0ff92-147">Utilise l’image de Windows Server 2012 R2 Datacenter hello.</span><span class="sxs-lookup"><span data-stu-id="0ff92-147">Uses hello Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="0ff92-148">est une machine virtuelle très petite</span><span class="sxs-lookup"><span data-stu-id="0ff92-148">Is an extra small virtual machine.</span></span>
* <span data-ttu-id="0ff92-149">A le nom hello Contoso100 et de test.</span><span class="sxs-lookup"><span data-stu-id="0ff92-149">Has hello name Contoso100-test.</span></span>
* <span data-ttu-id="0ff92-150">Est automatiquement jointe toohello contoso100 managé un domaine.</span><span class="sxs-lookup"><span data-stu-id="0ff92-150">Is automatically domain joined toohello contoso100 managed domain.</span></span>
* <span data-ttu-id="0ff92-151">Est ajouté toohello même réseau virtuel que hello géré de domaine.</span><span class="sxs-lookup"><span data-stu-id="0ff92-151">Is added toohello same virtual network as hello managed domain.</span></span>

<span data-ttu-id="0ff92-152">Voici hello exemple complet script toocreate hello Windows virtual machine et le joindre automatiquement domaine géré de toohello des Services de domaine Active Directory de Azure.</span><span class="sxs-lookup"><span data-stu-id="0ff92-152">Here is hello full sample script toocreate hello Windows virtual machine and automatically join it toohello Azure AD Domain Services managed domain.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

    $svcname="Contoso100-test"
    $vnetname="MyPreviewVnet"

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $localadmincred=Get-Credential –Message "Type hello name and password of hello local administrator account."

    $domainadmincred=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account in hello AAD DC Administrators group, that has permission tooadd hello machine toohello domain."

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="related-content"></a><span data-ttu-id="0ff92-153">Contenu connexe</span><span class="sxs-lookup"><span data-stu-id="0ff92-153">Related Content</span></span>
* [<span data-ttu-id="0ff92-154">Services de domaine Azure AD : guide de prise en main</span><span class="sxs-lookup"><span data-stu-id="0ff92-154">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="0ff92-155">Administrer un domaine géré par les services de domaine Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0ff92-155">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
