---
title: "Didacticiel : Intégration d’Azure Active Directory à Concur | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Concur."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: df47f55f-a894-4e01-a82e-0dbf55fc8af1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 13ba364af26a5ce0f1d2b51aaa0f84a4c353b107
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-concur-for-user-provisioning"></a><span data-ttu-id="1028e-103">Didacticiel : Configuration de Concur pour l’approvisionnement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="1028e-103">Tutorial: Configuring Concur for User Provisioning</span></span>

<span data-ttu-id="1028e-104">objectif Hello de ce didacticiel est tooshow vous hello étapes que vous devez tooperform dans Concur et Azure AD tooautomatically approvisionner et configurer des comptes d’utilisateur à partir d’Azure AD tooConcur.</span><span class="sxs-lookup"><span data-stu-id="1028e-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Concur and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooConcur.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1028e-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1028e-105">Prerequisites</span></span>

<span data-ttu-id="1028e-106">scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1028e-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="1028e-107">Un locataire Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1028e-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="1028e-108">Un abonnement Concur pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="1028e-108">A Concur single sign-on enabled subscription.</span></span>
*   <span data-ttu-id="1028e-109">Un compte d’utilisateur dans Concur avec les autorisations d’administrateur d’équipe</span><span class="sxs-lookup"><span data-stu-id="1028e-109">A user account in Concur with Team Admin permissions.</span></span>

## <a name="assigning-users-tooconcur"></a><span data-ttu-id="1028e-110">Affectation d’utilisateurs tooConcur</span><span class="sxs-lookup"><span data-stu-id="1028e-110">Assigning users tooConcur</span></span>

<span data-ttu-id="1028e-111">Azure Active Directory utilise un concept appelé toodetermine « affectations » les utilisateurs qui doivent recevoir l’accès tooselected applications.</span><span class="sxs-lookup"><span data-stu-id="1028e-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="1028e-112">Dans le contexte de hello de configuration de compte automatique d’utilisateurs, seuls les utilisateurs de hello et les groupes qui ont été « affectés » application tooan dans Azure AD est synchronisé.</span><span class="sxs-lookup"><span data-stu-id="1028e-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="1028e-113">Avant de configurer et de l’activation de hello service de configuration, vous devez toodecide quels utilisateurs ou des groupes dans Azure AD représentent hello utilisateurs qui doivent accéder à application de Concur tooyour.</span><span class="sxs-lookup"><span data-stu-id="1028e-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Concur app.</span></span> <span data-ttu-id="1028e-114">Une fois décidé, vous pouvez attribuer ces applications de Concur tooyour les utilisateurs en suivant les instructions hello ici :</span><span class="sxs-lookup"><span data-stu-id="1028e-114">Once decided, you can assign these users tooyour Concur app by following hello instructions here:</span></span>

