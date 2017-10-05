---
title: "Création d'API dans Gestion des API Azure"
description: "Apprenez à créer et à configurer des API dans Gestion des API Azure."
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
ms.openlocfilehash: ab08256fbc3caca05bf23a12016ad2acf4fc7412
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-apis-in-azure-api-management"></a>Création d'API dans Gestion des API Azure
Une API du service Gestion des API représente un ensemble d'opérations qui peuvent être appelées par des applications clientes. Les nouvelles API sont créées dans le portail des éditeurs, puis les opérations souhaitées sont ajoutées. Une fois les opérations ajoutées, l'API est ajoutée à un produit et peut être publiée. Une fois l'API publiée, les développeurs peuvent s'y abonner et l'utiliser.

Ce guide présente la première étape du processus : comment créer et configurer une nouvelle API dans Gestion des API. Pour plus d’informations sur l’ajout d’opérations et la publication d’un produit, consultez les rubriques [Ajout d’opérations à une API][How to add operations to an API] et [Création et publication d’un produit][How to create and publish a product].

## <a name="create-new-api"> </a>Création d’une API
Les API sont créées et configurées dans le portail des éditeurs. Pour accéder au portail des éditeurs, cliquez sur **Portail des éditeurs** dans le portail Azure de votre service Gestion des API.

![Portail des éditeurs][api-management-management-console]

> Si vous n’avez pas encore créé une instance de service Gestion des API, consultez la page de [création d’une instance de service Gestion des API][Create an API Management service instance] dans le didacticiel de [prise en main de Gestion des API Azure][Get started with Azure API Management].
> 
> 

Cliquez sur **API** dans le menu **Gestion des API** à gauche, puis sur **Ajouter des API**.

![Create API][api-management-create-api]

Utilisez la fenêtre **Ajouter une nouvelle API** pour configurer la nouvelle API.

![Ajouter une nouvelle API][api-management-add-new-api]

Les champs suivants permettent de configurer la nouvelle API.

* **Titre d'API web** fournit un nom descriptif unique pour l'API. Il s’affiche dans les portails des développeurs et de publication.
* **URL du service web** indique le service HTTP implémentant l'API. La gestion des API transmet les demandes à cette adresse.
* Le **suffixe de l’URL d’API web** est ajouté à l’URL de base du service Gestion des API. L'URL de base est commune à toutes les API hébergées par une instance de service Gestion des API. Gestion des API distingue les API selon leur suffixe. Celui-ci doit donc être unique pour chaque API d'un éditeur donné.
* **schéma d’URL d’API web** détermine quels sont les protocoles qui peuvent être utilisés pour accéder à l’API. Le protocole HTTPS est spécifié par défaut.
* Pour ajouter éventuellement cette nouvelle API à un produit, cliquez sur la liste déroulante **Produits (facultatif)** et choisissez un produit. Cette étape peut être répétée plusieurs fois pour ajouter l'API à plusieurs produits.

Une fois les valeurs de votre choix configurées, cliquez sur **Enregistrer**. Une fois l'API créée, la page de résumé de l'API s'affiche dans le portail de publication.

![API summary][api-management-api-summary]

## <a name="configure-api-settings"> </a>Configuration des paramètres de l’API
L’onglet **Paramètres** permet de vérifier et de modifier la configuration d’une API. Les options **Nom d’API web**, **URL du service web** et **Suffixe d’URL de l’API web** sont définis initialement lors de la création de l’API. Vous pouvez les modifier ici. **Description** contient une description facultative et **Schéma d’URL d’API web** détermine quels sont les protocoles qui peuvent être utilisés pour accéder à l’API.

![API settings][api-management-api-settings]

Pour configurer l'authentification de la passerelle pour le service principal avec mise en œuvre de l'API, sélectionnez l’onglet **Sécurité** . La liste déroulante **Avec informations d’identification** peut servir à configurer l’authentification **HTTP de base** ou par **Certificats client**. Pour utiliser l'authentification HTTP de base, entrez simplement les informations d'identification de votre choix. Pour plus d’informations sur l’utilisation de l’authentification avec certificats client, consultez la page [Comment sécuriser les services principaux à l’aide d’une authentification de certificat client dans Gestion des API Azure][How to secure back-end services using client certificate authentication in Azure API Management].

L’onglet **Sécurité** peut également être utilisé pour configurer **Autorisation utilisateur** avec OAuth 2.0. Pour plus d’informations, consultez la page [Comment autoriser des comptes de développeurs à l’aide d’OAuth 2.0 dans Gestion des API Azure][How to authorize developer accounts using OAuth 2.0 in Azure API Management].

![Basic authentication settings][api-management-api-settings-credentials]

Cliquez sur **Enregistrer** pour enregistrer les modifications apportées aux paramètres de l'API.

## <a name="next-steps"> </a>Étapes suivantes
Une fois l'API créée et les paramètres configurés, l'étape suivante consiste à ajouter les opérations à l'API, à ajouter l'API à un produit et à la publier pour la mettre à disposition des développeurs. Pour plus d'informations, consultez les articles suivants.

* [Ajout d’opérations à une API][How to add operations to an API]
* [Création et publication d’un produit][How to create and publish a product]

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

[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[How to secure back-end services using client certificate authentication in Azure API Management]: api-management-howto-mutual-certificates.md
[How to authorize developer accounts using OAuth 2.0 in Azure API Management]: api-management-howto-oauth2.md
