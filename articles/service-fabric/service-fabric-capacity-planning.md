---
title: aaaCapacity planification pour les applications de Service Fabric | Documents Microsoft
description: "Décrit comment tooidentify hello le nombre de nœuds de calcul requis pour une application de Service Fabric"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: markfuss
editor: 
ms.assetid: 9fa47be0-50a2-4a51-84a5-20992af94bea
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 44a69e9d8ec5efcc43122dc42e8f923ef37378f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="capacity-planning-for-service-fabric-applications"></a>Planification de la capacité pour les applications Service Fabric
Ce document explique comment tooestimate hello la quantité de ressources (UC, RAM, disque) vous devez toorun vos applications Azure Service Fabric. Il est courant pour votre toochange d’exigences de ressources au fil du temps. Vous avez besoin généralement de peu de ressources quand vous développez/testez votre service, puis vous avez besoin de plus de ressources quand vous passez en production et que votre application grandit en popularité. Lorsque vous concevez votre application, penser à la configuration requise à long terme de hello et prendre des décisions qui permettent de votre service tooscale toomeet forte demande des clients.

 Lorsque vous créez un cluster Service Fabric, vous décidez que les types de machines virtuelles (VM) qui composent le cluster de hello. Chaque machine virtuelle est fourni avec un nombre limité de ressources sous forme de hello d’unités centrales (cœurs et vitesse), la bande passante réseau, mémoire RAM et le stockage sur disque. À mesure que votre service augmente au fil du temps, vous pouvez mettre à niveau tooVMs qui offrent davantage de ressources et/ou ajouter plusieurs ordinateurs virtuels du cluster tooyour. hello de toodo ce dernier, vous devez créer l’architecture votre service initialement afin qu’il peut tirer parti des nouvelles machines virtuelles ajoutées dynamiquement toohello cluster.

Certains services gérer peu de données toono hello machines virtuelles elles-mêmes. Par conséquent, la capacité de la planification de ces services doivent se concentrer principalement sur les performances, ce qui signifie que la sélection hello appropriées UC (cœurs et vitesse) des machines virtuelles de hello. En outre, vous devez prendre en compte la bande passante réseau, notamment la fréquence des transferts réseau et la quantité de données transférées. Si votre service doit tooperform ainsi que l’utilisation de service augmente, vous pouvez ajouter plusieurs machines virtuelles du cluster toohello et la charge d’équilibrer les demandes réseau hello sur tous les ordinateurs virtuels de hello.

Pour les services qui gèrent les grandes quantités de données sur des machines virtuelles de hello, la planification de la capacité doit se concentrer principalement sur la taille. Par conséquent, vous étudiez attentivement capacité hello de la machine virtuelle hello RAM et espace disque. système de gestion de mémoire virtuelle Hello dans Windows rende espace disque comme mémoire RAM tooapplication code. En outre, le runtime du Service Fabric hello fournit la pagination intelligente en conservant les données chaudes uniquement en mémoire et de déplacement toodisk de données à froid hello. Applications peuvent ainsi utiliser plus de mémoire que physiquement disponible sur la machine virtuelle de hello. Avoir davantage de RAM simplement augmente les performances, étant donné que hello machine virtuelle peut conserver plus de stockage de disque dans la mémoire RAM. Hello machine virtuelle que vous sélectionnez doit avoir une disque toostore suffisante les données de salutation que vous voulez sur hello machine virtuelle. De même, hello machine virtuelle doit avoir suffisamment tooprovide RAM vous hello performances souhaité. Si les données de votre service augmentent au fil du temps, vous pouvez ajouter plusieurs machines virtuelles toohello cluster partition hello données et sur tous les ordinateurs virtuels de hello.

## <a name="determine-how-many-nodes-you-need"></a>Déterminer le nombre de nœuds nécessaire
Partitionnement de votre service vous permet de tooscale les données de votre service. Pour plus d’informations sur le partitionnement, consultez [Partitionnement de Service Fabric](service-fabric-concepts-partitioning.md). Chaque partition doit tenir sur une seule machine virtuelle, mais plusieurs (petites) partitions peuvent être placées sur une seule machine virtuelle. Ainsi, avoir plus de petites partitions offre davantage de souplesse que d’avoir un petit nombre de grandes partitions. trouver un compromis Hello est que comportant un grand nombre de partitions augmente la charge de l’infrastructure de Service et ne peut pas effectuer des opérations traitées sur plusieurs partitions. Il est également plus de trafic réseau potentiels si votre code de service doit fréquemment tooaccess d’ensembles de données qui se trouvent dans des partitions différentes. Lorsque vous concevez votre service, vous devez envisager soigneusement ces tooarrive leurs avantages et inconvénients à une stratégie de partitionnement efficace.

