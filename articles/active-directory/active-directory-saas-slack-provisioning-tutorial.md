---
title: "Didacticiel : Configuration de Slack pour l’approvisionnement automatique d’utilisateurs avec Azure Active Directory | Microsoft Docs"
description: "Découvrez comment configurer Azure Active Directory pour approvisionner et retirer automatiquement des comptes utilisateur sur Slack."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: sakula
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: asmalser-msft
ms.reviewer: asmalser
ms.openlocfilehash: 3cb49a4abb26c34a938c963c4cf326b5ccd490de
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-configuring-slack-for-automatic-user-provisioning"></a><span data-ttu-id="8be63-103">Didacticiel : Configuration de Slack pour l’approvisionnement automatique d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="8be63-103">Tutorial: Configuring Slack for Automatic User Provisioning</span></span>


<span data-ttu-id="8be63-104">L’objectif de ce didacticiel est de vous montrer les étapes à effectuer dans Slack et Azure AD pour approvisionner et retirer automatiquement des comptes utilisateur d’Azure AD vers Slack.</span><span class="sxs-lookup"><span data-stu-id="8be63-104">The objective of this tutorial is to show you the steps you need to perform in Slack and Azure AD to automatically provision and de-provision user accounts from Azure AD to Slack.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="8be63-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8be63-105">Prerequisites</span></span>

