---
title: aaaHow toocreate un espace de noms Service Bus hello portail Azure | Documents Microsoft
description: "Créer un espace de noms Service Bus à l’aide de hello portail Azure."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: fbb10e62-b133-4851-9d27-40bd844db3ba
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: d8907e7e4a804056f6d66d5a177d9ace967ed2ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-using-hello-azure-portal"></a>Créer un espace de noms Service Bus à l’aide de hello portail Azure

Un espace de noms est un conteneur d’étendue pour tous les composants de messagerie. Plusieurs files d’attente et rubriques peuvent résider dans un seul espace de noms, et les espaces de noms servent souvent de conteneurs d’applications. Il existe deux façons différentes toocreate un espace de noms Service Bus :

1. Portail Azure (cet article)
2. [Modèles Microsoft Azure Resource Manager][create-namespace-using-arm]

## <a name="create-a-namespace-in-hello-azure-portal"></a>Créer un espace de noms Bonjour portail Azure

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

Félicitations ! Vous venez de créer un espace de noms de messagerie Service Bus.

## <a name="next-steps"></a>Étapes suivantes

Découvrez notre [GitHub exemples][github-samples], qui présentent certaines Hello plus avancés des fonctionnalités de messagerie Azure Service Bus.

[create-namespace-using-arm]: service-bus-resource-manager-overview.md
[github-samples]: https://github.com/Azure/azure-service-bus/tree/master/samples