Supposons que votre application possède un seul service avec état qui a une taille de stockage que vous attendez toogrow tooDB_Size Go par an. Vous êtes prêt tooadd plus d’applications (et partitions) en tant que vous rencontrez croissance au-delà de cette année.  Hello facteur de réplication (RF), qui détermine le nombre hello de réplicas pour les impacts de votre service hello DB_Size total. Hello DB_Size total sur tous les réplicas est hello multipliée par DB_Size de facteur de réplication.  Node_Size représente l’espace de disque hello/RAM par nœud souhaité toouse pour votre service. Pour de meilleures performances, hello DB_Size doit tenir dans la mémoire entre hello cluster et un Node_Size autour de hello RAM Hello que machine virtuelle doit être choisi. En allouant un Node_Size est supérieure à la capacité de mémoire vive de hello, reposent sur la pagination hello fournie par le runtime du Service Fabric hello. Par conséquent, les performances ne peuvent pas être optimales si vos données sont considérée comme toobe à chaud (depuis le hello puis données paginées dans/out). Toutefois, pour de nombreux services où seule une fraction des données de hello est active, il est plus rentable.

nombre de Hello de nœuds nécessaires pour optimiser les performances peut être calculée comme suit :

```
Number of Nodes = (DB_Size * RF)/Node_Size

```


## <a name="account-for-growth"></a>Prendre la croissance en compte
Vous pouvez choisir le nombre de hello toocompute de nœuds selon hello DB_Size désirées toogrow de votre service, en outre toohello DB_Size que vous avez commencé avec. Ensuite, la croissance nombre hello de nœuds à mesure que votre service augmente afin que vous n’êtes pas un approvisionnement nombre hello de nœuds. Mais nombre hello de partitions doit être basé sur nombre hello de nœuds qui sont nécessaires lorsque vous exécutez votre service à croissance maximale.

Il est bon toohave des ordinateurs supplémentaires disponibles à tout moment afin que vous pouvez gérer les pics inattendues ou l’échec (par exemple, si plusieurs machines virtuelles s’arrêtent).  Alors que hello capacité supplémentaire doit être déterminée à l’aide de votre pics attendus, un point de départ est tooreserve quelques machines virtuelles supplémentaires (5 à 10 % supplémentaire).

Hello précédent suppose qu’un seul service avec état. Si vous avez plusieurs services avec état, vous avez tooadd hello DB_Size associé hello d’autres services dans l’équation de hello. Ou bien, vous pouvez calculer le nombre de hello de nœuds séparément pour chaque service avec état.  Votre service peut avoir des réplicas ou des partitions qui ne sont pas équilibrés. N’oubliez pas que certaines partitions peuvent également contenir plus de données que d’autres. Pour plus d’informations sur le partitionnement, consultez [l’article sur les meilleures pratiques de partitionnement](service-fabric-concepts-partitioning.md). Toutefois, hello équation précédente est partition et le réplica agnostique, étant donné que le Service Fabric garantit que les réplicas hello sont répartis entre les nœuds de hello de manière optimisée.

## <a name="use-a-spreadsheet-for-cost-calculation"></a>Utiliser une feuille de calcul pour le calcul des coûts
Maintenant nous allons placer des nombres réels dans la formule de hello. Un [feuille de calcul exemple](https://servicefabricsdkstorage.blob.core.windows.net/publicrelease/SF%20VM%20Cost%20calculator-NEW.xlsx) montre comment tooplan hello capacité pour une application qui contient trois types d’objets de données. Pour chaque objet, nous être proche de sa taille et le nombre d’objets nous pensons que toohave. Nous sélectionnons également le nombre de réplicas pour chaque type d’objet. feuille de calcul Hello calcule la quantité totale de hello de toobe mémoire stockée dans un cluster de hello.

Ensuite, nous entrons une taille de machine virtuelle et le coût mensuel. En fonction de hello taille de machine virtuelle, feuille de calcul hello indique hello de nombre minimal de partitions, que vous devez utiliser toosplit votre toophysically données tenir sur les nœuds hello. Vous pouvez lancer un plus grand nombre de tooaccommodate partitions que besoins de trafic de réseau et de calcul spécifique de votre application. feuille de calcul de Hello affiche le nombre de hello de partitions qui gèrent les objets de profil utilisateur hello a augmenté à partir d’un toosix.

En fonction de toutes ces informations, feuille de calcul hello affiche à présent que vous pouvez obtenir physiquement toutes les données de hello avec hello souhaité partitions et réplicas sur un cluster à nœud 26. Toutefois, ce cluster serait être très compactes, vous pouvez donc certains échecs de nœud des nœuds supplémentaires tooaccommodate et les mises à niveau. feuille de calcul Hello montre également que comportant plus de 57 nœuds offre aucun avantage supplémentaire, car il vous faudrait des nœuds vides. Là encore, vous voudrez toogo au-dessus des 57 nœuds quand même tooaccommodate les échecs des nœuds et des mises à niveau. Les besoins spécifiques de votre application, vous pouvez régler toomatch de feuille de calcul hello.   

![Feuille de calcul pour le calcul des coûts][Image1]

## <a name="next-steps"></a>Étapes suivantes
Extraire [services partitionnement Service Fabric] [ 10] toolearn plus d’informations sur le partitionnement de votre service.

<!--Image references-->
[Image1]: ./media/SF-Cost.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-concepts-partitioning.md
