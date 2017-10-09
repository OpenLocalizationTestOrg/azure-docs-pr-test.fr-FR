---
title: "Azure Active Directory B2C : Disponibilité régionale et résidence des données | Microsoft Docs"
description: "Une rubrique sur les types de clients d’Azure Active Directory B2C hello"
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
ms.openlocfilehash: d382921fe9d62183b6d52c47d62f952dabd116c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-region-availability--data-residency"></a><span data-ttu-id="941ca-103">Azure Active Directory B2C : Disponibilité régionale et résidence des données</span><span class="sxs-lookup"><span data-stu-id="941ca-103">Azure Active Directory B2C: Region availability & data residency</span></span>
<span data-ttu-id="941ca-104">Disponibilité de la région et la délégation de données sont deux concepts très différents qui s’appliquent différemment tooAzure AD B2C reste hello de Azure.</span><span class="sxs-lookup"><span data-stu-id="941ca-104">Region availability and data residency are two very different concepts that apply differently tooAzure AD B2C from hello rest of Azure.</span></span> <span data-ttu-id="941ca-105">Cet article expliquent hello les différences entre ces deux concepts et comparer la façon dont elles s’appliquent tooAzure et Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="941ca-105">This article will explain hello differences between these two concepts and compare how they apply tooAzure versus Azure AD B2C.</span></span>

## <a name="summary"></a><span data-ttu-id="941ca-106">Résumé</span><span class="sxs-lookup"><span data-stu-id="941ca-106">Summary</span></span>
<span data-ttu-id="941ca-107">Azure AD B2C est **généralement disponible dans le monde** avec l’option hello pour **délégation de données dans un État-Unis ou Europe**.</span><span class="sxs-lookup"><span data-stu-id="941ca-107">Azure AD B2C is **generally available worldwide** with hello option for **data residency in United States or Europe**.</span></span>

## <a name="concepts"></a><span data-ttu-id="941ca-108">Concepts</span><span class="sxs-lookup"><span data-stu-id="941ca-108">Concepts</span></span>
* <span data-ttu-id="941ca-109">**Disponibilité de la région** fait référence toowhere un service est disponible pour utilisation.</span><span class="sxs-lookup"><span data-stu-id="941ca-109">**Region availability** refers toowhere a service is available for use.</span></span>
* <span data-ttu-id="941ca-110">**Délégation de données** fait référence utilisateur toowhere les données sont stockées.</span><span class="sxs-lookup"><span data-stu-id="941ca-110">**Data residency** refers toowhere user data is stored.</span></span>

## <a name="region-availability"></a><span data-ttu-id="941ca-111">Disponibilité des régions</span><span class="sxs-lookup"><span data-stu-id="941ca-111">Region availability</span></span>
<span data-ttu-id="941ca-112">Azure AD B2C est disponible dans le monde entier via hello cloud public Azure.</span><span class="sxs-lookup"><span data-stu-id="941ca-112">Azure AD B2C is available worldwide via hello Azure public cloud.</span></span> 

