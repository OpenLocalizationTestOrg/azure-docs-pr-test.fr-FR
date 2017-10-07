---
title: aaaNode.js Getting Started Guide | Documents Microsoft
description: "Découvrez comment toocreate un Node.js simple application web et service de cloud Azure tooan le déployer."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 50951a87-fed4-48e0-bcfa-453b9e50452e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 22945bfcc1b0e5da2a2d37dc5cc86be013cc0b5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-a-nodejs-application-tooan-azure-cloud-service"></a>Créer et déployer un tooan d’application Node.js Azure Cloud Service

Ce didacticiel montre comment toocreate un Node.js simple application qui s’exécute dans un Service Cloud Azure. Services de cloud computing sont les blocs de construction de hello d’applications cloud évolutives dans Azure. Elles permettent de séparation de hello et gestion indépendante et montée en puissance parallèle de serveurs frontaux et principaux composants de votre application.  Cloud Services héberge de façon fiable chaque rôle sur une machine virtuelle dédiée.

Pour plus d’informations sur les Services de cloud computing et leurs particularités tooAzure sites Web et les machines virtuelles, consultez [comparaison de sites Web Azure, Services de cloud computing et Machines virtuelles].

> [!TIP]
> Recherchez toobuild un site Web simple ? Si votre scénario ne comporte qu’un simple composant frontal web, envisagez d’[utiliser une application web légère]. Vous pouvez facilement mettre à niveau tooa Service de cloud computing que votre application web se développe et l’évolution de vos besoins.

Dans ce didacticiel, vous allez créer une application Web simple, hébergée dans un rôle Web. Vous serez utiliser, hello calcul émulateur tootest votre application localement, puis déployez-la à l’aide des outils de ligne de commande PowerShell.

application Hello est une application « hello world » simple :

![Un navigateur web affichage page web de Hello World hello][A web browser displaying hello Hello World web page]

## <a name="prerequisites"></a>Composants requis
> [!NOTE]
> Ce didacticiel utilise Azure PowerShell, qui nécessite Windows.

* Installez et configurez [Azure PowerShell].
* Téléchargez et installez hello [Azure SDK pour .NET 2.7]. Bonjour, installer le programme d’installation, sélectionnez :
  * MicrosoftAzureAuthoringTools
  * MicrosoftAzureComputeEmulator

## <a name="create-an-azure-cloud-service-project"></a>Créer un projet Azure Cloud Services
Effectuez hello suivant de tâches toocreate un nouveau projet de Service Cloud Azure, ainsi que la structure de Node.js base :

1. Exécutez **Windows PowerShell** en tant qu’administrateur ; à partir de hello **Menu Démarrer** ou **écran d’accueil de**, recherchez **Windows PowerShell**.
2. [Se connecter à PowerShell] tooyour abonnement.
3. Entrez hello suivant le projet hello toocreate PowerShell applet de commande toocreate :

        New-AzureServiceProject helloworld

    ![résultat de Hello de commande de helloworld hello New-AzureService][hello result of hello New-AzureService helloworld command]

    Hello **New-AzureServiceProject** applet de commande génère une structure de base pour la publication d’un tooa d’application Node.js Service Cloud. Il contient les fichiers de configuration nécessaires à la publication tooAzure. applet de commande Hello change également votre répertoire toohello répertoire de travail hello service.

    applet de commande Hello crée hello fichiers suivants :

   * **ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** et **ServiceDefinition.csdef** sont des fichiers propres à Azure, nécessaires à la publication de votre application. Pour plus d'informations, consultez la page [Présentation de la création d'un service hébergé pour Azure].
   * **deploymentSettings.json**: stocke les paramètres locaux qui sont utilisés par hello applets de commande de déploiement Azure PowerShell.
4. Entrez hello suivant commande tooadd un nouveau rôle web :

       Add-AzureNodeWebRole

   ![sortie Hello Hello Add-AzureNodeWebRole commande][hello output of hello Add-AzureNodeWebRole command]

   Hello **Add-AzureNodeWebRole** applet de commande crée une application Node.js base. Il modifie également hello **.csfg** et **.csdef** fichiers tooadd les entrées de configuration pour le nouveau rôle de hello.

   > [!NOTE]
   > Si vous ne spécifiez pas de nom de rôle, un nom par défaut est utilisé. Vous pouvez fournir un nom en tant que paramètre d’applet de commande premier hello :`Add-AzureNodeWebRole MyRole`

application de Node.js Hello est définie dans le fichier de hello **server.js**, situé dans le répertoire hello pour le rôle web de hello (**WebRole1** par défaut). Voici le code de hello :

    var http = require('http');
    var port = process.env.port || 1337;
    http.createServer(function (req, res) {
        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end('Hello World\n');
    }).listen(port);

Ce code est essentiellement les hello identique hello « Hello World » exemple sur hello [nodejs.org] site Web, sauf qu’elle utilise le numéro de port hello affecté par l’environnement de cloud hello.

## <a name="deploy-hello-application-tooazure"></a>Déployer hello application tooAzure

> [!NOTE]
> toocomplete ce didacticiel, vous avez besoin d’un compte Azure. Vous pouvez [activer les avantages de votre abonnement MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) ou [vous inscrire pour un compte gratuit](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).

### <a name="download-hello-azure-publishing-settings"></a>Télécharger hello Azure paramètres de publication
toodeploy tooAzure de votre application, vous devez d’abord télécharger hello pour votre abonnement Azure, les paramètres de publication.

1. Exécutez hello suivant l’applet de commande PowerShell de Azure :

       Get-AzurePublishSettingsFile

   Ce processus utilisera votre navigateur toonavigate toohello page de téléchargement des paramètres de publication. Vous pouvez être invité à toolog avec un Account Microsoft. Dans ce cas, utilisez le compte hello associé à votre abonnement Azure.

   Vous pouvez accéder facilement à hello téléchargé profil tooa fichier emplacement d’enregistrement.