<span data-ttu-id="8be63-106">Le scénario décrit dans ce didacticiel part du principe que vous disposez des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="8be63-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="8be63-107">Un client Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8be63-107">An Azure Active Active directory tenant</span></span>
*   <span data-ttu-id="8be63-108">Un client Slack avec le [forfait Plus](https://aadsyncfabric.slack.com/pricing) ou mieux activé</span><span class="sxs-lookup"><span data-stu-id="8be63-108">A Slack tenant with the [Plus plan](https://aadsyncfabric.slack.com/pricing) or better enabled</span></span> 
*   <span data-ttu-id="8be63-109">Un compte d’utilisateur dans Slack avec les autorisations d’administrateur d’équipe</span><span class="sxs-lookup"><span data-stu-id="8be63-109">A user account in Slack with Team Admin permissions</span></span> 

<span data-ttu-id="8be63-110">Remarque : L’intégration de l’approvisionnement Azure AD s’appuie sur [l’API Slack SCIM](https://api.slack.com/scim) qui est disponible pour les équipes Slack disposant du forfait Plus ou mieux.</span><span class="sxs-lookup"><span data-stu-id="8be63-110">Note: The Azure AD provisioning integration relies on the [Slack SCIM API](https://api.slack.com/scim) which is available to Slack teams on the Plus plan or better.</span></span>

## <a name="assigning-users-to-slack"></a><span data-ttu-id="8be63-111">Affectation d’utilisateurs à Slack</span><span class="sxs-lookup"><span data-stu-id="8be63-111">Assigning users to Slack</span></span>

<span data-ttu-id="8be63-112">Azure Active Directory utilise un concept appelé « affectations » pour déterminer les utilisateurs devant recevoir l’accès aux applications sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="8be63-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="8be63-113">Dans le cadre de l’approvisionnement automatique en comptes utilisateur, les utilisateurs et les groupes qui ont été « attribués » à une application dans Azure AD seront synchronisés.</span><span class="sxs-lookup"><span data-stu-id="8be63-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="8be63-114">Avant de configurer et activer le service d’approvisionnement, vous devez déterminer quels utilisateurs et/ou groupes dans Azure AD représentent les utilisateurs qui ont besoin d’accéder à votre application Slack.</span><span class="sxs-lookup"><span data-stu-id="8be63-114">Before configuring and enabling the provisioning service, you will need to decide what users and/or groups in Azure AD represent the users who need access to your Slack app.</span></span> <span data-ttu-id="8be63-115">Une fois que vous avez choisi, vous pouvez affecter ces utilisateurs à votre application Slack en suivant les instructions fournies ici :</span><span class="sxs-lookup"><span data-stu-id="8be63-115">Once decided, you can assign these users to your Slack app by following the instructions here:</span></span>

[<span data-ttu-id="8be63-116">Affecter un utilisateur ou un groupe à une application d’entreprise</span><span class="sxs-lookup"><span data-stu-id="8be63-116">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-slack"></a><span data-ttu-id="8be63-117">Conseils importants pour l’affectation d’utilisateurs à Slack</span><span class="sxs-lookup"><span data-stu-id="8be63-117">Important tips for assigning users to Slack</span></span>

*   <span data-ttu-id="8be63-118">Il est recommandé qu’un seul utilisateur Azure AD soit affecté à Slack pour tester la configuration de l’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="8be63-118">It is recommended that a single Azure AD user be assigned to Slack to test the provisioning configuration.</span></span> <span data-ttu-id="8be63-119">Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="8be63-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="8be63-120">Lorsque vous affectez un utilisateur à Slack, vous devez sélectionner le rôle **Utilisateur** ou « Groupe » dans la boîte de dialogue d’attribution.</span><span class="sxs-lookup"><span data-stu-id="8be63-120">When assigning a user to Slack, you must select the **User** or "Group" role in the assignment dialog.</span></span> <span data-ttu-id="8be63-121">Le rôle « Accès par défaut » ne fonctionne pas pour l’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="8be63-121">The "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-to-slack"></a><span data-ttu-id="8be63-122">Configuration de l'approvisionnement des utilisateurs sur Slack</span><span class="sxs-lookup"><span data-stu-id="8be63-122">Configuring user provisioning to Slack</span></span> 

<span data-ttu-id="8be63-123">Cette section vous guide à travers la connexion de votre instance d’Azure AD au compte d’utilisateur fournissant l’API et la configuration du service d’approvisionnement pour créer, mettre à jour et désactiver les comptes utilisateur affectés dans Slack en fonction des attributions d’utilisateurs et de groupes dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8be63-123">This section guides you through connecting your Azure AD to Slack's user account provisioning API, and configuring the provisioning service to create, update and disable assigned user accounts in Slack based on user and group assignment in Azure AD.</span></span>

<span data-ttu-id="8be63-124">**Conseil :** vous pouvez également choisir d’activer l’authentification unique basée sur SAML pour Slack en suivant les instructions fournies dans le (portail Azure)[https://portal.azure.com].</span><span class="sxs-lookup"><span data-stu-id="8be63-124">**Tip:** You may also choose to enabled SAML-based Single Sign-On for Slack, following the instructions provided in (Azure portal)[https://portal.azure.com].</span></span> <span data-ttu-id="8be63-125">L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que chacune de ces deux fonctionnalités compléte l’autre.</span><span class="sxs-lookup"><span data-stu-id="8be63-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="to-configure-automatic-user-account-provisioning-to-slack-in-azure-ad"></a><span data-ttu-id="8be63-126">Pour configurer l’approvisionnement automatique de comptes utilisateur vers Slack dans Azure AD :</span><span class="sxs-lookup"><span data-stu-id="8be63-126">To configure automatic user account provisioning to Slack in Azure AD:</span></span>


1)  <span data-ttu-id="8be63-127">Dans le [portail Azure](https://portal.azure.com), accédez à la section **Azure Active Directory > Applications d’entreprise > Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8be63-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2) <span data-ttu-id="8be63-128">Si vous avez déjà configuré Slack pour l’authentification unique, recherchez votre instance de Slack à l’aide du champ de recherche.</span><span class="sxs-lookup"><span data-stu-id="8be63-128">If you have already configured Slack for single sign-on, search for your instance of Slack using the search field.</span></span> <span data-ttu-id="8be63-129">Sinon, sélectionnez **Ajouter** et recherchez **Slack** dans la galerie d’applications.</span><span class="sxs-lookup"><span data-stu-id="8be63-129">Otherwise, select **Add** and search for **Slack** in the application gallery.</span></span> <span data-ttu-id="8be63-130">Sélectionnez Slack dans les résultats de recherche et ajoutez-le à votre liste d’applications.</span><span class="sxs-lookup"><span data-stu-id="8be63-130">Select Slack from the search results, and add it to your list of applications.</span></span>

3)  <span data-ttu-id="8be63-131">Sélectionnez votre instance de Slack, puis sélectionnez l’onglet **Approvisionnement**.</span><span class="sxs-lookup"><span data-stu-id="8be63-131">Select your instance of Slack, then select the **Provisioning** tab.</span></span>

4)  <span data-ttu-id="8be63-132">Définissez le **Mode d’approvisionnement** sur **Automatique**.</span><span class="sxs-lookup"><span data-stu-id="8be63-132">Set the **Provisioning Mode** to **Automatic**.</span></span>

![Approvisionnement Slack](./media/active-directory-saas-slack-provisioning-tutorial/Slack1.PNG)

5)  <span data-ttu-id="8be63-134">Sous la section **informations d’identification de l’administrateur**, cliquez sur **Autoriser**.</span><span class="sxs-lookup"><span data-stu-id="8be63-134">Under the **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="8be63-135">Une boîte de dialogue d’autorisation Slack s’ouvre dans une nouvelle fenêtre de navigateur.</span><span class="sxs-lookup"><span data-stu-id="8be63-135">This opens a Slack authorization dialog in a new browser window.</span></span> 

6) <span data-ttu-id="8be63-136">Dans la nouvelle fenêtre, connectez-vous à Slack à l’aide de votre compte d’administrateur d’équipe.</span><span class="sxs-lookup"><span data-stu-id="8be63-136">In the new window, sign into Slack using your Team Admin account.</span></span> <span data-ttu-id="8be63-137">Dans la boîte de dialogue d’autorisation qui s’affiche, sélectionnez l’équipe Slack pour laquelle vous souhaitez activer l’approvisionnement, puis sélectionnez **Autoriser**.</span><span class="sxs-lookup"><span data-stu-id="8be63-137">in the resulting authorization dialog, select the Slack team that you want to enable provisioning for, and then select **Authorize**.</span></span> <span data-ttu-id="8be63-138">Une fois cela terminé, revenez au portail Azure pour terminer la configuration de l’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="8be63-138">Once completed, return to the Azure portal to complete the provisioning configuration.</span></span>

