---
title: aaaWeb application avec Express (Node.js) | Documents Microsoft
description: "Un didacticiel qui s’appuie sur didacticiel de service cloud hello et montre comment toouse hello Express module."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 24f8e7ef-e90d-4554-9b1e-a9b31d5824e5
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 91921bfbe137eeca9a110d4cb18eb57b46b0060e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-web-application-using-express-on-an-azure-cloud-service"></a><span data-ttu-id="de23e-103">Création d'une application web Node.js avec Express sur un service cloud Azure</span><span class="sxs-lookup"><span data-stu-id="de23e-103">Build a Node.js web application using Express on an Azure Cloud Service</span></span>
<span data-ttu-id="de23e-104">Node.js inclut un jeu minimal de fonctionnalités dans hello core runtime.</span><span class="sxs-lookup"><span data-stu-id="de23e-104">Node.js includes a minimal set of functionality in hello core runtime.</span></span>
<span data-ttu-id="de23e-105">Les développeurs utilisent souvent 3e partie modules tooprovide des fonctionnalités supplémentaires lorsque vous développez une application Node.js.</span><span class="sxs-lookup"><span data-stu-id="de23e-105">Developers often use 3rd party modules tooprovide additional functionality when developing a Node.js application.</span></span> <span data-ttu-id="de23e-106">Dans ce didacticiel, vous allez créer une nouvelle application à l’aide de hello [Express] [ Express] module, qui fournit une infrastructure MVC pour créer des applications web Node.js.</span><span class="sxs-lookup"><span data-stu-id="de23e-106">In this tutorial you will create a new application using hello [Express][Express] module, which provides an MVC framework for creating Node.js web applications.</span></span>

<span data-ttu-id="de23e-107">Une capture d’écran de l’application hello terminée est ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="de23e-107">A screenshot of hello completed application is below:</span></span>

