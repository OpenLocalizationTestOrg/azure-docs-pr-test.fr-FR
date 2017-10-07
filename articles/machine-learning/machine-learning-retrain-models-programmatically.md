---
title: "aaaRetrain apprentissage des modèles par programme | Documents Microsoft"
description: "Découvrez comment tooprogrammatically recycler un modèle et mise à jour hello web service toouse hello qui vient d’être formé dans Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: 7ae4f977-e6bf-4d04-9dde-28a66ce7b664
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: raymondl;garye;v-donglo
ms.openlocfilehash: edbb64c08f7d9edf3c76e23e0cc7e14c0125d697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-machine-learning-models-programmatically"></a>Reformation des modèles Machine Learning par programme
Dans cette procédure pas à pas, vous allez apprendre comment tooprogrammatically recycler un Service Web Azure Machine Learning à l’aide de c# et hello service d’exécution de lot Machine Learning.

Une fois que vous avez reformés modèle de hello, hello suivant les procédures pas à pas montrent comment tooupdate hello modèle dans votre service web prédictif :

* Si vous avez déployé un service web de classique dans le portail de Services Web de Machine Learning hello, consultez [recycler le service web standard](machine-learning-retrain-a-classic-web-service.md). 
* Si vous avez déployé un service web, consultez [recycler un nouveau service web à l’aide des applets de commande hello Machine Learning Management](machine-learning-retrain-new-web-service-using-powershell.md).

Pour une vue d’ensemble de hello recyclage de processus, consultez [recycler un modèle d’apprentissage automatique](machine-learning-retrain-machine-learning-model.md).

Si vous souhaitez toostart avec votre nouveau gestionnaire de ressources Azure en fonction de service web, consultez [recycler un service web prédictif existant](machine-learning-retrain-existing-resource-manager-based-web-service.md).

## <a name="create-a-training-experiment"></a>Créez une expérience d'apprentissage
Pour cet exemple, vous allez utiliser « exemple 5 : Evaluate Train, Test, pour la Classification binaire : jeu de données adulte » à partir d’exemples de Microsoft Azure Machine Learning hello. 

expérience de hello toocreate :

1. Connectez-vous à tooMicrosoft Azure Machine Learning Studio. 
2. Dans hello coin inférieur droit du tableau de bord hello, cliquez sur **nouveau**.
3. À partir de hello Microsoft Samples, sélectionnez exemple 5.
4. l’expérience toorename hello, haut hello du canevas de l’expérience hello, sélectionnez le nom d’expérience de hello « exemple 5 : Evaluate Train, Test, pour la Classification binaire : jeu de données adulte ».
5. Tapez Modèle de recensement.
6. Au bas de hello du canevas de l’expérience hello, cliquez sur **exécuter**.
7. Cliquez sur **Configurer le service web**, puis sélectionnez **Reformation du service web**. 

Hello Voici expérience initiale de hello.
   
   ![Expérience initiale.][2]


## <a name="create-a-predictive-experiment-and-publish-as-a-web-service"></a>Créer une expérience prédictive et la publier comme service web
Ensuite, vous créez une expérience prédictive.

1. Au bas de hello du canevas de l’expérience hello, cliquez sur **configurer le Service Web** et sélectionnez **prédictive Service Web**. Cela enregistre le modèle de hello sous la forme d’un modèle formé et ajoute des modules d’entrée et de sortie du service web. 
2. Cliquez sur **Exécuter**. 
3. Une fois l’expérience de hello est terminée, cliquez sur **déployer le Service Web [standard]** ou **déployer le Service Web [nouveau]**.

> [!NOTE] 
> toodeploy un nouveau service web, vous devez disposer des autorisations suffisantes dans hello abonnement toowhich vous déployez le service web de hello. Pour plus d’informations, consultez [gérer un service Web à l’aide du portail de Services Web de Azure Machine Learning hello](machine-learning-manage-new-webservice.md). 

## <a name="deploy-hello-training-experiment-as-a-training-web-service"></a>Déployer l’expérience de formation hello comme un service web de formation
modèle formé de hello tooretrain, vous devez déployer l’expérience de formation hello que vous avez créé en tant que Retraining web service. Ce service web a besoin d’un *sortie du Service Web* module connecté toohello  *[Train Model] [ train-model]*  module, tooproduce en mesure de toobe nouveau modèles formés.

