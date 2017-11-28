---
title: "Liste des erreurs et des solutions Logic Apps B2B : Azure App Service | Microsoft Docs"
description: Liste des erreurs et des solutions Logic Apps B2B
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 0340e2979f1972ba631354e206c93969e55946e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-b2b-list-of-errors-and-solutions"></a><span data-ttu-id="7933c-103">Liste des erreurs et des solutions Logic Apps B2B</span><span class="sxs-lookup"><span data-stu-id="7933c-103">Logic Apps B2B list of errors and solutions</span></span>  
<span data-ttu-id="7933c-104">Cet article vous aide à comprendre les erreurs qui peuvent se produire dans le cadre des scénarios Logic Apps B2B et suggère des actions appropriées pour corriger ces erreurs.</span><span class="sxs-lookup"><span data-stu-id="7933c-104">This article helps you troubleshoot errors that might happen in Logic Apps B2B scenarios and suggests appropriate actions for correcting those errors.</span></span>


## <a name="agreement-resolution"></a><span data-ttu-id="7933c-105">Résolution d’accord</span><span class="sxs-lookup"><span data-stu-id="7933c-105">Agreement Resolution</span></span>

### <a name="no-agreement-found"></a><span data-ttu-id="7933c-106">* Aucun accord trouvé</span><span class="sxs-lookup"><span data-stu-id="7933c-106">*No agreement found</span></span> 

|   |   |  
|---|---|
| <span data-ttu-id="7933c-107">Description de l’erreur</span><span class="sxs-lookup"><span data-stu-id="7933c-107">Error description</span></span> | <span data-ttu-id="7933c-108">Aucun accord trouvé avec les paramètres de résolution d’accord</span><span class="sxs-lookup"><span data-stu-id="7933c-108">No agreement found with Agreement Resolution Parameters</span></span>|    
| <span data-ttu-id="7933c-109">Action requise</span><span class="sxs-lookup"><span data-stu-id="7933c-109">User action</span></span> | <span data-ttu-id="7933c-110">accord de Hello doit être ajouté toohello compte d’intégration avec des identités d’entreprise convenu.</span><span class="sxs-lookup"><span data-stu-id="7933c-110">hello agreement should be added toohello integration account with agreed business identities.</span></span></br> <span data-ttu-id="7933c-111">les identités d’entreprise Hello doivent correspondre à l’ID de message d’entrée toohello</span><span class="sxs-lookup"><span data-stu-id="7933c-111">hello business identities should match toohello input message ids</span></span>|  
|   |   |

### <a name="-no-agreement-found-with-identities"></a><span data-ttu-id="7933c-112">* Aucun accord trouvé avec les identités</span><span class="sxs-lookup"><span data-stu-id="7933c-112">* No agreement found with identities</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="7933c-113">Description de l’erreur</span><span class="sxs-lookup"><span data-stu-id="7933c-113">Error description</span></span> | <span data-ttu-id="7933c-114">Aucun accord trouvé avec les identités : ’AS2Identity’::’Partner1’ et ’AS2Identity’::’Partner3’.</span><span class="sxs-lookup"><span data-stu-id="7933c-114">No agreement found with identities: 'AS2Identity'::'Partner1' and'AS2Identity'::'Partner3'</span></span>| 
| <span data-ttu-id="7933c-115">Action requise</span><span class="sxs-lookup"><span data-stu-id="7933c-115">User action</span></span> | <span data-ttu-id="7933c-116">AS2 non valide-à partir d’ou AS2-tooconfigured pour l’accord.</span><span class="sxs-lookup"><span data-stu-id="7933c-116">Invalid AS2-From or AS2-tooconfigured for agreement.</span></span> </br> <span data-ttu-id="7933c-117">Messages AS2 AS2-à partir d’ou en-têtes avec des configurations de contrat de message AS2-tooheaders ou contrat ID toomatch AS2 dans AS2</span><span class="sxs-lookup"><span data-stu-id="7933c-117">Correct AS2 message AS2-From or AS2-tooheaders or agreement toomatch AS2 ids in AS2 message headers with agreement configurations</span></span> |
|   |   |     

## <a name="as2"></a><span data-ttu-id="7933c-118">AS2</span><span class="sxs-lookup"><span data-stu-id="7933c-118">AS2</span></span>

### <a name="-missing-as2-message-headers"></a><span data-ttu-id="7933c-119">* En-têtes de message AS2 manquants</span><span class="sxs-lookup"><span data-stu-id="7933c-119">* Missing AS2 message headers</span></span>  

