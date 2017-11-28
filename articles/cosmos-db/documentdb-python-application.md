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
# <a name="build-a-python-flask-web-application-using-azure-cosmos-db"></a><span data-ttu-id="ef7a9-105">Créer une application web Python Flask à l’aide d’Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ef7a9-105">Build a Python Flask web application using Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ef7a9-106">.NET</span><span class="sxs-lookup"><span data-stu-id="ef7a9-106">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="ef7a9-107">Node.JS</span><span class="sxs-lookup"><span data-stu-id="ef7a9-107">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="ef7a9-108">Java</span><span class="sxs-lookup"><span data-stu-id="ef7a9-108">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="ef7a9-109">Python</span><span class="sxs-lookup"><span data-stu-id="ef7a9-109">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="ef7a9-110">Ce didacticiel vous montre comment les données de toostore et d’accès de base de données Azure Cosmos à partir d’une Python toouse web application hébergée sur Azure et suppose que vous avez une connaissance préalable à l’aide de Python et des sites Web Azure.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-110">This tutorial shows you how toouse Azure Cosmos DB toostore and access data from a Python web application hosted on Azure and presumes that you have some prior experience using Python and Azure websites.</span></span>

<span data-ttu-id="ef7a9-111">Ce didacticiel de base de données traite les points suivants :</span><span class="sxs-lookup"><span data-stu-id="ef7a9-111">This database tutorial covers:</span></span>

1. <span data-ttu-id="ef7a9-112">Création et approvisionnement d’un compte Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-112">Creating and provisioning a Cosmos DB account.</span></span>
2. <span data-ttu-id="ef7a9-113">Création d’une application Python Flask.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-113">Creating a Python Flask application.</span></span>
3. <span data-ttu-id="ef7a9-114">Connexion tooand à l’aide de la base de données Cosmos à partir de votre application web.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-114">Connecting tooand using Cosmos DB from your web application.</span></span>
4. <span data-ttu-id="ef7a9-115">Déploiement hello web application tooAzure.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-115">Deploying hello web application tooAzure.</span></span>

<span data-ttu-id="ef7a9-116">En suivant ce didacticiel, vous allez générer une application de vote simple qui vous permet de toovote pour une interrogation.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-116">By following this tutorial, you will build a simple voting application that allows you toovote for a poll.</span></span>

![Capture d’écran de l’application de vote hello créée par ce didacticiel de base de données](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)

## <a name="database-tutorial-prerequisites"></a><span data-ttu-id="ef7a9-118">Conditions préalables à l’exécution de ce didacticiel de base de données</span><span class="sxs-lookup"><span data-stu-id="ef7a9-118">Database tutorial prerequisites</span></span>
<span data-ttu-id="ef7a9-119">Avant de suivre les instructions de hello dans cet article, vous devez vous assurer d’avoir installé des éléments suivants hello :</span><span class="sxs-lookup"><span data-stu-id="ef7a9-119">Before following hello instructions in this article, you should ensure that you have hello following installed:</span></span>

