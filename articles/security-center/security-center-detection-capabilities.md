---
title: "fonctionnalités aaaDetection dans le centre de sécurité Azure | Documents Microsoft"
description: "Ce document vous aide à toounderstand fonctionnement des fonctionnalités de détection Azure Security Center."
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 4c5599cc-99a1-430f-895f-601615ef12a0
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: d8001cc2acdd0026bd9b3596bbdfec56f8874513
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-detection-capabilities"></a>Fonctionnalités de détection d’Azure Security Center
Ce document traite des fonctionnalités de détection avancée du centre de sécurité Azure qui permet d’identifier des menaces actives ciblant vos ressources Microsoft Azure et fournit que des informations de hello requise toorespond rapidement.

> [!NOTE]
> Détections avancées sont disponibles dans hello niveau Standard de Azure Security Center. Une version d’évaluation gratuite de 60 jours est disponible. Vous pouvez mettre à niveau hello sélection du niveau tarifaire Bonjour [stratégie de sécurité](security-center-policies.md). Visitez [page du centre de sécurité](https://azure.microsoft.com/pricing/details/security-center/) toolearn plus d’informations sur la tarification. 
> 
> 

## <a name="responding-tootodays-threats"></a>Les menaces de tootoday de réponse
Ont été apportées dans le paysage des menaces hello sur hello 20 dernières années. Bonjour passées, sociétés uniquement étaient tooworry sur la dégradation de site web par les pirates individuels qui ont été principalement intéressé voir « qu’ils ne pouvaient faire ». Les pirates d’aujourd’hui sont beaucoup plus sophistiqués et organisés. Ils ont souvent des objectifs financiers et stratégiques spécifiques. Ils ont également plus toothem disponible de ressources, car ils peuvent être perturbante par les États de pays ou de criminalité organisée.

Cette approche a conduit tooan inégalée professionnalisme rangs des intrus hello. Ces derniers ne s’intéressent plus à la dégradation de site web, Ils sont maintenant intéressé de vol d’informations, les comptes financiers et les données privées, tous dont ils peuvent utiliser toogenerate contre remboursement hello open market ou tooleverage un commercial particulier, la position politique ou militaire. Encore plus concernant que les intrus avec un objectif financier sont des personnes malveillantes hello qui enfreignent les personnes et les réseaux toodo tout effet nuisible tooinfrastructure.

En réponse, les organisations déploient souvent différentes solutions de point, ce qui vous concentrer sur la défense de périmètre de l’entreprise hello ou points de terminaison en recherchant des signatures d’attaques connues. Ces solutions ont tendance à toogenerate un grand nombre d’alertes de faible fidélité, qui nécessitent un tootriage analyste de sécurité et d’examiner. La plupart des organisations ne disposent pas de temps de hello et compétences requises toorespond toothese alertes : ainsi, plusieurs accédez unaddressed.  Pendant ce temps, des personnes malveillantes ont évolué toosubvert de leurs méthodes nombreuses défenses de signature et [adapter toocloud environnements](https://azure.microsoft.com/blog/detecting-threats-with-azure-security-center/). Nouvelles approches sont requis toomore rapidement identifier les nouvelles menaces et d’accélérer la détection et réponse. 

## <a name="how-azure-security-center-detects-and-responds-toothreats"></a>Comment Azure Security Center détecte et répond toothreats
Chercheurs en sécurité de Microsoft sont constamment sur lookout hello pour les menaces. Ils ont accès tooan vaste de télémétrie acquise à partir de la présence de Microsoft dans le cloud de hello et sur site. Cette collection de large et différents des jeux de données permet de Microsoft toodiscover nouveaux modèles et tendances sur ses produits en local de consommateur et d’entreprise, ainsi que ses services en ligne. Par conséquent, Azure Security Center peut rapidement mettre à jour ses algorithmes de détection, puisque les pirates sont à l’origine d’attaques innovantes de plus en plus sophistiquées. Cette approche permet de faire face à des menaces en pleine mutation. 

Détection des menaces de sécurité Center fonctionne en collectant automatiquement des informations de sécurité à partir de vos ressources Azure, hello réseau et les solutions de partenaire connecté. Il analyse cette information, corrélation souvent des informations provenant de plusieurs sources, les menaces tooidentify. Alertes de sécurité sont définies dans le centre de sécurité ainsi que des recommandations sur la tooremediate hello menace.

![Collecte et présentation des données dans Azure Security Center](./media/security-center-detection-capabilities/security-center-detection-capabilities-fig1.png)

Azure Security Center emploie des analyses de sécurité avancées allant bien au-delà des approches simplement basées sur la signature. Découvertes dans les données volumineuses et [apprentissage](https://azure.microsoft.com/blog/machine-learning-in-azure-security-center/) technologies sont optimisées tooevaluate événements entre l’infrastructure de cloud entière hello : détection des menaces qui seraient impossible tooidentify à l’aide des méthodes manuelles et de prédiction hello évolution d’attaques. Ces analyses de sécurité comprennent les éléments suivants : 

* **Intégré sur les menaces**: il semble pour connus mauvais acteurs, en tirant parti des menaces global à partir des produits et services, Microsoft hello Microsoft Digital Crimes unité (DCU), hello MSRC Microsoft Security Response Center () et est externe les flux.
* **Analytique comportementale**: applique le comportement de modèles connus toodiscover malveillant. 
* **Détection d’anomalie**: utilise statistiques de profilage toobuild une ligne de base historique. Il avertit sur des écarts par rapport à des lignes de base établies conformes vecteur d’attaque potentielle tooa.

### <a name="threat-intelligence"></a>Informations sur les menaces
Microsoft dispose d’une multitude d’informations en matière de menaces à l’échelle mondiale. Télémétrie transfère à partir de plusieurs sources, tels que Azure, Office 365, Microsoft CRM online, Microsoft Dynamics AX, outlook.com, MSN.com, hello Microsoft Digital Crimes unité (DCU) et MSRC Microsoft Security Response Center (). Chercheurs également informé threat intelligence qui est partagé entre les fournisseurs de services cloud principal et s’abonne toothreat intelligence flux provenant de tiers. Centre de sécurité Azure peut utiliser cette tooalert informations vous toothreats de connus mauvais acteurs. Voici quelques exemples :

* **Adresse IP malveillante de communications sortantes tooa**: tooa le trafic sortant connus botnet ou darknet probablement indique que votre ressource a été compromise et qu’une personne malveillante d’essayer tooexecute de commandes sur ces données système ou exfiltrate. Centre de sécurité Azure compare la base de données de menace global de tooMicrosoft de trafic réseau et vous avertit s’il détecte l’adresse IP malveillante de communication tooa.

## <a name="behavioral-analytics"></a>Analyse comportementale
Analytique comportementale est une technique qui analyse et compare la collecte des données tooa de modèles connus. Toutefois, ces modèles ne sont pas de simples signatures. Ils sont déterminés par les algorithmes d’apprentissage automatique complexes qui sont des jeux de données toomassive appliqué. Ils sont également déterminés à travers une analyse minutieuse des comportements malveillants par des experts. Centre de sécurité Azure peuvent utiliser des ressources de tooidentify compromis d’analytique comportementale basées sur l’analyse des journaux de l’ordinateur virtuel, des journaux de périphérique réseau virtuel, les journaux de l’ensemble fibre optique, vidages sur incident et d’autres sources. 

En outre, il est corrélation avec les autres toocheck signaux pour prendre en charge de la preuve d’une campagne généralisée. Cette corrélation permet tooidentify les événements qui sont cohérents avec les indicateurs établies de compromission. Voici quelques exemples :

* **L’exécution du processus suspects**: les attaquants utilisent plusieurs logiciels malveillants techniques tooexecute sans risque de détection. Par exemple, une personne malveillante peut donner contre les programmes malveillants hello même nom que les fichiers système légitimes mais placez ces fichiers dans un autre emplacement, utilisez un nom qui est très similaire tooa sans gravité ou l’extension de fichier du hello de masque true. Analyses et les comportements de processus de modèles de centre de sécurité traitent les valeurs hors norme d’exécutions toodetect telles que celles-ci.  
* **Masqué contre les programmes malveillants et l’exploitation des tentatives**: sophistiquées contre les programmes malveillants sont tooevade en mesure de logiciel anti-programme malveillant traditionnel produits par l’écriture toodisk jamais ou chiffrement des composants logiciels stockés sur le disque.  Toutefois, les logiciels malveillants peuvent être détectées à l’aide de l’analyse de mémoire, comme hello contre les programmes malveillants doivent conserver les traces en mémoire dans l’ordre toofunction. Lorsque le logiciel tombe en panne, un vidage sur incident capture une partie de la mémoire lors de pannes de hello hello.  En analysant la mémoire hello dans le vidage sur incident de hello, Azure Security Center peut détecter des techniques utilisées tooexploit vulnérabilités dans le logiciel, accéder aux données confidentielles et subrepticement conserver dans un ordinateur compromis sans affecter les performances de hello du votre ordinateur.
* **Latérale le déplacement et la reconnaissance interne**: toopersist dans une compromis réseau et localiser/récolte importantes de données, les attaquants tentent souvent toomove latéralement de hello compromis tooothers machine dans hello même réseau. Centre de sécurité surveille les processus et activités de connexion dans l’ordre toodiscover tente tooexpand brèche de la personne malveillante dans réseau hello, telles que la commande à distance d’exécution réseau détection et d’énumération de compte.
* **Les Scripts PowerShell malveillants**: PowerShell est utilisé par les pirates tooexecute du code malveillant sur les machines virtuelles cible pour à des fins diverses. Azure Security Center inspecte l’activité PowerShell à la recherche d’activité suspecte. 
* **Sortant attaques**: les attaquants ciblent souvent les ressources de cloud avec comme objectif hello à l’aide de ces attaques supplémentaires toomount de ressources. Compromis des machines virtuelles, par exemple, est peut-être utilisé toolaunch les attaques en force par rapport aux autres machines virtuelles, envoyer du courrier indésirable ou analyser les ports ouverts et autres appareils sur hello internet. En appliquant la machine learning toonetwork trafic, le centre de sécurité peut détecter lorsque les communications réseau sortant dépassent la norme hello. Dans les cas de hello de courrier indésirable, centre de sécurité également met en corrélation les e-mails inhabituel avec intelligence à partir d’Office 365 toodetermine si les messages hello sont susceptible de malveillant ou résultat hello d’une campagne e-mail légitime.  

### <a name="anomaly-detection"></a>Détection des anomalies
Centre de sécurité Azure utilise également les menaces de tooidentify de détection d’anomalies. Dans analytique de toobehavioral contraste (qui dépend des modèles connus dérivés de grands jeux de données), détection d’anomalie plus « personnalisée » et se concentre sur les lignes de base qui sont des déploiements de tooyour spécifique. Apprentissage automatique est appliqué toodetermine une activité normale pour vos déploiements et ensuite les règles sont les conditions d’observation ABERRANTE toodefine généré qui peut représenter un événement de sécurité. Voici un exemple :

* **Attaques par force brute RDP/SSH entrantes**: vos déploiements peuvent comporter des machines virtuelles occupées par un nombre plus ou moins important de connexions quotidiennes. Centre de sécurité Azure peut déterminer l’activité de connexion de base de ces ordinateurs virtuels et utiliser machine learning toodefine ce qui est en dehors de l’activité de connexion normale. Si nombre hello de connexions, ou de l’heure hello de connexions de hello, ou emplacement hello à partir de quels hello connexions sont demandées, ou d’autres caractéristiques associées à la connexion est considérablement différentes à partir de la ligne de base hello, une alerte peut être générée. Là encore, l’apprentissage automatique détermine ce qui est significatif.

## <a name="continuous-threat-intelligence-monitoring"></a>Analyse continue des informations sur les menaces
Centre de sécurité Azure fonctionne de recherche et données pour la science des équipes de sécurité qui en permanence surveillent les modifications apportées dans le paysage des menaces hello. Hello suivant initiatives sont les suivantes :

* **Analyse des informations sur les menaces**: les informations sur les menaces incluent des mécanismes, des indicateurs, des implications et des conseils pratiques sur les menaces, nouvelles ou existantes. Cette information est partagée dans la Communauté de la sécurité hello et Microsoft surveille en permanence threat intelligence des flux à partir de sources internes et externes.
* **Partage de signal**: les informations fournies par les équipes de sécurité sur le portefeuille complet de services cloud et locaux, de serveurs, et d’appareils de point de terminaison client de Microsoft sont partagées et analysées. 
* **Spécialistes de la sécurité Microsoft**: engagement continu avec les équipes Microsoft travaillant dans des domaines de la sécurité spécialisés, tels que la forensique et la détection d’attaques web.
* **Optimisation de la détection**: algorithmes sont exécutées sur des jeux de données des clients réels et chercheurs en sécurité fonctionnent avec les résultats de clients toovalidate hello. VRAI et faux positifs sont des algorithmes d’apprentissage toorefine utilisé.

Ces efforts combinées aboutissent à des détections nouvelle et améliorées, vous pouvez bénéficier d’instantanément : aucune action n’est pour vous tootake.

## <a name="see-also"></a>Voir aussi
Dans ce document, vous avez appris comment fonctionnent les fonctionnalités de détection du centre de sécurité tooAzure. toolearn en savoir plus sur le centre de sécurité, voir hello :

* [Guide des opérations et de planification du Centre de sécurité Azure](security-center-planning-and-operations-guide.md)
* [La gestion et de répondre toosecurity des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md)
* [Alertes de sécurité par type dans le centre de sécurité Azure](security-center-alerts-type.md)
* [Contrôle d’intégrité de la sécurité dans le centre de sécurité Azure](security-center-monitoring.md) — Découvrez comment toomonitor hello d’intégrité de vos ressources Azure.
* [Surveillance des solutions de partenaire avec Azure Security Center](security-center-partner-solutions.md) — Découvrez comment toomonitor hello état d’intégrité de vos solutions de partenaire.
* [Forum aux questions sur Azure Security Center](security-center-faq.md) : Forum aux questions sur l’utilisation hello service de recherche.
* [Blog sur la sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) : accédez à des billets de blog sur la sécurité et la conformité Azure.

