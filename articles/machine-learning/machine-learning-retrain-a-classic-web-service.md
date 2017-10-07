---
title: aaaRetrain un service web de classique | Documents Microsoft
description: "Découvrez comment tooprogrammatically recycler un modèle et mise à jour hello web service toouse hello qui vient d’être formé dans Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: e36e1961-9e8b-4801-80ef-46d80b140452
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: d3ba21ed75f02868535cb2fcac607643303a9554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-classic-web-service"></a>Reformer un service web Classic
Hello prédictive vous déployé le Service Web est par défaut de hello calcul du score du point de terminaison. Points de terminaison par défaut sont synchronisés avec hello d’origine de jeux d’apprentissage et le score des expériences, et par conséquent hello formé pour le point de terminaison par défaut hello ne peut pas être remplacé. service web de hello tooretrain, vous devez ajouter un nouveau service web de toohello point de terminaison. 

## <a name="prerequisites"></a>Composants requis
Vous devez avoir configuré une expérience de formation et une expérimentation prédictive comme indiqué dans [Reformer des modèles Machine Learning par programme](machine-learning-retrain-models-programmatically.md). 

> [!IMPORTANT]
> expérience de prédictive Hello doit être déployé comme un service web d’apprentissage classique. 
> 
> 

Pour plus d’informations sur le déploiement de services web, consultez [Déployer un service web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

## <a name="add-a-new-endpoint"></a>Ajouter un nouveau point de terminaison
Hello prédictive Service Web que vous avez déployé contient le point de terminaison qui est synchronisé avec l’apprentissage d’origine de hello et calcul de score formé d’expériences de calcul de score par défaut. tooupdate votre toowith de service web un nouveau modèle formé, vous devez créer un nouveau point de terminaison de score. 

toocreate un nouveau calcul de score point de terminaison sur hello prédictive Service Web pouvant être mis à jour avec le modèle formé de hello :

> [!NOTE]
> Assurez-vous que vous ajoutez toohello de point de terminaison hello prédictive Web Service, pas hello formation Web Service. Si vous avez correctement déployé à la fois un service web prédictif et un service web d’apprentissage, vous devez voir deux services web distincts répertoriés. Hello prédictive Service Web doit se terminer par « [exp prédictive.] ».
> 
> 

Il existe trois façons dans laquelle vous pouvez ajouter un nouveau service web de tooa point de terminaison :

1. Par programmation
2. Utiliser le portail de Services Web de Microsoft Azure hello
3. Utilisez hello portail Azure classic

### <a name="programmatically-add-an-endpoint"></a>Ajouter un point de terminaison par programmation
Vous pouvez ajouter des points de terminaison de score à l’aide de code hello fourni dans cette [référentiel github](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).

### <a name="use-hello-microsoft-azure-web-services-portal-tooadd-an-endpoint"></a>Utilisez tooadd portail de Services Web de Microsoft Azure hello un point de terminaison
1. Dans Machine Learning Studio, sur la colonne du volet de navigation gauche hello, cliquez sur les Services Web.
2. Au bas de hello du tableau de bord de service web hello, cliquez sur **aperçu des points de terminaison de gestion**.
3. Cliquez sur **Add**.
4. Tapez un nom et une description pour le nouveau point de terminaison hello. Sélectionnez le niveau de journalisation hello et indique si les exemples de données sont activées. Pour plus d’informations sur la journalisation, consultez [Activation de la journalisation pour les services web de Machine Learning](machine-learning-web-services-logging.md).

### <a name="use-hello-azure-classic-portal-tooadd-an-endpoint"></a>Utilisez hello tooadd portail classique Azure un point de terminaison
1. Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com).
2. Dans le menu de gauche hello, cliquez sur **Machine Learning**.
3. Sous Nom, cliquez sur votre espace de travail, puis sur **Services web**.
4. Sous Nom, cliquez sur **Modèle de recensement [exp. prédictive]**.
5. Au bas de hello de page de hello, cliquez sur **ajouter le point de terminaison**. Pour plus d’informations sur l’ajout de points de terminaison, consultez [Création de points de terminaison](machine-learning-create-endpoint.md). 

## <a name="update-hello-added-endpoints-trained-model"></a>Hello de mise à jour ajoutée formé du point de terminaison
processus de reconversion hello toocomplete, vous devez mettre à jour modèle formé de hello de hello nouveau point de terminaison que vous avez ajouté.

