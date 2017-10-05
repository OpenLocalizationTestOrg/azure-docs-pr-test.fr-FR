---
title: "Limiter l’accès à votre contenu CDN Azure par pays | Microsoft Docs"
description: "Découvrez comment limiter l’accès à votre contenu Azure CDN à l’aide de la fonctionnalité de filtrage géographique."
services: cdn
documentationcenter: 
author: lichard
manager: akucer
editor: 
ms.assetid: 12c17cc5-28ee-4b0b-ba22-2266be2e786a
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: 30160088d9c770400f342e67527e1cf1cabc4f6b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="restrict-azure-cdn-content-by-country"></a><span data-ttu-id="bee58-103">Limiter l’accès à votre contenu CDN Azure par pays</span><span class="sxs-lookup"><span data-stu-id="bee58-103">Restrict Azure CDN content by country</span></span>

## <a name="overview"></a><span data-ttu-id="bee58-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="bee58-104">Overview</span></span>
<span data-ttu-id="bee58-105">Par défaut, lorsqu'un utilisateur demande du contenu, le contenu est pris en charge, quel que soit l’endroit d’où vient la demande.</span><span class="sxs-lookup"><span data-stu-id="bee58-105">When a user requests your content, by default, the content is served regardless of where the user made this request from.</span></span> <span data-ttu-id="bee58-106">Dans certains cas, vous souhaiterez limiter l'accès à votre contenu par pays.</span><span class="sxs-lookup"><span data-stu-id="bee58-106">In some cases, you may want to restrict access to your content by country.</span></span> <span data-ttu-id="bee58-107">Cette rubrique explique comment utiliser la fonctionnalité de **Filtrage géographique** afin de configurer le service pour autoriser ou bloquer l'accès par pays.</span><span class="sxs-lookup"><span data-stu-id="bee58-107">This topic explains how to use the **Geo-Filtering** feature in order to configure the service to allow or block access by country.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bee58-108">Les produits Verizon et Akamai fournissent la même fonctionnalité de filtrage géographique, mais dans une interface utilisateur légèrement différente.</span><span class="sxs-lookup"><span data-stu-id="bee58-108">The Verizon and Akamai products provide the same geo-filtering functionality but have a small difference in te country codes they support.</span></span> <span data-ttu-id="bee58-109">Un lien vers les différences est disponible à l’étape 3.</span><span class="sxs-lookup"><span data-stu-id="bee58-109">See Step 3 for a link to the differences.</span></span>


