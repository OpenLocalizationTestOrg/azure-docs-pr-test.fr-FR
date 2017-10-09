---
title: aaaAzure analyse de Service Fabric conteneurs et aux Diagnostics | Documents Microsoft
description: "Découvrez comment toomonitor et diagnostiquer les conteneurs orchestrés sur Microsoft Azure Service Fabric avec solution de conteneurs d’OMS."
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
ms.date: 05/10/2017
ms.author: dekapur
ms.openlocfilehash: cd79111cf78b9d76a60d489bb9953587aa06186d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-windows-server-containers-with-oms"></a>Surveiller les conteneurs Windows Server avec OMS

## <a name="oms-containers-solution"></a>Solution de conteneurs d’OMS

équipe de Operations Management Suite (OMS) Hello a publié une solution de conteneurs pour les diagnostics et la surveillance des conteneurs. En même temps que la solution de Service Fabric, cette solution est un excellent outil toomonitor conteneur les déploiements orchestrés sur l’infrastructure de Service. Voici un exemple simple de quel tableau de bord hello dans les solutions hello ressemble à :

![Tableau de bord OMS de base](./media/service-fabric-diagnostics-containers-windowsserver/oms-containers-dashboard.png)

Il collecte également les différents types de fichiers journaux qui peuvent être interrogées dans l’outil d’Analytique des journaux OMS hello, et peut être utilisé toovisualize les métriques ou les événements générés. types de journaux Hello collectés sont :

1. ContainerInventory : affiche des informations sur les images, le nom et l’emplacement du conteneur
2. ContainerImageInventory : informations sur les images déployées, ID ou tailles compris
3. ContainerLog : journaux d’erreurs spécifiques, journaux de docker (stdout, etc.) et autres entrées
4. ContainerServiceLog : les commandes de démon docker qui ont été exécutées
5. Performances : les compteurs de performances, y compris le conteneur de processeur, mémoire, le trafic réseau, les e/s disque et des mesures personnalisées à partir de hello hébergent des ordinateurs

Cet article traite des tooset requis de hello étapes d’analyse pour votre cluster de conteneur. toolearn plus d’informations sur les solutions de conteneurs d’OMS, consultez leurs [documentation](../log-analytics/log-analytics-containers.md).

## <a name="1-set-up-a-service-fabric-cluster"></a>1. Configuration d’un cluster Service Fabric

Créer un cluster à l’aide du modèle Azure Resource Manager hello [ici](https://github.com/dkkapur/Service-Fabric/tree/master/ARM%20Templates/SF%20OMS%20Sample). Assurez-vous que tooadd un nom d’espace de travail OMS unique. Ce modèle est également par défaut toodeploying un cluster dans l’aperçu de hello build de l’infrastructure de Service (v255.255), ce qui signifie qu’il ne peut pas être utilisé en production et ne peut pas être mis à niveau tooa une autre version de l’infrastructure de Service. Si vous décidez de ce modèle pour toouse à long terme ou de production à utiliser, de modifier le numéro de version stable hello version tooa.

Une fois que le cluster de hello est configuré, vérifiez que vous avez installé les certificats appropriés hello et vérifiez que vous êtes en mesure de tooconnect toohello cluster.

Vérifiez que votre groupe de ressources est correctement configuré par titre toohello [portail Azure](https://portal.azure.com/) et la recherche de déploiement de hello. groupe de ressources Hello doit contenir toutes les ressources de Service Fabric hello et ont également une solution Analytique de journal ainsi que d’une solution de Service Fabric.

Pour modifier un cluster Service Fabric existant :
* Vérifiez que les tests de diagnostic est activée (dans le cas contraire, l’activer via [mise à jour ensemble d’échelle de machine virtuelle hello](/rest/api/virtualmachinescalesets/create-or-update-a-set))
* Ajouter un espace de travail OMS en créant une solution « Analytique de l’infrastructure de Service » via hello Azure Marketplace
* Modifier les sources de données de hello de hello Service Fabric solution toopick des données à partir de tables Azure Storage appropriées hello (configurés par WAD) Bonjour groupe de ressources qui hello cluster est dans
* Ajouter l’agent hello en tant qu’un [extension toohello machines virtuelles identiques](/powershell/module/azurerm.compute/add-azurermvmssextension) via PowerShell ou l’ensemble d’échelle de machine virtuelle hello (même liaison comme indiqué ci-dessus, modèle de gestionnaire de ressources toomodify hello) de mise à jour

## <a name="2-deploy-a-container"></a>2. Déploiement d’un conteneur

Une fois que le cluster de hello est prêt et que vous avez confirmé que vous pouvez y accéder, déployez un tooit du conteneur. Si vous avez choisi de version d’évaluation toouse hello en tant que jeu par modèle de hello, vous pouvez également Explorer docker de nouveau de Service Fabric composent les fonctionnalités. N’oubliez pas que hello première fois une image de conteneur est déployé tooa cluster, il accepte plusieurs images de hello toodownload minutes en fonction de sa taille.

## <a name="3-add-hello-containers-solution"></a>3. Ajouter la solution de conteneurs hello

Dans l’hello portail Azure, créez une ressource de conteneurs (sous hello analyse + gestion catégorie) via Azure Marketplace. 

![Ajout de la solution Conteneurs](./media/service-fabric-diagnostics-containers-windowsserver/containers-solution.png)

À l’étape de la création de hello, il demande un espace de travail OMS. Sélectionnez hello qui a été créé avec un déploiement hello ci-dessus. Cette étape ajoute une solution de conteneurs au sein de votre espace de travail OMS et est automatiquement détectée par l’agent OMS de hello déployé par le modèle de hello. démarre l’agent de Hello collecte des données sur les processus de conteneurs hello dans un cluster de hello et dans environ 10-15 minutes, vous devez voir des solutions hello allument avec des données comme image hello du tableau de bord hello ci-dessus.

## <a name="4-next-steps"></a>4. Étapes suivantes

OMS propose divers outils dans toomake d’espace de travail hello si elle est plus utile pour vous. Explorer hello suivant options toocustomize hello solution tooyour besoins :
- Obtenir être familiarisé avec hello [recherche et interrogation de journal](../log-analytics/log-analytics-log-searches.md) fonctionnalités proposées dans le cadre de l’Analytique des journaux
- Configurer hello OMS agent toopick des compteurs de performance spécifiques (accédez toohello espace de travail Accueil > Paramètres > données > compteurs de performances Windows)
- Configurer OMS tooset [automatisée d’alerte](../log-analytics/log-analytics-alerts.md) tooaid de règles de détection et de diagnostics
