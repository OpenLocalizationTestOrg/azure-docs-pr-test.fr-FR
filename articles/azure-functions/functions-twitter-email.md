---
title: "aaaCreate une fonction qui s’intègre à Azure Logic Apps | Documents Microsoft"
description: "Créez une fonction qui s’intègre à Azure Logic Apps et Services cognitifs Azure sentiment de tweet toocategorize et envoyer des notifications lorsque l’opinion est faible."
services: functions, logic-apps, cognitive-services
keywords: "flux de travail, applications cloud, services cloud, processus d’entreprise, intégration de systèmes, intégration d’applications d’entreprise, IAE"
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
ms.assetid: 60495cc5-1638-4bf0-8174-52786d227734
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: e176bd946af9a3684b3ad0e4b1bed1c3ee344019
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-that-integrates-with-azure-logic-apps"></a>Créer une fonction qui s’intègre avec Azure Logic Apps

Les fonctions Azure s’intègre avec Azure Logic Apps Bonjour logique de concepteur d’applications. Cette intégration vous permet d’utiliser hello puissance de calcul fonctions dans les orchestrations avec d’autres services Azure et des services tiers. 

Ce didacticiel vous montre comment toouse fonctionne avec la logique d’applications et Services cognitifs Azure sentiment tooanalyze de billets de Twitter. Une fonction HTTP déclenchée classe tweet en vert, jaune ou rouge en fonction de score d’opinion hello. Un courrier électronique est envoyé lors de la détection de sentiments négatifs. 

![Image : deux premières étapes de l’application dans le Concepteur d’applications logiques](media/functions-twitter-email/designer1.png)

Ce didacticiel vous montre comment effectuer les opérations suivantes :

> [!div class="checklist"]
> * Créez un compte Cognitive Services.
> * Créer une fonction qui classe le sentiment des tweets.
> * Créer une application de la logique qui se connecte tooTwitter.
> * Ajouter une application de sentiment détection toohello logique. 
> * Se connecter (fonction) toohello application hello logique.
> * Envoyer un courrier électronique en fonction de la réponse hello à partir de la fonction hello.

## <a name="prerequisites"></a>Composants requis

