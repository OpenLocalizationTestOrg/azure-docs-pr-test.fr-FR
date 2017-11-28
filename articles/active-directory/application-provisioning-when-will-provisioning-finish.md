---
title: "aaaUser approvisionnement d’une application de la galerie tooan Azure AD est prise en heures ou plus | Documents Microsoft"
description: "Comment toofind out pourquoi configuration tooyour application peut prendre plus de temps que prévu"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 0658f041724c91ddd1997cc7759393b46680f13a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="user-provisioning-tooan-azure-ad-gallery-application-is-taking-hours-or-more"></a><span data-ttu-id="1e40e-103">Configuration d’application de la galerie tooan Azure AD de l’utilisateur est tenu heures ou plus</span><span class="sxs-lookup"><span data-stu-id="1e40e-103">User provisioning tooan Azure AD Gallery application is taking hours or more</span></span>

<span data-ttu-id="1e40e-104">Lorsque vous activez tout d’abord la configuration automatique pour une application, la synchronisation initiale hello peut prendre entre 20 minutes tooseveral heures, selon la taille de hello de Windows Azure AD pour hello et hello des utilisateurs dans la portée pour la configuration.</span><span class="sxs-lookup"><span data-stu-id="1e40e-104">When first enabling automatic provisioning for an application, hello initial sync can take anywhere from 20 minutes tooseveral hours, depending on hello size of hello Azure AD directory and hello number of users in scope for provisioning.</span></span> 

<span data-ttu-id="1e40e-105">Les synchronisations suivantes après la synchronisation initiale hello être plus rapide, hello configuration service stocke les filigranes qui représentent l’état hello des deux systèmes après la synchronisation initiale hello, améliorer les performances des synchronisations suivantes.</span><span class="sxs-lookup"><span data-stu-id="1e40e-105">Subsequent syncs after hello initial sync be faster, as hello provisioning service stores watermarks that represent hello state of both systems after hello initial sync, improving performance of subsequent syncs.</span></span>

## <a name="how-tooimprove-provisioning-performance"></a><span data-ttu-id="1e40e-106">Comment tooimprove mise en service des performances</span><span class="sxs-lookup"><span data-stu-id="1e40e-106">How tooimprove provisioning performance</span></span>

<span data-ttu-id="1e40e-107">Si la synchronisation initiale hello prend plusieurs heures, il est une chose à faire tooimprove performances :</span><span class="sxs-lookup"><span data-stu-id="1e40e-107">If hello initial sync is taking more than a few hours, there is one thing you can do tooimprove performance:</span></span>

-   <span data-ttu-id="1e40e-108">**Filtres d’étendue utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="1e40e-108">**User scoping filters.**</span></span> <span data-ttu-id="1e40e-109">Filtres d’étendue permettent de données hello régler toofine hello configuration extraits de service à partir d’Azure AD en filtrant les utilisateurs basés sur des valeurs d’attribut spécifiques.</span><span class="sxs-lookup"><span data-stu-id="1e40e-109">Scoping filters allow you toofine tune hello data that hello provisioning service extracts from Azure AD by filtering out users based on specific attribute values.</span></span> <span data-ttu-id="1e40e-110">Pour plus d’informations sur les filtres d’étendue, consultez [Approvisionnement d’applications basé sur les attributs avec filtres d’étendue](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).</span><span class="sxs-lookup"><span data-stu-id="1e40e-110">For more information on scoping filters, see [Attribute-based application provisioning with scoping filters](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e40e-111">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1e40e-111">Next steps</span></span>
[<span data-ttu-id="1e40e-112">Automatiser la configuration de l’utilisateur et Deprovisioning tooSaaS Applications avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1e40e-112">Automate User Provisioning and Deprovisioning tooSaaS Applications with Azure Active Directory</span></span>](active-directory-saas-app-provisioning.md)

