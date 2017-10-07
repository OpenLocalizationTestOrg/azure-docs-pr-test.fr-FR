---
title: "aaaAdding Services mobiles à l’aide des Services connectés dans Visual Studio | Documents Microsoft"
description: "Ajouter des Services mobiles à l’aide de boîte de dialogue hello Visual Studio ajouter des Services connectés"
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
ms.openlocfilehash: c47b6fb63dc99fbc012e1c627c6c7e95249de7a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-mobile-services-by-using-visual-studio-connected-services"></a>Ajout de Mobile Services à l’aide des services connectés de Visual Studio
Avec Visual Studio 2015, vous pouvez vous connecter tooAzure Mobile Services à l’aide de hello **ajouter un Service connecté** boîte de dialogue. Vous pouvez établir une connexion de n’importe quelle application cliente C#, application JavaScript ou application interplateforme Cordova. Une fois connecté, vous pouvez créer et utiliser des données, créer des API personnalisées et des tâches planifiées, et ajouter la prise en charge des notifications Push.  Hello services connectés opération ajoute toutes les références appropriées et le code de connexion. Vous pouvez également tirer parti de la prise en charge intégrée de l’authentification avec de nombreux schémas d’identité courants, par exemple les comptes Azure AD, Facebook, Twitter et Microsoft.

## <a name="supported-project-types"></a>Types de projet pris en charge
> [!NOTE]
> Dans Visual Studio 2015, l’ajout de projets Windows universel (Windows 10) de Azure Mobile Services tooa en utilisant la boîte de dialogue Ajouter des Services connectés hello n’est pas pris en charge. Vous pouvez ajouter des Services mobiles Azure en installant les packages appropriés hello utilisant hello Gestionnaire de Package NuGet pour votre projet.
> 
> 

Vous pouvez utiliser la boîte de dialogue tooconnect tooAzure Services mobiles hello Services connectés dans hello les types de projet suivants.

* Projets d’applications Store, Phone et universelles Windows 8.1 .NET
* Projets d’applications Store, Phone et universelles Windows 8.1 JavaScript
* Projets créés à l’aide de Visual Studio Tools pour Apache Cordova

## <a name="connect-tooazure-mobile-services-using-hello-add-connected-services-dialog"></a>Se connecter à l’aide de la boîte de dialogue Ajouter des Services connectés hello de tooAzure Mobile Services
1. Assurez-vous que vous disposez d’un compte Azure. Si vous n’en avez pas, vous pouvez demander un [essai gratuit](http://go.microsoft.com/fwlink/?LinkId=518146).
2. Ouvrez hello **ajouter des Services connectés** boîte de dialogue.
   
   * Pour les applications .NET, ouvrez votre projet dans Visual Studio, le menu contextuel Ouvrir hello hello **références** nœud dans l’Explorateur de solutions, puis choisissez **ajouter un Service connecté**
     
        ![Connexion tooAzure Service Mobile](./media/vs-azure-tools-connected-services-add-mobile-services/IC797635.png)
   * Pour les projets d’application Apache Cordova, ouvrez votre projet dans Visual Studio, le menu contextuel de hello ouvrir hello nœud de projet dans l’Explorateur de solutions, puis **ajouter un Service connecté**.
3. Bonjour **ajouter un Service connecté** boîte de dialogue, choisissez **Azure Mobile Services**, puis choisissez hello **configurer** bouton. Vous pouvez être invité à toolog dans Azure si vous n’avez pas déjà fait.
   
    ![Ajout d’un service Azure Mobile Service](./media/vs-azure-tools-connected-services-add-mobile-services/IC797636.png)
4. Bonjour **Azure Mobile Services** boîte de dialogue, choisissez un service mobile existant si vous en avez. Si vous avez besoin d’un nouveau service mobile Azure de toocreate, procédure hello ci-dessous toodo donc. Sinon, passez toohello prochaine étape.
   
    toocreate un nouveau compte de service mobile :
   
   1. Choisissez hello ** Create Service ** lien en bas de hello de boîte de dialogue hello.
       ![Ajouter un nouveau service connecté mobile](./media/vs-azure-tools-connected-services-add-mobile-services/IC797637.png)
   2. Sur hello **créer un Service Mobile** boîte de dialogue, vous pouvez choisir un service mobile principal de JavaScript, ou un service mobile principal de .NET à partir de hello **Runtime** liste déroulante. 
      
       ![Création d’un service mobile](./media/vs-azure-tools-connected-services-add-mobile-services/IC797638.png)
      
       Le service principal JavaScript est simple et puissant. Si vous créez un service mobile principal de JavaScript, du code JavaScript côté serveur hello est stocké dans le cloud de hello, mais vous pouvez modifier les scripts serveur à l’aide de l’Explorateur de serveurs ou le portail de gestion Azure hello. 
      
       Service mobile principal .NET vous donne hello puissance et la flexibilité de l’API Web et Entity Framework. Si vous créez un service de mobile principal .NET, un projet est créé et ajouté tooyour solution. 
   3. Choisissez hello **région** où les services mobiles hello et puis entrez un nom d’utilisateur et un mot de passe pour le serveur de hello.
   4. Une fois que vous avez entré toutes les informations de hello requises, choisissez hello **créer** bouton service mobile de toocreate hello.
   5. nouveau service de mobile Hello doit apparaître dans la liste service hello hello **Azure Mobile Services** boîte de dialogue. Choisissez un nouveau service de mobile hello dans la liste de hello, puis hello **ajouter** le projet tooyour service button tooadd hello.
5. Révision hello route page qui s’affiche et découvrez comment votre projet a été modifié. Cette page s’affiche dans votre navigateur quand vous ajoutez un service connecté. Vous pouvez passer en revue hello étapes suggérées et les exemples de code, ou basculez toohello que s’est-il passé page toosee quelles références ont été ajoutées tooyour projet, et comment vos fichiers de code et la configuration ont été modifiés.
6. À l’aide des exemples de code hello comme guide, démarrer l’écriture de code tooaccess votre service mobile !

## <a name="how-your-project-is-modified"></a>Modifications apportées à votre projet
Comment Visual Studio modifie votre projet dépend du type de projet hello. Pour les applications clientes C#, consultez [Qu’est-il arrivé à mon projet (C#)](http://go.microsoft.com/fwlink/p/?LinkId=513119). Pour les applications clientes JavaScript, consultez [Qu’est-il arrivé à mon projet (JavaScript)](http://go.microsoft.com/fwlink/p/?LinkId=513120). Pour les applications Cordova, consultez [Qu’est-il arrivé à mon projet (Cordova)](http://go.microsoft.com/fwlink/p/?LinkId=513116).

## <a name="next-steps"></a>Étapes suivantes
Posez des questions et obtenez de l’aide : 

* [Forum MSDN : Azure Mobile Services](https://social.msdn.microsoft.com/forums/azure/home?forum=azuremobile)
* [Azure Mobile Services à hello Blog de l’équipe Microsoft Azure](https://azure.microsoft.com/blog/topics/mobile/)
* [Azure Mobile Services sur azure.microsoft.com](https://azure.microsoft.com/services/mobile-services/)
* [Documentation Azure Mobile Services sur azure.microsoft.com](https://azure.microsoft.com/documentation/services/mobile-services/)

