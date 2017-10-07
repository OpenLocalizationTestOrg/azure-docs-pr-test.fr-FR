---
title: "didacticiel d’application web aaaPython ballon pour la base de données Azure Cosmos | Documents Microsoft"
description: "Passez en revue un didacticiel de base de données sur l’utilisation de données de base de données Azure Cosmos toostore et l’accès à partir d’une application web de Python ballon hébergée sur Azure. Trouvez des solutions de développement d’applications."
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
ms.openlocfilehash: 87b73c656ed96a7efbd162843a1529d435f027f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-python-flask-web-application-using-azure-cosmos-db"></a>Créer une application web Python Flask à l’aide d’Azure Cosmos DB
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [Node.JS](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

Ce didacticiel vous montre comment les données de toostore et d’accès de base de données Azure Cosmos à partir d’une Python toouse web application hébergée sur Azure et suppose que vous avez une connaissance préalable à l’aide de Python et des sites Web Azure.

Ce didacticiel de base de données traite les points suivants :

1. Création et approvisionnement d’un compte Cosmos DB.
2. Création d’une application Python Flask.
3. Connexion tooand à l’aide de la base de données Cosmos à partir de votre application web.
4. Déploiement hello web application tooAzure.

En suivant ce didacticiel, vous allez générer une application de vote simple qui vous permet de toovote pour une interrogation.

![Capture d’écran de l’application de vote hello créée par ce didacticiel de base de données](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)

## <a name="database-tutorial-prerequisites"></a>Conditions préalables à l’exécution de ce didacticiel de base de données
Avant de suivre les instructions de hello dans cet article, vous devez vous assurer d’avoir installé des éléments suivants hello :

* Un compte Azure actif. Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).
 
    OU 

    Une installation locale de hello [Azure Cosmos DB émulateur](local-emulator.md).