|   |   |  
|---|---|
| <span data-ttu-id="7933c-120">Description de l’erreur</span><span class="sxs-lookup"><span data-stu-id="7933c-120">Error description</span></span>| <span data-ttu-id="7933c-121">En-têtes AS2 non valides.</span><span class="sxs-lookup"><span data-stu-id="7933c-121">Invalid AS2 headers.</span></span> <span data-ttu-id="7933c-122">L’en-tête « AS2-To » ou « AS2-From » est vide.</span><span class="sxs-lookup"><span data-stu-id="7933c-122">One of 'AS2-To' or 'AS2-From' headers are empty</span></span>| 
| <span data-ttu-id="7933c-123">Action requise</span><span class="sxs-lookup"><span data-stu-id="7933c-123">User action</span></span> | <span data-ttu-id="7933c-124">Réception d’un message AS2 ne contenant pas hello AS2-à partir d’ou AS2-tooor les deux en-têtes.</span><span class="sxs-lookup"><span data-stu-id="7933c-124">An AS2 message was received that did not contain hello AS2-From or AS2-tooor both headers.</span></span> </br> <span data-ttu-id="7933c-125">Vérifiez le message AS2 AS2-à partir d’et AS2-tooheaders et corrigez-les en fonction de la configuration de l’accord</span><span class="sxs-lookup"><span data-stu-id="7933c-125">Check AS2 message AS2-From and AS2-tooheaders and correct them based on agreement configuration</span></span> |
|  |  | 


### <a name="-missing-as2-message-body-and-headers"></a><span data-ttu-id="7933c-126">* Corps et en-têtes de message AS2 manquants</span><span class="sxs-lookup"><span data-stu-id="7933c-126">* Missing AS2 message body and headers</span></span>    

|   |   |  
|---|---|
| <span data-ttu-id="7933c-127">Description de l’erreur</span><span class="sxs-lookup"><span data-stu-id="7933c-127">Error description</span></span>| <span data-ttu-id="7933c-128">contenu de la demande Hello est null ou vide</span><span class="sxs-lookup"><span data-stu-id="7933c-128">hello request content is null or empty</span></span> | 
| <span data-ttu-id="7933c-129">Action requise</span><span class="sxs-lookup"><span data-stu-id="7933c-129">User action</span></span> | <span data-ttu-id="7933c-130">Réception d’un message AS2 ne contenant pas de corps de message hello</span><span class="sxs-lookup"><span data-stu-id="7933c-130">An AS2 message was received that did not contain hello message body</span></span> |
|  |  | 

### <a name="-as2-message-decryption-failure"></a><span data-ttu-id="7933c-131">* Échec du déchiffrement de message AS2</span><span class="sxs-lookup"><span data-stu-id="7933c-131">* AS2 message decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="7933c-132">Description de l’erreur</span><span class="sxs-lookup"><span data-stu-id="7933c-132">Error description</span></span> |  <span data-ttu-id="7933c-133">[processed/Error: decryption-failed]</span><span class="sxs-lookup"><span data-stu-id="7933c-133">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="7933c-134">Action requise</span><span class="sxs-lookup"><span data-stu-id="7933c-134">User action</span></span> | <span data-ttu-id="7933c-135">Ajouter @base64ToBinary tooAS2Message avant d’envoyer toopartner</span><span class="sxs-lookup"><span data-stu-id="7933c-135">Add @base64ToBinary tooAS2Message before sending toopartner</span></span> 
```java
            "HTTP": {
                "inputs": {
                    "body": "@base64ToBinary(body('Encode_to_AS2_message')?['AS2Message']?['Content'])",
                    "headers": "@body('Encode_to_AS2_message')?['AS2Message']?['OutboundHeaders']",
                    "method": "POST",
                    "uri": "xxxxx.xxx"
                },
                
``` 

### <a name="-mdn-decryption-failure"></a><span data-ttu-id="7933c-136">* Échec du déchiffrement du MDN</span><span class="sxs-lookup"><span data-stu-id="7933c-136">* MDN decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="7933c-137">Description de l’erreur</span><span class="sxs-lookup"><span data-stu-id="7933c-137">Error description</span></span> |  <span data-ttu-id="7933c-138">[processed/Error: decryption-failed]</span><span class="sxs-lookup"><span data-stu-id="7933c-138">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="7933c-139">Action requise</span><span class="sxs-lookup"><span data-stu-id="7933c-139">User action</span></span> | <span data-ttu-id="7933c-140">Ajouter @base64ToBinary tooMDN avant d’envoyer toopartner</span><span class="sxs-lookup"><span data-stu-id="7933c-140">Add @base64ToBinary tooMDN before sending toopartner</span></span> 
```java
            "Response": {
                "inputs": {
                    "body": "@base64ToBinary(body('Decode_AS2_message')?['OutgoingMDN']?['Content'])",
                    "headers": "@body('Decode_AS2_message')?['OutgoingMDN']?['OutboundHeaders']",
                    "statusCode": 200
                },
                
``` 

### <a name="-missing-signing-certificate"></a><span data-ttu-id="7933c-141">* Certificat de signature manquant</span><span class="sxs-lookup"><span data-stu-id="7933c-141">* Missing signing certificate</span></span>

