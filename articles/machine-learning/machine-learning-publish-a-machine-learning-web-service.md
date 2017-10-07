---
title: aaaDeploy service web Machine Learning | Documents Microsoft
description: "Comment tooconvert une formation expérimenter l’expérience de prédictive tooa, préparer pour le déploiement, puis le déployer en tant qu’un service web Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 73a3e9c6-00d0-41d4-8cf1-2ec87713867e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: garye
ms.openlocfilehash: 9cb7af637632b2c3688c11483f29cf24df8fd065
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-azure-machine-learning-web-service"></a>Déploiement d’un service web Azure Machine Learning
Azure Machine Learning vous permet de toobuild, tester et déployer des solutions d’analyses prédictives.

D'un point de vue très général, cela s'effectue en trois étapes :

* **[Créer une expérience d’apprentissage]**  -Azure Machine Learning Studio est un environnement collaboratif de développement visuel que vous utilisez tootrain et testez un analytique prédictive de modèle à l’aide des données d’apprentissage que vous fournissez.
* **[Convertir les expérience prédictive tooa]**  - une fois que votre modèle a été formé avec des données existantes et vous êtes prêt toouse il tooscore de nouvelles données, préparer et de simplifier votre expérience pour les prédictions.
* **[Déployez-la en tant que service web]** : vous pouvez déployer votre expérience prédictive sous la forme d’un [nouveau] service web Azure ou d’un service web Azure [classique]. Les utilisateurs peuvent envoyer le modèle de données tooyour et recevoir les prédictions de votre modèle.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="create-a-training-experiment"></a>Créez une expérience d'apprentissage
tootrain un modèle prédictif analytique, vous utilisez Azure Machine Learning Studio toocreate une expérience d’apprentissage où inclure les données d’apprentissage de différents modules tooload, préparer les données hello si nécessaire, appliquer des algorithmes d’apprentissage automatique et évaluer les résultats de hello . Vous pouvez effectuer une itération sur une expérience essayez toocompare d’algorithmes d’apprentissage différentes et évaluer les résultats hello.

processus Hello créer et gérer des expériences d’apprentissage est couvert plus en détail ailleurs. Pour plus d’informations, voir les articles suivants :

