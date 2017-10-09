---
title: "AAA « niveaux de tarification dans la base de données Azure pour MySQL | Documents Microsoft »"
description: Niveaux tarifaires dans Azure Database pour MySQL
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 2a05f00aff4f7166f04e035eb2a47e7662888ebc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-options-and-performance-understand-whats-available-in-each-pricing-tier"></a>Options et performances d’Azure Database pour MySQL : comprendre ce qui est disponible dans chaque niveau tarifaire
Lorsque vous créez une base de données Azure pour le serveur MySQL, vous décidez des trois options principales ressources de hello tooconfigure alloués pour ce serveur. Ces choix un impact sur les performances de hello et l’échelle du serveur de hello.
- Niveau tarifaire 
- Unités de calcul
- Stockage (Go)

Chaque niveau de tarification a une plage de performances toochoose de niveaux (unités de calcul), selon vos besoins de charges de travail. Les niveaux de performance supérieurs fournissent des ressources supplémentaires pour votre débit toodeliver conçus de serveur. Vous pouvez modifier le niveau de performance du serveur hello au sein d’un niveau de tarification pratiquement sans interruption de l’application.

> [!IMPORTANT]
> Alors que le service de hello est en version préliminaire publique, il n’est pas une garantie contrat de niveau de Service (SLA).

Dans un serveur Azure Database pour MySQL, vous pouvez avoir une ou plusieurs bases de données. Vous pouvez choisir toocreate une base de données par serveur tooutilize toutes les ressources hello ou créer plusieurs bases de données tooshare les ressources hello. 

## <a name="choose-a-pricing-tier"></a>Sélectionnez un niveau tarifaire
En phase de préversion, le service Azure Database pour MySQL offre deux niveaux tarifaires : De base et Standard. Le niveau Premium n’est pas encore disponible, mais il le sera bientôt. 

Hello tableau suivant fournit des exemples de hello tarification niveaux meilleures adaptés pour les charges de travail d’application.

| Niveau tarifaire  | Charges de travail cibles |
| :----------- | :----------------|
| De base | Idéal pour les petites charges de travail qui requièrent une capacité de calcul et de stockage évolutive sans garantie d’E/S par seconde. Exemple : serveurs utilisés pour le développement ou le test ou pour des applications à petite échelle rarement utilisées. |
| Standard | Hello go-toooption pour cloud garantissent des applications nécessitant des e/s avec un débit élevé. Exemples : applications web ou applications d’analyse. |
| Premium | Idéal pour les charges de travail nécessitant une latence faible pour les transactions et les E/S. Fournit la meilleure prise en charge de hello pour de nombreux utilisateurs simultanés. Toodatabases applicable qui prennent en charge des applications critiques.<br />niveau de tarification Hello Premium n’est pas disponible en version préliminaire. |

toodecide sur la tarification d’un niveau, premier démarrage en déterminant si votre charge de travail a besoin d’une garantie d’e/s. Si c’est le cas, utilisez le niveau tarifaire Standard.

| **Caractéristiques des niveaux tarifaires** | **De base** | **Standard** |
| :------------------------ | :-------- | :----------- |
| Nombre maximal d’unités de calcul | 100 | 800 | 
| Volume total de stockage maximal | 1 To | 1 To | 
| Garantie d’E/S par seconde de stockage | N/A  | Oui | 
| E/S par seconde de stockage maximales | N/A  | 3 000 | 
| Période de rétention de sauvegarde de bases de données | 7 jours | 35 jours | 

Période hello preview, vous ne pouvez modifier le niveau tarifaire une fois que le serveur de hello est créé. Bonjour future, il sera tooupgrade possible ou rétrograder un serveur à partir d’un niveau de tooanother niveau tarifaire.

