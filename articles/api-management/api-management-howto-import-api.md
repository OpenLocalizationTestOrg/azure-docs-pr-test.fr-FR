---
title: aaaImport une API dans la gestion des API Azure | Documents Microsoft
description: "Découvrez comment tooimport une API et ses opérations dans la gestion des API Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 40398b0a-ac2c-43f0-89e1-07e4abbf502f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 20fbbb53243aecc24d72833ec0904ae8fab97863
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimport-hello-definition-of-an-api-with-operations-in-azure-api-management"></a>Comment tooimport hello définition d’une API avec les opérations de gestion des API Azure
Gestion des API, nouvelles API peut être créées et opérations hello ajoutées manuellement ou hello API peut être importés, ainsi que les opérations de hello en une seule étape.

API et leurs opérations peuvent être importées à l’aide de hello suivant formats.

* WADL
* Swagger

Ce guide vous présente comment créer une API et importer des opérations en une seule fois. Pour plus d’informations sur la création manuelle d’une API et l’ajout des opérations, consultez [comment toocreate API] [ How toocreate APIs] et [comment tooadd opérations tooan API] [ How tooadd operations tooan API].

## <a name="import-api"></a>Importation d’une API
API est créés et configurés dans le portail de publication hello. tooaccess hello cliquez portail, du serveur de publication **portail de publication** Bonjour portail Azure pour votre service de gestion des API. Si vous n’avez pas encore créé une instance de service de gestion des API, consultez [de créer une instance de service de gestion des API] [ Create an API Management service instance] Bonjour [prise en main Azure API Management] [ Get started with Azure API Management] didacticiel.

![Portail des éditeurs][api-management-management-console]

Cliquez sur **API** de hello **gestion des API** menu sur hello gauche, puis cliquez sur **importer API**.

![Importer l'API][api-management-import-apis]

Hello **API d’importation** fenêtre comporte trois onglets correspondant de spécification de hello API tooprovide toohello trois façons.

* **À partir du Presse-papiers** vous permet de spécifier de hello API toopaste dans la zone de texte hello.
* **À partir du fichier** vous permet de toobrowse tooand hello Sélectionnez fichier qui contient la spécification de hello API.
* **À partir de l’URL** vous permet de spécification de toohello toosupply hello URL pour hello API.

![Import API format][api-management-import-api-clipboard]

Après avoir entré la spécification de l’API de hello, utilisez cases d’option hello sur format de spécification hello hello tooindicate droite. Hello suivant les formats est pris en charge.

* WADL
* Swagger

Ensuite, entrez un **suffixe d’URL d’API web**. Il s’agit d’URL de base toohello ajouté pour votre service de gestion des API. URL de base Hello est courant pour toutes les API hébergées sur chaque instance d’un service de gestion des API. Gestion des API distingue les API par leur suffixe et par conséquent le suffixe de hello doit être unique pour toutes les API dans une instance spécifique du service de gestion de l’API.

Une fois que toutes les valeurs sont entrées, cliquez sur **enregistrer** toocreate hello API et hello associées des opérations. 

> [!NOTE]
> Pour voir un didacticiel sur l’importation d’une API de calculatrice de base au format Swagger, consultez [Gestion de votre première API dans Gestion des API Azure](api-management-get-started.md).
> 
> 

## <a name="export-api"></a> Exportation d’une API
En outre tooimporting nouvelles API, vous pouvez exporter des définitions de hello de votre API à partir du portail de publication hello. toodo, cliquez sur **exporter les API** de hello **onglet Résumé** de votre **API**.

![Export API][api-management-export-api]

Les API peuvent être exportées avec WADL ou Swagger. Sélectionnez le format désiré de hello, cliquez sur **enregistrer**et choisir un emplacement de hello dans laquelle le fichier toosave hello.

![Export API format][api-management-export-api-format]

## <a name="next-steps"></a>Étapes suivantes
Une fois qu’une API est créée et les opérations hello importées, vous pouvez examiner et configurer des paramètres supplémentaires, ajouter hello API tooa produit et publiez-le afin qu’il soit disponible pour les développeurs. Pour plus d’informations, consultez hello guides de.

* [Comment les paramètres tooconfigure API][How tooconfigure API settings]
* [Comment toocreate et publier un produit][How toocreate and publish a product]

[api-management-management-console]: ./media/api-management-howto-import-api/api-management-management-console.png
[api-management-import-apis]: ./media/api-management-howto-import-api/api-management-api-import-apis.png
[api-management-import-api-clipboard]: ./media/api-management-howto-import-api/api-management-import-api-wizard.png
[api-management-export-api]: ./media/api-management-howto-import-api/api-management-export-api.png
[api-management-export-api-format]: ./media/api-management-howto-import-api/api-management-export-api-format.png

[Import an API]: #import-api
[Export an API]: #export-api
[Configure API settings]: #configure-api-settings
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocreate APIs]: api-management-howto-create-apis.md
[How tooconfigure API settings]: api-management-howto-create-apis.md#configure-api-settings
