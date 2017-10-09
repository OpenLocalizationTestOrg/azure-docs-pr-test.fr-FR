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
# <a name="create-a-linux-high-performance-computing-hpc-cluster-with-hello-hpc-pack-iaas-deployment-script"></a>Créer un cluster de calcul de hautes performances (HPC) Linux avec le script de déploiement IaaS de HPC Pack hello
Exécutez hello IaaS de HPC Pack déploiement PowerShell script toodeploy un cluster HPC Pack 2012 R2 complète pour les charges de travail Linux dans des machines virtuelles. cluster de Hello se compose d’un nœud principal joint à Active Directory Windows Server et Microsoft HPC Pack et les nœuds de calcul qui exécutent une Hello distributions Linux prises en charge par HPC Pack. Si vous souhaitez toodeploy un cluster HPC Pack dans les charges de travail Azure pour Windows, consultez [créer un cluster HPC Windows avec hello script de déploiement IaaS de HPC Pack](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Vous pouvez également utiliser une toodeploy de modèle un cluster HPC Pack Azure Resource Manager. Pour obtenir un exemple, consultez [Création d’un cluster HPC avec des nœuds de calcul Linux](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/).

> [!IMPORTANT] 
> Hello script PowerShell décrit dans cet article crée un cluster Microsoft HPC Pack 2012 R2 dans Azure à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.
> En outre, script hello décrit dans cet article ne prend pas en charge HPC Pack 2016.

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-file"></a>Exemple de fichier de configuration
Hello fichier de configuration suivant crée un contrôleur de domaine et la forêt de domaines et déploie un cluster HPC Pack qui a un seul nœud principal avec les bases de données locales et 10 nœuds de calcul Linux. Tous les services de cloud hello sont créés directement dans l’emplacement Asie orientale hello. les nœuds de calcul Linux Hello sont créés dans les deux services de cloud computing et les deux comptes de stockage (autrement dit, *MyLnxCN à 0001* à *MyLnxCN-0005* dans *MyLnxCNService01* et *mylnxstorage01*, et *MyLnxCN-0006* à *MyLnxCN-0010* dans *MyLnxCNService02* et *mylnxstorage02* ). les nœuds de calcul Hello sont créés à partir d’une image de Linux OpenLogic CentOS version 7.0. 

Remplacez par vos propres valeurs pour votre nom d’abonnement et les noms de compte et le service de hello.

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
## <a name="troubleshooting"></a>Résolution des problèmes
* **Erreur « Le réseau virtuel n’existe pas »**. Si vous exécutez hello IaaS de HPC Pack déploiement script toodeploy plusieurs clusters dans Azure simultanément dans un seul abonnement, un ou plusieurs déploiements peuvent échouer avec l’erreur de hello « réseau virtuel *VNet\_nom* n’existe pas ».
  Si cette erreur se produit, réexécutez le script hello pour le déploiement de hello a échoué.
* **L’accès à des problème hello Internet à partir du réseau virtuel Azure de hello**. Si vous créez un cluster HPC Pack avec un contrôleur de domaine à l’aide du script de déploiement hello ou que vous promouvez manuellement un contrôleur de toodomain de machine virtuelle de nœud principal, vous pouvez rencontrer des problèmes de connexion des machines virtuelles de hello dans toohello de réseau virtuel Azure hello Internet. Cela peut se produire si un serveur DNS redirecteur est automatiquement configuré sur le contrôleur de domaine hello et que ce serveur DNS redirecteur ne résout pas correctement.
  
    toowork résoudre ce problème, ouvrez une session sur le contrôleur de domaine toohello et un paramètre de configuration de redirecteur hello supprimer ou configurer un serveur DNS redirecteur valide. toodo, cliquez sur Gestionnaire de serveur **outils** > **DNS** tooopen le Gestionnaire DNS, puis double-cliquez sur **redirecteurs**.

## <a name="next-steps"></a>Étapes suivantes
* Consultez [prise en main des nœuds de calcul Linux dans un cluster HPC Pack dans Azure](hpcpack-cluster.md) pour plus d’informations sur les distributions Linux prises en charge, déplacement de données et l’envoi de cluster HPC Pack travaux tooan Linux les nœuds de calcul.
* Pour consulter des didacticiels qui utilisent des hello script toocreate un cluster et exécuter une charge de travail Linux HPC, consultez :
  * [Exécution de NAMD avec Microsoft HPC Pack sur des nœuds de calcul Linux dans Azure](hpcpack-cluster-namd.md)
  * [Exécution d’OpenFOAM avec Microsoft HPC Pack sur des nœuds de calcul Linux dans Azure](hpcpack-cluster-openfoam.md)
  * [Exécution de STAR-CCM+ avec Microsoft HPC Pack sur des nœuds de calcul Linux dans Azure](hpcpack-cluster-starccm.md)

