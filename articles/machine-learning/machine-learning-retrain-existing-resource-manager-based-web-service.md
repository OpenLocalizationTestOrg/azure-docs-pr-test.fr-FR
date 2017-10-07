---
title: "aaaRetrain existant prédictive de service web | Documents Microsoft"
description: "Découvrez comment tooretrain un modèle et mise à jour hello web service toouse hello qui vient d’être formé dans Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: cc4c26a2-5672-4255-a767-cfd971e46775
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: v-donglo
ms.openlocfilehash: fb0760d0a2adc34fc5f3df1ae41bdac075f91bf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-an-existing-predictive-web-service"></a>Reformer un service web prédictif existant
Ce document décrit hello recyclage de processus pour hello scénario :

* Vous avez une expérience de formation et une expérience de prévision que vous avez déployées en tant que service web mis en œuvre.
* Vous avez des nouvelles données que vous souhaitez votre tooperform toouse du service web prédictif son calcul de score.

> [!NOTE] 
> toodeploy un nouveau service web, vous devez disposer des autorisations suffisantes dans hello abonnement toowhich vous déployez le service web de hello. Pour plus d’informations, consultez [gérer un service Web à l’aide du portail de Services Web de Azure Machine Learning hello](machine-learning-manage-new-webservice.md). 

À partir de votre service web existant et les expériences, vous devez toofollow comme suit :

1. Modèle de mise à jour hello.
   1. Modifiez votre tooallow d’expérience d’apprentissage pour web service entrées et sorties.
   2. Déployer l’expérience de formation hello comme un service web reconversion.
   3. Utilisez modèle de hello tooretrain d’expérience de formation hello Service de l’exécution de lot (BES).
2. Utilisez expérience prédictive hello du tooupdate applets de commande hello Azure Machine Learning PowerShell.
   1. Connectez-vous tooyour compte de gestionnaire de ressources Azure.
   2. Obtenir la définition du service web hello.
   3. Exporter la définition du service web hello au format JSON.
   4. Mise à jour hello toohello ilearner objet blob de référence Bonjour JSON.
   5. Importer hello JSON dans une définition de service web.
   6. Mettre à jour le service web de hello avec une nouvelle définition de service web.

## <a name="deploy-hello-training-experiment"></a>Déployer l’expérience de formation hello
toodeploy hello l’expérience d’apprentissage comme un service web reconversion, vous devez ajouter des entrées et sorties toohello modèle de service web. En connectant un *sortie du Service Web* d’expérience module toohello  *[Train Model] [ train-model]*  module, vous activez hello expérience d’apprentissage tooproduce un nouveau modèle formé que vous pouvez utiliser dans votre expérience prédictive. Si vous avez un *modèle Evaluate* module, vous pouvez également attacher des résultats de l’évaluation web service sortie tooget hello en tant que sortie.

tooupdate votre expérience d’apprentissage :

1. Connecter un *Web Service d’entrée* données tooyour du module d’entrée (par exemple, un *Clean Missing Data* module). En règle générale, vous souhaitez tooensure vos données d’entrée sont traitées dans hello la même façon que vos données d’apprentissage d’origine.
2. Connecter un *sortie du Service Web* sortie toohello de module de votre *Train Model* module.
3. Si vous avez un *modèle Evaluate* module et que vous souhaitez obtenir des résultats d’évaluation toooutput hello, connectez-vous une *sortie du Service Web* sortie toohello de module de votre *modèle Evaluate* module.

Exécutez votre expérience.

Ensuite, vous devez déployer l’expérience de formation hello comme un service web qui génère un modèle et les résultats d’évaluation du modèle.  

Au bas de hello du canevas de l’expérience hello, cliquez sur **configurer le Service Web**, puis sélectionnez **déployer le Service Web [nouveau]**. portail de Services Web de Azure Machine Learning Hello ouvre toohello **déployer le Service Web** page. Tapez un nom pour votre service web, choisissez un plan de paiement, puis cliquez sur **Déployer**. Vous pouvez uniquement utiliser la méthode de l’exécution par lots de hello pour la création de modèles formés.

