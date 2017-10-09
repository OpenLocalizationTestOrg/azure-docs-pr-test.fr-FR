---
title: aaaCreate une machine virtuelle de Windows avec PowerShell | Documents Microsoft
description: "Créer des machines virtuelles Windows Azure PowerShell et le modèle de déploiement classique hello."
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
ms.openlocfilehash: 5339f458c1f08f6e1752a53191f19402fab8ea25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell-and-hello-classic-deployment-model"></a><span data-ttu-id="f3f61-103">Créer une machine virtuelle Windows avec PowerShell et hello modèle de déploiement classique</span><span class="sxs-lookup"><span data-stu-id="f3f61-103">Create a Windows virtual machine with PowerShell and hello classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f3f61-104">Portail Azure - Windows</span><span class="sxs-lookup"><span data-stu-id="f3f61-104">Azure portal - Windows</span></span>](tutorial.md)
> * [<span data-ttu-id="f3f61-105">PowerShell - Windows</span><span class="sxs-lookup"><span data-stu-id="f3f61-105">PowerShell - Windows</span></span>](create-powershell.md)
> 
> 

<br>

> [!IMPORTANT] 
> <span data-ttu-id="f3f61-106">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f3f61-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f3f61-107">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="f3f61-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="f3f61-108">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="f3f61-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="f3f61-109">Découvrez comment trop[effectuer ces étapes à l’aide du modèle de gestionnaire de ressources hello](../../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f3f61-109">Learn how too[perform these steps using hello Resource Manager model](../../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="f3f61-110">Ces étapes montrent le fonctionnement des commandes toocustomize un ensemble d’Azure PowerShell qui créer et préconfigurer une machine virtuelle Azure Windows à l’aide d’une approche de bloc de construction.</span><span class="sxs-lookup"><span data-stu-id="f3f61-110">These steps show you how toocustomize a set of Azure PowerShell commands that create and preconfigure a Windows-based Azure virtual machine by using a building block approach.</span></span> <span data-ttu-id="f3f61-111">Vous pouvez utiliser ce processus tooquickly créer un jeu de commandes pour un nouvel ordinateur virtuel basé sur Windows et développez un déploiement existant ou toocreate plusieurs commandes qui définit rapidement créer un environnement de pro informatique ou de développement et de test personnalisé.</span><span class="sxs-lookup"><span data-stu-id="f3f61-111">You can use this process tooquickly create a command set for a new Windows-based virtual machine and expand an existing deployment or toocreate multiple command sets that quickly build out a custom dev/test or IT pro environment.</span></span>

<span data-ttu-id="f3f61-112">Ces étapes utilisent une méthode de cases à remplir pour créer des jeux de commandes Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f3f61-112">These steps follow a fill-in-the-blanks approach for creating Azure PowerShell command sets.</span></span> <span data-ttu-id="f3f61-113">Cette approche peut être utile si vous êtes tooPowerShell nouveau ou vous souhaitiez tooknow le toospecify de valeurs pour la configuration réussie.</span><span class="sxs-lookup"><span data-stu-id="f3f61-113">This approach can be useful if you are new tooPowerShell or you just want tooknow what values toospecify for successful configuration.</span></span> <span data-ttu-id="f3f61-114">Les utilisateurs expérimentés PowerShell peuvent prendre les commandes hello et remplacer leurs propres valeurs pour les variables de hello (lignes hello commençant par « $»).</span><span class="sxs-lookup"><span data-stu-id="f3f61-114">Advanced PowerShell users can take hello commands and substitute their own values for hello variables (hello lines beginning with "$").</span></span>

<span data-ttu-id="f3f61-115">Si vous n’avez pas déjà fait, suivez les instructions de hello de [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="f3f61-115">If you haven't done so already, use hello instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell on your local computer.</span></span> <span data-ttu-id="f3f61-116">Puis ouvrez une invite de commandes Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f3f61-116">Then, open a Windows PowerShell command prompt.</span></span>

## <a name="step-1-add-your-account"></a><span data-ttu-id="f3f61-117">Étape 1 : Ajouter votre compte</span><span class="sxs-lookup"><span data-stu-id="f3f61-117">Step 1: Add your account</span></span>
1. <span data-ttu-id="f3f61-118">À l’invite de commandes PowerShell hello, tapez **Add-AzureAccount** et cliquez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="f3f61-118">At hello PowerShell prompt, type **Add-AzureAccount** and click **Enter**.</span></span> 
2. <span data-ttu-id="f3f61-119">Tapez hello adresse de messagerie associée à votre abonnement Azure et cliquez sur **continuer**.</span><span class="sxs-lookup"><span data-stu-id="f3f61-119">Type in hello email address associated with your Azure subscription and click **Continue**.</span></span> 
3. <span data-ttu-id="f3f61-120">Tapez hello de mot de passe pour votre compte.</span><span class="sxs-lookup"><span data-stu-id="f3f61-120">Type in hello password for your account.</span></span> 
4. <span data-ttu-id="f3f61-121">Cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="f3f61-121">Click **Sign in**.</span></span>

## <a name="step-2-set-your-subscription-and-storage-account"></a><span data-ttu-id="f3f61-122">Étape 2 : Configurer votre abonnement et votre compte de stockage</span><span class="sxs-lookup"><span data-stu-id="f3f61-122">Step 2: Set your subscription and storage account</span></span>
<span data-ttu-id="f3f61-123">Définissez votre abonnement Azure et le compte de stockage en exécutant ces commandes à l’invite de commandes Windows PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="f3f61-123">Set your Azure subscription and storage account by running these commands at hello Windows PowerShell command prompt.</span></span> <span data-ttu-id="f3f61-124">Tous les éléments entre guillemets hello, notamment hello < et >, remplacez les noms corrects hello.</span><span class="sxs-lookup"><span data-stu-id="f3f61-124">Replace everything within hello quotes, including hello < and > characters, with hello correct names.</span></span>

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

<span data-ttu-id="f3f61-125">Vous pouvez obtenir les nom d’abonnement approprié hello de hello propriété SubscriptionName de sortie hello Hello **Get-AzureSubscription** commande.</span><span class="sxs-lookup"><span data-stu-id="f3f61-125">You can get hello correct subscription name from hello SubscriptionName property of hello output of hello **Get-AzureSubscription** command.</span></span> <span data-ttu-id="f3f61-126">Vous pouvez obtenir nom de compte de stockage correct hello de hello propriété Label du résultat hello de hello **Get-AzureStorageAccount** commande une fois que vous exécutez hello **Select-AzureSubscription** commande.</span><span class="sxs-lookup"><span data-stu-id="f3f61-126">You can get hello correct storage account name from hello Label property of hello output of hello **Get-AzureStorageAccount** command after you run hello **Select-AzureSubscription** command.</span></span>

## <a name="step-3-determine-hello-imagefamily"></a><span data-ttu-id="f3f61-127">Étape 3 : Déterminer hello ImageFamily</span><span class="sxs-lookup"><span data-stu-id="f3f61-127">Step 3: Determine hello ImageFamily</span></span>
<span data-ttu-id="f3f61-128">Ensuite, vous devez toodetermine hello ImageFamily ou la valeur de l’étiquette pour hello image spécifique toohello correspondante machine virtuelle Azure, vous souhaitez toocreate.</span><span class="sxs-lookup"><span data-stu-id="f3f61-128">Next, you need toodetermine hello ImageFamily or Label value for hello specific image corresponding toohello Azure virtual machine you want toocreate.</span></span> <span data-ttu-id="f3f61-129">Vous pouvez obtenir la liste de hello de valeurs ImageFamily disponibles avec cette commande.</span><span class="sxs-lookup"><span data-stu-id="f3f61-129">You can get hello list of available ImageFamily values with this command.</span></span>

    Get-AzureVMImage | select ImageFamily -Unique

<span data-ttu-id="f3f61-130">Voici des exemples de valeurs ImageFamily pour les ordinateurs basés sur Windows :</span><span class="sxs-lookup"><span data-stu-id="f3f61-130">Here are some examples of ImageFamily values for Windows-based computers:</span></span>

* <span data-ttu-id="f3f61-131">Windows Server 2012 R2 Datacenter</span><span class="sxs-lookup"><span data-stu-id="f3f61-131">Windows Server 2012 R2 Datacenter</span></span>
* <span data-ttu-id="f3f61-132">Windows Server 2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="f3f61-132">Windows Server 2008 R2 SP1</span></span>
* <span data-ttu-id="f3f61-133">Windows Server 2016 Technical Preview 4</span><span class="sxs-lookup"><span data-stu-id="f3f61-133">Windows Server 2016 Technical Preview 4</span></span>
* <span data-ttu-id="f3f61-134">SQL Server 2012 SP1 Enterprise sur Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="f3f61-134">SQL Server 2012 SP1 Enterprise on Windows Server 2012</span></span>

<span data-ttu-id="f3f61-135">Si vous trouvez image hello que vous cherchez, ouvrez une nouvelle instance de l’éditeur de texte hello de votre choix ou de hello PowerShell Integrated Scripting Environment (ISE).</span><span class="sxs-lookup"><span data-stu-id="f3f61-135">If you find hello image you are looking for, open a fresh instance of hello text editor of your choice or hello PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="f3f61-136">Copiez suivant de hello en fichier texte hello ou hello PowerShell ISE, en remplaçant la valeur de ImageFamily hello.</span><span class="sxs-lookup"><span data-stu-id="f3f61-136">Copy hello following into hello new text file or hello PowerShell ISE, substituting hello ImageFamily value.</span></span>

    $family="<ImageFamily value>"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

<span data-ttu-id="f3f61-137">Dans certains cas, le nom d’image de hello est Bonjour propriété Label au lieu de hello ImageFamily valeur.</span><span class="sxs-lookup"><span data-stu-id="f3f61-137">In some cases, hello image name is in hello Label property instead of hello ImageFamily value.</span></span> <span data-ttu-id="f3f61-138">Si vous ne trouvez pas image hello que vous cherchez à l’aide de la propriété ImageFamily hello, la liste des images de hello par leur propriété étiquette avec cette commande.</span><span class="sxs-lookup"><span data-stu-id="f3f61-138">If you didn't find hello image that you are looking for using hello ImageFamily property, list hello images by their Label property with this command.</span></span>

    Get-AzureVMImage | select Label -Unique

<span data-ttu-id="f3f61-139">Si vous trouvez d’image de droite hello avec cette commande, ouvrez une nouvelle instance de l’éditeur de texte hello de votre choix ou de hello PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="f3f61-139">If you find hello right image with this command, open a fresh instance of hello text editor of your choice or hello PowerShell ISE.</span></span> <span data-ttu-id="f3f61-140">Copiez suivant de hello en fichier texte hello ou hello PowerShell ISE, en remplaçant la valeur de l’étiquette hello.</span><span class="sxs-lookup"><span data-stu-id="f3f61-140">Copy hello following into hello new text file or hello PowerShell ISE, substituting hello Label value.</span></span>

    $label="<Label value>"
    $image = Get-AzureVMImage | where { $_.Label -eq $label } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

## <a name="step-4-build-your-command-set"></a><span data-ttu-id="f3f61-141">Étape 4 : générer votre jeu de commandes</span><span class="sxs-lookup"><span data-stu-id="f3f61-141">Step 4: Build your command set</span></span>
<span data-ttu-id="f3f61-142">Créer reste hello de votre commande en copiant l’ensemble approprié de hello de blocs ci-dessous dans votre nouveau fichier texte ou hello ISE renseigner les valeurs des variables hello et suppression hello < et >.</span><span class="sxs-lookup"><span data-stu-id="f3f61-142">Build hello rest of your command set by copying hello appropriate set of blocks below into your new text file or hello ISE and then filling in hello variable values and removing hello < and > characters.</span></span> <span data-ttu-id="f3f61-143">Consultez hello deux [exemples](#examples) à fin hello de cet article pour avoir une idée du résultat final de hello.</span><span class="sxs-lookup"><span data-stu-id="f3f61-143">See hello two [examples](#examples) at hello end of this article for an idea of hello final result.</span></span>

<span data-ttu-id="f3f61-144">Pour commencer, choisissez l'un des deux blocs de commandes suivants (obligatoire).</span><span class="sxs-lookup"><span data-stu-id="f3f61-144">Start your command set by choosing one of these two command blocks (required).</span></span>

<span data-ttu-id="f3f61-145">Option 1 : spécifiez un nom et une taille de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f3f61-145">Option 1: Specify a virtual machine name and a size.</span></span>

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

<span data-ttu-id="f3f61-146">Option 2 : spécifiez un nom, une taille et un nom de groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="f3f61-146">Option 2: Specify a name, size, and availability set name.</span></span>

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $availset="<set name>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image -AvailabilitySetName $availset

<span data-ttu-id="f3f61-147">Pour les valeurs de InstanceSize hello pour D, DS ou machines virtuelles de série G, consultez [Machine virtuelle et les tailles de Service Cloud pour Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="f3f61-147">For hello InstanceSize values for D-, DS-, or G-series virtual machines, see [Virtual Machine and Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="f3f61-148">Si vous avez un contrat d’entreprise avec Software Assurance et que vous envisagez d’avantage tootake Hello Windows Server [hybride utilisez avantage](https://azure.microsoft.com/pricing/hybrid-use-benefit/), ajouter le **- LicenseType** paramètre toohello  **Nouveau-AzureVMConfig** applet de commande, en passant la valeur de hello **Windows_Server** hello classique pour les cas d’usage.</span><span class="sxs-lookup"><span data-stu-id="f3f61-148">If you have an Enterprise Agreement with Software Assurance, and intend tootake advantage of hello Windows Server [Hybrid Use Benefit](https://azure.microsoft.com/pricing/hybrid-use-benefit/), add the **-LicenseType** parameter toohello **New-AzureVMConfig** cmdlet, passing hello value **Windows_Server** for hello typical use case.</span></span>  <span data-ttu-id="f3f61-149">Vérifiez que vous utilisez une image que vous avez téléchargé ; Vous ne pouvez pas utiliser une image standard à partir de la galerie de hello avec hello avantage d’utiliser hybride.</span><span class="sxs-lookup"><span data-stu-id="f3f61-149">Be sure you are using an image you have uploaded; you cannot use a standard image from hello Gallery with hello Hybrid Use Benefit.</span></span>
> 
> 

<span data-ttu-id="f3f61-150">Si vous le souhaitez, pour un ordinateur Windows autonome, vous devez spécifier un mot de passe et le compte d’administrateur local hello.</span><span class="sxs-lookup"><span data-stu-id="f3f61-150">Optionally, for a standalone Windows computer, specify hello local administrator account and password.</span></span>

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

<span data-ttu-id="f3f61-151">Choisissez un mot de passe fort.</span><span class="sxs-lookup"><span data-stu-id="f3f61-151">Choose a strong password.</span></span> <span data-ttu-id="f3f61-152">toocheck sa force, consultez [vérificateur de mot de passe : à l’aide de mots de passe forts](https://www.microsoft.com/security/pc-security/password-checker.aspx).</span><span class="sxs-lookup"><span data-stu-id="f3f61-152">toocheck its strength, see [Password Checker: Using Strong Passwords](https://www.microsoft.com/security/pc-security/password-checker.aspx).</span></span>

<span data-ttu-id="f3f61-153">Si vous le souhaitez, tooadd hello Windows ordinateur tooan domaine Active Directory existant, spécifiez le compte d’administrateur local hello et de mot de passe, de domaine hello et de nom de hello et de mot de passe d’un compte de domaine.</span><span class="sxs-lookup"><span data-stu-id="f3f61-153">Optionally, tooadd hello Windows computer tooan existing Active Directory domain, specify hello local administrator account and password, hello domain, and hello name and password of a domain account.</span></span>

    $cred1=Get-Credential –Message "Type hello name and password of hello local administrator account."
    $cred2=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account that has permission tooadd hello machine toohello domain."
    $domaindns="<FQDN of hello domain that hello machine is joining>"
    $domacctdomain="<domain of hello account that has permission tooadd hello machine toohello domain>"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

<span data-ttu-id="f3f61-154">Pour d’autres options de configuration préalable pour les ordinateurs virtuels basés sur Windows, consultez la syntaxe hello pour hello **Windows** et **WindowsDomain** paramètre définit [ Ajouter-AzureProvisioningConfig](/powershell/module/azure/add-azureprovisioningconfig).</span><span class="sxs-lookup"><span data-stu-id="f3f61-154">For additional pre-configuration options for Windows-based virtual machines, see hello syntax for hello **Windows** and **WindowsDomain** parameter sets in [Add-AzureProvisioningConfig](/powershell/module/azure/add-azureprovisioningconfig).</span></span>

<span data-ttu-id="f3f61-155">Assignez éventuellement une machine virtuelle hello une adresse IP spécifique, appelée une adresse DIP statique.</span><span class="sxs-lookup"><span data-stu-id="f3f61-155">Optionally, assign hello virtual machine a specific IP address, known as a static DIP.</span></span>

    $vm1 | Set-AzureStaticVNetIP -IPAddress <IP address>

<span data-ttu-id="f3f61-156">Vous pouvez vérifier la disponibilité d'une adresse IP particulière à l'aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f3f61-156">You can verify that a specific IP address is available with:</span></span>

    Test-AzureStaticVNetIP –VNetName <VNet name> –IPAddress <IP address>

<span data-ttu-id="f3f61-157">Assignez éventuellement sous-réseau spécifique du tooa hello machine virtuelle dans un réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="f3f61-157">Optionally, assign hello virtual machine tooa specific subnet in an Azure virtual network.</span></span>

    $vm1 | Set-AzureSubnet -SubnetNames "<name of hello subnet>"

<span data-ttu-id="f3f61-158">Si vous le souhaitez, ajoutez un ordinateur virtuel de données unique disque toohello.</span><span class="sxs-lookup"><span data-stu-id="f3f61-158">Optionally, add a single data disk toohello virtual machine.</span></span>

    $disksize=<size of hello disk in GB>
    $disklabel="<hello label on hello disk>"
    $lun=<Logical Unit Number (LUN) of hello disk>
    $hcaching="<Specify one: ReadOnly, ReadWrite, None>"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

<span data-ttu-id="f3f61-159">Pour un contrôleur de domaine Active Directory, définissez $hcaching trop « None ».</span><span class="sxs-lookup"><span data-stu-id="f3f61-159">For an Active Directory domain controller, set $hcaching too"None".</span></span>

<span data-ttu-id="f3f61-160">Si vous le souhaitez, ajoutez hello tooan existant équilibrée ensemble de machines virtuelles pour le trafic externe.</span><span class="sxs-lookup"><span data-stu-id="f3f61-160">Optionally, add hello virtual machine tooan existing load-balanced set for external traffic.</span></span>

    $protocol="<Specify one: tcp, udp>"
    $localport=<port number of hello internal port>
    $pubport=<port number of hello external port>
    $endpointname="<name of hello endpoint>"
    $lbsetname="<name of hello existing load-balanced set>"
    $probeprotocol="<Specify one: tcp, http>"
    $probeport=<TCP or HTTP port number of probe traffic>
    $probepath="<URL path for probe traffic>"
    $vm1 | Add-AzureEndpoint -Name $endpointname -Protocol $protocol -LocalPort $localport -PublicPort $pubport -LBSetName $lbsetname -ProbeProtocol $probeprotocol -ProbePort $probeport -ProbePath $probepath

<span data-ttu-id="f3f61-161">Enfin, choisissez un de ces blocs de commande requis pour la création d’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="f3f61-161">Finally, choose one of these required command blocks for creating hello virtual machine.</span></span>

<span data-ttu-id="f3f61-162">Option 1 : Créer une machine virtuelle de hello dans un service cloud existant.</span><span class="sxs-lookup"><span data-stu-id="f3f61-162">Option 1: Create hello virtual machine in an existing cloud service.</span></span>

    New-AzureVM –ServiceName "<short name of hello cloud service>" -VMs $vm1

<span data-ttu-id="f3f61-163">nom court de Hello du service de cloud hello est nom hello qui apparaît dans la liste hello de Services de cloud computing dans hello portail Azure ou dans liste hello des groupes de ressources hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f3f61-163">hello short name of hello cloud service is hello name that appears in hello list of Cloud Services in hello Azure portal or in hello list of Resource Groups in hello Azure portal.</span></span>

<span data-ttu-id="f3f61-164">Option 2 : Créer hello virtuels dans un service cloud existant et le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f3f61-164">Option 2: Create hello virtual machine in an existing cloud service and virtual network.</span></span>

    $svcname="<short name of hello cloud service>"
    $vnetname="<name of hello virtual network>"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

## <a name="step-5-run-your-command-set"></a><span data-ttu-id="f3f61-165">Étape 5 : exécuter votre jeu de commandes</span><span class="sxs-lookup"><span data-stu-id="f3f61-165">Step 5: Run your command set</span></span>
<span data-ttu-id="f3f61-166">Passez en revue le jeu de commandes Azure PowerShell hello créé dans votre éditeur de texte ou hello PowerShell ISE composé de plusieurs blocs de commandes à partir de l’étape 4.</span><span class="sxs-lookup"><span data-stu-id="f3f61-166">Review hello Azure PowerShell command set you built in your text editor or hello PowerShell ISE consisting of multiple blocks of commands from step 4.</span></span> <span data-ttu-id="f3f61-167">Assurez-vous que vous avez spécifié toutes les variables hello nécessité et ont les valeurs correctes hello.</span><span class="sxs-lookup"><span data-stu-id="f3f61-167">Ensure that you have specified all hello needed variables and that they have hello correct values.</span></span> <span data-ttu-id="f3f61-168">Assurez-vous également que vous avez supprimé tous les hello < et > caractères.</span><span class="sxs-lookup"><span data-stu-id="f3f61-168">Also make sure that you have removed all hello < and > characters.</span></span>

<span data-ttu-id="f3f61-169">Si vous utilisez un éditeur de texte, copie hello commande définir toohello Presse-papiers et puis cliquez sur votre invite de commandes Windows PowerShell ouverte.</span><span class="sxs-lookup"><span data-stu-id="f3f61-169">If you are using a text editor, copy hello command set toohello clipboard and then right-click your open Windows PowerShell command prompt.</span></span> <span data-ttu-id="f3f61-170">Cela émettre un jeu de commandes hello comme une série de commandes PowerShell et créez votre machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="f3f61-170">This will issue hello command set as a series of PowerShell commands and create your Azure virtual machine.</span></span> <span data-ttu-id="f3f61-171">Vous pouvez également exécuter commande hello Bonjour PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="f3f61-171">Alternately, run hello command set in hello PowerShell ISE.</span></span>

<span data-ttu-id="f3f61-172">Si vous comptez créer cette machine virtuelle de nouveau ou une autre similaire, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="f3f61-172">If you will be creating this virtual machine again or a similar one, you can:</span></span>

* <span data-ttu-id="f3f61-173">Enregistrez ce jeu de commandes en tant que fichier de script PowerShell (*.ps1).</span><span class="sxs-lookup"><span data-stu-id="f3f61-173">Save this command set as a PowerShell script file (*.ps1).</span></span>
* <span data-ttu-id="f3f61-174">Enregistrer cette commande défini comme un runbook Azure Automation Bonjour **comptes Automation** section Hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f3f61-174">Save this command set as an Azure Automation runbook in hello **Automation Accounts** section of hello Azure portal.</span></span>

## <span data-ttu-id="f3f61-175"><a id="examples"></a>Exemples</span><span class="sxs-lookup"><span data-stu-id="f3f61-175"><a id="examples"></a>Examples</span></span>
<span data-ttu-id="f3f61-176">Voici deux exemples d’étapes de hello ci-dessus toobuild des ensembles de commandes Azure PowerShell qui créent des machines virtuelles basées sur Windows.</span><span class="sxs-lookup"><span data-stu-id="f3f61-176">Here are two examples of using hello steps above toobuild Azure PowerShell command sets that create Windows-based Azure virtual machines.</span></span>

### <a name="example-1"></a><span data-ttu-id="f3f61-177">Exemple 1</span><span class="sxs-lookup"><span data-stu-id="f3f61-177">Example 1</span></span>
<span data-ttu-id="f3f61-178">J’ai besoin d’un PowerShell toocreate hello machine virtuelle initiale pour un contrôleur de domaine Active Directory de commande de définir :</span><span class="sxs-lookup"><span data-stu-id="f3f61-178">I need a PowerShell command set toocreate hello initial virtual machine for an Active Directory domain controller that:</span></span>

* <span data-ttu-id="f3f61-179">Utilise l’image de Windows Server 2012 R2 Datacenter hello.</span><span class="sxs-lookup"><span data-stu-id="f3f61-179">Uses hello Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="f3f61-180">A le nom hello AZDC1.</span><span class="sxs-lookup"><span data-stu-id="f3f61-180">Has hello name AZDC1.</span></span>
* <span data-ttu-id="f3f61-181">est un ordinateur autonome</span><span class="sxs-lookup"><span data-stu-id="f3f61-181">Is a standalone computer.</span></span>
* <span data-ttu-id="f3f61-182">comporte un disque de données supplémentaire de 20 Go</span><span class="sxs-lookup"><span data-stu-id="f3f61-182">Has an additional data disk of 20 GB.</span></span>
* <span data-ttu-id="f3f61-183">A hello d’adresse IP statique 192.168.244.4.</span><span class="sxs-lookup"><span data-stu-id="f3f61-183">Has hello static IP address 192.168.244.4.</span></span>
* <span data-ttu-id="f3f61-184">Est dans un sous-réseau de principal de hello du réseau virtuel de AZDatacenter hello.</span><span class="sxs-lookup"><span data-stu-id="f3f61-184">Is in hello BackEnd subnet of hello AZDatacenter virtual network.</span></span>
* <span data-ttu-id="f3f61-185">Est en hello TailspinToys-Azure cloud service.</span><span class="sxs-lookup"><span data-stu-id="f3f61-185">Is in hello Azure-TailspinToys cloud service.</span></span>

<span data-ttu-id="f3f61-186">Voici toocreate Azure PowerShell correspondante du jeu de commande hello cet ordinateur virtuel, des lignes vides entre chaque bloc pour une meilleure lisibilité.</span><span class="sxs-lookup"><span data-stu-id="f3f61-186">Here is hello corresponding Azure PowerShell command set toocreate this virtual machine, with blank lines between each block for readability.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="AZDC1"
    $vmsize="Medium"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
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

### <a name="example-2"></a><span data-ttu-id="f3f61-187">Exemple 2</span><span class="sxs-lookup"><span data-stu-id="f3f61-187">Example 2</span></span>
<span data-ttu-id="f3f61-188">J’ai besoin d’un PowerShell commande définir toocreate un ordinateur virtuel pour un serveur de métier qui :</span><span class="sxs-lookup"><span data-stu-id="f3f61-188">I need a PowerShell command set toocreate a virtual machine for a line-of-business server that:</span></span>

* <span data-ttu-id="f3f61-189">Utilise l’image de Windows Server 2012 R2 Datacenter hello.</span><span class="sxs-lookup"><span data-stu-id="f3f61-189">Uses hello Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="f3f61-190">A le nom hello LOB1.</span><span class="sxs-lookup"><span data-stu-id="f3f61-190">Has hello name LOB1.</span></span>
* <span data-ttu-id="f3f61-191">Est un membre du domaine corp.contoso.com de hello.</span><span class="sxs-lookup"><span data-stu-id="f3f61-191">Is a member of hello corp.contoso.com domain.</span></span>
* <span data-ttu-id="f3f61-192">comporte un disque de données supplémentaire de 200 Go</span><span class="sxs-lookup"><span data-stu-id="f3f61-192">Has an additional data disk of 200 GB.</span></span>
* <span data-ttu-id="f3f61-193">Est dans le sous-réseau du serveur frontal hello du réseau virtuel de AZDatacenter hello.</span><span class="sxs-lookup"><span data-stu-id="f3f61-193">Is in hello FrontEnd subnet of hello AZDatacenter virtual network.</span></span>
* <span data-ttu-id="f3f61-194">Est en hello TailspinToys-Azure cloud service.</span><span class="sxs-lookup"><span data-stu-id="f3f61-194">Is in hello Azure-TailspinToys cloud service.</span></span>

<span data-ttu-id="f3f61-195">Voici toocreate Azure PowerShell correspondante du jeu de commande hello cet ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="f3f61-195">Here is hello corresponding Azure PowerShell command set toocreate this virtual machine.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="LOB1"
    $vmsize="Large"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred1=Get-Credential –Message "Type hello name and password of hello local administrator account."
    $cred2=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account that has permission tooadd hello machine toohello domain."
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


## <a name="next-steps"></a><span data-ttu-id="f3f61-196">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f3f61-196">Next steps</span></span>
<span data-ttu-id="f3f61-197">Si vous avez besoin d’un disque de système d’exploitation qui est supérieur à 127 Go, vous pouvez [développez hello du système d’exploitation disque](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f3f61-197">If you need an OS disk that is larger than 127 GB, you can [expand hello OS drive](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

