---
title: "Didacticiel : Intégration d’Azure Active Directory à Citrix GoToMeeting | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Citrix GoToMeeting."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f59fedb-2cf8-48d2-a5fb-222ed943ff78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 1ddfcd991431a11e5c3e306bd5905003d094ac18
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-citrix-gotomeeting-for-automatic-user-provisioning"></a><span data-ttu-id="25579-103">Didacticiel : Configuration de Citrix GoToMeeting pour l’attribution automatique des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="25579-103">Tutorial: Configuring Citrix GoToMeeting for Automatic User Provisioning</span></span>

<span data-ttu-id="25579-104">L’objectif de ce didacticiel est de vous montrer les étapes à effectuer dans Citrix GoToMeeting et Azure AD pour approvisionner automatiquement des comptes d’utilisateur Azure AD dans Citrix GoToMeeting, ainsi que pour annuler automatiquement cet approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="25579-104">The objective of this tutorial is to show you the steps you need to perform in Citrix GoToMeeting and Azure AD to automatically provision and de-provision user accounts from Azure AD to Citrix GoToMeeting.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="25579-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="25579-105">Prerequisites</span></span>

<span data-ttu-id="25579-106">Le scénario décrit dans ce didacticiel part du principe que vous disposez des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="25579-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="25579-107">Un locataire Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="25579-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="25579-108">Un abonnement Citrix GoToMeeting pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="25579-108">A Citrix GoToMeeting single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="25579-109">Un compte d’utilisateur Citrix GoToMeeting avec les autorisations d’administrateur d’équipe</span><span class="sxs-lookup"><span data-stu-id="25579-109">A user account in Citrix GoToMeeting with Team Admin permissions.</span></span>

## <a name="assigning-users-to-citrix-gotomeeting"></a><span data-ttu-id="25579-110">Attribution d’utilisateurs à Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="25579-110">Assigning users to Citrix GoToMeeting</span></span>

<span data-ttu-id="25579-111">Azure Active Directory utilise un concept appelé « affectations » pour déterminer les utilisateurs devant recevoir l’accès aux applications sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="25579-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="25579-112">Dans le cadre de l’approvisionnement automatique des comptes d’utilisateur, les utilisateurs et les groupes qui ont été « attribués » à une application dans Azure AD sont synchronisés.</span><span class="sxs-lookup"><span data-stu-id="25579-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="25579-113">Avant de configurer et d’activer le service d’approvisionnement, vous devez déterminer quels utilisateurs et/ou groupes Azure AD ont besoin d’accéder à votre application Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="25579-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Citrix GoToMeeting app.</span></span> <span data-ttu-id="25579-114">Une fois que vous avez choisi, vous pouvez attribuer ces utilisateurs à votre application Citrix GoToMeeting en suivant les instructions fournies ici :</span><span class="sxs-lookup"><span data-stu-id="25579-114">Once decided, you can assign these users to your Citrix GoToMeeting app by following the instructions here:</span></span>

