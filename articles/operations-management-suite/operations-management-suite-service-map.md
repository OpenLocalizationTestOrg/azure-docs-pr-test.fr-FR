---
title: Utiliser la solution Service Map dans Operations Management Suite | Microsoft Docs
description: "Service Map est une solution OMS (Operations Management Suite) qui détecte automatiquement les composants d’application sur les systèmes Windows et Linux et mappe la communication entre les services. Cet article fournit des informations sur le déploiement de Service Map dans votre environnement et son utilisation dans divers scénarios."
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
ms.openlocfilehash: 2e5475a0563549ddfaa2c146e4acf94c019841ec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-service-map-solution-in-operations-management-suite"></a>Utiliser la solution Service Map dans Operations Management Suite
La solution Service Map détecte automatiquement les composants d’application sur les systèmes Windows et Linux, et mappe la communication entre les services. Elle vous permet d’afficher vos serveurs comme vous les imaginez, en tant que systèmes interconnectés fournissant des services critiques. Elle affiche les connexions entre serveurs, processus et ports au sein de toute architecture TCP connectée, sans nécessiter de configuration autre que l’installation d’un agent.

Cet article décrit les détails de l’utilisation de Service Map. Pour plus d’informations sur la configuration de la solution Service Map et l’intégration d’agents, voir [Configuration de la solution Service Map dans Operations Management Suite (OMS)](operations-management-suite-service-map-configure.md).


## <a name="use-cases-make-your-it-processes-dependency-aware"></a>Cas d’utilisation : Intégrer la dépendance dans les processus informatiques

### <a name="discovery"></a>Découverte
Service Map crée automatiquement une carte de référence commune des dépendances entre vos serveurs, les processus et les services tiers. La solution découvre et mappe toutes les dépendances TCP, en identifiant les connexions inattendues, les systèmes tiers distants dont vous dépendez et les dépendances envers les zones sombres traditionnelles de votre réseau comme Active Directory. Service Map détecte les échecs de connexion réseau que vos systèmes gérés tentent d’établir, vous aidant ainsi à identifier d’éventuels problèmes de réseau, interruptions de service et autres configurations de serveur inappropriées.

### <a name="incident-management"></a>Gestion des incidents
Service Map vous montre comment les systèmes sont connectés et ont une incidence les uns sur les autres, ce qui vous évide de devoir isoler vous-même le problème. Outre l’identification des échecs de connexion, la solution aide à identifier les équilibreurs de charge mal configurés, des charges imprévues ou excessives sur des services critiques, ainsi que des clients non autorisés tels que des ordinateurs de développeurs qui communiquent avec les systèmes de production. En utilisant des flux de travail intégrés avec la fonction Change Tracking d’Operations Management Suite, vous pouvez également voir si un événement de modification sur un ordinateur ou service principal explique la cause première d’un incident.

### <a name="migration-assurance"></a>Garantie d’une migration réussie
La solution Service Map vous permet de planifier, d’accélérer et de valider efficacement les migrations vers Azure pour vous assurer que rien n’est oublié et vous prémunir contre toute panne surprise. Vous pouvez découvrir tous les systèmes interdépendants qui doivent migrer en même temps, évaluer la capacité et la configuration du système et déterminer si un système en cours d’exécution continue de servir les utilisateurs ou si une mise hors service peut être envisagée au lieu de la migration. Une fois la migration terminée, vous pouvez vérifier la charge et l’identité du client pour contrôler que les systèmes de test et les clients se connectent. Si vos définitions de pare-feu et de planification de sous-réseau rencontrent des problèmes, les connexions ayant échoué dans les mappages Service Map vous dirigent vers les systèmes nécessitant une connectivité.

### <a name="business-continuity"></a>Continuité de l’activité
Si vous utilisez Azure Site Recovery et que vous avez besoin d’aide pour définir la séquence de récupération pour votre environnement d’application, Service Map peut automatiquement vous indiquer comment les systèmes s’appuient les uns sur les autres pour s’assurer que votre plan de récupération est fiable. En choisissant un serveur ou un groupe critiques, et en affichant ses clients, vous pouvez identifier les systèmes frontaux à récupérer une fois le serveur restauré et disponible. Inversement, en examinant les dépendances des serveurs critiques par rapport au serveur principal, vous pouvez identifier les systèmes à récupérer avant la restauration de vos systèmes principaux.

