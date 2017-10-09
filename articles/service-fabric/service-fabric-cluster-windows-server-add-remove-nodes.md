---
title: "cluster nœuds tooa autonome Service Fabric aaaAdd ou supprimez | Documents Microsoft"
description: "Découvrez comment tooadd ou supprimez tooan de nœuds Azure Service Fabric de cluster sur un ordinateur physique ou virtuel exécutant Windows Server, qui peut être local ou dans n’importe quel cloud."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: bc6b8fc0-d2af-42f8-a164-58538be38d02
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 2/02/2017
ms.author: dekapur
ms.openlocfilehash: 1da908ad9840faa052e0b4021bc2d4ce732b02bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-remove-nodes-tooa-standalone-service-fabric-cluster-running-on-windows-server"></a>Ajouter ou supprimer le cluster Service Fabric nœuds tooa autonome sont en cours d’exécution sur Windows Server
Une fois que vous avez [créé votre cluster de Service Fabric autonomes sur les ordinateurs Windows Server](service-fabric-cluster-creation-for-windows-server.md), les besoins de votre entreprise peuvent changer et que vous deviez tooadd ou supprimer le cluster tooyour de nœuds. Cet article fournit des instructions détaillées tooachieve cela. Veuillez noter que la fonctionnalité d’ajout/suppression de nœud n’est pas prise en charge dans les clusters de développement locaux.

## <a name="add-nodes-tooyour-cluster"></a>Ajouter tooyour nœuds du cluster
1. Préparation hello VM/machine à tooadd tooyour cluster en suivant les étapes de hello mentionnés dans hello [hello de préparer les ordinateurs toomeet conditions préalables de hello pour le déploiement de cluster](service-fabric-cluster-creation-for-windows-server.md) section
2. Identifier les domaine d’erreur et la mise à niveau domaine vous tooadd du cours de cet ordinateur virtuel/ordinateur
3. Bureau à distance (RDP) dans hello VM/machine que vous souhaitez tooadd toohello cluster
4. Copie ou [télécharger le package autonome de hello pour Service Fabric pour Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) toohello VM/machine et décompressez le package de hello
5. Exécuter Powershell avec des privilèges élevés et naviguer toohello l’emplacement du package décompressé de hello
6. Exécutez hello *AddNode.ps1* script avec les paramètres de hello décrivant hello nouveau nœud tooadd. exemple Hello ci-dessous ajoute un nouveau nœud appelé VM5, avec le type NodeType0 et une adresse IP 182.17.34.52, UD1 et fd : / dc1/r0. Hello *ExistingClusterConnectionEndPoint* est déjà un point de terminaison de connexion pour un nœud de cluster existant de hello, qui peut être adresse IP hello *tout* nœud hello cluster.

    ```
    .\AddNode.ps1 -NodeName VM5 -NodeType NodeType0 -NodeIPAddressorFQDN 182.17.34.52 -ExistingClientConnectionEndpoint 182.17.34.50:19000 -UpgradeDomain UD1 -FaultDomain fd:/dc1/r0 -AcceptEULA
    ```
    Une fois le script de hello terminée, vous pouvez vérifier si le nouveau nœud de hello a été ajoutée en exécutant hello [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) applet de commande.

