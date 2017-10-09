---
title: "aaaEnterprise intégration B2B - Azure Logic Apps | Documents Microsoft"
description: "Générer des flux de travail B2B et prend en charge les scénarios d’intégration d’entreprise pour les applications logique avec hello Pack d’intégration Enterprise"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: dd517c4d-1701-4247-b83c-183c4d8d8aae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8dc866533110b1d07f51cf446056d2ca5ce869ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-b2b-scenarios-and-communication-with-hello-enterprise-integration-pack"></a><span data-ttu-id="a3025-103">Vue d’ensemble : Les scénarios B2B et de la communication avec hello Pack d’intégration Enterprise</span><span class="sxs-lookup"><span data-stu-id="a3025-103">Overview: B2B scenarios and communication with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="a3025-104">Pour les workflows d’entreprise-entreprise (B2B) et une communication transparente avec Azure Logic Apps, vous pouvez activer des scénarios d’intégration d’entreprise avec la solution de nuage de Microsoft, hello Pack d’intégration Enterprise.</span><span class="sxs-lookup"><span data-stu-id="a3025-104">For business-to-business (B2B) workflows and seamless communication with Azure Logic Apps, you can enable enterprise integration scenarios with Microsoft's cloud-based solution, hello Enterprise Integration Pack.</span></span> <span data-ttu-id="a3025-105">Les entreprises peuvent échanger des messages électroniques, même si elles utilisent des formats et des protocoles différents.</span><span class="sxs-lookup"><span data-stu-id="a3025-105">Organizations can exchange messages electronically, even if they use different protocols and formats.</span></span> <span data-ttu-id="a3025-106">pack de Hello transforme des formats différents dans un format que les systèmes de l’organisation peuvent interpréter et de traiter.</span><span class="sxs-lookup"><span data-stu-id="a3025-106">hello pack transforms different formats into a format that organizations' systems can interpret and process.</span></span> <span data-ttu-id="a3025-107">Les entreprises peuvent échanger des messages via des protocoles standard, notamment [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md) et [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md).</span><span class="sxs-lookup"><span data-stu-id="a3025-107">Organizations can exchange messages through industry-standard protocols, including [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md), and [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md).</span></span> <span data-ttu-id="a3025-108">Vous pouvez également sécuriser les messages grâce au chiffrement et aux signatures numériques.</span><span class="sxs-lookup"><span data-stu-id="a3025-108">You can also secure messages with both encryption and digital signatures.</span></span>

<span data-ttu-id="a3025-109">Si vous êtes familiarisé avec BizTalk Server ou Microsoft Azure BizTalk Services, fonctionnalités d’intégration d’entreprise hello sont toouse facile, car la plupart des concepts sont similaires.</span><span class="sxs-lookup"><span data-stu-id="a3025-109">If you are familiar with BizTalk Server or Microsoft Azure BizTalk Services, hello Enterprise Integration features are easy toouse because most concepts are similar.</span></span> <span data-ttu-id="a3025-110">Une différence majeure est que l’intégration d’entreprise utilise gestion des artefacts utilisés dans les communications B2B et stockage de l’intégration des comptes toosimplify hello.</span><span class="sxs-lookup"><span data-stu-id="a3025-110">One major difference is that Enterprise Integration uses integration accounts toosimplify hello storage and management of artifacts used in B2B communications.</span></span> 

<span data-ttu-id="a3025-111">Point de vue architectural, hello Pack d’intégration Enterprise est basé sur « comptes intégration ».</span><span class="sxs-lookup"><span data-stu-id="a3025-111">Architecturally, hello Enterprise Integration Pack is based on "integration accounts".</span></span> <span data-ttu-id="a3025-112">Ces comptes sont des conteneurs basés sur le cloud qui stockent tous vos artefacts, tels que les schémas, les partenaires, les certificats, les mappages et les contrats.</span><span class="sxs-lookup"><span data-stu-id="a3025-112">These accounts are cloud-based containers that store all your artifacts, like schemas, partners, certificates, maps, and agreements.</span></span> <span data-ttu-id="a3025-113">Vous pouvez utiliser ces toodesign d’artefacts, déployer et maintenir les applications B2B et également toobuild B2B de flux de travail pour les applications de la logique.</span><span class="sxs-lookup"><span data-stu-id="a3025-113">You can use these artifacts toodesign, deploy, and maintain your B2B apps and also toobuild B2B workflows for logic apps.</span></span> <span data-ttu-id="a3025-114">Mais avant de pouvoir utiliser ces artefacts, vous devez d’abord lier votre application de la logique de l’intégration compte tooyour.</span><span class="sxs-lookup"><span data-stu-id="a3025-114">But before you can use these artifacts, you must first link your integration account tooyour logic app.</span></span> <span data-ttu-id="a3025-115">Ainsi, votre application logique pourra accéder aux artefacts de votre compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="a3025-115">After that, your logic app can access your integration account's artifacts.</span></span>

