---
title: "Didacticiel : Intégration d’Azure Active Directory à Workplace par Facebook | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Workplace by Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6341e67e-8ce6-42dc-a4ea-7295904a53ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 9b22679c304248ed7ba7a6bd9eaf82b64f7143cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-workplace-by-facebook-for-user-provisioning"></a><span data-ttu-id="bf4be-103">Didacticiel : Configuration de Workplace by Facebook pour l’approvisionnement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="bf4be-103">Tutorial: Configuring Workplace by Facebook for User Provisioning</span></span>

<span data-ttu-id="bf4be-104">L’objectif de ce didacticiel est de vous montrer les étapes à effectuer dans Workplace by Facebook et Azure AD pour approvisionner et déprovisionner automatiquement des comptes d’utilisateur d’Azure AD vers Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="bf4be-104">The objective of this tutorial is to show you the steps you need to perform in Workplace by Facebook and Azure AD to automatically provision and de-provision user accounts from Azure AD to Workplace by Facebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bf4be-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="bf4be-105">Prerequisites</span></span>

<span data-ttu-id="bf4be-106">Pour configurer l’intégration d’Azure AD avec Workplace by Facebook, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="bf4be-106">To configure Azure AD integration with Workplace by Facebook, you need the following items:</span></span>

- <span data-ttu-id="bf4be-107">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf4be-107">An Azure AD subscription</span></span>
- <span data-ttu-id="bf4be-108">Un abonnement Workplace by Facebook pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="bf4be-108">A Workplace by Facebook single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bf4be-109">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="bf4be-109">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bf4be-110">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="bf4be-110">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bf4be-111">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="bf4be-111">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bf4be-112">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bf4be-112">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="assigning-users-to-workplace-by-facebook"></a><span data-ttu-id="bf4be-113">Affectation d’utilisateurs à Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="bf4be-113">Assigning users to Workplace by Facebook</span></span>

<span data-ttu-id="bf4be-114">Azure Active Directory utilise un concept appelé « affectations » pour déterminer les utilisateurs devant recevoir l’accès aux applications sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="bf4be-114">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="bf4be-115">Dans le cadre de l’approvisionnement automatique des comptes d’utilisateur, seuls les utilisateurs et les groupes qui ont été « affectés » à une application dans Azure AD sont synchronisés.</span><span class="sxs-lookup"><span data-stu-id="bf4be-115">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="bf4be-116">Avant de configurer et d’activer le service d’approvisionnement, vous devez déterminer quels utilisateurs et/ou groupes dans Azure AD représentent les utilisateurs qui ont besoin d’accéder à votre application Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="bf4be-116">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Workplace by Facebook app.</span></span> <span data-ttu-id="bf4be-117">Une fois que vous avez choisi, vous pouvez affecter ces utilisateurs à votre application Workplace by Facebook en suivant les instructions fournies ici :</span><span class="sxs-lookup"><span data-stu-id="bf4be-117">Once decided, you can assign these users to your Workplace by Facebook app by following the instructions here:</span></span>

