---
title: "ressources de données aaaManage dans Azure Data Catalog | Documents Microsoft"
description: "article de Hello met en évidence comment toocontrol visibilité et la propriété des ressources de données enregistrée dans Azure Data Catalog."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 623f5ed4-8da7-48f5-943a-448d0b7cba69
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 48a634b92d7da19c32c9e551f295eec257f54f1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-data-assets-in-azure-data-catalog"></a>Gérer les ressources de données dans Azure Data Catalog
## <a name="introduction"></a>Introduction
Azure Data Catalog est conçu pour la découverte de la source de données, afin que vous pouvez facilement découvrir et comprendre les sources de données hello vous devez tooperform analyse et prenez des décisions. Ces fonctionnalités de découverte font impressionnants hello lorsque d’autres utilisateurs peuvent rechercher et comprendre hello plus large gamme de sources de données disponibles. Ces éléments à l’esprit, a un comportement par défaut de hello du catalogue de données pour toutes les données des sources toobe visible tooand détectable par tous les utilisateurs du catalogue.

Catalogue de données ne vous donne pas accès aux données toohello lui-même. Accès aux données est contrôlé par le propriétaire de hello hello de source de données. Avec le catalogue de données, vous pouvez découvrir les sources de données et afficher les métadonnées hello sources toohello connexes qui sont inscrits dans le catalogue de hello.

Il peut exister des situations où des sources de données doivent être uniquement visible toospecific utilisateurs ou toomembers de groupes spécifiques. Dans de tels scénarios, les utilisateurs peuvent prendre possession de ressources de données enregistré dans le catalogue de hello et ensuite contrôler la visibilité hello de biens hello qu’ils possèdent.

> [!NOTE]
> fonctionnalités de Hello décrites dans cet article sont disponible uniquement dans hello Édition Standard d’Azure Data Catalog. Hello édition gratuite ne fournit pas les fonctionnalités pour la propriété et la restriction de la visibilité de la ressource de données.
>
>

## <a name="manage-ownership-of-data-assets"></a>Gérer la propriété des ressources de données
Par défaut, les ressources de données qui sont inscrites dans le catalogue de données n’ont pas de propriétaire. Tout utilisateur disposant de catalogue de hello tooaccess autorisation peut détecter et annoter ces ressources. Les utilisateurs peuvent s’approprier les ressources de données sans propriétaire, puis limiter visibilité hello de biens hello qu’ils possèdent.

Quand une ressource de données dans le catalogue de données appartient, seuls les utilisateurs qui sont autorisés par les propriétaires de hello peuvent découvrir les ressources hello et afficher ses métadonnées, et seuls les propriétaires de hello peuvent supprimer les actifs hello hello catalogue.

> [!NOTE]
> La propriété dans le catalogue de données affecte uniquement les métadonnées hello sont stockée dans le catalogue de hello. La propriété ne confère pas d’autorisations sur la source de données sous-jacente hello.
>
>

### <a name="take-ownership"></a>Prendre possession
Les utilisateurs peuvent prendre possession de ressources de données en sélectionnant hello **Take Ownership** option dans le portail du catalogue de données hello. Aucune autorisation spéciale n’est requis tootake approprier une ressource de données sans propriétaire. Tout utilisateur peut prendre possession d’une ressource de données sans propriétaire.

### <a name="add-owners-and-co-owners"></a>Ajouter des propriétaires et des copropriétaires
Si une ressource de données est déjà la propriété d’un utilisateur, les autres utilisateurs ne peuvent pas en prendre possession. Toutefois, ils peuvent être ajoutés en tant que copropriétaires par le propriétaire existant. N’importe quel propriétaire peut ajouter des utilisateurs ou groupes de sécurité supplémentaires en tant que copropriétaires.

> [!NOTE]
> Il est une meilleure toohave de pratique au moins deux personnes en tant que propriétaires d’un propriétaire de ressource de données.
>
>

### <a name="remove-owners"></a>Supprimer des propriétaires
De la même manière que n’importe quel propriétaire de ressources peut ajouter des copropriétaires, n’importe quel propriétaire de ressource a la possibilité de supprimer des copropriétaires.

Un propriétaire de la ressource qui supprime lui-même en tant que propriétaire ne peut plus gérer asset de hello. Si le propriétaire de la ressource hello supprime lui-même en tant que propriétaire et qu’aucun autres copropriétaires, asset de hello revient tooan sans propriétaire d’état.

## <a name="control-visibility"></a>Contrôler la visibilité
Propriétaires de la ressource de données peuvent contrôler la visibilité de hello hello de ressources de données qu’ils possèdent. visibilité toorestrict comme valeur par défaut de hello, où tous les Data Catalog, les utilisateurs peuvent détecter et vue hello ressource de données, le propriétaire de ressource hello peut désactiver hello visibilité paramètre **tout le monde** trop**propriétaires & ces utilisateurs** dans les propriétés pour un composant de hello hello. Les propriétaires peuvent ensuite ajouter des utilisateurs et groupes de sécurité spécifiques.

> [!NOTE]
> Dès que possible, les autorisations de la propriété et la visibilité d’actif doivent être attribuées toosecurity groupes et non aux utilisateurs de tooindividual.
>
>

## <a name="catalog-administrators"></a>Administrateurs de Data Catalog
Les administrateurs de catalogue de données sont implicitement copropriétaires de tous les éléments multimédias dans le catalogue de hello. Propriétaires des ressources ne peut pas supprimer la visibilité des administrateurs et les administrateurs peuvent gérer la propriété et la visibilité de toutes les ressources de données dans le catalogue de hello.

## <a name="summary"></a>Résumé
Hello catalogue de données marketing participatif modèle toometadata et les données de découverte permet à tous les toocontribute les utilisateurs de catalogue et actifs découvrir. Hello Édition Standard de catalogue de données est conçu pour la gestion et la propriété visibilité de hello toolimit et l’utilisation des ressources de données spécifique.
