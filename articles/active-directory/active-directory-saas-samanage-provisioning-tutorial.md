---
title: "Didacticiel : Configuration de Samanage pour l’approvisionnement automatique d’utilisateurs avec Azure Active Directory | Microsoft Docs"
description: "Découvrez comment tooconfigure Azure Active Directory tooautomatically disposition et la disposition de l’utilisateur des comptes tooSamanage."
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
ms.openlocfilehash: 6cb36d2cc6ce33da4f8ebba65d138bfd4f2aca9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-samanage-for-automatic-user-provisioning"></a><span data-ttu-id="983fa-103">Didacticiel : configuration de Samanage pour l’approvisionnement automatique d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="983fa-103">Tutorial: Configuring Samanage for Automatic User Provisioning</span></span>


<span data-ttu-id="983fa-104">objectif Hello de ce didacticiel est tooshow vous hello étapes que vous devez tooperform dans Samanage et Azure AD tooautomatically approvisionner et configurer des comptes d’utilisateur à partir d’Azure AD tooSamanage.</span><span class="sxs-lookup"><span data-stu-id="983fa-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Samanage and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooSamanage.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="983fa-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="983fa-105">Prerequisites</span></span>

<span data-ttu-id="983fa-106">scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="983fa-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="983fa-107">Un locataire Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="983fa-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="983fa-108">Un locataire Samanage avec hello [plan professionnel](https://www.samanage.com/pricing/) ou mieux activé</span><span class="sxs-lookup"><span data-stu-id="983fa-108">A Samanage tenant with hello [Professional plan](https://www.samanage.com/pricing/) or better enabled</span></span> 
*   <span data-ttu-id="983fa-109">Un compte d’utilisateur dans Samanage avec des autorisations d’administrateur</span><span class="sxs-lookup"><span data-stu-id="983fa-109">A user account in Samanage with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="983fa-110">Hello mise en service d’intégration de Azure AD s’appuie sur hello [API REST de Samanage](https://www.samanage.com/api/), qui est équipes tooSamanage disponible sur hello Professionnel planifier ou mieux.</span><span class="sxs-lookup"><span data-stu-id="983fa-110">hello Azure AD provisioning integration relies on hello [Samanage REST API](https://www.samanage.com/api/), which is available tooSamanage teams on hello Professional plan or better.</span></span>

## <a name="assigning-users-toosamanage"></a><span data-ttu-id="983fa-111">Affectation d’utilisateurs tooSamanage</span><span class="sxs-lookup"><span data-stu-id="983fa-111">Assigning users tooSamanage</span></span>

<span data-ttu-id="983fa-112">Azure Active Directory utilise un concept appelé toodetermine « affectations » les utilisateurs qui doivent recevoir l’accès tooselected applications.</span><span class="sxs-lookup"><span data-stu-id="983fa-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="983fa-113">Dans le contexte de hello de configuration de compte automatique d’utilisateurs, seuls les utilisateurs de hello et les groupes qui ont été « affectés » application tooan dans Azure AD est synchronisé.</span><span class="sxs-lookup"><span data-stu-id="983fa-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="983fa-114">Avant de configurer et de l’activation de hello service de configuration, vous devez toodecide quels utilisateurs ou des groupes dans Azure AD représentent hello utilisateurs qui doivent accéder à application de Samanage tooyour.</span><span class="sxs-lookup"><span data-stu-id="983fa-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Samanage app.</span></span> <span data-ttu-id="983fa-115">Une fois décidé, vous pouvez attribuer ces applications de Samanage tooyour les utilisateurs en suivant les instructions hello ici :</span><span class="sxs-lookup"><span data-stu-id="983fa-115">Once decided, you can assign these users tooyour Samanage app by following hello instructions here:</span></span>

[<span data-ttu-id="983fa-116">Affecter une application d’entreprise tooan utilisateur ou un groupe</span><span class="sxs-lookup"><span data-stu-id="983fa-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toosamanage"></a><span data-ttu-id="983fa-117">Conseils importants pour l’affectation d’utilisateurs tooSamanage</span><span class="sxs-lookup"><span data-stu-id="983fa-117">Important tips for assigning users tooSamanage</span></span>

*   <span data-ttu-id="983fa-118">Il est recommandé qu’un seul utilisateur Azure AD est attribué tooSamanage tootest hello est mise en service de configuration.</span><span class="sxs-lookup"><span data-stu-id="983fa-118">It is recommended that a single Azure AD user is assigned tooSamanage tootest hello provisioning configuration.</span></span> <span data-ttu-id="983fa-119">Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="983fa-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="983fa-120">Lorsque vous affectez un tooSamanage d’utilisateur, vous devez sélectionner soit hello **utilisateur** rôle, ou un autre valide spécifique à l’application (si disponible) dans la boîte de dialogue attribution hello.</span><span class="sxs-lookup"><span data-stu-id="983fa-120">When assigning a user tooSamanage, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="983fa-121">Hello **accès par défaut** rôle ne fonctionne pas pour la configuration, et ces utilisateurs sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="983fa-121">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>

> [!NOTE]
> <span data-ttu-id="983fa-122">Comme une fonctionnalité ajoutée, hello configuration service lit tous les rôles personnalisés définis dans Samanage et les importe dans Azure AD où ils peuvent être sélectionnées dans la boîte de dialogue Sélectionner un rôle hello.</span><span class="sxs-lookup"><span data-stu-id="983fa-122">As an added feature, hello provisioning service reads any custom roles defined in Samanage, and imports them into Azure AD where they can be selected in hello Select Role dialog.</span></span> <span data-ttu-id="983fa-123">Ces rôles seront visibles dans hello portail Azure après hello mise en service du service est activé et un cycle de synchronisation est terminée.</span><span class="sxs-lookup"><span data-stu-id="983fa-123">These roles will be visible in hello Azure portal after hello provisioning service is enabled and one synchronization cycle has completed.</span></span>

## <a name="configuring-user-provisioning-toosamanage"></a><span data-ttu-id="983fa-124">Configuration tooSamanage de configuration de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="983fa-124">Configuring user provisioning tooSamanage</span></span> 

<span data-ttu-id="983fa-125">Cette section vous guide à travers de la connexion du compte d’utilisateur de votre tooSamanage AD Azure API de configuration et configurez hello toocreate du service de configuration, de mettre à jour et de désactiver les comptes d’utilisateur affecté dans Samanage en fonction de l’affectation d’utilisateurs et de groupes dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="983fa-125">This section guides you through connecting your Azure AD tooSamanage's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Samanage based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="983fa-126">Vous pouvez également choisir tooenabled basé sur SAML Single Sign-On pour Samanage, en suivant les instructions hello fournies dans [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="983fa-126">You may also choose tooenabled SAML-based Single Sign-On for Samanage, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="983fa-127">L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que chacune de ces deux fonctionnalités compléte l’autre.</span><span class="sxs-lookup"><span data-stu-id="983fa-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toosamanage-in-azure-ad"></a><span data-ttu-id="983fa-128">Configurez le compte d’automatique de l’utilisateur de configuration tooSamanage dans Azure AD :</span><span class="sxs-lookup"><span data-stu-id="983fa-128">Configure automatic user account provisioning tooSamanage in Azure AD:</span></span>


1. <span data-ttu-id="983fa-129">Bonjour [portail Azure](https://portal.azure.com), parcourir toohello **Azure Active Directory > applications d’entreprise > toutes les applications** section.</span><span class="sxs-lookup"><span data-stu-id="983fa-129">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="983fa-130">Si vous avez déjà configuré Samanage pour l’authentification unique, recherchez votre instance de Samanage à l’aide du champ de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="983fa-130">If you have already configured Samanage for single sign-on, search for your instance of Samanage using hello search field.</span></span> <span data-ttu-id="983fa-131">Sinon, sélectionnez **ajouter** et recherchez **Samanage** dans la galerie d’applications hello.</span><span class="sxs-lookup"><span data-stu-id="983fa-131">Otherwise, select **Add** and search for **Samanage** in hello application gallery.</span></span> <span data-ttu-id="983fa-132">Sélectionnez Samanage à partir des résultats de recherche hello et ajoutez-le tooyour la liste des applications.</span><span class="sxs-lookup"><span data-stu-id="983fa-132">Select Samanage from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="983fa-133">Sélectionnez votre instance de Samanage, puis hello **Provisioning** onglet.</span><span class="sxs-lookup"><span data-stu-id="983fa-133">Select your instance of Samanage, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="983fa-134">Ensemble hello **Mode d’approvisionnement** trop**automatique**.</span><span class="sxs-lookup"><span data-stu-id="983fa-134">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![Approvisionnement de Samanage](./media/active-directory-saas-samanage-provisioning-tutorial/Samanage1.png)

5. <span data-ttu-id="983fa-136">Sous hello **informations d’identification administrateur** section, entrée hello **Admin Username & mot de passe administrateur** du compte de votre Samanage.</span><span class="sxs-lookup"><span data-stu-id="983fa-136">Under hello **Admin Credentials** section, input hello **Admin Username&Admin Password** of your Samanage's account.</span></span> 

6. <span data-ttu-id="983fa-137">Bonjour portail Azure, cliquez sur **tester la connexion** tooensure AD Azure peut se connecter tooyour Samanage application.</span><span class="sxs-lookup"><span data-stu-id="983fa-137">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Samanage app.</span></span> <span data-ttu-id="983fa-138">Si hello connexion échoue, vérifiez que votre compte de Samanage a des autorisations d’administrateur et recommencez l’étape 5.</span><span class="sxs-lookup"><span data-stu-id="983fa-138">If hello connection fails, ensure your Samanage account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="983fa-139">Entrez hello adresse de messagerie d’une personne ou un groupe qui doit recevoir des notifications d’erreur approvisionnement hello **courrier électronique de Notification** champ et la case à cocher de vérification hello « envoient une notification par courrier électronique lorsqu’une défaillance se produit ».</span><span class="sxs-lookup"><span data-stu-id="983fa-139">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="983fa-140">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="983fa-140">Click **Save**.</span></span> 

9. <span data-ttu-id="983fa-141">Sous la section des mappages de hello, sélectionnez **tooSamanage de synchronisation Azure Active Directory Users**.</span><span class="sxs-lookup"><span data-stu-id="983fa-141">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooSamanage**.</span></span>

10. <span data-ttu-id="983fa-142">Bonjour **des mappages d’attributs** section, passez en revue les attributs utilisateur hello qui sont synchronisés à partir d’Azure AD tooSamanage.</span><span class="sxs-lookup"><span data-stu-id="983fa-142">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooSamanage.</span></span> <span data-ttu-id="983fa-143">Hello attributs sélectionnés en tant que **correspondance** propriétés sont des comptes d’utilisateur hello toomatch utilisés dans Samanage pour les opérations de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="983fa-143">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Samanage for update operations.</span></span> <span data-ttu-id="983fa-144">Sélectionnez toocommit de bouton hello enregistrer toutes les modifications.</span><span class="sxs-lookup"><span data-stu-id="983fa-144">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="983fa-145">tooenable hello service de configuration d’Azure AD pour Samanage, la modification hello **état d’approvisionnement** trop**sur** Bonjour **paramètres** section</span><span class="sxs-lookup"><span data-stu-id="983fa-145">tooenable hello Azure AD provisioning service for Samanage, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="983fa-146">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="983fa-146">Click **Save**.</span></span> 

<span data-ttu-id="983fa-147">Cette opération démarre la synchronisation initiale d’utilisateurs et/ou groupes affectés tooSamanage Bonjour les utilisateurs et la section groupes de hello.</span><span class="sxs-lookup"><span data-stu-id="983fa-147">This operation starts hello initial synchronization of any users and/or groups assigned tooSamanage in hello Users and Groups section.</span></span> <span data-ttu-id="983fa-148">la synchronisation initiale Hello prend tooperform plus de temps que les synchronisations suivantes, qui se produisent toutes les 20 minutes environ tant que service de hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="983fa-148">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="983fa-149">Vous pouvez utiliser hello **détails de synchronisation** section toomonitor cours et suivre des rapports d’activité tooprovisioning des liens, qui décrivent toutes les actions effectuées par hello service de configuration.</span><span class="sxs-lookup"><span data-stu-id="983fa-149">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="983fa-150">Pour plus d’informations sur l’approvisionnement hello Azure AD tooread du mode de connexion, consultez [création de rapports sur la configuration de compte automatique d’utilisateurs](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="983fa-150">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="983fa-151">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="983fa-151">Additional resources</span></span>

* [<span data-ttu-id="983fa-152">Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise</span><span class="sxs-lookup"><span data-stu-id="983fa-152">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="983fa-153">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="983fa-153">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="983fa-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="983fa-154">Next steps</span></span>

* [<span data-ttu-id="983fa-155">Découvrez comment tooreview se connecte et obtenir des rapports sur l’activité de configuration</span><span class="sxs-lookup"><span data-stu-id="983fa-155">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
