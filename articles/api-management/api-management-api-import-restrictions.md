---
title: "Restrictions et problèmes connus relatifs à l’importation d’API dans la gestion des API Azure | Microsoft Docs"
description: "Détails des problèmes connus et des restrictions relatifs à l’importation dans la gestion des API Azure à l’aide des formats Open API, WSDL ou WADL."
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
ms.openlocfilehash: ac799d66b5038c207413086b0fa71239ff2a332f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="api-import-restrictions-and-known-issues"></a><span data-ttu-id="3ca9a-103">Restrictions et problèmes connus relatifs à l’importation d’API</span><span class="sxs-lookup"><span data-stu-id="3ca9a-103">API import restrictions and known issues</span></span>
## <a name="about-this-list"></a><span data-ttu-id="3ca9a-104">À propos de cette liste</span><span class="sxs-lookup"><span data-stu-id="3ca9a-104">About this list</span></span>
<span data-ttu-id="3ca9a-105">Bien que tout soit mis en œuvre pour garantir que l’importation de votre API dans la gestion des API Azure soit aussi transparente et exempte de problèmes que possible, nous imposons parfois des restrictions ou identifions des problèmes qui devront être corrigés pour vous permettre d’importer correctement.</span><span class="sxs-lookup"><span data-stu-id="3ca9a-105">While every effort is made to ensure that importing your API into Azure API Management is as seamless and problem-free as possible, we do occasionally impose restrictions or identify issues that will need to be rectified before you can successfully import.</span></span> <span data-ttu-id="3ca9a-106">Cet article documente ces restrictions et problèmes connus, organisés par format d’importation de l’API.</span><span class="sxs-lookup"><span data-stu-id="3ca9a-106">This article documents these, organised by the import format of the API.</span></span>

## <span data-ttu-id="3ca9a-107"><a name="open-api"> </a>Open API/Swagger</span><span class="sxs-lookup"><span data-stu-id="3ca9a-107"><a name="open-api"> </a>Open API/Swagger</span></span>
<span data-ttu-id="3ca9a-108">En général, si vous recevez des erreurs lors de l’importation de votre document Open API, vérifiez que vous l’avez validé à l’aide du concepteur dans le nouveau portail Azure (Conception - Principal - Open API Specification Editor) ou à l’aide d’un outil tiers tel que <a href="http://www.swagger.io">Swagger Editor</a>.</span><span class="sxs-lookup"><span data-stu-id="3ca9a-108">In general, if you are receiving errors importing your Open API document, please ensure you have validated it - either using the designer in the new Azure Portal (Design - Front End - Open API Specification Editor), or with a 3rd party tool such as <a href="http://www.swagger.io">Swagger Editor</a>.</span></span>

* <span data-ttu-id="3ca9a-109">**Nom d’hôte** : nous exigeons un attribut de nom d’hôte.</span><span class="sxs-lookup"><span data-stu-id="3ca9a-109">**Host Name** we require a host name attribute.</span></span>
* <span data-ttu-id="3ca9a-110">**Chemin d’accès de base** : nous exigeons un attribut de chemin d’accès de base.</span><span class="sxs-lookup"><span data-stu-id="3ca9a-110">**Base Path** we require a base path attribute.</span></span>
* <span data-ttu-id="3ca9a-111">**Schémas** : nous exigeons un tableau de schéma.</span><span class="sxs-lookup"><span data-stu-id="3ca9a-111">**Schemes** we require a scheme array.</span></span> 

## <span data-ttu-id="3ca9a-112"><a name="wsdl"> </a>WSDL</span><span class="sxs-lookup"><span data-stu-id="3ca9a-112"><a name="wsdl"> </a>WSDL</span></span>
<span data-ttu-id="3ca9a-113">Les fichiers WSDL servent à générer des API Pass-through SOAP ou constituent le back-end d’une API SOAP à REST.</span><span class="sxs-lookup"><span data-stu-id="3ca9a-113">WSDL files are used to generate SOAP Pass-through APIs, or serve as the backend of a SOAP-to-REST API.</span></span>

* <span data-ttu-id="3ca9a-114">**WSDL:Import** : nous ne prenons actuellement pas en charge les API utilisant cet attribut.</span><span class="sxs-lookup"><span data-stu-id="3ca9a-114">**WSDL:Import** we do not currently support APIs using this attribute.</span></span> <span data-ttu-id="3ca9a-115">Les clients doivent fusionner les éléments importés dans un seul document.</span><span class="sxs-lookup"><span data-stu-id="3ca9a-115">Customers should merge the imported elements into one document.</span></span>
* <span data-ttu-id="3ca9a-116">Les **messages en plusieurs parties** ne sont actuellement pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="3ca9a-116">**Messages with multiple parts** are currently not supported.</span></span>
* <span data-ttu-id="3ca9a-117">**WCF wsHttpBinding** : les services SOAP créés avec Windows Communication Foundation doivent utiliser basicHttpBinding. wsHttpBinding n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="3ca9a-117">**WCF wsHttpBinding** SOAP services created with Windows Communication Foundation should use basicHttpBinding - wsHttpBinding is not supported.</span></span>
* <span data-ttu-id="3ca9a-118">**MTOM** : les services utilisant MTOM <em>peuvent</em> fonctionner.</span><span class="sxs-lookup"><span data-stu-id="3ca9a-118">**MTOM** Services using MTOM <em>may</em> work.</span></span> <span data-ttu-id="3ca9a-119">Aucune prise en charge officielle n’est disponible pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="3ca9a-119">Official support is not offered at this time.</span></span>
* <span data-ttu-id="3ca9a-120">Les types de **récursivité** qui sont définis de manière récursive (par exemple, qui font référence à leur propre tableau) ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="3ca9a-120">**Recursion** types that are defined recursively (e.g. refer to an array of themselves) are not supported.</span></span>

## <span data-ttu-id="3ca9a-121"><a name="wadl"> </a>WADL</span><span class="sxs-lookup"><span data-stu-id="3ca9a-121"><a name="wadl"> </a>WADL</span></span>
<span data-ttu-id="3ca9a-122">Il n’existe actuellement aucun problème connu relatif à l’importation WADL.</span><span class="sxs-lookup"><span data-stu-id="3ca9a-122">There are no known WADL import issues currently.</span></span>


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

[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md
[How to cache operation results in Azure API Management]: api-management-howto-cache.md