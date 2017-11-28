---
title: "Intégration d’entreprise pour B2B - Azure Logic Apps | Microsoft Docs"
description: "Créer des workflows B2B et prendre en charge des scénarios d’intégration d’entreprise pour les applications logiques avec Enterprise Integration Pack"
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
ms.openlocfilehash: 9462707db03ecfcc3d5186ce7ded8655ad3bdcc9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="overview-b2b-scenarios-and-communication-with-the-enterprise-integration-pack"></a><span data-ttu-id="ff535-103">Vue d’ensemble : scénarios B2B et communication avec Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="ff535-103">Overview: B2B scenarios and communication with the Enterprise Integration Pack</span></span>

<span data-ttu-id="ff535-104">Dans le cadre des workflows entreprise-entreprise (B2B) et d’une communication transparente avec Azure Logic Apps, vous pouvez activer des scénarios d’intégration d’entreprise à l’aide d’une solution Microsoft basée sur le cloud : Enterprise Integration Pack.</span><span class="sxs-lookup"><span data-stu-id="ff535-104">For business-to-business (B2B) workflows and seamless communication with Azure Logic Apps, you can enable enterprise integration scenarios with Microsoft's cloud-based solution, the Enterprise Integration Pack.</span></span> <span data-ttu-id="ff535-105">Les entreprises peuvent échanger des messages électroniques, même si elles utilisent des formats et des protocoles différents.</span><span class="sxs-lookup"><span data-stu-id="ff535-105">Organizations can exchange messages electronically, even if they use different protocols and formats.</span></span> <span data-ttu-id="ff535-106">Le pack convertit les différents formats dans un format que les systèmes des entreprises peuvent interpréter et traiter.</span><span class="sxs-lookup"><span data-stu-id="ff535-106">The pack transforms different formats into a format that organizations' systems can interpret and process.</span></span> <span data-ttu-id="ff535-107">Les entreprises peuvent échanger des messages via des protocoles standard, notamment [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md) et [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md).</span><span class="sxs-lookup"><span data-stu-id="ff535-107">Organizations can exchange messages through industry-standard protocols, including [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md), and [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md).</span></span> <span data-ttu-id="ff535-108">Vous pouvez également sécuriser les messages grâce au chiffrement et aux signatures numériques.</span><span class="sxs-lookup"><span data-stu-id="ff535-108">You can also secure messages with both encryption and digital signatures.</span></span>

<span data-ttu-id="ff535-109">Si vous êtes familiarisé avec BizTalk Server ou Microsoft Azure BizTalk Services, vous saurez facilement utiliser les fonctionnalités Enterprise Integration, car la plupart des concepts sont similaires.</span><span class="sxs-lookup"><span data-stu-id="ff535-109">If you are familiar with BizTalk Server or Microsoft Azure BizTalk Services, the Enterprise Integration features are easy to use because most concepts are similar.</span></span> <span data-ttu-id="ff535-110">La principale différence réside dans le fait qu'Enterprise Integration utilise les comptes d’intégration pour simplifier le stockage et la gestion des artefacts utilisés dans les communications B2B.</span><span class="sxs-lookup"><span data-stu-id="ff535-110">One major difference is that Enterprise Integration uses integration accounts to simplify the storage and management of artifacts used in B2B communications.</span></span> 

<span data-ttu-id="ff535-111">D’un point de vue architectural, Enterprise Integration Pack est basé sur des « comptes d’intégration ».</span><span class="sxs-lookup"><span data-stu-id="ff535-111">Architecturally, the Enterprise Integration Pack is based on "integration accounts".</span></span> <span data-ttu-id="ff535-112">Ces comptes sont des conteneurs basés sur le cloud qui stockent tous vos artefacts, tels que les schémas, les partenaires, les certificats, les mappages et les contrats.</span><span class="sxs-lookup"><span data-stu-id="ff535-112">These accounts are cloud-based containers that store all your artifacts, like schemas, partners, certificates, maps, and agreements.</span></span> <span data-ttu-id="ff535-113">Vous pouvez utiliser ces artefacts pour concevoir, déployer et gérer vos applications B2B, mais aussi créer des workflows B2B pour les applications logiques.</span><span class="sxs-lookup"><span data-stu-id="ff535-113">You can use these artifacts to design, deploy, and maintain your B2B apps and also to build B2B workflows for logic apps.</span></span> <span data-ttu-id="ff535-114">Toutefois, avant de pouvoir utiliser ces artefacts, vous devez d’abord lier votre compte d’intégration à votre application logique.</span><span class="sxs-lookup"><span data-stu-id="ff535-114">But before you can use these artifacts, you must first link your integration account to your logic app.</span></span> <span data-ttu-id="ff535-115">Ainsi, votre application logique pourra accéder aux artefacts de votre compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="ff535-115">After that, your logic app can access your integration account's artifacts.</span></span>

