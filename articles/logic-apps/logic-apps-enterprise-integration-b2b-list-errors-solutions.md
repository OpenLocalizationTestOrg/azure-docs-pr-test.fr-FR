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
ms.openlocfilehash: 1865d75f1b4c2aa18d5a3130f639572d19563b3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="logic-apps-b2b-list-of-errors-and-solutions"></a><span data-ttu-id="b0237-103">Liste des erreurs et des solutions Logic Apps B2B</span><span class="sxs-lookup"><span data-stu-id="b0237-103">Logic Apps B2B list of errors and solutions</span></span>  
<span data-ttu-id="b0237-104">Cet article vous aide à comprendre les erreurs qui peuvent se produire dans le cadre des scénarios Logic Apps B2B et suggère des actions appropriées pour corriger ces erreurs.</span><span class="sxs-lookup"><span data-stu-id="b0237-104">This article helps you troubleshoot errors that might happen in Logic Apps B2B scenarios and suggests appropriate actions for correcting those errors.</span></span>


## <a name="agreement-resolution"></a><span data-ttu-id="b0237-105">Résolution d’accord</span><span class="sxs-lookup"><span data-stu-id="b0237-105">Agreement Resolution</span></span>

### <a name="no-agreement-found"></a><span data-ttu-id="b0237-106">* Aucun accord trouvé</span><span class="sxs-lookup"><span data-stu-id="b0237-106">*No agreement found</span></span> 

|   |   |  
|---|---|
| <span data-ttu-id="b0237-107">Description de l’erreur</span><span class="sxs-lookup"><span data-stu-id="b0237-107">Error description</span></span> | <span data-ttu-id="b0237-108">Aucun accord trouvé avec les paramètres de résolution d’accord</span><span class="sxs-lookup"><span data-stu-id="b0237-108">No agreement found with Agreement Resolution Parameters</span></span>|    
| <span data-ttu-id="b0237-109">Action requise</span><span class="sxs-lookup"><span data-stu-id="b0237-109">User action</span></span> | <span data-ttu-id="b0237-110">L’accord doit être ajouté au compte d’intégration avec les identités commerciales convenues.</span><span class="sxs-lookup"><span data-stu-id="b0237-110">The agreement should be added to the integration account with agreed business identities.</span></span></br> <span data-ttu-id="b0237-111">Les identités commerciales doivent correspondre aux ID de message entrant.</span><span class="sxs-lookup"><span data-stu-id="b0237-111">The business identities should match to the input message ids</span></span>|  
|   |   |

### <a name="-no-agreement-found-with-identities"></a><span data-ttu-id="b0237-112">* Aucun accord trouvé avec les identités</span><span class="sxs-lookup"><span data-stu-id="b0237-112">* No agreement found with identities</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="b0237-113">Description de l’erreur</span><span class="sxs-lookup"><span data-stu-id="b0237-113">Error description</span></span> | <span data-ttu-id="b0237-114">Aucun accord trouvé avec les identités : ’AS2Identity’::’Partner1’ et ’AS2Identity’::’Partner3’.</span><span class="sxs-lookup"><span data-stu-id="b0237-114">No agreement found with identities: 'AS2Identity'::'Partner1' and'AS2Identity'::'Partner3'</span></span>| 
| <span data-ttu-id="b0237-115">Action requise</span><span class="sxs-lookup"><span data-stu-id="b0237-115">User action</span></span> | <span data-ttu-id="b0237-116">En-tête AS2-From ou AS2-To non valide configuré pour l’accord.</span><span class="sxs-lookup"><span data-stu-id="b0237-116">Invalid AS2-From or AS2-To configured for agreement.</span></span> </br> <span data-ttu-id="b0237-117">Corrigez les en-têtes de message AS2 AS2-From ou AS2-To de l’accord de manière à ce que les ID AS2 des en-têtes de message AS2 correspondent aux configurations de l’accord.</span><span class="sxs-lookup"><span data-stu-id="b0237-117">Correct AS2 message AS2-From or AS2-To headers or agreement to match AS2 ids in AS2 message headers with agreement configurations</span></span> |
|   |   |     

## <a name="as2"></a><span data-ttu-id="b0237-118">AS2</span><span class="sxs-lookup"><span data-stu-id="b0237-118">AS2</span></span>

### <a name="-missing-as2-message-headers"></a><span data-ttu-id="b0237-119">* En-têtes de message AS2 manquants</span><span class="sxs-lookup"><span data-stu-id="b0237-119">* Missing AS2 message headers</span></span>  

