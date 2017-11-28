---
title: "aaaConfigure un écouteur d’équilibrage de charge interne pour les groupes de disponibilité Always On dans Azure | Documents Microsoft"
description: "Ce didacticiel utilise des ressources créées avec le modèle de déploiement classique hello et crée un écouteur de groupe de disponibilité Always On dans Azure qui utilise un équilibrage de charge interne."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 291288a0-740b-4cfa-af62-053218beba77
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/02/2017
ms.author: mikeray
ms.openlocfilehash: 2ce9b64fea491c945b58f7641e41fd39d90b078a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-ilb-listener-for-always-on-availability-groups-in-azure"></a><span data-ttu-id="9cc02-103">Configurer un écouteur à équilibrage de charge interne pour des groupes de disponibilité Always On dans Azure</span><span class="sxs-lookup"><span data-stu-id="9cc02-103">Configure an ILB listener for Always On availability groups in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9cc02-104">Écouteur interne</span><span class="sxs-lookup"><span data-stu-id="9cc02-104">Internal listener</span></span>](../classic/ps-sql-int-listener.md)
> * [<span data-ttu-id="9cc02-105">Écouteur externe</span><span class="sxs-lookup"><span data-stu-id="9cc02-105">External listener</span></span>](../classic/ps-sql-ext-listener.md)
>
>

## <a name="overview"></a><span data-ttu-id="9cc02-106">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="9cc02-106">Overview</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9cc02-107">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Azure Resource Manager et classique](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="9cc02-107">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="9cc02-108">Cet article traite des utilisez hello hello classique de modèle de déploiement.</span><span class="sxs-lookup"><span data-stu-id="9cc02-108">This article covers hello use of hello classic deployment model.</span></span> <span data-ttu-id="9cc02-109">Nous recommandons que la plupart des nouveaux déploiements utilisent le modèle de gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="9cc02-109">We recommend that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="9cc02-110">tooconfigure un écouteur pour un groupe de disponibilité Always On dans le modèle de gestionnaire de ressources hello, consultez [configurer un équilibreur de charge pour un groupe de disponibilité Always On dans Azure](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="9cc02-110">tooconfigure a listener for an Always On availability group in hello Resource Manager model, see [Configure a load balancer for an Always On availability group in Azure](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span></span>

<span data-ttu-id="9cc02-111">Votre groupe de disponibilité peut contenir des réplicas locaux uniquement, Azure uniquement, ou locaux et Azure pour les configurations hybrides.</span><span class="sxs-lookup"><span data-stu-id="9cc02-111">Your availability group can contain replicas that are on-premises only or Azure only, or that span both on-premises and Azure for hybrid configurations.</span></span> <span data-ttu-id="9cc02-112">Azure peuvent résider dans hello même région ou dans plusieurs régions qui utilisent plusieurs réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="9cc02-112">Azure replicas can reside within hello same region or across multiple regions that use multiple virtual networks.</span></span> <span data-ttu-id="9cc02-113">Hello dans cet article supposent que vous avez déjà [configuré un groupe de disponibilité](../classic/portal-sql-alwayson-availability-groups.md) mais n’avez pas encore configuré un port d’écoute.</span><span class="sxs-lookup"><span data-stu-id="9cc02-113">hello procedures in this article assume that you have already [configured an availability group](../classic/portal-sql-alwayson-availability-groups.md) but have not yet configured a listener.</span></span>

## <a name="guidelines-and-limitations-for-internal-listeners"></a><span data-ttu-id="9cc02-114">Instructions et limitations pour les écouteurs internes</span><span class="sxs-lookup"><span data-stu-id="9cc02-114">Guidelines and limitations for internal listeners</span></span>
<span data-ttu-id="9cc02-115">Hello l’utilisation d’un équilibreur de charge interne (ILB) avec un écouteur de groupe de disponibilité dans Azure est toohello sujet suivant les instructions :</span><span class="sxs-lookup"><span data-stu-id="9cc02-115">hello use of an internal load balancer (ILB) with an availability group listener in Azure is subject toohello following guidelines:</span></span>

