---
title: "Services de domaine Azure Active Directory : Créer le groupe d’administrateurs Azure AD DC | Microsoft Docs"
description: "Activer Azure Active Directory Domain Services à l’aide du portail Azure Classic"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: maheshu
ms.openlocfilehash: 5ed0125e05928cf0f6d9941e099b433ecb46e6e2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="enable-azure-active-directory-domain-services-using-the-azure-classic-portal"></a><span data-ttu-id="c39cd-103">Activer Azure Active Directory Domain Services à l’aide du portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="c39cd-103">Enable Azure Active Directory Domain Services using the Azure classic portal</span></span>
<span data-ttu-id="c39cd-104">Cet article décrit et vous guide à travers les tâches de configuration requises pour activer Azure Active Directory Domain Services (Azure AD DS) pour votre client Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c39cd-104">This article describes and walks through the configuration tasks that are required for you to enable Azure Active Directory Domain Services (Azure AD DS) for your Azure Active Directory (Azure AD) tenant.</span></span>

> [!NOTE]
> <span data-ttu-id="c39cd-105">[**Essayez plutôt la nouvelle expérience de portail Azure (préversion)**](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="c39cd-105">[**Try the new (preview) Azure portal experience instead**](active-directory-ds-getting-started.md).</span></span> 
>

## <a name="task-1-create-the-azure-ad-dc-administrators-group"></a><span data-ttu-id="c39cd-106">Tâche 1 : Créer le groupe d’administrateurs Azure AD DC</span><span class="sxs-lookup"><span data-stu-id="c39cd-106">Task 1: create the Azure AD DC administrators group</span></span>
<span data-ttu-id="c39cd-107">La première tâche consiste à créer un groupe d’administration dans votre client Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c39cd-107">The first task is to create an administrative group in your Azure AD tenant.</span></span> <span data-ttu-id="c39cd-108">Ce groupe d’administration spécial est appelé *AAD DC Administrators*.</span><span class="sxs-lookup"><span data-stu-id="c39cd-108">This special administrative group is called *AAD DC Administrators*.</span></span> <span data-ttu-id="c39cd-109">Les membres de ce groupe se voient accorder des autorisations d’administrateur sur les ordinateurs joints au domaine géré des services de domaine Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c39cd-109">Members of this group are granted administrative permissions on machines that are domain-joined to the Azure Active Directory Domain Services-managed domain.</span></span> <span data-ttu-id="c39cd-110">Sur les ordinateurs joints au domaine, ce groupe est ajouté au groupe « Administrateurs ».</span><span class="sxs-lookup"><span data-stu-id="c39cd-110">On domain-joined machines, this group is added to the administrators group.</span></span> <span data-ttu-id="c39cd-111">En outre, les membres de ce groupe sont également autorisés à utiliser le Bureau à distance pour se connecter à distance aux ordinateurs joints au domaine.</span><span class="sxs-lookup"><span data-stu-id="c39cd-111">Additionally, members of this group can use Remote Desktop to connect remotely to domain-joined machines.</span></span>  

> [!NOTE]
> <span data-ttu-id="c39cd-112">Vous ne bénéficiez pas des autorisations d’administrateur de domaine ou d’administrateur d’entreprise sur le domaine géré que vous avez créé à l’aide des services de domaine Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c39cd-112">You do not have Domain Administrator or Enterprise Administrator permissions on the managed domain that you created by using Azure Active Directory Domain Services.</span></span> <span data-ttu-id="c39cd-113">Dans un domaine géré, ces autorisations sont réservées par le service et ne sont pas accessibles aux utilisateurs au sein du client.</span><span class="sxs-lookup"><span data-stu-id="c39cd-113">On managed domains, these permissions are reserved by the service and are not made available to users within the tenant.</span></span> <span data-ttu-id="c39cd-114">Toutefois, vous pouvez utiliser le groupe d’administrateurs spécial créé dans cette tâche de configuration, afin d’exécuter des opérations privilégiées.</span><span class="sxs-lookup"><span data-stu-id="c39cd-114">However, you can use the special administrative group created in this configuration task to perform some privileged operations.</span></span> <span data-ttu-id="c39cd-115">Ces opérations comprennent l’ajout d’ordinateurs au domaine, l’appartenance au groupe Administrateurs sur les ordinateurs joints au domaine, la configuration de stratégie de groupe.</span><span class="sxs-lookup"><span data-stu-id="c39cd-115">These operations include joining computers to the domain, belonging to the administration group on domain-joined machines, and configuring Group Policy.</span></span>
>

<span data-ttu-id="c39cd-116">Au cours de cette tâche de configuration, vous créez le groupe d’administration et y ajoutez un ou plusieurs utilisateurs de votre répertoire.</span><span class="sxs-lookup"><span data-stu-id="c39cd-116">In this configuration task, you create the administrative group and add one or more users in your directory to the group.</span></span> <span data-ttu-id="c39cd-117">Pour créer le groupe d’administration pour les services de domaine Azure Active Directory, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c39cd-117">To create the administrative group for Azure Active Directory Domain Services, do the following:</span></span>

1. <span data-ttu-id="c39cd-118">Connectez-vous au [Portail Azure Classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="c39cd-118">Go to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="c39cd-119">Dans le volet de gauche, cliquez sur le bouton **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c39cd-119">In the left pane, select the **Active Directory** button.</span></span>
3. <span data-ttu-id="c39cd-120">Sélectionnez le client Azure AD (annuaire) pour lequel vous souhaitez activer Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="c39cd-120">Select the Azure AD tenant (directory) for which you want to enable Azure Active Directory Domain Services.</span></span> <span data-ttu-id="c39cd-121">Vous ne pouvez créer qu’un seul domaine par annuaire Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c39cd-121">You can create only one domain for each Azure AD directory.</span></span>

    ![Sélectionnez un annuaire Azure AD.](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="c39cd-123">Sur la page de la **version préliminaire de l’annuaire**, cliquez sur l’onglet **Groupes**.</span><span class="sxs-lookup"><span data-stu-id="c39cd-123">On the **preview directory** page, click the **Groups** tab.</span></span>
5. <span data-ttu-id="c39cd-124">Cliquez sur **Ajouter un groupe** à partir du volet de tâches en bas de la fenêtre pour ajouter un groupe à votre client Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c39cd-124">To add a group to your Azure AD tenant, on the task pane at the bottom of the window, click **Add Group**.</span></span>

    ![Le bouton Ajouter un groupe](./media/active-directory-domain-services-getting-started/add-group-button.png)
6. <span data-ttu-id="c39cd-126">Dans la boîte de dialogue **Ajouter un groupe**, créez un groupe nommé **Administrateurs AAD DC**, puis définissez **Type de groupe** sur **Sécurité**.</span><span class="sxs-lookup"><span data-stu-id="c39cd-126">In the **Add Group** dialog box, create a group named **AAD DC Administrators**, and then set **Group Type** to **Security**.</span></span>

   > [!WARNING]
   > <span data-ttu-id="c39cd-127">Vous devez créer un groupe portant exactement ce nom pour activer l’accès au sein des services de domaine Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c39cd-127">To enable access within your Azure Active Directory Domain Services-managed domain, create a group with this exact name.</span></span>
   >
   >

    ![La boîte de dialogue Ajouter un groupe](./media/active-directory-domain-services-getting-started/create-admin-group.png)
7. <span data-ttu-id="c39cd-129">Dans la zone **Description**, entrez une description qui permettra à d’autres de comprendre que ce groupe accorde des autorisations administratives dans Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="c39cd-129">In the **Description** box, enter a description that enables others to understand that this group grants administrative permissions within Azure Active Directory Domain Services.</span></span>
8. <span data-ttu-id="c39cd-130">Une fois que vous avez créé le groupe, cliquez sur le nom du groupe pour afficher ses propriétés.</span><span class="sxs-lookup"><span data-stu-id="c39cd-130">After you've created the group, click the group name to view its properties.</span></span>
9. <span data-ttu-id="c39cd-131">Cliquez sur le bouton **Ajouter des membres** en bas de la fenêtre pour ajouter des utilisateurs en tant que membres de ce groupe.</span><span class="sxs-lookup"><span data-stu-id="c39cd-131">To add users as members of the group, at the bottom of the window, click the **Add Members** button.</span></span>

    ![Bouton Ajouter des membres au groupe](./media/active-directory-domain-services-getting-started/add-group-members-button.png)
10. <span data-ttu-id="c39cd-133">Dans la boîte de dialogue **Ajouter des membres** , sélectionnez les utilisateurs qui doivent être membres de ce groupe et cliquez sur l’icône de coche en bas à droite.</span><span class="sxs-lookup"><span data-stu-id="c39cd-133">In the **Add members** dialog box, select the users who should be members of this group, and then click the checkmark icon at the lower right.</span></span>

    ![Ajouter des utilisateurs au groupe d’administrateurs](./media/active-directory-domain-services-getting-started/add-group-members.png)


## <a name="next-step"></a><span data-ttu-id="c39cd-135">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="c39cd-135">Next step</span></span>
[<span data-ttu-id="c39cd-136">Tâche 2 : Créer ou sélectionner un réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="c39cd-136">Task 2: create or select an Azure virtual network</span></span>](active-directory-ds-getting-started-vnet.md)
