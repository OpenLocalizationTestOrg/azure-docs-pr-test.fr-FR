---
title: "les applications aaaConnect et intégrer les données des flux de travail - Azure Logic Apps | Documents Microsoft"
description: "Créer des flux de travail et automatisez les processus en connectant des applications et en intégrant des données avec Azure Logic Apps."
author: kevinlam1
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 07765c05-72a6-4169-a8ab-f6420bfbaf07
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/23/2017
ms.author: klam
ms.openlocfilehash: 53d4e165bb2205ddd56c1950719389725267ddea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-logic-apps"></a>Qu'est-ce qu'une application logique ?
Logic Apps fournissent un moyen toosimplify et implémentent des intégrations évolutives et flux de travail dans le cloud de hello. Il fournit un toomodel concepteur visuel et automatiser votre processus comme une série d’étapes connu comme un flux de travail.  Il n’y [de connecteurs](../connectors/apis-list.md) entre tooquickly de cloud et locales hello s’intègrent à plusieurs services et protocoles.  Une application logique commence par un déclencheur (par exemple, « quand un compte est ajouté tooDynamics CRM ») et après le déclenchement de l’événement peut commencer plusieurs combinaisons d’actions, les conversions et logique de la condition.

avantages de Hello de l’utilisation de Logic Apps hello suivants :  

* Gagner du temps en concevant des processus complexes à l’aide des outils de conception toounderstand facile
* L’implémentation de modèles et les flux de travail en toute transparence, qui seraient difficile tooimplement dans le code
* Mise en route rapide à partir de modèles
* Personnalisation de votre application logique avec vos propres API, lignes de code et actions personnalisées
* Se connecter et synchroniser différents systèmes locaux et hello cloud
* Exploitation du serveur BizTalk, de Gestion des API, d’Azure Functions et d’Azure Service Bus avec la prise en charge d’une intégration de premier plan

Logique d’applications est un iPaaS entièrement géré (intégration de plateforme en tant que Service) permettant aux développeurs pas toohave tooworry sur la création d’hébergement, de l’évolutivité, de disponibilité et de gestion.  Logique d’applications sera montée en puissance à la demande toomeet automatiquement.

![Concepteur d’application de flux](media/logic-apps-what-are-logic-apps/LogicAppCapture2.png)

Comme indiqué, Logic Apps vous permet d’automatiser vos processus métier. Voici quelques exemples :  

* Déplacer les fichiers téléchargement serveur FTP de tooan dans le stockage Azure
* Traitement et routage de commandes sur différents systèmes locaux et systèmes cloud
* Analyser tous les tweets sur une rubrique donnée, l’analyse des sentiments de hello et créer des alertes et des tâches pour qu’il soit nécessaire du suivi des éléments.

Scénarios suivants peuvent être configurées à partir de concepteur visuel de hello et sans écrire une seule ligne de code. Commencez dès maintenant à [générer votre application logique][create].  Une fois écrite, une application logique peut être [rapidement déployée et reconfigurée](../logic-apps/logic-apps-create-deploy-template.md) dans plusieurs environnements et régions.

## <a name="why-logic-apps"></a>Pourquoi des applications logiques ?
Logique d’applications met la vitesse et l’évolutivité dans l’espace de l’intégration d’entreprise hello.  Hello convivialité du concepteur hello, plusieurs déclencheurs disponibles et les actions et les outils de gestion performante vous centraliser vos API plus simple que jamais.  Comme les entreprises vous rapprocher de numérisation, Logic Apps vous permet de tooconnect des systèmes hérités et pointe ensemble.

En outre, avec notre [compte d’intégration Enterprise] [ biztalk] vous pouvez faire évoluer des scénarios d’intégration toomature disposant d’une puissance de hello un [messagerie XML] [ xml], [gestion des partenaires commerciaux][tpm]et bien plus encore.

