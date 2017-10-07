---
title: aaaHow toocreate API de gestion des API Azure
description: "Découvrez comment toocreate et configurer les API de gestion des API Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 14c20da4-f29f-4b28-bec7-3d4c50b734da
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 48ed8d93947253aa1e67ad995927ed6101cac072
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-apis-in-azure-api-management"></a>Comment toocreate API de gestion des API Azure
Une API du service Gestion des API représente un ensemble d'opérations qui peuvent être appelées par des applications clientes. Nouvelles API est créés dans le portail de publication hello et puis hello souhaité opérations sont ajoutées. Une fois ajoutées, les opérations hello hello API est ajouté tooa produit et peut être publié. Une fois qu’une API est publiée, il peut être souscrit tooand utilisée par les développeurs.

Ce guide montre la première étape de hello dans les processus hello : comment toocreate et configurer une nouvelle API de gestion des API. Pour plus d’informations sur l’ajout des opérations et la publication d’un produit, consultez [comment tooadd opérations tooan API] [ How tooadd operations tooan API] et [comment toocreate et publier un produit] [ How toocreate and publish a product].

## <a name="create-new-api"></a>Création d’une API
API est créés et configurés dans le portail de publication hello. tooaccess hello cliquez portail, du serveur de publication **portail de publication** Bonjour portail Azure pour votre service de gestion des API.

![Portail des éditeurs][api-management-management-console]

> Si vous n’avez pas encore créé une instance de service de gestion des API, consultez [de créer une instance de service de gestion des API] [ Create an API Management service instance] Bonjour [prise en main Azure API Management] [ Get started with Azure API Management] didacticiel.
> 
> 

Cliquez sur **API** de hello **gestion des API** menu sur hello gauche, puis cliquez sur **ajouter API**.

![Create API][api-management-create-api]

Hello d’utilisation **ajouter la nouvelle API** fenêtre tooconfigure hello nouvelle API.

![Ajouter une nouvelle API][api-management-add-new-api]

Hello suivant les champs est utilisés tooconfigure hello nouvelle API.

* **Nom de l’API Web** fournit un nom unique et descriptif pour hello API. Il est affiché dans les portails de développeur et éditeur hello.
* **URL du service Web** références hello service HTTP hello API de mise en œuvre. Gestion des API transfère les demandes de toothis adresse.
* **Suffixe d’URL de l’API Web** est l’URL de base toohello ajouté hello API de service de gestion. URL de base Hello est courant pour toutes les API hébergées par une instance de service de gestion des API. Gestion des API distingue les API par leur suffixe et par conséquent le suffixe de hello doit être unique pour toutes les API pour un serveur de publication donné.
* **Schéma de l’URL de l’API Web** détermine les protocoles qui peuvent être utilisés tooaccess hello API. Le protocole HTTPS est spécifié par défaut.
* toooptionally ajouter ce produit tooa de nouvelles API, cliquez sur hello **produits (facultatifs)** liste déroulante et choisissez un produit. Cette étape peut être répété à plusieurs reprises tooadd hello API toomultiple produits.

Une fois hello souhaité de valeurs sont configurées, cliquez sur **enregistrer**. Après la création de la nouvelle API de hello, hello page Résumé pour l’API de hello s’affiche dans le portail de publication hello.

![Résumé des API][api-management-api-summary]

## <a name="configure-api-settings"></a>Configuration des paramètres de l’API
Vous pouvez utiliser hello **paramètres** onglet tooverify et modifier la configuration de hello d’API. **Nom de l’API Web**, **URL du service Web**, et **suffixe d’URL d’API Web** sont initialement définies lors de l’API de hello est créé et peut être modifié. **Description** fournit une description facultative, et **le modèle d’URL d’API Web** détermine les protocoles qui peuvent être utilisés tooaccess hello API.

![API settings][api-management-api-settings]

authentification de la passerelle tooconfigure hello principal de service application hello API, sélectionnez hello **sécurité** hello d’onglet **avec les informations d’identification** déroulante peut être utilisé tooconfigure **HTTP base** ou **les certificats clients** l’authentification. l’authentification de base toouse HTTP, il suffit d’entrer les informations d’identification de hello souhaité. Pour plus d’informations sur l’utilisation de l’authentification du certificat client, consultez [comment toosecure services de back-end à l’aide du client de certificat d’authentification dans la gestion des API Azure][How toosecure back-end services using client certificate authentication in Azure API Management].

Hello **sécurité** onglet peut également être utilisé tooconfigure **autorisation de l’utilisateur** à l’aide d’OAuth 2.0. Pour plus d’informations, consultez [comment tooauthorize développeur comptes à l’aide OAuth 2.0 dans Azure API Management][How tooauthorize developer accounts using OAuth 2.0 in Azure API Management].

![Basic authentication settings][api-management-api-settings-credentials]

Cliquez sur **enregistrer** toosave toutes les modifications que vous apportez toohello paramètres de l’API.

## <a name="next-steps"></a>Étapes suivantes
Une fois qu’une API est créée et configurés les paramètres hello, hello suivants étapes tooadd hello operations toohello API, ajouter hello API tooa produit et publiez-le afin qu’il soit disponible pour les développeurs. Pour plus d’informations, consultez hello suivant des articles.

* [Comment tooadd opérations tooan API][How tooadd operations tooan API]
* [Comment toocreate et publier un produit][How toocreate and publish a product]

[api-management-create-api]: ./media/api-management-howto-create-apis/api-management-create-api.png
[api-management-management-console]: ./media/api-management-howto-create-apis/api-management-management-console.png
[api-management-add-new-api]: ./media/api-management-howto-create-apis/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-create-apis/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-create-apis/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-create-apis/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-create-apis/api-management-echo-operations.png

[What is an API?]: #what-is-api
[Create a new API]: #create-new-api
[Configure API settings]: #configure-api-settings
[Configure API operations]: #configure-api-operations
[Next steps]: #next-steps

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[How toosecure back-end services using client certificate authentication in Azure API Management]: api-management-howto-mutual-certificates.md
[How tooauthorize developer accounts using OAuth 2.0 in Azure API Management]: api-management-howto-oauth2.md
