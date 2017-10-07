---
title: "aaaAdd stockage Azure à l’aide des Services connectés dans Visual Studio | Documents Microsoft"
description: "Ajouter une application de tooyour de stockage Azure en utilisant la boîte de dialogue hello Visual Studio ajouter des Services connectés"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 521ec044-ad4b-4828-8864-01decde2e758
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/26/2017
ms.author: kraigb
ms.openlocfilehash: 56b42063d86510b330e405108e28d50e6ba4da05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-azure-storage-by-using-visual-studio-connected-services"></a>Ajout de stockage Azure à l’aide des services connectés de Visual Studio
Avec Visual Studio, vous pouvez connecter des hello suivant tooAzure stockage à l’aide de hello **ajouter des Services connectés** boîte de dialogue :

- Service cloud C#
- Service mobile principal .NET
- Service ou site web ASP.NET
- Service Core ASP.NET
- Service de tâche web Azure 

Hello service connecté fonctionnalité ajoute toutes les références de hello nécessité et projet de tooyour de code de connexion et modifie vos fichiers de configuration de manière appropriée. 

Une fois terminé, hello **ajouter des Services connectés** boîte de dialogue affiche automatiquement la documentation détaillant les toostart requis étapes hello fonctionne avec le stockage d’objets blob, files d’attente et les tables.

## <a name="connect-tooazure-storage-using-hello-connected-services-dialog"></a>Se connecter tooAzure stockage à l’aide des Services connectés hello boîte de dialogue
1. Ouvrez votre projet dans Visual Studio.

1. Dans **l’Explorateur de solutions**, avec le bouton hello **Services connectés** nœud et, dans le menu contextuel de hello, sélectionnez **ajouter un Service connecté**.
   
    ![Ajouter un service connecté Azure](./media/vs-azure-tools-connected-services-storage/IC796702.png)

1. Bonjour **Services connectés** page, sélectionnez **stockage en Cloud avec le stockage Azure**.
   
    ![Ajouter le Stockage Azure](./media/vs-azure-tools-connected-services-storage/add-azure-storage.png)

1. Bonjour **Azure Storage** boîte de dialogue, sélectionnez un compte de stockage existant et sélectionnez **ajouter**.
   
    Si vous avez besoin de toocreate un compte de stockage, accédez toohello prochaine étape. Sinon, passez toostep 6.
    
    ![Ajouter tooproject de compte de stockage existant](./media/vs-azure-tools-connected-services-storage/select-azure-storage-account.png)

1. toocreate un compte de stockage : 
   
   1. Sélectionnez **créer un nouveau compte de stockage** bas hello de boîte de dialogue hello.

   1. Remplir hello **créer un compte de stockage** boîte de dialogue, puis sélectionnez **créer**.
      
       ![Nouveau compte de stockage Azure](./media/vs-azure-tools-connected-services-storage/create-storage-account.png)
      
   1. Hello lorsque **Azure Storage** boîte de dialogue s’affiche, le nouveau compte de stockage hello s’affiche dans la liste de hello. Sélectionnez le nouveau compte de stockage hello dans la liste de hello, puis sélectionnez **ajouter**.

1. Hello stockage service connecté s’affiche sous hello **références de Service** nœud de votre projet.
   
## <a name="how-your-project-is-modified"></a>Modifications apportées à votre projet
Lorsque vous avez terminé la boîte de dialogue hello, Visual Studio ajoute des références et modifie certains fichiers de configuration. modifications Hello varient selon le type de projet hello : 

- Projet ASP.NET : [Que s’est-il passé ? – Projets ASP.NET](http://go.microsoft.com/fwlink/p/?LinkId=513126)
- Projet Core ASP.NET : [Que s’est-il passé ? – Projets ASP.NET 5](http://go.microsoft.com/fwlink/p/?LinkId=513124) 
- Projet de service cloud (rôles web et de travail) : [Que s’est-il passé ? – Projets de service cloud](http://go.microsoft.com/fwlink/p/?LinkId=516965)
- Projets de tâche web - [Que s’est-il passé ? – Projets de tâche web](visual-studio/vs-storage-webjobs-what-happened.md)

## <a name="next-steps"></a>Étapes suivantes
- [Forum MSDN : Stockage Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)
- [Blog de l’équipe Stockage Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/)
- [Documentation d’Azure Storage](https://docs.microsoft.com/azure/storage/)
