---
title: "jeux de données aaaAccess avec la bibliothèque cliente de Machine Learning Python | Documents Microsoft"
description: "Installer et utiliser hello tooaccess de bibliothèque cliente de Python et gérer les données d’Azure Machine Learning en toute sécurité à partir d’un environnement local de Python."
services: machine-learning
documentationcenter: python
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 9ab42272-c30c-4b7e-8e66-d64eafef22d0
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: huvalo;bradsev
ms.openlocfilehash: f55067118f13c52bf677930a20836ce6989f8187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="access-datasets-with-python-using-hello-azure-machine-learning-python-client-library"></a>Accès de jeux de données avec Python à l’aide de la bibliothèque cliente de hello Azure Machine Learning Python
afficher un aperçu de Hello de bibliothèque cliente de Microsoft Azure Machine Learning Python permettre un accès sécurisé tooyour jeux de données Azure Machine Learning à partir d’un environnement local de Python et permet la création de hello et la gestion de jeux de données dans un espace de travail.

Cette rubrique fournit des instructions pour les procédures suivantes :

* installer la bibliothèque cliente de Machine Learning Python hello 
* accéder à et de jeux de données, y compris des instructions sur la façon de télécharger tooget d’autorisation tooaccess jeux de données Azure Machine Learning à partir de votre environnement local de Python
* accès aux jeux de données intermédiaires à partir d'expériences
* utiliser des datasets tooenumerate bibliothèque hello Python client accéder aux métadonnées, lire le contenu d’un dataset hello, créer de nouveaux datasets et mettre à jour des jeux de données existants

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="prerequisites"></a>Configuration requise
bibliothèque cliente de Python Hello a été testé sous hello suivant environnements :

* Windows, Mac et Linux
* Python 2.7, 3.3 et 3.4

Il a une dépendance sur hello suivant des packages :

* requêtes
* python-dateutil
* pandas

