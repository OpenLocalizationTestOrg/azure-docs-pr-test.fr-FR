---
title: "un service web de Machine Learning avec un modèle d’application web d’aaaConsume | Documents Microsoft"
description: "Utilisez un modèle d’application web dans Azure Marketplace tooconsume un service web prédictif dans Azure Machine Learning."
keywords: "service Web, opérationnalisation, API REST, apprentissage automatique"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e0d71683-61b9-4675-8df5-09ddc2f0d92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;raymondl
ms.openlocfilehash: 1199377bead470807d58ca7f7a667175cbb88450
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-azure-machine-learning-web-service-with-a-web-app-template"></a>Utilisation d’un service Web Microsoft Azure Machine Learning à l’aide d’un modèle d’application Web

Une fois vous avez développé votre modèle de prévision et déployé en tant que service web Azure à l’aide de la Machine Learning Studio, ou à l’aide des outils tels que R ou Python, vous pouvez accéder au modèle mis à hello à l’aide d’une API REST.

Il existe plusieurs façons tooconsume hello API REST accès hello service web et. Par exemple, vous pouvez écrire une application en c#, R, ou Python à l’aide de hello exemple de code généré lorsque vous avez déployé le service web de hello (disponible dans hello [portail de Services Web Machine Learning](https://services.azureml.net/quickstart) ou tableau de bord de service web hello dans Machine Learning Studio). Ou vous pouvez utiliser le classeur Microsoft Excel de hello exemple créé à hello même temps.

