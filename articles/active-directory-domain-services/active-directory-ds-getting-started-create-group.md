---
title: "Azure Active Directory Domain Services : Créer le groupe d’administrateurs hello Azure AD DC | Documents Microsoft"
description: "Activer Azure Active Directory Domain Services à l’aide de hello portail Azure classic"
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
ms.openlocfilehash: d629ab9632ef6a45b549630999ff9a122d60c040
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-classic-portal"></a><span data-ttu-id="5c461-103">Activer Azure Active Directory Domain Services à l’aide de hello portail Azure classic</span><span class="sxs-lookup"><span data-stu-id="5c461-103">Enable Azure Active Directory Domain Services using hello Azure classic portal</span></span>
<span data-ttu-id="5c461-104">Cet article décrit et guide à travers les tâches de configuration hello qui sont requises pour vous tooenable Azure Active Directory Services de domaine (Azure AD DS) pour votre client Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5c461-104">This article describes and walks through hello configuration tasks that are required for you tooenable Azure Active Directory Domain Services (Azure AD DS) for your Azure Active Directory (Azure AD) tenant.</span></span>

> [!NOTE]
> <span data-ttu-id="5c461-105">[**Essayez plutôt de nouvelle expérience de portail (aperçu) Azure hello**](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="5c461-105">[**Try hello new (preview) Azure portal experience instead**](active-directory-ds-getting-started.md).</span></span> 
>

## <a name="task-1-create-hello-azure-ad-dc-administrators-group"></a><span data-ttu-id="5c461-106">Tâche 1 : créer le groupe Administrateurs de contrôleur de domaine hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c461-106">Task 1: create hello Azure AD DC administrators group</span></span>
<span data-ttu-id="5c461-107">tâche première Hello est toocreate un groupe d’administration dans votre locataire Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c461-107">hello first task is toocreate an administrative group in your Azure AD tenant.</span></span> <span data-ttu-id="5c461-108">Ce groupe d’administration spécial est appelé *AAD DC Administrators*.</span><span class="sxs-lookup"><span data-stu-id="5c461-108">This special administrative group is called *AAD DC Administrators*.</span></span> <span data-ttu-id="5c461-109">Membres de ce groupe bénéficient d’autorisations administratives sur les ordinateurs qui appartiennent à un domaine géré par les Services de domaine Active Directory de Azure de toohello de domaine.</span><span class="sxs-lookup"><span data-stu-id="5c461-109">Members of this group are granted administrative permissions on machines that are domain-joined toohello Azure Active Directory Domain Services-managed domain.</span></span> <span data-ttu-id="5c461-110">Sur les ordinateurs joints à un domaine, ce groupe est ajouté toohello groupe d’administrateurs.</span><span class="sxs-lookup"><span data-stu-id="5c461-110">On domain-joined machines, this group is added toohello administrators group.</span></span> <span data-ttu-id="5c461-111">En outre, les membres de ce groupe peuvent utiliser Bureau à distance tooconnect à distance toodomain-ordinateurs joints à un.</span><span class="sxs-lookup"><span data-stu-id="5c461-111">Additionally, members of this group can use Remote Desktop tooconnect remotely toodomain-joined machines.</span></span>  

> [!NOTE]
> <span data-ttu-id="5c461-112">Il est inutile des autorisations administrateur de domaine ou administrateur d’entreprise sur un domaine géré hello que vous avez créé à l’aide d’Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="5c461-112">You do not have Domain Administrator or Enterprise Administrator permissions on hello managed domain that you created by using Azure Active Directory Domain Services.</span></span> <span data-ttu-id="5c461-113">Dans des domaines gérés, ces autorisations sont réservées par le service de hello et ne sont pas apportées toousers disponibles au sein de client de hello.</span><span class="sxs-lookup"><span data-stu-id="5c461-113">On managed domains, these permissions are reserved by hello service and are not made available toousers within hello tenant.</span></span> <span data-ttu-id="5c461-114">Toutefois, vous pouvez utiliser hello spéciaux groupe d’administration créés dans cette tooperform de tâche de configuration certaines opérations privilégiées.</span><span class="sxs-lookup"><span data-stu-id="5c461-114">However, you can use hello special administrative group created in this configuration task tooperform some privileged operations.</span></span> <span data-ttu-id="5c461-115">Ces opérations comprennent la jonction de domaine toohello des ordinateurs, appartenant toohello groupe d’administration sur les ordinateurs joints au domaine et stratégie de groupe.</span><span class="sxs-lookup"><span data-stu-id="5c461-115">These operations include joining computers toohello domain, belonging toohello administration group on domain-joined machines, and configuring Group Policy.</span></span>
>

<span data-ttu-id="5c461-116">Dans cette tâche de configuration, vous créez le groupe d’administration hello et ajoutez un ou plusieurs utilisateurs dans votre groupe de toohello active.</span><span class="sxs-lookup"><span data-stu-id="5c461-116">In this configuration task, you create hello administrative group and add one or more users in your directory toohello group.</span></span> <span data-ttu-id="5c461-117">groupe d’administration toocreate hello pour les Services de domaine Active Directory Azure, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="5c461-117">toocreate hello administrative group for Azure Active Directory Domain Services, do hello following:</span></span>

1. <span data-ttu-id="5c461-118">Accédez toohello [portail Azure classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="5c461-118">Go toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="5c461-119">Dans le volet gauche de hello, sélectionnez hello **Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="5c461-119">In hello left pane, select hello **Active Directory** button.</span></span>
3. <span data-ttu-id="5c461-120">Sélectionnez le locataire Azure AD de hello (répertoire) pour lequel vous souhaitez tooenable Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="5c461-120">Select hello Azure AD tenant (directory) for which you want tooenable Azure Active Directory Domain Services.</span></span> <span data-ttu-id="5c461-121">Vous ne pouvez créer qu’un seul domaine par annuaire Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c461-121">You can create only one domain for each Azure AD directory.</span></span>

    ![Sélectionnez un annuaire Azure AD.](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="5c461-123">Sur hello **active de la version préliminaire** , cliquez sur hello **groupes** onglet.</span><span class="sxs-lookup"><span data-stu-id="5c461-123">On hello **preview directory** page, click hello **Groups** tab.</span></span>
5. <span data-ttu-id="5c461-124">Cliquez sur un client tooyour Azure AD de groupe, dans le volet de tâches hello bas hello de fenêtre hello, de tooadd **ajouter un groupe**.</span><span class="sxs-lookup"><span data-stu-id="5c461-124">tooadd a group tooyour Azure AD tenant, on hello task pane at hello bottom of hello window, click **Add Group**.</span></span>

    ![bouton Ajouter un groupe de Hello](./media/active-directory-domain-services-getting-started/add-group-button.png)
6. <span data-ttu-id="5c461-126">Bonjour **ajouter un groupe** boîte de dialogue zone, créez un groupe nommé **administrateurs du contrôleur de domaine AAD**, puis définissez **le Type de groupe** trop**sécurité**.</span><span class="sxs-lookup"><span data-stu-id="5c461-126">In hello **Add Group** dialog box, create a group named **AAD DC Administrators**, and then set **Group Type** too**Security**.</span></span>

   > [!WARNING]
   > <span data-ttu-id="5c461-127">accès tooenable au sein de votre domaine géré par les Services de domaine Active Directory de Azure, créez un groupe portant ce nom exact.</span><span class="sxs-lookup"><span data-stu-id="5c461-127">tooenable access within your Azure Active Directory Domain Services-managed domain, create a group with this exact name.</span></span>
   >
   >

    ![boîte de dialogue Ajouter un groupe Hello](./media/active-directory-domain-services-getting-started/create-admin-group.png)
7. <span data-ttu-id="5c461-129">Bonjour **Description** , entrez une description qui permet à d’autres toounderstand que ce groupe accorde des autorisations administratives dans Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="5c461-129">In hello **Description** box, enter a description that enables others toounderstand that this group grants administrative permissions within Azure Active Directory Domain Services.</span></span>
8. <span data-ttu-id="5c461-130">Une fois que vous avez créé le groupe de hello, cliquez sur tooview de nom de groupe hello ses propriétés.</span><span class="sxs-lookup"><span data-stu-id="5c461-130">After you've created hello group, click hello group name tooview its properties.</span></span>
9. <span data-ttu-id="5c461-131">les utilisateurs de tooadd en tant que membres du groupe hello, au bas de hello de fenêtre hello, cliquez sur hello **ajouter des membres** bouton.</span><span class="sxs-lookup"><span data-stu-id="5c461-131">tooadd users as members of hello group, at hello bottom of hello window, click hello **Add Members** button.</span></span>

    ![Bouton Ajouter des membres au groupe](./media/active-directory-domain-services-getting-started/add-group-members-button.png)
10. <span data-ttu-id="5c461-133">Bonjour **ajouter des membres** boîte de dialogue, sélectionnez hello utilisateurs doivent être membres de ce groupe, puis cliquez sur icône de coche de hello en hello inférieur droit.</span><span class="sxs-lookup"><span data-stu-id="5c461-133">In hello **Add members** dialog box, select hello users who should be members of this group, and then click hello checkmark icon at hello lower right.</span></span>

    ![Ajouter le groupe d’utilisateurs tooadministrators](./media/active-directory-domain-services-getting-started/add-group-members.png)


## <a name="next-step"></a><span data-ttu-id="5c461-135">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="5c461-135">Next step</span></span>
[<span data-ttu-id="5c461-136">Tâche 2 : Créer ou sélectionner un réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="5c461-136">Task 2: create or select an Azure virtual network</span></span>](active-directory-ds-getting-started-vnet.md)
