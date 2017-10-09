---
title: "aaaOverview d’architecture mutualisée précédent se termine par la passerelle d’Application Azure | Documents Microsoft"
description: "Cette page fournit une vue d’ensemble de la prise en charge de la passerelle d’Application hello pour dorsale architecture mutualisée."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: 
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: gwallace
ms.openlocfilehash: b7da8c9c68e34bd83ad2b828fab62c00caea354a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-support-for-multi-tenant-back-ends"></a>Prise en charge des serveurs principaux multilocataires par Application Gateway

Azure Application Gateway prend en charge les groupes de machines virtuelles identiques, les interfaces réseau, les adresses IP publiques/privées ou les noms de domaines complets pour ses pools de serveurs principaux. Par défaut, passerelle d’application ne modifie pas l’en-tête d’hôte HTTP entrant hello à partir du client de hello et envoie hello en-tête toohello non modifiés back-end. Il existe de nombreux services comme [Azure Web Apps](../app-service-web/app-service-web-overview.md) et [gestion des API](../api-management/api-management-key-concepts.md) qui sont plusieurs locataires par nature et s’appuient sur un en-tête d’hôte spécifique ou un SNI extension tooresolve toohello point de terminaison correct. Passerelle d’application prend désormais en charge la possibilité de hello pour les utilisateurs toooverwrite hello entrant en-tête d’hôte HTTP en fonction des paramètres de serveur principal HTTP hello. Cette fonctionnalité permet la prise en charge des applications web Azure de serveurs principaux multilocataires et de la gestion des API. Cette fonctionnalité est disponible pour les hello standard et WAF référence (SKU). Mutualisé back end prise en charge également fonctionne avec SSL arrêt et fin tooend différents scénarios de SSL.

![scénario d’application web](./media/application-gateway-web-app-overview/scenario.png)

toospecify de capacité Hello un remplacement de l’hôte est défini à hello paramètres HTTP et peut être appliqué tooany précédent se terminer pool lors de la création de règle. Architecture mutualisée précédent termine hello prise en charge de deux façons de la substitution d’en-tête d’hôte et l’extension SNI suivantes.

1. Hello capacité tooset hello hôte nom tooa fixe valeur Bonjour paramètres HTTP. Cette fonctionnalité garantit que la substitution de cet en-tête d’hôte hello toothis valeur pour le trafic toohello back-end pool où hello HTTP paramètres sont appliqués. Lorsque vous utilisez fin tooend SSL, ce nom d’hôte substituée est utilisé dans hello extension SNI. Cette fonctionnalité permet des scénarios où une batterie de serveurs du pool principal attend un en-tête d’hôte qui est différent de l’en-tête d’hôte de client entrantes hello.

2. nom d’hôte hello Hello capacité tooderive de hello IP ou nom de domaine complet de membres du pool hello back-end. Paramètres HTTP fournissent également un nom d’hôte option toopick hello à partir d’un membre du pool principal si configuré avec le nom d’hôte tooderive hello option à partir d’un membre du pool principal individuels. Lorsque vous utilisez fin tooend SSL, ce nom d’hôte est dérivé de nom de domaine complet de hello et sert à hello extension SNI. Cette fonctionnalité permet des scénarios où un pool principal peut avoir deux ou plusieurs des services PaaS mutualisées à des applications web Azure et membre de la demande hello hôte en-tête tooeach contient nom d’hôte hello dérivé de son nom de domaine complet.

> [!NOTE]
> Dans les deux hello précédant cas hello uniquement ces paramètres comportement le trafic dynamique de hello et pas les comportement de sonde d’intégrité hello. Personnalisé des sondes déjà prise en charge hello capacité toospecify un en-tête d’hôte dans la configuration de sonde hello. Les sondes personnalisés prennent désormais en charge également les hello capacité tooderive hello en-tête comportement d’hôte à partir des paramètres de HTTP hello actuellement configuré. Cette configuration peut être spécifiée à l’aide de hello `PickHostNameFromback endAddress` paramètre dans la configuration de sonde hello. Pour fin tooend fonctionnalité toowork, sonde de hello et paramètres de hello HTTP doivent être configuration correctes de hello tooreflect modifié.

Avec cette fonctionnalité, clients spécifient toohello les configuration appropriée des sondes options hello dans les paramètres HTTP hello et personnalisées. Ce paramètre est ensuite lié tooa écouteur et une sauvegarde de pool fin à l’aide d’une règle.

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment tooset d’une passerelle d’application avec une application web en tant qu’une sauvegarde de fin membre du pool en visitant : [configurer le Service application web apps avec Application Gateway](application-gateway-web-app-powershell.md)
