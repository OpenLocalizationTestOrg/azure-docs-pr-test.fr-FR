---
title: "aaaAzure l’agrégation d’événements Service Fabric avec Linux Azure Diagnostics | Documents Microsoft"
description: "Découvrez l’agrégation et la collecte d’événements à l’aide de Linux Azure Diagnostics (LAD) pour la surveillance et le diagnostic de clusters Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/17/2017
ms.author: dekapur
ms.openlocfilehash: aefa869219a0dd219e01e6574816fe3ce47fe472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-linux-azure-diagnostics"></a>Agrégation et collection d’événements à l’aide de Linux Azure Diagnostics
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-event-aggregation-wad.md)
> * [Linux](service-fabric-diagnostics-event-aggregation-lad.md)
>
>

Lorsque vous exécutez un cluster Azure Service Fabric, il s’agit d’une bonne idée toocollect hello les journaux à partir de tous les nœuds hello dans un emplacement central. Ayant hello journaux dans un emplacement central vous permet d’analyser et résoudre les problèmes de votre cluster, ou dans les applications hello et les services exécutés dans ce cluster.

Tooupload d’une façon et collecter des journaux est extension toouse hello Linux Azure Diagnostics (SCÉNARISTE), qui télécharge les journaux tooAzure stockage et est également hello option toosend journaux tooAzure Application Insights ou concentrateurs d’événements. Vous pouvez également utiliser un processus externe tooread hello d’événements à partir du stockage et les placer dans un produit de plateforme d’analyse, tels que [Analytique des journaux OMS](../log-analytics/log-analytics-service-fabric.md) ou une autre solution d’analyse de journal.

## <a name="log-and-event-sources"></a>Sources de journaux et d’événements

### <a name="service-fabric-platform-events"></a>Événements de la plateforme Service Fabric
Service Fabric émet quelques journaux prêts à l’emploi via [LTTng](http://lttng.org), notamment les événements opérationnels ou des événements du runtime. Ces journaux sont stockés dans l’emplacement hello hello modèle spécifie le Gestionnaire de ressources du cluster. tooget ou définir les détails de compte de stockage hello, recherchez la balise de hello **AzureTableWinFabETWQueryable** et recherchez **StoreConnectionString**.

### <a name="application-events"></a>Événements liés aux applications
 Les événements émis à partir du code de vos applications et services tel que spécifié par vous-même lors de l’instrumentation de votre logiciel. Vous pouvez utiliser une solution de journalisation qui écrit des fichiers journaux textuels, par exemple LTTng. Pour plus d’informations, consultez la documentation de LTTng hello le suivi de votre application.

[Surveillance et diagnostic des services dans une configuration de développement d’ordinateur local](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).

## <a name="deploy-hello-diagnostics-extension"></a>Déployer l’extension de Diagnostics hello
Hello première étape de collecte de journaux est l’extension de Diagnostics toodeploy hello sur chacune des machines virtuelles de hello dans le cluster Service Fabric de hello. Hello, extension de diagnostic collecte des journaux sur chaque machine virtuelle et les charge compte de stockage toohello que vous spécifiez. étapes de Hello varient selon que vous utilisez hello portail Azure ou Azure Resource Manager.

toodeploy hello Diagnostics extension toohello machines virtuelles dans le cluster hello dans le cadre de la création du cluster, définissez **Diagnostics** trop**sur**. Après avoir créé le cluster de hello, vous ne pouvez pas modifier ce paramètre à l’aide du portail de hello.

Ensuite, configurez les fichiers de hello toocollect Linux Azure Diagnostics (SCÉNARISTE) et les placer dans votre compte de stockage. Ce processus est expliqué en tant que scénario 3 (« charger vos propres fichiers journaux ») dans l’article de hello [à l’aide de SCÉNARISTE toomonitor et diagnostiquer les machines virtuelles Linux](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json). Après cette Obtient de processus que vous l’accès toohello effectue le suivi. Vous pouvez télécharger le visualiseur de tooa hello traces de votre choix.

Vous pouvez également déployer l’extension de Diagnostics hello à l’aide du Gestionnaire de ressources Azure. Hello processus est similaire pour Windows et Linux et est documenté pour les clusters Windows dans [comment toocollect se connecte avec Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md).

Vous pouvez également utiliser Operations Management Suite, comme indiqué dans [Operations Management Suite Log Analytics with Linux (Analyse des journaux Operations Management Suite avec Linux)](https://blogs.technet.microsoft.com/hybridcloud/2016/01/28/operations-management-suite-log-analytics-with-linux/).

Après avoir terminé cette configuration, analyses de l’agent hello SCÉNARISTE hello des fichiers journaux spécifiés. Chaque fois qu’une nouvelle ligne est ajoutée toohello fichier, il crée une entrée de journal système qui est envoyé toohello de stockage que vous avez spécifié.

## <a name="next-steps"></a>Étapes suivantes

toounderstand plus en détail les événements que vous devez examiner lors de la résolution des problèmes, consultez [LTTng documentation](http://lttng.org/docs) et [à l’aide de SCÉNARISTE](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).
