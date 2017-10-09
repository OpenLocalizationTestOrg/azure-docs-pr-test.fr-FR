---
title: "aaaCreate plusieurs modèles à partir d’une expérience | Documents Microsoft"
description: "Utilisez PowerShell toocreate plusieurs modèles d’apprentissage et de points de terminaison de service avec hello web même algorithme, mais les jeux de données d’apprentissage différentes."
services: machine-learning
documentationcenter: 
author: hning86
manager: jhubbard
editor: cgronlun
ms.assetid: 1076b8eb-5a0d-4ac5-8601-8654d9be229f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: garye;haining
ms.openlocfilehash: 4a258a8ab26395d4169a058520151c860e16e169
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-many-machine-learning-models-and-web-service-endpoints-from-one-experiment-using-powershell"></a>Créer de nombreux modèles Machine Learning et points de terminaison de service web à partir d’une expérience à l’aide de PowerShell
Voici un problème d’apprentissage machine courant : vous souhaitez toocreate nombreux modèles qui ont hello même flux de travail de formation et utilisez hello même algorithme, mais ont des datasets différents d’apprentissage comme entrée. Cet article vous montre comment toodo cela à grande échelle dans Azure Machine Learning Studio à l’aide de simplement une expérience unique.

Supposez par exemple que vous avez une franchise de location de vélos à l’échelle internationale. Vous souhaitez toobuild une demande de location de régression modèle toopredict hello basée sur des données historiques. Vous avez des 1 000 emplacements de location sur Bonjour et que vous avez collecté un dataset pour chaque emplacement qui inclut des fonctionnalités importantes telles que date, heure, la météo et le trafic qui sont spécifiques tooeach emplacement.

Vous pouvez former le modèle une fois à l’aide d’une version fusionnée de tous les jeux de données hello sur tous les sites. Mais étant donné que chacun de vos magasins a un environnement unique, une meilleure approche serait être tootrain votre modèle de régression séparément à l’aide d’un jeu de données hello pour chaque emplacement. De cette façon, chaque modèle formé peut tenir tailles de compte hello autre magasin, volume, geography, remplissage, environnement de vélo convivial trafic, *etc.*.

Qui peut être la meilleure approche de hello, mais vous ne souhaitez pas expériences d’apprentissage toocreate 1 000 dans Azure Machine Learning avec chacun d’eux représentant un emplacement unique. En plus de constituer une tâche écrasante, il est également semble très inefficace, car chaque expérience tous aurait hello les mêmes composants à l’exception du jeu de données d’apprentissage hello.

Heureusement, nous pouvons faire en utilisant hello [réapprentissage des API Azure Machine Learning](machine-learning-retrain-models-programmatically.md) et automatisation tâche hello avec [Azure Machine Learning PowerShell](machine-learning-powershell-module.md).

> [!NOTE]
> toomake notre exemple de s’exécuter plus rapidement, nous allons réduire nombre hello des emplacements à partir de 1 000 too10. Mais hello mêmes principes et procédures s’appliquent too1, 000 emplacements. Hello seule différence est que si vous souhaitez que tootrain de 1 000 groupes de données vous souhaitez probablement toothink de l’exécution de hello suivant des scripts PowerShell en parallèle. Comment toodo n’est pas abordée de hello de cet article, mais vous pouvez rechercher des exemples de PowerShell multi-threading sur hello Internet.  
> 
> 