|   |   |  
|---|---|
| <span data-ttu-id="7933c-142">Description de l’erreur</span><span class="sxs-lookup"><span data-stu-id="7933c-142">Error description</span></span>| <span data-ttu-id="7933c-143">Hello certificat de signature n'a pas été configuré pour le tiers AS2.</span><span class="sxs-lookup"><span data-stu-id="7933c-143">hello Signing Certificate has not been configured for AS2 party.</span></span> </br> <span data-ttu-id="7933c-144">AS2-From : partner1 AS2-To : partner2</span><span class="sxs-lookup"><span data-stu-id="7933c-144">AS2-From: partner1 AS2-To: partner2</span></span> | 
| <span data-ttu-id="7933c-145">Action requise</span><span class="sxs-lookup"><span data-stu-id="7933c-145">User action</span></span> | <span data-ttu-id="7933c-146">Configurez les paramètres d’accord AS2 avec le certificat approprié pour la signature.</span><span class="sxs-lookup"><span data-stu-id="7933c-146">Configure AS2 agreement settings with correct certificate for signature</span></span> |
|  |  | 

## <a name="x12-and-edifact"></a><span data-ttu-id="7933c-147">X12 et EDIFACT</span><span class="sxs-lookup"><span data-stu-id="7933c-147">X12 and EDIFACT</span></span>

### <a name="-leading-or-trailing-space-found"></a><span data-ttu-id="7933c-148">* Espace de début ou de fin trouvé</span><span class="sxs-lookup"><span data-stu-id="7933c-148">* Leading or trailing space found</span></span>    
    
|   |   | 
|---|---|
| <span data-ttu-id="7933c-149">Description de l’erreur</span><span class="sxs-lookup"><span data-stu-id="7933c-149">Error description</span></span> | <span data-ttu-id="7933c-150">Erreur rencontrée lors de l’analyse.</span><span class="sxs-lookup"><span data-stu-id="7933c-150">Error encountered during parsing.</span></span> <span data-ttu-id="7933c-151">Hello document informatisé Edifact avec l’id ' 123456 'contenu dans l’échange (sans groupe) avec l’id ' 987654', id d’expéditeur 'Partner1', id de destinataire 'Partner2' est interrompu avec les erreurs suivantes : début à la fin de séparateur trouvé</span><span class="sxs-lookup"><span data-stu-id="7933c-151">hello Edifact transaction set with id '123456' contained in interchange (without group) with id '987654', with sender id 'Partner1', receiver id 'Partner2' is being suspended with following errors: Leading Trailing separator found</span></span> |
| <span data-ttu-id="7933c-152">Action requise</span><span class="sxs-lookup"><span data-stu-id="7933c-152">User action</span></span> | <span data-ttu-id="7933c-153">toobe de paramètres d’accord Hello configuré tooallow de début et de fin d’espace.</span><span class="sxs-lookup"><span data-stu-id="7933c-153">hello agreement settings toobe configured tooallow leading and trailing space.</span></span> </br> <span data-ttu-id="7933c-154">Modifier le contrat paramètres tooallow début et de fin d’espace</span><span class="sxs-lookup"><span data-stu-id="7933c-154">Edit agreement settings tooallow leading and trailing space</span></span> |
|   |   |

![Autoriser l’espace](./media/logic-apps-enterprise-integration-b2b-list-errors-solutions/leadingandtrailing.png)

### <a name="-duplicate-check-has-enabled-in-hello-agreement"></a><span data-ttu-id="7933c-156">* Check en double a activé dans l’accord de hello</span><span class="sxs-lookup"><span data-stu-id="7933c-156">* Duplicate check has enabled in hello agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="7933c-157">Description de l’erreur</span><span class="sxs-lookup"><span data-stu-id="7933c-157">Error description</span></span> | <span data-ttu-id="7933c-158">Numéro de contrôle en double</span><span class="sxs-lookup"><span data-stu-id="7933c-158">Duplicate Control Number</span></span> |
| <span data-ttu-id="7933c-159">Action requise</span><span class="sxs-lookup"><span data-stu-id="7933c-159">User action</span></span> | <span data-ttu-id="7933c-160">Cette erreur indique que message de salutation reçu a des numéros de contrôle dupliqués.</span><span class="sxs-lookup"><span data-stu-id="7933c-160">This error indicates hello received message has duplicate control numbers.</span></span> </br> <span data-ttu-id="7933c-161">Corrigez le numéro de contrôle hello et renvoyez le message de type hello</span><span class="sxs-lookup"><span data-stu-id="7933c-161">Correct hello control number and resend hello message</span></span> |
|   |   |

