---
title: aaaContainer solution de surveillance dans Azure journal Analytique | Documents Microsoft
description: "Hello solution d’analyse de conteneur dans le journal Analytique vous aide à afficher et gérer vos Docker et les fenêtres hôtes de conteneur dans un emplacement unique."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: e1e4b52b-92d5-4bfa-8a09-ff8c6b5a9f78
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: magoedte;banders
ms.openlocfilehash: 2eed1dd81c22faef78a375fca3ebece9e5300c09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="container-monitoring-solution-in-log-analytics"></a>Solution Container Monitoring dans Log Analytics

![Symbole Containers](./media/log-analytics-containers/containers-symbol.png)

Cet article décrit comment tooset configuration et utilisation hello solution d’analyse de conteneur dans le journal Analytique, ce qui vous permet d’afficher et gérer vos Docker et les fenêtres hôtes de conteneur dans un emplacement unique. Docker est un système logiciel de virtualisation utilisée conteneurs toocreate qui automatisent tootheir de déploiement de logiciel informatique infrastructure.

Hello solution montre quels conteneurs sont en cours d’exécution, image de conteneur qu’ils s’exécutent, et où les conteneurs sont en cours d’exécution. Vous pouvez afficher des informations d’audit détaillées montrant les commandes utilisées avec les conteneurs. Et, vous pouvez résoudre les conteneurs en affichant et en recherche de journaux centralisées sans avoir tooremotely vue Docker ou des hôtes Windows. Vous pouvez rechercher des conteneurs bruyants et consommant des ressources excessives sur un ordinateur hôte. Et vous pouvez consulter des informations centralisées sur le processeur, la mémoire, le stockage ainsi que l’utilisation et les performances du réseau. Sur les ordinateurs exécutant Windows, vous pouvez centraliser et comparer les journaux des conteneurs Windows Server, Hyper-V et Docker. solution de Hello prend en charge hello suivant orchestrators de conteneur :

- Docker Swarm
- DC/OS
- kubernetes
- Service Fabric
- Red Hat OpenShift


Hello diagramme suivant montre les relations entre différents hôtes de conteneurs et les agents OMS hello.

![Schéma des conteneurs](./media/log-analytics-containers/containers-diagram.png)

## <a name="system-requirements"></a>Conditions requises pour le système

Avant de commencer, passez en revue hello suivant tooverify détails préalables hello.

### <a name="container-monitoring-solution-support-for-docker-orchestrator-and-os-platform"></a>Prise en charge de solution de surveillance de conteneur pour la plateforme Docker Orchestrator et celle du système d’exploitation
Hello tableau suivant indique hello orchestration de Docker et le système d’exploitation prise en charge de l’inventaire de conteneur, les performances et les journaux avec Analytique de journal d’analyse.   

| | ACS | Linux | Windows | Conteneur<br>Inventaire | Image<br>Inventaire | Nœud<br>Inventaire | Conteneur<br>Performances | Conteneur<br>Événement | Événement<br>Journal | Conteneur<br>Journal |
|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| kubernetes | &#8226; | &#8226; | | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; |
| Mésosphère<br>DC/OS | &#8226; | &#8226; | | &#8226; | &#8226; | &#8226; | &#8226;| &#8226; | &#8226; | &#8226; |
| Docker<br>Swarm | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | | &#8226; |
| Service<br>Structure | | | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; |
| Red Hat Open<br>Shift | | &#8226; | | &#8226; | &#8226;| &#8226; | &#8226; | &#8226; | | &#8226; |
| Windows Server<br>(autonome) | | | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | | &#8226; |
| Serveur Linux<br>(autonome) | | &#8226; | | &#8226; | &#8226; | &#8226; | &#8226; | &#8226; | | &#8226; |


### <a name="docker-versions-supported-on-linux"></a>Versions de Docker prises en charge sur Linux

- Docker 1.11 too1.13
- Docker CE et EE v17.06

### <a name="x64-linux-distributions-supported-as-container-hosts"></a>Distributions Linux x64 suivantes prises en charge en tant qu’hôtes de conteneur

- Ubuntu 14.04 LTS et 16.04 LTS
- CoreOS(stable)
- Amazon Linux 2016.09.0
- openSUSE 13.2
- openSUSE LEAP 42.2
- CentOS 7.2 et 7.3
- SLES 12
- RHEL 7.2 et 7.3
- Red Hat OpenShift Container Platform (OCP) 3.4 et 3.5
- ACS mésosphère DC/OS 1.7.3 too1.8.8
- ACS Kubernetes 1.4.5 too1.6
- ACS Docker Swarm

### <a name="supported-windows-operating-system"></a>Système d’exploitation Windows pris en charge

