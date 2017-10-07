---
title: "science aaaData sur hello une Machine virtuelle pour la science des données Linux | Documents Microsoft"
description: "Comment tooperform scientifiques de données commun plusieurs tâches avec hello VM de science des données Linux."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 34ef0b10-9270-474f-8800-eecb183bbce4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev;paulsh
ms.openlocfilehash: 78764825f2e834fa4ddb7fdc2f59418dbe736e1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="data-science-on-hello-linux-data-science-virtual-machine"></a>Recherche de données sur hello une Machine virtuelle pour la science des données Linux
Cette procédure pas à pas vous montre comment tooperform scientifiques de données commun plusieurs tâches avec hello VM de science des données Linux. Hello Machine virtuelle de science des données Linux (DSVM) est une image de machine virtuelle disponible sur Azure est préinstallé avec un ensemble d’outils utilisés pour l’analytique des données et l’apprentissage. les composants logiciels de clé Hello sont répertoriés dans hello [hello de configurer une Machine virtuelle pour la science des données Linux](machine-learning-data-science-linux-dsvm-intro.md) rubrique. Hello image de machine virtuelle rend facile tooget commencé à faire la science des données en quelques minutes, sans avoir tooinstall et configurer chacun des outils de hello individuellement. Vous pouvez facilement évoluer hello machine virtuelle, si nécessaire et l’arrêter inutilisés. Cette ressource est donc flexible et économique.

tâches courantes relatives aux données présentées dans cette procédure pas à pas Hello suivent étapes hello hello [processus de science des données équipe](https://azure.microsoft.com/documentation/learning-paths/data-science-process/). Ce processus fournit une science toodata approche systématique permettant aux équipes de chercheurs de données tooeffectively collaborer hello du cycle de vie de la création d’applications intelligentes. processus de science des données Hello fournit également une infrastructure itérative pour la science des données qui peuvent être suivie par une personne.

Nous analysons hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) jeu de données dans cette procédure pas à pas. Il s’agit d’un ensemble d’adresses de messagerie qui sont marqués comme étant du courrier indésirable ou ham (ce qui signifie qu’ils ne sont pas courrier indésirable), et contient également des statistiques sur le contenu des e-mails de hello hello. statistiques Hello inclus sont abordés plus loin dans hello mais une seule section.

## <a name="prerequisites"></a>Composants requis
Avant de pouvoir utiliser un ordinateur de virtuel de science des données Linux, vous devez disposer de hello :