|   |   |  
|---|---|
| <span data-ttu-id="b0237-120">Description de l’erreur</span><span class="sxs-lookup"><span data-stu-id="b0237-120">Error description</span></span>| <span data-ttu-id="b0237-121">En-têtes AS2 non valides.</span><span class="sxs-lookup"><span data-stu-id="b0237-121">Invalid AS2 headers.</span></span> <span data-ttu-id="b0237-122">L’en-tête « AS2-To » ou « AS2-From » est vide.</span><span class="sxs-lookup"><span data-stu-id="b0237-122">One of 'AS2-To' or 'AS2-From' headers are empty</span></span>| 
| <span data-ttu-id="b0237-123">Action requise</span><span class="sxs-lookup"><span data-stu-id="b0237-123">User action</span></span> | <span data-ttu-id="b0237-124">Un message AS2 ne contenant pas d’en-tête AS2-From ou AS2-To a été reçu.</span><span class="sxs-lookup"><span data-stu-id="b0237-124">An AS2 message was received that did not contain the AS2-From or AS2-To or both headers.</span></span> </br> <span data-ttu-id="b0237-125">Vérifiez les en-têtes AS2-From et AS2-To de message AS2 et corrigez-les en fonction de la configuration de l’accord.</span><span class="sxs-lookup"><span data-stu-id="b0237-125">Check AS2 message AS2-From and AS2-To headers and correct them based on agreement configuration</span></span> |
|  |  | 


### <a name="-missing-as2-message-body-and-headers"></a><span data-ttu-id="b0237-126">* Corps et en-têtes de message AS2 manquants</span><span class="sxs-lookup"><span data-stu-id="b0237-126">* Missing AS2 message body and headers</span></span>    

|   |   |  
|---|---|
| <span data-ttu-id="b0237-127">Description de l’erreur</span><span class="sxs-lookup"><span data-stu-id="b0237-127">Error description</span></span>| <span data-ttu-id="b0237-128">Le contenu de la requête est nul ou vide.</span><span class="sxs-lookup"><span data-stu-id="b0237-128">The request content is null or empty</span></span> | 
| <span data-ttu-id="b0237-129">Action requise</span><span class="sxs-lookup"><span data-stu-id="b0237-129">User action</span></span> | <span data-ttu-id="b0237-130">Un message AS2 ne comportant pas de corps de message a été reçu.</span><span class="sxs-lookup"><span data-stu-id="b0237-130">An AS2 message was received that did not contain the message body</span></span> |
|  |  | 

### <a name="-as2-message-decryption-failure"></a><span data-ttu-id="b0237-131">* Échec du déchiffrement de message AS2</span><span class="sxs-lookup"><span data-stu-id="b0237-131">* AS2 message decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="b0237-132">Description de l’erreur</span><span class="sxs-lookup"><span data-stu-id="b0237-132">Error description</span></span> |  <span data-ttu-id="b0237-133">[processed/Error: decryption-failed]</span><span class="sxs-lookup"><span data-stu-id="b0237-133">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="b0237-134">Action requise</span><span class="sxs-lookup"><span data-stu-id="b0237-134">User action</span></span> | <span data-ttu-id="b0237-135">Ajoutez @base64ToBinary au message AS2 avant de l’envoyer au partenaire.</span><span class="sxs-lookup"><span data-stu-id="b0237-135">Add @base64ToBinary to AS2Message before sending to partner</span></span> 
```java
            "HTTP": {
                "inputs": {
                    "body": "@base64ToBinary(body('Encode_to_AS2_message')?['AS2Message']?['Content'])",
                    "headers": "@body('Encode_to_AS2_message')?['AS2Message']?['OutboundHeaders']",
                    "method": "POST",
                    "uri": "xxxxx.xxx"
                },
                
``` 

### <a name="-mdn-decryption-failure"></a><span data-ttu-id="b0237-136">* Échec du déchiffrement du MDN</span><span class="sxs-lookup"><span data-stu-id="b0237-136">* MDN decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="b0237-137">Description de l’erreur</span><span class="sxs-lookup"><span data-stu-id="b0237-137">Error description</span></span> |  <span data-ttu-id="b0237-138">[processed/Error: decryption-failed]</span><span class="sxs-lookup"><span data-stu-id="b0237-138">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="b0237-139">Action requise</span><span class="sxs-lookup"><span data-stu-id="b0237-139">User action</span></span> | <span data-ttu-id="b0237-140">Ajoutez @base64ToBinary au MDN avant de l’envoyer au partenaire.</span><span class="sxs-lookup"><span data-stu-id="b0237-140">Add @base64ToBinary to MDN before sending to partner</span></span> 
```java
            "Response": {
                "inputs": {
                    "body": "@base64ToBinary(body('Decode_AS2_message')?['OutgoingMDN']?['Content'])",
                    "headers": "@body('Decode_AS2_message')?['OutgoingMDN']?['OutboundHeaders']",
                    "statusCode": 200
                },
                
``` 

