---
title: "Gérer les administrateurs de serveur dans Azure Analysis Services | Microsoft Docs"
description: "Apprenez à gérer des administrateurs de serveur pour un serveur Analysis Services dans Azure."
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
ms.openlocfilehash: a1b58125dafdf73f245b6a8cd0f4917513b22ea9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-server-administrators"></a><span data-ttu-id="7119a-103">Gérer des administrateurs de serveur</span><span class="sxs-lookup"><span data-stu-id="7119a-103">Manage server administrators</span></span>
<span data-ttu-id="7119a-104">Un administrateur de serveur doit être un utilisateur ou un groupe valide présent dans Azure Active Directory (Azure AD) pour le client disposant du serveur.</span><span class="sxs-lookup"><span data-stu-id="7119a-104">Server administrators must be a valid user or group in the Azure Active Directory (Azure AD) for the tenant in which the server resides.</span></span> <span data-ttu-id="7119a-105">Vous pouvez utiliser les **Administrateurs Analysis Services** dans le panneau de commande de votre serveur dans le portail ou Propriétés du serveur dans SSMS pour gérer les administrateurs de serveur.</span><span class="sxs-lookup"><span data-stu-id="7119a-105">You can use **Analysis Services Admins** in the control blade for your server in Azure portal, or Server Properties in SSMS to manage server administrators.</span></span> 

## <a name="to-add-server-administrators-by-using-azure-portal"></a><span data-ttu-id="7119a-106">Pour ajouter des administrateurs de serveur à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="7119a-106">To add server administrators by using Azure portal</span></span>
1. <span data-ttu-id="7119a-107">Dans le panneau de contrôle de votre serveur, cliquez sur **Administrateurs Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="7119a-107">In the control blade for your server, click **Analysis Services Admins**.</span></span>
2. <span data-ttu-id="7119a-108">Dans le panneau **\<nom_serveur > Administrateurs Analysis Services**, cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="7119a-108">In the **\<servername> - Analysis Services Admins** blade, click **Add**.</span></span>
3. <span data-ttu-id="7119a-109">Dans le panneau **Ajouter des administrateurs de serveur**, sélectionnez les comptes d’utilisateur depuis Azure AD ou invitez des utilisateurs externes via leur adresse e-mail.</span><span class="sxs-lookup"><span data-stu-id="7119a-109">In the **Add Server Administrators** blade, select user accounts from your Azure AD or invite external users by email address.</span></span>

    ![Administrateurs de serveur dans le portail Azure](./media/analysis-services-server-admins/aas-manage-users-admins.png)

## <a name="to-add-server-administrators-by-using-ssms"></a><span data-ttu-id="7119a-111">Pour ajouter des administrateurs de serveur à l’aide de SSMS</span><span class="sxs-lookup"><span data-stu-id="7119a-111">To add server administrators by using SSMS</span></span>
1. <span data-ttu-id="7119a-112">Faites un clic droit sur le serveur > **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="7119a-112">Right-click the server > **Properties**.</span></span>
2. <span data-ttu-id="7119a-113">Dans **Propriétés de Analysis Server**, cliquez sur **Sécurité**.</span><span class="sxs-lookup"><span data-stu-id="7119a-113">In **Analysis Server Properties**, click **Security**.</span></span>
3. <span data-ttu-id="7119a-114">Cliquez sur **Ajouter**, puis entrez l’adresse e-mail d’un utilisateur ou d’un groupe dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7119a-114">Click **Add**, and then enter the email address for a user or group in your Azure AD.</span></span>
   
    ![Ajouter des administrateurs de serveur dans SSMS](./media/analysis-services-server-admins/aas-manage-users-ssms.png)

## <a name="next-steps"></a><span data-ttu-id="7119a-116">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7119a-116">Next steps</span></span> 
[<span data-ttu-id="7119a-117">Authentification et autorisations utilisateur</span><span class="sxs-lookup"><span data-stu-id="7119a-117">Authentication and user permissions</span></span>](analysis-services-manage-users.md)  
[<span data-ttu-id="7119a-118">Gérer les utilisateurs et rôles de base de données</span><span class="sxs-lookup"><span data-stu-id="7119a-118">Manage database roles and users</span></span>](analysis-services-database-users.md)  
[<span data-ttu-id="7119a-119">Contrôle d’accès en fonction du rôle</span><span class="sxs-lookup"><span data-stu-id="7119a-119">Role-Based Access Control</span></span>](../active-directory/role-based-access-control-what-is.md)  

