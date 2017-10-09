---
title: AAA(deprecated) classifieur binaire - Azure | Documents Microsoft
description: "(obsolète) Classificateur binaire"
services: machine-learning
documentationcenter: 
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 8045038a-9dcf-44b9-a6de-7f1f8e791575
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: jaymathe
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 0496fcec9952ca243270caf67f55fe191b2dc9f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-binary-classifier"></a>(obsolète) Classificateur binaire

> [!NOTE]
> Hello Microsoft DataMarket a été supprimée et que cette API est déconseillée. 
> 
> Vous trouverez plusieurs API et les expériences d’exemple utile Bonjour [Cortana Intelligence galerie](http://gallery.cortanaintelligence.com). Pour plus d’informations sur la galerie de hello, consultez [partager et découvrir des ressources Bonjour Cortana Intelligence galerie](machine-learning-gallery-how-to-use-contribute-publish.md).

Supposons que vous avez un jeu de données et que vous souhaitez toopredict une variable dépendante binaire en fonction des variables indépendantes de hello. La « régression logistique » est une technique statistique très répandue qui est utilisée pour de telles prédictions. Variable dépendante de hello est binaire ou dichotomiques, et que p est probabilité hello de présence de caractéristique hello dignes d’intérêt. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Un scénario simple peut être où un chercheur tente toopredict si un étudiant potentiel est probablement tooaccept une université de tooa admission offre en fonction des informations (amp lycée, family revenu, état résident, sexe). résultat prédit de Hello hello la probabilité d’est étudiant potentiel de hello accepter hello admission offre. Cela [service web](https://datamarket.azure.com/dataset/aml_labs/log_regression) sera ajusté hello toohello données du modèle de régression logistique et de sorties hello la valeur de probabilité (y) pour chacun des observations hello dans les données de salutation.  

> Les utilisateurs peuvent potentiellement accéder à ce service web par le biais d’une application mobile, d’un site web ou même d’un ordinateur local, par exemple. Mais hello objectif du service web de hello est également tooserve comme exemple illustrant comment Azure Machine Learning peuvent être des services web toocreate utilisé sur le code R. Avec seulement quelques lignes de code R et quelques clics dans Azure Machine Learning Studio, vous pouvez créer une expérience avec le code R et la publier en tant que service web. service web de Hello peut ensuite être publié toohello Azure Marketplace et consommé par les utilisateurs et périphériques sur Bonjour sans configuration d’infrastructure par l’auteur de hello du service web de hello.  
> 
> 

## <a name="consumption-of-web-service"></a>Utilisation du service web
Cette hello offre de service web a prédit des valeurs de variable dépendante de hello en fonction des variables indépendantes de hello pour toutes les observations de hello. service web de Hello attend des données tooinput hello sous forme de chaîne où lignes sont séparées par des virgules (,) et les colonnes sont séparées par des points-virgules ( ;). service web de Hello attend 1 ligne à la fois et attend hello première colonne toobe hello variable dépendante. Un exemple de jeu de données pourrait ressembler à ceci :

![Exemples de données][1]

Les observations sans variable dépendante doivent être entrées en tant que « NA » pour y. Hello données d’entrée pour hello au-dessus de jeu de données serait hello après chaîne : « 1 ; 5 ; 2,1 ; 1 ; 6,0 ; 5.3 ; 2.1,0 ; 5 ; 5,0 ; 3 ; 4,1 ; 2 ; 1, NA ; 3 ; 4 ». Hello sortie hello valeur prévue pour chacune des lignes de hello repose sur les variables indépendantes de hello. 

> Ce service, comme hébergé sur hello Azure Marketplace, est un service OData ; Il peuvent être appelées par le biais des méthodes POST ou GET. 
> 
> 

Il existe plusieurs manières de consommation de service hello de manière automatique (un exemple d’application est [ici](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).

### <a name="starting-c-code-for-web-service-consumption"></a>Début du code C# pour l'utilisation du service web :
    public class Input
    {
           public string value;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
        byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
        return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
        var input = new Input() { value = TextBox1.Text };
        var json = JsonConvert.SerializeObject(input);
        var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
        var httpClient = new HttpClient();

        httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
        httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

        var response = httpClient.PostAsync(acitionUri, new StringContent(json));
        var result = response.Result.Content;
        var scoreResult = result.ReadAsStringAsync().Result;
    }


## <a name="creation-of-web-service"></a>Création du service web
> Ce service web a été créé à l’aide d’Azure Machine Learning. Pour un essai gratuit, ainsi que des vidéos de présentation relatives à la création d’expériences et à la [publication de services web](machine-learning-publish-a-machine-learning-web-service.md), consultez [azure.com/ml](http://azure.com/ml). Voici une capture d’écran d’expérience hello qui a créé un code de service et un exemple hello web pour chacun des modules hello au sein de l’expérience de hello.
> 
> 

À partir d’Azure Machine Learning, une nouvelle expérience vide a été créée et deux [Execute R Script] [ execute-r-script] extraite de modules sur l’espace de travail hello. Ce service web exécute une expérience Azure Machine Learning avec un script R sous-jacent. Il existe 2 parties toothis expérimenter : définition de schéma, modèle d’apprentissage et de calcul de score. module de première Hello définit la structure hello attendu de dataset d’entrée hello, où hello première variable est variable dépendante de hello et autres variables de hello sont indépendantes. module de deuxième Hello associe un modèle de régression logistique générique pour les données d’entrée hello.    

![Flux de l’expérience][2]

#### <a name="module-1"></a>Module 1 :
    #Schema definition  
    data <- data.frame(value = "1;2;3,1;5;6,0;8;9", stringsAsFactors=FALSE) 
    maml.mapOutputPort("data");  

#### <a name="module-2"></a>Module 2 :
    #GLM modeling   
    data <- maml.mapInputPort(1) # class: data.frame  

    data.split <- strsplit(data[1,1], ",")[[1]] 
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE) 
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE) 
    data.split <- as.data.frame(t(data.split)) data.split <- 
    data.matrix(data.split) 
    data.split <- data.frame(data.split) 

    model <- glm(data.split$V1 ~., family='binomial', data=data.split)  
    out <- data.frame(predict(model,data.split, type="response")) 
    pred1 <- as.data.frame(out) 
    group <- array(1:nrow(pred1)) 
    for (i in 1:nrow(pred1))  
        {
        if(as.numeric(pred1[i,])>0.5) {group[i]=1} 
        else {group[i]=0}
        } 
    pred2 <- as.data.frame(group) 
    maml.mapOutputPort("pred2");  


## <a name="limitations"></a>Limitations
Il s'agit d'un exemple très simple de service web de classification binaire. Comme indiqué à partir du code d’exemple hello ci-dessus, aucune erreur interception n’est implémenté et service de hello suppose que tout est une variable continue/binaire (aucune fonctionnalité catégorielles autorisée), comme hello service uniquement les entrées numériques valeurs lors de la création de hello de ce hello service Web. En outre, service de hello gère actuellement taille limitée de données, en raison de la nature de demande/réponse toohello du service web de hello fait appel et hello que hello modèle est en cours correspondre à chaque fois hello web service est appelé. 

## <a name="faq"></a>Forum Aux Questions
Pour les questions fréquemment posées sur la consommation de service web de hello ou publication toohello Azure Marketplace, consultez [ici](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-binary-classifier/binary1.png
[2]: ./media/machine-learning-r-csharp-binary-classifier/binary2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