![Un navigateur web affichage tooExpress Bienvenue dans Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="create-a-cloud-service-project"></a><span data-ttu-id="de23e-109">Création d'un projet de service cloud</span><span class="sxs-lookup"><span data-stu-id="de23e-109">Create a Cloud Service Project</span></span>
[!INCLUDE [install-dev-tools](../../includes/install-dev-tools.md)]

<span data-ttu-id="de23e-110">Hello suivants étapes toocreate un nouveau projet de service cloud nommé « expressapp » :</span><span class="sxs-lookup"><span data-stu-id="de23e-110">Perform hello following steps toocreate a new cloud service project named 'expressapp':</span></span>

1. <span data-ttu-id="de23e-111">À partir de hello **Menu Démarrer** ou **écran d’accueil de**, recherchez **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="de23e-111">From hello **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span> <span data-ttu-id="de23e-112">Enfin, cliquez avec le bouton droit sur **Windows PowerShell** et sélectionnez **Exécuter en tant qu’administrateur**.</span><span class="sxs-lookup"><span data-stu-id="de23e-112">Finally, right-click **Windows PowerShell** and select **Run As Administrator**.</span></span>
   
    ![Icône Azure PowerShell](./media/cloud-services-nodejs-develop-deploy-express-app/azure-powershell-start.png)
2. <span data-ttu-id="de23e-114">Modifiez les répertoires toohello **c:\\nœud** active, puis entrez hello suivant de commandes toocreate une solution nommée **expressapp** et un rôle web nommé **WebRole1** :</span><span class="sxs-lookup"><span data-stu-id="de23e-114">Change directories toohello **c:\\node** directory and then enter hello following commands toocreate a new solution named **expressapp** and a web role named **WebRole1**:</span></span>
   
        PS C:\node> New-AzureServiceProject expressapp
        PS C:\Node\expressapp> Add-AzureNodeWebRole
        PS C:\Node\expressapp> Set-AzureServiceProjectRole WebRole1 Node 0.10.21
   
    > [!NOTE]
    > <span data-ttu-id="de23e-115">Par défaut, **Add-AzureNodeWebRole** utilise une ancienne version de Node.js.</span><span class="sxs-lookup"><span data-stu-id="de23e-115">By default, **Add-AzureNodeWebRole** uses an older version of Node.js.</span></span> <span data-ttu-id="de23e-116">Hello **Set-AzureServiceProjectRole** v0.10.21 toouse Azure du nœud indique à l’instruction ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="de23e-116">hello **Set-AzureServiceProjectRole** statement above instructs Azure toouse v0.10.21 of Node.</span></span>  <span data-ttu-id="de23e-117">Notez les paramètres hello respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="de23e-117">Note hello parameters are case-sensitive.</span></span>  <span data-ttu-id="de23e-118">Vous pouvez vérifier la version correcte de hello de Node.js a été sélectionnée en vérifiant hello **moteurs** propriété dans **WebRole1\package.json**.</span><span class="sxs-lookup"><span data-stu-id="de23e-118">You can verify hello correct version of Node.js has been selected by checking hello **engines** property in **WebRole1\package.json**.</span></span>
    > 
    > 

## <a name="install-express"></a><span data-ttu-id="de23e-119">Installation d'Express</span><span class="sxs-lookup"><span data-stu-id="de23e-119">Install Express</span></span>
1. <span data-ttu-id="de23e-120">Installer le Générateur de Express hello en émettant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="de23e-120">Install hello Express generator by issuing hello following command:</span></span>
   
        PS C:\node\expressapp> npm install express-generator -g
   
    <span data-ttu-id="de23e-121">sortie Hello de commande de npm hello doit se présenter comme résultat toohello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="de23e-121">hello output of hello npm command should look similar toohello result below.</span></span> 
   
    ![La sortie hello affichage Windows PowerShell de hello npm installer commande express.](./media/cloud-services-nodejs-develop-deploy-express-app/express-g.png)
2. <span data-ttu-id="de23e-123">Modifiez les répertoires toohello **WebRole1** active et l’utilisation hello commande express toogenerate une nouvelle application :</span><span class="sxs-lookup"><span data-stu-id="de23e-123">Change directories toohello **WebRole1** directory and use hello express command toogenerate a new application:</span></span>
   
        PS C:\node\expressapp\WebRole1> express
   
    <span data-ttu-id="de23e-124">Vous est demandée toooverwrite votre ancienne application.</span><span class="sxs-lookup"><span data-stu-id="de23e-124">You will be prompted toooverwrite your earlier application.</span></span> <span data-ttu-id="de23e-125">Entrez **y** ou **Oui** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="de23e-125">Enter **y** or **yes** toocontinue.</span></span> <span data-ttu-id="de23e-126">Express génère le fichier de app.js hello et une structure de dossiers pour la création de votre application.</span><span class="sxs-lookup"><span data-stu-id="de23e-126">Express will generate hello app.js file and a folder structure for building your application.</span></span>
   
    ![sortie Hello de commande express hello](./media/cloud-services-nodejs-develop-deploy-express-app/node23.png)
3. <span data-ttu-id="de23e-128">les dépendances supplémentaires tooinstall définis dans le fichier du package.json hello, entrez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="de23e-128">tooinstall additional dependencies defined in hello package.json file, enter hello following command:</span></span>
   
       PS C:\node\expressapp\WebRole1> npm install
   
   ![commande d’installation de sortie Hello de hello npm](./media/cloud-services-nodejs-develop-deploy-express-app/node26.png)
4. <span data-ttu-id="de23e-130">Suivant de hello utilisez commande toocopy hello **bin/www** trop de fichiers**server.js**.</span><span class="sxs-lookup"><span data-stu-id="de23e-130">Use hello following command toocopy hello **bin/www** file too**server.js**.</span></span> <span data-ttu-id="de23e-131">Il s’agit pour le service cloud hello puisse trouver un point d’entrée hello pour cette application.</span><span class="sxs-lookup"><span data-stu-id="de23e-131">This is so hello cloud service can find hello entry point for this application.</span></span>
   
       PS C:\node\expressapp\WebRole1> copy bin/www server.js
   
   <span data-ttu-id="de23e-132">Une fois cette commande terminée, vous devez avoir un **server.js** fichier hello WebRole1 répertoire.</span><span class="sxs-lookup"><span data-stu-id="de23e-132">After this command completes, you should have a **server.js** file in hello WebRole1 directory.</span></span>
5. <span data-ttu-id="de23e-133">Modifier hello **server.js** tooremove d'entre hello '.' caractères de hello ligne suivante.</span><span class="sxs-lookup"><span data-stu-id="de23e-133">Modify hello **server.js** tooremove one of hello '.' characters from hello following line.</span></span>
   
       var app = require('../app');
   
   <span data-ttu-id="de23e-134">Après avoir apporté cette modification, la ligne de hello doit apparaître comme suit.</span><span class="sxs-lookup"><span data-stu-id="de23e-134">After making this modification, hello line should appear as follows.</span></span>
   
       var app = require('./app');
   
   <span data-ttu-id="de23e-135">Cette modification n’est requise, car nous avons déplacé le fichier de hello (anciennement **bin/www**,) toohello même répertoire que le fichier de l’application hello est obligatoire.</span><span class="sxs-lookup"><span data-stu-id="de23e-135">This change is required since we moved hello file (formerly **bin/www**,) toohello same directory as hello app file being required.</span></span> <span data-ttu-id="de23e-136">Après avoir apporté cette modification, enregistrez hello **server.js** fichier.</span><span class="sxs-lookup"><span data-stu-id="de23e-136">After making this change, save hello **server.js** file.</span></span>
6. <span data-ttu-id="de23e-137">Utilisez hello suite commande toorun hello application Bonjour émulateur Azure :</span><span class="sxs-lookup"><span data-stu-id="de23e-137">Use hello following command toorun hello application in hello Azure emulator:</span></span>
   
       PS C:\node\expressapp\WebRole1> Start-AzureEmulator -launch
   
    ![Une page web contenant tooexpress Bienvenue.](./media/cloud-services-nodejs-develop-deploy-express-app/node28.png)

## <a name="modifying-hello-view"></a><span data-ttu-id="de23e-139">Hello, vue de modification</span><span class="sxs-lookup"><span data-stu-id="de23e-139">Modifying hello View</span></span>
<span data-ttu-id="de23e-140">À présent modifier hello afficher toodisplay hello le message « Bienvenue tooExpress dans Azure ».</span><span class="sxs-lookup"><span data-stu-id="de23e-140">Now modify hello view toodisplay hello message "Welcome tooExpress in Azure".</span></span>

1. <span data-ttu-id="de23e-141">Entrez hello commande tooopen hello index.jade fichier suivant :</span><span class="sxs-lookup"><span data-stu-id="de23e-141">Enter hello following command tooopen hello index.jade file:</span></span>
   
       PS C:\node\expressapp\WebRole1> notepad views/index.jade
   
   ![contenu Hello du fichier de index.jade hello.](./media/cloud-services-nodejs-develop-deploy-express-app/getting-started-19.png)
   
   <span data-ttu-id="de23e-143">Jade est un moteur d’affichage par défaut hello utilisé par les applications Express.</span><span class="sxs-lookup"><span data-stu-id="de23e-143">Jade is hello default view engine used by Express applications.</span></span> <span data-ttu-id="de23e-144">Pour plus d’informations sur le moteur d’affichage Jade hello, consultez [http://jade-lang.com][http://jade-lang.com].</span><span class="sxs-lookup"><span data-stu-id="de23e-144">For more information on hello Jade view engine, see [http://jade-lang.com][http://jade-lang.com].</span></span>
2. <span data-ttu-id="de23e-145">Modifier hello dernière ligne de texte en ajoutant **dans Azure**.</span><span class="sxs-lookup"><span data-stu-id="de23e-145">Modify hello last line of text by appending **in Azure**.</span></span>
   
   ![lit les fichiers de index.jade Hello, dernière ligne de hello : p Bienvenue trop\#{titre} dans Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node31.png)
3. <span data-ttu-id="de23e-147">Enregistrez le fichier de hello et quittez le bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="de23e-147">Save hello file and exit Notepad.</span></span>
4. <span data-ttu-id="de23e-148">Actualisez votre navigateur pour afficher vos modifications.</span><span class="sxs-lookup"><span data-stu-id="de23e-148">Refresh your browser and you will see your changes.</span></span>
   
   ![Une fenêtre de navigateur, la page de hello contient tooExpress Bienvenue dans Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node32.png)

<span data-ttu-id="de23e-150">Après l’application de test hello, utilisez hello **Stop-AzureEmulator** émulateur de hello toostop applet de commande.</span><span class="sxs-lookup"><span data-stu-id="de23e-150">After testing hello application, use hello **Stop-AzureEmulator** cmdlet toostop hello emulator.</span></span>

## <a name="publishing-hello-application-tooazure"></a><span data-ttu-id="de23e-151">Publication tooAzure d’Application hello</span><span class="sxs-lookup"><span data-stu-id="de23e-151">Publishing hello Application tooAzure</span></span>
<span data-ttu-id="de23e-152">Dans la fenêtre Azure PowerShell de hello, utilisez hello **AzureServiceProject de publication** service de cloud d’applet de commande toodeploy hello application tooa</span><span class="sxs-lookup"><span data-stu-id="de23e-152">In hello Azure PowerShell window, use hello **Publish-AzureServiceProject** cmdlet toodeploy hello application tooa cloud service</span></span>

    PS C:\node\expressapp\WebRole1> Publish-AzureServiceProject -ServiceName myexpressapp -Location "East US" -Launch

<span data-ttu-id="de23e-153">Une fois l’opération de déploiement hello terminé, votre navigateur ouvrira et affichera la page web de hello.</span><span class="sxs-lookup"><span data-stu-id="de23e-153">Once hello deployment operation completes, your browser will open and display hello web page.</span></span>

![Un navigateur web que l’affichage de page de Express hello.](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="next-steps"></a><span data-ttu-id="de23e-156">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="de23e-156">Next steps</span></span>
<span data-ttu-id="de23e-157">Pour plus d’informations, consultez hello [centre de développement Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="de23e-157">For more information, see hello [Node.js Developer Center](/develop/nodejs/).</span></span>

[Node.js Web Application]: http://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[Express]: http://expressjs.com/
[http://jade-lang.com]: http://jade-lang.com


