---
title: exemples de hello aaaUse datasets dans Machine Learning Studio | Documents Microsoft
description: "Descriptions des hello de jeux de données utilisés dans les exemples de modèles inclus dans Machine Learning Studio. Vous pouvez utiliser ces exemples de jeux de données pour vos expériences."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 03a0b844-e8a7-4896-996f-d3c7a0db7a50
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: c7786478db82d40aaf27c37b3947ded5f042dd70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-sample-datasets-in-azure-machine-learning-studio"></a>Utiliser des jeux de données exemple hello dans Azure Machine Learning Studio
[top]: #machine-learning-sample-datasets

Quand vous créez un espace de travail dans Azure Machine Learning, vous disposez par défaut d’un certain nombre d’exemples de jeux de données et d’expériences. Un grand nombre de ces jeux de données exemple sont utilisés par les modèles d’exemple hello Bonjour [Azure Cortana Intelligence galerie](http://gallery.cortanaintelligence.com/). D’autres sont inclus comme exemples des différents types de données généralement utilisées dans Machine Learning.

Certains de ces jeux de données sont disponibles dans le Stockage Blob Azure. Pour ces jeux de données, hello tableau suivant fournit un lien direct. Vous pouvez utiliser ces jeux de données dans vos expériences à l’aide de hello [importer des données] [ import-data] module.

autres Hello ces jeux de données exemple sont disponibles dans votre espace de travail **jeux de données enregistrés** en hello module palette toohello à gauche du canevas de l’expérience hello lorsque vous ouvrez ou créez une nouvelle expérience dans Machine Learning Studio.
Vous pouvez utiliser un de ces jeux de données dans votre propre expérience en le faisant glisser tooyour canevas de l’expérience.


[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<table>

<tr>
  <th align=left>Nom du jeu de données</th>
  <th align=left>Description du jeu de données</th>
</tr>

<tr>
  <td valign=top>Jeu de données Adult Census Income Binary Classification</td>
  <td valign=top>
Un sous-ensemble de la base de données de recensement hello 1994, à l’aide de travail adultes ans hello de 16 avec un index de revenu ajusté de > 100.<p> </p><b>Utilisation :</b> classer des personnes à l’aide des données démographiques toopredict si une personne gagne an supérieure à 50 Ko.<p> </p><b>Recherche associée :</b> Kohavi, R., Becker, B., (1996). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, Californie : Université de Californie, School of Information and Computer Science  </td>
</tr>

<tr ID=airport-codes-dataset>
  <td valign=top>Jeu de données des codes de l'aéroport</td>
  <td valign=top>
Codes des aéroports des États-Unis.<p> </p>Ce jeu de données contient une ligne pour chaque aéroport des États-Unis, en fournissant hello aéroport ID et nom, ainsi que de hello emplacement ville et état.
  </td>
</tr>

<tr>
  <td valign=top>Données sur le prix des véhicules automobiles (brutes)</td>
  <td valign=top>
Informations sur les automobiles par marque et modèle, y compris de prix de hello, fonctionnalités, telles que nombre hello de cylindres et MPG, ainsi que d’une évaluation du risque d’assurance.<p> </p>score de risque Hello est initialement associé à prix automatique et puis ajustée pour risque réel dans un processus appelé tooactuaries comme symboling. Une valeur de + 3 indique qu’automatique de hello est risqué, et une valeur de -3 qu’il est probablement sécurisé.<p> </p><b>Utilisation :</b> score de risque Predict hello en fonctionnalités, à l’aide de la classification de régression ou multivariate. <p> </p><b>Recherche associée :</b> Schlimmer, J.C. (1987). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, Californie : Université de Californie, School of Information and Computer Science  </td>
</tr>

<tr ID=bike-rental-uci-dataset>
  <td valign=top>Jeu de données de location de vélos de l'UCI</td>
  <td valign=top>
Le jeu de données de location de vélo de l'UCI est basé sur les données réelles de la société Capital Bikeshare qui assure l'entretien du réseau de location de vélos à Washington DC.<p> </p>jeu de données Hello possède une ligne pour chaque heure de chaque jour 2011 et 2012, pour un total de 17,379 lignes. plage de Hello de toutes les heures des locations vélo est de 1 too977.

  </td>
</tr>

<tr ID=bill-gates-rgb-image>
  <td valign=top>Image RVB de Bill Gates</td>
  <td valign=top>
Fichier image disponible publiquement converti tooCSV données.<p> </p>code pour la conversion d’image de hello Hello est fourni dans hello <strong>à l’aide du clustering K-Means de quantification des couleurs</strong> page de détails de modèle.
  </td>
</tr>

<tr>
  <td valign=top>Données sur le don de sang</td>
  <td valign=top>
Un sous-ensemble de données de base de données de donneurs de sang hello Hello sang Transfusion Service Chu de centre de Hsin ville, Taïwan.<p> </p>Les données de donneurs incluent mois hello depuis le dernier don) et fréquence ou hello le nombre total de dons, la durée écoulée depuis le dernier don et quantité de don de sang.<p> </p><b>Utilisation :</b> hello vise toopredict via classification si donneurs de hello donnés sang en mars 2007, où 1 indique un donneur pendant la période de cible hello et 0 un donneur-non. <p> </p><b>Recherche associée :</b> Yeh, I.C., (2008). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, Californie : Université de Californie, School of Information and Computer Science  <p> </p>Yeh, I-Cheng, Yang, King-Jang et Ting, Tao-Ming, « Knowledge discovery on RFM model using Bernoulli sequence », Expert Systems with Applications, 2008, <a href="http://dx.doi.org/10.1016/j.eswa.2008.07.018">http://dx.doi.org/10.1016/j.eswa.2008.07.018</a>
  </td>
</tr>

<tr ID=book-reviews-from-amazon>
  <td valign=top>Critiques de livres d'Amazon</td>
  <td valign=top>
Révisions de livres d’Amazon, effectuée à partir du site Web de amazon.com hello par les chercheurs de l’Université de Pennsylvanie (<a href="http://www.cs.jhu.edu/~mdredze/datasets/sentiment/">sentiment</a>). Consultez le document de recherche hello, « biographie, films indiens, zones de flèche et séparable : Adaptation de domaine pour la Classification des sentiments » par John Blitzer, Mark Dredze et Fernando Pereira ; Association du calcul Linguistics (ACL), 2007.<p> </p>jeu de données d’origine Hello a K 975 les révisions des classements 1, 2, 3, 4 ou 5. Hello révisions ont été écrites en anglais et hello proviennent de la période de temps 1997-2007. Ce jeu de données a été échantillonnées en bas de too10K révisions.
  </td>
</tr>

<tr>
  <td valign=top>Données sur le cancer du sein</td>
  <td valign=top>
Une des trois au cancer jeux de données fournies par hello Institute oncologie qui apparaît fréquemment dans la documentation d’apprentissage machine. Combine des informations de diagnostic et des caractéristiques d'analyse de laboratoire sur environ 300 échantillons de tissu.<p> </p><b>Utilisation :</b> classer de type hello du cancer, basé sur 9 attributs, dont certains sont linéaires et certaines sont catégorielles. <p> </p><b>Recherche associée :</b> Wohlberg, W.H., Street, W.N., &amp; Mangasarian, O.L. (1995). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, Californie : Université de Californie, School of Information and Computer Science  </td>
</tr>

<tr ID=breast-cancer-features>
  <td valign=top>Caractéristiques du cancer du sein <td valign=top>
Hello dataset contient des informations pour les régions de suspectes 102K (candidats) des images de rayons x, décrites par les 117 fonctionnalités. fonctionnalités de Hello sont propriétaires et leur signification n’est pas révélée par les créateurs de dataset hello (Siemens de soins de santé). 
  </td>
</tr>

<tr ID=breast-cancer-info>
  <td valign=top>Informations sur le cancer du sein</td>
  <td valign=top>
Hello dataset contient des informations supplémentaires pour chaque région suspecte d’image de rayon x. Chaque exemple fournit des informations (par exemple, étiquette, patient ID, les coordonnées de l’image entière de correctif relatif toohello) sur le numéro de ligne correspondant hello dans le jeu de données de fonctionnalités de Cancer du sein hello. Chaque patient présente un certain nombre d’exemples. Pour les patients atteints de cancer, certains exemples sont positifs et d’autres négatifs. Pour les patients non atteints de cancer, tous les exemples sont négatifs. jeu de données Hello a 102K exemples. Hello dataset est influencé, 0,6 % des points de hello sont positives, hello sont négatives. Hello dataset a été rendue disponible par Siemens de soins de santé.
  </td>
</tr>

<tr ID=crm-appetency-labels-shared>
  <td valign=top>Étiquettes de l'appétence CRM partagées</td>
  <td valign=top>
Les étiquettes de défi de prédiction de relation de client hello KDD Cup 2009 (<a href="http://www.sigkdd.org/site/2009/files/orange_small_train_appetency.labels">orange_small_train_appetency.labels</a>).
  </td>
</tr>

<tr ID=crm-churn-labels-shared>
  <td valign=top>Étiquettes de l'attrition CRM partagées</td>
  <td valign=top>
Les étiquettes de défi de prédiction de relation de client hello KDD Cup 2009 (<a href="http://www.sigkdd.org/site/2009/files/orange_small_train_churn.labels">orange_small_train_churn.labels</a>).
  </td>
</tr>

<tr ID=crm-dataset-shared>
  <td valign=top>Jeu de données CRM partagé</td>
  <td valign=top>
Ces données proviennent d’un défi de prédiction de relation de client hello KDD Cup 2009 (<a href="http://www.sigkdd.org/kdd-cup-2009-customer-relationship-prediction - orange_small_train.data.zip">orange_small_train.data.zip</a>).<p> </p>Hello dataset contient 50K clients hello entreprise de télécommunications de Français Orange. Chaque client possède 230 caractéristiques rendues anonymes, dont 190 sont numériques et 40 sont catégorielles. fonctionnalités de Hello sont très éparses.
  </td>
</tr>

<tr ID=crm-upselling-labels-shared>
  <td valign=top>Étiquettes de vente incitative CRM partagées</td>
  <td valign=top>
Les étiquettes de défi de prédiction de relation de client hello KDD Cup 2009 (<a href="http://www.sigkdd.org/site/2009/files/orange_large_train_upselling.labels">orange_large_train_upselling.labels</a>).
  </td>
</tr>

<tr>
  <td valign=top>Données sur la régression de l'efficacité énergétique</td>
  <td valign=top>
Collection de profils d'énergie simulés, basée sur 12 formes différentes de bâtiments. les bâtiments Hello sont différenciées par 8 fonctionnalités, telles que glaçage de zone, hello glaçage de distribution de la zone et l’orientation.<p> </p><b>Utilisation :</b> utiliser régression ou classification toopredict hello efficacité énergétique note comme l’une des deux réponses réel évalués. Pour la classification de multi-classes, est arrondi toohello de variable de réponse hello entière la plus proche. <p> </p><b>Recherche associée :</b> Xifara, A. &amp; Tsanas, A. (2012). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, Californie : Université de Californie, School of Information and Computer Science  </td>
</tr>

<tr ID=flight-delays-data>
  <td valign=top>Données relatives aux vols retardés</td>
  <td valign=top>
Vol de passagers à temps les données de performances provenant de hello TranStats collecte des données de hello des États-Unis Ministère des transports des États-Unis (<a href="http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time">à l’heure</a>).<p> </p>jeu de données Hello couvre hello période avril-octobre 2013. Avant de télécharger tooAzure Machine Learning Studio, hello dataset a été traité comme suit :<ul><li>Hello dataset a été filtré toocover uniquement hello 70 plus occupées aéroports aux États-Unis continentaux de hello</li><li>Les vols annulés ont été considérés comme ayant été retardés de plus de 15 minutes</li><li>Les vols déviés ont été supprimés.</li><li>Hello colonnes suivantes ont été sélectionnés : année, mois, DayofMonth, DayOfWeek, support, OriginAirportID, DestAirportID, CRSDepTime, DepDelay, DepDel15, CRSArrTime, ArrDelay, ArrDel15, annulé</li></ul>
</td>
</tr>

<tr>
  <td valign=top>Performance concernant les vols à l'heure (brutes)</td>
  <td valign=top>
Enregistrements des arrivées et départs de vols aux États-Unis à compter d’octobre 2011.<p> </p><b>Utilisation :</b> prédire les retards des vols. <p> </p><b>Recherche associée :</b> ministère du transport des États-Unis <a href="http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time">http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&amp;DB_Short_Name=On-Time</a>.
  </td>
</tr>

<tr>
  <td valign=top>Données sur les feux de forêt</td>
  <td valign=top>
Contient des données sur la météo, comme les indices de température et d'humidité et la vitesse du vent, pour une zone du nord-est du Portugal, combinées aux enregistrements des feux de forêt.<p> </p><b>Utilisation :</b> il s’agit d’une tâche difficile de régression, où hello vise toopredict hello gravé zone d’incendie de forêt. <p> </p><b>Recherche associée :</b> Cortez, P., &amp; Morais, A. (2008). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, Californie : Université de Californie, School of Information and Computer Science  <p> </p>[Cortez et Morais, 2007] P. Cortez et A. Morais. Une approche d’exploration de données tooPredict se déclenche de forêt à l’aide des données météorologiques. Aux éditions J. Neves, M. F. Santos et J. Machado éditeurs, nouvelles tendances intelligence artificielle, procédure de hello 13 EPIA 2007 - portugais conférence sur Intelligence artificielle, décembre, 523-Guimarães (Portugal), pages 512, 2007. APPIA, ISBN-13 978-989-95618-0-9. Disponible à l’adresse <a href="http://www.dsi.uminho.pt/~pcortez/fires.pdf">http://www.dsi.uminho.pt/~pcortez/fires.pdf</a>.
  </td>
</tr>

<tr ID=german-credit-card-uci-dataset>
  <td valign=top>Jeu de données d'UCI pour une carte de crédit allemande</td>
  <td valign=top>
Hello UCI Statlog (carte de crédit allemande) dataset (<a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">Statlog + allemand + crédit + données</a>), à l’aide du fichier de german.data hello.<p> </p>jeu de données Hello répartit les personnes, décrites par un ensemble d’attributs, comme les risques de crédit faible ou trop élevée. Chaque exemple représente une personne. Il existe des 20 fonctionnalités, numériques et par catégorie et une étiquette binaire (valeur de risque de crédit hello). Les entrées avec un risque de crédit élevé portent une étiquette = 2, tandis que les entrées avec un risque de crédit faible portent une étiquette = 1. Hello de classer par erreur entrées un exemple de faible risque élevé est 1, tandis que le coût de hello de classer par erreur entrées un exemple d’un risque élevé comme faible est 5.
  </td>
</tr>

<tr ID=imdb-movie-titles>
  <td valign=top>Titres de films IMDB</td>
  <td valign=top>
Hello dataset contient des informations sur les films qui ont été évalués dans Twitter tweet : IMDB film ID, nom du film, genre et année de production. Il existe K 17 films hello le jeu de données. Hello dataset a été introduite dans le livre hello « S. Dooms, T. De Pessemier et L. Martens. MovieTweetings: a Movie Rating Dataset Collected From Twitter. Workshop on Crowdsourcing and Human Computation for Recommender Systems, CrowdRec at RecSys 2013. »
  </td>
</tr>

<tr>
  <td valign=top>Données sur deux classes d'iris</td>
  <td valign=top>
Il s’agit peut-être de hello toobe de base de données plus connue trouvé dans la documentation de reconnaissance de modèle hello. jeu de données Hello est relativement faible, contenant 50 chacun des exemples de mesures pétale à partir de trois variétés d’iris.<p> </p><b>Utilisation :</b> prédire le type d’iris hello à partir des mesures hello.  <p> </p><b>Recherche associée :</b> Fisher, R.A. (1988). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, Californie : Université de Californie, School of Information and Computer Science  </td>
</tr>

<tr ID=movie-tweets>
  <td valign=top>Tweets de films</td>
  <td valign=top>
jeu de données Hello est une version étendue du jeu de données de film Tweetings hello. Hello le jeu de données a des évaluations de 170K pour les films, extraites tweet structurés sur Twitter. Chaque instance correspond à un tweet et constitue un tuple : ID utilisateur, ID IMDB, évaluation, horodatage, nombre de favoris pour ce tweet et nombre de retweets pour ce tweet. Hello dataset a été libéré par a dit S. Dooms, B. Loni et D. Tikk pour des conseils sur les systèmes de stimulation 2014.
  </td>
</tr>

<tr>
  <td valign=top>Données sur la quantité de litres au 100 pour différents véhicules automobiles</td>
  <td valign=top>
Ce jeu de données est une version légèrement modifiée du jeu de données hello fournie par la bibliothèque de StatLib hello de Carnegie Mellon University. Hello le jeu de données a été utilisé dans hello 1983 American spécifications Association statistique.<p> </p>les données de salutation répertorient la consommation de carburant pour automobiles différentes en miles par gallon, ainsi qu’avec des informations telles hello nombre de cylindres, déplacement de moteur, la puissance, poids total et l’accélération.<p> </p><b>Utilisation :</b> prédire l’économie de carburant en se basant sur 3 attributs discrets multivalués et 5 attributs continus. <p> </p><b>Recherches connexes :</b> StatLib, Carnegie Mellon University, (1993). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, Californie : Université de Californie, School of Information and Computer Science  </td>
</tr>

<tr>
  <td valign=top>Jeu de données sur la classification binaire du diabète chez les indiens Pima</td>
  <td valign=top>
Un sous-ensemble de données à partir de la base de données National Institute de diabète et appareil et NEPHROPATHIES hello. Hello dataset a été filtré toofocus sur les patients female d’héritage d’indien Pima. les données de salutation incluent des données médicales telles que glucose et niveaux d’INSULINE, ainsi que les facteurs de style de vie.<p> </p><b>Utilisation :</b> prédire si l’objet hello contient DIABÈTE (classification binaire). <p> </p><b>Recherche associée :</b> Sigillito, V. (1990). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, Californie : Université de Californie, School of Information and Computer Science  </td>
</tr>

<tr>
  <td valign=top>Données sur les clients de restaurant</td>
  <td valign=top>
Jeu de données sur les clients, comprenant des données démographiques et des préférences.<p> </p><b>Utilisation :</b> utilisent ce dataset, en association avec hello autres deux datasets restaurant, tootrain et tester un système de recommandation. <p> </p><b>Recherche associée :</b> Bache, K et Lichman, M. (2013). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, Californie : Université de Californie, School of Information and Computer Science.
  </td>
</tr>

<tr>
  <td valign=top>Données sur les caractéristiques de restaurants</td>
  <td valign=top>
Jeu de métadonnées sur des restaurants et leurs caractéristiques, comme le type de gastronomie, le style de lieu et l'emplacement.<p> </p><b>Utilisation :</b> utilisent ce dataset, en association avec hello autres deux datasets restaurant, tootrain et tester un système de recommandation. <p> </p><b>Recherche associée :</b> Bache, K et Lichman, M. (2013). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, Californie : Université de Californie, School of Information and Computer Science.
  </td>
</tr>

<tr>
  <td valign=top>Notations de restaurants</td>
  <td valign=top>
Contient des évaluations fournies par les utilisateurs toorestaurants sur une échelle de 0 too2.<p> </p><b>Utilisation :</b> utilisent ce dataset, en association avec hello autres deux datasets restaurant, tootrain et tester un système de recommandation. <p> </p><b>Recherche associée :</b> Bache, K et Lichman, M. (2013). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, Californie : Université de Californie, School of Information and Computer Science.
  </td>
</tr>

<tr>
  <td valign=top>Jeu de données multiclasse de recuit d'acier</td>
  <td valign=top>
Ce jeu de données contient une série d’enregistrements à partir de l’acier annealing des essais avec les attributs physiques de hello (largeur, épaisseur, de type (téléphone, feuille, etc.) de hello résultant acier types.<p> </p><b>Utilisation :</b> prédire un des deux attributs de classe numérique : robustesse ou force. Vous pouvez également analyser les corrélations entre attributs.<p> </p>Les qualités d'acier répondent à un standard défini par la SAE et d'autres organisations. Vous recherchez une « classe » (variable de classe hello) spécifique et que vous souhaitez les valeurs de hello toounderstand nécessaires. <p> </p><b>Recherche associée :</b> Sterling, D. &amp; Buntine, W. (NA). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, Californie : Université de Californie, School of Information and Computer Science  <p> </p>Un qualités de toosteel guide utile se trouve ici : <a href="http://www.outokumpu.com/SiteCollectionDocuments/Outokumpu-steel-grades-properties-global-standards.pdf">http://www.outokumpu.com/SiteCollectionDocuments/Outokumpu-steel-grades-properties-global-standards.pdf</a>
  </td>
</tr>

<tr>
  <td valign=top>Données sur les télescopes</td>
  <td valign=top>
Enregistrements sur les sursauts de particules gamma de haute énergie et le bruit de fond, à partir de simulations Monte Carlo.<p> </p>intention de Hello de simulation de hello a été précision de hello tooimprove au sol atmosphérique Cherenkov gamma spéciaux, à l’aide des méthodes statistiques des toodifferentiate entre le signal souhaité de hello (Cherenkov RAYONNEMENT douches) et le bruit de fond (hadronic douches initiées par rayons cosmiques dans hello supérieur atmosphère).<p> </p>Hello données a été toocreate prétraitée un cluster allonge avec axe de long hello est orientée vers le centre de caméra hello. caractéristiques Hello de cette ellipse (souvent appelés Hillas paramètres) font partie des paramètres d’image hello qui peuvent être utilisés pour la discrimination.<p> </p><b>Utilisation :</b> prédire si l’image d’une douche représente le signal ou le bruit de fond.<p> </p><b>Remarque :</b> la simple précision de la classification n’est pas significative pour ces données, car classifier un événement de bruit de fond comme événement de signal est pire que classifier un événement de signal comme événement de bruit de fond. Pour la comparaison de différents classifieurs graphique ROC hello doit être utilisé. Hello la probabilité d’acceptation d’un événement en arrière-plan comme signal doit être inférieure à un des hello suivant seuils : 0,01, 0,02, 0,05, 0,1 ou 0,2.<p> </p>Notez également que le nombre de hello d’événements de l’arrière-plan (h, pour douches hadronic) est sous-estimé, tandis que dans les mesures réels, classe h ou bruit de hello représente majorité hello d’événements. <p> </p><b>Recherche associée :</b> Bock, R.K. (1995). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, Californie : University of California, School of Information </td>
</tr>

<tr ID=weather-dataset>
  <td valign=top>Jeu de données météorologiques</td>
  <td valign=top>
Toutes les heures observations terrestres la météo de NOAA (<a href="http://cdo.ncdc.noaa.gov/qclcd_ascii/, merged data from 201304 too201310">fusionner des données à partir de too201310 201304</a>).<p> </p>les données météorologiques Hello couvrent les observations effectuées à partir de stations de météo aéroport, couvrant hello période avril-octobre 2013. Avant de télécharger tooAzure Machine Learning Studio, hello dataset a été traité comme suit :<ul><li>ID de station météorologique ont été mappés toocorresponding aéroport ID</li><li>Stations météo non associées à ceux des aéroports plus occupées hello 70 ont été filtrées</li><li>colonne de Date Hello a été divisé en colonnes d’année, mois et jour séparées</li><li>Hello colonnes suivantes ont été sélectionnés : AirportID, année, mois, jour, heure, fuseau horaire, SkyCondition, visibilité, WeatherType, DryBulbFarenheit, DryBulbCelsius, WetBulbFarenheit, WetBulbCelsius, DewPointFarenheit, DewPointCelsius, RelativeHumidity, Vitesse du vent, WindDirection, ValueForWindCharacter, StationPressure, PressureTendency, PressureChange, SeaLevelPressure, RecordType, HourlyPrecip, altimètre</li></ul>
  </td>
</tr>

<tr ID=wikipedia-sp-500-dataset>
  <td valign=top>Jeu de données Wikipedia concernant le SP 500</td>
  <td valign=top>
Les données sont extraites de Wikipédia (<a href="http://www.wikipedia.org/">http://www.wikipedia.org/</a>), notamment d’articles sur chaque société S&P 500, et sont stockées sous forme de données XML.<p> </p>Avant de télécharger tooAzure Machine Learning Studio, hello dataset a été traité comme suit :<ul><li>Extraction du contenu textuel de chaque société particulière</li><li>Suppression de la mise en forme wiki</li><li>Suppression des caractères non alphanumériques</li><li>Convertir tous les toolowercase de texte</li><li>Ajout d'autres catégories de sociétés connues</li></ul><p> </p>Notez que pour certaines sociétés un article est introuvable, nombre hello d’enregistrements est inférieur à 500.
  </td>
</tr>





<tr ID=direct-marketing>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/direct_marketing.csv">direct_marketing.csv</a></td>
  <td valign=top>
Hello dataset contient des données client et des indications relatives à leur campagne de publipostage direct tooa réponse. Chaque ligne représente un client. Hello dataset contient des 9 fonctionnalités sur les données démographiques des utilisateurs et au-delà de comportement et les colonnes d’étiquette 3 (visitez, conversion et les dépenses).  Visitez est une colonne binaire qui indique qu’un client visité après hello campagne de marketing, conversion indique un client a acheté un élément et passer est Montant hello qui a été passé.  Hello dataset a été rendue disponible par Kevin Hillstrom pour MineThatData messagerie Analytique demande et de données d’exploration de données.
  </td>
</tr>

<tr ID=lyrl2004-tokens-test>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/lyrl2004_tokens_test.csv">lyrl2004_tokens_test.csv</a></td>
  <td valign=top>
Fonctionnalités d’exemples de test de hello RCV1-V2 Reuters news dataset. jeu de données Hello a K 781 des articles d’actualité, ainsi que leurs ID (première colonne du jeu de données hello). Chaque article est tokénisé, traité et les mots vides définis. Hello dataset a été rendue disponible par David. D. Lewis.
  </td>
</tr>

<tr ID=lyrl2004-tokens-train>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/lyrl2004_tokens_train.csv">lyrl2004_tokens_train.csv</a></td>
  <td valign=top>
Fonctionnalités d’exemples d’apprentissage dans hello RCV1-V2 Reuters news dataset. jeu de données Hello a 23K des articles d’actualité, ainsi que leurs ID (première colonne du jeu de données hello). Chaque article est tokénisé, traité et les mots vides définis. Hello dataset a été rendue disponible par David. D. Lewis.
  </td>
</tr>

<tr ID=intrusion-detection>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/network_intrusion_detection.csv">network_intrusion_detection.csv</a><br></td>
  <td valign=top>
DataSet à partir de hello KDD Cup 1999 la découverte des connaissances et la concurrence d’outils d’exploration de données (<a href="http://kdd.ics.uci.edu/databases/kddcup99/kddcup99.html">kddcup99.html</a>).<p> </p>Hello dataset a été téléchargé et stocké dans le stockage d’objets Blob Azure (<a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/network_intrusion_detection.csv">network_intrusion_detection.csv</a>) et inclut l’apprentissage et le test des jeux de données. jeu de données d’apprentissage Hello a environ 126 Ko lignes et 43 colonnes, y compris les étiquettes de hello. Trois colonnes font partie des informations sur les étiquettes hello et 40 colonnes, consistant en fonctionnalités numériques et de chaîne/catégorielles, sont disponibles pour l’apprentissage du modèle de hello. les données de test Hello ont environ 22,5 K exemples avec des colonnes hello 43 même que dans les données d’apprentissage hello de test.

  </td>
</tr>

<tr ID=rcv1-v2-topics-qrels>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/rcv1-v2.topics.qrels.csv">rcv1-v2.topics.qrels.csv</a></td>
  <td valign=top>
Affectations de rubrique pour des articles d’actualité dans hello RCV1-V2 Reuters news dataset. Les rubriques tooseveral peut être attribué à un article. le format de chaque ligne Hello est «&lt;nom de la rubrique&gt; &lt;id de document&gt; 1 ». Hello dataset contient des affectations de rubrique 2.6M. Hello dataset a été rendue disponible par David. D. Lewis.
  </td>
</tr>

<tr ID=student-performance>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/student_performance.txt">student_performance.txt</a></td>
  <td valign=top>
Ces données proviennent d’hello challenge d’évaluation KDD Cup 2010 Student performance (<a href="http://www.kdd.org/kdd-cup-2010-student-performance-evaluation">évaluation des performances étudiant</a>). jeu d’apprentissage hello Algebra_2008_2009 sont Hello données utilisées (horodateur, J., Niculescu-Mizil, A., Ritter, s, Gordon, G.J. & Koedinger, K.R. (2010). Algebra I 2008-2009. Jeu de données issu du KDD Cup 2010 Educational Data Mining Challenge. Pour le trouver, accédez à <a href="http://pslcdatashop.web.cmu.edu/KDDCup/downloads.jsp">downloads.jsp</a> ou <a href="http://www.kdd.org/sites/default/files/kddcup/site/2010/files/algebra_2008_2009.zip">algebra_2008_2009.zip</a>.<p> </p>Hello dataset a été téléchargé et stocké dans le stockage d’objets Blob Azure (<a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/student_performance.txt">student_performance.txt</a>) et contient des fichiers journaux d’un étudiant cours particuliers du système. Hello fournie comprend ID du problème et son brève description, ID de l’étudiant, timestamp, et nombre de tentatives étudiant hello effectuée avant la résolution de problème hello Bonjour bonne façon. jeu de données d’origine Hello a 8,9 M enregistrements ; Ce jeu de données a été échantillonnées en bas de toohello premières lignes de 100 Ko. jeu de données Hello a 23 colonnes séparées par des tabulations de différents types : numérique, par catégorie et timestamp.

  </td>
</tr>




</table>


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
