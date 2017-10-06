---
title: "aaaAnalyzing client évolution à l’aide de la Machine Learning | Documents Microsoft"
description: "Étude de cas de développement d’un modèle intégré pour l’analyse et la notation de l’attrition des clients."
services: machine-learning
documentationcenter: 
author: jeannt
manager: jhubbard
editor: cgronlun
ms.assetid: 1333ffe2-59b8-4f40-9be7-3bf1173fc38d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeannt
ms.openlocfilehash: 070e6a2ebe4f2fe439a42ffe1a3fa9d6d3788d62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="analyzing-customer-churn-by-using-azure-machine-learning"></a>Analyse de l’attrition des clients à l’aide de Microsoft Azure Machine Learning
## <a name="overview"></a>Vue d’ensemble
Cet article présente une implémentation de référence d’un projet d’analyse de l’attrition des clients, créé à l’aide de Microsoft Azure Machine Learning. Dans cet article, nous traitent les modèles génériques associés pour résoudre les problème hello de résiliations industriels guidage. Nous avons également mesurer la précision de hello de modèles qui sont générés à l’aide de Machine Learning, et nous évaluons les directions pour un développement ultérieur.  

### <a name="acknowledgements"></a>Remerciements
Cette expérience a été développée et testée par Serge Berger, spécialiste des données chez Microsoft, et Roger Barga, anciennement chef de produits pour Microsoft Azure Machine Learning. équipe de documentation sur Azure Hello grandement appréciées accuse réception de leurs compétences et leur Merci ce livre blanc.

