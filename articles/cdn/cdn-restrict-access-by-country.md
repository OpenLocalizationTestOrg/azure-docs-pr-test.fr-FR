---
title: aaaRestrict contenu du CDN Azure par pays | Documents Microsoft
description: "Découvrez comment toorestrict accès tooyour Azure CDN contenu à l’aide hello les fonctionnalité de filtrage de géo-réplication."
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
ms.openlocfilehash: ffdd994612b6c9cfbf1a6e29d260709b4afa86e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="restrict-azure-cdn-content-by-country"></a><span data-ttu-id="4892d-103">Limiter l’accès à votre contenu CDN Azure par pays</span><span class="sxs-lookup"><span data-stu-id="4892d-103">Restrict Azure CDN content by country</span></span>

## <a name="overview"></a><span data-ttu-id="4892d-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="4892d-104">Overview</span></span>
<span data-ttu-id="4892d-105">Lorsqu’un utilisateur demande votre contenu, par défaut, le contenu hello est pris en charge, quelle que soit l’endroit cette demande à partir d’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="4892d-105">When a user requests your content, by default, hello content is served regardless of where hello user made this request from.</span></span> <span data-ttu-id="4892d-106">Dans certains cas, vous souhaiterez peut-être toorestrict accéder au contenu de tooyour par pays.</span><span class="sxs-lookup"><span data-stu-id="4892d-106">In some cases, you may want toorestrict access tooyour content by country.</span></span> <span data-ttu-id="4892d-107">Cette rubrique explique comment toouse hello **filtrage géographique** fonctionnalité dans l’ordre tooconfigure hello service tooallow ou bloquer l’accès par pays.</span><span class="sxs-lookup"><span data-stu-id="4892d-107">This topic explains how toouse hello **Geo-Filtering** feature in order tooconfigure hello service tooallow or block access by country.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4892d-108">les produits Verizon et Akamai Hello fournissent hello les mêmes fonctionnalités de filtrage de géo-réplication, mais ont une légère différence dans les codes de pays te ils prennent en charge.</span><span class="sxs-lookup"><span data-stu-id="4892d-108">hello Verizon and Akamai products provide hello same geo-filtering functionality but have a small difference in te country codes they support.</span></span> <span data-ttu-id="4892d-109">Consultez l’étape 3 pour un différences toohello de lien.</span><span class="sxs-lookup"><span data-stu-id="4892d-109">See Step 3 for a link toohello differences.</span></span>


