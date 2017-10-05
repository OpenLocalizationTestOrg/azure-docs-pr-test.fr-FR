---
title: "Didacticiel : configuration de GitHub pour l’approvisionnement automatique d’utilisateurs avec Azure Active Directory | Documents Microsoft"
description: "Découvrez comment configurer Azure Active Directory pour approvisionner et déprovisionner automatiquement des comptes utilisateur sur GitHub."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: asmalser-msft
ms.openlocfilehash: 3cc70273e95dbf4913e7bbcd8a37bd9a52987b60
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-configuring-github-for-automatic-user-provisioning"></a><span data-ttu-id="fcfb8-103">Didacticiel : configuration de GitHub pour l’approvisionnement automatique d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="fcfb8-103">Tutorial: Configuring GitHub for Automatic User Provisioning</span></span>


<span data-ttu-id="fcfb8-104">L’objectif de ce didacticiel est de vous indiquer les étapes à suivre dans GitHub et Azure AD pour approvisionner et déprovisionner automatiquement des comptes utilisateur d’Azure AD vers GitHub.</span><span class="sxs-lookup"><span data-stu-id="fcfb8-104">The objective of this tutorial is to show you the steps you need to perform in GitHub and Azure AD to automatically provision and de-provision user accounts from Azure AD to GitHub.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="fcfb8-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="fcfb8-105">Prerequisites</span></span>

