---
title: aaaAzure Machine Learning Forum aux questions (FAQ) | Documents Microsoft
description: "Présentation d'Azure Machine Learning : FAQ portant sur la facturation, les fonctionnalités et les limitations d'un service cloud pour la modélisation prédictive rationalisée."
keywords: "introduction à l’apprentissage automatique, modélisation prédictive, présentation de l’apprentissage automatique"
services: machine-learning
documentationcenter: 
author: garyericson
manager: paulettm
editor: cgronlun
ms.assetid: a4a32a06-dbed-4727-a857-c10da774ce66
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/02/2017
ms.author: garye
ms.openlocfilehash: 3af84451dde064c3c9520ee520b541128b1eef92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-frequently-asked-questions-billing-capabilities-limitations-and-support"></a>Forum Aux Questions Azure Machine Learning : facturation, fonctionnalités, limitations et support
Voici quelques-unes des questions fréquemment posées et des réponses correspondantes sur Azure Machine Learning, un service cloud pour le développement de modèles prédictifs et la mise en œuvre de solutions via des services web. Ces forums aux questions fournissent des questions sur comment toouse hello service, qui inclut hello prise en charge, les fonctionnalités, limitations et modèle de facturation.

**Vous ne parvenez pas à trouver votre question ?**

Azure Machine Learning a un forum MSDN où les membres de la Communauté de science des données hello peuvent poser des questions sur Azure Machine Learning. équipe d’Azure Machine Learning Hello analyse forum de hello. Accédez toohello [Azure Machine Learning Forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) toosearch pour les réponses ou toopost une nouvelle question de votre choix.

## <a name="general-questions"></a>Questions générales
**Qu'est-ce que Microsoft Azure Machine Learning ?**

Azure Machine Learning est un service entièrement géré que vous pouvez utiliser toocreate, tester, fonctionner et gérez des solutions d’analyses prédictives dans le cloud de hello. À l’aide d’un simple navigateur, vous pouvez vous connecter, charger des données et commencer immédiatement des expériences d’apprentissage automatique. Grâce à la modélisation prédictive par glisser-déplacer, à une vaste palette de modules et à une bibliothèque de modèles de départ, les tâches d’apprentissage automatique les plus courantes sont simples et rapides. Pour plus d’informations, consultez hello [vue d’ensemble du service Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/). Pour en savoir plus toomachine introduction qui explique la terminologie et les concepts, consultez [tooAzure Introduction apprentissage](machine-learning-what-is-machine-learning.md).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

**Qu'est-ce que Machine Learning Studio ?**

Machine Learning Studio est un environnement de banc d’essai accessible par l’intermédiaire d’un navigateur web. Machine Learning Studio héberge une palette de modules dans une interface de composition visuelle qui vous permet de générer un bout en bout, de flux de travail de science des données sous forme de hello d’une expérience.

