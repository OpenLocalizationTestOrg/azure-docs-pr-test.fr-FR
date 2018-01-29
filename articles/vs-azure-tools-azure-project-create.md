---
title: "Création d’un projet de service cloud Azure avec Visual Studio | Microsoft Docs"
description: "Apprenez dès maintenant à créer un projet de service cloud Azure avec Visual Studio"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: ec580df7-3dcc-45a9-a1d9-8c110678dfb5
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 1f6ded87b551f660853ea4eb0548f3d942e28fa8
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="creating-an-azure-cloud-service-project-with-visual-studio"></a>Création d’un projet de service cloud Azure avec Visual Studio
Les outils Azure pour Visual Studio fournissent un modèle de projet vous permettant de créer un service cloud Azure. Une fois le projet créé, Visual Studio vous permet de configurer, déboguer et déployer le service cloud dans Azure.

## <a name="steps-to-create-an-azure-cloud-service-project-in-visual-studio"></a>Étapes pour créer un projet de service cloud Azure dans Visual Studio
Cette section vous guide dans le processus de création d’un projet de service cloud Azure dans Visual Studio avec un ou plusieurs rôles web.  

1. Démarrez Visual Studio en tant qu’administrateur.

1. Dans le menu principal, sélectionnez **Fichier** > **Nouveau** > **Projet**.

1. Sélectionnez **Cloud** à partir des nœuds de modèles de projets Visual C# ou Visual Basic , puis sélectionnez **Service cloud Azure** dans la liste des modèles.

    ![Nouveau service cloud Azure](./media/vs-azure-tools-azure-project-create/new-project-wizard-for-cloud-service.png)

1. Spécifiez la version de .NET Framework que vous souhaitez utiliser pour développer votre projet.

1. Entrez un nom et un emplacement pour votre projet et un nom pour la solution. 

1. Sélectionnez **OK**.

1. Dans la boîte de dialogue **Nouveau service cloud Microsoft Azure**, sélectionnez les rôles que vous souhaitez ajouter et appuyez sur la touche de direction droite pour les ajouter à votre solution.

    ![Sélectionner de nouveaux rôles de service cloud Azure](./media/vs-azure-tools-azure-project-create/new-cloud-service.png)

1. Pour renommer un rôle que vous avez ajouté, passez la souris sur le rôle dans la boîte de dialogue **Nouveau service cloud Microsoft Azure**, puis, dans le menu contextuel, sélectionnez **Renommer**. Vous pouvez également renommer un rôle dans votre solution (dans **l’Explorateur de solutions**) une fois qu’il a été ajouté.

    ![Renommer un rôle de service cloud Azure](./media/vs-azure-tools-azure-project-create/new-cloud-service-rename.png)

Le projet Azure Visual Studio est associé aux projets de rôle de la solution. Le projet comprend également le *fichier de définition de service* et le *fichier de configuration de service* :

- **Fichier de définition de service** : définit les paramètres d’exécution de votre application, notamment les rôles requis, les points de terminaison et la taille de la machine virtuelle. 
- **Fichier de configuration de service** : configure le nombre d’instances d’un rôle exécutées et les valeurs des paramètres définis pour un rôle. 

Pour plus d’informations sur ces fichiers,voir [Configuration des rôles pour un service cloud Azure avec Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md).

## <a name="next-steps"></a>Étapes suivantes
- [Gestion des rôles dans les projets de service cloud Azure avec Visual Studio](./vs-azure-tools-cloud-service-project-managing-roles.md)
