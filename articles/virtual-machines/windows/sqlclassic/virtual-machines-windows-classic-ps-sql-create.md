---
title: aaaCreate une Machine virtuelle de SQL Server dans Azure PowerShell (classiques) | Documents Microsoft
description: "Fournit une procédure et des scripts PowerShell pour la création d’une machine virtuelle Azure à l’aide des images de la galerie de machines virtuelles SQL Server. Cette rubrique utilise le mode de déploiement classique hello."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-service-management
ms.assetid: b73be387-9323-4e08-be53-6e5928e3786e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.openlocfilehash: b14d5d9bc192fa0a21126395ee20ffd06b3bf47d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-classic"></a><span data-ttu-id="b2e4d-104">Approvisionner une machine virtuelle SQL Server à l’aide d’Azure PowerShell (Classic)</span><span class="sxs-lookup"><span data-stu-id="b2e4d-104">Provision a SQL Server virtual machine using Azure PowerShell (Classic)</span></span>

<span data-ttu-id="b2e4d-105">Cet article explique comment un ordinateur virtuel de SQL Server dans Azure à l’aide de toocreate hello applets de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b2e4d-105">This article provides steps for how toocreate a SQL Server virtual machine in Azure by using hello PowerShell cmdlets.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="b2e4d-106">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b2e4d-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="b2e4d-107">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="b2e4d-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="b2e4d-108">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="b2e4d-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="b2e4d-109">Version de gestionnaire de ressources hello de cette rubrique, consultez [configurer un ordinateur virtuel de SQL Server à l’aide du Gestionnaire de ressources Azure PowerShell](../sql/virtual-machines-windows-ps-sql-create.md).</span><span class="sxs-lookup"><span data-stu-id="b2e4d-109">For hello Resource Manager version of this topic, see [Provision a SQL Server virtual machine using Azure PowerShell Resource Manager](../sql/virtual-machines-windows-ps-sql-create.md).</span></span>