[<span data-ttu-id="1028e-115">Affecter une application d’entreprise tooan utilisateur ou un groupe</span><span class="sxs-lookup"><span data-stu-id="1028e-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-tooconcur"></a><span data-ttu-id="1028e-116">Conseils importants pour l’affectation d’utilisateurs tooConcur</span><span class="sxs-lookup"><span data-stu-id="1028e-116">Important tips for assigning users tooConcur</span></span>

*   <span data-ttu-id="1028e-117">Il est recommandé qu’un seul utilisateur Azure AD avoir tooConcur tootest hello est mise en service de configuration.</span><span class="sxs-lookup"><span data-stu-id="1028e-117">It is recommended that a single Azure AD user be assigned tooConcur tootest hello provisioning configuration.</span></span> <span data-ttu-id="1028e-118">Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="1028e-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="1028e-119">Lorsque vous affectez un tooConcur d’utilisateur, vous devez sélectionner un rôle d’utilisateur valide.</span><span class="sxs-lookup"><span data-stu-id="1028e-119">When assigning a user tooConcur, you must select a valid user role.</span></span> <span data-ttu-id="1028e-120">rôle de « Accès par défaut » Hello ne fonctionne pas pour la configuration.</span><span class="sxs-lookup"><span data-stu-id="1028e-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="1028e-121">Activer l’approvisionnement d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="1028e-121">Enable user provisioning</span></span>

<span data-ttu-id="1028e-122">Cette section vous guide à travers de la connexion du compte d’utilisateur de votre tooConcur AD Azure API de configuration et configurez hello toocreate du service de configuration, de mettre à jour et de désactiver les comptes d’utilisateur affecté dans Concur en fonction de l’affectation d’utilisateurs et de groupes dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1028e-122">This section guides you through connecting your Azure AD tooConcur's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Concur based on user and group assignment in Azure AD.</span></span>

> [!Tip] 
> <span data-ttu-id="1028e-123">Vous pouvez également choisir tooenabled basé sur SAML Single Sign-On pour Concur, en suivant les instructions hello fournies dans [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1028e-123">You may also choose tooenabled SAML-based Single Sign-On for Concur, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="1028e-124">L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que chacune de ces deux fonctionnalités compléte l’autre.</span><span class="sxs-lookup"><span data-stu-id="1028e-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning"></a><span data-ttu-id="1028e-125">approvisionnement des comptes utilisateur tooconfigure :</span><span class="sxs-lookup"><span data-stu-id="1028e-125">tooconfigure user account provisioning:</span></span>

<span data-ttu-id="1028e-126">objectif Hello de cette section est toooutline comment tooenable configuration d’utilisateur Active Directory de comptes de tooConcur.</span><span class="sxs-lookup"><span data-stu-id="1028e-126">hello objective of this section is toooutline how tooenable provisioning of Active Directory user accounts tooConcur.</span></span>

<span data-ttu-id="1028e-127">applications tooenable dans hello Expense Service, il y a une configuration correcte toobe et l’utilisation d’un profil d’administrateur de Service Web.</span><span class="sxs-lookup"><span data-stu-id="1028e-127">tooenable apps in hello Expense Service, there has toobe proper setup and use of a Web Service Admin profile.</span></span> <span data-ttu-id="1028e-128">N’ajoutez pas hello WS Admin rôle tooyour profil d’administrateur existant que vous utilisez pour les fonctions administratives T & E.</span><span class="sxs-lookup"><span data-stu-id="1028e-128">Don't add hello WS Admin role tooyour existing administrator profile that you use for T&E administrative functions.</span></span>

<span data-ttu-id="1028e-129">Concur Consultants ou administrateur de client de hello doit créer un profil d’administrateur de Service Web distinct et administrateur de Client hello doit utiliser ce profil pour les fonctions d’administrateur de Services Web hello (par exemple, l’activation des applications).</span><span class="sxs-lookup"><span data-stu-id="1028e-129">Concur Consultants or hello client administrator must create a distinct Web Service Administrator profile and hello Client administrator must use this profile for hello Web Services Administrator functions (for example, enabling apps).</span></span> <span data-ttu-id="1028e-130">Ces profils doivent être conservés séparément à partir de quotidienne T & E profil d’administrateur l’administrateur de client hello (hello T & profil d’administrateur E ne doivent pas avoir rôle d’écart hello attribué).</span><span class="sxs-lookup"><span data-stu-id="1028e-130">These profiles must be kept separate from hello client administrator's daily T&E admin profile (hello T&E admin profile should not have hello WSAdmin role assigned).</span></span>

<span data-ttu-id="1028e-131">Lorsque vous créez hello profil toobe est utilisé pour activer l’application hello, entrez le nom de l’administrateur de client hello dans les champs du profil utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="1028e-131">When you create hello profile toobe used for enabling hello app, enter hello client administrator's name into hello user profile fields.</span></span> <span data-ttu-id="1028e-132">Cela affecte le profil toohello de la propriété.</span><span class="sxs-lookup"><span data-stu-id="1028e-132">This assigns ownership toohello profile.</span></span> <span data-ttu-id="1028e-133">Après la création d’un ou plusieurs profils, le client de hello doit se connecter avec ce hello tooclick de profil «*activer*» bouton pour une application partenaire dans le menu des Services Web hello.</span><span class="sxs-lookup"><span data-stu-id="1028e-133">Once one or more profiles is created, hello client must log in with this profile tooclick hello "*Enable*" button for a Partner App within hello Web Services menu.</span></span>

<span data-ttu-id="1028e-134">Cette action ne doit pas être exécutée avec le profil de hello qu’ils utilisent pour l’administration T & E normale pour hello suivant raisons.</span><span class="sxs-lookup"><span data-stu-id="1028e-134">For hello following reasons, this action should not be done with hello profile they use for normal T&E administration.</span></span>

* <span data-ttu-id="1028e-135">Hello client a toobe hello qui clique sur «*Oui*» sur la boîte de dialogue de hello qui s’affiche après l’activation d’une application.</span><span class="sxs-lookup"><span data-stu-id="1028e-135">hello client has toobe hello one that clicks "*Yes*" on hello dialogue window that is displayed after an app is enabled.</span></span> <span data-ttu-id="1028e-136">Ce clic signifie que les clients hello sont disposé pour hello partenaire application tooaccess leurs données, afin de vous ou hello partenaire cliquez sur ce bouton Oui.</span><span class="sxs-lookup"><span data-stu-id="1028e-136">This click acknowledges hello client is willing for hello Partner application tooaccess their data, so you or hello Partner cannot click that Yes button.</span></span>

* <span data-ttu-id="1028e-137">Si un administrateur de clients ayant activé une application à l’aide de T Bonjour profil d’administrateur E quitte l’entreprise hello (entraînant profil hello cessera), toute application activée à l’aide de ce profil ne fonctionne pas tant que l’application hello est activée avec un autre active WS Admin profil.</span><span class="sxs-lookup"><span data-stu-id="1028e-137">If a client administrator that has enabled an app using hello T&E admin profile leaves hello company (resulting in hello profile being inactivated), any apps enabled using that profile does not function until hello app is enabled with another active WS Admin profile.</span></span> <span data-ttu-id="1028e-138">C’est pourquoi vous êtes supposé toocreate les profils WS Admin distincts.</span><span class="sxs-lookup"><span data-stu-id="1028e-138">This is why you are supposed toocreate distinct WS Admin profiles.</span></span>

* <span data-ttu-id="1028e-139">Si un administrateur quitte l’entreprise de hello, nom de hello associée toohello profil WS Admin peut être administrateur de remplacement toohello modifiés si vous le souhaitez sans affecter hello activée application car ce profil n’a pas besoin d’être désactivé.</span><span class="sxs-lookup"><span data-stu-id="1028e-139">If an administrator leaves hello company, hello name associated toohello WS Admin profile can be changed toohello replacement administrator if desired without impacting hello enabled app because that profile does not need inactivated.</span></span>

<span data-ttu-id="1028e-140">**configuration, de l’utilisateur tooconfigure effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1028e-140">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="1028e-141">Ouvrez une session sur tooyour **Concur** client.</span><span class="sxs-lookup"><span data-stu-id="1028e-141">Log on tooyour **Concur** tenant.</span></span>

2. <span data-ttu-id="1028e-142">À partir de hello **Administration** menu, sélectionnez **Services Web**.</span><span class="sxs-lookup"><span data-stu-id="1028e-142">From hello **Administration** menu, select **Web Services**.</span></span>
   
    <span data-ttu-id="1028e-143">![Client Concur](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Client Concur")</span><span class="sxs-lookup"><span data-stu-id="1028e-143">![Concur tenant](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Concur tenant")</span></span>

3. <span data-ttu-id="1028e-144">Sur hello gauche, à partir de hello **Services Web** volet, sélectionnez **Enable Partner Application**.</span><span class="sxs-lookup"><span data-stu-id="1028e-144">On hello left side, from hello **Web Services** pane, select **Enable Partner Application**.</span></span>
   
    <span data-ttu-id="1028e-145">![Enable Partner Application](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "Enable Partner Application")</span><span class="sxs-lookup"><span data-stu-id="1028e-145">![Enable Partner Application](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "Enable Partner Application")</span></span>

4. <span data-ttu-id="1028e-146">À partir de hello **Enable Application** liste, sélectionnez **Azure Active Directory**, puis cliquez sur **activer**.</span><span class="sxs-lookup"><span data-stu-id="1028e-146">From hello **Enable Application** list, select **Azure Active Directory**, and then click **Enable**.</span></span>
   
    <span data-ttu-id="1028e-147">![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span><span class="sxs-lookup"><span data-stu-id="1028e-147">![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span></span>

5. <span data-ttu-id="1028e-148">Cliquez sur **Oui** tooclose hello **confirmer l’Action** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1028e-148">Click **Yes** tooclose hello **Confirm Action** dialog.</span></span>
   
    <span data-ttu-id="1028e-149">![Confirm Action](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "Confirm Action")</span><span class="sxs-lookup"><span data-stu-id="1028e-149">![Confirm Action](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "Confirm Action")</span></span>

6. <span data-ttu-id="1028e-150">Bonjour [portail Azure](https://portal.azure.com), parcourir toohello **Azure Active Directory > applications d’entreprise > toutes les applications** section.</span><span class="sxs-lookup"><span data-stu-id="1028e-150">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

7. <span data-ttu-id="1028e-151">Si vous avez déjà configuré Concur pour l’authentification unique, recherchez votre instance de Concur à l’aide du champ de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="1028e-151">If you have already configured Concur for single sign-on, search for your instance of Concur using hello search field.</span></span> <span data-ttu-id="1028e-152">Sinon, sélectionnez **ajouter** et recherchez **Concur** dans la galerie d’applications hello.</span><span class="sxs-lookup"><span data-stu-id="1028e-152">Otherwise, select **Add** and search for **Concur** in hello application gallery.</span></span> <span data-ttu-id="1028e-153">Sélectionnez Concur à partir des résultats de recherche hello et ajoutez-le tooyour la liste des applications.</span><span class="sxs-lookup"><span data-stu-id="1028e-153">Select Concur from hello search results, and add it tooyour list of applications.</span></span>

8. <span data-ttu-id="1028e-154">Sélectionnez votre instance de Concur, puis hello **Provisioning** onglet.</span><span class="sxs-lookup"><span data-stu-id="1028e-154">Select your instance of Concur, then select hello **Provisioning** tab.</span></span>

9. <span data-ttu-id="1028e-155">Ensemble hello **Mode d’approvisionnement** trop**automatique**.</span><span class="sxs-lookup"><span data-stu-id="1028e-155">Set hello **Provisioning Mode** too**Automatic**.</span></span> 
 
    ![approvisionnement](./media/active-directory-saas-concur-provisioning-tutorial/provisioning.png)

10. <span data-ttu-id="1028e-157">Sous hello **informations d’identification administrateur** section, entrez hello **nom d’utilisateur** et hello **mot de passe** de l’administrateur Concur.</span><span class="sxs-lookup"><span data-stu-id="1028e-157">Under hello **Admin Credentials** section, enter hello **user name** and hello **password** of your Concur administrator.</span></span>

11. <span data-ttu-id="1028e-158">Bonjour portail Azure, cliquez sur **tester la connexion** tooensure AD Azure peut se connecter tooyour Concur application.</span><span class="sxs-lookup"><span data-stu-id="1028e-158">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Concur app.</span></span> <span data-ttu-id="1028e-159">Si hello connexion échoue, assurez-vous que votre compte de Concur dispose d’autorisations d’administrateur d’équipe.</span><span class="sxs-lookup"><span data-stu-id="1028e-159">If hello connection fails, ensure your Concur account has Team Admin permissions.</span></span>

12. <span data-ttu-id="1028e-160">Entrez hello adresse de messagerie d’une personne ou un groupe qui doit recevoir des notifications d’erreur approvisionnement hello **courrier électronique de Notification** champ et la case à cocher hello.</span><span class="sxs-lookup"><span data-stu-id="1028e-160">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

13. <span data-ttu-id="1028e-161">Cliquez sur **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="1028e-161">Click **Save.**</span></span>

14. <span data-ttu-id="1028e-162">Sous la section des mappages de hello, sélectionnez **tooConcur de synchronisation Azure Active Directory Users.**</span><span class="sxs-lookup"><span data-stu-id="1028e-162">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooConcur.**</span></span>

15. <span data-ttu-id="1028e-163">Bonjour **des mappages d’attributs** section, passez en revue les attributs utilisateur hello qui sont synchronisés à partir d’Azure AD tooConcur.</span><span class="sxs-lookup"><span data-stu-id="1028e-163">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooConcur.</span></span> <span data-ttu-id="1028e-164">Hello attributs sélectionnés en tant que **correspondance** propriétés sont des comptes d’utilisateur hello toomatch utilisés dans Concur pour les opérations de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="1028e-164">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Concur for update operations.</span></span> <span data-ttu-id="1028e-165">Sélectionnez toocommit de bouton hello enregistrer toutes les modifications.</span><span class="sxs-lookup"><span data-stu-id="1028e-165">Select hello Save button toocommit any changes.</span></span>

16. <span data-ttu-id="1028e-166">tooenable hello service de configuration d’Azure AD pour Concur, modification hello **état d’approvisionnement** trop**sur** Bonjour **paramètres** section</span><span class="sxs-lookup"><span data-stu-id="1028e-166">tooenable hello Azure AD provisioning service for Concur, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

17. <span data-ttu-id="1028e-167">Cliquez sur **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="1028e-167">Click **Save.**</span></span>

<span data-ttu-id="1028e-168">Vous pouvez à présent créer un compte de test.</span><span class="sxs-lookup"><span data-stu-id="1028e-168">You can now create a test account.</span></span> <span data-ttu-id="1028e-169">Attendez que les minutes too20 tooverify hello compte a été synchronisé tooConcur.</span><span class="sxs-lookup"><span data-stu-id="1028e-169">Wait for up too20 minutes tooverify that hello account has been synchronized tooConcur.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1028e-170">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="1028e-170">Additional resources</span></span>

* [<span data-ttu-id="1028e-171">Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise</span><span class="sxs-lookup"><span data-stu-id="1028e-171">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1028e-172">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="1028e-172">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="1028e-173">Configurer l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="1028e-173">Configure Single Sign-on</span></span>](active-directory-saas-concur-tutorial.md)