## <a name="why-should-you-use-enterprise-integration"></a><span data-ttu-id="ff535-116">Pourquoi utiliser l'intégration d’entreprise ?</span><span class="sxs-lookup"><span data-stu-id="ff535-116">Why should you use enterprise integration?</span></span>

* <span data-ttu-id="ff535-117">Grâce à l’intégration d’entreprise, vous pouvez stocker tous vos artefacts dans un même endroit : votre compte d’intégration.</span><span class="sxs-lookup"><span data-stu-id="ff535-117">With enterprise integration, you can store all your artifacts in one place -- your integration account.</span></span>
* <span data-ttu-id="ff535-118">Vous pouvez créer des workflows B2B et les intégrer dans des applications SaaS tierces, des applications locales et des applications personnalisées à l’aide du moteur Azure Logic Apps et de tous ses connecteurs.</span><span class="sxs-lookup"><span data-stu-id="ff535-118">You can build B2B workflows and integrate with third-party software-as-service (SaaS) apps, on-premises apps, and custom apps by using the Azure Logic Apps engine and all its connectors.</span></span>
* <span data-ttu-id="ff535-119">Vous pouvez créer un code personnalisé pour vos applications logiques avec Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="ff535-119">You can create custom code for your logic apps with Azure functions.</span></span>

## <a name="how-to-get-started-with-enterprise-integration"></a><span data-ttu-id="ff535-120">Comment prendre en main Enterprise Integration Pack ?</span><span class="sxs-lookup"><span data-stu-id="ff535-120">How to get started with enterprise integration?</span></span>

<span data-ttu-id="ff535-121">Vous pouvez créer et gérer des applications B2B à l’aide d’Enterprise Integration Pack via le concepteur Logic Apps du **portail Azure**.</span><span class="sxs-lookup"><span data-stu-id="ff535-121">You can build and manage B2B apps with the Enterprise Integration Pack through the Logic App Designer in the **Azure portal**.</span></span> <span data-ttu-id="ff535-122">Vous pouvez également gérer vos applications logiques avec [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Rubriques PowerShell sur les applications logiques").</span><span class="sxs-lookup"><span data-stu-id="ff535-122">You can also manage your logic apps with [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Logic apps PowerShell topics").</span></span>

<span data-ttu-id="ff535-123">Voici les étapes de niveau supérieur permettant de créer des applications dans le portail Azure :</span><span class="sxs-lookup"><span data-stu-id="ff535-123">Here are the high-level steps you must take before you can create apps in the Azure portal:</span></span>

![image de présentation](media/logic-apps-enterprise-integration-overview/overview-0.png)  

## <a name="what-are-some-common-scenarios"></a><span data-ttu-id="ff535-125">Quels sont les scénarios courants ?</span><span class="sxs-lookup"><span data-stu-id="ff535-125">What are some common scenarios?</span></span>

<span data-ttu-id="ff535-126">Enterprise Integration prend en charge les normes suivantes :</span><span class="sxs-lookup"><span data-stu-id="ff535-126">Enterprise Integration supports these industry standards:</span></span>

* <span data-ttu-id="ff535-127">EDI - Electronic Data Interchange</span><span class="sxs-lookup"><span data-stu-id="ff535-127">EDI - Electronic Data Interchange</span></span>
* <span data-ttu-id="ff535-128">EAI - Enterprise Application Integration</span><span class="sxs-lookup"><span data-stu-id="ff535-128">EAI - Enterprise Application Integration</span></span>

## <a name="heres-what-you-need-to-get-started"></a><span data-ttu-id="ff535-129">Voici ce dont vous avez besoin pour commencer</span><span class="sxs-lookup"><span data-stu-id="ff535-129">Here's what you need to get started</span></span>

