---
title: "aaaConfigure hello toujours sur le groupe de disponibilité sur une machine virtuelle de Azure à l’aide de PowerShell | Documents Microsoft"
description: "Ce didacticiel utilise des ressources qui ont été créées avec le modèle de déploiement classique hello. Vous utilisez PowerShell toocreate un groupe de disponibilité Always On dans Azure."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a4e2f175-fe56-4218-86c7-a43fb916cc64
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: d4a27e203b2ff299adebec2b010c03422459b3c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-always-on-availability-group-on-an-azure-vm-with-powershell"></a><span data-ttu-id="d7d2e-104">Configurer hello Always On groupe de disponibilité sur une machine virtuelle de Azure avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="d7d2e-104">Configure hello Always On availability group on an Azure VM with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d7d2e-105">Classic : interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="d7d2e-105">Classic: UI</span></span>](../classic/portal-sql-alwayson-availability-groups.md)
> * <span data-ttu-id="d7d2e-106">[Classic : PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
</span><span class="sxs-lookup"><span data-stu-id="d7d2e-106">[Classic: PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
</span></span><br/>

<span data-ttu-id="d7d2e-107">Avant de commencer, rappelez-vous que vous pouvez accomplir cette tâche dans le modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-107">Before you begin, consider that you can now complete this task in Azure resource manager model.</span></span> <span data-ttu-id="d7d2e-108">Nous vous recommandons d’utiliser le modèle Azure Resource Manager pour les nouveaux déploiements.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-108">We recommend Azure resource manager model for new deployments.</span></span> <span data-ttu-id="d7d2e-109">Consultez [Présentation des groupes de disponibilité SQL Server AlwaysOn sur des machines virtuelles Azure](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d7d2e-109">See [SQL Server Always On availability groups on Azure virtual machines](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d7d2e-110">Nous recommandons que la plupart des nouveaux déploiements utilisent le modèle de gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-110">We recommend that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="d7d2e-111">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d7d2e-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d7d2e-112">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-112">This article covers using hello classic deployment model.</span></span>

<span data-ttu-id="d7d2e-113">Machines virtuelles (VM) Azure peut aider le coût de base de données administrateurs toolower hello d’un système de SQL Server haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-113">Azure virtual machines (VMs) can help database administrators toolower hello cost of a high-availability SQL Server system.</span></span> <span data-ttu-id="d7d2e-114">Ce didacticiel vous montre comment tooimplement une disponibilité de groupe à l’aide de SQL Server Always On de bout en bout à l’intérieur d’un environnement Azure.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-114">This tutorial shows you how tooimplement an availability group by using SQL Server Always On end-to-end inside an Azure environment.</span></span> <span data-ttu-id="d7d2e-115">À la fin de hello du didacticiel de hello, votre solution SQL Server Always On dans Azure comprendra hello suivant d’éléments :</span><span class="sxs-lookup"><span data-stu-id="d7d2e-115">At hello end of hello tutorial, your SQL Server Always On solution in Azure will consist of hello following elements:</span></span>

* <span data-ttu-id="d7d2e-116">un réseau virtuel contenant plusieurs sous-réseaux, notamment un sous-réseau frontal et un sous-réseau principal ;</span><span class="sxs-lookup"><span data-stu-id="d7d2e-116">A virtual network that contains multiple subnets, including a front-end and a back-end subnet.</span></span>
* <span data-ttu-id="d7d2e-117">un contrôleur de domaine avec un domaine Active Directory ;</span><span class="sxs-lookup"><span data-stu-id="d7d2e-117">A domain controller with an Active Directory domain.</span></span>
* <span data-ttu-id="d7d2e-118">Deux machines virtuelles SQL Server qui sont déployés toohello principal sous-réseau et domaine d’Active Directory toohello jointes.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-118">Two SQL Server VMs that are deployed toohello back-end subnet and joined toohello Active Directory domain.</span></span>
* <span data-ttu-id="d7d2e-119">Un cluster de basculement de Windows de trois nœuds avec le modèle de quorum nœud majoritaire hello.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-119">A three-node Windows failover cluster with hello Node Majority quorum model.</span></span>
* <span data-ttu-id="d7d2e-120">un groupe de disponibilité avec deux réplicas avec validation synchrone d’une base de données de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-120">An availability group with two synchronous-commit replicas of an availability database.</span></span>

<span data-ttu-id="d7d2e-121">Ce scénario est choisi pour sa simplicité, pas pour sa rentabilité ou pour d’autres avantages apportés par Azure.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-121">This scenario is a good choice for its simplicity on Azure, not for its cost-effectiveness or other factors.</span></span> <span data-ttu-id="d7d2e-122">Par exemple, vous pouvez réduire nombre hello d’ordinateurs virtuels pour un toosave de groupe de disponibilité de deux réplicas sur les heures de calcul dans Azure à l’aide du contrôleur de domaine hello en tant que témoin de partage de fichiers hello quorum dans un cluster de basculement à deux nœuds.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-122">For example, you can minimize hello number of VMs for a two-replica availability group toosave on compute hours in Azure by using hello domain controller as hello quorum file share witness in a two-node failover cluster.</span></span> <span data-ttu-id="d7d2e-123">Cette méthode réduit le nombre d’ordinateurs virtuels hello par rapport à hello au-dessus de configuration.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-123">This method reduces hello VM count by one from hello above configuration.</span></span>

<span data-ttu-id="d7d2e-124">Ce didacticiel est destiné à tooshow vous hello étapes sont requise tooset des hello décrit la solution ci-dessus, sans développer les détails hello de chaque étape.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-124">This tutorial is intended tooshow you hello steps that are required tooset up hello described solution above, without elaborating on hello details of each step.</span></span> <span data-ttu-id="d7d2e-125">Par conséquent, au lieu de fournir des étapes de configuration de l’interface graphique utilisateur de hello, il utilise tootake de script PowerShell vous rapidement à chaque étape.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-125">Therefore, instead of providing hello GUI configuration steps, it uses PowerShell scripting tootake you quickly through each step.</span></span> <span data-ttu-id="d7d2e-126">Ce didacticiel suppose hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="d7d2e-126">This tutorial assumes hello following:</span></span>

* <span data-ttu-id="d7d2e-127">Vous avez déjà un compte Azure avec un abonnement de machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-127">You already have an Azure account with hello virtual machine subscription.</span></span>
* <span data-ttu-id="d7d2e-128">Vous avez installé hello [applets de commande Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d7d2e-128">You've installed hello [Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>
* <span data-ttu-id="d7d2e-129">Vous disposez déjà d’une connaissance approfondie des groupes de disponibilité Always On pour les solutions locales.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-129">You already have a solid understanding of Always On availability groups for on-premises solutions.</span></span> <span data-ttu-id="d7d2e-130">Pour plus d’informations, voir [Groupes de disponibilité AlwaysOn (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).</span><span class="sxs-lookup"><span data-stu-id="d7d2e-130">For more information, see [Always On availability groups (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).</span></span>

## <a name="connect-tooyour-azure-subscription-and-create-hello-virtual-network"></a><span data-ttu-id="d7d2e-131">Se connecter tooyour abonnement Azure et créer des réseaux virtuels de hello</span><span class="sxs-lookup"><span data-stu-id="d7d2e-131">Connect tooyour Azure subscription and create hello virtual network</span></span>
1. <span data-ttu-id="d7d2e-132">Dans une fenêtre PowerShell sur votre ordinateur local, importez hello module Azure, téléchargez hello machine de tooyour de fichier de paramètres de publication et connecter votre tooyour de session PowerShell abonnement Azure en important les paramètres de publication hello téléchargé.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-132">In a PowerShell window on your local computer, import hello Azure module, download hello publishing settings file tooyour machine, and connect your PowerShell session tooyour Azure subscription by importing hello downloaded publishing settings.</span></span>

        Import-Module "C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\Azure\Azure.psd1"
        Get-AzurePublishSettingsFile
        Import-AzurePublishSettingsFile <publishsettingsfilepath>

    <span data-ttu-id="d7d2e-133">Hello **Get-AzurePublishSettingsFile** commande génère automatiquement un certificat de gestion Azure et le télécharge tooyour machine.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-133">hello **Get-AzurePublishSettingsFile** command automatically generates a management certificate with Azure and downloads it tooyour machine.</span></span> <span data-ttu-id="d7d2e-134">Un navigateur s’ouvre automatiquement et que vous les informations d’identification du compte Microsoft hello tooenter demandées pour votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-134">A browser is automatically opened, and you're prompted tooenter hello Microsoft account credentials for your Azure subscription.</span></span> <span data-ttu-id="d7d2e-135">Hello téléchargé **.publishsettings** fichier contient toutes les informations de hello que vous avez besoin de toomanage votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-135">hello downloaded **.publishsettings** file contains all hello information that you need toomanage your Azure subscription.</span></span> <span data-ttu-id="d7d2e-136">Après avoir enregistré ce répertoire tooa local, importez-le à l’aide de hello **Import-AzurePublishSettingsFile** commande.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-136">After saving this file tooa local directory, import it by using hello **Import-AzurePublishSettingsFile** command.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d7d2e-137">fichier .publishsettings de Hello contient vos informations d’identification (non encodées) qui sont utilisé tooadminister vos abonnements Azure et services.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-137">hello .publishsettings file contains your credentials (unencoded) that are used tooadminister your Azure subscriptions and services.</span></span> <span data-ttu-id="d7d2e-138">Hello meilleure pratique de sécurité pour ce fichier est toostore il temporairement en dehors de vos répertoires sources (par exemple, dans le dossier bibliothèques\documents hello), puis supprimez-le après l’importation du hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-138">hello security best practice for this file is toostore it temporarily outside your source directories (for example, in hello Libraries\Documents folder), and then delete it after hello import has finished.</span></span> <span data-ttu-id="d7d2e-139">Un utilisateur malveillant qui réussit à fichier .publishsettings de toohello access permettre modifier, créer et supprimer vos services Azure.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-139">A malicious user who gains access toohello .publishsettings file can edit, create, and delete your Azure services.</span></span>

2. <span data-ttu-id="d7d2e-140">Définissez une série de variables que vous allez utiliser toocreate votre infrastructure de cloud computing.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-140">Define a series of variables that you'll use toocreate your cloud IT infrastructure.</span></span>

        $location = "West US"
        $affinityGroupName = "ContosoAG"
        $affinityGroupDescription = "Contoso SQL HADR Affinity Group"
        $affinityGroupLabel = "IaaS BI Affinity Group"
        $networkConfigPath = "C:\scripts\Network.netcfg"
        $virtualNetworkName = "ContosoNET"
        $storageAccountName = "<uniquestorageaccountname>"
        $storageAccountLabel = "Contoso SQL HADR Storage Account"
        $storageAccountContainer = "https://" + $storageAccountName + ".blob.core.windows.net/vhds/"
        $winImageName = (Get-AzureVMImage | where {$_.Label -like "Windows Server 2008 R2 SP1*"} | sort PublishedDate -Descending)[0].ImageName
        $sqlImageName = (Get-AzureVMImage | where {$_.Label -like "SQL Server 2012 SP1 Enterprise*"} | sort PublishedDate -Descending)[0].ImageName
        $dcServerName = "ContosoDC"
        $dcServiceName = "<uniqueservicename>"
        $availabilitySetName = "SQLHADR"
        $vmAdminUser = "AzureAdmin"
        $vmAdminPassword = "Contoso!000"
        $workingDir = "c:\scripts\"

    <span data-ttu-id="d7d2e-141">Payer toohello attention suivant tooensure vos commandes réussira ultérieurement :</span><span class="sxs-lookup"><span data-stu-id="d7d2e-141">Pay attention toohello following tooensure that your commands will succeed later:</span></span>

   * <span data-ttu-id="d7d2e-142">Variables **$storageAccountName** et **$dcServiceName** doit être unique parce qu’ils sont utilisés tooidentify votre compte de stockage cloud et le serveur en nuage, respectivement, sur hello Internet.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-142">Variables **$storageAccountName** and **$dcServiceName** must be unique because they're used tooidentify your cloud storage account and cloud server, respectively, on hello Internet.</span></span>
   * <span data-ttu-id="d7d2e-143">Hello des noms que vous spécifiez pour les variables **$affinityGroupName** et **$virtualNetworkName** sont configurés dans le document de configuration de réseau virtuel hello que vous utiliserez plus tard.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-143">hello names that you specify for variables **$affinityGroupName** and **$virtualNetworkName** are configured in hello virtual network configuration document that you'll use later.</span></span>
   * <span data-ttu-id="d7d2e-144">**$sqlImageName** Spécifie le nom hello mis à jour de l’image de machine virtuelle hello qui contient l’édition Enterprise de SQL Server 2012 Service Pack 1.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-144">**$sqlImageName** specifies hello updated name of hello VM image that contains SQL Server 2012 Service Pack 1 Enterprise Edition.</span></span>
   * <span data-ttu-id="d7d2e-145">Par souci de simplicité, **Contoso ! 000** est hello même mot de passe qui est utilisé dans tout le didacticiel hello.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-145">For simplicity, **Contoso!000** is hello same password that's used throughout hello entire tutorial.</span></span>

3. <span data-ttu-id="d7d2e-146">Créez un groupe d’affinités.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-146">Create an affinity group.</span></span>

        New-AzureAffinityGroup `
            -Name $affinityGroupName `
            -Location $location `
            -Description $affinityGroupDescription `
            -Label $affinityGroupLabel

4. <span data-ttu-id="d7d2e-147">Créez un réseau virtuel en important un fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-147">Create a virtual network by importing a configuration file.</span></span>

        Set-AzureVNetConfig `
            -ConfigurationPath $networkConfigPath

    <span data-ttu-id="d7d2e-148">fichier de configuration Hello contient hello suivant du document XML.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-148">hello configuration file contains hello following XML document.</span></span> <span data-ttu-id="d7d2e-149">En bref, il spécifie un réseau virtuel appelé **ContosoNET** dans le groupe d’affinité hello appelé **ContosoAG**.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-149">In brief, it specifies a virtual network called **ContosoNET** in hello affinity group called **ContosoAG**.</span></span> <span data-ttu-id="d7d2e-150">Il a l’espace d’adressage hello **10.10.0.0/16** et deux sous-réseaux, **10.10.1.0/24** et **10.10.2.0/24**, qui sont hello les sous-réseau frontal et le sous-réseau principal, respectivement.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-150">It has hello address space **10.10.0.0/16** and has two subnets, **10.10.1.0/24** and **10.10.2.0/24**, which are hello front subnet and back subnet, respectively.</span></span> <span data-ttu-id="d7d2e-151">sous-réseau frontal de Hello est où vous pouvez placer des applications clientes telles que Microsoft SharePoint.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-151">hello front subnet is where you can place client applications such as Microsoft SharePoint.</span></span> <span data-ttu-id="d7d2e-152">sous-réseau principal de Hello est où vous allez placer les machines virtuelles hello SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-152">hello back subnet is where you'll place hello SQL Server VMs.</span></span> <span data-ttu-id="d7d2e-153">Si vous modifiez hello **$affinityGroupName** et **$virtualNetworkName** variables précédemment, vous devez également modifier hello correspondant de noms ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-153">If you change hello **$affinityGroupName** and **$virtualNetworkName** variables earlier, you must also change hello corresponding names below.</span></span>

        <NetworkConfiguration xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <Dns />
            <VirtualNetworkSites>
              <VirtualNetworkSite name="ContosoNET" AffinityGroup="ContosoAG">
                <AddressSpace>
                  <AddressPrefix>10.10.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="Front">
                    <AddressPrefix>10.10.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="Back">
                    <AddressPrefix>10.10.2.0/24</AddressPrefix>
                  </Subnet>
                </Subnets>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

5. <span data-ttu-id="d7d2e-154">Créez un compte de stockage a associé à un groupe d’affinité hello que vous créé et définissez en tant que compte de stockage actif hello dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-154">Create a storage account that's associated with hello affinity group that you created, and set it as hello current storage account in your subscription.</span></span>

        New-AzureStorageAccount `
            -StorageAccountName $storageAccountName `
            -Label $storageAccountLabel `
            -AffinityGroup $affinityGroupName
        Set-AzureSubscription `
            -SubscriptionName (Get-AzureSubscription).SubscriptionName `
            -CurrentStorageAccount $storageAccountName

6. <span data-ttu-id="d7d2e-155">Créer des serveur de contrôleur de domaine hello dans hello nouveau cloud service et la disponibilité de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-155">Create hello domain controller server in hello new cloud service and availability set.</span></span>

        New-AzureVMConfig `
            -Name $dcServerName `
            -InstanceSize Medium `
            -ImageName $winImageName `
            -MediaLocation "$storageAccountContainer$dcServerName.vhd" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -Windows `
                -DisableAutomaticUpdates `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword |
                New-AzureVM `
                    -ServiceName $dcServiceName `
                    –AffinityGroup $affinityGroupName `
                    -VNetName $virtualNetworkName

    <span data-ttu-id="d7d2e-156">Ces commandes dirigées hello suivants choses :</span><span class="sxs-lookup"><span data-stu-id="d7d2e-156">These piped commands do hello following things:</span></span>

   * <span data-ttu-id="d7d2e-157">**New-AzureVMConfig** crée une configuration de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-157">**New-AzureVMConfig** creates a VM configuration.</span></span>
   * <span data-ttu-id="d7d2e-158">**Ajouter-AzureProvisioningConfig** donne hello des paramètres de configuration d’un serveur Windows autonome.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-158">**Add-AzureProvisioningConfig** gives hello configuration parameters of a standalone Windows server.</span></span>
   * <span data-ttu-id="d7d2e-159">**Ajouter-AzureDataDisk** ajoute le disque de données hello que vous allez utiliser pour le stockage de données Active Directory, avec hello tooNone de jeu d’option de mise en cache.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-159">**Add-AzureDataDisk** adds hello data disk that you'll use for storing Active Directory data, with hello caching option set tooNone.</span></span>
   * <span data-ttu-id="d7d2e-160">**New-AzureVM** crée un nouveau service cloud et hello du nouvel ordinateur virtuel Azure dans le nouveau service de cloud hello.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-160">**New-AzureVM** creates a new cloud service and creates hello new Azure VM in hello new cloud service.</span></span>

7. <span data-ttu-id="d7d2e-161">Patientez hello nouvelle machine virtuelle toobe est entièrement configuré et télécharger le répertoire de travail tooyour hello fichier Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-161">Wait for hello new VM toobe fully provisioned, and download hello remote desktop file tooyour working directory.</span></span> <span data-ttu-id="d7d2e-162">Étant donné que hello nouvel ordinateur virtuel Azure a une tooprovision beaucoup de temps, hello `while` boucle continue toopoll hello nouvelle machine virtuelle jusqu'à ce qu’il est prêt à être utilisé.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-162">Because hello new Azure VM takes a long time tooprovision, hello `while` loop continues toopoll hello new VM until it's ready for use.</span></span>

        $VMStatus = Get-AzureVM -ServiceName $dcServiceName -Name $dcServerName

        While ($VMStatus.InstanceStatus -ne "ReadyRole")
        {
            write-host "Waiting for " $VMStatus.Name "... Current Status = " $VMStatus.InstanceStatus
            Start-Sleep -Seconds 15
            $VMStatus = Get-AzureVM -ServiceName $dcServiceName -Name $dcServerName
        }

        Get-AzureRemoteDesktopFile `
            -ServiceName $dcServiceName `
            -Name $dcServerName `
            -LocalPath "$workingDir$dcServerName.rdp"

<span data-ttu-id="d7d2e-163">serveur de contrôleur de domaine Hello est maintenant correctement configuré.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-163">hello domain controller server is now successfully provisioned.</span></span> <span data-ttu-id="d7d2e-164">Ensuite, vous devez configurer le domaine Active Directory de hello sur ce serveur de contrôleur de domaine.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-164">Next, you'll configure hello Active Directory domain on this domain controller server.</span></span> <span data-ttu-id="d7d2e-165">Laissez la fenêtre de PowerShell hello ouverte sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-165">Leave hello PowerShell window open on your local computer.</span></span> <span data-ttu-id="d7d2e-166">Vous l’utiliserez à nouveau toocreate ultérieure hello deux machines virtuelles de serveur SQL.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-166">You'll use it again later toocreate hello two SQL Server VMs.</span></span>

## <a name="configure-hello-domain-controller"></a><span data-ttu-id="d7d2e-167">Configurer le contrôleur de domaine hello</span><span class="sxs-lookup"><span data-stu-id="d7d2e-167">Configure hello domain controller</span></span>
1. <span data-ttu-id="d7d2e-168">Se connecter toohello serveur de contrôleur de domaine en lançant le fichier Bureau à distance de hello.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-168">Connect toohello domain controller server by launching hello remote desktop file.</span></span> <span data-ttu-id="d7d2e-169">Utilisez le nom d’utilisateur AzureAdmin et le mot de passe d’administrateur de la machine hello **Contoso ! 000**, que vous avez spécifiés lors de la création hello nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-169">Use hello machine administrator’s username AzureAdmin and password **Contoso!000**, which you specified when you created hello new VM.</span></span>
2. <span data-ttu-id="d7d2e-170">Ouvrez une fenêtre PowerShell en mode administrateur.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-170">Open a PowerShell window in administrator mode.</span></span>
3. <span data-ttu-id="d7d2e-171">Exécutez hello **DCPROMO. EXE** tooset de commande des hello **corp.contoso.com** domaine, avec les répertoires de données hello sur le lecteur M.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-171">Run hello following **DCPROMO.EXE** command tooset up hello **corp.contoso.com** domain, with hello data directories on drive M.</span></span>

        dcpromo.exe `
            /unattend `
            /ReplicaOrNewDomain:Domain `
            /NewDomain:Forest `
            /NewDomainDNSName:corp.contoso.com `
            /ForestLevel:4 `
            /DomainNetbiosName:CORP `
            /DomainLevel:4 `
            /InstallDNS:Yes `
            /ConfirmGc:Yes `
            /CreateDNSDelegation:No `
            /DatabasePath:"C:\Windows\NTDS" `
            /LogPath:"C:\Windows\NTDS" `
            /SYSVOLPath:"C:\Windows\SYSVOL" `
            /SafeModeAdminPassword:"Contoso!000"

    <span data-ttu-id="d7d2e-172">Après la commande hello, hello machine virtuelle redémarre automatiquement.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-172">After hello command finishes, hello VM restarts automatically.</span></span>

4. <span data-ttu-id="d7d2e-173">Connectez-vous de nouveau serveur de contrôleur de domaine toohello en lançant le fichier Bureau à distance de hello.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-173">Connect toohello domain controller server again by launching hello remote desktop file.</span></span> <span data-ttu-id="d7d2e-174">Cette fois, connectez-vous en tant que **CORP\Administrator**.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-174">This time, sign in as **CORP\Administrator**.</span></span>
5. <span data-ttu-id="d7d2e-175">Ouvrez une fenêtre PowerShell en mode administrateur et d’importation du module Active Directory PowerShell hello à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d7d2e-175">Open a PowerShell window in administrator mode, and import hello Active Directory PowerShell module by using hello following command:</span></span>

        Import-Module ActiveDirectory

6. <span data-ttu-id="d7d2e-176">Exécutez hello suivant du domaine de toohello commandes tooadd trois utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-176">Run hello following commands tooadd three users toohello domain.</span></span>

        $pwd = ConvertTo-SecureString "Contoso!000" -AsPlainText -Force
        New-ADUser `
            -Name 'Install' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true
        New-ADUser `
            -Name 'SQLSvc1' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true
        New-ADUser `
            -Name 'SQLSvc2' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true

    <span data-ttu-id="d7d2e-177">**CORP\Install** est tooconfigure utilisé tout ce dont les instances de service SQL Server toohello, cluster de basculement hello et groupe de disponibilité hello.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-177">**CORP\Install** is used tooconfigure everything related toohello SQL Server service instances, hello failover cluster, and hello availability group.</span></span> <span data-ttu-id="d7d2e-178">**CORP\SQLSvc1** et **CORP\SQLSvc2** sont utilisés comme comptes de service SQL Server hello pour les machines virtuelles hello deux SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-178">**CORP\SQLSvc1** and **CORP\SQLSvc2** are used as hello SQL Server service accounts for hello two SQL Server VMs.</span></span>
7. <span data-ttu-id="d7d2e-179">Suivant de hello suivant, exécutez les commandes toogive **CORP\Install** hello autorisations toocreate ordinateur objets hello domaine.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-179">Next, run hello following commands toogive **CORP\Install** hello permissions toocreate computer objects in hello domain.</span></span>

        Cd ad:
        $sid = new-object System.Security.Principal.SecurityIdentifier (Get-ADUser "Install").SID
        $guid = new-object Guid bf967a86-0de6-11d0-a285-00aa003049e2
        $ace1 = new-object System.DirectoryServices.ActiveDirectoryAccessRule $sid,"CreateChild","Allow",$guid,"All"
        $corp = Get-ADObject -Identity "DC=corp,DC=contoso,DC=com"
        $acl = Get-Acl $corp
        $acl.AddAccessRule($ace1)
        Set-Acl -Path "DC=corp,DC=contoso,DC=com" -AclObject $acl

    <span data-ttu-id="d7d2e-180">Hello GUID spécifié ci-dessus est hello GUID pour le type d’objet ordinateur hello.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-180">hello GUID specified above is hello GUID for hello computer object type.</span></span> <span data-ttu-id="d7d2e-181">Hello **CORP\Install** compte doit hello **lire toutes les propriétés** et **créer des objets ordinateur** hello de toocreate autorisations Active Directory des objets pour le basculement de hello cluster.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-181">hello **CORP\Install** account needs hello **Read All Properties** and **Create Computer Objects** permission toocreate hello Active Direct objects for hello failover cluster.</span></span> <span data-ttu-id="d7d2e-182">Hello **lire toutes les propriétés** autorisation est accordée déjà tooCORP\Install par défaut, vous n’avez pas besoin toogrant il explicitement.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-182">hello **Read All Properties** permission is already given tooCORP\Install by default, so you don't need toogrant it explicitly.</span></span> <span data-ttu-id="d7d2e-183">Pour plus d’informations sur les autorisations qui sont nécessaires le cluster de basculement toocreate hello, consultez [Guide pas à pas du Cluster de basculement : configuration des comptes dans Active Directory](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="d7d2e-183">For more information on permissions that are needed toocreate hello failover cluster, see [Failover Cluster Step-by-Step Guide: Configuring Accounts in Active Directory](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx).</span></span>

    <span data-ttu-id="d7d2e-184">Maintenant que vous avez terminé de configurer Active Directory et les objets utilisateur hello, vous allez créer deux machines virtuelles de serveur SQL et joignez-les toothis domaine.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-184">Now that you've finished configuring Active Directory and hello user objects, you'll create two SQL Server VMs and join them toothis domain.</span></span>

## <a name="create-hello-sql-server-vms"></a><span data-ttu-id="d7d2e-185">Créer des machines virtuelles hello SQL Server</span><span class="sxs-lookup"><span data-stu-id="d7d2e-185">Create hello SQL Server VMs</span></span>
1. <span data-ttu-id="d7d2e-186">Continuer toouse hello PowerShell fenêtre qui est ouverte sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-186">Continue toouse hello PowerShell window that's open on your local computer.</span></span> <span data-ttu-id="d7d2e-187">Définissez hello suivant des variables supplémentaires :</span><span class="sxs-lookup"><span data-stu-id="d7d2e-187">Define hello following additional variables:</span></span>

        $domainName= "corp"
        $FQDN = "corp.contoso.com"
        $subnetName = "Back"
        $sqlServiceName = "<uniqueservicename>"
        $quorumServerName = "ContosoQuorum"
        $sql1ServerName = "ContosoSQL1"
        $sql2ServerName = "ContosoSQL2"
        $availabilitySetName = "SQLHADR"
        $dataDiskSize = 100
        $dnsSettings = New-AzureDns -Name "ContosoBackDNS" -IPAddress "10.10.0.4"

    <span data-ttu-id="d7d2e-188">adresse IP de Hello **10.10.0.4** est généralement assignée toohello première machine virtuelle que vous créez dans hello **10.10.0.0/16** sous-réseau de votre réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-188">hello IP address **10.10.0.4** is typically assigned toohello first VM that you create in hello **10.10.0.0/16** subnet of your Azure virtual network.</span></span> <span data-ttu-id="d7d2e-189">Vous devez vérifier qu’il s’agit des adresses de hello de votre serveur de contrôleur de domaine en exécutant **IPCONFIG**.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-189">You should verify that this is hello address of your domain controller server by running **IPCONFIG**.</span></span>
2. <span data-ttu-id="d7d2e-190">Exécution hello suivant hello toocreate de commandes dirigées tout d’abord nommé de machine virtuelle dans un cluster de basculement hello, **ContosoQuorum**:</span><span class="sxs-lookup"><span data-stu-id="d7d2e-190">Run hello following piped commands toocreate hello first VM in hello failover cluster, named **ContosoQuorum**:</span></span>

        New-AzureVMConfig `
            -Name $quorumServerName `
            -InstanceSize Medium `
            -ImageName $winImageName `
            -MediaLocation "$storageAccountContainer$quorumServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    New-AzureVM `
                        -ServiceName $sqlServiceName `
                        –AffinityGroup $affinityGroupName `
                        -VNetName $virtualNetworkName `
                        -DnsSettings $dnsSettings

    <span data-ttu-id="d7d2e-191">Notez ce qui suit hello concernant la commande hello ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="d7d2e-191">Note hello following regarding hello command above:</span></span>

   * <span data-ttu-id="d7d2e-192">**Nouveau-AzureVMConfig** crée une configuration de machine virtuelle avec le nom de jeu hello haute disponibilité souhaité.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-192">**New-AzureVMConfig** creates a VM configuration with hello desired availability set name.</span></span> <span data-ttu-id="d7d2e-193">Hello machines virtuelles suivantes seront créées avec hello même nom à haute disponibilité afin qu’ils sont joints toohello même groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-193">hello subsequent VMs will be created with hello same availability set name so that they're joined toohello same availability set.</span></span>
   * <span data-ttu-id="d7d2e-194">**Ajouter-AzureProvisioningConfig** jointures hello de domaine Active Directory de toohello machine virtuelle que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-194">**Add-AzureProvisioningConfig** joins hello VM toohello Active Directory domain that you created.</span></span>
   * <span data-ttu-id="d7d2e-195">**Set-AzureSubnet** emplacements hello machine virtuelle dans le sous-réseau principal de hello.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-195">**Set-AzureSubnet** places hello VM in hello back subnet.</span></span>
   * <span data-ttu-id="d7d2e-196">**New-AzureVM** crée un nouveau service cloud et hello du nouvel ordinateur virtuel Azure dans le nouveau service de cloud hello.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-196">**New-AzureVM** creates a new cloud service and creates hello new Azure VM in hello new cloud service.</span></span> <span data-ttu-id="d7d2e-197">Hello **DnsSettings** paramètre spécifie le serveur DNS hello pour les serveurs dans le nouveau service de cloud hello hello a adresseIP hello **10.10.0.4**.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-197">hello **DnsSettings** parameter specifies that hello DNS server for hello servers in hello new cloud service has hello IP address **10.10.0.4**.</span></span> <span data-ttu-id="d7d2e-198">Il s’agit d’adresse IP de hello du serveur de contrôleur de domaine hello.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-198">This is hello IP address of hello domain controller server.</span></span> <span data-ttu-id="d7d2e-199">Ce paramètre est nécessaire tooenable hello nouvelles machines virtuelles dans un domaine Active Directory de hello cloud service toojoin toohello avec succès.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-199">This parameter is needed tooenable hello new VMs in hello cloud service toojoin toohello Active Directory domain successfully.</span></span> <span data-ttu-id="d7d2e-200">Sans ce paramètre, vous devez définir manuellement des paramètres IPv4 hello dans votre serveur de contrôleur de domaine de machine virtuelle toouse hello en tant que serveur DNS principal de hello après hello machine virtuelle est configurée, puis joindre le domaine Active Directory de hello VM toohello.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-200">Without this parameter, you must manually set hello IPv4 settings in your VM toouse hello domain controller server as hello primary DNS server after hello VM is provisioned, and then join hello VM toohello Active Directory domain.</span></span>
3. <span data-ttu-id="d7d2e-201">Exécution hello suivant dirigée commandes toocreate hello machines virtuelles SQL Server nommée **ContosoSQL1** et **ContosoSQL2**.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-201">Run hello following piped commands toocreate hello SQL Server VMs, named **ContosoSQL1** and **ContosoSQL2**.</span></span>

        # Create ContosoSQL1...
        New-AzureVMConfig `
            -Name $sql1ServerName `
            -InstanceSize Large `
            -ImageName $sqlImageName `
            -MediaLocation "$storageAccountContainer$sql1ServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -HostCaching "ReadOnly" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    Add-AzureEndpoint `
                        -Name "SQL" `
                        -Protocol "tcp" `
                        -PublicPort 1 `
                        -LocalPort 1433 |
                        New-AzureVM `
                            -ServiceName $sqlServiceName

        # Create ContosoSQL2...
        New-AzureVMConfig `
            -Name $sql2ServerName `
            -InstanceSize Large `
            -ImageName $sqlImageName `
            -MediaLocation "$storageAccountContainer$sql2ServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -HostCaching "ReadOnly" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    Add-AzureEndpoint `
                        -Name "SQL" `
                        -Protocol "tcp" `
                        -PublicPort 2 `
                        -LocalPort 1433 |
                        New-AzureVM `
                            -ServiceName $sqlServiceName

    <span data-ttu-id="d7d2e-202">Notez ce qui suit hello concernant les commandes hello ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="d7d2e-202">Note hello following regarding hello commands above:</span></span>

   * <span data-ttu-id="d7d2e-203">**Nouveau-AzureVMConfig** utilise hello le même nom de groupe de disponibilité en tant que serveur de contrôleur de domaine hello et utilise hello image de SQL Server 2012 Service Pack 1 Enterprise Edition dans la galerie de machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-203">**New-AzureVMConfig** uses hello same availability set name as hello domain controller server, and uses hello SQL Server 2012 Service Pack 1 Enterprise Edition image in hello virtual machine gallery.</span></span> <span data-ttu-id="d7d2e-204">Il définit également hello d’exploitation système tooread-mise en cache disque uniquement (aucun cache d’écriture).</span><span class="sxs-lookup"><span data-stu-id="d7d2e-204">It also sets hello operating system disk tooread-caching only (no write caching).</span></span> <span data-ttu-id="d7d2e-205">Nous vous recommandons de migrer hello de base de données fichiers tooa disque de données distinct que vous attachez toohello machine virtuelle et configurez avec aucune lecture ou le cache d’écriture.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-205">We recommend that you migrate hello database files tooa separate data disk that you attach toohello VM, and configure it with no read or write caching.</span></span> <span data-ttu-id="d7d2e-206">Toutefois, hello il est recommandé ensuite tooremove cache d’écriture sur le disque du système d’exploitation hello, car vous ne pouvez pas supprimer le cache sur le disque du système d’exploitation hello de lecture.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-206">However, hello next best thing is tooremove write caching on hello operating system disk because you can't remove read caching on hello operating system disk.</span></span>
   * <span data-ttu-id="d7d2e-207">**Ajouter-AzureProvisioningConfig** jointures hello de domaine Active Directory de toohello machine virtuelle que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-207">**Add-AzureProvisioningConfig** joins hello VM toohello Active Directory domain that you created.</span></span>
   * <span data-ttu-id="d7d2e-208">**Set-AzureSubnet** emplacements hello machine virtuelle dans le sous-réseau principal de hello.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-208">**Set-AzureSubnet** places hello VM in hello back subnet.</span></span>
   * <span data-ttu-id="d7d2e-209">**Ajouter-AzureEndpoint** ajoute des points de terminaison de l’accès afin que les applications clientes puissent accéder à ces instances de service SQL Server sur hello Internet.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-209">**Add-AzureEndpoint** adds access endpoints so that client applications can access these SQL Server services instances on hello Internet.</span></span> <span data-ttu-id="d7d2e-210">Des ports différents sont fournis tooContosoSQL1 et ContosoSQL2.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-210">Different ports are given tooContosoSQL1 and ContosoSQL2.</span></span>
   * <span data-ttu-id="d7d2e-211">**New-AzureVM** crée hello nouvelle machine virtuelle de serveur SQL Bonjour même service de cloud computing comme ContosoQuorum.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-211">**New-AzureVM** creates hello new SQL Server VM in hello same cloud service as ContosoQuorum.</span></span> <span data-ttu-id="d7d2e-212">Vous devez placer les machines virtuelles de hello Bonjour même service cloud si vous souhaitez les toobe dans hello du même groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-212">You must place hello VMs in hello same cloud service if you want them toobe in hello same availability set.</span></span>
4. <span data-ttu-id="d7d2e-213">Attendez que chaque toobe de machine virtuelle entièrement configuré et de toodownload de chaque ordinateur virtuel de son répertoire de travail tooyour fichier Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-213">Wait for each VM toobe fully provisioned and for each VM toodownload its remote desktop file tooyour working directory.</span></span> <span data-ttu-id="d7d2e-214">Hello `for` boucle hello parcourt les trois nouvelles machines virtuelles et exécute des commandes hello à l’intérieur des accolades hello pour chacun d’eux.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-214">hello `for` loop cycles through hello three new VMs and executes hello commands inside hello top-level curly brackets for each of them.</span></span>

        Foreach ($VM in $VMs = Get-AzureVM -ServiceName $sqlServiceName)
        {
            write-host "Waiting for " $VM.Name "..."

            # Loop until hello VM status is "ReadyRole"
            While ($VM.InstanceStatus -ne "ReadyRole")
            {
                write-host "  Current Status = " $VM.InstanceStatus
                Start-Sleep -Seconds 15
                $VM = Get-AzureVM -ServiceName $VM.ServiceName -Name $VM.InstanceName
            }

            write-host "  Current Status = " $VM.InstanceStatus

            # Download remote desktop file
            Get-AzureRemoteDesktopFile -ServiceName $VM.ServiceName -Name $VM.InstanceName -LocalPath "$workingDir$($VM.InstanceName).rdp"
        }

    <span data-ttu-id="d7d2e-215">machines virtuelles Hello SQL Server sont maintenant configurés et en cours d’exécution, mais ils sont installés avec SQL Server avec les options par défaut.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-215">hello SQL Server VMs are now provisioned and running, but they're installed with SQL Server with default options.</span></span>

## <a name="initialize-hello-failover-cluster-vms"></a><span data-ttu-id="d7d2e-216">Initialiser les machines virtuelles du cluster de basculement hello</span><span class="sxs-lookup"><span data-stu-id="d7d2e-216">Initialize hello failover cluster VMs</span></span>
<span data-ttu-id="d7d2e-217">Dans cette section, vous devez toomodify hello trois serveurs que vous allez utiliser dans un cluster de basculement hello et l’installation de SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-217">In this section, you need toomodify hello three servers that you'll use in hello failover cluster and hello SQL Server installation.</span></span> <span data-ttu-id="d7d2e-218">Plus précisément :</span><span class="sxs-lookup"><span data-stu-id="d7d2e-218">Specifically:</span></span>

* <span data-ttu-id="d7d2e-219">Tous les serveurs : vous devez tooinstall hello **le Clustering de basculement** fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-219">All servers: You need tooinstall hello **Failover Clustering** feature.</span></span>
* <span data-ttu-id="d7d2e-220">Tous les serveurs : vous devez tooadd **CORP\Install** en tant qu’ordinateur de hello **administrateur**.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-220">All servers: You need tooadd **CORP\Install** as hello machine **administrator**.</span></span>
* <span data-ttu-id="d7d2e-221">ContosoSQL1 et ContosoSQL2 uniquement : vous devez tooadd **CORP\Install** comme un **sysadmin** rôle dans la base de données par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-221">ContosoSQL1 and ContosoSQL2 only: You need tooadd **CORP\Install** as a **sysadmin** role in hello default database.</span></span>
* <span data-ttu-id="d7d2e-222">ContosoSQL1 et ContosoSQL2 uniquement : vous devez tooadd **NT AUTHORITY\System** comme un signe avec hello les autorisations suivantes :</span><span class="sxs-lookup"><span data-stu-id="d7d2e-222">ContosoSQL1 and ContosoSQL2 only: You need tooadd **NT AUTHORITY\System** as a sign-in with hello following permissions:</span></span>

  * <span data-ttu-id="d7d2e-223">Modifier un groupe de disponibilité</span><span class="sxs-lookup"><span data-stu-id="d7d2e-223">Alter any availability group</span></span>
  * <span data-ttu-id="d7d2e-224">Connecter SQL</span><span class="sxs-lookup"><span data-stu-id="d7d2e-224">Connect SQL</span></span>
  * <span data-ttu-id="d7d2e-225">Afficher l’état du serveur</span><span class="sxs-lookup"><span data-stu-id="d7d2e-225">View server state</span></span>
* <span data-ttu-id="d7d2e-226">ContosoSQL1 et ContosoSQL2 uniquement : hello **TCP** protocole est déjà activé sur hello machine virtuelle SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-226">ContosoSQL1 and ContosoSQL2 only: hello **TCP** protocol is already enabled on hello SQL Server VM.</span></span> <span data-ttu-id="d7d2e-227">Toutefois, vous devez toujours le pare-feu tooopen hello pour l’accès à distance de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-227">However, you still need tooopen hello firewall for remote access of SQL Server.</span></span>

<span data-ttu-id="d7d2e-228">Vous êtes désormais prêt toostart.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-228">Now, you're ready toostart.</span></span> <span data-ttu-id="d7d2e-229">À partir de **ContosoQuorum**, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="d7d2e-229">Beginning with **ContosoQuorum**, follow hello steps below:</span></span>

1. <span data-ttu-id="d7d2e-230">Vous connecter trop**ContosoQuorum** en lançant les fichiers Bureau à distance de hello.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-230">Connect too**ContosoQuorum** by launching hello remote desktop files.</span></span> <span data-ttu-id="d7d2e-231">Utilisez le nom d’utilisateur de l’administrateur hello **AzureAdmin** et le mot de passe **Contoso ! 000**, que vous avez spécifiés lors de la création de machines virtuelles de hello.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-231">Use hello machine administrator’s username **AzureAdmin** and password **Contoso!000**, which you specified when you created hello VMs.</span></span>
2. <span data-ttu-id="d7d2e-232">Vérifiez que les ordinateurs hello ont été correctement attachés trop**corp.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-232">Verify that hello computers have been successfully joined too**corp.contoso.com**.</span></span>
3. <span data-ttu-id="d7d2e-233">Attendez que toofinish d’installation de SQL Server hello en cours d’exécution hello automatisée des tâches d’initialisation avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-233">Wait for hello SQL Server installation toofinish running hello automated initialization tasks before proceeding.</span></span>
4. <span data-ttu-id="d7d2e-234">Ouvrez une fenêtre PowerShell en mode administrateur.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-234">Open a PowerShell window in administrator mode.</span></span>
5. <span data-ttu-id="d7d2e-235">Installer la fonctionnalité de Clustering de basculement Windows hello.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-235">Install hello Windows Failover Clustering feature.</span></span>

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. <span data-ttu-id="d7d2e-236">Ajoutez **CORP\Install** en tant qu’administrateur local.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-236">Add **CORP\Install** as a local administrator.</span></span>

        net localgroup administrators "CORP\Install" /Add
7. <span data-ttu-id="d7d2e-237">Déconnectez-vous de ContosoQuorum.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-237">Sign out of ContosoQuorum.</span></span> <span data-ttu-id="d7d2e-238">Vous avez terminé avec ce serveur.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-238">You're done with this server now.</span></span>

        logoff.exe

<span data-ttu-id="d7d2e-239">Ensuite, initialisez **ContosoSQL1** et **ContosoSQL2**.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-239">Next, initialize **ContosoSQL1** and **ContosoSQL2**.</span></span> <span data-ttu-id="d7d2e-240">Suivez les étapes de hello ci-dessous, identiques pour les deux machines virtuelles SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-240">Follow hello steps below, which are identical for both SQL Server VMs.</span></span>

1. <span data-ttu-id="d7d2e-241">Connecter des machines virtuelles toohello deux SQL Server en lançant les fichiers Bureau à distance de hello.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-241">Connect toohello two SQL Server VMs by launching hello remote desktop files.</span></span> <span data-ttu-id="d7d2e-242">Utilisez le nom d’utilisateur de l’administrateur hello **AzureAdmin** et le mot de passe **Contoso ! 000**, que vous avez spécifiés lors de la création de machines virtuelles de hello.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-242">Use hello machine administrator’s username **AzureAdmin** and password **Contoso!000**, which you specified when you created hello VMs.</span></span>
2. <span data-ttu-id="d7d2e-243">Vérifiez que les ordinateurs hello ont été correctement attachés trop**corp.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-243">Verify that hello computers have been successfully joined too**corp.contoso.com**.</span></span>
3. <span data-ttu-id="d7d2e-244">Attendez que toofinish d’installation de SQL Server hello en cours d’exécution hello automatisée des tâches d’initialisation avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-244">Wait for hello SQL Server installation toofinish running hello automated initialization tasks before proceeding.</span></span>
4. <span data-ttu-id="d7d2e-245">Ouvrez une fenêtre PowerShell en mode administrateur.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-245">Open a PowerShell window in administrator mode.</span></span>
5. <span data-ttu-id="d7d2e-246">Installer la fonctionnalité de Clustering de basculement Windows hello.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-246">Install hello Windows Failover Clustering feature.</span></span>

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. <span data-ttu-id="d7d2e-247">Ajoutez **CORP\Install** en tant qu’administrateur local.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-247">Add **CORP\Install** as a local administrator.</span></span>

        net localgroup administrators "CORP\Install" /Add
7. <span data-ttu-id="d7d2e-248">Importer hello fournisseur PowerShell SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-248">Import hello SQL Server PowerShell Provider.</span></span>

        Set-ExecutionPolicy -Execution RemoteSigned -Force
        Import-Module -Name "sqlps" -DisableNameChecking
8. <span data-ttu-id="d7d2e-249">Ajouter **CORP\Install** en tant que rôle de sysadmin hello pour l’instance de SQL Server par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-249">Add **CORP\Install** as hello sysadmin role for hello default SQL Server instance.</span></span>

        net localgroup administrators "CORP\Install" /Add
        Invoke-SqlCmd -Query "EXEC sp_addsrvrolemember 'CORP\Install', 'sysadmin'" -ServerInstance "."
9. <span data-ttu-id="d7d2e-250">Ajouter **NT AUTHORITY\System** comme un connectez-vous avec les autorisations hello trois décrites ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-250">Add **NT AUTHORITY\System** as a sign-in with hello three permissions described above.</span></span>

        Invoke-SqlCmd -Query "CREATE LOGIN [NT AUTHORITY\SYSTEM] FROM WINDOWS" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT ALTER ANY AVAILABILITY GROUP too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT CONNECT SQL too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT VIEW SERVER STATE too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
10. <span data-ttu-id="d7d2e-251">Ouvrez le pare-feu hello pour l’accès à distance de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-251">Open hello firewall for remote access of SQL Server.</span></span>

         netsh advfirewall firewall add rule name='SQL Server (TCP-In)' program='C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Binn\sqlservr.exe' dir=in action=allow protocol=TCP
11. <span data-ttu-id="d7d2e-252">Déconnectez-vous des deux machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-252">Sign out of both VMs.</span></span>

         logoff.exe

<span data-ttu-id="d7d2e-253">Enfin, vous êtes prêt tooconfigure le groupe de disponibilité hello.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-253">Finally, you're ready tooconfigure hello availability group.</span></span> <span data-ttu-id="d7d2e-254">Vous allez utiliser tooperform de fournisseur PowerShell SQL Server hello concernent tous des hello **ContosoSQL1**.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-254">You'll use hello SQL Server PowerShell Provider tooperform all of hello work on **ContosoSQL1**.</span></span>

## <a name="configure-hello-availability-group"></a><span data-ttu-id="d7d2e-255">Configurer le groupe de disponibilité hello</span><span class="sxs-lookup"><span data-stu-id="d7d2e-255">Configure hello availability group</span></span>
1. <span data-ttu-id="d7d2e-256">Vous connecter trop**ContosoSQL1** en lançant les fichiers Bureau à distance de hello.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-256">Connect too**ContosoSQL1** again by launching hello remote desktop files.</span></span> <span data-ttu-id="d7d2e-257">Au lieu de vous connecter à l’aide du compte d’ordinateur hello, connectez-vous à l’aide de **CORP\Install**.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-257">Instead of signing in by using hello machine account, sign in by using **CORP\Install**.</span></span>
2. <span data-ttu-id="d7d2e-258">Ouvrez une fenêtre PowerShell en mode administrateur.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-258">Open a PowerShell window in administrator mode.</span></span>
3. <span data-ttu-id="d7d2e-259">Définissez hello suivant variables :</span><span class="sxs-lookup"><span data-stu-id="d7d2e-259">Define hello following variables:</span></span>

        $server1 = "ContosoSQL1"
        $server2 = "ContosoSQL2"
        $serverQuorum = "ContosoQuorum"
        $acct1 = "CORP\SQLSvc1"
        $acct2 = "CORP\SQLSvc2"
        $password = "Contoso!000"
        $clusterName = "Cluster1"
        $timeout = New-Object System.TimeSpan -ArgumentList 0, 0, 30
        $db = "MyDB1"
        $backupShare = "\\$server1\backup"
        $quorumShare = "\\$server1\quorum"
        $ag = "AG1"
4. <span data-ttu-id="d7d2e-260">Importer hello fournisseur PowerShell SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-260">Import hello SQL Server PowerShell Provider.</span></span>

        Set-ExecutionPolicy RemoteSigned -Force
        Import-Module "sqlps" -DisableNameChecking
5. <span data-ttu-id="d7d2e-261">Modifier le compte de service SQL Server hello pour ContosoSQL1 tooCORP\SQLSvc1.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-261">Change hello SQL Server service account for ContosoSQL1 tooCORP\SQLSvc1.</span></span>

        $wmi1 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server1
        $wmi1.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct1,$password)}
        $svc1 = Get-Service -ComputerName $server1 -Name 'MSSQLSERVER'
        $svc1.Stop()
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc1.Start();
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
6. <span data-ttu-id="d7d2e-262">Modifier le compte de service SQL Server hello pour ContosoSQL2 tooCORP\SQLSvc2.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-262">Change hello SQL Server service account for ContosoSQL2 tooCORP\SQLSvc2.</span></span>

        $wmi2 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server2
        $wmi2.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct2,$password)}
        $svc2 = Get-Service -ComputerName $server2 -Name 'MSSQLSERVER'
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
7. <span data-ttu-id="d7d2e-263">Télécharger **CreateAzureFailoverCluster.ps1** de [création d’un Cluster de basculement pour les groupes de disponibilité AlwaysOn dans Azure VM](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a) toohello répertoire de travail local.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-263">Download **CreateAzureFailoverCluster.ps1** from [Create Failover Cluster for Always On Availability Groups in Azure VM](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a) toohello local working directory.</span></span> <span data-ttu-id="d7d2e-264">Vous utiliserez cette toohelp de script que vous créez un cluster de basculement fonctionnel.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-264">You'll use this script toohelp you create a functional failover cluster.</span></span> <span data-ttu-id="d7d2e-265">Pour plus d’informations sur l’interaction de Clustering de basculement Windows avec hello Azure réseau, voir [haute disponibilité et récupération d’urgence pour SQL Server dans Azure Virtual Machines](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d7d2e-265">For important information on how Windows Failover Clustering interacts with hello Azure network, see [High availability and disaster recovery for SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>
8. <span data-ttu-id="d7d2e-266">Modifier le répertoire de travail tooyour et créer un cluster de basculement hello avec le script de hello téléchargé.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-266">Change tooyour working directory and create hello failover cluster with hello downloaded script.</span></span>

        Set-ExecutionPolicy Unrestricted -Force
        .\CreateAzureFailoverCluster.ps1 -ClusterName "$clusterName" -ClusterNode "$server1","$server2","$serverQuorum"
