---
title: "Azure Active Directory Domain Services : guide d’administration | Microsoft Docs"
description: "Joignez une machine virtuelle Windows à un domaine géré avec Azure PowerShell et le modèle de déploiement classique."
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
ms.openlocfilehash: 1bb1546fb616131a1e1868a0d0610c4cad5d73e2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="join-a-windows-server-virtual-machine-to-a-managed-domain-using-powershell"></a><span data-ttu-id="0bfd2-103">Joindre une machine virtuelle Windows Server à un domaine géré à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="0bfd2-103">Join a Windows Server virtual machine to a managed domain using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0bfd2-104">Portail Azure Classic - Windows</span><span class="sxs-lookup"><span data-stu-id="0bfd2-104">Azure classic portal - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
> * [<span data-ttu-id="0bfd2-105">PowerShell - Windows</span><span class="sxs-lookup"><span data-stu-id="0bfd2-105">PowerShell - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

> [!IMPORTANT]
> <span data-ttu-id="0bfd2-106">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="0bfd2-106">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="0bfd2-107">Cet article traite du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="0bfd2-107">This article covers using the classic deployment model.</span></span> <span data-ttu-id="0bfd2-108">Actuellement, les services de domaine Azure AD ne prennent pas en charge le modèle de gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="0bfd2-108">Azure AD Domain Services does not currently support the Resource Manager model.</span></span>
>
>

<span data-ttu-id="0bfd2-109">Ces étapes vous montrent comment personnaliser un jeu de commandes Azure PowerShell en vue de créer et de préconfigurer une machine virtuelle Azure basée sur Windows à l'aide d'une approche modulaire.</span><span class="sxs-lookup"><span data-stu-id="0bfd2-109">These steps show you how to customize a set of Azure PowerShell commands that create and preconfigure a Windows-based Azure virtual machine by using a building block approach.</span></span> <span data-ttu-id="0bfd2-110">Ces étapes peuvent vous aider à créer une machine virtuelle Azure Windows et à la joindre à un domaine géré de services de domaine Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0bfd2-110">These steps help you build a Windows-based Azure virtual machine and join it to an Azure AD Domain Services managed domain.</span></span>

<span data-ttu-id="0bfd2-111">Ces étapes utilisent une méthode de cases à remplir pour créer des jeux de commandes Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0bfd2-111">These steps follow a fill-in-the-blanks approach for creating Azure PowerShell command sets.</span></span> <span data-ttu-id="0bfd2-112">Cette méthode peut être utile si vous découvrez PowerShell ou souhaitez connaître les valeurs à indiquer pour une configuration réussie.</span><span class="sxs-lookup"><span data-stu-id="0bfd2-112">This approach can be useful if you are new to PowerShell or you want to know what values to specify for successful configuration.</span></span> <span data-ttu-id="0bfd2-113">Les utilisateurs avancés de PowerShell peuvent prendre les commandes et indiquer leurs propres valeurs pour les variables (lignes commençant par « $ »).</span><span class="sxs-lookup"><span data-stu-id="0bfd2-113">Advanced PowerShell users can take the commands and substitute their own values for the variables (the lines beginning with "$").</span></span>

<span data-ttu-id="0bfd2-114">Si ce n’est pas encore fait, installez Azure PowerShell sur votre ordinateur local à l’aide des instructions décrites dans [Installation et configuration d’Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="0bfd2-114">If you haven't done so already, use the instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) to install Azure PowerShell on your local computer.</span></span> <span data-ttu-id="0bfd2-115">Puis ouvrez une invite de commandes Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0bfd2-115">Then, open a Windows PowerShell command prompt.</span></span>

## <a name="step-1-add-your-account"></a><span data-ttu-id="0bfd2-116">Étape 1 : Ajouter votre compte</span><span class="sxs-lookup"><span data-stu-id="0bfd2-116">Step 1: Add your account</span></span>
1. <span data-ttu-id="0bfd2-117">À l’invite PowerShell, tapez **Add-AzureAccount**, puis cliquez sur **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="0bfd2-117">At the PowerShell prompt, type **Add-AzureAccount** and click **Enter**.</span></span>
2. <span data-ttu-id="0bfd2-118">Tapez l’adresse de messagerie associée à votre abonnement Azure, puis cliquez sur **Continuer**.</span><span class="sxs-lookup"><span data-stu-id="0bfd2-118">Type in the email address associated with your Azure subscription and click **Continue**.</span></span>
3. <span data-ttu-id="0bfd2-119">Tapez le mot de passe de votre compte.</span><span class="sxs-lookup"><span data-stu-id="0bfd2-119">Type in the password for your account.</span></span>
4. <span data-ttu-id="0bfd2-120">Cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="0bfd2-120">Click **Sign in**.</span></span>

## <a name="step-2-set-your-subscription-and-storage-account"></a><span data-ttu-id="0bfd2-121">Étape 2 : Configurer votre abonnement et votre compte de stockage</span><span class="sxs-lookup"><span data-stu-id="0bfd2-121">Step 2: Set your subscription and storage account</span></span>
<span data-ttu-id="0bfd2-122">Pour configurer votre abonnement et votre compte de stockage Azure, exécutez ces commandes à l’invite de commandes Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0bfd2-122">Set your Azure subscription and storage account by running these commands at the Windows PowerShell command prompt.</span></span> <span data-ttu-id="0bfd2-123">Remplacez tous les éléments entre guillemets, y compris les caractères < et >, par les noms appropriés.</span><span class="sxs-lookup"><span data-stu-id="0bfd2-123">Replace everything within the quotes, including the < and > characters, with the correct names.</span></span>

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

<span data-ttu-id="0bfd2-124">Le nom de l’abonnement apparaît dans la propriété SubscriptionName du résultat de la commande **Get-AzureSubscription** .</span><span class="sxs-lookup"><span data-stu-id="0bfd2-124">You can get the correct subscription name from the SubscriptionName property of the output of the **Get-AzureSubscription** command.</span></span> <span data-ttu-id="0bfd2-125">Le nom du compte de stockage correct apparaît dans la propriété Label de la sortie de la commande **Get-AzureStorageAccount** une fois que vous avez exécuté la commande **Select-AzureSubscription**.</span><span class="sxs-lookup"><span data-stu-id="0bfd2-125">You can get the correct storage account name from the Label property of the output of the **Get-AzureStorageAccount** command after you run the **Select-AzureSubscription** command.</span></span>

## <a name="step-3-step-by-step-walkthrough---provision-the-virtual-machine-and-join-it-to-the-managed-domain"></a><span data-ttu-id="0bfd2-126">Étape 3: Procédure pas à pas – approvisionnez la machine virtuelle et joignez-la au domaine géré</span><span class="sxs-lookup"><span data-stu-id="0bfd2-126">Step 3: Step-by-step walkthrough - provision the virtual machine and join it to the managed domain</span></span>
<span data-ttu-id="0bfd2-127">Voici le jeu de commandes Azure PowerShell correspondant qui permet de créer cette machine virtuelle. Les lignes vides entre chaque bloc offrent une meilleure lisibilité.</span><span class="sxs-lookup"><span data-stu-id="0bfd2-127">Here is the corresponding Azure PowerShell command set to create this virtual machine, with blank lines between each block for readability.</span></span>

<span data-ttu-id="0bfd2-128">Spécifiez des informations sur la machine virtuelle Windows à approvisionner.</span><span class="sxs-lookup"><span data-stu-id="0bfd2-128">Specify information about the Windows virtual machine to be provisioned.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

<span data-ttu-id="0bfd2-129">Pour plus d’informations sur les valeurs InstanceSize des machines virtuelles des séries D, DS et G, voir l’article [Tailles de machines virtuelles et de services cloud pour Microsoft Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="0bfd2-129">For the InstanceSize values for D-, DS-, or G-series virtual machines, see [Virtual Machine and Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span>

<span data-ttu-id="0bfd2-130">Fournissent des informations sur le domaine géré.</span><span class="sxs-lookup"><span data-stu-id="0bfd2-130">Provide information about the managed domain.</span></span>

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

<span data-ttu-id="0bfd2-131">Spécifiez le nom du service cloud.</span><span class="sxs-lookup"><span data-stu-id="0bfd2-131">Specify the name of the cloud service.</span></span>

    $svcname="Contoso100-test"

<span data-ttu-id="0bfd2-132">Spécifiez le nom du réseau virtuel auquel la machine virtuelle doit être jointe.</span><span class="sxs-lookup"><span data-stu-id="0bfd2-132">Specify the name of the virtual network to which the VM should be joined.</span></span> <span data-ttu-id="0bfd2-133">Assurez-vous que le domaine géré AAD-DS est disponible dans ce réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="0bfd2-133">Ensure that the AAD-DS managed domain is available in this virtual network.</span></span>

    $vnetname="MyPreviewVnet"

<span data-ttu-id="0bfd2-134">Sélectionnez l'image de machine virtuelle à utiliser pour approvisionner la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0bfd2-134">Select the VM image to be used to provision the VM.</span></span>

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

<span data-ttu-id="0bfd2-135">Configurez la machine virtuelle - définissez le nom de la machine virtuelle, la taille d'instance et l’image à utiliser.</span><span class="sxs-lookup"><span data-stu-id="0bfd2-135">Configure the VM - set VM name, instance size & image to be used.</span></span>

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

<span data-ttu-id="0bfd2-136">Obtenez les informations d’identification du compte d’administrateur local pour la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0bfd2-136">Obtain local administrator credentials for the VM.</span></span> <span data-ttu-id="0bfd2-137">Choisissez un mot de passe administrateur fort.</span><span class="sxs-lookup"><span data-stu-id="0bfd2-137">Choose a strong local administrator password.</span></span>

    $localadmincred=Get-Credential –Message "Type the name and password of the local administrator account."

<span data-ttu-id="0bfd2-138">Obtenez des informations d'identification pour un compte d'utilisateur appartenant au groupe « Administrateurs de contrôleur de domaine AAD » pour joindre la machine virtuelle au domaine géré.</span><span class="sxs-lookup"><span data-stu-id="0bfd2-138">Obtain credentials for a user account belonging to 'AAD DC Administrators' group to join VM to the managed domain.</span></span> <span data-ttu-id="0bfd2-139">Ne spécifiez pas le nom de domaine – par exemple, dans notre exemple, nous spécifions « bob » comme nom d'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0bfd2-139">Do not specify the domain name - for instance, in our example, we specify 'bob' as the user name.</span></span>

    $domainadmincred=Get-Credential –Message "Now type the name (DO NOT INCLUDE THE DOMAIN) and password of an account in the AAD DC Administrators group, that has permission to add the machine to the domain."

<span data-ttu-id="0bfd2-140">Configurez la machine virtuelle - spécifiez la nécessité de jonction de domaine et les informations d'identification requises.</span><span class="sxs-lookup"><span data-stu-id="0bfd2-140">Configure the VM - specify domain join requirement & required credentials.</span></span>

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

<span data-ttu-id="0bfd2-141">Définissez un sous-réseau pour la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0bfd2-141">Set a subnet for the VM.</span></span>

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

<span data-ttu-id="0bfd2-142">Facultatif : point vers l'adresse IP du domaine.</span><span class="sxs-lookup"><span data-stu-id="0bfd2-142">Optional: Point to the IP address of the domain.</span></span> <span data-ttu-id="0bfd2-143">Si vous définissez les adresses IP du domaine des services de domaine Azure AD géré pour être les serveurs DNS du réseau virtuel, cette étape n'est pas requise.</span><span class="sxs-lookup"><span data-stu-id="0bfd2-143">If you set the IP addresses of the Azure AD Domain Services managed domain to be the DNS servers for the virtual network, this step is not required.</span></span>

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

<span data-ttu-id="0bfd2-144">Maintenant, approvisionnez la machine virtuelle Windows jointe à un domaine.</span><span class="sxs-lookup"><span data-stu-id="0bfd2-144">Now, provision the domain-joined Windows VM.</span></span>

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="script-to-provision-a-windows-vm-and-automatically-join-it-to-an-aad-domain-services-managed-domain"></a><span data-ttu-id="0bfd2-145">Script pour approvisionner une machine virtuelle Windows et la joindre automatiquement à un domaine géré de services de domaine AAD</span><span class="sxs-lookup"><span data-stu-id="0bfd2-145">Script to provision a Windows VM and automatically join it to an AAD Domain Services managed domain</span></span>
<span data-ttu-id="0bfd2-146">Cette commande PowerShell crée une machine virtuelle pour un serveur métier qui :</span><span class="sxs-lookup"><span data-stu-id="0bfd2-146">This PowerShell command set creates a virtual machine for a line-of-business server that:</span></span>

* <span data-ttu-id="0bfd2-147">utilise l'image Windows Server 2012 R2 Datacenter</span><span class="sxs-lookup"><span data-stu-id="0bfd2-147">Uses the Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="0bfd2-148">est une machine virtuelle très petite</span><span class="sxs-lookup"><span data-stu-id="0bfd2-148">Is an extra small virtual machine.</span></span>
* <span data-ttu-id="0bfd2-149">porte le nom Contoso100-test</span><span class="sxs-lookup"><span data-stu-id="0bfd2-149">Has the name Contoso100-test.</span></span>
* <span data-ttu-id="0bfd2-150">est automatiquement joint au domaine géré contoso100</span><span class="sxs-lookup"><span data-stu-id="0bfd2-150">Is automatically domain joined to the contoso100 managed domain.</span></span>
* <span data-ttu-id="0bfd2-151">est ajouté au même réseau virtuel en tant que le domaine géré.</span><span class="sxs-lookup"><span data-stu-id="0bfd2-151">Is added to the same virtual network as the managed domain.</span></span>

<span data-ttu-id="0bfd2-152">Voici l'exemple de script complet pour créer la machine virtuelle Windows et la joindre automatiquement aux services de domaine Azure AD gérés.</span><span class="sxs-lookup"><span data-stu-id="0bfd2-152">Here is the full sample script to create the Windows virtual machine and automatically join it to the Azure AD Domain Services managed domain.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

    $svcname="Contoso100-test"
    $vnetname="MyPreviewVnet"

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $localadmincred=Get-Credential –Message "Type the name and password of the local administrator account."

    $domainadmincred=Get-Credential –Message "Now type the name (not including the domain) and password of an account in the AAD DC Administrators group, that has permission to add the machine to the domain."

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="related-content"></a><span data-ttu-id="0bfd2-153">Contenu connexe</span><span class="sxs-lookup"><span data-stu-id="0bfd2-153">Related Content</span></span>
* [<span data-ttu-id="0bfd2-154">Services de domaine Azure AD : guide de prise en main</span><span class="sxs-lookup"><span data-stu-id="0bfd2-154">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="0bfd2-155">Administrer un domaine géré par les services de domaine Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0bfd2-155">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
