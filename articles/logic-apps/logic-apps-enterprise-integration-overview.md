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
# <a name="overview-b2b-scenarios-and-communication-with-hello-enterprise-integration-pack"></a>Vue d’ensemble : Les scénarios B2B et de la communication avec hello Pack d’intégration Enterprise

Pour les workflows d’entreprise-entreprise (B2B) et une communication transparente avec Azure Logic Apps, vous pouvez activer des scénarios d’intégration d’entreprise avec la solution de nuage de Microsoft, hello Pack d’intégration Enterprise. Les entreprises peuvent échanger des messages électroniques, même si elles utilisent des formats et des protocoles différents. pack de Hello transforme des formats différents dans un format que les systèmes de l’organisation peuvent interpréter et de traiter. Les entreprises peuvent échanger des messages via des protocoles standard, notamment [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md) et [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md). Vous pouvez également sécuriser les messages grâce au chiffrement et aux signatures numériques.

Si vous êtes familiarisé avec BizTalk Server ou Microsoft Azure BizTalk Services, fonctionnalités d’intégration d’entreprise hello sont toouse facile, car la plupart des concepts sont similaires. Une différence majeure est que l’intégration d’entreprise utilise gestion des artefacts utilisés dans les communications B2B et stockage de l’intégration des comptes toosimplify hello. 

Point de vue architectural, hello Pack d’intégration Enterprise est basé sur « comptes intégration ». Ces comptes sont des conteneurs basés sur le cloud qui stockent tous vos artefacts, tels que les schémas, les partenaires, les certificats, les mappages et les contrats. Vous pouvez utiliser ces toodesign d’artefacts, déployer et maintenir les applications B2B et également toobuild B2B de flux de travail pour les applications de la logique. Mais avant de pouvoir utiliser ces artefacts, vous devez d’abord lier votre application de la logique de l’intégration compte tooyour. Ainsi, votre application logique pourra accéder aux artefacts de votre compte d’intégration.

## <a name="why-should-you-use-enterprise-integration"></a>Pourquoi utiliser l'intégration d’entreprise ?

* Grâce à l’intégration d’entreprise, vous pouvez stocker tous vos artefacts dans un même endroit : votre compte d’intégration.
* Vous pouvez générer des flux de travail B2B et intégrer des logiciels en tant que service (SaaS) applications tierces, les applications locales et les applications personnalisées à l’aide du moteur de Azure Logic Apps hello et tous les connecteurs de son.
* Vous pouvez créer un code personnalisé pour vos applications logiques avec Azure Functions.

## <a name="how-tooget-started-with-enterprise-integration"></a>Comment tooget démarrer avec l’intégration de l’entreprise ?

Vous pouvez créer et gérer les applications B2B avec hello Pack d’intégration Enterprise via le Concepteur d’application logique de hello Bonjour **portail Azure**. Vous pouvez également gérer vos applications logiques avec [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Rubriques PowerShell sur les applications logiques").

Voici les étapes principales hello que vous devez prendre avant de pouvoir créer des applications Bonjour portail Azure :

![image de présentation](media/logic-apps-enterprise-integration-overview/overview-0.png)  

## <a name="what-are-some-common-scenarios"></a>Quels sont les scénarios courants ?

Enterprise Integration prend en charge les normes suivantes :

* EDI - Electronic Data Interchange
* EAI - Enterprise Application Integration

## <a name="heres-what-you-need-tooget-started"></a>Voici ce que vous devez tooget démarré

* Un abonnement Azure avec un compte d’intégration
* Visual Studio 2015 toocreate mappages et schémas
* [Microsoft Azure Logic Apps Enterprise Integration Tools for Visual Studio 2015 2.0](https://aka.ms/vsmapsandschemas)  

## <a name="try-it-now"></a>Essayez-le dès maintenant

[Déployer un envoi de AS2 exemple complètement opérationnel & application logique de réception](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) qui utilise les fonctions hello B2B pour Azure Logic Apps.

## <a name="learn-more"></a>En savoir plus
* [Accords](../logic-apps/logic-apps-enterprise-integration-agreements.md "Découvrez les contrats d’intégration d’entreprise")
* [Scénarios d’entreprise tooBusiness (B2B)](../logic-apps/logic-apps-enterprise-integration-b2b.md "apprendre comment toocreate Logic apps avec les fonctionnalités de B2B")  
* [Certificats](logic-apps-enterprise-integration-certificates.md "Découvrez les certificats d’intégration d’entreprise")
* [Plats fichier codage/décodage](logic-apps-enterprise-integration-flatfile.md "apprendre comment tooencode et décoder le contenu du fichier plat")  
* [Comptes d’intégration](../logic-apps/logic-apps-enterprise-integration-accounts.md "En savoir plus sur les comptes d’intégration")
* [Mappages](../logic-apps/logic-apps-enterprise-integration-maps.md "Découvrez les mappages d’intégration d’entreprise")
* [Partenaires](logic-apps-enterprise-integration-partners.md "Découvrez les partenaires d’intégration d’entreprise")
* [Schémas](logic-apps-enterprise-integration-schemas.md "Découvrez les schémas d’intégration d’entreprise")
* [Validation des messages XML](logic-apps-enterprise-integration-xml.md "savoir comment les messages toovalidate XML avec Logic apps")
* [Transformation XML](logic-apps-enterprise-integration-transform.md "Découvrez les mappages d’intégration d’entreprise")
* [Connecteurs d'intégration d’entreprise](../connectors/apis-list.md "En savoir plus sur les connecteurs Enterprise Integration Pack")
* [Métadonnées du compte d'intégration](../logic-apps/logic-apps-enterprise-integration-metadata.md "En savoir plus sur les métadonnées du compte d’intégration")
* [Suivi des messages B2B](logic-apps-monitor-b2b-message.md "En savoir plus sur le suivi des messages B2B")
* [Suivi des messages B2B dans le portail OMS](logic-apps-track-b2b-messages-omsportal.md "En savoir plus sur le suivi des messages B2B dans le portail OMS")