1. expérience de formation tooreturn toohello, cliquez sur icône d’expériences hello dans le volet gauche de hello, puis expérience hello nommée modèle de recensement.  
2. Dans la zone de recherche de rechercher les éléments expérience hello, type de service web. 
3. Faites glisser un *entrée du Service Web* module sur hello faire des essais canevas et se connecter à sa sortie toohello *Clean Missing Data* module.  Cela garantit que vos données reconversion sont traitées hello la même façon que vos données d’apprentissage d’origine.
4. Faites glisser deux *sortie de service web* modules sur hello expérimenter la zone de dessin. Connectez la sortie hello Hello *Train Model* module tooone hello sorties et de hello *modèle Evaluate* module toohello autres. Hello la sortie du service web pour **Train Model** nous donne le modèle formé hello. Hello sortie jointe trop**modèle Evaluate** retourne ce module de sortie, ce qui est des résultats de performance hello.
5. Cliquez sur **Exécuter**. 

Ensuite, vous devez déployer expérience de formation hello comme un service web qui génère un modèle et les résultats d’évaluation du modèle. tooaccomplish cela, votre prochain ensemble d’actions varient selon que vous travaillez avec un service web de classique ou un service web.  

**Service web classique**

Au bas de hello du canevas de l’expérience hello, cliquez sur **configurer le Service Web** et sélectionnez **déployer le Service Web [standard]**. Service Web de Hello **tableau de bord** s’affiche avec la page d’aide hello clé API et hello API pour l’exécution du lot. Uniquement hello méthode d’exécution du traitement par lots peut servir pour la création de modèles formés.

**Nouveau service web**

Au bas de hello du canevas de l’expérience hello, cliquez sur **configurer le Service Web** et sélectionnez **déployer le Service Web [nouveau]**. portail de Services Web de Web Service Azure Machine Learning Hello ouvre la page du service web toohello déployer. Tapez un nom pour votre service web, choisissez un plan de paiement, puis cliquez sur **Déployer**. Uniquement hello méthode d’exécution du traitement par lots peut être utilisé pour la création de modèles formés

Dans les deux cas, une fois que l’expérience exécution est terminée, flux de travail qui en résulte hello doit se présenter comme suit :

![Flux de travail produit après l’exécution.][4]



## <a name="retrain-hello-model-with-new-data-using-bes"></a>Recycler un modèle de hello avec de nouvelles données à l’aide de BES
Pour cet exemple, vous utilisez c# toocreate hello recyclage d’application. Vous pouvez également utiliser hello Python ou R exemple code tooaccomplish cette tâche.

toocall hello réapprentissage des API :

1. Créez une application console en C# dans Visual Studio : **Nouveau** > **Projet** > **Visual C#** > **Bureau classique Windows** > **Application console (.NET Framework)**.
2. Se connecter toohello portail du Service Web de Machine Learning.
3. Si vous utilisez un service web classique, cliquez sur **Services web classiques**.
   1. Cliquez sur le service web de hello que vous travaillez.
   2. Cliquez sur le point de terminaison par défaut hello.
   3. Cliquez sur **Consommer**.
   4. En bas de hello Hello **consommer** page hello **exemple de Code** , cliquez sur **lot**.
   5. Continuer toostep 5 de cette procédure.
4. Si vous utilisez un nouveau service web, cliquez sur **Services web**.
   1. Cliquez sur le service web de hello que vous travaillez.
   2. Cliquez sur **Consommer**.
   3. Au bas de hello de page de consommer de hello, Bonjour **exemple de Code** , cliquez sur **lot**.
5. Copier le code c# exemple hello pour l’exécution du lot et collez-le dans le fichier Program.cs hello assurant l’espace de noms hello reste intacte.

