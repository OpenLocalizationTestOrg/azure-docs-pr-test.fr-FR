---
title: "aaaMonitor un cluster de contrôleur de domaine/système d’exploitation Azure - ELK pile | Documents Microsoft"
description: Surveillez un cluster DC/OS dans un cluster Azure Container Service avec ELK (Elasticsearch, Logstash et Kibana).
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: Conteneurs, DC/OS, Azure, surveillance, elk
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 8d81c5342616ec14880d38803cdf95f5845a669b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-elk"></a>Surveillez un cluster Azure Container Service avec ELK
Dans cet article, nous allons montrer comment la pile toodeploy hello ELK (Elasticsearch, Logstash, Kibana) sur un cluster de contrôleur de domaine/système d’exploitation dans le Service de conteneur Azure. 

## <a name="prerequisites"></a>Composants requis
[Déployez](container-service-deployment.md) et [connectez](../container-service-connect.md) un cluster DC/OS configuré par Azure Container Service. Explorez le tableau de bord de contrôleur de domaine/système d’exploitation hello et les services Marathon [ici](container-service-mesos-marathon-ui.md). Installez également hello [équilibrage de charge Marathon](container-service-load-balancing.md).


## <a name="elk-elasticsearch-logstash-kibana"></a>ELK (Elasticsearch, Logstash, Kibana)
Pile ELK est une combinaison de Elasticsearch, Logstash, et Kibana qui fournit une pile de tooend de fin qui peut être des toomonitor utilisé et analyser les journaux de votre cluster.

## <a name="configure-hello-elk-stack-on-a-dcos-cluster"></a>Configurer la pile ELK hello sur un cluster de contrôleur de domaine/système d’exploitation
Accéder à votre interface utilisateur de contrôleur de domaine/système d’exploitation via [http://localhost : 80 /](http://localhost:80/) qu’une seule fois dans hello l’interface utilisateur du contrôleur de domaine/système d’exploitation accédez trop**univers**. Rechercher et installer des Elasticsearch, Logstash et Kibana de hello univers du contrôleur de domaine/système d’exploitation et dans cet ordre spécifique. Vous pouvez en savoir plus sur la configuration si vous accédez toohello **Installation avancé** lien.

![ELK1](./media/container-service-monitoring-elk/elk1.PNG) ![ELK2](./media/container-service-monitoring-elk/elk2.PNG) ![ELK3](./media/container-service-monitoring-elk/elk3.PNG) 

Une fois Bonjour les conteneurs ELK et sont opérationnels, vous devez tooenable Kibana toobe est accessible via Marathon kg. Accédez trop **Services** > **kibana**, puis cliquez sur **modifier** comme indiqué ci-dessous.

![ELK4](./media/container-service-monitoring-elk/elk4.PNG)


Activer/désactiver trop**mode JSON** et faites défiler la section d’étiquettes toohello.
Vous devez tooadd une `"HAPROXY_GROUP": "external"` entrée ici comme indiqué ci-dessous.
Une fois que vous cliquez sur **Deploy changes** (Déployer les changements), votre conteneur redémarre.

![ELK5](./media/container-service-monitoring-elk/elk5.PNG)


Si vous souhaitez tooverify que Kibana est inscrit en tant que service dans le tableau de bord hello HAPROXY, vous devez tooopen port 9090 sur le cluster de l’agent hello comme HAPROXY s’exécute sur le port 9090.
Par défaut, nous allons ouvrir les ports 80, 8080 et 443 dans hello cluster de l’agent de contrôleur de domaine/système d’exploitation.
Instructions tooopen un port et fournir public évaluer fournis [ici](container-service-enable-public-access.md).

tooaccess hello du tableau de bord HAPROXY, interface d’administration ouverts hello Marathon kg à : `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`.
Une fois que vous accédez toohello URL, vous devez voir le tableau de bord hello HAPROXY comme indiqué ci-dessous, et vous devriez voir une entrée de service de Kibana.

![ELK6](./media/container-service-monitoring-elk/elk6.PNG)


tooaccess hello Kibana tableau de bord, qui est déployé sur le port 5601, vous devez tooopen port 5601. Suivez les instructions [ici](container-service-enable-public-access.md). Puis ouvrez le tableau de bord hello Kibana à : `http://localhost:5601`.

## <a name="next-steps"></a>Étapes suivantes

* Pour le transfert et la configuration du journal système et d’application, consultez [Log Management in DC/OS with ELK](https://docs.mesosphere.com/1.8/administration/logging/elk/) (Gestion de journaux dans DC/OS avec ELK).

* toofilter journaux, consultez [filtrage de journaux avec ELK](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/). 

 