9. <span data-ttu-id="d7d2e-267">Activer les groupes de disponibilité Always On pour les instances de SQL Server par défaut hello sur **ContosoSQL1** et **ContosoSQL2**.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-267">Enable Always On availability groups for hello default SQL Server instances on **ContosoSQL1** and **ContosoSQL2**.</span></span>

        Enable-SqlAlwaysOn `
            -Path SQLSERVER:\SQL\$server1\Default `
            -Force
        Enable-SqlAlwaysOn `
            -Path SQLSERVER:\SQL\$server2\Default `
            -NoServiceRestart
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
10. <span data-ttu-id="d7d2e-268">Créer un répertoire de sauvegarde et accorder des autorisations pour les comptes de service SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-268">Create a backup directory and grant permissions for hello SQL Server service accounts.</span></span> <span data-ttu-id="d7d2e-269">Vous allez utiliser cette base de données de répertoire tooprepare hello disponibilité sur réplica secondaire de hello.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-269">You'll use this directory tooprepare hello availability database on hello secondary replica.</span></span>

         $backup = "C:\backup"
         New-Item $backup -ItemType directory
         net share backup=$backup "/grant:$acct1,FULL" "/grant:$acct2,FULL"
         icacls.exe "$backup" /grant:r ("$acct1" + ":(OI)(CI)F") ("$acct2" + ":(OI)(CI)F")
