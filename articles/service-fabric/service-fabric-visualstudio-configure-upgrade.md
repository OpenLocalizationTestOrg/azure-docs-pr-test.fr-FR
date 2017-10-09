---
title: "mise à niveau de hello aaaConfigure d’une application de Service Fabric | Documents Microsoft"
description: "Découvrez comment tooconfigure hello les paramètres de mise à niveau d’une application de Service Fabric à l’aide de Microsoft Visual Studio."
services: service-fabric
documentationcenter: na
author: mikkelhegn
manager: mfussell
editor: tglee
ms.assetid: 1757ba85-0b7b-4f16-8a23-2ddaa61c86c6
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/29/2017
ms.author: mikkelhegn
ms.openlocfilehash: 8ca50aa9d911f3c98f017490c8fe29011e8d80cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-upgrade-of-a-service-fabric-application-in-visual-studio"></a>Configurer la mise à niveau hello d’une application de Service Fabric dans Visual Studio
Visual Studio tools pour Azure Service Fabric fournissent la prise en charge de mise à niveau pour la publication toolocal ou des clusters distants. Il existe trois scénarios dans lesquels vous tooupgrade tooa nouvelle version de votre application au lieu de remplacer l’application hello durant les tests et de débogage :

* Données d’application ne seront pas perdues pendant la mise à niveau hello.
* Disponibilité reste élevée afin qu’il ne sera pas y avoir toute interruption de service au cours de la mise à niveau de hello, s’il y a que suffisamment d’instances de service réparties sur plusieurs domaines de mise à niveau.
* Une application peut faire l’objet de tests pendant sa mise à niveau.

## <a name="parameters-needed-tooupgrade"></a>Les paramètres nécessaires tooupgrade
Vous avez le choix entre deux types de déploiement : standard ou mise à niveau. Un déploiement régulière efface les données sur le cluster de hello et les informations sur le déploiement précédent pendant un déploiement de mise à niveau conserve. Lorsque vous mettez à niveau une application de Service Fabric dans Visual Studio, vous devez tooprovide paramètres de mise à niveau l’application et les stratégies de contrôle d’intégrité. Mise à niveau de l’application les paramètres permettent de contrôler la mise à niveau de la hello, tandis que les stratégies de contrôle d’intégrité déterminent si la mise à niveau hello a réussi. Pour en savoir plus, consultez [Mise à niveau d’une application Service Fabric : paramètres de mise à niveau](service-fabric-application-upgrade-parameters.md) .

Il existe trois modes de mise à niveau : *Monitored*, *UnmonitoredAuto* et *UnmonitoredManual*.

* Une mise à niveau analysées automatise la mise à niveau hello et application du contrôle d’intégrité.
* Une mise à niveau UnmonitoredAuto automatise la mise à niveau hello, mais ignore hello intégrité d’application.
* Lorsque vous effectuez une mise à niveau UnmonitoredManual, vous devez toomanually mise à niveau de chaque domaine de mise à niveau.

Chaque mode de mise à niveau nécessite différents jeux de paramètres. Consultez [paramètres de mise à niveau l’Application](service-fabric-application-upgrade-parameters.md) toolearn plus d’informations sur les options de mise à niveau disponibles hello.

## <a name="upgrade-a-service-fabric-application-in-visual-studio"></a>Mise à niveau d’une application Service Fabric dans Visual Studio
Si vous utilisez hello Visual Studio Service Fabric tools tooupgrade une application de Service Fabric, vous pouvez spécifier une mise à niveau au lieu d’un déploiement régulière un toobe de processus de publication en vérifiant hello **mise à niveau d’application hello** vérifier zone.

### <a name="tooconfigure-hello-upgrade-parameters"></a>paramètres de mise à niveau tooconfigure hello
1. Cliquez sur hello **paramètres** bouton toohello case à cocher. Hello **modifier les paramètres de mise à niveau** boîte de dialogue s’affiche. Hello **modifier les paramètres de mise à niveau** boîte de dialogue prend en charge les modes mise à niveau de hello surveillés, UnmonitoredAuto et UnmonitoredManual.
2. Sélectionnez hello le mode de mise à niveau que vous souhaitez toouse et puis remplissez à la grille de paramètres hello.

    Chaque paramètre a des valeurs par défaut. paramètre facultatif de Hello *DefaultServiceTypeHealthPolicy* prend une entrée de table de hachage. Voici un exemple de format d’entrée de la table de hachage d’hello pour *DefaultServiceTypeHealthPolicy*:

    ```
    @{ ConsiderWarningAsError = "false"; MaxPercentUnhealthyDeployedApplications = 0; MaxPercentUnhealthyServices = 0; MaxPercentUnhealthyPartitionsPerService = 0; MaxPercentUnhealthyReplicasPerPartition = 0 }
    ```

    *ServiceTypeHealthPolicyMap* est un autre paramètre facultatif qui accepte une entrée de table de hachage Bonjour suivant format :

    ```    
    @ {"ServiceTypeName" : "MaxPercentUnhealthyPartitionsPerService,MaxPercentUnhealthyReplicasPerPartition,MaxPercentUnhealthyServices"}
    ```

    Voici un exemple concret :

    ```
    @{ "ServiceTypeName01" = "5,10,5"; "ServiceTypeName02" = "5,5,5" }
    ```
3. Si vous sélectionnez le mode de mise à niveau UnmonitoredManual, vous devez manuellement un toocontinue de console PowerShell et terminer le processus de mise à niveau hello. Consultez trop[mise à niveau de Service Fabric application : rubriques avancées](service-fabric-application-upgrade-advanced.md) toolearn manuel Mise à niveau fonctionne.

## <a name="upgrade-an-application-by-using-powershell"></a>Mettre à niveau une application à l’aide de PowerShell
Vous pouvez utiliser les applets de commande de PowerShell tooupgrade une application de Service Fabric. Pour plus d’informations, consultez [Didacticiel sur la mise à niveau d’une application Service Fabric](service-fabric-application-upgrade-tutorial.md) et [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx).

## <a name="specify-a-health-check-policy-in-hello-application-manifest-file"></a>Spécifier une stratégie de contrôle d’intégrité dans le fichier manifeste d’application hello
Chaque service dans une application de Service Fabric peut avoir ses propres paramètres de stratégie de contrôle d’intégrité qui remplacent les valeurs par défaut de hello. Vous pouvez fournir ces valeurs de paramètre dans le fichier manifeste d’application hello.

Hello suivant montre comment tooapply un contrôle d’intégrité unique vérifier la stratégie pour chaque service dans le manifeste de l’application hello.

```xml
<Policies>
    <HealthPolicy ConsiderWarningAsError="false" MaxPercentUnhealthyDeployedApplications="20">
        <DefaultServiceTypeHealthPolicy MaxPercentUnhealthyServices="20"               
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />
        <ServiceTypeHealthPolicy ServiceTypeName="ServiceTypeName1"
                MaxPercentUnhealthyServices="20"
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />      
    </HealthPolicy>
</Policies>
```
## <a name="next-steps"></a>Étapes suivantes
Pour plus d'informations sur le déploiement d'une application, consultez la page [Déploiement d’une application existante dans Azure Service Fabric](service-fabric-deploy-existing-app.md).