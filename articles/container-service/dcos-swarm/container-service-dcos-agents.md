---
title: "pools d’agents aaaDC/système d’exploitation pour le Service de conteneur Azure | Documents Microsoft"
description: "Fonctionnement des pools d’agents publics et privés de hello avec un cluster du Service de conteneur Azure DC/OS"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, conteneurs, micro-services, Mesos, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: c7d3889db07cb9908e8b68b668bd8a14ef3c2552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="dcos-agent-pools-for-azure-container-service"></a>Pools d’agents DC/OS pour Azure Container Service
Des clusters DC/OS d’Azure Container Service contiennent des nœuds d’agent dans deux pools, un pool public et un pool privé. Une application peut être déployée pool tooeither, affecter l’accessibilité entre des ordinateurs dans votre service de conteneur. Hello machines peuvent être exposé toohello internet (public) ou interne (privé) à conserver. Cet article explique brièvement pourquoi il existe des pools publics et privés.


* **Agents privés** : les nœuds d’un agent privé sont exécutés via un réseau non routable. Ce réseau est accessible uniquement à partir de la zone d’administration hello ou via un routeur de périphérie hello zone publique. Par défaut, DC/OS lance les applications sur les nœuds de l’agent privé. 

* **Agents publics** : les nœuds d’un agent public exécutent des services et des applications DC/OS sur un réseau accessible publiquement. 

Pour plus d’informations sur la sécurité de réseau de contrôleur de domaine/système d’exploitation, consultez hello [documentation du contrôleur de domaine/système d’exploitation](https://dcos.io/docs/1.7/administration/securing-your-cluster/).

## <a name="deploy-agent-pools"></a>Déploiement de pools d’agents

pools d’agents Hello/OS du contrôleur de domaine dans le Service de conteneur Azure sont créés comme suit :

* Hello **pool privé** contient le numéro hello de nœuds de l’agent que vous spécifiez lorsque vous [déployer le cluster de contrôleur de domaine/système d’exploitation hello](container-service-deployment.md). 

* Hello **public pool** initialement contient un nombre prédéterminé de nœuds de l’agent. Ce pool est ajouté automatiquement lors de la configuration de cluster de contrôleur de domaine/système d’exploitation hello.

pool privé de Hello et pool de public de hello sont des machines virtuelles Azure identiques. Vous pouvez redimensionner ces pools après le déploiement.

## <a name="use-agent-pools"></a>Utilisation de pools d’agents
Par défaut, **Marathon** déploie toute nouvelle toohello d’application *privé* des nœuds de l’agent. Vous avez tooexplicitly déployer hello application toohello *public* nœuds pendant la création de l’application hello hello. Sélectionnez hello **facultatif** onglet et entrez **slave_public** pour hello **accepté les rôles de ressources** valeur. Ce processus est documenté [ici](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) et Bonjour [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) documentation.

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur la [gestion de vos conteneurs DC/OS](container-service-mesos-marathon-ui.md).

* Découvrez comment trop[ouvrir le pare-feu hello](container-service-enable-public-access.md) fournie par les conteneurs de contrôleur de domaine/système d’exploitation tooyour tooallow Azure accès public.

