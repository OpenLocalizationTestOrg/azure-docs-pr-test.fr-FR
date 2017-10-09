---
title: "aaaCortana Intelligence Solution modèle manuel pour les prévisions de la demande d’énergie | Documents Microsoft"
description: "Un modèle de solution avec Microsoft Cortana Intelligence permettant de prévoir la demande en énergie d’une société de service public de distribution d’énergie."
services: cortana-analytics
documentationcenter: 
author: ilanr9
manager: ilanr9
editor: yijichen
ms.assetid: 8855dbb9-8543-45b9-b4c6-aa743a04d547
ms.service: cortana-analytics
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2016
ms.author: ilanr9;yijichen;garye
ms.openlocfilehash: 32fc6ece7e24ced34282baf107548039694a38b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="cortana-intelligence-solution-template-playbook-for-demand-forecasting-of-energy"></a>Manuel du modèle de solution Microsoft Cortana Intelligence de prévision de la demande d’énergie
## <a name="executive-summary"></a>Résumé
Bonjour dernières années, Internet of Things (IoT), les sources d’énergie alternatives et les données volumineuses ont fusionné opportunités de grande toocreate dans l’utilitaire de hello et le domaine de l’énergie. À hello simultanément, utilitaire de hello et secteur de l’énergie entière hello connaissent la consommation de la mise à plat avec les consommateurs en exigeant des meilleures méthodes toocontrol leur utilisation d’énergie. Par conséquent, hello utilitaire et grille active sociétés sont absolument besoin tooinnovate et renouvellement eux-mêmes. En outre, plusieurs grilles de puissance et l’utilitaire deviennent obsolète et très coûteux toomaintain et gérer. Au cours de hello année dernière, équipe de hello a travaillé sur un nombre de contrats dans le domaine de l’énergie hello. Pendant ces engagements, nous avons rencontré dans quel hello utilitaires ou des éditeurs de logiciels indépendants (éditeurs de logiciels indépendants) ont été recherche en prévision de la demande future énergétique de nombreux cas. Ces prévisions jouent un rôle important dans leur entreprise actuel et futurs et sont devenues foundation hello pour différents cas d’utilisation. parmi lesquelles les prévisions de charge à court et à long terme, les échanges et l’équilibrage des charges, l’optimisation des réseaux, etc. Big data et méthodes d’Analytique avancée (AA) telles que la Machine Learning (ML) sont déterminants hello pour produire des prévisions précises et fiables.  

Dans ce scénario, nous mis en place d’entreprise de hello et analytiques instructions nécessaires pour la réussite du développement et déploiement de la demande énergétique prédire la solution. Ces instructions peuvent aider les services publics, les spécialistes et les ingénieurs de données à mettre en place des solutions de prévision de la demande parfaitement opérationnelles basées sur le cloud. Pour les entreprises qui sont en cours de démarrage leurs données et le voyage d’analytique avancée, telle une solution peut représenter la valeur initiale hello dans leur stratégie à long terme de la grille active.

> [!TIP]
> toodownload un diagramme qui fournit une présentation de l’architecture de ce modèle, consultez [architecture des modèles de Solution d’Intelligence Cortana pour la prévision de la demande d’énergie](cortana-analytics-architecture-demand-forecasting-energy.md).  
> 
> 

## <a name="overview"></a>Vue d'ensemble
Ce document traite des aspects techniques de l’utilisation de Cortana Intelligence et en particulier Azure Machine Learning (LAM) pour le déploiement de Solutions de prévision d’énergie et de mise en œuvre hello, les données et business de hello. document de Hello se compose de trois parties principales :  

1. Présentation de l’entreprise  
2. Présentation des données  
3. Implémentation technique

Hello **compréhension commerciale** partie hello entreprise aspect un besoins toounderstand et envisagez toomaking préalable d’une décision d’investissement. Il explique comment tooqualify hello problème d’entreprise à tooensure main analytique prédictive et l’apprentissage sont réellement efficace et applicable. document Hello présente les notions de base de hello d’apprentissage automatique et comment il s’agit des problèmes de prévision d’énergie tooaddress utilisé. Elle décrit les conditions préalables de hello et les critères de qualification hello d’un cas d’usage. Certains exemples d’études de cas et scénarios pratiques sont également fournis.

Les données sont un composant principal de hello pour les solutions d’apprentissage. Hello **présentation des données** partie de ce document aborde certains aspects importants de données de salutation. Il décrit le type hello de données sont nécessaire pour la prévision de l’énergie, des exigences de qualité de données et quelles sources de données existent en général. Nous expliquons également comment les données brutes hello sont tooprepare utilisé les fonctionnalités de données réellement lecteur hello partie de modélisation.

Hello troisième partie de document de hello couvre hello **implémentation technique** aspect d’une solution. Ingénierie de fonctionnalité et de modélisation sont au cœur de hello du processus de science des données hello et sont donc présentées icis en détail. Elle couvre le concept hello de services web, qui sont un véhicule important pour le déploiement de solutions d’analytique prédictive cloud. Nous y décrivons également une architecture classique de solution de bout en bout opérationnelle.

En outre, hello comprend des documents de référence que vous pouvez utiliser toogain comprendre plus de technologie et de domaine de hello.