* Si vous avez ajouté le nouveau point de terminaison hello à l’aide du portail Azure classic de hello, vous pouvez cliquez sur nom hello nouveau du point de terminaison dans le portail de hello, puis hello **UpdateResource** lien URL de hello tooget vous avez besoin de modèle de tooupdate hello du point de terminaison.
* Si vous avez ajouté le point de terminaison hello à l’aide des exemples de code hello, cela inclut l’emplacement de l’URL d’aide hello identifié par hello *HelpLocationURL* valeur dans la sortie de hello.

URL du chemin d’accès tooretrieve hello :

1. Copiez et collez l’URL de hello dans votre navigateur.
2. Cliquez sur le lien de ressource de la mise à jour de hello.
3. Copiez hello poster une URL de demande de correctif hello. Par exemple :
   
     URL DU CORRECTIF : https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2

Vous pouvez maintenant utiliser hello de tooupdate hello formé calcul du score du point de terminaison que vous avez créé précédemment.

Hello suivant l’exemple de code montre comment toouse hello *BaseLocation*, *RelativeLocation*, *SasBlobToken*et de correctif logiciel tooupdate hello point de terminaison URL.

    private async Task OverwriteModel()
    {
        var resourceLocations = new
        {
            Resources = new[]
            {
                new
                {
                    Name = "Census Model [trained model]",
                    Location = new AzureBlobDataReference()
                    {
                        BaseLocation = "https://esintussouthsus.blob.core.windows.net/",
                        RelativeLocation = "your endpoint relative location", //from hello output, for example: “experimentoutput/8946abfd-79d6-4438-89a9-3e5d109183/8946abfd-79d6-4438-89a9-3e5d109183.ilearner”
                        SasBlobToken = "your endpoint SAS blob token" //from hello output, for example: “?sv=2013-08-15&sr=c&sig=37lTTfngRwxCcf94%3D&st=2015-01-30T22%3A53%3A06Z&se=2015-01-31T22%3A58%3A06Z&sp=rl”
                    }
                }
            }
        };

        using (var client = new HttpClient())
        {
            client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", apiKey);

            using (var request = new HttpRequestMessage(new HttpMethod("PATCH"), endpointUrl))
            {
                request.Content = new StringContent(JsonConvert.SerializeObject(resourceLocations), System.Text.Encoding.UTF8, "application/json");
                HttpResponseMessage response = await client.SendAsync(request);

                if (!response.IsSuccessStatusCode)
                {
                    await WriteFailedResponse(response);
                }

                // Do what you want with a successful response here.
            }
        }
    }

Hello *apiKey* et hello *endpointUrl* pour l’appel de hello peut être obtenu à partir du tableau de bord de point de terminaison.

Hello valeur Hello *nom* paramètre dans *ressources* doit hello de correspondance de nom de ressource de hello enregistré formé dans expérience prédictive de hello. hello tooget nom de la ressource :

1. Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com).
2. Dans le menu de gauche hello, cliquez sur **Machine Learning**.
3. Sous Nom, cliquez sur votre espace de travail, puis sur **Services web**.
4. Sous Nom, cliquez sur **Modèle de recensement [exp. prédictive]**.
5. Cliquez sur le nouveau point de terminaison hello que vous avez ajouté.
6. Dans le tableau de bord du point de terminaison hello, cliquez sur **mise à jour de ressource**.
7. Sur la page de mise à jour de documentation sur les API de ressources hello pour le service web de hello, vous pouvez trouver hello **nom de la ressource** sous **être mise à jour des ressources**.

Si votre jeton SAS expire avant la fin de la mise à jour du point de terminaison hello, vous devez effectuer une opération GET avec l’Id de tâche de hello tooobtain un nouveau jeton.

Lorsque le code de hello correctement exécutée, nouveau point de terminaison hello doit démarrer à l’aide de modèle de hello reformé dans environ 30 secondes.

## <a name="summary"></a>Résumé
À l’aide de hello réapprentissage des API, vous pouvez mettre à jour modèle formé de hello d’un Service Web prédictif, permettant ainsi des scénarios tels que :

* Nouvel apprentissage périodique d’un modèle avec de nouvelles données.
* Distribution d’un modèle de toocustomers avec comme objectif hello leur permettant de former le modèle de hello à l’aide de leurs propres données.

## <a name="next-steps"></a>Étapes suivantes
[Résolution des problèmes de hello recyclage d’un service web classique de Azure Machine Learning](machine-learning-troubleshooting-retraining-models.md)