<span data-ttu-id="fcfb8-106">Le scénario décrit dans ce didacticiel part du principe que vous disposez des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="fcfb8-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="fcfb8-107">Un client Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fcfb8-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="fcfb8-108">Un client GitHub avec le [Plan d’entreprise](https://help.github.com/articles/organization-billing-plans/#business-plan) ou supérieur</span><span class="sxs-lookup"><span data-stu-id="fcfb8-108">A Github tenant with the [Business plan](https://help.github.com/articles/organization-billing-plans/#business-plan) or better enabled</span></span> 
*   <span data-ttu-id="fcfb8-109">Un compte d’utilisateur dans GitHub avec des autorisations d’administrateur</span><span class="sxs-lookup"><span data-stu-id="fcfb8-109">A user account in GitHub with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="fcfb8-110">L’intégration de l’approvisionnement Azure AD s’appuie sur [l’API GitHub SCIM](https://developer.github.com/v3/scim/) disponible pour les équipes GitHub disposant du Plan d’entreprise ou supérieur.</span><span class="sxs-lookup"><span data-stu-id="fcfb8-110">The Azure AD provisioning integration relies on the [GitHub SCIM API](https://developer.github.com/v3/scim/), which is available to Github teams on the Business plan or better.</span></span>

## <a name="assigning-users-to-github"></a><span data-ttu-id="fcfb8-111">Attribution d’utilisateurs à GitHub</span><span class="sxs-lookup"><span data-stu-id="fcfb8-111">Assigning users to GitHub</span></span>

<span data-ttu-id="fcfb8-112">Azure Active Directory utilise un concept appelé « affectations » pour déterminer les utilisateurs devant recevoir l’accès aux applications sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="fcfb8-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="fcfb8-113">Dans le cadre de l’approvisionnement automatique de comptes utilisateur, seuls les utilisateurs et les groupes qui ont été « attribués » à une application dans Azure AD sont synchronisés.</span><span class="sxs-lookup"><span data-stu-id="fcfb8-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="fcfb8-114">Avant de configurer et d’activer le service d’approvisionnement, vous devez déterminer quels utilisateurs et/ou groupes dans Azure AD représentent les utilisateurs qui ont besoin d’accéder à votre application GitHub.</span><span class="sxs-lookup"><span data-stu-id="fcfb8-114">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your GitHub app.</span></span> <span data-ttu-id="fcfb8-115">Une fois que vous avez choisi, vous pouvez attribuer ces utilisateurs à votre application GitHub en suivant les instructions fournies ici :</span><span class="sxs-lookup"><span data-stu-id="fcfb8-115">Once decided, you can assign these users to your GitHub app by following the instructions here:</span></span>

[<span data-ttu-id="fcfb8-116">Affecter un utilisateur ou un groupe à une application d’entreprise</span><span class="sxs-lookup"><span data-stu-id="fcfb8-116">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-github"></a><span data-ttu-id="fcfb8-117">Conseils importants pour l’attribution d’utilisateurs à GitHub</span><span class="sxs-lookup"><span data-stu-id="fcfb8-117">Important tips for assigning users to GitHub</span></span>

*   <span data-ttu-id="fcfb8-118">Nous vous recommandons de n’assigner qu’un seul utilisateur Azure AD à GitHub afin de tester la configuration de l’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="fcfb8-118">It is recommended that a single Azure AD user is assigned to GitHub to test the provisioning configuration.</span></span> <span data-ttu-id="fcfb8-119">Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="fcfb8-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="fcfb8-120">Quand vous attribuez un utilisateur à GitHub, vous devez sélectionner le rôle **Utilisateur** ou un autre rôle valide propre à l’application (si disponible) dans la boîte de dialogue d’attribution.</span><span class="sxs-lookup"><span data-stu-id="fcfb8-120">When assigning a user to GitHub, you must select either the **User** role, or another valid application-specific role (if available) in the assignment dialog.</span></span> <span data-ttu-id="fcfb8-121">Le rôle **Accès par défaut** ne fonctionne pas pour l’approvisionnement et ces utilisateurs sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="fcfb8-121">The **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-to-github"></a><span data-ttu-id="fcfb8-122">Configuration de l'approvisionnement des utilisateurs sur GitHub</span><span class="sxs-lookup"><span data-stu-id="fcfb8-122">Configuring user provisioning to GitHub</span></span> 

<span data-ttu-id="fcfb8-123">Cette section explique comment connecter votre Azure AD à l’API d’approvisionnement de comptes d’utilisateur de GitHub pour créer, mettre à jour et désactiver les comptes d’utilisateur attribués dans GitHub en fonction des attributions d’utilisateurs et de groupes dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fcfb8-123">This section guides you through connecting your Azure AD to GitHub's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in GitHub based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="fcfb8-124">Vous pouvez également choisir d’activer l’authentification unique basée sur SAML pour GitHub en suivant les instructions fournies dans le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fcfb8-124">You may also choose to enabled SAML-based Single Sign-On for GitHub, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="fcfb8-125">L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que chacune de ces deux fonctionnalités compléte l’autre.</span><span class="sxs-lookup"><span data-stu-id="fcfb8-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-to-github-in-azure-ad"></a><span data-ttu-id="fcfb8-126">Configurer l’approvisionnement automatique de comptes utilisateurs vers GitHub dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="fcfb8-126">Configure automatic user account provisioning to GitHub in Azure AD</span></span>


1. <span data-ttu-id="fcfb8-127">Dans le [portail Azure](https://portal.azure.com), accédez à la section **Azure Active Directory > Applications d’entreprise > Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="fcfb8-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="fcfb8-128">Si vous avez déjà configuré GitHub pour l’authentification unique, recherchez votre instance de GitHub à l’aide du champ de recherche.</span><span class="sxs-lookup"><span data-stu-id="fcfb8-128">If you have already configured GitHub for single sign-on, search for your instance of GitHub using the search field.</span></span> <span data-ttu-id="fcfb8-129">Sinon, sélectionnez **Ajouter** et recherchez **GitHub** dans la galerie d’applications.</span><span class="sxs-lookup"><span data-stu-id="fcfb8-129">Otherwise, select **Add** and search for **GitHub** in the application gallery.</span></span> <span data-ttu-id="fcfb8-130">Sélectionnez GitHub dans les résultats de recherche et ajoutez-le à votre liste d’applications.</span><span class="sxs-lookup"><span data-stu-id="fcfb8-130">Select GitHub from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="fcfb8-131">Sélectionnez votre instance de GitHub, puis sélectionnez l’onglet **Approvisionnement**.</span><span class="sxs-lookup"><span data-stu-id="fcfb8-131">Select your instance of GitHub, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="fcfb8-132">Définissez le **Mode d’approvisionnement** sur **Automatique**.</span><span class="sxs-lookup"><span data-stu-id="fcfb8-132">Set the **Provisioning Mode** to **Automatic**.</span></span>

    ![Approvisionnement GitHub](./media/active-directory-saas-github-provisioning-tutorial/GitHub1.png)

5. <span data-ttu-id="fcfb8-134">Sous la section **informations d’identification de l’administrateur**, cliquez sur **Autoriser**.</span><span class="sxs-lookup"><span data-stu-id="fcfb8-134">Under the **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="fcfb8-135">Cette opération ouvre une boîte de dialogue d’autorisation GitHub dans une nouvelle fenêtre du navigateur.</span><span class="sxs-lookup"><span data-stu-id="fcfb8-135">This operation opens a GitHub authorization dialog in a new browser window.</span></span> 

6. <span data-ttu-id="fcfb8-136">Dans la nouvelle fenêtre, connectez-vous à GitHub à l’aide de votre compte d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="fcfb8-136">In the new window, sign into GitHub using your Admin account.</span></span> <span data-ttu-id="fcfb8-137">Dans la boîte de dialogue d’autorisation qui s’affiche, sélectionnez l’équipe GitHub pour laquelle vous souhaitez activer l’approvisionnement, puis sélectionnez **Autoriser**.</span><span class="sxs-lookup"><span data-stu-id="fcfb8-137">In the resulting authorization dialog, select the GitHub team that you want to enable provisioning for, and then select **Authorize**.</span></span> <span data-ttu-id="fcfb8-138">Une fois cela terminé, revenez au portail Azure pour terminer la configuration de l’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="fcfb8-138">Once completed, return to the Azure portal to complete the provisioning configuration.</span></span>

    ![Boîte de dialogue d’autorisation](./media/active-directory-saas-github-provisioning-tutorial/GitHub2.png)

7. <span data-ttu-id="fcfb8-140">Dans le portail Azure, entrez **URL cliente** et cliquez sur **Connexion test** pour vous assurer qu’Azure AD peut se connecter à votre application GitHub.</span><span class="sxs-lookup"><span data-stu-id="fcfb8-140">In the Azure portal, input **Tenant URL** and click **Test Connection** to ensure Azure AD can connect to your GitHub app.</span></span> <span data-ttu-id="fcfb8-141">Si la connexion échoue, vérifiez votre compte GitHub dispose des autorisations administratives et que**URl de client** est correctement entrée, puis recommencez l’étape « Autoriser » (vous pouvez constituer **l’URL de client** par règle : « https://api.github.com/scim/v2/organizations/ + < Organizations_name > », vous pouvez rechercher votre organisation sous votre compte GitHub : **Paramètres** > **Organisations**).</span><span class="sxs-lookup"><span data-stu-id="fcfb8-141">If the connection fails, ensure your GitHub account has Admin permissions and **Tenant URl** is inputted correctly, then try the "Authorize" step again (you can constitute **Tenant URL** by rule: "https://api.github.com/scim/v2/organizations/ + <Organizations_name>", you can find your organizations under your GitHub account: **Settings** > **Organizations**).</span></span>

    ![Boîte de dialogue d’autorisation](./media/active-directory-saas-github-provisioning-tutorial/GitHub3.png)

8. <span data-ttu-id="fcfb8-143">Entrez l’adresse e-mail d’une personne ou d’un groupe qui doit recevoir les notifications d’erreur d’approvisionnement dans le champ **E-mail de notification**, puis cochez la case « Envoyer une notification par e-mail en cas de défaillance ».</span><span class="sxs-lookup"><span data-stu-id="fcfb8-143">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox "Send an email notification when a failure occurs."</span></span>

9. <span data-ttu-id="fcfb8-144">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="fcfb8-144">Click **Save**.</span></span> 

10. <span data-ttu-id="fcfb8-145">Dans la section Mappages, sélectionnez **Synchroniser les utilisateurs Azure Active Directory avec GitHub**.</span><span class="sxs-lookup"><span data-stu-id="fcfb8-145">Under the Mappings section, select **Synchronize Azure Active Directory Users to GitHub**.</span></span>

11. <span data-ttu-id="fcfb8-146">Dans la section **Mappages des attributs**, passez en revue les attributs d’utilisateur qui sont synchronisés d’Azure AD vers GitHub.</span><span class="sxs-lookup"><span data-stu-id="fcfb8-146">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to GitHub.</span></span> <span data-ttu-id="fcfb8-147">Les attributs sélectionnés en tant que propriétés de **Correspondance** sont utilisés pour faire correspondre les comptes d’utilisateur dans GitHub pour les opérations de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="fcfb8-147">The attributes selected as **Matching** properties are used to match the user accounts in GitHub for update operations.</span></span> <span data-ttu-id="fcfb8-148">Cliquez sur le bouton Enregistrer pour valider les modifications.</span><span class="sxs-lookup"><span data-stu-id="fcfb8-148">Select the Save button to commit any changes.</span></span>

12. <span data-ttu-id="fcfb8-149">Pour activer le service d’approvisionnement Azure AD pour GitHub, définissez **l’état d’approvisionnement** sur **Activé** dans la section **Paramètres**</span><span class="sxs-lookup"><span data-stu-id="fcfb8-149">To enable the Azure AD provisioning service for GitHub, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

13. <span data-ttu-id="fcfb8-150">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="fcfb8-150">Click **Save**.</span></span> 

<span data-ttu-id="fcfb8-151">Cette opération démarre la synchronisation initiale des utilisateurs et/ou des groupes attribués à GitHub dans la section Utilisateurs et Groupes.</span><span class="sxs-lookup"><span data-stu-id="fcfb8-151">This operation starts the initial synchronization of any users and/or groups assigned to GitHub in the Users and Groups section.</span></span> <span data-ttu-id="fcfb8-152">La synchronisation initiale prend plus de temps que les synchronisations suivantes, qui se produisent environ toutes les 20 minutes, tant que le service est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="fcfb8-152">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="fcfb8-153">Vous pouvez utiliser la section **Détails de la synchronisation** pour surveiller la progression et suivre les liens vers les rapports d’activité d’approvisionnement, qui décrivent toutes les actions effectuées par le service d’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="fcfb8-153">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service.</span></span>

<span data-ttu-id="fcfb8-154">Pour plus d’informations sur la lecture des journaux d’approvisionnement Azure AD, consultez [Création de rapports sur l’approvisionnement automatique de comptes d’utilisateur](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="fcfb8-154">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="fcfb8-155">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="fcfb8-155">Additional resources</span></span>

* [<span data-ttu-id="fcfb8-156">Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise</span><span class="sxs-lookup"><span data-stu-id="fcfb8-156">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="fcfb8-157">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="fcfb8-157">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="fcfb8-158">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fcfb8-158">Next steps</span></span>

* [<span data-ttu-id="fcfb8-159">Découvrez comment consulter les journaux et obtenir des rapports sur l’activité d’approvisionnement</span><span class="sxs-lookup"><span data-stu-id="fcfb8-159">Learn how to review logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