[<span data-ttu-id="25579-115">Affecter un utilisateur ou un groupe à une application d’entreprise</span><span class="sxs-lookup"><span data-stu-id="25579-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-citrix-gotomeeting"></a><span data-ttu-id="25579-116">Conseils importants pour l’attribution d’utilisateurs à Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="25579-116">Important tips for assigning users to Citrix GoToMeeting</span></span>

*   <span data-ttu-id="25579-117">Dans un premier temps, il est recommandé de n’assigner qu’un seul utilisateur Azure AD à Citrix GoToMeeting pour tester la configuration de l’attribution.</span><span class="sxs-lookup"><span data-stu-id="25579-117">It is recommended that a single Azure AD user is assigned to Citrix GoToMeeting to test the provisioning configuration.</span></span> <span data-ttu-id="25579-118">Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="25579-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="25579-119">Quand vous attribuez un utilisateur à Citrix GoToMeeting, vous devez sélectionner un rôle d’utilisateur valide.</span><span class="sxs-lookup"><span data-stu-id="25579-119">When assigning a user to Citrix GoToMeeting, you must select a valid user role.</span></span> <span data-ttu-id="25579-120">Le rôle « Accès par défaut » ne fonctionne pas pour l’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="25579-120">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="25579-121">Activer l’attribution automatique des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="25579-121">Enable Automated User Provisioning</span></span>

<span data-ttu-id="25579-122">Cette section explique comment connecter Azure AD à l’API d’approvisionnement de comptes d’utilisateur de Citrix GoToMeeting pour créer, mettre à jour et désactiver les comptes d’utilisateur attribués dans Citrix GoToMeeting, en fonction des attributions d’utilisateurs et de groupes dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="25579-122">This section guides you through connecting your Azure AD to Citrix GoToMeeting's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Citrix GoToMeeting based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="25579-123">Vous pouvez également choisir d’activer l’authentification unique SAML pour Citrix GoToMeeting en suivant les instructions fournies dans le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="25579-123">You may also choose to enabled SAML-based Single Sign-On for Citrix GoToMeeting, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="25579-124">L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que chacune de ces deux fonctionnalités compléte l’autre.</span><span class="sxs-lookup"><span data-stu-id="25579-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-automatic-user-account-provisioning"></a><span data-ttu-id="25579-125">Pour configurer l’approvisionnement automatique des comptes d’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="25579-125">To configure automatic user account provisioning:</span></span>

1. <span data-ttu-id="25579-126">Dans le [portail Azure](https://portal.azure.com), accédez à la section **Azure Active Directory > Applications d’entreprise > Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="25579-126">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="25579-127">Si vous avez déjà configuré Citrix GoToMeeting pour l’authentification unique, recherchez votre instance de Citrix GoToMeeting à l’aide du champ de recherche.</span><span class="sxs-lookup"><span data-stu-id="25579-127">If you have already configured Citrix GoToMeeting for single sign-on, search for your instance of Citrix GoToMeeting using the search field.</span></span> <span data-ttu-id="25579-128">Sinon, sélectionnez **Ajouter**, puis recherchez **Citrix GoToMeeting** dans la galerie d’applications.</span><span class="sxs-lookup"><span data-stu-id="25579-128">Otherwise, select **Add** and search for **Citrix GoToMeeting** in the application gallery.</span></span> <span data-ttu-id="25579-129">Sélectionnez Citrix GoToMeeting dans les résultats de la recherche, puis ajoutez-le à votre liste d’applications.</span><span class="sxs-lookup"><span data-stu-id="25579-129">Select Citrix GoToMeeting from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="25579-130">Sélectionnez votre instance de Citrix GoToMeeting, puis sélectionnez l’onglet **Approvisionnement**.</span><span class="sxs-lookup"><span data-stu-id="25579-130">Select your instance of Citrix GoToMeeting, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="25579-131">Définissez le **Mode d’approvisionnement** sur **Automatique**.</span><span class="sxs-lookup"><span data-stu-id="25579-131">Set the **Provisioning** Mode to **Automatic**.</span></span> 

    ![approvisionnement](./media/active-directory-saas-citrixgotomeeting-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="25579-133">Dans la section Informations d’identification de l’administrateur, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="25579-133">Under the Admin Credentials section, perform the following steps:</span></span>
   
    <span data-ttu-id="25579-134">a.</span><span class="sxs-lookup"><span data-stu-id="25579-134">a.</span></span> <span data-ttu-id="25579-135">Dans la zone de texte **Nom d’utilisateur admin Citrix GoToMeeting** , tapez le nom d’utilisateur d’un administrateur.</span><span class="sxs-lookup"><span data-stu-id="25579-135">In the **Citrix GoToMeeting Admin User Name** textbox, type the user name of an administrator.</span></span>

    <span data-ttu-id="25579-136">b.</span><span class="sxs-lookup"><span data-stu-id="25579-136">b.</span></span> <span data-ttu-id="25579-137">Dans la zone de texte **Mot de passe de l’admin Citrix GoToMeeting** , tapez le mot de passe de l’administrateur.</span><span class="sxs-lookup"><span data-stu-id="25579-137">In the **Citrix GoToMeeting Admin Password** textbox, the administrator's password.</span></span>

6. <span data-ttu-id="25579-138">Dans le portail Azure, cliquez sur **Tester la connexion** pour vérifier qu’Azure AD peut se connecter à votre application Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="25579-138">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Citrix GoToMeeting app.</span></span> <span data-ttu-id="25579-139">Si la connexion échoue, vérifiez que votre compte Citrix GoToMeeting dispose des autorisations d’administrateur d’équipe, puis revenez à l’étape **Informations d’identification de l’administrateur**.</span><span class="sxs-lookup"><span data-stu-id="25579-139">If the connection fails, ensure your Citrix GoToMeeting account has Team Admin permissions and try the **"Admin Credentials"** step again.</span></span>

7. <span data-ttu-id="25579-140">Entrez l’adresse e-mail d’une personne ou d’un groupe qui doit recevoir les notifications d’erreur d’approvisionnement dans le champ **E-mail de notification**, puis cochez la case.</span><span class="sxs-lookup"><span data-stu-id="25579-140">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

8. <span data-ttu-id="25579-141">Cliquez sur **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="25579-141">Click **Save.**</span></span>

9. <span data-ttu-id="25579-142">Dans la section Mappages, sélectionnez **Synchroniser les utilisateurs Azure Active Directory avec Citrix GoToMeeting**.</span><span class="sxs-lookup"><span data-stu-id="25579-142">Under the Mappings section, select **Synchronize Azure Active Directory Users to Citrix GoToMeeting.**</span></span>

10. <span data-ttu-id="25579-143">Dans la section **Mappages des attributs**, passez en revue les attributs utilisateur qui sont synchronisés entre Azure et Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="25579-143">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Citrix GoToMeeting.</span></span> <span data-ttu-id="25579-144">Les attributs sélectionnés en tant que propriétés de **Correspondance** sont utilisés pour établir une correspondance avec les comptes d’utilisateur Citrix GoToMeeting en vue de mises à jour ultérieures.</span><span class="sxs-lookup"><span data-stu-id="25579-144">The attributes selected as **Matching** properties are used to match the user accounts in Citrix GoToMeeting for update operations.</span></span> <span data-ttu-id="25579-145">Cliquez sur le bouton Enregistrer pour valider les modifications.</span><span class="sxs-lookup"><span data-stu-id="25579-145">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="25579-146">Pour activer le service d’approvisionnement Azure AD pour Citrix GoToMeeting, définissez **État de l’approvisionnement** sur **Activé** dans la section Paramètres.</span><span class="sxs-lookup"><span data-stu-id="25579-146">To enable the Azure AD provisioning service for Citrix GoToMeeting, change the **Provisioning Status** to **On** in the Settings section</span></span>

12. <span data-ttu-id="25579-147">Cliquez sur **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="25579-147">Click **Save.**</span></span>

<span data-ttu-id="25579-148">Cette commande démarre la synchronisation initiale des utilisateurs et/ou des groupes attribués à Citrix GoToMeeting dans la section Utilisateurs et Groupes.</span><span class="sxs-lookup"><span data-stu-id="25579-148">It starts the initial synchronization of any users and/or groups assigned to Citrix GoToMeeting in the Users and Groups section.</span></span> <span data-ttu-id="25579-149">La synchronisation initiale prend plus de temps que les synchronisations suivantes, qui se produisent environ toutes les 20 minutes, tant que le service est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="25579-149">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="25579-150">Vous pouvez utiliser la section **Détails de la synchronisation** pour surveiller la progression et suivre les liens vers les rapports d’activité d’approvisionnement, qui décrivent toutes les actions effectuées par le service d’approvisionnement dans votre application Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="25579-150">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Citrix GoToMeeting app.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="25579-151">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="25579-151">Additional resources</span></span>

* [<span data-ttu-id="25579-152">Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise</span><span class="sxs-lookup"><span data-stu-id="25579-152">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="25579-153">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="25579-153">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="25579-154">Configurer l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="25579-154">Configure Single Sign-on</span></span>](active-directory-saas-citrix-gotomeeting-tutorial.md)