## <a name="retrain-hello-model-with-new-data-by-using-bes"></a>Recycler un modèle hello avec de nouvelles données à l’aide de BES
Pour cet exemple, nous utilisons hello toocreate c# recyclage d’application. Vous pouvez également utiliser Python ou R tooaccomplish de code d’exemple à cette tâche.

hello toocall réapprentissage API :

1. Créez une application console en C# dans Visual Studio : **Nouveau** > **Projet** > **Visual C#** > **Bureau classique Windows** > **Application console (.NET Framework)**.
2. Se connecter toohello portail de Services Web de Machine Learning.
3. Cliquez sur hello web service avec lequel vous travaillez.
4. Cliquez sur **Consommer**.
5. En bas de hello Hello **consommer** page hello **exemple de Code** , cliquez sur **lot**.
6. Copier le code c# exemple hello pour l’exécution du lot et collez-le dans le fichier Program.cs de hello. Assurez-vous que cet espace de noms hello reste intacte.

Ajouter le package de NuGet hello Microsoft.AspNet.WebApi.Client, comme indiqué dans les commentaires de hello. tooadd hello référence tooMicrosoft.WindowsAzure.Storage.dll, vous devrez peut-être tout d’abord tooinstall hello [bibliothèque cliente pour les services de stockage Azure](https://www.nuget.org/packages/WindowsAzure.Storage).

capture d’écran suivante Hello affiche hello **consommer** page du portail de Services Web de Azure Machine Learning hello.

![Page Consommer][1]

### <a name="update-hello-apikey-declaration"></a>Mise à jour hello apikey déclaration
Recherchez hello **apikey** déclaration :

    const string apiKey = "abc123"; // Replace this with hello API key for hello web service

Bonjour **les informations de base de la consommation** section Hello **consommer** page, recherchez la clé primaire de hello et copiez-le toohello **apikey** déclaration.

### <a name="update-hello-azure-storage-information"></a>Mettre à jour les informations de stockage Azure hello
Hello, exemple de code BES télécharge un fichier à partir d’un stockage de tooAzure disque local (par exemple, « C:\temp\CensusIpnput.csv »), la traite et écrit hello résultats tooAzure arrière stockage.  

informations de stockage Azure tooupdate hello, vous devez récupérer un compte de stockage hello nom, clé et un conteneur des informations de votre compte de stockage à partir de hello portail Azure classic, puis correspondi hello de mise à jour après l’exécution de votre expérience, hello résultant flux de travail sont similaires toohello suivants :

![Flux de travail obtenu après l’exécution][4]valeurs NG dans le code hello.

1. Se connecter toohello portail Azure classic.
2. Dans la colonne du volet de navigation gauche hello, cliquez sur **stockage**.
3. À partir de la liste de hello des comptes de stockage, sélectionnez un toostore hello reformés modèle.
4. Au bas de hello de page de hello, cliquez sur **gérer les clés d’accès**.
5. Copiez et enregistrez hello **clé d’accès primaire** et hello fermer la boîte de dialogue.
6. En hello haut hello, cliquez sur **conteneurs**.
7. Sélectionnez un conteneur existant, ou créez-en un nouveau et enregistrer le nom de hello.

Recherchez hello *StorageAccountName*, *StorageAccountKey*, et *StorageContainerName* déclarations et les valeurs hello mise à jour que vous avez enregistré à partir du portail classique de hello .

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure storage account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage container name

Vous devez également vérifier que ce fichier d’entrée hello est disponible à l’emplacement de hello que vous spécifiez dans le code hello.

### <a name="specify-hello-output-location"></a>Spécifiez l’emplacement de sortie hello
Lorsque vous spécifiez l’emplacement de sortie hello Bonjour charge utile de demander, hello extension du fichier hello qui est spécifié dans *RelativeLocation* doit être spécifié en tant que `ilearner`. Consultez hello l’exemple suivant :

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with hello location you want toouse for your output file and a valid file extension (usually .csv for scoring results or .ilearner for trained models)*/
            }
        },

Hello Voici un exemple de sortie de recyclage : ![réapprentissage de sortie][6]

## <a name="evaluate-hello-retraining-results"></a>Évaluer hello réapprentissage des résultats
Lorsque vous exécutez des application hello, sortie de hello inclut hello URL et le jeton de signatures d’accès partagé sont des résultats de l’évaluation hello tooaccess nécessaire.

