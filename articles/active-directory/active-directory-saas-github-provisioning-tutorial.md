---
title: "Didacticiel : configuration de GitHub pour l’approvisionnement automatique d’utilisateurs avec Azure Active Directory | Documents Microsoft"
description: "Découvrez comment tooconfigure Azure Active Directory tooautomatically disposition et la disposition de l’utilisateur des comptes tooGitHub."
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
ms.openlocfilehash: c1f0f7a42e4f8a94db3f409cd463e13bb1bc13bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-github-for-automatic-user-provisioning"></a><span data-ttu-id="873d2-103">Didacticiel : configuration de GitHub pour l’approvisionnement automatique d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="873d2-103">Tutorial: Configuring GitHub for Automatic User Provisioning</span></span>


<span data-ttu-id="873d2-104">objectif Hello de ce didacticiel est tooshow vous hello étapes que vous devez tooperform dans GitHub et Azure AD tooautomatically approvisionner et configurer des comptes d’utilisateur à partir d’Azure AD tooGitHub.</span><span class="sxs-lookup"><span data-stu-id="873d2-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in GitHub and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooGitHub.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="873d2-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="873d2-105">Prerequisites</span></span>

<span data-ttu-id="873d2-106">scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="873d2-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="873d2-107">Un locataire Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="873d2-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="873d2-108">Un locataire Github avec hello [offre commerciale](https://help.github.com/articles/organization-billing-plans/#business-plan) ou mieux activé</span><span class="sxs-lookup"><span data-stu-id="873d2-108">A Github tenant with hello [Business plan](https://help.github.com/articles/organization-billing-plans/#business-plan) or better enabled</span></span> 
*   <span data-ttu-id="873d2-109">Un compte d’utilisateur dans GitHub avec des autorisations d’administrateur</span><span class="sxs-lookup"><span data-stu-id="873d2-109">A user account in GitHub with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="873d2-110">Hello mise en service d’intégration de Azure AD s’appuie sur hello [GitHub SCIM API](https://developer.github.com/v3/scim/), qui est disponible tooGithub équipes sur le plan d’entreprise hello ou supérieures.</span><span class="sxs-lookup"><span data-stu-id="873d2-110">hello Azure AD provisioning integration relies on hello [GitHub SCIM API](https://developer.github.com/v3/scim/), which is available tooGithub teams on hello Business plan or better.</span></span>

## <a name="assigning-users-toogithub"></a><span data-ttu-id="873d2-111">Affectation d’utilisateurs tooGitHub</span><span class="sxs-lookup"><span data-stu-id="873d2-111">Assigning users tooGitHub</span></span>

<span data-ttu-id="873d2-112">Azure Active Directory utilise un concept appelé toodetermine « affectations » les utilisateurs qui doivent recevoir l’accès tooselected applications.</span><span class="sxs-lookup"><span data-stu-id="873d2-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="873d2-113">Dans le contexte de hello de configuration de compte automatique d’utilisateurs, seuls les utilisateurs de hello et les groupes qui ont été « affectés » application tooan dans Azure AD est synchronisé.</span><span class="sxs-lookup"><span data-stu-id="873d2-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="873d2-114">Avant de configurer et de l’activation de hello service de configuration, vous devez toodecide quels utilisateurs ou des groupes dans Azure AD représentent hello utilisateurs qui doivent accéder à application de GitHub tooyour.</span><span class="sxs-lookup"><span data-stu-id="873d2-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour GitHub app.</span></span> <span data-ttu-id="873d2-115">Après choisi, vous pouvez attribuer à ces applications de GitHub tooyour les utilisateurs en suivant les instructions hello ici :</span><span class="sxs-lookup"><span data-stu-id="873d2-115">Once decided, you can assign these users tooyour GitHub app by following hello instructions here:</span></span>

[<span data-ttu-id="873d2-116">Affecter une application d’entreprise tooan utilisateur ou un groupe</span><span class="sxs-lookup"><span data-stu-id="873d2-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toogithub"></a><span data-ttu-id="873d2-117">Conseils importants pour l’affectation d’utilisateurs tooGitHub</span><span class="sxs-lookup"><span data-stu-id="873d2-117">Important tips for assigning users tooGitHub</span></span>

*   <span data-ttu-id="873d2-118">Il est recommandé qu’un seul utilisateur Azure AD est attribué tooGitHub tootest hello est mise en service de configuration.</span><span class="sxs-lookup"><span data-stu-id="873d2-118">It is recommended that a single Azure AD user is assigned tooGitHub tootest hello provisioning configuration.</span></span> <span data-ttu-id="873d2-119">Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="873d2-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="873d2-120">Lorsque vous affectez un tooGitHub d’utilisateur, vous devez sélectionner soit hello **utilisateur** rôle, ou un autre valide spécifique à l’application (si disponible) dans la boîte de dialogue attribution hello.</span><span class="sxs-lookup"><span data-stu-id="873d2-120">When assigning a user tooGitHub, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="873d2-121">Hello **accès par défaut** rôle ne fonctionne pas pour la configuration, et ces utilisateurs sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="873d2-121">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-toogithub"></a><span data-ttu-id="873d2-122">Configuration tooGitHub de configuration de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="873d2-122">Configuring user provisioning tooGitHub</span></span> 

<span data-ttu-id="873d2-123">Cette section vous guide à travers de la connexion du compte d’utilisateur de votre tooGitHub AD Azure API de configuration et configurez hello toocreate du service de configuration, de mettre à jour et de désactiver les comptes d’utilisateur affecté dans GitHub en fonction de l’affectation d’utilisateurs et de groupes dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="873d2-123">This section guides you through connecting your Azure AD tooGitHub's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in GitHub based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="873d2-124">Vous pouvez également choisir tooenabled basé sur SAML Single Sign-On pour GitHub, en suivant les instructions hello fournies dans [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="873d2-124">You may also choose tooenabled SAML-based Single Sign-On for GitHub, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="873d2-125">L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que chacune de ces deux fonctionnalités compléte l’autre.</span><span class="sxs-lookup"><span data-stu-id="873d2-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toogithub-in-azure-ad"></a><span data-ttu-id="873d2-126">Configurer le compte d’automatique de l’utilisateur de configuration tooGitHub dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="873d2-126">Configure automatic user account provisioning tooGitHub in Azure AD</span></span>


1. <span data-ttu-id="873d2-127">Bonjour [portail Azure](https://portal.azure.com), parcourir toohello **Azure Active Directory > applications d’entreprise > toutes les applications** section.</span><span class="sxs-lookup"><span data-stu-id="873d2-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="873d2-128">Si vous avez déjà configuré GitHub pour l’authentification unique, recherchez votre instance de GitHub à l’aide du champ de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="873d2-128">If you have already configured GitHub for single sign-on, search for your instance of GitHub using hello search field.</span></span> <span data-ttu-id="873d2-129">Sinon, sélectionnez **ajouter** et recherchez **GitHub** dans la galerie d’applications hello.</span><span class="sxs-lookup"><span data-stu-id="873d2-129">Otherwise, select **Add** and search for **GitHub** in hello application gallery.</span></span> <span data-ttu-id="873d2-130">Sélectionnez GitHub à partir des résultats de recherche hello et ajoutez-le tooyour la liste des applications.</span><span class="sxs-lookup"><span data-stu-id="873d2-130">Select GitHub from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="873d2-131">Sélectionnez votre instance de GitHub, puis hello **Provisioning** onglet.</span><span class="sxs-lookup"><span data-stu-id="873d2-131">Select your instance of GitHub, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="873d2-132">Ensemble hello **Mode d’approvisionnement** trop**automatique**.</span><span class="sxs-lookup"><span data-stu-id="873d2-132">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![Approvisionnement GitHub](./media/active-directory-saas-github-provisioning-tutorial/GitHub1.png)

5. <span data-ttu-id="873d2-134">Sous hello **informations d’identification administrateur** , cliquez sur **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="873d2-134">Under hello **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="873d2-135">Cette opération ouvre une boîte de dialogue d’autorisation GitHub dans une nouvelle fenêtre du navigateur.</span><span class="sxs-lookup"><span data-stu-id="873d2-135">This operation opens a GitHub authorization dialog in a new browser window.</span></span> 

6. <span data-ttu-id="873d2-136">Dans la nouvelle fenêtre de hello, connectez-vous à GitHub à l’aide de votre compte d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="873d2-136">In hello new window, sign into GitHub using your Admin account.</span></span> <span data-ttu-id="873d2-137">Hello résultant d’autorisation boîte de dialogue, sélectionnez équipe de GitHub hello que vous souhaitez la préparation de tooenable, puis sélectionnez **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="873d2-137">In hello resulting authorization dialog, select hello GitHub team that you want tooenable provisioning for, and then select **Authorize**.</span></span> <span data-ttu-id="873d2-138">Une fois terminée, retournez toohello toocomplete portail Azure hello est mise en service de configuration.</span><span class="sxs-lookup"><span data-stu-id="873d2-138">Once completed, return toohello Azure portal toocomplete hello provisioning configuration.</span></span>

    ![Boîte de dialogue d’autorisation](./media/active-directory-saas-github-provisioning-tutorial/GitHub2.png)

7. <span data-ttu-id="873d2-140">Bonjour portail Azure, d’entrée **URL de client** et cliquez sur **tester la connexion** tooensure AD Azure peut se connecter tooyour GitHub application.</span><span class="sxs-lookup"><span data-stu-id="873d2-140">In hello Azure portal, input **Tenant URL** and click **Test Connection** tooensure Azure AD can connect tooyour GitHub app.</span></span> <span data-ttu-id="873d2-141">Si hello connexion échoue, vérifiez votre compte GitHub dispose des autorisations administratives et **URl de client** vous entrez correctement, puis essayez de hello à nouveau l’étape « Autoriser » (vous pouvez constituer **URL de client** par règle : « https : //api.github.com/scim/v2/organizations/ + < Organizations_name > », vous pouvez trouver votre organisation sous votre compte GitHub : **paramètres** > **organisations**).</span><span class="sxs-lookup"><span data-stu-id="873d2-141">If hello connection fails, ensure your GitHub account has Admin permissions and **Tenant URl** is inputted correctly, then try hello "Authorize" step again (you can constitute **Tenant URL** by rule: "https://api.github.com/scim/v2/organizations/ + <Organizations_name>", you can find your organizations under your GitHub account: **Settings** > **Organizations**).</span></span>

    ![Boîte de dialogue d’autorisation](./media/active-directory-saas-github-provisioning-tutorial/GitHub3.png)

8. <span data-ttu-id="873d2-143">Entrez hello adresse de messagerie d’une personne ou un groupe qui doit recevoir des notifications d’erreur approvisionnement hello **courrier électronique de Notification** champ et la case à cocher de vérification hello « envoient une notification par courrier électronique lorsqu’une défaillance se produit ».</span><span class="sxs-lookup"><span data-stu-id="873d2-143">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

9. <span data-ttu-id="873d2-144">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="873d2-144">Click **Save**.</span></span> 

10. <span data-ttu-id="873d2-145">Sous la section des mappages de hello, sélectionnez **tooGitHub de synchronisation Azure Active Directory Users**.</span><span class="sxs-lookup"><span data-stu-id="873d2-145">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooGitHub**.</span></span>

11. <span data-ttu-id="873d2-146">Bonjour **des mappages d’attributs** section, passez en revue les attributs utilisateur hello qui sont synchronisés à partir d’Azure AD tooGitHub.</span><span class="sxs-lookup"><span data-stu-id="873d2-146">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooGitHub.</span></span> <span data-ttu-id="873d2-147">Hello attributs sélectionnés en tant que **correspondance** propriétés sont des comptes d’utilisateur hello toomatch utilisés dans GitHub pour les opérations de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="873d2-147">hello attributes selected as **Matching** properties are used toomatch hello user accounts in GitHub for update operations.</span></span> <span data-ttu-id="873d2-148">Sélectionnez toocommit de bouton hello enregistrer toutes les modifications.</span><span class="sxs-lookup"><span data-stu-id="873d2-148">Select hello Save button toocommit any changes.</span></span>

12. <span data-ttu-id="873d2-149">tooenable hello service de configuration d’Azure AD pour GitHub, modification hello **état d’approvisionnement** trop**sur** Bonjour **paramètres** section</span><span class="sxs-lookup"><span data-stu-id="873d2-149">tooenable hello Azure AD provisioning service for GitHub, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

13. <span data-ttu-id="873d2-150">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="873d2-150">Click **Save**.</span></span> 

<span data-ttu-id="873d2-151">Cette opération démarre la synchronisation initiale d’utilisateurs et/ou groupes affectés tooGitHub Bonjour les utilisateurs et la section groupes de hello.</span><span class="sxs-lookup"><span data-stu-id="873d2-151">This operation starts hello initial synchronization of any users and/or groups assigned tooGitHub in hello Users and Groups section.</span></span> <span data-ttu-id="873d2-152">la synchronisation initiale Hello prend tooperform plus de temps que les synchronisations suivantes, qui se produisent toutes les 20 minutes environ tant que service de hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="873d2-152">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="873d2-153">Vous pouvez utiliser hello **détails de synchronisation** section toomonitor cours et suivre des rapports d’activité tooprovisioning des liens, qui décrivent toutes les actions effectuées par hello service de configuration.</span><span class="sxs-lookup"><span data-stu-id="873d2-153">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="873d2-154">Pour plus d’informations sur l’approvisionnement hello Azure AD tooread du mode de connexion, consultez [création de rapports sur la configuration de compte automatique d’utilisateurs](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="873d2-154">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="873d2-155">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="873d2-155">Additional resources</span></span>

* [<span data-ttu-id="873d2-156">Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise</span><span class="sxs-lookup"><span data-stu-id="873d2-156">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="873d2-157">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="873d2-157">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="873d2-158">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="873d2-158">Next steps</span></span>

* [<span data-ttu-id="873d2-159">Découvrez comment tooreview se connecte et obtenir des rapports sur l’activité de configuration</span><span class="sxs-lookup"><span data-stu-id="873d2-159">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
