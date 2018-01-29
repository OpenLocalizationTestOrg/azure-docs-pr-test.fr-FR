---
title: "Exemple de la stratégie de gestion des API Azure - Envoyer les erreurs à Stackify à des fins de journalisation | Microsoft Docs"
description: "Exemple de stratégie de gestion des API Azure - Démontre comment ajouter une stratégie de journalisation des erreurs pour envoyer les erreurs à Stackify à des fins de journalisation."
services: api-management
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/13/2017
ms.author: apimpm
ms.openlocfilehash: 34319e43789d0f2c7d3e48a0277926eb598e88fc
ms.sourcegitcommit: b854df4fc66c73ba1dd141740a2b348de3e1e028
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/04/2017
---
# <a name="send-errors-to-stackify-for-logging"></a>Envoyer les erreurs à Stackify à des fins de journalisation

Cet article représente un exemple de stratégie de gestion des API Azure qui explique comment ajouter une stratégie de journalisation des erreurs pour envoyer des erreurs à Stackify à des fins de journalisation. Pour définir ou modifier un code de stratégie, suivez les étapes décrites dans [Définir ou modifier une stratégie](../set-edit-policies.md). Pour voir d’autres exemples, consultez [Exemples de stratégie](../policy-samples.md).

## <a name="policy"></a>Stratégie

Collez le code dans le bloc **on-error**.

[!code-xml[Main](../../../api-management-policy-samples/Snippets/Log errors to Stackify.policy.xml)]

## <a name="next-steps"></a>Étapes suivantes

En savoir plus sur les stratégies APIM :

+ [Stratégies de transformation](../api-management-transformation-policies.md)
+ [Exemples de stratégie](../policy-samples.md)

