---
title: "version aaaCanary avec une EMPEIGNE sur le cluster de contrôleur de domaine/système d’exploitation Azure | Documents Microsoft"
description: Comment toouse Vamp des services de mise en production toocanary et appliquer le filtrage sur un cluster du Service de conteneur Azure DC/OS du trafic actif
services: container-service
author: gggina
manager: rasquill
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/17/2017
ms.author: rasquill
ms.custom: mvc
ms.openlocfilehash: e7b8658a161a7cddcf718e3e1c12a889a330d3d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="canary-release-microservices-with-vamp-on-an-azure-container-service-dcos-cluster"></a>Contrôler la validité de microservices de mise en production avec Vamp sur un cluster de contrôleur de domaine/système d’exploitation Azure Container Service

Dans cette procédure pas à pas, nous configurons Vamp sur Azure Container Service avec un cluster de contrôleur de domaine/système d’exploitation. Nous canary version du service de démo hello une EMPEIGNE « sava », puis résolvez un problème d’incompatibilité du service hello avec Firefox en appliquant un filtrage du trafic actif. 

> [!TIP] 
> Dans cette procédure pas à pas une EMPEIGNE s’exécute sur un cluster de contrôleur de domaine/système d’exploitation, mais vous pouvez également utiliser une EMPEIGNE avec Kubernetes en tant qu’orchestrateur de hello.
>

## <a name="about-canary-releases-and-vamp"></a>À propos du contrôle de la validité des mises en production et de Vamp