* <span data-ttu-id="9cc02-116">écouteur du groupe de disponibilité Hello est pris en charge sur Windows Server 2008 R2, Windows Server 2012 et Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="9cc02-116">hello availability group listener is supported on Windows Server 2008 R2, Windows Server 2012, and Windows Server 2012 R2.</span></span>
* <span data-ttu-id="9cc02-117">Qu’un seul écouteur interne est prise en charge pour chaque service cloud, car hello écouteur est configuré toohello équilibrage de charge interne, et qu’un seul équilibrage de charge pour chaque service cloud.</span><span class="sxs-lookup"><span data-stu-id="9cc02-117">Only one internal availability group listener is supported for each cloud service, because hello listener is configured toohello ILB, and there is only one ILB for each cloud service.</span></span> <span data-ttu-id="9cc02-118">Toutefois, il est possible de toocreate plusieurs écouteurs externes.</span><span class="sxs-lookup"><span data-stu-id="9cc02-118">However, it is possible toocreate multiple external listeners.</span></span> <span data-ttu-id="9cc02-119">Pour plus d’informations, voir [Configurer un écouteur externe pour les groupes de disponibilité Always On dans Azure](../classic/ps-sql-ext-listener.md).</span><span class="sxs-lookup"><span data-stu-id="9cc02-119">For more information, see [Configure an external listener for Always On availability groups in Azure](../classic/ps-sql-ext-listener.md).</span></span>

## <a name="determine-hello-accessibility-of-hello-listener"></a><span data-ttu-id="9cc02-120">Déterminer l’accessibilité hello d’écouteur de hello</span><span class="sxs-lookup"><span data-stu-id="9cc02-120">Determine hello accessibility of hello listener</span></span>
[!INCLUDE [ag-listener-accessibility](../../../../includes/virtual-machines-ag-listener-determine-accessibility.md)]

