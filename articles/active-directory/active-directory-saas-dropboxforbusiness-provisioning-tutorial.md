---
title: "Didacticiel : Intégration d'Azure Active Directory à Dropbox for Business | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Dropbox for Business."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f3a42e4-6897-4234-af84-b47c148ec3e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 6f7616e47322242f01a13d763f71c93d4ac06a92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-dropbox-for-business-for-automatic-user-provisioning"></a><span data-ttu-id="57f3f-103">Didacticiel : Configuration de Dropbox for Business pour approvisionner automatiquement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="57f3f-103">Tutorial: Configuring Dropbox for Business for Automatic User Provisioning</span></span>

<span data-ttu-id="57f3f-104">L’objectif de ce didacticiel est de présenter les étapes à effectuer dans Dropbox for Business et Azure AD permettant d’approvisionner et retirer automatiquement des comptes utilisateur d’Azure AD vers Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="57f3f-104">The objective of this tutorial is to show you the steps you need to perform in Dropbox for Business and Azure AD to automatically provision and de-provision user accounts from Azure AD to Dropbox for Business.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57f3f-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="57f3f-105">Prerequisites</span></span>

<span data-ttu-id="57f3f-106">Le scénario décrit dans ce didacticiel part du principe que vous disposez des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="57f3f-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="57f3f-107">Un abonné Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="57f3f-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="57f3f-108">Un abonnement Dropbox for Business pour lequel l’authentification unique est activée.</span><span class="sxs-lookup"><span data-stu-id="57f3f-108">A Dropbox for Business single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="57f3f-109">Un compte d’utilisateur dans Dropbox for Business avec les autorisations d’administrateur d’équipe.</span><span class="sxs-lookup"><span data-stu-id="57f3f-109">A user account in Dropbox for Business with Team Admin permissions.</span></span>

## <a name="assigning-users-to-dropbox-for-business"></a><span data-ttu-id="57f3f-110">Assignation d’utilisateurs à Dropbox for Business</span><span class="sxs-lookup"><span data-stu-id="57f3f-110">Assigning users to Dropbox for Business</span></span>

<span data-ttu-id="57f3f-111">Azure Active Directory utilise un concept appelé « affectations » pour déterminer les utilisateurs devant recevoir l’accès aux applications sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="57f3f-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="57f3f-112">Dans le cadre de l’approvisionnement automatique de comptes d’utilisateur, les utilisateurs et les groupes qui ont été « affectés » à une application dans Azure AD sont synchronisés.</span><span class="sxs-lookup"><span data-stu-id="57f3f-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="57f3f-113">Avant de configurer et d’activer le service d’approvisionnement, vous devez déterminer quels utilisateurs et/ou groupes dans Azure AD représentent les utilisateurs qui ont besoin d’accéder à votre application Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="57f3f-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Dropbox for Business app.</span></span> <span data-ttu-id="57f3f-114">Dès que vous avez fait votre choix, vous pouvez assigner ces utilisateurs à votre application Dropbox for Business en suivant les instructions disponibles ici :</span><span class="sxs-lookup"><span data-stu-id="57f3f-114">Once decided, you can assign these users to your Dropbox for Business app by following the instructions here:</span></span>

