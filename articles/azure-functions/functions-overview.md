---
title: "vue d’ensemble des fonctions d’aaaAzure | Documents Microsoft"
description: Comprendre comment toouse les fonctions Azure toooptimize asynchrones les charges de travail en minutes.
services: functions
documentationcenter: na
author: mattchenderson
manager: erikre
editor: 
tags: 
keywords: "azure functions, fonctions, traitement des événements, webhooks, calcul dynamique, architecture sans serveur"
ms.assetid: 01d6ca9f-ca3f-44fa-b0b9-7ffee115acd4
ms.service: functions
ms.devlang: multiple
ms.topic: overview
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 02/27/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 668f9055a007fee662a4c7ec774d3c0a1d847800
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-tooazure-functions"></a>Un tooAzure présentation des fonctions  
Les fonctions Azure est une solution pour exécuter facilement des petits éléments de code, ou « fonctions » dans le cloud de hello. Vous pouvez écrire du code de hello simplement que vous avez besoin pour hello problème, sans se préoccuper un ensemble toorun d’infrastructure application ou hello il. Grâce aux fonctions, le développement gagne en productivité et vous pouvez utiliser votre langage de développement préféré, tel que C#, F#, Node.js, Python ou PHP. Payez uniquement pour le moment hello que votre code s’exécute et confiance tooscale Azure en fonction des besoins. Azure Functions vous permet de développer des applications sans serveur sur Microsoft Azure.

Cette rubrique fournit une vue d’ensemble d’Azure Functions. Si vous souhaitez toojump droite dans et prise en main des fonctions de Azure, commencez par [créer votre première fonction Azure](functions-create-first-azure-function.md). Si vous recherchez des informations techniques supplémentaires sur les fonctions, consultez hello [référence du développeur](functions-reference.md).

## <a name="features"></a>Caractéristiques
Voici les principales fonctionnalités d’Azure Functions :

