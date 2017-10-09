---
title: "aaaOverview de mise à l’échelle dans les applications Web, Services de cloud computing et des Machines virtuelles Microsoft Azure | Documents Microsoft"
description: "Vue d’ensemble de la mise à l’échelle automatique dans Microsoft Azure. S’applique tooVirtual Machines, Cloud Services et applications Web."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 74bf03be-e658-4239-a214-c12424b53e4c
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2016
ms.author: robb
ms.openlocfilehash: ef68b722ea22c4149a7d7a89c5855ba761db9247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-autoscale-in-microsoft-azure-virtual-machines-cloud-services-and-web-apps"></a>Vue d’ensemble de la mise à l’échelle automatique sur les machines virtuelles Microsoft Azure, les services cloud et les applications web
Cet article décrit la mise à l’échelle le Microsoft Azure, ses avantages, et comment tooget démarré à l’utiliser.  

Mise à l’échelle du moniteur Azure s’applique uniquement trop[machines virtuelles identiques](https://azure.microsoft.com/services/virtual-machine-scale-sets/), [Services de cloud computing](https://azure.microsoft.com/services/cloud-services/), et [du Service d’applications - applications Web](https://azure.microsoft.com/services/app-service/web/).

> [!NOTE]
> Azure dispose de deux méthodes de mise à l’échelle automatique. Une ancienne version de mise à l’échelle s’applique tooVirtual Machines (haute disponibilité). Cette fonctionnalité prend en charge limitée et nous vous recommandons d’échelle de machines toovirtual migration définit pour la prise en charge de la mise à l’échelle plus rapide et plus fiable. Un lien sur la technologie plus ancienne de toouse hello est incluse dans cet article.  
>
>

## <a name="what-is-autoscale"></a>Qu’est-ce que la mise à l’échelle automatique ?
Mise à l’échelle vous permet de toohave hello bonne quantité de ressources toohandle hello charge en cours d’exécution sur votre application. Il vous permet de ressources tooadd toohandle les augmentations de chargent et également réaliser des économies en supprimant des ressources qui sont période d’inactivité. Vous spécifiez un nombre minimal et maximal d’instances toorun et ajoutez ou supprimez des machines virtuelles automatiquement selon un ensemble de règles. Avoir un nombre minimal d’instances permet de vous assurer que votre application est toujours en cours d’exécution même en l’absence de charge. Avoir un nombre maximal d’instances limite votre coût total possible par heure. Vous effectuez une mise à l’échelle automatique entre ces deux extrêmes, à l’aide de règles que vous créez.

 ![Description de la mise à l’échelle automatique. Ajouter et supprimer des machines virtuelles](./media/monitoring-overview-autoscale/AutoscaleConcept.png)

Lorsque les conditions relatives aux règles sont remplies, une ou plusieurs actions de mise à l’échelle automatique sont déclenchées. Vous pouvez ajouter et supprimer des machines virtuelles ou effectuer d’autres actions. Hello diagramme conceptuel suivant illustre ce processus.  

 ![Diagramme de flux de la mise à l’échelle automatique](./media/monitoring-overview-autoscale/Autoscale_Overview_v4.png)

Hello explication ci-dessous s’applique toohello des éléments de diagramme précédent de hello.   

## <a name="resource-metrics"></a>Métriques de ressources
Les ressources émettent des métriques, qui sont ensuite traitées par des règles. Les mesures sont fournies via différentes méthodes.
Machines virtuelles identiques utilisent des données de télémétrie d’agents de diagnostics Azure tandis que les données de télémétrie pour les applications Web et les services de cloud computing proviennent directement d’hello Infrastructure Azure. Parmi les statistiques couramment utilisées figurent l’utilisation du processeur, l’utilisation de la mémoire, le nombre de threads, la longueur de la file d’attente et l’utilisation du disque. Pour obtenir une liste des données de télémétrie que vous pouvez utiliser, voir [Mesures courantes pour la mise à l’échelle automatique](insights-autoscale-common-metrics.md).

## <a name="custom-metrics"></a>Métriques personnalisées
Vous pouvez également utiliser vos propres métriques personnalisées que peuvent émettre vos applications. Si vous avez configuré votre ordinateur ou les applications toosend métriques tooApplication Insights, vous pouvez tirer parti de ces décisions toomake de métriques s’il faut tooscale ou non. 

## <a name="time"></a>Temps
Les règles basées sur la planification s’appuient sur l’heure UTC. Vous devez définir votre fuseau horaire correctement lorsque vous configurez vos règles.  

## <a name="rules"></a>Règles
diagramme de Hello ne montre qu’une seule règle de mise à l’échelle, mais vous pouvez avoir beaucoup d'entre eux. Vous pouvez créer des règles complexes qui se chevauchent en fonction de vos besoins.  Les types de règles incluent  

* **Basées sur des mesures** : par exemple, effectuer cette action lorsque l’utilisation du processeur est supérieure à 50 %.
* **Basées sur l’heure** : par exemple, déclencher un webhook chaque samedi à 8h dans un fuseau horaire donné.

Les règles basées sur les mesures mesurent la charge de l’application et ajoutent ou suppriment des machines virtuelles en fonction de cette charge. Règles basées sur une planification permettent de tooscale lorsque vous consultez des modèles d’heure dans votre charge et que vous souhaitez tooscale avant une augmentation de la charge possible ou diminution se produit.  

## <a name="actions-and-automation"></a>Actions et automatisation
Les règles peuvent déclencher un ou plusieurs types d’actions.

* **Mise à l’échelle** : mettre les machines virtuelles à l’échelle
* **Messagerie** -envoyer par courrier électronique toosubscription administrateurs, coadministrateurs et/ou adresse électronique supplémentaire que vous spécifiez.
* **Automatisation via webhooks** : appeler des webhooks, qui peuvent déclencher plusieurs actions complexes à l’intérieur ou en dehors d’Azure. Dans Azure, vous pouvez démarrer un runbook Azure Automation, une fonction Azure ou une application logique Azure. Parmi les URL tierces en dehors d’Azure figurent des services comme Slack et Twilio.

## <a name="autoscale-settings"></a>Paramètres de mise à l’échelle automatique
Mise à l’échelle, utilisez hello suit la terminologie et la structure.

- Un **paramètre de mise à l’échelle** est lu par hello échelle moteur toodetermine si tooscale vers le haut ou vers le bas. Il contient une ou plusieurs profils, plus d’informations sur la ressource cible de hello et les paramètres de notification.

    - Un **profil de mise à l’échelle automatique** est la combinaison des éléments suivants :

        - **paramètre de capacité**, ce qui indique au minimum, maximum de hello et valeurs par défaut pour le nombre d’instances.
        - Un **ensemble de règles**, comprenant chacun un déclencheur (heure ou métrique) et une action de mise à l’échelle (augmentation ou réduction).
        - Une **périodicité** indiquant le moment auquel une mise à l’échelle automatique doit appliquer ce profil.

        Vous pouvez avoir plusieurs profils, qui vous permettront de tootake administration des exigences différentes qui se chevauchent. Vous pouvez avoir des profils de mise à l’échelle différents pour différents moments de l’ou les jours de semaine de hello, par exemple.

    - A **paramètre de notification** définit quelles notifications doivent se produire lorsqu’un événement de mise à l’échelle se produit en fonction de répondant à des critères de l’un des profils du paramètre de mise à l’échelle hello hello. Mise à l’échelle peut notifier un ou plusieurs adresses de messagerie ou que les appels tooone ou plusieurs webhooks.


![Structure de règle, de profil et de paramètre de mise à l’échelle automatique Azure](./media/monitoring-overview-autoscale/AzureResourceManagerRuleStructure3.png)

Hello la liste complète des champs configurables et les descriptions n’est disponible dans hello [API REST de mise à l’échelle](https://msdn.microsoft.com/library/dn931928.aspx).

Pour plus d’exemples de code, consultez

* [Configuration avancée de la mise à l’échelle automatique à l’aide des modèles Resource Manager pour les groupes de machines virtuelles identiques](insights-advanced-autoscale-virtual-machine-scale-sets.md)  
* [Paramètres de mise à l’échelle automatique](https://msdn.microsoft.com/library/dn931953.aspx)

## <a name="horizontal-vs-vertical-scaling"></a>Mise à l’échelle horizontale/verticale
Mise à l’échelle uniquement mettre à l’échelle horizontalement, qui est une augmentation (« out ») ou diminuer (« in ») dans nombre de hello d’instances de machine virtuelle.  Horizontal est plus souple dans une situation de cloud, car elle vous permet de toorun potentiellement des milliers de machines virtuelles toohandle charge.

La mise à l’échelle verticale est différente. Il conserve hello même nombre d’ordinateurs virtuels, mais rend hello des machines virtuelles plus (« up ») ou moins (« bas ») puissant. La puissance se mesure en termes de mémoire, de vitesse du processeur, d’espace disque, etc.  La mise à l’échelle verticale a davantage de limites. Il est dépendant de la disponibilité de hello de matériel plus puissant, qui rapidement atteint une limite supérieure et peut varier selon la région. Vertical également généralement la mise à l’échelle nécessite une toostop de l’ordinateur virtuel et redémarrez.

Pour plus d’informations, voir [Évolution verticale des machines virtuelles Azure avec Azure Automation](../virtual-machines/linux/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="methods-of-access"></a>Méthodes d’accès
Vous pouvez configurer la mise à l’échelle automatique via

* [Portail Azure](insights-how-to-scale.md)
* [PowerShell](insights-powershell-samples.md#create-and-manage-autoscale-settings)
* [Interface de ligne de commande interplateforme (CLI)](insights-cli-samples.md#autoscale)
* [API REST Azure Monitor](https://msdn.microsoft.com/library/azure/dn931953.aspx)

## <a name="supported-services-for-autoscale"></a>Services pris en charge pour la mise à l’échelle automatique
| de diffusion en continu | Schéma et documentation |
| --- | --- |
| Applications Web |[Mise à l’échelle des applications web](insights-how-to-scale.md) |
| Services cloud |[Mise à l’échelle automatique d’un service cloud](../cloud-services/cloud-services-how-to-scale.md) |
| Machines virtuelles : classique |[Mise à l’échelle de groupes à haute disponibilité de machines virtuelles classiques](https://blogs.msdn.microsoft.com/kaevans/2015/02/20/autoscaling-azurevirtual-machines/) |
| Machines virtuelles : jeux de mise à l’échelle Windows |[Mise à l’échelle des jeux de mise à l’échelle de machine virtuelle dans Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) |
| Machines virtuelles : jeux de mise à l’échelle Linux |[Mise à l’échelle des jeux de mise à l’échelle de machine virtuelle dans Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) |
| Machines virtuelles : exemple Windows |[Configuration avancée de la mise à l’échelle automatique à l’aide des modèles Resource Manager pour les groupes de machines virtuelles identiques](insights-advanced-autoscale-virtual-machine-scale-sets.md) |

## <a name="next-steps"></a>Étapes suivantes
toolearn en savoir plus sur la mise à l’échelle, utilisez hello Autoscale Walkthroughs répertoriées précédemment ou reportez-vous toohello suivant des ressources :

* [Mesures courantes pour la mise à l’échelle automatique dans Azure Monitor](insights-autoscale-common-metrics.md)
* [Meilleures pratiques pour la mise à l’échelle automatique d’Azure Insights](insights-autoscale-best-practices.md)
* [Utilisez la mise à l’échelle actions toosend par courrier électronique et webhook des notifications d’alerte](insights-autoscale-to-webhook-email.md)
* [Paramètres de mise à l’échelle automatique](https://msdn.microsoft.com/library/dn931953.aspx)
* [Dépannage de la mise à l’échelle automatique avec des jeux de mise à l’échelle de machine virtuelle](../virtual-machine-scale-sets/virtual-machine-scale-sets-troubleshoot.md)