### <a name="patch-management"></a>Gestion des correctifs
La solution Service Map améliore l’utilisation de la fonction Évaluation des mises à jour système d’Operations Management Suite en vous montrant les autres équipes et serveurs dépendant de votre service. Vous pouvez ainsi notifier ces derniers avant d’arrêter vos systèmes en vue d’une mise à jour corrective. La solution Service Map facilite également la gestion des correctifs dans Operations Management Suite en vous montrant si vos services sont disponibles et connectés correctement après application de la mise à jour corrective et redémarrage.


## <a name="mapping-overview"></a>Vue d’ensemble du mappage
Les agents Service Map rassemblent des informations sur tous les processus connectés via TCP sur le serveur où ils sont installés, ainsi que des détails sur les connexions entrantes et sortantes pour chaque processus. Dans la liste du volet gauche, vous pouvez sélectionner les ordinateurs ou les groupes disposant d’agents Service Map afin de visualiser leurs dépendances sur une plage de temps spécifiée. Les cartes de dépendance d’ordinateur ciblent un ordinateur spécifique, et montrent tous les ordinateurs qui sont des clients ou serveurs TCP directs de cet ordinateur.  Les cartes de groupe d’ordinateurs montrent des ensembles de serveurs et leurs dépendances.

![Vue d’ensemble de Service Map](media/oms-service-map/service-map-overview.png)

Les ordinateurs peuvent être développés sur le mappage de manière à afficher les processus en cours d’exécution avec les connexions réseau actives pendant la période sélectionnée. Quand un ordinateur distant doté d’un agent Service Map est développé pour afficher des détails de processus, seuls les processus qui communiquent avec l’ordinateur ciblé sont affichés. Le nombre d’ordinateurs frontaux sans agent qui se connectent à l’ordinateur ciblé est indiqué à gauche des processus auxquels ils se connectent. Si l’ordinateur ciblé se connecte à un ordinateur principal dépourvu d’agent, ce serveur principal est inclus dans un groupe de ports du serveur, avec les autres connexions au même numéro de port.

Par défaut, les mappages Service Map affichent les 30 dernières minutes des informations de dépendance. Les contrôles de temps en haut à gauche permettent d’interroger des cartes pour obtenir des plages horaires historiques de jusqu’à une heure afin de voir l’aspect passé des dépendances (par exemple, pendant un incident ou avant une modification). Les données Service Map sont stockées pendant 30 jours dans les espaces de travail payants et pendant 7 jours dans les espaces de travail gratuits.

## <a name="status-badges-and-border-coloring"></a>Badges d’état et couleur de bordure
En bas de chaque serveur dans le mappage, une liste de badges état affiche des informations sur l’état du serveur. Les badges indiquent qu’il existe des informations pertinentes concernant le serveur provenant d’une des intégrations des solutions Operations Management Suite. En cliquant sur un badge, vous accédez directement aux détails de l’état dans le volet droit. Les badges d’état actuellement disponibles sont Alertes, Service Desk, Modifications, Sécurité et Mises à jour.

Selon la gravité des badges d’état, les bordures de nœud de machine peuvent être colorées en rouge (critique), en jaune (avertissement) ou en bleu (informations). La couleur est celle du badge d’état dont la gravité est la plus critique. Une bordure de couleur grise indique un nœud dépourvu d’indicateur d’état.

![Badges d’état](media/oms-service-map/status-badges.png)

## <a name="machine-groups"></a>Groupes de machines
Les groupes de machines permettent de voir les cartes centrées autour d’un ensemble de serveurs, pas seulement d’un seul. Vous pouvez ainsi voir tous les membres d’un cluster d’applications ou de serveurs multiniveau dans une seule carte.

Les utilisateurs sélectionnent les serveurs appartenant à un groupe, puis choisissent un nom pour celui-ci.  Vous pouvez ensuite choisir d’afficher le groupe avec l’ensemble de ses processus et connexions, ou de l’afficher uniquement avec les processus et connexions directement liés aux autres membres du groupe.

![Groupe de machines](media/oms-service-map/machine-group.png)

### <a name="creating-a-machine-group"></a>Création d’un groupe de machines
Pour créer un groupe, sélectionnez la ou les machines souhaitées dans la liste des machines, puis cliquez sur **Ajouter au groupe**.

![Créer un groupe](media/oms-service-map/machine-groups-create.png)

Vous pouvez alors choisir **Créer un nouveau** et attribuer un nom au groupe.

