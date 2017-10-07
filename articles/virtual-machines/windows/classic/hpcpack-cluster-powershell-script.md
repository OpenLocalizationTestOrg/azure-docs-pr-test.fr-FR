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
# <a name="create-a-windows-high-performance-computing-hpc-cluster-with-hello-hpc-pack-iaas-deployment-script"></a>Créer un cluster de calcul de hautes performances (HPC) de Windows avec le script de déploiement IaaS de HPC Pack hello
Exécutez hello IaaS de HPC Pack déploiement PowerShell script toodeploy un cluster HPC Pack 2012 R2 complète pour les charges de travail Windows dans les machines virtuelles. cluster de Hello se compose d’un nœud principal joint à Active Directory Windows Server et Microsoft HPC Pack, et vous spécifiez des ressources de calcul de fenêtres supplémentaires. Si vous souhaitez toodeploy un cluster HPC Pack dans Azure pour les charges de travail Linux, consultez [créer un cluster HPC de Linux avec hello script de déploiement IaaS de HPC Pack](../../linux/classic/hpcpack-cluster-powershell-script.md). Vous pouvez également utiliser une toodeploy de modèle un cluster HPC Pack Azure Resource Manager. Pour obtenir des exemples, consultez [Création d’un cluster HPC](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/) et [Création d’un cluster HPC avec une image de nœud de calcul personnalisée](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-custom-image/).

> [!IMPORTANT] 
> Hello script PowerShell décrit dans cet article crée un cluster Microsoft HPC Pack 2012 R2 dans Azure à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.
> En outre, script hello décrit dans cet article ne prend pas en charge HPC Pack 2016.

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-files"></a>Exemples de fichiers de configuration
Bonjour les exemples suivants, remplacez par vos propres valeurs pour votre Id d’abonnement ou les nom et les noms de compte et le service de hello.

### <a name="example-1"></a>Exemple 1
Hello fichier de configuration suivant déploie un cluster HPC Pack qui a un nœud principal avec des bases de données locales et cinq nœuds de calcul exécutant le système d’exploitation de Windows Server 2012 R2 hello. Tous les services de cloud hello sont créés directement dans hello emplacement de l’ouest des États-Unis. nœud principal de Hello agit en tant que contrôleur de domaine de forêt de domaines hello.

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

### <a name="example-2"></a>Exemple 2
Hello, le fichier de configuration suivant déploie un cluster HPC Pack dans une forêt de domaines existante. cluster de Hello possède 1 nœud principal avec les bases de données locales et 12 nœuds par hello extension BGInfo VM appliquée.
L’installation automatique des mises à jour Windows est désactivée pour hello toutes les machines virtuelles dans la forêt de domaines hello. Tous les services de cloud hello sont créés directement dans l’emplacement de l’Asie. les nœuds de calcul Hello sont créés dans les trois services cloud et trois comptes de stockage : *MyHPCCN-0001* trop*MyHPCCN-0005* dans *MyHPCCNService01* et  *mycnstorage01*; *MyHPCCN-0006* trop*MyHPCCN0010* dans *MyHPCCNService02* et *mycnstorage02*; et  *MyHPCCN-0011* trop*MyHPCCN-0012* dans *MyHPCCNService03* et *mycnstorage03*). les nœuds de calcul Hello sont créés à partir d’une image privée existante capturée à partir d’un nœud de calcul. Hello automatique augmenter et réduire le service est activé avec la valeur par défaut augmenter et réduire les intervalles.

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

### <a name="example-3"></a>Exemple 3
Hello, le fichier de configuration suivant déploie un cluster HPC Pack dans une forêt de domaines existante. cluster de Hello contient un seul nœud principal, un serveur de base de données avec un disque de données de 500 Go, deux nœuds de broker exécutant le système d’exploitation de Windows Server 2012 R2 hello et cinq nœuds de calcul exécutant le système d’exploitation de Windows Server 2012 R2 hello. Hello service cloud MyHPCCNService est créé dans le groupe d’affinités de hello *MyIBAffinityGroup*, et autres services de cloud computing hello sont créés dans le groupe d’affinités de hello *MyAffinityGroup*. Hello API REST de Scheduler de travail HPC et le portail web HPC sont activés sur le nœud principal de hello.

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



