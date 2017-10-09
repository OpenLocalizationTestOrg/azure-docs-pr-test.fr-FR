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
# <a name="manage-server-administrators"></a><span data-ttu-id="9e603-103">Gérer des administrateurs de serveur</span><span class="sxs-lookup"><span data-stu-id="9e603-103">Manage server administrators</span></span>
<span data-ttu-id="9e603-104">Les administrateurs de serveur doivent être un utilisateur valide ou un groupe Bonjour Azure Active Directory (Azure AD) pour le client hello dans le hello serveur réside.</span><span class="sxs-lookup"><span data-stu-id="9e603-104">Server administrators must be a valid user or group in hello Azure Active Directory (Azure AD) for hello tenant in which hello server resides.</span></span> <span data-ttu-id="9e603-105">Vous pouvez utiliser **les administrateurs de Services Analysis** dans le panneau de contrôle hello pour votre serveur dans le portail Azure, ou des propriétés du serveur dans les administrateurs de serveur SSMS toomanage.</span><span class="sxs-lookup"><span data-stu-id="9e603-105">You can use **Analysis Services Admins** in hello control blade for your server in Azure portal, or Server Properties in SSMS toomanage server administrators.</span></span> 

## <a name="tooadd-server-administrators-by-using-azure-portal"></a><span data-ttu-id="9e603-106">administrateurs de serveur tooadd à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="9e603-106">tooadd server administrators by using Azure portal</span></span>
1. <span data-ttu-id="9e603-107">Dans le panneau de contrôle hello pour votre serveur, cliquez sur **administrateurs de Services d’analyse**.</span><span class="sxs-lookup"><span data-stu-id="9e603-107">In hello control blade for your server, click **Analysis Services Admins**.</span></span>
2. <span data-ttu-id="9e603-108">Bonjour  **\<nom_serveur >-les administrateurs de Services Analysis** panneau, cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="9e603-108">In hello **\<servername> - Analysis Services Admins** blade, click **Add**.</span></span>
3. <span data-ttu-id="9e603-109">Bonjour **ajouter des administrateurs de serveur** panneau, sélectionnez les comptes d’utilisateur à partir de votre annuaire Azure AD ou inviter les utilisateurs externes par adresse de messagerie.</span><span class="sxs-lookup"><span data-stu-id="9e603-109">In hello **Add Server Administrators** blade, select user accounts from your Azure AD or invite external users by email address.</span></span>

    ![Administrateurs de serveur dans le portail Azure](./media/analysis-services-server-admins/aas-manage-users-admins.png)

## <a name="tooadd-server-administrators-by-using-ssms"></a><span data-ttu-id="9e603-111">administrateurs de serveur tooadd à l’aide de SSMS</span><span class="sxs-lookup"><span data-stu-id="9e603-111">tooadd server administrators by using SSMS</span></span>
1. <span data-ttu-id="9e603-112">Serveur de hello avec le bouton droit > **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="9e603-112">Right-click hello server > **Properties**.</span></span>
2. <span data-ttu-id="9e603-113">Dans **Propriétés de Analysis Server**, cliquez sur **Sécurité**.</span><span class="sxs-lookup"><span data-stu-id="9e603-113">In **Analysis Server Properties**, click **Security**.</span></span>
3. <span data-ttu-id="9e603-114">Cliquez sur **ajouter**, puis entrez l’adresse de messagerie hello pour un utilisateur ou un groupe dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9e603-114">Click **Add**, and then enter hello email address for a user or group in your Azure AD.</span></span>
   
    ![Ajouter des administrateurs de serveur dans SSMS](./media/analysis-services-server-admins/aas-manage-users-ssms.png)

## <a name="next-steps"></a><span data-ttu-id="9e603-116">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9e603-116">Next steps</span></span> 
[<span data-ttu-id="9e603-117">Authentification et autorisations utilisateur</span><span class="sxs-lookup"><span data-stu-id="9e603-117">Authentication and user permissions</span></span>](analysis-services-manage-users.md)  
[<span data-ttu-id="9e603-118">Gérer les utilisateurs et rôles de base de données</span><span class="sxs-lookup"><span data-stu-id="9e603-118">Manage database roles and users</span></span>](analysis-services-database-users.md)  
[<span data-ttu-id="9e603-119">Contrôle d’accès en fonction du rôle</span><span class="sxs-lookup"><span data-stu-id="9e603-119">Role-Based Access Control</span></span>](../active-directory/role-based-access-control-what-is.md)  

