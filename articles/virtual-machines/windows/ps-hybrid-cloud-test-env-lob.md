---
title: "environnement de test d’application aaaLOB | Documents Microsoft"
description: "En savoir plus l’environnement de cloud toocreate sur le web, application métier dans un hybride IT pro ou tests de développement."
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 92d2d8ce-60ed-4512-95e5-a7fe3b0ca00b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.openlocfilehash: e9f825bbb1cbeb841ee3c974ebf6721dc236c311
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-web-based-lob-application-in-a-hybrid-cloud-for-testing"></a><span data-ttu-id="cc902-103">Configuration d’une application métier web dans un cloud hybride pour le test</span><span class="sxs-lookup"><span data-stu-id="cc902-103">Set up a web-based LOB application in a hybrid cloud for testing</span></span>
<span data-ttu-id="cc902-104">Cette rubrique vous guide lors de la création d’un environnement cloud hybride simulé pour tester une application métier web hébergée dans Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="cc902-104">This topic steps you through creating a simulated hybrid cloud environment for testing a web-based line of business (LOB) application hosted in Microsoft Azure.</span></span> <span data-ttu-id="cc902-105">Voici la configuration obtenue de hello.</span><span class="sxs-lookup"><span data-stu-id="cc902-105">Here is hello resulting configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

<span data-ttu-id="cc902-106">Cette configuration se compose des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="cc902-106">This configuration consists of:</span></span>

* <span data-ttu-id="cc902-107">Un réseau local simulé hébergé dans Azure (hello TestLab VNet).</span><span class="sxs-lookup"><span data-stu-id="cc902-107">A simulated on-premises network hosted in Azure (hello TestLab VNet).</span></span>
* <span data-ttu-id="cc902-108">Un réseau virtuel intersite hébergé dans Azure (TestVNET).</span><span class="sxs-lookup"><span data-stu-id="cc902-108">A cross-premises virtual network hosted in Azure (TestVNET).</span></span>
* <span data-ttu-id="cc902-109">Une connexion VPN de réseau virtuel à réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="cc902-109">A VNet-to-VNet VPN connection.</span></span>
* <span data-ttu-id="cc902-110">Un serveur web métier, SQL server et contrôleur de domaine secondaire dans le réseau virtuel de TestVNET hello.</span><span class="sxs-lookup"><span data-stu-id="cc902-110">A web-based LOB server, SQL server, and secondary domain controller in hello TestVNET virtual network.</span></span>

<span data-ttu-id="cc902-111">Cette configuration fournit une base et un point de départ commun à partir duquel vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="cc902-111">This configuration provides a basis and common starting point from which you can:</span></span>

* <span data-ttu-id="cc902-112">Développer et tester des applications métier hébergées sur IIS (Internet Information Services) avec un serveur principal de base de données SQL Server 2014 dans Azure.</span><span class="sxs-lookup"><span data-stu-id="cc902-112">Develop and test LOB applications hosted on Internet Information Services (IIS) with a SQL Server 2014 database backend in Azure.</span></span>
* <span data-ttu-id="cc902-113">Tester cette charge de travail informatique hybride simulée basée sur le cloud.</span><span class="sxs-lookup"><span data-stu-id="cc902-113">Perform testing of this simulated hybrid cloud-based IT workload.</span></span>

<span data-ttu-id="cc902-114">Il existe trois principales phases toosetting, cet environnement de test de cloud hybride :</span><span class="sxs-lookup"><span data-stu-id="cc902-114">There are three major phases toosetting up this hybrid cloud test environment:</span></span>

1. <span data-ttu-id="cc902-115">Configurer l’environnement de cloud hybride simulé hello.</span><span class="sxs-lookup"><span data-stu-id="cc902-115">Set up hello simulated hybrid cloud environment.</span></span>
2. <span data-ttu-id="cc902-116">Configurez l’ordinateur hello SQL server (SQL1).</span><span class="sxs-lookup"><span data-stu-id="cc902-116">Configure hello SQL server computer (SQL1).</span></span>
3. <span data-ttu-id="cc902-117">Configurer hello LOB serveur (LOB1).</span><span class="sxs-lookup"><span data-stu-id="cc902-117">Configure hello LOB server (LOB1).</span></span>

