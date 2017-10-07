---
title: "mise à niveau des applications de l’ensemble fibre optique aaaService | Documents Microsoft"
description: "Cet article fournit une présentation tooupgrading une application de Service Fabric, notamment les modes de mise à niveau en choisissant l’option et effectuer des vérifications d’intégrité."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 803c9c63-373a-4d6a-8ef2-ea97e16e88dd
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 6f649ef4a5c0afab682522bcba7d2d66a4268ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade"></a>Mise à niveau des applications Service Fabric
Une application Azure Service Fabric est une collection de services. Pendant une mise à niveau, Service Fabric compare hello nouvelle [manifeste d’application](service-fabric-application-model.md#describe-an-application) avec la version précédente de hello et détermine les services dans une application hello nécessitent des mises à jour. Service Fabric compare version hello chiffres dans le service hello manifestes avec les numéros de version hello dans la version précédente de hello. Si un service n'a pas changé, ce service n'est pas mis à niveau.

## <a name="rolling-upgrades-overview"></a>Vue d'ensemble des mises à niveau propagées
Dans une mise à niveau propagée d’application, la mise à niveau hello est effectuée en étapes. À chaque étape, mise à niveau hello est sous-ensemble tooa appliqué de nœuds de cluster hello, appelé un domaine de mise à jour. Par conséquent, application hello reste disponible pour l’ensemble de la mise à niveau hello. Au cours de la mise à niveau de hello, cluster de hello peut contenir une combinaison de versions anciennes et nouvelles de hello.

Pour cette raison, les versions de hello deux doivent être vers l’avant et vers l’arrière compatible. Si elles ne sont pas compatibles, administrateur de l’application hello est responsable de la disponibilité d’une toomaintain de mise à niveau de plusieurs phases de mise en lots. Dans une mise à niveau plusieurs phases, première étape de hello est mise à niveau tooan la version intermédiaire de l’application hello qui est compatible avec la version précédente de hello. deuxième étape de Hello est version finale tooupgrade hello qui interrompt la compatibilité avec une version mise à jour préalable hello, mais est compatible avec la version intermédiaire de hello.

Les domaines de mise à jour sont spécifiés dans le manifeste du cluster hello lorsque vous configurez hello cluster. Les domaines de mise à jour ne reçoivent pas les mises à jour dans un ordre particulier. Un domaine de mise à jour est une unité logique de déploiement pour une application. Les domaines de mise à jour permettent hello services tooremain à haute disponibilité pendant une mise à niveau.

Mises à niveau propagées de non sont possibles si mise à niveau de hello tooall appliqué des nœuds dans le cluster hello, qui est le cas de hello lors de l’application hello n'a qu’un seul domaine de mise à jour. Cette approche n’est pas recommandée étant donné que le service de hello tombe en panne et n’est pas disponible au moment de hello de mise à niveau. En outre, Azure ne fournit aucune garantie quand un cluster est configuré avec un seul domaine de mise à jour.

## <a name="health-checks-during-upgrades"></a>Vérifications d'intégrité pendant les mises à niveau
Pour une mise à niveau, les stratégies de contrôle d’intégrité sont toobe définies (ou les valeurs par défaut peuvent être utilisées). Une mise à niveau est appelé réussie lorsque tous les domaines de mise à jour sont mis à niveau au sein de hello spécifié des délais d’expiration, et lors de la mise à jour des domaines sont considérées comme sains.  Un domaine de mise à jour intègre signifie que ce domaine de mise à jour hello passé toutes les vérifications d’intégrité hello spécifiées dans la stratégie de contrôle d’intégrité hello. Par exemple, une stratégie d'intégrité peut imposer que tous les services dans une instance d'application doivent être *intègres*, car l'intégrité est définie par Service Fabric.

Pendant une mise à jour effectuée par Service Fabric, les stratégies et vérifications d'intégrité sont indépendantes du service et de l'application. Autrement dit, aucun test spécifique au service n'est exécuté.  Par exemple, votre service peut avoir besoin de débit, mais le Service Fabric n’a pas de débit de toocheck informations hello. Consultez toohello [articles de contrôle d’intégrité](service-fabric-health-introduction.md) pour les contrôles de hello sont effectuées. les vérifications Hello qui se produisent pendant une mise à niveau d’inclure de tests pour indique si le package d’application hello a été copié correctement, si le démarrage de l’instance hello et ainsi de suite.

intégrité des applications Hello est un regroupement d’entités enfants de hello de l’application hello. En bref, l’infrastructure de Service prend la valeur intégrité hello application hello par le biais d’intégrité hello signalé sur l’application hello. Il évalue également la santé de tous les services hello application hello hello de cette manière. Service Fabric davantage évalue l’intégrité hello de services d’application hello agrégation d’intégrité de hello leurs enfants, tels que des réplicas de service hello. Une fois que la stratégie de contrôle d’intégrité d’application hello est satisfaite, la mise à niveau hello peut continuer. Si la stratégie de contrôle d’intégrité hello est violée, mise à niveau des applications hello échoue.

## <a name="upgrade-modes"></a>Modes de mise à niveau
Hello mode que nous recommandons pour la mise à niveau de l’application est hello analysé, qui est le mode hello couramment utilisée. Analysés en mode effectue la mise à niveau hello sur le domaine de mise à jour et si toutes les vérifications passe (par hello stratégie spécifiée), déplace automatiquement sur le domaine de mise à jour suivant toohello.  Si l’échouent des vérifications d’intégrité et/ou des délais d’expiration sont atteints, mise à niveau hello est soit restaurée pour le domaine de mise à jour hello ou mode de hello est modifié toounmonitored manuel. Vous pouvez configurer toochoose de mise à niveau hello un de ces deux modes pour les mises à niveau a échoué. 

Le mode manuel non contrôlé doit une intervention manuelle après chaque mise à niveau sur un domaine de mise à jour, le tookick désactiver la mise à niveau de hello sur hello domaine de mise à jour suivant. Aucune vérification de l'intégrité de Service Fabric n'est effectuée. l’administrateur Hello effectue hello des vérifications d’intégrité ou d’état avant de commencer la mise à niveau hello dans le domaine de mise à jour suivant hello.

## <a name="upgrade-default-services"></a>Mettre à niveau les services par défaut
Par défaut des services au sein de l’application de Service Fabric peuvent être mis à niveau pendant le processus de mise à niveau hello d’une application. Services par défaut sont définis dans hello [manifeste d’application](service-fabric-application-model.md#describe-an-application). Hello des règles standard de mise à niveau des services par défaut sont :

1. Par défaut des services Bonjour nouvelle [manifeste d’application](service-fabric-application-model.md#describe-an-application) qui n’existent pas dans le cluster de hello sont créés.
> [!TIP]
> [EnableDefaultServicesUpgrade](service-fabric-cluster-fabric-settings.md#fabric-settings-that-you-can-customize) besoins toobe définir hello de tooenable tootrue suivant les règles. Cette fonctionnalité est prise en charge à partir de la version 5.5.

2. Les services par défaut présents à la fois dans le [manifeste de l’application](service-fabric-application-model.md#describe-an-application) précédent et dans la nouvelle version sont mis à jour. Descriptions de service dans la nouvelle version de hello remplacerait ceux déjà présents dans le cluster de hello. La mise à niveau de l’application serait restaurée automatiquement en cas d’échec de mise à jour des services par défaut.
3. Par défaut des services Bonjour précédente [manifeste d’application](service-fabric-application-model.md#describe-an-application) mais pas dans la nouvelle version de hello sont supprimés. **Notez qu’il n’est pas possible de rétablir les services par défaut supprimés.**

En cas d’une application mise à niveau est annulée, services par défaut sont rétablies toohello état avant le début de la mise à niveau. Mais les services supprimés ne peuvent plus être créés.

## <a name="application-upgrade-flowchart"></a>Organigramme de la mise à niveau d'application
Organigramme de Hello ci-dessous peut vous aider à comprendre le processus de mise à niveau hello d’une application de Service Fabric. En particulier, les flux hello décrit comment hello délais d’attente, y compris *HealthCheckStableDuration*, *HealthCheckRetryTimeout*, et *UpgradeHealthCheckInterval*, permettent de contrôler lors de la mise à niveau hello dans le domaine de mise à jour est considérée comme une réussite ou échec.

![processus de mise à niveau Hello pour une Application Service Fabric][image]

## <a name="next-steps"></a>Étapes suivantes
[mise à niveau de votre application à l’aide de Visual Studio](service-fabric-application-upgrade-tutorial.md) vous guide à travers une mise à niveau de l’application à l’aide de Visual Studio.

[mise à niveau de votre application à l’aide de PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) vous guide à travers une mise à niveau de l’application à l’aide de PowerShell.

Contrôlez les mises à niveau de votre application à l'aide des [Paramètres de mise à niveau](service-fabric-application-upgrade-parameters.md).

Rendre les mises à niveau de votre application compatible par learning comment toouse [sérialisation des données](service-fabric-application-upgrade-data-serialization.md).

Découvrez comment toouse des fonctionnalités avancées lors de la mise à niveau de votre application en vous reportant trop[rubriques avancées](service-fabric-application-upgrade-advanced.md).

Résoudre les problèmes courants dans les mises à niveau de l’application en faisant référence à des étapes de toohello de [résolution des problèmes de mises à niveau Application](service-fabric-application-upgrade-troubleshooting.md).

[image]: media/service-fabric-application-upgrade/service-fabric-application-upgrade-flowchart.png
