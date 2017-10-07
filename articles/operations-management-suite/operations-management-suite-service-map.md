---
title: aaaUse hello solution de carte de Service dans Operations Management Suite | Documents Microsoft
description: "Carte de service est une solution de Operations Management Suite qui découvre automatiquement les composants de l’application sur Windows et cartes et les systèmes Linux hello la communication entre les services. Cet article fournit des informations sur le déploiement de Service Map dans votre environnement et son utilisation dans divers scénarios."
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: 3ceb84cc-32d7-4a7a-a916-8858ef70c0bd
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/22/2016
ms.author: daseidma;bwren;dairwin
ms.openlocfilehash: f7c209182c9171cc520192ac13ca4d85174081b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-service-map-solution-in-operations-management-suite"></a>Utiliser des solutions de carte de Service hello dans Operations Management Suite
Carte de service découvre automatiquement les composants de l’application sur les systèmes Windows et Linux et mappages hello la communication entre les services. Avec la carte de Service, vous pouvez afficher vos serveurs de façon hello que vous pensez d'entre eux : en tant que réseaux interconnectés qui fournissent des services critiques. Carte de service affiche les connexions entre les serveurs, les processus et les ports sur n’importe quelle architecture TCP connectés, sans aucune configuration autre que hello installation d’un agent.

Cet article décrit les détails de hello d’à l’aide de la carte de Service. Pour plus d’informations sur la configuration de la solution Service Map et l’intégration d’agents, voir [Configuration de la solution Service Map dans Operations Management Suite (OMS)](operations-management-suite-service-map-configure.md).


## <a name="use-cases-make-your-it-processes-dependency-aware"></a>Cas d’utilisation : Intégrer la dépendance dans les processus informatiques

### <a name="discovery"></a>Découverte
Service Map crée automatiquement une carte de référence commune des dépendances entre vos serveurs, les processus et les services tiers. Il découvre et mappe toutes les dépendances TCP, identification surprise connexions à distance des systèmes tiers que vous dépendez et dépendances tootraditional sombre des zones du réseau, tels qu’Active Directory. Carte de service détecte les connexions réseau que vos systèmes gérés tentent de toomake, vous aident à identifier une mauvaise configuration de serveur potentiels, interruption de service et les problèmes de réseau.

### <a name="incident-management"></a>Gestion des incidents
Carte de service vous aide à éliminer le hasard hello d’isolation des problèmes en vous montrant comment les systèmes sont connectés et affecter les uns des autres. En outre tooidentifying connexions qui ont échoué, il vous aide à identifier les équilibreurs de charge mal configuré, étonnant ou excessive de charge sur les services critiques et non autorisés de clients, tels que les ordinateurs des développeurs communique avec les systèmes tooproduction. À l’aide de flux de travail intégrés avec Operations Management Suite de suivi des modifications, vous pouvez également voir si un événement de modification sur un ordinateur de serveur principal ou d’un service explique la cause première hello d’un incident.

### <a name="migration-assurance"></a>Garantie d’une migration réussie
La solution Service Map vous permet de planifier, d’accélérer et de valider efficacement les migrations vers Azure pour vous assurer que rien n’est oublié et vous prémunir contre toute panne surprise. Vous pouvez détecter, interdépendants tous les systèmes qui toomigrate besoin ensemble, évaluer la capacité et configuration du système et déterminer si un système en cours d’exécution est toujours desservant les utilisateurs ou constitue un candidat pour la mise hors service au lieu de la migration. Une fois hello déplacement terminé, vous pouvez vérifier sur tooverify de charge et l’identité client qui testent les systèmes et les clients sont connectent. Si vous rencontrez des problèmes vos définitions de planification et de pare-feu de sous-réseau, les connexions ayant échouées dans les mappages de carte de Service point toohello les systèmes nécessitant une connectivité.

### <a name="business-continuity"></a>Continuité de l’activité
Si vous utilisez Azure Site Recovery et devez aide définissant la séquence de restauration hello pour votre environnement d’application, carte de Service automatiquement vous indique comment les systèmes s’appuient sur eux tooensure que votre plan de récupération est fiable. En choisissant un serveur critique ou un groupe et en affichant ses clients, vous pouvez identifier le toorecover de systèmes frontaux une fois que le serveur de hello est restaurée et disponible. À l’inverse, en examinant les dépendances des principaux des serveurs critiques, vous pouvez identifier le systèmes toorecover avant la restauration de vos systèmes de focus.