## <a name="set-up-hello-training-experiment"></a>Configurer expérience de formation hello
Nous allons toouse exemple [expérience de formation](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Training-Experiment-1) que nous avons déjà créé dans hello [Cortana Intelligence galerie](http://gallery.cortanaintelligence.com). Ouvrez cette expérience dans votre espace de travail [Azure Machine Learning Studio](https://studio.azureml.net) .

> [!NOTE]
> Dans l’ordre des toofollow avec cet exemple, vous voudrez toouse un espace de travail standard au lieu d’un espace de travail disponible. Nous allons créer un point de terminaison pour chaque client - pour un total de points de 10 terminaison - et qui nécessite un espace de travail standard, car un espace de travail gratuit est limité too3 de points de terminaison. Si vous disposez d’un espace de travail disponible, il suffit de modifier scripts hello ci-dessous tooallow pour les emplacements uniquement 3.
> 
> 

expérience de Hello utilise un **importer des données** dataset d’apprentissage de module tooimport hello *customer001.csv* à partir d’un compte de stockage Azure. Supposons que nous avons collecté des jeux de données d’apprentissage à partir de tous les emplacements de location de vélo et stockés dans hello même blob emplacement de stockage avec des noms de fichiers allant *rentalloc001.csv* trop*rentalloc10.csv* .

![image](./media/machine-learning-create-models-and-endpoints-with-powershell/reader-module.png)

Notez qu’un **sortie du Service Web** module a été ajouté toohello **Train Model** module.
Lorsque cette expérience est déployée comme un service web, point de terminaison hello associé à cette sortie retournera formé hello au format hello d’un fichier .ilearner.

Notez également que nous allons configurer un paramètre de service web hello URL que hello **importer des données** module utilise. Cela nous permet toouse hello paramètre toospecify des jeux de données tootrain hello modèle d’apprentissage pour chaque emplacement.
Nous avons effectuées, par exemple à l’aide d’une requête SQL avec un web service paramètre tooget des données à partir d’une base de données SQL Azure, ou simplement à l’aide d’autres manières une **entrée du Service Web** toopass du module dans un toohello de jeu de données de service web.

![image](./media/machine-learning-create-models-and-endpoints-with-powershell/web-service-output.png)

Maintenant, nous allons exécuter cette expérience d’apprentissage à l’aide de la valeur par défaut de hello *rental001.csv* comme hello dataset d’apprentissage. Si vous affichez la sortie de hello Hello **évaluer** module (cliquez sur la sortie de hello et sélectionnez **visualiser**), vous constatez que nous obtenons une performance acceptable de *AUC* = 0.91. À ce stade, nous sommes prêt toodeploy un service web en dehors de cette expérience d’apprentissage.

## <a name="deploy-hello-training-and-scoring-web-services"></a>Déployer la formation de hello et le score des services web
toodeploy hello formation du service web, cliquez sur hello **configurer le Service Web** bouton ci-dessous canevas de l’expérience hello **déployer le Service Web**. Nommez ce service web « Bike Rental Training ».

Nous devons maintenant service web score de toodeploy hello.
toodo, nous pouvons cliquer sur **configurer le Service Web** ci-dessous hello canevas et sélectionnez **prédictive Service Web**. Une expérience de notation est créée.
Nous devrons toomake quelques légères toomake, il fonctionne comme un service web, telles que Supprimer colonne d’étiquette hello « cnt » hello, données d’entrée et de limiter les id d’instance hello sortie tooonly hello et hello correspondant a prédit valeur.

toosave vous-même qui fonctionnent, vous pouvez ouvrir simplement hello [expérience prédictive](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Predicative-Experiment-1) Bonjour galerie qui est déjà été préparée.

le service web toodeploy hello, exécutez l’expérience prédictive hello, puis cliquez sur hello **déployer le Service Web** situé sous la zone de dessin hello. Hello nom du calcul du score du service web « Bike location de calcul de score » ».

## <a name="create-10-identical-web-service-endpoints-with-powershell"></a>Créer 10 points de terminaison de service web identiques avec PowerShell
Ce service web est fourni avec un point de terminaison par défaut. Mais nous n'intéresse pas comme point de terminaison par défaut hello, car il ne peut pas être mis à jour. Ce que nous devons toodo est toocreate 10 points de terminaison supplémentaires, une pour chaque emplacement. Nous allons pour cela utiliser PowerShell.

Tout d’abord, nous allons configurer notre environnement PowerShell :

    Import-Module .\AzureMLPS.dll
    # Assume hello default configuration file exists and is properly set toopoint toohello valid Workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

Ensuite, exécutez hello suivant de commande PowerShell :

    # Create 10 endpoints on hello scoring web service.
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpointName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

Maintenant, nous avons créé 10 points de terminaison et tous les contiennent hello même modèle formé formé sur *customer001.csv*. Vous pouvez les afficher dans le portail de gestion de hello.

![image](./media/machine-learning-create-models-and-endpoints-with-powershell/created-endpoints.png)

## <a name="update-hello-endpoints-toouse-separate-training-datasets-using-powershell"></a>Mettre à jour hello points de terminaison toouse formation distincte des groupes de données à l’aide de PowerShell
étape suivante de Hello est points de terminaison tooupdate hello avec des modèles de façon unique formés sur les données individuelles de chaque client. Mais tout d’abord nous devons tooproduce ces modèles à partir de hello **Bike location formation** service web. Passons arrière toohello **Bike location formation** service web. Nous avons besoin de son point de terminaison BES 10 fois avec 10 formation différents jeux de données dans les différents modèles de commande tooproduce 10 toocall. Nous allons utiliser hello **InovkeAmlWebServiceBESEndpoint** toodo d’applet de commande PowerShell cela.

Vous aurez également besoin des informations d’identification tooprovide pour votre compte de stockage d’objets blob dans `$configContent`, à savoir, les champs hello `AccountName`, `AccountKey` et `RelativeLocation`. Hello `AccountName` peut prendre l’une de vos noms de compte, comme dans hello **portail de gestion classique Azure** (*stockage* onglet). Une fois que vous cliquez sur un compte de stockage, ses `AccountKey` sont accessibles en appuyant sur les hello **gérer les clés d’accès** bouton en bas de hello et copie hello *clé d’accès primaire*. Hello `RelativeLocation` est stockage de hello chemin d’accès relatif tooyour où un nouveau modèle sera stocké. Par exemple, chemin d’accès de hello `hai/retrain/bike_rental/` dans le script hello sous le conteneur de tooa points nommé `hai`, et `/retrain/bike_rental/` des sous-dossiers. Actuellement, vous ne pouvez pas créer des sous-dossiers via l’interface utilisateur du portail hello, mais il n’y [plusieurs explorateurs de stockage Azure](../storage/common/storage-explorers.md) qui permettent de toodo donc. Il est recommandé de créer un nouveau conteneur dans votre hello toostore de stockage nouveaux modèles formés (fichiers .ilearner) comme suit : à partir de votre page de stockage, cliquez sur hello **ajouter** bouton bas hello et nommez-le `retrain`. En résumé, hello modifications nécessaires toohello le script ci-dessous se rapportent trop`AccountName`, `AccountKey` et `RelativeLocation` ( :`"retrain/model' + $seq + '.ilearner"`).

    # Invoke hello retraining API 10 times
    # This is hello default (and hello only) endpoint on hello training web service
    $trainingSvcEp = (Get-AmlWebServiceEndpoint -WebServiceId $trainingSvc.Id)[0];
    $submitJobRequestUrl = $trainingSvcEp.ApiLocation + '/jobs?api-version=2.0';
    $apiKey = $trainingSvcEp.PrimaryKey;
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $inputFileName = 'https://bostonmtc.blob.core.windows.net/hai/retrain/bike_rental/BikeRental' + $seq + '.csv';
        $configContent = '{ "GlobalParameters": { "URI": "' + $inputFileName + '" }, "Outputs": { "output1": { "ConnectionString": "DefaultEndpointsProtocol=https;AccountName=<myaccount>;AccountKey=<mykey>", "RelativeLocation": "hai/retrain/bike_rental/model' + $seq + '.ilearner" } } }';
        Write-Host ('training regression model on ' + $inputFileName + ' for rental location ' + $seq + '...');
        Invoke-AmlWebServiceBESEndpoint -JobConfigString $configContent -SubmitJobRequestUrl $submitJobRequestUrl -ApiKey $apiKey
    }