* <span data-ttu-id="ef7a9-120">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-120">An active Azure account.</span></span> <span data-ttu-id="ef7a9-121">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="ef7a9-122">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ef7a9-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
 
    <span data-ttu-id="ef7a9-123">OU</span><span class="sxs-lookup"><span data-stu-id="ef7a9-123">OR</span></span> 

    <span data-ttu-id="ef7a9-124">Une installation locale de hello [Azure Cosmos DB émulateur](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="ef7a9-124">A local installation of hello [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="ef7a9-125">[Microsoft Visual Studio Community 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="ef7a9-125">[Microsoft Visual Studio Community 2017](http://www.visualstudio.com/).</span></span>  
* <span data-ttu-id="ef7a9-126">[Python Tools pour Visual Studio](https://github.com/Microsoft/PTVS/).</span><span class="sxs-lookup"><span data-stu-id="ef7a9-126">[Python Tools for Visual Studio](https://github.com/Microsoft/PTVS/).</span></span>  
* <span data-ttu-id="ef7a9-127">[Kit de développement logiciel (SDK) Microsoft Azure pour Python 2.7](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="ef7a9-127">[Microsoft Azure SDK for Python 2.7](https://azure.microsoft.com/downloads/).</span></span> 
* <span data-ttu-id="ef7a9-128">[Python 2.7.13](https://www.python.org/downloads/windows/).</span><span class="sxs-lookup"><span data-stu-id="ef7a9-128">[Python 2.7.13](https://www.python.org/downloads/windows/).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="ef7a9-129">Si vous installez Python 2.7 pour hello première fois, vérifiez que l’écran hello personnaliser Python 2.7.13, vous sélectionnez **ajouter python.exe tooPath**.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-129">If you are installing Python 2.7 for hello first time, ensure that in hello Customize Python 2.7.13 screen, you select **Add python.exe tooPath**.</span></span>
> 
> ![Capture d’écran de l’écran de personnaliser les Python 2.7.11 hello, dans lequel vous devez tooselect ajouter python.exe tooPath](./media/documentdb-python-application/cosmos-db-python-install.png)
> 
> 

* <span data-ttu-id="ef7a9-131">[Compilateur Microsoft Visual C++ pour Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266).</span><span class="sxs-lookup"><span data-stu-id="ef7a9-131">[Microsoft Visual C++ Compiler for Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-database-account"></a><span data-ttu-id="ef7a9-132">Étape 1 : création d’un compte de base de données Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ef7a9-132">Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="ef7a9-133">Commençons par créer un compte Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-133">Let's start by creating an Cosmos DB account.</span></span> <span data-ttu-id="ef7a9-134">Si vous déjà disposez d’un compte ou si vous utilisez hello Azure Cosmos DB émulateur pour ce didacticiel, vous pouvez ignorer trop[étape 2 : créer une application web Python ballon](#step-2-create-a-new-python-flask-web-application).</span><span class="sxs-lookup"><span data-stu-id="ef7a9-134">If you already have an account or if you are using hello Azure Cosmos DB Emulator for this tutorial, you can skip too[Step 2: Create a new Python Flask web application](#step-2-create-a-new-python-flask-web-application).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<br/>
<span data-ttu-id="ef7a9-135">Nous étudierons maintenant comment toocreate une application web à partir de hello Python ballon au sol.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-135">We will now walk through how toocreate a new Python Flask web application from hello ground up.</span></span>

## <a name="step-2-create-a-new-python-flask-web-application"></a><span data-ttu-id="ef7a9-136">Étape 2 : Création d’une application web Python Flask</span><span class="sxs-lookup"><span data-stu-id="ef7a9-136">Step 2: Create a new Python Flask web application</span></span>
1. <span data-ttu-id="ef7a9-137">Dans Visual Studio, sur hello **fichier** menu, pointez trop**nouveau**, puis cliquez sur **projet**.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-137">In Visual Studio, on hello **File** menu, point too**New**, and then click **Project**.</span></span>
   
    <span data-ttu-id="ef7a9-138">Hello **nouveau projet** boîte de dialogue s’affiche.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-138">hello **New Project** dialog box appears.</span></span>
2. <span data-ttu-id="ef7a9-139">Dans le volet gauche de hello, développez **modèles** , puis **Python**, puis cliquez sur **Web**.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-139">In hello left pane, expand **Templates** and then **Python**, and then click **Web**.</span></span> 
3. <span data-ttu-id="ef7a9-140">Sélectionnez **ballon Web projet** dans le volet central de hello, puis dans hello **nom** zone **didacticiel**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-140">Select **Flask  Web Project** in hello center pane, then in hello **Name** box type **tutorial**, and then click **OK**.</span></span> <span data-ttu-id="ef7a9-141">Souvenez-vous que les noms de package Python doivent être en minuscules comme décrit dans hello [Guide de Style pour le Code Python](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).</span><span class="sxs-lookup"><span data-stu-id="ef7a9-141">Remember that Python package names should be all lowercase, as described in hello [Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).</span></span>
   
    <span data-ttu-id="ef7a9-142">Pour ces tooPython nouveau ballon, il est une infrastructure de développement d’application web qui vous permet de générer des applications web de Python plus rapidement.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-142">For those new tooPython Flask, it is a web application development framework that helps you build web applications in Python faster.</span></span>
   
    ![Capture d’écran de la fenêtre de nouveau projet hello dans Visual Studio avec Python mis en surbrillance sur hello gauche, Python ballon Web projet dans hello intermédiaire et de didacticiel de nom hello dans la zone de nom hello](./media/documentdb-python-application/image9.png)
4. <span data-ttu-id="ef7a9-144">Bonjour **outils Python pour Visual Studio** fenêtre, cliquez sur **installer dans un environnement virtuel**.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-144">In hello **Python Tools for Visual Studio** window, click **Install into a virtual environment**.</span></span> 
   
    ![Capture d’écran du didacticiel de base de données hello - outils Python pour la fenêtre de Visual Studio](./media/documentdb-python-application/python-install-virtual-environment.png)
5. <span data-ttu-id="ef7a9-146">Bonjour **ajouter l’environnement virtuel** fenêtre, vous pouvez accepter les valeurs par défaut hello et utiliser Python 2.7 comme environnement de base de hello, car PyDocumentDB ne prend pas en charge les Python 3.x, puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-146">In hello **Add Virtual Environment** window, you can accept hello defaults and use Python 2.7 as hello base environment because PyDocumentDB does not currently support Python 3.x, and then click **Create**.</span></span> <span data-ttu-id="ef7a9-147">Cela configure l’environnement virtuel de Python hello requis pour votre projet.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-147">This sets up hello required Python virtual environment for your project.</span></span>
   
    ![Capture d’écran du didacticiel de base de données hello - outils Python pour la fenêtre de Visual Studio](./media/documentdb-python-application/image10_A.png)
   
    <span data-ttu-id="ef7a9-149">affiche de la fenêtre de sortie Hello `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` lorsque des environnement de hello est correctement installé.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-149">hello output window displays `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` when hello environment is successfully installed.</span></span>

## <a name="step-3-modify-hello-python-flask-web-application"></a><span data-ttu-id="ef7a9-150">Étape 3 : Modifier l’application web de Python ballon hello</span><span class="sxs-lookup"><span data-stu-id="ef7a9-150">Step 3: Modify hello Python Flask web application</span></span>
### <a name="add-hello-python-flask-packages-tooyour-project"></a><span data-ttu-id="ef7a9-151">Ajouter un projet de tooyour packages hello ballon de Python</span><span class="sxs-lookup"><span data-stu-id="ef7a9-151">Add hello Python Flask packages tooyour project</span></span>
<span data-ttu-id="ef7a9-152">Une fois que votre projet est configuré, vous devez tooadd hello requis ballon packages tooyour projet, y compris pydocumentdb, package de Python hello pour DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-152">After your project is set up, you'll need tooadd hello required Flask packages tooyour project, including pydocumentdb, hello Python package for DocumentDB.</span></span>

1. <span data-ttu-id="ef7a9-153">Dans l’Explorateur de solutions, ouvrez le fichier de hello nommé **requirements.txt** et remplacez le contenu de hello par qui suit hello :</span><span class="sxs-lookup"><span data-stu-id="ef7a9-153">In Solution Explorer, open hello file named **requirements.txt** and replace hello contents with hello following:</span></span>
   
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
2. <span data-ttu-id="ef7a9-154">Enregistrer hello **requirements.txt** fichier.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-154">Save hello **requirements.txt** file.</span></span> 
3. <span data-ttu-id="ef7a9-155">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur **env**, puis cliquez sur **Install from requirements.txt** (Installer depuis requirements.txt).</span><span class="sxs-lookup"><span data-stu-id="ef7a9-155">In Solution Explorer, right-click **env** and click **Install from requirements.txt**.</span></span>
   
    ![Capture d’écran montrant env (Python 2.7) sélectionné avec l’installation à partir de requirements.txt mis en surbrillance dans la liste de hello](./media/documentdb-python-application/cosmos-db-python-install-from-requirements.png)
   
    <span data-ttu-id="ef7a9-157">Après l’installation, la fenêtre de sortie de hello affiche suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="ef7a9-157">After successful installation, hello output window displays hello following:</span></span>
   
        Successfully installed Babel-2.3.2 Tempita-0.5.2 WTForms-2.1 Whoosh-2.7.4 blinker-1.4 decorator-4.0.9 flask-0.9 flask-babel-0.8 flask-mail-0.7.6 flask-sqlalchemy-0.16 flask-whooshalchemy-0.55a0 flask-wtf-0.8.4 flup-1.0.2 pydocumentdb-1.6.1 pytz-2013b0 speaklater-1.3 sqlalchemy-0.7.9 sqlalchemy-migrate-0.7.2
   
   > [!NOTE]
   > <span data-ttu-id="ef7a9-158">Dans de rares cas, vous pouvez voir un échec dans la fenêtre de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-158">In rare cases, you might see a failure in hello output window.</span></span> <span data-ttu-id="ef7a9-159">Si cela se produit, vérifiez si des erreurs de hello sont toocleanup connexe.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-159">If this happens, check if hello error is related toocleanup.</span></span> <span data-ttu-id="ef7a9-160">Parfois, le nettoyage de hello échoue, mais hello installation toujours sera réussie (défiler vers le haut dans tooverify de fenêtre de sortie hello cela).</span><span class="sxs-lookup"><span data-stu-id="ef7a9-160">Sometimes hello cleanup fails, but hello installation will still be successful (scroll up in hello output window tooverify this).</span></span> <span data-ttu-id="ef7a9-161">Vous pouvez vérifier votre installation en [environnement virtuel de vérification hello](#verify-the-virtual-environment).</span><span class="sxs-lookup"><span data-stu-id="ef7a9-161">You can check your installation by [Verifying hello virtual environment](#verify-the-virtual-environment).</span></span> <span data-ttu-id="ef7a9-162">Si l’échec de l’installation de hello mais hello vérification s’effectue correctement, il est toocontinue OK.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-162">If hello installation failed but hello verification is successful, it's OK toocontinue.</span></span>
   > 
   > 

### <a name="verify-hello-virtual-environment"></a><span data-ttu-id="ef7a9-163">Vérifier l’environnement virtuel de hello</span><span class="sxs-lookup"><span data-stu-id="ef7a9-163">Verify hello virtual environment</span></span>
<span data-ttu-id="ef7a9-164">Vérifiez que l'installation est réussie.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-164">Let's make sure that everything is installed correctly.</span></span>

1. <span data-ttu-id="ef7a9-165">Générez la solution de hello en appuyant sur **Ctrl**+**MAJ**+**B**.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-165">Build hello solution by pressing **Ctrl**+**Shift**+**B**.</span></span>
2. <span data-ttu-id="ef7a9-166">Une fois hello génération terminée, démarrez le site Web de hello en appuyant sur **F5**.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-166">Once hello build succeeds, start hello website by pressing **F5**.</span></span> <span data-ttu-id="ef7a9-167">Cela lance le serveur de développement ballon hello et lance votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-167">This launches hello Flask development server and starts your web browser.</span></span> <span data-ttu-id="ef7a9-168">Vous devez voir hello après page.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-168">You should see hello following page.</span></span>
   
    ![Hello Python ballon projet web vide développement affiché dans un navigateur](./media/documentdb-python-application/image12.png)
3. <span data-ttu-id="ef7a9-170">Arrêter le débogage du site Web hello en appuyant sur **MAJ**+**F5** dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-170">Stop debugging hello website by pressing **Shift**+**F5** in Visual Studio.</span></span>

### <a name="create-database-collection-and-document-definitions"></a><span data-ttu-id="ef7a9-171">Création des définitions pour la base de données, la collection et le document</span><span class="sxs-lookup"><span data-stu-id="ef7a9-171">Create database, collection, and document definitions</span></span>
<span data-ttu-id="ef7a9-172">Nous allons maintenant créer votre application de vote en ajoutant de nouveaux fichiers et en mettant à jour d’autres fichiers.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-172">Now let's create your voting application by adding new files and updating others.</span></span>

1. <span data-ttu-id="ef7a9-173">Dans l’Explorateur de solutions, cliquez sur hello **didacticiel** de projet, cliquez sur **ajouter**, puis cliquez sur **un nouvel élément**.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-173">In Solution Explorer, right-click hello **tutorial** project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="ef7a9-174">Sélectionnez **fichier Python vide** et le nom de fichier hello **forms.py**.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-174">Select **Empty Python File** and name hello file **forms.py**.</span></span>  
2. <span data-ttu-id="ef7a9-175">Ajouter hello code toohello forms.py fichier suivant, puis enregistrez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-175">Add hello following code toohello forms.py file, and then save hello file.</span></span>

```python
from flask.ext.wtf import Form
from wtforms import RadioField

class VoteForm(Form):
    deploy_preference  = RadioField('Deployment Preference', choices=[
        ('Web Site', 'Web Site'),
        ('Cloud Service', 'Cloud Service'),
        ('Virtual Machine', 'Virtual Machine')], default='Web Site')
```


### <a name="add-hello-required-imports-tooviewspy"></a><span data-ttu-id="ef7a9-176">Ajouter tooviews.py d’importations hello requis</span><span class="sxs-lookup"><span data-stu-id="ef7a9-176">Add hello required imports tooviews.py</span></span>
1. <span data-ttu-id="ef7a9-177">Dans l’Explorateur de solutions, développez hello **didacticiel** dossier et ouvrez hello **views.py** fichier.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-177">In Solution Explorer, expand hello **tutorial** folder, and open hello **views.py** file.</span></span> 
2. <span data-ttu-id="ef7a9-178">Ajouter hello après importation instructions toohello en haut de hello **views.py** de fichier, puis enregistrez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-178">Add hello following import statements toohello top of hello **views.py** file, then save hello file.</span></span> <span data-ttu-id="ef7a9-179">Ces importer Cosmos DB PythonSDK et hello les packages flacon.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-179">These import Cosmos DB's PythonSDK and hello Flask packages.</span></span>
   
    ```python
    from forms import VoteForm
    import config
    import pydocumentdb.document_client as document_client
    ```

### <a name="create-database-collection-and-document"></a><span data-ttu-id="ef7a9-180">Création de base de données, de collection et de document</span><span class="sxs-lookup"><span data-stu-id="ef7a9-180">Create database, collection, and document</span></span>
* <span data-ttu-id="ef7a9-181">Toujours dans **views.py**, ajouter hello suivant code toohello la fin du fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-181">Still in **views.py**, add hello following code toohello end of hello file.</span></span> <span data-ttu-id="ef7a9-182">Il prend en charge de la création de la base de données hello utilisé par le formulaire de hello.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-182">This takes care of creating hello database used by hello form.</span></span> <span data-ttu-id="ef7a9-183">Ne supprimez pas de code existant de hello dans **views.py**.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-183">Do not delete any of hello existing code in **views.py**.</span></span> <span data-ttu-id="ef7a9-184">Ajouter simplement cette terminaison toohello.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-184">Simply append this toohello end.</span></span>

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


### <a name="read-database-collection-document-and-submit-form"></a><span data-ttu-id="ef7a9-185">Lecture de la base de données, de la collection et du document, et envoi du formulaire</span><span class="sxs-lookup"><span data-stu-id="ef7a9-185">Read database, collection, document, and submit form</span></span>
* <span data-ttu-id="ef7a9-186">Toujours dans **views.py**, ajouter hello suivant code toohello la fin du fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-186">Still in **views.py**, add hello following code toohello end of hello file.</span></span> <span data-ttu-id="ef7a9-187">Il prend en charge de la définition de formulaire hello, lire le document, la collection et base de données hello.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-187">This takes care of setting up hello form, reading hello database, collection, and document.</span></span> <span data-ttu-id="ef7a9-188">Ne supprimez pas de code existant de hello dans **views.py**.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-188">Do not delete any of hello existing code in **views.py**.</span></span> <span data-ttu-id="ef7a9-189">Ajouter simplement cette terminaison toohello.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-189">Simply append this toohello end.</span></span>

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


### <a name="create-hello-html-files"></a><span data-ttu-id="ef7a9-190">Créer des fichiers HTML hello</span><span class="sxs-lookup"><span data-stu-id="ef7a9-190">Create hello HTML files</span></span>
1. <span data-ttu-id="ef7a9-191">Dans l’Explorateur de solutions, Bonjour **didacticiel** dossier, à droite cliquez sur hello **modèles** dossier, cliquez sur **ajouter**, puis cliquez sur **un nouvel élément**.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-191">In Solution Explorer, in hello **tutorial** folder, right click hello **templates** folder, click **Add**, and then click **New Item**.</span></span> 
2. <span data-ttu-id="ef7a9-192">Sélectionnez **HTML Page**, puis, dans le type de zone de nom hello **create.html**.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-192">Select **HTML Page**, and then in hello name box type **create.html**.</span></span> 
3. <span data-ttu-id="ef7a9-193">Répétez les étapes 1 et 2 toocreate deux autres fichiers HTML : results.html et vote.html.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-193">Repeat steps 1 and 2 toocreate two additional HTML files: results.html and vote.html.</span></span>
4. <span data-ttu-id="ef7a9-194">Ajouter hello suivant code trop**create.html** Bonjour `<body>` élément.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-194">Add hello following code too**create.html** in hello `<body>` element.</span></span> <span data-ttu-id="ef7a9-195">Il affiche un message indiquant la création d’une base de données, d’une collection et d’un document.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-195">It displays a message stating that we created a new database, collection, and document.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>{{ title }}.</h2>
    <h3>{{ message }}</h3>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```
5. <span data-ttu-id="ef7a9-196">Ajouter hello suivant code trop**results.html** Bonjour `<body`> élément.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-196">Add hello following code too**results.html** in hello `<body`> element.</span></span> <span data-ttu-id="ef7a9-197">Il affiche les résultats de hello d’interrogation de hello.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-197">It displays hello results of hello poll.</span></span>
   
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
6. <span data-ttu-id="ef7a9-198">Ajouter hello suivant code trop**vote.html** Bonjour `<body`> élément.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-198">Add hello following code too**vote.html** in hello `<body`> element.</span></span> <span data-ttu-id="ef7a9-199">Il affiche l’interrogation hello et accepte les votes hello.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-199">It displays hello poll and accepts hello votes.</span></span> <span data-ttu-id="ef7a9-200">Sur l’enregistrement des votes de hello, contrôle de hello est transmise sur tooviews.py où nous reconnaîtra hello vote cast et ajouter le document de hello en conséquence.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-200">On registering hello votes, hello control is passed over tooviews.py where we will recognize hello vote cast and append hello document accordingly.</span></span>
   
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
7. <span data-ttu-id="ef7a9-201">Bonjour **modèles** dossier, le contenu de hello de remplacement de **index.html** avec les éléments suivants de hello.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-201">In hello **templates** folder, replace hello contents of **index.html** with hello following.</span></span> <span data-ttu-id="ef7a9-202">Cela sert de hello page de votre application de destination.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-202">This serves as hello landing page for your application.</span></span>
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Python + Azure Cosmos DB Voting Application.</h2>
    <h3>This is a sample Cosmos DB voting application using PyDocumentDB</h3>
    <p><a href="{{ url_for('create') }}" class="btn btn-primary btn-large">Create/Clear hello Voting Database &raquo;</a></p>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```

### <a name="add-a-configuration-file-and-change-hello-initpy"></a><span data-ttu-id="ef7a9-203">Ajouter un fichier de configuration et de modifier hello \_ \_init\_\_.py</span><span class="sxs-lookup"><span data-stu-id="ef7a9-203">Add a configuration file and change hello \_\_init\_\_.py</span></span>
1. <span data-ttu-id="ef7a9-204">Dans l’Explorateur de solutions, cliquez sur hello **didacticiel** de projet, cliquez sur **ajouter**, cliquez sur **un nouvel élément**, sélectionnez **fichier Python vide**, puis nom de fichier hello **config.py**.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-204">In Solution Explorer, right-click hello **tutorial** project, click **Add**, click **New Item**, select **Empty Python File**, and then name hello file **config.py**.</span></span> <span data-ttu-id="ef7a9-205">Ce fichier de configuration est requis par les formulaires dans Flask.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-205">This config file is required by forms in Flask.</span></span> <span data-ttu-id="ef7a9-206">Vous pouvez l’utiliser tooprovide une clé de secret principal.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-206">You can use it tooprovide a secret key as well.</span></span> <span data-ttu-id="ef7a9-207">Cette clé n'est cependant pas nécessaire dans le cadre de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-207">This key is not needed for this tutorial though.</span></span>
2. <span data-ttu-id="ef7a9-208">Ajoutez hello suivant tooconfig.py de code, vous aurez besoin de valeurs hello tooalter **DOCUMENTDB\_hôte** et **DOCUMENTDB\_clé** à l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-208">Add hello following code tooconfig.py, you'll need tooalter hello values of **DOCUMENTDB\_HOST** and **DOCUMENTDB\_KEY** in hello next step.</span></span>
   
    ```python
    CSRF_ENABLED = True
    SECRET_KEY = 'you-will-never-guess'
   
    DOCUMENTDB_HOST = 'https://YOUR_DOCUMENTDB_NAME.documents.azure.com:443/'
    DOCUMENTDB_KEY = 'YOUR_SECRET_KEY_ENDING_IN_=='
   
    DOCUMENTDB_DATABASE = 'voting database'
    DOCUMENTDB_COLLECTION = 'voting collection'
    DOCUMENTDB_DOCUMENT = 'voting document'
    ```
3. <span data-ttu-id="ef7a9-209">Bonjour [portail Azure](https://portal.azure.com/), accédez toohello **clés** panneau en cliquant sur **Parcourir**, **des comptes de base de données Azure Cosmos**, double-cliquez sur le nom de hello Hello toouse de compte, puis cliquez sur hello **clés** bouton Bonjour **Essentials** zone.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-209">In hello [Azure portal](https://portal.azure.com/), navigate toohello **Keys** blade by clicking **Browse**, **Azure Cosmos DB Accounts**, double-click hello name of hello account toouse, and then click hello **Keys** button in hello **Essentials** area.</span></span> <span data-ttu-id="ef7a9-210">Bonjour **clés** panneau, hello de copie **URI** valeur et le coller dans hello **config.py** fichier, en tant que valeur hello pour hello **DOCUMENTDB\_hôte**  propriété.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-210">In hello **Keys** blade, copy hello **URI** value and paste it into hello **config.py** file, as hello value for hello **DOCUMENTDB\_HOST** property.</span></span> 
4. <span data-ttu-id="ef7a9-211">Dans hello portail Azure, Bonjour **clés** panneau, copier la valeur hello Hello **clé primaire** ou hello **clé secondaire**et le coller dans hello **config.py**  fichier, en tant que valeur hello pour hello **DOCUMENTDB\_clé** propriété.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-211">Back in hello Azure portal, in hello **Keys** blade, copy hello value of hello **Primary Key** or hello **Secondary Key**, and paste it into hello **config.py** file, as hello value for hello **DOCUMENTDB\_KEY** property.</span></span>
5. <span data-ttu-id="ef7a9-212">Bonjour  **\_ \_init\_\_.py** , ajoutez hello ligne suivante.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-212">In hello **\_\_init\_\_.py** file, add hello following line.</span></span> 
   
        app.config.from_object('config')
   
    <span data-ttu-id="ef7a9-213">Afin que le contenu du fichier de hello hello est la suivante :</span><span class="sxs-lookup"><span data-stu-id="ef7a9-213">So that hello content of hello file is:</span></span>
   
    ```python
    from flask import Flask
    app = Flask(__name__)
    app.config.from_object('config')
    import tutorial.views
    ```
6. <span data-ttu-id="ef7a9-214">Après avoir ajouté tous les fichiers de hello, l’Explorateur de solutions doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="ef7a9-214">After adding all hello files, Solution Explorer should look like this:</span></span>
   
    ![Capture d’écran de la fenêtre de l’Explorateur de solutions Visual Studio hello](./media/documentdb-python-application/cosmos-db-python-solution-explorer.png)

## <a name="step-4-run-your-web-application-locally"></a><span data-ttu-id="ef7a9-216">Étape 4 : Exécution locale de votre application web</span><span class="sxs-lookup"><span data-stu-id="ef7a9-216">Step 4: Run your web application locally</span></span>
1. <span data-ttu-id="ef7a9-217">Générez la solution de hello en appuyant sur **Ctrl**+**MAJ**+**B**.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-217">Build hello solution by pressing **Ctrl**+**Shift**+**B**.</span></span>
2. <span data-ttu-id="ef7a9-218">Une fois hello génération terminée, démarrez le site Web de hello en appuyant sur **F5**.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-218">Once hello build succeeds, start hello website by pressing **F5**.</span></span> <span data-ttu-id="ef7a9-219">Vous devez voir s’afficher hello sur votre écran.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-219">You should see hello following on your screen.</span></span>
   
    ![Capture d’écran de hello Python + Azure Cosmos DB vote Application affichée dans un navigateur web](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)
3. <span data-ttu-id="ef7a9-221">Cliquez sur **créer/effacer hello vote de la base de données** base de données toogenerate hello.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-221">Click **Create/Clear hello Voting Database** toogenerate hello database.</span></span>
   
    ![Capture d’écran de hello créer une Page d’application web de hello – informations sur le développement](./media/documentdb-python-application/cosmos-db-python-run-create-page.png)
4. <span data-ttu-id="ef7a9-223">Cliquez ensuite sur **Vote** et sélectionnez votre option.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-223">Then, click **Vote** and select your option.</span></span>
   
    ![Capture d’écran de l’application web de hello à poser une question de vote posée](./media/documentdb-python-application/cosmos-db-vote.png)
5. <span data-ttu-id="ef7a9-225">Pour chaque vote que vous effectuer un cast, elle incrémente compteur approprié de hello.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-225">For every vote you cast, it increments hello appropriate counter.</span></span>
   
    ![Capture d’écran de hello résultats de la page de vote hello indiqué](./media/documentdb-python-application/cosmos-db-voting-results.png)
6. <span data-ttu-id="ef7a9-227">Arrêter le débogage du projet de hello en appuyant sur MAJ + F5.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-227">Stop debugging hello project by pressing Shift+F5.</span></span>

## <a name="step-5-deploy-hello-web-application-tooazure"></a><span data-ttu-id="ef7a9-228">Étape 5 : Déployer hello web application tooAzure</span><span class="sxs-lookup"><span data-stu-id="ef7a9-228">Step 5: Deploy hello web application tooAzure</span></span>
<span data-ttu-id="ef7a9-229">Maintenant que vous avez application complète de hello fonctionne correctement sur la base de données Cosmos, nous allons toodeploy cette tooAzure.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-229">Now that you have hello complete application working correctly against Cosmos DB, we're going toodeploy this tooAzure.</span></span>

1. <span data-ttu-id="ef7a9-230">Projet de hello avec le bouton droit dans l’Explorateur de solutions (Assurez-vous que vous n’êtes pas en cours d’exécution il localement), puis sélectionnez **publier**.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-230">Right-click hello project in Solution Explorer (make sure you're not still running it locally) and select **Publish**.</span></span>  
   
     ![Capture d’écran du didacticiel hello sélectionné dans l’Explorateur de solutions, avec l’option de publication hello mis en surbrillance](./media/documentdb-python-application/image20.png)
2. <span data-ttu-id="ef7a9-232">Bonjour **publier** boîte de dialogue, sélectionnez **Microsoft Azure App Service**, sélectionnez **créer un nouveau**, puis cliquez sur **publier**.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-232">In hello **Publish** dialog box, select **Microsoft Azure App Service**, select **Create New**, and then click **Publish**.</span></span>
   
    ![Capture d’écran de la fenêtre de publier le site Web hello avec Microsoft Azure App Service est mis en surbrillance](./media/documentdb-python-application/cosmos-db-python-publish.png)
3. <span data-ttu-id="ef7a9-234">Bonjour **créer un Service application** boîte de dialogue, entrez le nom hello pour votre application web avec votre **abonnement**, **groupe de ressources**, et **du Plan App Service** , puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-234">In hello **Create App Service** dialog box, enter hello name for your web app along with your **Subscription**, **Resource Group**, and **App Service Plan**, then click **Create**.</span></span>
   
    ![Capture d’écran de la fenêtre de Microsoft Azure Web Apps fenêtre hello](./media/documentdb-python-application/cosmos-db-python-create-app-service.png)
4. <span data-ttu-id="ef7a9-236">Dans quelques secondes, Visual Studio achèvera la publication de votre service d’application et lancera un navigateur, dans lequel vous pourrez voir votre réalisation exécutée dans Azure.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-236">In a few seconds, Visual Studio will finish publishing your app service and launch a browser where you can see your handiwork running in Azure!</span></span>

    ![Capture d’écran de la fenêtre de Microsoft Azure Web Apps fenêtre hello](./media/documentdb-python-application/cosmos-db-python-appservice-created.png)

## <a name="troubleshooting"></a><span data-ttu-id="ef7a9-238">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="ef7a9-238">Troubleshooting</span></span>
<span data-ttu-id="ef7a9-239">Si c’est la première application Python hello, que vous exécutez sur votre ordinateur, vérifiez ce qui suit hello dossiers (ou l’emplacement d’installation équivalente hello) est inclus dans votre variable de chemin d’accès :</span><span class="sxs-lookup"><span data-stu-id="ef7a9-239">If this is hello first Python app you've run on your computer, ensure that hello following folders (or hello equivalent installation locations) are included in your PATH variable:</span></span>

    C:\Python27\site-packages;C:\Python27\;C:\Python27\Scripts;

<span data-ttu-id="ef7a9-240">Si vous recevez une erreur sur votre page de vote, et que vous avez nommé votre projet autre que **didacticiel**, assurez-vous que  **\_ \_init\_\_.py** références hello nom de projet approprié dans la ligne de hello : `import tutorial.view`.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-240">If you receive an error on your vote page, and you named your project something other than **tutorial**, make sure that **\_\_init\_\_.py** references hello correct project name in hello line: `import tutorial.view`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef7a9-241">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ef7a9-241">Next steps</span></span>
<span data-ttu-id="ef7a9-242">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="ef7a9-242">Congratulations!</span></span> <span data-ttu-id="ef7a9-243">Vous avez simplement terminé votre première application web de Python à l’aide de la base de données Cosmos et publié tooAzure.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-243">You have just completed your first Python web application using Cosmos DB and published it tooAzure.</span></span>

<span data-ttu-id="ef7a9-244">Nous mettons à jour et améliorons cette rubrique fréquemment en fonction de vos commentaires.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-244">We update and improve this topic frequently based on your feedback.</span></span>  <span data-ttu-id="ef7a9-245">Une fois vous venez de terminer hello didacticiel, veuillez à l’aide de hello vote des boutons situés en haut de hello et en bas de cette page et tooinclude que vos commentaires sur les améliorations souhaitées toosee apportée.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-245">Once you've completed hello tutorial, please using hello voting buttons at hello top and bottom of this page, and be sure tooinclude your feedback on what improvements you want toosee made.</span></span> <span data-ttu-id="ef7a9-246">Si vous souhaitez que nous toocontact vous directement, vous pouvez tooinclude libre votre adresse de messagerie dans vos commentaires.</span><span class="sxs-lookup"><span data-stu-id="ef7a9-246">If you'd like us toocontact you directly, feel free tooinclude your email address in your comments.</span></span>

<span data-ttu-id="ef7a9-247">application de web tooyour tooadd des fonctionnalités supplémentaires, consultez hello API disponibles dans hello [Azure Cosmos DB Python SDK](documentdb-sdk-python.md).</span><span class="sxs-lookup"><span data-stu-id="ef7a9-247">tooadd additional functionality tooyour web application, review hello APIs available in hello [Azure Cosmos DB Python SDK](documentdb-sdk-python.md).</span></span>

<span data-ttu-id="ef7a9-248">Pour plus d’informations sur Azure, Visual Studio et Python, consultez hello [centre de développement Python](https://azure.microsoft.com/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="ef7a9-248">For more information about Azure, Visual Studio, and Python, see hello [Python Developer Center](https://azure.microsoft.com/develop/python/).</span></span> 

<span data-ttu-id="ef7a9-249">Pour d’autres didacticiels ballon de Python, consultez [hello ballon méga-didacticiel, partie i : Hello, World !](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world).</span><span class="sxs-lookup"><span data-stu-id="ef7a9-249">For additional Python Flask tutorials, see [hello Flask Mega-Tutorial, Part I: Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world).</span></span> 

[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[2]: https://www.python.org/downloads/windows/
[3]: https://www.microsoft.com/download/details.aspx?id=44266
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Azure portal]: http://portal.azure.com
