---
title: "tooresources d’autorisations aaaManage par utilisateur dans la pile de Azure (administrateur de service et client) | Documents Microsoft"
description: Comme un client ou un administrateur de service, vous devez savoir comment les autorisations RBAC toomanage.
services: azure-stack
documentationcenter: 
author: Heathl17
manager: byronr
editor: 
ms.assetid: cccac19a-e1bf-4e36-8ac8-2228e8487646
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: 461feab12a4cb8b9402c6c61b721371c50f60559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control"></a><span data-ttu-id="285bb-103">Gérer le contrôle d’accès en fonction du rôle</span><span class="sxs-lookup"><span data-stu-id="285bb-103">Manage Role-Based Access Control</span></span>
<span data-ttu-id="285bb-104">Un utilisateur Azure Stack peut être un lecteur, un propriétaire ou un collaborateur pour chaque instance d’un abonnement, d’un groupe de ressources ou d’un service.</span><span class="sxs-lookup"><span data-stu-id="285bb-104">A user in Azure Stack can be a reader, owner, or contributor for each instance of a subscription, resource group, or service.</span></span> <span data-ttu-id="285bb-105">Par exemple, l’utilisateur A peut disposer des autorisations de lecture du tooSubscription 1, mais ont des autorisations de propriétaire tooVirtual 7 de l’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="285bb-105">For example, User A might have reader permissions tooSubscription 1, but have owner permissions tooVirtual Machine 7.</span></span>

* <span data-ttu-id="285bb-106">Lecteur : l’utilisateur peut tout afficher, mais ne peut pas effectuer de modifications.</span><span class="sxs-lookup"><span data-stu-id="285bb-106">Reader: User can view everything, but can’t make any changes.</span></span>
* <span data-ttu-id="285bb-107">Collaborateur : Utilisateur peut gérer tout sauf tooresources d’accès.</span><span class="sxs-lookup"><span data-stu-id="285bb-107">Contributor: User can manage everything except access tooresources.</span></span>
* <span data-ttu-id="285bb-108">Propriétaire : Utilisateur peut gérer tout, y compris les accès tooresources.</span><span class="sxs-lookup"><span data-stu-id="285bb-108">Owner: User can manage everything, including access tooresources.</span></span>

## <a name="set-access-permissions-for-a-user"></a><span data-ttu-id="285bb-109">Définir des autorisations d’accès pour un utilisateur</span><span class="sxs-lookup"><span data-stu-id="285bb-109">Set access permissions for a user</span></span>
1. <span data-ttu-id="285bb-110">Connectez-vous avec un compte qui dispose du propriétaire autorisations toohello ressource toomanage.</span><span class="sxs-lookup"><span data-stu-id="285bb-110">Sign in with an account that has owner permissions toohello resource you want toomanage.</span></span>
2. <span data-ttu-id="285bb-111">Dans le panneau hello pour la ressource de hello, cliquez sur hello **accès** icône ![](media/azure-stack-manage-permissions/image1.png).</span><span class="sxs-lookup"><span data-stu-id="285bb-111">In hello blade for hello resource, click hello **Access** icon ![](media/azure-stack-manage-permissions/image1.png).</span></span>
3. <span data-ttu-id="285bb-112">Bonjour **utilisateurs** panneau, cliquez sur **rôles**.</span><span class="sxs-lookup"><span data-stu-id="285bb-112">In hello **Users** blade, click **Roles**.</span></span>
4. <span data-ttu-id="285bb-113">Bonjour **rôles** panneau, cliquez sur **ajouter** tooadd les autorisations pour l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="285bb-113">In hello **Roles** blade, click **Add** tooadd permissions for hello user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="285bb-114">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="285bb-114">Next steps</span></span>
[<span data-ttu-id="285bb-115">Ajouter un locataire Azure Stack</span><span class="sxs-lookup"><span data-stu-id="285bb-115">Add an Azure Stack tenant</span></span>](azure-stack-add-new-user-aad.md)

