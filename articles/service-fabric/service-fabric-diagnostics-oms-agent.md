---
title: "Azure Service Fabric - Configuration de la surveillance avec l’agent OMS | Microsoft Docs"
description: "Découvrez comment configurer l’agent OMS pour surveiller les conteneurs et les compteurs de performances de vos clusters Azure Service Fabric."
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
ms.date: 10/31/2017
ms.author: dekapur
ms.openlocfilehash: 095db20e7d22bd517337f24fc9a81b84988d1465
ms.sourcegitcommit: 7edfa9fbed0f9e274209cec6456bf4a689a4c1a6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/17/2018
---
# <a name="add-the-oms-agent-to-a-cluster"></a>Ajouter l’agent OMS à un cluster

Cet article explique comment ajouter l’agent OMS à votre cluster comme une extension de groupe de machines virtuelles identiques, puis le connecter à votre espace de travail OMS Log Analytics existant. Cela permet de collecter des données de diagnostic sur les conteneurs, les applications et les performances. Si vous l’ajoutez comme une extension, Azure Resource Manager l’installe sur tous les nœuds, même lors de la mise à l’échelle du cluster.

> [!NOTE]
> Cet article suppose que vous disposez d’un espace de travail OMS Log Analytics déjà configuré. Si ce n’est pas le cas, consultez [Configurer OMS Log Analytics](service-fabric-diagnostics-oms-setup.md).

## <a name="add-the-agent-extension-via-azure-cli"></a>Ajouter l’extension d’agent via Azure CLI

La meilleure façon d’ajouter l’agent OMS à votre cluster est d’utiliser les API des groupes de machines virtuelles identiques de l’interface CLI Azure. Si vous n’avez pas encore configuré Azure CLI, accédez au portail Azure, puis ouvrez une instance de [Cloud Shell](../cloud-shell/overview.md) ou [installez Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).

1. Lorsque votre instance de Cloud Shell est demandée, veillez à vous trouver dans le même abonnement que votre ressource. Utilisez la commande `az account show` pour vérifier que la valeur « name » correspond à celle de l’abonnement de votre cluster.

2. Dans le portail, accédez au groupe de ressources où se trouve votre espace de travail OMS. Cliquez sur la ressource Log Analytics (le type de la ressource sera Log Analytics) dans le volet de navigation droit, faites défiler, puis cliquez sur **Propriétés**.

    ![Page Propriétés OMS](media/service-fabric-diagnostics-oms-agent/oms-properties.png)

    Notez votre `workspaceId`. 

3. Vous aurez également besoin de votre `workspaceKey` pour déployer l’agent. Pour accéder à votre clé, cliquez sur **Paramètres avancés** sous la section *Paramètres* du volet de navigation gauche. Cliquez sur **Serveurs Windows** si vous créez un cluster Windows, ou sur **Serveurs Linux** si vous créez un cluster Linux. Vous aurez besoin de la *clé primaire* qui s’affiche pour déployer vos agents en tant que `workspaceKey`.

4. Exécutez la commande pour installer l’agent OMS sur votre cluster en utilisant l’API `vmss extension set` de votre instance Cloud Shell :

    Pour un cluster Windows :
    
    ```sh
    az vmss extension set --name MicrosoftMonitoringAgent --publisher Microsoft.EnterpriseCloud.Monitoring --resource-group <nameOfResourceGroup> --vmss-name <nameOfNodeType> --settings "{'workspaceId':'<OMSworkspaceId>'}" --protected-settings "{'workspaceKey':'<OMSworkspaceKey>'}"
    ```

    Pour un cluster Linux :

    ```sh
    az vmss extension set --name OmsAgentForLinux --publisher Microsoft.EnterpriseCloud.Monitoring --resource-group <nameOfResourceGroup> --vmss-name <nameOfNodeType> --settings "{'workspaceId':'<OMSworkspaceId>'}" --protected-settings "{'workspaceKey':'<OMSworkspaceKey>'}"
    ```

    Voici un exemple montrant l’ajout de l’agent OMS à un cluster Windows.

    ![Commande CLI - Agent OMS](media/service-fabric-diagnostics-oms-agent/cli-command.png)
 
    Normalement, l’ajout de l’agent aux nœuds prend moins de 15 minutes. Vous pouvez vérifier que les agents ont bien été ajoutés à l’aide de l’API `az vmss extension list` :

    ```sh
    az vmss extension list --resource-group <nameOfResourceGroup> --vmss-name <nameOfNodeType>
    ```

## <a name="add-the-agent-via-the-resource-manager-template"></a>Ajouter l’agent en utilisant un modèle Resource Manager

Des exemples de modèles Resource Manager qui déploient un espace de travail OMS Log Analytics et ajoutent un agent à chacun de vos nœuds sont disponibles pour [Windows](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/SF%20OMS%20Samples/Windows) et pour [Linux](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/SF%20OMS%20Samples/Linux).

Vous pouvez télécharger et modifier ces modèles pour déployer un cluster qui correspond mieux à vos besoins.

## <a name="next-steps"></a>Étapes suivantes

* Collectez les [compteurs de performances](service-fabric-diagnostics-event-generation-perf.md) dont vous avez besoin. Pour configurer l’agent OMS de manière à collecter certains compteurs de performances,accédez au portail OMS (le lien se trouve en haut de la ressource OMS Log Analytics). Ensuite, cliquez sur **Accueil > Paramètres > Données > Compteurs de performances Windows** ou **Compteurs de performances Linux**, puis choisissez les compteurs que vous voulez collecter.
* Configurez OMS pour configurer l’[alerte automatisée](../log-analytics/log-analytics-alerts.md) afin de faciliter la détection et les diagnostics