11. <span data-ttu-id="d7d2e-270">Créer une base de données sur **ContosoSQL1** appelé **MyDB1**, effectuez une sauvegarde complète et une sauvegarde de journal et les restaurer sur **ContosoSQL2** avec hello **WITH NORECOVERY** option.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-270">Create a database on **ContosoSQL1** called **MyDB1**, take both a full backup and a log backup, and restore them on **ContosoSQL2** with hello **WITH NORECOVERY** option.</span></span>

         Invoke-SqlCmd -Query "CREATE database $db"
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server1
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server1 -BackupAction Log
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server2 -NoRecovery
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server2 -RestoreAction Log -NoRecovery
12. <span data-ttu-id="d7d2e-271">Créer des points de terminaison groupe de disponibilité hello sur hello machines virtuelles SQL Server et définissez des autorisations appropriées de hello sur les points de terminaison hello.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-271">Create hello availability group endpoints on hello SQL Server VMs and set hello proper permissions on hello endpoints.</span></span>

         $endpoint =
             New-SqlHadrEndpoint MyMirroringEndpoint `
             -Port 5022 `
             -Path "SQLSERVER:\SQL\$server1\Default"
         Set-SqlHadrEndpoint `
             -InputObject $endpoint `
             -State "Started"
         $endpoint =
             New-SqlHadrEndpoint MyMirroringEndpoint `
             -Port 5022 `
             -Path "SQLSERVER:\SQL\$server2\Default"
         Set-SqlHadrEndpoint `
             -InputObject $endpoint `
             -State "Started"

         Invoke-SqlCmd -Query "CREATE LOGIN [$acct2] FROM WINDOWS" -ServerInstance $server1
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] too[$acct2]" -ServerInstance $server1
         Invoke-SqlCmd -Query "CREATE LOGIN [$acct1] FROM WINDOWS" -ServerInstance $server2
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] too[$acct1]" -ServerInstance $server2
13. <span data-ttu-id="d7d2e-272">Créer des réplicas de disponibilité hello.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-272">Create hello availability replicas.</span></span>

         $primaryReplica =
             New-SqlAvailabilityReplica `
             -Name $server1 `
             -EndpointURL "TCP://$server1.corp.contoso.com:5022" `
             -AvailabilityMode "SynchronousCommit" `
             -FailoverMode "Automatic" `
             -Version 11 `
             -AsTemplate
         $secondaryReplica =
             New-SqlAvailabilityReplica `
             -Name $server2 `
             -EndpointURL "TCP://$server2.corp.contoso.com:5022" `
             -AvailabilityMode "SynchronousCommit" `
             -FailoverMode "Automatic" `
             -Version 11 `
             -AsTemplate