* <span data-ttu-id="ff535-130">Un abonnement Azure avec un compte d’intégration</span><span class="sxs-lookup"><span data-stu-id="ff535-130">An Azure subscription with an integration account</span></span>
* <span data-ttu-id="ff535-131">Visual Studio 2015 pour créer des mappages et des schémas</span><span class="sxs-lookup"><span data-stu-id="ff535-131">Visual Studio 2015 to create maps and schemas</span></span>
* [<span data-ttu-id="ff535-132">Microsoft Azure Logic Apps Enterprise Integration Tools for Visual Studio 2015 2.0</span><span class="sxs-lookup"><span data-stu-id="ff535-132">Microsoft Azure Logic Apps Enterprise Integration Tools for Visual Studio 2015 2.0</span></span>](https://aka.ms/vsmapsandschemas)  

## <a name="try-it-now"></a><span data-ttu-id="ff535-133">Essayez-le dès maintenant</span><span class="sxs-lookup"><span data-stu-id="ff535-133">Try it now</span></span>

<span data-ttu-id="ff535-134">[Déployez votre propre exemple d’application d’envoi et de réception AS2 entièrement fonctionnelle](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) utilisant les fonctionnalités B2B d’Azure Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="ff535-134">[Deploy a fully operational sample AS2 send & receive logic app](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) that uses the B2B features for Azure Logic Apps.</span></span>

## <a name="learn-more"></a><span data-ttu-id="ff535-135">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="ff535-135">Learn more</span></span>
* [<span data-ttu-id="ff535-136">Accords</span><span class="sxs-lookup"><span data-stu-id="ff535-136">Agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Découvrez les contrats d’intégration d’entreprise")
* [<span data-ttu-id="ff535-137">Scénarios Business to Business (B2B)</span><span class="sxs-lookup"><span data-stu-id="ff535-137">Business to Business (B2B) scenarios</span></span>](../logic-apps/logic-apps-enterprise-integration-b2b.md "Apprenez à créer des applications logiques avec fonctionnalités B2B")  
* [<span data-ttu-id="ff535-138">Certificats</span><span class="sxs-lookup"><span data-stu-id="ff535-138">Certificates</span></span>](logic-apps-enterprise-integration-certificates.md "Découvrez les certificats d’intégration d’entreprise")
* [<span data-ttu-id="ff535-139">Codage/décodage de fichier plat</span><span class="sxs-lookup"><span data-stu-id="ff535-139">Flat file encoding/decoding</span></span>](logic-apps-enterprise-integration-flatfile.md "Découvrez comment encoder et décoder le contenu d’un fichier plat")  
* [<span data-ttu-id="ff535-140">Comptes d’intégration</span><span class="sxs-lookup"><span data-stu-id="ff535-140">Integration accounts</span></span>](../logic-apps/logic-apps-enterprise-integration-accounts.md "En savoir plus sur les comptes d’intégration")
* [<span data-ttu-id="ff535-141">Mappages</span><span class="sxs-lookup"><span data-stu-id="ff535-141">Maps</span></span>](../logic-apps/logic-apps-enterprise-integration-maps.md "Découvrez les mappages d’intégration d’entreprise")
* [<span data-ttu-id="ff535-142">Partenaires</span><span class="sxs-lookup"><span data-stu-id="ff535-142">Partners</span></span>](logic-apps-enterprise-integration-partners.md "Découvrez les partenaires d’intégration d’entreprise")
* [<span data-ttu-id="ff535-143">Schémas</span><span class="sxs-lookup"><span data-stu-id="ff535-143">Schemas</span></span>](logic-apps-enterprise-integration-schemas.md "Découvrez les schémas d’intégration d’entreprise")
* [<span data-ttu-id="ff535-144">Validation de message XML</span><span class="sxs-lookup"><span data-stu-id="ff535-144">XML message validation</span></span>](logic-apps-enterprise-integration-xml.md "Découvrez comment valider des messages XML avec vos applications logiques")
* [<span data-ttu-id="ff535-145">Transformation XML</span><span class="sxs-lookup"><span data-stu-id="ff535-145">XML transform</span></span>](logic-apps-enterprise-integration-transform.md "Découvrez les mappages d’intégration d’entreprise")
* [<span data-ttu-id="ff535-146">Connecteurs d'intégration d’entreprise</span><span class="sxs-lookup"><span data-stu-id="ff535-146">Enterprise Integration Connectors</span></span>](../connectors/apis-list.md "En savoir plus sur les connecteurs Enterprise Integration Pack")
* [<span data-ttu-id="ff535-147">Métadonnées du compte d'intégration</span><span class="sxs-lookup"><span data-stu-id="ff535-147">Integration Account Metadata</span></span>](../logic-apps/logic-apps-enterprise-integration-metadata.md "En savoir plus sur les métadonnées du compte d’intégration")
* [<span data-ttu-id="ff535-148">Suivi des messages B2B</span><span class="sxs-lookup"><span data-stu-id="ff535-148">Monitor B2B messages</span></span>](logic-apps-monitor-b2b-message.md "En savoir plus sur le suivi des messages B2B")
* [<span data-ttu-id="ff535-149">Suivi des messages B2B dans le portail OMS</span><span class="sxs-lookup"><span data-stu-id="ff535-149">Tracking B2B messages in OMS portal</span></span>](logic-apps-track-b2b-messages-omsportal.md "En savoir plus sur le suivi des messages B2B dans le portail OMS")