### <a name="-missing-signing-certificate"></a><span data-ttu-id="b0237-141">* Certificat de signature manquant</span><span class="sxs-lookup"><span data-stu-id="b0237-141">* Missing signing certificate</span></span>

|   |   |  
|---|---|
| <span data-ttu-id="b0237-142">Description de l’erreur</span><span class="sxs-lookup"><span data-stu-id="b0237-142">Error description</span></span>| <span data-ttu-id="b0237-143">Le certificat de signature n’a pas été configuré pour le tiers AS2.</span><span class="sxs-lookup"><span data-stu-id="b0237-143">The Signing Certificate has not been configured for AS2 party.</span></span> </br> <span data-ttu-id="b0237-144">AS2-From : partner1 AS2-To : partner2</span><span class="sxs-lookup"><span data-stu-id="b0237-144">AS2-From: partner1 AS2-To: partner2</span></span> | 
| <span data-ttu-id="b0237-145">Action requise</span><span class="sxs-lookup"><span data-stu-id="b0237-145">User action</span></span> | <span data-ttu-id="b0237-146">Configurez les paramètres d’accord AS2 avec le certificat approprié pour la signature.</span><span class="sxs-lookup"><span data-stu-id="b0237-146">Configure AS2 agreement settings with correct certificate for signature</span></span> |
|  |  | 

## <a name="x12-and-edifact"></a><span data-ttu-id="b0237-147">X12 et EDIFACT</span><span class="sxs-lookup"><span data-stu-id="b0237-147">X12 and EDIFACT</span></span>

### <a name="-leading-or-trailing-space-found"></a><span data-ttu-id="b0237-148">* Espace de début ou de fin trouvé</span><span class="sxs-lookup"><span data-stu-id="b0237-148">* Leading or trailing space found</span></span>    
    
|   |   | 
|---|---|
| <span data-ttu-id="b0237-149">Description de l’erreur</span><span class="sxs-lookup"><span data-stu-id="b0237-149">Error description</span></span> | <span data-ttu-id="b0237-150">Erreur rencontrée lors de l’analyse.</span><span class="sxs-lookup"><span data-stu-id="b0237-150">Error encountered during parsing.</span></span> <span data-ttu-id="b0237-151">Le document informatisé EDIFACT ayant l’id ’123456’ contenu dans l’échange (sans groupe) ayant l’id ’987654’, l’id d’expéditeur ’Partner1’, l’id de destinataire ’Partner2’ est interrompu avec les erreurs suivantes : Séparateur de début trouvé.</span><span class="sxs-lookup"><span data-stu-id="b0237-151">The Edifact transaction set with id '123456' contained in interchange (without group) with id '987654', with sender id 'Partner1', receiver id 'Partner2' is being suspended with following errors: Leading Trailing separator found</span></span> |
| <span data-ttu-id="b0237-152">Action requise</span><span class="sxs-lookup"><span data-stu-id="b0237-152">User action</span></span> | <span data-ttu-id="b0237-153">Les paramètres d’accord doivent être configurés de manière à autoriser les espaces de début et de fin.</span><span class="sxs-lookup"><span data-stu-id="b0237-153">The agreement settings to be configured to allow leading and trailing space.</span></span> </br> <span data-ttu-id="b0237-154">Modifiez les paramètres d’accord de manière à autoriser les espaces de début et de fin.</span><span class="sxs-lookup"><span data-stu-id="b0237-154">Edit agreement settings to allow leading and trailing space</span></span> |
|   |   |

![Autoriser l’espace](./media/logic-apps-enterprise-integration-b2b-list-errors-solutions/leadingandtrailing.png)

### <a name="-duplicate-check-has-enabled-in-the-agreement"></a><span data-ttu-id="b0237-156">* La vérification de doublons a été activée dans l’accord</span><span class="sxs-lookup"><span data-stu-id="b0237-156">* Duplicate check has enabled in the agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="b0237-157">Description de l’erreur</span><span class="sxs-lookup"><span data-stu-id="b0237-157">Error description</span></span> | <span data-ttu-id="b0237-158">Numéro de contrôle en double</span><span class="sxs-lookup"><span data-stu-id="b0237-158">Duplicate Control Number</span></span> |
| <span data-ttu-id="b0237-159">Action requise</span><span class="sxs-lookup"><span data-stu-id="b0237-159">User action</span></span> | <span data-ttu-id="b0237-160">Cette erreur indique que le message reçu contient des numéros de contrôle en double.</span><span class="sxs-lookup"><span data-stu-id="b0237-160">This error indicates the received message has duplicate control numbers.</span></span> </br> <span data-ttu-id="b0237-161">Corrigez le numéro de contrôle et renvoyez le message.</span><span class="sxs-lookup"><span data-stu-id="b0237-161">Correct the control number and resend the message</span></span> |
|   |   |