### <a name="patch-management"></a>Gestion des correctifs
Carte de service améliore l’utilisation de hello évaluation des mises à jour du système Operations Management Suite en vous montrant autres équipes et les serveurs varie en fonction de votre service, afin de les avertir à l’avance d’avant de mettre vos systèmes de mise à jour corrective. La solution Service Map facilite également la gestion des correctifs dans Operations Management Suite en vous montrant si vos services sont disponibles et connectés correctement après application de la mise à jour corrective et redémarrage.


## <a name="mapping-overview"></a>Vue d’ensemble du mappage
Agents de la carte de service recueillir des informations sur tous les processus de connexion TCP sur le serveur hello où elles sont installées et plus d’informations sur hello les connexions entrantes et sortantes pour chaque processus. Dans la liste hello dans le volet gauche de hello, vous pouvez sélectionner des machines ou des groupes qui ont toovisualize des agents de carte de Service à leurs dépendances sur une plage de temps spécifié. Dépendance de l’ordinateur mappe le focus sur un ordinateur spécifique, et elles affichent toutes les machines de hello sont les clients TCP directs ou des serveurs de la machine.  Les cartes de groupe d’ordinateurs montrent des ensembles de serveurs et leurs dépendances.

![Vue d’ensemble de Service Map](media/oms-service-map/service-map-overview.png)

Les ordinateurs peuvent être développés dans hello de tooshow hello carte en cours d’exécution des processus avec des connexions réseau actives pendant l’intervalle de temps hello sélectionné. Lorsqu’un ordinateur distant avec un agent de carte de Service est développé tooshow détails du processus, que les processus qui communiquent avec l’ordinateur de focus hello sont affichés. nombre Hello d’ordinateurs frontales sans agent qui se connectent à machine de focus hello est indiqué sur le côté gauche de hello de processus hello à qu'ils se connectent. Si la machine de focus hello effectue un ordinateur principal tooa connexion n’a aucun agent, serveur principal de hello est incluse dans un groupe de ports du serveur, ainsi que d’autres connexions toohello même numéro de port.

Par défaut, la carte de Service mappe afficher hello 30 dernières minutes d’informations de dépendance. À l’aide de contrôles hello au coin supérieur gauche de hello, vous pouvez interroger les mappages pour les plages horaires historiques de configuration tooshow d’heure tooone comment rechercher des dépendances Bonjour passé (par exemple, pendant un incident ou avant une modification s’est produite). Les données Service Map sont stockées pendant 30 jours dans les espaces de travail payants et pendant 7 jours dans les espaces de travail gratuits.

## <a name="status-badges-and-border-coloring"></a>Badges d’état et couleur de bordure
À hello en bas de chaque serveur de mappage de hello peut être une liste de badges état transporter les informations d’état sur le serveur de hello. les badges Hello indiquent qu’il existe des informations pertinentes pour le serveur hello à partir d’une des intégrations de solution hello Operations Management Suite. Cliquez sur un badge pour accéder directement toohello les détails de l’état de hello dans le volet de droite hello. Hello badges d’état disponibles incluent actuellement les alertes, Service d’assistance, modifications, la sécurité et mises à jour.

Selon la gravité de hello de badges d’état hello, bordures de nœud d’ordinateur peuvent être de couleur rouge (critique), jaune (avertissement) ou bleu (informations). couleur de Hello représente hello pire état de badges d’état hello. Une bordure de couleur grise indique un nœud dépourvu d’indicateur d’état.

![Badges d’état](media/oms-service-map/status-badges.png)

## <a name="machine-groups"></a>Groupes de machines
Groupes d’ordinateurs permettent maps toosee vous centrées autour d’un ensemble de serveurs, pas seulement un afin de voir tous les membres de hello d’un cluster à plusieurs niveaux de l’application ou le serveur dans un mappage.

