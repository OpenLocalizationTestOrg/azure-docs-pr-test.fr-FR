---
title: "vue d’ensemble de la sécurité opérationnelle aaaAzure | Documents Microsoft"
description: "Cet article fournit une vue d’ensemble de hello Azure sécurité opérationnelle."
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: tomsh
ms.openlocfilehash: b91c7889660b32e4933c305007692bd6e1ded05f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-operational-security-overview"></a>Vue d’ensemble d’Azure Operational Security
Sécurité opérationnelle Azure fait référence toohello services, des contrôles et toousers disponibles de fonctionnalités pour protéger leurs données, les applications et les autres composants dans Microsoft Azure. [Sécurité opérationnelle Azure](https://docs.microsoft.com/azure/security/azure-operational-security) est une infrastructure qui intègre les connaissances hello acquises via une variété de fonctions de tooMicrosoft unique, y compris hello Microsoft du cycle de vie SDL (Security Development), hello Microsoft Security Programme de centre de réponse et connaissance approfondie du paysage des menaces de sécurité cyber hello.

Cet article de présentation de la sécurité opérationnelle Azure se concentre sur hello suivant de zones :

- Azure Operations Management Suite
-   Azure Security Center
-   Azure Monitor
-   Azure Network Watcher
-   Azure Storage Analytics
-   Azure Active Directory

## <a name="azure-operations-management-suite"></a>Azure Operations Management Suite
Opérations informatiques est chargé de gérer l’infrastructure de centre de données, des applications et des données, y compris la stabilité de hello et la sécurité de ces systèmes. Toutefois, obtenir les informations de sécurité sur la fréquence à laquelle l’augmentation des environnements informatiques complexes nécessite des organisations toocobble rassemblent des données à partir de plusieurs systèmes de gestion et de sécurité.

[Microsoft Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) est une solution de gestion informatique basée sur le cloud de Microsoft qui vous permet de gérer et de protéger votre infrastructure locale et de cloud.

OMS est une solution de gestion informatique basée sur le cloud proposant de nombreuses offres comme IT Automation, Security & Compliance, Log Analytics, ainsi que la sauvegarde et la récupération. Par conséquent, il est un toomanage aide parfait et protéger votre infrastructure informatique, localement et dans le cloud de hello.

fonctionnalités principales de Hello d’OMS sont fournie par un ensemble de services qui s’exécutent dans Azure. Chaque service fournit une fonction de gestion spécifique, et vous pouvez combiner des scénarios de gestion de services tooachieve. Ces services incluent :

-   Log Analytics
-   Automatisation
-   Sauvegarde
-   Site Recovery

### <a name="log-analytics"></a>Log Analytics
[Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics) assure des services de surveillance pour OMS en collectant les données de ressources gérées et en les regroupant dans un référentiel central. Ces données peuvent inclure des événements, données de performances ou des données personnalisées fournies par le biais hello API. Une fois collectées, les données de salutation sont disponibles pour la génération d’alertes, analyse et l’exportation. Cette méthode vous permet tooconsolidate des données à partir de diverses sources, donc vous pouvez combiner des données à partir de vos services Azure avec votre environnement local existant. Elle sépare clairement collection hello de données de salutation à l’action de hello entreprise sur ces données afin que toutes les actions sont tooall disponibles les types de données.

### <a name="automation"></a>Automatisation
Microsoft [Azure Automation](https://docs.microsoft.com/azure/automation/automation-intro) offre un moyen pour les utilisateurs tooautomate des tâches manuelles, longues, sujettes aux erreurs et répétitives hello qui sont couramment exécutées dans un environnement de cloud et d’entreprise. Il fait gagner du temps et augmente la fiabilité hello des tâches d’administration récurrentes et même les planifie toobe automatiquement effectuées à intervalles réguliers. Vous pouvez automatiser les processus à l'aide de Runbooks ou automatiser la gestion de configuration avec la Configuration de l'état souhaité (DSC, Desired State Configuration).

### <a name="backup"></a>Sauvegarde
[Sauvegarde Azure](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup) est hello Azure service vous pouvez utiliser un tooback (ou protéger) et restaurer vos données Bonjour cloud de Microsoft. Azure Backup remplace votre solution de sauvegarde locale ou hors site par une solution basée dans le cloud à la fois fiable, sécurisée et économique. Sauvegarde Azure offre plusieurs composants que vous téléchargez et déployez sur les ordinateurs appropriés hello, server, ou dans le cloud de hello. composant de Hello, ou un agent, que vous déployez dépend de ce que vous souhaitez tooprotect. Tous les composants d’Azure Backup (quel que soit le si vous protégez des données en local ou dans le cloud de hello) peuvent être utilisé tooback configuration coffre de Services de récupération des données tooa dans Azure. Consultez hello [table des composants Azure Backup](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup#which-azure-backup-components-should-i-use).

### <a name="site-recovery"></a>Site Recovery
[Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery) permet la continuité en coordonnant la réplication des locaux virtuels et tooAzure de machines physiques ou site secondaire de tooa. Si votre site principal est indisponible, vous basculez les emplacement secondaire toohello afin que les utilisateurs peuvent continuer de travailler et restauré lorsque systèmes tooworking de retour. Détection des menaces intelligente et efficace.

## <a name="azure-active-directory"></a>Azure Active Directory
[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-enable-sso-scenario) est une solution Microsoft de type IDaaS (Identity as a Service) qui :

-   active IAM en tant que service cloud ;
-   assure la centralisation de la gestion de l’accès, l’authentification unique et le compte-rendu ;
-   Prend en charge la gestion des accès intégré pour [des milliers d’applications](https://azure.microsoft.com/marketplace/active-directory/) dans la galerie d’applications hello, notamment Salesforce, Google Apps, Box, Concur et bien plus encore.

Azure AD inclut également une suite complète de [fonctionnalités de gestion d’identité](https://docs.microsoft.com/azure/security/security-identity-management-overview#security-monitoring-alerts-and-machine-learning-based-reports), comme l’[authentification multifacteur](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication), l’[inscription d’appareil]( https://docs.microsoft.com/azure/active-directory/active-directory-device-registration-overview), la [gestion de mot de passe libre-service](https://azure.microsoft.com/resources/videos/self-service-password-reset-azure-ad/), la [gestion de groupes libre-service](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-update-your-own-password), la [gestion des comptes privilégiés](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure), le [contrôle d’accès en fonction du rôle](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is), la [surveillance de l’utilisation de l’application](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health), ainsi que la [création d’audits complets](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs), la [surveillance de la sécurité et la création d’alertes](https://docs.microsoft.com/azure/operations-management-suite/oms-security-responding-alerts).

Avec Azure Active Directory, toutes les applications que vous publiez pour vos partenaires et les clients (professionnels et particuliers) ont hello mêmes fonctions de gestion des identités et des accès. Cela permet de vous toosignificantly réduire les coûts d’exploitation.

## <a name="azure-security-center"></a>Azure Security Center
[Centre de sécurité Azure](https://docs.microsoft.com/azure/security-center/security-center-get-started) vous aide à vous empêchez, détectez et répondre toothreats avec une meilleure visibilité et contrôler hello la sécurité de vos ressources Azure. Il fournit une surveillance de la sécurité et une gestion des stratégies intégrées pour l’ensemble de vos abonnements, vous aidant ainsi à détecter les menaces qui pourraient passer inaperçues. De plus, il est compatible avec un vaste écosystème de solutions de sécurité.

[Security Center](https://docs.microsoft.com/azure/security-center/security-center-linux-virtual-machine) vous aide à protéger les données de vos machines virtuelles dans Azure en vous offrant une visibilité sur les paramètres de sécurité de vos machines virtuelles et en surveillant les menaces. Security Center surveille les éléments suivants sur vos machines virtuelles :

-   Paramètres de sécurité de système d’exploitation (OS) avec hello recommandé de règles de configuration
-   Sécurité du système et mises à jour critiques manquantes
-   Recommandations de protection du point de terminaison
-   Validation du chiffrement de disque
-   Attaques réseau

Centre de sécurité Azure utilise [contrôle d’accès en fonction du rôle (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure), qui fournit des [rôles intégrés](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles) qui peuvent être attribuées toousers, des groupes et des services dans Azure.

Centre de sécurité évalue la configuration de hello de vos problèmes de sécurité tooidentify de ressources et les vulnérabilités. Dans le centre de sécurité, vous voyez uniquement les informations liées tooa ressource lorsque vous sont assignés rôle hello de propriétaire, collaborateur ou lecteur pour le groupe d’abonnement ou une ressource hello appartenant à une ressource.

>[!Note]
>Consultez [autorisations dans le centre de sécurité Azure](https://docs.microsoft.com/azure/security-center/security-center-permissions) toolearn plus d’informations sur les rôles et les actions autorisées dans le centre de sécurité.

Centre de sécurité utilise hello Microsoft Monitoring Agent – il s’agit d’hello même agent utilisé par le service Operations Management Suite et Analytique de journal de hello. Données collectées à partir de cet agent sont stockées dans soit un Analytique de journal existants [espace de travail](https://docs.microsoft.com/azure/log-analytics/log-analytics-manage-access) associé à votre abonnement Azure ou d’un nouvel espace, en prenant en compte de géolocalisation hello Hello machine virtuelle.

## <a name="azure-monitor"></a>Azure Monitor
Les problèmes de performances dans votre application cloud peuvent affecter votre entreprise. Avec plusieurs composants interconnectés et de nouvelles versions fréquentes, des dégradations peuvent se produire à tout moment. Et si vous développez une application, vos utilisateurs découvrent généralement des problèmes que vous n’avez pas trouvés dans le test. Vous devez savoir immédiatement sur ces problèmes et disposer des outils de diagnostic et résolution des problèmes de hello.

[Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-azure-monitor) est l’outil de base pour la surveillance des services s’exécutant sur Azure. Il vous fournit des données de niveau de l’infrastructure sur débit hello d’un service et un hello entourant l’environnement. Si vous gérez vos applications dans Azure, vous décidez si tooscale vers le haut ou vers le bas des ressources, analyse d’Azure vous donne ensuite ce que vous utilisez toostart.

En outre, vous pouvez utiliser l’analyse données toogain des informations détaillées relatives à votre application. Ces connaissances peuvent vous aider à tooimprove des performances des applications ou facilité de maintenance, ou automatiser des actions qui nécessiteraient sinon une intervention manuelle. Il inclut :

-   Journaux d’activité
-   Journaux de diagnostic Azure
-   Mesures
-   Azure Diagnostics

### <a name="azure-activity-log"></a>Journaux d’activité
Il s’agit d’un journal qui fournit des indications sur les opérations de hello qui ont été effectuées sur les ressources dans votre abonnement. Hello [le journal d’activité](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) était précédemment appelé « Journaux d’Audit » ou « Journaux des opérations », dans la mesure où il signale les événements de panneau pour vos abonnements.

### <a name="azure-diagnostic-logs"></a>Journaux de diagnostic Azure
[Les journaux de Diagnostic Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) sont émis par une ressource et fournir des données riches et fréquentes relatives au fonctionnement de hello d’une ressource. le contenu de ces journaux Hello varie selon le type de ressource.

Par exemple, les journaux des événements système Windows sont une catégorie de journal de diagnostic pour les machines virtuelles et les objets blob, les tables, et les journaux de file d’attente sont les catégories de journaux de diagnostic pour les comptes de stockage.

Les journaux de diagnostic diffèrent hello [journal d’activité (anciennement appelé journal d’Audit ou de journal des opérations)](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs). journal d’activité Hello fournit des indications sur les opérations de hello qui ont été effectuées sur les ressources dans votre abonnement. Les journaux de diagnostic fournissent des informations sur les opérations effectuées par votre ressource.

### <a name="metrics"></a>Mesures
Moniteur de Azure vous permet de tooconsume télémétrie toogain visibilité des performances de hello et de l’intégrité de vos charges de travail sur Azure. type le plus important de données de télémétrie Azure Hello est métriques hello (également appelés des compteurs de performances) est émis par les ressources Azure plus. Moniteur de Azure fournit plusieurs façons tooconfigure et consommez [métriques](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-metrics) pour la surveillance et la résolution des problèmes.

### <a name="azure-diagnostics"></a>Azure Diagnostics
Il s’agit de capacité hello dans Azure qui active la collecte de hello de données de diagnostic sur une application déployée. Vous pouvez utiliser l’extension de diagnostics hello provenant de différentes sources différentes. Les sources actuellement prises en charge sont les [rôles web et les rôles de travail Azure Cloud Services](https://docs.microsoft.com/azure/vs-azure-tools-configure-roles-for-cloud-service), les [machines virtuelles Azure](https://docs.microsoft.com/azure/vs-azure-tools-configure-roles-for-cloud-service) sous Microsoft Windows et [Service Fabric](https://docs.microsoft.com/azure/monitoring-and-diagnostics/azure-diagnostics).


## <a name="network-watcher"></a>Network Watcher
Les clients créent un réseau de bout en bout dans Azure en orchestrant et composant diverses ressources réseau telles qu’un réseau virtuel, ExpressRoute, Application Gateway, des équilibrages de charge, etc. Analyse est disponible sur chacune des ressources du réseau hello.

réseau tooend Hello peut avoir des configurations complexes et les interactions entre les ressources, créer des scénarios complexes qui doivent basée sur un scénario d’analyse via l’Observateur réseau.

[Network Watcher](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) simplifie la surveillance et le diagnostic de votre réseau Azure. Outils de diagnostic et de visualisation disponibles avec enable Observateur réseau vous paquets distants tootake capture sur une Machine virtuelle Azure, obtenir votre trafic réseau à l’aide des journaux de flux et diagnostiquer les connexions et passerelle VPN.

Observateur réseau a actuellement hello suivant de fonctionnalités :

- [Topologie](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-overview) -fournit un Bonjour montrant de vue de niveau réseau différents interconnexions et les associations entre les ressources réseau dans un groupe de ressources.
-   [Capture de paquets variables](https://docs.microsoft.com/azure/network-watcher/network-watcher-packet-capture-overview) - Capture des données de paquets dans et en dehors d’une machine virtuelle. Advanced options de filtrage et des contrôles ajustées par exemple, tooset en mesure de temps et les limitations de taille fournissent des raisons de souplesse. données de paquet de Hello peuvent être stockées dans un magasin d’objets blob ou sur le disque local dans un format de .cap hello.
-   [Vérification des flux IP](https://docs.microsoft.com/azure/network-watcher/network-watcher-ip-flow-verify-overview) - Vérifie si un paquet est autorisé ou refusé en fonction des paramètres de paquet des informations à 5 tuples de flux (adresse IP de destination, adresse IP source, port de destination, port source et protocole). Si les paquets hello sont refusée par un groupe de sécurité, hello règle et groupe qui a refusé les paquets hello est retournée.
-   [Tronçon suivant](https://docs.microsoft.com/azure/network-watcher/network-watcher-next-hop-overview) -détermine le saut suivant de hello pour les paquets routés Bonjour Azure Fabric de réseau, ce qui vous les itinéraires toodiagnose toute mauvaise configuration définie par l’utilisateur.
-   [Affichage de groupe de sécurité](https://docs.microsoft.com/azure/network-watcher/network-watcher-security-group-view-overview) -Obtient les règles de sécurité efficace et appliquées hello qui sont appliquées sur une machine virtuelle.
-   [Enregistrement de flux de groupe de sécurité réseau](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview) -journaux de flux pour les groupes de sécurité réseau permettent de tootraffic connexes toocapture journaux qui sont autorisés ou refusés par des règles de sécurité hello dans le groupe de hello. flux de Hello est défini par une 5-tuple d’informations : l’adresse IP Source, adresse IP de Destination, Port Source, le Port de Destination et protocole.
-   [Passerelle de réseau virtuel et la résolution des problèmes de connexion](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest) -hello capacité tootroubleshoot fournit des connexions et des passerelles de réseau virtuel.
-   [Limites de l’abonnement du réseau](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) -vous permet de l’utilisation des ressources réseau tooview par rapport aux limites.
-   [Configuration du journal de diagnostic](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) – fournit un tooenable un seul volet ou désactivez des journaux de Diagnostics pour les ressources réseau dans un groupe de ressources.

toolearn plus Observateur de réseau tooconfigure voir, [configurer Observateur réseau](https://docs.microsoft.com/azure/network-watcher/network-watcher-create).

## <a name="developer-operations-devops"></a>Opérations de développement (DevOps)
Développement d’applications tooDevOps préalable, les équipes ont été responsable de collecte des exigences d’entreprise pour un programme logiciel et l’écriture de code. Une équipe distincte de questions et réponses vérifie ensuite les programme hello dans un environnement de développement isolé si les exigences ont été respectées, et les versions hello code pour les opérations toodeploy. les équipes de déploiement Hello sont ensuite fragmentées en groupes isolées, comme la mise en réseau et de la base de données. Chaque fois qu’un programme logiciel est « levé sur mur de hello » équipe indépendante de tooan il ajoute les goulots d’étranglement.

[DevOps](https://www.visualstudio.com/learn/what-is-devops/) permet aux équipes toodeliver solutions plus sécurisées et une meilleure qualité, plus rapides et économique. Les clients s’attendent à une expérience dynamique et fiable lors de l’utilisation de logiciels et de services.  Les équipes doivent effectuer une itération au rapidement sur les mises à jour logicielles, mesurer l’impact hello des mises à jour de hello et répondre rapidement avec les nouveaux problèmes de tooaddress développement itérations ou fournir plus de valeur.  Les plateformes cloud comme Microsoft Azure ont supprimé les goulots d’étranglement traditionnels et aidé à faire de l’infrastructure une marchandise. Logiciel règne dans chaque entreprise comme hello atout et facteur dans les résultats de l’entreprise. Aucune organisation, un développeur ou un travailleur de l’informatique permettre ou doit-elle éviter de déplacement de DevOps hello.

Les praticiens DevOps matures adoptent plusieurs hello pratiques. Ces pratiques [impliquent des personnes](https://www.visualstudio.com/learn/what-is-devops-culture/) tooform stratégies basées sur les scénarios d’entreprise hello.  Outils peuvent aider à automatiser hello différentes méthodes :

-   [Gestion de projets et de planification Agile](https://www.visualstudio.com/learn/what-is-agile/) techniques sont utilisée tooplan et isoler le travail à des sprints, gérer la capacité de l’équipe et aident les équipes à s’adapter rapidement les besoins toochanging.
-   [Contrôle de version, généralement avec Git](https://www.visualstudio.com/learn/what-is-git/), permet aux équipes situés n’importe où dans la source de hello world tooshare et d’intégrer avec le pipeline de mise en production de logiciel développement outils tooautomate hello.
-   [Intégration continue](https://www.visualstudio.com/learn/what-is-continuous-integration/) lecteurs hello en cours de fusion et de test du code, ce qui conduit toofinding défauts au début.  Les autres avantages sont notamment un gain de temps sur la résolution des problèmes de fusion et la rapidité des retours pour les équipes de développement.
-   [Livraison continue](https://www.visualstudio.com/learn/what-is-continuous-delivery/) des solutions logicielles tooproduction et environnements de test aident les organisations à résoudre les bogues et tooever modification de l’entreprise de répondre rapidement configuration requise.
-   La [surveillance](https://www.visualstudio.com/learn/what-is-monitoring/) des applications en cours d’exécution, y compris les environnements de production pour contrôler l’intégrité de l’application et l’utilisation du client, aide les organisations à élaborer une hypothèse et à valider ou refuser rapidement des stratégies.  Les données enrichies sont capturées et stockées dans divers formats d’enregistrement.
-   [Infrastructure en tant que Code (IaC)](https://www.visualstudio.com/learn/what-is-infrastructure-as-code/) est une pratique qui permet une automatisation de hello et validation de la création et de démontage de réseaux et les ordinateurs virtuels toohelp avec la remise des applications sécurisées, stable plateformes d’hébergement.
-   [Microservices](https://www.visualstudio.com/learn/what-are-microservices/) architecture est exploitée tooisolate exemples d’utilisation dans les petits services réutilisables.  Cette architecture est synonyme d’extensibilité et d’efficacité.

## <a name="next-steps"></a>Étapes suivantes
toolearn en savoir plus sur OMS solution de sécurité et d’Audit, consultez hello suivant des articles :

- [Operations Management Suite | Security &amp; Compliance](https://www.microsoft.com/cloud-platform/security-and-compliance).
- [Surveillance et de réponse tooSecurity les alertes de Operations Management Suite de Solution de sécurité et d’Audit](https://docs.microsoft.com/en-us/azure/operations-management-suite/oms-security-responding-alerts).
- [Surveillance des ressources dans la solution de sécurité et d’audit d’Operations Management Suite](https://docs.microsoft.com/en-us/azure/operations-management-suite/oms-security-monitoring-resources).