14. <span data-ttu-id="d7d2e-273">Enfin, créez le groupe de disponibilité hello et groupe de disponibilité toohello jointure hello réplica secondaire.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-273">Finally, create hello availability group and join hello secondary replica toohello availability group.</span></span>

         New-SqlAvailabilityGroup `
             -Name $ag `
             -Path "SQLSERVER:\SQL\$server1\Default" `
             -AvailabilityReplica @($primaryReplica,$secondaryReplica) `
             -Database $db
         Join-SqlAvailabilityGroup `
             -Path "SQLSERVER:\SQL\$server2\Default" `
             -Name $ag
         Add-SqlAvailabilityDatabase `
             -Path "SQLSERVER:\SQL\$server2\Default\AvailabilityGroups\$ag" `
             -Database $db

## <a name="next-steps"></a><span data-ttu-id="d7d2e-274">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d7d2e-274">Next steps</span></span>
<span data-ttu-id="d7d2e-275">Vous avez correctement implémenté SQL Server Always On en créant un groupe de disponibilité dans Azure.</span><span class="sxs-lookup"><span data-stu-id="d7d2e-275">You've now successfully implemented SQL Server Always On by creating an availability group in Azure.</span></span> <span data-ttu-id="d7d2e-276">tooconfigure un écouteur pour ce groupe de disponibilité, consultez [configurer un écouteur d’équilibrage de charge interne pour les groupes de disponibilité Always On dans Azure](../classic/ps-sql-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="d7d2e-276">tooconfigure a listener for this availability group, see [Configure an ILB listener for Always On availability groups in Azure](../classic/ps-sql-int-listener.md).</span></span>

<span data-ttu-id="d7d2e-277">Pour en savoir plus sur l’utilisation de SQL Server dans Azure, consultez [Présentation de SQL Server sur les machines virtuelles Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d7d2e-277">For other information about using SQL Server in Azure, see [SQL Server on Azure virtual machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
