---
title: "Ressources associées et liées dans la Galerie de vignettes"
description: "Apprenez en quoi consistent les ressources associées et liées qui sont affichées dans la Galerie de vignettes du portail Azure en version préliminaire."
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
ms.openlocfilehash: efa7bce26c2c4c153b083e0e34d689a11d27dd16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="related-and-linked-resources-in-the-tile-gallery"></a>Ressources associées et liées dans la Galerie de vignettes
La Galerie de vignettes vous permet de rechercher des vignettes pour une ressource spécifique et de les faire glisser jusqu’à votre panneau actif. À l’aide de la Galerie de vignettes, vous pouvez créer des vues de gestion portant sur les ressources. Pour n’importe quelle ressource donnée, les ressources associées englobent toutes les ressources de son groupe de ressources, ainsi que toutes les ressources qui établissent des liens à destination ou en provenance de la ressource.

## <a name="linked-resources-in-resource-manager"></a>Ressources liées dans Resource Manager
La liaison est une fonctionnalité de Resource Manager.  Elle vous permet de déclarer des relations entre les ressources, même si ces dernières n’appartiennent pas au même groupe de ressources. La liaison n’a aucun impact sur le moment de l’exécution de vos ressources, sur la facturation, ni sur l’accès en fonction du rôle.  Il s’agit simplement d’un mécanisme qui vous permet de représenter les relations afin que les outils comme la Galerie de vignettes puissent offrir une expérience de gestion enrichie.  Vos outils peuvent inspecter les liens à l’aide de l’API de liens et fournir également des expériences de gestion des relations personnalisées. 

## <a name="how-do-i-link-my-resources"></a>Comment lier mes ressources ?
Lorsque vous créez des ressources par le biais du portail ou en déployant un modèle par l’intermédiaire d’Azure PowerShell ou de l’interface de ligne de commande Azure, des liens sont automatiquement créés pour certaines ressources dépendantes. Vous pouvez également lier des ressources par programme à l’aide de [l’API REST Ressources liées](/rest/api/resources/resourcelinks).

## <a name="next-steps"></a>Étapes suivantes
* Pour plus d’informations sur l’écriture de modèles Resource Manager, consultez la page [Création de modèles](../azure-resource-manager/resource-group-authoring-templates.md).
* Pour plus d’informations sur l’utilisation des groupes de ressources par le biais du portail, consultez la page [Utiliser le Portail Azure pour gérer vos ressources Azure](../azure-resource-manager/resource-group-portal.md).

