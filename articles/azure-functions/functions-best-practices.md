---
title: Pratiques aaaBest pour les fonctions de Azure | Documents Microsoft
description: "Découvrez les bonnes pratiques et les modèles pour Azure Functions."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "azure functions, modèles, bonne pratique, fonctions, traitement des événements, webhooks, calcul dynamique, architecture sans serveur"
ms.assetid: 9058fb2f-8a93-4036-a921-97a0772f503c
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/13/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bd3d826b75267a740e355b008943a48f71ebd339
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-hello-performance-and-reliability-of-azure-functions"></a>Optimiser les performances de hello et la fiabilité des fonctions d’Azure

Cet article fournit des conseils tooimprove hello et fiabilité des applications de votre fonction. 


## <a name="avoid-long-running-functions"></a>Évitez les fonctions dont l’exécution prend beaucoup de longtemps

Ces fonctions peuvent provoquer des problèmes de délai d’attente inattendus. Une fonction peut devenir volumineux en raison des dépendances de Node.js réduire. L’importation des dépendances peut entraîner une augmentation des temps de chargement aboutissant à des délais d’attente inattendus. Les dépendances sont chargées tant explicitement qu’implicitement. Un module chargé par votre code peut charger ses propres modules supplémentaires.  

Autant que possible, subdivisez les fonctions volumineuses en ensembles de fonctions plus petits qui fonctionnent ensemble et retournent des réponses rapides. Par exemple, un webhook ou une fonction de déclenchement HTTP peut nécessiter une réponse de l’accusé de réception dans un délai imparti ; Il est courant pour le webhooks toorequire une réponse immédiate. Vous pouvez passer la charge utile de déclencheur hello HTTP dans un toobe de file d’attente traité par une fonction de déclenchement de file d’attente. Cette approche vous permet de travail réel de toodefer hello et retourner une réponse immédiate.


## <a name="cross-function-communication"></a>Communication entre fonctions

Lors de l’intégration de plusieurs fonctions, il est généralement d’une meilleure pratique toouse stockage files d’attente pour entre la communication de la fonction.  Hello est files d’attente de stockage sont moins chers et quantité tooprovision plus facile. 

Les messages individuels dans une file d’attente de stockage sont limités en taille too64 Ko. Si vous avez besoin de toopass des messages plus volumineux entre les fonctions, une file d’attente Azure Service Bus peut être utilisé toosupport la taille des messages des too256 Ko.

Les rubriques Service Bus sont utiles si vous avez besoin de filtrer les messages avant de les traiter.

Concentrateurs d’événements sont des communications d’un volume élevé de toosupport utile.


## <a name="write-functions-toobe-stateless"></a>Écrire des fonctions toobe de sans état 

Les fonctions doivent être sans état et idempotentes si possible. Associez toutes les informations d’état requises à vos données. Par exemple, une commande en cours de traitement aurait probablement un membre `state` associé. Une fonction a pu traiter une commande en fonction de cet état tant que fonction hello proprement dite reste sans état. 

Les fonctions idempotentes sont particulièrement recommandées avec les déclencheurs à minuterie. Par exemple, si vous avez quelque chose que vous devez absolument exécuter une fois par jour, son écriture afin qu’il puisse s’exécuter n’importe quel moment de la journée de hello avec hello mêmes résultats. fonction Hello peut se fermer lorsqu’il n’existe aucun travail d’un jour donné. Également si une exécution précédente a échoué toocomplete, de la prochaine exécution de hello doit choisir où elle s’était arrêtée.


## <a name="write-defensive-functions"></a>Écrire des fonctions défensives

Supposons que votre fonction peut être confrontée à une exception à tout moment. Concevez vos fonctions avec toocontinue de capacité hello à partir d’un point d’échec précédent lors de l’exécution suivante de hello. Considérez un scénario qui nécessite hello suivant des actions :

1. Récupérer 10 000 lignes d’une base de données.
2. Créer un message de la file d’attente pour chacun de ces tooprocess lignes davantage les ligne hello vers le bas.
 
Selon la complexité de votre système, il est possible que des services impliqués en aval se comportent de manière incorrecte, que des pannes réseau se produisent, que des limites de quota soient atteintes, etc. Tous ces facteurs peuvent affecter votre fonction à tout moment. Vous devez toodesign votre toobe fonctions préparé.

Comment votre code réagit-il si une défaillance se produit après l’insertion de 5 000 de ces éléments dans une file d’attente en vue de leur traitement ? Suivez les éléments dans un jeu que vous avez terminé. Sinon, vous pouvez les réinsérer la prochaine fois. Cela peut avoir un impact sérieux sur votre flux de travail. 

Si un élément de la file d’attente a déjà été traité, autoriser votre toobe fonction aucune opération.

Tirer parti des mesures de protection déjà fournie pour les composants que vous utilisez dans la plateforme des fonctions de Azure hello. Par exemple, consultez **la gestion des messages de la file d’attente de messages incohérents** dans la documentation de hello de [déclenche de la file d’attente de stockage Azure](functions-bindings-storage-queue.md#trigger).
 

## <a name="dont-mix-test-and-production-code-in-hello-same-function-app"></a>Ne combinaison de test et production de code Bonjour même application de la fonction

Les fonctions d’une application de fonction partagent des ressources. Par exemple, la mémoire est partagée. Si vous utilisez une application de la fonction en production, n’ajoutez pas aux tests de fonctions et ressources tooit. Cela peut entraîner une surcharge inattendue pendant l’exécution du code de production.

Soyez attentif à ce que vous chargez dans vos applications de fonction en production. Mémoire moyenne est calculée sur chaque fonction de l’application hello.

Si un assembly partagé est référencé dans plusieurs fonctions .Net, placez-le dans un dossier partagé commun. Assembly hello de référence avec un toohello similaire instruction l’exemple suivant : 

    #r "..\Shared\MyAssembly.dll". 

Dans le cas contraire, il est facile tooaccidentally déployer plusieurs versions de test du même binaire qui se comportent différemment entre les fonctions de hello.

N’utilisez pas de journalisation détaillée dans le code de production. Cela affecte les performances.



## <a name="use-async-code-but-avoid-blocking-calls"></a>Utiliser du code asynchrone tout en évitant de bloquer les appels

La programmation asynchrone est une pratique recommandée. Toutefois, toujours éviter de référencer hello `Result` propriété ou l’appel `Wait` méthode sur un `Task` instance. Cette approche peut entraîner l’épuisement de toothread.


[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations, consultez hello suivant des ressources :

Étant donné qu’Azure Functions utilise Azure App Service, vous devez également connaître les directives d’App Service.
* [Modèles et pratiques d’optimisations des performances HTTP](https://docs.microsoft.com/azure/architecture/antipatterns/improper-instantiation/)