[<span data-ttu-id="bf4be-118">Affecter un utilisateur ou un groupe à une application d’entreprise</span><span class="sxs-lookup"><span data-stu-id="bf4be-118">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-workplace-by-facebook"></a><span data-ttu-id="bf4be-119">Conseils importants concernant l’affectation d’utilisateurs à Workplace by Facebook</span><span class="sxs-lookup"><span data-stu-id="bf4be-119">Important tips for assigning users to Workplace by Facebook</span></span>

*   <span data-ttu-id="bf4be-120">Nous vous recommandons de n’assigner qu’un seul utilisateur Azure AD à Workplace by Facebook afin de tester la configuration de l’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="bf4be-120">It is recommended that a single Azure AD user is assigned to Workplace by Facebook to test the provisioning configuration.</span></span> <span data-ttu-id="bf4be-121">Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="bf4be-121">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="bf4be-122">Quand vous assignez un utilisateur à Workplace by Facebook, vous devez sélectionner un rôle d’utilisateur valide.</span><span class="sxs-lookup"><span data-stu-id="bf4be-122">When assigning a user to Workplace by Facebook, you must select a valid user role.</span></span> <span data-ttu-id="bf4be-123">Le rôle « Accès par défaut » ne fonctionne pas pour l’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="bf4be-123">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="bf4be-124">Activer l’approvisionnement d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="bf4be-124">Enable User Provisioning</span></span>

<span data-ttu-id="bf4be-125">Cette section vous explique comment connecter votre annuaire Azure AD à l’API d’approvisionnement de comptes d’utilisateur Workplace by Facebook, et comment créer, mettre à jour et désactiver les comptes utilisateur affectés dans Workplace by Facebook en fonction des affectations d’utilisateurs et de groupes dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bf4be-125">This section guides you through connecting your Azure AD to Workplace by Facebook's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Workplace by Facebook based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="bf4be-126">Vous pouvez également choisir d’activer l’authentification unique basée sur SAML pour Workplace by Facebook, grâce aux instructions disponibles sur le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bf4be-126">You may also choose to enabled SAML-based Single Sign-On for Workplace by Facebook, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="bf4be-127">L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que chacune de ces deux fonctionnalités compléte l’autre.</span><span class="sxs-lookup"><span data-stu-id="bf4be-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning-to-workplace-by-facebook-in-azure-ad"></a><span data-ttu-id="bf4be-128">Pour configurer l’approvisionnement de comptes d’utilisateur vers Workplace by Facebook dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="bf4be-128">To configure user account provisioning to Workplace by Facebook in Azure AD:</span></span>

<span data-ttu-id="bf4be-129">Cette section décrit comment activer l’approvisionnement des comptes d’utilisateur Active Directory vers Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="bf4be-129">The objective of this section is to outline how to enable provisioning of Active Directory user accounts to Workplace by Facebook.</span></span>

<span data-ttu-id="bf4be-130">Azure AD prend en charge la possibilité de synchroniser automatiquement les informations de compte des utilisateurs affectés à Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="bf4be-130">Azure AD supports the ability to automatically synchronize the account details of assigned users to Workplace by Facebook.</span></span> <span data-ttu-id="bf4be-131">La synchronisation automatique permet à Workplace by Facebook d’obtenir les données nécessaires pour autoriser l’accès des utilisateurs, avant leur première tentative de connexion.</span><span class="sxs-lookup"><span data-stu-id="bf4be-131">This automatic synchronization enables Workplace by Facebook to get the data it needs to authorize users for access, before them attempting to sign in for the first time.</span></span> <span data-ttu-id="bf4be-132">Elle annule également l’approvisionnement des utilisateurs à Workplace by Facebook lorsque l’accès a été révoqué dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bf4be-132">It also de-provisions users from Workplace by Facebook when access has been revoked in Azure AD.</span></span>

1. <span data-ttu-id="bf4be-133">Sur le [portail Azure](https://portal.azure.com), accédez à la section **Azure Active Directory** > **Applications d’entreprise** > **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="bf4be-133">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory** > **Enterprise Apps** > **All applications** section.</span></span>

2. <span data-ttu-id="bf4be-134">Si vous avez déjà configuré Workplace by Facebook pour l’authentification unique, recherchez votre instance de Workplace by Facebook à l’aide du champ de recherche.</span><span class="sxs-lookup"><span data-stu-id="bf4be-134">If you have already configured Workplace by Facebook for single sign-on, search for your instance of Workplace by Facebook using the search field.</span></span> <span data-ttu-id="bf4be-135">Sinon, sélectionnez **Ajouter** et recherchez **Workplace by Facebook** dans la galerie d’applications.</span><span class="sxs-lookup"><span data-stu-id="bf4be-135">Otherwise, select **Add** and search for **Workplace by Facebook** in the application gallery.</span></span> <span data-ttu-id="bf4be-136">Sélectionnez Workplace by Facebook dans les résultats de recherche et ajoutez-le à votre liste d’applications.</span><span class="sxs-lookup"><span data-stu-id="bf4be-136">Select Workplace by Facebook from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="bf4be-137">Sélectionnez votre instance de Workplace by Facebook, puis sélectionnez l’onglet **Approvisionnement**.</span><span class="sxs-lookup"><span data-stu-id="bf4be-137">Select your instance of Workplace by Facebook, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="bf4be-138">Définissez le **Mode d’approvisionnement** sur **Automatique**.</span><span class="sxs-lookup"><span data-stu-id="bf4be-138">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![approvisionnement](./media/active-directory-saas-workplacebyfacebook-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="bf4be-140">Dans la section **Informations d’identification de l’administrateur**, entrez le jeton secret et l’URL d’abonné de votre administrateur Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="bf4be-140">Under the **Admin Credentials** section, enter the Secret Token and the Tenant URL of your Workplace by Facebook administrator.</span></span>

6. <span data-ttu-id="bf4be-141">Sur le portail Azure, cliquez sur **Tester la connexion** pour vérifier qu’Azure AD peut se connecter à votre application Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="bf4be-141">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Workplace by Facebook app.</span></span> <span data-ttu-id="bf4be-142">Si la connexion échoue, vérifiez que votre compte Workplace by Facebook dispose des autorisations d’administrateur d’équipe.</span><span class="sxs-lookup"><span data-stu-id="bf4be-142">If the connection fails, ensure your Workplace by Facebook account has Team Admin permissions.</span></span>

7. <span data-ttu-id="bf4be-143">Entrez l’adresse e-mail d’une personne ou d’un groupe qui doit recevoir les notifications d’erreur d’approvisionnement dans le champ **E-mail de notification**, et cochez la case.</span><span class="sxs-lookup"><span data-stu-id="bf4be-143">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

8. <span data-ttu-id="bf4be-144">Cliquez sur **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="bf4be-144">Click **Save.**</span></span>

9. <span data-ttu-id="bf4be-145">Dans la section Mappages, sélectionnez **Synchroniser des utilisateurs Azure Active Directory avec Workplace by Facebook**.</span><span class="sxs-lookup"><span data-stu-id="bf4be-145">Under the Mappings section, select **Synchronize Azure Active Directory Users to Workplace by Facebook.**</span></span>

10. <span data-ttu-id="bf4be-146">Dans la section **Mappages d’attributs**, passez en revue les attributs utilisateur qui sont synchronisés à partir d’Azure AD vers Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="bf4be-146">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Workplace by Facebook.</span></span> <span data-ttu-id="bf4be-147">Les attributs sélectionnés en tant que propriétés de **Correspondance** servent à faire correspondre les comptes d’utilisateur dans Workplace by Facebook, en vue d’opérations de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="bf4be-147">The attributes selected as **Matching** properties are used to match the user accounts in Workplace by Facebook for update operations.</span></span> <span data-ttu-id="bf4be-148">Cliquez sur le bouton Enregistrer pour valider les modifications.</span><span class="sxs-lookup"><span data-stu-id="bf4be-148">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="bf4be-149">Pour activer le service d’approvisionnement Azure AD pour Workplace by Facebook, modifiez le paramètre **État de l’approvisionnement** en spécifiant **Activé** dans la section **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="bf4be-149">To enable the Azure AD provisioning service for Workplace by Facebook, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

12. <span data-ttu-id="bf4be-150">Cliquez sur **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="bf4be-150">Click **Save.**</span></span>

<span data-ttu-id="bf4be-151">Pour plus d’informations sur la façon de configurer l’approvisionnement automatique, consultez [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers).</span><span class="sxs-lookup"><span data-stu-id="bf4be-151">For more information on how to configure automatic provisioning, see [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span></span>

<span data-ttu-id="bf4be-152">Vous pouvez désormais créer un compte de test.</span><span class="sxs-lookup"><span data-stu-id="bf4be-152">You can now create a test account.</span></span> <span data-ttu-id="bf4be-153">Patientez jusqu’à 20 minutes avant de vérifier que le compte a bien été synchronisé avec Workplace by Facebook.</span><span class="sxs-lookup"><span data-stu-id="bf4be-153">Wait for up to 20 minutes to verify that the account has been synchronized to Workplace by Facebook.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bf4be-154">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="bf4be-154">Additional resources</span></span>

* [<span data-ttu-id="bf4be-155">Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise</span><span class="sxs-lookup"><span data-stu-id="bf4be-155">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bf4be-156">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="bf4be-156">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="bf4be-157">Configurer l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="bf4be-157">Configure Single Sign-on</span></span>](active-directory-saas-workplacebyfacebook-tutorial.md)

