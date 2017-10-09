---
title: "script d’aaaPowerShell toodeploy cluster HPC de Linux | Documents Microsoft"
description: "Exécuter un toodeploy de script PowerShell à un cluster Linux HPC Pack 2012 R2 dans des machines virtuelles"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 73041960-58d3-4ecf-9540-d7e1a612c467
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 885b03fa2fd604827dc388803fc21debab730979
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-high-performance-computing-hpc-cluster-with-hello-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="92ec7-103">Créer un cluster de calcul de hautes performances (HPC) Linux avec le script de déploiement IaaS de HPC Pack hello</span><span class="sxs-lookup"><span data-stu-id="92ec7-103">Create a Linux high-performance computing (HPC) cluster with hello HPC Pack IaaS deployment script</span></span>
<span data-ttu-id="92ec7-104">Exécutez hello IaaS de HPC Pack déploiement PowerShell script toodeploy un cluster HPC Pack 2012 R2 complète pour les charges de travail Linux dans des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="92ec7-104">Run hello HPC Pack IaaS deployment PowerShell script toodeploy a complete HPC Pack 2012 R2 cluster for Linux workloads in Azure virtual machines.</span></span> <span data-ttu-id="92ec7-105">cluster de Hello se compose d’un nœud principal joint à Active Directory Windows Server et Microsoft HPC Pack et les nœuds de calcul qui exécutent une Hello distributions Linux prises en charge par HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="92ec7-105">hello cluster consists of an Active Directory-joined head node running Windows Server and Microsoft HPC Pack, and compute nodes that run one of hello Linux distributions supported by HPC Pack.</span></span> <span data-ttu-id="92ec7-106">Si vous souhaitez toodeploy un cluster HPC Pack dans les charges de travail Azure pour Windows, consultez [créer un cluster HPC Windows avec hello script de déploiement IaaS de HPC Pack](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="92ec7-106">If you want toodeploy an HPC Pack cluster in Azure for Windows workloads, see [Create a Windows HPC cluster with hello HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="92ec7-107">Vous pouvez également utiliser une toodeploy de modèle un cluster HPC Pack Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="92ec7-107">You can also use an Azure Resource Manager template toodeploy an HPC Pack cluster.</span></span> <span data-ttu-id="92ec7-108">Pour obtenir un exemple, consultez [Création d’un cluster HPC avec des nœuds de calcul Linux](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/).</span><span class="sxs-lookup"><span data-stu-id="92ec7-108">For an example, see [Create an HPC cluster with Linux compute nodes](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="92ec7-109">Hello script PowerShell décrit dans cet article crée un cluster Microsoft HPC Pack 2012 R2 dans Azure à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="92ec7-109">hello PowerShell script described in this article creates a Microsoft HPC Pack 2012 R2 cluster in Azure using hello classic deployment model.</span></span> <span data-ttu-id="92ec7-110">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="92ec7-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> <span data-ttu-id="92ec7-111">En outre, script hello décrit dans cet article ne prend pas en charge HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="92ec7-111">In addition, hello script described in this article does not support HPC Pack 2016.</span></span>

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-file"></a><span data-ttu-id="92ec7-112">Exemple de fichier de configuration</span><span class="sxs-lookup"><span data-stu-id="92ec7-112">Example configuration file</span></span>
<span data-ttu-id="92ec7-113">Hello fichier de configuration suivant crée un contrôleur de domaine et la forêt de domaines et déploie un cluster HPC Pack qui a un seul nœud principal avec les bases de données locales et 10 nœuds de calcul Linux.</span><span class="sxs-lookup"><span data-stu-id="92ec7-113">hello following configuration file creates a domain controller and domain forest and deploys an HPC Pack cluster which has one head node with local databases and 10 Linux compute nodes.</span></span> <span data-ttu-id="92ec7-114">Tous les services de cloud hello sont créés directement dans l’emplacement Asie orientale hello.</span><span class="sxs-lookup"><span data-stu-id="92ec7-114">All hello cloud services are created directly in hello East Asia location.</span></span> <span data-ttu-id="92ec7-115">les nœuds de calcul Linux Hello sont créés dans les deux services de cloud computing et les deux comptes de stockage (autrement dit, *MyLnxCN à 0001* à *MyLnxCN-0005* dans *MyLnxCNService01* et *mylnxstorage01*, et *MyLnxCN-0006* à *MyLnxCN-0010* dans *MyLnxCNService02* et *mylnxstorage02* ).</span><span class="sxs-lookup"><span data-stu-id="92ec7-115">hello Linux compute nodes are created in two cloud services and two storage accounts (that is, *MyLnxCN-0001* to *MyLnxCN-0005* in *MyLnxCNService01* and *mylnxstorage01*, and *MyLnxCN-0006* to *MyLnxCN-0010* in *MyLnxCNService02* and *mylnxstorage02*).</span></span> <span data-ttu-id="92ec7-116">les nœuds de calcul Hello sont créés à partir d’une image de Linux OpenLogic CentOS version 7.0.</span><span class="sxs-lookup"><span data-stu-id="92ec7-116">hello compute nodes are created from an OpenLogic CentOS version 7.0 Linux image.</span></span> 

<span data-ttu-id="92ec7-117">Remplacez par vos propres valeurs pour votre nom d’abonnement et les noms de compte et le service de hello.</span><span class="sxs-lookup"><span data-stu-id="92ec7-117">Substitute your own values for your subscription name and hello account and service names.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>NewDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
    <DomainController>
      <VMName>MyDCServer</VMName>
      <ServiceName>MyHPCService</ServiceName>
      <VMSize>Large</VMSize>
    </DomainController>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>MyLnxCN-%0001%</VMNamePattern>
    <ServiceNamePattern>MyLnxCNService%01%</ServiceNamePattern>
    <MaxNodeCountPerService>5</MaxNodeCountPerService>
    <StorageAccountNamePattern>mylnxstorage%01%</StorageAccountNamePattern>
    <VMSize>Medium</VMSize>
    <NodeCount>10</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20150325 </ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```
## <a name="troubleshooting"></a><span data-ttu-id="92ec7-118">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="92ec7-118">Troubleshooting</span></span>
* <span data-ttu-id="92ec7-119">**Erreur « Le réseau virtuel n’existe pas »**.</span><span class="sxs-lookup"><span data-stu-id="92ec7-119">**“VNet doesn’t exist” error**.</span></span> <span data-ttu-id="92ec7-120">Si vous exécutez hello IaaS de HPC Pack déploiement script toodeploy plusieurs clusters dans Azure simultanément dans un seul abonnement, un ou plusieurs déploiements peuvent échouer avec l’erreur de hello « réseau virtuel *VNet\_nom* n’existe pas ».</span><span class="sxs-lookup"><span data-stu-id="92ec7-120">If you run hello HPC Pack IaaS deployment script toodeploy multiple clusters in Azure concurrently under one subscription, one or more deployments may fail with hello error “VNet *VNet\_Name* doesn't exist”.</span></span>
  <span data-ttu-id="92ec7-121">Si cette erreur se produit, réexécutez le script hello pour le déploiement de hello a échoué.</span><span class="sxs-lookup"><span data-stu-id="92ec7-121">If this error occurs, rerun hello script for hello failed deployment.</span></span>
* <span data-ttu-id="92ec7-122">**L’accès à des problème hello Internet à partir du réseau virtuel Azure de hello**.</span><span class="sxs-lookup"><span data-stu-id="92ec7-122">**Problem accessing hello Internet from hello Azure virtual network**.</span></span> <span data-ttu-id="92ec7-123">Si vous créez un cluster HPC Pack avec un contrôleur de domaine à l’aide du script de déploiement hello ou que vous promouvez manuellement un contrôleur de toodomain de machine virtuelle de nœud principal, vous pouvez rencontrer des problèmes de connexion des machines virtuelles de hello dans toohello de réseau virtuel Azure hello Internet.</span><span class="sxs-lookup"><span data-stu-id="92ec7-123">If you create an HPC Pack cluster with a new domain controller by using hello deployment script, or you manually promote a head node VM toodomain controller, you may experience problems connecting hello VMs in hello Azure virtual network toohello Internet.</span></span> <span data-ttu-id="92ec7-124">Cela peut se produire si un serveur DNS redirecteur est automatiquement configuré sur le contrôleur de domaine hello et que ce serveur DNS redirecteur ne résout pas correctement.</span><span class="sxs-lookup"><span data-stu-id="92ec7-124">This can occur if a forwarder DNS server is automatically configured on hello domain controller, and this forwarder DNS server doesn’t resolve properly.</span></span>
  
    <span data-ttu-id="92ec7-125">toowork résoudre ce problème, ouvrez une session sur le contrôleur de domaine toohello et un paramètre de configuration de redirecteur hello supprimer ou configurer un serveur DNS redirecteur valide.</span><span class="sxs-lookup"><span data-stu-id="92ec7-125">toowork around this problem, log on toohello domain controller and either remove hello forwarder configuration setting or configure a valid forwarder DNS server.</span></span> <span data-ttu-id="92ec7-126">toodo, cliquez sur Gestionnaire de serveur **outils** > **DNS** tooopen le Gestionnaire DNS, puis double-cliquez sur **redirecteurs**.</span><span class="sxs-lookup"><span data-stu-id="92ec7-126">toodo this, in Server Manager click **Tools** > **DNS** tooopen DNS Manager, and then double-click **Forwarders**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="92ec7-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="92ec7-127">Next steps</span></span>
* <span data-ttu-id="92ec7-128">Consultez [prise en main des nœuds de calcul Linux dans un cluster HPC Pack dans Azure](hpcpack-cluster.md) pour plus d’informations sur les distributions Linux prises en charge, déplacement de données et l’envoi de cluster HPC Pack travaux tooan Linux les nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="92ec7-128">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for information about supported Linux distributions, moving data, and submitting jobs tooan HPC Pack cluster with Linux compute nodes.</span></span>
* <span data-ttu-id="92ec7-129">Pour consulter des didacticiels qui utilisent des hello script toocreate un cluster et exécuter une charge de travail Linux HPC, consultez :</span><span class="sxs-lookup"><span data-stu-id="92ec7-129">For tutorials that use hello script toocreate a cluster and run a Linux HPC workload, see:</span></span>
  * [<span data-ttu-id="92ec7-130">Exécution de NAMD avec Microsoft HPC Pack sur des nœuds de calcul Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="92ec7-130">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-namd.md)
  * [<span data-ttu-id="92ec7-131">Exécution d’OpenFOAM avec Microsoft HPC Pack sur des nœuds de calcul Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="92ec7-131">Run OpenFOAM with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-openfoam.md)
  * [<span data-ttu-id="92ec7-132">Exécution de STAR-CCM+ avec Microsoft HPC Pack sur des nœuds de calcul Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="92ec7-132">Run STAR-CCM+ with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-starccm.md)