![Boîte de dialogue d’autorisation](./media/active-directory-saas-slack-provisioning-tutorial/Slack3.PNG)

7) <span data-ttu-id="8be63-140">Dans le portail Azure, cliquez sur **Tester la connexion** pour vous assurer qu’Azure AD peut se connecter à votre application Slack.</span><span class="sxs-lookup"><span data-stu-id="8be63-140">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Slack app.</span></span> <span data-ttu-id="8be63-141">Si la connexion échoue, vérifiez que votre compte Slack dispose des autorisations d’administrateur d’équipe et recommencez l’étape « Autoriser ».</span><span class="sxs-lookup"><span data-stu-id="8be63-141">If the connection fails, ensure your Slack account has Team Admin permissions and try the "Authorize" step again.</span></span>

8) <span data-ttu-id="8be63-142">Entrez l’adresse de messagerie d’une personne ou d’un groupe qui doit recevoir les notifications d’erreur d’approvisionnement dans le champ **Adresse électronique de notification**, puis cochez la case se trouvant en dessous.</span><span class="sxs-lookup"><span data-stu-id="8be63-142">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

9) <span data-ttu-id="8be63-143">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="8be63-143">Click **Save**.</span></span> 

10) <span data-ttu-id="8be63-144">Dans la section Mappages, sélectionnez **Synchroniser les utilisateurs Azure Active Directory avec Slack**.</span><span class="sxs-lookup"><span data-stu-id="8be63-144">Under the Mappings section, select **Synchronize Azure Active Directory Users to Slack**.</span></span>

11) <span data-ttu-id="8be63-145">Dans la section **Mappages des attributs**, passez en revue les attributs utilisateur qui seront synchronisés d’Azure AD vers Slack.</span><span class="sxs-lookup"><span data-stu-id="8be63-145">In the **Attribute Mappings** section, review the user attributes that will be synchronized from Azure AD to Slack.</span></span> <span data-ttu-id="8be63-146">Notez que les attributs sélectionnés en tant que propriétés de **Correspondance** seront utilisés pour faire correspondre les comptes d’utilisateur dans Slack pour les opérations de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="8be63-146">Note that the attributes selected as **Matching** properties will be used to match the user accounts in Slack for update operations.</span></span> <span data-ttu-id="8be63-147">Cliquez sur le bouton Enregistrer pour valider les modifications.</span><span class="sxs-lookup"><span data-stu-id="8be63-147">Select the Save button to commit any changes.</span></span>

12) <span data-ttu-id="8be63-148">Pour activer le service d’approvisionnement Azure AD pour Slack, modifiez le paramètre **État d’approvisionnement** sur **Activé** dans la section **Paramètres**</span><span class="sxs-lookup"><span data-stu-id="8be63-148">To enable the Azure AD provisioning service for Slack, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

13) <span data-ttu-id="8be63-149">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="8be63-149">Click **Save**.</span></span> 