* [créez une expérience simple dans Azure Machine Learning Studio](machine-learning-create-experiment.md)
* [développez une solution prédictive avec Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)
* [importez vos données d'apprentissage dans Azure Machine Learning Studio](machine-learning-data-science-import-data.md)
* [gérez des itérations d'expériences dans Azure Machine Learning Studio](machine-learning-manage-experiment-iterations.md)

## <a name="convert-hello-training-experiment-tooa-predictive-experiment"></a>Convertir l’expérience prédictive des tooa expérience d’apprentissage hello
Une fois que vous avez formé votre modèle, vous êtes prêt tooconvert votre formation d’expérimenter dans une expérience prédictive tooscore nouvelles données.

En convertissant tooa prédictive faire des essais, vous obtenez votre toobe prêt formé déployé comme un service web de score. Les utilisateurs du service web de hello peuvent envoyer modèle tooyour de données d’entrée et de votre modèle envoie les résultats de prédiction hello précédent. Lorsque vous convertissez tooa prédictive faire des essais, n’oubliez pas comment vous prévoyez vos toobe modèle utilisé par d’autres.

tooconvert tooa de votre expérience d’apprentissage prédictive tester, cliquez sur **exécuter** bas hello du canevas de l’expérience hello, cliquez sur **configurer le Service Web**, puis sélectionnez **prédictive Service Web** .

![Convertir l’expérience de tooscoring](./media/machine-learning-publish-a-machine-learning-web-service/figure-1.png)

Pour plus d’informations sur la façon de tooperform cette conversion, consultez [comment tooprepare votre modèle pour le déploiement dans Azure Machine Learning Studio](machine-learning-convert-training-experiment-to-scoring-experiment.md).

Hello étapes suivantes décrivent déploiement d’une expérience prédictive comme un service web. Vous pouvez également déployer hello expérience en tant que service web de classique.

## <a name="deploy-it-as-a-web-service"></a>Déployez-la en tant que service web

Vous pouvez déployer les expérience prédictive hello comme un service web ou service web standard.

### <a name="deploy-hello-predictive-experiment-as-a-new-web-service"></a>Déployer l’expérience de prédictive hello comme un service web
Maintenant que l’expérience de prédictive hello a été préparée, vous pouvez le déployer en tant qu’un nouveau service web Azure. À l’aide du service web de hello, les utilisateurs peuvent envoyer le modèle de données tooyour et modèle de hello retourne ses prédictions.

toodeploy faire des essais, un sur votre prédictive **exécuter** bas hello hello expérimenter la zone de dessin. Une fois que l’expérience de hello est terminée, cliquez sur **déployer le Service Web** et sélectionnez **déployer le Service Web [nouveau]**.  page de déploiement Hello hello Machine Learning Web du portail de Service s’ouvre.

> [!NOTE] 
> toodeploy un nouveau service web, vous devez disposer des autorisations suffisantes dans hello abonnement toowhich vous déployez le service web de hello. Pour plus d’informations, consultez [gérer un service Web à l’aide du portail de Services Web de Azure Machine Learning hello](machine-learning-manage-new-webservice.md). 

#### <a name="machine-learning-web-service-portal-deploy-experiment-page"></a>Page d’expérience de déploiement du portail du service web Machine Learning
Sur la page de déployer une expérience de hello, entrez un nom pour le service web de hello.
Sélectionnez un plan de tarification. Si vous avez un plan de tarification existant, que vous pouvez le sélectionner, sinon vous devez créer un nouveau plan de prix pour le service de hello.

1. Bonjour **Plan tarifaire** liste déroulante, sélectionnez un plan existant ou hello **sélectionnez Nouveau plan** option.
2. Dans **le nom du Plan**, tapez un nom qui identifie le plan hello sur votre facture.
3. Sélectionnez une des hello **niveaux de planification mensuelle**. plan Hello niveaux par défaut toohello des plans pour votre région par défaut et votre service web est déployé toothat région.

Cliquez sur **déployer** et hello **Quickstart** page de votre service web s’ouvre.

page de démarrage rapide du service web Hello vous donne accès et des conseils sur les tâches les plus courantes hello que vous allez effectuer après la création d’un service web. À ce stade, vous pouvez accéder facilement les pages de Test hello et consommer.

<!-- ![Deploy hello web service](./media/machine-learning-publish-a-machine-learning-web-service/figure-2.png)-->

#### <a name="test-your-new-web-service"></a>Test de votre nouveau service web
tootest votre nouveau service web, cliquez sur **tester un service web** sous tâches courantes. Sur la page de Test hello, vous pouvez tester votre service web en tant qu’un Service de requête-réponse (RR) ou un service de l’exécution par lots (BES).

page de test RR Hello affiche hello entrées, sorties et tous les paramètres globaux que vous avez définis pour une expérience de hello. service web de hello tootest, vous pouvez entrer manuellement les valeurs appropriées pour les entrées de hello ou fournissez un fichier de mise en forme CSV (valeurs) séparés par des virgules contenant les valeurs de test hello.

tootest à l’aide d’enregistrements de ressources, à partir du mode liste hello, entrez les valeurs appropriées pour les entrées de hello et cliquez sur **demande-réponse de Test**. Vos résultats de prédiction s’affichent dans toohello de colonne de sortie hello gauche.

![Déployer le service web de hello](./media/machine-learning-publish-a-machine-learning-web-service/figure-5-test-request-response.png)

Cliquez sur votre BES, de tootest **lot**. Sur la page de test de traitement par lots hello, cliquez sur Parcourir sous votre entrée et sélectionnez un fichier CSV contenant les valeurs d’échantillonnage approprié. Si vous n’avez pas un fichier CSV, et que vous avez créé votre expérience prédictif à l’aide de la Machine Learning Studio, vous pouvez télécharger le jeu de données hello pour votre expérience prédictive et l’utiliser.

jeu de données toodownload hello, ouvrez Machine Learning Studio. Ouvrez votre expérience prédictive et cliquez avec le bouton droit sur une entrée hello pour votre expérience. Dans le menu contextuel de hello, sélectionnez **dataset** , puis sélectionnez **télécharger**.

![Déployer le service web de hello](./media/machine-learning-publish-a-machine-learning-web-service/figure-7-mls-download.png)

Cliquez sur **Test**. état de Hello de votre travail de l’exécution par lots s’affiche juste toohello sous **traitements par lots de Test**.

![Déployer le service web de hello](./media/machine-learning-publish-a-machine-learning-web-service/figure-6-test-batch-execution.png)

<!--![Test hello web service](./media/machine-learning-publish-a-machine-learning-web-service/figure-3.png)-->

Sur hello **CONFIGURATION** page, vous pouvez hello description de la modification, titre, mettre à jour la clé de compte de stockage hello et activer les exemples de données pour votre service web.

![Configurer le service web de hello](./media/machine-learning-publish-a-machine-learning-web-service/figure-8-arm-configure.png)

Une fois que vous avez déployé le service web de hello, vous pouvez :

* **Accès** par le biais d’API du service web hello.
* **Gérer les** par le biais d’Azure Machine Learning portail de services web ou hello portail Azure classic.
* **le mettre à jour** si vous modifiez votre modèle.

#### <a name="access-your-new-web-service"></a>Accès à votre nouveau service web
Une fois que vous déployez votre service web à partir de la Machine Learning Studio, vous pouvez toohello données envoyer et recevoir des réponses par programme.

Hello **consommer** page fournit toutes les informations de hello vous devez tooaccess votre service web. Par exemple, la clé de hello API est fournie tooallow autorisé accès toohello.

Pour plus d’informations sur l’accès à un service web de Machine Learning, consultez [comment tooconsume un service Web de Azure Machine Learning](machine-learning-consume-web-services.md).

#### <a name="manage-your-new-web-service"></a>Gestion de votre nouveau service web
Vous pouvez gérer vos nouveaux services web par le biais du portail Service web Machine Learning. À partir de hello [page du portail principal](https://services.azureml-test.net/), cliquez sur **Services Web**. À partir de la page des services web hello, vous pouvez supprimer ou copie d’un service. toomonitor un service spécifique, cliquez sur le service hello et puis cliquez sur **tableau de bord**. traitements toomonitor associés hello web service, cliquez sur **journal des demandes de lot**.

### <a name="deploy-hello-predictive-experiment-as-a-classic-web-service"></a>Déployer l’expérience de prédictive hello comme service web classique

Maintenant que l’expérience de prédictive hello suffisamment préparé, vous pouvez le déployer en tant que service web Azure Classic. À l’aide du service web de hello, les utilisateurs peuvent envoyer le modèle de données tooyour et modèle de hello retourne ses prédictions.

toodeploy faire des essais, un sur votre prédictive **exécuter** bas hello hello expérimenter la zone de dessin, puis cliquez sur **déployer le Service Web**. service web de Hello est configuré et vous sont placés dans le tableau de bord hello web service.

![Déployer le service web de hello](./media/machine-learning-publish-a-machine-learning-web-service/figure-2.png)

#### <a name="test-your-classic-web-service"></a>Test de votre service web classique

Vous pouvez tester le service web de hello dans le portail de Services Web de Machine Learning hello ou de Machine Learning Studio.

tootest hello service web de réponse à la demande, cliquez sur hello **Test** bouton dans le tableau de bord hello web service. Une boîte de dialogue s’affiche tooask vous pour les données d’entrée de hello pour le service de hello. Ce sont les colonnes hello attendus par hello expérience de score. Entrez un jeu de données, puis cliquez sur **OK**. les résultats de Hello générés par le service web de hello sont affichés en bas de hello du tableau de bord hello.

Vous pouvez cliquer sur hello **Test** afficher un aperçu de lien tootest votre service dans le portail de Services Web de Azure Machine Learning hello comme indiqué précédemment dans hello nouvelle section de service web.

tootest hello Batch Execution Service, cliquez sur **Test** prévisualiser le lien. Sur la page de test de traitement par lots hello, cliquez sur Parcourir sous votre entrée et sélectionnez un fichier CSV contenant les valeurs d’échantillonnage approprié. Si vous n’avez pas un fichier CSV, et que vous avez créé votre expérience prédictif à l’aide de la Machine Learning Studio, vous pouvez télécharger le jeu de données hello pour votre expérience prédictive et l’utiliser.

![Tester un service web de hello](./media/machine-learning-publish-a-machine-learning-web-service/figure-3.png)

Sur hello **CONFIGURATION** page, vous pouvez modifier le nom d’affichage hello du service de hello et lui donner une description. Hello nom et la description s’affiche dans hello [portail Azure classic](http://manage.windowsazure.com/) où vous gérez vos services web.

Vous pouvez fournir une description de vos données d’entrée, de vos données de sortie et des paramètres de service web en saisissant une chaîne pour chaque colonne sous **SCHÉMA D’ENTRÉE**, **SCHÉMA DE SORTIE** et **PARAMÈTRE DU SERVICE WEB**. Ces descriptions sont utilisées dans la documentation du code exemple hello fournie pour hello web service.

Vous pouvez activer la journalisation toodiagnose toutes les erreurs que vous voyez lorsque vous accédez à votre service web. Pour plus d'informations, consultez [Activation de la journalisation pour les services web de Machine Learning](machine-learning-web-services-logging.md).

![Configurer le service web de hello](./media/machine-learning-publish-a-machine-learning-web-service/figure-4.png)

Vous pouvez également configurer des points de terminaison hello pour le service web de hello Bonjour Azure Machine Learning Web Services portail similaire toohello procédure illustrée précédemment hello nouvelle section de service web. options de Hello sont différentes, vous pouvez ajouter ou modifier la description de service hello, activez la journalisation et activer exemples de données de test.

#### <a name="access-your-classic-web-service"></a>Accès à votre service web classique
Une fois que vous déployez votre service web à partir de la Machine Learning Studio, vous pouvez toohello données envoyer et recevoir des réponses par programme.

tableau de bord Hello fournit toutes les informations de hello vous devez tooaccess votre service web. Par exemple, une clé API hello est fourni tooallow autorisé service toohello d’accès, et des pages d’aide API sont fournies toohelp que commencer l’écriture de votre code.

Pour plus d’informations sur l’accès à un service web de Machine Learning, consultez [comment tooconsume un service Web de Azure Machine Learning](machine-learning-consume-web-services.md).

#### <a name="manage-your-classic-web-service"></a>Gestion de votre service web classique
Il existe diverses actions, vous pouvez effectuer toomonitor un service web. Vous pouvez le mettre à jour et le supprimer. Vous pouvez également ajouter le service web de points de terminaison supplémentaires tooa classique dans le point de terminaison par défaut de toohello addition qui est créé lors de son déploiement.

Pour plus d’informations, consultez [gérer un espace de travail Azure Machine Learning](machine-learning-manage-workspace.md) et [gérer un service web à l’aide du portail de Services Web de Azure Machine Learning hello](machine-learning-manage-new-webservice.md).

<!-- When this article gets published, fix hello link and uncomment
For more information on how toomanage Azure Machine Learning web service endpoints using hello REST API, see **Azure machine learning web service endpoints**.
-->

## <a name="update-hello-web-service"></a>Mettre à jour hello web service
Vous pouvez apporter des modifications tooyour web service, telles que la mise à jour du modèle de hello avec des données d’apprentissage supplémentaire et le déployer à nouveau, remplacement du service web d’origine de hello.

service web de hello tooupdate, ouvrez l’expérience d’origine prédictive hello vous avez utilisé le service web de hello toodeploy et faire une copie modifiable en cliquant sur **SAVE AS**. Effectuez vos modifications, puis cliquez sur **Déployer le service web**.

Étant donné que vous avez déployé cette expérience avant, vous êtes invité si vous souhaitez toooverwrite (Classic Web Service) ou le service de mise à jour (un service web) hello existant. En cliquant sur **Oui** ou **mise à jour** arrête le service web existant de hello et déploie expérience de prédictive nouvelle hello est déployé à la place.

> [!NOTE]
> Si vous avez des modifications de configuration dans le service web d’origine hello, par exemple, entrez un nouveau nom complet ou une description, vous devez tooenter ces valeurs à nouveau.
> 
> 

Une option de mise à jour de votre service web est modèle de hello tooretrain par programmation. Pour plus d'informations, consultez la page [Reformation des modèles Machine Learning par programme](machine-learning-retrain-models-programmatically.md).

<!-- internal links -->
[Créer une expérience d’apprentissage]: #create-a-training-experiment
[Convertir les expérience prédictive tooa]: #convert-the-training-experiment-to-a-predictive-experiment
[Déployez-la en tant que service web]: #deploy-it-as-a-web-service.
[nouveau]: #deploy-the-predictive-experiment-as-a-new-Web-service
[classique]: #deploy-the-predictive-experiment-as-a-new-Web-service
[Access]: #access-the-Web-service
[Manage]: #manage-the-Web-service-in-the-azure-management-portal
[Update]: #update-the-Web-service
