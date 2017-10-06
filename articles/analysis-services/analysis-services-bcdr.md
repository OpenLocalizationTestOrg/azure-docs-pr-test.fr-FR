---
title: "aaaAzure disponibilité Analysis Services | Documents Microsoft"
description: "Garantissez la haute disponibilité Azure Analysis Services."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 6e09536c5bd7dc7f88f9b662e1a9f42d2b8c969b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="analysis-services-high-availability"></a>Haute disponibilité Analysis Services
Cet article décrit la garantie d’une haute disponibilité pour les serveurs Azure Analysis Services. 


## <a name="assuring-high-availability-during-a-service-disruption"></a>Garantissez une haute disponibilité au cours d’une interruption de service
Bien que le fait soit rare, un centre de données Azure peut subir une panne. En cas de panne, il entraîne une interruption de service qui peut durer de quelques minutes à plusieurs heures. La haute disponibilité est souvent obtenue grâce à la redondance des serveurs. Avec Azure Analysis Services, vous pouvez obtenir une redondance en créant des serveurs secondaires supplémentaires dans une ou plusieurs régions. Lors de la création des serveurs redondants, les données de hello tooassure et les métadonnées sur ces serveurs est synchronisé avec le serveur hello dans une région qui a été mis hors connexion, vous pouvez :

* Déployer des serveurs de tooredundant de modèles dans d’autres régions. Cette méthode requiert le traitement des données sur votre serveur principal et sur les serveurs redondants en parallèle, garantissant ainsi la synchronisation de tous les serveurs.

* Sauvegardez les bases de données à partir de votre serveur principal et restaurez-les sur des serveurs redondants. Par exemple, vous pouvez automatiser le stockage de tooAzure de sauvegardes de nuit et restaurer les tooother des serveurs redondants dans d’autres régions. 

Dans les deux cas, si votre serveur principal connaît une panne, vous devez modifier les chaînes de connexion hello dans les clients tooconnect toohello serveur dans un autre centre de données régional de rapports. Cette modification doit être envisagée en dernier recours et uniquement en cas de panne très grave du centre de données régional. Il est plus probable qu’une panne du centre de données hébergeant votre serveur principal réapparaisse en ligne avant que vous ne puissiez mettre à jour les connexions sur tous les clients. 



## <a name="related-information"></a>Informations connexes
[Sauvegarde et restauration](analysis-services-backup.md)   
[Gérer Azure Analysis Services](analysis-services-manage.md) 

