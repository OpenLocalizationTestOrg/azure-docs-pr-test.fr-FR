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
ms.openlocfilehash: ed5284b5a265840c43dbc9890082a7c038d22975
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="build-a-python-flask-web-application-using-azure-cosmos-db"></a><span data-ttu-id="663d9-105">Créer une application web Python Flask à l’aide d’Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="663d9-105">Build a Python Flask web application using Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="663d9-106">.NET</span><span class="sxs-lookup"><span data-stu-id="663d9-106">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="663d9-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="663d9-107">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="663d9-108">Java</span><span class="sxs-lookup"><span data-stu-id="663d9-108">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="663d9-109">Python</span><span class="sxs-lookup"><span data-stu-id="663d9-109">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="663d9-110">Ce didacticiel vous montre comment utiliser Azure Cosmos DB pour stocker des données et y accéder à partir d’une application web Python hébergée sur Azure. Il suppose que vous avez déjà une expérience de l’utilisation de Python et des sites web Azure.</span><span class="sxs-lookup"><span data-stu-id="663d9-110">This tutorial shows you how to use Azure Cosmos DB to store and access data from a Python web application hosted on Azure and presumes that you have some prior experience using Python and Azure websites.</span></span>

<span data-ttu-id="663d9-111">Ce didacticiel de base de données traite les points suivants :</span><span class="sxs-lookup"><span data-stu-id="663d9-111">This database tutorial covers:</span></span>

1. <span data-ttu-id="663d9-112">Création et approvisionnement d’un compte Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="663d9-112">Creating and provisioning a Cosmos DB account.</span></span>
2. <span data-ttu-id="663d9-113">Création d’une application Python Flask.</span><span class="sxs-lookup"><span data-stu-id="663d9-113">Creating a Python Flask application.</span></span>
3. <span data-ttu-id="663d9-114">Connexion à Cosmos DB pour une utilisation à partir de votre application web.</span><span class="sxs-lookup"><span data-stu-id="663d9-114">Connecting to and using Cosmos DB from your web application.</span></span>
4. <span data-ttu-id="663d9-115">Déploiement de l’application web sur Azure.</span><span class="sxs-lookup"><span data-stu-id="663d9-115">Deploying the web application to Azure.</span></span>

<span data-ttu-id="663d9-116">Dans ce didacticiel, vous allez créer une application de vote simple qui vous permettra de voter lors d’un sondage.</span><span class="sxs-lookup"><span data-stu-id="663d9-116">By following this tutorial, you will build a simple voting application that allows you to vote for a poll.</span></span>

![Capture d’écran de l’application de vote créée avec ce didacticiel d’utilisation de la base de données](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)

## <a name="database-tutorial-prerequisites"></a><span data-ttu-id="663d9-118">Conditions préalables à l’exécution de ce didacticiel de base de données</span><span class="sxs-lookup"><span data-stu-id="663d9-118">Database tutorial prerequisites</span></span>
<span data-ttu-id="663d9-119">Avant de suivre les instructions de cet article, vérifiez que les éléments suivants sont installés :</span><span class="sxs-lookup"><span data-stu-id="663d9-119">Before following the instructions in this article, you should ensure that you have the following installed:</span></span>

