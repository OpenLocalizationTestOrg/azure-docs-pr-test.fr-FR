---
title: "concurrence de tooincrease aaaHow d’un service web Azure Machine Learning | Documents Microsoft"
description: "Découvrez comment concurrence tooincrease d’un apprentissage Azure web service en ajoutant des points de terminaison supplémentaires."
services: machine-learning
documentationcenter: 
author: neerajkh
manager: srikants
editor: cgronlun
keywords: "Azure Machine Learning, services web, opérationalisation, mise à l’échelle, point de terminaison, accès concurrentiel"
ms.assetid: c2c51d7f-fd2d-4f03-bc51-bf47e6969296
ms.service: machine-learning
ms.devlang: NA
ms.workload: data-services
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 01/23/2017
ms.author: neerajkh
ms.openlocfilehash: e2ad16ec766820a64f36c31232f6a33a79196af4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-an-azure-machine-learning-web-service-by-adding-additional-endpoints"></a>Mise à l’échelle d’un service web Azure Machine Learning en ajoutant des points de terminaison
> [!NOTE]
> Cette rubrique décrit les techniques des tooa applicable **classique** service Machine Learning Web. 
> 
> 

Par défaut, chaque service Web publié est configuré toosupport 20 requêtes simultanées et peut être aussi élevée que 200 requêtes simultanées. Alors que hello portail classique Azure fournit un moyen tooset cette valeur, Azure Machine Learning optimise automatiquement hello paramètre tooprovide hello des performances optimales pour votre service web et valeur de portail hello est ignorée. 

Si vous envisagez d’API de hello toocall avec une charge supérieure à une valeur de nombre maximal d’appels simultanés de 200 prend en charge, vous devez créer plusieurs points de terminaison sur hello même service Web. Vous pouvez ensuite répartir la charge entre tous de façon aléatoire.

Hello mise à l’échelle d’un service Web est une tâche courante. Certaines des raisons tooscale sont toosupport plus de 200 demandes simultanées, accroître la disponibilité par plusieurs points de terminaison ou fournir des points de terminaison distincts pour le service web de hello. Vous pouvez augmenter l’échelle de hello en ajoutant des points de terminaison supplémentaires pour hello même service Web via [portail Azure classic](https://manage.windowsazure.com/) ou hello [Service Web de Azure Machine Learning](https://services.azureml.net/) portal.

Pour plus d’informations sur l’ajout de points de terminaison, voir [Création de points de terminaison](machine-learning-create-endpoint.md).

Gardez à l’esprit qui peut être négatif si vous appelez pas hello API avec un taux élevé en conséquence à l’aide d’un nombre élevé d’opérations simultanées. Vous pouvez voir des délais d’attente sporadiques et/ou des pics de latence de hello si vous placez une charge relativement faible sur une API configurée pour une charge élevée.

Hello Qu'api synchrones est généralement utilisés dans les situations où une latence faible est souhaité. Latence ici implique des temps de hello nécessaire pour une demande d’API de hello toocomplete et les délais de réseau prise en compte. Supposons que vous avez une API avec une latence de 50 millisecondes. toofully consommer la capacité disponible de hello avec le niveau de limitation de bande passante élevée et le nombre maximal d’appels simultanés = 20, vous devez toocall cette API 20 * 1 000 / 50 = 400 heures par seconde. Étendre davantage, un nombre maximal d’appels simultanés de 200 permet de vous toocall hello API 4000 fois par seconde, en supposant une latence de 50 ms.

<!--Image references-->
[1]: ./media/machine-learning-scaling-webservice/machlearn-1.png
[2]: ./media/machine-learning-scaling-webservice/machlearn-2.png