Les utilisateurs sélectionnent les serveurs regroupés dans un groupe et choisissez un nom pour le groupe de hello.  Vous pouvez ensuite choisissez tooview hello un groupe avec tous ses processus et les connexions, ou afficher uniquement avec les processus hello et les connexions qui sont directement liées toohello autres membres du groupe de hello.

![Groupe de machines](media/oms-service-map/machine-group.png)

### <a name="creating-a-machine-group"></a>Création d’un groupe de machines
toocreate un groupe, sélectionnez hello ou des ordinateurs souhaité dans les Machines hello liste et cliquez sur **ajouter toogroup**.

![Créer un groupe](media/oms-service-map/machine-groups-create.png)

Vous pouvez alors choisir **nouvel** et attribuez un nom hello groupe.

![Nommer un groupe](media/oms-service-map/machine-groups-name.png)

>[!NOTE]
>Groupes d’ordinateurs sont actuellement limitées too10 serveurs, mais nous prévoyons de cette limite tooincrease bientôt.

### <a name="viewing-a-group"></a>Affichage d’un groupe
Une fois que vous avez créé des groupes, vous pouvez les afficher en choisissant l’onglet de groupes hello.

![Onglet Groupes](media/oms-service-map/machine-groups-tab.png)

Puis sélectionnez carte hello tooview de nom de groupe hello pour ce groupe d’ordinateurs.
![Groupe de machines](media/oms-service-map/machine-group.png) machines hello appartenant toohello groupe sont décrites en blanc dans le mappage de hello.

Expansion hello groupe va répertorier les machines hello qui composent hello groupe d’ordinateurs.

![Ordinateurs d’un groupe de machines](media/oms-service-map/machine-groups-machines.png)

### <a name="filter-by-processes"></a>Filtrer par processus
Vous pouvez activer/désactiver la vue de mappage hello entre l’affichage de tous les processus et les connexions dans le groupe de hello et uniquement hello ceux qui sont directement liées toohello groupe d’ordinateurs.  Hello vue par défaut est tooshow tous les processus.  Vous pouvez modifier la vue de hello en cliquant sur icône de filtre hello au-dessus de carte de hello.

![Groupe de filtres](media/oms-service-map/machine-groups-filter.png)

Lorsque **tous les processus** est sélectionnée, le mappage de hello inclura tous les processus et les connexions sur chacun des ordinateurs de hello Bonjour groupe.

![Tous les processus d’un groupe de machines](media/oms-service-map/machine-groups-all.png)

Si vous modifiez hello vue tooshow uniquement **connecté-groupe de processus**, carte de hello est réduite bas tooonly les processus et les connexions qui sont directement connectés tooother des ordinateurs dans le groupe de hello, création d’une vue simplifiée.

![Processus filtrés d’un groupe de machines](media/oms-service-map/machine-groups-filtered.png)
 
### <a name="adding-machines-tooa-group"></a>Ajout du groupe ordinateurs tooa
tooadd machines tooan les groupe existant, vérifiez hello zones suivant toohello machines, puis cliquez sur **ajouter toogroup**.  Ensuite, sélectionnez le groupe hello vous voulez que les machines hello tooadd.
 
### <a name="removing-machines-from-a-group"></a>Suppression de machines d’un groupe
Dans la liste des groupes de hello, développez hello groupe nom toolist hello machines dans hello groupe d’ordinateurs.  Ensuite, cliquez sur hello sélection menu suivant toohello machine tooremove puis choisissez **supprimer**.

![Supprimer une machine d’un groupe](media/oms-service-map/machine-groups-remove.png)

### <a name="removing-or-renaming-a-group"></a>Suppression ou changement de nom d’un groupe
Cliquez sur hello sélection menu suivant toohello nom du groupe dans la liste de groupes de hello.

![Menu de groupe de machines](media/oms-service-map/machine-groups-menu.png)


## <a name="role-icons"></a>Icônes de rôle
Certains processus jouent des rôles particuliers sur les machines : serveurs web, serveurs d’applications, base de données, etc. Carte de service annote processus et identifient les zones de l’ordinateur avec toohelp des icônes de rôle à un rôle de hello coup de œil un processus ou un serveur joue.

