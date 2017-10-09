---
title: "sécurité des données Analytique d’aaaLog | Documents Microsoft"
description: "Découvrez comment Log Analytics protège vos données personnelles et sécurise vos données."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: a33bb05d-b310-4f2c-8f76-f627e600c8e7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: magoedte
ms.openlocfilehash: 130b59f22fc3dd249f32717367cc62ea25c55a21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-data-security"></a>Sécurité des données Log Analytics
Microsoft est validée tooprotecting votre confidentialité et sécuriser vos données, tout en proposant des logiciels et services qui vous aider à gérer hello infrastructure informatique de votre organisation. Nous reconnaissons que lorsque vous confiez vos tooothers de données, cette confiance exige une sécurité rigoureuse. Microsoft respecte les instructions de sécurité et de conformité toostrict : du codage toooperating un service.

La sécurisation et la protection des données constituent une priorité de premier plan pour Microsoft. Nous contacter pour toute question, des suggestions ou Remarque concernant les hello suivant d’informations, y compris notre politique de sécurité à [options de support Azure](http://azure.microsoft.com/support/options/).

Cet article explique comment les données sont collectées, traitées et sécurisées par journal Analytique Bonjour Operations Management Suite (OMS). Vous pouvez utiliser le service web d’agents tooconnect toohello, utiliser des données opérationnelles de System Center Operations Manager toocollect ou récupérer des données à partir d’Azure diagnostics pour une utilisation par Analytique de journal. les données collectées Hello sont envoyées via hello Internet à l’aide de l’authentification basée sur certificat & SSL 3 toohello service d’Analytique de journal, qui est hébergé dans Microsoft Azure. Données sont compressées par l’agent de hello avant d’être envoyée.

Hello service d’Analytique de journal gère vos données en nuage en toute sécurité à l’aide de hello méthodes suivantes :

* ségrégation des données
* conservation des données
* sécurité physique
* gestion des incidents
* conformité
* certifications relatives aux normes de sécurité

## <a name="data-segregation"></a>Ségrégation des données
Données client sont maintenues séparées logiquement sur chaque composant dans hello service OMS. Toutes les données sont balisées en fonction de l'organisation. Ce balisage est conservé tout au long du cycle de vie des données hello, et elle est appliquée à chaque couche de service de hello. Chaque client possède un blob Azure dédié qui héberge les données à long terme hello

## <a name="data-retention"></a>Conservation des données
Les données indexées de recherche de journal sont stockées et conservées tooyour conséquente plan de tarification. Pour plus d’informations, consultez [Tarification - Log Analytics](https://azure.microsoft.com/pricing/details/log-analytics/).

Microsoft supprime les données client 30 jours après que l’espace de travail OMS hello est fermé. Microsoft supprime également hello compte de stockage Azure où se trouvent les données hello. La suppression des données client n’entraîne pas de destruction de lecteurs physiques.

Hello tableau suivant répertorie quelques-unes des solutions disponibles de hello dans OMS et exemples hello des types de données qu’elles recueillent.

| **Solution** | **Types de données** |
| --- | --- |
| Évaluation de la configuration |Données de configuration, métadonnées et données d'état |
| Planification de la capacité |Données et métadonnées de performances |
| Logiciel anti-programme malveillant |Données et métadonnées de configuration |
| Évaluation des mises à jour du système |Métadonnées et données d'état |
| Gestion du journal |Journaux des événements défini par l’utilisateur, journaux des événements Windows et/ou journaux IIS |
| Suivi des modifications |Inventaire logiciel et métadonnées de service Windows |
| Évaluation de SQL et d'Active Directory |Données WMI, données du Registre, données de performances et résultats de vues de gestion dynamique de SQL Server |

Hello tableau suivant présente des exemples de types de données :

| **Type de données** | **Champs** |
| --- | --- |
| Alerte |Alert Name, Alert Description, BaseManagedEntityId, Problem ID, IsMonitorAlert, RuleId, ResolutionState, Priority, Severity, Category, Owner, ResolvedBy, TimeRaised, TimeAdded, LastModified, LastModifiedBy, LastModifiedExceptRepeatCount, TimeResolved, TimeResolutionStateLastModified, TimeResolutionStateLastModifiedInDB, RepeatCount |
| Configuration |CustomerID, AgentID, EntityID, ManagedTypeID, ManagedTypePropertyID, CurrentValue, ChangeDate |
| Événement |EventId, EventOriginalID, BaseManagedEntityInternalId, RuleId, PublisherId, PublisherName, FullNumber, Number, Category, ChannelLevel, LoggingComputer, EventData, EventParameters, TimeGenerated, TimeAdded <br>**Remarque :** lorsque vous écrivez des événements avec des champs personnalisés dans le journal des événements Windows toohello, OMS les collecte. |
| Metadata |BaseManagedEntityId, ObjectStatus, OrganizationalUnit, ActiveDirectoryObjectSid, PhysicalProcessors, NetworkName, IPAddress, ForestDNSName, NetbiosComputerName, VirtualMachineName, LastInventoryDate, HostServerNameIsVirtualMachine, IP Address, NetbiosDomainName, LogicalProcessors, DNSName, DisplayName, DomainDnsName, ActiveDirectorySite, PrincipalName, OffsetInMinuteFromGreenwichTime |
| Performances |ObjectName, CounterName, PerfmonInstanceName, PerformanceDataId, PerformanceSourceInternalID, SampleValue, TimeSampled, TimeAdded |
| État |StateChangeEventId, StateId, NewHealthState, OldHealthState, Context, TimeGenerated, TimeAdded, StateId2, BaseManagedEntityId, MonitorId, HealthState, LastModified, LastGreenAlertGenerated, DatabaseTimeModified |

## <a name="physical-security"></a>Sécurité physique
fonctionnement de Hello Analytique de journal dans le service OMS est assuré par le personnel de Microsoft et toutes les activités sont enregistrées et peuvent être auditées. Hello service s’exécute entièrement dans Azure et satisfait aux critères de conception communs Azure hello. Vous pouvez afficher des détails sur la sécurité physique de hello des ressources Azure sur la page 18 du hello [Microsoft Azure Security Overview](http://download.microsoft.com/download/6/0/2/6028B1AE-4AEE-46CE-9187-641DA97FC1EE/Windows%20Azure%20Security%20Overview%20v1.01.pdf). Zones de toosecure de droits accès physique sont modifiés au sein d’un jour ouvrable pour toute personne qui n’a plus la responsabilité pour le service OMS de hello, y compris le transfert et l’arrêt. Vous pouvez découvrir l’infrastructure physique globale hello nous utilisons à [Microsoft Datacenters](https://www.microsoft.com/en-us/server-cloud/cloud-os/global-datacenters.aspx).

## <a name="incident-management"></a>Gestion des incidents
OMS inclut un processus de gestion des incidents auquel tous les services Microsoft adhèrent. toosummarize, nous avons :

* Utilisation d’un modèle de gestion partagé où une partie de la responsabilité de sécurité appartient tooMicrosoft et une partie appartient toohello client
* Nous gérons les incidents de sécurité liés à Azure.
  * Nous lançons une investigation lors de la détection d’un incident.
  * Évaluer l’impact de hello et la gravité d’un incident par un membre de l’équipe de réponse aux incidents d’appel. Basée sur la preuve, évaluation de hello peut ou peut ne pas donner davantage escalade de verrous toohello équipe de sécurité.
  * Diagnostiquer un incident par sécurité réponse experts tooconduct hello techniques ou investigation enquête, identifier les stratégies de relation contenant-contenu, des risques et de solution de contournement. Si l’équipe de sécurité hello pense que les données des clients peuvent devenir tooan exposé illégal ou non autorisée individuelle, parallèle l’exécution de processus de Notification d’Incident de client de hello commence en parallèle.  
  * Stabiliser et récupérer à partir de l’incident de hello. équipe de réponse aux incidents Hello crée un problème de récupération plan toomitigate hello. Des mesures d’endiguement de crise telles que la mise en quarantaine des systèmes affectés peuvent être prises immédiatement et parallèlement au diagnostic. Les solutions d’atténuation plus longues terme peuvent être planifiées qui se produisent après que risque immédiat de hello est passé.  
  * Fermer l’incident de hello et procéder à une analyse post-mortem. équipe de réponse aux incidents Hello crée une post-mortem qui présente les détails de hello Hello incident, les stratégies toorevise hello intention, procédures et processus tooprevent une périodicité de l’événement de hello.
* Nous informons les clients concernant les incidents de sécurité.
  * Détermination de l’objectif de hello de clients affectés et tooprovide toute personne qui est affectée que détaillée d’une notification que possible
  * Créer un tooprovide avis clients avec des informations suffisamment détaillées afin qu’ils peuvent effectuer une enquête de leur côté et toutes les engagements que les utilisateurs finaux de tootheir effectuées lors de la retarder pas indûment les processus de notification hello.
  * Vérifiez et déclarer incident hello, selon les besoins.
  * Nous avertissons les clients à l’aide d’une notification d’incident sans délai déraisonnable, et conformément aux obligations légales ou contractuelles applicables. Notifications des incidents de sécurité sont remises tooone ou plusieurs des administrateurs de clients, par quelque moyen que sélectionne Microsoft, y compris par courrier électronique.
* Nous assurons la formation et la préparation de notre équipe
  * Technique de Microsoft est requis toocomplete sécurité et formation spécifique, ce qui vous permet de les tooidentify et rapport suspecté de problèmes de sécurité.  
  * Opérateurs travaillant sur hello service Microsoft Azure ont des obligations de formation Ajout se rapportant à leurs systèmes de toosensitive accès hébergeant des données du client.
  * Le personnel de réponse aux problèmes de sécurité de Microsoft reçoit une formation spécialisée en relation avec les rôles qui lui sont confiés.

En cas de perte de données client, nous avertissons chaque client dans la journée. Toutefois, aucune perte de données client ne s’est jamais produite avec OMS. Par ailleurs, nous conservons des copies de données créées, qui sont distribuées géographiquement.

Pour plus d’informations sur la manière dont Microsoft répond toosecurity incidents, consultez [réponse de sécurité Microsoft Azure Bonjour Cloud](https://gallery.technet.microsoft.com/Azure-Security-Response-in-dd18c678/file/150826/1/Microsoft Azure Security Response in hello cloud.pdf).

## <a name="compliance"></a>Conformité
Hello la sécurité des informations de OMS service équipe de développement et et les programmes de gouvernance prend en charge de ses besoins et respecte les réglementations et toolaws comme décrit dans [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/) et [Microsoft Trust Center conformité](https://www.microsoft.com/en-us/TrustCenter/Compliance/default.aspx). Ceux-ci expliquent également comment OMS fixe les exigences de sécurité, identifie les contrôles de sécurité, et gère et analyse les risques. Chaque année, nous révisons les stratégies, normes, procédures et directives.

Chaque membre de l’équipe de développement d’OMS reçoit une formation formelle en matière de sécurité des applications. En interne, nous utilisons un système de contrôle de version pour le développement de logiciels. Chaque projet de logiciel est protégé par le système de contrôle de version hello.

Microsoft dispose d’une équipe dédiée à la sécurité et à la conformité, qui surveille et évalue tous les services en son sein. Responsables de la sécurité des informations constituent les équipe hello et ne sont pas associés avec hello départements développement OMS d’ingénierie. responsables de la sécurité Hello ont leur propre chaîne de gestion et effectuer des évaluations de produits et de sécurité tooensure de services et de conformité indépendantes.

Le conseil d’administration de Microsoft est informé via un rapport annuel de l’ensemble des programmes relatifs à la sécurité des informations mis en œuvre au sein de Microsoft.

Hello OMS service équipe de développement et travaille activement avec les équipes Microsoft légales et de conformité hello et autres tooacquire de partenaires du secteur certifications différents.

## <a name="certifications-and-attestations"></a>Certifications et attestations
Analytique des journaux OMS répond aux hello suivant les exigences :

* [ISO/IEC 27001](http://www.iso.org/iso/home/standards/management-standards/iso27001.htm)
* [ISO/IEC 27018:2014](http://www.iso.org/iso/home/store/catalogue_tc/catalogue_detail.htm?csnumber=61498)
* [ISO 22301](https://azure.microsoft.com/en-us/blog/iso22301/)
* [Paiement industrie carte (PCI conforme) Data Security Standard (PCI DSS)](https://www.microsoft.com/en-us/TrustCenter/Compliance/PCI) par hello Conseil de normes de sécurité PCI.
* [SOC 1 Type 1 et SOC 2 Type 1](https://www.microsoft.com/en-us/TrustCenter/Compliance/SOC1-and-2).
* [HIPAA et Hi-TECH](https://www.microsoft.com/en-us/TrustCenter/Compliance/HIPAA) pour les organisations qui disposent d’un contrat HIPAA Business Associate Agreement
* Critères de conception communs Windows
* Microsoft Trustworthy Computing
* Comme un service Azure, composants de hello OMS utilise respectent les exigences de conformité tooAzure. Pour en savoir plus, voir le site du [Microsoft Trust Center](https://www.microsoft.com/en-us/TrustCenter/Compliance/default.aspx).

> [!NOTE]
> Dans certaines certifications/attestations, Log Analytics est mentionné sous son ancien nom, *Operational Insights*.
>
>


## <a name="cloud-computing-security-data-flow"></a>Flux de données de sécurité du cloud computing
Hello diagramme suivant montre une architecture de sécurité cloud en tant que flux hello d’informations à partir de votre entreprise et comment il est sécurisé toohello Analytique de journal service, au final vu par vous dans du portail OMS hello. Plus d’informations sur chaque étape suit le diagramme de hello.

![Image de la collecte de données OMS et de la sécurité](./media/log-analytics-security/log-analytics-security-diagram.png)

## <a name="1-sign-up-for-log-analytics-and-collect-data"></a>1. S’inscrire à Log Analytics et collecter des données
Pour votre organisation toosend données tooLog Analytique, vous configurez les agents Windows, les agents qui s’exécutent sur des machines virtuelles ou des Agents OMS pour Linux. Si vous utilisez des agents d’Operations Manager, puis que vous utilisez un Assistant de configuration dans hello Operations console tooconfigure les. Les utilisateurs (vous, d’autres utilisateurs ou d’un groupe de personnes) créer un ou plusieurs comptes OMS (espaces de travail OMS) et d’enregistrent des agents en utilisant l’une de hello suivant des comptes :

* [ID d'organisation](../active-directory/sign-up-organization.md)
* [Compte Microsoft - Outlook, Office Live, MSN](http://www.microsoft.com/account/default.aspx)

Un espace de travail OMS est l’emplacement où les données sont collectées, agrégées, analysées et présentées. Un espace de travail est principalement utilisé en tant que moyen toopartition données, et chaque espace de travail est unique. Par exemple, vous pourriez toohave vos données de production gérées avec un espace de travail OMS et de vos données de test gérées avec un autre espace de travail. Espaces de travail aident également à un administrateur contrôle utilisateur accès toohello de données. Chaque espace de travail peut être associé à plusieurs comptes d’utilisateur, et chaque compte d’utilisateur peut accéder à plusieurs espaces de travail OMS. Vous créez des espaces de travail en fonction d’une région de centre de données. Chaque espace de travail est répliquée tooother des centres de données dans la région de hello, principalement pour la disponibilité du service OMS.

Pour Operations Manager, fin de l’Assistant de configuration de hello, chaque groupe d’administration Operations Manager établit une connexion avec hello service d’Analytique de journal. Vous utilisez ensuite toochoose Assistant Ajouter des ordinateurs de hello les ordinateurs dans le groupe d’administration hello autorisés service toohello de données toosend. Pour les autres types de l’agent, chacun connecte en toute sécurité du service OMS de toohello.

Toutes les communications entre systèmes connectés et hello service d’Analytique de journal sont chiffrées.  Hello TLS, le protocole (HTTPS) est utilisé pour le chiffrement.  Hello processus SDL de Microsoft est suivi tooensure Analytique de journal est à jour avec les progrès plus récent hello dans les protocoles de chiffrement.

Chaque type d’agent collecte des données pour Log Analytics. type Hello des données collectées dépend de types hello de solutions utilisés. Vous pouvez afficher un résumé de la collecte de données à [solutions Analytique de journal ajouter à partir de la galerie des Solutions de hello](log-analytics-add-solutions.md). Par ailleurs, des informations plus détaillées concernant la collecte sont disponibles pour la plupart des solutions. Une solution est un ensemble de vues prédéfinies, de requêtes de recherche de journal, de règles de collecte de données et de logique de traitement. Seuls les administrateurs peuvent utiliser Analytique de journal tooimport une solution. Après avoir importé les solutions hello, il est déplacé toohello serveurs d’administration Operations Manager (si utilisé), puis tooany agents que vous avez choisi. Ensuite, les agents de hello collectent les données de salutation.

## <a name="2-send-data-from-agents"></a>2. Envoyer des données à partir d'agents
Vous enregistrez tous les types de l’agent avec une clé d’inscription, puis une connexion sécurisée est établie entre l’agent de hello et de service de journal Analytique hello à l’aide de l’authentification par certificat et SSL avec le port 443. OMS utilise un magasin des secrets de toogenerate et mettre à jour les clés. Les clés privées pivotent tous les 90 jours et sont stockées dans Azure et sont gérés par hello Azure les opérations qui suivent des pratiques réglementaires et de conformité strictes.

Avec Operations Manager, vous inscrivez un espace de travail avec le service de journal Analytique hello et une connexion HTTPS sécurisée est établie entre le serveur d’administration Operations Manager hello.

Pour les agents Windows s’exécutant sur des machines virtuelles, une clé de stockage en lecture seule est utilisé tooread les événements de diagnostic dans des tables Azure.

Si n’importe quel agent est un service de toohello toocommunicate Impossible pour une raison quelconque, hello les données collectées sont stockées localement dans un cache temporaire et serveur d’administration hello tente tooresend les données de salutation toutes les huit minutes pendant 2 heures. données mises en cache de l’agent Hello sont protégées par la banque d’informations d’identification du système d’exploitation de hello. Si le service de hello ne peut pas traiter les données de salutation au bout de deux heures, les agents hello file d’attente les données de salutation. Si la file d’attente hello est saturé, OMS commence la suppression de types de données, en commençant par les données de performances. limite de file d’attente de l’agent Hello est une clé de Registre afin que vous puissiez modifier, si nécessaire. Les données collectées sont compressées et envoyées toohello service, en ignorant les bases de données locales, donc il n’ajoute pas de n’importe quel toothem de charge. Après que hello collecté les données sont envoyées, il est supprimé du cache de hello.

Comme décrit ci-dessus, les données à partir de vos agents sont envoyées via SSL tooMicrosoft centres de données Azure. Si vous le souhaitez, vous pouvez utiliser ExpressRoute tooprovide une sécurité supplémentaire pour les données de salutation. ExpressRoute est un moyen toodirectly connecter tooAzure à partir de votre réseau WAN existant, comme un multiprotocole étiqueter commutation VPN (MPLS), fourni par un fournisseur de services réseau. Pour plus d’informations, voir [ExpressRoute](https://azure.microsoft.com/services/expressroute/).

## <a name="3-hello-log-analytics-service-receives-and-processes-data"></a>3. hello service de journal Analytique reçoit et traite les données
Hello service d’Analytique de journal s’assure que les données entrantes à partir d’une source approuvée en validant des certificats et l’intégrité des données avec l’authentification Azure hello. Hello données brutes non traitées sont ensuite stockées en tant qu’un objet blob dans [Microsoft Azure Storage](../storage/common/storage-introduction.md) et n’est pas chiffré. Toutefois, chaque objet blob de stockage Azure a un ensemble d’un jeu unique de clés, qui est accessible toothat uniquement l’utilisateur. type Hello des données stockées dépend des types de hello de solutions qui ont été importées et utilisés toocollect données. Puis, hello service d’Analytique de journal traite des données brutes hello pour l’objet blob de stockage Azure hello.

## <a name="4-use-log-analytics-tooaccess-hello-data"></a>4. Utiliser les données de journal Analytique tooaccess hello
Vous pouvez vous connecter tooLog Analytique dans le portail OMS de hello en utilisant le compte de société hello ou compte Microsoft que vous avez configurée précédemment. Tout le trafic entre le portail OMS est hello et Analytique de journal d’OMS est envoyé via un canal HTTPS sécurisé. Lors de l’utilisation du portail OMS hello, un ID de session est généré sur le client d’utilisateur hello (navigateur web) et les données sont stockées dans un cache local jusqu'à ce que la session de hello est terminée. Une fois terminée, hello est supprimé. Les cookies côté client qui ne contiennent pas d’informations d’identification personnelle ne sont pas supprimés automatiquement. Les cookies de session sont marqués HTTPOnly et sécurisés. Après une période d’inactivité prédéterminée, session de portail OMS hello est arrêtée.

À l’aide du portail OMS hello, vous pouvez exporter le fichier de données tooa CSV et vous pouvez accéder à des données à l’aide des API de recherche. Exportation des volumes partagés de cluster est limité too50, 000 lignes par exportation et les données de l’API est restreint too5, 000 lignes par recherche.

## <a name="next-steps"></a>Étapes suivantes
* [Prise en main Analytique de journal](log-analytics-get-started.md) toolearn plus d’informations sur le journal Analytique et get opérationnel en quelques minutes.
