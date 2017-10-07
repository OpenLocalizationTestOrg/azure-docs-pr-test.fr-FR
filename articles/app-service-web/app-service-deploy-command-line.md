---
title: "déploiement aaaAutomate de votre application Azure avec des outils de ligne de commande | Documents Microsoft"
description: "Découvrir des informations sur la façon dont vous pouvez déployer votre application Azure hello de ligne de commande"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 8b65980c-eb75-44a2-8e0f-f9eb9e617d16
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2017
ms.author: cephalin
ms.openlocfilehash: 3df66cc4bf4e6819ed0eee7278ac79dca2e5daa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-deployment-of-your-azure-app-with-command-line-tools"></a>Automatiser le déploiement de votre application Azure avec les outils en ligne de commande
Vous pouvez automatiser le déploiement de votre application Azure avec les outils en ligne de commande. Cet article répertorie les outils disponibles et les liens utiles hello qui vous montrent comment toouse dans votre flux de travail de déploiement. 

## <a name="msbuild"></a>Automatiser le déploiement avec MSBuild
Si vous utilisez hello [IDE de Visual Studio](#vs) pour le développement, vous pouvez utiliser [MSBuild](http://msbuildbook.com/) tooautomate vous pouvez faire dans votre IDE. Vous pouvez configurer des MSBuild toouse [Web Deploy](#webdeploy) ou [FTP/FTPS](#ftp) toocopy fichiers. Web Deploy peut également automatiser de nombreuses autres tâches de déploiement, comme le déploiement des bases de données.

Pour plus d’informations sur le déploiement de ligne de commande à l’aide de MSBuild, consultez hello suivant des ressources :

* [Déploiement Web ASP.NET en utilisant Visual Studio : déploiement en ligne de commande](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/command-line-deployment)(en anglais). Dixième dans une série de didacticiels sur tooAzure de déploiement à l’aide de Visual Studio. Montre comment toouse hello toodeploy de ligne de commande après avoir configuré des profils de publication dans Visual Studio.
* [À l’intérieur hello Microsoft Build Engine : à l’aide de MSBuild et Team Foundation Build](http://msbuildbook.com/). Livre de papier qui inclut les chapitres sur la façon de toouse MSBuild pour le déploiement.

## <a name="powershell"></a>Automatiser le déploiement avec Windows PowerShell
Vous pouvez utiliser des fonctions de déploiement MSBuild ou FTP à partir de [Windows PowerShell](http://msdn.microsoft.com/library/dd835506.aspx). Si vous procédez ainsi, vous pouvez également utiliser une collection d’applets de commande Windows PowerShell qui rendent toocall facile de hello Azure REST gestion des API.

Pour plus d’informations, consultez hello suivant des ressources :

* [Déployer un référentiel GitHub de web application lié tooa](app-service-web-arm-from-github-provision.md)
* [Mettre en service une application Web avec une base de données SQL](app-service-web-arm-with-sql-database-provision.md)
* [Mise en service et déploiement de microservices de manière prévisible dans Azure](app-service-deploy-complex-application-predictably.md)
* [Tout automatiser (développement d'applications de cloud concrètes avec Azure)](http://asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything). Chapitre livres qui explique comment exemple d’application hello indiqué dans le livre électronique hello utilise toocreate de scripts Windows PowerShell Azure environnement de test et déployez tooit. Consultez hello [ressources](http://asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything#resources) section pour les liens tooadditional documentation Azure PowerShell.
* [À l’aide d’environnements de Test et les Scripts Windows PowerShell tooPublish tooDev](../vs-azure-tools-publishing-using-powershell-scripts.md). Comment toouse le déploiement de Windows PowerShell scripts que Visual Studio génère.

## <a name="api"></a>Automatiser le déploiement avec l’API de gestion .NET
Vous pouvez écrire du code c# tooperform les fonctions de MSBuild ou FTP pour le déploiement. Si vous procédez ainsi, vous pouvez accéder de fonctions de gestion de site hello Azure management REST API tooperform.

Pour plus d’informations, consultez hello suivant des ressources :

* [Automatisation de tous les éléments avec les bibliothèques de gestion Azure hello et .NET](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx). Introduction toohello .NET API et des liens toomore documentation de gestion.

## <a name="cli"></a>Déploiement à partir de l’interface de ligne de commande Azure
Vous pouvez utiliser la ligne de commande hello dans toodeploy des ordinateurs Windows, Mac ou Linux à l’aide de FTP. Si vous procédez ainsi, vous pouvez également accéder aux API de gestion Azure REST hello hello CLI d’Azure à l’aide de.

Pour plus d’informations, consultez hello suivant des ressources :

* [Outils en ligne de commande Azure](https://azure.microsoft.com/downloads/). Page du portail Azure.com qui fournit des informations sur les outils en ligne de commande.

## <a name="webdeploy"></a>Déploiement à partir de la ligne de commande Web Deploy
[Web Deploy](http://www.iis.net/downloads/microsoft/web-deploy) est un logiciel Microsoft pour tooIIS de déploiement qui ne fournit pas seulement des fichiers intelligent fonctionnalités de synchronisation, mais également effectuer ou coordonner de nombreuses autres tâches liées au déploiement qui ne peut pas être automatisées quand vous utilisez FTP. Par exemple, Web Deploy peut déployer une nouvelle base de données ou mettre à jour une base de données existante avec votre application web. Web Deploy peut également réduire hello durée tooupdate un site existant dans la mesure où il peut copier intelligemment uniquement les fichiers modifiés. Microsoft Visual Studio et Team Foundation Server ont prise en charge de Web Deploy intégrés, mais vous pouvez également utiliser Web Deploy directement à partir de déploiement de tooautomate de ligne de commande hello. Commandes de déploiement Web sont très puissants mais hello courbe d’apprentissage peut être difficile.

## <a name="more-resources"></a>Autres ressources
Automatisation de ligne toocommand un autre déploiement option est toouse basée sur un cloud service tel que [multiple déployer](http://en.wikipedia.org/wiki/Octopus_Deploy). Pour plus d’informations, consultez [tooAzure d’applications ASP.NET de déployer des Sites Web](https://octopusdeploy.com/blog/deploy-aspnet-applications-to-azure-websites).

Pour plus d’informations sur les outils de ligne de commande, consultez hello suivant de ressource :

* [Web Apps en toute simplicité : déploiement](https://azure.microsoft.com/blog/2014/07/28/simple-azure-websites-deployment/)(en anglais). Blog de David Ebbo sur un outil, il a écrit toomake il plus facile toouse Web Deploy.
* [Outils de déploiement Web](http://technet.microsoft.com/library/dd568996). Documentation officielle sur site de Microsoft TechNet hello. Date d’effet, mais toujours un toostart parfait.
* [Utilisation de Web Deploy](http://www.iis.net/learn/publish/using-web-deploy). Documentation officielle sur site de Microsoft IIS.NET hello. Date d’effet également, mais un toostart parfait.
* [Déploiement Web ASP.NET en utilisant Visual Studio : déploiement en ligne de commande](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/command-line-deployment)(en anglais). MSBuild est hello générer moteur utilisé par Visual Studio, et il peut également servir à partir du web applications tooWeb applications hello ligne de commande toodeploy. Ce didacticiel fait partie d'une série traitant principalement des déploiements Visual Studio.