| Icône de rôle | Description |
|:--|:--|
| ![Serveur web](media/oms-service-map/role-web-server.png) | Serveur web |
| ![App Server](media/oms-service-map/role-application-server.png) | Serveur d’applications |
| ![Serveur de base de données](media/oms-service-map/role-database.png) | Serveur de base de données |
| ![Serveur LDAP](media/oms-service-map/role-ldap.png) | Serveur LDAP |
| ![Serveur SMB](media/oms-service-map/role-smb.png) | Serveur SMB |

![Icônes de rôle](media/oms-service-map/role-icons.png)


## <a name="failed-connections"></a>Connexions ayant échoué
Échec de connexion est affiché dans carte de Service mappe les processus et les ordinateurs, avec une ligne en pointillés rouge, indiquant qu’un système client échoue tooreach un processus ou un port. Échec de connexion est signalé à partir de n’importe quel système avec un agent de carte de Service déployé si ce système est hello une seule connexion hello a échoué lors de le. Carte de service mesure ce processus en observant les sockets TCP qui échouent tooestablish une connexion. Cet échec peut entraîner à partir d’un pare-feu, une configuration incorrecte dans hello client ou serveur, ou un service distant n’est pas disponible.

![Connexions ayant échoué](media/oms-service-map/failed-connections.png)

Le fait de comprendre les connexions ayant échoué peut faciliter le dépannage, la validation de la migration, l’analyse de la sécurité et la compréhension globale de l’architecture. Échec de connexion est parfois sans incidence, mais ils souvent pointent directement tooa problème, tel qu’un environnement de basculement soudainement devenir inaccessible ou les deux niveaux d’application en cours tootalk impossible après une migration de cloud.

## <a name="client-groups"></a>Groupes de clients
Groupes de clients sont des zones sur la carte de hello qui représentent les ordinateurs client qui n’ont pas d’Agents de dépendance. Un seul groupe Client représente clients hello pour un processus individuel ou l’ordinateur.

![Groupes de clients](media/oms-service-map/client-groups.png)

adresses IP du hello toosee des serveurs hello dans un groupe de Client, le groupe de hello select. contenu Hello du groupe de hello est répertoriées dans hello **propriétés du groupe de Client** volet.

![Propriétés du groupe de clients](media/oms-service-map/client-group-properties.png)

## <a name="server-port-groups"></a>Groupes de ports du serveur
Les groupes de ports du serveur sont des zones qui représentent les ports de chaque serveur n’ayant pas d’agents de dépendance. boîte de Hello contient port du serveur hello et nombre hello de serveurs avec le port de connexion toothat. Développez les connexions et des serveurs individuels hello boîte toosee hello. S’il existe un seul serveur dans la zone de hello, hello nom ou adresse IP est répertorié.

![Groupes de ports du serveur](media/oms-service-map/server-port-groups.png)

## <a name="context-menu"></a>Menu contextuel
En cliquant sur les points de suspension hello (...) en haut de hello droite de n’importe quel serveur affiche le menu contextuel de hello pour ce serveur.

![Connexions ayant échoué](media/oms-service-map/context-menu.png)

### <a name="load-server-map"></a>Charger la carte des serveurs
En cliquant sur **charge serveur carte** vous amène tooa nouveau mappage avec le serveur sélectionné de hello en tant que nouvel ordinateur de focus hello.

### <a name="show-self-links"></a>Afficher les self-links
En cliquant sur **Self-Links d’afficher** redessine hello nœud du serveur, y compris ceux Self-Link, qui sont des connexions TCP qui commencent et se terminent par des processus au sein du serveur de hello. Si Self-Link sont affichés, hello des modifications de commande de menu trop**Self-Links de masquer**, de sorte que vous pouvez les désactiver.

## <a name="computer-summary"></a>Récapitulatif de la machine
Hello **résumé de l’ordinateur** volet inclut une vue d’ensemble du système d’exploitation d’un serveur, le nombre de la dépendance et les données à partir d’autres solutions Operations Management Suite. Ces données ont trait aux métriques de performance, aux tickets de Service Desk, au suivi des modifications, à la sécurité et aux mises à jour.

![Volet Récapitulatif d’une machine](media/oms-service-map/machine-summary.png)

