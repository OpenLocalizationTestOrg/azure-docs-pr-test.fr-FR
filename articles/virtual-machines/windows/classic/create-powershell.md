---
title: "Créer une machine virtuelle Windows avec PowerShell | Microsoft Docs"
description: "Créez des machines virtuelles Windows avec Azure PowerShell et le modèle de déploiement classique."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 42c0d4be-573c-45d1-b9b0-9327537702f7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 75c6cf17ee269ae169d9f2f748d0985ca07e454e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell-and-the-classic-deployment-model"></a><span data-ttu-id="5e312-103">Créer une machine virtuelle Windows avec PowerShell et le modèle de déploiement Classic</span><span class="sxs-lookup"><span data-stu-id="5e312-103">Create a Windows virtual machine with PowerShell and the classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5e312-104">Portail Azure - Windows</span><span class="sxs-lookup"><span data-stu-id="5e312-104">Azure portal - Windows</span></span>](tutorial.md)
> * [<span data-ttu-id="5e312-105">PowerShell - Windows</span><span class="sxs-lookup"><span data-stu-id="5e312-105">PowerShell - Windows</span></span>](create-powershell.md)
> 
> 

<br>

> [!IMPORTANT] 
> <span data-ttu-id="5e312-106">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="5e312-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="5e312-107">Cet article traite du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="5e312-107">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="5e312-108">Pour la plupart des nouveaux déploiements, Microsoft recommande d’utiliser le modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5e312-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="5e312-109">Découvrez comment [effectuer ces étapes à l’aide du modèle Resource Manager](../../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5e312-109">Learn how to [perform these steps using the Resource Manager model](../../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="5e312-110">Ces étapes vous montrent comment personnaliser un jeu de commandes Azure PowerShell en vue de créer et de préconfigurer une machine virtuelle Azure basée sur Windows à l'aide d'une approche modulaire.</span><span class="sxs-lookup"><span data-stu-id="5e312-110">These steps show you how to customize a set of Azure PowerShell commands that create and preconfigure a Windows-based Azure virtual machine by using a building block approach.</span></span> <span data-ttu-id="5e312-111">À l'aide de cette procédure, vous pouvez créer rapidement un jeu de commandes pour une nouvelle machine virtuelle basée sur Windows et étendre un déploiement existant, ou créer plusieurs jeux de commandes qui génèrent rapidement un environnement personnalisé de développement/test ou destiné aux professionnels de l'informatique.</span><span class="sxs-lookup"><span data-stu-id="5e312-111">You can use this process to quickly create a command set for a new Windows-based virtual machine and expand an existing deployment or to create multiple command sets that quickly build out a custom dev/test or IT pro environment.</span></span>

<span data-ttu-id="5e312-112">Ces étapes utilisent une méthode de cases à remplir pour créer des jeux de commandes Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5e312-112">These steps follow a fill-in-the-blanks approach for creating Azure PowerShell command sets.</span></span> <span data-ttu-id="5e312-113">Cette méthode peut être utile si vous découvrez PowerShell ou simplement si vous souhaitez connaître les valeurs à indiquer pour une configuration réussie.</span><span class="sxs-lookup"><span data-stu-id="5e312-113">This approach can be useful if you are new to PowerShell or you just want to know what values to specify for successful configuration.</span></span> <span data-ttu-id="5e312-114">Les utilisateurs avancés de PowerShell peuvent prendre les commandes et indiquer leurs propres valeurs pour les variables (lignes commençant par « $ »).</span><span class="sxs-lookup"><span data-stu-id="5e312-114">Advanced PowerShell users can take the commands and substitute their own values for the variables (the lines beginning with "$").</span></span>

<span data-ttu-id="5e312-115">Si ce n’est pas encore fait, installez Azure PowerShell sur votre ordinateur local à l’aide des instructions décrites dans [Installation et configuration d’Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="5e312-115">If you haven't done so already, use the instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) to install Azure PowerShell on your local computer.</span></span> <span data-ttu-id="5e312-116">Puis ouvrez une invite de commandes Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5e312-116">Then, open a Windows PowerShell command prompt.</span></span>

## <a name="step-1-add-your-account"></a><span data-ttu-id="5e312-117">Étape 1 : Ajouter votre compte</span><span class="sxs-lookup"><span data-stu-id="5e312-117">Step 1: Add your account</span></span>
1. <span data-ttu-id="5e312-118">À l’invite PowerShell, tapez **Add-AzureAccount**, puis cliquez sur **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="5e312-118">At the PowerShell prompt, type **Add-AzureAccount** and click **Enter**.</span></span> 
2. <span data-ttu-id="5e312-119">Tapez l’adresse de messagerie associée à votre abonnement Azure, puis cliquez sur **Continuer**.</span><span class="sxs-lookup"><span data-stu-id="5e312-119">Type in the email address associated with your Azure subscription and click **Continue**.</span></span> 
3. <span data-ttu-id="5e312-120">Tapez le mot de passe de votre compte.</span><span class="sxs-lookup"><span data-stu-id="5e312-120">Type in the password for your account.</span></span> 
4. <span data-ttu-id="5e312-121">Cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="5e312-121">Click **Sign in**.</span></span>

## <a name="step-2-set-your-subscription-and-storage-account"></a><span data-ttu-id="5e312-122">Étape 2 : Configurer votre abonnement et votre compte de stockage</span><span class="sxs-lookup"><span data-stu-id="5e312-122">Step 2: Set your subscription and storage account</span></span>
<span data-ttu-id="5e312-123">Pour configurer votre abonnement et votre compte de stockage Azure, exécutez ces commandes à l’invite de commandes Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5e312-123">Set your Azure subscription and storage account by running these commands at the Windows PowerShell command prompt.</span></span> <span data-ttu-id="5e312-124">Remplacez tous les éléments entre guillemets, y compris les caractères < et >, par les noms appropriés.</span><span class="sxs-lookup"><span data-stu-id="5e312-124">Replace everything within the quotes, including the < and > characters, with the correct names.</span></span>

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

<span data-ttu-id="5e312-125">Le nom de l’abonnement apparaît dans la propriété SubscriptionName du résultat de la commande **Get-AzureSubscription** .</span><span class="sxs-lookup"><span data-stu-id="5e312-125">You can get the correct subscription name from the SubscriptionName property of the output of the **Get-AzureSubscription** command.</span></span> <span data-ttu-id="5e312-126">Le nom du compte de stockage correct apparaît dans la propriété Label de la sortie de la commande **Get-AzureStorageAccount** une fois que vous avez exécuté la commande **Select-AzureSubscription**.</span><span class="sxs-lookup"><span data-stu-id="5e312-126">You can get the correct storage account name from the Label property of the output of the **Get-AzureStorageAccount** command after you run the **Select-AzureSubscription** command.</span></span>

## <a name="step-3-determine-the-imagefamily"></a><span data-ttu-id="5e312-127">Étape 3 : déterminer la valeur ImageFamily</span><span class="sxs-lookup"><span data-stu-id="5e312-127">Step 3: Determine the ImageFamily</span></span>
<span data-ttu-id="5e312-128">Vous devez ensuite déterminer la valeur ImageFamily ou Étiquette pour l'image spécifique correspondant à la machine virtuelle Azure que vous voulez créer.</span><span class="sxs-lookup"><span data-stu-id="5e312-128">Next, you need to determine the ImageFamily or Label value for the specific image corresponding to the Azure virtual machine you want to create.</span></span> <span data-ttu-id="5e312-129">Vous pouvez obtenir la liste des valeurs ImageFamily disponibles à l'aide de cette commande.</span><span class="sxs-lookup"><span data-stu-id="5e312-129">You can get the list of available ImageFamily values with this command.</span></span>

    Get-AzureVMImage | select ImageFamily -Unique

<span data-ttu-id="5e312-130">Voici des exemples de valeurs ImageFamily pour les ordinateurs basés sur Windows :</span><span class="sxs-lookup"><span data-stu-id="5e312-130">Here are some examples of ImageFamily values for Windows-based computers:</span></span>

* <span data-ttu-id="5e312-131">Windows Server 2012 R2 Datacenter</span><span class="sxs-lookup"><span data-stu-id="5e312-131">Windows Server 2012 R2 Datacenter</span></span>
* <span data-ttu-id="5e312-132">Windows Server 2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="5e312-132">Windows Server 2008 R2 SP1</span></span>
* <span data-ttu-id="5e312-133">Windows Server 2016 Technical Preview 4</span><span class="sxs-lookup"><span data-stu-id="5e312-133">Windows Server 2016 Technical Preview 4</span></span>
* <span data-ttu-id="5e312-134">SQL Server 2012 SP1 Enterprise sur Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="5e312-134">SQL Server 2012 SP1 Enterprise on Windows Server 2012</span></span>

<span data-ttu-id="5e312-135">Si vous trouvez l’image que vous recherchez, ouvrez une nouvelle instance de l’éditeur de texte de votre choix ou de l’environnement d’écriture de scripts intégré de PowerShell (ISE).</span><span class="sxs-lookup"><span data-stu-id="5e312-135">If you find the image you are looking for, open a fresh instance of the text editor of your choice or the PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="5e312-136">Copiez le texte suivant dans le nouveau fichier texte ou PowerShell ISE, en remplaçant la valeur ImageFamily.</span><span class="sxs-lookup"><span data-stu-id="5e312-136">Copy the following into the new text file or the PowerShell ISE, substituting the ImageFamily value.</span></span>

    $family="<ImageFamily value>"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

<span data-ttu-id="5e312-137">Dans certains cas, le nom de l'image se trouve dans la propriété Étiquette au lieu de la valeur ImageFamily.</span><span class="sxs-lookup"><span data-stu-id="5e312-137">In some cases, the image name is in the Label property instead of the ImageFamily value.</span></span> <span data-ttu-id="5e312-138">Si vous ne trouvez pas l'image souhaitée à l'aide de la propriété ImageFamily, triez les images par propriété Étiquette à l'aide de cette commande.</span><span class="sxs-lookup"><span data-stu-id="5e312-138">If you didn't find the image that you are looking for using the ImageFamily property, list the images by their Label property with this command.</span></span>

    Get-AzureVMImage | select Label -Unique

<span data-ttu-id="5e312-139">Si vous trouvez l'image appropriée avec cette commande, ouvrez une nouvelle instance de l'éditeur de texte de votre choix ou PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="5e312-139">If you find the right image with this command, open a fresh instance of the text editor of your choice or the PowerShell ISE.</span></span> <span data-ttu-id="5e312-140">Copiez le texte suivant dans le nouveau fichier texte ou PowerShell ISE, en remplaçant la valeur Label.</span><span class="sxs-lookup"><span data-stu-id="5e312-140">Copy the following into the new text file or the PowerShell ISE, substituting the Label value.</span></span>

    $label="<Label value>"
    $image = Get-AzureVMImage | where { $_.Label -eq $label } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

## <a name="step-4-build-your-command-set"></a><span data-ttu-id="5e312-141">Étape 4 : générer votre jeu de commandes</span><span class="sxs-lookup"><span data-stu-id="5e312-141">Step 4: Build your command set</span></span>
<span data-ttu-id="5e312-142">Créez le reste de votre jeu de commandes en copiant le jeu de blocs approprié ci-dessous dans votre nouveau fichier texte ou ISE, puis en renseignant les valeurs des variables et en supprimant les caractères < et >.</span><span class="sxs-lookup"><span data-stu-id="5e312-142">Build the rest of your command set by copying the appropriate set of blocks below into your new text file or the ISE and then filling in the variable values and removing the < and > characters.</span></span> <span data-ttu-id="5e312-143">Pour avoir une idée du résultat final, consultez les deux [exemples](#examples) figurant à la fin de cet article.</span><span class="sxs-lookup"><span data-stu-id="5e312-143">See the two [examples](#examples) at the end of this article for an idea of the final result.</span></span>

<span data-ttu-id="5e312-144">Pour commencer, choisissez l'un des deux blocs de commandes suivants (obligatoire).</span><span class="sxs-lookup"><span data-stu-id="5e312-144">Start your command set by choosing one of these two command blocks (required).</span></span>

<span data-ttu-id="5e312-145">Option 1 : spécifiez un nom et une taille de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5e312-145">Option 1: Specify a virtual machine name and a size.</span></span>

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

<span data-ttu-id="5e312-146">Option 2 : spécifiez un nom, une taille et un nom de groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="5e312-146">Option 2: Specify a name, size, and availability set name.</span></span>

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $availset="<set name>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image -AvailabilitySetName $availset

<span data-ttu-id="5e312-147">Pour plus d’informations sur les valeurs InstanceSize des machines virtuelles des séries D, DS et G, voir l’article [Tailles de machines virtuelles et de services cloud pour Microsoft Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="5e312-147">For the InstanceSize values for D-, DS-, or G-series virtual machines, see [Virtual Machine and Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="5e312-148">Si vous avez conclu un accord d’entreprise avec Software Assurance et souhaitez tirer parti de Windows Server [Hybrid Use Benefit](https://azure.microsoft.com/pricing/hybrid-use-benefit/), ajoutez le paramètre **-LicenseType** à l’applet de commande **New-AzureVMConfig**, en passant la valeur **Windows_Server** pour le cas d’utilisation standard.</span><span class="sxs-lookup"><span data-stu-id="5e312-148">If you have an Enterprise Agreement with Software Assurance, and intend to take advantage of the Windows Server [Hybrid Use Benefit](https://azure.microsoft.com/pricing/hybrid-use-benefit/), add the **-LicenseType** parameter to the **New-AzureVMConfig** cmdlet, passing the value **Windows_Server** for the typical use case.</span></span>  <span data-ttu-id="5e312-149">Vérifiez que vous utilisez une image que vous avez téléchargée ; vous ne pouvez pas utiliser une image standard de la galerie avec Hybrid Use Benefit.</span><span class="sxs-lookup"><span data-stu-id="5e312-149">Be sure you are using an image you have uploaded; you cannot use a standard image from the Gallery with the Hybrid Use Benefit.</span></span>
> 
> 

<span data-ttu-id="5e312-150">Pour un ordinateur Windows autonome, vous pouvez éventuellement spécifier le compte et le mot de passe de l'administrateur local.</span><span class="sxs-lookup"><span data-stu-id="5e312-150">Optionally, for a standalone Windows computer, specify the local administrator account and password.</span></span>

    $cred=Get-Credential -Message "Type the name and password of the local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

<span data-ttu-id="5e312-151">Choisissez un mot de passe fort.</span><span class="sxs-lookup"><span data-stu-id="5e312-151">Choose a strong password.</span></span> <span data-ttu-id="5e312-152">Pour en vérifier la force, consultez la page [Password Checker : Utilisation de mots de passe forts](https://www.microsoft.com/security/pc-security/password-checker.aspx).</span><span class="sxs-lookup"><span data-stu-id="5e312-152">To check its strength, see [Password Checker: Using Strong Passwords](https://www.microsoft.com/security/pc-security/password-checker.aspx).</span></span>

<span data-ttu-id="5e312-153">Pour ajouter l’ordinateur Windows à un domaine Active Directory existant, vous pouvez éventuellement spécifier le compte et le mot de passe de l’administrateur local, le domaine, ainsi que le nom et le mot de passe d’un compte de domaine.</span><span class="sxs-lookup"><span data-stu-id="5e312-153">Optionally, to add the Windows computer to an existing Active Directory domain, specify the local administrator account and password, the domain, and the name and password of a domain account.</span></span>

    $cred1=Get-Credential –Message "Type the name and password of the local administrator account."
    $cred2=Get-Credential –Message "Now type the name (not including the domain) and password of an account that has permission to add the machine to the domain."
    $domaindns="<FQDN of the domain that the machine is joining>"
    $domacctdomain="<domain of the account that has permission to add the machine to the domain>"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

<span data-ttu-id="5e312-154">Pour connaître les autres options de préconfiguration disponibles pour les machines virtuelles Windows, consultez la syntaxe des jeux de paramètres **Windows** et **WindowsDomain** dans [Add-AzureProvisioningConfig](/powershell/module/azure/add-azureprovisioningconfig).</span><span class="sxs-lookup"><span data-stu-id="5e312-154">For additional pre-configuration options for Windows-based virtual machines, see the syntax for the **Windows** and **WindowsDomain** parameter sets in [Add-AzureProvisioningConfig](/powershell/module/azure/add-azureprovisioningconfig).</span></span>

<span data-ttu-id="5e312-155">Vous pouvez éventuellement attribuer à la machine virtuelle une adresse IP spécifique, appelée DIP statique.</span><span class="sxs-lookup"><span data-stu-id="5e312-155">Optionally, assign the virtual machine a specific IP address, known as a static DIP.</span></span>

    $vm1 | Set-AzureStaticVNetIP -IPAddress <IP address>

<span data-ttu-id="5e312-156">Vous pouvez vérifier la disponibilité d'une adresse IP particulière à l'aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5e312-156">You can verify that a specific IP address is available with:</span></span>

    Test-AzureStaticVNetIP –VNetName <VNet name> –IPAddress <IP address>

<span data-ttu-id="5e312-157">Vous pouvez éventuellement affecter la machine virtuelle à un sous-réseau spécifique dans un réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="5e312-157">Optionally, assign the virtual machine to a specific subnet in an Azure virtual network.</span></span>

    $vm1 | Set-AzureSubnet -SubnetNames "<name of the subnet>"

<span data-ttu-id="5e312-158">Vous pouvez éventuellement ajouter un disque de données unique à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5e312-158">Optionally, add a single data disk to the virtual machine.</span></span>

    $disksize=<size of the disk in GB>
    $disklabel="<the label on the disk>"
    $lun=<Logical Unit Number (LUN) of the disk>
    $hcaching="<Specify one: ReadOnly, ReadWrite, None>"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

<span data-ttu-id="5e312-159">Pour un contrôleur de domaine Active Directory, définissez $hcaching sur « Aucun ».</span><span class="sxs-lookup"><span data-stu-id="5e312-159">For an Active Directory domain controller, set $hcaching to "None".</span></span>

<span data-ttu-id="5e312-160">Vous pouvez éventuellement ajouter la machine virtuelle à un jeu à charge équilibrée existant pour le trafic externe.</span><span class="sxs-lookup"><span data-stu-id="5e312-160">Optionally, add the virtual machine to an existing load-balanced set for external traffic.</span></span>

    $protocol="<Specify one: tcp, udp>"
    $localport=<port number of the internal port>
    $pubport=<port number of the external port>
    $endpointname="<name of the endpoint>"
    $lbsetname="<name of the existing load-balanced set>"
    $probeprotocol="<Specify one: tcp, http>"
    $probeport=<TCP or HTTP port number of probe traffic>
    $probepath="<URL path for probe traffic>"
    $vm1 | Add-AzureEndpoint -Name $endpointname -Protocol $protocol -LocalPort $localport -PublicPort $pubport -LBSetName $lbsetname -ProbeProtocol $probeprotocol -ProbePort $probeport -ProbePath $probepath

<span data-ttu-id="5e312-161">Enfin, choisissez l'un de ces blocs de commande requis pour la création de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5e312-161">Finally, choose one of these required command blocks for creating the virtual machine.</span></span>

<span data-ttu-id="5e312-162">Option 1 : créez la machine virtuelle dans un service cloud existant.</span><span class="sxs-lookup"><span data-stu-id="5e312-162">Option 1: Create the virtual machine in an existing cloud service.</span></span>

    New-AzureVM –ServiceName "<short name of the cloud service>" -VMs $vm1

<span data-ttu-id="5e312-163">Le nom abrégé du service cloud est celui qui apparaît dans la liste Cloud Services dans le portail Azure ou dans la liste des groupes de ressources dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5e312-163">The short name of the cloud service is the name that appears in the list of Cloud Services in the Azure portal or in the list of Resource Groups in the Azure portal.</span></span>

<span data-ttu-id="5e312-164">Option 2 : créez la machine virtuelle dans un service cloud et un réseau virtuel existants.</span><span class="sxs-lookup"><span data-stu-id="5e312-164">Option 2: Create the virtual machine in an existing cloud service and virtual network.</span></span>

    $svcname="<short name of the cloud service>"
    $vnetname="<name of the virtual network>"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

## <a name="step-5-run-your-command-set"></a><span data-ttu-id="5e312-165">Étape 5 : exécuter votre jeu de commandes</span><span class="sxs-lookup"><span data-stu-id="5e312-165">Step 5: Run your command set</span></span>
<span data-ttu-id="5e312-166">Passez en revue le jeu de commandes Azure PowerShell que vous avez créé dans votre éditeur de texte ou dans l’environnement d’écriture de scripts intégré de PowerShell (ISE), constitué de plusieurs blocs de commandes de l’étape 4.</span><span class="sxs-lookup"><span data-stu-id="5e312-166">Review the Azure PowerShell command set you built in your text editor or the PowerShell ISE consisting of multiple blocks of commands from step 4.</span></span> <span data-ttu-id="5e312-167">Vérifiez que vous avez spécifié toutes les variables nécessaires et qu’elles ont les valeurs correctes.</span><span class="sxs-lookup"><span data-stu-id="5e312-167">Ensure that you have specified all the needed variables and that they have the correct values.</span></span> <span data-ttu-id="5e312-168">Vérifiez également que vous avez supprimé tous les caractères < et >.</span><span class="sxs-lookup"><span data-stu-id="5e312-168">Also make sure that you have removed all the < and > characters.</span></span>

<span data-ttu-id="5e312-169">Si vous utilisez un éditeur de texte, copiez le jeu de commandes dans le Presse-papiers, puis cliquez avec le bouton droit sur votre invite de commandes Windows PowerShell ouverte.</span><span class="sxs-lookup"><span data-stu-id="5e312-169">If you are using a text editor, copy the command set to the clipboard and then right-click your open Windows PowerShell command prompt.</span></span> <span data-ttu-id="5e312-170">Vous émettez ainsi le jeu de commandes en tant que série de commandes PowerShell et créez votre machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="5e312-170">This will issue the command set as a series of PowerShell commands and create your Azure virtual machine.</span></span> <span data-ttu-id="5e312-171">Vous pouvez également exécuter le jeu de commandes dans PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="5e312-171">Alternately, run the command set in the PowerShell ISE.</span></span>

<span data-ttu-id="5e312-172">Si vous comptez créer cette machine virtuelle de nouveau ou une autre similaire, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="5e312-172">If you will be creating this virtual machine again or a similar one, you can:</span></span>

* <span data-ttu-id="5e312-173">Enregistrez ce jeu de commandes en tant que fichier de script PowerShell (*.ps1).</span><span class="sxs-lookup"><span data-stu-id="5e312-173">Save this command set as a PowerShell script file (*.ps1).</span></span>
* <span data-ttu-id="5e312-174">Enregistrez ce jeu de commandes en tant que Runbook Azure Automation dans la section **Comptes Automation** du Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5e312-174">Save this command set as an Azure Automation runbook in the **Automation Accounts** section of the Azure portal.</span></span>

## <span data-ttu-id="5e312-175"><a id="examples"></a>Exemples</span><span class="sxs-lookup"><span data-stu-id="5e312-175"><a id="examples"></a>Examples</span></span>
<span data-ttu-id="5e312-176">Voici deux exemples d'utilisation des étapes ci-dessus pour créer des jeux de commandes Azure PowerShell qui créent des machines virtuelles Azure basées sur Windows.</span><span class="sxs-lookup"><span data-stu-id="5e312-176">Here are two examples of using the steps above to build Azure PowerShell command sets that create Windows-based Azure virtual machines.</span></span>

### <a name="example-1"></a><span data-ttu-id="5e312-177">Exemple 1</span><span class="sxs-lookup"><span data-stu-id="5e312-177">Example 1</span></span>
<span data-ttu-id="5e312-178">J'ai besoin d'un jeu de commandes PowerShell permettant de créer la machine virtuelle initiale pour un contrôleur de domaine Active Directory qui :</span><span class="sxs-lookup"><span data-stu-id="5e312-178">I need a PowerShell command set to create the initial virtual machine for an Active Directory domain controller that:</span></span>

* <span data-ttu-id="5e312-179">utilise l'image Windows Server 2012 R2 Datacenter</span><span class="sxs-lookup"><span data-stu-id="5e312-179">Uses the Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="5e312-180">se nomme AZDC1</span><span class="sxs-lookup"><span data-stu-id="5e312-180">Has the name AZDC1.</span></span>
* <span data-ttu-id="5e312-181">est un ordinateur autonome</span><span class="sxs-lookup"><span data-stu-id="5e312-181">Is a standalone computer.</span></span>
* <span data-ttu-id="5e312-182">comporte un disque de données supplémentaire de 20 Go</span><span class="sxs-lookup"><span data-stu-id="5e312-182">Has an additional data disk of 20 GB.</span></span>
* <span data-ttu-id="5e312-183">possède l'adresse IP statique 192.168.244.4</span><span class="sxs-lookup"><span data-stu-id="5e312-183">Has the static IP address 192.168.244.4.</span></span>
* <span data-ttu-id="5e312-184">se trouve dans le sous-réseau BackEnd du réseau virtuel AZDatacenter</span><span class="sxs-lookup"><span data-stu-id="5e312-184">Is in the BackEnd subnet of the AZDatacenter virtual network.</span></span>
* <span data-ttu-id="5e312-185">se trouve dans le service cloud Azure-TailspinToys.</span><span class="sxs-lookup"><span data-stu-id="5e312-185">Is in the Azure-TailspinToys cloud service.</span></span>

<span data-ttu-id="5e312-186">Voici le jeu de commandes Azure PowerShell correspondant qui permet de créer cette machine virtuelle. Les lignes vides entre chaque bloc offrent une meilleure lisibilité.</span><span class="sxs-lookup"><span data-stu-id="5e312-186">Here is the corresponding Azure PowerShell command set to create this virtual machine, with blank lines between each block for readability.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="AZDC1"
    $vmsize="Medium"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred=Get-Credential -Message "Type the name and password of the local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

    $vm1 | Set-AzureSubnet -SubnetNames "BackEnd"

    $vm1 | Set-AzureStaticVNetIP -IPAddress 192.168.244.4

    $disksize=20
    $disklabel="DCData"
    $lun=0
    $hcaching="None"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

    $svcname="Azure-TailspinToys"
    $vnetname="AZDatacenter"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

### <a name="example-2"></a><span data-ttu-id="5e312-187">Exemple 2</span><span class="sxs-lookup"><span data-stu-id="5e312-187">Example 2</span></span>
<span data-ttu-id="5e312-188">J'ai besoin d'un jeu de commandes PowerShell permettant de créer une machine virtuelle pour un serveur métier qui :</span><span class="sxs-lookup"><span data-stu-id="5e312-188">I need a PowerShell command set to create a virtual machine for a line-of-business server that:</span></span>

* <span data-ttu-id="5e312-189">utilise l'image Windows Server 2012 R2 Datacenter</span><span class="sxs-lookup"><span data-stu-id="5e312-189">Uses the Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="5e312-190">se nomme LOB1</span><span class="sxs-lookup"><span data-stu-id="5e312-190">Has the name LOB1.</span></span>
* <span data-ttu-id="5e312-191">appartient au domaine corp.contoso.com</span><span class="sxs-lookup"><span data-stu-id="5e312-191">Is a member of the corp.contoso.com domain.</span></span>
* <span data-ttu-id="5e312-192">comporte un disque de données supplémentaire de 200 Go</span><span class="sxs-lookup"><span data-stu-id="5e312-192">Has an additional data disk of 200 GB.</span></span>
* <span data-ttu-id="5e312-193">se trouve dans le sous-réseau FrontEnd du réseau virtuel AZDatacenter</span><span class="sxs-lookup"><span data-stu-id="5e312-193">Is in the FrontEnd subnet of the AZDatacenter virtual network.</span></span>
* <span data-ttu-id="5e312-194">se trouve dans le service cloud Azure-TailspinToys.</span><span class="sxs-lookup"><span data-stu-id="5e312-194">Is in the Azure-TailspinToys cloud service.</span></span>

<span data-ttu-id="5e312-195">Voici le jeu de commandes Azure PowerShell correspondant qui permet de créer cette machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5e312-195">Here is the corresponding Azure PowerShell command set to create this virtual machine.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="LOB1"
    $vmsize="Large"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred1=Get-Credential –Message "Type the name and password of the local administrator account."
    $cred2=Get-Credential –Message "Now type the name (not including the domain) and password of an account that has permission to add the machine to the domain."
    $domaindns="corp.contoso.com"
    $domacctdomain="CORP"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "FrontEnd"

    $disksize=200
    $disklabel="LOBData"
    $lun=0
    $hcaching="ReadWrite"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

    $svcname="Azure-TailspinToys"
    $vnetname="AZDatacenter"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname


## <a name="next-steps"></a><span data-ttu-id="5e312-196">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5e312-196">Next steps</span></span>
<span data-ttu-id="5e312-197">Si vous avez besoin d’un disque de système d’exploitation supérieur à 127 Go, vous pouvez [étendre ce dernier](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5e312-197">If you need an OS disk that is larger than 127 GB, you can [expand the OS drive](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

