---
title: "Présentation des unités de calcul dans Azure Database pour MySQL | Microsoft Docs"
description: "Base de données Azure pour MySQL : cet article explique les concepts de hello d’unités de calcul et que se passe-t-il lorsque votre charge de travail atteint hello nombre maximum d’unités de calcul."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 751b4fff2760e55565e2bc80d49db17a57397779
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="explaining-compute-units-in-azure-database-for-mysql"></a>Présentation des unités de calcul dans Azure Database pour MySQL
Cet article explique le concept de hello d’unités de calcul et que se passe-t-il lorsque votre charge de travail atteint hello nombre maximum d’unités de calcul.

## <a name="what-are-compute-units"></a>Que sont les unités de calcul ?
Les unités sont une mesure de débit de traitement de l’UC est garantie tooa disponible de toobe de calcul en une seule base de données Azure pour le serveur MySQL. Une unité de calcul est une mesure mélangée de ressources processeur et mémoire. En règle générale, 50 unités de calcul sont équivalentes toohalf d’un cœur. 100 unités de calcul sont équivalentes tooone core. Unités de calcul 2000 sont équivalentes cœurs tootwenty du serveur de traitement garantie débit tooyour disponibles.

quantité de Hello de mémoire par unité de calcul est optimisée pour Basic de hello et niveaux de tarification Standard. Doubler les unités de calcul hello en augmentant le niveau de performance hello équivaut ensemble de hello toodoubling de toothat disponible des ressources en une seule base de données Azure pour MySQL.

Par exemple, 800 unités de calcul Standard fournissent 8 fois plus de débit d’UC et de mémoire qu’une configuration de 100 unités de calcul Standard. Toutefois, alors que les unités de calcul Standard 100 fournissent hello même débit d’UC comparée unités de calcul tooBasic 100, hello mémoire qui est préconfigurée dans le niveau de tarification Standard est de double hello quantité de mémoire configurée pour le niveau tarifaire de base. Par conséquent, niveau de tarification Standard fournit les meilleures performances et une latence plus faible de transaction au niveau de tarification de base avec hello sélectionnée de la même unité de calcul.

## <a name="how-can-i-determine-hello-number-of-compute-units-needed-for-my-workload"></a>Comment puis-je déterminer le nombre hello d’unités de calcul nécessaires pour ma charge de travail ?
Si vous cherchez toomigrate un serveur MySQL existant exécuté localement ou sur un ordinateur virtuel, vous pouvez déterminer le nombre hello d’unités de calcul par l’estimation des besoins de votre charge de travail le nombre de cœurs du débit de traitement. 

Si votre serveur actuel local ou sur machine virtuelle utilise actuellement 4 cœurs (sans compter l’hyperthread d’UC), commencez par configurer 400 unités de calcul pour votre serveur Azure Database pour serveur MySQL. Les unités de calcul peuvent être augmentées ou diminuées dynamiquement en fonction des besoins de votre charge de travail, pratiquement sans interruption des applications. 

Graphique de mesures moniteur hello Bonjour Azure portal ou écriture CLI d’Azure commandes - toomeasure unités de calcul. Toomonitor de mesures sont le pourcentage d’unité de calcul hello et limite de l’unité de calcul.

>[!IMPORTANT]
> Si vous trouvez le stockage par seconde ne sont pas entièrement utilisé toohello maximum, envisagez de hello unités l’utilisation du calcul et de surveillance. Le déclenchement d’unités de calcul hello peut autoriser pour augmenter le débit d’e/s par en réduisant hello goulot d’étranglement en raison de l’UC de toolimited ou de la mémoire.

## <a name="what-happens-when-i-hit-my-maximum-compute-units"></a>Que se passe-t-il quand j’atteins le maximum d’unités de calculs ?
Les niveaux de performance sont étalonnés et régie tooprovide ressources toorun votre charge de travail de base de données des limites de max toohello pour le niveau de tarification sélectionné hello et niveau de performance. 

Si votre charge de travail atteint les limites maximales de hello en unités hello calcul soit ou les limites d’IOPS configurées, vous pouvez continuer de ressources de hello tooutilize niveau hello maximale autorisée, mais vos requêtes sont toosee susceptibles d’augmenter le temps de latence. Ces limites n’entraînent pas toutes les erreurs, mais plutôt un ralentissement de la charge de travail hello, sauf si le problème de ralentissement hello devient donc grave qui interroge le délai d’attente. 

Si votre charge de travail atteint les limites maximales de hello sur le nombre de connexions, les erreurs explicites sont déclenchés. Pour plus d’informations sur les limites des ressources, consultez [Limitations dans Azure Database pour MySQL](concepts-limits.md).

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur les niveaux tarifaires, consultez [Niveaux tarifaires d’Azure Database pour MySQL](./concepts-service-tiers.md).