### <a name="-missing-schema-in-hello-agreement"></a><span data-ttu-id="7933c-162">* Schéma manquant dans le contrat de hello</span><span class="sxs-lookup"><span data-stu-id="7933c-162">* Missing schema in hello agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="7933c-163">Description de l’erreur</span><span class="sxs-lookup"><span data-stu-id="7933c-163">Error description</span></span> | <span data-ttu-id="7933c-164">Erreur rencontrée lors de l’analyse.</span><span class="sxs-lookup"><span data-stu-id="7933c-164">Error encountered during parsing.</span></span> <span data-ttu-id="7933c-165">jeu de transactions Hello X12 avec l’id '564220001' contenue dans le groupe fonctionnel avec l’id '56422', dans l’échange avec l’id '000056422', id d’expéditeur ' 12345678', id de destinataire ' 87654321' est interrompu avec les erreurs suivantes « message de salutation a un type de document inconnu PE et n’a pas résolu tooany de schémas existants de hello configuré dans l’accord de hello »</span><span class="sxs-lookup"><span data-stu-id="7933c-165">hello X12 transaction set with id '564220001' contained in functional group with id '56422', in interchange with id '000056422', with sender id '12345678       ', receiver id '87654321       ' is being suspended with following errors "hello message has an unknown document type and did not resolve tooany of hello existing schemas configured in hello agreement"</span></span> |
| <span data-ttu-id="7933c-166">Action requise</span><span class="sxs-lookup"><span data-stu-id="7933c-166">User action</span></span> | <span data-ttu-id="7933c-167">Configurer le schéma dans les paramètres de l’accord hello</span><span class="sxs-lookup"><span data-stu-id="7933c-167">Configure schema in hello agreement settings</span></span>  |
|   |   |

### <a name="-incorrect-schema-in-hello-agreement"></a><span data-ttu-id="7933c-168">* Schéma incorrect dans l’accord de hello</span><span class="sxs-lookup"><span data-stu-id="7933c-168">* Incorrect schema in hello agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="7933c-169">Description de l’erreur</span><span class="sxs-lookup"><span data-stu-id="7933c-169">Error description</span></span> | <span data-ttu-id="7933c-170">message de type Hello a un type de document inconnu et tooany de schémas existants de hello configurés dans hello accord n’a pas été résolue.</span><span class="sxs-lookup"><span data-stu-id="7933c-170">hello message has an unknown document type and did not resolve tooany of hello existing schemas configured in hello agreement.</span></span> |
| <span data-ttu-id="7933c-171">Action requise</span><span class="sxs-lookup"><span data-stu-id="7933c-171">User action</span></span> | <span data-ttu-id="7933c-172">Configurer le schéma correct dans les paramètres de l’accord hello</span><span class="sxs-lookup"><span data-stu-id="7933c-172">Configure correct schema in hello agreement settings</span></span>  |
|   |   |

## <a name="flat-file"></a><span data-ttu-id="7933c-173">Fichier plat</span><span class="sxs-lookup"><span data-stu-id="7933c-173">Flat file</span></span>

### <a name="-input-message-with-no-body"></a><span data-ttu-id="7933c-174">* Message d’entrée sans corps</span><span class="sxs-lookup"><span data-stu-id="7933c-174">* Input message with no body</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="7933c-175">Description de l’erreur</span><span class="sxs-lookup"><span data-stu-id="7933c-175">Error description</span></span> | <span data-ttu-id="7933c-176">Modèle non valide.</span><span class="sxs-lookup"><span data-stu-id="7933c-176">InvalidTemplate.</span></span> <span data-ttu-id="7933c-177">Les expressions de langage de modèle tooprocess impossible dans les entrées d’action 'Flat_File_Decoding' à la ligne '1' et la colonne '1902' : ' requise de la propriété « content » attend une valeur, mais dispose null.</span><span class="sxs-lookup"><span data-stu-id="7933c-177">Unable tooprocess template language expressions in action 'Flat_File_Decoding' inputs at line '1' and column '1902': 'Required property 'content' expects a value but got null.</span></span> <span data-ttu-id="7933c-178">Chemin d’accès « . ».</span><span class="sxs-lookup"><span data-stu-id="7933c-178">Path ''.'.</span></span> |
| <span data-ttu-id="7933c-179">Action requise</span><span class="sxs-lookup"><span data-stu-id="7933c-179">User action</span></span> | <span data-ttu-id="7933c-180">Cette erreur indique le message d’entrée de type hello ne contient pas un corps</span><span class="sxs-lookup"><span data-stu-id="7933c-180">This error indicates hello input message does not contain a body</span></span> |
|   |   | 

## <a name="learn-more"></a><span data-ttu-id="7933c-181">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="7933c-181">Learn more</span></span>
[<span data-ttu-id="7933c-182">En savoir plus sur hello Pack d’intégration Enterprise</span><span class="sxs-lookup"><span data-stu-id="7933c-182">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md)
