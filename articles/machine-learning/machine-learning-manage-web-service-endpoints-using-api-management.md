---
title: "aaaLearn comment toomanage AzureML web services à l’aide de la gestion des API | Documents Microsoft"
description: "Un guide indiquant comment toomanage AzureML web services à l’aide de la gestion des API."
keywords: apprentissage automatique,gestion des api
services: machine-learning
documentationcenter: 
author: roalexan
manager: jhubbard
editor: 
ms.assetid: 05150ae1-5b6a-4d25-ac67-fb2f24a68e8d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/19/2017
ms.author: roalexan
ms.openlocfilehash: 6e764fbfd71be6cc908a1c8d3d8889969fc651a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="learn-how-toomanage-azureml-web-services-using-api-management"></a>Découvrez comment toomanage AzureML web services à l’aide de la gestion des API
## <a name="overview"></a>Vue d'ensemble
Ce guide vous explique comment démarrer tooquickly à l’aide de gestion des API toomanage vos services web de AzureML.

## <a name="what-is-azure-api-management"></a>Qu’est-ce que Gestion des API Azure ?
Gestion des API Azure est un service Azure qui vous permet de gérer vos points de terminaison d’API REST en définissant l’accès utilisateur, la limitation d’utilisation et la surveillance du tableau de bord. Cliquez [ici](https://azure.microsoft.com/services/api-management/) pour plus d’informations sur Gestion des API Azure. Cliquez sur [ici](../api-management/api-management-get-started.md) pour obtenir un guide sur comment tooget démarrer avec la gestion des API Azure. Cet autre guide, sur lequel ce guide est basé, couvre plus de rubriques, notamment les configurations de notification, la tarification, la gestion des réponses, l’authentification des utilisateurs, la création de produits, les abonnements pour développeur et le tableau de bord d’utilisation.

## <a name="what-is-azureml"></a>Présentation d’AzureML
AzureML est un service Azure pour l’apprentissage qui vous permet de tooeasily build, déployer et partager des solutions d’analytique avancée. Cliquez [ici](https://azure.microsoft.com/services/machine-learning/) pour plus d’informations sur AzureML.

## <a name="prerequisites"></a>Composants requis
toocomplete ce guide, vous devez :

* Un compte Azure. Si vous n’avez pas un compte Azure, cliquez sur [ici](https://azure.microsoft.com/pricing/free-trial/) pour plus d’informations sur la façon de toocreate un compte d’évaluation gratuit.
* Un compte AzureML. Si vous n’avez pas un compte AzureML, cliquez sur [ici](https://studio.azureml.net/) pour plus d’informations sur la façon de toocreate un compte d’évaluation gratuit.
* espace de travail Hello, service et api_key pour une expérience AzureML déployée comme un service web. Cliquez sur [ici](machine-learning-create-experiment.md) pour plus d’informations sur comment toocreate un AzureML faire des essais. Cliquez sur [ici](machine-learning-publish-a-machine-learning-web-service.md) pour plus d’informations sur comment toodeploy un AzureML faire des essais en tant qu’un service web. Ou bien, l’annexe A comporte des instructions pour toocreate et test d’un simple AzureML tester et déploiement en tant que service web.

## <a name="create-an-api-management-instance"></a>Création d'une instance Gestion des API
Vous trouverez ci-dessous les étapes hello pour à l’aide de la gestion des API toomanage votre service web de AzureML. Créez d’abord une instance de service. Connectez-vous à toohello [portail classique](https://manage.windowsazure.com/) et cliquez sur **nouveau** > **des Services d’application** > **gestion des API**  >  **Créer**.

![create-instance](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-instance.png)

Spécifiez une **URL** unique. Ce guide utilise **demoazureml** – vous devez toochoose quelque chose d’autre. Choisissez hello souhaité **abonnement** et **région** pour votre instance de service. Après avoir effectué vos sélections, cliquez sur le bouton suivant de hello.

![create-service-1](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-1.png)

Spécifiez une valeur pour hello **nom de l’organisation**. Ce guide utilise **demoazureml** – vous devez toochoose quelque chose d’autre. Entrez votre adresse de messagerie dans hello **e-mail administrateur** champ. Cette adresse de messagerie est utilisée pour les notifications de hello système de gestion des API.

![create-service-2](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-2.png)

Cliquez sur toocreate de case à cocher hello votre instance de service. *Elle occupe minutes toothirty pour une nouvelle toobe de service créé*.

## <a name="create-hello-api"></a>Créer des API de hello
Une fois créé, l’instance de service hello hello prochaine étape consiste toocreate hello API. Une API se compose d’un ensemble d’opérations pouvant être appelées à partir d’une application cliente. Opérations d’API sont traitées tooexisting des services web. Ce guide crée des API qui toohello proxy des services web AzureML RRS et BES existants.

API est créés et configurés à partir du portail de publication d’API hello, qui est accessible via le portail classique Azure de hello. tooreach hello sélectionnez portail, du serveur de publication de votre instance de service.

![select-service-instance](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-service-instance.png)

Cliquez sur **gérer** Bonjour portail classique Azure pour votre service de gestion des API.

![manage-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/manage-service.png)

Cliquez sur **API** de hello **gestion des API** menu sur hello gauche, puis cliquez sur **ajouter les API**.

![api-management-menu](./media/machine-learning-manage-web-service-endpoints-using-api-management/api-management-menu.png)

Type **AzureML démonstration API** comme hello **nom de l’API Web**. Type **https://ussouthcentral.services.azureml.net** comme hello **URL du service Web**. Type **azureml-demo** comme hello **suffixe d’URL d’API Web**. Vérifiez **HTTPS** comme hello **URL d’API Web** schéma. Sélectionnez **Starter** comme **produit**. Lorsque vous avez terminé, cliquez sur **enregistrer** toocreate hello API.

![add-new-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-new-api.png)

## <a name="add-hello-operations"></a>Ajouter des opérations de hello
Cliquez sur **l’opération d’ajout** tooadd operations toothis API.

![add-operation](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-operation.png)

Hello **nouvelle opération** fenêtre s’affiche et hello **Signature** est activée par défaut.

## <a name="add-rrs-operation"></a>Ajout d’une opération RRS
Tout d’abord créer une opération de service de AzureML RRS de hello. Sélectionnez **POST** comme hello **verbe HTTP**. Type **/workspaces/ {espace de travail} /services/ {service} / exécuter ? api-version = {apiversion} & détails = {détails}** comme hello **modèle d’URL**. Type **RR exécuter** comme hello **nom d’affichage**.

![add-rrs-operation-signature](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-signature.png)

Cliquez sur **réponses** > **ajouter** sur hello gauche et sélectionnez **200 OK**. Cliquez sur **enregistrer** toosave cette opération.

![add-rrs-operation-response](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-response.png)

## <a name="add-bes-operations"></a>Ajout d’opérations BES
Captures d’écran ne sont pas incluses pour hello les opérations BES lorsqu’ils sont toothose très similaire pour l’ajout d’opération de RR hello.

### <a name="submit-but-not-start-a-batch-execution-job"></a>Envoi (et non démarrage) d’un travail d’exécution de lot
Cliquez sur **l’opération d’ajout** tooadd hello AzureML BES opération toohello API. Sélectionnez **POST** pour hello **verbe HTTP**. Type **/workspaces/ {espace de travail} /services/ {service} / travaux ? api-version = {apiversion}** pour hello **modèle d’URL**. Type **BES soumettre** pour hello **nom d’affichage**. Cliquez sur **réponses** > **ajouter** sur hello gauche et sélectionnez **200 OK**. Cliquez sur **enregistrer** toosave cette opération.

### <a name="start-a-batch-execution-job"></a>Démarrage d’une tâche d’exécution de lot
Cliquez sur **l’opération d’ajout** tooadd hello AzureML BES opération toohello API. Sélectionnez **POST** pour hello **verbe HTTP**. Type **/workspaces/ {espace de travail} /services/ {service} /jobs/ {jobid} / démarrer ? api-version = {apiversion}** pour hello **modèle d’URL**. Type **BES Démarrer** pour hello **nom d’affichage**. Cliquez sur **réponses** > **ajouter** sur hello gauche et sélectionnez **200 OK**. Cliquez sur **enregistrer** toosave cette opération.

### <a name="get-hello-status-or-result-of-a-batch-execution-job"></a>Obtenir l’état de hello ou le résultat d’une tâche d’exécution de lot
Cliquez sur **l’opération d’ajout** tooadd hello AzureML BES opération toohello API. Sélectionnez **obtenir** pour hello **verbe HTTP**. Type **/workspaces/ {espace de travail} /services/ {service} /jobs/ {jobid} ? api-version = {apiversion}** pour hello **modèle d’URL**. Type **BES état** pour hello **nom d’affichage**. Cliquez sur **réponses** > **ajouter** sur hello gauche et sélectionnez **200 OK**. Cliquez sur **enregistrer** toosave cette opération.

### <a name="delete-a-batch-execution-job"></a>Suppression d’une tâche d’exécution de lot
Cliquez sur **l’opération d’ajout** tooadd hello AzureML BES opération toohello API. Sélectionnez **supprimer** pour hello **verbe HTTP**. Type **/workspaces/ {espace de travail} /services/ {service} /jobs/ {jobid} ? api-version = {apiversion}** pour hello **modèle d’URL**. Type **BES supprimer** pour hello **nom d’affichage**. Cliquez sur **réponses** > **ajouter** sur hello gauche et sélectionnez **200 OK**. Cliquez sur **enregistrer** toosave cette opération.

## <a name="call-an-operation-from-hello-developer-portal"></a>Appeler une opération de hello portail des développeurs
Opérations peuvent être appelées directement depuis le portail des développeurs hello, qui fournit un moyen pratique de tooview et tester le fonctionnement d’une API hello. Dans cette étape du guide, vous appelez hello **RR exécuter** méthode qui a été ajouté toohello **AzureML démonstration API**. Cliquez sur **portail des développeurs** à partir du menu de hello en hello haut à droite de hello portail classique.

![developer-portal](./media/machine-learning-manage-web-service-endpoints-using-api-management/developer-portal.png)

Cliquez sur **API** dans le menu du haut hello, puis cliquez sur **AzureML démonstration API** opérations de hello toosee disponibles.

![demoazureml-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/demoazureml-api.png)

Sélectionnez **RR exécuter** pour l’opération de hello. Cliquez sur **Essayer**.

![try-it](./media/machine-learning-manage-web-service-endpoints-using-api-management/try-it.png)

Pour les paramètres de requête, tapez votre **espace de travail**, **service**, **2.0** pour hello **apiversion**, et **true**pour hello **détails**. Vous pouvez trouver votre **espace de travail** et **service** dans le tableau de bord hello AzureML web service (consultez **tester un service web de hello** dans l’annexe A).

Pour les en-têtes de requête, cliquez sur **Ajouter en-tête** et tapez **Content-Type** et **application/json**, puis cliquez sur **Ajouter en-tête** et tapez **Autorisation** et **Porteur<YOUR AZUREML SERVICE API-KEY>**. Vous pouvez trouver votre **clé api** dans le tableau de bord hello AzureML web service (consultez **tester un service web de hello** dans l’annexe A).

Type **{« Entrées » : {« entrée1 » : {« ColumnNames » : « Valeurs » [« Col2 »] : [[« Ceci est une bonne journée »]]}}, « GlobalParameters » : {}}** hello corps de requête.

![azureml-demo-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/azureml-demo-api.png)

Cliquez sur **Envoyer**.

![Envoyer](./media/machine-learning-manage-web-service-endpoints-using-api-management/send.png)

Une fois une opération est appelée, le portail des développeurs hello affiche hello **URL demandée** à partir du service principal de hello, hello **état de la réponse**, hello **les en-têtes de réponse**, et n’importe quel **contenu de la réponse**.

![response-status](./media/machine-learning-manage-web-service-endpoints-using-api-management/response-status.png)

## <a name="appendix-a---creating-and-testing-a-simple-azureml-web-service"></a>Annexe A - Création et test d’un service web AzureML simple
### <a name="creating-hello-experiment"></a>Création d’expérience de hello
Vous trouverez ci-dessous les étapes de hello pour la création d’une expérience simple de AzureML et de les déployer comme un service web. Hello web service prend comme entrée une colonne de texte arbitraire et retourne un jeu de fonctionnalités représentées en tant qu’entiers. Par exemple :

| Texte | Texte haché |
| --- | --- |
| C’est une belle journée |1 1 2 2 0 2 0 1 |

Tout d’abord, à l’aide d’un navigateur de votre choix, accédez à : [https://studio.azureml.net/](https://studio.azureml.net/) et entrez votre toolog des informations d’identification dans. Ensuite, créez une nouvelle expérience vide.

![search-experiment-templates](./media/machine-learning-manage-web-service-endpoints-using-api-management/search-experiment-templates.png)

Renommez-le trop**SimpleFeatureHashingExperiment**. Développez **Datasets enregistrés** et faites glisser **Critiques de livres d’Amazon** sur votre expérimentation.

![simple-feature-hashing-experiment](./media/machine-learning-manage-web-service-endpoints-using-api-management/simple-feature-hashing-experiment.png)

Développez **Transformation des données** et **Manipulation** et faites glisser **Sélectionner des colonnes dans le jeu de données** sur votre expérimentation. Se connecter **critiques à partir d’Amazon** trop**sélectionner les colonnes dans le jeu de données**.

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/project-columns.png)

Cliquez sur **Sélectionner des colonnes dans le jeu de données**, puis sur **Exécuter le sélecteur de colonne** et sélectionnez **Col2**. Cliquez sur hello coche tooapply ces modifications.

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-columns.png)

Développez **texte Analytique** et faites glisser **Feature Hashing** sur l’expérience de hello. Se connecter **sélectionner les colonnes dans le jeu de données** trop**Feature Hashing**.

![connect-project-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/connect-project-columns.png)

Type **3** pour hello **taille de bit hachage**. Cela crée 8 (23) colonnes.

![hashing-bitsize](./media/machine-learning-manage-web-service-endpoints-using-api-management/hashing-bitsize.png)

À ce stade, vous souhaiterez peut-être tooclick **exécuter** expérience de hello tootest.

![Exécuter](./media/machine-learning-manage-web-service-endpoints-using-api-management/run.png)

### <a name="create-a-web-service"></a>Création d’un service web
Maintenant, créez un service web. Développez **Service Web** et faites glisser **Entrée** sur votre expérimentation. Se connecter **entrée** trop**Feature Hashing**. Faites également glisser **Sortie** sur votre expérience. Se connecter **sortie** trop**Feature Hashing**.

![output-to-feature-hashing](./media/machine-learning-manage-web-service-endpoints-using-api-management/output-to-feature-hashing.png)

Cliquez sur **Publier le service Web**.

![publish-web-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/publish-web-service.png)

Cliquez sur **Oui** expérience de hello toopublish.

![yes-to-publish](./media/machine-learning-manage-web-service-endpoints-using-api-management/yes-to-publish.png)

### <a name="test-hello-web-service"></a>Tester un service web de hello
Un service web AzureML se compose de points de terminaison RRS (service de requête/réponse) et BES (service d’exécution de lot). RSS est conçu pour l’exécution synchrone. BES est conçu pour l’exécution de tâches asynchrone. tootest votre site web de service avec une source de Python hello exemple ci-dessous, vous devrez peut-être toodownload et installation Bonjour Azure SDK pour Python (voir : [comment tooinstall Python](../python-how-to-install.md)).

Vous devez également hello **espace de travail**, **service**, et **api_key** de votre expérience pour la source d’exemple hello ci-dessous. Vous pouvez trouver l’espace de travail hello et le service en cliquant sur **demande/réponse** ou **l’exécution par lots** pour votre expérience dans le tableau de bord hello web service.

![find-workspace-and-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-workspace-and-service.png)

Vous pouvez trouver hello **api_key** en cliquant sur votre expérience dans le tableau de bord hello web service.

![find-api-key](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-api-key.png)

#### <a name="test-rrs-endpoint"></a>Test du point de terminaison RRS
##### <a name="test-button"></a>Bouton de test
Un point de terminaison facilement tootest hello RR est tooclick **Test** sur le tableau de bord hello web service.

![test](./media/machine-learning-manage-web-service-endpoints-using-api-management/test.png)

Tapez **C’est une belle journée** en **col2**. Cliquez sur hello coche.

![enter-data](./media/machine-learning-manage-web-service-endpoints-using-api-management/enter-data.png)

Le résultat suivant doit s’afficher :

![sample-output](./media/machine-learning-manage-web-service-endpoints-using-api-management/sample-output.png)

##### <a name="sample-code"></a>Exemple de code
Une autre façon tootest vos enregistrements de ressources est à partir de votre code client. Si vous cliquez sur **demande/réponse** sur hello du tableau de bord et défilement toohello bas, vous verrez les exemples de code pour c#, Python et R. Vous verrez également la syntaxe hello de hello RR demande, y compris les URI de demande hello, en-têtes et corps.

Ce guide fournit un exemple Python opérationnel. Vous devez toomodify avec hello **espace de travail**, **service**, et **api_key** de votre expérience.

    import urllib2
    import json
    workspace = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE WORKSPACE ID>"
    service = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE SERVICE ID>"
    api_key = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE API KEY>"
    data = {
    "Inputs": {
        "input1": {
            "ColumnNames": ["Col2"],
            "Values": [ [ "This is a good day" ] ]
        },
    },
    "GlobalParameters": { }
    }
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace + "/services/" + service + "/execute?api-version=2.0&details=true"
    headers = {'Content-Type':'application/json', 'Authorization':('Bearer '+ api_key)}
    body = str.encode(json.dumps(data))
    try:
        req = urllib2.Request(url, body, headers)
        response = urllib2.urlopen(req)
        result = response.read()
        print "result:" + result
            except urllib2.HTTPError, error:
        print("hello request failed with status code: " + str(error.code))
        print(error.info())
        print(json.loads(error.read()))

#### <a name="test-bes-endpoint"></a>Test du point de terminaison BES
Cliquez sur **l’exécution du lot** sur hello du tableau de bord et défilement toohello bas. Vous verrez un exemple de code pour c#, Python et R. Vous verrez également syntaxe hello de hello BES demandes toosubmit un travail, démarrer une tâche, obtenir le statut de hello ou les résultats d’une tâche et supprimer un travail.

Ce guide fournit un exemple Python opérationnel. Vous devez toomodify avec hello **espace de travail**, **service**, et **api_key** de votre expérience. En outre, vous devez toomodify hello **nom de compte de stockage**, **clé de compte de stockage**, et **nom de conteneur de stockage**. Enfin, vous aurez besoin d’emplacement de hello toomodify Hello **fichier d’entrée** et l’emplacement de hello Hello **fichier de sortie**.

    import urllib2
    import json
    import time
    from azure.storage import *
    workspace = "<REPLACE WITH YOUR WORKSPACE ID>"
    service = "<REPLACE WITH YOUR SERVICE ID>"
    api_key = "<REPLACE WITH hello API KEY FOR YOUR WEB SERVICE>"
    storage_account_name = "<REPLACE WITH YOUR AZURE STORAGE ACCOUNT NAME>"
    storage_account_key = "<REPLACE WITH YOUR AZURE STORAGE KEY>"
    storage_container_name = "<REPLACE WITH YOUR AZURE STORAGE CONTAINER NAME>"
    input_file = "<REPLACE WITH hello LOCATION OF YOUR INPUT FILE>" # Example: C:\\mydata.csv
    output_file = "<REPLACE WITH hello LOCATION OF YOUR OUTPUT FILE>" # Example: C:\\myresults.csv
    input_blob_name = "mydatablob.csv"
    output_blob_name = "myresultsblob.csv"
    def printHttpError(httpError):
    print("hello request failed with status code: " + str(httpError.code))
    print(httpError.info())
    print(json.loads(httpError.read()))
    return
    def saveBlobToFile(blobUrl, resultsLabel):
    print("Reading hello result from " + blobUrl)
    try:
        response = urllib2.urlopen(blobUrl)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    with open(output_file, "w+") as f:
        f.write(response.read())
    print(resultsLabel + " have been written toohello file " + output_file)
    return
    def processResults(result):
    first = True
    results = result["Results"]
    for outputName in results:
        result_blob_location = results[outputName]
        sas_token = result_blob_location["SasBlobToken"]
        base_url = result_blob_location["BaseLocation"]
        relative_url = result_blob_location["RelativeLocation"]
        print("hello results for " + outputName + " are available at hello following Azure Storage location:")
        print("BaseLocation: " + base_url)
        print("RelativeLocation: " + relative_url)
        print("SasBlobToken: " + sas_token)
        if (first):
            first = False
            url3 = base_url + relative_url + sas_token
            saveBlobToFile(url3, "hello results for " + outputName)
    return

    def invokeBatchExecutionService():
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace +"/services/" + service +"/jobs"
    blob_service = BlobService(account_name=storage_account_name, account_key=storage_account_key)
    print("Uploading hello input tooblob storage...")
    data_to_upload = open(input_file, "r").read()
    blob_service.put_blob(storage_container_name, input_blob_name, data_to_upload, x_ms_blob_type="BlockBlob")
    print "Uploaded hello input tooblob storage"
    input_blob_path = "/" + storage_container_name + "/" + input_blob_name
    connection_string = "DefaultEndpointsProtocol=https;AccountName=" + storage_account_name + ";AccountKey=" + storage_account_key
    payload =  {
        "Input": {
            "ConnectionString": connection_string,
            "RelativeLocation": input_blob_path
        },
        "Outputs": {
            "output1": { "ConnectionString": connection_string, "RelativeLocation": "/" + storage_container_name + "/" + output_blob_name },
        },
        "GlobalParameters": {
        }
    }
        body = str.encode(json.dumps(payload))
    headers = { "Content-Type":"application/json", "Authorization":("Bearer " + api_key)}
    print("Submitting hello job...")
    # submit hello job
    req = urllib2.Request(url + "?api-version=2.0", body, headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    result = response.read()
    job_id = result[1:-1] # remove hello enclosing double-quotes
    print("Job ID: " + job_id)
    # start hello job
    print("Starting hello job...")
    req = urllib2.Request(url + "/" + job_id + "/start?api-version=2.0", "", headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    url2 = url + "/" + job_id + "?api-version=2.0"

    while True:
        print("Checking hello job status...")
        # If you are using Python 3+, replace urllib2 with urllib.request in hello follwing code
        req = urllib2.Request(url2, headers = { "Authorization":("Bearer " + api_key) })
        try:
            response = urllib2.urlopen(req)
        except urllib2.HTTPError, error:
            printHttpError(error)
            return
        result = json.loads(response.read())
        status = result["StatusCode"]
        print "status:" + status
        if (status == 0 or status == "NotStarted"):
            print("Job " + job_id + " not yet started...")
        elif (status == 1 or status == "Running"):
            print("Job " + job_id + " running...")
        elif (status == 2 or status == "Failed"):
            print("Job " + job_id + " failed!")
            print("Error details: " + result["Details"])
            break
        elif (status == 3 or status == "Cancelled"):
            print("Job " + job_id + " cancelled!")
            break
        elif (status == 4 or status == "Finished"):
            print("Job " + job_id + " finished!")
            processResults(result)
            break
        time.sleep(1) # wait one second
    return
    invokeBatchExecutionService()
