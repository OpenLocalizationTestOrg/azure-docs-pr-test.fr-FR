---
title: aaaWorking avec XML des messages dans votre flux de travail - Azure Logic Apps | Documents Microsoft
description: "Traiter, valider, transformer et enrichir XML messages dans les applications de la logique et à l’aide de l’entreprise-tooscenarios hello Pack d’intégration Enterprise"
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
ms.openlocfilehash: f90ae89fef0a4bd17286adbce398e573940bb790
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="validate-and-transform-xml-encode-and-decode-flat-files-and-enrich-messages-features-in-logic-apps"></a><span data-ttu-id="6ac1a-103">Validation et transformation XML, codage et décodage de fichiers plats et enrichissement des fonctionnalités des messages dans les applications logiques</span><span class="sxs-lookup"><span data-stu-id="6ac1a-103">Validate and transform XML, encode and decode flat files, and enrich messages features in logic apps</span></span>

<span data-ttu-id="6ac1a-104">À l’aide d’applications de la logique, vous disposez des messages hello capacité tooprocess XML que vous envoyez et recevez.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-104">Using logic apps, you have hello ability tooprocess XML messages that you send and receive.</span></span> <span data-ttu-id="6ac1a-105">Cette fonctionnalité est fournie avec hello Pack d’intégration Enterprise.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-105">This feature is included with hello Enterprise Integration Pack.</span></span> <span data-ttu-id="6ac1a-106">Pour les utilisateurs avec un arrière-plan de BizTalk Server, hello Pack d’intégration Enterprise vous donne tootransform de capacités similaires et valider les messages, travailler avec des fichiers plats et même utiliser XPath tooenrich ou extraire des propriétés spécifiques d’un message.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-106">For those users with a BizTalk Server background, hello Enterprise Integration Pack gives you similar abilities tootransform and validate messages, work with flat files, and even use XPath tooenrich or extract specific properties from a message.</span></span> 

<span data-ttu-id="6ac1a-107">Pour les utilisateurs qui sont le nouvel espace toothis, ces fonctionnalités développez vous comment traitez les messages au sein de votre flux de travail.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-107">For those users who are new toothis space, these features expand how you process messages within your workflow.</span></span> <span data-ttu-id="6ac1a-108">Par exemple, si vous êtes dans un scénario d’entreprise-entreprise et travaillez avec des schémas XML spécifiques, vous pouvez ensuite utiliser hello Pack d’intégration Enterprise tooenhance comment votre société traite ces messages.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-108">For example, if you are in a business-to-business scenario, and work with specific XML schemas, then you can use hello Enterprise Integration Pack tooenhance how your company processes these messages.</span></span> 

<span data-ttu-id="6ac1a-109">Hello Pack d’intégration Enterprise comprend :</span><span class="sxs-lookup"><span data-stu-id="6ac1a-109">hello Enterprise Integration Pack includes:</span></span> 

* <span data-ttu-id="6ac1a-110">[Validation XML](logic-apps-enterprise-integration-xml-validation.md "En savoir plus sur la validation de messages XML") : permet de valider un message XML entrant ou sortant par rapport à un schéma spécifique.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-110">[XML validation](logic-apps-enterprise-integration-xml-validation.md "Learn about XML message validation") - Validate an incoming or outgoing XML message against a specific schema.</span></span>
* <span data-ttu-id="6ac1a-111">[Transformation XML](../logic-apps/logic-apps-enterprise-integration-transform.md "en savoir plus sur les transformations de message XML et des mappages") - convertir ou personnaliser un message XML en fonction de vos exigences ou des spécifications hello d’un partenaire.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-111">[XML transform](../logic-apps/logic-apps-enterprise-integration-transform.md "Learn about XML message transformations and maps") - Convert or customize an XML message based on your requirements, or hello requirements of a partner.</span></span>
* <span data-ttu-id="6ac1a-112">[Encodage et décodage de fichier plat](logic-apps-enterprise-integration-flatfile.md "En savoir plus sur l’encodage/décodage de fichier plat") : permet de coder ou décoder un fichier plat.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-112">[Flat file encoding and flat file decoding](logic-apps-enterprise-integration-flatfile.md "Learn about flat file encoding/decoding") - Encode or decode a flat file.</span></span> <span data-ttu-id="6ac1a-113">Par exemple, SAP accepte et envoie des fichiers IDOC dans un format de fichier plat.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-113">For example, SAP accepts and sends IDOC files in flat file format.</span></span> <span data-ttu-id="6ac1a-114">De nombreuses plates-formes d’intégration créent des messages XML, y compris Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-114">Many integration platforms create XML messages, including Logic Apps.</span></span> <span data-ttu-id="6ac1a-115">Par conséquent, vous pouvez créer une application de la logique qu’encodeur de fichier plat hello utilise trop « convert » tooflat de fichiers XML.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-115">So, you can create a logic app that uses hello flat file encoder too"convert" XML files tooflat files.</span></span> 
* <span data-ttu-id="6ac1a-116">[XPath](https://msdn.microsoft.com/library/mt643789.aspx) - enrichir un message et extraire des propriétés spécifiques à partir du message de type hello.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-116">[XPath](https://msdn.microsoft.com/library/mt643789.aspx) - Enrich a message and extract specific properties from hello message.</span></span> <span data-ttu-id="6ac1a-117">Vous pouvez ensuite utiliser hello extrait les propriétés tooroute hello message tooa destination ou un point de terminaison intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-117">You can then use hello extracted properties tooroute hello message tooa destination, or an intermediary endpoint.</span></span>

## <a name="try-it-out"></a><span data-ttu-id="6ac1a-118">Faites un essai</span><span class="sxs-lookup"><span data-stu-id="6ac1a-118">Try it out</span></span>
<span data-ttu-id="6ac1a-119">[Déployer une application entièrement opérationnelle logique ](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (exemple GitHub) à l’aide des fonctionnalités XML de hello dans Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-119">[Deploy a fully operational logic app ](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (GitHub sample) by using hello XML features in Azure Logic Apps.</span></span>

## <a name="learn-more"></a><span data-ttu-id="6ac1a-120">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="6ac1a-120">Learn more</span></span>
[<span data-ttu-id="6ac1a-121">En savoir plus sur hello Pack d’intégration Enterprise</span><span class="sxs-lookup"><span data-stu-id="6ac1a-121">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "en savoir plus sur le Pack d’intégration Enterprise")