* [Microsoft Visual Studio Community 2017](http://www.visualstudio.com/).  
* [Python Tools pour Visual Studio](https://github.com/Microsoft/PTVS/).  
* [Kit de développement logiciel (SDK) Microsoft Azure pour Python 2.7](https://azure.microsoft.com/downloads/). 
* [Python 2.7.13](https://www.python.org/downloads/windows/). 

> [!IMPORTANT]
> Si vous installez Python 2.7 pour hello première fois, vérifiez que l’écran hello personnaliser Python 2.7.13, vous sélectionnez **ajouter python.exe tooPath**.
> 
> ![Capture d’écran de l’écran de personnaliser les Python 2.7.11 hello, dans lequel vous devez tooselect ajouter python.exe tooPath](./media/documentdb-python-application/cosmos-db-python-install.png)
> 
> 

* [Compilateur Microsoft Visual C++ pour Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266).

## <a name="step-1-create-an-azure-cosmos-db-database-account"></a>Étape 1 : création d’un compte de base de données Azure Cosmos DB
Commençons par créer un compte Cosmos DB. Si vous déjà disposez d’un compte ou si vous utilisez hello Azure Cosmos DB émulateur pour ce didacticiel, vous pouvez ignorer trop[étape 2 : créer une application web Python ballon](#step-2-create-a-new-python-flask-web-application).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<br/>
Nous étudierons maintenant comment toocreate une application web à partir de hello Python ballon au sol.

## <a name="step-2-create-a-new-python-flask-web-application"></a>Étape 2 : Création d’une application web Python Flask
1. Dans Visual Studio, sur hello **fichier** menu, pointez trop**nouveau**, puis cliquez sur **projet**.
   
    Hello **nouveau projet** boîte de dialogue s’affiche.
2. Dans le volet gauche de hello, développez **modèles** , puis **Python**, puis cliquez sur **Web**. 
3. Sélectionnez **ballon Web projet** dans le volet central de hello, puis dans hello **nom** zone **didacticiel**, puis cliquez sur **OK**. Souvenez-vous que les noms de package Python doivent être en minuscules comme décrit dans hello [Guide de Style pour le Code Python](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).
   
    Pour ces tooPython nouveau ballon, il est une infrastructure de développement d’application web qui vous permet de générer des applications web de Python plus rapidement.
   
    ![Capture d’écran de la fenêtre de nouveau projet hello dans Visual Studio avec Python mis en surbrillance sur hello gauche, Python ballon Web projet dans hello intermédiaire et de didacticiel de nom hello dans la zone de nom hello](./media/documentdb-python-application/image9.png)
4. Bonjour **outils Python pour Visual Studio** fenêtre, cliquez sur **installer dans un environnement virtuel**. 
   
    ![Capture d’écran du didacticiel de base de données hello - outils Python pour la fenêtre de Visual Studio](./media/documentdb-python-application/python-install-virtual-environment.png)
5. Bonjour **ajouter l’environnement virtuel** fenêtre, vous pouvez accepter les valeurs par défaut hello et utiliser Python 2.7 comme environnement de base de hello, car PyDocumentDB ne prend pas en charge les Python 3.x, puis cliquez sur **créer**. Cela configure l’environnement virtuel de Python hello requis pour votre projet.
   
    ![Capture d’écran du didacticiel de base de données hello - outils Python pour la fenêtre de Visual Studio](./media/documentdb-python-application/image10_A.png)
   
    affiche de la fenêtre de sortie Hello `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` lorsque des environnement de hello est correctement installé.

## <a name="step-3-modify-hello-python-flask-web-application"></a>Étape 3 : Modifier l’application web de Python ballon hello
### <a name="add-hello-python-flask-packages-tooyour-project"></a>Ajouter un projet de tooyour packages hello ballon de Python
Une fois que votre projet est configuré, vous devez tooadd hello requis ballon packages tooyour projet, y compris pydocumentdb, package de Python hello pour DocumentDB.

1. Dans l’Explorateur de solutions, ouvrez le fichier de hello nommé **requirements.txt** et remplacez le contenu de hello par qui suit hello :
   
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
2. Enregistrer hello **requirements.txt** fichier. 
3. Dans l’Explorateur de solutions, cliquez avec le bouton droit sur **env**, puis cliquez sur **Install from requirements.txt** (Installer depuis requirements.txt).
   
    ![Capture d’écran montrant env (Python 2.7) sélectionné avec l’installation à partir de requirements.txt mis en surbrillance dans la liste de hello](./media/documentdb-python-application/cosmos-db-python-install-from-requirements.png)
   
    Après l’installation, la fenêtre de sortie de hello affiche suivant de hello :
   
        Successfully installed Babel-2.3.2 Tempita-0.5.2 WTForms-2.1 Whoosh-2.7.4 blinker-1.4 decorator-4.0.9 flask-0.9 flask-babel-0.8 flask-mail-0.7.6 flask-sqlalchemy-0.16 flask-whooshalchemy-0.55a0 flask-wtf-0.8.4 flup-1.0.2 pydocumentdb-1.6.1 pytz-2013b0 speaklater-1.3 sqlalchemy-0.7.9 sqlalchemy-migrate-0.7.2
   
   > [!NOTE]
   > Dans de rares cas, vous pouvez voir un échec dans la fenêtre de sortie hello. Si cela se produit, vérifiez si des erreurs de hello sont toocleanup connexe. Parfois, le nettoyage de hello échoue, mais hello installation toujours sera réussie (défiler vers le haut dans tooverify de fenêtre de sortie hello cela). Vous pouvez vérifier votre installation en [environnement virtuel de vérification hello](#verify-the-virtual-environment). Si l’échec de l’installation de hello mais hello vérification s’effectue correctement, il est toocontinue OK.
   > 
   > 

### <a name="verify-hello-virtual-environment"></a>Vérifier l’environnement virtuel de hello
Vérifiez que l'installation est réussie.

1. Générez la solution de hello en appuyant sur **Ctrl**+**MAJ**+**B**.
2. Une fois hello génération terminée, démarrez le site Web de hello en appuyant sur **F5**. Cela lance le serveur de développement ballon hello et lance votre navigateur web. Vous devez voir hello après page.
   
    ![Hello Python ballon projet web vide développement affiché dans un navigateur](./media/documentdb-python-application/image12.png)
3. Arrêter le débogage du site Web hello en appuyant sur **MAJ**+**F5** dans Visual Studio.

### <a name="create-database-collection-and-document-definitions"></a>Création des définitions pour la base de données, la collection et le document
Nous allons maintenant créer votre application de vote en ajoutant de nouveaux fichiers et en mettant à jour d’autres fichiers.

1. Dans l’Explorateur de solutions, cliquez sur hello **didacticiel** de projet, cliquez sur **ajouter**, puis cliquez sur **un nouvel élément**. Sélectionnez **fichier Python vide** et le nom de fichier hello **forms.py**.  
2. Ajouter hello code toohello forms.py fichier suivant, puis enregistrez le fichier de hello.

```python
from flask.ext.wtf import Form
from wtforms import RadioField

class VoteForm(Form):
    deploy_preference  = RadioField('Deployment Preference', choices=[
        ('Web Site', 'Web Site'),
        ('Cloud Service', 'Cloud Service'),
        ('Virtual Machine', 'Virtual Machine')], default='Web Site')
```


### <a name="add-hello-required-imports-tooviewspy"></a>Ajouter tooviews.py d’importations hello requis
1. Dans l’Explorateur de solutions, développez hello **didacticiel** dossier et ouvrez hello **views.py** fichier. 
2. Ajouter hello après importation instructions toohello en haut de hello **views.py** de fichier, puis enregistrez le fichier de hello. Ces importer Cosmos DB PythonSDK et hello les packages flacon.
   
    ```python
    from forms import VoteForm
    import config
    import pydocumentdb.document_client as document_client
    ```

### <a name="create-database-collection-and-document"></a>Création de base de données, de collection et de document
* Toujours dans **views.py**, ajouter hello suivant code toohello la fin du fichier de hello. Il prend en charge de la création de la base de données hello utilisé par le formulaire de hello. Ne supprimez pas de code existant de hello dans **views.py**. Ajouter simplement cette terminaison toohello.

```python
@app.route('/create')
def create():
    """Renders hello contact page."""
    client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

    # Attempt toodelete hello database.  This allows this toobe used toorecreate as well as create
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
* Toujours dans **views.py**, ajouter hello suivant code toohello la fin du fichier de hello. Il prend en charge de la définition de formulaire hello, lire le document, la collection et base de données hello. Ne supprimez pas de code existant de hello dans **views.py**. Ajouter simplement cette terminaison toohello.

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

        # Take hello data from hello deploy_preference and increment our database
        doc[form.deploy_preference.data] = doc[form.deploy_preference.data] + 1
        replaced_document = client.ReplaceDocument(doc['_self'], doc)

        # Create a model toopass tooresults.html
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


### <a name="create-hello-html-files"></a>Créer des fichiers HTML hello
1. Dans l’Explorateur de solutions, Bonjour **didacticiel** dossier, à droite cliquez sur hello **modèles** dossier, cliquez sur **ajouter**, puis cliquez sur **un nouvel élément**. 
2. Sélectionnez **HTML Page**, puis, dans le type de zone de nom hello **create.html**. 
3. Répétez les étapes 1 et 2 toocreate deux autres fichiers HTML : results.html et vote.html.
4. Ajouter hello suivant code trop**create.html** Bonjour `<body>` élément. Il affiche un message indiquant la création d’une base de données, d’une collection et d’un document.
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>{{ title }}.</h2>
    <h3>{{ message }}</h3>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```
5. Ajouter hello suivant code trop**results.html** Bonjour `<body`> élément. Il affiche les résultats de hello d’interrogation de hello.
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Results of hello vote</h2>
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
6. Ajouter hello suivant code trop**vote.html** Bonjour `<body`> élément. Il affiche l’interrogation hello et accepte les votes hello. Sur l’enregistrement des votes de hello, contrôle de hello est transmise sur tooviews.py où nous reconnaîtra hello vote cast et ajouter le document de hello en conséquence.
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>What is your favorite way toohost an application on Azure?</h2>
    <form action="" method="post" name="vote">
        {{form.hidden_tag()}}
            {{form.deploy_preference}}
            <button class="btn btn-primary" type="submit">Vote</button>
    </form>
    {% endblock %}
    ```
7. Bonjour **modèles** dossier, le contenu de hello de remplacement de **index.html** avec les éléments suivants de hello. Cela sert de hello page de votre application de destination.
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Python + Azure Cosmos DB Voting Application.</h2>
    <h3>This is a sample Cosmos DB voting application using PyDocumentDB</h3>
    <p><a href="{{ url_for('create') }}" class="btn btn-primary btn-large">Create/Clear hello Voting Database &raquo;</a></p>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```

### <a name="add-a-configuration-file-and-change-hello-initpy"></a>Ajouter un fichier de configuration et de modifier hello \_ \_init\_\_.py
1. Dans l’Explorateur de solutions, cliquez sur hello **didacticiel** de projet, cliquez sur **ajouter**, cliquez sur **un nouvel élément**, sélectionnez **fichier Python vide**, puis nom de fichier hello **config.py**. Ce fichier de configuration est requis par les formulaires dans Flask. Vous pouvez l’utiliser tooprovide une clé de secret principal. Cette clé n'est cependant pas nécessaire dans le cadre de ce didacticiel.
2. Ajoutez hello suivant tooconfig.py de code, vous aurez besoin de valeurs hello tooalter **DOCUMENTDB\_hôte** et **DOCUMENTDB\_clé** à l’étape suivante de hello.
   
    ```python
    CSRF_ENABLED = True
    SECRET_KEY = 'you-will-never-guess'
   
    DOCUMENTDB_HOST = 'https://YOUR_DOCUMENTDB_NAME.documents.azure.com:443/'
    DOCUMENTDB_KEY = 'YOUR_SECRET_KEY_ENDING_IN_=='
   
    DOCUMENTDB_DATABASE = 'voting database'
    DOCUMENTDB_COLLECTION = 'voting collection'
    DOCUMENTDB_DOCUMENT = 'voting document'
    ```
3. Bonjour [portail Azure](https://portal.azure.com/), accédez toohello **clés** panneau en cliquant sur **Parcourir**, **des comptes de base de données Azure Cosmos**, double-cliquez sur le nom de hello Hello toouse de compte, puis cliquez sur hello **clés** bouton Bonjour **Essentials** zone. Bonjour **clés** panneau, hello de copie **URI** valeur et le coller dans hello **config.py** fichier, en tant que valeur hello pour hello **DOCUMENTDB\_hôte**  propriété. 
4. Dans hello portail Azure, Bonjour **clés** panneau, copier la valeur hello Hello **clé primaire** ou hello **clé secondaire**et le coller dans hello **config.py**  fichier, en tant que valeur hello pour hello **DOCUMENTDB\_clé** propriété.
5. Bonjour  **\_ \_init\_\_.py** , ajoutez hello ligne suivante. 
   
        app.config.from_object('config')
   
    Afin que le contenu du fichier de hello hello est la suivante :
   
    ```python
    from flask import Flask
    app = Flask(__name__)
    app.config.from_object('config')
    import tutorial.views
    ```
6. Après avoir ajouté tous les fichiers de hello, l’Explorateur de solutions doit ressembler à ceci :
   
    ![Capture d’écran de la fenêtre de l’Explorateur de solutions Visual Studio hello](./media/documentdb-python-application/cosmos-db-python-solution-explorer.png)

## <a name="step-4-run-your-web-application-locally"></a>Étape 4 : Exécution locale de votre application web
1. Générez la solution de hello en appuyant sur **Ctrl**+**MAJ**+**B**.
2. Une fois hello génération terminée, démarrez le site Web de hello en appuyant sur **F5**. Vous devez voir s’afficher hello sur votre écran.
   
    ![Capture d’écran de hello Python + Azure Cosmos DB vote Application affichée dans un navigateur web](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)
3. Cliquez sur **créer/effacer hello vote de la base de données** base de données toogenerate hello.
   
    ![Capture d’écran de hello créer une Page d’application web de hello – informations sur le développement](./media/documentdb-python-application/cosmos-db-python-run-create-page.png)
4. Cliquez ensuite sur **Vote** et sélectionnez votre option.
   
    ![Capture d’écran de l’application web de hello à poser une question de vote posée](./media/documentdb-python-application/cosmos-db-vote.png)
5. Pour chaque vote que vous effectuer un cast, elle incrémente compteur approprié de hello.
   
    ![Capture d’écran de hello résultats de la page de vote hello indiqué](./media/documentdb-python-application/cosmos-db-voting-results.png)
6. Arrêter le débogage du projet de hello en appuyant sur MAJ + F5.

## <a name="step-5-deploy-hello-web-application-tooazure"></a>Étape 5 : Déployer hello web application tooAzure
Maintenant que vous avez application complète de hello fonctionne correctement sur la base de données Cosmos, nous allons toodeploy cette tooAzure.

1. Projet de hello avec le bouton droit dans l’Explorateur de solutions (Assurez-vous que vous n’êtes pas en cours d’exécution il localement), puis sélectionnez **publier**.  
   
     ![Capture d’écran du didacticiel hello sélectionné dans l’Explorateur de solutions, avec l’option de publication hello mis en surbrillance](./media/documentdb-python-application/image20.png)
2. Bonjour **publier** boîte de dialogue, sélectionnez **Microsoft Azure App Service**, sélectionnez **créer un nouveau**, puis cliquez sur **publier**.
   
    ![Capture d’écran de la fenêtre de publier le site Web hello avec Microsoft Azure App Service est mis en surbrillance](./media/documentdb-python-application/cosmos-db-python-publish.png)
3. Bonjour **créer un Service application** boîte de dialogue, entrez le nom hello pour votre application web avec votre **abonnement**, **groupe de ressources**, et **du Plan App Service** , puis cliquez sur **créer**.
   
    ![Capture d’écran de la fenêtre de Microsoft Azure Web Apps fenêtre hello](./media/documentdb-python-application/cosmos-db-python-create-app-service.png)
4. Dans quelques secondes, Visual Studio achèvera la publication de votre service d’application et lancera un navigateur, dans lequel vous pourrez voir votre réalisation exécutée dans Azure.

    ![Capture d’écran de la fenêtre de Microsoft Azure Web Apps fenêtre hello](./media/documentdb-python-application/cosmos-db-python-appservice-created.png)

## <a name="troubleshooting"></a>Résolution des problèmes
Si c’est la première application Python hello, que vous exécutez sur votre ordinateur, vérifiez ce qui suit hello dossiers (ou l’emplacement d’installation équivalente hello) est inclus dans votre variable de chemin d’accès :

    C:\Python27\site-packages;C:\Python27\;C:\Python27\Scripts;

Si vous recevez une erreur sur votre page de vote, et que vous avez nommé votre projet autre que **didacticiel**, assurez-vous que  **\_ \_init\_\_.py** références hello nom de projet approprié dans la ligne de hello : `import tutorial.view`.

## <a name="next-steps"></a>Étapes suivantes
Félicitations ! Vous avez simplement terminé votre première application web de Python à l’aide de la base de données Cosmos et publié tooAzure.

Nous mettons à jour et améliorons cette rubrique fréquemment en fonction de vos commentaires.  Une fois vous venez de terminer hello didacticiel, veuillez à l’aide de hello vote des boutons situés en haut de hello et en bas de cette page et tooinclude que vos commentaires sur les améliorations souhaitées toosee apportée. Si vous souhaitez que nous toocontact vous directement, vous pouvez tooinclude libre votre adresse de messagerie dans vos commentaires.

application de web tooyour tooadd des fonctionnalités supplémentaires, consultez hello API disponibles dans hello [Azure Cosmos DB Python SDK](documentdb-sdk-python.md).

Pour plus d’informations sur Azure, Visual Studio et Python, consultez hello [centre de développement Python](https://azure.microsoft.com/develop/python/). 

Pour d’autres didacticiels ballon de Python, consultez [hello ballon méga-didacticiel, partie i : Hello, World !](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world). 

[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[2]: https://www.python.org/downloads/windows/
[3]: https://www.microsoft.com/download/details.aspx?id=44266
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Azure portal]: http://portal.azure.com
