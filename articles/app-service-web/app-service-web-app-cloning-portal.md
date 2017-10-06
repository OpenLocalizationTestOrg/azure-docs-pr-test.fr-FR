---
title: "aaaWeb clonage d’application à l’aide du portail Azure"
description: "Découvrez comment tooclone votre toonew d’applications Web des applications Web à l’aide du portail Azure."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 20b0ae4e-67e8-4bae-9d74-8a24dc445cce
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2016
ms.author: aelnably
ms.openlocfilehash: 605c4879f34d568e9981c34109f9496731c9ed18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-app-cloning-using-azure-portal"></a>Clonage de l’application Azure App Service à l’aide du portail Azure
Hello fonctionnalité dans de clonage [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) vous permet de facilement cloner application web existante applications tooa qui vient d’être créé dans une autre région ou dans hello même région. Cela permet aux clients toodeploy un nombre d’applications sur différentes régions rapidement et facilement.

Le clonage d’application n’est actuellement pris en charge que pour les plans de service d’application de niveau Premium. nouvelles utilisations de fonctionnalité Hello hello même limitations en tant que fonctionnalité de sauvegarde des applications Web, consultez [sauvegardez une application web dans Azure App Service](web-sites-backup.md).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="cloning-an-existing-app"></a>Clonage d’une application existante
l’application Hello web doit s’exécuter dans hello **Premium** mode afin que vous toocreate un clone de l’application web hello.

1. Bonjour [Azure Portal](https://portal.azure.com/), ouvrez le panneau de votre application web.
2. Cliquez sur **Outils**. Ensuite, dans hello **outils** panneau, cliquez sur **le clonage d’application**.
   
    ![][1]
   
   > [!NOTE]
   > Si l’application web hello n’est pas déjà hello **Premium** mode, vous recevrez un message indiquant les modes hello pris en charge pour le clonage de l’application. À ce stade, vous avez hello option tooselect **mise à niveau**.
   > 
   > 
3. Bonjour **le clonage d’application** panneau fournir un nom d’application web hello, groupe de ressources et un Plan App Service. Également hello utilisateur sera en mesure de toochoose si tooclone un nombre de paramètres de l’application web source ou non.
   
    ![][2]
4. Après avoir cliqué sur **créer** plate-forme de hello va commencer à travailler sur la création d’un clone de l’application web de source hello.

## <a name="cloning-an-existing-app-tooan-app-service-environment"></a>Le clonage d’un tooan d’application existant environnement App Service
Bonjour **le clonage d’application** panneau hello client dispose hello option toochoose un pool d’applications dans un environnement App Service existant.

## <a name="current-restrictions"></a>Restrictions actuelles
Cette fonctionnalité est actuellement en version préliminaire, nous travaillons tooadd nouvelles fonctionnalités au fil du temps, hello suivant liste sont hello restrictions connues sur la prise en charge actuelle de hello au clonage de l’application dans le portail Azure :

* Les paramètres d’Azure Traffic Manager ne sont pas clonés.
* Les paramètres de mise à l’échelle automatique ne sont pas clonés.
* Les paramètres de planification de sauvegarde ne sont pas clonés.
* Les paramètres de réseau virtuel ne sont pas clonés.
* Application Insights ne sont pas automatiquement définies sur l’application web de destination hello
* Les paramètres d’authentification simple ne sont pas clonés.
* Les paramètres d’extension Kudu ne sont pas clonés.
* Les règles TiP ne sont pas clonées.
* Les contenus de la base de données ne sont pas clonés.

### <a name="references"></a>Références
* [Clonage d’application web à l’aide de PowerShell](app-service-web-app-cloning.md)
* [Sauvegarde d’une application web dans Azure App Service](web-sites-backup.md)
* [Comment tooCreate un environnement App Service](app-service-web-how-to-create-an-app-service-environment.md)
* [Créer une application web dans un environnement App Service](app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [Introduction tooApp environnement de Service](app-service-app-service-environment-intro.md)

<!--Image references-->
[1]: ./media/app-service-web-app-cloning-portal/CloningBlade.png
[2]: ./media/app-service-web-app-cloning-portal/CloneSettings.png