+ Un compte [Twitter](https://twitter.com/) actif. 
+ Un compte [Outlook.com](https://outlook.com/) (pour l’envoi de notifications).
+ Cette rubrique utilise en tant que ses ressources de hello de point de départ créés dans [créer votre première fonction de hello Azure portal](functions-create-first-azure-function.md).  
Si vous n’avez pas déjà fait, effectuez ces toocreate de maintenant étapes votre application de la fonction.

## <a name="create-a-cognitive-services-account"></a>Créez un compte Cognitive Services

Un compte de Services cognitifs est sentiment de hello toodetect obligatoire de tweets en cours d’analyse.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).

2. Cliquez sur hello **nouveau** bouton se trouve sur le coin supérieur gauche hello Hello portail Azure.

3. Cliquez sur **Données + analyse** > **Cognitive Services**. Ensuite, utiliser les paramètres de hello en tant que spécifié dans la table de hello, accepter les termes du contrat de hello et vérifiez **toodashboard du code confidentiel**.

    ![Panneau Créer un compte Cognitive](media/functions-twitter-email/cog_svcs_account.png)

    | Paramètre      |  Valeur suggérée   | Description                                        |
    | --- | --- | --- |
    | **Nom** | MyCognitiveServicesAccnt | Choisissez un nom de compte unique. |
    | **Type d’API** | API Analyse de texte | API utilisée tooanalyze texte.  |
    | **Emplacement** | Ouest des États-Unis | Actuellement, seule la région **États-Unis de l’Ouest** est disponible pour l’analyse de texte. |
    | **Niveau tarifaire** | F0 | Commencer par la couche la plus basse de hello. Si vous manquez d’appels, mettre à l’échelle de niveau supérieur de tooa.|
    | **Groupe de ressources** | myResourceGroup | Utilisez hello même groupe de ressources pour tous les services dans ce didacticiel.|

4. Cliquez sur **créer** toocreate votre compte. Une fois hello compte est créé, cliquez sur Nouveau Services cognitifs compte épinglé toohello tableau de bord. 

5. Dans hello compte, cliquez sur **clés**, puis copiez la valeur hello **clé 1** et l’enregistrer. Vous utilisez cette logique de clé tooconnect hello application tooyour compte Services cognitifs. 
 
    ![Clés](media/functions-twitter-email/keys.png)

## <a name="create-hello-function"></a>Créer la fonction hello

Fonctions fournit un toooffload excellent moyen des tâches de traitement dans un flux de travail applications logique. Ce didacticiel utilise un HTTP déclenchée fonction tooprocess tweet sentiment les scores à partir des Services cognitifs et retournent une valeur de catégorie.  

1. Développez votre application de la fonction, cliquez sur hello  **+**  bouton ensuite trop**fonctions**, cliquez sur hello **HTTPTrigger** modèle. Type `CategorizeSentiment` pour la fonction hello **nom** et cliquez sur **créer**.

    ![Panneau Function Apps, Fonctions +](media/functions-twitter-email/add_fun.png)

2. Remplacez contenu hello du fichier de run.csx hello hello suivant de code, puis cliquez sur **enregistrer**:

    ```c#
    using System.Net;
    
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
    {
        // hello sentiment category defaults too'GREEN'. 
        string category = "GREEN";
    
        // Get hello sentiment score from hello request body.
        double score = await req.Content.ReadAsAsync<double>();
        log.Info(string.Format("hello sentiment score received is '{0}'.",
                    score.ToString()));
    
        // Set hello category based on hello sentiment score.
        if (score < .3)
        {
            category = "RED";
        }
        else if (score < .6)
        {
            category = "YELLOW";
        }
        return req.CreateResponse(HttpStatusCode.OK, category);
    }
    ```
    Le code de cette fonction retourne une catégorie de couleur en fonction de score d’opinion hello reçu dans la demande hello. 

3. fonction de hello tootest, cliquez sur **Test** à onglet hello hello tooexpand plus à droite. Tapez la valeur `0.2` pour hello **corps de la demande**, puis cliquez sur **exécuter**. La valeur **rouge** est retourné dans le corps de réponse de hello de hello. 

    ![Tester la fonction hello Bonjour portail Azure](./media/functions-twitter-email/test.png)

Vous disposez maintenant d’une fonction permettant de classer les scores des sentiments. Ensuite, créez une application logique qui intègre votre fonction avec vos comptes Twitter et Cognitive Services. 

## <a name="create-a-logic-app"></a>Créer une application logique   

1. Dans l’hello portail Azure, cliquez sur hello **nouveau** bouton se trouve sur le coin supérieur gauche hello Hello portail Azure.

2. Cliquez sur **Intégration d’entreprise** > **Application logique**. Vérifiez ensuite utiliser les paramètres hello comme spécifié dans la table de hello, **code confidentiel toodashboard**, puis cliquez sur **créer**.
 
4. Ensuite, tapez un **nom** comme `TweetSentiment`, utiliser des paramètres de hello comme spécifié dans la table de hello, acceptez les termes du contrat de hello et vérifier **toodashboard du code confidentiel**.

    ![Créer l’application logique Bonjour portail Azure](./media/functions-twitter-email/new_logicApp.png)

    | Paramètre      |  Valeur suggérée   | Description                                        |
    | ----------------- | ------------ | ------------- |
    | **Nom** | TweetSentiment | Choisissez un nom approprié pour votre application. |
    | **Groupe de ressources** | myResourceGroup | API utilisée tooanalyze texte.  |
    | **Emplacement** | Est des États-Unis | Choisissez un tooyou fermer d’emplacement. |
    | **Groupe de ressources** | myResourceGroup | Choisissez hello le même groupe de ressources existant comme avant.|

4. Cliquez sur **créer** toocreate votre application logique. Une fois l’application hello est créée, cliquez sur votre nouveau tableau de bord toohello épinglée d’application logique. Dans le Concepteur d’applications de logique de hello, faites défiler, puis cliquez sur hello **application logique vide** modèle. 

    ![Modèle d’applications logiques vides](media/functions-twitter-email/blank.png)

Vous pouvez maintenant utiliser le Concepteur d’applications logique tooadd services et des déclencheurs tooyour application hello.

## <a name="connect-tootwitter"></a>Se connecter tooTwitter

Commencez par créer une connexion de tooyour compte Twitter. Hello logique application interroge tweets, lequel déclenchent hello application toorun.

1. Dans le Concepteur de hello, cliquez sur hello **Twitter** de service, puis cliquez sur hello **lors de la validation d’un tweet nouvelle** déclencheur. Connectez-vous à tooyour compte Twitter et autoriser Logic Apps toouse votre compte.

2. Utiliser les paramètres de déclencheur hello Twitter comme spécifié dans la table de hello. 

    ![Paramètres du connecteur Twitter](media/functions-twitter-email/azure_tweet.png)

    | Paramètre      |  Valeur suggérée   | Description                                        |
    | ----------------- | ------------ | ------------- |
    | **Texte de recherche** | #Azure | Utilisez un #sqlhelp qui est souvent assez utilisé pour toogenerate des tweets nouveau dans l’intervalle de salutation choisie. Lorsque l’utilisation de niveau gratuit de hello et votre #sqlhelp est trop populaire, vous pouvez utiliser rapidement les transactions hello dans votre compte de Services cognitifs. |
    | **Fréquence** | Minute | unité de fréquence Hello utilisée pour l’interrogation Twitter.  |
    | **Intervalle** | 15 | Hello du délai entre les demandes de Twitter, en unités de fréquence. |

3.  Cliquez sur **enregistrer** tooconnect tooyour compte Twitter. 

Votre application est maintenant connecté tooTwitter. Ensuite, vous vous connectez sentiment de hello toodetect tootext analytique de tweet collectées.

## <a name="add-sentiment-detection"></a>Ajouter la détection de sentiments

1. Cliquez sur **Nouvelle étape**, puis sélectionnez **Ajouter une action**.

    ![Nouvelle étape, puis Ajouter une action](media/functions-twitter-email/new_step.png)

2. Dans **choisir une action**, cliquez sur **texte Analytique**, puis cliquez sur hello **détecter sentiment** action.

    ![Detect Sentiment (Détecter le sentiment)](media/functions-twitter-email/detect_sent.png)

3. Tapez un nom de connexion comme `MyCognitiveServicesConnection`, collez la clé de hello pour vos Services cognitifs compte que vous avez enregistré, puis cliquez sur **créer**.  

4. Cliquez sur **texte tooanalyze** > **tweetez-texte**, puis cliquez sur **enregistrer**.  

    ![Detect Sentiment (Détecter le sentiment)](media/functions-twitter-email/ds_tta.png)

Maintenant que la détection de sentiment est configurée, vous pouvez ajouter une fonction de tooyour de connexion qui consomme la sortie de score d’opinion hello.

## <a name="connect-sentiment-output-tooyour-function"></a>Connecter la sortie sentiment tooyour (fonction)

1. Bonjour logique de concepteur d’applications, cliquez sur **nouvelle étape** > **ajouter une action**, puis cliquez sur **Azure fonctions**. 

2. Cliquez sur **choisissez une fonction d’Azure**, sélectionnez hello **CategorizeSentiment** fonction que vous avez créé précédemment.  

    ![Zone Azure Functions montrant Choisir une fonction Azure](media/functions-twitter-email/choose_fun.png)

3. Dans **Corps de la requête**, cliquez sur **Score**, puis sur **Enregistrer**.

    ![Score](media/functions-twitter-email/trigger_score.png)

À présent, votre fonction est déclenchée lorsqu’un score d’opinion est envoyé à partir de l’application logique de hello. Une catégorie de couleur est retournée toohello logique application par fonction hello. Ensuite, vous ajoutez une notification par courrier électronique qui est envoyée lorsqu’une valeur d’indice de sentiment de **rouge** est retournée à partir de la fonction hello. 

## <a name="add-email-notifications"></a>Ajouter des notifications par courrier électronique

Hello dernière partie du flux de travail hello est tootrigger un courrier électronique lors de l’opinion de hello est catégorisée en tant que _rouge_. Cette rubrique utilise un connecteur Outlook.com. Vous pouvez effectuer toouse des étapes similaires un connecteur Gmail ou Outlook Office 365.   

1. Bonjour logique de concepteur d’applications, cliquez sur **nouvelle étape** > **ajouter une condition**. 

2. Cliquez sur **Choisir une valeur**, puis cliquez sur **Corps**. Sélectionnez **Est égal à**, cliquez sur **Choisir une valeur** et saisissez `RED`, puis cliquez sur **Enregistrer**. 

    ![Ajouter une application de la logique de toohello de condition.](media/functions-twitter-email/condition.png)

3. Dans **si Oui, ne rien faire**, cliquez sur **ajouter une action**, recherchez `outlook.com`, cliquez sur **envoyer un courrier électronique**et vous connecter tooyour Outlook.com compte.
    
    ![Choisissez une action de condition de hello.](media/functions-twitter-email/outlook.png)

    > [!NOTE]
    > Si vous n’avez pas de compte Outlook.com, vous pouvez choisir un autre connecteur, comme Gmail ou Office 365 Outlook

4. Bonjour **envoyer un courrier électronique** action, utiliser les paramètres de messagerie hello comme spécifié dans la table de hello. 

    ![Configurer la messagerie de hello pour l’envoi de hello une action de courrier électronique.](media/functions-twitter-email/sendemail.png)

    | Paramètre      |  Valeur suggérée   | Description  |
    | ----------------- | ------------ | ------------- |
    | **To** | Saisissez votre adresse de messagerie | adresse de messagerie Hello qui reçoit la notification de hello. |
    | **Objet** | Sentiment de tweet négatif détecté  | ligne d’objet Hello de notification par courrier électronique de hello.  |
    | **Corps** | Texte du tweet, Emplacement | Cliquez sur hello **tweetez-texte** et **emplacement** paramètres. |

5.  Cliquez sur **Enregistrer**.

Maintenant que le flux de travail hello est terminée, vous pouvez activer l’application logique de hello et consultez la fonction hello au travail.

## <a name="test-hello-workflow"></a>Flux de travail de test hello

1. Dans le Concepteur d’application logique de hello, cliquez sur **exécuter** toostart hello application.

2. Dans la colonne de gauche hello, cliquez sur **vue d’ensemble** état hello toosee application logique de hello. 
 
    ![État d’exécution de l’application logique](media/functions-twitter-email/over1.png)

3. (Facultatif) Cliquez sur une des hello exécute toosee détails de l’exécution de hello.

4. Fonction, tooyour, afficher les journaux de hello et vérifiez que les valeurs de sentiment reçus et traités.
 
    ![Affichez les journaux de fonction](media/functions-twitter-email/sent.png)

5. Lorsqu’un sentiment potentiellement négatif est détecté, vous recevez un courrier électronique. Si vous n’avez pas reçu un message électronique, vous pouvez modifier chaque fois tooreturn de code de fonction hello rouge :

        return req.CreateResponse(HttpStatusCode.OK, "RED");

    Après avoir vérifié les notifications par courrier électronique, modifier le code d’origine de toohello précédent :

        return req.CreateResponse(HttpStatusCode.OK, category);

    > [!IMPORTANT]
    > Une fois que vous avez terminé ce didacticiel, vous devez désactiver l’application logique de hello. En désactivant l’application hello, vous éviter d’être facturés pour les exécutions et que vous utilisez des transactions hello dans votre compte de Services cognitifs.

Maintenant, vous savez combien il est facile toointegrate des fonctions dans un flux de travail Logic Apps.

## <a name="disable-hello-logic-app"></a>Désactiver l’application logique de hello

application de la logique de hello toodisable, cliquez sur **vue d’ensemble** puis cliquez sur **désactiver** haut hello écran hello. Cela arrête hello logique application en cours d’exécution et la comptabilisation des frais sans supprimer l’application hello. 

![Journaux de fonction](media/functions-twitter-email/disable-logic-app.png)

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez appris à :

> [!div class="checklist"]
> * Créez un compte Cognitive Services.
> * Créer une fonction qui classe le sentiment des tweets.
> * Créer une application de la logique qui se connecte tooTwitter.
> * Ajouter une application de sentiment détection toohello logique. 
> * Se connecter (fonction) toohello application hello logique.
> * Envoyer un courrier électronique en fonction de la réponse hello à partir de la fonction hello.

Avancer toolearn de didacticiel suivant toohello comment toocreate une API sans serveur de votre fonction.

> [!div class="nextstepaction"] 
> [Créer une API sans serveur à l’aide d’Azure Functions](functions-create-serverless-api.md)

toolearn en savoir plus sur les applications de la logique, consultez [Azure Logic Apps](../logic-apps/logic-apps-what-are-logic-apps.md).