<span data-ttu-id="941ca-113">Cela diffère de modèle de hello la plupart des autres suivent des services Azure risquent de disponibilité avec la délégation de données.</span><span class="sxs-lookup"><span data-stu-id="941ca-113">This differs from hello model most other Azure services follow which couple availability with data residency.</span></span> <span data-ttu-id="941ca-114">Vous pouvez voir des exemples dans les deux Azure [produits disponibles par région](https://azure.microsoft.com/regions/services/) page et hello [calculatrice de prix Active Directory B2C](https://azure.microsoft.com/pricing/details/active-directory-b2c/).</span><span class="sxs-lookup"><span data-stu-id="941ca-114">You can see examples of this in both Azure's [Products Available By Region](https://azure.microsoft.com/regions/services/) page and hello [Active Directory B2C pricing calculator](https://azure.microsoft.com/pricing/details/active-directory-b2c/).</span></span>

## <a name="data-residency"></a><span data-ttu-id="941ca-115">Résidence des données</span><span class="sxs-lookup"><span data-stu-id="941ca-115">Data residency</span></span>
<span data-ttu-id="941ca-116">Azure Active Directory B2C conserve les données des utilisateurs aux États-Unis ou en Europe.</span><span class="sxs-lookup"><span data-stu-id="941ca-116">Azure AD B2C stores user data in either United States or Europe.</span></span>

<span data-ttu-id="941ca-117">La résidence des données est déterminée selon le pays/la région sélectionné lors de la [création d’un client Azure Active Directory B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="941ca-117">Data residency is determined based on which country/region is selected when [creating an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

![Capture d’écran d’un client de la version préliminaire](./media/active-directory-b2c-reference-tenant-type/data-residency-b2c-tenant.png)

<span data-ttu-id="941ca-119">Données se trouvent aux États-Unis hello pour hello suivant pays/régions :</span><span class="sxs-lookup"><span data-stu-id="941ca-119">Data resides in hello United States for hello following countries/regions:</span></span>

> <span data-ttu-id="941ca-120">États-Unis, Canada, Costa Rica, République dominicaine, Salvador, Guatemala, Mexique, Panama, Porto Rico et Trinité-et-Tobago</span><span class="sxs-lookup"><span data-stu-id="941ca-120">United States, Canada, Costa Rica, Dominican Republic, El Salvador, Guatemala, Mexico, Panama, Puerto Rico and Trinidad & Tobago</span></span>

<span data-ttu-id="941ca-121">Données se trouvent en Europe pour hello suivant pays/régions :</span><span class="sxs-lookup"><span data-stu-id="941ca-121">Data resides in Europe for hello following countries/regions:</span></span>

> <span data-ttu-id="941ca-122">Algérie, Autriche, Azerbaïdjan, Bahreïn, Biélorussie, Belgique, Bulgarie, Croatie, Chypre, République tchèque, Danemark, Égypte, Estonie, Finlande, France, Allemagne, Grèce, Hongrie, Islande, Irlande, Israël, Italie, Jordanie, Kazakhstan, Kenya, Koweït, Lettonie, Liban, Liechtenstein, Lituanie, Luxembourg, Macédoine, Malte, Monténégro, Maroc, Pays-Bas, Nigeria, Norvège , Oman, Pakistan, Pologne, Portugal, Qatar, Roumanie, Russie, Arabie saoudite, Serbie, Slovaquie, Slovénie, Afrique du Sud, Espagne, Suède, Suisse, Tunisie, Turquie, Ukraine, Émirats Arabes Unis et Royaume-Uni.</span><span class="sxs-lookup"><span data-stu-id="941ca-122">Algeria, Austria, Azerbaijan, Bahrain, Belarus, Belgium, Bulgaria, Croatia, Cyprus, Czech Republic, Denmark, Egypt, Estonia, Finland, France, Germany, Greece, Hungary, Iceland, Ireland, Israel, Italy, Jordan, Kazakhstan, Kenya, Kuwait, Lativa, Lebanon, Liechtenstein, Lituania, Luxembourg, Macedonia FYRO, Malta, Montenegro, Morocco, Netherlands, Nigeria, Norway, Oman, Pakistan, Poland, Portugal, Qatar, Romania, Russia, Saudi Arabia, Serbia, Slovakia, Slovenia, South Africa, Spain, Sweden, Switzerland, Tunisia, Turkey, Ukraine, United Arab Emirates and United Kingdom.</span></span>

<span data-ttu-id="941ca-123">Hello autres pays/régions sont dans le processus de hello de toohello liste ajoutée.</span><span class="sxs-lookup"><span data-stu-id="941ca-123">hello remaining countries/regions are in hello process of being added toohello list.</span></span>  <span data-ttu-id="941ca-124">Pour l’instant, vous pouvez toujours utiliser Azure AD B2C en choisissant une des pays/régions de hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="941ca-124">For now, you can still use Azure AD B2C by picking any of hello countries/regions above.</span></span>

> <span data-ttu-id="941ca-125">Afghanistan, Argentine, Australie, Brésil, Chili, Colombie, Équateur, RAS de Hong Kong, Inde, Indonésie, Irak, Japon, Corée, Malaisie, Nouvelle-Zélande, Paraguay, Pérou, Philippines, Singapour, Sri Lanka, Taïwan, Thaïlande, Uruguay et Venezuela.</span><span class="sxs-lookup"><span data-stu-id="941ca-125">Afghanistan, Argentina, Australia, Brazil, Chile, Colombia, Ecuador, Hong Kong SAR, India, Indonesia, Iraq, Japan, Korea, Malaysia, New Zealand, Paraguay, Peru, Philippines, Singapore, Sri Lanka, Taiwan, Thailand, Uruguay and Venezuela.</span></span>

## <a name="preview-tenant"></a><span data-ttu-id="941ca-126">Client de la version préliminaire</span><span class="sxs-lookup"><span data-stu-id="941ca-126">Preview tenant</span></span>
<span data-ttu-id="941ca-127">Si vous avez créé un client B2C pendant la période d’évaluation d’Azure AD B2C, il est probable que votre **type de client** indique **Client de la version préliminaire**.</span><span class="sxs-lookup"><span data-stu-id="941ca-127">If you had created a B2C tenant during Azure AD B2C's preview period, it is likely that your **Tenant type** says **Preview tenant**.</span></span> <span data-ttu-id="941ca-128">Si c’est le cas de hello, vous devez utiliser votre client uniquement pour le développement et à des fins de tests et pas pour les applications de production.</span><span class="sxs-lookup"><span data-stu-id="941ca-128">If this is hello case, you MUST use your tenant only for development and testing purposes, and NOT for production apps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="941ca-129">Il n’existe aucun chemin d’accès de la migration à partir d’un client de B2C B2C locataire tooa production à l’échelle d’aperçu.</span><span class="sxs-lookup"><span data-stu-id="941ca-129">There is no migration path from a preview B2C tenant tooa production-scale B2C tenant.</span></span> <span data-ttu-id="941ca-130">Notez que des problèmes connus lorsque vous supprimez un client Aperçu B2C et recréer un B2C de production à l’échelle de locataire avec hello le même nom de domaine.</span><span class="sxs-lookup"><span data-stu-id="941ca-130">Note that there are known issues when you delete a preview B2C tenant and re-create a production-scale B2C tenant with hello same domain name.</span></span> <span data-ttu-id="941ca-131">Vous avez toocreate un locataire B2C de production à l’échelle avec un nom de domaine différent.</span><span class="sxs-lookup"><span data-stu-id="941ca-131">You have toocreate a production-scale B2C tenant with a different domain name.</span></span>


![Capture d’écran d’un client de la version préliminaire](./media/active-directory-b2c-reference-tenant-type/preview-b2c-tenant.png)
