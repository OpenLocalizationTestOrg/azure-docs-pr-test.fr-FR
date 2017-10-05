---
title: "Azure Active Directory B2C : Disponibilité régionale et résidence des données | Microsoft Docs"
description: Une rubrique sur les types de clients Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: gsacavdm
manager: krassk
editor: bryanla
ms.assetid: 8a0644da-b825-4edc-8ce9-541c3c976afb
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: gsacavdm
ms.openlocfilehash: facd66f0324e382ea7609a035de8129ba433846f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-region-availability--data-residency"></a><span data-ttu-id="f9a8b-103">Azure Active Directory B2C : Disponibilité régionale et résidence des données</span><span class="sxs-lookup"><span data-stu-id="f9a8b-103">Azure Active Directory B2C: Region availability & data residency</span></span>
<span data-ttu-id="f9a8b-104">La disponibilité régionale et la résidence des données sont deux concepts très différents qui ne s’appliquent pas à Azure Active Directory B2C de la même façon qu’à Azure.</span><span class="sxs-lookup"><span data-stu-id="f9a8b-104">Region availability and data residency are two very different concepts that apply differently to Azure AD B2C from the rest of Azure.</span></span> <span data-ttu-id="f9a8b-105">Cet article explique les différences entre ces deux concepts et compare la manière dont ils s’appliquent à Azure et Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="f9a8b-105">This article will explain the differences between these two concepts and compare how they apply to Azure versus Azure AD B2C.</span></span>

## <a name="summary"></a><span data-ttu-id="f9a8b-106">Résumé</span><span class="sxs-lookup"><span data-stu-id="f9a8b-106">Summary</span></span>
<span data-ttu-id="f9a8b-107">Azure Active Directory B2C est **généralement disponible dans le monde entier** avec l’option de **résidence des données aux États-Unis ou en Europe**.</span><span class="sxs-lookup"><span data-stu-id="f9a8b-107">Azure AD B2C is **generally available worldwide** with the option for **data residency in United States or Europe**.</span></span>

## <a name="concepts"></a><span data-ttu-id="f9a8b-108">Concepts</span><span class="sxs-lookup"><span data-stu-id="f9a8b-108">Concepts</span></span>
* <span data-ttu-id="f9a8b-109">La **disponibilité régionale** fait référence à l’endroit où se trouve le service pour utilisation.</span><span class="sxs-lookup"><span data-stu-id="f9a8b-109">**Region availability** refers to where a service is available for use.</span></span>
* <span data-ttu-id="f9a8b-110">La **résidence des données** fait référence à l’endroit où sont stockées les données des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f9a8b-110">**Data residency** refers to where user data is stored.</span></span>

## <a name="region-availability"></a><span data-ttu-id="f9a8b-111">Disponibilité des régions</span><span class="sxs-lookup"><span data-stu-id="f9a8b-111">Region availability</span></span>
<span data-ttu-id="f9a8b-112">Azure Active Directory B2C est disponible dans le monde entier via le cloud public Azure.</span><span class="sxs-lookup"><span data-stu-id="f9a8b-112">Azure AD B2C is available worldwide via the Azure public cloud.</span></span> 