<span data-ttu-id="8be63-150">Cette commande démarre la synchronisation initiale des utilisateurs et/ou groupes affectés à Slack dans la section Utilisateurs et Groupes.</span><span class="sxs-lookup"><span data-stu-id="8be63-150">This will start the initial synchronization of any users and/or groups assigned to Slack in the Users and Groups section.</span></span> <span data-ttu-id="8be63-151">Notez que la synchronisation initiale prendra plus de temps que les synchronisations suivantes, qui se produisent toutes les 10 minutes environ, tant que le service est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="8be63-151">Note that the initial sync will take longer to perform than subsequent syncs, which occur approximately every 10 minutes as long as the service is running.</span></span> <span data-ttu-id="8be63-152">Vous pouvez utiliser la section **Détails de synchronisation** pour surveiller la progression et les liens vers les rapports d’activité d’approvisionnement, qui décrivent toutes les actions effectuées par le service de configuration dans votre application Slack.</span><span class="sxs-lookup"><span data-stu-id="8be63-152">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Slack app.</span></span>

## <a name="optional-configuring-group-object-provisioning-to-slack"></a><span data-ttu-id="8be63-153">[Facultatif] Configuration de l’approvisionnement d’objets de groupe vers Slack</span><span class="sxs-lookup"><span data-stu-id="8be63-153">[Optional] Configuring group object provisioning to Slack</span></span> 

<span data-ttu-id="8be63-154">Si vous le souhaitez, vous pouvez activer l’approvisionnement des objets de groupe d’Azure AD vers Slack.</span><span class="sxs-lookup"><span data-stu-id="8be63-154">Optionally, you can enable the provisioning of group objects from Azure AD to Slack.</span></span> <span data-ttu-id="8be63-155">Cela est différent de « l’affectation de groupes d’utilisateurs », dans la mesure où l’objet de groupe réel sera répliqué en plus de ses membres d’Azure AD vers Slack.</span><span class="sxs-lookup"><span data-stu-id="8be63-155">This is different from "assigning groups of users", in that the actual group object in addition to its members will be replicated from Azure AD to Slack.</span></span> <span data-ttu-id="8be63-156">Par exemple, si vous avez un groupe nommé « Mon groupe » dans Azure AD, un groupe identique nommé « Mon groupe » est créé dans Slack.</span><span class="sxs-lookup"><span data-stu-id="8be63-156">For example, if you have a group named "My Group" in Azure AD, an identitical group named "My Group" will be created inside Slack.</span></span>

### <a name="to-enable-provisioning-of-group-objects"></a><span data-ttu-id="8be63-157">Pour activer l’approvisionnement des objets de groupe :</span><span class="sxs-lookup"><span data-stu-id="8be63-157">To enable provisioning of group objects:</span></span>

1) <span data-ttu-id="8be63-158">Dans la section Mappages, sélectionnez **Synchroniser les groupes Azure Active Directory avec Slack**.</span><span class="sxs-lookup"><span data-stu-id="8be63-158">Under the Mappings section, select **Synchronize Azure Active Directory Groups to Slack**.</span></span>

2) <span data-ttu-id="8be63-159">Dans le volet de Mappage des attributs, définissez Activé sur Oui.</span><span class="sxs-lookup"><span data-stu-id="8be63-159">In the Attribute Mapping blade, set Enabled to Yes.</span></span>

3) <span data-ttu-id="8be63-160">Dans la section **Mappages des attributs**, passez en revue les attributs de groupe qui seront synchronisés d’Azure AD vers Slack.</span><span class="sxs-lookup"><span data-stu-id="8be63-160">In the **Attribute Mappings** section, review the group attributes that will be synchronized from Azure AD to Slack.</span></span> <span data-ttu-id="8be63-161">Notez que les attributs sélectionnés en tant que propriétés de **Correspondance** seront utilisés pour faire correspondre les groupes dans Slack pour les opérations de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="8be63-161">Note that the attributes selected as **Matching** properties will be used to match the groups in Slack for update operations.</span></span> 

4) <span data-ttu-id="8be63-162">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="8be63-162">Click **Save**.</span></span>

<span data-ttu-id="8be63-163">Ainsi, les objets de groupe affectés à Slack dans la section **Utilisateurs et groupes** seront entièrement synchronisés d’Azure AD vers Slack.</span><span class="sxs-lookup"><span data-stu-id="8be63-163">This result in any group objects assigned to Slack in the **Users and Groups** section being fully synchronized from Azure AD to Slack.</span></span> <span data-ttu-id="8be63-164">Vous pouvez utiliser la section **Détails de synchronisation** pour surveiller la progression et les liens vers les rapports d’activité d’approvisionnement, qui décrivent toutes les actions effectuées par le service de configuration dans votre application Slack.</span><span class="sxs-lookup"><span data-stu-id="8be63-164">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Slack app.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="8be63-165">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="8be63-165">Additional Resources</span></span>

* [<span data-ttu-id="8be63-166">Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise</span><span class="sxs-lookup"><span data-stu-id="8be63-166">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="8be63-167">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="8be63-167">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