[<span data-ttu-id="57f3f-115">Affecter un utilisateur ou un groupe à une application d’entreprise</span><span class="sxs-lookup"><span data-stu-id="57f3f-115">Assign a user or group to an enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-dropbox-for-business"></a><span data-ttu-id="57f3f-116">Conseils importants concernant l’assignation d’utilisateurs à Dropbox for Business</span><span class="sxs-lookup"><span data-stu-id="57f3f-116">Important tips for assigning users to Dropbox for Business</span></span>

*   <span data-ttu-id="57f3f-117">Il est recommandé de n’assigner qu’un seul utilisateur Azure AD à Dropbox for Business afin de tester la configuration de l’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="57f3f-117">It is recommended that a single Azure AD user is assigned to Dropbox for Business to test the provisioning configuration.</span></span> <span data-ttu-id="57f3f-118">Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="57f3f-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="57f3f-119">Lorsque vous assignez un utilisateur à Dropbox for Business, vous devez sélectionner un rôle d’utilisateur valide.</span><span class="sxs-lookup"><span data-stu-id="57f3f-119">When assigning a user to Dropbox for Business, you must select a valid user role.</span></span> <span data-ttu-id="57f3f-120">Le rôle « Accès par défaut » ne fonctionne pas pour l’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="57f3f-120">The "Default Access" role does not work for provisioning..</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="57f3f-121">Activer l’approvisionnement automatique des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="57f3f-121">Enable Automated User Provisioning</span></span>

<span data-ttu-id="57f3f-122">Cette section va vous guider pour connecter votre instance Azure AD à votre compte d’utilisateur Dropbox for Business qui fournit l’API. Vous pourrez aussi découvrir comment configurer le service d’approvisionnement pour créer, mettre à jour et désactiver les comptes d’utilisateur assignés dans Dropbox for Business, en fonction de l’assignation des utilisateurs et des groupes dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="57f3f-122">This section guides you through connecting your Azure AD to Dropbox for Business's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Dropbox for Business based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="57f3f-123">Vous pouvez également choisir d’activer l’authentification unique basée sur SAML pour Dropbox for Business, grâce aux instructions disponibles sur le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="57f3f-123">You may also choose to enabled SAML-based Single Sign-On for Dropbox for Business, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="57f3f-124">L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que chacune de ces deux fonctionnalités compléte l’autre.</span><span class="sxs-lookup"><span data-stu-id="57f3f-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="to-configure-automatic-user-account-provisioning"></a><span data-ttu-id="57f3f-125">Pour configurer l’approvisionnement automatique des comptes d’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="57f3f-125">To configure automatic user account provisioning:</span></span>

1. <span data-ttu-id="57f3f-126">Sur le [portail Azure](https://portal.azure.com), accédez à la section **Azure Active Directory > Applications d’entreprise > Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="57f3f-126">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="57f3f-127">Si vous avez déjà configuré Dropbox for Business pour l’authentification unique, recherchez votre instance de Dropbox for Business à l’aide du champ de recherche.</span><span class="sxs-lookup"><span data-stu-id="57f3f-127">If you have already configured Dropbox for Business for single sign-on, search for your instance of Dropbox for Business using the search field.</span></span> <span data-ttu-id="57f3f-128">Sinon, sélectionnez **Ajouter** et recherchez **Dropbox for Business** dans la galerie d’applications.</span><span class="sxs-lookup"><span data-stu-id="57f3f-128">Otherwise, select **Add** and search for **Dropbox for Business** in the application gallery.</span></span> <span data-ttu-id="57f3f-129">Dans les résultats de la recherche, sélectionnez Dropbox for Business, puis ajoutez-la à votre liste d’applications.</span><span class="sxs-lookup"><span data-stu-id="57f3f-129">Select Dropbox for Business from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="57f3f-130">Sélectionnez votre instance de Dropbox for Business, puis sélectionnez l’onglet **Approvisionnement**.</span><span class="sxs-lookup"><span data-stu-id="57f3f-130">Select your instance of Dropbox for Business, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="57f3f-131">Définissez le **Mode d’approvisionnement** sur **Automatique**.</span><span class="sxs-lookup"><span data-stu-id="57f3f-131">Set the **Provisioning Mode** to **Automatic**.</span></span> 

    ![approvisionnement](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="57f3f-133">Sous la section **informations d’identification de l’administrateur**, cliquez sur **Autoriser**.</span><span class="sxs-lookup"><span data-stu-id="57f3f-133">Under the **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="57f3f-134">Cela permet d’ouvrir une boîte de dialogue de connexion à Dropbox for Business dans une nouvelle fenêtre de navigateur.</span><span class="sxs-lookup"><span data-stu-id="57f3f-134">It opens a Dropbox for Business login dialog in a new browser window.</span></span>

6. <span data-ttu-id="57f3f-135">Dans la boîte de dialogue **Se connecter à Dropbox pour établir une connexion à Active Directory**, connectez-vous à votre abonné Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="57f3f-135">On the **Sign-in to Dropbox to link with Azure AD** dialog, sign in to your Dropbox for Business tenant.</span></span>

     <span data-ttu-id="57f3f-136">![Approvisionnement d'utilisateurs](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "Approvisionnement d’utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="57f3f-136">![User provisioning](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "User provisioning")</span></span>

7. <span data-ttu-id="57f3f-137">Confirmez que vous souhaitez permettre à Azure Active Directory d’apporter des modifications à votre client Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="57f3f-137">Confirm that you would like to give Azure Active Directory permission to make changes to your Dropbox for Business tenant.</span></span> <span data-ttu-id="57f3f-138">Cliquez sur **Autoriser**.</span><span class="sxs-lookup"><span data-stu-id="57f3f-138">Click **Allow**.</span></span>
    
      <span data-ttu-id="57f3f-139">![Approvisionnement d'utilisateurs](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "Approvisionnement d’utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="57f3f-139">![User provisioning](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "User provisioning")</span></span>

8. <span data-ttu-id="57f3f-140">Sur le portail Azure, cliquez sur **Tester la connexion** pour vous assurer qu’Azure AD peut se connecter à votre application Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="57f3f-140">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Dropbox for Business app.</span></span> <span data-ttu-id="57f3f-141">Si la connexion échoue, vérifiez que votre compte Dropbox for Business dispose des autorisations d’administrateur d’équipe et recommencez l’étape **« Autoriser »**.</span><span class="sxs-lookup"><span data-stu-id="57f3f-141">If the connection fails, ensure your Dropbox for Business account has Team Admin permissions and try the **"Authorize"** step again.</span></span>

9. <span data-ttu-id="57f3f-142">Entrez l’adresse e-mail d’une personne ou d’un groupe qui doit recevoir les notifications d’erreur d’approvisionnement dans le champ **E-mail de notification**, et cochez la case.</span><span class="sxs-lookup"><span data-stu-id="57f3f-142">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

10. <span data-ttu-id="57f3f-143">Cliquez sur **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="57f3f-143">Click **Save.**</span></span>

11. <span data-ttu-id="57f3f-144">Dans la section Mappages, sélectionnez **Synchroniser des utilisateurs Azure Active Directory avec Dropbox for Business**.</span><span class="sxs-lookup"><span data-stu-id="57f3f-144">Under the Mappings section, select **Synchronize Azure Active Directory Users to Dropbox for Business.**</span></span>

12. <span data-ttu-id="57f3f-145">Dans la section **Mappages d’attributs**, passez en revue les attributs utilisateur qui sont synchronisés à partir d’Azure AD vers Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="57f3f-145">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Dropbox for Business.</span></span> <span data-ttu-id="57f3f-146">Les attributs sélectionnés en tant que propriétés de **Correspondance** servent à faire correspondre les comptes d’utilisateur dans Dropbox for Business, en vue d’opérations de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="57f3f-146">The attributes selected as **Matching** properties are used to match the user accounts in Dropbox for Business for update operations.</span></span> <span data-ttu-id="57f3f-147">Cliquez sur le bouton Enregistrer pour valider les modifications.</span><span class="sxs-lookup"><span data-stu-id="57f3f-147">Select the Save button to commit any changes.</span></span>

13. <span data-ttu-id="57f3f-148">Pour activer le service d’approvisionnement Azure AD pour Dropbox for Business, accédez à la section Paramètres et définissez l’**État de l’approvisionnement** sur **Activé**.</span><span class="sxs-lookup"><span data-stu-id="57f3f-148">To enable the Azure AD provisioning service for Dropbox for Business, change the **Provisioning Status** to **On** in the Settings section</span></span>

14. <span data-ttu-id="57f3f-149">Cliquez sur **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="57f3f-149">Click **Save.**</span></span>

<span data-ttu-id="57f3f-150">Cette commande démarre la synchronisation initiale des utilisateurs et/ou des groupes assignés à Dropbox for Business dans la section Utilisateurs et Groupes.</span><span class="sxs-lookup"><span data-stu-id="57f3f-150">It starts the initial synchronization of any users and/or groups assigned to Dropbox for Business in the Users and Groups section.</span></span> <span data-ttu-id="57f3f-151">La synchronisation initiale prend plus de temps que les synchronisations suivantes, qui se produisent environ toutes les 20 minutes, tant que le service est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="57f3f-151">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="57f3f-152">Vous pouvez utiliser la section **Détails de synchronisation** pour surveiller la progression et les liens vers les rapports d’activité d’approvisionnement, qui décrivent toutes les actions effectuées par le service de configuration dans votre application Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="57f3f-152">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Dropbox for Business app.</span></span>

<span data-ttu-id="57f3f-153">Vous pouvez désormais créer un compte de test.</span><span class="sxs-lookup"><span data-stu-id="57f3f-153">You can now create a test account.</span></span> <span data-ttu-id="57f3f-154">Patientez jusqu’à 20 minutes avant de vérifier que le compte a bien été synchronisé avec Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="57f3f-154">Wait for up to 20 minutes to verify that the account has been synchronized to Dropbox for Business.</span></span>

<span data-ttu-id="57f3f-155">Si le cycle d'approvisionnement d'utilisateur a abouti, l'état associé est indiqué.</span><span class="sxs-lookup"><span data-stu-id="57f3f-155">A successfully completed user provisioning cycle is indicated by a related status.</span></span>

<span data-ttu-id="57f3f-156">![Affecter des utilisateurs](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "Affecter des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="57f3f-156">![Assign users](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "Assign users")</span></span>


## <a name="additional-resources"></a><span data-ttu-id="57f3f-157">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="57f3f-157">Additional resources</span></span>

* [<span data-ttu-id="57f3f-158">Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise</span><span class="sxs-lookup"><span data-stu-id="57f3f-158">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="57f3f-159">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="57f3f-159">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="57f3f-160">Configurer l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="57f3f-160">Configure Single Sign-on</span></span>](active-directory-saas-dropboxforbusiness-tutorial.md)