![Nommer un groupe](media/oms-service-map/machine-groups-name.png)

>[!NOTE]
>Les groupes de machines sont actuellement limités à 10 serveurs, mais nous prévoyons d’augmenter bientôt cette limite.

### <a name="viewing-a-group"></a>Affichage d’un groupe
Une fois que vous avez créé des groupes, vous pouvez les afficher en cliquant sur l’onglet Groupes.

![Onglet Groupes](media/oms-service-map/machine-groups-tab.png)

Sélectionnez ensuite le nom du groupe de machines pour afficher la carte de celui-ci.
![Groupe de machines](media/oms-service-map/machine-group.png) Les machines appartenant au groupe sont entourées d’un contour blanc sur la carte.

Le développement du groupe de machines permet d’afficher la liste des ordinateurs qui le composent.

![Ordinateurs d’un groupe de machines](media/oms-service-map/machine-groups-machines.png)

### <a name="filter-by-processes"></a>Filtrer par processus
Vous pouvez basculer la vue de carte entre l’affichage de tous les processus et connexions au sein du groupe, ou uniquement de ceux qui sont directement liés au groupe de machines.  La vue par défaut affiche tous les processus.  Vous pouvez modifier la vue en cliquant sur l’icône de filtre au-dessus de la carte.

![Groupe de filtres](media/oms-service-map/machine-groups-filter.png)

Lorsque l’option **Tous les processus** est activée, la carte inclut l’ensemble des processus et connexions sur chaque machine du groupe.

![Tous les processus d’un groupe de machines](media/oms-service-map/machine-groups-all.png)

Si vous modifiez l’affichage pour voir uniquement les **Processus connectés au groupe**, la carte est rétrécie de façon à n’afficher que les processus et connexions directement liés aux autres machines du groupe, créant ainsi un affichage simplifié.

![Processus filtrés d’un groupe de machines](media/oms-service-map/machine-groups-filtered.png)
 
### <a name="adding-machines-to-a-group"></a>Ajout de machines à un groupe
Pour ajouter des machines à un groupe, cochez les cases en regard des machines souhaitées, puis cliquez sur **Ajouter au groupe**.  Ensuite, sélectionnez le groupe auquel vous souhaitez ajouter les machines.
 
### <a name="removing-machines-from-a-group"></a>Suppression de machines d’un groupe
Dans la liste des groupes, développez le nom du groupe pour afficher les machines constituant celui-ci.  Cliquez ensuite sur le menu représenté par des points de suspension en regard de la machine à supprimer, puis choisissez **Supprimer**.

![Supprimer une machine d’un groupe](media/oms-service-map/machine-groups-remove.png)

### <a name="removing-or-renaming-a-group"></a>Suppression ou changement de nom d’un groupe
Cliquez sur le menu représenté par des points de suspension en regard du nom dans la liste de groupes.

![Menu de groupe de machines](media/oms-service-map/machine-groups-menu.png)


## <a name="role-icons"></a>Icônes de rôle
Certains processus jouent des rôles particuliers sur les machines : serveurs web, serveurs d’applications, base de données, etc. Service Map annote les zones de processus et de machine avec des icônes de rôle pour identifier en un coup d’œil le rôle que joue un processus ou un serveur.

| Icône de rôle | Description |
|:--|:--|
| ![Serveur web](media/oms-service-map/role-web-server.png) | Serveur web |
| ![App Server](media/oms-service-map/role-application-server.png) | Serveur d’applications |
| ![Serveur de base de données](media/oms-service-map/role-database.png) | Serveur de base de données |
| ![Serveur LDAP](media/oms-service-map/role-ldap.png) | Serveur LDAP |
| ![Serveur SMB](media/oms-service-map/role-smb.png) | Serveur SMB |

![Icônes de rôle](media/oms-service-map/role-icons.png)


## <a name="failed-connections"></a>Connexions ayant échoué
Les connexions qui ont échoué sont affichées dans les cartes de type Service Map des processus et machines, avec une ligne rouge en pointillés indiquant qu’un système client ne parvient pas à atteindre un processus ou un port. Les connexions ayant échoué sont signalées par n’importe quel système ayant un agentService Map déployé si ce système est celui qui a tenté d’établir de telles connexions. La solution Service Map mesure ce processus en observant les sockets TCP qui ne parviennent pas à établir une connexion. Cet échec peut être dû à un pare-feu, à une configuration incorrecte du client ou du serveur, ou à l’indisponibilité d’un service distant.