- Windows Server 2016
- Édition Anniversaire Windows 10 (Professionnel ou Entreprise)

### <a name="docker-versions-supported-on-windows"></a>Versions de docker prises en charge sur Windows

- Docker 1.12 et 1.13
- Docker 17.03.0 et versions ultérieures

## <a name="installing-and-configuring-hello-solution"></a>L’installation et la configuration de solution de hello
Utilisez hello suivant tooinstall des informations et configurer une solution de hello.

1. Ajouter hello conteneur analyse solution tooyour espace de travail OMS à partir de [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) ou à l’aide de hello est décrite dans [solutions Analytique de journal ajouter à partir de la galerie des Solutions de hello](log-analytics-add-solutions.md).

2. Installez et utilisez Docker avec un agent OMS.  Selon votre système d’exploitation, vous pouvez choisir parmi hello méthodes suivantes :

  * Sur les systèmes d’exploitation Linux pris en charge, vous devez installer et exécuter Docker et puis installer et configurer hello [Agent OMS pour Linux](log-analytics-agent-linux.md).  
  * CoreOS, Impossible d’exécuter hello Agent OMS pour Linux. Au lieu de cela, vous exécutez une version en conteneur Hello Agent OMS pour Linux. Si vous utilisez des conteneurs dans Azure Government Cloud, consultez les sections relatives aux [hôtes de conteneurs Linux, y compris CoreOS](#for-all-linux-container-hosts-including-coreos) ou aux [hôtes de conteneurs Linux Azure Government, y compris CoreOS](#for-all-azure-government-linux-container-hosts-including-coreos).
  * Sur Windows Server 2016 et Windows 10, installez hello moteur Docker et le client, puis se connecter informations toogather agent et l’envoyer tooLog Analytique.  

### <a name="container-services"></a>Services de conteneur

- Si vous disposez d’un environnement Red Hat OpenShift, consultez [Configurer un agent OMS pour Red Hat OpenShift](#configure-an-oms-agent-for-red-hat-openshift).
- Si vous avez un cluster Kubernetes à l’aide de hello Service de conteneur Azure, consultez [surveiller un cluster du Service de conteneur Azure avec Microsoft Operations Management Suite (OMS)](../container-service/kubernetes/container-service-kubernetes-oms.md).
- Si vous possédez un cluster DC/OS Azure Container Service, consultez l’article [Surveiller un cluster DC/OS Azure Container Service avec Operations Management Suite](../container-service/dcos-swarm/container-service-monitoring-oms.md).
- Si vous avez un environnement en mode Docker Swarm, apprenez en plus en lisant [Configurer un agent OMS pour Docker Swarm](#configure-an-oms-agent-for-docker-swarm).
- Si vous utilisez des conteneurs avec Service Fabric, consultez [Vue d’ensemble d’Azure Service Fabric](../service-fabric/service-fabric-overview.md).
- Hello de révision [moteur Docker sur Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) article pour plus d’informations sur la façon tooinstall et configurer vos moteurs Docker sur les ordinateurs exécutant Windows.

> [!IMPORTANT]
> Docker doit être en cours d’exécution **avant** vous installez hello [Agent OMS pour Linux](log-analytics-agent-linux.md) sur vos ordinateurs hôtes de conteneur. Si vous avez déjà installé l’agent de hello avant d’installer Docker, vous devez tooreinstall hello Agent OMS pour Linux. Pour plus d’informations sur Docker, consultez hello [site Web de Docker](https://www.docker.com).


## <a name="linux-container-hosts"></a>Hôtes de conteneur Linux

Une fois que vous avez installé Docker, utilisez hello suivant les paramètres de votre agent de hello conteneur hôte tooconfigure pour une utilisation avec Docker. Vous devez commencer votre ID d’espace de travail OMS et la clé que vous pouvez trouver dans hello portail Azure. Dans votre espace de travail, cliquez sur **Quick Start** > **ordinateurs** tooview votre **ID de l’espace de travail** et **clé primaire**.  Copiez-collez ces deux valeurs dans votre éditeur favori.

### <a name="for-all-linux-container-hosts-except-coreos"></a>Pour tous les hôtes de conteneur Linux, à l’exception de CoreOS

- Pour plus d’informations sur la façon dont tooinstall hello Agent OMS pour Linux, consultez [connecter vos ordinateurs Linux de tooOperations Management Suite (OMS)](log-analytics-agent-linux.md).

### <a name="for-all-linux-container-hosts-including-coreos"></a>Pour tous les hôtes de conteneur Linux, avec CoreOS

Démarrer le conteneur d’OMS hello que vous souhaitez toomonitor. Modifier et utiliser hello l’exemple suivant :

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -e WSID="your workspace id" -e KEY="your key" -h=`hostname` -p 127.0.0.1:25225:25225 --name="omsagent" --restart=always microsoft/oms
```

### <a name="for-all-azure-government-linux-container-hosts-including-coreos"></a>Pour tous les hôtes de conteneur Linux Azure Government, y compris CoreOS

Démarrer le conteneur d’OMS hello que vous souhaitez toomonitor. Modifier et utiliser hello l’exemple suivant :

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -v /var/log:/var/log -e WSID="your workspace id" -e KEY="your key" -e DOMAIN="opinsights.azure.us" -p 127.0.0.1:25225:25225 -p 127.0.0.1:25224:25224/udp --name="omsagent" -h=`hostname` --restart=always microsoft/oms
```

### <a name="switching-from-using-an-installed-linux-agent-tooone-in-a-container"></a>Basculement à partir de l’aide d’un tooone de l’agent Linux installé dans un conteneur
Si vous utilisé agent de hello directement installé précédemment et que vous souhaitez utiliser tooinstead un agent en cours d’exécution dans un conteneur, vous devez d’abord supprimer hello Agent OMS pour Linux. Consultez [désinstallation hello Agent OMS pour Linux](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) toounderstand comment toosuccessfully désinstaller hello agent.  

### <a name="configure-an-oms-agent-for-docker-swarm"></a>Configurer un agent OMS pour Docker Swarm

Vous pouvez exécuter hello Agent OMS en tant qu’un service global sur Docker Swarm. Utilisez hello suivant informations toocreate un service de l’Agent OMS. Vous devez tooinsert votre ID d’espace de travail OMS et la clé primaire.

- Exécutez la procédure suivante hello sur le nœud principal de hello.

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock  -e WSID="<WORKSPACE ID>" -e KEY="<PRIMARY KEY>" -p 25225:25225 -p 25224:25224/udp  --restart-condition=on-failure microsoft/oms
    ```

### <a name="configure-an-oms-agent-for-red-hat-openshift"></a>Configurer un agent OMS pour Red Hat OpenShift
Il existe trois façons tooadd hello Agent OMS tooRed Hat OpenShift toostart collecte conteneur analyse des données.

* [Installer hello Agent OMS pour Linux](log-analytics-agent-linux.md) directement sur chaque nœud OpenShift  
* [Activer l’extension de machine virtuelle Log Analytics](log-analytics-azure-vm-extension.md) sur chaque nœud OpenShift résidant dans Azure  
* Installer hello Agent OMS en tant qu’un ensemble de démon OpenShift  

Dans cette section nous couvrent hello étapes tooinstall requis hello OMS Agent comme un ensemble de démon OpenShift.  

1. Ouverture de session toohello OpenShift nœud et copie hello yaml fichier maître [ocp-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) à partir de GitHub tooyour maître de nœud et de modifier la valeur hello avec votre ID d’espace de travail OMS et votre clé primaire.
2. Exécution d’un projet hello suivant de commandes toocreate pour OMS et définir le compte d’utilisateur hello.

    ```
    oadm new-project omslogging --node-selector='zone=default'
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. toodeploy hello démon-set, exécutez la commande suivante hello :

    `oc create -f ocp-omsagent.yaml`

5. tooverify, il est configuré et fonctionne correctement, tapez hello qui suit :

    `oc describe daemonset omsagent`  

    et hello sortie doit ressembler à :

    ```
    [ocpadmin@khm-0 ~]$ oc describe ds oms  
    Name:           oms  
    Image(s):       microsoft/oms  
    Selector:       name=omsagent  
    Node-Selector:  zone=default  
    Labels:         agentVersion=1.4.0-12  
                    dockerProviderVersion=10.0.0-25  
                    name=omsagent  
    Desired Number of Nodes Scheduled: 3  
    Current Number of Nodes Scheduled: 3  
    Number of Nodes Misscheduled: 0  
    Pods Status:    3 Running / 0 Waiting / 0 Succeeded / 0 Failed  
    No events.  
    ```

Si vous souhaitez toouse secrets toosecure votre ID d’espace de travail OMS et la clé primaire lors de l’utilisation du fichier de jeu de démon yaml hello Agent OMS, effectuer hello comme suit.

1. Ouverture de session toohello OpenShift nœud et copie hello yaml fichier maître [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) et la clé secrète de la génération du script [ocp-secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) à partir de GitHub.  Ce script générera le fichier d’yaml hello secrets pour l’ID d’espace de travail OMS et la clé primaire toosecure votre SÉCRÉTER plus d’informations.  
2. Exécution d’un projet hello suivant de commandes toocreate pour OMS et définir le compte d’utilisateur hello. secret Hello génération du script vous demande votre ID d’espace de travail OMS <WSID> et la clé primaire <KEY> à la fin, il crée des fichiers d’ocp-secret.yaml hello.  

    ```
    oadm new-project omslogging --node-selector='zone=default'  
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. Déployer le fichier de secret principal hello en exécutant hello suivante :

    `oc create -f ocp-secret.yaml`

5. Vérifier le déploiement en exécutant hello suivante :

    `oc describe secret omsagent-secret`  

    et hello sortie doit ressembler à :  

    ```
    [ocpadmin@khocp-master-0 ~]$ oc describe ds oms  
    Name:           oms  
    Image(s):       microsoft/oms  
    Selector:       name=omsagent  
    Node-Selector:  zone=default  
    Labels:         agentVersion=1.4.0-12  
                    dockerProviderVersion=10.0.0-25  
                    name=omsagent  
    Desired Number of Nodes Scheduled: 3  
    Current Number of Nodes Scheduled: 3  
    Number of Nodes Misscheduled: 0  
    Pods Status:    3 Running / 0 Waiting / 0 Succeeded / 0 Failed  
    No events.  
    ```

6. Déployer le fichier de jeu de démon yaml de l’Agent OMS hello en exécutant hello suivante :

    `oc create -f ocp-ds-omsagent.yaml`  

7. Vérifier le déploiement en exécutant hello suivante :

    `oc describe ds oms`

    et hello sortie doit ressembler à :

    ```
    [ocpadmin@khocp-master-0 ~]$ oc describe secret omsagent-secret  
    Name:           omsagent-secret  
    Namespace:      omslogging  
    Labels:         <none>  
    Annotations:    <none>  

    Type:   Opaque  

     Data  
     ====  
     KEY:    89 bytes  
     WSID:   37 bytes  
    ```

### <a name="secure-your-secret-information-for-docker-swarm-and-kubernetes"></a>Sécuriser vos informations secrètes pour Docker Swarm et Kubernetes

Vous pouvez sécuriser l’ID d’espace de travail OMS et les clés primaires pour les services de conteneur Docker Swarm et Kubernetes.

#### <a name="secure-secrets-for-docker-swarm"></a>Sécuriser les secrets pour Docker Swarm

Pour Docker Swarm, une fois le secret hello pour l’ID de l’espace de travail et la clé primaire est créé, vous pouvez exécuter hello créer le service de Docker hello pour OMSagent. Utilisez hello suivant informations toocreate vos informations confidentielles.

1. Exécutez la procédure suivante hello sur le nœud principal de hello.

    ```
    echo "WSID" | docker secret create WSID -
    echo "KEY" | docker secret create KEY -
    ```

2. Vérifiez que les secrets ont été créés correctement.

    ```
    keiko@swarmm-master-13957614-0:/run# sudo docker secret ls
    ```

    ```
    ID                          NAME                CREATED             UPDATED
    j2fj153zxy91j8zbcitnjxjiv   WSID                43 minutes ago      43 minutes ago
    l9rh3n987g9c45zffuxdxetd9   KEY                 38 minutes ago      38 minutes ago
    ```

3. Exécution hello suivant commande toomount hello secrets toohello placées dans des conteneurs de l’Agent OMS.

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock --secret source=WSID,target=WSID --secret source=KEY,target=KEY  -p 25225:25225 -p 25224:25224/udp --restart-condition=on-failure microsoft/oms
    ```

#### <a name="secure-secrets-for-kubernetes-with-yaml-files"></a>Sécuriser des secrets pour Kubernetes avec des fichiers yaml

Pour Kubernetes, vous utilisez un fichier de script toogenerate hello secrets yaml pour votre ID d’espace de travail et la clé primaire. À hello [OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) page, il existe des fichiers que vous pouvez utiliser avec ou sans vos informations confidentielles.

- Hello DaemonSet de l’Agent OMS par défaut n’a pas d’informations confidentielles (omsagent.yaml)
- fichier d’yaml Hello DaemonSet de l’Agent OMS utilise des informations confidentielles (omsagent-ds-secrets.yaml) avec secret fichier génération de scripts toogenerate hello secrets yaml (omsagentsecret.yaml).

Vous pouvez choisir toocreate omsagent DaemonSets avec ou sans les clés secrètes.

##### <a name="default-omsagent-daemonset-yaml-file-without-secrets"></a>Le fichier yaml par défaut DaemonSet de l’agent OMS sans secrets

- Hello fichier par défaut OMS Agent DaemonSet yaml, remplacez hello `<WSID>` et `<KEY>` tooyour WSID et la clé. Copiez nœud maître du tooyour fichier hello et suivante d’exécution hello :

    ```
    sudo kubectl create -f omsagent.yaml
    ```

##### <a name="default-omsagent-daemonset-yaml-file-with-secrets"></a>Le fichier yaml par défaut DaemonSet de l’agent OMS avec secrets

1. toouse DaemonSet de l’Agent OMS à l’aide des informations confidentielles, les secrets hello d’abord créer.
    1. Copiez le script de hello et fichier de modèle de secret principal et assurez-vous qu’ils sont sur hello même répertoire.
        - Script de génération de secrets - secret-gen.sh
        - Modèle de secret - secret-template.yaml
    2. Exécutez le script de hello comme hello l’exemple suivant. script de Hello demande hello ID d’espace de travail OMS et la clé primaire et une fois que vous les entrez, script de hello crée un fichier de secret principal yaml, vous pouvez l’exécuter.   

        ```
        #> sudo bash ./secret-gen.sh
        ```

    3. Créer des pod de secrets hello en exécutant hello suivante :
        ```
        sudo kubectl create -f omsagentsecret.yaml
        ```

    4. tooverify, exécutez hello suivante :

        ```
        keiko@ubuntu16-13db:~# sudo kubectl get secrets
        ```

        La sortie doit ressembler à :

        ```
        NAME                  TYPE                                  DATA      AGE
        default-token-gvl91   kubernetes.io/service-account-token   3         50d
        omsagent-secret       Opaque                                2         1d
        ```

        ```
        keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
        ```

        La sortie doit ressembler à :

        ```
        Name:           omsagent-secret
        Namespace:      default
        Labels:         <none>
        Annotations:    <none>

        Type:   Opaque

        Data
        ====
        WSID:   36 bytes
        KEY:    88 bytes
        ```

    5. Créer votre DaemonsSet de l’agent OMS en exécutant ``` sudo kubectl create -f omsagent-ds-secrets.yaml ```

2. Vérifiez que hello que daemonset de l’Agent OMS est en cours d’exécution, toohello comme suit :

    ```
    keiko@ubuntu16-13db:~# sudo kubectl get ds omsagent
    ```

    ```
    NAME       DESIRED   CURRENT   NODE-SELECTOR   AGE
    omsagent   3         3         <none>          1h
    ```


Pour Kubernetes, utilisez un fichier de script toogenerate hello secrets yaml pour l’ID de l’espace de travail et la clé primaire. Hello utilisez informations exemple avec hello suivantes [omsagent yaml fichier](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml) toosecure vos informations confidentielles.

```
keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
Name:           omsagent-secret
Namespace:      default
Labels:         <none>
Annotations:    <none>

Type:   Opaque

Data
====
WSID:   36 bytes
KEY:    88 bytes
```

## <a name="windows-container-hosts"></a>Hôtes de conteneur Windows

### <a name="preparation-before-installing-windows-agents"></a>Préparation préalable à l’installation des agents Windows

Avant d’installer des agents sur les ordinateurs exécutant Windows, vous devez le service de Docker tooconfigure hello. configuration de Hello autorise hello Windows hello ou l’agent Analytique de journal machine virtuelle extension toouse hello de socket TCP de Docker afin que les agents hello peuvent accéder au démon Docker de hello à distance et les données toocapture l’analyse.

#### <a name="toostart-docker-and-verify-its-configuration"></a>toostart Docker et vérifiez sa configuration.

Il existe tooset étapes nécessaires de TCP, canal nommé pour Windows Server :

1. Dans Windows PowerShell, activez les canaux TCP et nommé.

    ```
    Stop-Service docker
    dockerd --unregister-service
    dockerd --register-service -H npipe:// -H 0.0.0.0:2375  
    Start-Service docker
    ```

2. Configurer Docker avec le fichier de configuration hello pour le canal de communication TCP et le canal nommé. fichier de configuration Hello se trouve dans C:\ProgramData\docker\config\daemon.json.

    Dans le fichier de daemon.json hello, vous devrez suivant de hello :

    ```
    {
    "hosts": ["tcp://0.0.0.0:2375", "npipe://"]
    }
    ```

Pour plus d’informations sur la configuration du démon Docker hello utilisée avec des conteneurs Windows, consultez [moteur Docker sur Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).


### <a name="install-windows-agents"></a>Installer les agents Windows

tooenable Windows et conteneur Hyper-V à l’analyse, installez hello Microsoft Monitoring Agent (MMA) sur les ordinateurs Windows qui sont des hôtes de conteneur. Pour les ordinateurs exécutant Windows dans votre environnement local, consultez [tooLog d’ordinateurs Windows de se connecter Analytique](log-analytics-windows-agents.md). Pour les ordinateurs virtuels en cours d’exécution dans Azure, les connecter tooLog Analytique à l’aide de hello [extension de machine virtuelle](log-analytics-azure-vm-extension.md).

Vous pouvez surveiller les conteneurs Windows en cours d’exécution sur Service Fabric. Toutefois, seules les [machines virtuelles qui s’exécutent dans Azure](log-analytics-azure-vm-extension.md) et les [ordinateurs exécutant Windows dans votre environnement local](log-analytics-windows-agents.md) sont actuellement pris en charge pour Service Fabric.

Vous pouvez vérifier que hello solution d’analyse de conteneur est correctement configuré pour Windows. toocheck si le pack d’administration hello était téléchargement correctement, recherchez *ContainerManagement.xxx*. fichiers de Hello doivent être dans le dossier C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs de hello.


## <a name="solution-components"></a>Composants de la solution

Si vous utilisez des agents Windows, puis hello Pack d’administration suivant est installé sur chaque ordinateur sur lequel un agent lorsque vous ajoutez cette solution. Aucune configuration ou maintenance n’est requis pour le pack d’administration hello.

- *ContainerManagement.xxx* installé dans le dossier C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs

## <a name="container-data-collection-details"></a>Détails sur la collecte de données des conteneurs
Hello solution d’analyse de conteneur collecte diverses données de journaux et des métriques de performances à partir des hôtes de conteneurs et les conteneurs à l’aide d’agents que vous activez.

Données sont collectées toutes les trois minutes par hello suivant les types d’agents.

- [Agent OMS pour Linux](log-analytics-linux-agents.md)
- [Agent Windows](log-analytics-windows-agents.md)
- [Extension de machine virtuelle Log Analytics](log-analytics-azure-vm-extension.md)


### <a name="container-records"></a>Enregistrements de conteneur

Hello tableau suivant présente des exemples d’enregistrements collectées par la solution d’analyse de conteneur hello et types de données hello qui s’affichent dans les résultats de recherche de journal.

| Type de données | Type de données dans Recherche de journaux | Champs |
| --- | --- | --- |
| Performances des hôtes et des conteneurs | `Type=Perf` | Computer, ObjectName, CounterName &#40;%Processor Time, Disk Reads MB, Disk Writes MB, Memory Usage MB, Network Receive Bytes, Network Send Bytes, Processor Usage sec, Network&#41;, CounterValue,TimeGenerated, CounterPath, SourceSystem |
| Inventaire de conteneur | `Type=ContainerInventory` | TimeGenerated, Computer, container name, ContainerHostname, Image, ImageTag, ContainerState, ExitCode, EnvironmentVar, Command, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID |
| Inventaire d’image de conteneur | `Type=ContainerImageInventory` | TimeGenerated, Computer, Image, ImageTag, ImageSize, VirtualSize, Running, Paused, Stopped, Failed, SourceSystem, ImageID, TotalContainer |
| Journal de conteneur | `Type=ContainerLog` | TimeGenerated, Computer, image ID, container name, LogEntrySource, LogEntry, SourceSystem, ContainerID |
| Journal de service de conteneur | `Type=ContainerServiceLog`  | TimeGenerated, Computer, TimeOfCommand, Image, Command, SourceSystem, ContainerID |
| Inventaire du nœud de conteneur | `Type=ContainerNodeInventory_CL`| TimeGenerated, Computer, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem|
| Inventaire de Kubernetes | `Type=KubePodInventory_CL` | TimeGenerated, Computer, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem |
| Processus de conteneur | `Type=ContainerProcess_CL` | TimeGenerated, Computer, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem |
| Événements Kubernetes | `Type=KubeEvents_CL` | TimeGenerated, Computer, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, Message |

Étiquettes ajouté trop*PodLabel* des types de données sont vos propres étiquettes personnalisées. Hello ajouté PodLabel étiquettes indiqués dans la table de hello sont des exemples. Par conséquent, `PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s` seront différentes dans le jeu de données de votre environnement et ressembleront à `PodLabel_yourlabel_s`.


## <a name="monitor-containers"></a>Analyser les conteneurs
Après avoir configuré solution hello activée dans le portail OMS de hello, hello **conteneurs** vignette affiche des informations résumées concernant vos hôtes de conteneurs et les conteneurs hello en cours d’exécution dans des hôtes.

![Vignette Conteneurs](./media/log-analytics-containers/containers-title.png)

vignette de Hello montre une vue d’ensemble des conteneurs combien vous avez dans l’environnement de hello et si elles sont ont échoué, en cours d’exécution ou arrêté.

### <a name="using-hello-containers-dashboard"></a>À l’aide du tableau de bord hello conteneurs
Cliquez sur hello **conteneurs** vignette. À partir de là, vous voyez les vues organisées par :

- **Événements de conteneur** : affiche l’état du conteneur et les ordinateurs dont le conteneur a échoué.
- **Journaux du conteneur** -affiche un graphique des fichiers journaux de conteneur générés au fil du temps et une liste d’ordinateurs avec hello plus grand nombre de fichiers journaux.
- **Événements de Kubernetes** -affiche un graphique des événements Kubernetes générés au fil du temps et une liste des raisons hello pourquoi POD généré les événements hello. *Ce jeu de données est utilisé uniquement dans les environnements Linux.*
- **Inventaire de Namespace Kubernetes** - affiche le nombre de hello d’espaces de noms et les blocs et affiche leur hiérarchie. *Ce jeu de données est utilisé uniquement dans les environnements Linux.*
- **Inventaire de nœud conteneur** -affiche le nombre hello des types d’orchestration utilisé sur les nœuds/hôtes de conteneur. nœuds d’ordinateur Hello/hôtes sont également répertoriés par nombre hello de conteneurs. *Ce jeu de données est utilisé uniquement dans les environnements Linux.*
- **Inventaire des Images de conteneur** -affiche le nombre total de hello d’images de conteneur utilisé et le nombre de types d’images. nombre de Hello d’images est également répertorié par balise d’image hello.
- **État de conteneurs** -affiche nombre total de hello du conteneur ordinateurs nœuds/hôte conteneurs en cours d’exécution. Les ordinateurs sont également répertoriés par nombre hello des ordinateurs hôtes en cours d’exécution.
- **Processus de conteneur** : affiche un graphique en courbes représentant les processus de conteneur exécutés jusqu’à maintenant. Les conteneurs peuvent également être répertoriés en exécutant la commande /process dans les conteneurs. *Ce jeu de données est utilisé uniquement dans les environnements Linux.*
- **Les performances de l’UC de conteneur** -affiche un graphique en courbes de hello utilisation moyenne du processeur au fil du temps pour les nœuds/hôtes d’ordinateur. Également listes hello ordinateur/hôtes de nœuds en fonction de moyenne de l’UC.
- **Performances de la mémoire du conteneur** : affiche un graphique en courbes représentant l’utilisation de la mémoire jusqu’à maintenant. Répertorie également l’utilisation de la mémoire par l’ordinateur en fonction du nom de l’instance.
- **Performances de l’ordinateur** -affiche les graphiques en courbes de % hello de performances de l’UC au fil du temps, pourcentage d’utilisation de mémoire dans le temps et mégaoctets d’espace disque libre au fil du temps. Vous pouvez pointer sur n’importe quelle ligne dans un graphique de tooview plus de détails.


Chaque zone du tableau de bord hello est une représentation visuelle d’une recherche qui est exécutée sur les données collectées.

![Tableau de bord Conteneurs](./media/log-analytics-containers/containers-dash01.png)

![Tableau de bord Conteneurs](./media/log-analytics-containers/containers-dash02.png)

Bonjour **état du conteneur** zone, cliquez sur zone supérieure de hello, comme indiqué ci-dessous.

![État des conteneurs](./media/log-analytics-containers/containers-status.png)

Recherche de journal s’ouvre et affiche des informations sur l’état de hello vos conteneurs.

![Recherche de journal pour les conteneurs](./media/log-analytics-containers/containers-log-search.png)

À ce stade, vous pouvez modifier toomodify de requête de recherche hello elle des informations spécifiques hello toofind vous intéresse. Pour plus d’informations sur les recherches dans les journaux, voir [Recherches de journal dans Log Analytics](log-analytics-log-searches.md).

## <a name="troubleshoot-by-finding-a-failed-container"></a>Résoudre des problèmes en recherchant un conteneur en échec

Log Analytics marque un conteneur comme étant en **Échec** s’il a été fermé avec un code de sortie autre que zéro. Vous pouvez voir une vue d’ensemble des erreurs de hello et des défaillances dans un environnement hello Bonjour **Échec de conteneurs** zone.

### <a name="toofind-failed-containers"></a>conteneurs de toofind a échoué
1. Cliquez sur hello **état du conteneur** zone.  
   ![État des conteneurs](./media/log-analytics-containers/containers-status.png)
2. Recherche de journal s’ouvre et affiche hello de l’état de vos conteneurs, toohello comme suit.  
   ![État des conteneurs](./media/log-analytics-containers/containers-log-search.png)
3. Ensuite, cliquez sur la valeur hello agrégé des informations supplémentaires de tooview de conteneurs ayant échoué. Développez **afficher plus** tooview hello image ID.  
   ![Conteneurs défectueux](./media/log-analytics-containers/containers-state-failed.png)  
4. Ensuite, tapez hello texte suivant dans la requête de recherche hello. `Type=ContainerInventory <ImageID>`toosee des détails sur l’image hello telles que la taille de l’image et le nombre d’images arrêtés et a échoué.  
   ![Conteneurs défectueux](./media/log-analytics-containers/containers-failed04.png)

## <a name="search-logs-for-container-data"></a>Rechercher des données de conteneur dans les journaux
Lorsque vous êtes à résoudre une erreur spécifique, il peut aider à toosee où il se produit dans votre environnement. Hello, les types de journaux suivants vous aideront à créer des requêtes tooreturn hello informations.


- **ContainerImageInventory** : utilisez ce type lorsque vous essayez d’informations toofind organisées par image et tooview image les informations telles que les ID d’image ou des tailles.
- **ContainerInventory** : utilisez ce type de journal lorsque vous recherchez des informations sur l’emplacement des conteneurs, leurs noms et les images qu’ils exécutent.
- **ContainerLog** : utilisez ce type lorsque vous souhaitez que les informations concernant les journaux d’erreurs toofind et les entrées.
- **ContainerNodeInventory_CL** Utilisez ce type lorsque vous souhaitez que des informations sur le nœud d’hôte hello où résident des conteneurs. Il fournit la version Docker, le type d’orchestration, ainsi que des informations relatives au stockage et au réseau.
- **ContainerProcess_CL** tooquickly de ce type d’utilisation Voir processus hello en cours d’exécution dans le conteneur de hello.
- **ContainerServiceLog** : utilisez ce type lorsque vous essayez d’informations de piste d’audit toofind pour hello démon Docker, telles que Démarrer, arrêter, supprimer ou extraire les commandes.
- **KubeEvents_CL** utiliser ce type toosee hello Kubernetes les événements.
- **KubePodInventory_CL** Utilisez ce type lorsque vous souhaitez que les informations de hiérarchie toounderstand hello cluster.


### <a name="toosearch-logs-for-container-data"></a>journaux toosearch pour les données de conteneur
* Choisissez une image que vous connaissez récemment a échoué et rechercher les journaux d’erreurs hello. Commencez par rechercher un nom de conteneur exécutant cette image avec une recherche **ContainerInventory**. Par exemple, recherchez `Type=ContainerInventory ubuntu Failed`  
    ![Recherche de conteneurs Ubuntu](./media/log-analytics-containers/search-ubuntu.png)

  Hello le nom du conteneur de hello ensuite trop**nom**et recherchez ces journaux. Dans cet exemple, il s’agit de `Type=ContainerLog cranky_stonebreaker`.

**Afficher les informations de performances**

Lorsque vous êtes à partir de requêtes de tooconstruct, il peut aider à toosee ce qui est tout d’abord possible. Par exemple, toosee toutes les données de performances, essayez une requête large en tapant hello suivant recherche de requête.

```
Type=Perf
```

![Performances des conteneurs](./media/log-analytics-containers/containers-perf01.png)

Vous pouvez limiter les données de performances hello que vous voyez tooa les conteneur spécifique en tapant le nom hello de celui-ci toohello à droite de votre requête.

```
Type=Perf <containerName>
```

Qui affiche la liste hello des métriques de performances sont collectées pour un conteneur.

![Performances des conteneurs](./media/log-analytics-containers/containers-perf03.png)

## <a name="example-log-search-queries"></a>Exemples de requêtes de recherche de journal
Toobuild souvent utile de ses requêtes en commençant par un exemple d’une ou deux, puis en modifiant les toofit votre environnement. Comme point de départ, vous pouvez expérimenter hello **exemples de requêtes** toohelp zone vous générez des requêtes plus avancées.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Requêtes de conteneurs](./media/log-analytics-containers/containers-queries.png)


## <a name="saving-log-search-queries"></a>Enregistrement de requêtes de recherche de journal
L’enregistrement des requêtes est une fonctionnalité standard dans Log Analytics. En les enregistrant, vous aurez aisément accès à celles que vous avez trouvées utiles pour une utilisation ultérieure.

Après avoir créé une requête qui vous être utiles, l’enregistrer en cliquant sur **favoris** haut hello de page de recherche de journal hello. Ensuite, vous pouvez facilement y accéder ultérieurement à partir de hello **mon tableau de bord** page.

## <a name="next-steps"></a>Étapes suivantes
* [Rechercher des journaux](log-analytics-log-searches.md) tooview détaillé des enregistrements de données de conteneur.
