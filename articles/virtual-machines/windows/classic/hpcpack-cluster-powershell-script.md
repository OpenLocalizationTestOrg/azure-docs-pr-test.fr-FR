---
title: cluster de Windows HPC aaaPowerShell script toodeploy | Documents Microsoft
description: "Exécuter un toodeploy de script PowerShell à un cluster Windows HPC Pack 2012 R2 dans des machines virtuelles"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 286b2be8-2533-40df-b02a-26156b1f1133
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 10ce1e9bc4e98954b955549bd72aaaf6106c69fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-high-performance-computing-hpc-cluster-with-hello-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="cd697-103">Créer un cluster de calcul de hautes performances (HPC) de Windows avec le script de déploiement IaaS de HPC Pack hello</span><span class="sxs-lookup"><span data-stu-id="cd697-103">Create a Windows high-performance computing (HPC) cluster with hello HPC Pack IaaS deployment script</span></span>
<span data-ttu-id="cd697-104">Exécutez hello IaaS de HPC Pack déploiement PowerShell script toodeploy un cluster HPC Pack 2012 R2 complète pour les charges de travail Windows dans les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="cd697-104">Run hello HPC Pack IaaS deployment PowerShell script toodeploy a complete HPC Pack 2012 R2 cluster for Windows workloads in Azure virtual machines.</span></span> <span data-ttu-id="cd697-105">cluster de Hello se compose d’un nœud principal joint à Active Directory Windows Server et Microsoft HPC Pack, et vous spécifiez des ressources de calcul de fenêtres supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="cd697-105">hello cluster consists of an Active Directory-joined head node running Windows Server and Microsoft HPC Pack, and additional Windows compute resources you specify.</span></span> <span data-ttu-id="cd697-106">Si vous souhaitez toodeploy un cluster HPC Pack dans Azure pour les charges de travail Linux, consultez [créer un cluster HPC de Linux avec hello script de déploiement IaaS de HPC Pack](../../linux/classic/hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="cd697-106">If you want toodeploy an HPC Pack cluster in Azure for Linux workloads, see [Create a Linux HPC cluster with hello HPC Pack IaaS deployment script](../../linux/classic/hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="cd697-107">Vous pouvez également utiliser une toodeploy de modèle un cluster HPC Pack Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cd697-107">You can also use an Azure Resource Manager template toodeploy an HPC Pack cluster.</span></span> <span data-ttu-id="cd697-108">Pour obtenir des exemples, consultez [Création d’un cluster HPC](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/) et [Création d’un cluster HPC avec une image de nœud de calcul personnalisée](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-custom-image/).</span><span class="sxs-lookup"><span data-stu-id="cd697-108">For examples, see [Create an HPC cluster](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/) and [Create an HPC cluster with a custom compute node image](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-custom-image/).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="cd697-109">Hello script PowerShell décrit dans cet article crée un cluster Microsoft HPC Pack 2012 R2 dans Azure à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="cd697-109">hello PowerShell script described in this article creates a Microsoft HPC Pack 2012 R2 cluster in Azure using hello classic deployment model.</span></span> <span data-ttu-id="cd697-110">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="cd697-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> <span data-ttu-id="cd697-111">En outre, script hello décrit dans cet article ne prend pas en charge HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="cd697-111">In addition, hello script described in this article does not support HPC Pack 2016.</span></span>

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-files"></a><span data-ttu-id="cd697-112">Exemples de fichiers de configuration</span><span class="sxs-lookup"><span data-stu-id="cd697-112">Example configuration files</span></span>
<span data-ttu-id="cd697-113">Bonjour les exemples suivants, remplacez par vos propres valeurs pour votre Id d’abonnement ou les nom et les noms de compte et le service de hello.</span><span class="sxs-lookup"><span data-stu-id="cd697-113">In hello following examples, substitute your own values for your subscription Id or name and hello account and service names.</span></span>

### <a name="example-1"></a><span data-ttu-id="cd697-114">Exemple 1</span><span class="sxs-lookup"><span data-stu-id="cd697-114">Example 1</span></span>
<span data-ttu-id="cd697-115">Hello fichier de configuration suivant déploie un cluster HPC Pack qui a un nœud principal avec des bases de données locales et cinq nœuds de calcul exécutant le système d’exploitation de Windows Server 2012 R2 hello.</span><span class="sxs-lookup"><span data-stu-id="cd697-115">hello following configuration file deploys an HPC Pack cluster that has a head node with local databases and five compute nodes running hello Windows Server 2012 R2 operating system.</span></span> <span data-ttu-id="cd697-116">Tous les services de cloud hello sont créés directement dans hello emplacement de l’ouest des États-Unis.</span><span class="sxs-lookup"><span data-stu-id="cd697-116">All hello cloud services are created directly in hello West US location.</span></span> <span data-ttu-id="cd697-117">nœud principal de Hello agit en tant que contrôleur de domaine de forêt de domaines hello.</span><span class="sxs-lookup"><span data-stu-id="cd697-117">hello head node acts as domain controller of hello domain forest.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionId>08701940-C02E-452F-B0B1-39D50119F267</SubscriptionId>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <Location>West US</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%1000%</VMNamePattern>
    <ServiceName>MyHPCCNService</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>5</NodeCount>
    <OSVersion>WindowsServer2012R2</OSVersion>
  </ComputeNodes>
</IaaSClusterConfig>
```

### <a name="example-2"></a><span data-ttu-id="cd697-118">Exemple 2</span><span class="sxs-lookup"><span data-stu-id="cd697-118">Example 2</span></span>
<span data-ttu-id="cd697-119">Hello, le fichier de configuration suivant déploie un cluster HPC Pack dans une forêt de domaines existante.</span><span class="sxs-lookup"><span data-stu-id="cd697-119">hello following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="cd697-120">cluster de Hello possède 1 nœud principal avec les bases de données locales et 12 nœuds par hello extension BGInfo VM appliquée.</span><span class="sxs-lookup"><span data-stu-id="cd697-120">hello cluster has 1 head node with local databases and 12 compute nodes with hello BGInfo VM extension applied.</span></span>
<span data-ttu-id="cd697-121">L’installation automatique des mises à jour Windows est désactivée pour hello toutes les machines virtuelles dans la forêt de domaines hello.</span><span class="sxs-lookup"><span data-stu-id="cd697-121">Automatic installation of Windows updates is disabled for all hello VMs in hello domain forest.</span></span> <span data-ttu-id="cd697-122">Tous les services de cloud hello sont créés directement dans l’emplacement de l’Asie.</span><span class="sxs-lookup"><span data-stu-id="cd697-122">All hello cloud services are created directly in the East Asia location.</span></span> <span data-ttu-id="cd697-123">les nœuds de calcul Hello sont créés dans les trois services cloud et trois comptes de stockage : *MyHPCCN-0001* trop*MyHPCCN-0005* dans *MyHPCCNService01* et  *mycnstorage01*; *MyHPCCN-0006* trop*MyHPCCN0010* dans *MyHPCCNService02* et *mycnstorage02*; et  *MyHPCCN-0011* trop*MyHPCCN-0012* dans *MyHPCCNService03* et *mycnstorage03*).</span><span class="sxs-lookup"><span data-stu-id="cd697-123">hello compute nodes are created in three cloud services and three storage accounts: *MyHPCCN-0001* too*MyHPCCN-0005* in *MyHPCCNService01* and *mycnstorage01*; *MyHPCCN-0006* too*MyHPCCN0010* in *MyHPCCNService02* and *mycnstorage02*; and *MyHPCCN-0011* too*MyHPCCN-0012* in *MyHPCCNService03* and *mycnstorage03*).</span></span> <span data-ttu-id="cd697-124">les nœuds de calcul Hello sont créés à partir d’une image privée existante capturée à partir d’un nœud de calcul.</span><span class="sxs-lookup"><span data-stu-id="cd697-124">hello compute nodes are created from an existing private image captured from a compute node.</span></span> <span data-ttu-id="cd697-125">Hello automatique augmenter et réduire le service est activé avec la valeur par défaut augmenter et réduire les intervalles.</span><span class="sxs-lookup"><span data-stu-id="cd697-125">hello auto grow and shrink service is enabled with default grow and shrink intervals.</span></span>

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
     <NoWindowsAutoUpdate />
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <Certificates>
    <Certificate>
      <Id>1</Id>
      <PfxFile>d:\mytestcert1.pfx</PfxFile>
      <Password>MyPsw!!2</Password>
    </Certificate>
  </Certificates>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%0001%</VMNamePattern>
<ServiceNamePattern>MyHPCCNService%01%</ServiceNamePattern>
<MaxNodeCountPerService>5</MaxNodeCountPerService>
<StorageAccountNamePattern>mycnstorage%01%</StorageAccountNamePattern>
    <VMSize>Medium</VMSize>
    <NodeCount>12</NodeCount>
    <ImageName HPCPackInstalled=”true”>MyHPCComputeNodeImage</ImageName>
    <VMExtensions>
       <VMExtension>
          <ExtensionName>BGInfo</ExtensionName>
          <Publisher>Microsoft.Compute</Publisher>
          <Version>1.*</Version>
       </VMExtension>
    </VMExtensions>
  </ComputeNodes>
  <AutoGrowShrink>
    <CertificateId>1</CertificateId>
  </AutoGrowShrink>
</IaaSClusterConfig>

```

### <a name="example-3"></a><span data-ttu-id="cd697-126">Exemple 3</span><span class="sxs-lookup"><span data-stu-id="cd697-126">Example 3</span></span>
<span data-ttu-id="cd697-127">Hello, le fichier de configuration suivant déploie un cluster HPC Pack dans une forêt de domaines existante.</span><span class="sxs-lookup"><span data-stu-id="cd697-127">hello following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="cd697-128">cluster de Hello contient un seul nœud principal, un serveur de base de données avec un disque de données de 500 Go, deux nœuds de broker exécutant le système d’exploitation de Windows Server 2012 R2 hello et cinq nœuds de calcul exécutant le système d’exploitation de Windows Server 2012 R2 hello.</span><span class="sxs-lookup"><span data-stu-id="cd697-128">hello cluster contains one head node, one database server with a 500 GB data disk, two broker nodes running hello Windows Server 2012 R2 operating system, and five compute nodes running hello Windows Server 2012 R2 operating system.</span></span> <span data-ttu-id="cd697-129">Hello service cloud MyHPCCNService est créé dans le groupe d’affinités de hello *MyIBAffinityGroup*, et autres services de cloud computing hello sont créés dans le groupe d’affinités de hello *MyAffinityGroup*.</span><span class="sxs-lookup"><span data-stu-id="cd697-129">hello cloud service MyHPCCNService is created in hello affinity group *MyIBAffinityGroup*, and hello other cloud services are created in hello affinity group *MyAffinityGroup*.</span></span> <span data-ttu-id="cd697-130">Hello API REST de Scheduler de travail HPC et le portail web HPC sont activés sur le nœud principal de hello.</span><span class="sxs-lookup"><span data-stu-id="cd697-130">hello HPC Job Scheduler REST API and HPC web portal are enabled on hello head node.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <AffinityGroup>MyAffinityGroup</AffinityGroup>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>    
  <Domain>
    <DCOption>ExistingDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>NewRemoteDB</DBOption>
    <DBVersion>SQLServer2014_Enterprise</DBVersion>
    <DBServer>
      <VMName>MyDBServer</VMName>
      <ServiceName>MyHPCService</ServiceName>
      <VMSize>ExtraLarge</VMSize>
      <DataDiskSizeInGB>500</DataDiskSizeInGB>
    </DBServer>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%0000%</VMNamePattern>
    <ServiceName>MyHPCCNService</ServiceName>
    <VMSize>A8</VMSize>
<NodeCount>5</NodeCount>
<AffinityGroup>MyIBAffinityGroup</AffinityGroup>
  </ComputeNodes>
  <BrokerNodes>
    <VMNamePattern>MyHPCBN-%0000%</VMNamePattern>
    <ServiceName>MyHPCBNService</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>2</NodeCount>
  </BrokerNodes>
</IaaSClusterConfig>
```



### <a name="example-4"></a><span data-ttu-id="cd697-131">Exemple 4</span><span class="sxs-lookup"><span data-stu-id="cd697-131">Example 4</span></span>
<span data-ttu-id="cd697-132">Hello, le fichier de configuration suivant déploie un cluster HPC Pack dans une forêt de domaines existante.</span><span class="sxs-lookup"><span data-stu-id="cd697-132">hello following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="cd697-133">cluster de Hello possède deux nœud principal avec les bases de données locales, deux modèles de nœud Azure sont créés, et trois nœuds de support Azure de taille sont créés pour le modèle de nœud Azure *AzureTemplate1*.</span><span class="sxs-lookup"><span data-stu-id="cd697-133">hello cluster has two head node with local databases, two Azure node templates are created, and three size Medium Azure nodes are created for Azure node template *AzureTemplate1*.</span></span> <span data-ttu-id="cd697-134">Un fichier de script s’exécute sur le nœud principal de hello après la configuration du nœud principal hello.</span><span class="sxs-lookup"><span data-stu-id="cd697-134">A script file runs on hello head node after hello head node is configured.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <AffinityGroup>MyAffinityGroup</AffinityGroup>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>ExistingDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
<VMSize>ExtraLarge</VMSize>
    <PostConfigScript>c:\MyHNPostActions.ps1</PostConfigScript>
  </HeadNode>
  <Certificates>
    <Certificate>
      <Id>1</Id>
      <PfxFile>d:\mytestcert1.pfx</PfxFile>
      <Password>MyPsw!!2</Password>
    </Certificate>
    <Certificate>
      <Id>2</Id>
      <PfxFile>d:\mytestcert2.pfx</PfxFile>
    </Certificate>    
  </Certificates>
  <AzureBurst>
    <AzureNodeTemplate>
      <TemplateName>AzureTemplate1</TemplateName>
      <SubscriptionId>bb9252ba-831f-4c9d-ae14-9a38e6da8ee4</SubscriptionId>
      <CertificateId>1</CertificateId>
      <ServiceName>mytestsvc1</ServiceName>
      <StorageAccount>myteststorage1</StorageAccount>
      <NodeCount>3</NodeCount>
      <RoleSize>Medium</RoleSize>
    </AzureNodeTemplate>
    <AzureNodeTemplate>
      <TemplateName>AzureTemplate2</TemplateName>
      <SubscriptionId>ad4b9f9f-05f2-4c74-a83f-f2eb73000e0b</SubscriptionId>
      <CertificateId>1</CertificateId>
      <ServiceName>mytestsvc2</ServiceName>
      <StorageAccount>myteststorage2</StorageAccount>
      <Proxy>
        <UsesStaticProxyCount>false</UsesStaticProxyCount>     
        <ProxyRatio>100</ProxyRatio>
        <ProxyRatioBase>400</ProxyRatioBase>
      </Proxy>
      <OSVersion>WindowsServer2012</OSVersion>
    </AzureNodeTemplate>
  </AzureBurst>
</IaaSClusterConfig>
```

## <a name="troubleshooting"></a><span data-ttu-id="cd697-135">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="cd697-135">Troubleshooting</span></span>
* <span data-ttu-id="cd697-136">**Erreur de « Réseau virtuel n’existe pas »** -si vous exécutez hello script toodeploy plusieurs clusters dans Azure simultanément dans un seul abonnement, un ou plusieurs déploiements peuvent échouer avec l’erreur de hello « réseau virtuel *VNet\_nom* ne existe ».</span><span class="sxs-lookup"><span data-stu-id="cd697-136">**“VNet doesn’t exist” error** - If you run hello script toodeploy multiple clusters in Azure concurrently under one subscription, one or more deployments may fail with hello error “VNet *VNet\_Name* doesn't exist”.</span></span>
  <span data-ttu-id="cd697-137">Si cette erreur se produit, exécuter le script hello à nouveau pour le déploiement de hello a échoué.</span><span class="sxs-lookup"><span data-stu-id="cd697-137">If this error occurs, run hello script again for hello failed deployment.</span></span>
* <span data-ttu-id="cd697-138">**L’accès à des problème hello Internet à partir du réseau virtuel Azure de hello** : Si vous créez un cluster avec un contrôleur de domaine à l’aide du script de déploiement hello ou promouvoir manuellement un contrôleur de toodomain de machine virtuelle de nœud principal, vous pouvez rencontrer des problèmes connexion toohello de machines virtuelles hello Internet.</span><span class="sxs-lookup"><span data-stu-id="cd697-138">**Problem accessing hello Internet from hello Azure virtual network** - If you create a cluster with a new domain controller by using hello deployment script, or you manually promote a head node VM toodomain controller, you may experience problems connecting hello VMs toohello Internet.</span></span> <span data-ttu-id="cd697-139">Ce problème peut se produire si un serveur DNS redirecteur est automatiquement configuré sur le contrôleur de domaine hello et que ce serveur DNS redirecteur ne résout pas correctement.</span><span class="sxs-lookup"><span data-stu-id="cd697-139">This problem can occur if a forwarder DNS server is automatically configured on hello domain controller, and this forwarder DNS server doesn’t resolve properly.</span></span>
  
    <span data-ttu-id="cd697-140">toowork résoudre ce problème, ouvrez une session sur le contrôleur de domaine toohello et un paramètre de configuration de redirecteur hello supprimer ou configurer un serveur DNS redirecteur valide.</span><span class="sxs-lookup"><span data-stu-id="cd697-140">toowork around this problem, log on toohello domain controller and either remove hello forwarder configuration setting or configure a valid forwarder DNS server.</span></span> <span data-ttu-id="cd697-141">tooconfigure ce paramètre, dans le Gestionnaire de serveur, cliquez sur **outils** >
    **DNS** tooopen le Gestionnaire DNS, puis double-cliquez sur **redirecteurs**.</span><span class="sxs-lookup"><span data-stu-id="cd697-141">tooconfigure this setting, in Server Manager click **Tools** >
    **DNS** tooopen DNS Manager, and then double-click **Forwarders**.</span></span>
* <span data-ttu-id="cd697-142">**Problème d’accès au réseau RDMA à partir d’ordinateurs virtuels de calcul intensif** : Si vous ajoutez le calcul de Windows Server ou nœud de service Broker pour les machines virtuelles en utilisant un prenant en charge RDMA taille telles que A8 ou A9, vous pouvez rencontrer des problèmes de connexion ces réseau de machines virtuelles toohello RDMA application.</span><span class="sxs-lookup"><span data-stu-id="cd697-142">**Problem accessing RDMA network from compute-intensive VMs** - If you add Windows Server compute or broker node VMs using an RDMA-capable size such as A8 or A9, you may experience problems connecting those VMs toohello RDMA application network.</span></span> <span data-ttu-id="cd697-143">Ce problème se produit est si hello extension HpcVmDrivers n’est pas correctement installé lors de l’ajout d’ordinateurs virtuels de hello, toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="cd697-143">One reason this problem occurs is if hello HpcVmDrivers extension is not properly installed when hello VMs are added toohello cluster.</span></span> <span data-ttu-id="cd697-144">Par exemple, l’extension peut être bloquée dans hello installation état.</span><span class="sxs-lookup"><span data-stu-id="cd697-144">For example, the extension might be stuck in hello installing state.</span></span>
  
    <span data-ttu-id="cd697-145">toowork résoudre ce problème, la première hello vérifier l’état de l’extension hello hello sur des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="cd697-145">toowork around this problem, first check hello state of hello extension in hello VMs.</span></span> <span data-ttu-id="cd697-146">Si l’extension de hello n’est pas installée correctement, essayez de supprimer des nœuds de hello de cluster HPC de hello et puis ajoutez de nouveau les nœuds hello.</span><span class="sxs-lookup"><span data-stu-id="cd697-146">If hello extension is not properly installed, try removing hello nodes from hello HPC cluster and then add hello nodes again.</span></span> <span data-ttu-id="cd697-147">Par exemple, vous pouvez ajouter des machines virtuelles de nœud de calcul en exécutant le script Add-hpciaasnode.ps1 de hello sur le nœud principal de hello.</span><span class="sxs-lookup"><span data-stu-id="cd697-147">For example, you can add compute node VMs by running hello Add-HpcIaaSNode.ps1 script on hello head node.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd697-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cd697-148">Next steps</span></span>
* <span data-ttu-id="cd697-149">Essayez d’exécuter un test de charge sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="cd697-149">Try running a test workload on hello cluster.</span></span> <span data-ttu-id="cd697-150">Pour obtenir un exemple, consultez hello HPC Pack [mise en route](https://technet.microsoft.com/library/jj884144).</span><span class="sxs-lookup"><span data-stu-id="cd697-150">For an example, see hello HPC Pack [getting started guide](https://technet.microsoft.com/library/jj884144).</span></span>
* <span data-ttu-id="cd697-151">Pour un Bonjour didacticiel tooscript le déploiement du cluster et exécutez une charge de travail HPC, consultez [prise en main avec un cluster HPC Pack dans Azure toorun Excel et SOA les charges de travail](../../virtual-machines-windows-excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cd697-151">For a tutorial tooscript hello cluster deployment and run an HPC workload, see [Get started with an HPC Pack cluster in Azure toorun Excel and SOA workloads](../../virtual-machines-windows-excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="cd697-152">Essayez de toostart d’outils de Microsoft HPC Pack, arrêter, ajouter et supprimer des nœuds de calcul à partir d’un cluster que vous créez.</span><span class="sxs-lookup"><span data-stu-id="cd697-152">Try HPC Pack's tools toostart, stop, add, and remove compute nodes from a cluster you create.</span></span> <span data-ttu-id="cd697-153">Consultez [Gérer des nœuds de calcul dans un cluster HPC Pack dans Azure](hpcpack-cluster-node-manage.md).</span><span class="sxs-lookup"><span data-stu-id="cd697-153">See [Manage compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster-node-manage.md).</span></span>
* <span data-ttu-id="cd697-154">tooget configurer de cluster de toohello toosubmit travaux à partir d’un ordinateur local, consultez [cluster de travaux HPC de soumettre à partir d’un tooan d’ordinateur local HPC Pack dans Azure](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cd697-154">tooget set up toosubmit jobs toohello cluster from a local computer, see [Submit HPC jobs from an on-premises computer tooan HPC Pack cluster in Azure](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

