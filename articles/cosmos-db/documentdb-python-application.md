---
title: "Didacticiel de l’application web Python Flask avec Azure Cosmos DB | Microsoft Docs"
description: "Passez en revue un didacticiel de base de données qui explique comment utiliser Azure Cosmos DB pour stocker des données et y accéder à partir d’une application web Python Flask hébergée sur Azure. Trouvez des solutions de développement d’applications."
keywords: "Développement d’applications, Python Flask, application web Python, développement web Python"
services: cosmos-db
documentationcenter: python
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 20ebec18-67c2-4988-a760-be7c30cfb745
ms.service: cosmos-db
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/09/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c62520846ebdc102204e42b50e52383167c6aa14
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="build-a-python-flask-web-application-using-azure-cosmos-db"></a>Créer une application web Python Flask à l’aide d’Azure Cosmos DB
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [Node.JS](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

Ce didacticiel vous montre comment utiliser Azure Cosmos DB pour stocker des données et y accéder à partir d’une application web Python hébergée sur Azure. Il suppose que vous avez déjà une expérience de l’utilisation de Python et des sites web Azure.

Ce didacticiel de base de données traite les points suivants :

1. Création et approvisionnement d’un compte Cosmos DB.
2. Création d’une application Python Flask.
3. Connexion à Cosmos DB pour une utilisation à partir de votre application web.
4. Déploiement de l’application web sur Azure.

Dans ce didacticiel, vous allez créer une application de vote simple qui vous permettra de voter lors d’un sondage.

![Capture d’écran de l’application de vote créée avec ce didacticiel d’utilisation de la base de données](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)

## <a name="database-tutorial-prerequisites"></a>Conditions préalables à l’exécution de ce didacticiel de base de données
Avant de suivre les instructions de cet article, vérifiez que les éléments suivants sont installés :

* Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer. 

  [!INCLUDE [cosmos-db-emulator-docdb-api](../../includes/cosmos-db-emulator-docdb-api.md)]

* Si vous n’avez pas encore installé Visual Studio 2017, vous pouvez télécharger et utiliser la version **gratuite** [Visual Studio Community Edition](https://www.visualstudio.com/downloads/). Veillez à activer **le développement Azure** lors de l’installation de Visual Studio.  
* [Python Tools pour Visual Studio](https://github.com/Microsoft/PTVS/).  
* [Kit de développement logiciel (SDK) Microsoft Azure pour Python 2.7](https://azure.microsoft.com/downloads/). 
* [Python 2.7.13](https://www.python.org/downloads/windows/). 

> [!IMPORTANT]
> Si vous installez Python 2.7 pour la première fois, sélectionnez **Ajouter python.exe au chemin d’accès** dans l’écran Personnaliser Python 2.7.13.
> 
> ![Capture d’écran de l’écran Personnaliser Python 2.7.11, où vous devez sélectionner Ajouter python.exe au chemin](./media/documentdb-python-application/cosmos-db-python-install.png)
> 
> 

* [Compilateur Microsoft Visual C++ pour Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266).

## <a name="step-1-create-an-azure-cosmos-db-database-account"></a>Étape 1 : création d’un compte de base de données Azure Cosmos DB
Commençons par créer un compte Cosmos DB. Si vous possédez déjà un compte ou si vous utilisez l’émulateur Azure Cosmos DB pour ce didacticiel, vous pouvez passer à [l’étape 2 : création d’une application web Python Flask](#step-2-create-a-new-python-flask-web-application).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<br/>
Voyons à présent comment créer une application web Python Flask de A à Z.

## <a name="step-2-create-a-new-python-flask-web-application"></a>Étape 2 : Création d’une application web Python Flask
1. Dans Visual Studio, dans le menu **Fichier**, pointez sur **Nouveau**, puis cliquez sur **Projet**.
   
    La boîte de dialogue **Nouveau projet** apparaît.
2. Dans le volet gauche, développez **Modèles** puis **Python**, puis cliquez sur **Web**. 
3. Sélectionnez **Projet web Flask** dans le volet central puis, dans la zone **Nom**, tapez **tutorial**, puis cliquez sur **OK**. N’oubliez pas que les noms de package Python doivent être entièrement en minuscules, comme décrit dans le [Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).
   
    Si vous ne connaissez pas bien Python Flask, sachez qu’il s’agit d’une infrastructure de développement d’applications web qui permet d’accélérer la création d’applications web dans Python.
   
    ![Capture d’écran de la fenêtre Nouveau projet dans Visual Studio avec Python mis en surbrillance sur la gauche, le projet web Python Flask sélectionné au milieu et le didacticiel name dans la zone Nom](./media/documentdb-python-application/image9.png)
4. Dans la fenêtre **Outils Python pour Visual Studio**, cliquez sur **Installer dans un environnement virtuel**. 
   
    ![Capture d’écran du didacticiel de base de données - Fenêtre Python Tools pour Visual Studio](./media/documentdb-python-application/python-install-virtual-environment.png)
5. Dans la fenêtre **Ajouter un environnement virtuel**, vous pouvez accepter les valeurs par défaut et utiliser Python 2.7 comme environnement de base, car PyDocumentDB ne prend actuellement pas en charge Python 3.x, puis cliquez sur **Créer**. Cette opération configure l’environnement virtuel Python nécessaire à votre projet.
   
    ![Capture d’écran du didacticiel de base de données - Fenêtre Python Tools pour Visual Studio](./media/documentdb-python-application/image10_A.png)
   
    La fenêtre de sortie affiche `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` quand l’environnement est correctement installé.

## <a name="step-3-modify-the-python-flask-web-application"></a>Étape 3 : Modification de l’application web Python Flask
### <a name="add-the-python-flask-packages-to-your-project"></a>Ajouter les packages Python Flask à votre projet
Une fois votre projet configuré, vous devez ajouter les packages Flask requis, dont pydocumentdb, le package Python pour DocumentDB.

1. Dans l’Explorateur de solutions, ouvrez le fichier nommé **requirements.txt** et remplacez son contenu par le code suivant :
   
        flask==0.9
        flask-mail==0.7.6
        sqlalchemy==0.7.9
        flask-sqlalchemy==0.16
        sqlalchemy-migrate==0.7.2
        flask-whooshalchemy==0.55a
        flask-wtf==0.8.4
        pytz==2013b
        flask-babel==0.8
        flup
        pydocumentdb>=1.0.0
2. Enregistrez le fichier **requirements.txt** . 
3. Dans l’Explorateur de solutions, cliquez avec le bouton droit sur **env**, puis cliquez sur **Install from requirements.txt** (Installer depuis requirements.txt).
   
    ![Capture d’écran affichant env (Python 2.7) sélectionné avec Install from requirements.txt mis en surbrillance dans la liste](./media/documentdb-python-application/cosmos-db-python-install-from-requirements.png)
   
    Après l’installation, la fenêtre de sortie affiche les informations suivantes :
   
        Successfully installed Babel-2.3.2 Tempita-0.5.2 WTForms-2.1 Whoosh-2.7.4 blinker-1.4 decorator-4.0.9 flask-0.9 flask-babel-0.8 flask-mail-0.7.6 flask-sqlalchemy-0.16 flask-whooshalchemy-0.55a0 flask-wtf-0.8.4 flup-1.0.2 pydocumentdb-1.6.1 pytz-2013b0 speaklater-1.3 sqlalchemy-0.7.9 sqlalchemy-migrate-0.7.2
   
   > [!NOTE]
   > Dans de rares cas, la fenêtre de résultat peut afficher une erreur. Si cela se produit, vérifiez si l’erreur n'est pas liée au nettoyage. Parfois, le nettoyage peut échouer, alors que l’installation sera réussie (faites défiler le contenu de la fenêtre de résultat pour le vérifier). Vous pouvez vérifier votre installation via la [vérification de l’environnement virtuel](#verify-the-virtual-environment). Si l’installation échoue mais que la vérification réussit, vous pouvez continuer.
   > 
   > 

### <a name="verify-the-virtual-environment"></a>Vérification de l'environnement virtuel
Vérifiez que l'installation est réussie.

1. Appuyez sur **Ctrl**+**Maj**+**B** pour générer la solution.
2. Une fois la génération terminée, démarrez le site Web en appuyant sur **F5**. Cette action démarre le serveur de développement Flask ainsi que votre navigateur web. La page suivante doit s'afficher.
   
    ![Projet de développement web Python Flask vide affiché dans un navigateur](./media/documentdb-python-application/image12.png)
3. Arrêtez le débogage du site web en appuyant sur **Maj**+**F5** dans Visual Studio.

### <a name="create-database-collection-and-document-definitions"></a>Création des définitions pour la base de données, la collection et le document
Nous allons maintenant créer votre application de vote en ajoutant de nouveaux fichiers et en mettant à jour d’autres fichiers.

1. Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le projet **tutorial**, cliquez sur **Ajouter**, puis sur **Nouvel élément**. Sélectionnez **Fichier Python vide** et nommez le fichier **forms.py**.  
2. Ajoutez le code suivant au fichier forms.py, puis enregistrez le fichier.

```python
from flask.ext.wtf import Form
from wtforms import RadioField

class VoteForm(Form):
    deploy_preference  = RadioField('Deployment Preference', choices=[
        ('Web Site', 'Web Site'),
        ('Cloud Service', 'Cloud Service'),
        ('Virtual Machine', 'Virtual Machine')], default='Web Site')
```


### <a name="add-the-required-imports-to-viewspy"></a>Ajoutez les instructions import requises à views.py
1. Dans l’Explorateur de solutions, développez le dossier **tutorial** et ouvrez le fichier **views.py**. 
2. Ajoutez les instructions d’importation suivantes au début du fichier **views.py**, puis enregistrez le fichier. Elles importent les packages Flask et le kit de développement logiciel (SDK) Python de Cosmos DB.
   
    ```python
    from forms import VoteForm
    import config
    import pydocumentdb.document_client as document_client
    ```

### <a name="create-database-collection-and-document"></a>Création de base de données, de collection et de document
* Toujours dans **views.py**, ajoutez le code suivant à la fin du fichier. Cela permet de créer la base de données utilisée par le formulaire. Ne supprimez pas le code existant dans **views.py**. Il vous suffit d'ajouter le code à la fin.

```python
@app.route('/create')
def create():
    """Renders the contact page."""
    client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

    # Attempt to delete the database.  This allows this to be used to recreate as well as create
    try:
        db = next((data for data in client.ReadDatabases() if data['id'] == config.DOCUMENTDB_DATABASE))
        client.DeleteDatabase(db['_self'])
    except:
        pass

    # Create database
    db = client.CreateDatabase({ 'id': config.DOCUMENTDB_DATABASE })

    # Create collection
    collection = client.CreateCollection(db['_self'],{ 'id': config.DOCUMENTDB_COLLECTION })

    # Create document
    document = client.CreateDocument(collection['_self'],
        { 'id': config.DOCUMENTDB_DOCUMENT,
          'Web Site': 0,
          'Cloud Service': 0,
          'Virtual Machine': 0,
          'name': config.DOCUMENTDB_DOCUMENT 
        })

    return render_template(
       'create.html',
        title='Create Page',
        year=datetime.now().year,
        message='You just created a new database, collection, and document.  Your old votes have been deleted')
```


### <a name="read-database-collection-document-and-submit-form"></a>Lecture de la base de données, de la collection et du document, et envoi du formulaire
* Toujours dans **views.py**, ajoutez le code suivant à la fin du fichier. Ce code configure le formulaire et lit la base de données, la collection et le document. Ne supprimez pas le code existant dans **views.py**. Il vous suffit d'ajouter le code à la fin.

```python
@app.route('/vote', methods=['GET', 'POST'])
def vote(): 
    form = VoteForm()
    replaced_document ={}
    if form.validate_on_submit(): # is user submitted vote  
        client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

        # Read databases and take first since id should not be duplicated.
        db = next((data for data in client.ReadDatabases() if data['id'] == config.DOCUMENTDB_DATABASE))

        # Read collections and take first since id should not be duplicated.
        coll = next((coll for coll in client.ReadCollections(db['_self']) if coll['id'] == config.DOCUMENTDB_COLLECTION))

        # Read documents and take first since id should not be duplicated.
        doc = next((doc for doc in client.ReadDocuments(coll['_self']) if doc['id'] == config.DOCUMENTDB_DOCUMENT))

        # Take the data from the deploy_preference and increment our database
        doc[form.deploy_preference.data] = doc[form.deploy_preference.data] + 1
        replaced_document = client.ReplaceDocument(doc['_self'], doc)

        # Create a model to pass to results.html
        class VoteObject:
            choices = dict()
            total_votes = 0

        vote_object = VoteObject()
        vote_object.choices = {
            "Web Site" : doc['Web Site'],
            "Cloud Service" : doc['Cloud Service'],
            "Virtual Machine" : doc['Virtual Machine']
        }
        vote_object.total_votes = sum(vote_object.choices.values())

        return render_template(
            'results.html', 
            year=datetime.now().year, 
            vote_object = vote_object)

    else :
        return render_template(
            'vote.html', 
            title = 'Vote',
            year=datetime.now().year,
            form = form)
```


### <a name="create-the-html-files"></a>Création des fichiers HTML
1. Dans l’Explorateur de solutions, dans le dossier **tutorial**, cliquez avec le bouton droit sur le dossier **templates**, cliquez sur **Ajouter**, puis sur **Nouvel élément**. 
2. Sélectionnez **Page HTML** puis, dans la zone Nom, tapez **create.html**. 
3. Répétez les étapes 1 et 2 pour créer deux autres fichiers HTML : results.html et vote.html.
4. Ajoutez le code suivant à **create.html** in the `<body>` . Il affiche un message indiquant la création d’une base de données, d’une collection et d’un document.
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>{{ title }}.</h2>
    <h3>{{ message }}</h3>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```
5. Ajoutez le code suivant à **results.html** dans l’élément `<body`. Il affiche les résultats du sondage.
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Results of the vote</h2>
        <br />
   
    {% for choice in vote_object.choices %}
    <div class="row">
        <div class="col-sm-5">{{choice}}</div>
            <div class="col-sm-5">
                <div class="progress">
                    <div class="progress-bar" role="progressbar" aria-valuenow="{{vote_object.choices[choice]}}" aria-valuemin="0" aria-valuemax="{{vote_object.total_votes}}" style="width: {{(vote_object.choices[choice]/vote_object.total_votes)*100}}%;">
                                {{vote_object.choices[choice]}}
                </div>
            </div>
            </div>
    </div>
    {% endfor %}
   
    <br />
    <a class="btn btn-primary" href="{{ url_for('vote') }}">Vote again?</a>
    {% endblock %}
    ```
6. Ajoutez le code suivant à **vote.html** dans l’élément `<body`. Il affiche le sondage et accepte les votes. Lors de l'enregistrement des votes, le contrôle est transmis à views.py où nous allons identifier le vote associé et ajouter le document correspondant.
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>What is your favorite way to host an application on Azure?</h2>
    <form action="" method="post" name="vote">
        {{form.hidden_tag()}}
            {{form.deploy_preference}}
            <button class="btn btn-primary" type="submit">Vote</button>
    </form>
    {% endblock %}
    ```
7. Dans le dossier **templates**, remplacez le contenu **d’index.html** par le code suivant. Ce code définit une page d'accueil pour votre application
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Python + Azure Cosmos DB Voting Application.</h2>
    <h3>This is a sample Cosmos DB voting application using PyDocumentDB</h3>
    <p><a href="{{ url_for('create') }}" class="btn btn-primary btn-large">Create/Clear the Voting Database &raquo;</a></p>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```

### <a name="add-a-configuration-file-and-change-the-initpy"></a>Ajout d’un fichier de configuration et modification d’\_\_init\_\_.py
1. Dans l’Explorateur de solutions, cliquez sur le projet **tutorial**, cliquez sur **Ajouter**, cliquez sur **Nouvel élément**, sélectionnez **Fichier Python vide**, puis nommez le fichier **config.py**. Ce fichier de configuration est requis par les formulaires dans Flask. Vous pouvez l'utiliser pour fournir une clé secrète. Cette clé n'est cependant pas nécessaire dans le cadre de ce didacticiel.
2. Ajoutez le code suivant à config.py. Vous devrez modifier les valeurs de **DOCUMENTDB\_HOST** et de **DOCUMENTDB\_KEY** à l’étape suivante.
   
    ```python
    CSRF_ENABLED = True
    SECRET_KEY = 'you-will-never-guess'
   
    DOCUMENTDB_HOST = 'https://YOUR_DOCUMENTDB_NAME.documents.azure.com:443/'
    DOCUMENTDB_KEY = 'YOUR_SECRET_KEY_ENDING_IN_=='
   
    DOCUMENTDB_DATABASE = 'voting database'
    DOCUMENTDB_COLLECTION = 'voting collection'
    DOCUMENTDB_DOCUMENT = 'voting document'
    ```
3. Dans le [portail Azure](https://portal.azure.com/), accédez au panneau **Clés** en cliquant sur **Parcourir**, **Azure Cosmos DB Accounts** (Comptes Azure Cosmos DB), double-cliquez sur le nom du compte à utiliser, puis cliquez sur le bouton **Clés** dans la zone **Éléments principaux**. Dans le panneau **Clés**, copiez la valeur de **l’URI** et collez-la dans le fichier **config.py** comme valeur de la propriété **DOCUMENTDB\_HOST**. 
4. De retour dans le portail Azure, dans le panneau **Clés**, copiez la valeur de la **Clé principale** ou de la **Clé secondaire**, et collez-la dans le fichier **config.py** comme valeur de la propriété **DOCUMENTDB\_KEY**.
5. Dans le fichier **\_\_init\_\_.py**, ajoutez la ligne suivante. 
   
        app.config.from_object('config')
   
    Le contenu du fichier doit donc être :
   
    ```python
    from flask import Flask
    app = Flask(__name__)
    app.config.from_object('config')
    import tutorial.views
    ```
6. Après avoir ajouté tous les fichiers, l’Explorateur de solutions doit ressembler à ceci :
   
    ![Capture d’écran de la fenêtre Explorateur de solutions de Visual Studio](./media/documentdb-python-application/cosmos-db-python-solution-explorer.png)

## <a name="step-4-run-your-web-application-locally"></a>Étape 4 : Exécution locale de votre application web
1. Appuyez sur **Ctrl**+**Maj**+**B** pour générer la solution.
2. Une fois la génération terminée, démarrez le site Web en appuyant sur **F5**. Vous devez voir ceci sur votre écran.
   
    ![Capture d’écran de l’application de vote Python + Azure Cosmos DB affichée dans un navigateur web](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)
3. Cliquez sur **Create/Clear the Voting Database** pour générer la base de données.
   
    ![Capture d’écran de l’écran de création de page de l’application web – Détails du développement](./media/documentdb-python-application/cosmos-db-python-run-create-page.png)
4. Cliquez ensuite sur **Vote** et sélectionnez votre option.
   
    ![Capture d’écran de l’application web avec une question de vote posée](./media/documentdb-python-application/cosmos-db-vote.png)
5. Chaque vote associé augmente le compteur adéquat.
   
    ![Capture d’écran des résultats de la page de vote affichée](./media/documentdb-python-application/cosmos-db-voting-results.png)
6. Arrêtez le débogage du projet en appuyant sur Maj+F5.

## <a name="step-5-deploy-the-web-application-to-azure"></a>Étape 5 : Déploiement de l’application web sur Azure
Maintenant que l’application fonctionne correctement avec Cosmos DB, nous allons la déployer sur Azure.

1. Cliquez avec le bouton droit sur le projet dans l’Explorateur de solutions (assurez-vous de ne pas encore l’exécuter localement), puis sélectionnez **Publier**.  
   
     ![Capture d’écran du didacticiel sélectionné dans l’Explorateur de solutions, avec l’option Publier mise en surbrillance](./media/documentdb-python-application/image20.png)
2. Dans la boîte de dialogue **Publier**, sélectionnez **Microsoft Azure App Service**, choisissez **Création**, puis cliquez sur **Publier**.
   
    ![Capture d’écran de la fenêtre Publier le site web, avec Microsoft Azure App Service en surbrillance](./media/documentdb-python-application/cosmos-db-python-publish.png)
3. Dans la boîte de dialogue **Créer App Service**, saisissez le nom de l’application web, ainsi que **l’abonnement**, le **groupe de ressources** et le **plan App Service**, puis cliquez sur **Créer**.
   
    ![Capture d'écran de la fenêtre Microsoft Azure Web Apps](./media/documentdb-python-application/cosmos-db-python-create-app-service.png)
4. Dans quelques secondes, Visual Studio achèvera la publication de votre service d’application et lancera un navigateur, dans lequel vous pourrez voir votre réalisation exécutée dans Azure.

    ![Capture d'écran de la fenêtre Microsoft Azure Web Apps](./media/documentdb-python-application/cosmos-db-python-appservice-created.png)

## <a name="troubleshooting"></a>Résolution des problèmes
S’il s’agit de la première application Python que vous avez exécutée sur votre ordinateur, assurez-vous que les dossiers suivants (ou les emplacements d’installation équivalents) sont inclus dans votre variable PATH :

    C:\Python27\site-packages;C:\Python27\;C:\Python27\Scripts;

Si vous recevez une erreur sur votre page de vote et que vous avez nommé votre projet autrement que **tutorial**, assurez-vous que **\_\_init\_\_.py** fait référence au nom de projet correct dans la ligne : `import tutorial.view`.

## <a name="next-steps"></a>Étapes suivantes
Félicitations ! Vous venez de créer votre première application web Python avec Cosmos DB, et de la publier sur Azure.

Nous mettons à jour et améliorons cette rubrique fréquemment en fonction de vos commentaires.  Une fois le didacticiel terminé, utilisez les boutons de vote en haut et en bas de cette page et veillez à indiquer vos commentaires sur les améliorations que nous pourrions apporter. Si vous souhaitez que nous vous contactions directement, n’hésitez pas à inclure votre adresse de messagerie dans vos commentaires.

Pour ajouter des fonctionnalités supplémentaires à votre application web, passez en revue les API disponibles dans le [Kit de développement logiciel (SDK) Azure Cosmos DB](documentdb-sdk-python.md).

Pour plus d’informations sur Azure, Visual Studio et Python, consultez le [Centre de développement Python](https://azure.microsoft.com/develop/python/). 

Pour d’autres didacticiels Python Flask, consultez [The Flask Mega-Tutorial, Part I: Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world). 

[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[2]: https://www.python.org/downloads/windows/
[3]: https://www.microsoft.com/download/details.aspx?id=44266
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Azure portal]: http://portal.azure.com