Il est important toonote que nous ne comptez pas toocover ce document hello plus approfondis processus de données scientifiques, ses aspects mathématiques et techniques. Vous trouverez ces détails dans la [documentation](http://azure.microsoft.com/services/machine-learning/) et les [blogs](http://blogs.microsoft.com/blog/tag/azure-machine-learning/) Azure ML.

### <a name="target-audience"></a>Public cible
public visé Hello pour ce document est de l’entreprise et du personnel technique qui souhaiteraient toogain connaissances et compréhension de l’apprentissage en fonction des solutions et comment elles sont utilisées spécifiquement dans le domaine de prévision d’énergie hello.

Les chercheurs de données peuvent également tirer parti de cette toogain document une meilleure compréhension du processus de niveau élevé hello que lecteurs hello déploiement d’une solution de prévision d’énergie. Dans ce contexte, il peut également être utilisé tooestablish une bonne ligne de base et le point de départ pour plus d’informations détaillées et Avancé de matériel.

### <a name="industry-trends"></a>Tendances du secteur
Bonjour dernières années, données big IoT et sources d’énergie alternatives ont fusionné des opportunités de grande toocreate dans l’utilitaire de hello et l’espace de l’énergie. À hello simultanément, utilitaire de hello et secteurs de l’énergie entière hello connaissent la consommation de la mise à plat avec les consommateurs en exigeant des meilleures méthodes toocontrol leur utilisation d’énergie.

Nombreux utilitaire et les sociétés d’énergie actives ont été novatrices de hello [grille smart](https://en.wikipedia.org/wiki/Smart_grid) en déployant un nombre d’utilisation de cas qui rendent à utiliser les données hello générées par la grille de hello. Plusieurs cas d’usage sont axés sur les particularités de hello de la production d’électricité : elle ne peut pas être accumulé ni stockée mis de côté en tant qu’inventaire. Par conséquent, ce qui est produit doit être utilisé. Utilitaires de choix toobecome plus efficace doivent tooforecast consommation simplement parce que vous obtiendrez ainsi une capacité supérieure trop**équilibrer l’offre et la demande**, afin d’éviter les pertes d’énergie, **réduire greenhouse émission de gaz**et contrôler les coûts.

En matière de coûts, un autre aspect est important, celui du prix. Nouvelle alimentation tootrade de capacités entre utilitaires a amené une absolument besoin trop**de prévision de la demande future et prix futur d’électricité**. Les sociétés peuvent ainsi déterminer leurs volumes de production.

Quand vous utilisez word hello 'active', nous nous référons réellement grille tooa qui peut en savoir plus et effectuer des prévisions. Il peut anticiper des variations saisonnières de la consommation, **prévoir les situations de surcharge temporaire et faire des ajustements automatiques**. Par le contrôle à distance de la consommation (à l’aide de hello ces compteurs actives), les situations de surcharge localisée peuvent être gérées. **Par tout d’abord la prédiction et d’agir**, grille de hello devient plus intelligente au fil du temps.

Pour rest hello de ce document, nous allons nous concentrer sur une famille spécifique de cas d’usage qui couvrent les prévisions de futures, à court terme et à long terme à la demande de l’énergie. Nous travaillent dans ces domaines pendant quelques mois et acquis des connaissances et les capacités qui nous permettent de résultats de niveau tooproduce secteur. Autres cas d’utilisation seront abordées ainsi document hello Bonjour futur proche.

## <a name="business-understanding"></a>Présentation de l’entreprise
### <a name="business-goals"></a>Objectifs de l’entreprise
Hello **énergie démonstration** vise toodemonstrate un classique analytique prédictive et l’apprentissage de solution qui peut être déployée dans un laps de temps très court. Nous nous concentrons plus particulièrement sur l’activation de solutions de prévision de la demande d’énergie, et sa valeur peut donc être rapidement réalisée et exploitée par l’entreprise. informations Hello dans ce manuel peuvent aider à client hello accomplir hello suivant objectifs :

* Solution basée sur des toovalue d’heure courte de l’apprentissage
* Capacité tooexpand un tooother cas pilote cas d’usage ou tooa une portée plus large selon ses besoins d’entreprise
* Maîtrise rapide du produit Cortana Intelligence Suite

Avec ces objectifs à l’esprit, ce manuel a pour but de proposer une entreprise de hello et des connaissances techniques qui va vous aider à atteindre ces objectifs.

### <a name="power-load-and-demand-forecasting"></a>Prévision de charge et de demande d’électricité
Secteur de l’énergie hello, peuvent être des nombreuses façons dans la demande de prévision peut aider à résoudre des problèmes critiques. En fait, la demande de prévision peut être considéré comme foundation hello pour plusieurs cas d’utilisation de base dans l’industrie de hello. En règle générale, nous envisageons deux types de prévisions de la demande d’énergie : à court terme et à long terme. Chacun d’eux peut répondre à un objectif distinct et donc, utiliser une approche différente. Hello principale différence hello deux est hello horizon, ce qui signifie que hello plage horaire dans hello future pour laquelle nous serait prévisions de prévision.

#### <a name="short-term-load-forecasting"></a>Prévisions de charge à court terme
Dans le contexte de hello de demande d’énergie, court terme de charge de prévision (STLF) est défini en tant que charge agrégées hello qui est prévue dans hello proche avenir sur différentes parties de la grille de hello (ou grille hello entière). Dans ce contexte, à court terme est la période toobe défini au sein de la plage hello d’heures too24 de 1 heure. Dans certains cas, il peut s’agir d’un horizon à 48 heures. Par conséquent, STLF est très courant dans un cas d’usage opérationnelle de la grille de hello. Voici quelques exemples de cas d’utilisation avec le paramètre STLF :

* Équilibrage de l’offre et de la demande
* Prise en charge des échanges énergétiques
* Établissement du marché (prix de l’électricité)
* Optimisation opérationnelle du réseau
* [Réponse à la demande](https://en.wikipedia.org/wiki/Demand_response)
* Prévisions de pic de demande
* Gestion côté demande
* Équilibrage de charge et prévention des surcharges
* Prévision de charge à long terme
* Détection des anomalies et des défaillances
* Limitation/nivellement des pics 

STLF modèle sont principalement basé sur hello près au-delà (dernier jour ou semaine) les données de consommation et l’utilisation de température comme un PRÉDICTEUR important a prévu. Obtention de température précis de prévision pour hello prochaine heure et les heures de too24 devenant moins compliqué jours de maintenant. Ces modèles sont moins sensibles tooseasonal modèles ou les tendances de consommation à long terme.

SLTF solutions sont également susceptibles de toogenerate volume élevé d’appels de prédiction (demandes de service), car elles sont appelées sur une base horaire et dans certains cas même avec une fréquence plus élevée. Il est également très courant toosee implantation, où chaque sous-centrale individuel ou un transformateur est représentée comme un modèle autonome et par conséquent le volume hello de requêtes de prédiction sont accrues.

#### <a name="long-term-load-forecasting"></a>Prévision de charge à long terme
Hello de Long terme de charge de prévision (LTLF) vise à la demande de puissance tooforecast avec une période qu’il s’agisse des mois toomultiple de 1 semaine (et dans certains cas pour un nombre d’années). Cet horizon temporel est plus souvent applicable à des études de cas destinées à la planification et l’investissement.

Pour les scénarios à long terme, ce sont des données de haute qualité toohave important qui couvre une période de plusieurs années (minimum 3 ans). Ces modèles seront généralement extraire des modèles de caractère saisonnier des données historiques de hello et utiliser des predicators externes tels que les modèles météo et climat.

Il est important tooclarify qui hello hello plu horizon de prévision, hello moins précis hello prévision peut être. Il est donc important tooproduce que certains intervalles de confiance avec hello réelle de prévision qui permettrait l’homme variante possible de toofactor hello dans leurs processus de planification.

Étant donné que le scénario de consommation hello pour LTLF est principalement planification, il est possible de volumes de prédiction inférieure (en tant que tooSTLF comparé). Nous devriez généralement constater ces prédictions incorporées dans les outils de visualisation tels qu’Excel ou Power BI et appelés manuellement par l’utilisateur de hello.

### <a name="short-term-vs-long-term-prediction"></a>Prévision à court terme contre prévision à long terme
Hello tableau suivant compare STLF et LTLF dans les attributs les plus importants en ce qui concerne toohello :

| Attribut | Prévision de charge à court terme | Prévision de charge à long terme |
| --- | --- | --- |
| Période de prévision |Heures de too48 1 heure |À partir de 1 too6 mois ou plus |
| Granularité des données |Toutes les heures |Toutes les heures ou chaque jour |
| Études de cas classiques |<ul><li>Équilibrage de la demande/offre</li><li>Prévision des heures de prélèvement</li><li>Réponse à la demande</li></ul> |<ul><li>Planification à long terme</li><li>Planification des ressources réseau</li><li>Planification des ressources</li></ul> |
| Prévisions classiques |<ul><li>Jour ou semaine</li><li>Heure</li><li>Température toutes les heures</li></ul> |<ul><li>Mois</li><li>Jour</li><li>Température et climat à long terme</li></ul> |
| Plage de données historiques |Deux toothree années de données |Cinq too10 années de données |
| Précision classique |MAPE* de 5 % ou moins |MAPE* de 25 % ou moins |
| Fréquence de prévision |Générée toutes les heures ou toutes les 24 heures |Générée tous les mois, tous les trimestres ou tous les ans |

\*[MAPE](https://en.wikipedia.org/wiki/Mean_absolute_percentage_error) : erreur moyenne en pourcentage

Peuvent être consultés à partir de cette table, il est très important toodistinguish entre hello court et à long terme hello prévision des scénarios comme ces représentent différents besoins professionnels et peuvent avoir différents déploiement et consommation.

### <a name="example-use-case-1-esmart-systems--overload-optimization"></a>Exemple d’étude de cas 1 : systèmes eSmart, optimisation de surcharge
Un rôle important d’un [grille smart](https://en.wikipedia.org/wiki/Smart_grid) est toodynamically constamment optimiser et ajuster pourquoi la modification des modèles de consommation. La consommation d’énergie peut être affectée par les modifications à court terme provoquées principalement par les fluctuations de température (*par exemple*, lorsque davantage d’électricité est utilisée pour l’air conditionné ou le chauffage). AT hello même la consommation de temps, l’alimentation électrique est également influencée par les tendances à long terme. Ces dernières peuvent inclure les effets de saisonnalité, les jours fériés, la croissance à long terme de la consommation et même des facteurs économiques tels que l’indice des prix, le prix du pétrole et le produit intérieur brut.

Dans ce cas de figure, [eSmart](http://www.esmartsystems.com/) souhaitiez solution toodeploy basée sur un cloud qui permet de prédire tendance hello d’une situation de surcharge sur n’importe quel sous-centrale donné de la grille de hello. En particulier, eSmart souhaitait sous-stations tooidentify qui sont susceptibles de toooverload dans hello prochaine heure, par conséquent, une action immédiate pourraient être prises tooavoid ou résoudre cette situation.

Une prévision exacte et rapide nécessite la mise en œuvre de trois modèles prédictifs :

* Durée pendant laquelle le modèle terme que permet de prévision de consommation d’énergie sur chaque sous-centrale pendant hello peu suivant semaines ou mois
* Modèle à court terme qui permet de prédiction de la situation de surcharge sur une sous-station donnée pendant hello prochaine heure
* Un modèle de température offrant des prévisions de la température future dans plusieurs scénarios

objectif de Hello du modèle à long terme de hello est sous-stations de hello toorank par leur toooverload tendance (étant donné les capacités de transmission de puissance) hello semaine suivante ou le mois. Cela permet la création d’une liste courte des sous-stations pourra desservir comme entrée pour la prédiction à court terme de hello hello. Comme la température est un PRÉDICTEUR important pour le modèle à long terme de hello, il existe une température de scénario multi besoin tooconstantly produit prédit et les flux en tant qu’entrée dans le modèle de toohello à long terme. à court terme la Hello prévision est ensuite appelée toopredict le sous-centrale est probablement toooverload sur hello prochaine heure.

les modèles à court terme et à long terme Hello déployés individuellement par chaque sous-centrale. Par conséquent, l’exécution de pratique d’hello de ces modèles requiert une orchestration complète. dédié pour chaque heure de la journée de hello toogain une meilleure précision de prédiction dans hello à court terme, un modèle plus précis. Tous ces modèles sont exécutées toutes les heures et de fin d’exécution dans toorespond de temps suffisant tooallow de quelques minutes et prennent des mesures préventives si nécessaire. Cette collection de modèles est mises à jour par un recyclage périodique à l’aide des données les plus récentes de hello.

Vous trouverez d’autres informations sur ce cas d’utilisation [ici](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18945).

#### <a name="use-case-qualification-criteria--prerequisites"></a>Critères de qualification pour l’étude de cas : conditions préalables
Hello principal atout Cortana Intelligence est dans sa capacité puissant toodeploy et l’échelle machine learning centré sur les solutions. Il est conçu toosupport des milliers de prédictions qui sont exécutées simultanément. Il peut s’agrandir automatiquement toomeet un modèle de consommation de modification. Un des aspects principaux de la solution réside dans la précision et dans les performances de calcul. Par exemple, une société est intéressée de production à la demande de l’énergie précis de prévision pour hello prochaine heure et pour chaque heure de la journée de hello. Sur hello autre part, nous intéresse moins hello question Pourquoi à la demande hello est prédite toobe car il s’agit de répondre (modèle hello lui-même s’occupe de qui).

Il est donc important toorealize pas tous les cas d’usage et les problèmes de l’entreprise peuvent être résolus efficacement à l’aide d’apprentissage.

Cortana Intelligence et l’apprentissage peut être très efficaces pour résoudre un problème d’entreprise donné lorsque hello suivant des critères est remplie :

* Bonjour problème professionnel dans main est **prédictive** par nature. Un exemple de cas d’utilisation prédictive est une société qui souhaitez toopredict charge sur une sous-station donnée pendant hello prochaine heure. Sur hello autre part, d’analyse et de classement des pilotes de la demande historique serait **descriptif** par nature et par conséquent moins applicable.
* Il existe un clear **chemin d’accès de l’action** toobe effectuée une seule fois prédiction de hello est disponible. Par exemple, la prédiction d’une surcharge sur une sous-station pendant hello prochaine heure peut déclencher une action proactive de réduire la charge associée à ce sous-centrale et afin d’éviter une surcharge potentiellement.
* cas d’usage Hello représente un **type classique du problème** telles que lorsque résolu il peut préparer hello moyen toosolving autres cas d’utilisation similaires.
* client de Hello peut définir **objectifs quantitatives et qualitatives** toodemonstrate une implémentation d’une solution réussie. Par exemple, un objectif quantitatif pour la prévision de la demande d’énergie serait le seuil de précision requis de hello (*, par exemple*, des too5 %Error est autorisé) ou lors de la surcharge de sous-centrale puis la précision de hello (taux de vrais positifs) et rappel (étendue de vrais positifs) doit être au-dessus d’un seuil donné. Ces objectifs doivent être dérivées d’objectifs du client hello.
* Il existe un clear **scénario d’intégration** avec flux de travail de l’entreprise hello entreprise. Par exemple, hello sous-centrale charge prévision peut être intégrée dans hello grille contrôle tooallow surcharge de protection contre les activités du centre.
* client de Hello a toouse prêt **données avec une qualité suffisante** toosupport hello cas d’usage (voir plus d’informations dans la section suivante de hello, **de qualité des données**, de ce document).
* Hello client mortelles cloud données centrées sur l’architecture ou **apprentissage nuage**, y compris Azure ML et autres composants Cortana Intelligence Suite.
* client de Hello est disposé tooestablish **un flux de données fin tooend** que hello de livraison de données en nuage hello en continu et est prêt trop**opérationnaliser** hello solution.
* client de Hello est prêt trop**dédier les ressources** qui sera être activement au cours de la mise en œuvre pilote hello initial afin que la base de connaissances et de la propriété de la solution de hello peuvent être transférées toohello du client réussie Saisie semi-automatique.
* Hello client ressource doit être un **professionnel de données et les dons**, de préférence un chercheur de données.

Qualification d’un cas d’usage en fonction de hello critères ci-dessus peut considérablement améliorer le taux de réussite hello d’un cas d’usage et établir une bonne beachhead pour l’implémentation de hello de cas d’une utilisation ultérieure.

### <a name="cloud-based-solutions"></a>Solutions cloud
Cortana Intelligence Suite sur Azure est un environnement intégré qui réside dans le cloud de hello. déploiement Hello d’une solution d’analytique avancée dans un environnement cloud conserve des avantages substantiels pour les entreprises et à hello même temps peut signifier une modification importante pour les entreprises que toujours utiliser locaux solutions informatiques. Dans le domaine de l’énergie hello, il existe une tendance effacer de la migration progressive des opérations dans le cloud de hello. Cette tendance va de pair avec développement hello de grille active de hello comme indiqué ci-dessus, en **des tendances du secteur**. Ce manuel porte sur une solution basée sur le cloud dans le domaine de l’énergie hello, il est avantages de hello tooexplain important et d’autres considérations de déploiement d’une solution basée sur le cloud.

Hello plus grand avantage d’une solution basée sur le cloud est peut-être hello coût. Lorsqu’une solution utilise des composants déployés dans le cloud, il n’y a pas de frais initiaux ou de frais liés au coût des marchandises vendues. Cela signifie qu’il n’existe aucun tooinvest besoin de matériel, logiciels et la maintenance de l’informatique, et par conséquent, il existe une réduction significative de risques pour l’entreprise.

Un autre avantage important est la structure de coût de paiement à l’utilisation de hello des solutions basées sur le cloud. Des serveurs basés sur le cloud servant au calcul ou au stockage peuvent être déployés et mis à l’échelle en fonction des besoins Cela représente hello parti de l’efficacité du coût d’une solution basée sur le cloud.

Enfin, il n’est pas nécessaire pour l’acquisition de maintenance informatique ou le développement de l’infrastructure de futures que tout cela fait partie de l’offre de nuage hello. mesure toothat, Cortana Intelligence Suite comprend mieux hello dans les services de la classe et ses carte routière conserve en constante évolution. De nouvelles fonctionnalités, composants et capacités sont constamment présentés et ils évoluent.

Pour une société qui est en cours de démarrage sa transition à nuage de hello, hautement recommandons-nous tootake une approche progressive en implémentant un plan de migration de cloud. Nous pensons que pour les utilitaires et les sociétés dans le domaine de l’énergie hello, cas d’usage hello qui sont abordées dans ce manuel représentent une excellente opportunité pour pilotage du solutions prédictive analytique dans le cloud de hello.

#### <a name="business-case-justification-considerations"></a>Considérations relatives à la justification des études de cas
Dans de nombreux cas, le client de hello peut être intéressé par apporter une justification pour un cas d’usage donné dans lequel une solution basée sur le cloud et l’apprentissage sont des composants importants. Contrairement à une solution sur site, dans les cas de hello d’une solution basée sur le cloud, composant du coût initial hello est minime, et la plupart des éléments de coût hello est associée à l’utilisation réelle. Lorsqu’il s’agit toodeploying une solution sur Cortana Intelligence Suite de prévision d’énergie, plusieurs services peuvent être intégrés avec une structure de coût commune unique. Par exemple, les bases de données (*, par exemple*, SQL Azure) peuvent être utilisés toostore hello des données brutes et puis pour hello réel prévisions Azure ML est utilisé toohost hello prévoir des services. Dans cet exemple, hello coût structure peut inclure des composants transactionnels et stockage.

Sur hello autre part, un doit avoir une bonne compréhension de la valeur commerciale de hello de fonctionnement d’une demande d’énergie de prévision (ou à long terme). En fait, il est profit toorealize important hello de chaque opération de prévision. Par exemple, précisément prévision charge hello pour les prochaines 24 heures peut empêcher surproduction ou peut permettre d’éviter les surcharges de la grille de hello et cela peut être quantifié en termes d’économies sur une base quotidienne.

La formule de base pour le calcul des gains de hello de la demande de prévision solution serait : ![solution de prévision de la formule de base pour le calcul des gains de hello de la demande](media/cortana-analytics-playbook-demand-forecasting-energy/financial-benefit-formula.png)

Cortana Intelligence Suite fournit un modèle de tarification de paiement à l’utilisation, il est inutile de subir une formule toothis du composant coût fixe. Cette formule peut être calculée sur une base quotidienne, mensuelle ou annuelle.

Vous trouverez les tarifs de Cortana Intelligence Suite et Azure ML [ici](http://azure.microsoft.com/pricing/details/machine-learning/).

### <a name="solution-development-process"></a>Processus de développement de solution
cycle de développement Hello d’une demande d’énergie prévision solution implique généralement 4 phases, dans laquelle toutes les nous faisons utilisent des technologies de nuage et services au sein de hello Cortana Intelligence Suite.

Hello suivant le diagramme illustre ce concept :

![Cycle de réseau intelligent](media/cortana-analytics-playbook-demand-forecasting-energy/smart-grid-cycle.png)

Hello paragraphe suivant décrit ce processus de le 4 étape :

1. **Collecte des données** : toute solution d’analyse avancée repose sur des données (voir **Présentation des données**). Plus précisément, lorsqu’il s’agit de toopredictive analytique et les prévisions, nous s’appuient sur un flux continu et dynamique de données. Dans les cas de hello de la prévision de la demande de l’énergie, ces données peuvent provenir directement actives mètres ou être déjà agrégées sur une base de données locale. Nous utilisons également d’autres sources de données externes, notamment pour la météo et la température. Ce flux de données continu doit être orchestré, planifié et stocké. [Azure Data Factory](http://azure.microsoft.com/services/data-factory/) (ADF) est le principal moteur pour accomplir cette tâche.
2. **Modélisation** : pour les prévisions de l’énergie précis et fiable, un doit développer (train) et mettre à jour un modèle très qu’utiliser hello des données d’historique et extraits hello explicite et des modèles prédictifs dans hello des données. zone de Hello de Machine Learning (ML) a augmenté avec des algorithmes plus avancés en cours de développement régulièrement. Azure ML Studio fournit une expérience utilisateur satisfaisante qui permet d’utiliser les algorithmes ML dans un flux de travail d’exécution les plus avancés de hello. Ce flux de travail est illustrée dans un diagramme de flux intuitif et inclut la préparation des données hello, extraction de fonctionnalité, la modélisation et évaluation du modèle. utilisateur de Hello peut extraire des centaines de différents modèles qui sont inclus dans cet environnement. En fin de hello de cette phase, un chercheur de données aura un modèle de travail est complètement évalué et prêt pour le déploiement.
   
   Hello suivant schéma est une illustration d’un flux de travail classique :
   
   ![Workflow de modélisation](media/cortana-analytics-playbook-demand-forecasting-energy/modeling-workflow.png)
3. **Déploiement** : avec un modèle de travail en cours, étape suivante de hello est le déploiement. Ici, le modèle de hello est converti en un service web qui expose une API RESTful qui peuvent être appelés simultanément sur hello Internet à partir de différents clients de la consommation. Azure ML fournit un moyen simple de déploiement d’un modèle directement à partir de hello Azure ML Studio avec un seul clic d’un bouton. processus de déploiement complet de Hello se produit dans les coulisses de hello. Cette solution peut automatiquement mettre à l’échelle la consommation toomeet hello requis.
4. **Consommation** – dans cette phase, nous faisons en utiliser de hello tooproduce prédictions du modèle de prévision. consommation de Hello peut être pilotée à partir d’une application utilisateur (*, par exemple*, tableau de bord) ou directement à partir d’un système opérationnel, telles que la demande/approvisionnement équilibrage système ou une solution d’optimisation de grille. Plusieurs études de cas peuvent être pilotées depuis un modèle unique.

## <a name="data-understanding"></a>Présentation des données
Une fois les règles d’entreprise hello (consultez **compréhension commerciale**) d’une demande d’énergie prévision de solution, nous sommes maintenant prêt toodiscuss hello partie des données. La solution d’analyse prédictive se fonde sur des données fiables. Pour la prévision de demande d’énergie, nous nous reposons sur les données d’historique avec plusieurs niveaux de granularité. Que les données d’historique sont utilisées en tant que matière hello. Elle sera subir une analyse approfondie dans le hello chercheur de données identifie PRÉDICTEURS (également les fonctionnalités tooas visés) qui peuvent être placées dans un modèle qui génère les prévisions hello requis par la suite.

Dans le reste de hello de cette section, nous allons examiner hello différentes étapes et les considérations relatives à la présentation des données de hello et comment toobring il utilisable tooa.

### <a name="hello-model-development-cycle"></a>Hello Cycle de développement du modèle
La création de modèles de prévisions adéquats nécessite une préparation et une planification minutieuses. Décomposer hello modélisation des processus en plusieurs étapes et en mettant l’accent sur une seule étape à la fois peut améliorer considérablement le résultat hello d’ensemble du processus hello.

Hello diagramme suivant illustre comment les processus de modélisation de hello peut être divisé en plusieurs étapes :

![Cycle de développement de modèle](media/cortana-analytics-playbook-demand-forecasting-energy/model-development-cycle.png)

En tant que peuvent être consultés hello cycle comprend six étapes :

* Formulation du problème
* Ingestion des données et exploration des données
* Préparation des données et ingénierie des fonctionnalités
* Modélisation
* Évaluation de modèle
* Développement

Dans le reste de hello de cette section, nous allons examiner les étapes individuelles hello et tooconsider d’éléments à chaque étape.

### <a name="problem-formulation"></a>Formulation du problème
Nous pouvons envisager la formulation de problème hello en hello étape la plus importante un des besoins tooimplementing préalable de tootake une solution prédictive analytique. Ici, nous transforment hello problème d’entreprise et de décomposer les éléments toospecific qui peuvent être résolus à l’aide des données et de techniques de modélisation. Il s’agit d’un problème de hello tooformulate bonnes pratiques comme un ensemble de questions, nous aimerions tooanswer. Voici quelques questions possibles qui peuvent s’applique au sein de la portée hello de la prévision de la demande de l’énergie :

* Quelle est la charge hello attendu sur une sous-station individuelle Bonjour prochaine heure ou chaque jour ?
* À quelle heure du jour de hello ma grille est confrontés à la demande ?
* Quelle est la probabilité mon grille toosustain hello attendu pics de charge ?
* La quantité d’énergie hello power station doit générer pendant chaque heure du jour de hello ?

Formulation de ces questions, nous permet de toofocus sur l’obtention de données de droite hello et l’implémentation d’une solution est pleinement alignée avec hello problème de gestion. En outre, nous pouvons définir certaines métriques clés qui nous permettent de performances de hello tooevaluate du modèle de hello. Par exemple, le niveau de précision hello prévision doit être et quelle est la plage de hello d’erreur qui serait acceptable par les entreprises de hello ?

### <a name="data-sources"></a>Sources de données
grille de smart moderne Hello collecte les données à partir de différentes parties et les composants de grille de hello. Ces données représentent les différents aspects de l’opération de hello et utilisation hello de grille d’alimentation hello. Étendue hello de prévision de la demande d’énergie hello, nous limitons discussion hello sur des sources de données qui reflètent la consommation de la demande réelle hello. Les capteurs intelligents sont une source importante de consommation d’énergie. Utilitaires du monde hello déploient rapidement mètres actives pour leurs clients. Mètres actives enregistrent la consommation énergétique réelles hello et de relais en permanence cette société données toohello précédent. Données sont collectées et envoyées à un intervalle fixe, allant de toutes les heures too1 5 minutes. Compteurs actives plus avancées peuvent être programmées à distance toocontrol et solde hello réel de la consommation au sein d’une famille. Les données de compteurs intelligents sont relativement fiables et incluent un horodatage. Cela en fait un ingrédient important pour la prévision de la demande. Les données de compteur peuvent être agrégées (totalisées) à différents niveaux au sein de la topologie de grille hello : transformer, sous-centrale, région, *etc.*. Nous pouvons ensuite choisir toobuild de niveau d’agrégation hello requis un modèle de prévision pour celle-ci. Par exemple, si la société hello comme tooforecast future charge sur chacun de ses sous-stations grille puis données ensemble des compteurs peuvent être agrégées pour chaque sous-centrale individuel et utilisées comme entrée pour hello prévision de modèle. Nous appelons toosmart mètres à l’aide d’une source de données interne.

Une prévision de la demande d’énergie fiable dépend également d’autres sources de données externes. Un facteur important qui affecte la consommation d’énergie est la météo hello, ou plus précisément les température hello. Les données historiques montrent un lien étroit entre la température externe et la consommation d’électricité. Lors des jours d’été à chaud, rendre les consommateurs utilisent de leurs climatiseurs et lors du démarrage hiver hello chauffage. Une source fiable de températures historique à l’emplacement de grille hello est par conséquent de clé. De plus, nous nous reposons aussi sur des prévisions précises de température comme élément de prévision de la consommation électrique.

Il existe d’autres sources de données permettant de créer des modèles de prévision de la demande d’énergie. Parmi elles se trouvent les modifications climatiques à long terme et certains indices économiques (*par exemple*, produit intérieur brut) entre autres. Dans ce document, nous n’incluons pas les autres sources de données.

### <a name="data-structure"></a>Structure des données
Après que l’identification hello requis à des sources de données, nous serait comme tooensure que les données brutes qui ont été collectées incluent hello corriger des fonctionnalités de données. modèle de prévision toobuild une demande fiable, nous avons besoin tooensure qui hello les données collectées inclut les éléments de données qui peuvent aider à prévoir hello future de la demande. Voici certaines exigences de base concernant la structure de données hello (schéma) de données brutes de hello.

les données brutes Hello se comprennent de lignes et de colonnes. Chaque mesure est représentée comme une seule ligne de données. Chaque ligne de données contient plusieurs colonnes (également des fonctionnalités tooas référencé ou champs).

1. **Horodatage** : champ d’horodatage hello représente l’heure réelle de hello lorsque la mesure de hello a été enregistrée. Il doit respecter un des formats de date/heure courantes hello. Les parties Date et Heure doivent être incluses. Dans la plupart des cas, il n’est pas nécessaire pour les enregistrements de hello temps toobe jusqu’au deuxième niveau de granularité de hello. Il est important toospecify hello horaire dans lequel sont enregistrées les données de salutation.
2. **Contrôler les ID** -ce champ identifie le compteur de hello ou un périphérique de mesure hello. Il s’agit d’une variable catégorique, qui peut se présenter sous forme de combinaison de chiffres et de caractères.
3. **Valeur de la consommation** – il s’agit consommation réelle de hello à une date/heure donnée. consommation de Hello peut être mesurée en kWh (kilowatt-hour) ou tout autre préféré unités. Il est important de toonote qui hello unité de mesure doit maintenir une cohérence entre toutes les mesures dans les données de salutation. Dans certains cas, la consommation peut être fournie sur 3 phases de l’alimentation. Dans ce cas nous doit toocollect toutes les phases de la consommation indépendants hello.
4. **Température** – température de hello généralement collecté à partir d’une source indépendante. Toutefois, il doit être compatible avec les données de consommation hello. Il doit inclure un horodatage comme décrit ci-dessus qui lui permettront de toobe synchronisé avec les données de consommation réelle hello. valeur de la température Hello peut être spécifié en degrés Celsius ou Fahrenheit mais doit maintenir une cohérence entre toutes les mesures.
5. **Emplacement –** champ d’emplacement hello est généralement associé à la place de hello où les données de température hello ont été collectées. Il peut être représenté sous forme de code postal ou au format latitude/longitude (lat/long).

Hello les tableaux suivants montre des exemples d’un format de données de consommation de température bon :

| **Date** | **Time** | **ID du compteur** | **Phase 1** | **Phase 2** | **Phase 3** |
| --- | --- | --- | --- | --- | --- |
| 7/1/2015 |10:00:00 |ABC1234 |7.0 |2.1 |5.3 |
| 7/1/2015 |10:00:01 |ABC1234 |7.1 |2.2 |4.3 |
| 7/1/2015 |10:00:02 |ABC1234 |6.0 |2.1 |4.0 |

| **Date** | **Time** | **Emplacement** | **Température** |
| --- | --- | --- | --- |
| 7/1/2015 |10:00:00 |11242 |24,4 |
| 7/1/2015 |10:00:01 |11242 |24,4 |
| 7/1/2015 |10:00:02 |11242 |24,5 |

Comme illustré ci-dessus, cet exemple inclut 3 valeurs de la consommation associées à 3 phases d’alimentation différentes. Notez également que les champs de date et heure hello sont séparés, toutefois ils peuvent aussi être combinés en une seule colonne. Dans ce cas hello emplacement est représentée dans un format de code postal de 5 chiffres et de la température hello dans un format degrés Celsius.

### <a name="data-format"></a>Format de données
Cortana Intelligence Suite peut prendre en charge les formats de données les plus courants hello tels que CSV, TSV, JSON, *etc.*. Il est important de que ce format de données hello reste cohérent pour hello cycle de vie du projet de hello.

### <a name="data-ingestion"></a>Ingestion de données
Étant donné que la prévision de la demande d’énergie est constamment et fréquemment prédit, nous devons nous assurer que les données brutes hello sont transmis au moyen d’un processus d’acquisition de données solide et fiable. processus d’acquisition Hello doit garantir que les données brutes hello soient disponibles pour hello prévision des processus au moment de hello requis. Cela implique que fréquence de réception de données hello doit être supérieure à hello fréquence de prévision.

Par exemple : Si notre demande prévision solution susceptible de générer une prévision à 8 h 00 chaque jour, puis nous devons tooensure qui ont été collectées au cours de toutes les données hello hello dernière 24 heures a été entièrement ingéré jusqu'à ce point et a tooeven inclure hello dernière heure de données.

Dans commande tooaccomplish, Cortana Intelligence Suite offre divers moyens toosupport un processus d’acquisition de données fiable. Cette méthode est expliquée plus Bonjour **déploiement** section de ce document.

### <a name="data-quality"></a>Qualité des données
source de données brutes de Hello est obligatoire pour effectuer une prévision de la demande fiable et précise doit satisfaire à certains critères de qualité des données de base. Bien que des méthodes statistiques avancées peuvent être toocompensate utilisé pour un problème de qualité des données, nous devons encore tooensure que nous sommes dépasser un seuil de qualité des données de base lors de la réception de nouvelles données. Voici quelques considérations au sujet de qualité de données brutes :

* **Valeur manquante** – cela fait référence toohello situation lors de la mesure spécifique n’a pas été collecté. condition de base Hello ici est que hello pas de valeur taux ne doit pas comporter plu de 10 % pour une période donnée. Dans les cas où une valeur manque, cela doit être indiqué à l’aide d’une valeur prédéfinie (par exemple : « 9999 ») et non pas « 0 », qui peut être une mesure valide.
* **Précision de la mesure** – valeur réelle de hello de consommation ou de la température doit être enregistré avec précision. Des mesures incorrectes génèrent des résultats imprécis. En règle générale, l’erreur de mesure hello doit être inférieure à 1 % toohello relatif la valeur true.
* **Moment de la mesure** – nécessaire cet horodatage réelle hello de hello les données collectées n’est pas dévier de plus de 10 secondes toohello relatif true heure de mesure hello.
* **Synchronisation** : lorsque plusieurs sources de données sont utilisées (*par exemple*, la consommation et la température) nous devons nous assurer qu’il n’y a pas de problème de synchronisation entre elles. Cela signifie que cette heure hello différence entre l’horodatage hello collectée à partir de toutes les sources de données indépendantes deux ne doit pas dépasser plus de 10 secondes.
* **Latence** : comme indiqué ci-dessus, dans la section **Ingestion de données**, nous dépendons d’un flux de données fiable et du processus d’ingestion. toocontrol que nous devons nous assurer que nous contrôler la latence de données hello. Cela est spécifié en tant que différence d’heure hello entre hello hello réel mesure et temps hello à laquelle il a été chargé dans hello stockage de Cortana Intelligence Suite et est prêt à être utilisé. Pour la charge à court terme prévision latence totale de hello ne doit pas être supérieure à 30 minutes. Pour la charge à long terme prévision latence totale de hello ne doit pas être supérieure à 1 jour.

### <a name="data-preparation-and-feature-engineering"></a>Préparation des données et ingénierie des fonctionnalités
Une fois que les données brutes hello a été ingérées (consultez **intégrer les données**) et a été en toute sécurité stockée, il est prêt toobe traité. Hello phase de préparation des données est en fait les données brutes hello et la conversion (transformation, la mise en forme) dans un formulaire pour hello phase de modélisation. Qui peut inclure des opérations simples telles que l’utilisation des colonnes de données brutes hello à avec sa valeur mesurée réel, les valeurs standardisés, les opérations plus complexes telles que [en retard de temps](https://en.wikipedia.org/wiki/Lag_operator)et d’autres. Hello nouvellement créé des colonnes de données sont les fonctionnalités de données référencé tooas et processus hello de générer ces est ingénierie de fonctionnalité tooas référencé. En fin de hello de ce processus, nous devons un nouveau jeu de données qui a été dérivé à partir des données brutes de hello et peut être utilisé pour la modélisation. En outre, la phase de préparation des données hello doit tootake administration valeurs manquantes (consultez **Data Quality**) et compenser pour eux. Dans certains cas, nous doivent également toonormalize hello données tooensure que toutes les valeurs sont représentées dans hello même échelle.

Dans cette section, que nous répertorions certaines hello commune des fonctionnalités de données qui sont incluses dans l’énergie de hello modèles de prévision de la demande.

**Fonctionnalités pilotées par des temps :** ces fonctionnalités sont dérivées de données de date/horodatage hello. Elles sont extraites et converties en fonctionnalités de catégorie telles que :

* Heure du jour – il s’agit hello heure hello qui prend la valeur de 0 too23
* Jour de semaine – cela représente jour hello de la semaine de hello et prend la valeur de 1 (dimanche) too7 (samedi)
* Jour du mois – cela représente la date effective de hello et peut prendre les valeurs 1 too31
* Mois de l’année – cela représente les mois hello et prend la valeur de 1 (janvier) too12 (décembre)
* Week-end – il s’agit d’une fonctionnalité de valeur binaire qui prend des valeurs de hello 0 pour les jours de la semaine ou 1 pour le week-end
* Congé - il s’agit d’une fonctionnalité de valeur binaire qui accepte les valeurs hello 0 pour un jour régulière ou 1 pour un jour férié
* Termes de Fourier – hello Fourier termes sont poids dérivés hello timestamp et sont utilisés toocapture hello saisonnalité (cycles) dans les données de salutation. Comme plusieurs saisons peuvent figurer parmi les données, il se peut que nous ayons besoin de plusieurs termes de Fourier. Par exemple, les valeurs de demande peuvent comporter des saisons/cycles annuels, hebdomadaires et quotidiens, ce qui se traduira par 3 termes de Fourier.

**Les fonctionnalités de mesure indépendant :** hello indépendant comprend tous les éléments de données hello que nous souhaitons toouse comme PRÉDICTEURS dans notre modèle. Ici, nous exclure les fonctionnalité dépendante hello dont nous avons besoin de toopredict.

* Fonctionnalité de retard : il s’agit d’heure décalée vers les valeurs de la demande réelle de hello. Par exemple, les fonctionnalités de décalage 1 contiendra valeur de la demande de hello dans horodateur actuel du toohello relatif hello heure précédente (en supposant que les données de toutes les heures). De même, nous pouvons ajouter lag 2, 3, de retard *etc.*. combinaison de réel hello des fonctionnalités de décalage sont utilisés sont déterminés pendant la phase de modélisation de hello par l’évaluation des résultats du modèle hello.
* Tendances à long terme : cette fonctionnalité représente une croissance linéaire hello dans la demande entre les années.

**Fonctionnalité dépendante :** fonctionnalité dépendante de hello est la colonne de données hello qui nous aimerions notre toopredict de modèle. Avec [supervisé apprentissage](https://en.wikipedia.org/wiki/Supervised_learning), nous devons tout d’abord effectuer l’apprentissage hello modèle à l’aide des fonctionnalités dépendantes de hello (qui est également référencé tooas étiquettes). Ainsi, hello modèle toolearn hello de modèles dans les données de hello associées de fonctionnalité dépendante de hello. Dans la prévision de la demande de l’énergie nous souhaitons généralement à la demande réelle de toopredict hello et nous serait donc l’utiliser en tant que fonctionnalité dépendante de hello.

**La gestion des valeurs manquantes :** pendant la phase de préparation de données hello, nous avons besoin toodetermine hello meilleure stratégie toohandle les valeurs manquantes. Il s’agit principalement à l’aide de hello statistiques [méthodes d’imputation données](https://en.wikipedia.org/wiki/Imputation_\(statistics\)). Dans les cas de hello de demande d’énergie de prévision, nous avons généralement imputer les valeurs manquantes à l’aide d’une moyenne mobile à partir de points de données disponibles précédente.

**Normalisation des données :** normalisation des données est un autre type de transformation qui est utilisé toobring toutes les données numériques, telles que la demande de prévision dans une même échelle. Cela est généralement permet d’améliorer la précision et l’exactitude du modèle hello. Nous avons cette tâche est généralement nécessaire en divisant la valeur réelle de hello par plage hello de données de hello.
Cela sera valeur d’échelle hello d’origine vers le bas dans une plage plus petite, généralement entre -1 et 1.

## <a name="modeling"></a>Modélisation
phase de modélisation de Hello est où conversion hello de données de hello dans un modèle a lieu. Bonjour cœur de ce processus, il sont des algorithmes qui analyse les données d’historique hello (données d’apprentissage), extraire des motifs et générer un modèle. Ce modèle peut être plus tard toopredict utilisé sur les nouvelles données qui n’a pas de modèle de hello toobuild utilisé.

Une fois que nous avons une travail fiable modèle que nous pouvons réutilisez-la tooscore de nouvelles données est structuré tooinclude hello nécessaire fonctionnalités (X). Hello processus d’évaluation permettront à utiliser de modèle de hello persistantes (objet à partir de la phase de formation hello) et prédire variable hello cible qui est représentée par Ŷ.

### <a name="demand-forecasting-modeling-techniques"></a>Techniques de modélisation de prévision des demandes
Dans les cas de hello de la demande de prévision nous faire utiliser des données d’historique qui sont triées par heure. Nous nous référons généralement toodata qui inclut la dimension de temps hello comme [série chronologique](https://en.wikipedia.org/wiki/Time_series). objectif Hello modélisation de série est toofind temporels tendances, la saisonnalité, auto-corrélation (corrélation au fil du temps) et formuler dans un modèle.

Dernières années, des algorithmes avancés ont été tooimprove prévision de précision et séries tooaccommodate développée chronologiques. Nous en présentons brièvement quelques-unes ici.

> [!NOTE]
> Cette section n’est pas prévue toobe utilisé en tant qu’ordinateur d’apprentissage et les prévisions de vue d’ensemble, mais plutôt comme une brève enquête de techniques qui sont couramment utilisées pour la prévision de la demande de modélisation. Pour plus d’informations et scolaires sur les séries chronologiques, nous vous recommandons les livres en ligne hello [prévision : principes et pratique](https://www.otexts.org/book/fpp).
> 
> 

#### <a name="ma-moving-averagehttpswwwotextsorgfpp62"></a>[**MA (Moyenne mobile)**](https://www.otexts.org/fpp/6/2)
Moyenne mobile est un des hello première techniques d’analyse qui a été utilisée pour les séries chronologiques et il est toujours une des techniques de hello couramment utilisé à compter d’aujourd'hui. Il est également base hello plus avancées techniques de prévision. Avec la moyenne mobile, nous sommes prévision point de données suivant hello en faisant la moyenne sur les points les plus récents hello K, où K représente la commande hello Hello moyenne mobile.

technique de moyenne mobile Hello a d’effet de lissage hello prévision hello et par conséquent, peut ne pas gérer la volatilité bien volumineux dans les données de salutation.

#### <a name="ets-exponential-smoothinghttpswwwotextsorgfpp75"></a>[**ETS (Lissage exponentiel)**](https://www.otexts.org/fpp/7/5)
Lissage exponentiel (ETS) est une famille de différentes méthodes qui utilisent la moyenne pondérée des points de données récents dans le point de données suivant ordre toopredict hello. ne se produise Hello est tooassign des poids plus élevés toomore les valeurs récentes et diminuer progressivement ce poids pour les anciennes valeurs mesurées. Il existe plusieurs méthodes différentes avec cette famille, certains d'entre eux incluent la gestion de saisonnalité dans les données de salutation comme [méthode saisonnières de Tran-hivers dépourvus](https://www.otexts.org/fpp/7/5).

Certaines de ces méthodes tenir compte également saisonnalité hello de données de hello.

#### <a name="arima-auto-regression-integrated-moving-averagehttpswwwotextsorgfpp8"></a>[**ARIMA (Moyenne mobile intégrée de régression automatique)**](https://www.otexts.org/fpp/8)
La moyenne mobile intégrée de régression automatique (ARIMA) est une autre famille de méthodes couramment utilisée pour la prévision de séries chronologiques. Elle combine de façon pratique les méthodes de régression automatique avec la moyenne mobile. Les méthodes de régression d’automatique utilisent des modèles de régression en prenant la série chronologique les valeurs précédentes dans le point de date suivant ordre toocompute hello. Les méthodes ARIMA s’appliquent également la différenciation des méthodes qui incluent le calcul de différence hello entre les points de données et à l’aide de celles au lieu de la valeur de mesure d’origine hello. Enfin, ARIMA utilise aussi hello déplacement moyenne techniques présentées ci-dessus. combinaison de Hello de toutes ces méthodes de différentes manières est les constructions hello famille de méthodes d’ARIMA.

Aujourd’hui, ETS et ARIMA sont largement utilisés dans le cadre de la prévision de la demande d’énergie et de nombreuses autres problématiques de prévision. Dans de nombreux cas elles sont combinées toodeliver des résultats très précis.

**Régression Multiple général** modèles de régression peut être plus important approche de modélisation hello au sein du domaine hello d’apprentissage et de statistiques. Dans le contexte hello de série chronologique, nous utilisons des valeurs futures régression toopredict hello (*, par exemple*, de la demande). Dans la régression nous prennent une combinaison de PRÉDICTEURS de hello et poids hello (également désignée tooas coefficients) de ces PRÉDICTEURS pendant le processus d’apprentissage hello. Hello vise tooproduce une ligne de régression qui sera prévision notre valeur prédite. Méthodes de régression conviennent lors de la variable de cible hello est numérique et également s’adapte donc séries chronologiques. Il existe un large éventail de méthodes de régression, et notamment des modèles de régression très simples comme la [régression linéaire](https://en.wikipedia.org/wiki/Linear_regression) et certains plus sophistiqués, tels que les arbres de décision, les [forêts aléatoires](https://en.wikipedia.org/wiki/Random_forest), les [réseaux neuronaux](https://en.wikipedia.org/wiki/Artificial_neural_network) et les arbres de décision optimisés.

Construction de la demande d’énergie prévision comme un problème de régression nous offre une grande souplesse dans la sélection de nos fonctionnalités de données qui peuvent être combinées à partir des données de série chronologique hello la demande réelle et de facteurs externes tels que de la température. Plus d’informations sur les fonctions hello sélectionné sont décrites dans hello ingénierie de fonctionnalité (consultez **ingénierie de fonctionnalité et de préparation des données**) section de ce document.

À partir de notre expérience avec mise en œuvre et de déploiement du pilote de prévisions à la demande de l’énergie, nous avons constaté que les modèles de régression avancées qui sont disponibles dans Azure ML hello tendent des résultats optimaux tooproduce hello et nous de les utiliser.

## <a name="model-evaluation"></a>Évaluation de modèle
Évaluation du modèle a un rôle essentiel dans hello **Cycle de développement du modèle**. À ce stade, nous allons en validant le modèle de hello et ses performances avec les données réelles. Au cours de hello modélisation étape, nous utilisons une partie des données disponibles de hello pour l’apprentissage du modèle de hello. Pendant la phase d’évaluation de hello, nous prenons reste hello hello tootest hello un modèle de données. Pratiquement, cela signifie que nous sommes alimentant hello modèle nouvelles données qui a été restructurées et contient les mêmes fonctionnalités en tant que jeu de données d’apprentissage hello de hello. Toutefois, pendant le processus de validation de hello, nous utiliser hello modèle toopredict hello cible variable plutôt que fournir hello cibles disponibles variable. Nous nous référons souvent processus toothis en tant que le calcul du score du modèle. Nous devez utiliser les valeurs true cible hello et avec hello a prédit que ceux de comparaison. objectif Hello ici est toomeasure et réduire les erreurs de prédiction hello, ce qui signifie que différence hello entre les prédictions hello et la valeur true hello. Quantification de mesure des erreurs hello d’est la clé dans la mesure où nous comme modèle de hello toofine-régler et vérifier si l’erreur de hello réellement diminue. Modèle de hello réglage peut être effectuée en modifiant les paramètres du modèle qui contrôlent le processus d’apprentissage de hello, ou en ajoutant ou supprimant des fonctionnalités de données (appelée tooas [balayage de paramètres](https://channel9.msdn.com/Blogs/Azure/Data-Science-Series-Building-an-Optimal-Model-With-Parameter-Sweep)). Pratiquement, cela signifie que nous pouvons devez tooiterate entre l’ingénierie de fonctionnalité hello, de modélisation et les phases d’évaluation de modèle plusieurs fois jusqu'à ce que nous sommes au niveau de tooreduce en mesure de hello erreur toohello requis.

Il est important de tooemphasis qu’erreur de prévision hello ne seront jamais zéro qu’il n’est jamais un modèle qui peut prédire parfaitement chaque résultat. Toutefois, il existe une certaine envergure d’erreur qui est acceptable par les entreprises de hello. Au cours du processus de validation de hello, nous aimerions tooensure que notre erreur de prévision de modèle hello niveau s’ou niveau de meilleures performances que la tolérance de panne hello entreprise. Il est donc important tooset hello niveau de hello tolérables erreur début hello Hello cycle pendant hello **problème Formulation** phase.

### <a name="typical-evaluation-techniques"></a>Techniques d’évaluation classiques
Il existe différentes façons de mesurer et quantifier les erreurs de prévision. Dans cette section, nous nous concentrerons discussion de hello sur évaluation techniques tootime pertinentes de la série et spécifiques pour la prévision de la demande de l’énergie.

#### <a name="mapehttpsenwikipediaorgwikimeanabsolutepercentageerror"></a>[**MAPE**](https://en.wikipedia.org/wiki/Mean_absolute_percentage_error)
MAPE signifie Erreur de pourcentage absolue moyenne. Avec MAPE nous sommes informatique différence hello entre chaque point prévue et la valeur réelle de hello de ce point. Puis, nous quantifier erreur hello par point en calculant la proportion de hello de la valeur réelle de hello différence toohello relatif. À la dernière étape, nous faisons la moyenne de ces valeurs. formule mathématique de Hello utilisée pour MAPE est suivant de hello :

![Formule de MAPE](media/cortana-analytics-playbook-demand-forecasting-energy/mape-formula.png)
*où A<sub>t</sub> est la valeur réelle hello, F<sub>t</sub> est hello valeur prédite, et n est hello horizon de prévision.*

## <a name="deployment"></a>Déploiement
Une fois que nous avons cerné hello phase de modélisation et valider les performances du modèle hello nous sommes toogo prêt dans la phase de déploiement hello. Dans ce contexte, déploiement signifie l’activation du client de hello tooconsume hello modèle en exécutant des prédictions réelles à grande échelle. concept Hello du déploiement est la clé dans Azure ML, car notre objectif principal est tooconstantly appeler des prédictions en opposition toojust obtenir un aperçu de hello à partir des données de hello. phase de déploiement Hello appartient hello où nous activer toobe de modèle hello consommée à grande échelle.

Dans le contexte de hello de prévision de la demande de l’énergie, notre objectif est de prévisions périodique et continue de tooinvoke tout en garantissant que les données actualisées ne seront disponibles pour le modèle de hello et ce hello a prévu de données sont envoyées de client de consommateur toohello précédent.

### <a name="web-services-deployment"></a>Déploiement de services Web
Hello principal déployable bloc de construction dans Azure ML est un service web de hello. Il s’agit de consommation de tooenable de façon plus efficace hello d’un modèle de prévision dans le cloud de hello. service Web de Hello encapsule le modèle de hello et conclut avec un [RESTful](http://www.restapitutorial.com/) API (Application Programming Interface). Hello API peut servir dans le cadre de n’importe quel code client, comme illustré dans le diagramme hello ci-dessous.

![Nous assurons le déploiement du service et la consommation](media/cortana-analytics-playbook-demand-forecasting-energy/web-service-deployment-and-consumption.png)

Comme le montre, service web de hello est déployé dans hello cloud de Cortana Intelligence Suite et peut être invoqué via son point de terminaison REST API exposée. Un type différent de clients entre les différents domaines peut appeler service hello via hello API Web simultanément. service web de Hello peut également mettre à l’échelle pour prendre en charge des milliers d’appels simultanés.

### <a name="a-typical-solution-architecture"></a>Une architecture de solution classique
Lors du déploiement d’une demande d’énergie prévision de solution, nous sommes intéressés par déploiement d’une solution de tooend de fin qui va au-delà de service web de prédiction hello et facilite le flux de données entière hello. Au moment de hello que nous appeler une prévision, nous devez toomake que ce modèle hello est chargé avec les fonctionnalités de données à jour. Cela implique que hello qui vient d’être collecté des données brutes sont constamment ingérées, traitées et transformées en hello requis ensemble de fonctionnalités sur quel modèle hello a été créé. AT hello même temps, nous veut toomake hello a prévu de données disponibles pour hello fin beaucoup de clients. Schéma hello ci-dessous illustre un exemple données cycle de flux (ou de pipeline de données) :

![TooEnd de fin de flux de données de prévision de la demande de l’énergie](media/cortana-analytics-playbook-demand-forecasting-energy/energy-demand-forecase-end-data-flow.png)

Voici les étapes hello qui ont lieu dans le cadre du cycle de prévision hello énergie à la demande :

1. Des millions de compteurs de données déployés génèrent en permanence et en temps réel des données de consommation énergétique.
2. Ces données sont recueillies et téléchargées dans un référentiel cloud (*par exemple*, un objet Blob Azure).
3. Avant d’être traité, les données brutes hello sont agrégée tooa sous-centrale ou niveau régional tel que défini par l’entreprise de hello.
4. traitement de fonctionnalité Hello (consultez **la préparation des données et la fonctionnalité de traitement**) puis se déroule de formation ou d’évaluation de modèle de données de hello de produit qui est requises pour : hello fonctionnalité jeu de données sont stockées dans une base de données (*, par exemple*, SQL Azure).
5. Hello réapprentissage service est appelé hello toore-train prévision de modèle-mise à jour de la version du modèle de hello est conservé afin qu’il peut être utilisé par hello calcul du score du service web.
6. Hello calcul du score du service web est appelée sur une planification qui correspond à la fréquence de prévision hello requis.
7. Hello a prévu de données sont stockées dans une base de données qui sont accessibles par le client de la consommation de fin hello.
8. client de consommation Hello récupère les prévisions hello, il s’applique dans la grille de hello et consomme conformément aux cas d’usage hello requis.

Il est important toonote que ce cycle entier est entièrement automatisé et s’exécute selon une planification. Hello intégralité de l’orchestration de ce cycle de données peut être effectuée à l’aide des outils tels que [Azure Data Factory](http://azure.microsoft.com/services/data-factory/).

### <a name="end-tooend-deployment-architecture"></a>Fin tooEnd Architecture de déploiement
Dans l’ordre toopractically déployer une solution de prévision de la demande d’énergie sur Cortana Intelligence, nous devons tooensure que les composants requis de hello sont établies et configurés correctement.

Hello diagramme suivant illustre une architecture Intelligence Cortana en fonction de type qui implémente et orchestre le cycle de flux de données hello est décrit ci-dessus :

![Fin tooEnd Architecture de déploiement](media/cortana-analytics-playbook-demand-forecasting-energy/architecture.png)

Pour plus d’informations sur chacun des composants de hello et l’ensemble de l’architecture hello reportez-vous toohello modèle de Solution de l’énergie.