<span data-ttu-id="4892d-110">Pour plus d’informations sur les considérations qui s’appliquent tooconfiguring ce type de restriction, consultez hello [considérations](cdn-restrict-access-by-country.md#considerations) section à fin hello de rubrique de hello.</span><span class="sxs-lookup"><span data-stu-id="4892d-110">For information about considerations that apply tooconfiguring this type of restriction, see hello [Considerations](cdn-restrict-access-by-country.md#considerations) section at hello end of hello topic.</span></span>  

![Filtrage par pays](./media/cdn-filtering/cdn-country-filtering-akamai.png)

## <a name="step-1-define-hello-directory-path"></a><span data-ttu-id="4892d-112">Étape 1 : Définir le chemin d’accès du répertoire hello</span><span class="sxs-lookup"><span data-stu-id="4892d-112">Step 1: Define hello directory path</span></span>
<span data-ttu-id="4892d-113">Sélectionnez votre point de terminaison dans le portail de hello et hello filtrage géographique onglet toofind de navigation gauche hello vous trouverez cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="4892d-113">Select your endpoint within hello portal, and find hello Geo-Filtering tab on hello left-hand navigation toofind this feature.</span></span>

<span data-ttu-id="4892d-114">Lorsque vous configurez un filtre de pays, vous devez spécifier les utilisateurs toowhich hello chemin d’accès relatif toohello seront autorisés ou refusés l’accès.</span><span class="sxs-lookup"><span data-stu-id="4892d-114">When configuring a country filter, you must specify hello relative path toohello location toowhich users will be allowed or denied access.</span></span> <span data-ttu-id="4892d-115">Vous pouvez appliquer le filtrage géographique pour tous vos fichiers avec « / » ou certains dossiers en spécifiant des chemins d'accès au répertoire "/pictures/".</span><span class="sxs-lookup"><span data-stu-id="4892d-115">You can apply geo-filtering for all your files with "/" or selected folders by specifying directory paths "/pictures/".</span></span> <span data-ttu-id="4892d-116">Vous pouvez également appliquer filtrage géographique de tooa fichier unique en spécifiant le fichier de hello et en laissant hello barre oblique « / Pictures/City.png ».</span><span class="sxs-lookup"><span data-stu-id="4892d-116">You can also apply geo-filtering tooa single file by specifying hello file, and leaving out hello trailing slash "/pictures/city.png".</span></span>

<span data-ttu-id="4892d-117">Exemple de filtre de chemin d'accès au répertoire :</span><span class="sxs-lookup"><span data-stu-id="4892d-117">Example directory path filter:</span></span>

    /                                 
    /Photos/
    /Photos/Strasbourg/
      /Photos/Strasbourg/city.png

## <a name="step-2-define-hello-action-block-or-allow"></a><span data-ttu-id="4892d-118">Étape 2 : Définir l’action de hello : bloquer ou autoriser</span><span class="sxs-lookup"><span data-stu-id="4892d-118">Step 2: Define hello action: block or allow</span></span>
<span data-ttu-id="4892d-119">**Bloquer :** les utilisateurs de hello spécifié pays seront refusées tooassets accès demandé à partir de ce chemin d’accès récursif.</span><span class="sxs-lookup"><span data-stu-id="4892d-119">**Block:** Users from hello specified countries will be denied access tooassets requested from that recursive path.</span></span> <span data-ttu-id="4892d-120">Si aucune autre option de filtrage par pays n'a été configurée pour cet emplacement, tous les autres utilisateurs sont autorisés à y accéder.</span><span class="sxs-lookup"><span data-stu-id="4892d-120">If no other country filtering options have been configured for that location, then all other users will be allowed access.</span></span>

<span data-ttu-id="4892d-121">**Autoriser :** seuls les utilisateurs de hello spécifié pays pourront tooassets accès demandé à partir de ce chemin d’accès récursif.</span><span class="sxs-lookup"><span data-stu-id="4892d-121">**Allow:** Only users from hello specified countries will be allowed access tooassets requested from that recursive path.</span></span>

## <a name="step-3-define-hello-countries"></a><span data-ttu-id="4892d-122">Étape 3 : Définir des pays hello</span><span class="sxs-lookup"><span data-stu-id="4892d-122">Step 3: Define hello countries</span></span>
<span data-ttu-id="4892d-123">Sélectionnez le pays hello que vous souhaitez tooblock ou autoriser pour le chemin d’accès hello.</span><span class="sxs-lookup"><span data-stu-id="4892d-123">Select hello countries that you want tooblock or allow for hello path.</span></span> 

<span data-ttu-id="4892d-124">Par exemple, règle hello de blocage /Photos/Strasbourg/filtrer les fichiers, y compris :</span><span class="sxs-lookup"><span data-stu-id="4892d-124">For example, hello rule of blocking /Photos/Strasbourg/ will filter files including:</span></span>

    http://<endpoint>.azureedge.net/Photos/Strasbourg/1000.jpg
    http://<endpoint>.azureedge.net/Photos/Strasbourg/Cathedral/1000.jpg


### <a name="country-codes"></a><span data-ttu-id="4892d-125">Codes de pays</span><span class="sxs-lookup"><span data-stu-id="4892d-125">Country codes</span></span>
<span data-ttu-id="4892d-126">Hello **filtrage géographique** fonctionnalité utilise des codes toodefine hello pays à partir de laquelle une demande sera autorisée ou bloquée pour un répertoire sécurisé.</span><span class="sxs-lookup"><span data-stu-id="4892d-126">hello **Geo-Filtering** feature uses country codes toodefine hello countries from which a request will be allowed or blocked for a secured directory.</span></span> <span data-ttu-id="4892d-127">Vous trouverez hello indicatifs de pays dans [indicatifs de pays Azure CDN](https://msdn.microsoft.com/library/mt761717.aspx).</span><span class="sxs-lookup"><span data-stu-id="4892d-127">You will find hello country codes in [Azure CDN  Country Codes](https://msdn.microsoft.com/library/mt761717.aspx).</span></span> 

## <span data-ttu-id="4892d-128"><a id="considerations"></a>Considérations</span><span class="sxs-lookup"><span data-stu-id="4892d-128"><a id="considerations"></a>Considerations</span></span>
* <span data-ttu-id="4892d-129">Cela peut prendre jusqu'à minutes too90 Verizon ou quelques minutes avec Akamai, pour effet de tootake configuration filtrage modifications tooyour pays.</span><span class="sxs-lookup"><span data-stu-id="4892d-129">It may take up too90 minutes for Verizon, or a couple minutes with Akamai, for changes tooyour country filtering configuration tootake effect.</span></span>
* <span data-ttu-id="4892d-130">Cette fonctionnalité ne prend pas en charge les caractères génériques (par exemple, « * »).</span><span class="sxs-lookup"><span data-stu-id="4892d-130">This feature does not support wildcard characters (for example, ‘*’).</span></span>
* <span data-ttu-id="4892d-131">configuration du filtrage de géo-réplication Hello associée au chemin d’accès relatif de hello seront appliquées de manière récursive toothat chemin.</span><span class="sxs-lookup"><span data-stu-id="4892d-131">hello geo-filtering configuration associated with hello relative path will be applied recursively toothat path.</span></span>
* <span data-ttu-id="4892d-132">Une seule règle peut être appliquée toohello même chemin d’accès relatif (vous ne pouvez créer plusieurs filtres de pays que toohello point même chemin d’accès relatif.</span><span class="sxs-lookup"><span data-stu-id="4892d-132">Only one rule can be applied toohello same relative path (you cannot create multiple country filters that point toohello same relative path.</span></span> <span data-ttu-id="4892d-133">Toutefois, un dossier peut avoir plusieurs filtres par pays.</span><span class="sxs-lookup"><span data-stu-id="4892d-133">However, a folder may have multiple country filters.</span></span> <span data-ttu-id="4892d-134">Il s’agit en raison de la nature récursive de toohello des filtres de pays.</span><span class="sxs-lookup"><span data-stu-id="4892d-134">This is due toohello recursive nature of country filters.</span></span> <span data-ttu-id="4892d-135">En d'autres termes, un filtre par pays différent peut être attribué à un sous-dossier d'un dossier déjà configuré.</span><span class="sxs-lookup"><span data-stu-id="4892d-135">In other words, a subfolder of a previously configured folder can be assigned a different country filter.</span></span>

