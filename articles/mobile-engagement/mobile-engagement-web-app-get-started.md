---
title: "aaaGet main d’Azure Mobile Engagement pour les applications Web | Documents Microsoft"
description: "Découvrez comment toouse Azure Mobile Engagement avec analytique et des notifications push pour les applications Web."
services: mobile-engagement
documentationcenter: Mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 04afe53a-4caf-4c80-bd75-20cc630cd75c
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: js
ms.topic: hero-article
ms.date: 06/01/2016
ms.author: piyushjo
ms.openlocfilehash: a84c96cac13bf3b85e72aef55da5c91693e1766c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-web-apps"></a>Prise en main d’Azure Mobile Engagement pour les applications web
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Cette rubrique vous montre comment toouse Azure Mobile Engagement toounderstand votre utilisation de l’application Web.

> [!NOTE]
> Hello Azure Mobile Engagement service mars 2018 est retirée et est actuellement que les clients tooexisting disponibles. Pour plus d’informations, consultez [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).

Ce didacticiel requiert hello qui suit :

* Visual Studio 2015 ou tout autre éditeur de votre choix
* [Kit de développement logiciel (SDK) web](http://aka.ms/P7b453)

Ce kit de développement Web est en version préliminaire et prend en charge Analytique moment hello uniquement et ne gère pas encore d’envoi de notifications push de navigateur ou dans l’application. 

> [!NOTE]
> toocomplete ce didacticiel, vous devez disposer d’un compte Azure actif. Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started).
> 
> 

## <a name="setup-mobile-engagement-for-your-web-app"></a>Configuration de Mobile Engagement pour votre application web
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Se connecter à votre serveur principal d’application toohello Mobile Engagement
Ce didacticiel présente une « intégration de base, » qui est hello ensemble minimal requis toocollect données.

Bien que vous pouvez suivre les étapes de hello avec n’importe quelle application web également créée en dehors de Visual Studio, nous allons créer une application web de base avec l’intégration de Visual Studio toodemonstrate hello. 

### <a name="create-a-new-web-app"></a>Créer une application web
Hello étapes suivantes supposent hello utilisation de Visual Studio 2015 bien que les étapes de hello sont similaires dans les versions antérieures de Visual Studio. 

1. Démarrez Visual Studio et Bonjour **accueil** écran, sélectionnez **nouveau projet**.
2. Dans la fenêtre contextuelle hello, sélectionnez **Web** -> **Application Web ASP.Net**. Renseignez application hello **nom**, **emplacement** et **nom de la Solution**, puis cliquez sur **OK**.
3. Bonjour **sélectionner un modèle** menu contextuel, sélectionnez **vide** sous **ASP.Net 4.5 modèles** et cliquez sur **OK**. 

Vous venez de créer un nouveau projet d’application Web vide dans lequel nous intégrera hello Kit de développement Web Azure Mobile Engagement.

### <a name="connect-your-app-toomobile-engagement-backend"></a>Se connecter à votre serveur principal d’application tooMobile Engagement
1. Créez un dossier appelé **javascript** dans votre solution et ajoutez hello Web SDK JS fichier **azure-engagement.js** dans celui-ci. 
2. Ajouter un nouveau fichier appelé **main.js** dans ce dossier hello suivant du code javascript. Vérifiez la chaîne de connexion que tooupdate hello. Cela `azureEngagement` objet sera utilisé tooaccess méthodes du Kit de développement Web. 
   
        var azureEngagement = {
            debug: true,
            connectionString: 'xxxxx'
        };
   
    ![Visual Studio avec des fichiers js][1]

## <a name="enable-real-time-monitoring"></a>Activer la surveillance en temps réel
Dans l’ordre toostart envoi de données et en garantissant que les utilisateurs de hello sont actifs, vous devez envoyer au moins une activité toohello Mobile Engagement principal. Une activité dans le contexte de hello d’une application web est une page web. 

1. Créer une nouvelle page appelée **home.html** dans votre solution et de la définir en tant que hello démarrage page pour votre application web. 
2. Inclure hello deux scripts JavaScript que nous ajoutés précédemment dans cette page en ajoutant suivant hello au sein de la balise body de hello. 
   
        <script type="text/javascript" src="javascript/main.js"></script>
        <script type="text/javascript" src="javascript/azure-engagement.js"></script>
3. Mettre à jour EngagementAgent hello corps de la balise toocall `startActivity` (méthode)
   
        <body onload="engagement.agent.startActivity('Home')">
4. Voici à quoi ressemblera le code de votre page **home.html** .
   
        <html>
        <head>
            ...
        </head>
        <body onload="engagement.agent.startActivity('Home')">
            <script type="text/javascript" src="javascript/main.js"></script>
            <script type="text/javascript" src="javascript/azure-engagement.js"></script>
        </body>
        </html>

## <a name="connect-app-with-real-time-monitoring"></a>Connexion d’application avec l’analyse en temps réel
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

  ![][2]

## <a name="extend-analytics"></a>Étendre l’analyse
Voici toutes les méthodes hello actuellement disponibles avec le Kit de développement logiciel Web que vous pouvez utiliser pour l’analytique :

1. Activités/pages web :
   
        engagement.agent.startActivity(name);
        engagement.agent.endActivity();
2. Événements
   
        engagement.agent.sendEvent(name, extras);
3. Erreurs
   
        engagement.agent.sendError(name, extras);
4. Travaux
   
        engagement.agent.startJob(name);
        engagement.agent.endJob(name);

<!-- Images. -->
[1]: ./media/mobile-engagement-web-app-get-started/visual-studio-solution-js.png
[2]: ./media/mobile-engagement-web-app-get-started/session.png

