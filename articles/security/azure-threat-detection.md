---
title: "aaaAzure détection des menaces avancées | Documents Microsoft"
description: "En savoir plus sur Identity Protection et ses fonctionnalités."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: TomSh
ms.openlocfilehash: 63e2c541fd4ce2c571af9d5845c9a9bd4b03b2a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-advanced-threat-detection"></a>Détection avancée des menaces Azure
## <a name="introduction"></a>Introduction

### <a name="overview"></a>Vue d'ensemble

Microsoft a développé une série de livres blancs, des vues d’ensemble de la sécurité, des meilleures pratiques et des listes de contrôle tooassist Azure hello de clients sur diverses fonctionnalités liées à la sécurité qui sont disponibles dans et hello environnante plateforme Azure. les rubriques de Hello en termes de largeur et la profondeur de plage et sont régulièrement mises à jour. Ce document fait partie de cette série comme résumé dans hello après section abstraite.

### <a name="azure-platform"></a>Plateforme Azure

Azure est une plateforme de service de cloud public qui prend en charge hello plus vaste choix de systèmes d’exploitation, langages de programmation, infrastructures, outils, bases de données et les appareils.
Il prend en charge hello suivant des langages de programmation :
-   Exécuter des conteneurs Linux avec l’intégration Docker.
-   Créer des applications avec JavaScript, Python, .NET, PHP, Java et Node.js
-   créer des serveurs principaux pour les appareils iOS, Android et Windows.

Services de cloud public Azure prend en charge hello mêmes technologies des millions de développeurs et professionnels de l’informatique s’appuient sur déjà et faites confiance.

Lorsque vous effectuez une migration tooa cloud public avec une organisation, cette organisation est responsable de tooprotect vos données et fournir la sécurité et gouvernance autour de système de hello.

L’infrastructure Azure est conçu de tooapplications de fonctionnalité hello pour l’hébergement des millions de clients simultanément, et fournit une base fiable sur laquelle entreprises peuvent répondre aux besoins de leur sécurité. Azure fournit un large éventail d’options tooconfigure et personnaliser les exigences de hello toomeet de sécurité de vos déploiements d’applications. Ce document vous aide à répondre à ces exigences.

### <a name="abstract"></a>Résumé

Microsoft Azure intègre une fonctionnalité de détection des menaces avancée à travers certains services, comme Azure Active Directory, Azure Operations Management Suite (OMS) et Azure Security Center. Cette collection de services de sécurité et des fonctionnalités fournit un moyen simple et rapide de toounderstand que se passe-t-il dans vos déploiements Azure.

Ce livre blanc vous guide hello « approches de Microsoft Azure » à la vulnérabilité de menace diagnostic et analyse des risques de hello associés avec les activités malveillantes hello ciblées sur les serveurs et autres ressources Windows Azure. Cela vous permet de méthodes de hello tooidentify d’identification et la gestion des risques de vulnérabilité avec optimisée solutions par hello plateforme Azure et les services de sécurité des clients et les technologies.

Ce livre blanc se concentre sur la technologie hello de plateforme Azure et les contrôles côté client et ne tente pas de tooaddress SLA, tarification des modèles et des considérations relatives à la pratique DevOps.

## <a name="azure-active-directory-identity-protection"></a>Azure Active Directory Identity Protection

![Azure Active Directory Identity Protection](./media/azure-threat-detection/azure-threat-detection-fig1.png)