## <a name="computer-and-process-properties"></a>Propriétés des ordinateurs et processus
Lorsque vous accédez à une carte de la carte de Service, vous pouvez sélectionner les ordinateurs et les processus toogain un contexte supplémentaire sur leurs propriétés. Ordinateurs fournissent des informations sur DNS nom, IPv4 adresses, processeur et mémoire de capacité, type de machine virtuelle, système d’exploitation et version, redémarrer dernière heure et ID hello de leurs agents d’Operations Management Suite et de la carte de Service.

![Volet Propriétés d’une machine](media/oms-service-map/machine-properties.png)

Vous pouvez collecter les détails du processus à partir des métadonnées du système d’exploitation relatives à l’exécution des processus, qui comprennent les nom et description du processus, les nom et domaine de l’utilisateur (sur Windows), les noms de la société et du produit, la version du produit, le répertoire de travail, la ligne de commande et l’heure de début du processus.

![Volet Propriétés du processus](media/oms-service-map/process-properties.png)

Hello **résumé du processus** volet fournit des informations supplémentaires sur la connectivité du processus hello, y compris ses ports liés, les connexions entrantes et sortantes et les connexions qui ont échoué.

![Volet Récapitulatif du processus](media/oms-service-map/process-summary.png)

## <a name="operations-management-suite-alerts-integration"></a>Intégration des alertes d’Operations Management Suite
Carte de service s’intègre avec les alertes de tooshow déclenché d’alertes de Operations Management Suite pour serveur sélectionné de hello dans la plage de temps hello sélectionné. serveur de Hello affiche une icône s’il existe des alertes en cours et hello **Machine alertes** volet répertorie les alertes hello.

![Volet Alertes d’une machine](media/oms-service-map/machine-alerts.png)

alertes pertinentes tooenable carte de Service toodisplay, créez une règle d’alerte qui se déclenche pour un ordinateur spécifique. alertes toocreate approprié :
- Inclure une clause toogroup par ordinateur (par exemple, **par intervalle de l’ordinateur 1 minute**).
- Choisissez tooalert en fonction de la mesure métrique.

![Configuration des alertes](media/oms-service-map/alert-configuration.png)


## <a name="operations-management-suite-log-events-integration"></a>Intégration des journaux d’événements d’Operations Management Suite
Carte de service s’intègre à tooshow de recherche de journal un nombre de tous les événements de journal disponibles pour le serveur sélectionné de hello pendant l’intervalle de temps hello sélectionné. Vous pouvez cliquer sur une ligne dans la liste de hello d’événement nombres toojump tooLog recherche et afficher les événements de journal hello.

![Volet Journaux d’événements d’une machine](media/oms-service-map/log-events.png)

