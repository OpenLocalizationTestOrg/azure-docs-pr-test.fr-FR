---
title: "Didacticiel : Intégration d’Azure Active Directory à Netsuite | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Netsuite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8a6d3994-ee33-4a6f-b0a2-9d0389467f16
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 277c393536615fc8bfe8af0bc6d487115f04776c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-netsuite-for-automatic-user-provisioning"></a><span data-ttu-id="51d50-103">Didacticiel : Configuration de Netsuite pour l’approvisionnement automatique d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="51d50-103">Tutorial: Configuring Netsuite for Automatic User Provisioning</span></span>

<span data-ttu-id="51d50-104">L’objectif de ce didacticiel est de vous montrer la procédure à suivre dans Netsuite et Azure AD pour approvisionner et retirer automatiquement des comptes utilisateur Azure AD vers Netsuite.</span><span class="sxs-lookup"><span data-stu-id="51d50-104">The objective of this tutorial is to show you the steps you need to perform in Netsuite and Azure AD to automatically provision and de-provision user accounts from Azure AD to Netsuite.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="51d50-105">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="51d50-105">Prerequisites</span></span>

<span data-ttu-id="51d50-106">Le scénario décrit dans ce didacticiel part du principe que vous disposez des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="51d50-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="51d50-107">Un locataire Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="51d50-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="51d50-108">Un abonnement Netsuite pour lequel l’authentification unique est activée.</span><span class="sxs-lookup"><span data-stu-id="51d50-108">A Netsuite single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="51d50-109">Un compte utilisateur dans Netsuite avec les autorisations d’administrateur d’équipe.</span><span class="sxs-lookup"><span data-stu-id="51d50-109">A user account in Netsuite with Team Admin permissions.</span></span>

## <a name="assigning-users-to-netsuite"></a><span data-ttu-id="51d50-110">Affectation d’utilisateurs à Netsuite</span><span class="sxs-lookup"><span data-stu-id="51d50-110">Assigning users to Netsuite</span></span>

<span data-ttu-id="51d50-111">Azure Active Directory utilise un concept appelé « affectations » pour déterminer les utilisateurs devant recevoir l’accès aux applications sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="51d50-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="51d50-112">Dans le cadre de l’approvisionnement automatique de comptes utilisateur, seuls les utilisateurs et les groupes qui ont été « assignés » à une application dans Azure AD sont synchronisés.</span><span class="sxs-lookup"><span data-stu-id="51d50-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD are synchronized.</span></span>

<span data-ttu-id="51d50-113">Avant de configurer et d’activer le service d’approvisionnement, vous devez déterminer quels utilisateurs et/ou groupes dans Azure AD ont besoin d’accéder à votre application Netsuite.</span><span class="sxs-lookup"><span data-stu-id="51d50-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Netsuite app.</span></span> <span data-ttu-id="51d50-114">Une fois que vous avez effectuer votre choix, vous pouvez affecter ces utilisateurs à votre application Netsuite en suivant les instructions fournies ici :</span><span class="sxs-lookup"><span data-stu-id="51d50-114">Once decided, you can assign these users to your Netsuite app by following the instructions here:</span></span>