* Un **abonnement Azure**. Si vous n’en avez pas déjà un, voir [Créez votre compte Azure gratuit](https://azure.microsoft.com/free/).
* Une [**machine virtuelle de science des données Linux**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm). Pour plus d’informations sur la configuration de cet ordinateur virtuel, consultez [hello de configurer une Machine virtuelle pour la science des données Linux](machine-learning-data-science-linux-dsvm-intro.md).
* [X2Go](http://wiki.x2go.org/doku.php) installé sur votre ordinateur et une session XFCE ouverte. Pour plus d’informations sur l’installation et la configuration d’un **client X2Go**, consultez [Installation et configuration du client X2Go](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client). 
* Un **compte AzureML**. Si vous n’avez pas encore, inscrivez-vous pour un nouveau à hello [page d’accueil AzureML](https://studio.azureml.net/). Il existe un toohelp de niveau d’utilisation libre commencer.

## <a name="download-hello-spambase-dataset"></a>Télécharger le jeu de données hello spambase
Hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) jeu de données est un ensemble relativement réduit de données qui contient des 4601 uniquement exemples. Il s’agit d’un toouse taille pratique lors de la démonstration que certaines des fonctionnalités clés de hello Hello VM de science des données tel qu’il conserve les besoins en ressources hello modeste.

> [!NOTE]
> Cette procédure pas à pas a été créée sur une machine virtuelle de science des données Linux de taille D2 v2. Cette taille DSVM est capable de gérer des procédures hello dans cette procédure pas à pas.
>
>

Si vous avez besoin de davantage d’espace de stockage, vous pouvez créer des disques supplémentaires et les attacher tooyour machine virtuelle. Ces disques utilisent le stockage Azure persistant, afin de leurs données sont conservées même lorsque le serveur de hello est remise en service dues tooresizing ou est arrêté. tooadd un disque et attacher tooyour VM, suivez les instructions de hello dans [ajouter un tooa de disque Linux VM](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Ces étapes utilisent hello Azure Interface de ligne (Azure), qui est déjà installé sur hello DSVM. Par conséquent, ces procédures possible entièrement à partir hello machine virtuelle proprement dite. Une autre option de stockage tooincrease est toouse [fichiers Azure](../storage/files/storage-how-to-use-files-linux.md).

les données de salutation toodownload, ouvrez une fenêtre de terminal et exécuter cette commande :

    wget http://archive.ics.uci.edu/ml/machine-learning-databases/spambase/spambase.data

fichier téléchargé de Hello ne pas avoir une ligne d’en-tête, nous allons donc créer un autre fichier qui n’a pas un en-tête. Exécuter cette commande toocreate un fichier avec les en-têtes appropriés hello :

    echo 'word_freq_make, word_freq_address, word_freq_all, word_freq_3d,word_freq_our, word_freq_over, word_freq_remove, word_freq_internet,word_freq_order, word_freq_mail, word_freq_receive, word_freq_will,word_freq_people, word_freq_report, word_freq_addresses, word_freq_free,word_freq_business, word_freq_email, word_freq_you, word_freq_credit,word_freq_your, word_freq_font, word_freq_000, word_freq_money,word_freq_hp, word_freq_hpl, word_freq_george, word_freq_650, word_freq_lab,word_freq_labs, word_freq_telnet, word_freq_857, word_freq_data,word_freq_415, word_freq_85, word_freq_technology, word_freq_1999,word_freq_parts, word_freq_pm, word_freq_direct, word_freq_cs, word_freq_meeting,word_freq_original, word_freq_project, word_freq_re, word_freq_edu,word_freq_table, word_freq_conference, char_freq_semicolon, char_freq_leftParen,char_freq_leftBracket, char_freq_exclamation, char_freq_dollar, char_freq_pound, capital_run_length_average,capital_run_length_longest, capital_run_length_total, spam' > headers

Puis concaténer les deux fichiers de hello avec la commande hello :

    cat spambase.data >> headers
    mv headers spambaseHeaders.data

Hello dataset possède plusieurs types de statistiques sur chaque e-mail :

* Comme les colonnes ***word\_fréquence\_WORD*** indiquent le pourcentage hello de mots par courrier électronique hello qui correspondent aux *WORD*. Par exemple, si *word\_fréquence\_rendre* est 1, 1 % de tous les mots par courrier électronique hello ont été *rendre*.
* Comme les colonnes ***char\_fréquence\_CHAR*** indiquent le pourcentage hello de tous les caractères qui ont été par courrier électronique hello *CHAR*.
* ***majuscule\_exécuter\_longueur\_plus longue*** est la longueur la plus importante d’une séquence de lettres majuscules hello.
* ***majuscule\_exécuter\_longueur\_moyenne*** est hello la durée moyenne de toutes les séquences de lettres en majuscules.
* ***majuscule\_exécuter\_longueur\_total*** est hello la longueur totale de toutes les séquences de lettres en majuscules.
* ***anti-spam*** indique si les e-mails hello a été considéré comme du courrier indésirable ou non (1 = le courrier indésirable, 0 ne = pas de courrier indésirable).

## <a name="explore-hello-dataset-with-microsoft-r-open"></a>Explorer hello le jeu de données avec Microsoft R Open
Nous allons examiner les données de hello et effectuer un apprentissage base avec r. hello VM de science des données est fourni avec [Microsoft R Open](https://mran.revolutionanalytics.com/open/) préinstallé. Hello des bibliothèques de mathématiques multithread dans cette version de R offrent de meilleures performances que les différentes versions monothread. Microsoft R Open fournit également reproductibilité à l’aide d’un instantané d’un référentiel de packages CRAN hello.

exemples utilisés dans cette procédure pas à pas, hello du clone de code de copies tooget Hello **Azure-Machine-Learning--science des données** référentiel à l’aide de git, qui est préinstallé sur hello machine virtuelle. À partir de la ligne de commande git hello, exécutez :

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

Ouvrez une fenêtre de terminal et démarrez une nouvelle session de R à la console interactive hello R.

> [!NOTE]
> Vous pouvez également utiliser RStudio pour hello procédures suivantes. tooinstall RStudio, exécutez cette commande dans un terminal :`./Desktop/DSVM\ tools/installRStudio.sh`
>
>

les données de salutation tooimport et configurer l’environnement de hello, exécutez :

    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

toosee résumé des statistiques sur chaque colonne :

    summary(data)

Pour obtenir une vue différente des données de salutation :

    str(data)

Elle indique hello du type de chaque variable et de hello tout d’abord peu de valeurs dans le jeu de données hello.

Hello *anti-spam* colonne a été lu en tant qu’entier, mais il est réellement catégorielles variable (ou facteur). tooset son type :

    data$spam <- as.factor(data$spam)

toodo certains analyse exploratoire, l’utilisation hello [ggplot2](http://ggplot2.org/) du package, une bibliothèque de graphique courants pour R est déjà installé sur hello machine virtuelle. Notez, à partir des données de synthèse hello affichées précédemment, que nous avons résumé des statistiques sur la fréquence hello du caractère de point d’exclamation hello. Nous allons tracer les fréquences ici avec hello suivant de commandes :

    library(ggplot2)
    ggplot(data) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

Étant donné que la barre de hello zéro est inclinaison de traçage hello, nous allons la supprimer :

    email_with_exclamation = data[data$char_freq_exclamation > 0, ]
    ggplot(email_with_exclamation) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

Il existe une densité non triviale au-dessus de 1 qui semble intéressante. Examinons simplement ces données :

    ggplot(data[data$char_freq_exclamation > 1, ]) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

Ensuite, répartissez-les en courrier indésirable et courrier légitime :

    ggplot(data[data$char_freq_exclamation > 1, ], aes(x=char_freq_exclamation)) +
    geom_density(lty=3) +
    geom_density(aes(fill=spam, colour=spam), alpha=0.55) +
    xlab("spam") +
    ggtitle("Distribution of spam \nby frequency of !") +
    labs(fill="spam", y="Density")

Ces exemples doivent vous permettre de toomake des graphiques similaires de hello autres tooexplore colonnes hello les données qu’ils contiennent.

## <a name="train-and-test-an-ml-model"></a>Effectuer l’apprentissage et tester un modèle ML
Maintenant nous allons train quelques de l’apprentissage des modèles des messages électroniques de hello tooclassify hello DataSet comme contenant soit span ou ham. Dans cette section, nous effectuons l’apprentissage d’un modèle d’arbre de décision et d’un modèle de forêts aléatoires, puis nous testons la précision de leurs prédictions.

> [!NOTE]
> Hello rpart (partitionnement récursif et les arbres de régression) package utilisé Bonjour suivant de code est déjà installé sur hello VM de science des données.
>
>

Tout d’abord, nous allons fractionner hello le jeu de données en jeux d’apprentissage et de test :

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

Puis créez un Bonjour de tooclassify décision arborescence des messages électroniques.

    require(rpart)
    model.rpart <- rpart(spam ~ ., method = "class", data = trainSet)
    plot(model.rpart)
    text(model.rpart)

Voici le résultat de hello :

![1](./media/machine-learning-data-science-linux-dsvm-walkthrough/decision-tree.png)

toodetermine si elle fonctionne bien pour la formation de hello définir, utilisez les hello suivant de code :

    trainSetPred <- predict(model.rpart, newdata = trainSet, type = "class")
    t <- table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

degré de toodetermine qu’il exécute sur le jeu de test hello :

    testSetPred <- predict(model.rpart, newdata = testSet, type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

Essayons également un modèle de forêts aléatoires. Forêts aléatoires former une multitude d’arbres de décision et de sortie d’une classe qui est le mode de classifications hello de tous les arbres de décision individuelle hello hello. Ils fournissent une plus puissante d’apprentissage approche comme étant ils correcte pour la tendance d’un toooverfit de modèle de l’arborescence de la décision un jeu de données d’apprentissage hello.

    require(randomForest)
    trainVars <- setdiff(colnames(data), 'spam')
    model.rf <- randomForest(x=trainSet[, trainVars], y=trainSet$spam)

    trainSetPred <- predict(model.rf, newdata = trainSet[, trainVars], type = "class")
    table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)

    testSetPred <- predict(model.rf, newdata = testSet[, trainVars], type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy


## <a name="deploy-a-model-tooazure-ml"></a>Déployer un modèle de tooAzure ML
[Azure Machine Learning Studio](https://studio.azureml.net/) (AzureML) est un service cloud qui la rend facile toobuild et déployer des modèles de prévision analytique. Une des fonctionnalités intéressantes de hello de AzureML est son toopublish capacité tout R fonctionne comme un service web. Hello lot AzureML R rend toodo facile de déploiement à partir de notre session R sur hello DSVM.

toodeploy hello décision code de l’organigramme à partir de la section précédente de hello, vous devez toosign dans tooAzure Machine Learning Studio. Vous avez besoin de votre ID d’espace de travail et une toosign de jeton d’autorisation dans. toofind ces valeurs et des variables de AzureML hello initialize avec eux :

Sélectionnez **paramètres** sur le menu de gauche hello. Notez votre **ID D’ESPACE DE TRAVAIL**. ![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)

Sélectionnez **jetons d’autorisation** de menu de surcharge hello et notez votre **le jeton d’autorisation principal**.![ 3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)

Hello de charge **AzureML** du package et définissez les valeurs des variables hello avec votre ID de jeton et l’espace de travail dans votre session R sur hello DSVM :

    require(AzureML)
    wsAuth = "<authorization-token>"
    wsID = "<workspace-id>"


Nous allons simplifier hello modèle toomake cette tooimplement plus facile de démonstration. Choisir des trois variables hello dans hello décision arborescence le plus proche toohello racine et générer une nouvelle arborescence à l’aide des ces trois variables :

    colNames <- c("char_freq_dollar", "word_freq_remove", "word_freq_hp", "spam")
    smallTrainSet <- trainSet[, colNames]
    smallTestSet <- testSet[, colNames]
    model.rpart <- rpart(spam ~ ., method = "class", data = smallTrainSet)

Nous avons besoin d’une fonction de prédiction qui accepte les fonctions hello comme entrée et retourne hello valeurs prédites :

    predictSpam <- function(char_freq_dollar, word_freq_remove, word_freq_hp) {
        predictDF <- predict(model.rpart, data.frame("char_freq_dollar" = char_freq_dollar,
        "word_freq_remove" = word_freq_remove, "word_freq_hp" = word_freq_hp))
        return(colnames(predictDF)[apply(predictDF, 1, which.max)])
    }

Publier hello predictSpam fonction tooAzureML à l’aide de hello **publishWebService** (fonction) :

    spamWebService <- publishWebService("predictSpam",
        "spamWebService",
        list("char_freq_dollar"="float", "word_freq_remove"="float","word_freq_hp"="float"),
        list("spam"="int"),
        wsID, wsAuth)

Cette fonction accepte hello **predictSpam** de fonction, crée un service web appelé **spamWebService** avec défini les entrées et sorties et retourne des informations sur le nouveau point de terminaison hello.

Afficher les détails de hello publié le service web, y compris ses clés de point de terminaison et l’accès aux API avec la commande hello :

    spamWebService[[2]]

tootry son évolution horizontale sur hello 10 premières lignes du jeu de test hello :

    consumeDataframe(spamWebService$endpoints[[1]]$PrimaryKey, spamWebService$endpoints[[1]]$ApiLocation, smallTestSet[1:10, 1:3])


## <a name="use-other-tools-available"></a>Utiliser les autres outils disponibles
les sections restantes Hello montrent comment toouse certains des outils de hello installé sur hello VM de science des données Linux. Voici la liste hello des outils décrits :

* XGBoost
* Python
* Jupyterhub
* Rattle
* PostgreSQL et Squirrel SQL
* SQL Server Data Warehouse

## <a name="xgboost"></a>XGBoost
[XGBoost](https://xgboost.readthedocs.org/en/latest/) est un outil qui offre une implémentation rapide et précise des arborescences optimisées.

    require(xgboost)
    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

    bst <- xgboost(data = data.matrix(trainSet[,0:57]), label = trainSet$spam, nthread = 2, nrounds = 2, objective = "binary:logistic")

    pred <- predict(bst, data.matrix(testSet[, 0:57]))
    accuracy <- 1.0 - mean(as.numeric(pred > 0.5) != testSet$spam)
    print(paste("test accuracy = ", accuracy))

XGBoost peut également appeler à partir de Python ou d’une ligne de commande.

## <a name="python"></a>Python
Pour le développement à l’aide de Python, les distributions hello Anaconda Python 2.7 et 3.5 ont été installées dans hello DSVM.

> [!NOTE]
> Hello distribution Anaconda inclut [Condas](http://conda.pydata.org/docs/index.html), qui peut être utilisé toocreate environnements personnalisés pour Python qui ont des versions différentes et/ou des packages installés dans les.
>
>

Nous allons lire dans certains du jeu de données spambase hello et classer des messages électroniques hello avec des machines à vecteurs de support dans scikit-en savoir plus :

    import pandas
    from sklearn import svm    
    data = pandas.read_csv("spambaseHeaders.data", sep = ',\s*')
    X = data.ix[:, 0:57]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

toomake prédictions :

    clf.predict(X.ix[0:20, :])

tooshow comment toopublish AzureML d’un point de terminaison, nous allons créer un modèle plus simple hello trois variables comme nous l’avons fait lorsque nous avons publié le modèle de hello R précédemment.

    X = data.ix[["char_freq_dollar", "word_freq_remove", "word_freq_hp"]]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

toopublish hello modèle tooAzureML :

    # Publish hello model.
    workspace_id = "<workspace-id>"
    workspace_token = "<workspace-token>"
    from azureml import services
    @services.publish(workspace_id, workspace_token)
    @services.types(char_freq_dollar = float, word_freq_remove = float, word_freq_hp = float)
    @services.returns(int) # 0 or 1
    def predictSpam(char_freq_dollar, word_freq_remove, word_freq_hp):
        inputArray = [char_freq_dollar, word_freq_remove, word_freq_hp]
        return clf.predict(inputArray)

    # Get some info about hello resulting model.
    predictSpam.service.url
    predictSpam.service.api_key

    # Call hello model
    predictSpam.service(1, 1, 1)

> [!NOTE]
> Cette option est uniquement disponible pour Python 2.7 et n’est pas encore prise en charge sur 3.5. Exécutez avec **/anaconda/bin/python2.7**.
>
>

## <a name="jupyterhub"></a>Jupyterhub
distribution de Anaconda Hello Bonjour DSVM est fourni avec un bloc-notes jupyter, un environnement multiplateforme tooshare Python, R, Julia code ou et l’analyse. Bloc-notes jupyter de Hello est accessible via JupyterHub. Vous vous connectez en utilisant votre nom d’utilisateur Linux local et votre mot de passe à ***https://\<nom DNS de machine virtuelle ou adresse IP\>:8000/***. Tous les fichiers de configuration pour JupyterHub se trouvent dans le répertoire **/etc/jupyterhub**.

Plusieurs exemples d’agendas sont déjà installés sur hello machine virtuelle :

* Consultez hello [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) d’un ordinateur portable Python d’exemple.
* Consultez [IntroTutorialinR](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) pour un exemple de notebook **R** .
* Consultez hello [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) pour un autre exemple **Python** bloc-notes.

> [!NOTE]
> Hello language de Julia est également disponible à partir de la ligne de commande hello hello VM de science des données Linux.
>
>

## <a name="rattle"></a>Rattle
[Vibrer](https://cran.r-project.org/web/packages/rattle/index.html) (hello facilement l’outil d’analyse R tooLearn) est un outil graphique de R pour l’exploration de données. Elle a une interface intuitive qui le rend facile tooload, Explorer et transformer des données et générer et évaluer des modèles.  article de Hello [vibrer : GUI d’exploration de données A pour R](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) fournit une procédure pas à pas qui montre comment ses fonctionnalités.

Installer et démarrer vibrer avec hello suivant de commandes :

    if(!require("rattle")) install.packages("rattle")
    require(rattle)
    rattle()

> [!NOTE]
> L’installation n’est pas obligatoire sur hello DSVM. Mais Hochet peut vous demander de packages supplémentaires de tooinstall lors du chargement.
>
>

Rattle utilise une interface basée sur des onglets. La plupart des onglets de hello correspondent toosteps Bonjour [processus de science des données](https://azure.microsoft.com/documentation/learning-paths/data-science-process/), telles que le chargement de données ou l’exploration. processus de science des données Hello circulent à partir de la gauche tooright via les onglets hello. Mais le dernier onglet de hello contient un journal des commandes hello R exécuté par Hochet.

tooload et configurer le jeu de données hello :

* fichier de hello tooload, sélectionnez hello **données** sous l’onglet puis
* Cliquez sur le sélecteur de hello suivant trop**nom de fichier** et choisissez **spambaseHeaders.data**.
* fichier de hello tooload. Sélectionnez **Execute** dans la ligne du haut hello de boutons. Vous devez voir un résumé de chaque colonne, y compris son type de données identifié, s’il s’agit d’une entrée, une cible ou autre type de variable et le nombre de hello de valeurs uniques.
* Hochet a correctement identifié hello **anti-spam** colonne en tant que cible de hello. Colonne de spam hello sélectionnez, puis ensemble hello **Type de données cible** trop**Categoric**.

données de salutation tooexplore :

* Sélectionnez hello **Explorer** onglet.
* Cliquez sur **Résumé**, puis **Execute**, toosee certaines informations sur les types de variables hello et des statistiques de résumé.
* tooview autres types de statistiques à propos de chaque variable, sélectionnez d’autres options, comme **Describe** ou **notions de base**.

Hello **Explorer** onglet vous permet également de toogenerate nombreux instructif trace. tooplot un histogramme de données de salutation :

* Sélectionnez **Distributions**.
* Cochez **Histogramme** pour **word_freq_remove** et **word_freq_you**.
* Sélectionnez **Exécuter**. Vous devez voir que deux densité de la trace dans une fenêtre de graphique unique, où il est clair que word hello « vous » s’affiche plus fréquemment dans les messages électroniques que « supprimer ».

graphiques de corrélation Hello peuvent également vous intéresser. toocreate une :

* Choisissez **corrélation** comme hello **Type**, puis
* Sélectionnez **Exécuter**.
* Rattle vous avertit qu’il recommande un maximum de 40 variables. Sélectionnez **Oui** traçage de hello tooview.

Il existe des corrélations intéressantes qui apparaissent : « technologie » est en corrélation trop « HP » et « labs », par exemple. Il est également étroitement lié trop « 650 », code de région de hello de donneurs de dataset hello étant 650.

valeurs numériques de Hello pour les corrélations hello entre les mots sont disponibles dans la fenêtre d’Explorer hello. Il est intéressant toonote, par exemple, que « technologie » est négative corrélée avec « votre » et « money ».

Hochet peut transformer hello dataset toohandle certains problèmes courants. Par exemple, il vous permet de toorescale fonctionnalités imputer les valeurs manquantes, gérer les observations aberrantes et supprimer des variables ou des observations avec les données manquantes. Rattle peut également identifier des règles d’association entre des observations et/ou des variables. Ces onglets sont hors de portée pour cette introduction pas à pas.

Rattle peut également effectuer une analyse de cluster. Nous allons exclure certains tooread fonctionnalités toomake hello sortie plus facile. Sur hello **données** , onglet choisir **ignorer** tooeach suivant des variables hello, à l’exception de ces dix éléments :

* word_freq_hp
* word_freq_technology
* word_freq_george
* word_freq_remove
* word_freq_your
* word_freq_dollar
* word_freq_money
* capital_run_length_longest
* word_freq_business
* spam

Puis revenir en arrière toohello **Cluster** , onglet choisir **KMeans**et ensemble hello *nombre de clusters* too4. Ensuite, sélectionnez **Exécuter**. résultats de Hello sont affichés dans la fenêtre de sortie hello. Un cluster possède une fréquence élevée de « george » et de « hp » et est probablement un e-mail professionnel légitime.

toobuild un modèle d’apprentissage arbre de décision simple :

* Sélectionnez hello **modèle** onglet,
* Choisissez **arborescence** comme hello **Type**.
* Sélectionnez **Execute** arborescence de hello toodisplay sous forme de texte Bonjour fenêtre de sortie.
* Sélectionnez hello **dessiner** bouton tooview une version graphique. Cela ressemble assez similaire toohello arborescence, nous avons obtenu précédemment à l’aide de *rpart*.

Une des fonctionnalités intéressantes de hello de Hochet est sa capacité toorun apprentissage plusieurs méthodes et les évaluer rapidement. Voici la procédure de hello :

* Choisissez **tous les** pour hello **Type**.
* Sélectionnez **Exécuter**.
* Une fois celle-ci terminée, vous pouvez cliquer sur une même **Type**, comme **SVM**et afficher les résultats de hello.
* Vous pouvez également comparer les performances de hello des modèles de hello sur validation hello définies à l’aide de hello **évaluer** onglet. Par exemple, hello **erreur matrice** sélection vous montre matrice de confusion hello, erreur global et d’erreur de classe moyenne pour chaque modèle sur l’ensemble de validation hello.
* Vous pouvez également tracer des courbes ROC, effectuer des analyses de sensibilité et d’autres types d’évaluations de modèle.

Une fois que vous avez terminé la création de modèles, sélectionnez hello **journal** onglet code de hello R tooview exécuté par Hochet pendant votre session. Vous pouvez sélectionner hello **exporter** bouton toosave il.

> [!NOTE]
> Il existe un bogue dans la version actuelle de Rattle. toomodify hello script ou utilisez-le toorepeat vos étapes plus tard, vous devez insérer un caractère # devant * exporter ce journal... * dans le texte hello du journal de hello.
>
>

## <a name="postgresql--squirrel-sql"></a>PostgreSQL et Squirrel SQL
Hello DSVM est fourni avec PostgreSQL installé. PostgreSQL est une base de données relationnelle, open source et sophistiquée. Cette section montre comment tooload notre jeu de données de spam dans PostgreSQL et puis de la requête.

Avant de pouvoir charger les données de salutation, vous devez tooallow d’authentification de mot de passe à partir de localhost de hello. À l’invite de commandes :

    sudo gedit /var/lib/pgsql/data/pg_hba.conf

Bas hello hello du fichier de configuration sont plusieurs lignes de détaillent hello de connexions autorisée :

    # "local" is for Unix domain socket connections only
    local   all             all                                     trust
    # IPv4 local connections:
    host    all             all             127.0.0.1/32            ident
    # IPv6 local connections:
    host    all             all             ::1/128                 ident

Modifier hello « IPv4 des connexions locales » ligne toouse md5 au lieu d’ident, afin de nous pouvons connecter à l’aide d’un nom d’utilisateur et un mot de passe :

    # IPv4 local connections:
    host    all             all             127.0.0.1/32            md5

Et redémarrez le service postgres hello :

    sudo systemctl restart postgresql

toolaunch psql, un terminal interactive pour PostgreSQL, en tant qu’utilisateur de postgres intégrés hello, exécutez hello de commande suivante à partir d’une invite de commandes :

    sudo -u postgres psql

Créer un nouveau compte d’utilisateur, à l’aide de hello le même nom d’utilisateur comme hello compte Linux que vous êtes actuellement connecté, attribuez-lui un mot de passe :

    CREATE USER <username> WITH CREATEDB;
    CREATE DATABASE <username>;
    ALTER USER <username> password '<password>';
    \quit

Connectez-vous ensuite toopsql en tant que votre utilisateur :

    psql

Et importer des données de hello dans une base de données :

    CREATE DATABASE spam;
    \c spam
    CREATE TABLE data (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer);
    \copy data FROM /home/<username>/spambase.data DELIMITER ',' CSV;
    \quit

Maintenant, nous allons explorer les données hello et exécuter des requêtes à l’aide de **non SQL**, un outil graphique qui vous permet d’interagir avec les bases de données via un pilote JDBC.

tooget de démarrer, lancez non SQL à partir du menu d’Applications hello. tooset pilote de hello :

* Sélectionnez **Windows**, puis **Afficher les pilotes**.
* Cliquez avec le bouton droit sur **PostgreSQL** et sélectionnez **Modifier le pilote**.
* Sélectionnez **Chemin d’accès de la classe supplémentaire**, puis **Ajouter**.
* Entrez ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** pour hello **nom de fichier** et
* Sélectionnez **Ouvrir**.
* Choisissez Pilotes de la liste, puis sélectionnez **org.postgresql.Driver** dans **Nom de la classe**, et sélectionnez **OK**.

tooset des hello de connexion toohello local du serveur :

* Sélectionnez **Windows**, puis **Afficher les alias**.
* Choisissez hello  **+**  bouton toomake un nouvel alias.
* Nommez-le *base de données de courrier indésirable*, choisissez **PostgreSQL** Bonjour **pilote** liste déroulante.
* Définir les URL de hello trop*jdbc:postgresql://localhost/spam*.
* Entrez votre *nom d’utilisateur* et votre *mot de passe*.
* Cliquez sur **OK**.
* tooopen hello **connexion** fenêtre, double-cliquez sur hello ***base de données de courrier indésirable*** alias.
* Sélectionnez **Connecter**.

toorun certaines requêtes :

* Sélectionnez hello **SQL** onglet.
* Entrez une requête simple tel `SELECT * from data;` dans zone de texte hello requête haut hello d’onglet de hello SQL.
* Appuyez sur **Ctrl + entrée** toorun il. Par défaut non SQL renvoie hello 100 premières lignes de votre requête.

Il existe de nombreuses requêtes plus que tooexplore pourrait utiliser ces données. Par exemple, comment le fait hello fréquence du mot de hello *rendre* diffèrent entre anti-spam et ham ?

    SELECT avg(word_freq_make), spam from data group by spam;

Ou quelles sont les caractéristiques de hello des messages électroniques qui contiennent souvent *3d*?

    SELECT * from data order by word_freq_3d desc;

La plupart des e-mails qui ont une occurrence élevée de *3d* sont apparemment envoyer du courrier indésirable, il peut donc être une fonction très utile pour la création d’un Bonjour tooclassify de modèle de prévision des messages électroniques.

Si vous souhaitiez tooperform apprentissage des données stockées dans une base de données PostgreSQL, envisagez d’utiliser [MADlib](http://madlib.incubator.apache.org/).

## <a name="sql-server-data-warehouse"></a>SQL Server Data Warehouse
Azure SQL Data Warehouse est une base de données de mise à l’échelle basée sur le cloud qui prend en charge le traitement de grands volumes de données relationnelles et non relationnelles. Pour plus d’informations, consultez [En quoi consiste Azure SQL Data Warehouse ?](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)

tooconnect toohello données de l’entrepôt et créer table hello suivant de hello exécution de commandes à partir d’une invite de commandes :

    sqlcmd -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -I

Puis, à l’invite sqlcmd hello :

    CREATE TABLE spam (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer) WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = ROUND_ROBIN);
    GO

Copier des données avec bcp :

    bcp spam in spambaseHeaders.data -q -c -t  ',' -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -F 1 -r "\r\n"

> [!NOTE]
> les fins de ligne Hello dans le fichier téléchargé de hello sont de type Windows, mais bcp attend de style UNIX, donc nous devez bcp tootell qu’avec hello indicateur de - r.
>
>

Et exécuter des requêtes avec sqlcmd :

    select top 10 spam, char_freq_dollar from spam;
    GO

Vous pouvez également exécuter des requêtes avec Squirrel SQL. Suivez les étapes similaires pour PostgreSQL, à l’aide de hello Microsoft MSSQL Server JDBC Driver, qui se trouve dans ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.

## <a name="next-steps"></a>Étapes suivantes
Pour une vue d’ensemble des rubriques qui vous guident tout au long des tâches de hello qui impliquent des processus de science des données hello dans Azure, consultez [processus de science des données équipe](http://aka.ms/datascienceprocess).

Pour obtenir une description de l’autre bout en bout procédures pas à pas qui illustrent les étapes hello Bonjour processus de science des données équipe pour des scénarios spécifiques, consultez [procédures pas à pas du processus de science des données équipe](data-science-process-walkthroughs.md). procédures pas à pas Hello également illustrent comment toocombine cloud et locaux outils et services dans un toocreate de flux de travail ou d’un pipeline, une application intelligente.