Mais hello tooaccess rapidement et facilement votre service web se fait via les modèles d’application hello Web disponibles dans hello [Azure Marketplace des applications Web](https://azure.microsoft.com/marketplace/web-applications/all/).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-azure-machine-learning-web-app-templates"></a>Hello modèles d’application Web Azure Machine Learning
modèles d’application web Hello disponibles Bonjour Azure Marketplace peuvent générer une application web personnalisée qui connaît les données d’entrée et les résultats attendus de votre service web. Vous devez toodo est de fournir des données et le service web d’hello web application accès tooyour et modèle de hello hello rest.

Il existe deux modèles :

* [Modèle d’application Web Azure ML Request-Response Service](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/)
* [Modèle d’application Web Azure ML Batch Execution Service](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/)

Chaque modèle crée un exemple d’application ASP.NET, à l’aide de hello URI de l’API et la clé de votre service web et le déploie comme un tooAzure du site web. modèle de Service de requête-réponse (RR) Hello crée une application web qui vous permet de toosend une seule ligne de données toohello web service tooget un résultat unique. modèle de Service de l’exécution de lot (BES) Hello crée une application web qui vous permet de toosend nombre de lignes de données tooget plusieurs résultats.

Aucun codage n’est nécessaire de toouse ces modèles. Vous devez simplement spécifier hello clé API et l’URI et les versions de modèle de hello application hello pour vous.

clé de hello API tooget et l’URI de requête pour un service web :

1. Bonjour [portail de Services Web](https://services.azureml.net/quickstart), pour un service web, cliquez sur **Services Web** haut hello. Pour un service web classique, cliquez sur **Services web classiques**.
2. Cliquez sur hello web service tooaccess.
3. Pour un service web standard, cliquez sur hello point de terminaison tooaccess.
4. Cliquez sur **consommer** haut hello.
5. Hello de copie **principal** ou **clé secondaire** et l’enregistrer.
6. Si vous créez un modèle de Service de requête-réponse (RR), copiez hello **demande-réponse** URI et l’enregistrer. Si vous créez un modèle de Service de l’exécution de lot (BES), copiez hello **de requêtes de lots** URI et l’enregistrer.


## <a name="how-toouse-hello-request-response-service-rrs-template"></a>Comment toouse hello modèle de Service de requête-réponse (RR)
Suivez ces modèle application étapes toouse hello RR web, comme indiqué dans hello suivant schéma.

![Modèle de processus toouse RR web][image1]


<!--    ![API Key][image3] -->

<!-- This value will look like this:
   
        https://ussouthcentral.services.azureml.net/workspaces/<workspace-id>/services/<service-id>/execute?api-version=2.0&details=true
   
    ![Request URI][image4] -->

1. Accédez toohello [portail Azure](https://portal.azure.com), **connexion**, cliquez sur **nouveau**, recherchez et sélectionnez **l’application Web Azure ML avec requête-réponse Service**, puis cliquez sur **Créer**. 
   
   * Donnez un nom unique à votre application Web. URL de Hello de hello web application sera ce nom, suivi par `.azurewebsites.net.` , par exemple,`http://carprediction.azurewebsites.net.`
   * Sélectionnez hello abonnement Azure et des services sous lequel votre service web est en cours d’exécution.
   * Cliquez sur **Créer**.
     
     ![Créer une application web][image5]

4. Lorsque Azure a terminé le déploiement de l’application hello web, cliquez sur hello **URL** hello page de paramètres d’application web dans Azure, ou entrez l’URL de hello dans un navigateur web. Par exemple, `http://carprediction.azurewebsites.net.`
5. Lorsque hello web application première s’exécute qu’il vous demandera hello **API poster une URL** et **clé API**.
   Entrez les valeurs hello vous avez enregistré précédemment (**URI de requête** et **clé API**, respectivement).
     
     Cliquez sur **Envoyer**.
     
     ![Entrer l’URI de publication et la clé de l’API][image6]

6. Hello web application affiche son **Configuration de l’application Web** page avec les paramètres du service web en cours hello. Ici vous pouvez modifier les paramètres de toohello utilisés par l’application web hello.
   
   > [!NOTE]
   > Modification des paramètres de hello ici les modifie uniquement pour cette application web. Il ne change pas les paramètres par défaut hello de votre service web. Par exemple, si vous modifiez hello **Description** ici ne change pas description hello indiquée sur le tableau de bord du service hello web dans Machine Learning Studio.
   > 
   > 
   
    Lorsque vous avez terminé, cliquez sur **enregistrer les modifications**, puis cliquez sur **accédez tooHome Page**.

7. Page d’accueil, vous pouvez saisir les valeurs service web de tooyour toosend de hello. Cliquez sur **Submit** lorsque vous avez terminé, et hello résultat est retourné.

Si vous souhaitez tooreturn toohello **Configuration** page, aller toohello `setting.aspx` page de l’application web hello. Par exemple : `http://carprediction.azurewebsites.net/setting.aspx.` vous sera à nouveau clé de hello API demandées tooenter - vous avez besoin que tooaccess hello page et mettre à jour les paramètres hello.

Vous pouvez arrêter, redémarrer ou supprimer l’application web de hello Bonjour Azure portal comme toute autre application web. Tant qu’il est en cours d’exécution, vous pouvez parcourir l’adresse d’accueil web toohello et entrez les nouvelles valeurs.

## <a name="how-toouse-hello-batch-execution-service-bes-template"></a>Comment toouse hello modèle de Service de l’exécution de lot (BES)
Vous pouvez utiliser hello BES modèle d’application web Bonjour même sauf comme modèle de RR hello, cette application web hello créé vous permettra de toosubmit plusieurs lignes de données et de recevoir plusieurs résultats.

valeurs d’entrée de Hello pour un service web de l’exécution par lots peuvent provenir de stockage Azure ou un fichier local ; résultats de Hello sont stockés dans un conteneur de stockage Azure.
Par conséquent, vous aurez besoin une toohold de conteneur de stockage Azure hello résultats retournés par l’application web hello et vous aurez besoin de tooget vos données d’entrée prêt.

![Traiter toouse BES modèle web][image2]

1. Suivez hello même hello toocreate de procédure BES web application que pour les modèles de RR hello, à l’exception de go trop[modèle d’application Azure ML lot l’exécution du Service Web](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) tooopen hello modèle BES sur Azure Marketplace, puis cliquez sur **créer l’application Web** .

2. toospecify où vous souhaitez que les résultats de hello stockés, entrez les informations de conteneur de destination hello sur hello la page d’accueil de l’application web. Spécifiez également où l’application hello web peut obtenir les valeurs d’entrée hello, dans un fichier local ou un conteneur de stockage Azure.
   Cliquez sur **Envoyer**.
   
    ![Informations sur le stockage][image7]

l’application Hello web affiche une page avec l’état du travail.
Lorsque hello est terminée, vous aurez emplacement hello de résultats hello dans le stockage blob Azure. Vous avez également option hello du téléchargement de fichiers local de hello résultats tooa.

## <a name="for-more-information"></a>Pour plus d’informations
toolearn plus d’informations sur...

* la création d’une expérience d’apprentissage automatique avec Machine Learning Studio, consultez [Création de votre première expérience dans Azure Machine Learning Studio](machine-learning-create-experiment.md)
* Comment toodeploy votre apprentissage faire des essais en tant qu’un service web, consultez [déployer un service web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md)
* autres façons tooaccess votre service web, consultez [comment tooconsume un service Web de Azure Machine Learning](machine-learning-consume-web-services.md)

[image1]: media/machine-learning-consume-web-service-with-web-app-template/rrs-web-template-flow.png
[image2]: media/machine-learning-consume-web-service-with-web-app-template/bes-web-template-flow.png
[image3]: media/machine-learning-consume-web-service-with-web-app-template/api-key.png
[image4]: media/machine-learning-consume-web-service-with-web-app-template/post-uri.png
[image5]: media/machine-learning-consume-web-service-with-web-app-template/create-web-app.png
[image6]: media/machine-learning-consume-web-service-with-web-app-template/web-service-info.png
[image7]: media/machine-learning-consume-web-service-with-web-app-template/storage.png