### <a name="-missing-schema-in-the-agreement"></a><span data-ttu-id="b0237-162">* Schéma manquant dans l’accord</span><span class="sxs-lookup"><span data-stu-id="b0237-162">* Missing schema in the agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="b0237-163">Description de l’erreur</span><span class="sxs-lookup"><span data-stu-id="b0237-163">Error description</span></span> | <span data-ttu-id="b0237-164">Erreur rencontrée lors de l’analyse.</span><span class="sxs-lookup"><span data-stu-id="b0237-164">Error encountered during parsing.</span></span> <span data-ttu-id="b0237-165">Le document informatisé X12 possédant l’id ’564220001’ contenu dans le groupe fonctionnel d’id ’56422’, dans l’échange possédant l’id ’000056422’, l’id d’expéditeur ’12345678       ’ et l’id de destinataire ’87654321       ’ est interrompu avec les erreurs suivantes : « Le type de document du message est inconnu, et n’a pas été résolu en l’un des schémas existants configurés dans l’accord. »</span><span class="sxs-lookup"><span data-stu-id="b0237-165">The X12 transaction set with id '564220001' contained in functional group with id '56422', in interchange with id '000056422', with sender id '12345678       ', receiver id '87654321       ' is being suspended with following errors "The message has an unknown document type and did not resolve to any of the existing schemas configured in the agreement"</span></span> |
| <span data-ttu-id="b0237-166">Action requise</span><span class="sxs-lookup"><span data-stu-id="b0237-166">User action</span></span> | <span data-ttu-id="b0237-167">Configurez le schéma dans les paramètres d’accord.</span><span class="sxs-lookup"><span data-stu-id="b0237-167">Configure schema in the agreement settings</span></span>  |
|   |   |

### <a name="-incorrect-schema-in-the-agreement"></a><span data-ttu-id="b0237-168">* Schéma incorrect dans l’accord</span><span class="sxs-lookup"><span data-stu-id="b0237-168">* Incorrect schema in the agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="b0237-169">Description de l’erreur</span><span class="sxs-lookup"><span data-stu-id="b0237-169">Error description</span></span> | <span data-ttu-id="b0237-170">Le type de document du message est inconnu, et n’a pas été résolu en l’un des schémas existants configurés dans l’accord.</span><span class="sxs-lookup"><span data-stu-id="b0237-170">The message has an unknown document type and did not resolve to any of the existing schemas configured in the agreement.</span></span> |
| <span data-ttu-id="b0237-171">Action requise</span><span class="sxs-lookup"><span data-stu-id="b0237-171">User action</span></span> | <span data-ttu-id="b0237-172">Configurez le schéma correct dans les paramètres d’accord.</span><span class="sxs-lookup"><span data-stu-id="b0237-172">Configure correct schema in the agreement settings</span></span>  |
|   |   |

## <a name="flat-file"></a><span data-ttu-id="b0237-173">Fichier plat</span><span class="sxs-lookup"><span data-stu-id="b0237-173">Flat file</span></span>

### <a name="-input-message-with-no-body"></a><span data-ttu-id="b0237-174">* Message d’entrée sans corps</span><span class="sxs-lookup"><span data-stu-id="b0237-174">* Input message with no body</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="b0237-175">Description de l’erreur</span><span class="sxs-lookup"><span data-stu-id="b0237-175">Error description</span></span> | <span data-ttu-id="b0237-176">Modèle non valide.</span><span class="sxs-lookup"><span data-stu-id="b0237-176">InvalidTemplate.</span></span> <span data-ttu-id="b0237-177">Impossible de traiter les expressions de langage de gabarit dans les entrées d’action ’Flat_File_Decoding’ à la ligne « 1 » et à la colonne « 1902 » : La propriété « content » requise attend une valeur, mais a reçu null.</span><span class="sxs-lookup"><span data-stu-id="b0237-177">Unable to process template language expressions in action 'Flat_File_Decoding' inputs at line '1' and column '1902': 'Required property 'content' expects a value but got null.</span></span> <span data-ttu-id="b0237-178">Chemin d’accès « . ».</span><span class="sxs-lookup"><span data-stu-id="b0237-178">Path ''.'.</span></span> |
| <span data-ttu-id="b0237-179">Action requise</span><span class="sxs-lookup"><span data-stu-id="b0237-179">User action</span></span> | <span data-ttu-id="b0237-180">Cette erreur indique que le message d’entrée ne contient pas de corps.</span><span class="sxs-lookup"><span data-stu-id="b0237-180">This error indicates the input message does not contain a body</span></span> |
|   |   | 

## <a name="learn-more"></a><span data-ttu-id="b0237-181">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="b0237-181">Learn more</span></span>
[<span data-ttu-id="b0237-182">En savoir plus sur Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="b0237-182">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md)