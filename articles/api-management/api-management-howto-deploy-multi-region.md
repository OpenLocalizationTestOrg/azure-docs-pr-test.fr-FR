---
title: "aaaDeploy gestion des API Azure services toomultiple Azure régions | Documents Microsoft"
description: "Découvrez comment toodeploy une gestion des API Azure service instance toomultiple Azure régions."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 47389ad6-f865-4706-833f-846115e22e4d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 04a3e762261237d73a769320a21363f99f1d20cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-an-azure-api-management-service-instance-toomultiple-azure-regions"></a>Comment toodeploy une gestion des API Azure service instance toomultiple Azure régions
Gestion des API prend en charge le déploiement de plusieurs régions, ce qui permet des API éditeurs toodistribute un seul service de gestion des API sur n’importe quel nombre de régions Azure souhaités. Ceci permet de réduire la latence de la demande telle qu’elle est perçue par les utilisateurs distribués de l’API. La disponibilité du service est également améliorée si une région est mise hors connexion. 

Création d’un service de gestion des API au départ, il contient un seul [unité] [ unit] et se trouve dans une seule région Azure, qui est désignée comme hello région principale. Zones supplémentaires peuvent être ajoutées facilement via hello portail Azure. Un serveur de passerelle de gestion des API est déployé tooeach région et le trafic d’appel est routé toohello les passerelle le plus proche. Si une région est mis hors connexion, le trafic de hello est automatiquement redirigée toohello passerelle le plus proche suivant. 

> [!IMPORTANT]
> Déploiement de plusieurs régions est uniquement disponible dans hello  **[Premium] [ Premium]**  couche.
> 
> 

## <a name="add-region"></a>Déployer une région tooa nouvelle instance du service Gestion des API
> [!NOTE]
> Si vous n’avez pas encore créé une instance de service de gestion des API, consultez [de créer une instance de service de gestion des API] [ Create an API Management service instance] Bonjour [prise en main Azure API Management] [ Get started with Azure API Management] didacticiel.
> 
> 

Bonjour portail Azure, accédez toohello **mise à l’échelle et la tarification** page de votre instance de service de gestion des API. 

![Onglet Mettre à l’échelle][api-management-scale-service]

toodeploy tooa nouvelle zone, cliquez sur **+ ajouter région** à partir de la barre d’outils hello.

![Ajouter une région][api-management-add-region]

Sélectionnez l’emplacement de hello à partir de la liste déroulante de hello et définir nombre hello d’unités pour avec le curseur de hello.

![Spécifier les unités][api-management-select-location-units]

Cliquez sur **ajouter** tooplace votre sélection dans la table d’emplacements hello. 

Répétez ce processus jusqu'à ce que vous ayez tous les emplacements configurés, puis cliquez sur **enregistrer** hello barre d’outils toostart hello processus de déploiement.

## <a name="remove-region"></a>Suppression d’une instance de service Gestion des API dans un emplacement
Bonjour portail Azure, accédez toohello **mise à l’échelle et la tarification** page de votre instance de service de gestion des API. 

![Onglet Mettre à l’échelle][api-management-scale-service]

Pour hello emplacement auquel vous tooremove ouvrir le menu contextuel de hello à l’aide de hello **...**  bouton à hello droite de la table de hello. Sélectionnez hello **supprimer** option.

![Supprimer la région][api-management-remove-region]

Confirmer la suppression de hello et cliquez sur **enregistrer** modifications de hello tooapply.

[api-management-management-console]: ./media/api-management-howto-deploy-multi-region/api-management-management-console.png

[api-management-scale-service]: ./media/api-management-howto-deploy-multi-region/api-management-scale-service.png
[api-management-add-region]: ./media/api-management-howto-deploy-multi-region/api-management-add-region.png
[api-management-select-location-units]: ./media/api-management-howto-deploy-multi-region/api-management-select-location-units.png
[api-management-remove-region]: ./media/api-management-howto-deploy-multi-region/api-management-remove-region.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Get started with Azure API Management]: api-management-get-started.md

[Deploy an API Management service instance tooa new region]: #add-region
[Delete an API Management service instance from a region]: #remove-region

[unit]: http://azure.microsoft.com/pricing/details/api-management/
[Premium]: http://azure.microsoft.com/pricing/details/api-management/