[Azure Active Directory Identity Protection](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection) est une fonctionnalité de hello [Azure AD Premium P2](https://docs.microsoft.com/azure/active-directory/active-directory-editions) edition qui vous fournit une vue d’ensemble des événements à risque hello et des vulnérabilités potentielles qui affectent votre organisation identités. Microsoft a été la sécurisation des identités basée sur le cloud pour plus de dix ans, et avec Azure AD Identity Protection, Microsoft est d’effectuer ces mêmes systèmes de protection disponible tooenterprise clients. Identity Protection tire parti des fonctionnalités existantes de détection des anomalies d’Azure AD (disponibles via les [rapports d’activités anormales d’Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-view-access-usage-reports#anomalous-activity-reports)) et introduit de nouveaux types d’événements à risque capables de détecter les anomalies en temps réel.

Protection de l’identité utilise les algorithmes d’apprentissage automatique adaptative et anomalies de toodetect heuristique et événements à risque susceptibles d’indiquer qu’une identité a été compromise. À l’aide de ces données, la Protection d’identité génère des rapports et des alertes qui vous permettent de tooinvestigate ces événements à risque et prenez les mesures appropriées de mise à jour ou d’atténuation.

Mais Azure Active Directory Identity Protection est plus qu’un outil de surveillance et de création de rapports. Basé sur les événements à risque, Identity Protection calcule un niveau de risque d’utilisateur pour chaque utilisateur, ce qui vous tooconfigure des stratégies en fonction des risques tooautomatically protéger hello identités de votre organisation.

Ces stratégies en fonction des risques, ajout tooother [des contrôles d’accès conditionnel](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) fournies par Azure Active Directory et [EMS](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access), peut bloquer ou proposer des actions de mise à jour adaptative qui incluent automatiquement les réinitialisations de mot de passe et la mise en œuvre l’authentification multifacteur.

### <a name="identity-protections-capabilities"></a>Fonctionnalités du service Identity Protection

Mais Azure Active Directory Identity Protection est bien plus qu’un outil de surveillance et de création de rapports. tooprotect identités de votre organisation, vous pouvez configurer des stratégies basées sur les risques qui répondent automatiquement toodetected problèmes lorsqu’un niveau de risque spécifié a été atteint. Ces stratégies, en outre tooother conditionnel accéder aux contrôles fournis par Azure Active Directory et EMS, pouvez bloquer automatiquement ou initier des actions de mise à jour ADAPTATIF, y compris les réinitialisations de mot de passe et la mise en œuvre l’authentification multifacteur.

Quelques exemples de certaines façons de hello Azure Identity Protection peut aider à sécuriser vos comptes et identités incluent :

[Détection des événements et des comptes à risque :](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection#detection)
-   Détection de six types d’événements à risque à l’aide de l’apprentissage automatique et des règles heuristiques
-   Calcul du niveau de risque des utilisateurs
-   Fournir des recommandations personnalisées tooimprove globale posture de sécurité en mettant en surbrillance les vulnérabilités

[Examen des événements à risque :](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection#investigation)
-   Envoi de notifications pour les événements à risque
-   Examen des événements à risque à l’aide d’informations contextuelles et pertinentes
-   En fournissant des workflows de base tootrack enquêtes
-   Fournissant un accès facile tooremediation des actions telles que la réinitialisation de mot de passe

[Stratégies d’accès conditionnel en fonction des risques :](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection#risky-sign-ins)
-   Stratégie toomitigate risquées connexions par le blocage des connexions ou exigeant l’authentification multifacteur.
-   Stratégie tooblock ou des comptes d’utilisateur présente des risques sécurisé
-   Stratégie toorequire utilisateurs tooregister pour l’authentification multifacteur

### <a name="azure-ad-privileged-identity-management-pim"></a>Azure AD Privileged Identity Management (PIM)

Grâce à la [Gestion des identités privilégiées Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure),

![Azure AD Privileged Identity Management](./media/azure-threat-detection/azure-threat-detection-fig2.png)

vous pouvez gérer, contrôler et surveiller l’accès au sein de votre organisation. Cela inclut tooresources d’accès dans Azure AD et d’autres services en ligne Microsoft comme Office 365 ou Microsoft Intune.

Azure AD Privileged Identity Management vous aide à :

-   Obtention d’une alerte et de rapport sur les administrateurs Azure AD et « juste à temps » d’un accès administratif tooMicrosoft Online Services comme Office 365 et Intune

-   Obtenir des rapports sur l'historique des accès administrateur et sur les modifications apportées aux affectations de l'administrateur

-   Recevoir des alertes sur le rôle privilégié de tooa d’accès

## <a name="microsoft-operations-management-suite-oms"></a>Microsoft Operations Management Suite (OMS)

[Microsoft Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) est une solution de gestion informatique de Microsoft qui vous permet de gérer et de protéger votre infrastructure locale et de cloud. La solution OMS étant implémentée sous la forme d’un service informatique, elle peut être opérationnelle rapidement, avec un investissement minimal dans des services d’infrastructure. Les nouvelles fonctionnalités de sécurité sont fournies automatiquement, ce qui vous permet d’économiser sur les coûts de mise à niveau et de maintenance.

En outre des services précieux tooproviding sur son propre, OMS peuvent intégrer les composants de System Center tels que [System Center Operations Manager](https://blogs.technet.microsoft.com/cbernier/2013/10/23/monitoring-windows-azure-with-system-center-operations-manager-2012-get-me-started/) tooextend vos investissements de gestion de sécurité existant en hello de cloud computing. System Center et OMS peuvent travailler ensemble tooprovide expérience d’une gestion hybride complète.

### <a name="holistic-security-and-compliance-posture"></a>Approche globale de la sécurité et de la conformité

Hello [tableau de bord OMS sécurité et Audit](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started) fournit une vue globale de votre organisation posture de sécurité informatique avec des requêtes de recherche intégrées pour détecter les problèmes importants qui requièrent votre attention. tableau de bord sécurité et Audit Hello est écran d’accueil hello pour tous les éléments liés toosecurity d’OMS. Il fournit un aperçu de haut niveau dans l’état de sécurité hello de vos ordinateurs. Il inclut également hello capacité tooview tous les événements de hello dernières 24 heures, 7 jours, ou n’importe quel autre intervalle de temps personnalisé.

OMS tableaux de bord vous aident rapidement et facilement hello posture de sécurité globale de n’importe quel environnement, tout dans le contexte hello des opérations informatiques, y compris : évaluation de la mise à jour logicielles, l’évaluation du logiciel anti-programme malveillant et lignes de base de configuration. En outre, les données du journal de sécurité sont facilement accessibles toostreamline hello sécurité et conformité de l’audit des processus.

tableau de bord OMS sécurité et Audit Hello est organisé en quatre catégories principales :

![Tableau de bord de la solution de sécurité et d’audit d’OMS](./media/azure-threat-detection/azure-threat-detection-fig3.jpg)

-   **Domaines de sécurité :** dans cette zone, vous serez en mesure de toofurther Explorer les enregistrements de sécurité au fil du temps, accéder l’évaluation des logiciels malveillants, mettre à jour d’évaluation, la sécurité du réseau, informations d’identité et accès, les ordinateurs avec des événements de sécurité et rapidement tableau de bord du centre de sécurité de tooAzure accès.

-   **Problèmes importants :** cette option vous permet de tooquickly identifier le numéro de hello de problèmes actifs et hello gravité de ces problèmes.

-   **Détections (version préliminaire) :** vous permet de modèles d’attaque tooidentify en affichant les alertes de sécurité qu’elles ont lieu par rapport à vos ressources.

-   **Informations sur les menaces :** vous permet de modèles d’attaque tooidentify en affichant le nombre total de hello de serveurs avec le trafic malveillant IP sortant, type de menace nuisible hello et une carte qui montre la provenance des ces adresses IP.

-   **Requêtes de sécurité courantes :** cette option permet de vous une liste de sécurité les plus courantes hello des requêtes que vous pouvez utiliser toomonitor votre environnement. Lorsque vous cliquez sur une de ces requêtes, il ouvre le panneau de recherche hello avec résultats hello pour cette requête.

### <a name="insight-and-analytics"></a>Insight & Analytics
Au centre de hello du [Analytique de journal](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) est le référentiel OMS hello, qui est hébergé dans hello cloud Azure.

![Insight & Analytics](./media/azure-threat-detection/azure-threat-detection-fig4.png)

Collecte de données dans le référentiel de hello à partir de sources connectées par la configuration des sources de données et ajout abonnement tooyour de solutions.

![abonnement](./media/azure-threat-detection/azure-threat-detection-fig5.png)

Solutions et sources de données créent chacune différents types d’enregistrements qui ont leur propre jeu de propriétés, mais peuvent toujours être analysées ensemble dans le référentiel toohello de requêtes. Cela vous permet de hello toouse même toowork outils et méthodes avec différents types de données collecté par différentes sources.


La plupart de votre interaction avec Analytique de journal est par le biais du portail OMS hello, qui s’exécute dans n’importe quel navigateur et vous fournit des paramètres d’accès tooconfiguration et plusieurs outils tooanalyze et agir sur les données collectées. À partir du portail de hello, vous pouvez utiliser [recherche de journal](https://docs.microsoft.com/azure/log-analytics/log-analytics-log-searches) lorsque vous construisez la demande des données tooanalyze collectée, [tableaux de bord](https://docs.microsoft.com/azure/log-analytics/log-analytics-dashboards), que vous pouvez personnaliser avec des vues graphiques des recherches plus précieuses et [solutions](https://docs.microsoft.com/azure/log-analytics/log-analytics-add-solutions), qui fournissent des outils d’analyse et de fonctionnalités supplémentaires.

![outils d’analyse](./media/azure-threat-detection/azure-threat-detection-fig6.png)

Solutions ajoutent des fonctionnalités tooLog Analytique. Principalement, ils s’exécutent dans le cloud de hello et fournissent une analyse des données collectées dans le référentiel d’OMS hello. Ils peuvent également définir des nouveaux toobe types d’enregistrements collectée peut être analysée avec des recherches de journaux ou par l’interface utilisateur supplémentaire fournie par la solution hello dans le tableau de bord OMS hello.
Hello, sécurité et Audit est un exemple de ces types de solutions.



### <a name="automation--control-alert-on-security-configuration-drifts"></a>Automatisation et contrôle : alerte sur les anomalies de configuration de la sécurité

Azure Automation automatise les processus administratifs avec des runbooks qui sont basés sur PowerShell et exécutez Bonjour cloud Azure. Les runbooks peuvent également être exécutés sur un serveur dans votre ressources local toomanage de centre de données local. Azure Automation assure la gestion de la configuration avec PowerShell DSC (Desired State Configuration).

![Azure Automation](./media/azure-threat-detection/azure-threat-detection-fig7.png)

Vous pouvez créer et gérer des ressources DSC hébergées dans Azure et les appliquer toodefine des systèmes locaux et toocloud et automatiquement appliquer leur configuration ou obtenir des rapports sur dérive toohelp vous assurer que les configurations de sécurité doit rester au sein de la stratégie.

## <a name="azure-security-center"></a>Azure Security Center

Azure Security Center vous permet de protéger vos ressources Azure. Il fournit des fonctions intégrées de surveillance de la sécurité et de gestion des stratégies sur vos abonnements Azure. Dans le service de hello, vous ne pouvez toodefine stratégies non seulement par rapport à vos abonnements Azure, mais également contre [groupes de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal), de sorte que vous pouvez être plus précis.

![Azure Security Center](./media/azure-threat-detection/azure-threat-detection-fig8.png)

Chercheurs en sécurité de Microsoft sont constamment sur lookout hello pour les menaces. Ils ont accès tooan vaste de télémétrie acquise à partir de la présence de Microsoft dans le cloud de hello et sur site. Cette collection de large et différents des jeux de données permet de Microsoft toodiscover nouveaux modèles et tendances sur ses produits en local de consommateur et d’entreprise, ainsi que ses services en ligne.

Azure Security Center peut donc rapidement mettre à jour ses algorithmes de détection, puisque les pirates sont à l’origine d’attaques innovantes de plus en plus sophistiquées. Cette approche permet de faire face à des menaces en pleine mutation.

![Centre de sécurité](./media/azure-threat-detection/azure-threat-detection-fig9.jpg)

Détection des menaces de sécurité Center fonctionne en collectant automatiquement des informations de sécurité à partir de vos ressources Azure, hello réseau et les solutions de partenaire connecté.  Analyse de ces informations, la corrélation des informations provenant de plusieurs sources, les menaces tooidentify.
Alertes de sécurité sont définies dans le centre de sécurité ainsi que des recommandations sur la tooremediate hello menace.

Azure Security Center emploie des analyses de sécurité avancées allant bien au-delà des approches simplement basées sur la signature. Découvertes dans les données volumineuses et [apprentissage](https://azure.microsoft.com/blog/machine-learning-in-azure-security-center/) technologies sont les événements tooevaluate utilisé entre l’infrastructure de cloud entière hello : détection des menaces qui seraient impossible tooidentify à l’aide des méthodes manuelles et de prédiction hello évolution d’attaques. Ces analytique de sécurité inclut des éléments suivants de hello.

### <a name="threat-intelligence"></a>Informations sur les menaces

Microsoft dispose d’une multitude d’informations en matière de menaces à l’échelle mondiale.
Flux de données de télémétrie dans à partir de plusieurs sources, telles que Azure, Office 365, Microsoft CRM en ligne, Microsoft Dynamics AX, outlook.com, MSN.com, hello Microsoft Digital Crimes unité (DCU) et MSRC Microsoft Security Response Center ().

![Informations sur les menaces](./media/azure-threat-detection/azure-threat-detection-fig10.jpg)

Chercheurs également informé threat intelligence qui est partagé entre les fournisseurs de services cloud principal et s’abonne toothreat intelligence flux provenant de tiers. Centre de sécurité Azure peut utiliser cette tooalert informations vous toothreats de connus mauvais acteurs. Voici quelques exemples :

-   **Valorisation hello Power de Machine Learning -** Azure Security Center a accès tooa grande quantité de données sur l’activité réseau de cloud, qui peut être utilisé de menaces toodetect ciblant vos déploiements Azure. Par exemple :

-   **Détections de Force brute -** Machine learning est toocreate utilisé un modèle historique de tentatives d’accès à distance, ce qui permet de toodetect les attaques en force sur les ports SQL, RDP et SSH.

-   **Sortantes DDoS et Botnet détection** -un objectif commun d’attaques ciblées sur les ressources de cloud est la puissance de calcul hello toouse de tooexecute de ces ressources autres attaques.

-   **Nouveau comportement Analytique serveurs et les machines virtuelles -** une fois qu’un ordinateur virtuel ou le serveur est compromis, les attaquants utilisent une grande variété de techniques tooexecute un code malveillant sur ce système tout en évitant de détection, assurer la persistance, ce qui vous évite contrôles de sécurité.

-   **Détection des menaces de base de données SQL Azure -** tooaccess ou exploiter les bases de données tente de la détection des menaces pour la base de données SQL Azure qui identifient les activités de base de données anormales indiquant inhabituel et potentiellement dangereux.

### <a name="behavioral-analytics"></a>Analyse comportementale

Analytique comportementale est une technique qui analyse et compare la collecte des données tooa de modèles connus. Toutefois, ces modèles ne sont pas de simples signatures. Ils sont déterminés par les algorithmes d’apprentissage automatique complexes qui sont des jeux de données toomassive appliqué.

![Analyse comportementale](./media/azure-threat-detection/azure-threat-detection-fig11.jpg)


Ils sont également déterminés à travers une analyse minutieuse des comportements malveillants par des experts. Centre de sécurité Azure peuvent utiliser des ressources de tooidentify compromis d’analytique comportementale basées sur l’analyse des journaux de l’ordinateur virtuel, des journaux de périphérique réseau virtuel, les journaux de l’ensemble fibre optique, vidages sur incident et d’autres sources.

En outre, il est corrélation avec les autres toocheck signaux pour prendre en charge de la preuve d’une campagne généralisée. Cette corrélation permet tooidentify les événements qui sont cohérents avec les indicateurs établies de compromission.

Voici quelques exemples :
-   **L’exécution du processus suspects :** pirates plusieurs logiciels malveillants techniques tooexecute sans risque de détection. Par exemple, une personne malveillante peut donner contre les programmes malveillants hello même nom que les fichiers système légitimes mais placez ces fichiers dans un autre emplacement, utilisez un nom qui est très similaire à un fichier sans gravité ou l’extension de fichier du hello de masque true. Analyses et les comportements de processus de modèles de centre de sécurité traitent les valeurs hors norme d’exécutions toodetect telles que celles-ci.

-   **Masqué contre les programmes malveillants et l’exploitation des tentatives :** sophistiquées contre les programmes malveillants peuvent échapper les produits anti-programme malveillant traditionnel par écriture toodisk jamais ou le chiffrement des composants logiciels stockés sur le disque. Toutefois, les logiciels malveillants peuvent être détectées à l’aide de l’analyse de mémoire, comme hello contre les programmes malveillants doivent conserver les traces dans toofunction de mémoire. Lorsque le logiciel tombe en panne, un vidage sur incident capture une partie de la mémoire lors de pannes de hello hello. En analysant la mémoire hello dans le vidage sur incident de hello, Azure Security Center peut détecter des techniques utilisées tooexploit vulnérabilités dans le logiciel, accéder aux données confidentielles et subrepticement persistent au sein d’un ordinateur compromis sans affecter les performances de hello du votre ordinateur.

-   **Latérale le déplacement et la reconnaissance interne :** toopersist dans une compromis réseau et localiser/récolte importantes de données, les attaquants tentent souvent toomove latéralement de hello compromis tooothers machine dans hello même réseau. Centre de sécurité surveille les processus et toodiscover des activités de connexion tente tooexpand brèche de la personne malveillante dans hello réseau, telles que l’exécution de commande à distance, détection de réseau et d’énumération de compte.

-   **Les Scripts PowerShell malveillants :** PowerShell peut être utilisé par des personnes malveillantes tooexecute du code malveillant sur les machines virtuelles cible à des fins différentes. Azure Security Center inspecte l’activité PowerShell à la recherche d’activité suspecte.

-   **Sortant attaques :** attaquants ciblent souvent les ressources de cloud avec comme objectif hello à l’aide de ces attaques supplémentaires toomount de ressources. Compromis des machines virtuelles, par exemple, peut les attaques en force brute de toolaunch utilisé par rapport à d’autres ordinateurs virtuels, envoyer du courrier indésirable ou analyser les ports ouverts et autres appareils sur Internet de hello. En appliquant la machine learning toonetwork trafic, le centre de sécurité peut détecter lorsque les communications réseau sortant dépassent la norme hello. Lorsque du courrier indésirable, centre de sécurité correspond également inhabituel e-mails avec intelligence à partir d’Office 365 toodetermine si les messages hello sont susceptible de nuisance ou résultat hello d’une campagne e-mail légitime.

### <a name="anomaly-detection"></a>Détection des anomalies

Centre de sécurité Azure utilise également les menaces de tooidentify de détection d’anomalies. Dans analytique de toobehavioral contraste (qui dépend des modèles connus dérivés de grands jeux de données), détection d’anomalie plus « personnalisée » et se concentre sur les lignes de base qui sont des déploiements de tooyour spécifique. Apprentissage automatique est appliqué toodetermine une activité normale pour vos déploiements et ensuite les règles sont les conditions d’observation ABERRANTE toodefine généré qui peut représenter un événement de sécurité. Voici un exemple :

-   **Attaques par force brute RDP/SSH entrantes** : vos déploiements peuvent comporter des machines virtuelles occupées par un nombre plus ou moins important de connexions quotidiennes. Centre de sécurité Azure peut déterminer l’activité de connexion de base de ces ordinateurs virtuels et utiliser toodefine d’apprentissage machine autour des activités de connexion normale hello. S’il en existe toute différence avec ligne de base hello défini pour associées à la connexion des caractéristiques, puis une alerte peut être générée. Là encore, l’apprentissage automatique détermine ce qui est significatif.

### <a name="continuous-threat-intelligence-monitoring"></a>Analyse continue des informations sur les menaces

Centre de sécurité Azure fonctionne avec recherche et données pour la science des équipes de sécurité monde hello qui surveillent en continu des modifications dans le paysage des menaces hello. Hello suivant initiatives sont les suivantes :

-   **Analyse des informations sur les menaces** : les informations sur les menaces incluent des mécanismes, des indicateurs, des implications et des conseils pratiques sur les menaces, nouvelles ou existantes. Cette information est partagée dans la Communauté de la sécurité hello et Microsoft surveille en permanence threat intelligence des flux à partir de sources internes et externes.

-   **Partage de signal** : les informations fournies par les équipes de sécurité sur le portefeuille complet de services cloud et locaux, de serveurs, et d’appareils de point de terminaison client de Microsoft sont partagées et analysées.

-   **Spécialistes de la sécurité Microsoft** : engagement continu avec les équipes Microsoft travaillant dans des domaines de la sécurité spécialisés, tels que la forensique et la détection d’attaques web.

-   **Optimisation de la détection :** algorithmes sont exécutées sur des jeux de données des clients réels et chercheurs en sécurité fonctionnent avec les résultats de clients toovalidate hello. VRAI et faux positifs sont des algorithmes d’apprentissage toorefine utilisé.

Ces efforts combinées aboutissent à des détections nouvelle et améliorées, vous pouvez bénéficier d’instantanément : aucune action n’est pour vous tootake.

## <a name="advanced-threat-detection-features---other-azure-services"></a>Fonctionnalités de détection de menaces avancées - Autres services Azure

### <a name="virtual-machine-microsoft-antimalware"></a>Machine virtuelle : Microsoft Antimalware

[Microsoft Antimalware](https://docs.microsoft.com/azure/security/azure-security-antimalware) pour Azure est une solution d’agent unique pour les applications et les environnements de locataire, conçu toorun en arrière-plan hello sans intervention humaine. Vous pouvez déployer la protection en fonction des besoins de hello de votre application les charges de travail, avec une base sécurisée par défaut ou une configuration personnalisée, y compris les logiciels anti-programme malveillant d’analyse avancée. Azure Antimalware est une option de sécurité dédiée aux machines virtuelles Azure qui est automatiquement installée sur toutes les machines virtuelles PaaS Azure.

**Fonctionnalités d’Azure toodeploy et activer Microsoft Antimalware pour vos applications**

#### <a name="microsoft-antimalware-core-features"></a>Principales fonctionnalités de Microsoft Antimalware

-   **Protection en temps réel -** surveille l’activité dans les Services de cloud computing et Machines virtuelles toodetect et bloc contre les programmes malveillants de l’exécution.

-   **Analyse - planifiée** effectue périodiquement ciblé analyse toodetect contre les programmes malveillants, y compris les programmes en cours d’exécution.

-   **Correction de logiciels malveillants** : prend automatiquement des mesures sur les programmes malveillants détectés, notamment la suppression ou la mise en quarantaine des fichiers malveillants et le nettoyage des entrées de registre malveillantes.

-   **Mises à jour de signature -** automatiquement tooensure signatures (définitions de virus) protection plus récente installe hello protection est à jour selon une fréquence prédéterminée.

-   **Mises à jour du moteur du logiciel anti-programme malveillant -** automatiquement les mises à jour hello Microsoft Antimalware engine.

-   **Mises à jour de la plateforme de logiciel anti-programme malveillant-** automatiquement les mises à jour hello Microsoft Antimalware plateforme.

-   **Protection active -** des rapports sur les menaces détectées et ressources suspectes tooMicrosoft tooensure Azure réponse rapide toohello évolution paysage des menaces et l’activation de remise de signature synchrones en temps réel par le biais des métadonnées de télémétrie Hello Microsoft Active Protection système (MAPS).

-   **Exemples de création de rapports -** fournit et des exemples de rapports toohello Microsoft Antimalware service toohelp affiner le service de hello et la résolution des problèmes de l’activer.

-   **Exclusions –** permet tooconfigure des administrateurs de service d’application et de certains fichiers, des processus et lecteurs tooexclude de protection et de performances ou d’autres raisons.

-   **Collecte d’événements de logiciel anti-programme malveillant -** enregistre l’intégrité du service hello contre les logiciels malveillants, les activités suspectes et les actions de mise à jour effectuées dans le journal des événements système d’exploitation hello et les collecte dans le compte de stockage Azure hello client.

### <a name="azure-sql-database-threat-detection"></a>Azure SQL Database Threat Detection

[La détection des menaces de base de données SQL Azure](https://azure.microsoft.com/blog/azure-sql-database-threat-detection-your-built-in-security-expert/) est une nouvelle fonctionnalité d’analyse décisionnelle sécurité intégrée hello service de base de données SQL Azure. Contourner hello toolearn, le profil d’horloge et détecter les activités anormales base de données, la détection des menaces de base de données SQL Azure identifie la base de données de toohello les menaces potentielles.

Les responsables de la sécurité ou autres administrateurs désignés peuvent obtenir une notification immédiate concernant les activités suspectes qui interviennent sur la base de données. Chaque notification fournit des détails d’une activité suspecte hello et recommande comment toofurther examiner et d’atténuer les menaces de hello.

Azure SQL Database Threat Detection détecte actuellement les vulnérabilités potentielles et les attaque par injection SQL, ainsi que les schémas d’accès anormaux à la base de données.

Lorsqu’il reçoit la notification par courrier électronique de détection des menaces, les utilisateurs sont en mesure de toonavigate et vue hello applique les enregistrements d’audit à l’aide du lien ciblé de hello courrier hello qui ouvre un audit visionneuse et/ou d’un modèle préconfiguré audit à partir d’Excel qui montre d’audit appropriées de hello enregistrements en temps hello d’événement suspecte de hello selon toohello suivantes :
-   Stockage d’audit de serveur/base de données hello avec les activités de base de données anormales hello

-   Table de stockage d’audit pertinentes qui a été utilisée au moment de hello hello toowrite d’audit du journal des événements

-   Audit des enregistrements de hello suivant l’heure depuis hello événement se produit.

-   Enregistrements d’audit avec l’ID d’événement semblable au moment de hello d’événement hello (facultatif pour certains détecteurs)

Détecteurs de menace pour la base de données SQL utiliser hello suivant les méthodes de détection :

-   **La détection déterministe –** détecte les types suspects (en fonction des règles) dans les requêtes de client SQL hello qui correspondent à des attaques connues. Cette méthodologie a détection haute et basse faux positif, toutefois limité couverture car il se situe dans une catégorie de hello de « détections atomiques ».

-   **Détection de comportement :** défauts d’une activité anormale, qui est un comportement inhabituel pour une base de données hello qui n’est pas visible pendant hello 30 derniers jours.  Un exemple d’une activité anormale SQL client peut être un pic de connexions/requêtes ayant échouées, un volume élevé de données en cours d’extraction, requêtes canoniques inhabituels et IP adresses utilisées tooaccess hello base de données

### <a name="application-gateway-web-application-firewall"></a>Pare-feu d’applications web sur Application Gateway

[Web Application pare-feu](https://docs.microsoft.com/azure/app-service-web/app-service-app-service-environment-web-application-firewall) est une fonctionnalité de [passerelle d’Application Azure](https://docs.microsoft.com/azure/application-gateway/application-gateway-webapplicationfirewall-overview) qui assure la protection tooweb les applications qui utilisent la passerelle d’application pour standard [contrôle de remise d’Application](https://kemptechnologies.com/in/application-delivery-controllers) fonctions. Pare-feu d’applications Web pour cela les protège contre la plupart des hello [OWASP avoir top 10 vulnérabilités web courantes](https://www.owasp.org/index.php/Top_10_2010-Main)

![Pare-feu d’applications web sur Application Gateway](./media/azure-threat-detection/azure-threat-detection-fig13.png)

-   Protection contre les injections de code SQL

-   Protection de l’exécution de script de site à site

-   Protection contre les attaques web courante comme l’injection de commande, les dissimulations de requêtes HTTP, la séparation de réponse HTTP et les attaques RFI (Remote File Inclusion)

-   Protection contre les violations de protocole HTTP

-   Protection contre les anomalies de protocole HTTP comme un agent-utilisateur hôte manquant et les en-têtes Accept

-   Protection contre les robots, les crawlers et les scanneurs

-   Détection des erreurs de configuration d’application courantes (par exemple, Apache, IIS, etc.)

Configuration de WAF au niveau de la passerelle d’Application fournit hello suivant avantage tooyou :

-   Protéger votre application web contre les vulnérabilités de web et sans code toobackend de modification.

-   Protéger web plusieurs applications à hello même moment derrière une passerelle d’application. Passerelle d’application prend en charge l’hébergement des sites Web de too20 derrière une passerelle unique qui pourrait être protégée contre les attaques de web.

-   Surveillance de votre application web contre les attaques à l’aide de rapports en temps réel générées par les journaux WAF de la passerelle d’application.

-   Certains contrôles de conformité nécessitent tous les exposés à internet toobe de points de terminaison protégé par une solution WAF. En utilisant une passerelle d’application avec WAF activé, vous pouvez remplir ces exigences de conformité.

### <a name="anomaly-detection--an-api-built-with-azure-machine-learning"></a>API Anomaly Detection intégrée à Azure Machine Learning

Anomaly Detection est une API intégrée à Azure Machine Learning qui permet de détecter les différents types de séquences anormales dans vos données de série chronologique. Hello API attribue une anomalie du point de données tooeach de score de série chronologique hello, qui peut être utilisé pour générer des alertes, via des tableaux de bord d’analyse ou de la connexion à vos systèmes de gestion des tickets.

Hello [API de détection d’anomalie](https://docs.microsoft.com/azure/machine-learning/machine-learning-apps-anomaly-detection-api) peut détecter hello suivant les types d’anomalies de données de série chronologique :

-   **Des pics se produisent et DIP :** , par exemple, lors de l’analyse de nombre hello du service de tooa échecs de connexion ou le nombre d’extractions dans un site de commerce électronique, pics inhabituels ou les adresses IP dynamiques peuvent indiquer les attaques de sécurité ou interruptions de service.

-   **Tendances positives et négatives :** lorsque vous surveillez l’utilisation de la mémoire, par exemple, une réduction de taille de la mémoire disponible est signe d’une fuite de mémoire potentielle ; lorsque vous analysez la longueur de la file d’attente d’un service, une tendance à la hausse permanente peut indiquer un problème logiciel sous-jacent.

-   **Niveau de modifications et plage dynamique de valeurs :** , par exemple, niveau modifie des latences d’un service après un service de mise à niveau ou réduire les niveaux d’exceptions après mise à niveau peut être intéressante toomonitor.

apprentissage Hello en fonction d’API de :

-   **Détection flexible et robuste :** modèles de détection d’anomalie hello permettent aux utilisateurs de paramètres de sensibilité tooconfigure et détecter les anomalies entre non saisonnières ainsi que les jeux de données. Les utilisateurs puissent ajuster hello détection modèle toomake hello détection d’anomalie API moins ou plus sensible tootheir conséquente a besoin. Cela signifie détection hello plus ou moins des anomalies visibles dans les données avec et sans saisonnier.

-   **Détection évolutive et en temps voulue :** méthode traditionnelle de hello d’analyse avec présentes seuils définis par la base de connaissances de domaine experts sont toomillions coûteuses et évolutives pas de modifier dynamiquement les jeux de données. modèles de détection d’anomalie Hello dans cette API sont apprises et les modèles sont réglées automatiquement à partir des données historiques et en temps réel.

-   **Détection proactive et exploitable :** il est possible d’appliquer une détection des lents changements de tendance et de niveau afin d’anticiper les anomalies. signaux anormale anticipée Hello détectés peuvent être des utilisé toodirect humains tooinvestigate et agir sur les zones à problème hello.  En outre, il est possible de développer des modèles d’analyse des causes ainsi que des outils d’alerte sur ce service d’API de détection des anomalies.

détection d’anomalie Hello API est une solution efficace pour un large éventail de scénarios, tels que l’intégrité du service et les indicateurs de performance clés à surveiller, IoT, analyse des performances et la surveillance du trafic réseau. Voici quelques scénarios courants où cette API peut se révéler utile :
- Les services informatiques doivent événements tootrack des outils, code d’erreur, journal d’utilisation et les performances (UC, mémoire et ainsi de suite) en temps voulu.

-   Les sites de commerce en ligne que les activités du client tootrack, vues de page, clics et ainsi de suite.

-   Les sociétés utilitaire souhaitent tootrack la consommation d’eau, gaz, électricité et autres ressources.

-   Fonctionnalité/Création de services de gestion souhaitez toomonitor température, l’humidité, le trafic et ainsi de suite.

-   IoT/fabricants voulez des données de capteur de toouse dans temps série toomonitor le flux de travail, la qualité et ainsi de suite.

-   Fournisseurs de services, tels que les centres d’appel doivent tendance à la demande de service toomonitor, volume d’incidents, patienter longueur de file d’attente et ainsi de suite.

-   Des groupes professionnels analytique souhaitez toomonitor business des indicateurs de performance clés (par exemple, le volume des ventes, des éléments de client, tarification) mouvement anormal en temps réel.

### <a name="cloud-app-security"></a>Cloud App Security

[Cloud App Security](https://docs.microsoft.com/cloud-app-security/what-is-cloud-app-security) est un composant essentiel de la pile de Microsoft Cloud Security hello. Il est une solution complète qui peut aider votre organisation que vous déplacez tootake pleinement parti de la promesse hello des applications cloud, mais vous permettent de contrôler, via une meilleure visibilité dans l’activité. Cela vous permet également de renforcer la protection des hello de données critiques entre les applications cloud.

Avec des outils qui aident à découvrir le shadow IT, évaluer les risques, appliquer des stratégies, examiner les activités et arrêter des menaces, votre organisation peut déplacer en toute sécurité toohello cloud tout en conservant le contrôle de données critiques.

<table style="width:100%">
 <tr>
   <td>Découvrez</td>
   <td>Découvrez le Shadow IT grâce à Cloud App Security. Bénéficiez d’une meilleure visibilité grâce à une détection des applications, des activités, des utilisateurs, des données et des fichiers dans votre environnement cloud. Découvrir les applications tierces qui sont connectées tooyour cloud.</td>
 </tr>
 <tr>
   <td>Examiner</td>
   <td>Recherchez dans vos applications cloud à l’aide de cloud légales outils toodeep-présentation dans les fichiers dans votre réseau, les utilisateurs spécifiques et les applications présentant un risque. Rechercher des modèles dans les données de hello collectées à partir de votre cloud. Générer des rapports toomonitor votre cloud.</td>

 </tr>
 <tr>
   <td>Contrôle</td>
   <td>Atténuer les risques en définissant des stratégies et des alertes tooachieve un contrôle maximal sur le trafic cloud réseau. Utiliser Cloud App Security toomigrate votre toosafe les utilisateurs, les applications cloud approuvées alternatives.</td>

 </tr>
 <tr>
   <td>Protéger</td>
   <td>Utiliser Cloud App Security toosanction ou interdire les applications, appliquer la prévention des fuites de données, les autorisations de contrôle et de partage et générer des alertes et des rapports personnalisés.</td>

 </tr>
 <tr>
   <td>Contrôle</td>
   <td>Atténuer les risques en définissant des stratégies et des alertes tooachieve un contrôle maximal sur le trafic cloud réseau. Utiliser Cloud App Security toomigrate votre toosafe les utilisateurs, les applications cloud approuvées alternatives.</td>

 </tr>
</table>


![Cloud App Security](./media/azure-threat-detection/azure-threat-detection-fig14.png)

Cloud App Security intègre la visibilité à votre cloud :

-   À l’aide de Cloud Discovery toomap et identifier votre environnement cloud et hello applications cloud à l’aide de votre organisation.


-   en approuvant et en interdisant les applications dans votre cloud ;



-   en utilisant des connecteurs faciles à déployer qui tirent parti des API de fournisseurs pour améliorer la visibilité et la gouvernance des applications auxquelles vous vous connectez ;

-   en vous aidant à préserver le contrôle grâce à la définition et à l’optimisation de stratégies.

Sur la collecte des données à partir de ces sources, Cloud App Security exécute une analyse complexe sur les données de salutation. Il immédiatement vous avertit tooanomalous activités et vous donne une visibilité détaillée de votre environnement cloud. Vous pouvez configurer une stratégie de Cloud App Security et l’utiliser tooprotect tous les éléments de votre environnement cloud.

## <a name="third-party-atd-capabilities-through-azure-marketplace"></a>Fonctionnalités ATD tierces accessibles via la Place de marché Azure

### <a name="web-application-firewall"></a>Pare-feu d’applications web

Le pare-feu d’applications web inspecte le trafic web entrant et bloque les injections SQL, les attaques XSS, les téléchargements de programmes malveillants, les attaques DDoS, ainsi que les autres attaques ciblées sur vos applications web. Il examine également réponses hello à partir de serveurs web principal de hello pour Data Loss Prevention (DLP). moteur de contrôle d’accès intégré Hello permet des stratégies de contrôle d’accès granulaire aux administrateurs toocreate pour l’authentification et de l’autorisation (Remote), qui fournit une authentification forte organisations et contrôle utilisateur.

**Points forts :**
-   Détecte et bloque les injections SQL, les attaques XSS, les téléchargements de logiciels malveillants, les attaques DDoS d’application ou toute autre attaque dirigée contre votre application.

-   Authentification et contrôle d’accès.

-   Analyse des données sensibles du toodetect le trafic sortant et peuvent masquer ou bloquer des informations à partir de la fuite hello.

-   Accélère la remise hello du contenu d’application web, à l’aide des fonctionnalités telles que la mise en cache, la compression et autres optimisations de trafic.

Voici quelques exemples de pare-feu d’applications web disponibles sur la Place de marché Azure :

[Pare-feu d’applications Web Barracuda, Brocade virtuel pare-feu d’applications Web (Brocade vWAF), Imperva SecureSphere et hello ThreatSTOP IP pare-feu.](https://azure.microsoft.com/marketplace/partners/brocade_communications/brocade-virtual-web-application-firewall-templatevtmcluster/)

## <a name="next-steps"></a>Étapes suivantes

- [Fonctionnalités de détection d’Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities)

Fonctions de détection avancée du centre de sécurité Azure permet de tooidentify des menaces actives ciblant vos ressources Microsoft Azure et fournit des informations de hello requise toorespond rapidement.

- [Azure SQL Database Threat Detection](https://azure.microsoft.com/blog/azure-sql-database-threat-detection-your-built-in-security-expert/)

La détection des menaces de base de données SQL Azure a permis de résoudre leurs problèmes sur la base de données de tootheir les menaces potentielles.
