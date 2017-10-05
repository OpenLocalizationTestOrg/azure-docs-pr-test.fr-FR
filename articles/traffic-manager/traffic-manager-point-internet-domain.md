---
title: "Rediriger un domaine Internet d’entreprise sur un nom de domaine Traffic Manager | Microsoft Docs"
description: "Cet article vous aide à rediriger votre nom de domaine d’entreprise vers un nom de domaine Traffic Manager."
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
ms.openlocfilehash: 0322b3510cfd4f94031d8c1db8f1cc032b997fa8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="point-a-company-internet-domain-to-an-azure-traffic-manager-domain"></a><span data-ttu-id="b628a-103">Redirection d’un domaine Internet d’entreprise vers un domaine Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="b628a-103">Point a company Internet domain to an Azure Traffic Manager domain</span></span>

<span data-ttu-id="b628a-104">Lorsque vous créez un profil Traffic Manager, Azure attribue automatiquement un nom DNS pour ce profil.</span><span class="sxs-lookup"><span data-stu-id="b628a-104">When you create a Traffic Manager profile, Azure automatically assigns a DNS name for that profile.</span></span> <span data-ttu-id="b628a-105">Pour utiliser un nom de votre zone DNS, créez un enregistrement DNS CNAME qui mappe sur le nom de domaine de votre profil Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="b628a-105">To use a name from your DNS zone, create a CNAME DNS record that maps to the domain name of your Traffic Manager profile.</span></span> <span data-ttu-id="b628a-106">Vous pouvez trouver le nom de domaine Traffic Manager dans la section **Général** de la page Configuration du profil Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="b628a-106">You can find the Traffic Manager domain name in the **General** section on the Configuration page of the Traffic Manager profile.</span></span>

<span data-ttu-id="b628a-107">Par exemple, pour rediriger le nom www.contoso.com vers le nom DNS Traffic Manager contoso.trafficmanager.net, vous devez créer l’enregistrement de ressource DNS suivant :</span><span class="sxs-lookup"><span data-stu-id="b628a-107">For example, to point name www.contoso.com to the Traffic Manager DNS name contoso.trafficmanager.net, you would create the following DNS resource record:</span></span>

    www.contoso.com IN CNAME contoso.trafficmanager.net

<span data-ttu-id="b628a-108">L’intégralité des demandes de trafic pour *www.contoso.com* est redirigée vers *contoso.trafficmanager.net*.</span><span class="sxs-lookup"><span data-stu-id="b628a-108">All traffic requests to *www.contoso.com* get directed to *contoso.trafficmanager.net*.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b628a-109">Vous ne pouvez pas rediriger un domaine de second niveau tel que *contoso.com*vers le domaine Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="b628a-109">You cannot point a second-level domain, such as *contoso.com*, to the Traffic Manager domain.</span></span> <span data-ttu-id="b628a-110">Les normes de protocole DNS n’autorisent pas les enregistrements CNAME pour les noms de domaine de second niveau.</span><span class="sxs-lookup"><span data-stu-id="b628a-110">DNS protocol standards do not allow CNAME records for second-level domain names.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b628a-111">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b628a-111">Next steps</span></span>

* [<span data-ttu-id="b628a-112">Méthodes de routage de Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="b628a-112">Traffic Manager routing methods</span></span>](traffic-manager-routing-methods.md)
* [<span data-ttu-id="b628a-113">Traffic Manager - Désactiver, activer ou supprimer un profil</span><span class="sxs-lookup"><span data-stu-id="b628a-113">Traffic Manager - Disable, enable or delete a profile</span></span>](disable-enable-or-delete-a-profile.md)
* [<span data-ttu-id="b628a-114">Traffic Manager - Désactiver ou activer un point de terminaison</span><span class="sxs-lookup"><span data-stu-id="b628a-114">Traffic Manager - Disable or enable an endpoint</span></span>](disable-or-enable-an-endpoint.md)
