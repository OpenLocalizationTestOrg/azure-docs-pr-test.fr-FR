---
title: "Ajouter Azure Storage à l’aide des services connectés dans Visual Studio | Microsoft Docs"
description: "Ajouter le stockage Azure à votre application à l’aide de la boîte de dialogue Ajouter des services connectés de Visual Studio"
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
ms.openlocfilehash: 35638083cd75e1b751d00a9c8163a3bc7480f0cd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="adding-azure-storage-by-using-visual-studio-connected-services"></a>Ajout de stockage Azure à l’aide des services connectés de Visual Studio
Avec Visual Studio, vous pouvez connecter les éléments suivants au Stockage Azure à l’aide de la boîte de dialogue **Ajouter des services connectés** :

- Service cloud C#
- Service mobile principal .NET
- Service ou site web ASP.NET
- Service Core ASP.NET
- Service de tâche web Azure 

La fonctionnalité de service connecté ajoute l’ensemble des références et du code de connexion nécessaires à votre projet, et modifie vos fichiers de configuration de manière appropriée. 

Une fois cette opération terminée, la boîte de dialogue **Ajouter des services connectés** affiche automatiquement une documentation décrivant les étapes nécessaires pour commencer à travailler avec le Stockage Blob, les files d’attente et les tables.

## <a name="connect-to-azure-storage-using-the-connected-services-dialog"></a>Connexion au stockage Azure à l’aide de la boîte de dialogue Services connectés
1. Ouvrez votre projet dans Visual Studio.

1. Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur le nœud **Services connectés**, puis sélectionnez **Ajouter un service connecté** dans le menu contextuel.
   
    ![Ajouter un service connecté Azure](./media/vs-azure-tools-connected-services-storage/IC796702.png)

1. Sur la page **Services connectés**, sélectionnez **Stockage cloud avec le Stockage Azure**.
   
    ![Ajouter le Stockage Azure](./media/vs-azure-tools-connected-services-storage/add-azure-storage.png)

1. Dans la boîte de dialogue **Stockage Azure**, sélectionnez un compte de stockage existant, puis sélectionnez **Ajouter**.
   
    Si vous devez créer un compte de stockage, passez à l’étape suivante. Sinon, passez à l’étape 6.
    
    ![Ajouter un compte de stockage existant au projet](./media/vs-azure-tools-connected-services-storage/select-azure-storage-account.png)

1. Pour créer un compte de stockage : 
   
   1. Sélectionnez **Créer un compte de stockage** au bas de la boîte de dialogue.

   1. Renseignez les informations demandées dans la boîte de dialogue **Créer un compte de stockage**, puis sélectionnez **Créer**.
      
       ![Nouveau compte de stockage Azure](./media/vs-azure-tools-connected-services-storage/create-storage-account.png)
      
   1. Lorsque la boîte de dialogue **Stockage Azure** apparaît, le nouveau compte de stockage s’affiche dans la liste. Sélectionnez le nouveau compte de stockage dans la liste, puis **Ajouter**.

1. Le service connecté de stockage s’affiche sous le nœud **Références de service** de votre projet.
   
## <a name="how-your-project-is-modified"></a>Modifications apportées à votre projet
Quand vous avez terminé la boîte de dialogue, Visual Studio ajoute des références et modifie certains fichiers de configuration. Les modifications spécifiques varient selon le type de projet : 

- Projet ASP.NET : [Que s’est-il passé ? – Projets ASP.NET](http://go.microsoft.com/fwlink/p/?LinkId=513126)
- Projet Core ASP.NET : [Que s’est-il passé ? – Projets ASP.NET 5](http://go.microsoft.com/fwlink/p/?LinkId=513124) 
- Projet de service cloud (rôles web et de travail) : [Que s’est-il passé ? – Projets de service cloud](http://go.microsoft.com/fwlink/p/?LinkId=516965)
- Projets de tâche web - [Que s’est-il passé ? – Projets de tâche web](visual-studio/vs-storage-webjobs-what-happened.md)

## <a name="next-steps"></a>Étapes suivantes
- [Forum MSDN : Stockage Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)
- [Blog de l’équipe Stockage Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/)
- [Documentation d’Azure Storage](https://docs.microsoft.com/azure/storage/)