![Connexions ayant échoué](media/oms-service-map/failed-connections.png)

Le fait de comprendre les connexions ayant échoué peut faciliter le dépannage, la validation de la migration, l’analyse de la sécurité et la compréhension globale de l’architecture. Les échecs de connexion sont parfois sans incidence, mais ils dénotent souvent directement un problème tel qu’un environnement de basculement devenant subitement inaccessible ou deux couches Application incapables de communiquer après une migration vers le cloud.

## <a name="client-groups"></a>Groupes de clients
Les groupes de clients sont des zones sur la carte qui représentent des ordinateurs clients n’ayant pas d’agents de dépendance. Un groupe de clients représente les clients d’un processus ou d’une machine.

![Groupes de clients](media/oms-service-map/client-groups.png)

Pour afficher les adresses IP des serveurs d’un groupe de clients, sélectionnez le groupe. Le contenu du groupe est affiché dans le volet **Propriétés du groupe de clients**.

![Propriétés du groupe de clients](media/oms-service-map/client-group-properties.png)

## <a name="server-port-groups"></a>Groupes de ports du serveur
Les groupes de ports du serveur sont des zones qui représentent les ports de chaque serveur n’ayant pas d’agents de dépendance. La zone indique le port du serveur ainsi que le nombre de serveurs connectés à ce port. Développez la zone pour afficher chaque serveur et ses connexions. S’il n’y a qu’un serveur dans la zone, son nom ou son adresse IP s’affiche.

![Groupes de ports du serveur](media/oms-service-map/server-port-groups.png)

## <a name="context-menu"></a>Menu contextuel
Un clic sur les points de suspension (...) en haut à droite d’un serveur permet d’afficher le menu contextuel de ce serveur.

![Connexions ayant échoué](media/oms-service-map/context-menu.png)

### <a name="load-server-map"></a>Charger la carte des serveurs
Un clic sur l’option **Charger la carte des serveurs** permet d’accéder à une nouvelle carte présentant le serveur sélectionné en tant que nouvelle machine ciblée.

### <a name="show-self-links"></a>Afficher les self-links
Un clic sur l’option **Afficher les self-links** permet de redessiner le nœud du serveur incluant tous les self-links qui représentent des connexions TCP commençant et se terminant sur des processus au sein du serveur. Si des self-links sont affichés, la commande de menu devient **Masquer les self-links**, de sorte que vous pouvez les désactiver.

## <a name="computer-summary"></a>Récapitulatif de la machine
Le volet **Récapitulatif d’une machine** contient une vue d’ensemble du système d’exploitation, du nombre de dépendances et des données provenant d’autres solutions Operations Management Suite pour un serveur. Ces données ont trait aux métriques de performance, aux tickets de Service Desk, au suivi des modifications, à la sécurité et aux mises à jour.

![Volet Récapitulatif d’une machine](media/oms-service-map/machine-summary.png)

## <a name="computer-and-process-properties"></a>Propriétés des ordinateurs et processus
Lorsque vous naviguez dans une carte de type Service Map, vous pouvez sélectionner des machines et des processus afin d’obtenir un contexte supplémentaire concernant leurs propriétés. Les machines fournissent des informations sur le nom DNS, les adresses IPv4, la capacité du processeur et de la mémoire, le type de machine virtuelle, le système d’exploitation et sa version, l’heure du dernier redémarrage et les ID de leurs agents Operations Management Suite et Service Map.

![Volet Propriétés d’une machine](media/oms-service-map/machine-properties.png)

Vous pouvez collecter les détails du processus à partir des métadonnées du système d’exploitation relatives à l’exécution des processus, qui comprennent les nom et description du processus, les nom et domaine de l’utilisateur (sur Windows), les noms de la société et du produit, la version du produit, le répertoire de travail, la ligne de commande et l’heure de début du processus.

![Volet Propriétés du processus](media/oms-service-map/process-properties.png)

Le volet **Récapitulatif du processus** fournit des informations supplémentaires sur la connectivité du processus, qui comprennent les ports liés, les connexions entrantes et sortantes, et les connexions ayant échoué.

![Volet Récapitulatif du processus](media/oms-service-map/process-summary.png)