2. Exécutez suivante hello de tooimport d’applet de commande profil que vous avez téléchargé de publication :

       Import-AzurePublishSettingsFile [path toofile]

    > [!NOTE]
    > Après l’importation hello paramètres de publication, envisagez de suppression hello de télécharger le fichier .publishSettings, car il contient des informations qui pourrait permettre à une personne tooaccess votre compte.

### <a name="publish-hello-application"></a>Publier l’application hello
toopublish, exécutez hello suivant de commandes :

      $ServiceName = "NodeHelloWorld" + $(Get-Date -Format ('ddhhmm'))
    Publish-AzureServiceProject -ServiceName $ServiceName  -Location "East US" -Launch

* **-ServiceName** Spécifie le nom hello pour le déploiement de hello. Cela doit être un nom unique, sinon hello publier le processus échoue. Hello **Get-Date** commande s’attache à une chaîne de date/heure qui doit rendre le nom de hello unique.
* **-Location** spécifie hello de centre de données qui sera hébergée dans application hello. toosee une liste des centres de données disponibles, utilisez hello **Get-AzureLocation** applet de commande.
* **-Lancer** ouvre une fenêtre de navigateur et navigue toohello hébergé service après le déploiement est terminé.

Une fois la publication effectuée, vous découvrez une réponse similaire toohello :

![sortie Hello Hello Publish-AzureService commande][hello output of hello Publish-AzureService command]

> [!NOTE]
> Il peut prendre plusieurs minutes pour hello application toodeploy et sont disponible lors de la première publication.

Une fois le déploiement de hello est terminée, une fenêtre de navigateur vous ouvrez et accédez toohello le service cloud.

![Une fenêtre de navigateur affichant hello hello world page ; URL de Hello indique la page de hello est hébergé sur Azure.][A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]

Votre application s'exécute maintenant sur Azure.

Hello **AzureServiceProject de publication** applet de commande effectue hello comme suit :

1. Crée un toodeploy du package. Hello contient tous les fichiers hello dans votre dossier d’application.
2. Elle crée un **compte de stockage** , si celui-ci n'existe pas. Hello compte de stockage Azure est un package d’application hello toostore utilisés pendant le déploiement. Vous pouvez supprimer en toute sécurité de compte de stockage hello après le déploiement.
3. Elle crée un **service cloud** , si celui-ci n'existe pas. A **service de cloud computing** est conteneur hello dans lequel votre application est hébergée lorsqu’il est déployé tooAzure. Pour plus d'informations, consultez la page [Présentation de la création d'un service hébergé pour Azure].
4. Publie tooAzure de package de déploiement hello.

## <a name="stopping-and-deleting-your-application"></a>Arrêt et suppression de votre application
Après avoir déployé votre application, vous souhaiterez peut-être toodisable il afin d’éviter des coûts supplémentaires. Azure facture les instances de rôle Web par heure de serveur consommée. Heure du serveur est utilisée une fois que votre application est déployée, même si les instances de hello ne sont pas en cours d’exécution et état de hello s’est arrêté.

1. Dans la fenêtre Windows PowerShell de hello, arrêter le déploiement de service hello créé dans la section précédente de hello avec hello suivant l’applet de commande :

       Stop-AzureService

   L’arrêt du service de hello peut prendre plusieurs minutes. Lors de l’arrêt du service de hello, vous recevez un message indiquant qu’il s’est arrêtée.

   ![état Hello de commande hello Stop-AzureService][hello status of hello Stop-AzureService command]
2. service de hello toodelete, hello appel suivant l’applet de commande :

       Remove-AzureService

   Lorsque vous y êtes invité, entrez **Y** service de hello toodelete.

   Suppression du service de hello peut prendre plusieurs minutes. Une fois que le service de hello a été supprimé, vous recevez un message indiquant que le service de hello a été supprimée.

   ![état Hello de commande Remove-AzureService de hello][hello status of hello Remove-AzureService command]

   > [!NOTE]
   > Suppression du service de hello ne supprime pas le compte de stockage hello qui a été créé lorsque hello service a été initialement publié, et vous continuerez toobe facturé en fonction de stockage utilisé. Si rien d’autre utilise le stockage de hello, vous souhaiterez peut-être toodelete il.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations, consultez hello [centre de développement Node.js].

<!-- URL List -->

[comparaison de sites Web Azure, Services de cloud computing et Machines virtuelles]: ../app-service-web/choose-web-site-cloud-service-vm.md
[utiliser une application web légère]: ../app-service-web/app-service-web-get-started-nodejs.md
[Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Azure SDK pour .NET 2.7]: http://www.microsoft.com/en-us/download/details.aspx?id=48178
[Se connecter à PowerShell]: /powershell/azureps-cmdlets-docs#step-3-connect
[nodejs.org]: http://nodejs.org/
[Présentation de la création d'un service hébergé pour Azure]: https://azure.microsoft.com/documentation/services/cloud-services/
[centre de développement Node.js]: https://azure.microsoft.com/develop/nodejs/

<!-- IMG List -->

[hello result of hello New-AzureService helloworld command]: ./media/cloud-services-nodejs-develop-deploy-app/node9.png
[hello output of hello Add-AzureNodeWebRole command]: ./media/cloud-services-nodejs-develop-deploy-app/node11.png
[A web browser displaying hello Hello World web page]: ./media/cloud-services-nodejs-develop-deploy-app/node14.png
[hello output of hello Publish-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node19.png
[A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]: ./media/cloud-services-nodejs-develop-deploy-app/node21.png
[hello status of hello Stop-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node48.png
[hello status of hello Remove-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node49.png