<span data-ttu-id="cc902-118">Cette charge de travail nécessite un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="cc902-118">This workload requires an Azure subscription.</span></span> <span data-ttu-id="cc902-119">Si vous avez un abonnement MSDN ou Visual Studio, consultez [Crédit Azure mensuel pour les abonnés Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="cc902-119">If you have an MSDN or Visual Studio subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span>

<span data-ttu-id="cc902-120">Pour obtenir un exemple d’une application LOB hébergée dans Azure de production, consultez hello **des applications métier** plan architecture à [diagrammes d’Architecture logicielle Microsoft et les projets](http://msdn.microsoft.com/dn630664).</span><span class="sxs-lookup"><span data-stu-id="cc902-120">For an example of a production LOB application hosted in Azure, see hello **Line of business applications** architecture blueprint at [Microsoft Software Architecture Diagrams and Blueprints](http://msdn.microsoft.com/dn630664).</span></span>

## <a name="phase-1-set-up-hello-simulated-hybrid-cloud-environment"></a><span data-ttu-id="cc902-121">Phase 1 : Paramétrer l’environnement de cloud hybride simulé hello</span><span class="sxs-lookup"><span data-stu-id="cc902-121">Phase 1: Set up hello simulated hybrid cloud environment</span></span>
<span data-ttu-id="cc902-122">Créer hello [environnement de test de cloud hybride simulé](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cc902-122">Create hello [simulated hybrid cloud test environment](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="cc902-123">Étant donné que cet environnement de test ne nécessite pas la présence de hello du serveur hello APP1 sur le sous-réseau du réseau d’entreprise hello, vous pouvez l’arrêter pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="cc902-123">Because this test environment does not require hello presence of hello APP1 server on hello Corpnet subnet, you can shut it down for now.</span></span>

<span data-ttu-id="cc902-124">Ceci est votre configuration actuelle.</span><span class="sxs-lookup"><span data-stu-id="cc902-124">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph1.png)

## <a name="phase-2-configure-hello-sql-server-computer-sql1"></a><span data-ttu-id="cc902-125">Phase 2 : Configurer l’ordinateur hello SQL server (SQL1)</span><span class="sxs-lookup"><span data-stu-id="cc902-125">Phase 2: Configure hello SQL server computer (SQL1)</span></span>
<span data-ttu-id="cc902-126">À partir de hello portail Azure, démarrer l’ordinateur de DC2 hello si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="cc902-126">From hello Azure portal, start hello DC2 computer if needed.</span></span>

<span data-ttu-id="cc902-127">Ensuite, créez une machine virtuelle pour SQL1 avec ces commandes dans une invite de commandes Azure PowerShell sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="cc902-127">Next, create a virtual machine for SQL1 with these commands at an Azure PowerShell command prompt on your local computer.</span></span> <span data-ttu-id="cc902-128">Toorunning préalable ces commandes, renseignez hello valeurs des variables et remove hello < et > caractères.</span><span class="sxs-lookup"><span data-stu-id="cc902-128">Prior toorunning these commands, fill in hello variable values and remove hello < and > characters.</span></span>

    $rgName="<your resource group name>"
    $locName="<hello Azure location of your resource group>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName SQL1 -VMSize Standard_A4
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-SQLDataDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name "Data" -DiskSizeInGB 100 -VhdUri $vhdURI  -CreateOption empty

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for hello SQL Server computer." 
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName SQL1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftSQLServer -Offer SQL2014-WS2012R2 -Skus Standard -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name "OSDisk" -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

<span data-ttu-id="cc902-129">Utilisez hello tooSQL1 de tooconnect portail Azure à l’aide du compte d’administrateur local hello de SQL1.</span><span class="sxs-lookup"><span data-stu-id="cc902-129">Use hello Azure portal tooconnect tooSQL1 using hello local administrator account of SQL1.</span></span>

<span data-ttu-id="cc902-130">Ensuite, configurez le test de connectivité de base de tooallow règles pare-feu Windows et le trafic SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cc902-130">Next, configure Windows Firewall rules tooallow basic connectivity testing and SQL Server traffic.</span></span> <span data-ttu-id="cc902-131">À partir d'une invite de commandes Windows PowerShell de niveau administrateur sur SQL1, exécutez ces commandes.</span><span class="sxs-lookup"><span data-stu-id="cc902-131">From an administrator-level Windows PowerShell command prompt on SQL1, run these commands.</span></span>

    New-NetFirewallRule -DisplayName "SQL Server" -Direction Inbound -Protocol TCP -LocalPort 1433,1434,5022 -Action allow 
    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

<span data-ttu-id="cc902-132">commande ping de Hello doit aboutir à quatre réponses de réussite de l’adresse IP 192.168.0.4.</span><span class="sxs-lookup"><span data-stu-id="cc902-132">hello ping command should result in four successful replies from IP address 192.168.0.4.</span></span>

<span data-ttu-id="cc902-133">Ensuite, ajoutez hello disque de données supplémentaire sur SQL1 en tant que nouveau volume avec la lettre de lecteur hello F:.</span><span class="sxs-lookup"><span data-stu-id="cc902-133">Next, add hello extra data disk on SQL1 as a new volume with hello drive letter F:.</span></span>

1. <span data-ttu-id="cc902-134">Dans le volet gauche hello du Gestionnaire de serveur, cliquez sur **File and Storage Services**, puis cliquez sur **disques**.</span><span class="sxs-lookup"><span data-stu-id="cc902-134">In hello left pane of Server Manager, click **File and Storage Services**, and then click **Disks**.</span></span>
2. <span data-ttu-id="cc902-135">Dans le volet du sommaire hello, Bonjour **disques** , cliquez sur **disque 2** (avec hello **Partition** défini trop**inconnu**).</span><span class="sxs-lookup"><span data-stu-id="cc902-135">In hello contents pane, in hello **Disks** group, click **disk 2** (with hello **Partition** set too**Unknown**).</span></span>
3. <span data-ttu-id="cc902-136">Cliquez sur **Tâches**, puis sur **Nouveau volume**.</span><span class="sxs-lookup"><span data-stu-id="cc902-136">Click **Tasks**, and then click **New Volume**.</span></span>
4. <span data-ttu-id="cc902-137">Sur hello avant de commencer, page de hello Assistant Nouveau Volume, cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="cc902-137">On hello Before you begin page of hello New Volume Wizard, click **Next**.</span></span>
5. <span data-ttu-id="cc902-138">Sur le serveur hello Select de hello et page de disque, cliquez sur **Disk 2**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="cc902-138">On hello Select hello server and disk page, click **Disk 2**, and then click **Next**.</span></span> <span data-ttu-id="cc902-139">À l’invite, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="cc902-139">When prompted, click **OK**.</span></span>
6. <span data-ttu-id="cc902-140">Dans spécifier la taille de page de volume hello hello de hello, cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="cc902-140">On hello Specify hello size of hello volume page, click **Next**.</span></span>
7. <span data-ttu-id="cc902-141">Hello Assign tooa lecteur lettre ou un dossier de page, cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="cc902-141">On hello Assign tooa drive letter or folder page, click **Next**.</span></span>
8. <span data-ttu-id="cc902-142">Dans la page des paramètres système hello sélectionner un fichier, cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="cc902-142">On hello Select file system settings page, click **Next**.</span></span>
9. <span data-ttu-id="cc902-143">Dans hello page Confirmer les sélections, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="cc902-143">On hello Confirm selections page, click **Create**.</span></span>
10. <span data-ttu-id="cc902-144">Lorsque vous avez terminé, cliquez sur **Fermer**.</span><span class="sxs-lookup"><span data-stu-id="cc902-144">When complete, click **Close**.</span></span>

<span data-ttu-id="cc902-145">Exécutez ces commandes à l’invite de commande Windows PowerShell hello sur SQL1 :</span><span class="sxs-lookup"><span data-stu-id="cc902-145">Run these commands at hello Windows PowerShell command prompt on SQL1:</span></span>

    md f:\Data
    md f:\Log
    md f:\Backup

<span data-ttu-id="cc902-146">Joignez ensuite le domaine d’entreprise Windows Server Active Directory de toohello SQL1 avec les commandes suivantes à l’invite de Windows PowerShell hello sur SQL1.</span><span class="sxs-lookup"><span data-stu-id="cc902-146">Next, join SQL1 toohello CORP Windows Server Active Directory domain with these commands at hello Windows PowerShell prompt on SQL1.</span></span>

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

<span data-ttu-id="cc902-147">Utiliser le compte hello CORP\User1 quand vous y êtes invité informations d’identification du compte de domaine toosupply pour hello **Add-Computer** commande.</span><span class="sxs-lookup"><span data-stu-id="cc902-147">Use hello CORP\User1 account when prompted toosupply domain account credentials for hello **Add-Computer** command.</span></span>

<span data-ttu-id="cc902-148">Après le redémarrage, utilisez hello tooconnect portail Azure tooSQL1 *avec le compte administrateur local hello SQL1*.</span><span class="sxs-lookup"><span data-stu-id="cc902-148">After restarting, use hello Azure portal tooconnect tooSQL1 *with hello local administrator account of SQL1*.</span></span>

<span data-ttu-id="cc902-149">Ensuite, configurez le lecteur F: hello SQL Server 2014 de toouse pour les nouvelles bases de données et des autorisations de compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="cc902-149">Next, configure SQL Server 2014 toouse hello F: drive for new databases and for user account permissions.</span></span>

1. <span data-ttu-id="cc902-150">À partir de l’écran d’accueil hello, tapez **SQL Server Management**, puis cliquez sur **SQL Server 2014 Management Studio**.</span><span class="sxs-lookup"><span data-stu-id="cc902-150">From hello Start screen, type **SQL Server Management**, and then click **SQL Server 2014 Management Studio**.</span></span>
2. <span data-ttu-id="cc902-151">Dans **connecter tooServer**, cliquez sur **connexion**.</span><span class="sxs-lookup"><span data-stu-id="cc902-151">In **Connect tooServer**, click **Connect**.</span></span>
3. <span data-ttu-id="cc902-152">Dans le volet d’arborescence hello l’Explorateur d’objets, cliquez sur **SQL1**, puis cliquez sur **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="cc902-152">In hello Object Explorer tree pane, right-click **SQL1**, and then click **Properties**.</span></span>
4. <span data-ttu-id="cc902-153">Bonjour **propriétés du serveur** fenêtre, cliquez sur **les paramètres de base de données**.</span><span class="sxs-lookup"><span data-stu-id="cc902-153">In hello **Server Properties** window, click **Database Settings**.</span></span>
5. <span data-ttu-id="cc902-154">Recherchez hello **emplacements par défaut de base de données** et définir les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="cc902-154">Locate hello **Database default locations** and set these values:</span></span> 
   * <span data-ttu-id="cc902-155">Pour **données**, le chemin d’accès de type hello **f:\Data**.</span><span class="sxs-lookup"><span data-stu-id="cc902-155">For **Data**, type hello path **f:\Data**.</span></span>
   * <span data-ttu-id="cc902-156">Pour **journal**, le chemin d’accès de type hello **f:\Log**.</span><span class="sxs-lookup"><span data-stu-id="cc902-156">For **Log**, type hello path **f:\Log**.</span></span>
   * <span data-ttu-id="cc902-157">Pour **sauvegarde**, le chemin d’accès de type hello **f:\Backup**.</span><span class="sxs-lookup"><span data-stu-id="cc902-157">For **Backup**, type hello path **f:\Backup**.</span></span>
   * <span data-ttu-id="cc902-158">Remarque : seules les nouvelles bases de données utilisent ces emplacements.</span><span class="sxs-lookup"><span data-stu-id="cc902-158">Note: Only new databases use these locations.</span></span>
6. <span data-ttu-id="cc902-159">Cliquez sur hello **OK** fenêtre hello de tooclose.</span><span class="sxs-lookup"><span data-stu-id="cc902-159">Click hello **OK** tooclose hello window.</span></span>
7. <span data-ttu-id="cc902-160">Bonjour **l’Explorateur d’objets** volet de l’arborescence, ouvrez **sécurité**.</span><span class="sxs-lookup"><span data-stu-id="cc902-160">In hello **Object Explorer** tree pane, open **Security**.</span></span>
8. <span data-ttu-id="cc902-161">Cliquez avec le bouton droit sur **Connexions** et sélectionnez **Nouvelle connexion**.</span><span class="sxs-lookup"><span data-stu-id="cc902-161">Right-click **Logins** and then click **New Login**.</span></span>
9. <span data-ttu-id="cc902-162">Dans **Nom de connexion**, tapez **CORP\User1**.</span><span class="sxs-lookup"><span data-stu-id="cc902-162">In **Login name**, type **CORP\User1**.</span></span>
10. <span data-ttu-id="cc902-163">Sur hello **rôles serveur** , cliquez sur **sysadmin**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="cc902-163">On hello **Server Roles** page, click **sysadmin**, and then click **OK**.</span></span>
11. <span data-ttu-id="cc902-164">Fermez Microsoft SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="cc902-164">Close Microsoft SQL Server Management Studio.</span></span>

<span data-ttu-id="cc902-165">Ceci est votre configuration actuelle.</span><span class="sxs-lookup"><span data-stu-id="cc902-165">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph2.png)

## <a name="phase-3-configure-hello-lob-server-lob1"></a><span data-ttu-id="cc902-166">Phase 3 : Configurer le serveur LOB hello (LOB1)</span><span class="sxs-lookup"><span data-stu-id="cc902-166">Phase 3: Configure hello LOB server (LOB1)</span></span>
<span data-ttu-id="cc902-167">Commencez par créer un ordinateur virtuel pour LOB1 avec les commandes suivantes à l’invite de commandes Azure PowerShell hello sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="cc902-167">First, create a virtual machine for LOB1 with these commands at hello Azure PowerShell command prompt on your local computer.</span></span>

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName LOB1 -VMSize Standard_A2
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for LOB1."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName LOB1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/LOB1-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name LOB1-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

<span data-ttu-id="cc902-168">Ensuite, utilisez hello tooconnect portail Azure tooLOB1 avec informations d’identification hello du compte d’administrateur local hello de LOB1.</span><span class="sxs-lookup"><span data-stu-id="cc902-168">Next, use hello Azure portal tooconnect tooLOB1 with hello credentials of hello local administrator account of LOB1.</span></span>

<span data-ttu-id="cc902-169">Ensuite, configurez un trafic de tooallow de règle de pare-feu Windows pour le test de connectivité de base.</span><span class="sxs-lookup"><span data-stu-id="cc902-169">Next, configure a Windows Firewall rule tooallow traffic for basic connectivity testing.</span></span> <span data-ttu-id="cc902-170">À partir d'une invite de commandes de Windows PowerShell de niveau administrateur sur LOB1, exécutez les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="cc902-170">From an administrator-level Windows PowerShell command prompt on LOB1, run these commands.</span></span>

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

<span data-ttu-id="cc902-171">commande ping de Hello doit aboutir à quatre réponses de réussite de l’adresse IP 192.168.0.4.</span><span class="sxs-lookup"><span data-stu-id="cc902-171">hello ping command should result in four successful replies from IP address 192.168.0.4.</span></span>

<span data-ttu-id="cc902-172">Ensuite, joindre LOB1 toohello CORP domaine Active Directory avec les commandes suivantes à l’invite de commandes Windows PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="cc902-172">Next, join LOB1 toohello CORP Active Directory domain with these commands at hello Windows PowerShell prompt.</span></span>

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

<span data-ttu-id="cc902-173">Utiliser le compte hello CORP\User1 quand vous y êtes invité informations d’identification du compte de domaine toosupply pour hello **Add-Computer** commande.</span><span class="sxs-lookup"><span data-stu-id="cc902-173">Use hello CORP\User1 account when prompted toosupply domain account credentials for hello **Add-Computer** command.</span></span>

<span data-ttu-id="cc902-174">Après le redémarrage, utilisez hello tooconnect portail Azure tooLOB1 avec le mot de passe et le compte de hello CORP\User1.</span><span class="sxs-lookup"><span data-stu-id="cc902-174">After restarting, use hello Azure portal tooconnect tooLOB1 with hello CORP\User1 account and password.</span></span>

<span data-ttu-id="cc902-175">Ensuite, configurez LOB1 pour IIS et testez l'accès à partir de CLIENT1.</span><span class="sxs-lookup"><span data-stu-id="cc902-175">Next, configure LOB1 for IIS and test access from CLIENT1.</span></span>

1. <span data-ttu-id="cc902-176">Dans le Gestionnaire de serveur, cliquez sur **Ajouter des rôles et des fonctionnalités**.</span><span class="sxs-lookup"><span data-stu-id="cc902-176">From Server Manager, click **Add roles and features**.</span></span>
2. <span data-ttu-id="cc902-177">Sur hello **avant de commencer** , cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="cc902-177">On hello **Before you begin** page, click **Next**.</span></span>
3. <span data-ttu-id="cc902-178">Sur hello **sélectionner le type d’installation** , cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="cc902-178">On hello **Select installation type** page, click **Next**.</span></span>
4. <span data-ttu-id="cc902-179">Sur hello **serveur de destination sélectionnez** , cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="cc902-179">On hello **Select destination server** page, click **Next**.</span></span>
5. <span data-ttu-id="cc902-180">Sur hello **rôles serveur** , cliquez sur **serveur Web (IIS)** dans la liste des hello **rôles**.</span><span class="sxs-lookup"><span data-stu-id="cc902-180">On hello **Server roles** page, click **Web Server (IIS)** in hello list of **Roles**.</span></span>
6. <span data-ttu-id="cc902-181">Quand vous y êtes invité, cliquez sur **Ajouter des fonctionnalités**, puis sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="cc902-181">When prompted, click **Add Features**, and then click **Next**.</span></span>
7. <span data-ttu-id="cc902-182">Sur hello **sélectionner des fonctionnalités** , cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="cc902-182">On hello **Select features** page, click **Next**.</span></span>
8. <span data-ttu-id="cc902-183">Sur hello **serveur Web (IIS)** , cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="cc902-183">On hello **Web Server (IIS)** page, click **Next**.</span></span>
9. <span data-ttu-id="cc902-184">Sur hello **sélectionner les services de rôle** page, sélectionnez ou désactivez les cases à cocher hello pour les services hello nécessaires pour tester votre application métier, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="cc902-184">On hello **Select role services** page, select or clear hello check boxes for hello services you need for testing your LOB application, and then click **Next**.</span></span>
10. <span data-ttu-id="cc902-185">Sur hello **confirmer les sélections d’installation** , cliquez sur **installer**.</span><span class="sxs-lookup"><span data-stu-id="cc902-185">On hello **Confirm installation selections** page, click **Install**.</span></span>
11. <span data-ttu-id="cc902-186">Attendez que l’installation de hello de composants soit terminée, puis **fermer**.</span><span class="sxs-lookup"><span data-stu-id="cc902-186">Wait until hello installation of components has completed and then click **Close**.</span></span>
12. <span data-ttu-id="cc902-187">À partir de hello portail Azure, connectez-vous toohello CLIENT1 ordinateur avec les informations d’identification du compte hello CORP\User1 et puis démarrez Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="cc902-187">From hello Azure portal, connect toohello CLIENT1 computer with hello CORP\User1 account credentials, and then start Internet Explorer.</span></span>
13. <span data-ttu-id="cc902-188">Dans la barre d’adresses hello, tapez **http://lob1/** et appuyez sur ENTRÉE.</span><span class="sxs-lookup"><span data-stu-id="cc902-188">In hello Address bar, type **http://lob1/** and then press ENTER.</span></span> <span data-ttu-id="cc902-189">Vous devez voir la page web de hello par défaut IIS 8.</span><span class="sxs-lookup"><span data-stu-id="cc902-189">You should see hello default IIS 8 web page.</span></span>

<span data-ttu-id="cc902-190">Ceci est votre configuration actuelle.</span><span class="sxs-lookup"><span data-stu-id="cc902-190">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

<span data-ttu-id="cc902-191">Cet environnement est maintenant prêt pour vous toodeploy votre application basée sur le web sur les fonctionnalités LOB1 et de test à partir de CLIENT1 sur le sous-réseau du réseau d’entreprise hello.</span><span class="sxs-lookup"><span data-stu-id="cc902-191">This environment is now ready for you toodeploy your web-based application on LOB1 and test functionality from CLIENT1 on hello Corpnet subnet.</span></span>

## <a name="next-step"></a><span data-ttu-id="cc902-192">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="cc902-192">Next step</span></span>
* <span data-ttu-id="cc902-193">Ajouter un nouvel ordinateur virtuel à l’aide de hello [portail Azure](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cc902-193">Add a new virtual machine using hello [Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

