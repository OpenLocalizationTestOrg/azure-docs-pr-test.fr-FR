---
title: aaaTraffic Types de gestionnaires de point de terminaison | Documents Microsoft
description: "Cet article explique les différents types de points de terminaison pouvant être utilisés avec Azure Traffic Manager."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 4e506986-f78d-41d1-becf-56c8516e4d21
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/29/2017
ms.author: kumud
ms.openlocfilehash: 787412ac6207f76791bf3ff753d1df2767b1a964
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="traffic-manager-endpoints"></a>Points de terminaison Traffic Manager
Microsoft Azure Traffic Manager vous permet de toocontrol comment le trafic réseau est distribué tooapplication les déploiements en cours d’exécution dans différents centres de données. Vous pouvez configurer chaque déploiement d’application en tant que « point de terminaison » dans Traffic Manager. Lorsque Traffic Manager reçoit une requête DNS, il choisit un tooreturn de point de terminaison disponible dans hello réponse DNS. Gestionnaire de trafic base choix de hello sur l’état de point de terminaison actuel hello et méthode de routage du trafic hello. Pour plus d’informations, consultez l’article [Fonctionnement de Traffic Manager](traffic-manager-how-traffic-manager-works.md).

Traffic Manager prend en charge trois types de points de terminaison :
* **points de terminaison Azure** sont utilisés pour les services hébergés dans Azure.
* **points de terminaison externes** sont utilisés pour les services hébergés en dehors d’Azure, c’est-à-dire les services hébergés en local ou par un autre hébergeur.
* **Imbriqué des points de terminaison** est toocreate de profils Traffic Manager toocombine utilisé plus souple le routage du trafic schémas toosupport hello les besoins des déploiements plus volumineux et plus complexes.

Différents types de points de terminaison peuvent être combinés dans un même profil Traffic Manager sans la moindre restriction. Chaque profil peut contenir n’importe quelle combinaison de types de points de terminaison.

Hello les sections suivantes décrire chaque type de point de terminaison plus en détail.

## <a name="azure-endpoints"></a>points de terminaison Azure

Les points de terminaison Azure sont utilisés pour les services Azure dans Traffic Manager. Hello, les types de ressources Azure suivants est pris en charge :

* Machines virtuelles IaaS « classiques » et services cloud PaaS
* Web Apps
* Ressources d’adresse IP publique (qui ne pourra tooVMs connectés directement ou via un équilibrage de charge Azure). adresse IP publique Hello doit avoir un nom DNS assigné toobe utilisé dans un profil Traffic Manager.

Les ressources PublicIPAddress sont des ressources Azure Resource Manager. Ils n’existent pas dans le modèle de déploiement classique hello. Elles sont donc uniquement prises en charge dans les expériences Azure Resource Manager de Traffic Manager. Hello autres types de point de terminaison sont pris en charge via le modèle de déploiement classique de gestionnaire de ressources et hello.