## <a name="operations-management-suite-alerts-integration"></a>Intégration des alertes d’Operations Management Suite
La solution Service Map s’intègre avec les alertes d’Operations Management Suite pour afficher les alertes déclenchées pour le serveur sélectionné pendant la période sélectionnée. Le serveur affiche une icône s’il existe des alertes, et le volet **Alertes de la machine** répertorie les alertes.

![Volet Alertes d’une machine](media/oms-service-map/machine-alerts.png)

Pour permettre à la solution Service Map d’afficher les alertes pertinentes, créez une règle d’alerte qui se déclenche pour un ordinateur spécifique. Pour créer des alertes appropriées :
- Incluez une clause de regroupement par ordinateur (par exemple, **by Computer interval 1minute**).
- Choisissez d’alerter des mesures de métriques.

![Configuration des alertes](media/oms-service-map/alert-configuration.png)


## <a name="operations-management-suite-log-events-integration"></a>Intégration des journaux d’événements d’Operations Management Suite
Service Map intègre la recherche dans les journaux pour afficher un nombre de tous les événements du journal disponibles pour le serveur sélectionné au cours de la période sélectionnée. Vous pouvez cliquer sur n’importe quelle ligne dans la liste des événements pour passer à la recherche dans les journaux et consulter les événements du journal individuel.

![Volet Journaux d’événements d’une machine](media/oms-service-map/log-events.png)

