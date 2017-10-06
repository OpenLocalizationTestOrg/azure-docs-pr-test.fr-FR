---
title: "référentiels de Registre de conteneur aaaAzure | Documents Microsoft"
description: "Comment toouse les référentiels de Registre de conteneur Azure pour les images de Docker"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: cristyg
ms.openlocfilehash: 06172a63465838a78a607f268da116d8158789ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-registry-repositories"></a>Référentiels Azure Container Registry

Les référentiels Azure Container Registry sont compatibles avec une multitude de services et d’orchestrators. toomake il services de source de hello tootrack plus faciles et les agents à partir de laquelle l’ACR est utilisé, nous avons démarré à l’aide du champ d’en-tête hello Docker dans le fichier de Docker.config hello.



## <a name="viewing-repositories-in-hello-portal"></a>Affichage des référentiels dans hello portail

en-têtes d’ACR Hello suivent le format de hello :
```
X-Meta-Source-Client: <cloud>/<service>/<optionalservicename>
```

* Cloud : Azure, Azure Stack ou tout autre cloud Azure propre au secteur public ou à un pays. Même si Azure Stack et les clouds pour le secteur public ne sont actuellement pas pris en charge, ce paramètre permet d’envisager une prise en charge future.
* Service : le nom du service de hello.
* Optionalservicename : le paramètre facultatif pour les services avec sous-Services ou toospecify une référence SKU (ex : les applications web correspondent à Azure /-applications app service/web).

Orchestrators et services des partenaires sont encouragés toouse en-tête spécifique valeurs toohelp avec nos données de télémétrie. Les utilisateurs peuvent également modifier valeur hello transmis toohello en-tête s’ils le souhaitent.

les valeurs Hello vous souhaitez ACR partenaires toouse toopopulate hello « X-Meta-Source-Client » champ sont les suivants :

| Nom du service              | En-tête                                |
| ------------------------- | ------------------------------------- |
| Azure Container Service   | azure/compute/azure-container-service |
| App Service - Web Apps    | azure/app-service/web-apps            |
| App Service - Logic Apps  | azure/app-service/logic-apps          |
| Batch                     | azure/compute/batch                   |
| Cloud Console             | azure/cloud-console                   |
| Functions                 | azure/compute/functions               |
| Internet des objets - Hub  | azure/iot/hub                         |
| HDInsight                 | azure/data/hdinsight                  |
| Jenkins                   | azure/jenkins                         |
| Machine Learning          | azure/data/machile-learning           |
| Service Fabric            | azure/compute/service-fabric          |
| VSTS                      | azure/vsts                            |


## <a name="next-steps"></a>Étapes suivantes
[En savoir plus sur les registres et hello pris en charge les services et orchestrators](container-registry-intro.md)
