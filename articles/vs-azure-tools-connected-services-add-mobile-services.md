---
title: "Ajout de Mobile Services à l’aide des services connectés dans Visual Studio | Microsoft Docs"
description: "Ajouter Mobile Services à partir de la boîte de dialogue Ajouter des services connectés dans Visual Studio"
services: visual-studio-online
documentationcenter: na
author: mlhoop
manager: douge
editor: 
ms.assetid: 75c3cb93-88e1-476d-a416-f34caa3608e3
ms.service: visual-studio-online
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: mobile
ms.date: 12/16/2015
ms.author: mlearned
ms.openlocfilehash: d185fdafebad56f8970e390b2a0672c3fb84df8f
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="adding-mobile-services-by-using-visual-studio-connected-services"></a>Ajout de Mobile Services à l’aide des services connectés de Visual Studio
Avec Visual Studio 2015, vous pouvez vous connecter à Azure Mobile Services à partir de la boîte de dialogue **Ajouter un service connecté** . Vous pouvez établir une connexion de n’importe quelle application cliente C#, application JavaScript ou application interplateforme Cordova. Une fois connecté, vous pouvez créer et utiliser des données, créer des API personnalisées et des tâches planifiées, et ajouter la prise en charge des notifications Push.  Les services connectés ajoutent toutes les références et le code de connexion appropriés. Vous pouvez également tirer parti de la prise en charge intégrée de l’authentification avec de nombreux schémas d’identité courants, par exemple les comptes Azure AD, Facebook, Twitter et Microsoft.

## <a name="supported-project-types"></a>Types de projet pris en charge
> [!NOTE]
> Dans Visual Studio 2015, vous ne pouvez pas ajouter Azure Mobile Services à des projets Windows Universal (Windows 10) à partir de la boîte de dialogue Ajouter des services connectés. Vous pouvez le faire en installant les packages appropriés à l’aide du gestionnaire de package NuGet pour votre projet.
> 
> 

L’utilisation de la boîte de dialogue Services connectés vous permet de vous connecter à Azure Mobile Services pour les types de projet suivants.

* Projets d’applications Store, Phone et universelles Windows 8.1 .NET
* Projets d’applications Store, Phone et universelles Windows 8.1 JavaScript
* Projets créés à l’aide de Visual Studio Tools pour Apache Cordova

## <a name="connect-to-azure-mobile-services-using-the-add-connected-services-dialog"></a>Connexion à Azure Mobile Services à partir de la boîte de dialogue Ajouter des services connectés
1. Assurez-vous que vous disposez d’un compte Azure. Si vous n’en avez pas, vous pouvez demander un [essai gratuit](http://go.microsoft.com/fwlink/?LinkId=518146).
2. Ouvrez la boîte de dialogue **Ajouter des services connectés** .
   
   * Pour les applications .NET, ouvrez votre projet dans Visual Studio, ouvrez le menu contextuel du nœud **Références** dans l’Explorateur de solutions, puis choisissez **Ajouter un service connecté**.
     
        ![Connexion au service Azure Mobile](./media/vs-azure-tools-connected-services-add-mobile-services/IC797635.png)
   * Pour les projets d’application Apache Cordova, ouvrez votre projet dans Visual Studio, ouvrez le menu contextuel du nœud du projet dans l’Explorateur de solutions, puis choisissez **Ajouter un service connecté**.
3. Dans la boîte de dialogue **Ajouter un service connecté**, choisissez **Azure Mobile Services**, puis choisissez le bouton **Configurer**. Si vous n’êtes pas encore connecté à Azure, vous serez invité à le faire.
   
    ![Ajout d’un service Azure Mobile Service](./media/vs-azure-tools-connected-services-add-mobile-services/IC797636.png)
4. Dans la boîte de dialogue **Azure Mobile Services** , choisissez un service mobile existant. Si vous devez créer un service mobile Azure, suivez la procédure ci-dessous. Sinon, passez à l’étape suivante.
   
    Pour créer un compte de service mobile :
   
   1. Sélectionnez le lien **Créer un service** situé au bas de la boîte de dialogue.
       ![Ajouter un nouveau service connecté mobile](./media/vs-azure-tools-connected-services-add-mobile-services/IC797637.png)
   2. Dans la boîte de dialogue **Créer un service mobile**, choisissez un service mobile principal JavaScript ou .NET dans la liste déroulante **Runtime**. 
      
       ![Création d’un service mobile](./media/vs-azure-tools-connected-services-add-mobile-services/IC797638.png)
      
       Le service principal JavaScript est simple et puissant. Si vous créez un service mobile principal JavaScript, le code JavaScript côté serveur est stocké dans le cloud, mais vous pouvez modifier les scripts serveur dans l’Explorateur de serveurs ou sur le portail de gestion Azure. 
      
       Le service mobile principal .NET vous offre la puissance et la flexibilité de l’API web et d’Entity Framework. Si vous créez un service mobile principal .NET, un projet est automatiquement créé et ajouté à votre solution. 
   3. Choisissez la **région** où vous souhaitez créer le service mobile, puis entrez un nom d’utilisateur et un mot de passe pour le serveur.
   4. Quand vous avez entré toutes les informations nécessaires, choisissez le bouton **Créer** pour créer le service mobile.
   5. Le nouveau service mobile doit d’afficher dans la liste des services de la boîte de dialogue **Azure Mobile Services** . Choisissez le nouveau service mobile dans la liste, puis choisissez le bouton **Ajouter** pour ajouter le service à votre projet.
5. Dans la page Prise en main qui s’affiche, examinez de quelle manière votre projet a été modifié. Cette page s’affiche dans votre navigateur quand vous ajoutez un service connecté. Vous pouvez parcourir les étapes suggérées et les exemples de code fournis, ou bien afficher la page Qu’est-il arrivé à mon projet pour voir quelles références ont été ajoutées à votre projet et quelles modifications ont été apportées à vos fichiers de code et de configuration.
6. En vous aidant des exemples de code fournis, commencez à écrire le code d’accès à votre service mobile.

## <a name="how-your-project-is-modified"></a>Modifications apportées à votre projet
Visual Studio modifie votre projet différemment selon le type du projet. Pour les applications clientes C#, consultez [Qu’est-il arrivé à mon projet (C#)](http://go.microsoft.com/fwlink/p/?LinkId=513119). Pour les applications clientes JavaScript, consultez [Qu’est-il arrivé à mon projet (JavaScript)](http://go.microsoft.com/fwlink/p/?LinkId=513120). Pour les applications Cordova, consultez [Qu’est-il arrivé à mon projet (Cordova)](http://go.microsoft.com/fwlink/p/?LinkId=513116).

## <a name="next-steps"></a>Étapes suivantes
Posez des questions et obtenez de l’aide : 

* [Forum MSDN : Azure Mobile Services](https://social.msdn.microsoft.com/forums/azure/home?forum=azuremobile)
* [Azure Mobile Services sur le blog de l’équipe Microsoft Azure](https://azure.microsoft.com/blog/topics/mobile/)
* [Azure Mobile Services sur azure.microsoft.com](https://azure.microsoft.com/services/mobile-services/)
* [Documentation Azure Mobile Services sur azure.microsoft.com](https://azure.microsoft.com/documentation/services/mobile-services/)

