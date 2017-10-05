---
title: "Didacticiel : Intégration d’Azure Active Directory à Concur | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Concur."
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
ms.openlocfilehash: cd35b6e2dc3171e9cffdb820bbc5b0d45ff58e07
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-concur-for-user-provisioning"></a><span data-ttu-id="d8deb-103">Didacticiel : Configuration de Concur pour l’approvisionnement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="d8deb-103">Tutorial: Configuring Concur for User Provisioning</span></span>

<span data-ttu-id="d8deb-104">L’objectif de ce didacticiel est de vous montrer les étapes à effectuer dans Concur et Azure AD pour approvisionner et retirer automatiquement des comptes utilisateur d’Azure AD vers Concur.</span><span class="sxs-lookup"><span data-stu-id="d8deb-104">The objective of this tutorial is to show you the steps you need to perform in Concur and Azure AD to automatically provision and de-provision user accounts from Azure AD to Concur.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d8deb-105">Prérequis</span><span class="sxs-lookup"><span data-stu-id="d8deb-105">Prerequisites</span></span>

<span data-ttu-id="d8deb-106">Le scénario décrit dans ce didacticiel part du principe que vous disposez des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d8deb-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="d8deb-107">Un locataire Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d8deb-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="d8deb-108">Un abonnement Concur pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="d8deb-108">A Concur single sign-on enabled subscription.</span></span>
*   <span data-ttu-id="d8deb-109">Un compte d’utilisateur dans Concur avec les autorisations d’administrateur d’équipe</span><span class="sxs-lookup"><span data-stu-id="d8deb-109">A user account in Concur with Team Admin permissions.</span></span>

## <a name="assigning-users-to-concur"></a><span data-ttu-id="d8deb-110">Affectation d’utilisateurs à Concur</span><span class="sxs-lookup"><span data-stu-id="d8deb-110">Assigning users to Concur</span></span>

<span data-ttu-id="d8deb-111">Azure Active Directory utilise un concept appelé « affectations » pour déterminer les utilisateurs devant recevoir l’accès aux applications sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="d8deb-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="d8deb-112">Dans le cadre de l’approvisionnement automatique de comptes d’utilisateur, les utilisateurs et les groupes qui ont été « affectés » à une application dans Azure AD sont synchronisés.</span><span class="sxs-lookup"><span data-stu-id="d8deb-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="d8deb-113">Avant de configurer et d’activer le service d’approvisionnement, vous devez déterminer quels utilisateurs et/ou groupes dans Azure AD représentent les utilisateurs qui ont besoin d’accéder à votre application Concur.</span><span class="sxs-lookup"><span data-stu-id="d8deb-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Concur app.</span></span> <span data-ttu-id="d8deb-114">Une fois que vous avez choisi, vous pouvez affecter ces utilisateurs à votre application Concur en suivant les instructions fournies ici :</span><span class="sxs-lookup"><span data-stu-id="d8deb-114">Once decided, you can assign these users to your Concur app by following the instructions here:</span></span>