## <a name="operations-management-suite-service-desk-integration"></a>Intégration du Service Desk d’Operations Management Suite
Intégration de carte de service avec le connecteur de gestion du Service informatique de hello est automatique lorsque les deux solutions sont activées et configurées dans votre espace de travail Operations Management Suite. intégration de Hello dans la carte de Service est intitulée « Service Desk ». Pour plus d’informations, voir [Gérer de manière centralisée les éléments de travail ITSM à l’aide d’IT Service Management Connector (version préliminaire)](https://docs.microsoft.com/azure/log-analytics/log-analytics-itsmc-overview).

Hello **Machine Service Desk** volet répertorie tous les événements de gestion des services informatiques pour le serveur sélectionné de hello dans la plage de temps hello sélectionné. serveur de Hello affiche une icône s’il existe des éléments en cours et hello Machine Service Desk répertorie les.

![Volet Service Desk d’une machine](media/oms-service-map/service-desk.png)

élément de hello tooopen dans votre solution ITSM connectée, cliquez sur **élément de travail vue**.

Détails de hello tooview d’élément de hello dans recherche de journal, cliquez sur **afficher dans la recherche de journal**.


## <a name="operations-management-suite-change-tracking-integration"></a>Intégration de la solution Change Tracking d’Operations Management Suite
L’intégration de la solution Service Map avec la fonction Change Tracking est automatique lorsque les deux solutions sont activées et configurées dans votre espace de travail Operations Management Suite.

Hello **ordinateur suivi** répertorie toutes les modifications, avec hello plus récente tout d’abord, ainsi que d’un toodrill de lien vers le bas tooLog recherche pour plus d’informations.

![Volet Change Tracking d’une machine](media/oms-service-map/change-tracking.png)

Bonjour image suivante est une vue détaillée d’un événement ConfigurationChange que vous pouvez voir une fois que vous sélectionnez **afficher dans le journal Analytique**.

![Événement ModificationDeConfiguration](media/oms-service-map/configuration-change-event.png)


## <a name="operations-management-suite-performance-integration"></a>Intégration des performances d’Operations Management Suite
Hello **les performances des machines** volet affiche des métriques de performances standard pour le serveur sélectionné de hello. les métriques Hello incluent l’utilisation du processeur, utilisation de la mémoire, octets réseau envoyés et reçus et une liste des processus principaux de hello en octets réseau envoyés et reçus. données de performances réseau tooget hello, vous devez également avoir activé hello solution câble données 2.0 dans Operations Management Suite.

![Volet Performances d’une machine](media/oms-service-map/machine-performance.png)


## <a name="operations-management-suite-security-integration"></a>Intégration de la solution Security and Audit d’Operations Management Suite
L’intégration de la solution Service Map avec la fonction Security and Audit est automatique lorsque les deux solutions sont activées et configurées dans votre espace de travail Operations Management Suite.

Hello **sécurité de l’ordinateur** volet affiche les données hello solution Operations Management Suite de sécurité et d’Audit pour le serveur sélectionné de hello. volet de Hello répertorie un récapitulatif de tout problème de sécurité en attente pour le serveur de hello pendant l’intervalle de temps hello sélectionné. En cliquant sur un des exercices de problèmes de sécurité hello vers le bas dans une recherche de journal pour plus d’informations à leur sujet.

![Volet Sécurité d’une machine](media/oms-service-map/machine-security.png)


## <a name="operations-management-suite-updates-integration"></a>Intégration de la solution Update Management d’Operations Management Suite
L’intégration de la solution Service Map avec la solution Update Management est automatique lorsque les deux solutions sont activées et configurées dans votre espace de travail Operations Management Suite.

Hello **mises à jour de la Machine** volet affiche les données à partir de hello solution de gestion de mise à jour Operations Management Suite pour le serveur sélectionné de hello. volet de Hello répertorie un récapitulatif de toutes les mises à jour manquantes pour le serveur de hello pendant l’intervalle de temps hello sélectionné.

![Volet Change Tracking d’une machine](media/oms-service-map/machine-updates.png)

## <a name="log-analytics-records"></a>Enregistrements Log Analytics
Les données d’inventaire des ordinateurs et processus de la solution Service Map sont disponibles pour effectuer une [recherche](../log-analytics/log-analytics-log-searches.md) dans Log Analytics. Vous pouvez appliquer cette tooscenarios de données qui incluent la planification de la migration, analyse de capacité, détection et résolution des problèmes de performances de la demande.

Un enregistrement est généré par heure pour chaque ordinateur unique et le processus, de plus de la carte toohello les enregistrements qui sont générés lorsqu’un processus ou un ordinateur démarre ou est tooService d’embarquée. Ces enregistrements ont des propriétés de hello Bonjour les tableaux suivants. champs de Hello et des valeurs dans les événements ServiceMapComputer_CL hello mappent toofields Hello ressource d’ordinateur Bonjour API ServiceMap Azure Resource Manager. Hello champs et des valeurs dans les événements ServiceMapProcess_CL hello mappent toohello des champs de hello ressource de processus Bonjour API ServiceMap Azure Resource Manager. le champ de ResourceName_s Hello correspond au champ nom hello hello correspond le Gestionnaire de ressources à la ressource. 

>[!NOTE]
>À mesure que les fonctionnalités de carte de Service augmentent, ces champs sont toochange de sujet.

Il existe des propriétés générées en interne, vous pouvez utiliser des ordinateurs et les processus unique tooidentify :

- Ordinateur : Utilisez ResourceId ou ResourceName_s toouniquely identifie un ordinateur dans un espace de travail Operations Management Suite.
- Processus : Utilisez ResourceId toouniquely identifier un processus dans un espace de travail Operations Management Suite. ResourceName_s est unique dans le contexte de hello d’ordinateur hello sur quel hello est en cours (MachineResourceName_s) 

Étant donné que plusieurs enregistrements peuvent exister pour un processus spécifié et d’un ordinateur dans un intervalle de temps spécifié, les requêtes peuvent renvoyer plusieurs enregistrements pour hello même ordinateur ou processus. tooinclude hello uniquement enregistrement le plus récent, ajoutez « | la déduplication ResourceId » toohello requête.

### <a name="servicemapcomputercl-records"></a>Enregistrements ServiceMapComputer_CL
Les enregistrements de type *ServiceMapComputer_CL* ont des données d’inventaire pour les serveurs incluant des agents Service Map. Ces enregistrements ont les propriétés de hello Bonjour tableau suivant :

| Propriété | Description |
|:--|:--|
| Type | *ServiceMapComputer_CL* |
| SourceSystem | *OpsManager* |
| ResourceId | Identificateur unique pour un ordinateur au sein de l’espace de travail hello de Hello |
| ResourceName_s | Identificateur unique pour un ordinateur au sein de l’espace de travail hello de Hello |
| ComputerName_s | ordinateur Hello nom de domaine complet |
| Ipv4Addresses_s | Une liste d’adresses d’IPv4 du serveur hello |
| Ipv6Addresses_s | Une liste d’adresses IPv6 du serveur hello |
| DnsNames_s | Tableau de noms DNS |
| OperatingSystemFamily_s | Windows ou Linux |
| OperatingSystemFullName_s | nom complet du système d’exploitation de hello de Hello  |
| Bitness_s | nombre de bits Hello machine hello (32 bits ou 64 bits)  |
| PhysicalMemory_d | mémoire physique de Hello en Mo |
| Cpus_d | nombre de Hello d’unités centrales |
| CpuSpeed_d | Hello vitesse du processeur (en MHz)|
| VirtualizationState_s | *inconnu*, *physique*, *virtuel*, *hyperviseur* |
| VirtualMachineType_s | *hyper-v*, *vmware*, etc. |
| VirtualMachineNativeMachineId_g | Hello VM ID assigné par son hyperviseur |
| VirtualMachineName_s | nom Hello Hello machine virtuelle |
| BootTime_t | heure de démarrage Hello |



### <a name="servicemapprocesscl-type-records"></a>Enregistrements de type ServiceMapProcess_CL
Les enregistrements de type *ServiceMapProcess_CL* ont des données d’inventaire pour les processus connectés à TCP sur des serveurs ayant des agents Service Map. Ces enregistrements ont les propriétés de hello Bonjour tableau suivant :

| Propriété | Description |
|:--|:--|
| Type | *ServiceMapProcess_CL* |
| SourceSystem | *OpsManager* |
| ResourceId | Identificateur unique pour un processus dans l’espace de travail hello de Hello |
| ResourceName_s | Identificateur unique de Hello pour un processus au sein de la machine hello sur lequel il est en cours d’exécution|
| MachineResourceName_s | nom de la ressource de l’ordinateur de hello Hello |
| ExecutableName_s | nom Hello de l’exécutable du processus hello |
| StartTime_t | heure de début de pool de processus Hello |
| FirstPid_d | PID de première Hello hello pool de traitement |
| Description_s | description du processus Hello |
| CompanyName_s | nom Hello de société de hello |
| InternalName_s | nom interne de Hello |
| ProductName_s | nom Hello du produit de hello |
| ProductVersion_s | version du produit Hello |
| FileVersion_s | version du fichier Hello |
| CommandLine_s | ligne de commande Hello |
| ExecutablePath _s | fichier exécutable de Hello chemin d’accès toohello |
| WorkingDirectory_s | répertoire de travail Hello |
| Nom d’utilisateur | compte Hello sous le hello est l’exécution de processus |
| UserDomain | domaine Hello sous le hello est l’exécution de processus |


## <a name="sample-log-searches"></a>Exemples de recherches dans les journaux

### <a name="list-all-known-machines"></a>Liste de tous les ordinateurs connus
Type=ServiceMapComputer_CL | dedup ResourceId

### <a name="list-hello-physical-memory-capacity-of-all-managed-computers"></a>Capacité de mémoire physique de hello liste de tous les ordinateurs gérés.
Type=ServiceMapComputer_CL | select PhysicalMemory_d, ComputerName_s | Dedup ResourceId

### <a name="list-computer-name-dns-ip-and-os"></a>Répertorier le nom de l’ordinateur, le DNS, l’adresse IP et le système d’exploitation.
Type=ServiceMapComputer_CL | select ComputerName_s, OperatingSystemFullName_s, DnsNames_s, IPv4Addresses_s  | dedup ResourceId

### <a name="find-all-processes-with-sql-in-hello-command-line"></a>Rechercher tous les processus par « sql » dans la ligne de commande hello
Type=ServiceMapProcess_CL CommandLine_s = \*sql\* | dedup ResourceId

### <a name="find-a-machine-most-recent-record-by-resource-name"></a>Rechercher un ordinateur (enregistrement le plus récent) par nom de ressource
Type=ServiceMapComputer_CL "m-4b9c93f9-bc37-46df-b43c-899ba829e07b" | dedup ResourceId

### <a name="find-a-machine-most-recent-record-by-ip-address"></a>Rechercher une machine (enregistrement le plus récent) par adresse IP
Type=ServiceMapComputer_CL "10.229.243.232" | dedup ResourceId

### <a name="list-all-known-processes-on-a-specified-machine"></a>Répertorier tous les processus sur une machine spécifiée
Type=ServiceMapProcess_CL MachineResourceName_s="m-4b9c93f9-bc37-46df-b43c-899ba829e07b" | dedup ResourceId

### <a name="list-all-computers-running-sql"></a>Répertorier tous les ordinateurs exécutant SQL
Type=ServiceMapComputer_CL ResourceName_s IN {Type=ServiceMapProcess_CL \*sql\* | Distinct MachineResourceName_s} | dedup ResourceId | Distinct ComputerName_s

### <a name="list-all-unique-product-versions-of-curl-in-my-datacenter"></a>Répertorier toutes les versions de produit uniques de CURL dans mon centre de données
Type=ServiceMapProcess_CL ExecutableName_s=curl | Distinct ProductVersion_s

### <a name="create-a-computer-group-of-all-computers-running-centos"></a>Créer un groupe de tous les ordinateurs exécutant CentOS
Type=ServiceMapComputer_CL OperatingSystemFullName_s = \*CentOS\* | Distinct ComputerName_s


## <a name="rest-api"></a>API REST
Toutes les données serveur, processus et de la dépendance hello dans la carte de Service est disponible via hello [API REST du Service mappage](https://docs.microsoft.com/rest/api/servicemap/).


## <a name="diagnostic-and-usage-data"></a>Données relatives aux diagnostics et à l’utilisation
Microsoft recueille automatiquement des données d’utilisation et de performances via votre utilisation du service de carte de Service de hello. Microsoft utilise cette tooprovide de données et améliorer la qualité de hello, la sécurité et l’intégrité de hello service de carte de Service. tooprovide précise et efficace des capacités de dépannage, les données de salutation contient des informations sur la configuration hello de vos logiciels, tels que le système d’exploitation et version adresse IP, nom DNS et nom de la station de travail. Microsoft ne collecte pas de nom, d’adresse ou d’autres coordonnées.

Pour plus d’informations sur la collecte de données et l’utilisation, consultez hello [déclaration de confidentialité Microsoft Online Services](https://go.microsoft.com/fwlink/?LinkId=512132).


## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur [recherche de journal](../log-analytics/log-analytics-log-searches.md) dans les données de tooretrieve Analytique de journal qui sont collectées par carte de Service.


## <a name="troubleshooting"></a>Résolution des problèmes
Consultez hello [résolution des problèmes de la section du document de configuration de la carte de Service hello](operations-management-suite-service-map-configure.md#troubleshooting).


## <a name="feedback"></a>Commentaires
Avez-vous des commentaires à nous transmettre à propos de Service Map ou de sa documentation ?  Si c’est le cas, sachez que notre page [User Voice](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map) vous permet de nous suggérer des fonctionnalités ou de voter pour des suggestions en cours.
