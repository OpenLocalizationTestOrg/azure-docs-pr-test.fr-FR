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
# <a name="point-a-company-internet-domain-tooan-azure-traffic-manager-domain"></a><span data-ttu-id="d7190-103">Pointer un domaine de société Internet domaine tooan Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="d7190-103">Point a company Internet domain tooan Azure Traffic Manager domain</span></span>

<span data-ttu-id="d7190-104">Lorsque vous créez un profil Traffic Manager, Azure attribue automatiquement un nom DNS pour ce profil.</span><span class="sxs-lookup"><span data-stu-id="d7190-104">When you create a Traffic Manager profile, Azure automatically assigns a DNS name for that profile.</span></span> <span data-ttu-id="d7190-105">toouse un nom à partir de votre zone DNS, créez un enregistrement DNS CNAME qui mappe le nom de domaine toohello de votre profil Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="d7190-105">toouse a name from your DNS zone, create a CNAME DNS record that maps toohello domain name of your Traffic Manager profile.</span></span> <span data-ttu-id="d7190-106">Vous trouverez le nom de domaine Traffic Manager hello Bonjour **général** section sur la page de Configuration hello Hello profil Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="d7190-106">You can find hello Traffic Manager domain name in hello **General** section on hello Configuration page of hello Traffic Manager profile.</span></span>

<span data-ttu-id="d7190-107">Par exemple, toopoint nom www.contoso.com toohello contoso.trafficmanager.net de nom DNS Traffic Manager, vous devez créer hello suivant l’enregistrement de ressource DNS :</span><span class="sxs-lookup"><span data-stu-id="d7190-107">For example, toopoint name www.contoso.com toohello Traffic Manager DNS name contoso.trafficmanager.net, you would create hello following DNS resource record:</span></span>

    www.contoso.com IN CNAME contoso.trafficmanager.net

<span data-ttu-id="d7190-108">Tout le trafic demande trop*www.contoso.com* sont dirigés trop*contoso.trafficmanager.net*.</span><span class="sxs-lookup"><span data-stu-id="d7190-108">All traffic requests too*www.contoso.com* get directed too*contoso.trafficmanager.net*.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d7190-109">Vous ne peut pas pointer un domaine de second niveau, tel que *contoso.com*, domaine de Traffic Manager toohello.</span><span class="sxs-lookup"><span data-stu-id="d7190-109">You cannot point a second-level domain, such as *contoso.com*, toohello Traffic Manager domain.</span></span> <span data-ttu-id="d7190-110">Les normes de protocole DNS n’autorisent pas les enregistrements CNAME pour les noms de domaine de second niveau.</span><span class="sxs-lookup"><span data-stu-id="d7190-110">DNS protocol standards do not allow CNAME records for second-level domain names.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7190-111">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d7190-111">Next steps</span></span>

* [<span data-ttu-id="d7190-112">Méthodes de routage de Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="d7190-112">Traffic Manager routing methods</span></span>](traffic-manager-routing-methods.md)
* [<span data-ttu-id="d7190-113">Traffic Manager - Désactiver, activer ou supprimer un profil</span><span class="sxs-lookup"><span data-stu-id="d7190-113">Traffic Manager - Disable, enable or delete a profile</span></span>](disable-enable-or-delete-a-profile.md)
* [<span data-ttu-id="d7190-114">Traffic Manager - Désactiver ou activer un point de terminaison</span><span class="sxs-lookup"><span data-stu-id="d7190-114">Traffic Manager - Disable or enable an endpoint</span></span>](disable-or-enable-an-endpoint.md)
