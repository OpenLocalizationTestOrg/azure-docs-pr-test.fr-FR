---
title: "L’approvisionnement d’un utilisateur pour une application de la galerie Azure AD prend plusieurs heures | Microsoft Docs"
description: "Comment savoir si l’approvisionnement de votre application risque de prendre plus longtemps que prévu"
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
ms.openlocfilehash: 183d60cbbbc8d02f7cd3cacc160453c45717ef0d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="user-provisioning-to-an-azure-ad-gallery-application-is-taking-hours-or-more"></a><span data-ttu-id="f3d1c-103">L’approvisionnement d’un utilisateur pour une application de la galerie Azure AD prend plusieurs heures</span><span class="sxs-lookup"><span data-stu-id="f3d1c-103">User provisioning to an Azure AD Gallery application is taking hours or more</span></span>

<span data-ttu-id="f3d1c-104">Lorsque vous activez l’approvisionnement automatique d’une application pour la première fois, la synchronisation initiale peut prendre de 20 minutes à plusieurs heures, en fonction de la taille de l’annuaire Azure AD et du nombre d’utilisateurs dans la portée de l’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="f3d1c-104">When first enabling automatic provisioning for an application, the initial sync can take anywhere from 20 minutes to several hours, depending on the size of the Azure AD directory and the number of users in scope for provisioning.</span></span> 

<span data-ttu-id="f3d1c-105">Les synchronisations qui suivent la synchronisation initiale sont plus rapides, car le service d’approvisionnement stocke les filigranes qui représentent l’état des deux systèmes après la synchronisation initiale, ce qui améliore les performances des synchronisations suivantes.</span><span class="sxs-lookup"><span data-stu-id="f3d1c-105">Subsequent syncs after the initial sync be faster, as the provisioning service stores watermarks that represent the state of both systems after the initial sync, improving performance of subsequent syncs.</span></span>

## <a name="how-to-improve-provisioning-performance"></a><span data-ttu-id="f3d1c-106">Comment améliorer les performances de l’approvisionnement</span><span class="sxs-lookup"><span data-stu-id="f3d1c-106">How to improve provisioning performance</span></span>

<span data-ttu-id="f3d1c-107">Si la synchronisation initiale prend plus de quelques heures, une action est possible pour améliorer les performances :</span><span class="sxs-lookup"><span data-stu-id="f3d1c-107">If the initial sync is taking more than a few hours, there is one thing you can do to improve performance:</span></span>

-   <span data-ttu-id="f3d1c-108">**Filtres d’étendue utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="f3d1c-108">**User scoping filters.**</span></span> <span data-ttu-id="f3d1c-109">Les filtres d’étendue vous permettent d’affiner les données que le service d’approvisionnement extrait d’Azure AD en filtrant les utilisateurs en fonction d’attributs spécifiques.</span><span class="sxs-lookup"><span data-stu-id="f3d1c-109">Scoping filters allow you to fine tune the data that the provisioning service extracts from Azure AD by filtering out users based on specific attribute values.</span></span> <span data-ttu-id="f3d1c-110">Pour plus d’informations sur les filtres d’étendue, consultez [Approvisionnement d’applications basé sur les attributs avec filtres d’étendue](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).</span><span class="sxs-lookup"><span data-stu-id="f3d1c-110">For more information on scoping filters, see [Attribute-based application provisioning with scoping filters](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f3d1c-111">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f3d1c-111">Next steps</span></span>
[<span data-ttu-id="f3d1c-112">Automatisation de l’approvisionnement et de la l’annulation de l’approvisionnement des utilisateurs pour les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f3d1c-112">Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory</span></span>](active-directory-saas-app-provisioning.md)