### <a name="example-4"></a>Exemple 4
Hello, le fichier de configuration suivant déploie un cluster HPC Pack dans une forêt de domaines existante. cluster de Hello possède deux nœud principal avec les bases de données locales, deux modèles de nœud Azure sont créés, et trois nœuds de support Azure de taille sont créés pour le modèle de nœud Azure *AzureTemplate1*. Un fichier de script s’exécute sur le nœud principal de hello après la configuration du nœud principal hello.

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

## <a name="troubleshooting"></a>Résolution des problèmes
* **Erreur de « Réseau virtuel n’existe pas »** -si vous exécutez hello script toodeploy plusieurs clusters dans Azure simultanément dans un seul abonnement, un ou plusieurs déploiements peuvent échouer avec l’erreur de hello « réseau virtuel *VNet\_nom* ne existe ».
  Si cette erreur se produit, exécuter le script hello à nouveau pour le déploiement de hello a échoué.
* **L’accès à des problème hello Internet à partir du réseau virtuel Azure de hello** : Si vous créez un cluster avec un contrôleur de domaine à l’aide du script de déploiement hello ou promouvoir manuellement un contrôleur de toodomain de machine virtuelle de nœud principal, vous pouvez rencontrer des problèmes connexion toohello de machines virtuelles hello Internet. Ce problème peut se produire si un serveur DNS redirecteur est automatiquement configuré sur le contrôleur de domaine hello et que ce serveur DNS redirecteur ne résout pas correctement.
  
    toowork résoudre ce problème, ouvrez une session sur le contrôleur de domaine toohello et un paramètre de configuration de redirecteur hello supprimer ou configurer un serveur DNS redirecteur valide. tooconfigure ce paramètre, dans le Gestionnaire de serveur, cliquez sur **outils** >
    **DNS** tooopen le Gestionnaire DNS, puis double-cliquez sur **redirecteurs**.
* **Problème d’accès au réseau RDMA à partir d’ordinateurs virtuels de calcul intensif** : Si vous ajoutez le calcul de Windows Server ou nœud de service Broker pour les machines virtuelles en utilisant un prenant en charge RDMA taille telles que A8 ou A9, vous pouvez rencontrer des problèmes de connexion ces réseau de machines virtuelles toohello RDMA application. Ce problème se produit est si hello extension HpcVmDrivers n’est pas correctement installé lors de l’ajout d’ordinateurs virtuels de hello, toohello cluster. Par exemple, l’extension peut être bloquée dans hello installation état.
  
    toowork résoudre ce problème, la première hello vérifier l’état de l’extension hello hello sur des machines virtuelles. Si l’extension de hello n’est pas installée correctement, essayez de supprimer des nœuds de hello de cluster HPC de hello et puis ajoutez de nouveau les nœuds hello. Par exemple, vous pouvez ajouter des machines virtuelles de nœud de calcul en exécutant le script Add-hpciaasnode.ps1 de hello sur le nœud principal de hello.

## <a name="next-steps"></a>Étapes suivantes
* Essayez d’exécuter un test de charge sur le cluster de hello. Pour obtenir un exemple, consultez hello HPC Pack [mise en route](https://technet.microsoft.com/library/jj884144).
* Pour un Bonjour didacticiel tooscript le déploiement du cluster et exécutez une charge de travail HPC, consultez [prise en main avec un cluster HPC Pack dans Azure toorun Excel et SOA les charges de travail](../../virtual-machines-windows-excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Essayez de toostart d’outils de Microsoft HPC Pack, arrêter, ajouter et supprimer des nœuds de calcul à partir d’un cluster que vous créez. Consultez [Gérer des nœuds de calcul dans un cluster HPC Pack dans Azure](hpcpack-cluster-node-manage.md).
* tooget configurer de cluster de toohello toosubmit travaux à partir d’un ordinateur local, consultez [cluster de travaux HPC de soumettre à partir d’un tooan d’ordinateur local HPC Pack dans Azure](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

