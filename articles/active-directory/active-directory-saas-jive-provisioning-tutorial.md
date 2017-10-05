---
title: "Didacticiel : Intégration d’Azure Active Directory à Jive | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Jive."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6fbfdbe7-d66c-4305-9fea-76d6a6a92830
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 957b152fdd40d08a867e788b0cb9f7d57ed481e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-jive-for-user-provisioning"></a><span data-ttu-id="356e0-103">Didacticiel : Configuration de Jive pour l’approvisionnement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="356e0-103">Tutorial: Configuring Jive for User Provisioning</span></span>

<span data-ttu-id="356e0-104">L’objectif de ce didacticiel est de vous montrer les étapes à effectuer dans Jive et Azure AD pour approvisionner et retirer automatiquement des comptes utilisateur d’Azure AD vers Jive.</span><span class="sxs-lookup"><span data-stu-id="356e0-104">The objective of this tutorial is to show you the steps you need to perform in Jive and Azure AD to automatically provision and de-provision user accounts from Azure AD to Jive.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="356e0-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="356e0-105">Prerequisites</span></span>

<span data-ttu-id="356e0-106">Le scénario décrit dans ce didacticiel part du principe que vous disposez des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="356e0-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="356e0-107">Un locataire Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="356e0-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="356e0-108">Un abonnement Jive pour lequel l’authentification unique est activée.</span><span class="sxs-lookup"><span data-stu-id="356e0-108">A Jive single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="356e0-109">Un compte utilisateur dans Jive avec les autorisations d’administrateur d’équipe.</span><span class="sxs-lookup"><span data-stu-id="356e0-109">A user account in Jive with Team Admin permissions.</span></span>

## <a name="assigning-users-to-jive"></a><span data-ttu-id="356e0-110">Affectation d’utilisateurs à Jive</span><span class="sxs-lookup"><span data-stu-id="356e0-110">Assigning users to Jive</span></span>

<span data-ttu-id="356e0-111">Azure Active Directory utilise un concept appelé « affectations » pour déterminer les utilisateurs devant recevoir l’accès aux applications sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="356e0-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="356e0-112">Dans le cadre de l’approvisionnement automatique de comptes utilisateur, les utilisateurs et les groupes qui ont été « affectés » à une application dans Azure AD sont synchronisés.</span><span class="sxs-lookup"><span data-stu-id="356e0-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="356e0-113">Avant de configurer et d’activer le service d’approvisionnement, vous devez déterminer quels utilisateurs et/ou groupes dans Azure AD représentent les utilisateurs qui ont besoin d’accéder à votre application Jive.</span><span class="sxs-lookup"><span data-stu-id="356e0-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Jive app.</span></span> <span data-ttu-id="356e0-114">Une fois que vous avez choisi, vous pouvez affecter ces utilisateurs à votre application Jive en suivant les instructions fournies ici :</span><span class="sxs-lookup"><span data-stu-id="356e0-114">Once decided, you can assign these users to your Jive app by following the instructions here:</span></span>