Nous recommandons d’utiliser une distribution de Python comme [Anaconda](http://continuum.io/downloads#all) ou [Canopy](https://store.enthought.com/downloads/), qui sont fournis avec Python, notebooks et d’installer les packages hello trois répertoriés ci-dessus. Bien que IPython n'est pas formellement requis, il s'agit d'un environnement idéal pour la manipulation et la visualisation interactive des données.

### <a name="installation"></a>Comment tooinstall hello bibliothèque cliente de Azure Machine Learning Python
bibliothèque cliente de Azure Machine Learning Python Hello doit également être installé toocomplete des tâches hello présentées dans cette rubrique. Il est disponible à partir de hello [Python Package Index](https://pypi.python.org/pypi/azureml). tooinstall dans votre environnement de Python, exécutez hello après une commande à partir de votre environnement de Python local :

    pip install azureml

Ou bien, vous pouvez télécharger et installer à partir de sources de hello sur [github](https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python).

    python setup.py install

Si vous avez git installé sur votre ordinateur, vous pouvez utiliser pip tooinstall directement à partir de référentiel git de hello :

    pip install git+https://github.com/Azure/Azure-MachineLearning-ClientLibrary-Python.git


## <a name="datasetAccess"></a>Utiliser des datasets tooaccess Studio Code des extraits de code
bibliothèque cliente de Python Hello vous donne un accès par programmation tooyour jeux de données existante à partir d’expériences qui ont été exécutées.

À partir d’une interface web hello Studio, vous pouvez générer des extraits de code qui incluent toutes les toodownload d’informations nécessaires hello et désérialiser des jeux de données en tant qu’objets Pandas la trame de données sur votre ordinateur de l’emplacement.

### <a name="security"></a>Sécurité relative à l'accès aux données
extraits de code fournis par Studio pour utilisation avec la bibliothèque cliente de Python hello inclut votre id d’espace de travail et l’autorisation de Hello jeton. Ces fournissent l’espace de travail tooyour un accès complet et doivent être protégés comme un mot de passe.

Pour des raisons de sécurité, fonctionnalité d’extrait de code hello est uniquement disponible toousers qui ont leur rôle défini en tant que **propriétaire** pour l’espace de travail hello. Votre rôle est affiché dans Azure Machine Learning Studio sur hello **utilisateurs** page sous **paramètres**.

![Sécurité][security]

Si votre rôle n’est pas défini en tant que **propriétaire**, vous pouvez soit demander toobe nouvelle en tant que propriétaire, ou demandez au propriétaire de tooprovide d’espace de travail hello hello vous avec l’extrait de code hello.

jeton d’autorisation de hello tooobtain, vous pouvez effectuer hello suivantes :

* Demander un jeton à un propriétaire. Propriétaires peuvent accéder à leurs jetons d’autorisation à partir de la page des paramètres de leur espace de travail dans Studio hello. Sélectionnez **paramètres** de hello gauche du volet et cliquez sur **jetons d’autorisation** toosee hello les jetons principaux et secondaires.  Bien hello principal ou jetons d’autorisation secondaire hello peuvent être utilisés dans l’extrait de code hello, il est recommandé que les propriétaires uniquement partagent les jetons d’autorisation secondaire hello.

![Jetons d’autorisation](./media/machine-learning-python-data-access/ml-python-access-settings-tokens.png)

* Demandez à toorole toobe promue du propriétaire.  toodo cela, un propriétaire actuel du toofirst de besoins d’espace de travail hello vous supprimer à partir de l’espace de travail hello puis ré-vous inviter tooit en tant que propriétaire.

Une fois que les développeurs ont obtenu les id d’espace de travail hello et l’autorisation jetons, ils sont en mesure de tooaccess espace de travail de hello à l’aide d’extrait de code hello, quelle que soit leur rôle.

Jetons d’autorisation sont gérés sur hello **jetons d’autorisation** page sous **paramètres**. Vous pouvez régénérer les, mais cette procédure révoque le jeton précédent d’accès toohello.

### <a name="accessingDatasets"></a>Accès aux jeux de données depuis une application Python locale
1. Dans la Machine Learning Studio, cliquez sur **jeux de données** dans la barre de navigation hello sur hello gauche.
2. Sélectionnez le dataset hello tooaccess voulue. Vous pouvez sélectionner un des jeux de données hello hello **mes DATASETS** liste ou à partir de hello **exemples** liste.
3. Dans la barre d’outils du bas hello, cliquez sur **Code d’accès aux données générer**. Si les données de salutation sont dans un format incompatible avec la bibliothèque cliente de Python hello, ce bouton est désactivé.
   
    ![JEUX DE DONNÉES][datasets]
4. Sélectionnez l’extrait de code hello à partir de la fenêtre hello qui s’affiche et copiez-le tooyour Presse-papiers.
   
    ![Code d'accès][dataset-access-code]
5. Collez les code hello dans Bloc-notes hello de votre application Python locale.
   
    ![Bloc-notes][ipython-dataset]

## <a name="accessingIntermediateDatasets"></a>Accès aux jeux de données intermédiaires à partir d'expériences de Machine Learning
Après l’exécution d’une expérience Bonjour Machine Learning Studio, il est possible tooaccess hello intermédiaire des groupes de données à partir des nœuds de sortie hello des modules. Les jeux de données intermédiaires sont des données qui ont été créées et utilisées pour les étapes intermédiaires lorsqu'un outil de modèle a été exécuté.

Jeux de données intermédiaires sont accessibles tant que format de données hello est compatible avec la bibliothèque cliente de Python hello.

Hello formats suivants sont pris en charge (dans ce cas, les constantes sont Bonjour `azureml.DataTypeIds` classe) :

* Texte brut
* CSV générique
* TSV générique
* CSV générique sans en-tête
* TSV générique sans en-tête

Vous pouvez déterminer le format de hello en pointant sur un nœud de sortie de module. Il s’affiche avec le nom du nœud hello, dans une info-bulle.

Certains des modules hello, par exemple hello [fractionnement] [ split] module, le format de sortie de tooa nommé `Dataset`, qui n’est pas pris en charge par la bibliothèque cliente de Python hello.

![Format de jeu de données][dataset-format]

Vous devez toouse un module de conversion, tel que [convertir tooCSV][convert-to-csv], tooget une sortie dans un format pris en charge.

![Format CSV générique][csv-format]

Hello étapes suivantes montrent un exemple qui crée une expérience, exécute et accède au jeu de données intermédiaire hello.

1. Création d'une nouvelle expérience.
2. Insérez un module **Jeu de données Adult Census Income Binary Classification** .
3. Insérer un [fractionnement] [ split] module et vous connecter à sa sortie de module d’entrée toohello jeu de données.
4. Insérer un [convertir tooCSV] [ convert-to-csv] module et se connecter à son tooone d’entrée de hello [fractionnement] [ split] module génère.
5. Enregistrer l’expérience de hello, exécuter et attendez qu’elle toofinish en cours d’exécution.
6. Cliquez sur le nœud de sortie hello sur hello [convertir tooCSV] [ convert-to-csv] module.
7. Menu contextuel de hello, sélectionnez **Code d’accès aux données générer**.
   
    ![Menu contextuel][experiment]
8. Sélectionnez l’extrait de code hello et copier tooyour Presse-papiers à partir de la fenêtre hello qui s’affiche.
   
    ![Code d'accès][intermediate-dataset-access-code]
9. Collez le code de hello dans le bloc-notes.
   
    ![Bloc-notes][ipython-intermediate-dataset]
10. Vous pouvez visualiser les données de salutation avec matplotlib ;. Cela affiche dans un histogramme pour la colonne d’âge hello :
    
    ![Histogramme][ipython-histogram]

## <a name="clientApis"></a>Utilisez tooaccess de bibliothèque client hello Machine Learning Python, lire, créer et gérer des jeux de données
### <a name="workspace"></a>Espace de travail
espace de travail Hello est le point d’entrée hello pour la bibliothèque cliente de Python hello. Fournir hello `Workspace` classe avec votre espace de travail un id et l’autorisation toocreate jeton une instance :

    ws = Workspace(workspace_id='4c29e1adeba2e5a7cbeb0e4f4adfb4df',
                   authorization_token='f4f3ade2c6aefdb1afb043cd8bcf3daf')


### <a name="enumerate-datasets"></a>Énumérer les jeux de données
tooenumerate tous les jeux de données dans un espace de travail donné :

    for ds in ws.datasets:
        print(ds.name)

tooenumerate hello simplement créés par l’utilisateur des groupes de données :

    for ds in ws.user_datasets:
        print(ds.name)

jeux de données tooenumerate hello simplement exemple :

    for ds in ws.example_datasets:
        print(ds.name)

Vous pouvez accéder à un jeu de données par son nom (qui respecte la casse) :

    ds = ws.datasets['my dataset name']

Vous pouvez également y accéder par l'index :

    ds = ws.datasets[0]


### <a name="metadata"></a>Metadata
Jeux de données des métadonnées, dans toocontent d’addition. (Les jeux de données intermédiaires sont une règle d’exception toothis et n’ont pas toutes les métadonnées.)

Certaines valeurs de métadonnées sont affectés par l’utilisateur de hello lors de la création :

    print(ds.name)
    print(ds.description)
    print(ds.family_id)
    print(ds.data_type_id)

D'autres sont des valeurs affectées par Azure ML :

    print(ds.id)
    print(ds.created_date)
    print(ds.size)

Consultez hello `SourceDataset` classe pour les métadonnées disponibles plus on hello.

### <a name="read-contents"></a>Lire le contenu
extraits de code Hello fournis automatiquement par Machine Learning Studio, téléchargement et désérialiser l’objet de trame de données Pandas tooa hello dataset. Cette opération s’effectue par hello `to_dataframe` méthode :

    frame = ds.to_dataframe()

Si vous préférez des données brutes toodownload hello et procédez vous-même à la désérialisation de hello, qui est une option. Au moment de hello, il s’agit de hello seule option de formats tels que 'ARFF', Impossible de désérialiser la bibliothèque client Python hello.

contenu de hello tooread sous forme de texte :

    text_data = ds.read_as_text()

contenu de hello tooread sous forme binaire :

    binary_data = ds.read_as_binary()

Vous pouvez également ouvrir un contenu toohello :

    with ds.open() as file:
        binary_data_chunk = file.read(1000)


### <a name="create-a-new-dataset"></a>Créer un nouveau jeu de données
bibliothèque cliente de Python Hello vous permet de tooupload des jeux de données à partir de votre programme Python. Ces jeux de données sont alors disponibles pour une utilisation dans votre espace de travail.

Si vous disposez de vos données dans une trame de données Pandas, utilisez hello suivant de code :

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_dataframe(
        dataframe=frame,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

Si vos données sont déjà sérialisées, vous pouvez utiliser :

    from azureml import DataTypeIds

    dataset = ws.datasets.add_from_raw_data(
        raw_data=raw_data,
        data_type_id=DataTypeIds.GenericCSV,
        name='my new dataset',
        description='my description'
    )

la bibliothèque cliente Python Hello est en mesure de tooserialize met en forme une suivant de toohello Pandas de trame de données (dans ce cas, les constantes sont Bonjour `azureml.DataTypeIds` classe) :

* Texte brut
* CSV générique
* TSV générique
* CSV générique sans en-tête
* TSV générique sans en-tête

### <a name="update-an-existing-dataset"></a>Mettre à jour un jeu de données existant
Si vous essayez tooupload un nouveau dataset avec un nom qui correspond à un dataset existant, vous devez obtenir une erreur de conflit.

tooupdate un dataset existant, vous devez tout d’abord tooget un jeu de données référence toohello existant :

    dataset = ws.datasets['existing dataset']

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

Utilisez ensuite `update_from_dataframe` tooserialize et remplacer contenu hello du jeu de données hello sur Azure :

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(frame2)

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

Si vous souhaitez autre format tooserialize hello données tooa, spécifiez une valeur pour hello facultatif `data_type_id` paramètre.

    from azureml import DataTypeIds

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        data_type_id=DataTypeIds.GenericTSV,
    )

    print(dataset.data_type_id) # 'GenericTSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toojan 2015'

Vous pouvez éventuellement définir une nouvelle description en spécifiant une valeur pour hello `description` paramètre.

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        description='data up toofeb 2015',
    )

    print(dataset.data_type_id) # 'GenericCSV'
    print(dataset.name)         # 'existing dataset'
    print(dataset.description)  # 'data up toofeb 2015'

Vous pouvez éventuellement définir un nouveau nom en spécifiant une valeur pour hello `name` paramètre. Dès lors, vous allez récupérer hello le jeu de données à l’aide du nouveau nom uniquement hello. Hello suivant code met à jour la description, nom et les données de salutation.

    dataset = ws.datasets['existing dataset']

    dataset.update_from_dataframe(
        dataframe=frame2,
        name='existing dataset v2',
        description='data up toofeb 2015',
    )

    print(dataset.data_type_id)                    # 'GenericCSV'
    print(dataset.name)                            # 'existing dataset v2'
    print(dataset.description)                     # 'data up toofeb 2015'

    print(ws.datasets['existing dataset v2'].name) # 'existing dataset v2'
    print(ws.datasets['existing dataset'].name)    # IndexError

Hello `data_type_id`, `name` et `description` paramètres sont facultatifs et la valeur précédente de tootheir par défaut. Hello `dataframe` paramètre est toujours requis.

Si vos données sont déjà sérialisées, utilisez `update_from_raw_data` au lieu de `update_from_dataframe`. Si vous transmettez simplement `raw_data` au lieu de `dataframe`, cela fonctionne de la même manière.

<!-- Images -->
[security]:./media/machine-learning-python-data-access/security.png
[dataset-format]:./media/machine-learning-python-data-access/dataset-format.png
[csv-format]:./media/machine-learning-python-data-access/csv-format.png
[datasets]:./media/machine-learning-python-data-access/datasets.png
[dataset-access-code]:./media/machine-learning-python-data-access/dataset-access-code.png
[ipython-dataset]:./media/machine-learning-python-data-access/ipython-dataset.png
[experiment]:./media/machine-learning-python-data-access/experiment.png
[intermediate-dataset-access-code]:./media/machine-learning-python-data-access/intermediate-dataset-access-code.png
[ipython-intermediate-dataset]:./media/machine-learning-python-data-access/ipython-intermediate-dataset.png
[ipython-histogram]:./media/machine-learning-python-data-access/ipython-histogram.png


<!-- Module References -->
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/

