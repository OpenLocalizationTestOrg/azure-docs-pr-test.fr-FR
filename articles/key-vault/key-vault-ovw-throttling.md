---
ms.assetid: 
title: "aaaAzure des conseils de la limitation de coffre de clés | Documents Microsoft"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 06/21/2017
ms.openlocfilehash: a75cf96bc6503e51f14378bee598bad57e85be82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-throttling-guidance"></a>Aide sur la limitation de requêtes Azure Key Vault

La limitation est un processus que vous lancez qui limite le nombre de hello d’appels simultanés toohello service Azure tooprevent utilisation excessive de ressources. Azure Key Vault (AKV) est conçue toohandle un volume élevé de demandes. Si un grand nombre de demandes se produit, la limitation de requêtes de votre client vous permet d’assurer des performances optimales et la fiabilité du service AKV de hello.

Limites limitation dépend du scénario de hello. Par exemple, si vous effectuez un volume important d’écritures, possibilité hello pour la limitation est supérieure à si vous effectuez uniquement des lectures.

## <a name="how-does-key-vault-handle-its-limits"></a>Comment Key Vault gère-t-il ses limites ?

Limites de service dans le coffre de clés sont les abus tooprevent des ressources et garantir la qualité de service pour tous les clients du coffre de clés. En cas de dépassement d’un seuil de service, Key Vault limite toutes les autres requêtes de ce client sur une période donnée. Dans ce cas, le coffre de clés retourne le code d’état HTTP 429 (trop grand nombre de demandes), et les requêtes hello échouent. En outre, les demandes qui retournent un 429 comptabilisés dans les limites de limitation de bande passante hello suivies par le coffre de clés ayant échoué. 

Si vous avez un scénario valide justifiant une limitation supérieure, contactez-nous.


## <a name="how-toothrottle-your-app-in-response-tooservice-limits"></a>Comment toothrottle votre application dans la réponse tooservice limite

Hello Voici **meilleures pratiques** pour la limitation de votre application :
- Réduire le nombre hello d’opérations par demande.
- Réduisez la fréquence hello des requêtes.
- Évitez les nouvelles tentatives immédiates. 
    - Toutes les requêtes sont comptabilisées dans le cadre de vos limites d’utilisation.

Lorsque vous implémentez la gestion des erreurs de votre application, utilisez hello HTTP Erreur code 429 toodetect hello besoin pour la limitation au niveau du client. Si la demande de hello échoue à nouveau avec un code d’erreur HTTP 429, vous rencontrez toujours une limite de service Azure. Continuer toouse hello recommandé de méthode de limitation côté client, une nouvelle tentative de demande de hello jusqu'à ce qu’il réussisse.

### <a name="recommended-client-side-throttling-method"></a>Méthode de limitation côté client recommandée

En cas de code d’erreur HTTP 429, commencez à limiter votre client suivant une approche d’interruption exponentielle :

1. Patientez une seconde, relancez la requête ;
2. Si la limitation persiste, patientez deux secondes, relancez la requête ;
3. Si la limitation persiste, patientez quatre secondes, relancez la requête ;
4. Si la limitation persiste, patientez huit secondes, relancez la requête ;
5. Si la limitation persiste, patientez seize secondes, relancez la requête.

À ce stade, vous ne devriez pas recevoir de code de réponse HTTP 429.

## <a name="see-also"></a>Voir aussi

Pour une orientation plus approfondie de la limitation sur hello Cloud Microsoft, consultez [de limitation de modèle](https://docs.microsoft.com/azure/architecture/patterns/throttling).

