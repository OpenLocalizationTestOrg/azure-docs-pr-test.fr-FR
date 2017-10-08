---
title: "importer des aaaRestrictions et problèmes connus dans les API de gestion des API Azure | Documents Microsoft"
description: "Détails des problèmes connus et des restrictions à l’importation dans la gestion des API Azure à l’aide des formats d’API Open, WSDL ou WADL hello."
services: api-management
documentationcenter: 
author: mattfarm
manager: vlvinogr
editor: 
ms.assetid: 7a5a63f0-3e72-49d3-a28c-1bb23ab495e2
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: apipm
ms.openlocfilehash: 0bed5ace47de6ccbfbecba25ea6b69c5329de089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="api-import-restrictions-and-known-issues"></a>Restrictions et problèmes connus relatifs à l’importation d’API
## <a name="about-this-list"></a>À propos de cette liste
Alors que tout est mis en œuvre tooensure que l’importation de votre API dans la gestion des API Azure est plus transparente et exempt de problèmes que possible, nous parfois imposer des restrictions ou identifier les problèmes qui devront toobe rectifié avant de pouvoir importer correctement. Cet article décrit ces options, organisés par le format d’importation hello Hello API.

## <a name="open-api"></a>Open API/Swagger
En règle générale, si vous recevez des erreurs d’importation de votre document de l’API Open, vérifiez que vous avez validé, soit à l’aide du Concepteur de hello dans hello nouveau portail Azure (conception - Front End - ouvrir API spécification de l’éditeur), ou avec un 3e partie comme outil <a href="http://www.swagger.io"> Éditeur de swagger</a>.

* **Nom d’hôte** : nous exigeons un attribut de nom d’hôte.
* **Chemin d’accès de base** : nous exigeons un attribut de chemin d’accès de base.
* **Schémas** : nous exigeons un tableau de schéma. 

## <a name="wsdl"></a>WSDL
Fichiers WSDL sont utilisé toogenerate SOAP pass-through API ou servent hello du serveur principal d’une API SOAP pour REST.

* **WSDL:Import** : nous ne prenons actuellement pas en charge les API utilisant cet attribut. Clients doivent fusionner les éléments hello importé dans un document.
* Les **messages en plusieurs parties** ne sont actuellement pas pris en charge.
* **WCF wsHttpBinding** : les services SOAP créés avec Windows Communication Foundation doivent utiliser basicHttpBinding. wsHttpBinding n’est pas pris en charge.
* **MTOM** : les services utilisant MTOM <em>peuvent</em> fonctionner. Aucune prise en charge officielle n’est disponible pour l’instant.
* **La récursivité** types qui sont définis de manière récursive (par exemple, consultez le tableau tooan eux-mêmes) ne sont pas pris en charge.

## <a name="wadl"></a>WADL
Il n’existe actuellement aucun problème connu relatif à l’importation WADL.


[api-management-management-console]: ./media/api-management-howto-add-operations/api-management-management-console.png
[api-management-operations]: ./media/api-management-howto-add-operations/api-management-operations.png
[api-management-add-operation]: ./media/api-management-howto-add-operations/api-management-add-operation.png
[api-management-http-method]: ./media/api-management-howto-add-operations/api-management-http-method.png
[api-management-url-template]: ./media/api-management-howto-add-operations/api-management-url-template.png
[api-management-url-template-rewrite]: ./media/api-management-howto-add-operations/api-management-url-template-rewrite.png
[api-management-description]: ./media/api-management-howto-add-operations/api-management-description.png
[api-management-caching-tab]: ./media/api-management-howto-add-operations/api-management-caching-tab.png
[api-management-request-parameters]: ./media/api-management-howto-add-operations/api-management-request-parameters.png
[api-management-request-body]: ./media/api-management-howto-add-operations/api-management-request-body.png
[api-management-response-code]: ./media/api-management-howto-add-operations/api-management-response-code.png
[api-management-response-body-content-type]: ./media/api-management-howto-add-operations/api-management-response-body-content-type.png
[api-management-response-body]: ./media/api-management-howto-add-operations/api-management-response-body.png


[api-management-contoso-api]: ./media/api-management-howto-add-operations/api-management-contoso-api.png

[api-management-add-new-api]: ./media/api-management-howto-add-operations/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-add-operations/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-add-operations/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-add-operations/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-add-operations/api-management-echo-operations.png

[Add an operation]: #add-operation
[Operation caching]: #operation-caching
[Request parameters]: #request-parameters
[Request body]: #request-body
[Responses]: #responses
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocache operation results in Azure API Management]: api-management-howto-cache.md