[<span data-ttu-id="356e0-115">Affecter un utilisateur ou un groupe à une application d’entreprise</span><span class="sxs-lookup"><span data-stu-id="356e0-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-jive"></a><span data-ttu-id="356e0-116">Conseils importants pour l’affectation d’utilisateurs à Jive</span><span class="sxs-lookup"><span data-stu-id="356e0-116">Important tips for assigning users to Jive</span></span>

*   <span data-ttu-id="356e0-117">Il est recommandé qu’un seul utilisateur Azure AD soit affecté à Jive pour tester la configuration de l’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="356e0-117">It is recommended that a single Azure AD user be assigned to Jive to test the provisioning configuration.</span></span> <span data-ttu-id="356e0-118">Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="356e0-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="356e0-119">Quand vous affectez un utilisateur à Jive, vous devez sélectionner un rôle d’utilisateur valide.</span><span class="sxs-lookup"><span data-stu-id="356e0-119">When assigning a user to Jive, you must select a valid user role.</span></span> <span data-ttu-id="356e0-120">Le rôle « Accès par défaut » ne fonctionne pas pour l’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="356e0-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="356e0-121">Activer l’approvisionnement d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="356e0-121">Enable User Provisioning</span></span>

<span data-ttu-id="356e0-122">Cette section vous guide lors de la connexion de votre instance Azure AD au compte utilisateur Jive fournissant l’API et la configuration du service d’approvisionnement pour créer, mettre à jour et désactiver les comptes utilisateur affectés dans Jive en fonction des attributions d’utilisateurs et de groupes dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="356e0-122">This section guides you through connecting your Azure AD to Jive's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Jive based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="356e0-123">Vous pouvez également choisir d’activer l’authentification unique basée sur SAML pour Jive en suivant les instructions fournies dans le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="356e0-123">You may also choose to enabled SAML-based Single Sign-On for Jive, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="356e0-124">L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que chacune de ces deux fonctionnalités compléte l’autre.</span><span class="sxs-lookup"><span data-stu-id="356e0-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning"></a><span data-ttu-id="356e0-125">Pour configurer l’approvisionnement de comptes d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="356e0-125">To configure user account provisioning:</span></span>

<span data-ttu-id="356e0-126">Cette section décrit comment activer l’approvisionnement des utilisateurs des comptes d’utilisateurs Active Directory sur Jive.</span><span class="sxs-lookup"><span data-stu-id="356e0-126">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Jive.</span></span>
<span data-ttu-id="356e0-127">Dans le cadre de cette procédure, vous devez fournir un jeton de sécurité à demander sur Jive.com.</span><span class="sxs-lookup"><span data-stu-id="356e0-127">As part of this procedure, you are required to provide a user security token you need to request from Jive.com.</span></span>

1. <span data-ttu-id="356e0-128">Dans le [portail Azure](https://portal.azure.com), accédez à la section **Azure Active Directory > Applications d’entreprise > Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="356e0-128">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="356e0-129">Si vous avez déjà configuré Jive pour l’authentification unique, recherchez votre instance Jive à l’aide du champ de recherche.</span><span class="sxs-lookup"><span data-stu-id="356e0-129">If you have already configured Jive for single sign-on, search for your instance of Jive using the search field.</span></span> <span data-ttu-id="356e0-130">Sinon, sélectionnez **Ajouter** et recherchez **Jive** dans la galerie d’applications.</span><span class="sxs-lookup"><span data-stu-id="356e0-130">Otherwise, select **Add** and search for **Jive** in the application gallery.</span></span> <span data-ttu-id="356e0-131">Sélectionnez Jive dans les résultats de recherche et ajoutez-le à votre liste d’applications.</span><span class="sxs-lookup"><span data-stu-id="356e0-131">Select Jive from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="356e0-132">Sélectionnez votre instance Jive, puis sélectionnez l’onglet **Approvisionnement**.</span><span class="sxs-lookup"><span data-stu-id="356e0-132">Select your instance of Jive, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="356e0-133">Définissez le **Mode d’approvisionnement** sur **Automatique**.</span><span class="sxs-lookup"><span data-stu-id="356e0-133">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![approvisionnement](./media/active-directory-saas-jive-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="356e0-135">Dans la section **Informations d’identification de l’administrateur**, fournissez les paramètres de configuration suivants :</span><span class="sxs-lookup"><span data-stu-id="356e0-135">Under the **Admin Credentials** section, provide the following configuration settings:</span></span>
   
    <span data-ttu-id="356e0-136">a.</span><span class="sxs-lookup"><span data-stu-id="356e0-136">a.</span></span> <span data-ttu-id="356e0-137">Dans la zone de texte **Nom d’utilisateur admin Jive**, tapez le nom d’un compte Jive auquel le profil **System Administrator** est attribué dans Jive.com.</span><span class="sxs-lookup"><span data-stu-id="356e0-137">In the **Jive Admin User Name** textbox, type a Jive account name that has the **System Administrator** profile in Jive.com assigned.</span></span>
   
    <span data-ttu-id="356e0-138">b.</span><span class="sxs-lookup"><span data-stu-id="356e0-138">b.</span></span> <span data-ttu-id="356e0-139">Dans la zone de texte **Mot de passe de l’admin Jive** , tapez le mot de passe de ce compte.</span><span class="sxs-lookup"><span data-stu-id="356e0-139">In the **Jive Admin Password** textbox, type the password for this account.</span></span>
   
    <span data-ttu-id="356e0-140">c.</span><span class="sxs-lookup"><span data-stu-id="356e0-140">c.</span></span> <span data-ttu-id="356e0-141">Dans la zone de texte **URL de locataire Jive** , tapez l’URL de locataire Jive.</span><span class="sxs-lookup"><span data-stu-id="356e0-141">In the **Jive Tenant URL** textbox, type the Jive tenant URL.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="356e0-142">L’URL de locataire Jive est celle utilisée par votre organisation pour se connecter à Jive.</span><span class="sxs-lookup"><span data-stu-id="356e0-142">The Jive tenant URL is URL that is used by your organization to log in to Jive.</span></span>  
      > <span data-ttu-id="356e0-143">En règle générale, l’URL a le format suivant : **www.\<organisation\>.jive.com**.</span><span class="sxs-lookup"><span data-stu-id="356e0-143">Typically, the URL has the following format: **www.\<organization\>.jive.com**.</span></span>          

6. <span data-ttu-id="356e0-144">Dans le portail Azure, cliquez sur **Tester la connexion** pour vérifier qu’Azure AD peut se connecter à votre application Jive.</span><span class="sxs-lookup"><span data-stu-id="356e0-144">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Jive app.</span></span>

7. <span data-ttu-id="356e0-145">Entrez l’adresse e-mail d’une personne ou d’un groupe qui doit recevoir les notifications d’erreur d’approvisionnement dans le champ **E-mail de notification**, puis cochez la case se trouvant en dessous.</span><span class="sxs-lookup"><span data-stu-id="356e0-145">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

8. <span data-ttu-id="356e0-146">Cliquez sur **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="356e0-146">Click **Save.**</span></span>

9. <span data-ttu-id="356e0-147">Dans la section Mappages, sélectionnez **Synchroniser les utilisateurs Azure Active Directory avec Jive**.</span><span class="sxs-lookup"><span data-stu-id="356e0-147">Under the Mappings section, select **Synchronize Azure Active Directory Users to Jive.**</span></span>

10. <span data-ttu-id="356e0-148">Dans la section **Mappages des attributs**, passez en revue les attributs utilisateur qui sont synchronisés d’Azure AD vers Jive.</span><span class="sxs-lookup"><span data-stu-id="356e0-148">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Jive.</span></span> <span data-ttu-id="356e0-149">Les attributs sélectionnés en tant que propriétés de **Correspondance** sont utilisés pour faire correspondre les comptes utilisateur dans Jive pour les opérations de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="356e0-149">The attributes selected as **Matching** properties are used to match the user accounts in Jive for update operations.</span></span> <span data-ttu-id="356e0-150">Cliquez sur le bouton Enregistrer pour valider les modifications.</span><span class="sxs-lookup"><span data-stu-id="356e0-150">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="356e0-151">Pour activer le service d’approvisionnement Azure AD pour Jive, définissez le paramètre **État d’approvisionnement** sur **Activé** dans la section Paramètres.</span><span class="sxs-lookup"><span data-stu-id="356e0-151">To enable the Azure AD provisioning service for Jive, change the **Provisioning Status** to **On** in the Settings section</span></span>

12. <span data-ttu-id="356e0-152">Cliquez sur **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="356e0-152">Click **Save.**</span></span>

<span data-ttu-id="356e0-153">Cette commande démarre la synchronisation initiale des utilisateurs et/ou des groupes affectés à Jive dans la section Utilisateurs et Groupes.</span><span class="sxs-lookup"><span data-stu-id="356e0-153">It starts the initial synchronization of any users and/or groups assigned to Jive in the Users and Groups section.</span></span> <span data-ttu-id="356e0-154">La synchronisation initiale prend plus de temps que les synchronisations suivantes, qui se produisent environ toutes les 20 minutes, tant que le service est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="356e0-154">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="356e0-155">Vous pouvez utiliser la section **Détails de la synchronisation** pour surveiller la progression et les liens vers les rapports d’activité d’approvisionnement, qui décrivent toutes les actions effectuées par le service de configuration dans votre application Jive.</span><span class="sxs-lookup"><span data-stu-id="356e0-155">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Jive app.</span></span>

<span data-ttu-id="356e0-156">Vous pouvez à présent créer un compte de test.</span><span class="sxs-lookup"><span data-stu-id="356e0-156">You can now create a test account.</span></span> <span data-ttu-id="356e0-157">Patientez jusqu’à 20 minutes et vérifiez que le compte a bien été synchronisé avec Jive.</span><span class="sxs-lookup"><span data-stu-id="356e0-157">Wait for up to 20 minutes to verify that the account has been synchronized to Jive.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="356e0-158">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="356e0-158">Additional resources</span></span>

* [<span data-ttu-id="356e0-159">Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise</span><span class="sxs-lookup"><span data-stu-id="356e0-159">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="356e0-160">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="356e0-160">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="356e0-161">Configurer l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="356e0-161">Configure Single Sign-on</span></span>](active-directory-saas-jive-tutorial.md)