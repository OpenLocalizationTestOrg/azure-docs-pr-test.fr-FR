---
title: "aaaCreate autonome de cluster avec les machines virtuelles Azure exécutant Windows | Documents Microsoft"
description: "Découvrez comment toocreate et gérer un cluster Azure Service Fabric sur les machines virtuelles Azure exécutant Windows Server."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 7eeb40d2-fb22-4a77-80ca-f1b46b22edbc
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: ryanwi;chackdan
redirect_url: /azure/service-fabric/service-fabric-cluster-creation-via-arm
ms.openlocfilehash: 8900204fe69887a7a0ca54b06e0d32534421bcfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-three-node-standalone-service-fabric-cluster-with-azure-virtual-machines-running-windows-server"></a>Créer un cluster Service Fabric autonome à trois nœuds avec des machines virtuelles Azure sous Windows Server
Cet article décrit comment toocreate un cluster sur Windows Azure ordinateurs virtuels (VM), à l’aide de hello programme d’installation de l’infrastructure de Service autonome pour Windows Server. scénario de Hello est un cas spécial de [créer et gérer un cluster exécutant Windows Server](service-fabric-cluster-creation-for-windows-server.md) où les ordinateurs virtuels de hello sont [machines virtuelles Azure exécutant Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), mais vous ne créez pas [Azure cluster Service Fabric informatique](service-fabric-cluster-creation-via-portal.md). distinction Hello dans ce modèle est cluster Service Fabric autonomes hello créé par hello comme suit est entièrement géré par vous, tandis que hello Service nuage Azure Fabric clusters sont gérés et mis à niveau par hello Service Fabric fournisseur de ressources.

## <a name="steps-toocreate-hello-standalone-cluster"></a>Cluster d’étapes toocreate hello autonome
1. Connectez-vous à toohello portail Azure et créer un nouveau Windows Server 2012 R2 Datacenter ou Windows Server 2016 VM de centre de données dans un groupe de ressources. Lire l’article de hello [créer une machine virtuelle Windows Bonjour Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) pour plus d’informations.
2. Ajouter quelques toohello de machines virtuelles plus même groupe de ressources. Assurez-vous que chacune des machines virtuelles de hello a hello même nom d’utilisateur administrateur et un mot de passe lors de la création. Une fois créé, vous devez voir tous les trois machines virtuelles Bonjour même réseau virtuel.
3. Se connecter tooeach Hello machines virtuelles et de désactiver le pare-feu Windows à l’aide de hello hello [Gestionnaire de serveur, tableau de bord de serveur Local](https://technet.microsoft.com/library/jj134147.aspx). Cela garantit que le trafic réseau de hello peut communiquer entre les machines hello. Lors de l’ordinateur de tooeach connecté, obtenir l’adresse IP de hello en ouvrant une invite de commandes et en tapant `ipconfig`. Vous pouvez également voir hello IP adresse de chaque ordinateur sur le portail hello, en sélectionnant des ressources du réseau virtuel hello pour le groupe de ressources hello et en vérifiant les interfaces réseau de hello créés pour chacun de ces ordinateurs.
4. Se connecter tooone Hello machines virtuelles et test ping hello autres deux machines virtuelles avec succès.
5. Se connecter tooone Hello machines virtuelles et [télécharger le package de Service Fabric hello autonome pour Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) dans un nouveau dossier sur hello machine et extraire le package de hello.
6. Ouvrez hello *ClusterConfig.Unsecure.MultiMachine.json* dans le bloc-notes et modifier chaque nœud avec des adresses IP hello trois ordinateurs de hello. Modifier le nom du cluster hello haut hello et enregistrez le fichier de hello.  Voici un exemple partiels hello du manifeste du cluster.
   
    ```
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "01-2017",
        "nodes": [
        {
            "nodeName": "standalonenode0",
            "iPAddress": "10.1.0.4",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD0"
        },
        {
            "nodeName": "standalonenode1",
            "iPAddress": "10.1.0.5",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc2/r0",
            "upgradeDomain": "UD1"
        },
        {
            "nodeName": "standalonenode2",
            "iPAddress": "10.1.0.6",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc3/r0",
            "upgradeDomain": "UD2"
        }
        ],
    ```
7. Si vous envisagez cette toobe un cluster sécurisé, décider de mesures de sécurité hello vous comme toouse et suivez les étapes de hello en hello associés lien : [X509 certificat](service-fabric-windows-cluster-x509-security.md) ou [sécurité Windows](service-fabric-windows-cluster-windows-security.md). Si la configuration de cluster hello à l’aide de la sécurité de Windows, vous devez tooset d’un toomanage de contrôleur de domaine Active Directory. Notez que l’utilisation d’un ordinateur de contrôleur de domaine en tant que nœud Service Fabric n'est pas prise en charge.
8. Ouvrez une [fenêtre PowerShell ISE](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise). Accédez toohello dossier où vous extrait le package de programme d’installation autonome téléchargé hello et enregistré le fichier de configuration de cluster hello. Exécutez hello suivant du cluster de hello de toodeploy de commande PowerShell :
   
    ```
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.MultiMachine.json
    ```

script de Hello configure à distance cluster Service Fabric de hello et doit créer un rapport Progression comme déploiement restaure via.

9. Après environ une minute, vous pouvez vérifier si le cluster de hello est opérationnel en vous connectant toohello Service Fabric Explorer à l’aide de IP l’ordinateur hello adresses, par exemple à l’aide de `http://10.1.0.5:19080/Explorer/index.html`. 

## <a name="next-steps"></a>Étapes suivantes
* [Créer des clusters Service Fabric autonomes sur un serveur Windows Server ou Linux](service-fabric-deploy-anywhere.md)
* [Ajouter ou supprimer le cluster Service Fabric de nœuds tooa autonome](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [Paramètres de configuration pour un cluster Windows autonome](service-fabric-cluster-manifest.md)
* [Sécuriser un cluster autonome sur Windows à l’aide de la sécurité Windows](service-fabric-windows-cluster-windows-security.md)
* [Sécuriser un cluster autonome sur Windows à l’aide de certificats X509](service-fabric-windows-cluster-x509-security.md)