> [!NOTE]
> point de terminaison BES de Hello est hello pris en charge uniquement en mode pour cette opération. Vous ne pouvez pas utiliser RRE pour générer des modèles formés.
> 
> 

Comme vous pouvez le voir ci-dessus, au lieu de construire des 10 différents BES travail json fichiers de configuration, nous créer à la place de chaîne de configuration hello dynamiquement et toohello de flux *jobConfigString* paramètre Hello  **InvokeAmlWebServceBESEndpoint** applet de commande, car il n’existe réellement aucune tookeep besoin une copie sur le disque.

Si tout se passe bien, après un certain temps vous devez voir 10 fichiers .ilearner, à partir de *model001.ilearner* trop*model010.ilearner*, dans votre compte de stockage Azure. Maintenant, nous sommes prêt tooupdate notre 10 score web des points de terminaison avec ces modèles à l’aide de hello **AmlWebServiceEndpoint-correctif** applet de commande PowerShell. N’oubliez pas à nouveau que nous pouvons correctif uniquement les points de terminaison par défaut hello que nous avons créé par programme.

    # Patch hello 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '<my_blob_sas_token>'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }

L’exécution devrait être assez rapide. Une fois l’exécution de hello, nous allons ont été créés 10 points de terminaison de web prédictif service, chacune contenant un modèle formé identifie de façon unique une formation sur hello dataset tooa spécifique de location, à partir d’une expérience de formation unique. tooverify, vous pouvez essayer d’appeler ces points de terminaison à l’aide de hello **InvokeAmlWebServiceRRSEndpoint** applet de commande, en fournissant les avec hello même les données d’entrée, et vous devez vous attendre les résultats de prédiction différents de toosee étant donné que les modèles de hello sont formé avec les jeux d’apprentissage différentes.

## <a name="full-powershell-script"></a>Script PowerShell complet
Voici la liste de code source complet de hello hello :

    Import-Module .\AzureMLPS.dll
    # Assume hello default configuration file exists and properly set toopoint toohello valid workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

    # Create 10 endpoints on hello scoring web service
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpontName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

    # Invoke hello retraining API 10 times tooproduce 10 regression models in .ilearner format
    $trainingSvcEp = (Get-AmlWebServiceEndpoint -WebServiceId $trainingSvc.Id)[0];
    $submitJobRequestUrl = $trainingSvcEp.ApiLocation + '/jobs?api-version=2.0';
    $apiKey = $trainingSvcEp.PrimaryKey;
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $inputFileName = 'https://bostonmtc.blob.core.windows.net/hai/retrain/bike_rental/BikeRental' + $seq + '.csv';
        $configContent = '{ "GlobalParameters": { "URI": "' + $inputFileName + '" }, "Outputs": { "output1": { "ConnectionString": "DefaultEndpointsProtocol=https;AccountName=<myaccount>;AccountKey=<mykey>", "RelativeLocation": "hai/retrain/bike_rental/model' + $seq + '.ilearner" } } }';
        Write-Host ('training regression model on ' + $inputFileName + ' for rental location ' + $seq + '...');
        Invoke-AmlWebServiceBESEndpoint -JobConfigString $configContent -SubmitJobRequestUrl $submitJobRequestUrl -ApiKey $apiKey
    }

    # Patch hello 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '?test'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }
