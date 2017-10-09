---
title: "aaaExamples & communs scénarios - Azure Logic Apps | Documents Microsoft"
description: "Découvrez les applications logiques grâce à des exemples, des scénarios et des didacticiels."
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: e06311bc-29eb-49df-9273-1f05bbb2395c
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/9/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 17caa8539ec6a57726b9c6c07a71fb74caa07ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="examples-and-common-scenarios-for-azure-logic-apps"></a>Exemples et scénarios courants relatifs à Azure Logic Apps

toohelp vous en savoir plus sur Bonjour plusieurs modèles et fonctionnalités dans Azure Logic Apps, Voici des exemples et des scénarios courants.

## <a name="key-scenarios-for-logic-apps"></a>Scénarios clés relatifs aux applications logiques

Azure Logic Apps assure une orchestration et une intégration résilientes pour différents services. service d’applications de la logique de Hello est « sans serveur », vous n’avez pas tooworry relatives à l’échelle ou instances - vous avez toodo ne définir hello workflow (déclencheur et actions). plateforme sous-jacente de Hello gère la mise à l’échelle, la disponibilité et performances. N’importe quel scénario dans lequel vous devez toocoordinate plusieurs actions, plus particulièrement sur plusieurs systèmes, est une bonne cas d’utilisation pour Azure Logic Apps. Voici quelques modèles et exemples.

## <a name="respond-tootriggers-and-extend-actions"></a>Répondre tootriggers et étendre des actions

Chaque application logique commence avec un déclencheur. Par exemple, votre flux de travail peut commencer par un événement de planification, un appel manuels ou un événement à partir d’un système externe, par exemple hello « lorsqu’un fichier est ajouté tooan FTP serveur » de déclencheur. Azure Logic Apps prend actuellement en charge plus de 100 connecteurs prêt à l’emploi, allant de local SAP tooMicrosoft cognitifs Services. Pour les systèmes et services pour lesquels aucun connecteur n’a été publié, vous pouvez également étendre les applications logiques.