[<span data-ttu-id="51d50-115">Affecter un utilisateur ou un groupe à une application d’entreprise</span><span class="sxs-lookup"><span data-stu-id="51d50-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-netsuite"></a><span data-ttu-id="51d50-116">Conseils importants pour l’affectation d’utilisateurs à Netsuite</span><span class="sxs-lookup"><span data-stu-id="51d50-116">Important tips for assigning users to Netsuite</span></span>

*   <span data-ttu-id="51d50-117">Il est recommandé de n’assigner qu’un seul utilisateur Azure AD à Netsuite afin de tester la configuration de l’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="51d50-117">It is recommended that a single Azure AD user is assigned to Netsuite to test the provisioning configuration.</span></span> <span data-ttu-id="51d50-118">Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="51d50-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="51d50-119">Quand vous affectez un utilisateur à Netsuite, vous devez sélectionner un rôle d’utilisateur valide.</span><span class="sxs-lookup"><span data-stu-id="51d50-119">When assigning a user to Netsuite, you must select a valid user role.</span></span> <span data-ttu-id="51d50-120">Le rôle « Accès par défaut » ne fonctionne pas pour l’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="51d50-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="51d50-121">Activer l’approvisionnement d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="51d50-121">Enable User Provisioning</span></span>

<span data-ttu-id="51d50-122">Cette section explique comment connecter votre Azure AD à l’API d’approvisionnement de comptes utilisateur de Netsuite pour créer, mettre à jour et désactiver les comptes utilisateur affectés dans Netsuite en fonction des attributions d’utilisateurs et de groupes dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="51d50-122">This section guides you through connecting your Azure AD to Netsuite's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Netsuite based on user and group assignment in Azure AD.</span></span>

> [!TIP] 
> <span data-ttu-id="51d50-123">Vous pouvez également choisir d’activer l’authentification unique basée sur SAML pour Netsuite en suivant les instructions fournies dans le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="51d50-123">You may also choose to enabled SAML-based Single Sign-On for Netsuite, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="51d50-124">L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que chacune de ces deux fonctionnalités compléte l’autre.</span><span class="sxs-lookup"><span data-stu-id="51d50-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-user-account-provisioning"></a><span data-ttu-id="51d50-125">Pour configurer l’approvisionnement de comptes utilisateur :</span><span class="sxs-lookup"><span data-stu-id="51d50-125">To configure user account provisioning:</span></span>

<span data-ttu-id="51d50-126">L’objectif de cette section est d’expliquer comment activer l’approvisionnement utilisateur des comptes utilisateur Active Directory sur Netsuite.</span><span class="sxs-lookup"><span data-stu-id="51d50-126">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to Netsuite.</span></span>

1. <span data-ttu-id="51d50-127">Dans le [portail Azure](https://portal.azure.com), accédez à la section **Azure Active Directory > Applications d’entreprise > Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="51d50-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="51d50-128">Si vous avez déjà configuré Netsuite pour l’authentification unique, recherchez votre instance de Netsuite à l’aide du champ de recherche.</span><span class="sxs-lookup"><span data-stu-id="51d50-128">If you have already configured Netsuite for single sign-on, search for your instance of Netsuite using the search field.</span></span> <span data-ttu-id="51d50-129">Sinon, sélectionnez **Ajouter** et recherchez **Netsuite** dans la galerie d’applications.</span><span class="sxs-lookup"><span data-stu-id="51d50-129">Otherwise, select **Add** and search for **Netsuite** in the application gallery.</span></span> <span data-ttu-id="51d50-130">Sélectionnez Netsuite dans les résultats de recherche et ajoutez-la à votre liste d’applications.</span><span class="sxs-lookup"><span data-stu-id="51d50-130">Select Netsuite from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="51d50-131">Sélectionnez votre instance de Netsuite, puis sélectionnez l’onglet **Approvisionnement**.</span><span class="sxs-lookup"><span data-stu-id="51d50-131">Select your instance of Netsuite, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="51d50-132">Définissez le **Mode d’approvisionnement** sur **Automatique**.</span><span class="sxs-lookup"><span data-stu-id="51d50-132">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![approvisionnement](./media/active-directory-saas-netsuite-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="51d50-134">Dans la section **Informations d’identification de l’administrateur**, fournissez les paramètres de configuration suivants :</span><span class="sxs-lookup"><span data-stu-id="51d50-134">Under the **Admin Credentials** section, provide the following configuration settings:</span></span>
   
    <span data-ttu-id="51d50-135">a.</span><span class="sxs-lookup"><span data-stu-id="51d50-135">a.</span></span> <span data-ttu-id="51d50-136">Dans la zone de texte **Nom d'utilisateur Admin**, tapez le nom d’un compte Netsuite auquel le profil **System Administrator** (Administrateur système) est affecté dans Netsuite.com.</span><span class="sxs-lookup"><span data-stu-id="51d50-136">In the **Admin User Name** textbox, type a Netsuite account name that has the **System Administrator** profile in Netsuite.com assigned.</span></span>
   
    <span data-ttu-id="51d50-137">b.</span><span class="sxs-lookup"><span data-stu-id="51d50-137">b.</span></span> <span data-ttu-id="51d50-138">Dans la zone de texte **Mot de passe d’administrateur**, entrez le mot de passe de ce compte.</span><span class="sxs-lookup"><span data-stu-id="51d50-138">In the **Admin Password** textbox, type the password for this account.</span></span>
      
6. <span data-ttu-id="51d50-139">Dans le portail Azure, cliquez sur **Tester la connexion** pour vérifier qu’Azure AD peut se connecter à votre application Netsuite.</span><span class="sxs-lookup"><span data-stu-id="51d50-139">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Netsuite app.</span></span>

7. <span data-ttu-id="51d50-140">Dans le champ **E-mail de notification**, entrez l’adresse e-mail d’une personne ou d’un groupe qui doit recevoir les notifications d’erreur d’approvisionnement, puis cochez la case.</span><span class="sxs-lookup"><span data-stu-id="51d50-140">In the **Notification Email** field, enter the email address of a person or group who should receive provisioning error notifications, and check the checkbox.</span></span>

8. <span data-ttu-id="51d50-141">Cliquez sur **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="51d50-141">Click **Save.**</span></span>

9. <span data-ttu-id="51d50-142">Dans la section Mappages, sélectionnez **Synchroniser les utilisateurs Azure Active Directory avec Netsuite**.</span><span class="sxs-lookup"><span data-stu-id="51d50-142">Under the Mappings section, select **Synchronize Azure Active Directory Users to Netsuite.**</span></span>

10. <span data-ttu-id="51d50-143">Dans la section **Mappages d’attributs**, passez en revue les attributs utilisateur qui sont synchronisés d’Azure AD vers Netsuite.</span><span class="sxs-lookup"><span data-stu-id="51d50-143">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Netsuite.</span></span> <span data-ttu-id="51d50-144">Remarque : les attributs sélectionnés en tant que propriétés de **Correspondance** servent à faire correspondre les comptes utilisateur dans Netsuite, en vue d’opérations de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="51d50-144">Note that the attributes selected as **Matching** properties are used to match the user accounts in Netsuite for update operations.</span></span> <span data-ttu-id="51d50-145">Cliquez sur le bouton Enregistrer pour valider les modifications.</span><span class="sxs-lookup"><span data-stu-id="51d50-145">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="51d50-146">Pour activer le service d’approvisionnement Azure AD pour Netsuite, affectez la valeur **Activé** au paramètre **État de l’approvisionnement** dans la section Paramètres.</span><span class="sxs-lookup"><span data-stu-id="51d50-146">To enable the Azure AD provisioning service for Netsuite, change the **Provisioning Status** to **On** in the Settings section</span></span>

12. <span data-ttu-id="51d50-147">Cliquez sur **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="51d50-147">Click **Save.**</span></span>

<span data-ttu-id="51d50-148">Cette commande démarre la synchronisation initiale des utilisateurs et/ou des groupes affectés à Netsuite dans la section Utilisateurs et Groupes.</span><span class="sxs-lookup"><span data-stu-id="51d50-148">It starts the initial synchronization of any users and/or groups assigned to Netsuite in the Users and Groups section.</span></span> <span data-ttu-id="51d50-149">Remarquez que la synchronisation initiale prend plus de temps que les synchronisations suivantes, qui se produisent environ toutes les 20 minutes, tant que le service est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="51d50-149">Note that the initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="51d50-150">Vous pouvez utiliser la section **Détails de la synchronisation** pour surveiller la progression et les liens vers les rapports d’activité d’approvisionnement, qui décrivent toutes les actions effectuées par le service d’approvisionnement dans votre application Netsuite.</span><span class="sxs-lookup"><span data-stu-id="51d50-150">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Netsuite app.</span></span>

<span data-ttu-id="51d50-151">Vous pouvez à présent créer un compte de test.</span><span class="sxs-lookup"><span data-stu-id="51d50-151">You can now create a test account.</span></span> <span data-ttu-id="51d50-152">Patientez jusqu’à 20 minutes et vérifiez que le compte a bien été synchronisé avec Netsuite.</span><span class="sxs-lookup"><span data-stu-id="51d50-152">Wait for up to 20 minutes to verify that the account has been synchronized to Netsuite.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="51d50-153">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="51d50-153">Additional resources</span></span>

* [<span data-ttu-id="51d50-154">Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise</span><span class="sxs-lookup"><span data-stu-id="51d50-154">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="51d50-155">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="51d50-155">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="51d50-156">Configurer l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="51d50-156">Configure Single Sign-on</span></span>](active-directory-saas-netsuite-tutorial.md)