Ajouter le package de Nuget hello Microsoft.AspNet.WebApi.Client comme indiqué dans les commentaires de hello. tooadd hello référence tooMicrosoft.WindowsAzure.Storage.dll, vous devrez peut-être tout d’abord bibliothèque cliente de tooinstall hello pour les services de stockage Microsoft Azure. Pour plus d’informations, consultez [cette page](https://www.nuget.org/packages/WindowsAzure.Storage).

### <a name="update-hello-apikey-declaration"></a>Mise à jour hello apikey déclaration
Recherchez hello **apikey** déclaration.

    const string apiKey = "abc123"; // Replace this with hello API key for hello web service

Bonjour **les informations de base de la consommation** section Hello **consommer** page, recherchez la clé primaire de hello et copiez-le toohello **apikey** déclaration.

### <a name="update-hello-azure-storage-information"></a>Mettre à jour les informations de stockage Azure hello
Hello, exemple de code BES télécharge un fichier à partir d’un stockage de tooAzure disque local (par exemple « C:\temp\CensusIpnput.csv »), la traite et écrit hello résultats tooAzure arrière stockage.  

tooaccomplish cette tâche, vous devez récupérer hello informations compte de stockage nom, clé et un conteneur pour votre compte de stockage depuis le portail Azure classic de hello et mise à jour hello correspondant des valeurs dans le code hello. 

1. Se connecter toohello de portail Azure classic.
2. Dans la colonne du volet de navigation gauche hello, cliquez sur **stockage**.
3. À partir de la liste de hello des comptes de stockage, sélectionnez un toostore hello reformés modèle.
4. Au bas de hello de page de hello, cliquez sur **gérer les clés d’accès**.
5. Copiez et enregistrez hello **clé d’accès primaire** et hello fermer la boîte de dialogue. 
6. En hello haut hello, cliquez sur **conteneurs**.
7. Sélectionnez un conteneur existant ou créez-en un nouveau et enregistrer le nom de hello.

Recherchez hello *StorageAccountName*, *StorageAccountKey*, et *StorageContainerName* déclarations et les valeurs hello de mise à jour vous avez enregistré à partir de hello portail Azure.

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure Storage Account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage Key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage Container name

Vous devez également vérifier les fichiers d’entrée hello est disponible à l’emplacement hello que vous spécifiez dans le code hello. 

### <a name="specify-hello-output-location"></a>Spécifiez l’emplacement de sortie hello
Lorsque vous spécifiez l’emplacement de sortie hello Bonjour charge utile de demander, hello l’extension de fichier hello spécifié dans *RelativeLocation* doit être spécifié en tant qu’ilearner. 

Consultez hello l’exemple suivant :

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with hello location you would like toouse for your output file, and valid file extension (usually .csv for scoring results, or .ilearner for trained models)*/
            }
        },

> [!NOTE]
> les noms de Hello de vos emplacements de sortie peuvent être différents de hello dans cette procédure pas à pas selon l’ordre de hello dans lequel vous avez ajouté des modules de sortie du service web hello. Étant donné que vous définissez cette expérience d’apprentissage à deux sorties, les résultats de hello incluent des informations d’emplacement de stockage pour les deux.  
> 
> 

![Sortie du nouvel apprentissage.][6]

Diagramme 4 : Sortie du nouvel apprentissage.

## <a name="evaluate-hello-retraining-results"></a>Évaluer les résultats de recyclage hello
Lorsque vous exécutez des application hello, sortie de hello inclut les URL hello et tooaccess de nécessaires jeton SAS hello des résultats d’évaluation.

Vous pouvez voir les résultats des performances du modèle de hello reformé hello en combinant hello *BaseLocation*, *RelativeLocation*, et *SasBlobToken* à partir des résultats de sortie hello pour *output2* (comme indiqué dans hello précédent réapprentissage d’image de sortie) et collez l’URL complète de hello dans la barre d’adresse du navigateur hello.  

Examinez hello résultats toodetermine si qui vient d’être formé hello effectue également assez hello tooreplace existant à un.

Hello de copie *BaseLocation*, *RelativeLocation*, et *SasBlobToken* à partir des résultats de sortie hello, vous allez les utiliser au cours de hello recyclage de processus.

## <a name="next-steps"></a>Étapes suivantes
Si vous avez déployé le service web prédictif de hello en cliquant sur **déployer le Service Web [standard]**, consultez [recycler le service web standard](machine-learning-retrain-a-classic-web-service.md).

Si vous avez déployé le service web prédictif de hello en cliquant sur **déployer le Service Web [nouveau]**, consultez [recycler un nouveau service web à l’aide des applets de commande hello Machine Learning Management](machine-learning-retrain-new-web-service-using-powershell.md).

<!-- Retrain a New web service using hello Machine Learning Management REST API -->


[1]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE01.png
[2]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE02.png
[3]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE03.png
[4]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE04.png
[5]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE05.png
[6]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE06.png
[7]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE07.png


<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