### <a name="install-and-configure-powershell"></a><span data-ttu-id="b2e4d-110">Installation et configuration de PowerShell :</span><span class="sxs-lookup"><span data-stu-id="b2e4d-110">Install and configure PowerShell:</span></span>
1. <span data-ttu-id="b2e4d-111">Si vous n'avez pas de compte Azure, visitez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b2e4d-111">If you do not have an Azure account, visit [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
2. <span data-ttu-id="b2e4d-112">[Téléchargez et installez les commandes Azure PowerShell dernière hello](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b2e4d-112">[Download and install hello latest Azure PowerShell commands](/powershell/azure/overview).</span></span>
3. <span data-ttu-id="b2e4d-113">Démarrez Windows PowerShell et le connecter tooyour abonnement Azure avec hello **Add-AzureAccount** commande.</span><span class="sxs-lookup"><span data-stu-id="b2e4d-113">Start Windows PowerShell, and connect it tooyour Azure subscription with hello **Add-AzureAccount** command.</span></span>

   ```powershell
   Add-AzureAccount
   ```

## <a name="determine-your-target-azure-region"></a><span data-ttu-id="b2e4d-114">Déterminer votre région Azure cible</span><span class="sxs-lookup"><span data-stu-id="b2e4d-114">Determine your target Azure region</span></span>

<span data-ttu-id="b2e4d-115">Votre machine virtuelle SQL Server est hébergée dans un service cloud qui se trouve dans une région Azure spécifique.</span><span class="sxs-lookup"><span data-stu-id="b2e4d-115">Your SQL Server Virtual Machine will be hosted in a cloud service that resides a specific Azure region.</span></span> <span data-ttu-id="b2e4d-116">Hello suit aider à vous toodetermine votre région, le compte de stockage et le service cloud qui sera utilisé pour le reste de hello du didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="b2e4d-116">hello following steps help you toodetermine your region, storage account, and cloud service that will be used for hello rest of hello tutorial.</span></span>

1. <span data-ttu-id="b2e4d-117">Déterminer le centre de données hello que vous souhaitez toouse toohost votre machine virtuelle SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b2e4d-117">Determine hello data center that you want toouse toohost your SQL Server VM.</span></span> <span data-ttu-id="b2e4d-118">Hello PowerShell commande suivante affiche une liste de noms de région disponible.</span><span class="sxs-lookup"><span data-stu-id="b2e4d-118">hello following PowerShell command displays a list of available region names.</span></span>

   ```powershell
   (Get-AzureLocation).Name
   ```

2. <span data-ttu-id="b2e4d-119">Une fois que vous avez identifié l’emplacement par défaut, définissez une variable nommée **$dcLocation** toothat région.</span><span class="sxs-lookup"><span data-stu-id="b2e4d-119">Once you've identified your preferred location, set a variable named **$dcLocation** toothat region.</span></span> <span data-ttu-id="b2e4d-120">Par exemple, hello jeux hello région trop de commande suivante « États-Unis » :</span><span class="sxs-lookup"><span data-stu-id="b2e4d-120">For example, hello following command sets hello region too"East US":</span></span>

   ```powershell
   $dcLocation = "East US"
   ```

## <a name="set-your-subscription-and-storage-account"></a><span data-ttu-id="b2e4d-121">Configuration de votre compte d'abonnement et de stockage</span><span class="sxs-lookup"><span data-stu-id="b2e4d-121">Set your subscription and storage account</span></span>

1. <span data-ttu-id="b2e4d-122">Déterminer hello abonnement Azure, vous allez utiliser pour la machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="b2e4d-122">Determine hello Azure subscription you will use for hello new virtual machine.</span></span>

   ```powershell
   (Get-AzureSubscription).SubscriptionName
   ```

2. <span data-ttu-id="b2e4d-123">Affecter votre toohello d’abonnement Azure cible **$subscr** variable.</span><span class="sxs-lookup"><span data-stu-id="b2e4d-123">Assign your target Azure subscription toohello **$subscr** variable.</span></span> <span data-ttu-id="b2e4d-124">Définissez cet abonnement comme votre abonnement Azure actuel.</span><span class="sxs-lookup"><span data-stu-id="b2e4d-124">Then set this as your current Azure subscription.</span></span>

   ```powershell
   $subscr="<subscription name>"
   Select-AzureSubscription -SubscriptionName $subscr –Current
   ```

3. <span data-ttu-id="b2e4d-125">Recherchez ensuite des comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="b2e4d-125">Then check for existing storage accounts.</span></span> <span data-ttu-id="b2e4d-126">Hello script suivant affiche tous les comptes de stockage qui existent dans votre région choisie :</span><span class="sxs-lookup"><span data-stu-id="b2e4d-126">hello following script displays all storage accounts that exist in your chosen region:</span></span>

   ```powershell
   (Get-AzureStorageAccount | where { $_.GeoPrimaryLocation -eq $dcLocation }).StorageAccountName
   ```

   > [!NOTE]
   > <span data-ttu-id="b2e4d-127">Si vous avez besoin d’un compte de stockage, d’abord créer un nom de compte de stockage de toutes les minuscules avec la commande hello New-AzureStorageAccount comme hello l’exemple suivant :`New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`</span><span class="sxs-lookup"><span data-stu-id="b2e4d-127">If you require a new storage account, first create an all-lower-case storage account name with hello New-AzureStorageAccount command as in hello following example: `New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`</span></span>

4. <span data-ttu-id="b2e4d-128">Affecter hello cible stockage compte nom toohello **$staccount**.</span><span class="sxs-lookup"><span data-stu-id="b2e4d-128">Assign hello target storage account name toohello **$staccount**.</span></span> <span data-ttu-id="b2e4d-129">Utilisez ensuite **Set-AzureSubscription** tooset hello abonnement et compte de stockage actif.</span><span class="sxs-lookup"><span data-stu-id="b2e4d-129">Then use **Set-AzureSubscription** tooset hello subscription and current storage account.</span></span>

   ```powershell
   $staccount="<storage account name>"
   Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount
   ```

## <a name="select-a-sql-server-virtual-machine-image"></a><span data-ttu-id="b2e4d-130">Sélectionner une image de machine virtuelle SQL Server</span><span class="sxs-lookup"><span data-stu-id="b2e4d-130">Select a SQL Server virtual machine image</span></span>

1. <span data-ttu-id="b2e4d-131">Découvrez la liste hello des images de machines virtuelles SQL Server disponibles à partir de la galerie de hello.</span><span class="sxs-lookup"><span data-stu-id="b2e4d-131">Find out hello list of available SQL Server virtual machines images from hello gallery.</span></span> <span data-ttu-id="b2e4d-132">Ces images ont toutes la propriété **ImageFamily** qui commence par « SQL ».</span><span class="sxs-lookup"><span data-stu-id="b2e4d-132">These images all have an **ImageFamily** property that starts with "SQL".</span></span> <span data-ttu-id="b2e4d-133">suivant de Hello de requête affiche hello image famille disponible tooyou que SQL Server est préinstallé.</span><span class="sxs-lookup"><span data-stu-id="b2e4d-133">hello following query displays hello image family available tooyou that have SQL Server preinstalled.</span></span>

   ```powershell
   Get-AzureVMImage | where { $_.ImageFamily -like "SQL*" } | select ImageFamily -Unique | Sort-Object -Property ImageFamily
   ```

2. <span data-ttu-id="b2e4d-134">Lorsque vous trouvez la famille d’image de machine virtuelle hello, cette famille peuvent avoir plusieurs images publiées.</span><span class="sxs-lookup"><span data-stu-id="b2e4d-134">When you find hello  virtual machine image family, there could be multiple published images in this family.</span></span> <span data-ttu-id="b2e4d-135">Toofind hello plus récente publiée image nom de machine virtuelle pour votre famille de l’image sélectionnée de script suivant de hello utilisez (telles que **SQL Server 2016 RTM Enterprise sur Windows Server 2012 R2**) :</span><span class="sxs-lookup"><span data-stu-id="b2e4d-135">Use hello following script toofind hello latest published virtual machine image name for your selected image family (such as **SQL Server 2016 RTM Enterprise on Windows Server 2012 R2**):</span></span>

   ```powershell
   $family="<ImageFamily value>"
   $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

   echo "Selected SQL Server image name:"
   echo "   $image"
   ```

## <a name="create-hello-virtual-machine"></a><span data-ttu-id="b2e4d-136">Créer la machine virtuelle de hello</span><span class="sxs-lookup"><span data-stu-id="b2e4d-136">Create hello virtual machine</span></span>

<span data-ttu-id="b2e4d-137">Enfin, créer hello machine virtuelle avec PowerShell :</span><span class="sxs-lookup"><span data-stu-id="b2e4d-137">Finally, create hello virtual machine with PowerShell:</span></span>

1. <span data-ttu-id="b2e4d-138">Créer un cloud service toohost hello nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b2e4d-138">Create a cloud service toohost hello new VM.</span></span> <span data-ttu-id="b2e4d-139">Notez qu’il est également possible de toouse un service cloud existant à la place.</span><span class="sxs-lookup"><span data-stu-id="b2e4d-139">Note that it is also possible toouse an existing cloud service instead.</span></span> <span data-ttu-id="b2e4d-140">Créer une nouvelle variable **$svcname** avec le nom court de hello du service de cloud hello.</span><span class="sxs-lookup"><span data-stu-id="b2e4d-140">Create a new variable **$svcname** with hello short name of hello cloud service.</span></span>

   ```powershell
   $svcname = "<cloud service name>"
   New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation
   ```

2. <span data-ttu-id="b2e4d-141">Spécifiez le nom d’ordinateur virtuel hello et une taille.</span><span class="sxs-lookup"><span data-stu-id="b2e4d-141">Specify hello virtual machine name and a size.</span></span> <span data-ttu-id="b2e4d-142">Pour plus d’informations sur les tailles de machines virtuelles, voir [Tailles de machines virtuelles pour Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b2e4d-142">For more information about virtual machine sizes, see [Virtual Machine Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

   ```powershell
   $vmname="<machine name>"
   $vmsize="<Specify one: Large, ExtraLarge, A5, A6, A7, A8, A9, or see hello link toohello other VM sizes>"
   $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image
   ```

3. <span data-ttu-id="b2e4d-143">Spécifiez le mot de passe et le compte d’administrateur local hello.</span><span class="sxs-lookup"><span data-stu-id="b2e4d-143">Specify hello local administrator account and password.</span></span>

   ```powershell
   $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
   $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password
   ```

4. <span data-ttu-id="b2e4d-144">Exécutez hello suivant la machine virtuelle de script toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="b2e4d-144">Run hello following script toocreate hello virtual machine.</span></span>

   ```powershell
   New-AzureVM –ServiceName $svcname -VMs $vm1
   ```

> [!NOTE]
> <span data-ttu-id="b2e4d-145">Pour une explication supplémentaire et les options de configuration, consultez hello **créer votre jeu de commandes** section [toocreate d’utiliser Azure PowerShell et préconfigurer des Machines virtuelles basées sur Windows](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b2e4d-145">For additional explanation and configuration options, see hello **Build your command set** section in [Use Azure PowerShell toocreate and preconfigure Windows-based Virtual Machines](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="example-powershell-script"></a><span data-ttu-id="b2e4d-146">Exemple de script PowerShell</span><span class="sxs-lookup"><span data-stu-id="b2e4d-146">Example PowerShell script</span></span>

<span data-ttu-id="b2e4d-147">Hello script suivant fournit un exemple de script complet qui crée un **SQL Server 2016 RTM Enterprise sur Windows Server 2012 R2** machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b2e4d-147">hello following script provides an example of a complete script that creates a **SQL Server 2016 RTM Enterprise on Windows Server 2012 R2** virtual machine.</span></span> <span data-ttu-id="b2e4d-148">Si vous utilisez ce script, vous devez personnaliser les variables initiale hello en suivant les étapes précédentes hello dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="b2e4d-148">If you use this script, you must customize hello initial variables based on hello previous steps in this topic.</span></span>

```powershell
# Customize these variables based on your settings and requirements:
$dcLocation = "East US"
$subscr="mysubscription"
$staccount="mystorageaccount"
$family="SQL Server 2016 RTM Enterprise on Windows Server 2012 R2"
$svcname = "mycloudservice"
$vmname="myvirtualmachine"
$vmsize="A5"

# Set hello current subscription and storage account
# Comment out hello New-AzureStorageAccount line if hello account already exists
Select-AzureSubscription -SubscriptionName $subscr –Current
New-AzureStorageAccount -StorageAccountName $staccount -Location $dcLocation
Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

# Select hello most recent VM image in this image family:
$image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

# Create hello new cloud service; comment out this line if cloud service exists already:
New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation

# Create hello VM config:
$vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

# Set administrator credentials:
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password

# Create hello SQL Server VM:
New-AzureVM –ServiceName $svcname -VMs $vm1
```

## <a name="connect-with-remote-desktop"></a><span data-ttu-id="b2e4d-149">Connexion avec le Bureau à distance</span><span class="sxs-lookup"><span data-stu-id="b2e4d-149">Connect with remote desktop</span></span>

1. <span data-ttu-id="b2e4d-150">Créer des fichiers RDP hello dans toolaunch de dossier de document de l’utilisateur actuel hello ces toocomplete le programme d’installation les machines virtuelles :</span><span class="sxs-lookup"><span data-stu-id="b2e4d-150">Create hello RDP files in hello current user's document folder toolaunch these virtual machines toocomplete setup:</span></span>

   ```powershell
   $documentspath = [environment]::getfolderpath("mydocuments")
   Get-AzureRemoteDesktopFile -ServiceName $svcname -Name $vmname -LocalPath "$documentspath\vm1.rdp"
   ```

2. <span data-ttu-id="b2e4d-151">Dans le répertoire documents de hello, lancez le fichier RDP de hello.</span><span class="sxs-lookup"><span data-stu-id="b2e4d-151">In hello documents directory, launch hello RDP file.</span></span> <span data-ttu-id="b2e4d-152">Se connecter avec un nom d’utilisateur administrateur hello et le mot de passe fourni précédemment (par exemple, si votre nom d’utilisateur a été VMAdmin, spécifiez « \VMAdmin » en tant qu’utilisateur de hello et fournir le mot de passe hello).</span><span class="sxs-lookup"><span data-stu-id="b2e4d-152">Connect with hello administrator user name and password provided earlier (for example, if your user name was VMAdmin, specify "\VMAdmin" as hello user and provide hello password).</span></span>

   ```powershell
   cd $documentspath
   .\vm1.rdp
   ```

## <a name="complete-hello-configuration-of-hello-sql-server-machine-for-remote-access"></a><span data-ttu-id="b2e4d-153">Configuration terminée hello Hello ordinateur SQL Server pour l’accès à distance</span><span class="sxs-lookup"><span data-stu-id="b2e4d-153">Complete hello configuration of hello SQL Server Machine for remote access</span></span>

<span data-ttu-id="b2e4d-154">Une fois connecté sur l’ordinateur toohello avec le Bureau à distance, configurer SQL Server en fonction des instructions hello dans [étapes requises pour configurer la connectivité de SQL Server dans une machine virtuelle Azure](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="b2e4d-154">After logging on toohello machine with remote desktop, configure SQL Server based on hello instructions in [Steps for configuring SQL Server connectivity in an Azure VM](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2e4d-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b2e4d-155">Next steps</span></span>

<span data-ttu-id="b2e4d-156">Vous trouverez des instructions supplémentaires pour la configuration des machines virtuelles avec PowerShell Bonjour [documentation de machines virtuelles](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b2e4d-156">You can find additional instructions for provisioning virtual machines with PowerShell in hello [virtual machines documentation](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="b2e4d-157">Dans de nombreux cas, étape suivante de hello est toomigrate toothis de vos bases de données nouvelle machine virtuelle de serveur SQL.</span><span class="sxs-lookup"><span data-stu-id="b2e4d-157">In many cases, hello next step is toomigrate your databases toothis new SQL Server VM.</span></span> <span data-ttu-id="b2e4d-158">Pour obtenir des conseils de migration de base de données, consultez [migrer une base de données de tooSQL Server sur une machine virtuelle Azure](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b2e4d-158">For database migration guidance, see [Migrating a Database tooSQL Server on an Azure VM](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>

<span data-ttu-id="b2e4d-159">Si vous êtes également intéressé par l’utilisation de hello toocreate portail Azure Machines virtuelles SQL, consultez [approvisionnement d’une Machine virtuelle de SQL Server sur Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="b2e4d-159">If you're also interested in using hello Azure portal toocreate SQL Virtual Machines, see [Provisioning a SQL Server Virtual Machine on Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).</span></span> <span data-ttu-id="b2e4d-160">Notez ce didacticiel hello que vous via le portail de hello crée des machines virtuelles à l’aide de parcours hello recommandée modèle du Gestionnaire de ressources, plutôt que classique hello utilisé dans cette rubrique de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b2e4d-160">Note that hello tutorial that walks you through hello portal creates VMs using hello recommended Resource Manager model, rather than hello classic model used in this PowerShell topic.</span></span>

<span data-ttu-id="b2e4d-161">En outre des ressources toothese, nous vous recommandons de consulter [autres rubriques liées toorunning SQL Server dans Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b2e4d-161">In addition toothese resources, we recommend that you review [other topics related toorunning SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