<span data-ttu-id="9cc02-121">Cet article se concentre sur la création d’un écouteur qui utilise un équilibreur de charge interne.</span><span class="sxs-lookup"><span data-stu-id="9cc02-121">This article focuses on creating a listener that uses an ILB.</span></span> <span data-ttu-id="9cc02-122">Si vous avez besoin d’un écouteur public ou externe, consultez la version hello de cet article traite de la configuration d’un [port d’écoute externe](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9cc02-122">If you need an public or external listener, see hello version of this article that discusses setting up an [external listener](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="create-load-balanced-vm-endpoints-with-direct-server-return"></a><span data-ttu-id="9cc02-123">Créer des points de terminaison de machine virtuelle à charge équilibrée avec retour direct du serveur</span><span class="sxs-lookup"><span data-stu-id="9cc02-123">Create load-balanced VM endpoints with direct server return</span></span>
<span data-ttu-id="9cc02-124">Vous créez tout d’abord un équilibrage de charge interne en exécutant le script de hello plus loin dans cette section.</span><span class="sxs-lookup"><span data-stu-id="9cc02-124">You first create an ILB by running hello script later in this section.</span></span>

<span data-ttu-id="9cc02-125">Créez un point de terminaison avec équilibrage de charge pour chaque machine virtuelle qui héberge un réplica Azure.</span><span class="sxs-lookup"><span data-stu-id="9cc02-125">Create a load-balanced endpoint for each VM that hosts an Azure replica.</span></span> <span data-ttu-id="9cc02-126">Si vous avez des réplicas dans plusieurs régions, chaque réplica pour cette région doit être dans le même service de cloud de hello hello même réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="9cc02-126">If you have replicas in multiple regions, each replica for that region must be in hello same cloud service in hello same Azure virtual network.</span></span> <span data-ttu-id="9cc02-127">La création de réplicas de groupe de disponibilité couvrant plusieurs régions Azure nécessite de configurer plusieurs réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="9cc02-127">Creating availability group replicas that span multiple Azure regions requires configuring multiple virtual networks.</span></span> <span data-ttu-id="9cc02-128">Pour plus d’informations sur la configuration de cross-connectivité de réseau virtuel, consultez [configurer la connectivité de réseau virtuel toovirtual réseau](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span><span class="sxs-lookup"><span data-stu-id="9cc02-128">For more information on configuring cross virtual network connectivity, see [Configure virtual network toovirtual network connectivity](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span></span>

1. <span data-ttu-id="9cc02-129">Bonjour portail Azure, accédez à tooeach machine virtuelle qui héberge un réplica tooview hello plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="9cc02-129">In hello Azure portal, go tooeach VM that hosts a replica tooview hello details.</span></span>

2. <span data-ttu-id="9cc02-130">Cliquez sur hello **points de terminaison** onglet pour chaque machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="9cc02-130">Click hello **Endpoints** tab for each VM.</span></span>

3. <span data-ttu-id="9cc02-131">Vérifiez que hello **nom** et **Port Public** du point de terminaison d’écouteur hello que vous souhaitez toouse ne sont pas déjà en cours d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="9cc02-131">Verify that hello **Name** and **Public Port** of hello listener endpoint that you want toouse are not already in use.</span></span> <span data-ttu-id="9cc02-132">Dans l’exemple hello dans cette section, nom de hello est *MyEndpoint*, et le port hello est *1433*.</span><span class="sxs-lookup"><span data-stu-id="9cc02-132">In hello example in this section, hello name is *MyEndpoint*, and hello port is *1433*.</span></span>

4. <span data-ttu-id="9cc02-133">Sur votre ordinateur client local, téléchargez et installez hello dernières [module PowerShell](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="9cc02-133">On your local client, download and install hello latest [PowerShell module](https://azure.microsoft.com/downloads/).</span></span>

5. <span data-ttu-id="9cc02-134">Lancez Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9cc02-134">Start Azure PowerShell.</span></span>  
    <span data-ttu-id="9cc02-135">Une nouvelle session PowerShell s’ouvre, avec hello Azure modules d’administration chargés.</span><span class="sxs-lookup"><span data-stu-id="9cc02-135">A new PowerShell session opens, with hello Azure administrative modules loaded.</span></span>

6. <span data-ttu-id="9cc02-136">Exécutez `Get-AzurePublishSettingsFile`.</span><span class="sxs-lookup"><span data-stu-id="9cc02-136">Run `Get-AzurePublishSettingsFile`.</span></span> <span data-ttu-id="9cc02-137">Cette applet de commande dirige toodownload de navigateur tooa un répertoire local de publier les paramètres fichiers tooa.</span><span class="sxs-lookup"><span data-stu-id="9cc02-137">This cmdlet directs you tooa browser toodownload a publish settings file tooa local directory.</span></span> <span data-ttu-id="9cc02-138">Vous serez peut-être invité à entrer les informations d'identification de connexion de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="9cc02-138">You might be prompted for your sign-in credentials for your Azure subscription.</span></span>

7. <span data-ttu-id="9cc02-139">Exécutez hello `Import-AzurePublishSettingsFile` commande avec le chemin d’accès de hello Hello publier le fichier de paramètres que vous avez téléchargé :</span><span class="sxs-lookup"><span data-stu-id="9cc02-139">Run hello following `Import-AzurePublishSettingsFile` command with hello path of hello publish settings file that you downloaded:</span></span>

        Import-AzurePublishSettingsFile -PublishSettingsFile <PublishSettingsFilePath>

    <span data-ttu-id="9cc02-140">Une fois que hello publié l’importation du fichier de paramètres, vous pouvez gérer votre abonnement Azure dans la session de PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="9cc02-140">After hello publish settings file is imported, you can manage your Azure subscription in hello PowerShell session.</span></span>

8. <span data-ttu-id="9cc02-141">Affectez une adresse IP statique pour l’*équilibrage de charge interne*.</span><span class="sxs-lookup"><span data-stu-id="9cc02-141">For *ILB*, assign a static IP address.</span></span> <span data-ttu-id="9cc02-142">Examiner la configuration du réseau virtuel en cours hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9cc02-142">Examine hello current virtual network configuration by running hello following command:</span></span>

        (Get-AzureVNetConfig).XMLConfiguration
9. <span data-ttu-id="9cc02-143">Hello de note *sous-réseau* nom de sous-réseau hello qui contient des machines virtuelles hello qui hébergent les réplicas hello.</span><span class="sxs-lookup"><span data-stu-id="9cc02-143">Note hello *Subnet* name for hello subnet that contains hello VMs that host hello replicas.</span></span> <span data-ttu-id="9cc02-144">Ce nom est utilisé dans le paramètre hello $SubnetName dans le script de hello.</span><span class="sxs-lookup"><span data-stu-id="9cc02-144">This name is used in hello $SubnetName parameter in hello script.</span></span>

10. <span data-ttu-id="9cc02-145">Hello de note *VirtualNetworkSite* nommer et hello commençant *AddressPrefix* pour le sous-réseau hello qui contient des machines virtuelles hello qui hébergent les réplicas hello.</span><span class="sxs-lookup"><span data-stu-id="9cc02-145">Note hello *VirtualNetworkSite* name and hello starting *AddressPrefix* for hello subnet that contains hello VMs that host hello replicas.</span></span> <span data-ttu-id="9cc02-146">Rechercher une adresse IP disponible en passant les deux valeurs toohello `Test-AzureStaticVNetIP` commande et en examinant hello *AvailableAddresses*.</span><span class="sxs-lookup"><span data-stu-id="9cc02-146">Look for an available IP address by passing both values toohello `Test-AzureStaticVNetIP` command and by examining hello *AvailableAddresses*.</span></span> <span data-ttu-id="9cc02-147">Par exemple, si hello réseau virtuel est nommé *MyVNet* et a une plage d’adresses de sous-réseau qui commence à *172.16.0.128*, suivants de hello commande répertorie les adresses disponibles :</span><span class="sxs-lookup"><span data-stu-id="9cc02-147">For example, if hello virtual network is named *MyVNet* and has a subnet address range that starts at *172.16.0.128*, hello following command would list available addresses:</span></span>

        (Test-AzureStaticVNetIP -VNetName "MyVNet"-IPAddress 172.16.0.128).AvailableAddresses
11. <span data-ttu-id="9cc02-148">Sélectionnez une des adresses disponibles de hello et l’utiliser dans le paramètre hello $ILBStaticIP du script hello dans l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="9cc02-148">Select one of hello available addresses, and use it in hello $ILBStaticIP parameter of hello script in hello next step.</span></span>

12. <span data-ttu-id="9cc02-149">Copiez hello suivant l’éditeur de texte tooa script PowerShell et définissez toosuit des valeurs de variable hello votre environnement.</span><span class="sxs-lookup"><span data-stu-id="9cc02-149">Copy hello following PowerShell script tooa text editor, and set hello variable values toosuit your environment.</span></span> <span data-ttu-id="9cc02-150">Les valeurs par défaut ont été fournies pour certains paramètres.</span><span class="sxs-lookup"><span data-stu-id="9cc02-150">Defaults have been provided for some parameters.</span></span>  

    <span data-ttu-id="9cc02-151">Les déploiements existants qui utilisent des groupes d'affinités ne peuvent pas ajouter un équilibrage de charge interne.</span><span class="sxs-lookup"><span data-stu-id="9cc02-151">Existing deployments that use affinity groups cannot add an ILB.</span></span> <span data-ttu-id="9cc02-152">Pour plus d’informations sur les exigences liées à l’équilibreur de charge interne, consultez la rubrique [Présentation de l’équilibrage de charge interne](../../../load-balancer/load-balancer-internal-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9cc02-152">For more information about ILB requirements, see [Internal load balancer overview](../../../load-balancer/load-balancer-internal-overview.md).</span></span>

    <span data-ttu-id="9cc02-153">En outre, si votre groupe de disponibilité s’étend sur les régions Azure, vous devez exécuter une fois hello script dans chaque centre de données pour le service cloud hello et les nœuds qui résident dans ce centre de données.</span><span class="sxs-lookup"><span data-stu-id="9cc02-153">Also, if your availability group spans Azure regions, you must run hello script once in each datacenter for hello cloud service and nodes that reside in that datacenter.</span></span>

        # Define variables
        $ServiceName = "<MyCloudService>" # hello name of hello cloud service that contains hello availability group nodes
        $AGNodes = "<VM1>","<VM2>","<VM3>" # all availability group nodes containing replicas in hello same cloud service, separated by commas
        $SubnetName = "<MySubnetName>" # subnet name that hello replicas use in hello virtual network
        $ILBStaticIP = "<MyILBStaticIPAddress>" # static IP address for hello ILB in hello subnet
        $ILBName = "AGListenerLB" # customize hello ILB name or use this default value

        # Create hello ILB
        Add-AzureInternalLoadBalancer -InternalLoadBalancerName $ILBName -SubnetName $SubnetName -ServiceName $ServiceName -StaticVNetIPAddress $ILBStaticIP

        # Configure a load-balanced endpoint for each node in $AGNodes by using ILB
        ForEach ($node in $AGNodes)
        {
            Get-AzureVM -ServiceName $ServiceName -Name $node | Add-AzureEndpoint -Name "ListenerEndpoint" -LBSetName "ListenerEndpointLB" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -InternalLoadBalancerName $ILBName -DirectServerReturn $true | Update-AzureVM
        }

13. <span data-ttu-id="9cc02-154">Après avoir défini les variables hello, hello de copie créer un script à partir de hello texte éditeur tooyour PowerShell session toorun.</span><span class="sxs-lookup"><span data-stu-id="9cc02-154">After you have set hello variables, copy hello script from hello text editor tooyour PowerShell session toorun it.</span></span> <span data-ttu-id="9cc02-155">Si l’invite de commandes hello affiche toujours  **>>** , appuyez sur entrée à nouveau script de hello que toomake commence à s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="9cc02-155">If hello prompt still shows **>>**, press Enter again toomake sure hello script starts running.</span></span>

## <a name="verify-that-kb2854082-is-installed-if-necessary"></a><span data-ttu-id="9cc02-156">Vérifiez que KB2854082 est installé le cas échéant</span><span class="sxs-lookup"><span data-stu-id="9cc02-156">Verify that KB2854082 is installed if necessary</span></span>
[!INCLUDE [kb2854082](../../../../includes/virtual-machines-ag-listener-kb2854082.md)]

## <a name="open-hello-firewall-ports-in-availability-group-nodes"></a><span data-ttu-id="9cc02-157">Ouvrir les ports du pare-feu hello dans les nœuds de groupe de disponibilité</span><span class="sxs-lookup"><span data-stu-id="9cc02-157">Open hello firewall ports in availability group nodes</span></span>
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-open-firewall.md)]

## <a name="create-hello-availability-group-listener"></a><span data-ttu-id="9cc02-158">Créer l’écouteur du groupe de disponibilité hello</span><span class="sxs-lookup"><span data-stu-id="9cc02-158">Create hello availability group listener</span></span>

<span data-ttu-id="9cc02-159">Créez un écouteur du groupe de disponibilité hello en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="9cc02-159">Create hello availability group listener in two steps.</span></span> <span data-ttu-id="9cc02-160">Tout d’abord, créer la ressource de cluster hello point de l’accès client et configurer les dépendances.</span><span class="sxs-lookup"><span data-stu-id="9cc02-160">First, create hello client access point cluster resource and configure  dependencies.</span></span> <span data-ttu-id="9cc02-161">Ensuite, configurez les ressources de cluster hello dans PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9cc02-161">Second, configure hello cluster resources in PowerShell.</span></span>

### <a name="create-hello-client-access-point-and-configure-hello-cluster-dependencies"></a><span data-ttu-id="9cc02-162">Créer le point d’accès client hello et configurer les dépendances de cluster de hello</span><span class="sxs-lookup"><span data-stu-id="9cc02-162">Create hello client access point and configure hello cluster dependencies</span></span>
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-create-listener.md)]

### <a name="configure-hello-cluster-resources-in-powershell"></a><span data-ttu-id="9cc02-163">Configurer les ressources de cluster hello dans PowerShell</span><span class="sxs-lookup"><span data-stu-id="9cc02-163">Configure hello cluster resources in PowerShell</span></span>
1. <span data-ttu-id="9cc02-164">Pour l’équilibrage de charge interne, vous devez utiliser adresse IP hello hello équilibrage de charge interne qui a été créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="9cc02-164">For ILB, you must use hello IP address of hello ILB that was created earlier.</span></span> <span data-ttu-id="9cc02-165">tooobtain cette adresse IP d’adresses dans PowerShell, hello utilisez script suivant :</span><span class="sxs-lookup"><span data-stu-id="9cc02-165">tooobtain this IP address in PowerShell, use hello following script:</span></span>

        # Define variables
        $ServiceName="<MyServiceName>" # hello name of hello cloud service that contains hello AG nodes
        (Get-AzureInternalLoadBalancer -ServiceName $ServiceName).IPAddress

2. <span data-ttu-id="9cc02-166">Sur l’un des ordinateurs virtuels de hello, copiez le script PowerShell de hello pour votre éditeur de texte tooa système d’exploitation, puis définir des variables de hello toohello les valeurs notées précédemment.</span><span class="sxs-lookup"><span data-stu-id="9cc02-166">On one of hello VMs, copy hello PowerShell script for your operating system tooa text editor, and then set hello variables toohello values you noted earlier.</span></span>

    <span data-ttu-id="9cc02-167">Pour Windows Server 2012 ou version ultérieure, utilisez hello script suivant :</span><span class="sxs-lookup"><span data-stu-id="9cc02-167">For Windows Server 2012 or later, use hello following script:</span></span>

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}

    <span data-ttu-id="9cc02-168">Pour Windows Server 2008 R2, utilisez hello script suivant :</span><span class="sxs-lookup"><span data-stu-id="9cc02-168">For Windows Server 2008 R2, use hello following script:</span></span>

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        cluster res $IPResourceName /priv enabledhcp=0 address=$ILBIP probeport=59999  subnetmask=255.255.255.255

