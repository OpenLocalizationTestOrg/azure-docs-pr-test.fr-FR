---
title: les administrateurs de serveurs aaaManage dans Azure Analysis Services | Documents Microsoft
description: "Découvrez comment toomanage les administrateurs de serveur pour un serveur Analysis Services dans Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: e04387e48e9b9483c382ee5cc9fd65f8331fb2a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-server-administrators"></a>Gérer des administrateurs de serveur
Les administrateurs de serveur doivent être un utilisateur valide ou un groupe Bonjour Azure Active Directory (Azure AD) pour le client hello dans le hello serveur réside. Vous pouvez utiliser **les administrateurs de Services Analysis** dans le panneau de contrôle hello pour votre serveur dans le portail Azure, ou des propriétés du serveur dans les administrateurs de serveur SSMS toomanage. 

## <a name="tooadd-server-administrators-by-using-azure-portal"></a>administrateurs de serveur tooadd à l’aide du portail Azure
1. Dans le panneau de contrôle hello pour votre serveur, cliquez sur **administrateurs de Services d’analyse**.
2. Bonjour  **\<nom_serveur >-les administrateurs de Services Analysis** panneau, cliquez sur **ajouter**.
3. Bonjour **ajouter des administrateurs de serveur** panneau, sélectionnez les comptes d’utilisateur à partir de votre annuaire Azure AD ou inviter les utilisateurs externes par adresse de messagerie.

    ![Administrateurs de serveur dans le portail Azure](./media/analysis-services-server-admins/aas-manage-users-admins.png)

## <a name="tooadd-server-administrators-by-using-ssms"></a>administrateurs de serveur tooadd à l’aide de SSMS
1. Serveur de hello avec le bouton droit > **propriétés**.
2. Dans **Propriétés de Analysis Server**, cliquez sur **Sécurité**.
3. Cliquez sur **ajouter**, puis entrez l’adresse de messagerie hello pour un utilisateur ou un groupe dans Azure AD.
   
    ![Ajouter des administrateurs de serveur dans SSMS](./media/analysis-services-server-admins/aas-manage-users-ssms.png)

## <a name="next-steps"></a>Étapes suivantes 
[Authentification et autorisations utilisateur](analysis-services-manage-users.md)  
[Gérer les utilisateurs et rôles de base de données](analysis-services-database-users.md)  
[Contrôle d’accès en fonction du rôle](../active-directory/role-based-access-control-what-is.md)  