## <a name="why-should-you-use-enterprise-integration"></a><span data-ttu-id="a3025-116">Pourquoi utiliser l'intégration d’entreprise ?</span><span class="sxs-lookup"><span data-stu-id="a3025-116">Why should you use enterprise integration?</span></span>

* <span data-ttu-id="a3025-117">Grâce à l’intégration d’entreprise, vous pouvez stocker tous vos artefacts dans un même endroit : votre compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="a3025-117">With enterprise integration, you can store all your artifacts in one place -- your integration account.</span></span>
* <span data-ttu-id="a3025-118">Vous pouvez générer des flux de travail B2B et intégrer des logiciels en tant que service (SaaS) applications tierces, les applications locales et les applications personnalisées à l’aide du moteur de Azure Logic Apps hello et tous les connecteurs de son.</span><span class="sxs-lookup"><span data-stu-id="a3025-118">You can build B2B workflows and integrate with third-party software-as-service (SaaS) apps, on-premises apps, and custom apps by using hello Azure Logic Apps engine and all its connectors.</span></span>
* <span data-ttu-id="a3025-119">Vous pouvez créer un code personnalisé pour vos applications logiques avec Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="a3025-119">You can create custom code for your logic apps with Azure functions.</span></span>

## <a name="how-tooget-started-with-enterprise-integration"></a><span data-ttu-id="a3025-120">Comment tooget démarrer avec l’intégration de l’entreprise ?</span><span class="sxs-lookup"><span data-stu-id="a3025-120">How tooget started with enterprise integration?</span></span>

<span data-ttu-id="a3025-121">Vous pouvez créer et gérer les applications B2B avec hello Pack d’intégration Enterprise via le Concepteur d’application logique de hello Bonjour **portail Azure**.</span><span class="sxs-lookup"><span data-stu-id="a3025-121">You can build and manage B2B apps with hello Enterprise Integration Pack through hello Logic App Designer in hello **Azure portal**.</span></span> <span data-ttu-id="a3025-122">Vous pouvez également gérer vos applications logiques avec [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Rubriques PowerShell sur les applications logiques").</span><span class="sxs-lookup"><span data-stu-id="a3025-122">You can also manage your logic apps with [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Logic apps PowerShell topics").</span></span>

<span data-ttu-id="a3025-123">Voici les étapes principales hello que vous devez prendre avant de pouvoir créer des applications Bonjour portail Azure :</span><span class="sxs-lookup"><span data-stu-id="a3025-123">Here are hello high-level steps you must take before you can create apps in hello Azure portal:</span></span>

![image de présentation](media/logic-apps-enterprise-integration-overview/overview-0.png)  

## <a name="what-are-some-common-scenarios"></a><span data-ttu-id="a3025-125">Quels sont les scénarios courants ?</span><span class="sxs-lookup"><span data-stu-id="a3025-125">What are some common scenarios?</span></span>

<span data-ttu-id="a3025-126">Enterprise Integration prend en charge les normes suivantes :</span><span class="sxs-lookup"><span data-stu-id="a3025-126">Enterprise Integration supports these industry standards:</span></span>

* <span data-ttu-id="a3025-127">EDI - Electronic Data Interchange</span><span class="sxs-lookup"><span data-stu-id="a3025-127">EDI - Electronic Data Interchange</span></span>
* <span data-ttu-id="a3025-128">EAI - Enterprise Application Integration</span><span class="sxs-lookup"><span data-stu-id="a3025-128">EAI - Enterprise Application Integration</span></span>

## <a name="heres-what-you-need-tooget-started"></a><span data-ttu-id="a3025-129">Voici ce que vous devez tooget démarré</span><span class="sxs-lookup"><span data-stu-id="a3025-129">Here's what you need tooget started</span></span>

