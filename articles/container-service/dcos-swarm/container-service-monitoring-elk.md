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
# <a name="monitor-an-azure-container-service-cluster-with-elk"></a><span data-ttu-id="3ad1f-104">Surveillez un cluster Azure Container Service avec ELK</span><span class="sxs-lookup"><span data-stu-id="3ad1f-104">Monitor an Azure Container Service cluster with ELK</span></span>
<span data-ttu-id="3ad1f-105">Dans cet article, nous allons montrer comment la pile toodeploy hello ELK (Elasticsearch, Logstash, Kibana) sur un cluster de contrôleur de domaine/système d’exploitation dans le Service de conteneur Azure.</span><span class="sxs-lookup"><span data-stu-id="3ad1f-105">In this article, we demonstrate how toodeploy hello ELK (Elasticsearch, Logstash, Kibana) stack on a DC/OS cluster in Azure Container Service.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3ad1f-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="3ad1f-106">Prerequisites</span></span>
<span data-ttu-id="3ad1f-107">[Déployez](container-service-deployment.md) et [connectez](../container-service-connect.md) un cluster DC/OS configuré par Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="3ad1f-107">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a DC/OS cluster configured by Azure Container Service.</span></span> <span data-ttu-id="3ad1f-108">Explorez le tableau de bord de contrôleur de domaine/système d’exploitation hello et les services Marathon [ici](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="3ad1f-108">Explore hello DC/OS dashboard and Marathon services [here](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="3ad1f-109">Installez également hello [équilibrage de charge Marathon](container-service-load-balancing.md).</span><span class="sxs-lookup"><span data-stu-id="3ad1f-109">Also install hello [Marathon Load Balancer](container-service-load-balancing.md).</span></span>


## <a name="elk-elasticsearch-logstash-kibana"></a><span data-ttu-id="3ad1f-110">ELK (Elasticsearch, Logstash, Kibana)</span><span class="sxs-lookup"><span data-stu-id="3ad1f-110">ELK (Elasticsearch, Logstash, Kibana)</span></span>
<span data-ttu-id="3ad1f-111">Pile ELK est une combinaison de Elasticsearch, Logstash, et Kibana qui fournit une pile de tooend de fin qui peut être des toomonitor utilisé et analyser les journaux de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="3ad1f-111">ELK stack is a combination of Elasticsearch, Logstash, and Kibana that provides an end tooend stack that can be used toomonitor and analyze logs in your cluster.</span></span>

## <a name="configure-hello-elk-stack-on-a-dcos-cluster"></a><span data-ttu-id="3ad1f-112">Configurer la pile ELK hello sur un cluster de contrôleur de domaine/système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="3ad1f-112">Configure hello ELK stack on a DC/OS cluster</span></span>
<span data-ttu-id="3ad1f-113">Accéder à votre interface utilisateur de contrôleur de domaine/système d’exploitation via [http://localhost : 80 /](http://localhost:80/) qu’une seule fois dans hello l’interface utilisateur du contrôleur de domaine/système d’exploitation accédez trop**univers**.</span><span class="sxs-lookup"><span data-stu-id="3ad1f-113">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/) Once in hello DC/OS UI navigate too**Universe**.</span></span> <span data-ttu-id="3ad1f-114">Rechercher et installer des Elasticsearch, Logstash et Kibana de hello univers du contrôleur de domaine/système d’exploitation et dans cet ordre spécifique.</span><span class="sxs-lookup"><span data-stu-id="3ad1f-114">Search and install Elasticsearch, Logstash, and Kibana from hello DC/OS Universe and in that specific order.</span></span> <span data-ttu-id="3ad1f-115">Vous pouvez en savoir plus sur la configuration si vous accédez toohello **Installation avancé** lien.</span><span class="sxs-lookup"><span data-stu-id="3ad1f-115">You can learn more about configuration if you go toohello **Advanced Installation** link.</span></span>

![ELK1](./media/container-service-monitoring-elk/elk1.PNG) ![ELK2](./media/container-service-monitoring-elk/elk2.PNG) ![ELK3](./media/container-service-monitoring-elk/elk3.PNG) 

<span data-ttu-id="3ad1f-119">Une fois Bonjour les conteneurs ELK et sont opérationnels, vous devez tooenable Kibana toobe est accessible via Marathon kg.</span><span class="sxs-lookup"><span data-stu-id="3ad1f-119">Once hello ELK containers and are up and running, you need tooenable Kibana toobe accessed through Marathon-LB.</span></span> <span data-ttu-id="3ad1f-120">Accédez trop **Services** > **kibana**, puis cliquez sur **modifier** comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="3ad1f-120">Navigate too **Services** > **kibana**, and click **Edit** as shown below.</span></span>

![ELK4](./media/container-service-monitoring-elk/elk4.PNG)


<span data-ttu-id="3ad1f-122">Activer/désactiver trop**mode JSON** et faites défiler la section d’étiquettes toohello.</span><span class="sxs-lookup"><span data-stu-id="3ad1f-122">Toggle too**JSON mode** and scroll down toohello labels section.</span></span>
<span data-ttu-id="3ad1f-123">Vous devez tooadd une `"HAPROXY_GROUP": "external"` entrée ici comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="3ad1f-123">You need tooadd a `"HAPROXY_GROUP": "external"` entry here as shown below.</span></span>
<span data-ttu-id="3ad1f-124">Une fois que vous cliquez sur **Deploy changes** (Déployer les changements), votre conteneur redémarre.</span><span class="sxs-lookup"><span data-stu-id="3ad1f-124">Once you click **Deploy changes**, your container restarts.</span></span>

![ELK5](./media/container-service-monitoring-elk/elk5.PNG)


<span data-ttu-id="3ad1f-126">Si vous souhaitez tooverify que Kibana est inscrit en tant que service dans le tableau de bord hello HAPROXY, vous devez tooopen port 9090 sur le cluster de l’agent hello comme HAPROXY s’exécute sur le port 9090.</span><span class="sxs-lookup"><span data-stu-id="3ad1f-126">If you want tooverify that Kibana is registered as a service in hello HAPROXY dashboard, you need tooopen port 9090 on hello agent cluster as HAPROXY runs on port 9090.</span></span>
<span data-ttu-id="3ad1f-127">Par défaut, nous allons ouvrir les ports 80, 8080 et 443 dans hello cluster de l’agent de contrôleur de domaine/système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="3ad1f-127">By default, we open ports 80, 8080, and 443 in hello DC/OS agent cluster.</span></span>
<span data-ttu-id="3ad1f-128">Instructions tooopen un port et fournir public évaluer fournis [ici](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="3ad1f-128">Instructions tooopen a port and provide public assess are provided [here](container-service-enable-public-access.md).</span></span>

<span data-ttu-id="3ad1f-129">tooaccess hello du tableau de bord HAPROXY, interface d’administration ouverts hello Marathon kg à : `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`.</span><span class="sxs-lookup"><span data-stu-id="3ad1f-129">tooaccess hello HAPROXY dashboard, open hello Marathon-LB admin interface at: `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`.</span></span>
<span data-ttu-id="3ad1f-130">Une fois que vous accédez toohello URL, vous devez voir le tableau de bord hello HAPROXY comme indiqué ci-dessous, et vous devriez voir une entrée de service de Kibana.</span><span class="sxs-lookup"><span data-stu-id="3ad1f-130">Once you navigate toohello URL, you should see hello HAPROXY dashboard as shown below and you should see a service entry for Kibana.</span></span>

![ELK6](./media/container-service-monitoring-elk/elk6.PNG)


<span data-ttu-id="3ad1f-132">tooaccess hello Kibana tableau de bord, qui est déployé sur le port 5601, vous devez tooopen port 5601.</span><span class="sxs-lookup"><span data-stu-id="3ad1f-132">tooaccess hello Kibana dashboard, which is deployed on port 5601, you need tooopen port 5601.</span></span> <span data-ttu-id="3ad1f-133">Suivez les instructions [ici](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="3ad1f-133">Follow instructions [here](container-service-enable-public-access.md).</span></span> <span data-ttu-id="3ad1f-134">Puis ouvrez le tableau de bord hello Kibana à : `http://localhost:5601`.</span><span class="sxs-lookup"><span data-stu-id="3ad1f-134">Then open hello Kibana dashboard at: `http://localhost:5601`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ad1f-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3ad1f-135">Next steps</span></span>

* <span data-ttu-id="3ad1f-136">Pour le transfert et la configuration du journal système et d’application, consultez [Log Management in DC/OS with ELK](https://docs.mesosphere.com/1.8/administration/logging/elk/) (Gestion de journaux dans DC/OS avec ELK).</span><span class="sxs-lookup"><span data-stu-id="3ad1f-136">For system and application log forwarding and setup, see [Log Management in DC/OS with ELK](https://docs.mesosphere.com/1.8/administration/logging/elk/).</span></span>

* <span data-ttu-id="3ad1f-137">toofilter journaux, consultez [filtrage de journaux avec ELK](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/).</span><span class="sxs-lookup"><span data-stu-id="3ad1f-137">toofilter logs, see [Filtering Logs with ELK](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/).</span></span> 

 