## <a name="operations-management-suite-service-desk-integration"></a>Intégration du Service Desk d’Operations Management Suite
L’intégration de la solution Service Map avec IT Service Management Connector est automatique lorsque les deux solutions sont activées et configurées dans votre espace de travail Operations Management Suite. L’intégration dans Service Map est libellée « Service Desk ». Pour plus d’informations, voir [Gérer de manière centralisée les éléments de travail ITSM à l’aide d’IT Service Management Connector (version préliminaire)](https://docs.microsoft.com/azure/log-analytics/log-analytics-itsmc-overview).

Le volet **Service Desk d’une machine** affiche la liste de tous les événements d’IT Service Management survenus pour le serveur sélectionné pendant la période sélectionnée. Le serveur affiche une icône s’il existe des éléments en cours, et le volet Service Desk de la machine affiche la liste de ceux-ci.

![Volet Service Desk d’une machine](media/oms-service-map/service-desk.png)

Pour ouvrir l’élément dans votre solution ITSM connectée, cliquez sur **Afficher l’élément de travail**.

Pour afficher les détails de l’élément dans la recherche, cliquez sur **Recherche dans les journaux**.


## <a name="operations-management-suite-change-tracking-integration"></a>Intégration de la solution Change Tracking d’Operations Management Suite
L’intégration de la solution Service Map avec la fonction Change Tracking est automatique lorsque les deux solutions sont activées et configurées dans votre espace de travail Operations Management Suite.

Le volet **Change Tracking d’une machine** affiche la liste de toutes les modifications, les plus récentes en tête, ainsi qu’un lien pour consulter des détails supplémentaires dans Recherche dans les journaux.

![Volet Change Tracking d’une machine](media/oms-service-map/change-tracking.png)

L’illustration suivante est une vue détaillée d’un événement ModificationDeConfiguration que vous pourriez voir après avoir sélectionné **Afficher dans Log Analytics**.

![Événement ModificationDeConfiguration](media/oms-service-map/configuration-change-event.png)


## <a name="operations-management-suite-performance-integration"></a>Intégration des performances d’Operations Management Suite
Le volet **Performances d’une machine** affiche des métriques de performance standard pour le serveur sélectionné. Ces métriques incluent l’utilisation du processeur, l’utilisation de la mémoire, les octets réseau envoyés et reçus, et la liste des principaux processus classée par octets réseau envoyés et reçus. Pour obtenir les données de performances réseau, vous devez également activer la solution Wire Data 2.0 dans Operations Management Suite.

![Volet Performances d’une machine](media/oms-service-map/machine-performance.png)


## <a name="operations-management-suite-security-integration"></a>Intégration de la solution Security and Audit d’Operations Management Suite
L’intégration de la solution Service Map avec la fonction Security and Audit est automatique lorsque les deux solutions sont activées et configurées dans votre espace de travail Operations Management Suite.

Le volet **Sécurité d’une machine** affiche des données provenant de la solution Security and Audit d’Operations Management Suite pour le serveur sélectionné. Le volet affiche un récapitulatif de tous les problèmes de sécurité en attente pour le serveur pendant la période sélectionnée. Un clic sur un problème de sécurité permet d’accéder à Recherche dans les journaux pour plus d’informations concernant ce problème.

![Volet Sécurité d’une machine](media/oms-service-map/machine-security.png)


## <a name="operations-management-suite-updates-integration"></a>Intégration de la solution Update Management d’Operations Management Suite
L’intégration de la solution Service Map avec la solution Update Management est automatique lorsque les deux solutions sont activées et configurées dans votre espace de travail Operations Management Suite.

Le volet **Mises à jour d’une machine** affiche les données provenant de la solution Update Management d’Operations Management Suite pour le serveur sélectionné. Le volet affiche un récapitulatif de toutes les mises à jour manquantes pour le serveur pendant la période sélectionnée.

![Volet Change Tracking d’une machine](media/oms-service-map/machine-updates.png)

## <a name="log-analytics-records"></a>Enregistrements Log Analytics
Les données d’inventaire des ordinateurs et processus de la solution Service Map sont disponibles pour effectuer une [recherche](../log-analytics/log-analytics-log-searches.md) dans Log Analytics. Vous pouvez appliquer ces données à divers scénarios tels que la planification de la migration, l’analyse de la capacité, la détection et la résolution de problèmes de performances à la demande.

Un enregistrement par heure est généré pour chaque processus et ordinateur, en plus des enregistrements générés quand un processus ou ordinateur démarre ou est intégré à la solution Service Map. Les propriétés de ces enregistrements sont décrites dans les tableaux suivants. Les champs et les valeurs des événements ServiceMapComputer_CL sont mappés aux champs de la ressource Machine dans l’API Azure Resource Manager ServiceMap. Les champs et les valeurs des événements ServiceMapProcess_CL sont mappés aux champs de la ressource Processus dans l’API Azure Resource Manager ServiceMap. Le champ ResourceName_s correspond au champ de nom dans la ressource Azure Resource Manager correspondante. 

>[!NOTE]
>À mesure que les fonctionnalités la solution Service Map s’étofferont, il se peut que ces champs soient modifiés.

Il existe des propriétés générées en interne que vous pouvez utiliser pour identifier les ordinateurs et processus uniques :

- Ordinateur : utilisez ResourceId ou ResourceName_s pour identifier de façon unique un ordinateur au sein d’un espace de travail Operations Management Suite.
- Processus : utilisez ResourceId pour identifier de façon unique un processus au sein d’un espace de travail Operations Management Suite. ResourceName_s est unique dans le contexte de l’ordinateur sur lequel le processus est en cours d’exécution (MachineResourceName_s) 

Étant donné que plusieurs enregistrements peuvent exister pour un processus et un ordinateur donnés au cours d’une période spécifique, les requêtes peuvent renvoyer plusieurs enregistrements pour un même ordinateur ou processus. Pour inclure uniquement l’enregistrement le plus récent, ajoutez "| dedup ResourceId" à la requête.

### <a name="servicemapcomputercl-records"></a>Enregistrements ServiceMapComputer_CL
Les enregistrements de type *ServiceMapComputer_CL* ont des données d’inventaire pour les serveurs incluant des agents Service Map. Les propriétés de ces enregistrements sont décrites dans le tableau suivant :

| Propriété | Description |
|:--|:--|
| Type | *ServiceMapComputer_CL* |
| SourceSystem | *OpsManager* |
| ResourceId | Identificateur unique d’une machine au sein de l’espace de travail |
| ResourceName_s | Identificateur unique d’une machine au sein de l’espace de travail |
| ComputerName_s | Nom de domaine complet (FQDN) de l’ordinateur |
| Ipv4Addresses_s | Liste des adresses IPv4 du serveur |
| Ipv6Addresses_s | Liste des adresses IPv6 du serveur |
| DnsNames_s | Tableau de noms DNS |
| OperatingSystemFamily_s | Windows ou Linux |
| OperatingSystemFullName_s | Nom complet du système d’exploitation  |
| Bitness_s | Nombre de bits de la machine (32 bits ou 64 bits)  |
| PhysicalMemory_d | Mémoire physique en Mo |
| Cpus_d | Nombre de processeurs |
| CpuSpeed_d | Vitesse du processeur en MHz|
| VirtualizationState_s | *inconnu*, *physique*, *virtuel*, *hyperviseur* |
| VirtualMachineType_s | *hyper-v*, *vmware*, etc. |
| VirtualMachineNativeMachineId_g | ID de machine virtuelle assigné par son hyperviseur |
| VirtualMachineName_s | Nom de la machine virtuelle |
| BootTime_t | Temps de démarrage |



### <a name="servicemapprocesscl-type-records"></a>Enregistrements de type ServiceMapProcess_CL
Les enregistrements de type *ServiceMapProcess_CL* ont des données d’inventaire pour les processus connectés à TCP sur des serveurs ayant des agents Service Map. Les propriétés de ces enregistrements sont décrites dans le tableau suivant :

| Propriété | Description |
|:--|:--|
| Type | *ServiceMapProcess_CL* |
| SourceSystem | *OpsManager* |
| ResourceId | Identificateur unique d’un processus au sein de l’espace de travail |
| ResourceName_s | identificateur unique d’un processus au sein de la machine sur laquelle il s’exécute|
| MachineResourceName_s | Nom de ressource de la machine |
| ExecutableName_s | Nom de l’exécutable du processus |
| StartTime_t | Heure de début du pool de processus |
| FirstPid_d | Premier PID dans le pool de processus |
| Description_s | Description du processus |
| CompanyName_s | Nom de la société |
| InternalName_s | Nom interne |
| ProductName_s | Nom du produit |
| ProductVersion_s | Version du produit |
| FileVersion_s | Version du fichier |
| CommandLine_s | Ligne de commande |
| ExecutablePath _s | Chemin d’accès du fichier exécutable |
| WorkingDirectory_s | Le répertoire de travail |
| Nom d’utilisateur | Compte sous lequel le processus s’exécute |
| UserDomain | Domaine sous lequel le processus s’exécute |


## <a name="sample-log-searches"></a>Exemples de recherches dans les journaux

### <a name="list-all-known-machines"></a>Liste de tous les ordinateurs connus
Type=ServiceMapComputer_CL | dedup ResourceId

### <a name="list-the-physical-memory-capacity-of-all-managed-computers"></a>Répertorier la capacité de mémoire physique de tous les ordinateurs gérés
Type=ServiceMapComputer_CL | select PhysicalMemory_d, ComputerName_s | Dedup ResourceId

### <a name="list-computer-name-dns-ip-and-os"></a>Répertorier le nom de l’ordinateur, le DNS, l’adresse IP et le système d’exploitation.
Type=ServiceMapComputer_CL | select ComputerName_s, OperatingSystemFullName_s, DnsNames_s, IPv4Addresses_s  | dedup ResourceId

### <a name="find-all-processes-with-sql-in-the-command-line"></a>Rechercher tous les processus contenant « sql » dans la ligne de commande
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


## <a name="rest-api"></a>de l’API REST
L’ensemble des données relatives au serveur, au processus et aux dépendances dans Service Map est disponible via [l’API REST Carte de service](https://docs.microsoft.com/rest/api/servicemap/).


## <a name="diagnostic-and-usage-data"></a>Données relatives aux diagnostics et à l’utilisation
Microsoft collecte automatiquement les données sur l’utilisation et les performances via votre utilisation du service Service Map. Microsoft utilise ces données pour fournir et améliorer la qualité, la sécurité et l’intégrité de la solution Service Map. Afin d’offrir des fonctionnalités de dépannage précises et efficaces, les données incluent des informations sur la configuration de votre logiciel, telles que le système d’exploitation et la version, l’adresse IP, le nom DNS et le nom de la station de travail. Microsoft ne collecte pas de nom, d’adresse ou d’autres coordonnées.

Pour plus d’informations sur l’utilisation et la collecte de données, voir la [Déclaration de confidentialité des Services en ligne de Microsoft](https://go.microsoft.com/fwlink/?LinkId=512132).


## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur les [recherches dans les journaux](../log-analytics/log-analytics-log-searches.md) dans Log Analytics pour récupérer les données collectées par la solution Service Map.


## <a name="troubleshooting"></a>Résolution des problèmes
Consultez la [section Résolution des problèmes du document Configuration de la solution Carte de service](operations-management-suite-service-map-configure.md#troubleshooting).


## <a name="feedback"></a>Commentaires
Avez-vous des commentaires à nous transmettre à propos de Service Map ou de sa documentation ?  Si c’est le cas, sachez que notre page [User Voice](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map) vous permet de nous suggérer des fonctionnalités ou de voter pour des suggestions en cours.
