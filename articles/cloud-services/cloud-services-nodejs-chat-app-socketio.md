---
title: "application de aaaNode.js à l’aide de Socket.io | Documents Microsoft"
description: "Découvrez comment socket.io toouse dans une application node.js hébergé sur Azure."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 7f9435e0-7732-4aa1-a4df-ea0e894b847f
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 47c6c4a748938959315b880340f41f31faab4ea9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-chat-application-with-socketio-on-an-azure-cloud-service"></a>Création d'une application de conversation instantanée Node.js avec Socket.IO sur un service cloud Azure
Socket.IO permet une communication en temps réel entre votre serveur node.js et vos clients. Ce didacticiel présente l'hébergement d'une application de conversation instantanée socket.IO dans Azure. Pour plus d’informations sur Socket.IO, consultez le site <http://socket.io/>.

Une capture d’écran de l’application hello terminée est ci-dessous :

![Une fenêtre de navigateur affichant service hello hébergé sur Azure][completed-app]  

## <a name="prerequisites"></a>Composants requis
Vérifiez que hello suite de produits et les versions sont exemple hello complète de toosuccessfully installées dans cet article :

* Installez [Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)
* Installez [Node.js](https://nodejs.org/download/)
* Installez [Python version 2.7.10](https://www.python.org/)

## <a name="create-a-cloud-service-project"></a>Création d'un projet de service cloud
Hello étapes suivantes créent projet de service cloud hello qui hébergera l’application de Socket.IO hello.

1. À partir de hello **Menu Démarrer** ou **écran d’accueil de**, recherchez **Windows PowerShell**. Enfin, cliquez avec le bouton droit sur **Windows PowerShell** et sélectionnez **Exécuter en tant qu’administrateur**.
   
    ![Icône Azure PowerShell][powershell-menu]
2. Créez un répertoire appelé **c:\\node**. 
   
        PS C:\> md node
3. Modifiez les répertoires toohello **c:\\nœud** Active
   
        PS C:\> cd node
4. Entrez hello suivant de commandes toocreate une solution nommée **chatapp** et un rôle de travail nommé **WorkerRole1**:
   
        PS C:\node> New-AzureServiceProject chatapp
        PS C:\Node> Add-AzureNodeWorkerRole
   
    Vous verrez hello suivant la réponse :
   
    ![sortie Hello de hello nouvelle-azureservice et azurenodeworkerrolecmdlets ajouter](./media/cloud-services-nodejs-chat-app-socketio/socketio-1.png)

## <a name="download-hello-chat-example"></a>Télécharger hello Chat l’exemple
Pour ce projet, nous allons utiliser exemple hello conversation hello [référentiel GitHub de Socket.IO]. Effectuer hello étapes toodownload hello exemple suivant et l’ajouter projet toohello créé précédemment.

1. Créer une copie locale du référentiel de hello à l’aide de hello **Clone** bouton. Vous pouvez également utiliser hello **ZIP** projet de bouton toodownload hello.
   
   ![Une fenêtre de navigateur affichage https://github.com/LearnBoost/socket.io/tree/master/examples/chat, avec l’icône de téléchargement ZIP hello mis en surbrillance][chat-example-view]
2. Parcourir la structure de répertoire de hello du référentiel local de hello jusqu'à ce que vous arriviez à hello **exemples\\chat** active. Copier le contenu de hello de cette toothe active **C:\\nœud\\chatapp\\WorkerRole1** répertoire créé précédemment.
   
   ![Explorer, affichage du contenu des exemples de hello hello\\répertoire extraite à partir de l’archive de hello][chat-contents]
   
   Hello des éléments mis en surbrillance dans la capture d’écran hello ci-dessus sont des hello fichiers copiés à partir de hello **exemples\\chat** Active
3. Bonjour **C:\\nœud\\chatapp\\WorkerRole1** répertoire, delete hello **server.js** de fichiers, puis renommez hello **app.js**trop de fichiers**server.js**. Cela supprime la valeur par défaut hello **server.js** fichier créé précédemment par hello **Add-AzureNodeWorkerRole** applet de commande et de remplacement avec une application hello à partir du fichier hello exemple de la conversation.

### <a name="modify-serverjs-and-install-modules"></a>Modification du fichier Server.js et installation des modules
Avant l’application hello test Bonjour émulateur Azure, nous devons apporter de légères modifications. Effectuez hello étapes toothe server.js fichier suivant :

1. Ouvrez hello **server.js** fichier dans Visual Studio ou un éditeur de texte.
2. Recherche hello **les dépendances de modules** section au début de hello de server.js et modifier hello ligne contenant **sio = require('.. //.. lib//Socket.IO')** trop**sio = require('socket.io')** comme indiqué ci-dessous :
   
       var express = require('express')
         , stylus = require('stylus')
         , nib = require('nib')
       //, sio = require('..//..//lib//socket.io'); //Original
         , sio = require('socket.io');                //Updated
         var port = process.env.PORT || 3000;         //Updated
3. application de hello tooensure écoute le port correct hello, ouvrez server.js dans le bloc-notes ou votre éditeur favori, puis modifiez la ligne suivante en remplaçant **3000** avec **process.env.port** comme ci-dessous :
   
       //app.listen(3000, function () {            //Original
       app.listen(process.env.port, function () {  //Updated
         var addr = app.address();
         console.log('   app listening on http://' + addr.address + ':' + addr.port);
       });

Après avoir enregistré les modifications de hello trop**server.js**, utilisez hello comme suit pour installer les modules requis, puis tester application hello dans l’émulateur Azure :

1. À l’aide de **Azure PowerShell**, modifiez les répertoires toohello **C:\\nœud\\chatapp\\WorkerRole1** hello active et l’utilisation après la commande tooinstall hello modules requis par cette application :
   
       PS C:\node\chatapp\WorkerRole1> npm install
   
   Cela va installer les modules hello répertoriés dans le fichier de package.json hello. Une fois la commande hello terminée, vous devez voir s’afficher sortie similaire toothe :
   
   ![commande d’installation de sortie Hello de hello npm][The-output-of-the-npm-install-command]
2. Dans la mesure où cet exemple a été initialement une partie de hello référentiel GitHub de Socket.IO bibliothèque Socket.IO de hello fait directement référence dans le chemin d’accès relatif, Socket.IO n’est pas référencée dans le fichier du package.json hello, donc nous devons l’installer en émettant hello de commande suivante :
   
       PS C:\node\chatapp\WorkerRole1> npm install socket.io --save

### <a name="test-and-deploy"></a>Test et déploiement
1. Lancez l’émulateur de hello en émettant hello de commande suivante :
   
       PS C:\node\chatapp\WorkerRole1> Start-AzureEmulator -Launch
   
   > [!NOTE]
   > Si vous rencontrez des problèmes pour le lancement de l’émulateur, par ex. : Start-AzureEmulator : une erreur inattendue est survenue.  Détails : A rencontré un erreur inattendue hello communication objet, System.ServiceModel.Channels.ServiceChannel ne peut pas servir pour la communication car il est déjà hello état Faulted.
   
      réinstallez AzureAuthoringTools v 2.7.1 et AzureComputeEmulator v 2.7 : assurez-vous que la version correspond.
   >
   >


2. Ouvrez un navigateur et accédez trop**http://127.0.0.1**.
3. Lors de la fenêtre de navigateur hello s’ouvre, entrez le surnom et puis appuyez sur ENTRÉE.
   Cela vous permettra toopost messages comme un surnom spécifique. des fonctionnalités tootest multi-utilisateur, ouvrir des fenêtres de navigateur supplémentaires à l’aide de la même URL et entrez les surnoms différents.
   
   ![Deux fenêtres du navigateur affichant des messages de conversation instantanée des utilisateurs User1 et User2](./media/cloud-services-nodejs-chat-app-socketio/socketio-8.png)
4. Après l’application de test hello, arrêtez l’émulateur de hello en émettant la commande suivante :
   
       PS C:\node\chatapp\WorkerRole1> Stop-AzureEmulator
5. toodeploy tooAzure d’application hello, utilisez le **AzureServiceProject de publication** applet de commande. Par exemple :
   
       PS C:\node\chatapp\WorkerRole1> Publish-AzureServiceProject -ServiceName mychatapp -Location "East US" -Launch
   
   > [!IMPORTANT]
   > Être vraiment toouse un nom unique, sinon hello processus de publication échoue. Après la fin du déploiement de hello, navigateur de hello ouvrir et accédez toohello déployé service.
   > 
   > Si vous recevez une erreur indiquant que hello fourni de nom de l’abonnement n’existe pas dans hello importé le profil de publication, vous devez télécharger et importer le profil de publication hello pour votre abonnement avant de déployer tooAzure. Consultez hello **déploiement hello Application tooAzure** section [générer et déployer un tooan d’application Node.js Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)
   > 
   > 
   
   ![Une fenêtre de navigateur affichant service hello hébergé sur Azure][completed-app]
   
   > [!NOTE]
   > Si vous recevez une erreur indiquant que hello fourni de nom de l’abonnement n’existe pas dans hello importé le profil de publication, vous devez télécharger et importer le profil de publication hello pour votre abonnement avant de déployer tooAzure. Consultez hello **déploiement hello Application tooAzure** section [générer et déployer un tooan d’application Node.js Azure Cloud Service](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)
   > 
   > 

Votre application s'exécute à présent dans Azure, et peut transmettre des messages de conversation instantanée entre différents clients en utilisant Socket.IO.

> [!NOTE]
> Par souci de simplicité, cet exemple est limitée toochatting entre toohello connecté des utilisateurs même instance. Cela signifie que si le service de cloud computing hello crée deux instances de rôle de travail, les utilisateurs seulement pourront toochat avec d’autres utilisateurs connectés toohello même instance de rôle de travail. tooscale hello application toowork avec plusieurs instances de rôle, vous pouvez utiliser une technologie comme Service Bus tooshare hello Socket.IO stocker l’état entre les instances. Pour obtenir des exemples, consultez Bonjour dans les exemples d’utilisation de files d’attente du Bus de Service et des rubriques hello [Azure SDK pour Node.js GitHub référentiel](https://github.com/WindowsAzure/azure-sdk-for-node).
> 
> 

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous avez appris comment toocreate une application de base de conversation hébergés dans un Service Cloud Azure. toolearn toohost cette application dans un site Web Azure, voir [générer une Application de Chat Node.js avec Socket.IO sur un Site Web de Azure][chatwebsite].

Pour plus d’informations, consultez également hello [centre de développement Node.js](/develop/nodejs/).

[chatwebsite]: /develop/nodejs/tutorials/website-using-socketio/

[Azure SLA]: http://www.windowsazure.com/support/sla/
[Azure SDK for Node.js GitHub repository]: https://github.com/WindowsAzure/azure-sdk-for-node
[completed-app]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-10.png
[Azure SDK for Node.js]: https://www.windowsazure.com/develop/nodejs/
[Node.js Web Application]: https://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[référentiel GitHub de Socket.IO]: https://github.com/LearnBoost/socket.io/tree/0.9.14
[Azure Considerations]: #windowsazureconsiderations
[Hosting hello Chat Example in a Worker Role]: #hostingthechatexampleinawebrole
[Summary and Next Steps]: #summary
[powershell-menu]: ./media/cloud-services-nodejs-chat-app-socketio/azure-powershell-start.png

[chat example]: https://github.com/LearnBoost/socket.io/tree/master/examples/chat
[chat-example-view]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-22.png


[chat-contents]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-5.png
[The-output-of-the-npm-install-command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-7.png
[hello output of hello Publish-AzureService command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-9.png


