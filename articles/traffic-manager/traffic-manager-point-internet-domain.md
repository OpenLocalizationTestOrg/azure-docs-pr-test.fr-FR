---
title: aaaPoint un nom de domaine du domaine tooa Traffic Manager entreprise Internet | Documents Microsoft
description: "Cet article va vous aider à pointer votre nom de domaine de société domaine nom tooa Traffic Manager."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 29822946-2d45-4434-ba47-fc180a445cc3
ms.service: traffic-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/11/2016
ms.author: kumud
ms.openlocfilehash: 84c428f60a1dc70452bf957d98a68c95e0b51715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="point-a-company-internet-domain-tooan-azure-traffic-manager-domain"></a>Pointer un domaine de société Internet domaine tooan Azure Traffic Manager

Lorsque vous créez un profil Traffic Manager, Azure attribue automatiquement un nom DNS pour ce profil. toouse un nom à partir de votre zone DNS, créez un enregistrement DNS CNAME qui mappe le nom de domaine toohello de votre profil Traffic Manager. Vous trouverez le nom de domaine Traffic Manager hello Bonjour **général** section sur la page de Configuration hello Hello profil Traffic Manager.

Par exemple, toopoint nom www.contoso.com toohello contoso.trafficmanager.net de nom DNS Traffic Manager, vous devez créer hello suivant l’enregistrement de ressource DNS :

    www.contoso.com IN CNAME contoso.trafficmanager.net

Tout le trafic demande trop*www.contoso.com* sont dirigés trop*contoso.trafficmanager.net*.

> [!IMPORTANT]
> Vous ne peut pas pointer un domaine de second niveau, tel que *contoso.com*, domaine de Traffic Manager toohello. Les normes de protocole DNS n’autorisent pas les enregistrements CNAME pour les noms de domaine de second niveau.

## <a name="next-steps"></a>Étapes suivantes

* [Méthodes de routage de Traffic Manager](traffic-manager-routing-methods.md)
* [Traffic Manager - Désactiver, activer ou supprimer un profil](disable-enable-or-delete-a-profile.md)
* [Traffic Manager - Désactiver ou activer un point de terminaison](disable-or-enable-an-endpoint.md)