[<span data-ttu-id="d8deb-115">Affecter un utilisateur ou un groupe à une application d’entreprise</span><span class="sxs-lookup"><span data-stu-id="d8deb-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-concur"></a><span data-ttu-id="d8deb-116">Conseils importants pour l’affectation d’utilisateurs à Concur</span><span class="sxs-lookup"><span data-stu-id="d8deb-116">Important tips for assigning users to Concur</span></span>

*   <span data-ttu-id="d8deb-117">Nous vous recommandons de n’affecter qu’un seul utilisateur Azure AD à Concur pour tester la configuration de l’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="d8deb-117">It is recommended that a single Azure AD user be assigned to Concur to test the provisioning configuration.</span></span> <span data-ttu-id="d8deb-118">Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="d8deb-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="d8deb-119">Quand vous affectez un utilisateur à Concur, vous devez sélectionner un rôle d’utilisateur valide.</span><span class="sxs-lookup"><span data-stu-id="d8deb-119">When assigning a user to Concur, you must select a valid user role.</span></span> <span data-ttu-id="d8deb-120">Le rôle « Accès par défaut » ne fonctionne pas pour l’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="d8deb-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="d8deb-121">Activer l’approvisionnement d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="d8deb-121">Enable user provisioning</span></span>

<span data-ttu-id="d8deb-122">Cette section explique comment connecter votre annuaire Azure AD à l’API d’approvisionnement de comptes d’utilisateur de Concur pour créer, mettre à jour et désactiver les comptes d’utilisateur affectés dans Concur en fonction des attributions d’utilisateurs et de groupes dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d8deb-122">This section guides you through connecting your Azure AD to Concur's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Concur based on user and group assignment in Azure AD.</span></span>

> [!Tip] 
> <span data-ttu-id="d8deb-123">Vous pouvez également choisir d’activer l’authentification unique basée sur SAML pour Concur en suivant les instructions fournies dans le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d8deb-123">You may also choose to enabled SAML-based Single Sign-On for Concur, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="d8deb-124">L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que chacune de ces deux fonctionnalités complète l’autre.</span><span class="sxs-lookup"><span data-stu-id="d8deb-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning"></a><span data-ttu-id="d8deb-125">Pour configurer l’approvisionnement de comptes d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="d8deb-125">To configure user account provisioning:</span></span>

<span data-ttu-id="d8deb-126">Cette section décrit comment activer l’approvisionnement des comptes d’utilisateurs Active Directory sur Concur.</span><span class="sxs-lookup"><span data-stu-id="d8deb-126">The objective of this section is to outline how to enable provisioning of Active Directory user accounts to Concur.</span></span>

<span data-ttu-id="d8deb-127">Pour activer des applications dans le service Dépenses, vous devez vous assurer que la bonne configuration est définie et qu’un profil d’administrateur des services Web est utilisé.</span><span class="sxs-lookup"><span data-stu-id="d8deb-127">To enable apps in the Expense Service, there has to be proper setup and use of a Web Service Admin profile.</span></span> <span data-ttu-id="d8deb-128">N’ajoutez pas le rôle WS Admin au profil d’administrateur existant que vous utilisez pour les fonctions administratives T&E.</span><span class="sxs-lookup"><span data-stu-id="d8deb-128">Don't add the WS Admin role to your existing administrator profile that you use for T&E administrative functions.</span></span>

<span data-ttu-id="d8deb-129">Concur Consultants ou l’administrateur des clients doit créer un profil d’administrateur des services web distinct, et l’administrateur des clients doit utiliser ce profil pour les fonctions d’administrateur des services web (par exemple pour l’activation d’applications).</span><span class="sxs-lookup"><span data-stu-id="d8deb-129">Concur Consultants or the client administrator must create a distinct Web Service Administrator profile and the Client administrator must use this profile for the Web Services Administrator functions (for example, enabling apps).</span></span> <span data-ttu-id="d8deb-130">Ces profils doivent être séparés du profil d’administrateur T&E utilisé quotidiennement par l’administrateur des clients (le profil d’administrateur T&E ne doit pas se voir affecter le rôle WS Admin).</span><span class="sxs-lookup"><span data-stu-id="d8deb-130">These profiles must be kept separate from the client administrator's daily T&E admin profile (the T&E admin profile should not have the WSAdmin role assigned).</span></span>

<span data-ttu-id="d8deb-131">Quand vous créez le profil à utiliser pour l’activation de l’application, entrez le nom de l’administrateur des clients dans les champs du profil utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d8deb-131">When you create the profile to be used for enabling the app, enter the client administrator's name into the user profile fields.</span></span> <span data-ttu-id="d8deb-132">Cela permet d’affecter la propriété au profil.</span><span class="sxs-lookup"><span data-stu-id="d8deb-132">This assigns ownership to the profile.</span></span> <span data-ttu-id="d8deb-133">Une fois qu’un ou plusieurs profils ont été créés, le client doit se connecter avec ce profil pour pouvoir cliquer sur le bouton « *Activer* » d’une application partenaire dans le menu Services Web.</span><span class="sxs-lookup"><span data-stu-id="d8deb-133">Once one or more profiles is created, the client must log in with this profile to click the "*Enable*" button for a Partner App within the Web Services menu.</span></span>

<span data-ttu-id="d8deb-134">Cette action ne doit pas être exécutée avec le profil utilisé pour l’administration T&E normale, et ce pour les raisons suivantes.</span><span class="sxs-lookup"><span data-stu-id="d8deb-134">For the following reasons, this action should not be done with the profile they use for normal T&E administration.</span></span>

* <span data-ttu-id="d8deb-135">Le client doit être celui qui clique sur *Oui* dans la boîte de dialogue qui s’affiche quand une application est activée.</span><span class="sxs-lookup"><span data-stu-id="d8deb-135">The client has to be the one that clicks "*Yes*" on the dialogue window that is displayed after an app is enabled.</span></span> <span data-ttu-id="d8deb-136">Ce clic signifie que le client accepte que l’application partenaire accède aux données. Par conséquent, vous ou le partenaire ne pouvez pas cliquer sur le bouton Oui.</span><span class="sxs-lookup"><span data-stu-id="d8deb-136">This click acknowledges the client is willing for the Partner application to access their data, so you or the Partner cannot click that Yes button.</span></span>

* <span data-ttu-id="d8deb-137">Si un administrateur de clients ayant activé une application à l’aide du profil d’administrateur T&E quitte l’entreprise (entraînant la désactivation du profil), toute application activée à l’aide de ce profil cesse de fonctionner jusqu’à son activation au moyen d’un autre profil WS Admin actif.</span><span class="sxs-lookup"><span data-stu-id="d8deb-137">If a client administrator that has enabled an app using the T&E admin profile leaves the company (resulting in the profile being inactivated), any apps enabled using that profile does not function until the app is enabled with another active WS Admin profile.</span></span> <span data-ttu-id="d8deb-138">C’est pourquoi vous êtes censé créer des profils WS Admin distincts.</span><span class="sxs-lookup"><span data-stu-id="d8deb-138">This is why you are supposed to create distinct WS Admin profiles.</span></span>

* <span data-ttu-id="d8deb-139">Si un administrateur quitte l’entreprise, le nom associé au profil WS Admin peut être remplacé par celui du nouvel administrateur sans affecter l’application activée, puisque le profil n’a pas besoin d’être désactivé.</span><span class="sxs-lookup"><span data-stu-id="d8deb-139">If an administrator leaves the company, the name associated to the WS Admin profile can be changed to the replacement administrator if desired without impacting the enabled app because that profile does not need inactivated.</span></span>

<span data-ttu-id="d8deb-140">**Pour configurer l'approvisionnement des utilisateurs, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d8deb-140">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="d8deb-141">Connectez-vous à votre locataire **Concur**.</span><span class="sxs-lookup"><span data-stu-id="d8deb-141">Log on to your **Concur** tenant.</span></span>

2. <span data-ttu-id="d8deb-142">Dans le menu **Administration**, sélectionnez **Web Services**.</span><span class="sxs-lookup"><span data-stu-id="d8deb-142">From the **Administration** menu, select **Web Services**.</span></span>
   
    <span data-ttu-id="d8deb-143">![Client Concur](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Client Concur")</span><span class="sxs-lookup"><span data-stu-id="d8deb-143">![Concur tenant](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Concur tenant")</span></span>

3. <span data-ttu-id="d8deb-144">Sur le côté gauche, dans le volet **Web Services**, sélectionnez **Enable Partner Application**.</span><span class="sxs-lookup"><span data-stu-id="d8deb-144">On the left side, from the **Web Services** pane, select **Enable Partner Application**.</span></span>
   
    <span data-ttu-id="d8deb-145">![Enable Partner Application](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "Enable Partner Application")</span><span class="sxs-lookup"><span data-stu-id="d8deb-145">![Enable Partner Application](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "Enable Partner Application")</span></span>

4. <span data-ttu-id="d8deb-146">Dans la liste **Enable Application**, sélectionnez **Azure Active Directory**, puis cliquez sur **Enable**.</span><span class="sxs-lookup"><span data-stu-id="d8deb-146">From the **Enable Application** list, select **Azure Active Directory**, and then click **Enable**.</span></span>
   
    <span data-ttu-id="d8deb-147">![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span><span class="sxs-lookup"><span data-stu-id="d8deb-147">![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")</span></span>

5. <span data-ttu-id="d8deb-148">Cliquez sur **Yes** pour fermer la boîte de dialogue **Confirm Action**.</span><span class="sxs-lookup"><span data-stu-id="d8deb-148">Click **Yes** to close the **Confirm Action** dialog.</span></span>
   
    <span data-ttu-id="d8deb-149">![Confirm Action](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "Confirm Action")</span><span class="sxs-lookup"><span data-stu-id="d8deb-149">![Confirm Action](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "Confirm Action")</span></span>

6. <span data-ttu-id="d8deb-150">Dans le [portail Azure](https://portal.azure.com), accédez à la section **Azure Active Directory > Applications d’entreprise > Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d8deb-150">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

7. <span data-ttu-id="d8deb-151">Si vous avez déjà configuré Concur pour l’authentification unique, recherchez votre instance de Concur à l’aide du champ de recherche.</span><span class="sxs-lookup"><span data-stu-id="d8deb-151">If you have already configured Concur for single sign-on, search for your instance of Concur using the search field.</span></span> <span data-ttu-id="d8deb-152">Sinon, sélectionnez **Ajouter** et recherchez **Concur** dans la galerie d’applications.</span><span class="sxs-lookup"><span data-stu-id="d8deb-152">Otherwise, select **Add** and search for **Concur** in the application gallery.</span></span> <span data-ttu-id="d8deb-153">Sélectionnez Concur dans les résultats de recherche et ajoutez-la à votre liste d’applications.</span><span class="sxs-lookup"><span data-stu-id="d8deb-153">Select Concur from the search results, and add it to your list of applications.</span></span>

8. <span data-ttu-id="d8deb-154">Sélectionnez votre instance de Concur, puis sélectionnez l’onglet **Approvisionnement**.</span><span class="sxs-lookup"><span data-stu-id="d8deb-154">Select your instance of Concur, then select the **Provisioning** tab.</span></span>

9. <span data-ttu-id="d8deb-155">Définissez le **Mode d’approvisionnement** sur **Automatique**.</span><span class="sxs-lookup"><span data-stu-id="d8deb-155">Set the **Provisioning Mode** to **Automatic**.</span></span> 
 
    ![approvisionnement](./media/active-directory-saas-concur-provisioning-tutorial/provisioning.png)

10. <span data-ttu-id="d8deb-157">Dans la section **Informations d’identification administrateur**, entrez le **nom d’utilisateur** et le **mot de passe** de l’administrateur Concur.</span><span class="sxs-lookup"><span data-stu-id="d8deb-157">Under the **Admin Credentials** section, enter the **user name** and the **password** of your Concur administrator.</span></span>

11. <span data-ttu-id="d8deb-158">Dans le portail Azure, cliquez sur **Tester la connexion** pour vérifier qu’Azure AD peut se connecter à votre application Concur.</span><span class="sxs-lookup"><span data-stu-id="d8deb-158">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Concur app.</span></span> <span data-ttu-id="d8deb-159">Si la connexion échoue, vérifiez que votre compte Concur dispose des autorisations d’administrateur d’équipe.</span><span class="sxs-lookup"><span data-stu-id="d8deb-159">If the connection fails, ensure your Concur account has Team Admin permissions.</span></span>

12. <span data-ttu-id="d8deb-160">Entrez l’adresse e-mail d’une personne ou d’un groupe qui doit recevoir les notifications d’erreur d’approvisionnement dans le champ **E-mail de notification**, et cochez la case.</span><span class="sxs-lookup"><span data-stu-id="d8deb-160">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

13. <span data-ttu-id="d8deb-161">Cliquez sur **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="d8deb-161">Click **Save.**</span></span>

14. <span data-ttu-id="d8deb-162">Dans la section Mappages, sélectionnez **Synchroniser les utilisateurs Azure Active Directory avec Concur**.</span><span class="sxs-lookup"><span data-stu-id="d8deb-162">Under the Mappings section, select **Synchronize Azure Active Directory Users to Concur.**</span></span>

15. <span data-ttu-id="d8deb-163">Dans la section **Mappages des attributs**, passez en revue les attributs utilisateur qui sont synchronisés d’Azure AD vers Concur.</span><span class="sxs-lookup"><span data-stu-id="d8deb-163">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Concur.</span></span> <span data-ttu-id="d8deb-164">Les attributs sélectionnés en tant que propriétés de **Correspondance** sont utilisés pour faire correspondre les comptes d’utilisateur dans Concur pour les opérations de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="d8deb-164">The attributes selected as **Matching** properties are used to match the user accounts in Concur for update operations.</span></span> <span data-ttu-id="d8deb-165">Cliquez sur le bouton Enregistrer pour valider les modifications.</span><span class="sxs-lookup"><span data-stu-id="d8deb-165">Select the Save button to commit any changes.</span></span>

16. <span data-ttu-id="d8deb-166">Pour activer le service d’approvisionnement Azure AD pour Concur, affectez la valeur **Activé** au paramètre **Statut d’approvisionnement** dans la section **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="d8deb-166">To enable the Azure AD provisioning service for Concur, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

17. <span data-ttu-id="d8deb-167">Cliquez sur **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="d8deb-167">Click **Save.**</span></span>

<span data-ttu-id="d8deb-168">Vous pouvez maintenant créer un compte de test.</span><span class="sxs-lookup"><span data-stu-id="d8deb-168">You can now create a test account.</span></span> <span data-ttu-id="d8deb-169">Patientez jusqu’à 20 minutes et vérifiez que le compte a bien été synchronisé avec Concur.</span><span class="sxs-lookup"><span data-stu-id="d8deb-169">Wait for up to 20 minutes to verify that the account has been synchronized to Concur.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d8deb-170">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="d8deb-170">Additional resources</span></span>

* [<span data-ttu-id="d8deb-171">Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise</span><span class="sxs-lookup"><span data-stu-id="d8deb-171">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d8deb-172">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="d8deb-172">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="d8deb-173">Configurer l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="d8deb-173">Configure Single Sign-on</span></span>](active-directory-saas-concur-tutorial.md)

