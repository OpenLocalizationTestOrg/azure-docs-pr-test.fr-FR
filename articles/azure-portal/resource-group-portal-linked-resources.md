---
title: "aaaRelated et les ressources liées Bonjour vignette de la galerie"
description: "En savoir plus sur les ressources associées et liés sont affichent dans la galerie de vignette hello du portail Azure en version préliminaire de hello."
services: azure-portal
documentationcenter: 
author: adamabdelhamed
manager: wpickett
editor: 
ms.assetid: dba96d29-f518-49c8-bfd2-f14cecb44cbf
ms.service: azure-portal
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2015
ms.author: adamab
ms.openlocfilehash: c8f99be8e23dc9641ec3cd3169604b33a4b049f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="related-and-linked-resources-in-hello-tile-gallery"></a>Ressources connexes et liés dans la galerie de vignette hello
Galerie de vignette Hello vous permet de vignettes toofind pour une ressource particulière et faites-les glisser vers votre panneau actuel. À l’aide de la galerie de vignette hello, vous pouvez créer des vues de gestion qui s’étendent sur des ressources. Pour n’importe quelle ressource spécifiée, hello liée ressources incluent toutes les ressources de hello dans son groupe de ressources et toutes les ressources qui sont liées tooor à partir de la ressource de hello.

## <a name="linked-resources-in-resource-manager"></a>Ressources liées dans Resource Manager
La liaison est une fonctionnalité du Gestionnaire de ressources de hello.  Il vous permet de toodeclare les relations entre les ressources même si elles ne trouvent pas dans hello même groupe de ressources. Liaison n’a aucun impact sur le runtime hello de vos ressources, aucun impact sur la facturation et aucun impact sur l’accès en fonction du rôle.  Il est simplement un mécanisme que vous pouvez utiliser les relations toorepresent afin que les outils tels que la galerie de vignette hello peut fournir une gestion riche expérience.  Vos outils peuvent inspecter les liens de hello à l’aide de liens de hello API et fournissent également des expériences de gestion des relations personnalisées. 

## <a name="how-do-i-link-my-resources"></a>Comment lier mes ressources ?
Lorsque vous créez des ressources hello portal ou en déployant un modèle via Azure PowerShell ou CLI d’Azure, des liens sont créés automatiquement pour certaines des ressources dépendantes. Vous pouvez également programmer lier des ressources à l’aide de hello [lié API REST de ressources](/rest/api/resources/resourcelinks).

## <a name="next-steps"></a>Étapes suivantes
* Si vous avez besoin d’une présentation toowriting Gestionnaire de ressources des modèles, consultez [création de modèles](../azure-resource-manager/resource-group-authoring-templates.md).
* toounderstand en savoir plus sur l’utilisation des groupes de ressources via le portail de hello, consultez [Using hello toomanage portail Azure vos ressources Azure](../azure-resource-manager/resource-group-portal.md).

