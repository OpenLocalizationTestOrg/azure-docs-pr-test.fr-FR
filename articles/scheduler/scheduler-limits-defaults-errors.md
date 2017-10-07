---
title: "aaaScheduler limites et des valeurs par défaut"
description: "Limites et valeurs par défaut de Scheduler"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 88f4a3e9-6dbd-4943-8543-f0649d423061
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 6fe0600d3ce3249d5aab1b877369b175316b5437
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-limits-and-defaults"></a>Limites et valeurs par défaut de Scheduler
## <a name="scheduler-quotas-limits-defaults-and-throttles"></a>Limitations, valeurs par défaut, limites et quotas de Scheduler
[!INCLUDE [scheduler-limits-table](../../includes/scheduler-limits-table.md)]

## <a name="hello-x-ms-request-id-header"></a>Hello x-ms-request-id en-tête
Chaque demande adressée à hello service Planificateur renvoie un en-tête de réponse nommé**x-ms-request-id**. Cet en-tête contient une valeur opaque qui identifie de façon unique la demande de hello.

Si une demande est régulièrement défectueux et que vous avez vérifié que la demande de hello est correctement formulée, vous pouvez utiliser cette tooMicrosoft d’erreur valeur tooreport hello. Dans votre rapport, inclure la valeur de hello durée approximative de x-ms-request-id hello cette demande hello a été apportée, hello identificateur d’abonnement de hello, collection de travaux et/ou de travail, et hello du type d’opération hello a tenté de demande.

## <a name="see-also"></a>Voir aussi
 [Présentation d'Azure Scheduler](scheduler-intro.md)

 [Concepts, terminologie et hiérarchie d’entités d’Azure Scheduler](scheduler-concepts-terms.md)

 [Prise en main du planificateur Bonjour portail Azure](scheduler-get-started-portal.md)

 [Plans et facturation dans Azure Scheduler](scheduler-plans-billing.md)

 [Informations de référence sur l’API REST d’Azure Scheluler](https://msdn.microsoft.com/library/mt629143)

 [Informations de référence sur les applets de commande PowerShell d’Azure Scheluler](scheduler-powershell-reference.md)

 [Haute disponibilité et fiabilité d’Azure Scheluler](scheduler-high-availability-reliability.md)

 [Authentification sortante d’Azure Scheluler](scheduler-outbound-authentication.md)

