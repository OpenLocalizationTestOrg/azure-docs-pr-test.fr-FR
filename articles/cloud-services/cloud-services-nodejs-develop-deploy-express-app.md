---
title: Application web avec Express (Node.js) | Microsoft Docs
description: "Ce didacticiel poursuit le didacticiel relatif au service cloud et présente l’utilisation du module Express."
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
ms.openlocfilehash: 54b715695e24786ec4e8dfcabefc648d76179c8b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="build-a-nodejs-web-application-using-express-on-an-azure-cloud-service"></a><span data-ttu-id="2345f-103">Création d'une application web Node.js avec Express sur un service cloud Azure</span><span class="sxs-lookup"><span data-stu-id="2345f-103">Build a Node.js web application using Express on an Azure Cloud Service</span></span>
<span data-ttu-id="2345f-104">Node.js inclut un ensemble minimal de fonctionnalités dans le runtime principal.</span><span class="sxs-lookup"><span data-stu-id="2345f-104">Node.js includes a minimal set of functionality in the core runtime.</span></span>
<span data-ttu-id="2345f-105">Les développeurs utilisent souvent des modules tiers pour fournir des fonctionnalités supplémentaires lors du développement d'une application Node.js.</span><span class="sxs-lookup"><span data-stu-id="2345f-105">Developers often use 3rd party modules to provide additional functionality when developing a Node.js application.</span></span> <span data-ttu-id="2345f-106">Dans ce didacticiel, vous allez créer une application en utilisant le module [Express][Express], qui fournit une infrastructure MVC pour créer des applications web Node.js.</span><span class="sxs-lookup"><span data-stu-id="2345f-106">In this tutorial you will create a new application using the [Express][Express] module, which provides an MVC framework for creating Node.js web applications.</span></span>

<span data-ttu-id="2345f-107">Voici une capture d’écran de l’application terminée :</span><span class="sxs-lookup"><span data-stu-id="2345f-107">A screenshot of the completed application is below:</span></span>

