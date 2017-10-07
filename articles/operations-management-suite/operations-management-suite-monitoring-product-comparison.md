---
title: aaaMicrosoft analyse comparative | Documents Microsoft
description: "Microsoft Operations Management Suite (OMS) est une solution de gestion informatique basée sur le cloud de Microsoft qui vous permet de gérer et de protéger votre infrastructure locale et de cloud.  Cet article identifie hello différents services inclus dans OMS et fournit des liens tootheir détaillée le contenu."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: a63ca0ad-61f8-425d-a48c-d87ba518c104
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/27/2016
ms.author: bwren
ms.openlocfilehash: 61144a298fe73c35181070d552c41b96fc445097
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-monitoring-product-comparison"></a>Comparaison des produits de surveillance Microsoft
Cet article fournit une comparaison entre System Center Operations Manager (SCOM) et Analytique de journal dans Operations Management Suite (OMS) en termes de leur architecture, la logique de hello du mode de surveillance des ressources et la façon dont ils effectuent une analyse des données de hello ils collecter.  Il s’agit de toogive vous une connaissance fondamentale de leurs différences et les points forts relatifs.  

## <a name="basic-architecture"></a>Architecture de base
### <a name="system-center-operations-manager"></a>System Center Operations Manager
Tous les composants SCOM sont installés dans votre centre de données.  [Les agents sont installés](http://technet.microsoft.com/library/hh551142.aspx) sur des ordinateurs Windows et Linux gérés par SCOM.  Les agents se connectent trop[serveurs d’administration](https://technet.microsoft.com/library/hh301922.aspx) qui communiquent avec l’entrepôt de données et de la base de données SCOM hello.  Les agents s’appuient sur les serveurs de domaine d’authentification tooconnect toomanagement.  Ceux en dehors d’un domaine approuvé peuvent effectuer l’authentification par certificat ou se connecter tooa [serveur de passerelle](https://technet.microsoft.com/library/hh212823.aspx).

SCOM requiert deux bases de données SQL, un pour les données opérationnelles et un autre magasin toosupport création de rapports et de données analyse des données.  A [Reporting Server](https://technet.microsoft.com/library/hh298611.aspx) exécute tooreport de SQL Reporting Services sur des données à partir de l’entrepôt de données hello. 

La solution SCOM peut surveiller les ressources cloud à l’aide de packs d’administration pour des produits tels qu’[Azure](https://www.microsoft.com/download/details.aspx?id=38414), [Office 365](https://www.microsoft.com/download/details.aspx?id=43708) et [AWS](http://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/AWSManagementPack.html).  Ces packs d’administration utilisent un ou plusieurs agents locales en tant que proxy pour la détection de cloud computing ressources et en cours d’exécution des workflows toomeasure leurs performances et disponibilité.  Les agents proxy permettent également trop[analyser des périphériques réseau](https://technet.microsoft.com/library/hh212935.aspx) et d’autres ressources externes.

Bonjour Console opérateur est une application Windows qui se connecte tooone hello des serveurs d’administration permet de hello administrateur tooview et analyse les données collectées et configurer l’environnement de SCOM hello.  Une console web peut être hébergée sur n’importe quel serveur IIS et analyse les données via un navigateur.

![Architecture SCOM](media/operations-management-suite-monitoring-product-comparison/scom-architecture.png)

### <a name="log-analytics"></a>Log Analytics
La plupart des composants d’OMS sont Bonjour Azure cloud afin de pouvoir déployer et gérer à moindre coût et les tâches administratives.  Toutes les données collectées par Analytique de journal est stocké dans le référentiel d’OMS hello.

Log Analytics peut collecter des données à partir de l’une de ces trois sources :

* Machines physiques et virtuelles exécutant Windows et hello [Microsoft Monitoring Agent (MMA)](https://technet.microsoft.com/library/mt484108.aspx) ou Linux et hello [Operations Management Suite Agent for Linux](https://technet.microsoft.com/library/mt622052.aspx).  Ces machines peuvent être locales ou virtuelles (hébergées dans Azure ou dans un autre cloud).
* Un compte de stockage Azure qui collecte les données [Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) à partir d’un rôle de travail, d’un rôle Web ou d’une machine virtuelle dans Azure.
* [Groupe d’administration SCOM connexion tooa](https://technet.microsoft.com/library/mt484104.aspx).  Dans cette configuration, les agents de hello communiquent avec les serveurs d’administration SCOM qui livrent hello toohello SCOM de données où elle est ensuite remis toohello magasin de données OMS.
  Les administrateurs analyser les données collectées et configurez les Analytique de journal avec du portail OMS hello qui est hébergé dans Azure et sont accessibles à partir de n’importe quel navigateur.  Les applications mobiles tooaccess ces données sont disponibles pour les plateformes standard hello.

![Architecture Log Analytics](media/operations-management-suite-monitoring-product-comparison/log-analytics-architecture.png)

### <a name="integrating-scom-and-log-analytics"></a>Intégration des solutions SCOM et Log Analytics
SCOM est utilisé comme source de données pour l’Analytique des journaux vous pouvez tirer parti des fonctionnalités de hello des deux produits dans un environnement d’analyse de hybride.  Vous pouvez configurer des agents SCOM existants via toobe de Console opérateur hello gérées par OMS, en plus des packs d’administration de toorun toocontinuing de SCOM.  
Remise des données à partir d’un groupe d’administration SCOM connecté tooLog Analytique à l’aide d’une des quatre méthodes :

* Événements et les données de performances sont collectées par l’agent de hello et remises tooSCOM.  Serveurs d’administration dans SCOM remettra hello données tooLog Analytique.
* Certains événements tels que les journaux IIS des événements de sécurité continuent toobe remis directement tooLog Analytique à partir de l’agent de hello.
* Certaines solutions seront remettre l’agent toohello de logiciels supplémentaires ou exiger que le logiciel soit installé toocollect des données supplémentaires.  Ces données seront généralement être envoyées directement tooLog Analytique.
* Certaines solutions collectent des données directement à partir de serveurs d’administration SCOM qui ne proviennent pas d’agent de hello.  Par exemple, hello [solution de gestion des alertes](https://technet.microsoft.com/library/mt484092.aspx) collecte les alertes à partir de SCOM après qu’ils ont été créés.

## <a name="monitoring-logic"></a>Logique de surveillance
SCOM et Analytique de journal travailler avec des données collectées auprès des agents similaires mais présentent des différences fondamentales dans la façon dont ils définissent et implémentent la logique de la collecte de données et comment ils analysent les données hello qu’ils recueillent.

### <a name="operations-manager"></a>Operations Manager
Logique de l’analyse de SCOM est implémentée dans [packs d’administration](https://technet.microsoft.com/library/hh457558.aspx) qui contiennent la logique de détection des composants toomonitor, mesurer l’intégrité de hello de ces composants et pour la collecte des données tooanalyze.  La surveillance des données peut simplement consister à collecter un événement ou à mesurer les performances, ou utiliser une logique complexe implémentée dans un script.  Packs d’administration qui incluent une analyse complète sont disponibles pour un large éventail de [Microsoft et les applications tierces](http://go.microsoft.com/fwlink/?LinkId=82105) dans Ajout toohardware et périphériques réseau.  Vous pouvez [créer vos propres packs d’administration](http://aka.ms/mpauthor) pour vos applications personnalisées.

Packs d’administration contiennent plusieurs flux de travail effectuant chacune une fonction d’analyse distincte comme un compteur de performances, vérification de l’état d’un service hello ou un script en cours d’exécution.  Chaque flux de travail s’exécute indépendamment et définit ses propres résultats tels que la base de données, elle écrit tooand si elle génère une alerte. 

Vous pouvez remplacer les détails du flux de travail tels que la fréquence de hello que leur exécution, le seuil de hello considèrent une erreur et gravité hello d’alerte hello qu’ils génèrent.  Vous pouvez également déployer des fonctionnalités supplémentaires en ajoutant vos propres flux de travail.

![Remplace](media/operations-management-suite-monitoring-product-comparison/scom-overrides.png)

Packs d’administration sont installés dans la base de données Operations Manager hello et distribués automatiquement tooagents par les serveurs d’administration.  Chaque agent de télécharger les packs d’administration et de charge des applications de toohello pertinentes de flux de travail qu’ils ont installé automatiquement.  Données collectées par l’agent de hello sont remises toohello précédent serveur d’administration pour l’insertion dans l’entrepôt de données et de la base de données SCOM hello.  Hello Console opérateur vous permet de tooview et analyser ces données par le biais des affichages personnalisés, les tableaux de bord et les rapports inclus dans le pack d’administration hello.

distribution Hello des packs d’administration est illustrée dans hello suivant schéma.

![Flux du pack d’administration](media/operations-management-suite-monitoring-product-comparison/scom-mpflow.png)

### <a name="log-analytics"></a>Log Analytics
#### <a name="event-and-performance-collection"></a>Collecte d’événements et de données de performance
Log Analytics collecte les événements et les compteurs de performances des systèmes de l’agent à l’aide de sources telles que le journal des événements Windows, les journaux IIS et Syslog.  Vous pouvez définir des critères pour lesquels les données sont collectées via le portail d’Analytique de journal hello et ensuite créer des requêtes de journal tooanalyze hello collectée données.  Un ensemble de critères standard est défini lorsque vous créez votre espace de travail OMS. Vous pouvez également définir des critères supplémentaires pour des applications spécifiques. 

![Définition des journaux des événements dans Log Analytics](media/operations-management-suite-monitoring-product-comparison/log-analytics-definedata.png)

Alors que SCOM a plusieurs flux de travail détaillé qui définissent généralement des critères spécifiques pour les données et l’action de hello qui doit être effectuée dans la réponse, Analytique de journal a des critères plus générales pour la collecte de données.  Journal des requêtes et les solutions fournissent plus de critères ciblés pour l’analyse et agissant sur des données spécifiques dans le cloud de hello après leur collecte.

#### <a name="solutions"></a>Solutions
Les solutions offrent une logique supplémentaire pour la collecte et l’analyse des données.  Vous pouvez sélectionner l’abonnement de solutions tooadd tooyour OMS à partir de la galerie de solutions de hello.

![Galerie de solutions](media/operations-management-suite-monitoring-product-comparison/log-analytics-solutiongallery.png)

Les solutions exécutent principalement dans le cloud hello fournissant l’analyse des événements et compteurs de performances collectés dans le référentiel d’OMS hello.  Ils peuvent également définir les toobe des données supplémentaires collectée et qui peut être analysé avec journal des requêtes ou par l’interface utilisateur supplémentaire fournie par la solution hello dans le tableau de bord OMS hello. 

Par exemple, hello [solution de suivi des modifications](https://technet.microsoft.com/library/mt484099.aspx) détecte des modifications sur les systèmes de l’agent de configuration et écrit les événements toohello OMS référentiel qui peut être analysé avec plusieurs vues graphiques qui résument a détecté des modifications.  Vous pouvez descendre à partir de la vue de hello résumée dans les requêtes de journal que hello d’affichage des données collectées par hello solution détaillées.

Pendant que vous pouvez sélectionner les solutions vous ajoutez tooyour abonnement, vous n’avez actuellement hello capacité toocreate vos propres solutions.  Vous pouvez sélectionner les événements hello et toocollect des compteurs de performances et créer des vues personnalisées en fonction de vos propres requêtes de journal.

Hello logique pour l’Analytique des journaux de l’analyse est résumée dans hello suivant schéma.

![Flux de la solution Log Analytics](media/operations-management-suite-monitoring-product-comparison/log-analytics-solution-flow.png)

## <a name="health-monitoring"></a>Surveillance de l’intégrité
### <a name="operations-manager"></a>Operations Manager
SCOM peut hello différents composants d’une application de modèle et fournit un contrôle d’intégrité en temps réel pour chacun.  Ainsi, vous affichez uniquement toonot détecté des erreurs et des performances au fil du temps, mais également toovalidate hello d’intégrité réel du système ou une application et chacun de ses composants à un moment donné.  Car il prend en charge hello périodes dont une application est disponible, moteur de contrôle d’intégrité hello dans SCOM prend également en charge les contrats de niveau de Service (SLA) qui analyse et rapports sur la disponibilité d’une application au fil du temps hello.

Par exemple, hello ci-dessous affiche l’intégrité en temps réel de hello des moteurs de base de données SQL analysé par SCOM.  intégrité de Hello de chacune des bases de données hello pour un des moteurs de base de données hello figure en bas de hello la moitié de la vue de hello.

![Vue d’état](media/operations-management-suite-monitoring-product-comparison/scom-state-view.png)

Hello Explorateur d’intégrité d’un des moteurs de base de données hello ci-dessous avec les moniteurs hello sont utilisée toodetermine son intégrité globale.  Ces moniteurs sont définis dans hello Pack d’administration SQL et exécutées sur tous les moteurs de base de données SQL découverts par SCOM.

![Explorateur d’intégrité](media/operations-management-suite-monitoring-product-comparison/scom-health-explorer.png)

Composants sur plusieurs systèmes peuvent être combinées toomeasure hello la santé d’une application distribuée.  Cela peut être particulièrement utile pour les applications métier qui intègrent plusieurs composants distribués.  Vous pouvez créer un modèle qui mesure intégrité hello de chaque composant ce cumul en disponibilité pour l’application hello.

Active Directory est un exemple d’un Pack d’administration qui fournit un modèle tooanalyze ses composants distribués.  diagramme d’exemple Hello ci-dessous montre la santé hello de hello environnement global et relation hello entre forêts, domaines et les contrôleurs de domaine.  Chacun de ces composants inclut des sous-composants et plusieurs moniteurs exemple similaire de toohello SQL ci-dessus.

![Vue schématique de SCOM](media/operations-management-suite-monitoring-product-comparison/scom-diagram-view.png)

### <a name="log-analytics"></a>Log Analytics
OMS ne pas inclure un moteur courantes des applications toomodel ou mesurer leur intégrité en temps réel.  Les solutions individuelles peuvent évaluer hello intégrité globale des services particuliers en fonction des données collectées, et ils peuvent installer une logique personnalisée sur l’analyse en temps réel des tooperform agent hello.  Solutions s’exécutant dans le cloud hello avec le référentiel OMS de toohello accès, ils offrent souvent une analyse plus approfondie qu’est généralement effectué par les packs d’administration. 

Par exemple, hello [solutions d’évaluation d’Active Directory et l’évaluation SQL](https://technet.microsoft.com/library/mt484102.aspx) analyser les données collectées et fournir une évaluation pour les différents aspects de l’environnement de hello.  Il fournit des recommandations pour les améliorations qui peuvent être rendues tooimprove hello et performances des environnement de hello.

![Solution d’évaluation d’AD](media/operations-management-suite-monitoring-product-comparison/log-analytics-ad-assessment.png)

## <a name="data-analysis"></a>Analyse des données
SCOM et Analytique de journal fournissent des données de tooanalyze collectée différentes fonctionnalités.  SCOM a vues et tableaux de bord Bonjour Console opérateur pour l’analyse des données récentes dans une variété de formats et de rapports pour présenter des données à partir de l’entrepôt de données hello dans un format tabulaire.  Analytique de journal fournit une interface et un langage de requête complet du journal d’analyse des données dans le référentiel d’OMS hello.  Lorsque SCOM est utilisé comme source de données pour l’Analytique des journaux, référentiel de hello comprend les données collectées par SCOM outils d’Analytique de journal hello peuvent avoir des données tooanalyze utilisés des deux systèmes.

### <a name="operations-manager"></a>Operations Manager
#### <a name="views"></a>Views
Les vues dans la Console opérateur de hello permettent de vous tooview différents types de données collectées par SCOM dans différents formats, généralement sous forme de tableau pour les événements, alertes, données d’état et des graphiques de ligne pour les données de performances.  Vues effectuer une analyse minimale ou la consolidation de données de salutation mais vous autorisent le toofilter en fonction de critères de tooparticular. 

![Views](media/operations-management-suite-monitoring-product-comparison/scom-views.png)

Packs d’administration fournira généralement plusieurs vues prenant en charge application hello ou système qu’il surveille.  Cela peut inclure des affichages des États des objets différents hello qui détecte de pack d’administration de hello, affichages des alertes pour résoudre les problèmes détectés et des affichages pour les compteurs de performances.

Les vues sont particulièrement appropriées pour analyser l’état actuel de hello des hello, y compris les alertes actives et l’état de santé de hello des systèmes surveillés et des objets.  Vous pouvez explorer des données d’événement ou de performance toodetailed prise en charge d’une alerte donnée dans l’ordre toodiagnose sa cause racine. De même, vous pouvez afficher les performances hello et l’intégrité des différents composants d’une application de tooassess son état actuel.

#### <a name="dashboards"></a>Tableaux de bord
Tableaux de bord dans hello Console opérateur fonctionne principalement avec hello mêmes données que les vues, mais sont plus personnalisables et peuvent comporter des visualisations plus riches.  Vous disposez d’un ensemble de tableaux de bord standard que vous pouvez facilement personnaliser selon vos besoins.  Vous pouvez également utiliser un widget PowerShell qui peut afficher les données obtenues à l’aide d’une requête PowerShell.

![tableau de bord](media/operations-management-suite-monitoring-product-comparison/scom-dashboard.png)

Les développeurs ont hello capacité tooadd des composants personnalisés toodashboards qu'incluent dans leurs packs d’administration.  Il peut s’agir d’application hautement spécialisées tooa comme tableau de bord hello Bonjour Pack d’administration de SQL indiqué ci-dessous.  Ce tableau de bord peut également servir de modèle pour les versions personnalisées.

![Tableau de bord SQL](media/operations-management-suite-monitoring-product-comparison/scom-sql-dashboard.png)

#### <a name="reports"></a>Rapports
Rapports dans SCOM analyser les données à partir de l’entrepôt de données hello dans un format tabulaire.  Ils peuvent être imprimés et exécutés automatiquement dans différents formats de fichiers, notamment PDF, CSV et Word.  Les rapports fonctionnent avec les données d’entrepôt de données hello afin qu’ils soient particulièrement appropriés pour l’analyse des tendances à long terme.

Les packs d’administration incluent généralement des rapports personnalisés pour une application spécifique.  Vous pouvez également sélectionner des rapports à partir d’une bibliothèque de rapports génériques que vous pouvez personnaliser pour vos propres applications ou utiliser pour effectuer une analyse ad hoc.

Voici un exemple de rapport de performances affichant les données collectées par hello Active Directory Management Pack.

![Rapport](media/operations-management-suite-monitoring-product-comparison/scom-report.png)

### <a name="log-analytics"></a>Log Analytics
Analytique de journal a un [de langage de requête](https://technet.microsoft.com/library/mt484120.aspx) que vous pouvez utiliser tooperform analyse les données à partir de plusieurs applications sans hello besoin toocreate un affichage personnalisé ou un rapport.  OMS étant implémenté dans le cloud de hello, les performances des requêtes et d’analyse de données ne sont pas des limites matérielles de tooany sujet et peut analyser rapidement des requêtes, y compris des millions d’enregistrements. 

Requêtes d’Analytique de journal sont également base hello d’autres fonctionnalités.  Vous pouvez enregistrer une requête, exporter ses tooExcel de résultats ou automatiquement exécuter à intervalles réguliers afin de générer une alerte si ses résultats correspondent aux critères particuliers.  

![Flux d’une requête de journal](media/operations-management-suite-monitoring-product-comparison/log-analytics-query-flow.png)

Voici un exemple d’une requête Log Analytics.  Dans cet exemple, tous les événements « démarré » dans le nom de hello sont retournées et regroupés par événement ID.  utilisateur de Hello fournit simplement la requête de hello et Analytique de journal génère dynamiquement l’analyse de hello hello tooperform de l’interface utilisateur.  Sélection d’un élément dans la liste de hello retournera hello détaillées des données d’événement.

![Requête de journal](media/operations-management-suite-monitoring-product-comparison/log-analytics-query.png)

En outre analyse ad hoc de tooproviding, Analytique de journal des requêtes peuvent être enregistrées pour une utilisation ultérieure et également ajouté tooyour [tableau de bord OMS](http://technet.microsoft.com/library/mt484090.aspx) comme indiqué dans hello l’exemple suivant.

![tableau de bord OMS](media/operations-management-suite-monitoring-product-comparison/log-analytics-dashboard.png)

## <a name="next-steps"></a>Étapes suivantes
* Déployer [System Center Operations Manager (SCOM)](https://technet.microsoft.com/library/hh205987.aspx)
* S’inscrire au service [Log Analytics](https://azure.microsoft.com/documentation/services/log-analytics)  