7. cohérence tooensure sur différents nœuds dans un cluster de hello, vous devez lancer une mise à niveau de la configuration. Exécutez [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello du dernier fichier de configuration et ajoutez hello nouvellement ajoutés nœud trop section « Nœuds ». Il est également recommandé tooalways hello cluster configuration la plus récente disponible dans les cas de hello que vous avez besoin de tooredploy un cluster avec hello même configuration.

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
8. Exécutez [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) mise à niveau de toobegin hello.

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    Vous pouvez surveiller la progression de hello de mise à niveau de hello sur Service Fabric Explorer. Vous pouvez également exécuter [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps) pour cela.

### <a name="add-nodes-tooclusters-configured-with-windows-security-using-gmsa"></a>Ajouter des nœuds tooclusters configuré avec la sécurité de Windows à l’aide de service administré de groupe
Pour les clusters configurés avec un compte de service géré de groupe (gMSA, Group Managed Service Account) (https://technet.microsoft.com/library/hh831782.aspx), un nouveau nœud peut être ajouté à l’aide d’une mise à niveau de la configuration :
1. Exécutez [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) sur tous les nœuds existants hello tooget hello du dernier fichier de configuration et ajouter des détails sur le nouveau nœud de hello souhaité tooadd dans la section de hello « nœuds ». Assurez-vous que le nouveau nœud de hello fait partie de hello compte géré de groupe. Ce compte doit être un compte Administrateur sur tous les ordinateurs.

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
2. Exécutez [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) mise à niveau de toobegin hello.

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>
    ```
    Vous pouvez surveiller la progression de hello de mise à niveau de hello sur Service Fabric Explorer. Vous pouvez également exécuter [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps) pour cela.

### <a name="add-node-types-tooyour-cluster"></a>Ajouter un cluster de tooyour de types de nœud
Commande tooadd un nouveau type de nœud, modifiez votre configuration tooinclude hello nouveau type de nœud dans la section « NodeTypes » sous « Propriétés » et commencer une configuration de mise à niveau de l’aide [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps). Une fois la mise à niveau hello terminée, vous pouvez ajouter le nouveau cluster tooyour de nœuds avec ce type de nœud.

## <a name="remove-nodes-from-your-cluster"></a>Supprimer des nœuds de votre cluster
Un nœud peut être supprimé à partir d’un cluster à l’aide d’une mise à niveau de la configuration, Bonjour suivant de manière :

1. Exécutez [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) le fichier de configuration plus récent tooget hello et *supprimer* nœud hello à partir de la section « Nœuds ».
Ajouter hello « NodesToBeRemoved » paramètre trop » le programme d’installation « section au sein de la section de « FabricSettings ». Hello « valeur » doit être une liste séparée par des virgules des noms de nœud des nœuds qui doivent toobe supprimé.

    ```
         "fabricSettings": [
            {
            "name": "Setup",
            "parameters": [
                {
                "name": "FabricDataRoot",
                "value": "C:\\ProgramData\\SF"
                },
                {
                "name": "FabricLogRoot",
                "value": "C:\\ProgramData\\SF\\Log"
                },
                {
                "name": "NodesToBeRemoved",
                "value": "vm0, vm1"
                }
            ]
            }
        ]
    ```
2. Exécutez [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) mise à niveau de toobegin hello.

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    Vous pouvez surveiller la progression de hello de mise à niveau de hello sur Service Fabric Explorer. Vous pouvez également exécuter [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps) pour cela.

> [!NOTE]
> La suppression de nœuds peut entraîner plusieurs mises à niveau. Certains nœuds sont marqués avec `IsSeedNode=”true”` de balise et peut être identifiée en interrogeant le cluster de hello manifeste à l’aide de `Get-ServiceFabricClusterManifest`. Étant donné que les nœuds de départ hello portera toobe déplacé dans de tels scénarios, la suppression de ces nœuds peut prendre plus de temps que d’autres. cluster de Hello doit maintenir un minimum de 3 nœuds de type de nœud principal.
> 
> 

### <a name="remove-node-types-from-your-cluster"></a>Supprimer des types de nœuds de votre cluster
Avant de supprimer un type de nœud, vérifiez s’il existe des nœuds référençant le type de nœud hello. Supprimez ces nœuds avant de supprimer le type de nœud hello correspondant. Une fois que tous les nœuds correspondants sont supprimés, vous pouvez supprimer hello NodeType de configuration du cluster hello et commencer une configuration de mise à niveau de l’aide [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).


### <a name="replace-primary-nodes-of-your-cluster"></a>Remplacer les nœuds principaux de votre cluster
remplacement de Hello de nœuds principaux doit être effectuée un seul nœud après l’autre, au lieu de supprimer, puis ajouter dans des lots.


## <a name="next-steps"></a>Étapes suivantes
* [Paramètres de configuration pour un cluster Windows autonome](service-fabric-cluster-manifest.md)
* [Sécuriser un cluster autonome sur Windows à l’aide de certificats X509](service-fabric-windows-cluster-x509-security.md)
* [Créer un cluster Service Fabric autonome avec des machines virtuelles Azure Windows](service-fabric-cluster-creation-with-windows-azure-vms.md)