* **Choix du langage** : écrivez des fonctions avec C#, F#, Node.js, Python, PHP, Batch, Bash ou tout autre fichier exécutable.
* **Modèle de tarification de paie par utilisation** - payez uniquement pour hello temps passé à exécuter votre code. Consultez l’hébergement de la consommation hello planifier option Bonjour [tarification section](#pricing).  
* **Intégration de vos propres dépendances** : Azure Functions prenant en charge NuGet et NPM, vous pouvez utiliser vos bibliothèques préférées.  
* **Sécurité intégrée** : protégez les fonctions déclenchées par HTTP à l’aide de fournisseurs OAuth comme Azure Active Directory, Facebook, Google, Twitter et Microsoft Account.  
* **Intégration simplifiée** : tirez facilement parti des services Azure et des offres SaaS (software as a service). Consultez hello [section des intégrations](#integrations) pour obtenir des exemples.  
* **Développement flexible** - Code votre droit de fonctions dans le portail de hello ou configurer l’intégration continue et déployer votre code dans GitHub, Visual Studio Team Services et d’autres [prise en charge des outils de développement](../app-service-web/web-sites-deploy.md#deploy-using-an-ide).  
* **Open source** -hello fonctions runtime est open source et [disponible sur GitHub](https://github.com/azure/azure-webjobs-sdk-script).  

## <a name="what-can-i-do-with-functions"></a>Que puis-je faire avec Azure Functions ?
Fonctions Azure est une excellente solution pour le traitement des données, intégration des systèmes, utilisation de hello internet des objets (IoT), création d’une API simple et microservices. Considérez les fonctions pour des tâches telles que l’image ou le traitement des commandes, gestion des fichiers, ou toutes les tâches que vous souhaitez toorun selon une planification. 

Fonctions fournit tooget de modèles vous avez démarré avec des scénarios clés, y compris hello suivantes :

* **BlobTrigger** -processus Azure Storage BLOB lorsqu’ils sont ajoutés toocontainers. Vous pouvez utiliser cette fonction pour le redimensionnement d’images.
* **EventHubTrigger** -répondre tooevents remis tooan concentrateur d’événements Azure. Particulièrement utile pour l’instrumentation de l’application, le traitement du workflow ou de l’expérience utilisateur, et les scénarios de l’Internet des Objets (IoT).
* **Webhook générique** : traitez les requêtes HTTP de webhook à partir de n’importe quel service prenant en charge les webhooks.
* **GitHub webhook** -tooevents répondre qui se produisent dans vos référentiels GitHub. Pour obtenir un exemple, consultez l’article [Créer une fonction Azure d’API ou de webhook](functions-create-a-web-hook-or-api-function.md).
* **HTTPTrigger** -déclencher l’exécution de hello de votre code à l’aide d’une requête HTTP.
* **QueueTrigger** -répondre toomessages qu’elles arrivent dans une file d’attente de stockage Azure. Pour obtenir un exemple, consultez [créer une fonction d’Azure qui lie tooan service Azure](functions-create-an-azure-connected-function.md).
* **ServiceBusQueueTrigger** -se connecter à votre tooother de code Azure des services ou des services locaux en écoute toomessage les files d’attente. 
* **ServiceBusTopicTrigger** -se connecter à votre tooother de code Azure des services ou des services locaux en vous abonnant tootopics. 
* **TimerTrigger** : exécutez des tâches de nettoyage ou d’autres tâches de traitement par lots selon une planification prédéfinie. Pour obtenir un exemple, consultez l’article [Créer une fonction de traitement d’événement](functions-create-an-event-processing-function.md).

Azure prend en charge des fonctions *déclencheurs*, qui sont des méthodes exécution toostart de votre code, et *liaisons*, qui est toosimplify de méthodes de codage pour les données d’entrée et de sortie. Pour obtenir une description détaillée des déclencheurs de hello et des liaisons qui fournit des fonctions d’Azure, consultez [référence du développeur Azure fonctions déclencheurs et des liaisons](functions-triggers-bindings.md).

## <a name="integrations"></a>Intégrations
Azure Functions s’intègre avec différents services Azure et services tiers. Ces services peuvent déclencher votre fonction et démarrer l’exécution, ou servir d’entrée et de sortie à votre code. Hello suivant intégrations de service est prises en charge par les fonctions d’Azure. 

* Azure Cosmos DB
* Hubs d'événements Azure 
* Azure Mobile Apps (tables)
* Azure Notification Hubs
* Azure Service Bus (files d’attente et rubriques)
* Azure Storage (objets blob, files d’attente et tables) 
* GitHub (webhooks)
* Services locaux (à l’aide de Service Bus)
* Twilio (messages SMS)

## <a name="pricing"></a>Combien coûte Azure Functions ?
Fonctions Azure a deux types de plans de tarification, choisissez hello qui répond le mieux à vos besoins : 

* **Plan de la consommation** - lorsque votre fonction s’exécute, Azure fournit toutes les ressources de calcul nécessaires hello. Vous n’avez pas tooworry sur la gestion des ressources, et vous ne payez que pour les fois hello que votre code s’exécute. 
* **Plan App Service** : exécutez vos fonctions comme vos applications API, mobiles et web. Lorsque vous utilisez déjà le Service d’applications pour les autres applications, vous pouvez exécuter vos fonctions sur hello plan sans coût supplémentaire. 

Les détails de tarification complètes sont disponibles sur hello [page de tarification de fonctions](https://azure.microsoft.com/pricing/details/functions/). Pour plus d’informations sur la mise à l’échelle de vos fonctions, consultez [comment tooscale Azure fonctions](functions-scale.md).

## <a name="next-steps"></a>Étapes suivantes
* [Créer votre première fonction Azure](functions-create-first-azure-function.md)  
  Concrète et créer votre première fonction à l’aide du démarrage rapide de fonctions d’Azure hello. 
* [Référence du développeur Azure Functions](functions-reference.md)  
  Fournit des informations techniques supplémentaires sur l’exécution de fonctions d’Azure hello et une référence pour les fonctions de codage et la définition des déclencheurs et des liaisons.
* [Test d’Azure Functions](functions-test-a-function.md)  
  décrit plusieurs outils et techniques permettant de tester vos fonctions.
* [Comment tooscale les fonctions Azure](functions-scale.md)  
  Décrit des plans de service disponibles avec les fonctions d’Azure, y compris le plan d’hébergement hello consommation, et comment toochoose hello adaptée. 
* [En savoir plus sur Azure App Service](../app-service/app-service-value-prop-what-is.md)  
  Les fonctions Azure s’appuie sur la plateforme de Service d’applications Azure hello pour les fonctionnalités principales, comme les déploiements, les variables d’environnement et les diagnostics. 