> [!NOTE]
> les données de salutation utilisées pour cette expérience ne sont pas disponibles publiquement. Pour obtenir un exemple de comment toobuild un apprentissage de modèle pour l’analyse de l’évolution du code, consultez : [Retail évolution du modèle](https://gallery.cortanaintelligence.com/Collection/Retail-Customer-Churn-Prediction-Template-1) dans [Cortana Intelligence galerie](http://gallery.cortanaintelligence.com/)
> 
> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-problem-of-customer-churn"></a>problème de Hello d’évolution du client
Les entreprises de marché hello et dans tous les secteurs de l’entreprise ont toodeal avec l’évolution du code. Parfois, ce dernier est excessif et influence les décisions relatives aux politiques de l'entreprise. les solutions traditionnelles Hello est toopredict haute-tendance churners et leurs besoins via un service de conseiller, campagnes marketing, ou en appliquant dispense spéciaux. Ces approches peuvent varier à partir d’industrie tooindustry d’un tooanother de cluster consommateur particulier dans un secteur d’activité (par exemple, les télécommunications).

facteur commun de Hello est que les entreprises doivent toominimize ces efforts de rétention client spécial. Par conséquent, une méthodologie naturelle serait être tooscore tous les clients avec une probabilité d’évolution hello et haut de hello N autres d’adresses. les clients principaux Hello peut être hello ceux qui sont plus rentables ; par exemple, dans des scénarios plus complexes, une fonction des bénéfices est employée lors de la sélection de hello des candidats dispense spéciaux. Toutefois, ces considérations sont uniquement une partie de la stratégie globale de hello pour traiter les évolution du code. Les entreprises ont également tootake dans risque de compte (et la tolérance de panne risque associé), hello niveau et le coût d’une intervention hello et la segmentation du client plausible.  

## <a name="industry-outlook-and-approaches"></a>Perspectives et approches du secteur
La gestion sophistiquée de l'attrition témoigne de la maturité d'un secteur. l’exemple Hello classique est télécommunications hello où les abonnés sont commutateur elles sonttrop connus à partir d’un fournisseur tooanother. Cette attrition volontaire est l’un des principaux problèmes du secteur. En outre, les fournisseurs ont accumulé connaissance importante sur *évolution pilotes*, qui sont des facteurs de hello que tooswitch de clients du lecteur.

Par exemple, choix combiné ou un périphérique est un pilote bien connu d’évolution dans l’entreprise de téléphone mobile hello. Par conséquent, une stratégie populaire est toosubsidize les prix de hello d’un combiné pour les nouveaux abonnés et le chargement des clients pour une mise à niveau un tooexisting prix plein. Historiquement, cette stratégie a conduit toocustomers récurrente à partir d’un fournisseur tooanother tooget une remise, qui à son tour, a invité fournisseurs toorefine leurs stratégies.

La volatilité élevée des offres de téléphone est un facteur qui invalide très rapidement les modèles d’attrition basés sur les modèles de téléphone actuels. En outre, les téléphones mobiles ne sont pas uniquement les appareils de télécommunication ; ils sont également des instructions de manière (envisagez hello iPhone), et ces réseaux sociaux PRÉDICTEURS sont en dehors portée de hello télécommunications régulière des jeux de données.

Hello pour la modélisation résulte que vous ne peut pas concevoir une stratégie sonore simplement en éliminant les raisons connues d’évolution du code. En fait, il est **obligatoire** de recourir à une stratégie de modélisation continue, comprenant des modèles classiques qui quantifient les variables catégoriques (ex. : arbres de décision).

À l’aide de jeux de données volumineux sur leurs clients, les organisations effectuez analytique de données volumineuses (en particulier, la détection d’évolution du code basée sur les données volumineuses) comme un problème de toohello approche efficace. Vous trouverez plus d’informations sur les problème de toohello hello données volumineuses approche d’évolution Bonjour recommandations sur la section ETL.  

## <a name="methodology-toomodel-customer-churn"></a>Évolution du code client de méthodologie toomodel
Une common-résolution des problèmes processus toosolve résiliations sont représentée dans Figures 1 à 3 :  

1. Un modèle de risque vous permet de tooconsider répercussions des actions de probabilité et des risques.
2. Un modèle d’intervention vous permet de tooconsider comment niveau hello d’intervention peut affecter la probabilité de hello d’évolution du code et hello montant de la valeur de durée de vie client (CLV).
3. Cette analyse prête analyse qualitative tooa tooa promus proactive campagne marketing ciblant offre optimal de client segments toodeliver hello.  

![][1]

Cette approche orientée est hello meilleure manière tootreat évolution de ce dernier, mais il est fourni avec la complexité : nous avons toodevelop une dépendances archétype et trace comportant plusieurs modèles entre les modèles hello. interaction Hello entre les modèles peut être encapsulée comme indiqué dans hello suivant schéma :  

![][2]

*Figure 4 : archétype multi-modèles unifié*  

Interaction entre les modèles hello est la clé si nous sommes toodeliver une durée de rétention toocustomer approche globale. Chaque modèle nécessairement dégrade au fil du temps ; Par conséquent, architecture de hello est une boucle implicite (similaire archétype toohello définie par la norme d’exploration de données hello CRISP-DM, [***3***]).  

Hello ensemble du cycle de risque de décision-marketing segmentation/décomposition est toujours une structure généralisée, qui est applicable réduire problèmes de l’entreprise. Analyse de l’évolution du code est simplement un fort représentant de ce groupe de problèmes, car elle présente toutes les caractéristiques de hello d’un problème d’entreprise complexes qui n’autorise pas une solution prédictive simplifiée. Hello sociaux aspects de hello approche moderne toochurn ne sont pas mises en surbrillance en particulier dans l’approche de hello, mais les aspects sociaux hello sont encapsulées dans archétype de modélisation hello, tels qu’ils seraient dans n’importe quel modèle.  

L'analyse des données volumineuses est un ajout intéressant. Les entreprises de télécommunications et vente au détail d’aujourd'hui collectent des données exhaustives sur leurs clients, et nous pouvons facilement prévoir que hello besoin de connectivité comportant plusieurs modèle deviendra une tendance commune donnée émergentes telles que les tendances hello Internet des objets et appareils omniprésents qui autorisent des solutions smart tooemploy d’entreprise à plusieurs niveaux.  

 

## <a name="implementing-hello-modeling-archetype-in-machine-learning-studio"></a>Implémentation hello modélisation archétype dans Machine Learning Studio
Étant donné le problème hello décrit ci-dessus, nouveautés hello meilleure manière tooimplement une modélisation intégrée et l’approche de score Dans cette section, nous verrons comment nous y sommes parvenus à l’aide de Microsoft Azure Machine Learning Studio.  

approche comportant plusieurs modèles de Hello est indispensable lorsque vous concevez un archétype global pour l’évolution du code. Hello même calcul de score (prédictive) partie de l’approche de hello doit être comportant plusieurs modèle.  

Hello diagramme suivant illustre le prototype de hello que nous avons créé, qui utilise des algorithmes de calcul de score quatre des activités toopredict Machine Learning Studio. Bonjour à l’aide d’une approche comportant plusieurs modèle fait toocreate une précision de tooincrease classifieur ensemble, mais également tooprotect contre surapprentissage et sélection de fonctionnalité normative tooimprove.  

![][3]

*Figure 5 : prototype d’une méthode de modélisation de l’attrition*  

Hello sections suivantes fournissent plus de détails sur le prototype hello score du modèle que nous avons implémentées à l’aide de Machine Learning Studio.  

### <a name="data-selection-and-preparation"></a>Sélection et préparation des données
les données de salutation utilisé les modèles hello toobuild et clients de score obtenu à partir d’une solution verticale CRM, avec la confidentialité des clients tooprotect données obfusquées hello. Hello données contient des informations sur les 8 000 abonnements Bonjour des États-Unis et combine trois sources : mise en service de données (les métadonnées d’abonnement), les données d’activité (utilisation du système de hello) et les données de prise en charge de client. les données de salutation n’incluent pas de toute entreprise des informations sur les clients de hello ; par exemple, il n’inclut pas les scores de métadonnées ou le crédit de fidélité.  

Pour simplifier, les processus de nettoyage des données et ETL ne sont pas utilisés, car nous estimons que la préparation des données a déjà été effectuée à un autre niveau.   

Sélection des fonctionnalités pour la modélisation est basée sur la signification préliminaire calculer les scores du jeu hello de PRÉDICTEURS, inclus dans le processus hello qui utilise le module de forêt aléatoire hello. Pour l’implémentation de hello dans Machine Learning Studio, nous avons calculé hello moyenne, médiane et les plages pour les fonctionnalités représentatives. Par exemple, nous avons ajouté des agrégats de données qualitatives hello, telles que les valeurs minimales et maximales pour l’activité de l’utilisateur.    

Nous avons également capturées informations temporelles pour hello six mois les plus récents. Nous avons analysé les données pendant un an, et nous avons établi que, même s’il existe des tendances significatives, effet hello sur l’évolution du code est considérablement moindre après six mois.  

Hello plus il est important que hello tout processus, y compris ETL, sélection de fonctionnalités, et de modélisation a été implémentée dans Machine Learning Studio, à l’aide de sources de données dans Microsoft Azure.   

Hello diagrammes suivants illustrent les données hello qui a été utilisées.  

![][4]

*Figure 6 : extrait d’une source de données (masquée)*  

![][5]

*Figure 7 : caractéristiques extraites de la source de données*
 

> Notez que ces données sont privées et par conséquent les données et du modèle de hello ne peut pas être partagées.
> Toutefois, pour un modèle semblable à l’aide des données publiquement disponibles, consultez l’exemple d’expérience suivant dans hello [Cortana Intelligence galerie](http://gallery.cortanaintelligence.com/): [évolution du client de télécommunications](http://gallery.cortanaintelligence.com/Experiment/31c19425ee874f628c847f7e2d93e383).
> 
> toolearn plus d’informations sur la manière d’implémenter un modèle d’analyse de l’évolution à l’aide de Cortana Intelligence Suite, nous vous recommandons également [cette vidéo](https://info.microsoft.com/Webinar-Harness-Predictive-Customer-Churn-Model.html) par programme senior ouvrables Hyong Tok. 
> 
> 

### <a name="algorithms-used-in-hello-prototype"></a>Algorithmes utilisés dans le prototype de hello
Nous avons utilisé hello suivant quatre algorithmes d’apprentissage automatique prototype de hello toobuild (aucune personnalisation) :  

1. Régression logique (LR)
2. Arbre de décision optimisé(BT)
3. Perceptron moyenné (AP)
4. Machines à vecteurs de support (SVM)  

Hello diagramme suivant illustre une partie de l’aire de conception d’expérience hello, qui indique la séquence hello dans le hello modèles ont été créés :  

![][6]  

*Figure 8 : création de modèles dans Microsoft Azure ML Studio*  

### <a name="scoring-methods"></a>Méthodes de notation
Nous notées les modèles hello quatre à l’aide d’un jeu de données d’apprentissage étiqueté.  

Nous avons envoyé également hello score du modèle de données comparable dataset tooa générée à l’aide d’édition de bureau hello de SAP Enterprise Miner 12. Nous avons mesuré précision hello du modèle de SAP hello et toutes les quatre modèles de Machine Learning Studio.  

## <a name="results"></a>Résultats
Dans cette section, nous vous présentons nos conclusions à l’exactitude de hello de modèles hello, en fonction de hello calcul du score du jeu de données.  

### <a name="accuracy-and-precision-of-scoring"></a>Exactitude et précision de la notation
En règle générale, implémentation hello dans Azure Machine Learning est derrière SAS une précision d’environ 10-15 % (zone sous la courbe ou AUC).  

Toutefois, mesure la plus importante dans l’évolution du code hello est taux de mauvaise classification hello : autrement dit, de churners de N premiers hello comme prévu par le classifieur de hello, qui a réellement fait **pas** évolution et reçu un traitement spécial ? hello diagramme suivant compare ce taux de mauvaise classification pour tous les modèles hello :  

![][7]

*Figure 9 : aire sous la courbe du prototype Passau*

### <a name="using-auc-toocompare-results"></a>À l’aide des résultats de toocompare AUC
Zone sous courbe (AUC) est une mesure qui représente une mesure globale de *séparable* entre les distributions de hello de scores pour les remplissages positifs et négatifs. Il est similaire toohello de graphique de récepteur opérateur caractéristique (ROC) traditionnelles, mais une différence importante est que cette métrique AUC hello ne nécessite pas une valeur de seuil de toochoose. Au lieu de cela, il résume les résultats de hello sur **tous les** possibles. En revanche, graphique ROC traditionnel hello affiche le taux de positif de hello sur l’axe vertical de hello et hello taux de faux positifs sur l’axe horizontal de hello et varie en fonction du seuil de classification hello.   

AUC est généralement utilisé en tant que mesure d’intéressant pour différents algorithmes (ou des systèmes différents), car elle permet toobe modèles par rapport au moyen de leurs valeurs AUC. Il s’agit d’une approche populaire dans des secteurs comme la météorologie et les biosciences. Ainsi, l’ASC est un outil répandu pour évaluer les performances d’un classifieur.  

### <a name="comparing-misclassification-rates"></a>Comparaison des taux de classification incorrecte
Nous avons comparé taux de mauvaise classification hello hello du jeu de données en question à l’aide de données CRM hello d’environ 8 000 abonnements.  

* taux de mauvaise classification Hello SAP a été 10 à 15 %.
* taux de mauvaise classification Hello Machine Learning Studio a été 15 à 20 % de churners de haut 200-300 hello.  

Dans le secteur des télécommunications hello, il est important tooaddress uniquement les clients qui ont hello toochurn de risque le plus élevé en leur offrant un service de conseiller ou un traitement spécial. À cet égard, mise en œuvre de la Machine Learning Studio hello permet d’obtenir les résultats similaire à modèle de SAP hello.  

Par hello même jeton, analyse de précision est plus importante que la précision, car nous intéresse principalement correctement classification churners potentielles.  

Hello suivant le schéma de Wikipedia décrit la relation hello dans un graphique engageante et facile à comprendre :  

![][8]

*Figure 10 : équilibre entre exactitude et précision*

### <a name="accuracy-and-precision-results-for-boosted-decision-tree-model"></a>Résultats liés à l’exactitude et à la précision du modèle d’arbre de décision optimisé
Hello suivant hello d’affiche graphique brut résultant de score à l’aide du prototype d’apprentissage hello pour le modèle d’arbre de décision hello augmenté, ce qui se produit hello toobe plus précise entre les modèles de quatre hello :  

![][9]

*Figure 11 : caractéristiques du modèle d’arbre de décision optimisé*

## <a name="performance-comparison"></a>Comparaison entre les performances
Nous avons comparé vitesse hello à laquelle les données a été évaluées à l’aide de modèles de Machine Learning Studio hello et un modèle comparable créé à l’aide d’édition de bureau hello de SAP Enterprise Miner 12.1.  

Hello tableau suivant résume les performances hello des algorithmes de hello :  

*Tableau 1. Performances générales (précision) des algorithmes de hello*

| LR | BT | AP | SVM |
| --- | --- | --- | --- |
| Modèle moyen |Hello meilleur modèle |Mauvaises performances |Modèle moyen |

modèles de Hello hébergés dans Machine Learning Studio obtenu les meilleures performances de SAS par 15 à 25 % de la vitesse d’exécution, mais précision a été en grande partie sur les par.  

## <a name="discussion-and-recommendations"></a>Considérations et recommandations
Dans le secteur des télécommunications hello, plusieurs méthodes sont apparus tooanalyze évolution, y compris :  

* Mesures dérivées pour quatre catégories principales :
  * **Entité (par exemple, un abonnement)**. Configurer les informations de base sur les abonnement hello et/ou de client qui est sujet hello d’évolution.
  * **Activité**. Obtenir toutes les informations d’utilisation possibles entité toohello associées, par exemple, les nombre hello de connexions.
  * **Service client**. Collecter des informations à partir du client prise en charge des journaux tooindicate si l’abonnement de hello avait problèmes ou les interactions avec le client prend en charge.
  * **Données d'entreprise et concurrentielles**. Obtenir toutes les informations possibles sur un client de hello (par exemple, peut être indisponible ou dur tootrack).
* Utilisez la sélection de fonctionnalité toodrive importance. Cela implique ce modèle d’arbre de décision augmenté de hello est toujours une approche prometteuse.  

Hello utilisation de ces quatre catégories crée une illusion de hello qui simple *déterministe* approche, basée sur les index formés sur les facteurs raisonnables par catégorie, suffisante tooidentify des clients aux risques liés à l’évolution du code. Malheureusement, même si cette notion reste plausible, c'est une fausse idée. Hello raison est qu’évolution du code est un effet temporelle et facteurs hello toochurn se trouvent généralement dans les états transitoires. Entraîne un client tooconsider en laissant aujourd'hui peut-être être différente demain, et il sera certainement différents six mois à partir de maintenant. De ce fait, un modèle *probabiliste* est nécessaire.  

Cette observation importante est souvent négligée dans l’entreprise, ce qui est généralement préféré par un tooanalytics d’approche orientée sur intelligence d’entreprise, principalement car il s’agit d’une vente et admet automation simple.  

Toutefois, la promesse hello de libre-service d’analytique à l’aide de Machine Learning Studio est que hello quatre catégories d’informations, classés par division ou un service, devient une source précieuse pour l’apprentissage sur l’évolution du code.  

Une autre fonctionnalité intéressante à venir dans Azure Machine Learning est hello capacité tooadd un référentiel de toohello module personnalisé des modules prédéfinis qui sont déjà disponibles. Cette fonctionnalité, essentiellement, crée une opportunité tooselect bibliothèques et créer des modèles pour des marchés verticaux. Il est un différentiateur important d’Azure Machine Learning en place de marché hello.  

Nous espérons que toocontinue cette rubrique dans analytique de données hello toobig futures, particulièrement associées.
  

## <a name="conclusion"></a>Conclusion
Ce document décrit un problème courant hello raisonnable tootackling d’évolution du client à l’aide d’une infrastructure générique. Nous avons envisagé un prototype de modèle de notation, que nous avons implémenté à l’aide de Microsoft Azure ML. Enfin, nous évaluée d’analyse de précision hello et les performances des solutions de prototype hello avec les algorithmes de toocomparable égard dans SAP.  

**Pour plus d'informations :**  

Ce document vous a-t-il été utile ? Donnez-nous votre avis. Indiquez-nous, sur une échelle de 1 too5 (médiocre) (excellent), quelle note donneriez-vous ce document et pourquoi vous lui ayez donné cette évaluation ? Par exemple :  

* Vous l’avez élevé en raison de bons exemples de toohaving, les captures d’écran excellent, désactivez l’écriture ou une autre raison ?
* Vous l’avez jugé faible échéance toopoor exemples, captures d’écran floue ou écriture difficile de savoir ?  

Ces commentaires nous aideront à améliorer la qualité des livres blancs que nous diffusons hello.   

[Envoyer des commentaires](mailto:sqlfback@microsoft.com).
 

## <a name="references"></a>Références
[1] Analytique prédictive : au-delà de prédictions hello, w. McKnight, gestion de l’Information, juillet/août 2011, p. 18 à 20.  

[2] Article Wikipédia : [Accuracy and precision](http://en.wikipedia.org/wiki/Accuracy_and_precision)

[3] [CRISP-DM 1.0: Step-by-Step Data Mining Guide](http://www.the-modeling-agency.com/crisp-dm.pdf)   

[4] [Big Data Marketing: Engage Your Customers More Effectively and Drive Value](http://www.amazon.com/Big-Data-Marketing-Customers-Effectively/dp/1118733894/ref=sr_1_12?ie=UTF8&qid=1387541531&sr=8-12&keywords=customer+churn)

[5] [Modèle d’attrition Telco](http://gallery.cortanaintelligence.com/Experiment/Telco-Customer-Churn-5) dans la galerie [Cortana Intelligence](http://gallery.cortanaintelligence.com/) 
 

## <a name="appendix"></a>Annexe
![][10]

*Figure 12 : capture d’écran d’une présentation d’un prototype pour l’attrition*

[1]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-1.png
[2]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-2.png
[3]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-3.png
[4]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-4.png
[5]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-5.png
[6]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-6.png
[7]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-7.png
[8]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-8.png
[9]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-9.png
[10]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-10.png
