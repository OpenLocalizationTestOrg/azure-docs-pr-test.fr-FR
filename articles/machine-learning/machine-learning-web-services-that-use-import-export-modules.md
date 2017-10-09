---
title: "aaaUsing importer/exporter des données dans les services web Azure Machine Learning | Documents Microsoft"
description: "Découvrez comment toouse hello toosend de modules de données d’importation et exportation de données et recevoir des données d’un service web."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: 3a7ac351-ebd3-43a1-8c5d-18223903d08e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: 176380259b15cb338ede61c7f28ba2296b35dd52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-azure-ml-web-services-that-use-data-import-and-data-export-modules"></a>Déploiement de services web Azure ML utilisant les modules d’importation et d’exportation des données

Lorsque vous créez une expérience prédictive, vous ajoutez généralement une entrée et une sortie de service web. Lorsque vous déployez expérience de hello, consommateurs peuvent envoyer et recevoir des données de service web de hello via hello entrées et sorties. Pour certaines applications, les données d’un consommateur peuvent être disponibles à partir d’un flux de données ou figurer déjà dans une source de données externe tels que le stockage d’objets blob Azure. Dans ces cas, elles n’ont pas besoin de lire ni d’écrire les données en utilisant des entrées et sorties de service web. Au lieu de cela, ils peuvent utilisent des données de tooread hello Service de l’exécution de lot (BES) à partir de la source de données hello à l’aide d’un module d’importation de données et écrire hello score résultats tooa emplacement de données différentes à l’aide d’un module d’exporter des données.

Hello importer des données et des modules de données d’exportation, peut lire et écrire des données toovarious fournissent des emplacements, par exemple, une URL Web via HTTP, une requête Hive, une base de données SQL Azure, stockage de Table Azure, le stockage Blob Azure, un flux de données ou une base de données SQL locale.

Cette rubrique utilise hello « exemple 5 : Evaluate Train, Test, pour la Classification binaire : jeu de données adulte « exemple et suppose hello le jeu de données a déjà été chargé dans une table SQL Azure nommée censusdata.

## <a name="create-hello-training-experiment"></a>Créer l’expérience de formation hello
Lorsque vous ouvrez hello « exemple 5 : Evaluate Train, Test, pour la Classification binaire : jeu de données adulte « exemple de jeu de données utilise hello exemple adulte Classification binaire revenu de recensement. Et expérience hello dans la zone de dessin hello ressemblera similaire toohello suivant l’image :

![Configuration initiale de l’expérience de hello.](./media/machine-learning-web-services-that-use-import-export-modules/initial-look-of-experiment.png)

données de salutation tooread à partir de la table de SQL Azure hello :

1. Suppression du module de dataset hello.
2. Dans la zone de recherche de composants hello, tapez l’importation.
3. À partir de la liste des résultats hello, ajoutez un *importer des données* module toohello expérimenter la zone de dessin.
4. Connectez la sortie de hello *importer des données* entrée hello de module de hello *Clean Missing Data* module.
5. Dans le volet Propriétés, sélectionnez **base de données SQL Azure** Bonjour **Source de données** liste déroulante.
6. Bonjour **nom du serveur de base de données**, **nom de la base de données**, **nom d’utilisateur**, et **mot de passe** , saisissez les informations appropriées pour hello votre base de données.
7. Dans le champ de requête de base de données hello, entrez hello suivant la requête.
   
     select [age],
   
        [workclass],
        [fnlwgt],
        [education],
        [education-num],
        [marital-status],
        [occupation],
        [relationship],
        [race],
        [sex],
        [capital-gain],
        [capital-loss],
        [hours-per-week],
        [native-country],
        [income]
     from dbo.censusdata;
8. Au bas de hello du canevas de l’expérience hello, cliquez sur **exécuter**.

## <a name="create-hello-predictive-experiment"></a>Créer l’expérience de prédictive hello
Ensuite, vous configurez les expérience prédictive hello à partir duquel vous déployez votre service web.

1. Au bas de hello du canevas de l’expérience hello, cliquez sur **configurer le Service Web** et sélectionnez **Service Web prédictive [recommandé]**.
2. Supprimer hello *entrée du Service Web* et *des modules de sortie du Service Web* à partir de l’expérience de prédictive hello. 
3. Dans la zone de recherche de composants hello, tapez l’exportation.
4. À partir de la liste des résultats hello, ajoutez un *exporter les données* module toohello expérimenter la zone de dessin.
5. Connectez la sortie de hello *Score Model* entrée hello de module de hello *exporter les données* module. 
6. Dans le volet Propriétés, sélectionnez **base de données SQL Azure** dans la liste déroulante destination de données hello.
7. Bonjour **nom du serveur de base de données**, **nom de la base de données**, **le nom de compte d’utilisateur Server**, et **mot de passe utilisateur serveur** , saisissez Hello les informations appropriées pour votre base de données.
8. Bonjour **liste des toobe colonnes enregistrée séparées par des virgules** , tapez Scored Labels.
9. Bonjour **champ de nom de table de données**, tapez dbo. ScoredLabels. Si la table de hello n’existe pas, il est créé lors de l’expérience de hello est exécutée ou service web de hello est appelé.
10. Bonjour **liste des colonnes de table de données séparées par des virgules** champ, tapez ScoredLabels.

