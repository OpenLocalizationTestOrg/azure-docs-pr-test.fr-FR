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
# <a name="api-import-restrictions-and-known-issues"></a><span data-ttu-id="7753c-103">Restrictions et problèmes connus relatifs à l’importation d’API</span><span class="sxs-lookup"><span data-stu-id="7753c-103">API import restrictions and known issues</span></span>
## <a name="about-this-list"></a><span data-ttu-id="7753c-104">À propos de cette liste</span><span class="sxs-lookup"><span data-stu-id="7753c-104">About this list</span></span>
<span data-ttu-id="7753c-105">Alors que tout est mis en œuvre tooensure que l’importation de votre API dans la gestion des API Azure est plus transparente et exempt de problèmes que possible, nous parfois imposer des restrictions ou identifier les problèmes qui devront toobe rectifié avant de pouvoir importer correctement.</span><span class="sxs-lookup"><span data-stu-id="7753c-105">While every effort is made tooensure that importing your API into Azure API Management is as seamless and problem-free as possible, we do occasionally impose restrictions or identify issues that will need toobe rectified before you can successfully import.</span></span> <span data-ttu-id="7753c-106">Cet article décrit ces options, organisés par le format d’importation hello Hello API.</span><span class="sxs-lookup"><span data-stu-id="7753c-106">This article documents these, organised by hello import format of hello API.</span></span>

## <span data-ttu-id="7753c-107"><a name="open-api"></a>Open API/Swagger</span><span class="sxs-lookup"><span data-stu-id="7753c-107"><a name="open-api"> </a>Open API/Swagger</span></span>
<span data-ttu-id="7753c-108">En règle générale, si vous recevez des erreurs d’importation de votre document de l’API Open, vérifiez que vous avez validé, soit à l’aide du Concepteur de hello dans hello nouveau portail Azure (conception - Front End - ouvrir API spécification de l’éditeur), ou avec un 3e partie comme outil <a href="http://www.swagger.io"> Éditeur de swagger</a>.</span><span class="sxs-lookup"><span data-stu-id="7753c-108">In general, if you are receiving errors importing your Open API document, please ensure you have validated it - either using hello designer in hello new Azure Portal (Design - Front End - Open API Specification Editor), or with a 3rd party tool such as <a href="http://www.swagger.io">Swagger Editor</a>.</span></span>

* <span data-ttu-id="7753c-109">**Nom d’hôte** : nous exigeons un attribut de nom d’hôte.</span><span class="sxs-lookup"><span data-stu-id="7753c-109">**Host Name** we require a host name attribute.</span></span>
* <span data-ttu-id="7753c-110">**Chemin d’accès de base** : nous exigeons un attribut de chemin d’accès de base.</span><span class="sxs-lookup"><span data-stu-id="7753c-110">**Base Path** we require a base path attribute.</span></span>
* <span data-ttu-id="7753c-111">**Schémas** : nous exigeons un tableau de schéma.</span><span class="sxs-lookup"><span data-stu-id="7753c-111">**Schemes** we require a scheme array.</span></span> 

## <span data-ttu-id="7753c-112"><a name="wsdl"></a>WSDL</span><span class="sxs-lookup"><span data-stu-id="7753c-112"><a name="wsdl"> </a>WSDL</span></span>
<span data-ttu-id="7753c-113">Fichiers WSDL sont utilisé toogenerate SOAP pass-through API ou servent hello du serveur principal d’une API SOAP pour REST.</span><span class="sxs-lookup"><span data-stu-id="7753c-113">WSDL files are used toogenerate SOAP Pass-through APIs, or serve as hello backend of a SOAP-to-REST API.</span></span>

* <span data-ttu-id="7753c-114">**WSDL:Import** : nous ne prenons actuellement pas en charge les API utilisant cet attribut.</span><span class="sxs-lookup"><span data-stu-id="7753c-114">**WSDL:Import** we do not currently support APIs using this attribute.</span></span> <span data-ttu-id="7753c-115">Clients doivent fusionner les éléments hello importé dans un document.</span><span class="sxs-lookup"><span data-stu-id="7753c-115">Customers should merge hello imported elements into one document.</span></span>
* <span data-ttu-id="7753c-116">Les **messages en plusieurs parties** ne sont actuellement pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="7753c-116">**Messages with multiple parts** are currently not supported.</span></span>
* <span data-ttu-id="7753c-117">**WCF wsHttpBinding** : les services SOAP créés avec Windows Communication Foundation doivent utiliser basicHttpBinding. wsHttpBinding n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="7753c-117">**WCF wsHttpBinding** SOAP services created with Windows Communication Foundation should use basicHttpBinding - wsHttpBinding is not supported.</span></span>
* <span data-ttu-id="7753c-118">**MTOM** : les services utilisant MTOM <em>peuvent</em> fonctionner.</span><span class="sxs-lookup"><span data-stu-id="7753c-118">**MTOM** Services using MTOM <em>may</em> work.</span></span> <span data-ttu-id="7753c-119">Aucune prise en charge officielle n’est disponible pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="7753c-119">Official support is not offered at this time.</span></span>
* <span data-ttu-id="7753c-120">**La récursivité** types qui sont définis de manière récursive (par exemple, consultez le tableau tooan eux-mêmes) ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="7753c-120">**Recursion** types that are defined recursively (e.g. refer tooan array of themselves) are not supported.</span></span>

## <span data-ttu-id="7753c-121"><a name="wadl"></a>WADL</span><span class="sxs-lookup"><span data-stu-id="7753c-121"><a name="wadl"> </a>WADL</span></span>
<span data-ttu-id="7753c-122">Il n’existe actuellement aucun problème connu relatif à l’importation WADL.</span><span class="sxs-lookup"><span data-stu-id="7753c-122">There are no known WADL import issues currently.</span></span>


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
