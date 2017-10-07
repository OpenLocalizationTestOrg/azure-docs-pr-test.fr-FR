---
title: "journaux aaaCollect à l’aide des Diagnostics Azure Linux | Documents Microsoft"
description: "Cet article décrit comment tooset des Diagnostics Windows Azure toocollect se connecte à partir d’un cluster Service Fabric Linux s’exécutant dans Azure."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: a160d469-8b7d-4560-82dd-8500db34a44a
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/28/2017
ms.author: subramar
ms.openlocfilehash: f61172876e744ea3e361f9ae513254239d6ba27f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-logs-by-using-azure-diagnostics"></a>Collecte des journaux avec Azure Diagnostics
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-setup-wad.md)
> * [Linux](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

Lorsque vous exécutez un cluster Azure Service Fabric, il s’agit d’une bonne idée toocollect hello les journaux à partir de tous les nœuds hello dans un emplacement central. Hello journaux dans un emplacement central rend facile tooanalyze et résoudre les problèmes, qu’ils soient dans vos services, votre application ou le cluster hello lui-même. Tooupload d’une façon et collecter des journaux est l’extension de Diagnostics Windows Azure hello toouse, les téléchargements de journaux tooAzure stockage, Azure Application Insights ou Azure Event Hubs. Vous pouvez également lire les événements de hello de stockage ou les concentrateurs d’événements et les placer dans un produit tel que [Analytique de journal](../log-analytics/log-analytics-service-fabric.md) ou une autre solution d’analyse de journal. [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) est fourni avec un service complet de recherche dans les journaux et d’analyse des données intégré.

## <a name="log-sources-that-you-might-want-toocollect"></a>Vous voudrez probablement toocollect des sources de journal
* **Journaux du service Fabric**: émis à partir de la plateforme hello via [LTTng](http://lttng.org) et téléchargé le compte de stockage tooyour. Les journaux peuvent être des événements opérationnels ou émet des événements du runtime que hello plateforme. Ces journaux sont stockés dans un emplacement de hello spécifie ce manifeste du cluster hello. (tooget les détails du compte de stockage d’hello, recherchez la balise de hello **AzureTableWinFabETWQueryable** et recherchez **StoreConnectionString**.)
* **Événements d’application** : émis par le code de votre service. Vous pouvez utiliser une solution de journalisation qui écrit des fichiers journaux textuels, par exemple LTTng. Pour plus d’informations, consultez la documentation de LTTng hello le suivi de votre application.  

## <a name="deploy-hello-diagnostics-extension"></a>Déployer l’extension de Diagnostics hello
Hello première étape de collecte de journaux est l’extension de Diagnostics toodeploy hello sur chacune des machines virtuelles de hello dans le cluster Service Fabric de hello. Hello, extension de diagnostic collecte des journaux sur chaque machine virtuelle et les charge compte de stockage toohello que vous spécifiez. étapes de Hello varient selon que vous utilisez hello portail Azure ou Azure Resource Manager.

toodeploy hello Diagnostics extension toohello machines virtuelles dans le cluster hello dans le cadre de la création du cluster, définissez **Diagnostics** trop**sur**. Après avoir créé le cluster de hello, vous ne pouvez pas modifier ce paramètre à l’aide du portail de hello.

Ensuite, configurez les fichiers de hello toocollect Linux Azure Diagnostics (SCÉNARISTE) et les placer dans votre compte de stockage. Ce processus est expliqué en tant que scénario 3 (« charger vos propres fichiers journaux ») dans l’article de hello [à l’aide de SCÉNARISTE toomonitor et diagnostiquer les machines virtuelles Linux](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json). Après cette Obtient de processus que vous l’accès toohello effectue le suivi. Vous pouvez télécharger le visualiseur de tooa hello traces de votre choix.

Vous pouvez également déployer l’extension de Diagnostics hello à l’aide du Gestionnaire de ressources Azure. Hello processus est similaire pour Windows et Linux et est documenté pour les clusters Windows dans [comment toocollect se connecte avec Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md).

Vous pouvez également utiliser Operations Management Suite, comme indiqué dans [Operations Management Suite Log Analytics with Linux (Analyse des journaux Operations Management Suite avec Linux)](https://blogs.technet.microsoft.com/hybridcloud/2016/01/28/operations-management-suite-log-analytics-with-linux/).

Après avoir terminé cette configuration, analyses de l’agent hello SCÉNARISTE hello des fichiers journaux spécifiés. Chaque fois qu’une nouvelle ligne est ajoutée toohello fichier, il crée une entrée de journal système qui est envoyé toohello de stockage que vous avez spécifié.

## <a name="next-steps"></a>Étapes suivantes
toounderstand plus en détail les événements que vous devez examiner lors de la résolution des problèmes, consultez [LTTng documentation](http://lttng.org/docs) et [à l’aide de SCÉNARISTE](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