* **Outils de conception simple toouse** -Logic Apps peuvent être conçus de bout en bout dans le navigateur de hello ou avec les outils Visual Studio. Démarrez avec un déclencheur - à partir d’un toowhen calendrier simple qu'un problème de GitHub est créé. Puis orchestrer n’importe quel nombre d’actions à l’aide de la galerie de riches hello des connecteurs.
* **Se connecter facilement des API** -tâches de composition même toodescribe facile sont tooimplement difficile dans le code. Logique d’applications rend tooconnect facilement des systèmes hétérogènes. Choix tooconnect votre cloud marketing solution tooyour local système de facturation ? Vous souhaitez toocentralize sur les systèmes avec un Bus de Service d’entreprise et les API de messagerie ? Les applications logique présente des problèmes de toothese hello plus rapide et plus fiable de façon toodeliver solutions.
* **Commencer rapidement à partir de modèles** -toohelp de commencer, nous vous avons fourni un [galerie de modèles] [ templates] qui permettent de toorapidly créer des solutions courantes. D’avancée des solutions B2B toosimple SaaS connectivité et même quelques « pour vous amuser' ; la galerie de hello est tooget de manière plus rapide hello en main de power hello de Logic Apps.
* **Extensibilité intégrée dans** -ne pas voir connecteur hello vous avez besoin ? Logique d’applications est conçue toowork avec vos propres API et le code ; Vous pouvez facilement créer votre propre toouse d’application API comme un connecteur personnalisé ou appellent une [Azure fonction](https://functions.azure.com) tooexecute des extraits de code à la demande. 
* **Une réelle puissance d’intégration** : commencez en douceur et évoluez selon vos besoins. Logique d’applications permettre facilement tirer parti de hello puissance de BizTalk, industrie au début solution tooenable intégration professionnels toobuild hello solutions d’intégration de Microsoft dont ils ont besoin. En savoir plus sur hello [Pack d’intégration Enterprise](../logic-apps/logic-apps-enterprise-integration-overview.md).

## <a name="logic-app-concepts"></a>Concepts d'application logique
Hello Voici quelques-uns des éléments clés hello qui composent l’expérience de Logic Apps hello. 

* **Flux de travail** -Logic Apps fournit un moyen graphique de toomodel vos processus d’entreprise comme une série d’étapes ou d’un flux de travail.
* **Gérés connecteurs** -vos applications logiques besoin d’accès toodata et services. Connecteurs gérés sont créés spécifiquement tooaid vous lorsque vous vous connectez tooand fonctionne avec vos données. Consultez la liste hello des connecteurs maintenant disponibles dans [gérés connecteurs][managedapis].
* **Déclencheurs** : certains connecteurs gérés peuvent également se comporter comme des déclencheurs. Un déclencheur démarre une nouvelle instance d’un workflow basé sur un événement spécifique, comme l’arrivée de hello d’un message électronique ou une modification de votre compte de stockage Azure.
* **Actions** -chaque étape après l’appel d’une action de déclencheur hello dans un flux de travail. En règle générale, chaque action mappe opération tooan sur votre connecteur géré ou les applications API personnalisée.
* **Enterprise Integration Pack** : pour les scénarios d’intégration plus élaborés, Logic Apps intègre des fonctionnalités de BizTalk. BizTalk est la plateforme d’intégration de Microsoft, leader sur le marché. connecteurs de pack d’intégration Enterprise Hello permettent tooeasily inclure la validation, de transformation et d’informations dans le flux de travail tooyour application logique.

## <a name="getting-started"></a>Mise en route
* tooget en main de Logic Apps, procédez comme hello [créer une application logique] [ create] didacticiel.  
* [Afficher des exemples et des scénarios courants](../logic-apps/logic-apps-examples-and-scenarios.md)
* [Logic Apps vous permet d’automatiser vos processus métiers](http://channel9.msdn.com/Events/Build/2016/T694) 
* [Découvrez comment tooIntegrate vos systèmes avec Logic Apps](http://channel9.msdn.com/Events/Build/2016/P462)

[biztalk]: logic-apps-enterprise-integration-accounts.md
[appservice]: ../app-service/app-service-value-prop-what-is.md
[create]: logic-apps-create-a-logic-app.md
[managedapis]: ../connectors/apis-list.md
[tpm]: logic-apps-enterprise-integration-accounts.md
[xml]: logic-apps-enterprise-integration-b2b.md
[templates]: logic-apps-use-logic-app-templates.md