* [Créer des actions ou des déclencheurs personnalisés](../logic-apps/logic-apps-create-api-app.md)
* [Configurer des actions de longue durée pour les exécutions de flux de travail](../logic-apps/logic-apps-create-api-app.md)
* [Répondre tooexternal événements et actions avec webhooks](../logic-apps/logic-apps-create-api-app.md)
* [Appelez, déclencheur, ou imbriquer des flux de travail avec les réponses synchrones tooHTTP demandes](../logic-apps/logic-apps-http-endpoint.md)
* [Didacticiel : Répondre tooTwilio SMS webhooks et envoyer une réponse de texte](https://channel9.msdn.com/Blogs/Windows-Azure/Azure-Logic-Apps-Walkthrough-Webhook-Functions-and-an-SMS-Bot)
* [Didacticiel expliquant comment créer un tableau de bord social reposant sur l’intelligence artificielle en quelques minutes avec Logic Apps et Power BI](http://aka.ms/logicappsdemo)

## <a name="error-handling-logging-and-control-flow-capabilities"></a>Gestion des erreurs, journalisation et fonctionnalités de flux de contrôle

Les applications logiques incluent de puissantes fonctionnalités de flux de contrôle avancé, notamment des conditions, des commutateurs, des boucles et des étendues. les solutions résilient tooensure, vous pouvez également implémenter erreur et gestion des exceptions dans vos workflows. Pour la notification et les journaux de diagnostic relatifs à l’état d’exécution des flux de travail, Azure Logic Apps fournit également la surveillance et des alertes.

* [Effectuer différentes actions avec les instructions switch](../logic-apps/logic-apps-switch-case.md)
* [Traiter les éléments dans des tableaux et collections avec des boucles et des lots dans les applications logiques](../logic-apps/logic-apps-loops-and-scopes.md)
* [Gestion des erreurs de création et des exceptions dans un flux de travail](../logic-apps/logic-apps-exception-handling.md)
* [Activer la surveillance, la journalisation et les alertes pour les applications logiques existantes](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [Activer la surveillance et la journalisation des diagnostics lors de la création d’applications logiques](../logic-apps/logic-apps-monitor-your-logic-apps-oms.md)
* [Cas d’utilisation : comment un prestataire de soins de santé utilise la gestion des exceptions d’application logique pour les flux de travail HL7 FHIR](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)

## <a name="deploy-and-manage-logic-apps"></a>Déployer et gérer des applications logiques

Vous pouvez développer et déployer des applications logiques entièrement avec Visual Studio, Visual Studio Team Services ou tout autre outil de compilation automatisée et contrôle de code source. déploiement toosupport pour les connexions dépendantes dans un modèle de ressource et les flux de travail, les applications de logique utilisent des modèles de déploiement de ressources Azure. Visual Studio tools génère automatiquement ces modèles, vous pouvez vérifier dans le contrôle toosource pour le contrôle de version.

* [Créer un modèle de déploiement automatisé](../logic-apps/logic-apps-create-deploy-template.md)
* [Créer et déployer des applications logiques à partir de Visual Studio](../logic-apps/logic-apps-deploy-from-vs.md)
* [Surveiller la santé de vos applications logique hello](../logic-apps/logic-apps-monitor-your-logic-apps.md)

## <a name="content-types-conversions-and-transformations-within-a-run"></a>Types de contenu, conversions et transformations d’une exécution

Vous pouvez accéder, convertir et transformer plusieurs types de contenu à l’aide de hello de nombreuses fonctions Bonjour Azure Logic Apps [langage de définition de flux de travail](http://aka.ms/logicappsdocs). Par exemple, vous pouvez convertir entre une chaîne, JSON et XML avec hello `@json()` et `@xml()` les expressions de flux de travail. moteur de Logic Apps Hello conserve le transfert de contenu toosupport types de contenu de manière sans perte entre les services.

* [Gérer les types de contenu non-JSON](../logic-apps/logic-apps-content-type.md), comme `application/xml`, `application/octet-stream` et`multipart/formdata`
* [Fonctionnement des expressions de flux de travail dans les applications logiques](../logic-apps/logic-apps-author-definitions.md)
* [Référence : Langage de définition de flux de travail Azure Logic Apps](http://aka.ms/logicappsdocs)

## <a name="other-integrations-and-capabilities"></a>Autres intégrations et fonctionnalités

Les applications logiques offrent également une intégration avec de nombreux services comme Azure Functions, la Gestion des API Azure, Azure App Services et les points de terminaison HTTP personnalisés, par exemple, REST et SOAP.

* [Créer un tableau de bord social en temps réel avec Azure Serverless](../logic-apps/logic-apps-scenario-social-serverless.md)
* [Appeler Azure Functions à partir d’applications logiques](../logic-apps/logic-apps-azure-functions.md)
* [Scénario : Déclencher des applications logiques avec Azure Functions](../logic-apps/logic-apps-scenario-function-sb-trigger.md)
* [Blog : Appeler des points de terminaison SOAP à partir d’applications logiques](https://blogs.msdn.microsoft.com/logicapps/2016/04/07/using-soap-services-with-logic-apps/)

## <a name="end-to-end-scenarios"></a>Scénarios de bout en bout

* [Livre blanc : Gestion de cas de bout en bout d’intégration d’entreprise avec des services Azure, tels que des applications logiques](https://aka.ms/enterprise-integration-e2e-case-management-utilities-logic-apps)

## <a name="next-steps"></a>Étapes suivantes

- [Gérer les erreurs et les exceptions dans Azure Logic Apps](../logic-apps/logic-apps-exception-handling.md)
- [Créer des définitions de flux de travail avec le langage de définition de flux de travail hello](../logic-apps/logic-apps-author-definitions.md)
- [Envoyer vos questions, commentaires ou suggestions concernant les améliorations que nous pourrions apporter à Azure Logic Apps](https://feedback.azure.com/forums/287593-logic-apps)