3. <span data-ttu-id="9cc02-169">Une fois que vous avez ensemble hello variables, ouvrez une fenêtre Windows PowerShell avec élévation de privilèges, coller hello créer un script à partir de l’éditeur de texte hello dans votre toorun de session PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9cc02-169">After you have set hello variables, open an elevated Windows PowerShell window, paste hello script from hello text editor into your PowerShell session toorun it.</span></span> <span data-ttu-id="9cc02-170">Si l’invite de commandes hello affiche toujours  **>>** , appuyez sur entrée à nouveau les toomake assurer que le script de hello démarre en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="9cc02-170">If hello prompt still shows **>>**, Press Enter again toomake sure that hello script starts running.</span></span>

4. <span data-ttu-id="9cc02-171">Répétez les étapes précédentes pour chaque ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="9cc02-171">Repeat hello preceding steps for each VM.</span></span>  
    <span data-ttu-id="9cc02-172">Ce script configure la ressource d’adresse IP hello avec l’adresse IP de hello du service de cloud hello et définit d’autres paramètres, tel que le port de sonde hello.</span><span class="sxs-lookup"><span data-stu-id="9cc02-172">This script configures hello IP address resource with hello IP address of hello cloud service and sets other parameters, such as hello probe port.</span></span> <span data-ttu-id="9cc02-173">Lors de la ressource d’adresse IP hello est mises en ligne, il peut répondre toohello sur le port de la sonde hello hello équilibrée point de terminaison que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="9cc02-173">When hello IP address resource is brought online, it can respond toohello polling on hello probe port from hello load-balanced endpoint that you created earlier.</span></span>

