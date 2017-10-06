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
# <a name="restrict-azure-cdn-content-by-country"></a>Limiter l’accès à votre contenu CDN Azure par pays

## <a name="overview"></a>Vue d'ensemble
Lorsqu’un utilisateur demande votre contenu, par défaut, le contenu hello est pris en charge, quelle que soit l’endroit cette demande à partir d’utilisateur de hello. Dans certains cas, vous souhaiterez peut-être toorestrict accéder au contenu de tooyour par pays. Cette rubrique explique comment toouse hello **filtrage géographique** fonctionnalité dans l’ordre tooconfigure hello service tooallow ou bloquer l’accès par pays.

> [!IMPORTANT]
> les produits Verizon et Akamai Hello fournissent hello les mêmes fonctionnalités de filtrage de géo-réplication, mais ont une légère différence dans les codes de pays te ils prennent en charge. Consultez l’étape 3 pour un différences toohello de lien.


Pour plus d’informations sur les considérations qui s’appliquent tooconfiguring ce type de restriction, consultez hello [considérations](cdn-restrict-access-by-country.md#considerations) section à fin hello de rubrique de hello.  

![Filtrage par pays](./media/cdn-filtering/cdn-country-filtering-akamai.png)

## <a name="step-1-define-hello-directory-path"></a>Étape 1 : Définir le chemin d’accès du répertoire hello
Sélectionnez votre point de terminaison dans le portail de hello et hello filtrage géographique onglet toofind de navigation gauche hello vous trouverez cette fonctionnalité.

Lorsque vous configurez un filtre de pays, vous devez spécifier les utilisateurs toowhich hello chemin d’accès relatif toohello seront autorisés ou refusés l’accès. Vous pouvez appliquer le filtrage géographique pour tous vos fichiers avec « / » ou certains dossiers en spécifiant des chemins d'accès au répertoire "/pictures/". Vous pouvez également appliquer filtrage géographique de tooa fichier unique en spécifiant le fichier de hello et en laissant hello barre oblique « / Pictures/City.png ».

Exemple de filtre de chemin d'accès au répertoire :

    /                                 
    /Photos/
    /Photos/Strasbourg/
      /Photos/Strasbourg/city.png

## <a name="step-2-define-hello-action-block-or-allow"></a>Étape 2 : Définir l’action de hello : bloquer ou autoriser
**Bloquer :** les utilisateurs de hello spécifié pays seront refusées tooassets accès demandé à partir de ce chemin d’accès récursif. Si aucune autre option de filtrage par pays n'a été configurée pour cet emplacement, tous les autres utilisateurs sont autorisés à y accéder.

**Autoriser :** seuls les utilisateurs de hello spécifié pays pourront tooassets accès demandé à partir de ce chemin d’accès récursif.

## <a name="step-3-define-hello-countries"></a>Étape 3 : Définir des pays hello
Sélectionnez le pays hello que vous souhaitez tooblock ou autoriser pour le chemin d’accès hello. 

Par exemple, règle hello de blocage /Photos/Strasbourg/filtrer les fichiers, y compris :

    http://<endpoint>.azureedge.net/Photos/Strasbourg/1000.jpg
    http://<endpoint>.azureedge.net/Photos/Strasbourg/Cathedral/1000.jpg


### <a name="country-codes"></a>Codes de pays
Hello **filtrage géographique** fonctionnalité utilise des codes toodefine hello pays à partir de laquelle une demande sera autorisée ou bloquée pour un répertoire sécurisé. Vous trouverez hello indicatifs de pays dans [indicatifs de pays Azure CDN](https://msdn.microsoft.com/library/mt761717.aspx). 

## <a id="considerations"></a>Considérations
* Cela peut prendre jusqu'à minutes too90 Verizon ou quelques minutes avec Akamai, pour effet de tootake configuration filtrage modifications tooyour pays.
* Cette fonctionnalité ne prend pas en charge les caractères génériques (par exemple, « * »).
* configuration du filtrage de géo-réplication Hello associée au chemin d’accès relatif de hello seront appliquées de manière récursive toothat chemin.
* Une seule règle peut être appliquée toohello même chemin d’accès relatif (vous ne pouvez créer plusieurs filtres de pays que toohello point même chemin d’accès relatif. Toutefois, un dossier peut avoir plusieurs filtres par pays. Il s’agit en raison de la nature récursive de toohello des filtres de pays. En d'autres termes, un filtre par pays différent peut être attribué à un sous-dossier d'un dossier déjà configuré.

