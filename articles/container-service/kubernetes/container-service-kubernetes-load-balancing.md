---
title: "aaaLoad équilibrer Kubernetes des conteneurs dans Azure | Documents Microsoft"
description: "Connectez-vous en externe et équilibrez la charge sur plusieurs conteneurs dans un cluster Kubernetes dans Azure Container Service."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Conteneurs, micro-services, Kubernetes, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 8073c8d3a015a53a532c326749571cb2582e1bac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-containers-in-a-kubernetes-cluster-in-azure-container-service"></a>Équilibrer la charge des conteneurs dans un cluster Kubernetes dans Azure Container Service 
Cet article présente l’équilibrage de charge dans un cluster Kubernetes dans Azure Container Service. L’équilibrage de charge fournit une adresse IP accessible en externe pour le service de hello et distribue le trafic réseau entre les blocs hello en cours d’exécution dans des machines virtuelles de l’agent.

Vous pouvez configurer un toouse de service Kubernetes [équilibrage de charge Azure](../../load-balancer/load-balancer-overview.md) toomanage externe (TCP) le trafic. Avec une configuration supplémentaire, l’équilibrage de charge et le routage du trafic HTTP ou HTTPS ou des scénarios plus avancés sont possibles.

## <a name="prerequisites"></a>Conditions préalables
* [Déployer un cluster Kubernetes](container-service-kubernetes-walkthrough.md) dans Azure Container Service
* [Connectez votre client](../container-service-connect.md) tooyour cluster

## <a name="azure-load-balancer"></a>Équilibrage de charge Azure

Par défaut, un cluster Kubernetes déployé dans le Service de conteneur Azure comprend un équilibrage de charge Azure connecté à Internet pour l’agent hello machines virtuelles. (Une ressource d’équilibrage de charge distinct est configurée pour le maître hello machines virtuelles). L’équilibrage de charge Azure est de type Couche 4. Actuellement, équilibrage de charge hello prend uniquement en charge le trafic TCP dans Kubernetes.

Lorsque vous créez un service Kubernetes, vous pouvez automatiquement configurer le service de toohello accès tooallow équilibrage de charge Azure hello. équilibrage de charge tooconfigure hello, jeu hello service `type` trop`LoadBalancer`. équilibrage de charge Hello crée une règle toomap une adresse IP publique et de numéro de port d’entrant service trafic toohello des adresses IP privées et de numéros de port de POD de hello dans les machines virtuelles de l’agent (et vice versa pour le trafic de réponse). 

 Voici deux exemples montrant comment tooset hello Kubernetes service `type` trop`LoadBalancer`. (Après les exemples hello lors de la tentative, supprimez les déploiements hello si vous n’en avez plus besoin.).

### <a name="example-use-hello-kubectl-expose-command"></a>L’exemple : Hello d’utilisation `kubectl expose` commande 
Hello [Kubernetes procédure pas à pas](container-service-kubernetes-walkthrough.md) inclut un exemple de procédure tooexpose un service avec hello `kubectl expose` commande et son `--type=LoadBalancer` indicateur. Voici les étapes hello :

1. Démarrez un nouveau déploiement de conteneur. Par exemple, hello suivant de commande lance un nouveau déploiement appelé `mynginx`. déploiement de Hello se compose de trois conteneurs basés sur l’image de Docker hello pour le serveur de web Nginx hello.

    ```console
    kubectl run mynginx --replicas=3 --image nginx
    ```
2. Vérifiez que les conteneurs hello sont en cours d’exécution. Par exemple, si vous interrogez des conteneurs hello avec `kubectl get pods`, sortie similaire toohello suivante :

    ![Obtenir des conteneurs Nginx](./media/container-service-kubernetes-load-balancing/nginx-get-pods.png)

3. tooconfigure hello équilibrage tooaccept trafic externe toohello déploiement, exécutez `kubectl expose` avec `--type=LoadBalancer`. Hello commande suivante expose serveur Nginx de hello sur le port 80 :

    ```console
    kubectl expose deployments mynginx --port=80 --type=LoadBalancer
    ```

4. Type `kubectl get svc` état de hello toosee hello des services inclus dans le cluster de hello. Lors de l’équilibrage de charge hello configure la règle de hello, hello `EXTERNAL-IP` Hello service apparaît en tant que `<pending>`. Après quelques minutes, l’adresse IP externe de hello est configurée : 

    ![Configurer l’équilibrage de charge Azure](./media/container-service-kubernetes-load-balancing/nginx-external-ip.png)

5. Vérifiez que vous avez accès service hello à l’adresse IP externe de hello. Par exemple, ouvrez une adresse IP toohello navigateur web indiquée. navigateur de Hello affiche le serveur de web Nginx hello en cours d’exécution dans un des conteneurs de hello. Ou exécution hello `curl` ou `wget` commande. Par exemple :

    ```
    curl 13.82.93.130
    ```

    La sortie doit ressembler à celle-ci :

    ![Accéder à Nginx avec Curl](./media/container-service-kubernetes-load-balancing/curl-output.png)