Le [contrôle de la validité des mises en production](https://martinfowler.com/bliki/CanaryRelease.html) est une stratégie de déploiement intelligent adoptée par des entreprises innovantes telles que Netflix, Facebook et Spotify. Cette approche est intéressante, car elle réduit les problèmes, introduit des filets de sécurité et stimule l’innovation. Alors pourquoi toutes les entreprises ne l’adoptent-elles pas ? Étendre un tooinclude de pipeline de l’élément de configuration/CD stratégies canary ajoute une complexité et requiert l’expérience et devops complète de base de connaissances. C’est assez tooblock plus petites entreprises et les entreprises avant qu’ils même prise en main. 

[Vamp](http://vamp.io/) est un tooease système open source conçu cette transition et mettre canary libération fonctionnalités tooyour préféré conteneur du planificateur. La fonctionnalité de contrôle de validité de Vamp va au-delà des déploiements basés sur un pourcentage. Le trafic peut filtré et divisent sur un large éventail de conditions, par exemple des tootarget des utilisateurs spécifiques, des plages d’IP ou appareils. Vamp suit et analyse les métriques de performances, permettant ainsi une automatisation basée sur des données réelles. Vous pouvez configurer une restauration automatique en cas d’erreurs ou mettre à l’échelle des variantes de service en fonction de la charge ou de la latence.

## <a name="set-up-azure-container-service-with-dcos"></a>Configurer Azure Container Service avec un contrôleur de domaine/système d’exploitation



1. [Déployez un cluster de contrôleur de domaine/système d’exploitation](container-service-deployment.md) avec un maître et deux agents de la taille par défaut. 

2. [Créer un tunnel SSH](../container-service-connect.md) cluster de contrôleur de domaine/système d’exploitation tooconnect toohello. Cet article suppose que vous tunnel cluster toohello sur le port local 80.


## <a name="set-up-vamp"></a>Configurer Vamp

Maintenant que vous disposez d’un cluster de contrôleur de domaine/système d’exploitation en cours d’exécution, vous pouvez installer une EMPEIGNE depuis hello l’interface utilisateur du contrôleur de domaine/système d’exploitation (http://localhost : 80). 

![IU DC/OS](./media/container-service-dcos-vamp-canary-release/01_set_up_vamp.png)

L’installation s’effectue en deux étapes :

1. **Déploiement d’Elasticsearch**,

2. Puis **déployer une EMPEIGNE** en installant le package d’univers hello Vamp contrôleur de domaine/système d’exploitation.

### <a name="deploy-elasticsearch"></a>Déployer Elasticsearch

Vamp a besoin d’Elasticsearch pour la collecte et l’agrégation des métriques. Vous pouvez utiliser hello [magneticio Docker images](https://hub.docker.com/r/magneticio/elastic/) toodeploy une pile de Elasticsearch de Vamp compatible.

1. Dans l’interface utilisateur du contrôleur de domaine/système d’exploitation de hello, accédez trop**Services** et cliquez sur **déployer le Service**.

2. Sélectionnez **mode JSON** de hello **déployer un nouveau Service** contextuelle.

  ![Sélectionnez le mode JSON](./media/container-service-dcos-vamp-canary-release/02_deploy_service_json_mode.png)

3. Collez hello suivant JSON. Cette configuration s’exécute conteneur de hello avec 1 Go de RAM et une vérification d’intégrité de base sur le port Elasticsearch hello.
  
  ```JSON
  {
    "id": "elasticsearch",
    "instances": 1,
    "cpus": 0.2,
    "mem": 1024.0,
    "container": {
      "docker": {
        "image": "magneticio/elastic:2.2",
        "network": "HOST",
        "forcePullImage": true
      }
    },
    "healthChecks": [
      {
        "protocol": "TCP",
        "gracePeriodSeconds": 30,
        "intervalSeconds": 10,
        "timeoutSeconds": 5,
        "port": 9200,
        "maxConsecutiveFailures": 0
      }
    ]
  }
  ```
  

3. Cliquez sur **Déployer**.

  Contrôleur de domaine/système d’exploitation déploie le conteneur de Elasticsearch hello. Vous pouvez suivre la progression sur hello **Services** page.  

  ![déployer Elasticsearch](./media/container-service-dcos-vamp-canary-release/03_deply_elasticsearch.png)

### <a name="deploy-vamp"></a>Déployer Vamp

Une fois que Elasticsearch signale comme **en cours d’exécution**, vous pouvez ajouter le package d’univers de contrôleur de domaine/système d’exploitation Vamp hello. 

1. Accédez trop**univers** et recherchez **vamp**. 
  ![Vamp sur un univers de contrôleur de domaine/système d’exploitation](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)

2. Cliquez sur **installer** toohello suivant vamp package, puis choisissez **Installation avancé**.

3. Faites défiler la liste et entrez hello suivant elasticsearch-url : `http://elasticsearch.marathon.mesos:9200`. 

  ![Entrer l’URL d’Elasticsearch](./media/container-service-dcos-vamp-canary-release/05_universe_elasticsearch_url.png)

4. Cliquez sur **Examinez et installez**, puis cliquez sur **installer** déploiement de hello toostart.  

  Le contrôleur de domaine/système d’exploitation déploie tous les composants Vamp requis. Vous pouvez suivre la progression sur hello **Services** page.
  
  ![Déployer Vamp en tant que package d’univers](./media/container-service-dcos-vamp-canary-release/06_deploy_vamp.png)
  
5. Une fois le déploiement terminé, vous pouvez accéder hello Vamp de l’interface utilisateur :

  ![Service Vamp sur contrôleur de domaine/système d’exploitation](./media/container-service-dcos-vamp-canary-release/07_deploy_vamp_complete.png)
  
  ![Interface utilisateur de Vamp](./media/container-service-dcos-vamp-canary-release/08_vamp_ui.png)


## <a name="deploy-your-first-service"></a>Déployer votre premier service

À présent que Vamp est opérationnel, déployez un service à partir d’un schéma. 

Dans sa forme la plus simple, un [une EMPEIGNE plan](http://vamp.io/documentation/using-vamp/blueprints/) décrit les points de terminaison hello (passerelles), des clusters et des services toodeploy. Vamp utilise clusters toogroup différentes variantes de hello même service en groupes logiques pour libérer canary ou A / B de test.  

Ce scénario utilise un exemple d’application monolithique appelé [ **sava**](https://github.com/magneticio/sava), qui en est à la version 1.0. monolithique de Hello est empaqueté dans un conteneur Docker, qui est dans le Hub d’ancrage sous magneticio/sava:1.0.0. application Hello s’exécute normalement sur le port 8080, mais vous souhaitez tooexpose sous port 9050 dans ce cas. Déploiement d’une application hello via une EMPEIGNE à l’aide d’un modèle simple.

1. Accédez trop**déploiements**.

2. Cliquez sur **Add**.

3. Coller dans hello suivant Géomètre YAML. Ce schéma contient un seul cluster avec une seule variante de service, que nous allons changer ultérieurement :

  ```YAML
  name: sava                        # deployment name
  gateways:
    9050: sava_cluster/webport      # stable endpoint
  clusters:
    sava_cluster:               # cluster toocreate
     services:
        -
          breed:
            name: sava:1.0.0        # service variant name
            deployable: magneticio/sava:1.0.0
            ports:
              webport: 8080/http # cluster endpoint, used for canary releasing
  ```

4. Cliquez sur **Enregistrer**. Une EMPEIGNE lance le déploiement de hello.

déploiement de Hello est répertorié sur hello **déploiements** page. Cliquez sur hello déploiement toomonitor son état.

![Interface utilisateur de Vamp - Déploiement de sava](./media/container-service-dcos-vamp-canary-release/09_sava100.png)

![service Sava dans l’interface utilisateur de Vamp](./media/container-service-dcos-vamp-canary-release/09a_sava100.png)

Deux passerelles sont créés, qui sont répertoriées sur hello **passerelles** page :

* un Bonjour de tooaccess stable de point de terminaison (port 9050) de service en cours d’exécution 
* une passerelle interne gérée par Vamp (que nous décrirons plus en détail ultérieurement). 

![Interface utilisateur de Vamp - Passerelles sava](./media/container-service-dcos-vamp-canary-release/10_vamp_sava_gateways.png)

Hello sava service a maintenant déployé, mais vous ne peut pas y accéder en externe car hello équilibrage de charge Azure ne connaît pas encore tooforward trafic tooit. service hello tooaccess, hello de mise à jour de configuration de mise en réseau Azure.


## <a name="update-hello-azure-network-configuration"></a>Mettre à jour la configuration du réseau Azure hello

Une EMPEIGNE déployé le service sava hello sur des nœuds de l’agent de contrôleur de domaine/système d’exploitation hello, exposer un point de terminaison stable au port 9050. service de hello tooaccess cluster du contrôleur de domaine/système d’exploitation hello extérieur, apporter hello suivant la configuration de réseau Azure toohello de modifications dans votre déploiement de cluster : 

1. **Configurer hello équilibrage de charge Azure** pour les agents de hello (hello ressource nommée **dcos-agent-lb-xxxx**) avec une sonde d’intégrité et de trafic tooforward de règle sur les instances de port 9050 toohello sava. 

2. **Groupe de sécurité réseau de mise à jour hello** pour les agents publics hello (hello ressource nommée **XXXX-agent-public-groupe de sécurité réseau-XXXX**) le trafic de tooallow sur le port 9050.

Pour obtenir des instructions détaillées toocomplete ces tâches à l’aide de hello Azure portail, consultez [activer l’application de Service de conteneur Azure accès public tooan](container-service-enable-public-access.md). Spécifiez le port 9050 pour tous les paramètres de port.


Une fois que tout a été créé, accédez à toohello **vue d’ensemble** panneau d’équilibrage de charge de l’agent de contrôleur de domaine/système d’exploitation hello (hello ressource nommée **dcos-agent-lb-xxxx**). Recherche hello **adresse IP publique**et utilisez hello adresse tooaccess sava port 9050.

![Portail Azure - Obtenir un adresse IP publique](./media/container-service-dcos-vamp-canary-release/18_public_ip_address.png)

![sava](./media/container-service-dcos-vamp-canary-release/19_sava100.png)


## <a name="run-a-canary-release"></a>Exécuter un contrôle de validité de mise en production

Vous disposez d’une nouvelle version de cette application que vous souhaitez version toocanary en production. Vous avez placées dans des conteneurs en tant que magneticio/sava:1.1.0 et toogo prêt. Une EMPEIGNE vous permet d’ajouter facilement de nouveaux services toohello déploiement en cours d’exécution. Ces services « fusionnées » sont déployés en même temps que les services existants de hello dans un cluster de hello et une pondération de 0 %. Aucun trafic n’est routé tooa qui vient d’être fusionnée service jusqu'à ce que vous ajustez la distribution du trafic hello. curseur de poids Hello Bonjour Vamp de l’interface utilisateur procure un contrôle total sur distribution hello, en tenant compte d’ajustements incrémentielle (version canary) ou une restauration instantanée.

### <a name="merge-a-new-service-variant"></a>Fusionner une nouvelle variante de service

toomerge hello nouveau sava 1.1 service avec hello déploiement en cours d’exécution :

1. Bonjour Vamp de l’interface utilisateur, cliquez sur **projets**.

2. Cliquez sur **ajouter** et coller dans hello suivant Géomètre YAML : ce modèle décrit un nouveau toodeploy de variante (sava : 1.1.0) de service dans un cluster existant de hello (sava_cluster).

  ```YAML
  name: sava:1.1.0      # blueprint name
  clusters:
    sava_cluster:       # cluster tooupdate
      services:
        -
          breed:
            name: sava:1.1.0    # service variant name
            deployable: magneticio/sava:1.1.0    
            ports:
              webport: 8080/http # cluster endpoint tooupdate
  ```
  
3. Cliquez sur **Enregistrer**. plan de Hello est stocké et répertorié sur hello **projets** page.

4. Menu action de hello ouvert sur le plan de sava : 1.1 hello et cliquez sur **de fusion pour**.

  ![Interface utilisateur de Vamp - Schémas](./media/container-service-dcos-vamp-canary-release/20_sava110_mergeto.png)

5. Sélectionnez hello **sava** déploiement et cliquez sur **fusion**.

  ![Vamp UI - plan toodeployment de fusion](./media/container-service-dcos-vamp-canary-release/21_sava110_merge.png)

Une EMPEIGNE déploie hello nouvelle sava : 1.1.0 variante de service décrite dans le plan de hello en même temps que sava : 1.0.0 Bonjour **sava_cluster** Hello déploiement en cours d’exécution. 

![Interface utilisateur de Vamp - Déploiement de sava mis à jour](./media/container-service-dcos-vamp-canary-release/22_sava_cluster.png)

Hello **sava/sava_cluster/webport** passerelle (point de terminaison de cluster hello) est également mise à jour de, l’ajout d’un itinéraire toohello qui vient d’être déployé sava : 1.1.0. À ce stade, aucun trafic n’est routé ici (hello **poids** a la valeur too0 %).

![Interface utilisateur de Vamp - Passerelle de cluster](./media/container-service-dcos-vamp-canary-release/23_sava_cluster_webport.png)

### <a name="canary-release"></a>Contrôle la validité de la mise en production

Les deux versions de sava déployé Bonjour même cluster, ajuster la distribution de hello du trafic entre eux en déplaçant hello **poids** curseur.

1. Cliquez sur ![Vamp UI - modifier](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) suivant trop**poids**.

2. Définissez hello poids distribution too50%/50% et cliquez sur **enregistrer**.

  ![Interface utilisateur de Vamp - Curseur de poids de passerelle](./media/container-service-dcos-vamp-canary-release/24_sava_cluster_webport_weight.png)

3. Revenir en arrière tooyour navigateur et actualiser la page de sava hello plusieurs fois. application de sava Hello maintenant bascule entre une page sava : 1.0 et une page sava : 1.1.

  ![alternance des services sava1.0 et sava1.1](./media/container-service-dcos-vamp-canary-release/25_sava_100_101.png)


  > [!NOTE]
  > Cette alternative de page de hello fonctionne mieux avec hello « Furtif » ou « Anonymous » en mode de votre navigateur en raison de hello mise en cache des éléments statiques.
  >

### <a name="filter-traffic"></a>Filtrer le trafic

Supposons qu’après déploiement vous ayez découvert une incompatibilité dans sava:1.1.0 qui entraîne des problèmes d’affichage dans les navigateurs Firefox. Vous pouvez définir une EMPEIGNE toofilter du trafic entrant et diriger que tous les utilisateurs de Firefox sauvegarder toohello connu sava : 1.0.0 stable. Ce filtre instantanément résout hello interruption pour les utilisateurs de Firefox, tandis que celles des autres locataires continue tooenjoy les avantages de hello Hello améliorées sava : 1.1.0.

Vamp utilise **conditions** trafic toofilter entre les itinéraires dans une passerelle. Le trafic est tout d’abord filtré et dirigées conséquente toohello conditions appliquées tooeach itinéraire. Tout le trafic restant est distribué en fonction du paramètre d’épaisseur toohello passerelle.

Vous pouvez créer une condition toofilter tous les utilisateurs de Firefox et diriger les toohello ancien sava : 1.0.0 :

1. Sur hello sava/sava_cluster/webport **passerelles** , cliquez sur ![Vamp UI - modifier](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) tooadd un **CONDITION** toohello itinéraire sava/sava_cluster/sava:1.0.0/webport. 

2. Entrez la condition de hello **agent utilisateur == Firefox** et cliquez sur ![Vamp UI - enregistrer](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png).

  Une EMPEIGNE ajoute la condition hello avec un niveau par défaut de 0 %. toostart filtrant le trafic, vous avez besoin de puissance de condition tooadjust hello.

3. Cliquez sur ![Vamp UI - modifier](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) toochange hello **force** appliqué toohello condition.
 
4. Ensemble hello **force** too100 % et cliquez sur ![Vamp UI - enregistrer](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png) toosave.

  Désormais, une EMPEIGNE envoie tout le trafic correspondant hello condition (tous les utilisateurs de Firefox) toosava:1.0.0.

  ![Vamp UI - appliquer la condition toogateway](./media/container-service-dcos-vamp-canary-release/26_apply_condition.png)

5. Enfin, ajuster hello passerelle poids toosend tous les autres le trafic (tous les utilisateurs non-Firefox) toohello nouveau sava : 1.1.0. Cliquez sur ![Vamp UI - modifier](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) suivant trop**poids** et définissez la distribution du poids hello 100 % est dirigée toohello itinéraire sava/sava_cluster/sava:1.1.0/webport.

  Tout le trafic non filtré par la condition de hello est maintenant dirigée toohello nouveau sava : 1.1.0.

6. filtre de hello de toosee en action, ouvrez deux différents navigateurs (un Firefox et un autre navigateur) et accéder au service de sava hello à partir des deux. Toutes les demandes de Firefox sont envoyés toosava:1.0.0, alors que tous les autres navigateurs sont toosava:1.1.0 dirigée.

  ![Interface utilisateur de Vamp - Filtrer le trafic](./media/container-service-dcos-vamp-canary-release/27_filter_traffic.png)

## <a name="summing-up"></a>Résumé

Cet article a été un tooVamp brève introduction sur un cluster de contrôleur de domaine/système d’exploitation. Pour commencer, que vous avez obtenu une EMPEIGNE et en cours d’exécution sur votre conteneur de Service de contrôleur de domaine/système d’exploitation Azure cluster, déployé un service avec un plan d’une EMPEIGNE et consulté au point de terminaison hello exposé (passerelle).

Nous avons abordé également certaines fonctionnalités puissantes d’une EMPEIGNE : la fusion d’un nouveau toohello variant service déploiement en cours d’exécution et présentation de façon incrémentielle, puis le filtrage du trafic tooresolve une incompatibilité connue.


## <a name="next-steps"></a>Étapes suivantes

* En savoir plus sur la gestion des actions d’une EMPEIGNE via hello [Vamp des API REST](http://vamp.io/documentation/api/api-reference/).

* Générez des scripts d’automatisation de Vamp dans Node.js et exécutez-les en tant que [flux de travail Vamp](http://vamp.io/documentation/tutorials/create-a-workflow/).

* Consultez des [didacticiels Vamp](http://vamp.io/documentation/tutorials/overview/) supplémentaires.

