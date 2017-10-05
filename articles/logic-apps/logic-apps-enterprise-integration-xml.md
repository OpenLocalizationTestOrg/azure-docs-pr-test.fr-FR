---
title: Utilisation de messages XML dans vos flux de travail - Azure Logic Apps | Microsoft Docs
description: "Traitement, validation, transformation et enrichissement de messages XML dans les applications logiques et les scénarios d’entreprise à entreprise à l’aide de Enterprise Integration Pack"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 47672dc4-1caa-44e5-b8cb-68ec3a76b7dc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 02/27/2017
ms.author: LADocs; mandia
ms.openlocfilehash: 3fec4935f5317be4bf8c9e05f1c24a7c05381b1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="validate-and-transform-xml-encode-and-decode-flat-files-and-enrich-messages-features-in-logic-apps"></a><span data-ttu-id="b8eaa-103">Validation et transformation XML, codage et décodage de fichiers plats et enrichissement des fonctionnalités des messages dans les applications logiques</span><span class="sxs-lookup"><span data-stu-id="b8eaa-103">Validate and transform XML, encode and decode flat files, and enrich messages features in logic apps</span></span>

<span data-ttu-id="b8eaa-104">Les applications logiques vous permettent de traiter les messages XML envoyés et reçus.</span><span class="sxs-lookup"><span data-stu-id="b8eaa-104">Using logic apps, you have the ability to process XML messages that you send and receive.</span></span> <span data-ttu-id="b8eaa-105">Cette fonctionnalité est incluse dans Enterprise Integration Pack.</span><span class="sxs-lookup"><span data-stu-id="b8eaa-105">This feature is included with the Enterprise Integration Pack.</span></span> <span data-ttu-id="b8eaa-106">Pour les utilisateurs de BizTalk Server, Enterprise Integration Pack offre des capacités similaires pour transformer et valider des messages, utiliser des fichiers plats et même XPath pour enrichir ou extraire des propriétés spécifiques d’un message.</span><span class="sxs-lookup"><span data-stu-id="b8eaa-106">For those users with a BizTalk Server background, the Enterprise Integration Pack gives you similar abilities to transform and validate messages, work with flat files, and even use XPath to enrich or extract specific properties from a message.</span></span> 

<span data-ttu-id="b8eaa-107">Pour les utilisateurs qui découvrent cet environnement, ces fonctionnalités étendent les possibilités de traitement des messages au sein de votre flux de travail.</span><span class="sxs-lookup"><span data-stu-id="b8eaa-107">For those users who are new to this space, these features expand how you process messages within your workflow.</span></span> <span data-ttu-id="b8eaa-108">Par exemple, dans un scénario d’entreprise à entreprise où vous travaillez avec des schémas XML spécifiques, vous pouvez utiliser Enterprise Integration Pack pour améliorer la façon dont votre entreprise traite ces messages.</span><span class="sxs-lookup"><span data-stu-id="b8eaa-108">For example, if you are in a business-to-business scenario, and work with specific XML schemas, then you can use the Enterprise Integration Pack to enhance how your company processes these messages.</span></span> 

<span data-ttu-id="b8eaa-109">Enterprise Integration Pack inclut les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="b8eaa-109">The Enterprise Integration Pack includes:</span></span> 

* <span data-ttu-id="b8eaa-110">[Validation XML](logic-apps-enterprise-integration-xml-validation.md "En savoir plus sur la validation de messages XML") : permet de valider un message XML entrant ou sortant par rapport à un schéma spécifique.</span><span class="sxs-lookup"><span data-stu-id="b8eaa-110">[XML validation](logic-apps-enterprise-integration-xml-validation.md "Learn about XML message validation") - Validate an incoming or outgoing XML message against a specific schema.</span></span>
* <span data-ttu-id="b8eaa-111">[Transformation XML](../logic-apps/logic-apps-enterprise-integration-transform.md "En savoir plus sur les transformations et les mappages de message XML") : permet de convertir un message XML basé sur vos exigences ou celles d’un partenaire.</span><span class="sxs-lookup"><span data-stu-id="b8eaa-111">[XML transform](../logic-apps/logic-apps-enterprise-integration-transform.md "Learn about XML message transformations and maps") - Convert or customize an XML message based on your requirements, or the requirements of a partner.</span></span>
* <span data-ttu-id="b8eaa-112">[Encodage et décodage de fichier plat](logic-apps-enterprise-integration-flatfile.md "En savoir plus sur l’encodage/décodage de fichier plat") : permet de coder ou décoder un fichier plat.</span><span class="sxs-lookup"><span data-stu-id="b8eaa-112">[Flat file encoding and flat file decoding](logic-apps-enterprise-integration-flatfile.md "Learn about flat file encoding/decoding") - Encode or decode a flat file.</span></span> <span data-ttu-id="b8eaa-113">Par exemple, SAP accepte et envoie des fichiers IDOC dans un format de fichier plat.</span><span class="sxs-lookup"><span data-stu-id="b8eaa-113">For example, SAP accepts and sends IDOC files in flat file format.</span></span> <span data-ttu-id="b8eaa-114">De nombreuses plates-formes d’intégration créent des messages XML, y compris Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="b8eaa-114">Many integration platforms create XML messages, including Logic Apps.</span></span> <span data-ttu-id="b8eaa-115">Vous pouvez donc créer une application logique qui utilise l’encodeur de fichier plat afin de « convertir » des fichiers XML en fichiers plats.</span><span class="sxs-lookup"><span data-stu-id="b8eaa-115">So, you can create a logic app that uses the flat file encoder to "convert" XML files to flat files.</span></span> 
* <span data-ttu-id="b8eaa-116">[XPath](https://msdn.microsoft.com/library/mt643789.aspx) : permet d’enrichir un message et d’extraire des propriétés spécifiques du message.</span><span class="sxs-lookup"><span data-stu-id="b8eaa-116">[XPath](https://msdn.microsoft.com/library/mt643789.aspx) - Enrich a message and extract specific properties from the message.</span></span> <span data-ttu-id="b8eaa-117">Les propriétés extraites peuvent ensuite servir à acheminer le message vers une destination ou un point de terminaison intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="b8eaa-117">You can then use the extracted properties to route the message to a destination, or an intermediary endpoint.</span></span>

## <a name="try-it-out"></a><span data-ttu-id="b8eaa-118">Faites un essai</span><span class="sxs-lookup"><span data-stu-id="b8eaa-118">Try it out</span></span>
<span data-ttu-id="b8eaa-119">[Déployez votre propre application logique entièrement fonctionnelle](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (exemple GitHub) à l’aide des fonctionnalités XML d’Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="b8eaa-119">[Deploy a fully operational logic app ](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (GitHub sample) by using the XML features in Azure Logic Apps.</span></span>

## <a name="learn-more"></a><span data-ttu-id="b8eaa-120">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="b8eaa-120">Learn more</span></span>
[<span data-ttu-id="b8eaa-121">En savoir plus sur Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="b8eaa-121">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Découvrez Enterprise Integration Pack")
