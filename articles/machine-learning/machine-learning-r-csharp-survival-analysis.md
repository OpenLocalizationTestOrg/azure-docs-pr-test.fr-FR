---
title: AAA(deprecated) analyse de survie avec Azure Machine Learning | Documents Microsoft
description: "(obsolète) Probabilité d'occurrence d'un événement d'analyse de survie"
services: machine-learning
documentationcenter: 
author: zhangya
manager: jhubbard
editor: cgronlun
ms.assetid: a142fc45-cdfb-4971-910e-05dab8bc699e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: zhangya
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: af946d8df5ba650a9d74fbabbe3b15d3a07dd508
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-survival-analysis"></a>(obsolète) Analyse de survie

> [!NOTE]
> Hello Microsoft DataMarket a été supprimée et que cette API est déconseillée. 
> 
> Vous trouverez plusieurs API et les expériences d’exemple utile Bonjour [Cortana Intelligence galerie](http://gallery.cortanaintelligence.com). Pour plus d’informations sur la galerie de hello, consultez [partager et découvrir des ressources Bonjour Cortana Intelligence galerie](machine-learning-gallery-how-to-use-contribute-publish.md).

Dans nombreux scénarios, le résultat de principal de hello en cours d’évaluation est événement tooan hello dignes d’intérêt. En d’autres termes, les question hello « lorsque cet événement se produit ? » va-t-il se produire ? ». Par exemple, vous devez prendre en compte les situations où les données de salutation décrivent hello temps (jours, années, consommation, etc.) jusqu'à ce que hello événements d’intérêt (Échec de remplissage de frein, degré de bloc reçu, RECHUTE de maladie) se produit. Dans les données de salutation, chaque instance représente un objet spécifique (un patient, un étudiant, une voiture, etc.).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Cela [service web](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) répond à la question de hello « quelle est la probabilité de hello hello des événements d’intérêt se produit en n fois pour l’objet x ? » En fournissant un modèle d’analyse de survie, ce service web permet aux utilisateurs toosupply tootrain hello EDM et le tester. le thème principal de l’expérience de hello Hello est toomodel hello hello écoulé Durée jusqu'à ce que l’événement hello d’intérêt se produit. 

> Les utilisateurs peuvent potentiellement accéder à ce service web par le biais d’une application mobile, d’un site web ou même d’un ordinateur local, par exemple. Mais hello objectif du service web de hello est également tooserve comme exemple illustrant comment Azure Machine Learning peuvent être des services web toocreate utilisé sur le code R. Avec seulement quelques lignes de code R et quelques clics dans Azure Machine Learning Studio, vous pouvez créer une expérience avec le code R et la publier en tant que service web. service web de Hello peut ensuite être publié toohello Azure Marketplace et consommé par les utilisateurs et périphériques sur Bonjour sans configuration d’infrastructure par l’auteur de hello du service web de hello.  
> 
> 

## <a name="consumption-of-web-service"></a>Utilisation du service web
schéma de données d’entrée de Hello du service web de hello est présenté dans hello tableau suivant. Six informations sont nécessaires en tant qu’entrée de hello : données d’apprentissage, données de test, d’intérêt, index hello de dimension de « heure », index hello de dimension de le « événement » et les types de variables hello (continues ou facteur). données d’apprentissage Hello sont représentées par une chaîne, où les lignes de hello sont séparées par des virgules, et les colonnes de hello sont séparées par des points-virgules. nombre de Hello des fonctionnalités de données de hello est flexible. Tous les éléments hello dans la chaîne d’entrée de hello doivent être numériques. Dans les données d’apprentissage hello, dimension hello « temps » indique hello plusieurs unités de temps (jours, années, consommation, etc.) s’est écoulé depuis le point de départ hello Hello étudier (un patient recevoir des programmes de traitement de médicament, une étude de bloc de départ étudiant, une voiture démarrage toobe fonction, etc.) jusqu'à ce que hello événements d’intérêt (patient hello retour de l’utilisation de toodrug, degré de bloc hello étudiant obtention hello, véhicule hello frein remplissage échec, etc.) se produit. dimension de « événement » Hello indique si les événements hello d’intérêt se produit à fin hello d’étude de hello. Une valeur de « événement = 1 » signifie que les événements d’intérêt de hello se produit au moment de hello indiqué par la dimension « temps » de hello ; « événement = 0 » signifie que les événements d’intérêt de hello n’a pas eu lieu après le temps hello indiqué par la dimension « temps » de hello.

* trainingdata : il s’agit d’une chaîne de caractères. Les lignes sont séparées par des virgules et les colonnes sont séparées par des points-virgules. Chaque ligne inclut la dimension « temporelle », la dimension de l'« évènement » et les variables de prédiction.
* testingdata : il s’agit d’une ligne de données qui contient les variables de prédiction pour un objet particulier.
* time_of_interest - temps hello de n d’intérêt.
* index_time - index de colonne hello hello « dimension de temps » (à partir de 1).
* index_event - index de colonne hello de dimension de « événement » hello (à partir de 1).
* variable_types : une chaîne de caractères séparés par des points-virgules. 0 représente les variables continues et 1 représente les variables facteur.

sortie de Hello est la probabilité de hello d’un événement qui se produisent à une heure spécifique. 

> Ce service, comme hébergé sur hello Azure Marketplace, est un service OData ; Il peuvent être appelées par le biais des méthodes POST ou GET. 
> 
> 

Il existe plusieurs manières de consommation de service hello de manière automatique (un exemple d’application est [ici](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)). 

### <a name="starting-c-code-for-web-service-consumption"></a>Début du code C# pour l'utilisation du service web :
    public class Input
    {
            public string trainingdata;
            public string testingdata;
            public string timeofinterest;
            public string indextime;
            public string indexevent;
            public string variabletypes;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { trainingdata = TextBox1.Text, testingdata = TextBox2.Text, timeofinterest = TextBox3.Text, indextime = TextBox4.Text, indexevent = TextBox5.Text, variabletypes = TextBox6.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }




interprétation de Hello de ce test est la suivante. En supposant que l’objectif hello de données de hello est toomodel hello écoulé jusqu'à hello retourner toodrug utilisation de patients hello qui ont reçu un des programmes de traitement hello deux. Hello sortie de lectures de service web hello : patients en cours de 35 ans, ayant précédente médicament traitement 2 fois, en prenant le programme de traitement long résidentielle hello, et avec utilisation héroïne et cocaïne, probabilité hello de retour de l’utilisation de médicament toohello est % 95.64 par jour 500.

## <a name="creation-of-web-service"></a>Création du service web
> Ce service web a été créé à l’aide d’Azure Machine Learning. Pour un essai gratuit, ainsi que des vidéos de présentation relatives à la création d’expériences et à la [publication de services web](machine-learning-publish-a-machine-learning-web-service.md), consultez [azure.com/ml](http://azure.com/ml). Voici une capture d’écran d’expérience hello qui a créé un code de service et un exemple hello web pour chacun des modules hello au sein de l’expérience de hello.
> 
> 

À partir d’Azure Machine Learning, une nouvelle expérience vide a été créée et deux [Execute R Script] [ execute-r-script] modules ont été collectés dans l’espace de travail hello. schéma de données Hello a été créé avec une simple [Execute R Script][execute-r-script], qui définit le schéma de données d’entrée hello pour le service web de hello. Ce module est ensuite lié toohello deuxième [Execute R Script] [ execute-r-script] module, qui majeure de travail. Ce module réalise le prétraitement des données, la création du modèle et les prédictions. Dans l’étape de prétraitement hello données, les données d’entrée hello représentées par une longue chaîne sont transformées et converties en une trame de données. À l’étape de génération de modèle hello, un package R externe « survival_2.37-7.zip » est tout d’abord installé pour effectuer l’analyse de survie. Fonction de « coxph » hello est ensuite exécutée après une tâche de traitement des données de série. Détails de Hello de fonction de « coxph » hello pour l’analyse de survie peuvent être lus à partir de la documentation de hello R. À l’étape de prédiction hello, une instance de test est fournie dans le modèle formé de hello avec fonction de « surfit » hello et courbe de survie hello pour cette instance de test est généré en tant que variable de « curve ». Enfin, probabilité hello de temps hello dignes d’intérêt est obtenue. 

### <a name="experiment-flow"></a>Flux de l’expérience :
![Flux de l’expérience][1]

#### <a name="module-1"></a>Module 1 :
    #Data schema with example data (replaced with data from web service)
    trainingdata="53;1;29;0;0;3,79;1;34;0;1;2,45;1;27;0;1;1,37;1;24;0;1;1,122;1;30;0;1;1,655;0;41;0;0;1,166;1;30;0;0;3,227;1;29;0;0;3,805;0;30;0;0;1,104;1;24;0;0;1,90;1;32;0;0;1,373;1;26;0;0;1,70;1;36;0;0;1”
    testingdata="35;2;1;1"
    time_of_interest="500"
    index_time="1"
    index_event="2"

    # 0 - continuous; 1 -  factor
    variable_types="0;0;1;1"

    sampleInput=data.frame(trainingdata,testingdata,time_of_interest,index_time,index_event,variable_types)

    maml.mapOutputPort("sampleInput"); #send data toooutput port

#### <a name="module-2"></a>Module 2 :
    #Read data from input port
    data <- maml.mapInputPort(1) 
    colnames(data) <- c("trainingdata","testingdata","time_of_interest","index_time","index_event","variable_types")

    # Preprocessing training data
    traindingdata=data$trainingdata
    y=strsplit(as.character(data$trainingdata),",")
    n_row=length(unlist(y))
    z=sapply(unlist(y), strsplit, ";", simplify = TRUE)
    mydata <- data.frame(matrix(unlist(z), nrow=n_row, byrow=T), stringsAsFactors=FALSE)
    n_col=ncol(mydata)

    # Preprocessing testing data
    testingdata=as.character(data$testingdata)
    testingdata=unlist(strsplit(testingdata,";"))

    # Preprocessing other input parameters
    time_of_interest=data$time_of_interest
    time_of_interest=as.numeric(as.character(time_of_interest))
    index_time = data$index_time
    index_event = data$index_event
    variable_types = data$variable_types

    # Necessary R packages
    install.packages("src/packages_survival/survival_2.37-7.zip",lib=".",repos=NULL,verbose=TRUE)
    library(survival)

    # Prepare toobuild model
    attach(mydata)

    for (i in 1:n_col){ mydata[,i]=as.numeric(mydata[,i])} 
    d_time=paste("X",index_time,sep = "")
    d_event=paste("X",index_event,sep = "")
    v_time_event <- c(d_time,d_event)
    v_predictors = names(mydata)[!(names(mydata) %in% v_time_event)]

    variable_types = unlist(strsplit(as.character(variable_types),";"))

    len = length(v_predictors)
    c="" # Construct hello execution string
    for (i in 1:len){
    if(i==len){
    if(variable_types[i]!=0){ c=paste(c, "factor(",v_predictors[i],")",sep="")}
     else{ c=paste(c, v_predictors[i])}
    }else{
    if(variable_types[i]!=0){c=paste(c, "factor(",v_predictors[i],") + ",sep="")}
    else{c=paste(c, v_predictors[i],"+")}
    }
    }
    f=paste("coxph(Surv(",d_time,",",d_event,") ~")
    f=paste(f,c)
    f=paste(f,", data=mydata )")

    # Fit a Cox proportional hazards model and get hello predicted survival curve for a testing instance 
    fit=eval(parse(text=f))

    testingdata = as.data.frame(matrix(testingdata, ncol=len,byrow = TRUE),stringsAsFactors=FALSE)
    names(testingdata)=v_predictors
    for (i in 1:len){ testingdata[,i]=as.numeric(testingdata[,i])}

    curve=survfit(fit,testingdata)

    # Based on user input, find hello event occurrence probability
    position_closest=which.min(abs(prob_event$time - time_of_interest))

    if(prob_event[position_closest,"time"]==time_of_interest){# exact match
    output=prob_event[position_closest,"prob"]
    }else{# not exact match
    if(time_of_interest>max(prob_event$time)){
    output=prob_event[position_closest,"prob"]
    }else if(time_of_interest<min(prob_event$time)){
    output=prob_event[position_closest,"prob"]
    }else{output=(prob_event[position_closest,"prob"]+prob_event[position_closest+1,"prob"])/2}
    }

    #Pull out results toosend tooweb service
    output=paste(round(100*output, 2), "%") 
    maml.mapOutputPort("output"); #output port




## <a name="limitations"></a>Limitations
Ce service web accepte uniquement les valeurs numériques sous forme de variables de fonctionnalité (colonnes). colonne de « événement » Hello peut prendre la valeur 0 ou 1. colonne de « time » Hello doit toobe un entier positif.

## <a name="faq"></a>Forum Aux Questions
Pour les questions fréquemment posées sur la consommation de service web de hello ou publication toohello Azure Marketplace, consultez [ici](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-survival-analysis/survive_img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

