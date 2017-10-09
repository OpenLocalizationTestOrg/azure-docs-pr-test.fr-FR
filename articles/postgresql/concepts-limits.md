---
title: "aaaLimitations dans la base de données Azure pour PostgreSQL | Documents Microsoft"
description: "Décrit les limitations des bases de données Azure pour PostgreSQL."
services: postgresql
author: kamathsun
ms.author: sukamat
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.topic: article
ms.date: 06/01/2017
ms.openlocfilehash: f53dd240e55e0633bc1dfb8ad25e1818fa8ae18c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-in-azure-database-for-postgresql"></a>Limitations des bases de données Azure pour PostgreSQL
Bonjour Azure de base de données PostgreSQL service est en version préliminaire publique. Hello sections suivantes décrivent la capacité et des limites fonctionnelles dans le service de base de données hello.

## <a name="service-tier-maximums"></a>Maximums de niveau de service
La base de données Azure pour PostgreSQL a plusieurs niveaux de service que vous pouvez choisir pour créer un serveur. Pour plus d’informations, consultez la page [Comprendre les éléments disponibles dans chaque niveau de service](concepts-service-tiers.md).  

Est un nombre maximal de connexions, les unités de calcul et de stockage dans chaque niveau de service préliminaire hello service, comme suit : 

|                            |                   |
| :------------------------- | :---------------- |
| **Nombre maximal de connexions**        |                   |
| 50 unités de calcul de base     | 50 connexions    |
| 100 unités de calcul de base    | 100 connexions   |
| 100 unités de calcul standard | 200 connexions   |
| 200 unités de calcul standard | 300 connexions   |
| 400 unités de calcul standard | 400 connexions   |
| 800 unités de calcul standard | 500 connexions   |
| **Nombre maximal d’unités de calcul**      |                   |
| Niveau de service De base         | 100 unités de calcul |
| Niveau de service Standard      | 800 unités de calcul |
| **Volume maximal de stockage**            |                   |
| Niveau de service De base         | 1 To              |
| Niveau de service Standard      | 1 To              |

Lorsque de trop nombreuses connexions sont atteints, hello l’erreur suivante peut s’afficher :
> FATAL:  sorry, too many clients already

## <a name="preview-functional-limitations"></a>Limitations fonctionnelles de la préversion
### <a name="scale-operations"></a>Opérations de mise à l’échelle
1.  La mise à l’échelle dynamique de serveurs sur différents niveaux de service n’est pas prise en charge pour le moment. Autrement dit, il n’est pas possible de basculer entre les niveaux de service De base et Standard.
2.  L’augmentation dynamique de la demande de stockage sur un serveur créé au préalable n’est pas prise en charge pour le moment.
3.  La diminution de la taille de stockage du serveur n’est pas prise en charge.

### <a name="server-version-upgrades"></a>Mises à niveau de la version du serveur
- La migration automatique entre les versions principales du moteur de base de données n’est pas prise en charge pour le moment.

### <a name="subscription-management"></a>Gestion des abonnements
- Le déplacement dynamique de serveurs créés au préalable entre les groupes de ressources et d’abonnements n’est pas pris en charge pour le moment.

### <a name="point-in-time-restore"></a>Restauration dans le temps
1.  La restauration de niveau de service toodifferent et/ou la taille des unités de calcul et de stockage n’est pas autorisée.
2.  La restauration d’un serveur supprimé n’est pas prise en charge.

## <a name="next-steps"></a>Étapes suivantes
- Comprendre [les éléments disponibles dans chaque niveau tarifaire](concepts-service-tiers.md)
- Comprendre [les versions prises en charge de la base de données PostgreSQL](concepts-supported-versions.md)
- Révision [comment tooBack haut et restaurer un serveur de base de données Azure pour l’utilisation de PostgreSQL hello portail Azure](howto-restore-server-portal.md)
