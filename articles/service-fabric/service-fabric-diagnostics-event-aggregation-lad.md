---
title: "Agrégation d’événements Azure Service Fabric avec Linux Azure Diagnostics | Microsoft Docs"
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
ms.openlocfilehash: bcc3a229369a065cfcfbd32eadbf3f6ae6fe0036
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="event-aggregation-and-collection-using-linux-azure-diagnostics"></a>Agrégation et collection d’événements à l’aide de Linux Azure Diagnostics
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-event-aggregation-wad.md)
> * [Linux](service-fabric-diagnostics-event-aggregation-lad.md)
>
>

Lorsque vous exécutez un cluster Service Fabric dans Azure, il peut être intéressant de collecter les journaux de tous les nœuds pour les regrouper dans un emplacement central. La centralisation des journaux vous permet d’analyser et résoudre les problèmes que vous pourriez rencontrer dans votre cluster ou dans les applications et services exécutés dans ce cluster.

L’une des façons de charger et de collecter des journaux consiste à utiliser l’extension Linux Azure Diagnostics (LAD), qui assure le chargement des journaux dans le Stockage Azure, et qui a également la possibilité d’envoyer des journaux à Azure Application Insights ou Event Hubs. Vous pouvez également utiliser un processus externe pour lire les événements à partir du stockage et les placer dans un produit de plateforme d’analyse tel que [OMS Log Analytics](../log-analytics/log-analytics-service-fabric.md) ou une autre solution d’analyse de journaux.

## <a name="log-and-event-sources"></a>Sources de journaux et d’événements

### <a name="service-fabric-platform-events"></a>Événements de la plateforme Service Fabric
Service Fabric émet quelques journaux prêts à l’emploi via [LTTng](http://lttng.org), notamment les événements opérationnels ou des événements du runtime. Ces journaux sont stockés dans l’emplacement spécifié par le modèle Resource Manager du cluster. Pour obtenir ou définir les informations relatives au compte de stockage, recherchez l’étiquette **AzureTableWinFabETWQueryable**, puis recherchez **StoreConnectionString**.

### <a name="application-events"></a>Événements liés aux applications
 Les événements émis à partir du code de vos applications et services tel que spécifié par vous-même lors de l’instrumentation de votre logiciel. Vous pouvez utiliser une solution de journalisation qui écrit des fichiers journaux textuels, par exemple LTTng. Pour plus d’informations, consultez la documentation de LTTng sur le traçage de votre application.

[Surveillance et diagnostic des services dans une configuration de développement d’ordinateur local](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).

## <a name="deploy-the-diagnostics-extension"></a>Déployer l’extension Diagnostics
La première étape de la collecte de journaux consiste à déployer l’extension Diagnostics sur chaque machine virtuelle du cluster Service Fabric. Cette extension collecte les journaux sur chaque machine virtuelle et les charge dans le compte de stockage que vous spécifiez. Les étapes varient selon que vous utilisez le portail Azure ou Azure Resource Manager.

Pour déployer l’extension Diagnostics sur les machines virtuelles du cluster lors de la création de ce dernier, définissez **Diagnostics** sur **Activé**. Une fois le cluster créé, vous ne pouvez plus modifier ce paramètre à l’aide du portail.

Ensuite, configurez Linux Azure Diagnostics (LAD) pour collecter les fichiers et les placer dans votre compte de stockage. Ce processus est détaillé dans le scénario 3 (Charger vos propres fichiers journaux) de l’article [Utilisation de l’extension de diagnostic Linux pour analyser les données de performances et de diagnostic d’une machine virtuelle Linux](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json). Cette procédure vous fournit un accès aux suivis. Vous pouvez charger les suivis dans le visualiseur de votre choix.

Vous pouvez également déployer l’extension Diagnostics à l’aide d’Azure Resource Manager. Le processus, identique pour Windows et Linux, est documenté pour les clusters Windows, dans la section [Collecte des journaux avec Linux Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md).

Vous pouvez également utiliser Operations Management Suite, comme indiqué dans [Operations Management Suite Log Analytics with Linux (Analyse des journaux Operations Management Suite avec Linux)](https://blogs.technet.microsoft.com/hybridcloud/2016/01/28/operations-management-suite-log-analytics-with-linux/).

Une fois cette configuration effectuée, l’agent LAD analyse les fichiers journaux spécifiés. Dès qu’une nouvelle ligne est ajoutée au fichier, elle crée une entrée dans le journal syslog, qui est envoyée au stockage que vous avez spécifié.

## <a name="next-steps"></a>Étapes suivantes

Pour identifier plus précisément les événements à consulter lors de la résolution des problèmes, consultez la [documentation de LTTng](http://lttng.org/docs) et la section [Utilisation de l’extension de diagnostic Linux pour analyser les données de performances et de diagnostic d’une machine virtuelle Linux](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).