![Navigateur Web affichant Bienvenue sur Express dans Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="create-a-cloud-service-project"></a><span data-ttu-id="2345f-109">Création d'un projet de service cloud</span><span class="sxs-lookup"><span data-stu-id="2345f-109">Create a Cloud Service Project</span></span>
[!INCLUDE [install-dev-tools](../../includes/install-dev-tools.md)]

<span data-ttu-id="2345f-110">Procédez comme suit pour créer un projet de service cloud nommé « expressapp » :</span><span class="sxs-lookup"><span data-stu-id="2345f-110">Perform the following steps to create a new cloud service project named 'expressapp':</span></span>

1. <span data-ttu-id="2345f-111">À partir du **menu Démarrer** ou de l’**écran d’accueil**, recherchez **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="2345f-111">From the **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span> <span data-ttu-id="2345f-112">Enfin, cliquez avec le bouton droit sur **Windows PowerShell** et sélectionnez **Exécuter en tant qu’administrateur**.</span><span class="sxs-lookup"><span data-stu-id="2345f-112">Finally, right-click **Windows PowerShell** and select **Run As Administrator**.</span></span>
   
    ![Icône Azure PowerShell](./media/cloud-services-nodejs-develop-deploy-express-app/azure-powershell-start.png)
2. <span data-ttu-id="2345f-114">Remplacez les répertoires du répertoire **c:\\node**, puis entrez les commandes suivantes pour créer une solution nommée **expressapp** et un rôle web nommé **WebRole1** :</span><span class="sxs-lookup"><span data-stu-id="2345f-114">Change directories to the **c:\\node** directory and then enter the following commands to create a new solution named **expressapp** and a web role named **WebRole1**:</span></span>
   
        PS C:\node> New-AzureServiceProject expressapp
        PS C:\Node\expressapp> Add-AzureNodeWebRole
        PS C:\Node\expressapp> Set-AzureServiceProjectRole WebRole1 Node 0.10.21
   
    > [!NOTE]
    > <span data-ttu-id="2345f-115">Par défaut, **Add-AzureNodeWebRole** utilise une ancienne version de Node.js.</span><span class="sxs-lookup"><span data-stu-id="2345f-115">By default, **Add-AzureNodeWebRole** uses an older version of Node.js.</span></span> <span data-ttu-id="2345f-116">L'instruction **Set-AzureServiceProjectRole** ci-dessus indique à Azure d'utiliser la version v0.10.21 de Node.</span><span class="sxs-lookup"><span data-stu-id="2345f-116">The **Set-AzureServiceProjectRole** statement above instructs Azure to use v0.10.21 of Node.</span></span>  <span data-ttu-id="2345f-117">Notez que les paramètres respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="2345f-117">Note the parameters are case-sensitive.</span></span>  <span data-ttu-id="2345f-118">Vous pouvez vérifier que la version correcte de Node.js a été sélectionnée en vérifiant la propriété **moteurs** dans **WebRole1\package.json**.</span><span class="sxs-lookup"><span data-stu-id="2345f-118">You can verify the correct version of Node.js has been selected by checking the **engines** property in **WebRole1\package.json**.</span></span>
    > 
    > 

## <a name="install-express"></a><span data-ttu-id="2345f-119">Installation d'Express</span><span class="sxs-lookup"><span data-stu-id="2345f-119">Install Express</span></span>
1. <span data-ttu-id="2345f-120">Installez le générateur Express en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2345f-120">Install the Express generator by issuing the following command:</span></span>
   
        PS C:\node\expressapp> npm install express-generator -g
   
    <span data-ttu-id="2345f-121">Le résultat de la commande npm doit ressembler à l'exemple ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="2345f-121">The output of the npm command should look similar to the result below.</span></span> 
   
    ![Windows PowerShell affichant le résultat de la commande npm install express.](./media/cloud-services-nodejs-develop-deploy-express-app/express-g.png)
2. <span data-ttu-id="2345f-123">Remplacez les répertoires du répertoire **WebRole1** et utilisez la commande express pour créer une application :</span><span class="sxs-lookup"><span data-stu-id="2345f-123">Change directories to the **WebRole1** directory and use the express command to generate a new application:</span></span>
   
        PS C:\node\expressapp\WebRole1> express
   
    <span data-ttu-id="2345f-124">Vous êtes invité à remplacer votre application précédente.</span><span class="sxs-lookup"><span data-stu-id="2345f-124">You will be prompted to overwrite your earlier application.</span></span> <span data-ttu-id="2345f-125">Tapez **y** ou **yes** pour continuer.</span><span class="sxs-lookup"><span data-stu-id="2345f-125">Enter **y** or **yes** to continue.</span></span> <span data-ttu-id="2345f-126">Express génère le fichier app.js et une structure de dossiers pour la création de votre application.</span><span class="sxs-lookup"><span data-stu-id="2345f-126">Express will generate the app.js file and a folder structure for building your application.</span></span>
   
    ![Résultat de la commande express](./media/cloud-services-nodejs-develop-deploy-express-app/node23.png)
3. <span data-ttu-id="2345f-128">Pour installer les dépendances supplémentaires définies dans le fichier package.json, entrez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2345f-128">To install additional dependencies defined in the package.json file, enter the following command:</span></span>
   
       PS C:\node\expressapp\WebRole1> npm install
   
   ![Résultat de la commande npm install](./media/cloud-services-nodejs-develop-deploy-express-app/node26.png)
4. <span data-ttu-id="2345f-130">Utilisez la commande suivante pour copier le fichier **bin/www** vers **server.js**.</span><span class="sxs-lookup"><span data-stu-id="2345f-130">Use the following command to copy the **bin/www** file to **server.js**.</span></span> <span data-ttu-id="2345f-131">De cette façon, le service cloud peut trouver le point d'entrée pour cette application.</span><span class="sxs-lookup"><span data-stu-id="2345f-131">This is so the cloud service can find the entry point for this application.</span></span>
   
       PS C:\node\expressapp\WebRole1> copy bin/www server.js
   
   <span data-ttu-id="2345f-132">Une fois cette commande terminée, un fichier **server.js** doit se trouver dans le répertoire WebRole1.</span><span class="sxs-lookup"><span data-stu-id="2345f-132">After this command completes, you should have a **server.js** file in the WebRole1 directory.</span></span>
5. <span data-ttu-id="2345f-133">Modifiez **server.js** pour supprimer l’un des caractères « . » de la ligne suivante.</span><span class="sxs-lookup"><span data-stu-id="2345f-133">Modify the **server.js** to remove one of the '.' characters from the following line.</span></span>
   
       var app = require('../app');
   
   <span data-ttu-id="2345f-134">Une fois cette modification apportée, la ligne doit apparaître comme suit.</span><span class="sxs-lookup"><span data-stu-id="2345f-134">After making this modification, the line should appear as follows.</span></span>
   
       var app = require('./app');
   
   <span data-ttu-id="2345f-135">Cette modification est nécessaire, car nous avons déplacé le fichier (anciennement **bin/www**) vers le même répertoire que le fichier d'application requis.</span><span class="sxs-lookup"><span data-stu-id="2345f-135">This change is required since we moved the file (formerly **bin/www**,) to the same directory as the app file being required.</span></span> <span data-ttu-id="2345f-136">Une fois cette modification effectuée, enregistrez le fichier **server.js** .</span><span class="sxs-lookup"><span data-stu-id="2345f-136">After making this change, save the **server.js** file.</span></span>
6. <span data-ttu-id="2345f-137">Utilisez la commande suivante pour exécuter l'application dans l'émulateur Azure :</span><span class="sxs-lookup"><span data-stu-id="2345f-137">Use the following command to run the application in the Azure emulator:</span></span>
   
       PS C:\node\expressapp\WebRole1> Start-AzureEmulator -launch
   
    ![Page Web contenant Bienvenue sur Express.](./media/cloud-services-nodejs-develop-deploy-express-app/node28.png)

## <a name="modifying-the-view"></a><span data-ttu-id="2345f-139">Modification de la vue</span><span class="sxs-lookup"><span data-stu-id="2345f-139">Modifying the View</span></span>
<span data-ttu-id="2345f-140">À présent, modifiez la vue pour afficher le message « Bienvenue sur Express dans Azure ».</span><span class="sxs-lookup"><span data-stu-id="2345f-140">Now modify the view to display the message "Welcome to Express in Azure".</span></span>

1. <span data-ttu-id="2345f-141">Entrez la commande suivante pour ouvrir le fichier index.jade :</span><span class="sxs-lookup"><span data-stu-id="2345f-141">Enter the following command to open the index.jade file:</span></span>
   
       PS C:\node\expressapp\WebRole1> notepad views/index.jade
   
   ![Contenu du fichier index.jade.](./media/cloud-services-nodejs-develop-deploy-express-app/getting-started-19.png)
   
   <span data-ttu-id="2345f-143">Jade est le moteur de vue par défaut des applications Express.</span><span class="sxs-lookup"><span data-stu-id="2345f-143">Jade is the default view engine used by Express applications.</span></span> <span data-ttu-id="2345f-144">Pour plus d’informations sur le moteur de vue Jade, consultez [http://jade-lang.com][http://jade-lang.com].</span><span class="sxs-lookup"><span data-stu-id="2345f-144">For more information on the Jade view engine, see [http://jade-lang.com][http://jade-lang.com].</span></span>
2. <span data-ttu-id="2345f-145">Modifiez la dernière ligne du texte en ajoutant **dans Azure**.</span><span class="sxs-lookup"><span data-stu-id="2345f-145">Modify the last line of text by appending **in Azure**.</span></span>
   
   ![Dernières lignes du fichier index.jade : p Bienvenue sur \#{title} dans Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node31.png)
3. <span data-ttu-id="2345f-147">Enregistrez le fichier et quittez le Bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="2345f-147">Save the file and exit Notepad.</span></span>
4. <span data-ttu-id="2345f-148">Actualisez votre navigateur pour afficher vos modifications.</span><span class="sxs-lookup"><span data-stu-id="2345f-148">Refresh your browser and you will see your changes.</span></span>
   
   ![Navigateur Web affichant la page Bienvenue sur Express dans Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node32.png)

<span data-ttu-id="2345f-150">Après avoir testé l'application, utilisez la cmdlet **Stop-AzureEmulator** pour arrêter l'émulateur.</span><span class="sxs-lookup"><span data-stu-id="2345f-150">After testing the application, use the **Stop-AzureEmulator** cmdlet to stop the emulator.</span></span>

## <a name="publishing-the-application-to-azure"></a><span data-ttu-id="2345f-151">Publication de l'application dans Azure</span><span class="sxs-lookup"><span data-stu-id="2345f-151">Publishing the Application to Azure</span></span>
<span data-ttu-id="2345f-152">Dans la fenêtre Azure PowerShell, utilisez la cmdlet **Publish-AzureServiceProject** pour déployer l'application dans un service cloud.</span><span class="sxs-lookup"><span data-stu-id="2345f-152">In the Azure PowerShell window, use the **Publish-AzureServiceProject** cmdlet to deploy the application to a cloud service</span></span>

    PS C:\node\expressapp\WebRole1> Publish-AzureServiceProject -ServiceName myexpressapp -Location "East US" -Launch

<span data-ttu-id="2345f-153">Une fois le déploiement terminé, votre navigateur s'ouvre et affiche la page web.</span><span class="sxs-lookup"><span data-stu-id="2345f-153">Once the deployment operation completes, your browser will open and display the web page.</span></span>

![Navigateur web affichant la page Express.](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="next-steps"></a><span data-ttu-id="2345f-156">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2345f-156">Next steps</span></span>
<span data-ttu-id="2345f-157">Pour plus d’informations, consultez le [Centre pour développeurs Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="2345f-157">For more information, see the [Node.js Developer Center](/develop/nodejs/).</span></span>

[Node.js Web Application]: http://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[Express]: http://expressjs.com/
[http://jade-lang.com]: http://jade-lang.com