<span data-ttu-id="f9a8b-113">Cela diffère du modèle suivi par la plupart des autres services Azure qui associent la disponibilité à la résidence des données.</span><span class="sxs-lookup"><span data-stu-id="f9a8b-113">This differs from the model most other Azure services follow which couple availability with data residency.</span></span> <span data-ttu-id="f9a8b-114">C’est le cas par exemple dans la page [Produits disponibles par région](https://azure.microsoft.com/regions/services/) et la [calculatrice de tarification Active Directory B2C](https://azure.microsoft.com/pricing/details/active-directory-b2c/).</span><span class="sxs-lookup"><span data-stu-id="f9a8b-114">You can see examples of this in both Azure's [Products Available By Region](https://azure.microsoft.com/regions/services/) page and the [Active Directory B2C pricing calculator](https://azure.microsoft.com/pricing/details/active-directory-b2c/).</span></span>

## <a name="data-residency"></a><span data-ttu-id="f9a8b-115">Résidence des données</span><span class="sxs-lookup"><span data-stu-id="f9a8b-115">Data residency</span></span>
<span data-ttu-id="f9a8b-116">Azure Active Directory B2C conserve les données des utilisateurs aux États-Unis ou en Europe.</span><span class="sxs-lookup"><span data-stu-id="f9a8b-116">Azure AD B2C stores user data in either United States or Europe.</span></span>

<span data-ttu-id="f9a8b-117">La résidence des données est déterminée selon le pays/la région sélectionné lors de la [création d’un client Azure Active Directory B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f9a8b-117">Data residency is determined based on which country/region is selected when [creating an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

![Capture d’écran d’un client de la version préliminaire](./media/active-directory-b2c-reference-tenant-type/data-residency-b2c-tenant.png)

<span data-ttu-id="f9a8b-119">Les données des pays/régions suivants sont conservées aux États-Unis :</span><span class="sxs-lookup"><span data-stu-id="f9a8b-119">Data resides in the United States for the following countries/regions:</span></span>

> <span data-ttu-id="f9a8b-120">États-Unis, Canada, Costa Rica, République dominicaine, Salvador, Guatemala, Mexique, Panama, Porto Rico et Trinité-et-Tobago</span><span class="sxs-lookup"><span data-stu-id="f9a8b-120">United States, Canada, Costa Rica, Dominican Republic, El Salvador, Guatemala, Mexico, Panama, Puerto Rico and Trinidad & Tobago</span></span>

<span data-ttu-id="f9a8b-121">Les données des pays/régions suivants sont conservées en Europe :</span><span class="sxs-lookup"><span data-stu-id="f9a8b-121">Data resides in Europe for the following countries/regions:</span></span>

> <span data-ttu-id="f9a8b-122">Algérie, Autriche, Azerbaïdjan, Bahreïn, Biélorussie, Belgique, Bulgarie, Croatie, Chypre, République tchèque, Danemark, Égypte, Estonie, Finlande, France, Allemagne, Grèce, Hongrie, Islande, Irlande, Israël, Italie, Jordanie, Kazakhstan, Kenya, Koweït, Lettonie, Liban, Liechtenstein, Lituanie, Luxembourg, Macédoine, Malte, Monténégro, Maroc, Pays-Bas, Nigeria, Norvège , Oman, Pakistan, Pologne, Portugal, Qatar, Roumanie, Russie, Arabie saoudite, Serbie, Slovaquie, Slovénie, Afrique du Sud, Espagne, Suède, Suisse, Tunisie, Turquie, Ukraine, Émirats Arabes Unis et Royaume-Uni.</span><span class="sxs-lookup"><span data-stu-id="f9a8b-122">Algeria, Austria, Azerbaijan, Bahrain, Belarus, Belgium, Bulgaria, Croatia, Cyprus, Czech Republic, Denmark, Egypt, Estonia, Finland, France, Germany, Greece, Hungary, Iceland, Ireland, Israel, Italy, Jordan, Kazakhstan, Kenya, Kuwait, Lativa, Lebanon, Liechtenstein, Lituania, Luxembourg, Macedonia FYRO, Malta, Montenegro, Morocco, Netherlands, Nigeria, Norway, Oman, Pakistan, Poland, Portugal, Qatar, Romania, Russia, Saudi Arabia, Serbia, Slovakia, Slovenia, South Africa, Spain, Sweden, Switzerland, Tunisia, Turkey, Ukraine, United Arab Emirates and United Kingdom.</span></span>

<span data-ttu-id="f9a8b-123">Les autres pays/régions sont en cours d’ajout à cette liste.</span><span class="sxs-lookup"><span data-stu-id="f9a8b-123">The remaining countries/regions are in the process of being added to the list.</span></span>  <span data-ttu-id="f9a8b-124">Pour le moment, vous pouvez toujours utiliser Azure Active Directory B2C en choisissant l’un des pays ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="f9a8b-124">For now, you can still use Azure AD B2C by picking any of the countries/regions above.</span></span>

> <span data-ttu-id="f9a8b-125">Afghanistan, Argentine, Australie, Brésil, Chili, Colombie, Équateur, RAS de Hong Kong, Inde, Indonésie, Irak, Japon, Corée, Malaisie, Nouvelle-Zélande, Paraguay, Pérou, Philippines, Singapour, Sri Lanka, Taïwan, Thaïlande, Uruguay et Venezuela.</span><span class="sxs-lookup"><span data-stu-id="f9a8b-125">Afghanistan, Argentina, Australia, Brazil, Chile, Colombia, Ecuador, Hong Kong SAR, India, Indonesia, Iraq, Japan, Korea, Malaysia, New Zealand, Paraguay, Peru, Philippines, Singapore, Sri Lanka, Taiwan, Thailand, Uruguay and Venezuela.</span></span>

## <a name="preview-tenant"></a><span data-ttu-id="f9a8b-126">Client de la version préliminaire</span><span class="sxs-lookup"><span data-stu-id="f9a8b-126">Preview tenant</span></span>
<span data-ttu-id="f9a8b-127">Si vous avez créé un client B2C pendant la période d’évaluation d’Azure AD B2C, il est probable que votre **type de client** indique **Client de la version préliminaire**.</span><span class="sxs-lookup"><span data-stu-id="f9a8b-127">If you had created a B2C tenant during Azure AD B2C's preview period, it is likely that your **Tenant type** says **Preview tenant**.</span></span> <span data-ttu-id="f9a8b-128">Si c’est le cas, vous DEVEZ utiliser votre client uniquement à des fins de développement et de test, mais PAS pour les applications de production.</span><span class="sxs-lookup"><span data-stu-id="f9a8b-128">If this is the case, you MUST use your tenant only for development and testing purposes, and NOT for production apps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f9a8b-129">Il n’existe aucun chemin de migration à partir d’un client B2C de la version préliminaire vers un client B2C de mise à l’échelle pour production.</span><span class="sxs-lookup"><span data-stu-id="f9a8b-129">There is no migration path from a preview B2C tenant to a production-scale B2C tenant.</span></span> <span data-ttu-id="f9a8b-130">Notez qu’il existe des problèmes connus liés à la suppression d’un client B2C en version préliminaire et à la recréation d’un client B2C de mise à l’échelle pour production portant le même nom de domaine.</span><span class="sxs-lookup"><span data-stu-id="f9a8b-130">Note that there are known issues when you delete a preview B2C tenant and re-create a production-scale B2C tenant with the same domain name.</span></span> <span data-ttu-id="f9a8b-131">Vous devez créer un client B2C de mise à l’échelle pour production portant un nom de domaine différent.</span><span class="sxs-lookup"><span data-stu-id="f9a8b-131">You have to create a production-scale B2C tenant with a different domain name.</span></span>


![Capture d’écran d’un client de la version préliminaire](./media/active-directory-b2c-reference-tenant-type/preview-b2c-tenant.png)
