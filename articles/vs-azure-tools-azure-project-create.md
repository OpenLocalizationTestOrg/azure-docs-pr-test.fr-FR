---
title: aaaCreating un projet de service cloud Azure avec Visual Studio | Documents Microsoft
description: En savoir plus maintenant toocreate un projet de service cloud Azure avec Visual Studio
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
ms.openlocfilehash: 3c357016aa423688199a7ab3a670115e33a98fe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-azure-cloud-service-project-with-visual-studio"></a>Création d’un projet de service cloud Azure avec Visual Studio
Bonjour Azure Tools pour Visual Studio fournit un modèle de projet qui vous permet de créer un service cloud Azure. Une fois le projet de hello a été créé, Visual Studio vous permet de tooconfigure, déboguer et déployer hello cloud service tooAzure.

## <a name="steps-toocreate-an-azure-cloud-service-project-in-visual-studio"></a>Étapes toocreate un projet de service cloud Azure dans Visual Studio
Cette section vous guide dans le processus de création d’un projet de service cloud Azure dans Visual Studio avec un ou plusieurs rôles web.  

1. Démarrez Visual Studio en tant qu’administrateur.

1. Dans le menu principal de hello, sélectionnez **fichier** > **nouveau** > **projet**.

1. Sélectionnez **Cloud** de hello Visual c# ou Visual Basic nœuds du modèle de projet, puis sélectionnez **Azure Cloud Service** de liste hello des modèles.

    ![Nouveau service cloud Azure](./media/vs-azure-tools-azure-project-create/new-project-wizard-for-cloud-service.png)

1. Spécifiez la version de hello .NET Framework vous souhaitez toouse toodevelop votre projet.

1. Entrez un nom et un emplacement pour votre projet et un nom pour la solution de hello. 

1. Sélectionnez **OK**.

1. Bonjour **nouveau Microsoft Azure Cloud Service** boîte de dialogue, les rôles hello select que vous souhaitez tooadd, choisissez tooadd de bouton de flèche droite hello les tooyour solution.

    ![Sélectionner de nouveaux rôles de service cloud Azure](./media/vs-azure-tools-azure-project-create/new-cloud-service.png)

1. toorename un rôle que vous avez ajouté, amenez le pointeur sur le rôle hello Bonjour **nouveau Microsoft Azure Cloud Service** boîte de dialogue et, dans le menu contextuel de hello, sélectionnez **renommer**. Vous pouvez également renommer un rôle au sein de votre solution (Bonjour **l’Explorateur de solutions**) une fois qu’il a été ajouté.

    ![Renommer un rôle de service cloud Azure](./media/vs-azure-tools-azure-project-create/new-cloud-service-rename.png)

projet de Visual Studio Azure Hello a des projets de rôle toohello associations de solution de hello. projet de Hello inclut également hello *fichier de définition de service* et *fichier de configuration de service*:

- **Fichier de définition de service** -définit les paramètres d’exécution hello pour votre application, y compris les rôles sont requis, points de terminaison et taille de machine virtuelle. 
- **Fichier de configuration de service** -configure le nombre d’instances d’un rôle est exécuté et hello des valeurs de paramètres hello définis pour un rôle. 

Pour plus d’informations sur ces fichiers, consultez [configurer des rôles de hello pour un service cloud Azure avec Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md).

## <a name="next-steps"></a>Étapes suivantes
- [Gestion des rôles dans les projets de service cloud Azure avec Visual Studio](./vs-azure-tools-cloud-service-project-managing-roles.md)
