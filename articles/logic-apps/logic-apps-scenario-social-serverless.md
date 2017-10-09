---
title: "aaaScenario - créer un tableau de bord client insights avec Azure sans serveur | Documents Microsoft"
description: "Exemple de comment vous pouvez générer un client de toomanage du tableau de bord des commentaires, les données de réseaux sociale et bien plus encore avec Azure Logic Apps et fonctions de Azure."
keywords: 
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/29/2017
ms.author: jehollan
ms.openlocfilehash: db175e895e37aa795a9c34bf4d65566bf68f8c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-real-time-customer-insights-dashboard-with-azure-logic-apps-and-azure-functions"></a>Créer un tableau de bord Insights client en temps réel avec Azure Logic Apps et Azure Functions

Windows Azure tools sans fournissent des fonctionnalités puissantes tooquickly créer et héberger des applications dans le cloud de hello, sans avoir toothink sur l’infrastructure.  Dans ce scénario, nous sera créer un tableau de bord tootrigger des commentaires des clients, l’analyse des commentaires avec machine learning et publier insights une source comme Power BI ou Azure Data Lake.

## <a name="overview-of-hello-scenario-and-tools-used"></a>Vue d’ensemble du scénario de hello et outils utilisés

Dans commande tooimplement cette solution, nous mettons à profit hello deux principaux composants d’applications sans serveur dans Azure : [Azure fonctions](https://azure.microsoft.com/services/functions/) et [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/).

Logique d’applications est un moteur de flux de travail sans serveur dans le cloud de hello.  Il fournit l’orchestration pour les composants sans serveur et connecte également tooover les 100 services et API.  Pour ce scénario, nous allons créer un tootrigger d’application logique sur les commentaires des clients.  Connecteurs hello qui peuvent aider à réaction toocustomer commentaires quelques-uns des Outlook.com, Office 365, le d’enquête, Twitter et une requête HTTP [à partir d’un formulaire web](https://blogs.msdn.microsoft.com/logicapps/2017/01/30/calling-a-logic-app-from-an-html-form/).  Flux de travail hello ci-dessous, nous analyse un #sqlhelp sur Twitter.

Fonctions fournissent sans calcul dans le cloud de hello.  Dans ce scénario, nous allons utiliser tweet tooflag de fonctions d’Azure à partir des clients basés sur une série de prédéfinies par mots clés.

ensemble de la solution Hello peut être [génération dans Visual Studio](logic-apps-deploy-from-vs.md) et [déployé en tant que partie d’un modèle de ressource](logic-apps-create-deploy-template.md).  Procédure pas à pas vidéo du scénario de hello est également [sur Channel 9](http://aka.ms/logicappsdemo).

## <a name="build-hello-logic-app-tootrigger-on-customer-data"></a>Build hello logique application tootrigger sur les données des clients

Après avoir [création d’une application logique](logic-apps-create-a-logic-app.md) dans Visual Studio ou hello portail Azure :

1. Ajoutez un déclencheur pour **On New Tweets (Aux nouveaux tweets)** de Twitter.
2. Configurer hello déclencheur toolisten tootweets sur un mot clé ou un #sqlhelp.

   > [!NOTE]
   > propriété de périodicité Hello sur le déclencheur de hello détermine la fréquence de vérification application logique de hello pour les nouveaux éléments sur les déclencheurs d’interrogation

   ![Exemple de déclencheur Twitter][1]

Cette application se déclenche sur tous les nouveaux tweets.  Nous pouvons ensuite prendre ces données tweet et comprendre plus de sentiment hello exprimé.  Pour cela, nous utilisons hello [Service cognitifs Azure](https://azure.microsoft.com/services/cognitive-services/) sentiment toodetect du texte.

1. Cliquez sur **Nouvelle étape**.
1. Sélectionner ou rechercher hello **texte Analytique** connecteur
1. Sélectionnez hello **détecter un sentiments** opération
1. Si vous y êtes invité, fournissez une clé de Services cognitifs valide pour le service de texte Analytique de hello
1. Ajouter hello **texte Tweet** comme hello tooanalyze de texte.

Maintenant que nous avons hello tweet données et des informations sur les tweet hello, un nombre de tous les autres connecteurs peut-être être pertinente :
* Power BI - ajouter des lignes tooStreaming jeu de données : vue tweets sur un tableau de bord Power BI en temps réel.
* Azure Data Lake - Ajout d’un fichier : complément client données tooan Azure Data Lake dataset tooinclude travaux de l’analytique.
* SQL - Ajouter des lignes : stocker des données dans une base de données pour les récupérer ultérieurement.
* Slack - Envoyer un message : alerter un canal Slack en cas de commentaires négatifs nécessitant des actions.

Une fonction de Azure peut également être utilisé toodo plus personnalisée de calcul sur des données de hello.

## <a name="enriching-hello-data-with-an-azure-function"></a>Enrichir les données de salutation avec une fonction d’Azure

Nous pouvons créer une fonction, nous devons toohave une application de la fonction dans notre abonnement Azure.  Pour plus d’informations sur la création d’une fonction d’Azure dans le portail de hello peuvent [se trouve ici](../azure-functions/functions-create-first-azure-function-azure-portal.md)

Pour une fonction toobe appelée directement à partir d’une application logique, il a besoin toohave HTTP déclencher la liaison.  Nous vous recommandons d’utiliser des hello **HttpTrigger** modèle.

Dans ce scénario, le corps de la demande de hello Azure fonction hello serait texte tweet de hello.  Dans le code de la fonction hello, il suffit de définir la logique de si le texte de tweet hello contient un mot clé ou une expression.  fonction Hello proprement dit peut rester simple ou complexe que nécessaire pour le scénario de hello.

Extrémité hello de fonction hello, simplement retourner une application de la logique de toohello de réponse avec des données.  Il peut s’agir d’une valeur booléenne simple (par exemple, `containsKeyword`) ou d’un objet complexe.

![Étape de configuration d’une fonction Azure][2]

> [!TIP]
> Lors de l’accès à une réponse complexe à partir d’une fonction dans une application logique, utilisez l’action d’analyse de JSON hello.

Une fois que la fonction hello est enregistrée, il peut être ajouté dans l’application logique de hello créée ci-dessus.  Dans l’application hello logique :

1. Cliquez sur tooadd un **nouvelle étape**
1. Sélectionnez hello **Azure fonctions** connecteur
1. Sélectionnez les toochoose une fonction existante, puis parcourir la fonction toohello créée
1. Envoyer Bonjour **texte Tweet** pour hello **corps de la demande**

## <a name="running-and-monitoring-hello-solution"></a>En cours d’exécution et la surveillance des solutions de hello

Un des avantages de hello de la création d’orchestrations sans serveur dans les applications de la logique est débogage enrichi de hello et ses fonctionnalités de surveillance.  Toute exécution (en cours ou historique) peut être consultée à partir de Visual Studio, hello portail Azure, ou via l’API REST de hello et kits de développement logiciel.

Un des hello plus simple façons tootest une application de logique est à l’aide de hello **exécuter** bouton dans le Concepteur de hello.  En cliquant sur **exécuter** sera continuer déclencheur de hello toopoll toutes les 5 secondes jusqu'à ce qu’un événement est détecté et donnent une vue active fur hello exécuter.

Historiques d’exécution précédentes peuvent être affichés sur le panneau de vue d’ensemble de hello dans hello portail Azure, ou à l’aide de Visual Studio Cloud Explorer de hello.

## <a name="creating-a-deployment-template-for-automated-deployments"></a>Création d’un modèle de déploiement pour les déploiements automatisés

Une fois qu’une solution a été développée, il peut être capturé et déployée via un tooany de modèle de déploiement Azure région Azure dans Bonjour.  Cela est utile pour modifier les paramètres des différentes versions de ce flux de travail, mais également pour intégrer cette solution à un pipeline de génération et de mise en production.  Les détails sur la création d’un modèle de déploiement se trouvent [dans cet article](logic-apps-create-deploy-template.md).

Azure fonctions peuvent également être incorporées dans le modèle de déploiement hello - donc hello ensemble de la solution avec toutes les dépendances peut être géré comme un seul modèle.  Vous trouverez un exemple d’un modèle de déploiement de fonction Bonjour [référentiel de modèle de démarrage rapide Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/101-function-app-create-dynamic).

## <a name="next-steps"></a>Étapes suivantes

* [Voir d’autres exemples et scénarios relatifs à Azure Logic Apps](logic-apps-examples-and-scenarios.md)
* [Regarder une vidéo de procédure pas à pas sur la création de cette solution de bout en bout](http://aka.ms/logicappsdemo)
* [Découvrez comment toohandle et intercepter des exceptions au sein d’une application de logique](logic-apps-exception-handling.md)

<!-- Image References -->
[1]: ./media/logic-apps-scenario-social-serverless/twitter.png
[2]: ./media/logic-apps-scenario-social-serverless/function.png