Lorsque vous utilisez des points de terminaison Azure, Traffic Manager détecte l’arrêt ou le démarrage d’une machine virtuelle IaaS « classique », d’un service cloud ou d’une application web. Cet état est répercutée dans l’état du point de terminaison hello. Pour plus d’informations, consultez [Surveillance des points de terminaison Traffic Manager](traffic-manager-monitoring.md#endpoint-and-profile-status). Lorsque hello service sous-jacent est arrêté, Traffic Manager n’effectue pas les vérifications d’intégrité de point de terminaison ou de point de terminaison de diriger le trafic toohello. Aucun gestionnaire de trafic facturation se produisent pour hello a arrêté l’instance. Lorsque le service de hello est redémarré, curriculum vitae de facturation et de point de terminaison hello correspond au trafic tooreceive éligibles. Cette détection ne s’applique pas tooPublicIpAddress de points de terminaison.

## <a name="external-endpoints"></a>points de terminaison externes

Les points de terminaison externes sont utilisés pour les services hébergés en dehors d’Azure. Par exemple, un service hébergé en local ou avec un autre fournisseur. Points de terminaison externes peuvent être utilisés individuellement ou combinées avec des points de terminaison Azure Bonjour même profil Traffic Manager. La combinaison de points de terminaison Azure avec des points de terminaison externes permet la prise en charge de divers scénarios :

* Dans un modèle de basculement actif / actif ou actif / passif, utilisez Azure tooprovide augmenté redondance pour une application locale existante.
* latence de l’application pour les utilisateurs monde hello tooreduce étendre un existant sur site application tooadditional emplacements géographiques dans Azure. Pour plus d’informations, consultez [Routage du trafic Traffic Manager basé sur les performances](traffic-manager-routing-methods.md#performance).
* Utilisez Azure tooprovide une capacité supplémentaire pour une application locale existante, en continu ou en tant qu’un toomeet de solution de 'croissance dans le cloud' un pic d’activité dans la demande.

Dans certains cas, il est utile de toouse tooreference de points de terminaison externes Azure services (pour obtenir des exemples, consultez hello [FAQ](traffic-manager-faqs.md#traffic-manager-endpoints)). Dans ce cas, les contrôles d’intégrité sont facturées au taux de points de terminaison Azure hello, pas les taux de points de terminaison externes hello. Toutefois, contrairement aux points de terminaison Azure, si vous arrêtez ou supprimez hello, le service sous-jacent le contrôle d’intégrité facturation continue jusqu'à ce que vous désactivez ou supprimez le point de terminaison hello dans Traffic Manager.

## <a name="nested-endpoints"></a>points de terminaison imbriqués

Les points de terminaison imbriquées combinent plusieurs Traffic Manager profils toocreate flexible le routage du trafic schémas et prennent en charge les besoins de hello des déploiements plus volumineux et complexes. Avec les points de terminaison imbriquées, ajout d’un profil 'child' tant que profil 'parent' tooa de point de terminaison. Les deux profils de hello enfant et parent peuvent contenir d’autres points de terminaison de tout type, y compris des autres profils imbriqués. Pour plus d’informations, consultez [Profils Traffic Manager imbriqués](traffic-manager-nested-profiles.md).

## <a name="web-apps-as-endpoints"></a>Utilisation d’applications web en tant que points de terminaison

D’autres aspects doivent être pris en compte lors de la configuration d’applications web en tant que points de terminaison dans Traffic Manager :

1. Seules les applications Web à hello référence (SKU) « Standard » ou version ultérieure sont éligibles pour une utilisation avec le Gestionnaire de trafic. Tente de tooadd une application Web d’un échec SKU inférieure. Rétrogradation hello référence (SKU) d’une application Web existante entraîne dans Traffic Manager n’est plus envoyer le trafic toothat application Web.
2. Lorsqu’un point de terminaison reçoit une requête HTTP, elle utilise hello 'host' en-tête hello demande toodetermine quelle application Web doit demander des hello du service. en-tête d’hôte Hello contient hello DNS nom utilisé tooinitiate hello demande, par exemple « contosoapp.azurewebsites.net ». toouse un autre nom DNS dans votre application Web et nom DNS hello doit être inscrit en tant que nom de domaine personnalisé pour hello application. Lorsque vous ajoutez un point de terminaison d’application Web en tant qu’un point de terminaison Azure, nom DNS du profil Traffic Manager hello est automatiquement inscrit pour hello application. Cet enregistrement est automatiquement supprimé lorsque le point de terminaison hello est supprimé.
3. Chaque profil Traffic Manager peut contenir au maximum un point de terminaison d’application web provenant de chaque région Azure. toowork autour de cette contrainte, vous pouvez configurer une application Web en tant qu’un point de terminaison externe. Pour plus d’informations, consultez hello [FAQ](traffic-manager-faqs.md#traffic-manager-endpoints).

## <a name="enabling-and-disabling-endpoints"></a>Activation et désactivation des points de terminaison

La désactivation d’un point de terminaison dans Traffic Manager peut être utile de tootemporarily le trafic de supprimer à partir d’un point de terminaison est en mode de maintenance ou en cours de redéploiement. Une fois que le point de terminaison hello s’exécute à nouveau, il peut être réactivée.

Points de terminaison peuvent être activés et désactivés via le portail de Traffic Manager hello, PowerShell, CLI ou une API REST, qui sont pris en charge dans le Gestionnaire de ressources et le modèle de déploiement classique hello.

> [!NOTE]
> La désactivation d’un point de terminaison Azure n’a rien toodo état de son déploiement dans Azure. Azure service (comme une machine virtuelle ou une application Web est en cours d’exécution et en mesure de trafic tooreceive même lorsque désactivé dans Traffic Manager. Le trafic peut être adressé directement toohello instance de service plutôt que via hello Traffic Manager du nom DNS de profil. Pour plus d’informations, consultez l’article [Fonctionnement de Traffic Manager](traffic-manager-how-traffic-manager-works.md).

éligibilité actuel de Hello de chaque trafic tooreceive de point de terminaison dépend hello suivant facteurs :

* état du profil Hello (activé/désactivé)
* état du point de terminaison Hello (activé/désactivé)
* résultats Hello des contrôles d’intégrité de hello pour ce point de terminaison

Pour plus d’informations, consultez la rubrique relative à la [surveillance des points de terminaison avec Traffic Manager](traffic-manager-monitoring.md#endpoint-and-profile-status).

> [!NOTE]
> Traffic Manager fonctionne au niveau DNS de hello, il est impossible de tooinfluence existant connexions tooany point de terminaison de. Lorsqu’un point de terminaison n’est pas disponible, Traffic Manager dirige les nouvelles connexions tooanother point de terminaison disponible. Hôte hello derrière hello désactivé ou un point de terminaison non intègre peut néanmoins tooreceive du trafic via les connexions existantes jusqu'à ce que les sessions sont arrêtées. Il est convient de limiter les applications hello session durée tooallow trafic toodrain à partir des connexions existantes.

Si tous les points de terminaison dans un profil sont désactivées, ou si le profil hello lui-même est désactivé, Traffic Manager envoie une requête DNS 'NXDOMAIN' réponse tooa nouveau.


## <a name="next-steps"></a>Étapes suivantes

* En savoir plus sur le [fonctionnement de Traffic Manager](traffic-manager-how-traffic-manager-works.md).
* En savoir plus sur le [basculement automatique et la surveillance des points de terminaison](traffic-manager-monitoring.md)de Traffic Manager.
* En savoir plus sur les [méthodes de routage du trafic](traffic-manager-routing-methods.md)avec Traffic Manager.