* <span data-ttu-id="663d9-120">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="663d9-120">An active Azure account.</span></span> <span data-ttu-id="663d9-121">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="663d9-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="663d9-122">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="663d9-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
 
    <span data-ttu-id="663d9-123">OU</span><span class="sxs-lookup"><span data-stu-id="663d9-123">OR</span></span> 

    <span data-ttu-id="663d9-124">Une installation locale de [l’émulateur Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="663d9-124">A local installation of the [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="663d9-125">[Microsoft Visual Studio Community 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="663d9-125">[Microsoft Visual Studio Community 2017](http://www.visualstudio.com/).</span></span>  
* <span data-ttu-id="663d9-126">[Python Tools pour Visual Studio](https://github.com/Microsoft/PTVS/).</span><span class="sxs-lookup"><span data-stu-id="663d9-126">[Python Tools for Visual Studio](https://github.com/Microsoft/PTVS/).</span></span>  
* <span data-ttu-id="663d9-127">[Kit de développement logiciel (SDK) Microsoft Azure pour Python 2.7](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="663d9-127">[Microsoft Azure SDK for Python 2.7](https://azure.microsoft.com/downloads/).</span></span> 
* <span data-ttu-id="663d9-128">[Python 2.7.13](https://www.python.org/downloads/windows/).</span><span class="sxs-lookup"><span data-stu-id="663d9-128">[Python 2.7.13](https://www.python.org/downloads/windows/).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="663d9-129">Si vous installez Python 2.7 pour la première fois, sélectionnez **Ajouter python.exe au chemin d’accès** dans l’écran Personnaliser Python 2.7.13.</span><span class="sxs-lookup"><span data-stu-id="663d9-129">If you are installing Python 2.7 for the first time, ensure that in the Customize Python 2.7.13 screen, you select **Add python.exe to Path**.</span></span>
> 
> ![Capture d’écran de l’écran Personnaliser Python 2.7.11, où vous devez sélectionner Ajouter python.exe au chemin](./media/documentdb-python-application/cosmos-db-python-install.png)
> 
> 

* <span data-ttu-id="663d9-131">[Compilateur Microsoft Visual C++ pour Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266).</span><span class="sxs-lookup"><span data-stu-id="663d9-131">[Microsoft Visual C++ Compiler for Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-database-account"></a><span data-ttu-id="663d9-132">Étape 1 : création d’un compte de base de données Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="663d9-132">Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="663d9-133">Commençons par créer un compte Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="663d9-133">Let's start by creating an Cosmos DB account.</span></span> <span data-ttu-id="663d9-134">Si vous possédez déjà un compte ou si vous utilisez l’émulateur Azure Cosmos DB pour ce didacticiel, vous pouvez passer à [l’étape 2 : création d’une application web Python Flask](#step-2-create-a-new-python-flask-web-application).</span><span class="sxs-lookup"><span data-stu-id="663d9-134">If you already have an account or if you are using the Azure Cosmos DB Emulator for this tutorial, you can skip to [Step 2: Create a new Python Flask web application](#step-2-create-a-new-python-flask-web-application).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<br/>
<span data-ttu-id="663d9-135">Voyons à présent comment créer une application web Python Flask de A à Z.</span><span class="sxs-lookup"><span data-stu-id="663d9-135">We will now walk through how to create a new Python Flask web application from the ground up.</span></span>

## <a name="step-2-create-a-new-python-flask-web-application"></a><span data-ttu-id="663d9-136">Étape 2 : Création d’une application web Python Flask</span><span class="sxs-lookup"><span data-stu-id="663d9-136">Step 2: Create a new Python Flask web application</span></span>
1. <span data-ttu-id="663d9-137">Dans Visual Studio, dans le menu **Fichier**, pointez sur **Nouveau**, puis cliquez sur **Projet**.</span><span class="sxs-lookup"><span data-stu-id="663d9-137">In Visual Studio, on the **File** menu, point to **New**, and then click **Project**.</span></span>
   
    <span data-ttu-id="663d9-138">La boîte de dialogue **Nouveau projet** apparaît.</span><span class="sxs-lookup"><span data-stu-id="663d9-138">The **New Project** dialog box appears.</span></span>
2. <span data-ttu-id="663d9-139">Dans le volet gauche, développez **Modèles** puis **Python**, puis cliquez sur **Web**.</span><span class="sxs-lookup"><span data-stu-id="663d9-139">In the left pane, expand **Templates** and then **Python**, and then click **Web**.</span></span> 
3. <span data-ttu-id="663d9-140">Sélectionnez **Projet web Flask** dans le volet central puis, dans la zone **Nom**, tapez **tutorial**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="663d9-140">Select **Flask  Web Project** in the center pane, then in the **Name** box type **tutorial**, and then click **OK**.</span></span> <span data-ttu-id="663d9-141">N’oubliez pas que les noms de package Python doivent être entièrement en minuscules, comme décrit dans le [Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).</span><span class="sxs-lookup"><span data-stu-id="663d9-141">Remember that Python package names should be all lowercase, as described in the [Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).</span></span>
   
    <span data-ttu-id="663d9-142">Si vous ne connaissez pas bien Python Flask, sachez qu’il s’agit d’une infrastructure de développement d’applications web qui permet d’accélérer la création d’applications web dans Python.</span><span class="sxs-lookup"><span data-stu-id="663d9-142">For those new to Python Flask, it is a web application development framework that helps you build web applications in Python faster.</span></span>
   
    ![Capture d’écran de la fenêtre Nouveau projet dans Visual Studio avec Python mis en surbrillance sur la gauche, le projet web Python Flask sélectionné au milieu et le didacticiel name dans la zone Nom](./media/documentdb-python-application/image9.png)
4. <span data-ttu-id="663d9-144">Dans la fenêtre **Outils Python pour Visual Studio**, cliquez sur **Installer dans un environnement virtuel**.</span><span class="sxs-lookup"><span data-stu-id="663d9-144">In the **Python Tools for Visual Studio** window, click **Install into a virtual environment**.</span></span> 
   
    ![Capture d’écran du didacticiel de base de données - Fenêtre Python Tools pour Visual Studio](./media/documentdb-python-application/python-install-virtual-environment.png)
5. <span data-ttu-id="663d9-146">Dans la fenêtre **Ajouter un environnement virtuel**, vous pouvez accepter les valeurs par défaut et utiliser Python 2.7 comme environnement de base, car PyDocumentDB ne prend actuellement pas en charge Python 3.x, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="663d9-146">In the **Add Virtual Environment** window, you can accept the defaults and use Python 2.7 as the base environment because PyDocumentDB does not currently support Python 3.x, and then click **Create**.</span></span> <span data-ttu-id="663d9-147">Cette opération configure l’environnement virtuel Python nécessaire à votre projet.</span><span class="sxs-lookup"><span data-stu-id="663d9-147">This sets up the required Python virtual environment for your project.</span></span>
   
    ![Capture d’écran du didacticiel de base de données - Fenêtre Python Tools pour Visual Studio](./media/documentdb-python-application/image10_A.png)
   
    <span data-ttu-id="663d9-149">La fenêtre de sortie affiche `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` quand l’environnement est correctement installé.</span><span class="sxs-lookup"><span data-stu-id="663d9-149">The output window displays `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` when the environment is successfully installed.</span></span>

## <a name="step-3-modify-the-python-flask-web-application"></a><span data-ttu-id="663d9-150">Étape 3 : Modification de l’application web Python Flask</span><span class="sxs-lookup"><span data-stu-id="663d9-150">Step 3: Modify the Python Flask web application</span></span>
### <a name="add-the-python-flask-packages-to-your-project"></a><span data-ttu-id="663d9-151">Ajouter les packages Python Flask à votre projet</span><span class="sxs-lookup"><span data-stu-id="663d9-151">Add the Python Flask packages to your project</span></span>
<span data-ttu-id="663d9-152">Une fois votre projet configuré, vous devez ajouter les packages Flask requis, dont pydocumentdb, le package Python pour DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="663d9-152">After your project is set up, you'll need to add the required Flask packages to your project, including pydocumentdb, the Python package for DocumentDB.</span></span>

1. <span data-ttu-id="663d9-153">Dans l’Explorateur de solutions, ouvrez le fichier nommé **requirements.txt** et remplacez son contenu par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="663d9-153">In Solution Explorer, open the file named **requirements.txt** and replace the contents with the following:</span></span>
   
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
2. <span data-ttu-id="663d9-154">Enregistrez le fichier **requirements.txt** .</span><span class="sxs-lookup"><span data-stu-id="663d9-154">Save the **requirements.txt** file.</span></span> 
3. <span data-ttu-id="663d9-155">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur **env**, puis cliquez sur **Install from requirements.txt** (Installer depuis requirements.txt).</span><span class="sxs-lookup"><span data-stu-id="663d9-155">In Solution Explorer, right-click **env** and click **Install from requirements.txt**.</span></span>
   
    ![Capture d’écran affichant env (Python 2.7) sélectionné avec Install from requirements.txt mis en surbrillance dans la liste](./media/documentdb-python-application/cosmos-db-python-install-from-requirements.png)
   
    <span data-ttu-id="663d9-157">Après l’installation, la fenêtre de sortie affiche les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="663d9-157">After successful installation, the output window displays the following:</span></span>
   
        Successfully installed Babel-2.3.2 Tempita-0.5.2 WTForms-2.1 Whoosh-2.7.4 blinker-1.4 decorator-4.0.9 flask-0.9 flask-babel-0.8 flask-mail-0.7.6 flask-sqlalchemy-0.16 flask-whooshalchemy-0.55a0 flask-wtf-0.8.4 flup-1.0.2 pydocumentdb-1.6.1 pytz-2013b0 speaklater-1.3 sqlalchemy-0.7.9 sqlalchemy-migrate-0.7.2
   
   > [!NOTE]
   > <span data-ttu-id="663d9-158">Dans de rares cas, la fenêtre de résultat peut afficher une erreur.</span><span class="sxs-lookup"><span data-stu-id="663d9-158">In rare cases, you might see a failure in the output window.</span></span> <span data-ttu-id="663d9-159">Si cela se produit, vérifiez si l’erreur n'est pas liée au nettoyage.</span><span class="sxs-lookup"><span data-stu-id="663d9-159">If this happens, check if the error is related to cleanup.</span></span> <span data-ttu-id="663d9-160">Parfois, le nettoyage peut échouer, alors que l’installation sera réussie (faites défiler le contenu de la fenêtre de résultat pour le vérifier).</span><span class="sxs-lookup"><span data-stu-id="663d9-160">Sometimes the cleanup fails, but the installation will still be successful (scroll up in the output window to verify this).</span></span> <span data-ttu-id="663d9-161">Vous pouvez vérifier votre installation via la [vérification de l’environnement virtuel](#verify-the-virtual-environment).</span><span class="sxs-lookup"><span data-stu-id="663d9-161">You can check your installation by [Verifying the virtual environment](#verify-the-virtual-environment).</span></span> <span data-ttu-id="663d9-162">Si l’installation échoue mais que la vérification réussit, vous pouvez continuer.</span><span class="sxs-lookup"><span data-stu-id="663d9-162">If the installation failed but the verification is successful, it's OK to continue.</span></span>
   > 
   > 

### <a name="verify-the-virtual-environment"></a><span data-ttu-id="663d9-163">Vérification de l'environnement virtuel</span><span class="sxs-lookup"><span data-stu-id="663d9-163">Verify the virtual environment</span></span>
<span data-ttu-id="663d9-164">Vérifiez que l'installation est réussie.</span><span class="sxs-lookup"><span data-stu-id="663d9-164">Let's make sure that everything is installed correctly.</span></span>

1. <span data-ttu-id="663d9-165">Appuyez sur **Ctrl**+**Maj**+**B** pour générer la solution.</span><span class="sxs-lookup"><span data-stu-id="663d9-165">Build the solution by pressing **Ctrl**+**Shift**+**B**.</span></span>
2. <span data-ttu-id="663d9-166">Une fois la génération terminée, démarrez le site Web en appuyant sur **F5**.</span><span class="sxs-lookup"><span data-stu-id="663d9-166">Once the build succeeds, start the website by pressing **F5**.</span></span> <span data-ttu-id="663d9-167">Cette action démarre le serveur de développement Flask ainsi que votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="663d9-167">This launches the Flask development server and starts your web browser.</span></span> <span data-ttu-id="663d9-168">La page suivante doit s'afficher.</span><span class="sxs-lookup"><span data-stu-id="663d9-168">You should see the following page.</span></span>
   
    ![Projet de développement web Python Flask vide affiché dans un navigateur](./media/documentdb-python-application/image12.png)
3. <span data-ttu-id="663d9-170">Arrêtez le débogage du site web en appuyant sur **Maj**+**F5** dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="663d9-170">Stop debugging the website by pressing **Shift**+**F5** in Visual Studio.</span></span>

### <a name="create-database-collection-and-document-definitions"></a><span data-ttu-id="663d9-171">Création des définitions pour la base de données, la collection et le document</span><span class="sxs-lookup"><span data-stu-id="663d9-171">Create database, collection, and document definitions</span></span>
<span data-ttu-id="663d9-172">Nous allons maintenant créer votre application de vote en ajoutant de nouveaux fichiers et en mettant à jour d’autres fichiers.</span><span class="sxs-lookup"><span data-stu-id="663d9-172">Now let's create your voting application by adding new files and updating others.</span></span>

1. <span data-ttu-id="663d9-173">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le projet **tutorial**, cliquez sur **Ajouter**, puis sur **Nouvel élément**.</span><span class="sxs-lookup"><span data-stu-id="663d9-173">In Solution Explorer, right-click the **tutorial** project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="663d9-174">Sélectionnez **Fichier Python vide** et nommez le fichier **forms.py**.</span><span class="sxs-lookup"><span data-stu-id="663d9-174">Select **Empty Python File** and name the file **forms.py**.</span></span>  
2. <span data-ttu-id="663d9-175">Ajoutez le code suivant au fichier forms.py, puis enregistrez le fichier.</span><span class="sxs-lookup"><span data-stu-id="663d9-175">Add the following code to the forms.py file, and then save the file.</span></span>

```python
from flask.ext.wtf import Form
from wtforms import RadioField

class VoteForm(Form):
    deploy_preference  = RadioField('Deployment Preference', choices=[
        ('Web Site', 'Web Site'),
        ('Cloud Service', 'Cloud Service'),
        ('Virtual Machine', 'Virtual Machine')], default='Web Site')
```


### <a name="add-the-required-imports-to-viewspy"></a><span data-ttu-id="663d9-176">Ajoutez les instructions import requises à views.py</span><span class="sxs-lookup"><span data-stu-id="663d9-176">Add the required imports to views.py</span></span>
1. <span data-ttu-id="663d9-177">Dans l’Explorateur de solutions, développez le dossier **tutorial** et ouvrez le fichier **views.py**.</span><span class="sxs-lookup"><span data-stu-id="663d9-177">In Solution Explorer, expand the **tutorial** folder, and open the **views.py** file.</span></span> 
2. <span data-ttu-id="663d9-178">Ajoutez les instructions d’importation suivantes au début du fichier **views.py**, puis enregistrez le fichier.</span><span class="sxs-lookup"><span data-stu-id="663d9-178">Add the following import statements to the top of the **views.py** file, then save the file.</span></span> <span data-ttu-id="663d9-179">Elles importent les packages Flask et le kit de développement logiciel (SDK) Python de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="663d9-179">These import Cosmos DB's PythonSDK and the Flask packages.</span></span>
   
    ```python
    from forms import VoteForm
    import config
    import pydocumentdb.document_client as document_client
    ```

### <a name="create-database-collection-and-document"></a><span data-ttu-id="663d9-180">Création de base de données, de collection et de document</span><span class="sxs-lookup"><span data-stu-id="663d9-180">Create database, collection, and document</span></span>
* <span data-ttu-id="663d9-181">Toujours dans **views.py**, ajoutez le code suivant à la fin du fichier.</span><span class="sxs-lookup"><span data-stu-id="663d9-181">Still in **views.py**, add the following code to the end of the file.</span></span> <span data-ttu-id="663d9-182">Cela permet de créer la base de données utilisée par le formulaire.</span><span class="sxs-lookup"><span data-stu-id="663d9-182">This takes care of creating the database used by the form.</span></span> <span data-ttu-id="663d9-183">Ne supprimez pas le code existant dans **views.py**.</span><span class="sxs-lookup"><span data-stu-id="663d9-183">Do not delete any of the existing code in **views.py**.</span></span> <span data-ttu-id="663d9-184">Il vous suffit d'ajouter le code à la fin.</span><span class="sxs-lookup"><span data-stu-id="663d9-184">Simply append this to the end.</span></span>

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


### <a name="read-database-collection-document-and-submit-form"></a><span data-ttu-id="663d9-185">Lecture de la base de données, de la collection et du document, et envoi du formulaire</span><span class="sxs-lookup"><span data-stu-id="663d9-185">Read database, collection, document, and submit form</span></span>
* <span data-ttu-id="663d9-186">Toujours dans **views.py**, ajoutez le code suivant à la fin du fichier.</span><span class="sxs-lookup"><span data-stu-id="663d9-186">Still in **views.py**, add the following code to the end of the file.</span></span> <span data-ttu-id="663d9-187">Ce code configure le formulaire et lit la base de données, la collection et le document.</span><span class="sxs-lookup"><span data-stu-id="663d9-187">This takes care of setting up the form, reading the database, collection, and document.</span></span> <span data-ttu-id="663d9-188">Ne supprimez pas le code existant dans **views.py**.</span><span class="sxs-lookup"><span data-stu-id="663d9-188">Do not delete any of the existing code in **views.py**.</span></span> <span data-ttu-id="663d9-189">Il vous suffit d'ajouter le code à la fin.</span><span class="sxs-lookup"><span data-stu-id="663d9-189">Simply append this to the end.</span></span>

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


### <a name="create-the-html-files"></a><span data-ttu-id="663d9-190">Création des fichiers HTML</span><span class="sxs-lookup"><span data-stu-id="663d9-190">Create the HTML files</span></span>
1. <span data-ttu-id="663d9-191">Dans l’Explorateur de solutions, dans le dossier **tutorial**, cliquez avec le bouton droit sur le dossier **templates**, cliquez sur **Ajouter**, puis sur **Nouvel élément**.</span><span class="sxs-lookup"><span data-stu-id="663d9-191">In Solution Explorer, in the **tutorial** folder, right click the **templates** folder, click **Add**, and then click **New Item**.</span></span> 
2. <span data-ttu-id="663d9-192">Sélectionnez **Page HTML** puis, dans la zone Nom, tapez **create.html**.</span><span class="sxs-lookup"><span data-stu-id="663d9-192">Select **HTML Page**, and then in the name box type **create.html**.</span></span> 
3. <span data-ttu-id="663d9-193">Répétez les étapes 1 et 2 pour créer deux autres fichiers HTML : results.html et vote.html.</span><span class="sxs-lookup"><span data-stu-id="663d9-193">Repeat steps 1 and 2 to create two additional HTML files: results.html and vote.html.</span></span>
4. <span data-ttu-id="663d9-194">Ajoutez le code suivant à **create.html** in the `<body>` .</span><span class="sxs-lookup"><span data-stu-id="663d9-194">Add the following code to **create.html** in the `<body>` element.</span></span> <span data-ttu-id="663d9-195">Il affiche un message indiquant la création d’une base de données, d’une collection et d’un document.</span><span class="sxs-lookup"><span data-stu-id="663d9-195">It displays a message stating that we created a new database, collection, and document.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>{{ title }}.</h2>
    <h3>{{ message }}</h3>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```
5. <span data-ttu-id="663d9-196">Ajoutez le code suivant à **results.html** dans l’élément `<body`.</span><span class="sxs-lookup"><span data-stu-id="663d9-196">Add the following code to **results.html** in the `<body`> element.</span></span> <span data-ttu-id="663d9-197">Il affiche les résultats du sondage.</span><span class="sxs-lookup"><span data-stu-id="663d9-197">It displays the results of the poll.</span></span>
   
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
6. <span data-ttu-id="663d9-198">Ajoutez le code suivant à **vote.html** dans l’élément `<body`.</span><span class="sxs-lookup"><span data-stu-id="663d9-198">Add the following code to **vote.html** in the `<body`> element.</span></span> <span data-ttu-id="663d9-199">Il affiche le sondage et accepte les votes.</span><span class="sxs-lookup"><span data-stu-id="663d9-199">It displays the poll and accepts the votes.</span></span> <span data-ttu-id="663d9-200">Lors de l'enregistrement des votes, le contrôle est transmis à views.py où nous allons identifier le vote associé et ajouter le document correspondant.</span><span class="sxs-lookup"><span data-stu-id="663d9-200">On registering the votes, the control is passed over to views.py where we will recognize the vote cast and append the document accordingly.</span></span>
   
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
7. <span data-ttu-id="663d9-201">Dans le dossier **templates**, remplacez le contenu **d’index.html** par le code suivant.</span><span class="sxs-lookup"><span data-stu-id="663d9-201">In the **templates** folder, replace the contents of **index.html** with the following.</span></span> <span data-ttu-id="663d9-202">Ce code définit une page d'accueil pour votre application</span><span class="sxs-lookup"><span data-stu-id="663d9-202">This serves as the landing page for your application.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Python + Azure Cosmos DB Voting Application.</h2>
    <h3>This is a sample Cosmos DB voting application using PyDocumentDB</h3>
    <p><a href="{{ url_for('create') }}" class="btn btn-primary btn-large">Create/Clear the Voting Database &raquo;</a></p>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```

### <a name="add-a-configuration-file-and-change-the-initpy"></a><span data-ttu-id="663d9-203">Ajout d’un fichier de configuration et modification d’\_\_init\_\_.py</span><span class="sxs-lookup"><span data-stu-id="663d9-203">Add a configuration file and change the \_\_init\_\_.py</span></span>
1. <span data-ttu-id="663d9-204">Dans l’Explorateur de solutions, cliquez sur le projet **tutorial**, cliquez sur **Ajouter**, cliquez sur **Nouvel élément**, sélectionnez **Fichier Python vide**, puis nommez le fichier **config.py**.</span><span class="sxs-lookup"><span data-stu-id="663d9-204">In Solution Explorer, right-click the **tutorial** project, click **Add**, click **New Item**, select **Empty Python File**, and then name the file **config.py**.</span></span> <span data-ttu-id="663d9-205">Ce fichier de configuration est requis par les formulaires dans Flask.</span><span class="sxs-lookup"><span data-stu-id="663d9-205">This config file is required by forms in Flask.</span></span> <span data-ttu-id="663d9-206">Vous pouvez l'utiliser pour fournir une clé secrète.</span><span class="sxs-lookup"><span data-stu-id="663d9-206">You can use it to provide a secret key as well.</span></span> <span data-ttu-id="663d9-207">Cette clé n'est cependant pas nécessaire dans le cadre de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="663d9-207">This key is not needed for this tutorial though.</span></span>
2. <span data-ttu-id="663d9-208">Ajoutez le code suivant à config.py. Vous devrez modifier les valeurs de **DOCUMENTDB\_HOST** et de **DOCUMENTDB\_KEY** à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="663d9-208">Add the following code to config.py, you'll need to alter the values of **DOCUMENTDB\_HOST** and **DOCUMENTDB\_KEY** in the next step.</span></span>
   
    ```python
    CSRF_ENABLED = True
    SECRET_KEY = 'you-will-never-guess'
   
    DOCUMENTDB_HOST = 'https://YOUR_DOCUMENTDB_NAME.documents.azure.com:443/'
    DOCUMENTDB_KEY = 'YOUR_SECRET_KEY_ENDING_IN_=='
   
    DOCUMENTDB_DATABASE = 'voting database'
    DOCUMENTDB_COLLECTION = 'voting collection'
    DOCUMENTDB_DOCUMENT = 'voting document'
    ```
3. <span data-ttu-id="663d9-209">Dans le [portail Azure](https://portal.azure.com/), accédez au panneau **Clés** en cliquant sur **Parcourir**, **Azure Cosmos DB Accounts** (Comptes Azure Cosmos DB), double-cliquez sur le nom du compte à utiliser, puis cliquez sur le bouton **Clés** dans la zone **Éléments principaux**.</span><span class="sxs-lookup"><span data-stu-id="663d9-209">In the [Azure portal](https://portal.azure.com/), navigate to the **Keys** blade by clicking **Browse**, **Azure Cosmos DB Accounts**, double-click the name of the account to use, and then click the **Keys** button in the **Essentials** area.</span></span> <span data-ttu-id="663d9-210">Dans le panneau **Clés**, copiez la valeur de **l’URI** et collez-la dans le fichier **config.py** comme valeur de la propriété **DOCUMENTDB\_HOST**.</span><span class="sxs-lookup"><span data-stu-id="663d9-210">In the **Keys** blade, copy the **URI** value and paste it into the **config.py** file, as the value for the **DOCUMENTDB\_HOST** property.</span></span> 
4. <span data-ttu-id="663d9-211">De retour dans le portail Azure, dans le panneau **Clés**, copiez la valeur de la **Clé principale** ou de la **Clé secondaire**, et collez-la dans le fichier **config.py** comme valeur de la propriété **DOCUMENTDB\_KEY**.</span><span class="sxs-lookup"><span data-stu-id="663d9-211">Back in the Azure portal, in the **Keys** blade, copy the value of the **Primary Key** or the **Secondary Key**, and paste it into the **config.py** file, as the value for the **DOCUMENTDB\_KEY** property.</span></span>
5. <span data-ttu-id="663d9-212">Dans le fichier **\_\_init\_\_.py**, ajoutez la ligne suivante.</span><span class="sxs-lookup"><span data-stu-id="663d9-212">In the **\_\_init\_\_.py** file, add the following line.</span></span> 
   
        app.config.from_object('config')
   
    <span data-ttu-id="663d9-213">Le contenu du fichier doit donc être :</span><span class="sxs-lookup"><span data-stu-id="663d9-213">So that the content of the file is:</span></span>
   
    ```python
    from flask import Flask
    app = Flask(__name__)
    app.config.from_object('config')
    import tutorial.views
    ```
6. <span data-ttu-id="663d9-214">Après avoir ajouté tous les fichiers, l’Explorateur de solutions doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="663d9-214">After adding all the files, Solution Explorer should look like this:</span></span>
   
    ![Capture d’écran de la fenêtre Explorateur de solutions de Visual Studio](./media/documentdb-python-application/cosmos-db-python-solution-explorer.png)

## <a name="step-4-run-your-web-application-locally"></a><span data-ttu-id="663d9-216">Étape 4 : Exécution locale de votre application web</span><span class="sxs-lookup"><span data-stu-id="663d9-216">Step 4: Run your web application locally</span></span>
1. <span data-ttu-id="663d9-217">Appuyez sur **Ctrl**+**Maj**+**B** pour générer la solution.</span><span class="sxs-lookup"><span data-stu-id="663d9-217">Build the solution by pressing **Ctrl**+**Shift**+**B**.</span></span>
2. <span data-ttu-id="663d9-218">Une fois la génération terminée, démarrez le site Web en appuyant sur **F5**.</span><span class="sxs-lookup"><span data-stu-id="663d9-218">Once the build succeeds, start the website by pressing **F5**.</span></span> <span data-ttu-id="663d9-219">Vous devez voir ceci sur votre écran.</span><span class="sxs-lookup"><span data-stu-id="663d9-219">You should see the following on your screen.</span></span>
   
    ![Capture d’écran de l’application de vote Python + Azure Cosmos DB affichée dans un navigateur web](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)
3. <span data-ttu-id="663d9-221">Cliquez sur **Create/Clear the Voting Database** pour générer la base de données.</span><span class="sxs-lookup"><span data-stu-id="663d9-221">Click **Create/Clear the Voting Database** to generate the database.</span></span>
   
    ![Capture d’écran de l’écran de création de page de l’application web – Détails du développement](./media/documentdb-python-application/cosmos-db-python-run-create-page.png)
4. <span data-ttu-id="663d9-223">Cliquez ensuite sur **Vote** et sélectionnez votre option.</span><span class="sxs-lookup"><span data-stu-id="663d9-223">Then, click **Vote** and select your option.</span></span>
   
    ![Capture d’écran de l’application web avec une question de vote posée](./media/documentdb-python-application/cosmos-db-vote.png)
5. <span data-ttu-id="663d9-225">Chaque vote associé augmente le compteur adéquat.</span><span class="sxs-lookup"><span data-stu-id="663d9-225">For every vote you cast, it increments the appropriate counter.</span></span>
   
    ![Capture d’écran des résultats de la page de vote affichée](./media/documentdb-python-application/cosmos-db-voting-results.png)
6. <span data-ttu-id="663d9-227">Arrêtez le débogage du projet en appuyant sur Maj+F5.</span><span class="sxs-lookup"><span data-stu-id="663d9-227">Stop debugging the project by pressing Shift+F5.</span></span>

## <a name="step-5-deploy-the-web-application-to-azure"></a><span data-ttu-id="663d9-228">Étape 5 : Déploiement de l’application web sur Azure</span><span class="sxs-lookup"><span data-stu-id="663d9-228">Step 5: Deploy the web application to Azure</span></span>
<span data-ttu-id="663d9-229">Maintenant que l’application fonctionne correctement avec Cosmos DB, nous allons la déployer sur Azure.</span><span class="sxs-lookup"><span data-stu-id="663d9-229">Now that you have the complete application working correctly against Cosmos DB, we're going to deploy this to Azure.</span></span>

1. <span data-ttu-id="663d9-230">Cliquez avec le bouton droit sur le projet dans l’Explorateur de solutions (assurez-vous de ne pas encore l’exécuter localement), puis sélectionnez **Publier**.</span><span class="sxs-lookup"><span data-stu-id="663d9-230">Right-click the project in Solution Explorer (make sure you're not still running it locally) and select **Publish**.</span></span>  
   
     ![Capture d’écran du didacticiel sélectionné dans l’Explorateur de solutions, avec l’option Publier mise en surbrillance](./media/documentdb-python-application/image20.png)
2. <span data-ttu-id="663d9-232">Dans la boîte de dialogue **Publier**, sélectionnez **Microsoft Azure App Service**, choisissez **Création**, puis cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="663d9-232">In the **Publish** dialog box, select **Microsoft Azure App Service**, select **Create New**, and then click **Publish**.</span></span>
   
    ![Capture d’écran de la fenêtre Publier le site web, avec Microsoft Azure App Service en surbrillance](./media/documentdb-python-application/cosmos-db-python-publish.png)
3. <span data-ttu-id="663d9-234">Dans la boîte de dialogue **Créer App Service**, saisissez le nom de l’application web, ainsi que **l’abonnement**, le **groupe de ressources** et le **plan App Service**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="663d9-234">In the **Create App Service** dialog box, enter the name for your web app along with your **Subscription**, **Resource Group**, and **App Service Plan**, then click **Create**.</span></span>
   
    ![Capture d'écran de la fenêtre Microsoft Azure Web Apps](./media/documentdb-python-application/cosmos-db-python-create-app-service.png)
4. <span data-ttu-id="663d9-236">Dans quelques secondes, Visual Studio achèvera la publication de votre service d’application et lancera un navigateur, dans lequel vous pourrez voir votre réalisation exécutée dans Azure.</span><span class="sxs-lookup"><span data-stu-id="663d9-236">In a few seconds, Visual Studio will finish publishing your app service and launch a browser where you can see your handiwork running in Azure!</span></span>

    ![Capture d'écran de la fenêtre Microsoft Azure Web Apps](./media/documentdb-python-application/cosmos-db-python-appservice-created.png)

## <a name="troubleshooting"></a><span data-ttu-id="663d9-238">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="663d9-238">Troubleshooting</span></span>
<span data-ttu-id="663d9-239">S’il s’agit de la première application Python que vous avez exécutée sur votre ordinateur, assurez-vous que les dossiers suivants (ou les emplacements d’installation équivalents) sont inclus dans votre variable PATH :</span><span class="sxs-lookup"><span data-stu-id="663d9-239">If this is the first Python app you've run on your computer, ensure that the following folders (or the equivalent installation locations) are included in your PATH variable:</span></span>

    C:\Python27\site-packages;C:\Python27\;C:\Python27\Scripts;

<span data-ttu-id="663d9-240">Si vous recevez une erreur sur votre page de vote et que vous avez nommé votre projet autrement que **tutorial**, assurez-vous que **\_\_init\_\_.py** fait référence au nom de projet correct dans la ligne : `import tutorial.view`.</span><span class="sxs-lookup"><span data-stu-id="663d9-240">If you receive an error on your vote page, and you named your project something other than **tutorial**, make sure that **\_\_init\_\_.py** references the correct project name in the line: `import tutorial.view`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="663d9-241">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="663d9-241">Next steps</span></span>
<span data-ttu-id="663d9-242">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="663d9-242">Congratulations!</span></span> <span data-ttu-id="663d9-243">Vous venez de créer votre première application web Python avec Cosmos DB, et de la publier sur Azure.</span><span class="sxs-lookup"><span data-stu-id="663d9-243">You have just completed your first Python web application using Cosmos DB and published it to Azure.</span></span>

<span data-ttu-id="663d9-244">Nous mettons à jour et améliorons cette rubrique fréquemment en fonction de vos commentaires.</span><span class="sxs-lookup"><span data-stu-id="663d9-244">We update and improve this topic frequently based on your feedback.</span></span>  <span data-ttu-id="663d9-245">Une fois le didacticiel terminé, utilisez les boutons de vote en haut et en bas de cette page et veillez à indiquer vos commentaires sur les améliorations que nous pourrions apporter.</span><span class="sxs-lookup"><span data-stu-id="663d9-245">Once you've completed the tutorial, please using the voting buttons at the top and bottom of this page, and be sure to include your feedback on what improvements you want to see made.</span></span> <span data-ttu-id="663d9-246">Si vous souhaitez que nous vous contactions directement, n’hésitez pas à inclure votre adresse de messagerie dans vos commentaires.</span><span class="sxs-lookup"><span data-stu-id="663d9-246">If you'd like us to contact you directly, feel free to include your email address in your comments.</span></span>

<span data-ttu-id="663d9-247">Pour ajouter des fonctionnalités supplémentaires à votre application web, passez en revue les API disponibles dans le [Kit de développement logiciel (SDK) Azure Cosmos DB](documentdb-sdk-python.md).</span><span class="sxs-lookup"><span data-stu-id="663d9-247">To add additional functionality to your web application, review the APIs available in the [Azure Cosmos DB Python SDK](documentdb-sdk-python.md).</span></span>

<span data-ttu-id="663d9-248">Pour plus d’informations sur Azure, Visual Studio et Python, consultez le [Centre de développement Python](https://azure.microsoft.com/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="663d9-248">For more information about Azure, Visual Studio, and Python, see the [Python Developer Center](https://azure.microsoft.com/develop/python/).</span></span> 

<span data-ttu-id="663d9-249">Pour d’autres didacticiels Python Flask, consultez [The Flask Mega-Tutorial, Part I: Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world).</span><span class="sxs-lookup"><span data-stu-id="663d9-249">For additional Python Flask tutorials, see [The Flask Mega-Tutorial, Part I: Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world).</span></span> 

[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[2]: https://www.python.org/downloads/windows/
[3]: https://www.microsoft.com/download/details.aspx?id=44266
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Azure portal]: http://portal.azure.com
