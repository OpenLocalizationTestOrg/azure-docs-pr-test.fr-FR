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
# <a name="build-a-nodejs-web-application-using-express-on-an-azure-cloud-service"></a>Création d'une application web Node.js avec Express sur un service cloud Azure
Node.js inclut un jeu minimal de fonctionnalités dans hello core runtime.
Les développeurs utilisent souvent 3e partie modules tooprovide des fonctionnalités supplémentaires lorsque vous développez une application Node.js. Dans ce didacticiel, vous allez créer une nouvelle application à l’aide de hello [Express] [ Express] module, qui fournit une infrastructure MVC pour créer des applications web Node.js.

Une capture d’écran de l’application hello terminée est ci-dessous :

![Un navigateur web affichage tooExpress Bienvenue dans Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="create-a-cloud-service-project"></a>Création d'un projet de service cloud
[!INCLUDE [install-dev-tools](../../includes/install-dev-tools.md)]

Hello suivants étapes toocreate un nouveau projet de service cloud nommé « expressapp » :

1. À partir de hello **Menu Démarrer** ou **écran d’accueil de**, recherchez **Windows PowerShell**. Enfin, cliquez avec le bouton droit sur **Windows PowerShell** et sélectionnez **Exécuter en tant qu’administrateur**.
   
    ![Icône Azure PowerShell](./media/cloud-services-nodejs-develop-deploy-express-app/azure-powershell-start.png)
2. Modifiez les répertoires toohello **c:\\nœud** active, puis entrez hello suivant de commandes toocreate une solution nommée **expressapp** et un rôle web nommé **WebRole1** :
   
        PS C:\node> New-AzureServiceProject expressapp
        PS C:\Node\expressapp> Add-AzureNodeWebRole
        PS C:\Node\expressapp> Set-AzureServiceProjectRole WebRole1 Node 0.10.21
   
    > [!NOTE]
    > Par défaut, **Add-AzureNodeWebRole** utilise une ancienne version de Node.js. Hello **Set-AzureServiceProjectRole** v0.10.21 toouse Azure du nœud indique à l’instruction ci-dessus.  Notez les paramètres hello respectent la casse.  Vous pouvez vérifier la version correcte de hello de Node.js a été sélectionnée en vérifiant hello **moteurs** propriété dans **WebRole1\package.json**.
    > 
    > 

## <a name="install-express"></a>Installation d'Express
1. Installer le Générateur de Express hello en émettant hello de commande suivante :
   
        PS C:\node\expressapp> npm install express-generator -g
   
    sortie Hello de commande de npm hello doit se présenter comme résultat toohello ci-dessous. 
   
    ![La sortie hello affichage Windows PowerShell de hello npm installer commande express.](./media/cloud-services-nodejs-develop-deploy-express-app/express-g.png)
2. Modifiez les répertoires toohello **WebRole1** active et l’utilisation hello commande express toogenerate une nouvelle application :
   
        PS C:\node\expressapp\WebRole1> express
   
    Vous est demandée toooverwrite votre ancienne application. Entrez **y** ou **Oui** toocontinue. Express génère le fichier de app.js hello et une structure de dossiers pour la création de votre application.
   
    ![sortie Hello de commande express hello](./media/cloud-services-nodejs-develop-deploy-express-app/node23.png)
3. les dépendances supplémentaires tooinstall définis dans le fichier du package.json hello, entrez hello de commande suivante :
   
       PS C:\node\expressapp\WebRole1> npm install
   
   ![commande d’installation de sortie Hello de hello npm](./media/cloud-services-nodejs-develop-deploy-express-app/node26.png)
4. Suivant de hello utilisez commande toocopy hello **bin/www** trop de fichiers**server.js**. Il s’agit pour le service cloud hello puisse trouver un point d’entrée hello pour cette application.
   
       PS C:\node\expressapp\WebRole1> copy bin/www server.js
   
   Une fois cette commande terminée, vous devez avoir un **server.js** fichier hello WebRole1 répertoire.
5. Modifier hello **server.js** tooremove d'entre hello '.' caractères de hello ligne suivante.
   
       var app = require('../app');
   
   Après avoir apporté cette modification, la ligne de hello doit apparaître comme suit.
   
       var app = require('./app');
   
   Cette modification n’est requise, car nous avons déplacé le fichier de hello (anciennement **bin/www**,) toohello même répertoire que le fichier de l’application hello est obligatoire. Après avoir apporté cette modification, enregistrez hello **server.js** fichier.
6. Utilisez hello suite commande toorun hello application Bonjour émulateur Azure :
   
       PS C:\node\expressapp\WebRole1> Start-AzureEmulator -launch
   
    ![Une page web contenant tooexpress Bienvenue.](./media/cloud-services-nodejs-develop-deploy-express-app/node28.png)

## <a name="modifying-hello-view"></a>Hello, vue de modification
À présent modifier hello afficher toodisplay hello le message « Bienvenue tooExpress dans Azure ».

1. Entrez hello commande tooopen hello index.jade fichier suivant :
   
       PS C:\node\expressapp\WebRole1> notepad views/index.jade
   
   ![contenu Hello du fichier de index.jade hello.](./media/cloud-services-nodejs-develop-deploy-express-app/getting-started-19.png)
   
   Jade est un moteur d’affichage par défaut hello utilisé par les applications Express. Pour plus d’informations sur le moteur d’affichage Jade hello, consultez [http://jade-lang.com][http://jade-lang.com].
2. Modifier hello dernière ligne de texte en ajoutant **dans Azure**.
   
   ![lit les fichiers de index.jade Hello, dernière ligne de hello : p Bienvenue trop\#{titre} dans Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node31.png)
3. Enregistrez le fichier de hello et quittez le bloc-notes.
4. Actualisez votre navigateur pour afficher vos modifications.
   
   ![Une fenêtre de navigateur, la page de hello contient tooExpress Bienvenue dans Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node32.png)

Après l’application de test hello, utilisez hello **Stop-AzureEmulator** émulateur de hello toostop applet de commande.

## <a name="publishing-hello-application-tooazure"></a>Publication tooAzure d’Application hello
Dans la fenêtre Azure PowerShell de hello, utilisez hello **AzureServiceProject de publication** service de cloud d’applet de commande toodeploy hello application tooa

    PS C:\node\expressapp\WebRole1> Publish-AzureServiceProject -ServiceName myexpressapp -Location "East US" -Launch

Une fois l’opération de déploiement hello terminé, votre navigateur ouvrira et affichera la page web de hello.

![Un navigateur web que l’affichage de page de Express hello. URL de Hello indique qu’il est actuellement hébergé sur Azure.](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations, consultez hello [centre de développement Node.js](/develop/nodejs/).

[Node.js Web Application]: http://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[Express]: http://expressjs.com/
[http://jade-lang.com]: http://jade-lang.com