Pour plus d’informations sur Machine Learning Studio, consultez [Qu'est-ce que Machine Learning Studio ?](machine-learning-what-is-ml-studio.md)

**Qu’est le service de Machine Learning API hello ?**

Hello service Machine Learning API vous permet de toodeploy des modèles prédictifs, telles que celles qui sont intégrées dans Machine Learning Studio, comme les services web évolutifs et à tolérance de pannes. services web Hello hello Machine Learning API service crée sont des API REST qui fournissent une interface pour la communication entre vos modèles prédictifs analytique et les applications externes.

Pour plus d’informations, consultez [comment tooconsume un service Web de Azure Machine Learning](machine-learning-consume-web-services.md).

**Où sont répertoriés mes services web Classic ? Où sont répertoriés mes nouveaux services web (basés sur Azure Resource Manager) ?**

Les services Web créés à l’aide de hello classique web et le modèle de services de déploiement créés à l’aide du modèle de déploiement du nouveau gestionnaire de ressources Azure hello sont répertoriées dans hello [les Services Web de Microsoft Azure Machine Learning](https://services.azureml.net/) portal.

Services web classique sont également répertoriés dans [Machine Learning Studio](http://studio.azureml.net) sur hello **services Web** onglet.

## <a name="azure-machine-learning-questions"></a>Questions sur Azure Machine Learning
**Que sont les services web Azure Machine Learning ?**

Les services web Machine Learning fournissent une interface entre une application et un modèle de notation du workflow Machine Learning. Une application externe peut utiliser Azure Machine Learning toocommunicate avec un modèle de score de flux de travail Machine Learning en temps réel. Un tooa d’appel de service web Machine Learning retourne application externe de prédiction des résultats tooan. toomake un service web de tooa appel, vous passez une clé d’API qui a été créée lorsque vous avez déployé le service web de hello. Un service web Machine Learning s’appuie sur l’architecture REST, souvent choisie pour les projets de programmation web.

Azure Machine Learning propose deux types de services web :

* Service de requête-réponse (RR) : Une latence faible et service hautement évolutif qui fournit une interface toohello modèles sans état créé et déployé à l’aide de Machine Learning Studio.
* BES (Batch Execution Service) : service asynchrone qui effectue la notation d’un batch pour les enregistrements de données.

Il existe plusieurs façons de service par hello tooconsume API REST et accès web de hello. Par exemple, vous pouvez écrire une application en c#, R ou Python à l’aide des exemples de code hello est généré lorsque vous avez déployé le service web de hello.

exemple de code Hello est disponible sur :
- page de consommer Hello pour le service web de hello dans le portail de Services Web de Azure Machine Learning hello
- Hello, Page d’aide API dans le tableau de bord du service hello web dans Machine Learning Studio

Vous pouvez également utiliser le classeur Microsoft Excel d’exemple hello qui est créé pour vous et est disponible dans le tableau de bord du service hello web dans Machine Learning Studio.

**Quelles sont les tooAzure de mises à jour principal hello apprentissage ?**

Hello dernières mises à jour, consultez [quelles sont les nouveautés dans Azure Machine Learning](machine-learning-whats-new.md).

## <a name="machine-learning-studio-questions"></a>Questions sur Machine Learning Studio
### <a name="import-and-export-data-for-machine-learning"></a>Importation et exportation de données pour Machine Learning
**Quelles sources de données sont prises en charge par Machine Learning ?**

Vous pouvez télécharger des données tooa expérience Machine Learning Studio de trois façons :

- Chargement d’un fichier local en tant que jeu de données
- Utiliser une module tooimport des données à partir des services de données de cloud
- Importation d’un jeu de données enregistré à partir d’une autre expérience

toolearn en savoir plus sur les formats de fichiers, consultez [importer des données d’apprentissage dans Machine Learning Studio](machine-learning-data-science-import-data.md).

#### <a id="ModuleLimit"></a>Comment grand jeu de données hello possible pour mon modules ?
Modules dans Machine Learning Studio prend en charge les jeux de données de configuration Go too10 de données numériques pour les cas d’usage courants. Si un module accepte plusieurs entrées, hello 10 Go valeur est hello total des tailles de tous les d’entrée. Vous pouvez également échantillonner des jeux de données plus importants par le biais de requêtes Hive ou Azure SQL Database ou encore via un prétraitement Learning by Counts avant l’ingestion.  

Hello des types suivants de données peuvent développer des jeux de données toolarger lors de la normalisation de fonctionnalité et sont limité accessible sans à 10 Go :

* Partiellement alloué
* Par catégorie
* Chaînes
* Données binaires

Hello suivant modules est toodatasets limité inférieure à 10 Go :

* modules de recommandation
* Module SMOTE (Synthetic Minority Oversampling Technique)
* modules de script : R, Python, SQL
* Modules où la taille des données de sortie hello peuvent être supérieure à la taille des données d’entrée, telles que jointure ou la fonction de hachage
* La validation croisée, paramétrer des Hyperparamètres de modèle, Ordinal Regression et One-vs-All Multiclass, lorsque le nombre de hello d’itérations est très important

#### <a id="UploadLimit"></a>Quelles sont les limites de hello pour les données télécharger ?
Pour les jeux de données supérieures à deux gigaoctets, télécharger des données tooAzure stockage ou la base de données SQL Azure, ou utiliser Azure HDInsight au lieu de télécharger directement à partir d’un fichier local.

**Puis-je lire les données à partir d’Amazon S3 ?**

Si vous avez une petite quantité de données et que vous souhaitez tooexpose via une URL HTTP, puis vous pouvez utiliser hello [importer des données] [ import-data] module. Pour les grandes quantités de données, transférez-le tooAzure stockage tout d’abord et ensuite utiliser hello [importer des données] [ import-data] toobring de module dans votre expérience.
<!--

<SEE CLOUD DS PROCESS>
-->

**Existe-t-il une capacité d’entrée d’image intégrée ?**

Vous pouvez en savoir plus sur la capacité d’entrée d’image Bonjour [importer des Images] [ image-reader] référence.

### <a name="modules"></a>Modules
**algorithme de Hello, source de données, format de données ou une opération de transformation de données que je recherche n’est pas dans Azure Machine Learning Studio. Quelles sont mes options ?**

Vous pouvez accéder toohello [forum de commentaires utilisateur](http://go.microsoft.com/fwlink/?LinkId=404231) toosee fonctionnalité demande que nous surveillons. Ajoutez votre demande de vote de tooa si une fonctionnalité que vous recherchez a déjà été demandée. Si la fonction hello que vous recherchez n’existe pas, créez une nouvelle demande. Vous pouvez afficher état hello de votre demande dans ce forum, trop. Nous suivre de près cette liste et mettre à jour d’état hello de la disponibilité des fonctionnalités fréquemment. En outre, vous pouvez utiliser la prise en charge intégrée de hello pour R et Python toocreate transformations personnalisées si nécessaire.

**Puis-je importer mon code existant dans Machine Learning Studio ?**

Oui, vous pouvez importer votre code R ou Python existant dans Machine Learning Studio, exécutez-le dans hello faire des essais avec les apprenants Azure Machine Learning et déployer des solutions de hello comme un service web via Azure Machine Learning. Pour plus d’informations, voir [Prolongez votre expérience avec R](machine-learning-extend-your-experiment-with-r.md) et [Exécution des scripts d’apprentissage automatique Python dans Azure Machine Learning Studio](machine-learning-execute-python-scripts.md).

**Il est possible de toouse quelque chose comme [PMML](http://en.wikipedia.org/wiki/Predictive_Model_Markup_Language) toodefine un modèle ?**

Non. Le modèle PMML (Predictive Model Markup Language) n’est pas pris en charge. Vous pouvez utiliser R personnalisé et toodefine un module de code Python.

**Combien de modules puis-je exécuter en parallèle dans mon expérience ?**  

Vous pouvez exécuter des modules toofour en parallèle dans une expérience.

### <a name="data-processing"></a>Traitement des données
**Y a-t-il une données toovisualize de capacité (au-delà de visualisations R) interactivement au sein de l’expérience de hello ?**

Cliquez sur sortie hello d’un module toovisualize hello de données et obtenir des statistiques.

**Lors de l’aperçu des résultats ou des données dans un navigateur, nombre de hello de lignes et de colonnes est limité. Pourquoi ?**

Car de grandes quantités de données peuvent être envoyées tooa navigateur, la taille des données est limitée tooprevent ralentir Machine Learning Studio. toovisualize tous hello des résultats des données, ses meilleures toodownload hello des données et utiliser Excel ou un autre outil.

### <a name="algorithms"></a>Algorithmes
**Quels sont les algorithmes ML existants pris en charge dans Machine Learning Studio ?**

Machine Learning Studio fournit des algorithmes de pointe tels que les arbres de décision optimisés évolutifs, les systèmes de recommandation bayésiens, les réseaux neuronaux profonds et les jungles de décision développés chez Microsoft Research. Des modules d’apprentissage automatique open source évolutifs tels que Vowpal Wabbit sont également inclus. Machine Learning Studio prend en charge les algorithmes d’apprentissage automatique pour la classification, la régression et le clustering multiclasses et binaires. Consultez la liste complète des hello [Modules d’apprentissage Machine][machine-learning-modules].

**Vous suggérez automatiquement hello droite apprentissage algorithme toouse mes données ?**

Non, mais Machine Learning Studio a toocompare les résultats de hello de chaque toodetermine algorithme hello celui correspondant à votre problème de différentes manières.

**Vous disposez de toutes les instructions sur un algorithme de prélèvement vers un autre pour les algorithmes de hello fourni ?**

Consultez [comment toochoose un algorithme](machine-learning-algorithm-choice.md).

**Les algorithmes hello fournie sont écrites dans R ou Python ?**

Non, ces algorithmes sont principalement écrits langages compilés tooprovide améliore les performances.

**Sont tous les détails des algorithmes hello fournis ?**

documentation de Hello fournit des informations sur les algorithmes hello et paramètres de réglage sont algorithme de hello toooptimize décrites pour votre usage.  

**Existe-t-il une prise en charge pour l’apprentissage en ligne ?**

Non. Actuellement, seul le recyclage par programme est pris en charge.

**Puis-je visualiser les couches de hello d’un modèle de réseau neuronal à l’aide du module intégré de hello ?**

Non.

**Puis-je créer mes propres modules en C# ou un autre langage ?**

Actuellement, vous pouvez uniquement utiliser R toocreate nouvelle des modules personnalisés.

### <a name="r-module"></a>Module R
**Quels packages R sont disponibles dans Machine Learning Studio ?**

Machine Learning Studio prend en charge plus de 400 des packages CRAN R aujourd'hui et Voici hello [liste actuelle](http://az754797.vo.msecnd.net/docs/RPackages.xlsx) de tous les inclus les packages. Consultez également [étendre votre expérience avec R](machine-learning-extend-your-experiment-with-r.md) toolearn comment tooretrieve cette liste vous-même. Si le package hello n’est pas dans cette liste, fournir le nom hello du package hello en hello [forum de commentaires utilisateur](http://go.microsoft.com/fwlink/?LinkId=404231).

**Il est possible toobuild un R personnalisé module ?**

Oui. Consultez [Créer des modules R personnalisés dans Microsoft Azure Machine Learning](machine-learning-custom-r-modules.md) pour plus d’informations.

**Existe-t-il un environnement REPL pour R ?**

Non, il n’existe aucun environnement en lecture-Eval-Print-Loop (REPL) pour R dans studio de hello.

### <a name="python-module"></a>Module Python
**Il est possible toobuild un module Python personnalisé ?**

Pas actuellement, mais vous pouvez utiliser un ou plusieurs [Execute Python Script] [ python] tooget de modules hello même résultat.

**Existe-t-il un environnement REPL pour Python ?**

Vous pouvez utiliser hello Notebook portables dans Machine Learning Studio. Pour plus d’informations, voir [Introducing Jupyter Notebooks in Azure Machine Learning Studio](http://blogs.technet.com/b/machinelearning/archive/2015/07/24/introducing-jupyter-notebooks-in-azure-ml-studio.aspx)(Présentation des notebooks Jupyter dans Azure Machine Learning Studio).

## <a name="web-service"></a>Service Web
### <a name="retrain"></a>Recyclage
**Comment recycler des modèles Azure Machine Learning par programme ?**

Utilisez hello réapprentissage API. Pour plus d'informations, consultez la page [Reformation des modèles Machine Learning par programme](machine-learning-retrain-models-programmatically.md). Exemple de code est également disponible dans hello [démonstration de recyclage de Microsoft Azure Machine Learning](https://azuremlretrain.codeplex.com/).

### <a name="create"></a>Créer
**Puis-je déployer des modèles de hello localement ou dans une application qui ne dispose d’une connexion Internet ?**

Non.

**Existe-t-il une latence de référence attendue pour tous les services Web ?**

Consultez hello [limites de l’abonnement Azure](../azure-subscription-service-limits.md).

### <a name="use"></a>Utilisation
**Lorsque voudrais-je toorun mon modèle prédictif en tant que l’exécution par lots service par rapport à un service de réponse à la demande ?**

Hello service de réponse à la demande (RR) est une latence faible, de modèles de service à grande échelle web tooprovide utilisé un toostateless d’interface qui sont créés et déployés à partir de l’environnement d’expérimentation hello. Hello, le service de l’exécution par lots (BES) est un service qui évalue de façon asynchrone un lot d’enregistrements de données. Hello d’entrée pour BES est comme entrée de données qui utilise des enregistrements de ressources. Hello principale différence est que BES lit un bloc d’enregistrements à partir de diverses sources, telles que le stockage d’objets Blob Azure, stockage de Table Azure, base de données SQL Azure, HDInsight (requête hive) et des sources de HTTP. Pour plus d’informations, consultez [comment tooconsume un service Web de Azure Machine Learning](machine-learning-consume-web-services.md).

**Comment mettre à jour le modèle hello pour le service web de hello déployé ?**

tooupdate un modèle de prévision pour un service déjà déployé, modifier et réexécuter l’expérience hello que vous avez utilisé tooauthor et enregistrer le modèle formé de hello. Une fois que vous avez une nouvelle version du modèle formé hello disponible, la Machine Learning Studio vous demande si vous voulez tooupdate votre service web. Pour plus d’informations sur la façon tooupdate un service web déployé, consultez [déployer un service web de Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

Vous pouvez également utiliser hello Retraining API.
Pour plus d'informations, consultez la page [Reformation des modèles Machine Learning par programme](machine-learning-retrain-models-programmatically.md). Exemple de code est également disponible dans hello [démonstration de recyclage de Microsoft Azure Machine Learning](https://azuremlretrain.codeplex.com/).

**Comment puis-je surveiller mon service web déployé en production ?**

Après avoir déployé un modèle de prévision, vous pouvez le surveiller à partir de hello Azure classic portail (services web standard uniquement) ou le portail de Services Web de Azure Machine Learning de hello. Chaque service déployé dispose de son propre tableau de bord, à partir duquel vous pouvez consulter les informations de surveillance correspondant à ce service. Pour plus d’informations sur comment toomanage vos services web déployés, consultez [gérer un service Web à l’aide du portail de Services Web de Azure Machine Learning hello](machine-learning-manage-new-webservice.md) et [gérer un espace de travail Azure Machine Learning](machine-learning-manage-workspace.md).

**Existe-t-il un endroit où je peux voir sortie hello de mon RR/BES ?**

Pour les enregistrements de ressources, réponse du service web hello est généralement où vous voyez les résultats hello. Vous pouvez également écrire tooAzure stockage d’objets Blob. BES, hello sont affichées tooa blob par défaut. Vous pouvez également écrire la base de données tooa hello sortie ou une table à l’aide de hello [exporter les données] [ export-data] module.

**Puis-je créer des services web uniquement à partir de modèles générés dans Machine Learning Studio ?**

Non. Vous pouvez également créer des services web directement à partir de Jupyter Notebooks et RStudio.

**Où puis-je trouver plus d'informations sur les codes d'erreur ?**

Pour obtenir la liste des codes d’erreur et leur description, voir [Machine Learning Module Error Codes](https://msdn.microsoft.com/library/azure/dn905910.aspx) (Codes d’erreur des modules Machine Learning).

## <a name="scalability"></a>Extensibilité
**Quelle est l’évolutivité de hello du service web de hello ?**

Actuellement, le point de terminaison par défaut hello est configurée avec 20 requêtes RR simultanées par point de terminaison. Vous pouvez faire évoluer cette too200 de requêtes simultanées par point de terminaison, et vous pouvez faire évoluer chaque too10 de service web, des points de terminaison 000 par le service web comme décrit dans [mise à l’échelle un Service Web](machine-learning-scaling-webservice.md). Pour BES, chaque point de terminaison permet de traiter 40 demandes simultanées. Au-delà, les demandes supplémentaires sont mises en file d’attente. Ces requêtes en file d’attente d’identification automatiquement s’échappe de file d’attente hello.

**Les travaux R sont-ils répartis entre les nœuds ?**

Non.  

**Quelle quantité de données puis-je utiliser pour l'apprentissage ?**

Modules dans Machine Learning Studio prend en charge les jeux de données de configuration Go too10 de données numériques pour les cas d’usage courants. Si un module accepte plusieurs hello d’entrée, total taille pour toutes les entrées est de 10 Go. Vous pouvez également échantillonner des jeux de données plus importants par le biais de requêtes Hive ou Azure SQL Database, ou encore par l’intermédiaire d’un prétraitement avec des modules [Learning with Counts][counts] avant l’ingestion.  

Hello des types suivants de données peuvent développer des jeux de données toolarger lors de la normalisation de fonctionnalité et sont limité accessible sans à 10 Go :

* Partiellement alloué
* Par catégorie
* Chaînes
* Données binaires

Hello suivant modules est toodatasets limité inférieure à 10 Go :

* modules de recommandation
* Module SMOTE (Synthetic Minority Oversampling Technique)
* modules de script : R, Python, SQL
* Modules où la taille des données de sortie hello peuvent être supérieure à la taille des données d’entrée, telles que jointure ou la fonction de hachage
* Validation croisée, réglage des hyperparamètres de modèle, régression ordinale et plusieurs classes de un contre tous, lorsque le nombre d’itérations est très élevé

Pour les jeux de données qui sont plus de quelques gigaoctets, télécharger des données tooAzure stockage ou la base de données SQL Azure, ou utiliser HDInsight au lieu de télécharger directement à partir d’un fichier local.

**Existe-t-il des limitations de taille de vecteurs ?**

Lignes et colonnes sont chaque limitation de .NET toohello limitée de Max Int : 2 147 483 647.

**Puis-je ajuster taille hello de machine virtuelle hello qui exécute le service web de hello ?**

Non.  

## <a name="security-and-availability"></a>Sécurité et disponibilité
**Qui peut accéder au point de terminaison http hello pour le service web de hello par défaut ? Comment restreindre l’accès toohello point de terminaison ?**

Après le déploiement d’un service web, un point de terminaison par défaut est créé pour ce service. point de terminaison par défaut Hello peut être appelée à l’aide de sa clé d’API. Vous pouvez ajouter que plusieurs points de terminaison avec leurs propres clés de hello portail Azure classic ou par programme à l’aide de hello API de gestion des services Web. Clés d’accès sont nécessaires toomake appels de service web de toohello. Pour plus d’informations, consultez [comment tooconsume un service Web de Azure Machine Learning](machine-learning-consume-web-services.md).

**Que se passe-t-il si mon compte de stockage Azure est introuvable ?**

Machine Learning Studio s’appuie sur le stockage Azure fourni par l’utilisateur compte toosave intermédiaires de données lorsqu’il exécute le flux de travail hello. Ce compte de stockage est fourni tooMachine Learning Studio lors de la création d’un espace de travail. Après avoir hello, espace de travail est créé, si le compte de stockage hello est supprimé et ne sont plus accessibles, espace de travail hello cesseront de fonctionner, et toutes les expérimentations dans que l’espace de travail échoue.

Si vous avez supprimé par inadvertance le compte de stockage hello, recréez le compte de stockage hello hello même nom Bonjour même région que hello supprimé le compte de stockage. Après cela, resync clé d’accès hello.

**Que se passe-t-il si ma clé d’accès au compte de stockage n’est pas synchronisée ?**

Machine Learning Studio s’appuie sur le stockage Azure fourni par l’utilisateur compte toostore intermédiaires de données lorsqu’il exécute le flux de travail hello. Ce compte de stockage est fourni tooMachine Learning Studio lorsqu’un espace de travail est créé, et les clés d’accès hello sont associés à cet espace de travail. Si les clés d’accès hello sont modifiées après la création d’espace de travail hello, espace de travail hello ne peut plus accéder compte de stockage hello. Il cessera de fonctionner, et toutes les expériences dans cet espace de travail échoueront.

Si vous avez modifié les clés d’accès de compte de stockage, la resynchronisation hello les clés d’accès dans l’espace de travail à l’aide de hello hello portail Azure classic.  

## <a name="support-and-training"></a>Support et formations
**Où puis-je obtenir des formations pour Azure Machine Learning ?**

Hello [centre de Documentation Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) héberge les didacticiels vidéo et tooguides de procédure. Ces guides pas à pas introduisent des services de hello et expliquent hello cycle de vie du science des données de l’importation de données, nettoyage des données, créer des modèles de prévision et les déployer en production à l’aide d’Azure Machine Learning.

Nous ajoutons toohello matériel nouveau centre d’apprentissage Machine en continu. Vous pouvez soumettre des demandes pour les documents de formation supplémentaires sur le centre d’apprentissage Machine à hello [forum de commentaires utilisateur](https://windowsazure.uservoice.com/forums/257792-machine-learning).

Vous pouvez également rechercher des formations sur [Microsoft Virtual Academy](http://www.microsoftvirtualacademy.com/training-courses/getting-started-with-microsoft-azure-machine-learning).

**Comment puis-je bénéficier d’un support pour Azure Machine Learning ?**

tooget le support technique pour Azure Machine Learning, consultez trop[Azure prend en charge](/support/options/), puis sélectionnez **Machine Learning**.

Azure Machine Learning dispose également d’un forum communautaire sur MSDN, où vous pouvez poser des questions en rapport avec Azure Machine Learning. équipe d’Azure Machine Learning Hello analyse forum de hello. Accédez trop[Forum Azure](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning).

## <a name="billing-questions"></a>Questions sur la facturation
**Comment fonctionne la facturation dans Machine Learning ?**

Azure Machine Learning possède deux composants : Machine Learning Studio et les services web Machine Learning.

Lorsque vous évaluez Machine Learning Studio, vous pouvez utiliser la facturation gratuit hello. niveau gratuit de Hello vous permet également de déployer un service web classique a une capacité limitée.

Si vous décidez que Azure Machine Learning répond à vos besoins, vous pouvez inscrire hello niveau Standard. toosign haut, vous devez disposer d’un abonnement Microsoft Azure.

Niveau Standard de hello, vous êtes facturé chaque mois pour chaque espace de travail que vous définissez dans Machine Learning Studio. Lorsque vous exécutez une expérience dans studio de hello, vous êtes facturé pour les ressources de calcul lorsque vous exécutez une expérience. Lorsque vous déployez un service web standard, les transactions et les heures sont facturées selon le paiement hello de calcul.

Les nouveaux services web (qui s’appuient sur Azure Resource Manager) incluent des profils de facturation qui offrent une plus grande prévisibilité des coûts. À plusieurs niveaux de tarification offre toocustomers tarif qui ont besoin d’une grande quantité de capacité.

Lorsque vous créez un plan, vous validez tooa coût est fourni avec une quantité incluse des heures de calcul des API et les transactions des API fixé. Si vous avez besoin de plus de quantités incluses, vous pouvez ajouter des instances tooyour plan. Si vous avez besoin de beaucoup plus de quantités incluses, vous pouvez choisir un plan de niveau supérieur qui en offre davantage à un meilleur tarif.

Une fois hello quantités incluses dans les instances existantes sont utilisées, l’utilisation supplémentaire est facturée au taux de dépassement de hello associé avec le niveau de plan de facturation hello.

> [!NOTE]
Quantités incluses sont réaffectées tous les 30 jours et quantités incluses inutilisées ne réapparaissent pas toohello période suivante.

Pour plus d’informations sur la facturation et la tarification, consultez [Tarification Machine Learning](https://azure.microsoft.com/pricing/details/machine-learning/).

**Une version d’évaluation de Machine Learning est-elle disponible ?**

 Azure Machine Learning dispose d’une option d’abonnement gratuit qui est expliquée dans [Tarification de Machine Learning](https://azure.microsoft.com/pricing/details/machine-learning/). Machine Learning Studio a une version d’évaluation de huit heures évaluation qui est disponible lorsque vous vous connectez trop[Machine Learning Studio](https://studio.azureml.net/?selectAccess=true&o=2).

 En outre, lorsque vous vous inscrivez pour une version d’évaluation gratuite d’Azure, vous pouvez essayer n’importe quel service Azure pendant un mois. toolearn en savoir plus sur hello évaluation gratuite d’Azure, visitez [FAQ sur l’essai gratuit Azure](https://azure.microsoft.com/pricing/free-trial-faq/).

**Qu’est-ce qu’une transaction ?**

Une transaction correspond à un appel d’API pris en charge par Azure Machine Learning. Les transactions provenant d’appels de service de requête-réponse (RRS) et de service d’exécution de lots (BES) sont regroupées et facturées selon votre profil de facturation.

**Puis-je utiliser les quantités de transactions hello inclus dans un plan pour les transactions de RR et BES ?**

Oui, les transactions de vos RRS et BES sont regroupées et facturées selon votre profil de facturation.

**Qu’est-ce qu’une heure de calcul API ?**

Une heure de calcul des API est une unité de facturation de hello pour fois hello toorun de prendre les appels API à l’aide d’apprentissage des ressources de calcul. Tous vos appels sont regroupés pour la facturation.

**Combien de temps prend un appel d’API de production type ?**

Les durées d’appel API de production peuvent varier considérablement, généralement des centaines de millisecondes tooa allant de quelques secondes. Certains appels d’API peuvent nécessiter des minutes selon la complexité hello de hello le traitement des données et du modèle de l’apprentissage automatique. Hello meilleure manière tooestimate API de production appel est toobenchmark un modèle sur hello service Machine Learning.

**Qu’est-ce qu’une heure de calcul Studio ?**

Une heure de calcul Studio est l’unité de facturation de hello pour le temps de l’agrégat hello que vos expériences utilisent des ressources de calcul dans studio.

**Dans les nouveaux services web (basé sur Azure Resource Manager), couche de développement/Test hello signification pour ?**

Services web basés sur le Gestionnaire de ressources fournissent plusieurs niveaux que vous pouvez utiliser tooprovision votre plan de facturation. Hello niveau tarifaire de développement/Test fournit des quantités incluses limitées qui vous permettent de tootest votre expérience comme un service web sans encourir de frais. Vous avez toosee d’opportunité hello son fonctionnement.

**Existe-t-il des frais distincts pour le stockage ?**

Hello Machine Learning gratuit ne requièrent pas ou n’autoriser le stockage distinct. couche de Machine Learning Standard Hello requiert les utilisateurs toohave un compte de stockage Azure. Le stockage Azure est [facturé séparément](https://azure.microsoft.com/pricing/details/storage/).

**Machine Learning prend-il en charge la disponibilité élevée ?**

Oui. Pour plus d’informations, consultez [tarification de Machine Learning](https://azure.microsoft.com/en-us/pricing/details/machine-learning/) pour obtenir une description de contrat de niveau de service (SLA) hello.

**Sur quel type de ressources de calcul mes appels d’API de production seront-ils exécutés ?**

Hello service Machine Learning est un service partagé. Les ressources de calcul réel qui sont utilisés sur le back-end hello varient et sont optimisés pour les performances et la prévisibilité.

### <a name="management-of-new-resource-manager-based-web-services"></a>Gestion de nouveaux services web (basés sur Azure Resource Manager)
**Que se passe-t-il si je supprime mon profil ?**

plan de Hello est supprimé de votre abonnement, et vous êtes facturé au prorata à l’usage.

> [!NOTE]
Vous ne pouvez pas supprimer un plan utilisé par un service web. plan de hello toodelete, vous devez soit attribuer un nouveau plan de service web de toohello ou de supprimer le service web de hello.

**Qu’est-ce qu’une instance de plan ?**

Une instance de plan est une unité de quantités incluses, que vous pouvez ajouter tooyour plan de facturation. Lorsque vous sélectionnez un niveau de facturation pour votre profil de facturation, il contient une seule instance. Si vous avez besoin de plus de quantités incluses, vous pouvez ajouter des instances de hello sélectionné couche tooyour facturation.

**Combien d’instances de plan puis-je ajouter ?**

Vous pouvez avoir une seule instance de niveau de tarification de développement/Test hello dans un abonnement.

Par contre, pour les niveaux Standard S1, Standard S2 et Standard S3, vous pouvez en ajouter autant que nécessaire.

> [!NOTE]
En fonction de votre utilisation anticipée, il peut être plus rentable tooupgrade tooa niveau qui a utilisé plus de quantités plutôt que d’ajouter le niveau actuel de toohello instances.

**Que se passe-t-il lorsque je change de niveau de plan (et que je passe à un niveau supérieur/inférieur) ?**

plan de Hello ancien est supprimé et l’utilisation actuelle de hello est facturée prorata. Un nouveau plan avec des quantités inclus de hello complète du niveau de mise à niveau/rétrogradé hello est créé pour reste hello de période de hello.

> [!NOTE]
Les quantités incluses sont allouées par période et les quantités non utilisées ne sont pas reportées.

**Que se passe-t-il lorsque j’augmenter les instances de hello dans un plan de ?**

Quantités sont incluses prorata et peuvent prendre 24 heures toobe efficace.

**Que se passe-t-il lorsque je supprime une instance d’un profil ?**

instance de Hello est supprimé de votre abonnement, et vous êtes facturé au prorata à l’usage.

### <a name="sign-up-for-new-resource-manager-based-web-services-plans"></a>Inscription à de nouveaux services web (basés sur Azure Resource Manager)
**Comment s’inscrire à un plan ?**

Vous avez deux plans de facturation toocreate façons.

Lorsque vous déployez un nouveau service web basé sur Azure Resource Manager pour la première fois, vous pouvez choisir un plan existant ou en créer un.

Les plans que vous créez de cette manière sont dans votre région par défaut, et votre service web sera déployé toothat région.

Si vous souhaitez toodeploy services tooregions autre que votre région par défaut, vous souhaiterez toodefine vos plans de facturation avant de déployer votre service.

Dans ce cas, vous pouvez vous connecter dans le portail de Services Web de Azure Machine Learning toohello et passer des toohello Plans de page. Vous pourrez alors ajouter et supprimer des plans, mais aussi modifier des plans existants.

**Quel est le plan choisir toostart off avec ?**

Nous vous recommandons que vous démarrez avec hello Standard S1 niveau et surveillez votre service à l’usage. Si vous trouvez que vous utilisez votre quantités incluses rapidement, vous pouvez ajouter des instances ou déplacer le niveau supérieur de tooa et obtenir mieux les tarifs réduits. Vous pouvez ajuster votre profil de facturation en fonction de vos besoins tout au long de votre cycle de facturation.

**Les régions sont disponibles dans les nouveaux plans de hello ?**

les nouveaux plans de facturation Hello sont disponibles dans trois régions production hello, dans laquelle nous prenons en charge les nouveaux services web de hello :

* Centre-Sud des États-Unis
* Europe de l'Ouest
* Asie du Sud-Est

**J’ai des services web dans plusieurs régions. Dois-je avoir un profil pour chaque région ?**

Oui. La tarification des profils varie selon les régions. Lorsque vous déployez une région tooanother du service web, vous devez tooassign informatique un plan qui est la région toothat spécifique. Pour plus d’informations, consultez [Disponibilité des produits par région]( https://azure.microsoft.com/regions/services/).

### <a name="new-web-services-overages"></a>Nouveaux services web : dépassements
**Comment vérifier si mon utilisation du service web est en dépassement ?**

Vous pouvez afficher l’utilisation de hello sur tous les plans de votre page de Plans hello dans le portail de Services Web de Azure Machine Learning hello. Connectez-vous au portail de toohello, puis cliquez sur hello **Plans** option de menu.

Bonjour **Transactions** et **de calcul** colonnes de table de hello, vous pouvez voir les quantités hello inclus de plan de hello et pourcentage d’utilisation de hello.

**Que se passe-t-il lorsque j’utilise des hello inclure les quantités dans le niveau de tarification de développement/Test hello ?**

Services qui ont un développement/Test tarification niveau affecté toothem sont arrêtés jusqu'à ce que hello période suivant ou jusqu'à ce que vous les déplacez tooa payé couche.

**Pour les services web Classic et les dépassements des nouveaux services web (basés sur Azure Resource Manager), comment sont calculés les tarifs pour les charges de travail RRS et BES ?**

Pour une charge de travail des enregistrements de ressources, vous êtes facturé pour chaque appel d’API de transaction que vous apportez et temps de calcul hello qui est associée à ces demandes. Les coûts de transaction RR production API sont calculées comme hello le nombre total d’appels d’API que vous apportez multiplié par prix hello par 1 000 transactions (proratisée par transaction individuelle). Vos coûts de heures de calcul API de production API des enregistrements de ressources sont calculées en tant que durée hello requis pour chaque toorun appel d’API, multiplié par hello le nombre total de transactions des API, multipliée par prix hello par heure de calcul API de production.

Par exemple, pour dépassement Standard S1, 1 000 000 transactions des API qui prennent des secondes 0,72 chaque toorun entraînerait (1 000 000 * 0,50 $/ 1K transactions des API) de 500 $ de coûts de l’API de production et (1 000 000 * 0,72 s * $2 / h) $400 dans le calcul de l’API de production heures, pour un total de 900 $.

Pour une charge de travail BES, vous êtes facturé Bonjour même manière. Toutefois, les coûts de transaction hello API représentent le nombre hello de traitements que vous envoyez et coûts de calcul hello représentent le temps de calcul hello qui est associée à ces traitements par lots. Les coûts de transaction BES production API sont calculées comme le nombre total de hello soumis multipliée par prix hello par 1 000 transactions (proratisée par transaction individuelle). Vos coûts de heures de calcul API de production BES API sont calculées en tant que durée hello requise pour chaque ligne dans votre toorun travail multiplié par hello le nombre total de lignes dans votre travail multiplié par hello le nombre total de travaux multipliée par prix hello par l’API de production heures de calcul. Lorsque vous utilisez hello calculatrice d’apprentissage, hello transaction compteur représente hello nombre de tâches que vous envisagez de toosubmit et champ de temps par transaction hello représente hello combinées temps suffisant pour toutes les lignes dans chaque toorun de travail.

Par exemple, supposons que vous dépassez le niveau Standard S1 et que vous envoyez 100 tâches par jour, ce qui correspond à 500 lignes qui prennent 0,72 seconde chacune. Le coût mensuel de votre dépassement est le suivant : (100 travaux par jour = 3 100 travaux par mois * 0,50 $/1 000 transactions API), soit 1,55 $ en coût de transaction API de production et (500 lignes * 0,72 s * 3 100 travaux * 2 $/h), soit 620 $ en heures de calcul API de production, pour un total de 621,55 $.

### <a name="azure-machine-learning-classic-web-services"></a>Services web Azure Machine Learning
**Le paiement à l’utilisation est-il toujours disponible ?**

Oui. Les services web Classic sont toujours disponibles dans Azure Machine Learning.  

### <a name="azure-machine-learning-free-and-standard-tier"></a>Niveaux Gratuit et Standard d’Azure Machine Learning
**Ce qui est inclus dans hello Azure Machine Learning gratuit ?**

Bonjour Azure Machine Learning gratuit est prévue tooprovide un toohello de présentation approfondie Azure Machine Learning Studio. Il vous suffit est un toosign de compte Microsoft. niveau gratuit Hello inclut un accès gratuit tooone Azure Machine Learning Studio espace de travail [compte Microsoft](https://www.microsoft.com/account/default.aspx). Dans ce niveau, vous pouvez utiliser des too10 les Go de stockage et opérationnaliser les modèles en tant que l’API de mise en lots. Les charges de travail du niveau Gratuit ne sont couvertes par aucun contrat de niveau de service et sont uniquement destinées au développement et à une utilisation personnelle. 

Espaces de travail de niveau gratuit ont hello limites suivantes :

* Les charges de travail ne peut pas accéder aux données en vous connectant serveur tooan local qui exécute SQL Server.
* Vous ne pouvez pas déployer de nouveaux services web basés sur Resource Manager.


**Ce qui est inclus dans les plans et le niveau d’Azure Machine Learning Standard hello ?**

niveau d’Azure Machine Learning Standard Hello est une version de production payante de Azure Machine Learning Studio. Bonjour Azure Machine Learning Studio mensuel est facturé sur une base de mois par espace de travail par et au prorata pour les mois partiels. Les heures d’expérience Azure Machine Learning Studio sont facturées par heure de calcul pour l’expérience active. La facturation est ajustée pour les heures incomplètes.  

Hello service Azure Machine Learning API est facturé selon s’il s’agit d’un service web de classique ou un service web (basé sur le Gestionnaire de ressources).

Hello suivant frais est agrégée par espace de travail pour votre abonnement.

* Abonnement d’espace de travail machine Learning : hello abonnement d’espace de travail Machine Learning est frais mensuels qui fournit l’espace de travail access tooa Machine Learning Studio. l’abonnement Hello est expériences toorun requis dans hello studio tooutilize hello production et API.
* Heures d’expérience Studio : ce compteur regroupe tous les frais de calcul qui sont alloués en exécutant des expériences dans Machine Learning Studio et d’appels d’API de production en cours d’exécution dans l’environnement intermédiaire de hello.
* Accéder aux données par la connexion serveur tooan local qui exécute SQL Server dans les modèles à la formation et le score.
* Pour les services web Classic :
  * Heures de calcul API de production : ce compteur inclut les frais de calcul cumulés par les services web exécutés en production.
  * Transactions de production API (pour 1 000) : ce compteur inclut les frais qui sont alloués par le service web de production de tooyour appel.

Outre hello précédant les frais, dans les cas de hello du service de gestionnaire de ressources du site web, les frais sont agrégées toohello le plan sélectionné :

* Standard S1/S2/S3 API Plan (unités) : Ce compteur représente type hello d’instance qui est sélectionné pour les services web basés sur le Gestionnaire de ressources.
* Standard S1/S2/S3 dépassement heures de calcul API : Ce compteur inclut les frais de calcul qui sont alloués par le Gestionnaire de ressources des services qui s’exécutent en production après que les quantités hello inclus dans les instances existantes sont utilisées. l’utilisation de Hello supplémentaire est facturée aux hello overate taux a associé à un niveau de plan S1/S2/S3.
* Transactions des API standard S1/S2/S3 dépassement (en 1 000) : ce compteur inclut les frais qui sont alloués par la production de tooyour d’appel de service web basé sur le Gestionnaire de ressources hello incluses quantités dans les instances existantes soient utilisés. l’utilisation supplémentaire Hello est facturée au hello overate taux associé au niveau du plan S1/S2/S3.
* Heures de calcul des API quantité incluses : Avec les services web basés sur le Gestionnaire de ressources, ce compteur représente quantité hello inclus des heures de calcul des API.
* Inclure les Transactions des API quantité (de 1 000) : avec le Gestionnaire de ressources des services, ce compteur représente la quantité de hello inclus de transactions des API.

**Comment s’inscrire au niveau Gratuit d’Azure Machine Learning ?**

Vous avez besoin uniquement d'un compte Microsoft. Accédez trop[accueil d’Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/), puis cliquez sur **Démarrer maintenant**. Connectez-vous à votre compte Microsoft. Un espace de travail de niveau Gratuit est alors créé pour vous. Vous pouvez démarrer tooexplore et créer des expériences d’apprentissage immédiatement.

**Comment s’inscrire au niveau Standard d’Azure Machine Learning ?**

Vous devez avoir accès tooan abonnement Azure toocreate un espace de travail Standard Machine Learning. Vous pouvez souscrire un abonnement de Azure de version d’évaluation gratuit de 30 jours et tooa de mise à niveau ultérieure payé abonnement Azure, ou vous pouvez acheter un abonnement Azure payant ferme. Vous pouvez ensuite créer un espace de travail Machine Learning à partir du portail classique de Microsoft Azure hello après avoir accès toohello abonnement. Hello de vue [obtenir des instructions pas à pas](https://azure.microsoft.com/trial/get-started-machine-learning-b/).

Vous pouvez également invité par espace de travail de Standard Machine Learning propriétaire tooaccess hello propriétaire de l’espace.

**Puis-je spécifier mon propre toouse de compte de stockage Blob Azure avec gratuit hello ?**

Non, le niveau Standard de hello est version toohello équivalent de hello service Machine Learning qui était disponible avant hello niveaux ont été introduites.

**Puis-je déployer mon d’apprentissage des modèles comme les API de niveau gratuit de hello ?**

Oui, vous pouvez tiens apprentissage des modèles dans le cadre de niveau gratuit de hello toostaging API services. tooput hello du service de l’API de mise en lots en production et obtenir un point de terminaison de production hello mis service, vous devez utiliser le niveau Standard de hello.

**Qu’est la différence hello évaluation gratuite d’Azure et Azure Machine Learning gratuit ?**

Hello [version d’évaluation gratuite de Microsoft Azure](https://azure.microsoft.com/free/) offre de service crédits que vous pouvez appliquer tooany Azure pendant un mois. offres couche Hello Azure Machine Learning libre continue accéder spécifiquement tooAzure Machine Learning pour les charges de travail hors production.

**Comment déplacer une expérience de niveau Standard de hello gratuit toohello ?**

toocopy vos expériences de niveau Standard de hello gratuit toohello :

1. Connectez-vous à tooAzure Machine Learning Studio, puis assurez-vous que vous pouvez voir d’espace de travail gratuit hello et espace de travail Standard hello dans le sélecteur d’espace de travail hello dans la barre de navigation supérieure hello.
2. Basculer l’espace de travail tooFree si vous êtes dans l’espace de travail Standard hello.
3. Dans la vue de liste hello expérience, sélectionnez une expérience que vous feriez comme toocopy, puis cliquez sur hello **copie** bouton de commande.
4. Sélectionnez l’espace de travail hello Standard à partir de la boîte de dialogue hello qui s’ouvre, puis cliquez sur hello **copie** bouton.
   Tous les hello datasets associés, modèle formé, etc. sont copiés avec l’expérience hello dans l’espace de travail Standard hello.
5. Vous devez toorerun hello expérience et republiez votre service web dans l’espace de travail Standard hello.

### <a name="studio-workspace"></a>Espace de travail Studio
**Y a-t-il différentes factures pour différents espaces de travail ?**

Les frais liés à l’espace de travail sont décomposés pour chaque compteur applicable sur une seule facture.

**Sur quel type de ressources de calcul mes expériences seront-elles exécutées ?**

Hello service Machine Learning est un service partagé. Les ressources de calcul réel qui sont utilisés sur le back-end hello varient et sont optimisés pour les performances et la prévisibilité.

### <a name="guest-access"></a>Accès invité
**Quelle est l’accès des invités tooAzure Machine Learning Studio ?**

L’accès invité offre une expérience d’évaluation limitée. Vous pouvez créer et exécuter des expériences dans Azure Machine Learning Studio sans frais et sans authentification. Sessions Invité sont non persistants (ne peut pas être enregistré) et le nombre d’heures de tooeight limité. Elles sont assorties d’autres limitations comme l’absence de prise en charge des langages R et Python, l’absence d’API intermédiaires et une taille de jeu de données et une capacité de stockage limitées. En comparaison, les utilisateurs qui choisissent toosign avec un compte Microsoft ont un accès complet toohello gratuit de Machine Learning Studio qui est décrit précédemment, qui inclut un espace de travail persistant et de fonctionnalités plus complètes. toochoose votre apprentissage libre expérience, cliquez sur **prise en main** sur [https://studio.azureml.net](https://studio.azureml.net), puis sélectionnez **accès invités** ou connectez-vous avec Microsoft compte.

<!-- Module References -->
[image-reader]: https://msdn.microsoft.com/library/azure/893f8c57-1d36-456d-a47b-d29ae67f5d84/
[join]: https://msdn.microsoft.com/library/azure/124865f7-e901-4656-adac-f4cb08248099/
[machine-learning-modules]: https://msdn.microsoft.com/library/azure/6d9e2516-1343-4859-a3dc-9673ccec9edc/
[partition-and-sample]: https://msdn.microsoft.com/library/azure/a8726e34-1b3e-4515-b59a-3e4a475654b8/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[export-data]: https://msdn.microsoft.com/library/azure/7A391181-B6A7-4AD4-B82D-E419C0D6522C
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[python]: https://msdn.microsoft.com/library/azure/CDB56F95-7F4C-404D-BDE7-5BB972E6F232
[counts]: https://msdn.microsoft.com/library/azure/dn913056.aspx