Vous pouvez voir les résultats des performances du modèle de hello reformé hello en combinant hello *BaseLocation*, *RelativeLocation*, et *SasBlobToken* à partir des résultats de sortie hello pour *output2* (comme indiqué dans hello précédent réapprentissage d’image de sortie) et de coller des URL complète de hello dans la barre d’adresse du navigateur hello.  

Examinez hello résultats toodetermine si qui vient d’être formé hello effectue également assez hello tooreplace existant à un.

Hello de copie *BaseLocation*, *RelativeLocation*, et *SasBlobToken* à partir des résultats de sortie hello.

## <a name="retrain-hello-web-service"></a>Recycler le service web de hello
Lorsque vous recycler un nouveau service web, vous mettez à jour hello web prédictif service définition tooreference hello nouveau modèle formé. définition du service web Hello est une représentation interne du modèle formé de hello du service web de hello et n’est pas directement modifiable. Assurez-vous que la récupération de définition du service web hello pour votre expérience prédictive et pas votre expérience d’apprentissage.

## <a name="sign-in-tooazure-resource-manager"></a>Connectez-vous à tooAzure le Gestionnaire de ressources
Vous devez vous connecter tooyour compte Azure à partir de dans un environnement de hello PowerShell à l’aide de hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) applet de commande.

## <a name="get-hello-web-service-definition-object"></a>Obtenir l’objet de définition de Service Web hello
Ensuite, obtenez objet de définition de Service Web hello en appelant hello [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) applet de commande.

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

nom de groupe ressource toodetermine hello d’un service web existant, exécutez hello applet de commande Get-AzureRmMlWebService sans aucun service web de paramètres toodisplay hello dans votre abonnement. Recherchez le service web de hello et observez son ID de service web. nom Hello hello du groupe de ressources est hello quatrième élément de hello ID, juste après hello *resourceGroups* élément. Dans l’exemple suivant de hello, nom de groupe de ressources hello est par défaut-MachineLearning-SouthCentralUS.

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

Vous pouvez également toodetermine hello nom groupe de ressources d’un service web, connectez-vous au portail de Services Web de Azure Machine Learning toohello. Sélectionnez le service web de hello. nom de groupe de ressources Hello est hello cinquième élément de hello les URL du service web de hello, juste après hello *resourceGroups* élément. Dans l’exemple suivant de hello, nom de groupe de ressources hello est par défaut-MachineLearning-SouthCentralUS.

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-hello-web-service-definition-object-as-json"></a>Exporter l’objet de définition de Service Web hello au format JSON
définition de hello toomodify Hello de toouse hello formé formé qui vient d’être le modèle, vous devez d’abord utiliser hello [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) tooexport de l’applet de commande qu’il les fichier tooa au format JSON.

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-hello-reference-toohello-ilearner-blob"></a>Objet blob de mise à jour hello référence toohello ilearner
Dans les ressources hello, recherchez hello [modèle formé], mise à jour hello *uri* valeur Bonjour *locationInfo* nœud avec hello URI d’objet blob de hello ilearner. URI Hello est généré en combinant hello *BaseLocation* et hello *RelativeLocation* à partir de la sortie hello Hello appel de reconversion BES.

     "asset3": {
        "name": "Retrain Sample [trained model]",
        "type": "Resource",
        "locationInfo": {
          "uri": "https://mltestaccount.blob.core.windows.net/azuremlassetscontainer/baca7bca650f46218633552c0bcbba0e.ilearner"
        },
        "outputPorts": {
          "Results dataset": {
            "type": "Dataset"
          }
        }
      },

## <a name="import-hello-json-into-a-web-service-definition-object"></a>Importez des hello JSON dans un objet de définition de Service Web
Vous devez utiliser hello [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) applet de commande tooconvert hello modifié le fichier JSON dans un objet de définition de Service Web que vous pouvez utiliser expérience de predicative tooupdate hello.

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-hello-web-service"></a>Mettre à jour hello web service
Enfin, utilisez hello [AzureRmMlWebService de mise à jour](https://msdn.microsoft.com/library/azure/mt767922.aspx) tooupdate de l’applet de commande hello expérience prédictive.

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

[1]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-consume-page.png
[4]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE04.png
[6]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE06.png

<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