<span data-ttu-id="bee58-110">Pour plus d’informations sur les considérations qui s’appliquent à la configuration de ce type de restriction, consultez la section [Considérations](cdn-restrict-access-by-country.md#considerations) à la fin de la rubrique.</span><span class="sxs-lookup"><span data-stu-id="bee58-110">For information about considerations that apply to configuring this type of restriction, see the [Considerations](cdn-restrict-access-by-country.md#considerations) section at the end of the topic.</span></span>  

![Filtrage par pays](./media/cdn-filtering/cdn-country-filtering-akamai.png)

## <a name="step-1-define-the-directory-path"></a><span data-ttu-id="bee58-112">Étape 1 : définir le chemin d'accès</span><span class="sxs-lookup"><span data-stu-id="bee58-112">Step 1: Define the directory path</span></span>
<span data-ttu-id="bee58-113">Sélectionnez votre point de terminaison dans le portail et trouvez l’onglet Filtrage géographique dans le volet de navigation gauche pour trouver cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="bee58-113">Select your endpoint within the portal, and find the Geo-Filtering tab on the left-hand navigation to find this feature.</span></span>

<span data-ttu-id="bee58-114">Lorsque vous configurez un filtre de pays, vous devez spécifier le chemin d'accès relatif à l'emplacement auquel les accès utilisateurs sont autorisés ou refusés.</span><span class="sxs-lookup"><span data-stu-id="bee58-114">When configuring a country filter, you must specify the relative path to the location to which users will be allowed or denied access.</span></span> <span data-ttu-id="bee58-115">Vous pouvez appliquer le filtrage géographique pour tous vos fichiers avec « / » ou certains dossiers en spécifiant des chemins d'accès au répertoire "/pictures/".</span><span class="sxs-lookup"><span data-stu-id="bee58-115">You can apply geo-filtering for all your files with "/" or selected folders by specifying directory paths "/pictures/".</span></span> <span data-ttu-id="bee58-116">Vous pouvez également appliquer le filtrage géographique à un seul fichier en spécifiant le fichier et en omettant la barre oblique « /pictures/city.png ».</span><span class="sxs-lookup"><span data-stu-id="bee58-116">You can also apply geo-filtering to a single file by specifying the file, and leaving out the trailing slash "/pictures/city.png".</span></span>

<span data-ttu-id="bee58-117">Exemple de filtre de chemin d'accès au répertoire :</span><span class="sxs-lookup"><span data-stu-id="bee58-117">Example directory path filter:</span></span>

    /                                 
    /Photos/
    /Photos/Strasbourg/
      /Photos/Strasbourg/city.png

## <a name="step-2-define-the-action-block-or-allow"></a><span data-ttu-id="bee58-118">Étape 2 : Définir l'action : autoriser ou bloquer</span><span class="sxs-lookup"><span data-stu-id="bee58-118">Step 2: Define the action: block or allow</span></span>
<span data-ttu-id="bee58-119">**Bloquer** : l’accès aux ressources demandées à partir de ce chemin d'accès récursif est bloqué aux utilisateurs des pays spécifiés.</span><span class="sxs-lookup"><span data-stu-id="bee58-119">**Block:** Users from the specified countries will be denied access to assets requested from that recursive path.</span></span> <span data-ttu-id="bee58-120">Si aucune autre option de filtrage par pays n'a été configurée pour cet emplacement, tous les autres utilisateurs sont autorisés à y accéder.</span><span class="sxs-lookup"><span data-stu-id="bee58-120">If no other country filtering options have been configured for that location, then all other users will be allowed access.</span></span>

<span data-ttu-id="bee58-121">**Autoriser** : l’accès aux ressources demandées à partir de ce chemin d'accès récursif est autorisé aux seuls utilisateurs des pays spécifiés.</span><span class="sxs-lookup"><span data-stu-id="bee58-121">**Allow:** Only users from the specified countries will be allowed access to assets requested from that recursive path.</span></span>

## <a name="step-3-define-the-countries"></a><span data-ttu-id="bee58-122">Étape 3 : définir les pays</span><span class="sxs-lookup"><span data-stu-id="bee58-122">Step 3: Define the countries</span></span>
<span data-ttu-id="bee58-123">Sélectionnez les pays que vous souhaitez bloquer ou autoriser pour le chemin d'accès.</span><span class="sxs-lookup"><span data-stu-id="bee58-123">Select the countries that you want to block or allow for the path.</span></span> 

<span data-ttu-id="bee58-124">Par exemple, la règle de blocage /Photos/Strasbourg/ filtre les fichiers, notamment :</span><span class="sxs-lookup"><span data-stu-id="bee58-124">For example, the rule of blocking /Photos/Strasbourg/ will filter files including:</span></span>

    http://<endpoint>.azureedge.net/Photos/Strasbourg/1000.jpg
    http://<endpoint>.azureedge.net/Photos/Strasbourg/Cathedral/1000.jpg


### <a name="country-codes"></a><span data-ttu-id="bee58-125">Codes de pays</span><span class="sxs-lookup"><span data-stu-id="bee58-125">Country codes</span></span>
<span data-ttu-id="bee58-126">La fonctionnalité de **Filtrage géographique** utilise des codes de pays pour définir les pays à partir desquels une demande est autorisée ou bloquée pour un répertoire sécurisé.</span><span class="sxs-lookup"><span data-stu-id="bee58-126">The **Geo-Filtering** feature uses country codes to define the countries from which a request will be allowed or blocked for a secured directory.</span></span> <span data-ttu-id="bee58-127">Vous trouverez les codes de pays sur la page [Azure CDN Country Codes (Code de pays du CDN Azure)](https://msdn.microsoft.com/library/mt761717.aspx).</span><span class="sxs-lookup"><span data-stu-id="bee58-127">You will find the country codes in [Azure CDN  Country Codes](https://msdn.microsoft.com/library/mt761717.aspx).</span></span> 

## <span data-ttu-id="bee58-128"><a id="considerations"></a>Considérations</span><span class="sxs-lookup"><span data-stu-id="bee58-128"><a id="considerations"></a>Considerations</span></span>
* <span data-ttu-id="bee58-129">L’implémentation des modifications apportées à votre configuration de filtrage par pays peut prendre jusqu’à 90 minutes avec la solution Verizon ou quelques minutes avec la solution Akamai.</span><span class="sxs-lookup"><span data-stu-id="bee58-129">It may take up to 90 minutes for Verizon, or a couple minutes with Akamai, for changes to your country filtering configuration to take effect.</span></span>
* <span data-ttu-id="bee58-130">Cette fonctionnalité ne prend pas en charge les caractères génériques (par exemple, « * »).</span><span class="sxs-lookup"><span data-stu-id="bee58-130">This feature does not support wildcard characters (for example, ‘*’).</span></span>
* <span data-ttu-id="bee58-131">La configuration de filtrage géographique associée avec le chemin d'accès relatif de filtrage est appliquée de manière récursive à ce chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="bee58-131">The geo-filtering configuration associated with the relative path will be applied recursively to that path.</span></span>
* <span data-ttu-id="bee58-132">Une seule règle peut être appliquée au même chemin d'accès relatif (vous ne pouvez pas créer plusieurs filtres de pays qui pointent vers le même chemin d'accès relatif).</span><span class="sxs-lookup"><span data-stu-id="bee58-132">Only one rule can be applied to the same relative path (you cannot create multiple country filters that point to the same relative path.</span></span> <span data-ttu-id="bee58-133">Toutefois, un dossier peut avoir plusieurs filtres par pays.</span><span class="sxs-lookup"><span data-stu-id="bee58-133">However, a folder may have multiple country filters.</span></span> <span data-ttu-id="bee58-134">Cela est dû à la nature récursive des filtres par pays.</span><span class="sxs-lookup"><span data-stu-id="bee58-134">This is due to the recursive nature of country filters.</span></span> <span data-ttu-id="bee58-135">En d'autres termes, un filtre par pays différent peut être attribué à un sous-dossier d'un dossier déjà configuré.</span><span class="sxs-lookup"><span data-stu-id="bee58-135">In other words, a subfolder of a previously configured folder can be assigned a different country filter.</span></span>