Lorsque vous écrivez une application que les appels hello service web final, vous souhaiterez toospecify une table de requête ou la destination d’entrée différente au moment de l’exécution. tooconfigure ces entrées et sorties, utilisez Bonjour paramètres de Service Web fonctionnalité tooset Bonjour *importer des données* module *source de données* propriété et hello *exporter les données* mode propriété de destination de données.  Pour plus d’informations sur les paramètres de Service Web, consultez hello [entrée de paramètres de Service Web AzureML](https://blogs.technet.microsoft.com/machinelearning/2014/11/25/azureml-web-service-parameters/) sur hello Cortana Intelligence et Machine Learning Blog.

hello tooconfigure paramètres de Service Web pour la requête d’importation hello et la table de destination hello :

1. Dans le volet de propriétés hello pour hello *importer des données* module, cliquez sur icône de hello en hello haut à droite de hello **requête de base de données** champ, puis sélectionnez **définir en tant que paramètre de service web**.
2. Dans le volet de propriétés hello pour hello *exporter les données* module, cliquez sur icône de hello en hello haut à droite de hello **nom de table de données** champ, puis sélectionnez **définir en tant que paramètre de service web**.
3. En bas de hello Hello *exporter les données* volet de propriétés du module, Bonjour **paramètres de Service Web** section, cliquez sur requête de base de données et renommer la requête.
4. Cliquez sur le champ **Nom de la table de données** et renommez-le **Table**.

Lorsque vous avez terminé, votre expérience doit ressembler similaire toohello suivant l’image :

![Aspect final de l’expérience.](./media/machine-learning-web-services-that-use-import-export-modules/experiment-with-import-data-added.png)

Vous pouvez à présent déployer hello expérience comme un service web.

## <a name="deploy-hello-web-service"></a>Déployer le service web de hello
Vous pouvez déployer tooeither un service web classique ou nouveau.

### <a name="deploy-a-classic-web-service"></a>Déployer comme un service web classique
toodeploy comme un Service Web classique et créer une application tooconsume il :

1. Bas hello du canevas de l’expérience hello, cliquez sur Exécuter.
2. Hello exécuter a terminé, cliquez sur **déployer le Service Web** et sélectionnez **déployer le Service Web [standard]**.
3. Tableau de bord de service web hello, recherchez votre clé API. Copier et l’enregistrer toouse plus tard.
4. Bonjour **le point de terminaison par défaut** , cliquez sur hello **l’exécution par lots** hello tooopen de lien Page d’aide API.
5. Créez une application console en C# dans Visual Studio : **Nouveau** > **Projet** > **Visual C#** > **Bureau classique Windows** > **Application console (.NET Framework)**.
6. Sur la Page d’aide de l’API de hello, recherche hello **exemple de Code** section bas hello de page de hello.
7. Copiez et collez hello, exemple de code c# dans votre fichier Program.cs et de supprimer le stockage d’objets blob toohello toutes les références.
8. Mettre à jour la valeur hello hello *apiKey* variable avec clé hello API enregistré précédemment.
9. Recherchez hello demande déclaration et la mise à jour hello valeurs des paramètres de Service Web qui sont passés toohello *importer des données* et *exporter les données* modules. Dans ce cas, vous utilisez la requête d’origine de hello, mais définissez un nouveau nom de table.
   
        var request = new BatchExecutionRequest() 
        {           
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable2" },
            }
        };
10. Exécutez l’application hello. 

À la fin de hello exécuter, une nouvelle table est ajoutée contenant hello score des résultats de la base de données toohello.

### <a name="deploy-a-new-web-service"></a>Déployer comme un nouveau service web

> [!NOTE] 
> toodeploy un nouveau service web, vous devez disposer des autorisations suffisantes dans hello abonnement toowhich vous déployez le service web de hello. Pour plus d’informations, consultez [gérer un service Web à l’aide du portail de Services Web de Azure Machine Learning hello](machine-learning-manage-new-webservice.md). 

toodeploy comme un Service Web et de créer une application tooconsume il :

1. Au bas de hello du canevas de l’expérience hello, cliquez sur **exécuter**.
2. Hello exécuter a terminé, cliquez sur **déployer le Service Web** et sélectionnez **déployer le Service Web [nouveau]**.
3. Sur la page de déployer une expérience de hello, entrez un nom pour votre service web, sélectionnez un plan de tarification, puis cliquez sur **déployer**.
4. Sur hello **Quickstart** , cliquez sur **consommer**.
5. Bonjour **exemple de Code** , cliquez sur **lot**.
6. Créez une application console en C# dans Visual Studio : **Nouveau** > **Projet** > **Visual C#** > **Bureau classique Windows** > **Application console (.NET Framework)**.
7. Copiez et collez le code d’exemple hello c# dans votre fichier Program.cs.
8. Mettre à jour la valeur hello hello *apiKey* variable avec hello **clé primaire** situé dans hello **les informations de base de la consommation** section.
9. Recherchez hello *scoreRequest* les valeurs hello déclaration et la mise à jour des paramètres de Service Web qui sont passés toohello *importer des données* et *exporter les données* modules. Dans ce cas, vous utilisez la requête d’origine de hello, mais définissez un nouveau nom de table.
   
        var scoreRequest = new
        {       
            Inputs = new Dictionary<string, StringTable>()
            {
            },
            GlobalParameters = new Dictionary<string, string>() {
                { "Query", @"select [age], [workclass], [fnlwgt], [education], [education-num], [marital-status], [occupation], [relationship], [race], [sex], [capital-gain], [capital-loss], [hours-per-week], [native-country], [income] from dbo.censusdata" },
                { "Table", "dbo.ScoredTable3" },
            }
        };
10. Exécutez l’application hello. 

