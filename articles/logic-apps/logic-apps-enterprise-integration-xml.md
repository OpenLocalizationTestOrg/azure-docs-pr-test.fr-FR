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
# <a name="validate-and-transform-xml-encode-and-decode-flat-files-and-enrich-messages-features-in-logic-apps"></a>Validation et transformation XML, codage et décodage de fichiers plats et enrichissement des fonctionnalités des messages dans les applications logiques

À l’aide d’applications de la logique, vous disposez des messages hello capacité tooprocess XML que vous envoyez et recevez. Cette fonctionnalité est fournie avec hello Pack d’intégration Enterprise. Pour les utilisateurs avec un arrière-plan de BizTalk Server, hello Pack d’intégration Enterprise vous donne tootransform de capacités similaires et valider les messages, travailler avec des fichiers plats et même utiliser XPath tooenrich ou extraire des propriétés spécifiques d’un message. 

Pour les utilisateurs qui sont le nouvel espace toothis, ces fonctionnalités développez vous comment traitez les messages au sein de votre flux de travail. Par exemple, si vous êtes dans un scénario d’entreprise-entreprise et travaillez avec des schémas XML spécifiques, vous pouvez ensuite utiliser hello Pack d’intégration Enterprise tooenhance comment votre société traite ces messages. 

Hello Pack d’intégration Enterprise comprend : 

* [Validation XML](logic-apps-enterprise-integration-xml-validation.md "En savoir plus sur la validation de messages XML") : permet de valider un message XML entrant ou sortant par rapport à un schéma spécifique.
* [Transformation XML](../logic-apps/logic-apps-enterprise-integration-transform.md "en savoir plus sur les transformations de message XML et des mappages") - convertir ou personnaliser un message XML en fonction de vos exigences ou des spécifications hello d’un partenaire.
* [Encodage et décodage de fichier plat](logic-apps-enterprise-integration-flatfile.md "En savoir plus sur l’encodage/décodage de fichier plat") : permet de coder ou décoder un fichier plat. Par exemple, SAP accepte et envoie des fichiers IDOC dans un format de fichier plat. De nombreuses plates-formes d’intégration créent des messages XML, y compris Logic Apps. Par conséquent, vous pouvez créer une application de la logique qu’encodeur de fichier plat hello utilise trop « convert » tooflat de fichiers XML. 
* [XPath](https://msdn.microsoft.com/library/mt643789.aspx) - enrichir un message et extraire des propriétés spécifiques à partir du message de type hello. Vous pouvez ensuite utiliser hello extrait les propriétés tooroute hello message tooa destination ou un point de terminaison intermédiaire.

## <a name="try-it-out"></a>Faites un essai
[Déployer une application entièrement opérationnelle logique ](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (exemple GitHub) à l’aide des fonctionnalités XML de hello dans Azure Logic Apps.

## <a name="learn-more"></a>En savoir plus
[En savoir plus sur hello Pack d’intégration Enterprise](../logic-apps/logic-apps-enterprise-integration-overview.md "en savoir plus sur le Pack d’intégration Enterprise")