## <a name="understand-hello-price"></a>Comprendre les prix hello
Lorsque vous créez une nouvelle base de données Azure pour MySQL à l’intérieur de hello [Azure Portal](https://portal.azure.com/#create/Microsoft.MySQLServer), cliquez sur hello **niveau tarifaire** lame et hello coût mensuel seront affichera en fonction sur les options de hello que vous avez sélectionné. Si vous n’avez pas un abonnement Azure, utilisez hello tooget de calculatrice tarification Azure un prix estimé. Visitez hello [calculatrice de prix Azure](https://azure.microsoft.com/pricing/calculator/) site Web, puis cliquez sur **ajouter des éléments**, développez hello **bases de données** catégorie, puis choisissez **base de données Azure pour MySQL**  options de hello toocustomize.

## <a name="choose-a-performance-level-compute-units"></a>Choisir un niveau de performances (unités de calcul)
Une fois que vous avez déterminé hello niveau tarifaire pour votre base de données Azure pour le serveur MySQL, vous êtes au niveau de performances toodetermine prêt hello en sélectionnant nombre hello d’unités de calcul nécessaires. Un bon point de départ est 200 ou 400 unités de calcul pour les applications qui ont besoin d’accès concurrentiels en nombre plus élevé pour leurs charges de travail web ou d’analyse, puis d’ajuster par palier au fil des besoins. 

Les unités sont une mesure de débit de traitement de l’UC est garantie tooa disponible de toobe de calcul en une seule base de données Azure pour le serveur MySQL. Une unité de calcul est une mesure mélangée de ressources processeur et mémoire.  Pour plus d’informations, voir [Présentation des unités de calcul](concepts-compute-unit-and-storage.md)

### <a name="basic-pricing-tier-performance-levels"></a>Niveaux de performances du niveau tarifaire De base :

| **Niveau de performances** | **50** | **100** |
| :-------------------- | :----- | :------ |
| Nombre maximal d’unités de calcul | 50 | 100 |
| Taille du stockage inclus | 50 Go | 50 Go |
| Taille maximale de stockage du serveur\* | 1 To | 1 To |

### <a name="standard-pricing-tier-performance-levels"></a>Niveaux de performances du niveau tarifaire Standard :

| **Niveau de performances** | **100** | **200** | **400** | **800** |
| :-------------------- | :------ | :------ | :------ | :------ |
| Nombre maximal d’unités de calcul | 100 | 200 | 400 | 800 |
| Taille du stockage inclus et E/S par seconde approvisionnées | 125 GO,<br/> 375 E/S PAR SECONDE | 125 GO,<br/> 375 E/S PAR SECONDE | 125 GO,<br/> 375 E/S PAR SECONDE | 125 GO,<br/> 375 E/S PAR SECONDE |
| Taille maximale de stockage du serveur\* | 1 To | 1 To | 1 To | 1 To |
| Nombre maximal d’E/S par seconde du serveur approvisionnées | 3 000 E/S PAR SECONDE | 3 000 E/S PAR SECONDE | 3 000 E/S PAR SECONDE | 3 000 E/S PAR SECONDE |
| Nombre maximal d’E/S par seconde du serveur approvisionnées par Go | 3 E/S par seconde fixes par Go | 3 E/S par seconde fixes par Go | 3 E/S par seconde fixes par Go | 3 E/S par seconde fixes par Go |

\*Taille de stockage du serveur max fait référence taille maximale de stockage approvisionné de toohello pour votre serveur.

## <a name="storage"></a>Storage 
configuration du stockage Hello définit hello tooan disponible la capacité de stockage Azure de base de données du serveur MySQL. stockage Hello utilisé par le service de hello inclut les fichiers de base de données hello, les journaux des transactions et les journaux du serveur MySQL hello. Prendre en compte la taille hello de stockage nécessaire toohost vos bases de données et hello des exigences de performances (par seconde IOPS) lors de la sélection de configuration du stockage hello.

Une capacité de stockage est incluse au minimum avec chaque niveau de tarification, indiqué Bonjour précédant la table en tant que « Taille de stockage inclus ». Capacité de stockage supplémentaires peut être ajoutée lorsque le serveur de hello est créé, par incréments de 125 Go de stockage maximale autorisée de toohello. capacité de stockage supplémentaire Hello peut être configurée indépendamment de configuration des unités de calcul hello. modifications des prix Hello selon la quantité de hello de stockage sélectionné.

configuration d’IOPS Hello dans chaque niveau de performance relative toohello niveau tarifaire et taille de stockage hello choisi. Le niveau De base n’offre pas de garantie d’E/S par seconde. Dans le niveau de tarification Standard hello, hello IOPS échelle proportionnellement toomaximum la taille de stockage dans un rapport de 3:1 fixe. Hello inclus un stockage de garanties de 125 Go pour 375 configuré IOPS, chacun avec une taille d’e/s de haut too256 Ko. Vous pouvez choisir le stockage supplémentaire des too1 To maximum, tooguarantee 3 000 configuré IOPS.

Graphique des métriques du moniteur hello Bonjour Azure portal ou écriture CLI d’Azure commandes toomeasure hello la consommation du stockage et des e/s. Mesures toomonitor sont la limite de stockage, pourcentage de stockage, espace de stockage utilisé et pourcentage d’e/s.

>[!IMPORTANT]
> Dans l’aperçu, choisissez quantité hello de stockage au moment de hello lorsqu’un serveur de hello est créé. Modification de la taille de stockage hello sur un serveur existant n’est pas encore pris en charge. 

## <a name="scaling-a-server-up-or-down"></a>Augmentation ou diminution de la puissance d’un serveur
Vous choisissez initialement hello au niveau de performances et le niveau de tarification lorsque vous créez votre base de données Azure pour MySQL. Une version ultérieure, vous pouvez faire évoluer hello unités de calcul monter ou Descendre dynamiquement, au sein de la plage de hello Hello même niveau de tarification. Hello portail Azure, faites glisser des unités de calcul hello sur le panneau de niveau de tarification du serveur hello ou créer un script en suivant cet exemple : [analyse et mise à l’échelle une base de données Azure pour le serveur MySQL à l’aide de CLI d’Azure](scripts/sample-scale-server.md)

Mise à l’échelle des unités de calcul hello est effectuée indépendamment de taille de stockage maximale hello que vous avez choisi.

Coulisses de hello, la modification du niveau de performance hello d’une base de données crée un réplica de base de données d’origine hello nouveau niveau de performances hello et bascule ensuite les connexions sur le réplica de toohello. Aucune donnée n’est perdue au cours de ce processus. Au cours de hello instants lorsque nous basculer toohello réplica, connexions toohello base de données sont désactivées, certaines transactions en vol peuvent être annulées. Cette fenêtre de désactivation varie, mais dure moins de 4 secondes en moyenne, et ne dépasse pas 30 secondes dans plus de 99 % des cas. S’il existe grand nombre de transactions en vol au niveau des connexions de moment hello est désactivés, cette fenêtre peut être plus longue.

Durée Hello du processus de mise à l’échelle ensemble hello dépend de la taille de hello et niveau de tarification de serveur hello avant et après la modification de hello. Par exemple, un serveur qui est en cours de modification de calcul des unités au sein du niveau de tarification Standard hello, doit se terminer dans quelques minutes. Hello nouvelles propriétés de serveur de hello ne sont pas appliquées tant que hello modifications ont été effectuées.

## <a name="next-steps"></a>Étapes suivantes
- Pour plus d’informations sur les unités de calcul, consultez [Présentation des unités de calcul](concepts-compute-unit-and-storage.md)
- Découvrez comment trop[analyse et mise à l’échelle une base de données Azure pour le serveur MySQL à l’aide de CLI d’Azure](scripts/sample-scale-server.md)