* <span data-ttu-id="a3025-130">Un abonnement Azure avec un compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="a3025-130">An Azure subscription with an integration account</span></span>
* <span data-ttu-id="a3025-131">Visual Studio 2015 toocreate mappages et schémas</span><span class="sxs-lookup"><span data-stu-id="a3025-131">Visual Studio 2015 toocreate maps and schemas</span></span>
* [<span data-ttu-id="a3025-132">Microsoft Azure Logic Apps Enterprise Integration Tools for Visual Studio 2015 2.0</span><span class="sxs-lookup"><span data-stu-id="a3025-132">Microsoft Azure Logic Apps Enterprise Integration Tools for Visual Studio 2015 2.0</span></span>](https://aka.ms/vsmapsandschemas)  

## <a name="try-it-now"></a><span data-ttu-id="a3025-133">Essayez-le dès maintenant</span><span class="sxs-lookup"><span data-stu-id="a3025-133">Try it now</span></span>

<span data-ttu-id="a3025-134">[Déployer un envoi de AS2 exemple complètement opérationnel & application logique de réception](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) qui utilise les fonctions hello B2B pour Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="a3025-134">[Deploy a fully operational sample AS2 send & receive logic app](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) that uses hello B2B features for Azure Logic Apps.</span></span>

## <a name="learn-more"></a><span data-ttu-id="a3025-135">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="a3025-135">Learn more</span></span>
* [<span data-ttu-id="a3025-136">Accords</span><span class="sxs-lookup"><span data-stu-id="a3025-136">Agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Découvrez les contrats d’intégration d’entreprise")
* [<span data-ttu-id="a3025-137">Scénarios d’entreprise tooBusiness (B2B)</span><span class="sxs-lookup"><span data-stu-id="a3025-137">Business tooBusiness (B2B) scenarios</span></span>](../logic-apps/logic-apps-enterprise-integration-b2b.md "apprendre comment toocreate Logic apps avec les fonctionnalités de B2B")  
* [<span data-ttu-id="a3025-138">Certificats</span><span class="sxs-lookup"><span data-stu-id="a3025-138">Certificates</span></span>](logic-apps-enterprise-integration-certificates.md "Découvrez les certificats d’intégration d’entreprise")
* [<span data-ttu-id="a3025-139">Plats fichier codage/décodage</span><span class="sxs-lookup"><span data-stu-id="a3025-139">Flat file encoding/decoding</span></span>](logic-apps-enterprise-integration-flatfile.md "apprendre comment tooencode et décoder le contenu du fichier plat")  
* [<span data-ttu-id="a3025-140">Comptes d’intégration</span><span class="sxs-lookup"><span data-stu-id="a3025-140">Integration accounts</span></span>](../logic-apps/logic-apps-enterprise-integration-accounts.md "En savoir plus sur les comptes d’intégration")
* [<span data-ttu-id="a3025-141">Mappages</span><span class="sxs-lookup"><span data-stu-id="a3025-141">Maps</span></span>](../logic-apps/logic-apps-enterprise-integration-maps.md "Découvrez les mappages d’intégration d’entreprise")
* [<span data-ttu-id="a3025-142">Partenaires</span><span class="sxs-lookup"><span data-stu-id="a3025-142">Partners</span></span>](logic-apps-enterprise-integration-partners.md "Découvrez les partenaires d’intégration d’entreprise")
* [<span data-ttu-id="a3025-143">Schémas</span><span class="sxs-lookup"><span data-stu-id="a3025-143">Schemas</span></span>](logic-apps-enterprise-integration-schemas.md "Découvrez les schémas d’intégration d’entreprise")
* [<span data-ttu-id="a3025-144">Validation des messages XML</span><span class="sxs-lookup"><span data-stu-id="a3025-144">XML message validation</span></span>](logic-apps-enterprise-integration-xml.md "savoir comment les messages toovalidate XML avec Logic apps")
* [<span data-ttu-id="a3025-145">Transformation XML</span><span class="sxs-lookup"><span data-stu-id="a3025-145">XML transform</span></span>](logic-apps-enterprise-integration-transform.md "Découvrez les mappages d’intégration d’entreprise")
* [<span data-ttu-id="a3025-146">Connecteurs d'intégration d’entreprise</span><span class="sxs-lookup"><span data-stu-id="a3025-146">Enterprise Integration Connectors</span></span>](../connectors/apis-list.md "En savoir plus sur les connecteurs Enterprise Integration Pack")
* [<span data-ttu-id="a3025-147">Métadonnées du compte d'intégration</span><span class="sxs-lookup"><span data-stu-id="a3025-147">Integration Account Metadata</span></span>](../logic-apps/logic-apps-enterprise-integration-metadata.md "En savoir plus sur les métadonnées du compte d’intégration")
* [<span data-ttu-id="a3025-148">Suivi des messages B2B</span><span class="sxs-lookup"><span data-stu-id="a3025-148">Monitor B2B messages</span></span>](logic-apps-monitor-b2b-message.md "En savoir plus sur le suivi des messages B2B")
* [<span data-ttu-id="a3025-149">Suivi des messages B2B dans le portail OMS</span><span class="sxs-lookup"><span data-stu-id="a3025-149">Tracking B2B messages in OMS portal</span></span>](logic-apps-track-b2b-messages-omsportal.md "En savoir plus sur le suivi des messages B2B dans le portail OMS")