6. configuration de hello toosee d’équilibrage de charge Azure hello, accédez toohello [portail Azure](https://portal.azure.com).

7. Rechercher un groupe de ressources hello pour votre cluster de service de conteneur et sélectionnez l’équilibrage de charge hello pour l’agent hello machines virtuelles. Son nom doit être hello même en tant que service de conteneur hello. (Ne pas choisir d’équilibrage de charge hello pour les nœuds principaux hello, hello une dont le nom inclut **master kg**.) 

    ![Équilibrage de charge dans le groupe de ressources](./media/container-service-kubernetes-load-balancing/container-resource-group-portal.png)

8. Détails de hello toosee de configuration d’équilibrage de charge hello, cliquez sur **règles d’équilibrage de charge** et le nom hello de règle hello qui a été configuré.

    ![Règles d'équilibrage de charge](./media/container-service-kubernetes-load-balancing/load-balancing-rules.png) 

### <a name="example-specify-type-loadbalancer-in-hello-service-configuration-file"></a>Exemple : Spécification `type: LoadBalancer` dans le fichier de configuration de service hello

Si vous déployez une application de conteneur Kubernetes à partir de JSON YAML [fichier de configuration de service](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file), spécifiez un équilibrage de charge externe en ajoutant hello suivant ligne toohello service spécification :

```YAML
 "type": "LoadBalancer"
``` 



Hello étapes suivantes utilisent hello Kubernetes [or exemple](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook). Cet exemple s’appuie sur une application web multiniveau basée sur des images Redis et PHP Docker. Vous pouvez spécifier dans le fichier de configuration de service hello que serveur hello frontal PHP utilise l’équilibrage de charge Azure hello.

1. Télécharger le fichier de hello `guestbook-all-in-one.yaml` de [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one). 
2. Recherchez hello `spec` pour hello `frontend` service.
3. Supprimez les commentaires hello ligne `type: LoadBalancer`.

    ![Équilibrage de charge dans la configuration du service](./media/container-service-kubernetes-load-balancing/guestbook-frontend-loadbalance.png)

4. Enregistrer le fichier de hello et déployer l’application hello en exécutant hello de commande suivante :

    ```
    kubectl create -f guestbook-all-in-one.yaml
    ```

5. Type `kubectl get svc` état de hello toosee hello des services inclus dans le cluster de hello. Lors de l’équilibrage de charge hello configure la règle de hello, hello `EXTERNAL-IP` Hello `frontend` service apparaît sous la forme `<pending>`. Après quelques minutes, l’adresse IP externe de hello est configurée : 

    ![Configurer l’équilibrage de charge Azure](./media/container-service-kubernetes-load-balancing/guestbook-external-ip.png)

6. Vérifiez que vous avez accès service hello à l’adresse IP externe de hello. Par exemple, vous pouvez ouvrir une web navigateur toohello adresse IP externe du service de hello.

    ![Accéder en externe au livre d’or](./media/container-service-kubernetes-load-balancing/guestbook-web.png)

    Vous pouvez ajouter des entrées du livre d’or.

7. configuration de hello toosee d’équilibrage de charge Azure hello, recherchez pour la ressource de programme d’équilibrage de charge hello cluster hello Bonjour [portail Azure](https://portal.azure.com). Consultez les étapes dans l’exemple précédent de hello hello.

### <a name="considerations"></a>Considérations

* La création de la règle d’équilibrage de charge hello se produit de façon asynchrone, et plus d’informations sur l’équilibrage de hello configuré sont publiés dans le service hello `status.loadBalancer` champ.
* Chaque service est affecté automatiquement sa propre adresse IP virtuelle de l’équilibreur de charge hello.
* Si vous souhaitez l’équilibrage de charge hello tooreach par un nom DNS, fonctionne avec votre toocreate de fournisseur de service de domaine un nom DNS pour l’adresse IP de la règle hello.

## <a name="http-or-https-traffic"></a>Trafic HTTP ou HTTPS

Solde de tooload HTTP ou HTTPS trafic toocontainer les applications web et de gérer les certificats de sécurité de la couche transport (TLS), vous pouvez utiliser hello Kubernetes [entrée](https://kubernetes.io/docs/user-guide/ingress/) ressource. Une entrée est une collection de règles qui autorisent les connexions entrantes tooreach les services de cluster de hello. Pour un toowork de ressource en entrée, le cluster de Kubernetes de hello doit avoir un [contrôleur d’entrée](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) en cours d’exécution.

Azure Container Service n’implémente pas automatiquement un contrôleur d’entrée Kubernetes. Plusieurs implémentations de contrôleur sont disponibles. Actuellement, hello [contrôleur d’entrée de Nginx](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) est recommandé de règles d’entrée tooconfigure et équilibrer la charge du trafic HTTP et HTTPS. 

Pour plus d’informations, consultez hello [documentation du contrôleur Nginx entrée](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).

> [!IMPORTANT]
> Lorsque vous utilisez hello contrôleur de Nginx entrée dans le conteneur de Service Azure, vous devez exposer le déploiement de contrôleur hello en tant que service avec `type: LoadBalancer`. Cela configure le contrôleur de toohello hello Azure charge équilibrage tooroute le trafic. Pour plus d’informations, consultez la section précédente de hello.


## <a name="next-steps"></a>Étapes suivantes

* Consultez hello [Kubernetes LoadBalancer documentation](https://kubernetes.io/docs/user-guide/load-balancer/)
* En savoir plus sur les [contrôleurs d’entrée, en particulier le contrôleur d’entrée Kubernetes](https://kubernetes.io/docs/user-guide/ingress/)
* Consultez les [exemples Kubernetes](https://github.com/kubernetes/kubernetes/tree/master/examples)