## <a name="bring-hello-listener-online"></a><span data-ttu-id="9cc02-174">Mettez écouteur hello en ligne</span><span class="sxs-lookup"><span data-stu-id="9cc02-174">Bring hello listener online</span></span>
[!INCLUDE [Bring-Listener-Online](../../../../includes/virtual-machines-ag-listener-bring-online.md)]

## <a name="follow-up-items"></a><span data-ttu-id="9cc02-175">Éléments de suivi</span><span class="sxs-lookup"><span data-stu-id="9cc02-175">Follow-up items</span></span>
[!INCLUDE [Follow-up](../../../../includes/virtual-machines-ag-listener-follow-up.md)]

## <a name="test-hello-availability-group-listener-within-hello-same-virtual-network"></a><span data-ttu-id="9cc02-176">Écouteur du groupe de disponibilité hello test (dans hello même réseau virtuel)</span><span class="sxs-lookup"><span data-stu-id="9cc02-176">Test hello availability group listener (within hello same virtual network)</span></span>
[!INCLUDE [Test-Listener-Within-VNET](../../../../includes/virtual-machines-ag-listener-test.md)]

## <a name="next-steps"></a><span data-ttu-id="9cc02-177">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9cc02-177">Next steps</span></span>
[!INCLUDE [Listener-Next-Steps](../../../../includes/virtual-machines-ag-listener-next-steps.md)]
