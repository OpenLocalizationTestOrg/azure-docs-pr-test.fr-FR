---
title: "Didacticiel : Configuration de Cerner Central pour l’approvisionnement automatique d’utilisateurs avec Azure Active Directory | Microsoft Docs"
description: "Découvrez comment configurer Azure Active Directory pour approvisionner automatiquement des utilisateurs dans une liste de Cerner Central."
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
ms.date: 05/26/2017
ms.author: asmalser-msft
ms.openlocfilehash: 84613b7f8d7bd031d492a62da0bc53be96ac45a3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-configuring-cerner-central-for-automatic-user-provisioning"></a><span data-ttu-id="73f35-103">Didacticiel : Configuration de Cerner Central pour l’approvisionnement automatique d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="73f35-103">Tutorial: Configuring Cerner Central for Automatic User Provisioning</span></span>

<span data-ttu-id="73f35-104">Ce didacticiel vous montre les étapes à effectuer dans Cerner Central et Azure AD pour approvisionner et retirer automatiquement des comptes d’utilisateur d’Azure AD vers une liste d’utilisateurs dans Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="73f35-104">The objective of this tutorial is to show you the steps you need to perform in Cerner Central and Azure AD to automatically provision and de-provision user accounts from Azure AD to a user roster in Cerner Central.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="73f35-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="73f35-105">Prerequisites</span></span>

<span data-ttu-id="73f35-106">Le scénario décrit dans ce didacticiel part du principe que vous disposez des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="73f35-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="73f35-107">Un client Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="73f35-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="73f35-108">Un locataire Cerner Central</span><span class="sxs-lookup"><span data-stu-id="73f35-108">A Cerner Central tenant</span></span> 

> [!NOTE]
> <span data-ttu-id="73f35-109">Azure Active Directory s’intègre dans Cerner Central à l’aide du protocole [SCIM](http://www.simplecloud.info/).</span><span class="sxs-lookup"><span data-stu-id="73f35-109">Azure Active Directory integrates with Cerner Central using the [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-to-cerner-central"></a><span data-ttu-id="73f35-110">Assignation d’utilisateurs à Cerner Central</span><span class="sxs-lookup"><span data-stu-id="73f35-110">Assigning users to Cerner Central</span></span>

<span data-ttu-id="73f35-111">Azure Active Directory utilise un concept appelé « affectations » pour déterminer les utilisateurs devant recevoir l’accès aux applications sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="73f35-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="73f35-112">Dans le cadre de l’approvisionnement automatique de comptes utilisateur, seuls les utilisateurs et les groupes qui ont été « assignés » à une application dans Azure AD sont synchronisés.</span><span class="sxs-lookup"><span data-stu-id="73f35-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD are synchronized.</span></span> 

<span data-ttu-id="73f35-113">Avant de configurer et d’activer le service d’approvisionnement, vous devez déterminer quels utilisateurs et/ou groupes dans Azure AD représentent les utilisateurs qui ont besoin d’accéder à votre application Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="73f35-113">Before configuring and enabling the provisioning service, you should decide what users and/or groups in Azure AD represent the users who need access to Cerner Central.</span></span> <span data-ttu-id="73f35-114">Une fois que vous avez choisi, vous pouvez assigner ces utilisateurs à votre application Cerner Central en suivant les instructions fournies ici :</span><span class="sxs-lookup"><span data-stu-id="73f35-114">Once decided, you can assign these users to Cerner Central by following the instructions here:</span></span>

[<span data-ttu-id="73f35-115">Affecter un utilisateur ou un groupe à une application d’entreprise</span><span class="sxs-lookup"><span data-stu-id="73f35-115">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-cerner-central"></a><span data-ttu-id="73f35-116">Conseils importants pour l’assignation d’utilisateurs à Cerner Central</span><span class="sxs-lookup"><span data-stu-id="73f35-116">Important tips for assigning users to Cerner Central</span></span>

*   <span data-ttu-id="73f35-117">Il est recommandé qu’un seul utilisateur Azure AD soit assigné à Cerner Central pour tester la configuration de l’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="73f35-117">It is recommended that a single Azure AD user be assigned to Cerner Central to test the provisioning configuration.</span></span> <span data-ttu-id="73f35-118">Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="73f35-118">Additional users and/or groups may be assigned later.</span></span>

* <span data-ttu-id="73f35-119">Une fois le test initial terminé pour un seul utilisateur, Cerner Central recommande d’assigner la liste complète des utilisateurs censés pouvoir accéder à toutes les solutions Cerner (et pas seulement Cerner Central) pour un approvisionnement vers la liste d’utilisateurs Cerner.</span><span class="sxs-lookup"><span data-stu-id="73f35-119">Once initial testing is complete for a single user, Cerner Central recommends assigning the entire list of users intended to access any Cerner solution (not just Cerner Central) to be provisioned to Cerner’s user roster.</span></span>  <span data-ttu-id="73f35-120">Les autres solutions Cerner tirent parti de cette liste d’utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="73f35-120">Other Cerner solutions leverage this list of users in the user roster.</span></span>

*   <span data-ttu-id="73f35-121">Quand vous assignez un utilisateur à Cerner Central, vous devez sélectionner le rôle **Utilisateur** dans la boîte de dialogue d’assignation.</span><span class="sxs-lookup"><span data-stu-id="73f35-121">When assigning a user to Cerner Central, you must select the **User** role in the assignment dialog.</span></span> <span data-ttu-id="73f35-122">Les utilisateurs dont le rôle est « Accès par défaut » sont exclus de l’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="73f35-122">Users with the "Default Access" role are excluded from provisioning.</span></span>


## <a name="configuring-user-provisioning-to-cerner-central"></a><span data-ttu-id="73f35-123">Configuration de l’approvisionnement des utilisateurs sur Cerner Central</span><span class="sxs-lookup"><span data-stu-id="73f35-123">Configuring user provisioning to Cerner Central</span></span>

<span data-ttu-id="73f35-124">Cette section vous explique comment connecter votre instance d’Azure AD à la liste d’utilisateurs Cerner Central par le biais de l’API d’approvisionnement de comptes d’utilisateur SCIM Cerner, et comment configurer le service d’approvisionnement afin de créer, mettre à jour et désactiver des comptes d’utilisateur assignés dans Cerner Central en fonction des assignations d’utilisateurs et de groupes dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="73f35-124">This section guides you through connecting your Azure AD to Cerner Central’s User Roster using Cerner's SCIM user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Cerner Central based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="73f35-125">Vous pouvez également choisir d’activer l’authentification unique basée sur SAML pour Cerner Central en suivant les instructions fournies dans le portail Azure (https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="73f35-125">You may also choose to enabled SAML-based Single Sign-On for Cerner Central, following the instructions provided in [Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="73f35-126">L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que ces deux fonctionnalités se complètent.</span><span class="sxs-lookup"><span data-stu-id="73f35-126">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span> <span data-ttu-id="73f35-127">Pour plus d’informations, consultez le [didacticiel dédié à l’authentification unique dans Cerner Central](active-directory-saas-cernercentral-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="73f35-127">For more information, see the [Cerner Central single sign-on tutorial](active-directory-saas-cernercentral-tutorial.md).</span></span>


### <a name="to-configure-automatic-user-account-provisioning-to-cerner-central-in-azure-ad"></a><span data-ttu-id="73f35-128">Pour configurer l’approvisionnement automatique de comptes d’utilisateur sur Cerner Central dans Azure AD :</span><span class="sxs-lookup"><span data-stu-id="73f35-128">To configure automatic user account provisioning to Cerner Central in Azure AD:</span></span>


<span data-ttu-id="73f35-129">Pour approvisionner des comptes d’utilisateur sur Cerner Central, vous devez demander la création d’un compte système Cerner Central auprès de Cerner et générer un jeton du porteur OAuth qu’Azure AD utilisera pour se connecter au point de terminaison SCIM de Cerner.</span><span class="sxs-lookup"><span data-stu-id="73f35-129">In order to provision user accounts to Cerner Central, you’ll need to request a Cerner Central system account from Cerner, and generate an OAuth bearer token that Azure AD can use to connect to Cerner's SCIM endpoint.</span></span> <span data-ttu-id="73f35-130">Il est également recommandé d’exécuter l’intégration dans un environnement de bac à sable Cerner avant le déploiement en production.</span><span class="sxs-lookup"><span data-stu-id="73f35-130">It is also recommended that the integration be performed in a Cerner sandbox environment before deploying to production.</span></span>

1.  <span data-ttu-id="73f35-131">La première étape consiste à s’assurer que les personnes gérant l’intégration Cerner et Azure AD disposent d’un compte CernerCare, qui est requis afin d’accéder à la documentation nécessaire pour suivre les instructions.</span><span class="sxs-lookup"><span data-stu-id="73f35-131">The first step is to ensure the people managing the Cerner and Azure AD integration have a CernerCare account, which is required to access the documentation necessary to complete the instructions.</span></span> <span data-ttu-id="73f35-132">Si besoin est, utilisez les URL ci-dessous pour créer des comptes CernerCare dans chaque environnement applicable.</span><span class="sxs-lookup"><span data-stu-id="73f35-132">If necessary, use the URLs below to create CernerCare accounts in each applicable environment.</span></span>

   * <span data-ttu-id="73f35-133">Bac à sable : https://sandboxcernercare.com/accounts/create</span><span class="sxs-lookup"><span data-stu-id="73f35-133">Sandbox:  https://sandboxcernercare.com/accounts/create</span></span>

   * <span data-ttu-id="73f35-134">Production : https://cernercare.com/accounts/create</span><span class="sxs-lookup"><span data-stu-id="73f35-134">Production:  https://cernercare.com/accounts/create</span></span>  

2.  <span data-ttu-id="73f35-135">Vous devez ensuite créer un compte système pour Azure AD.</span><span class="sxs-lookup"><span data-stu-id="73f35-135">Next, a system account must be created for Azure AD.</span></span> <span data-ttu-id="73f35-136">Utilisez les instructions ci-dessous afin de demander un compte système pour vos environnements de bac à sable et de production.</span><span class="sxs-lookup"><span data-stu-id="73f35-136">Use the instructions below to request a System Account for your sandbox and production environments.</span></span>

   * <span data-ttu-id="73f35-137">Instructions : https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account</span><span class="sxs-lookup"><span data-stu-id="73f35-137">Instructions:  https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account</span></span>

   * <span data-ttu-id="73f35-138">Bac à sable : https://sandboxcernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="73f35-138">Sandbox: https://sandboxcernercentral.com/system-accounts/</span></span>

   * <span data-ttu-id="73f35-139">Production : https://cernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="73f35-139">Production:  https://cernercentral.com/system-accounts/</span></span>

3.  <span data-ttu-id="73f35-140">Générez ensuite un jeton du porteur OAuth pour chacun de vos comptes système.</span><span class="sxs-lookup"><span data-stu-id="73f35-140">Next, generate an OAuth bearer token for each of your system accounts.</span></span> <span data-ttu-id="73f35-141">Pour ce faire, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="73f35-141">To do this, follow the instructions below.</span></span>

   * <span data-ttu-id="73f35-142">Instructions : https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token</span><span class="sxs-lookup"><span data-stu-id="73f35-142">Instructions:  https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token</span></span>

   * <span data-ttu-id="73f35-143">Bac à sable : https://sandboxcernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="73f35-143">Sandbox: https://sandboxcernercentral.com/system-accounts/</span></span>

   * <span data-ttu-id="73f35-144">Production : https://cernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="73f35-144">Production:  https://cernercentral.com/system-accounts/</span></span>

4. <span data-ttu-id="73f35-145">Enfin, vous devez acquérir des ID de domaine de liste d’utilisateurs pour le bac à sable et les environnements de production dans Cerner afin de terminer la configuration.</span><span class="sxs-lookup"><span data-stu-id="73f35-145">Finally, you need to acquire User Roster Realm IDs for both the sandbox and production environments in Cerner to complete the configuration.</span></span> <span data-ttu-id="73f35-146">Pour plus d’informations à ce sujet, consultez : https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM.</span><span class="sxs-lookup"><span data-stu-id="73f35-146">For information on how to acquire this, see: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM.</span></span> 

5. <span data-ttu-id="73f35-147">Vous pouvez maintenant configurer Azure AD afin d’approvisionner des comptes d’utilisateur sur Cerner.</span><span class="sxs-lookup"><span data-stu-id="73f35-147">Now you can configure Azure AD to provision user accounts to Cerner.</span></span> <span data-ttu-id="73f35-148">Connectez-vous au [portail Azure](https://portal.azure.com), puis accédez à la section **Azure Active Directory > Applications d’entreprise > Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="73f35-148">Sign in to the [Azure portal](https://portal.azure.com), and browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

6. <span data-ttu-id="73f35-149">Si vous avez déjà configuré Cerner Central pour l’authentification unique, recherchez votre instance de Cerner Central à l’aide du champ de recherche.</span><span class="sxs-lookup"><span data-stu-id="73f35-149">If you have already configured Cerner Central for single sign-on, search for your instance of Cerner Central using the search field.</span></span> <span data-ttu-id="73f35-150">Sinon, sélectionnez **Ajouter** et recherchez **Cerner Central** dans la galerie d’applications.</span><span class="sxs-lookup"><span data-stu-id="73f35-150">Otherwise, select **Add** and search for **Cerner Central** in the application gallery.</span></span> <span data-ttu-id="73f35-151">Sélectionnez Cerner Central dans les résultats de recherche et ajoutez-le à votre liste d’applications.</span><span class="sxs-lookup"><span data-stu-id="73f35-151">Select Cerner Central from the search results, and add it to your list of applications.</span></span>

7.  <span data-ttu-id="73f35-152">Sélectionnez votre instance de Cerner Central, puis sélectionnez l’onglet **Approvisionnement**.</span><span class="sxs-lookup"><span data-stu-id="73f35-152">Select your instance of Cerner Central, then select the **Provisioning** tab.</span></span>

8.  <span data-ttu-id="73f35-153">Définissez le **Mode d’approvisionnement** sur **Automatique**.</span><span class="sxs-lookup"><span data-stu-id="73f35-153">Set the **Provisioning Mode** to **Automatic**.</span></span>

   ![Approvisionnement Central Cerner](./media/active-directory-saas-cernercentral-provisioning-tutorial/Cerner.PNG)

9.  <span data-ttu-id="73f35-155">Renseignez les champs suivants sous **Informations d’identification de l’administrateur** :</span><span class="sxs-lookup"><span data-stu-id="73f35-155">Fill in the following fields under **Admin Credentials**:</span></span>

   * <span data-ttu-id="73f35-156">Dans le champ **URL de locataire**, entrez une URL au format ci-dessous, en remplaçant « User-Roster-Realm-ID » par l’ID de domaine que vous avez obtenu à l’étape 4.</span><span class="sxs-lookup"><span data-stu-id="73f35-156">In the **Tenant URL** field, enter a URL in the format below, replacing "User-Roster-Realm-ID" with the realm ID you acquired in step #4.</span></span>

> <span data-ttu-id="73f35-157">Bac à sable : https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span><span class="sxs-lookup"><span data-stu-id="73f35-157">Sandbox: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span></span> 

> <span data-ttu-id="73f35-158">Production : https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span><span class="sxs-lookup"><span data-stu-id="73f35-158">Production: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span></span> 

   * <span data-ttu-id="73f35-159">Dans le champ **Jeton secret**, entrez le jeton du porteur OAuth que vous avez généré à l’étape 3, puis cliquez sur **Tester la connexion**.</span><span class="sxs-lookup"><span data-stu-id="73f35-159">In the **Secret Token** field, enter the OAuth bearer token you generated in step #3 and click **Test Connection**.</span></span>

   * <span data-ttu-id="73f35-160">Une notification de réussite doit s’afficher en haut à droite de votre portail.</span><span class="sxs-lookup"><span data-stu-id="73f35-160">You should see a success notification on the upper­right side of your portal.</span></span>

10. <span data-ttu-id="73f35-161">Entrez l’adresse e-mail d’une personne ou d’un groupe qui doit recevoir les notifications d’erreur d’approvisionnement dans le champ **E-mail de notification**, puis cochez la case se trouvant en dessous.</span><span class="sxs-lookup"><span data-stu-id="73f35-161">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

11. <span data-ttu-id="73f35-162">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="73f35-162">Click **Save**.</span></span> 

12. <span data-ttu-id="73f35-163">Dans la section **Mappages d’attributs**, passez en revue les attributs d’utilisateur et de groupe qui seront synchronisés entre Azure AD et Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="73f35-163">In the **Attribute Mappings** section, review the user and group attributes to be synchronized from Azure AD to Cerner Central.</span></span> <span data-ttu-id="73f35-164">Les attributs sélectionnés en tant que propriétés **Correspondance** sont utilisés pour faire correspondre les comptes d’utilisateur et les groupes dans Cerner Central pour les opérations de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="73f35-164">The attributes selected as **Matching** properties are used to match the user accounts and groups in Cerner Central for update operations.</span></span> <span data-ttu-id="73f35-165">Cliquez sur le bouton Enregistrer pour valider les modifications.</span><span class="sxs-lookup"><span data-stu-id="73f35-165">Select the Save button to commit any changes.</span></span>

13. <span data-ttu-id="73f35-166">Afin d’activer le service d’approvisionnement Azure AD pour Cerner Central, modifiez le paramètre **État d’approvisionnement** sur **Activé** dans la section **Paramètres**</span><span class="sxs-lookup"><span data-stu-id="73f35-166">To enable the Azure AD provisioning service for Cerner Central, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

14. <span data-ttu-id="73f35-167">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="73f35-167">Click **Save**.</span></span> 

<span data-ttu-id="73f35-168">Cette commande lance la synchronisation initiale des utilisateurs et/ou groupes assignés à Cerner Central dans la section Utilisateurs et Groupes.</span><span class="sxs-lookup"><span data-stu-id="73f35-168">This starts the initial synchronization of any users and/or groups assigned to Cerner Central in the Users and Groups section.</span></span> <span data-ttu-id="73f35-169">La synchronisation initiale prend plus de temps que les synchronisations suivantes, qui se produisent environ toutes les 20 minutes tant que le service d’approvisionnement Azure AD est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="73f35-169">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the Azure AD provisioning service is running.</span></span> <span data-ttu-id="73f35-170">Vous pouvez utiliser la section **Détails de synchronisation** pour surveiller la progression et les liens vers les rapports d’activité d’approvisionnement, qui décrivent toutes les actions effectuées par le service d’approvisionnement dans votre application Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="73f35-170">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Cerner Central app.</span></span>

<span data-ttu-id="73f35-171">Pour plus d’informations sur la lecture des journaux d’approvisionnement Azure AD, consultez [Création de rapports sur l’approvisionnement automatique de comptes d’utilisateur](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="73f35-171">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="73f35-172">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="73f35-172">Additional resources</span></span>

* <span data-ttu-id="73f35-173">[Cerner Central: Publishing identity data using Azure AD](https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+Azure+AD) (Cerner Central : Publication des données d’identité à l’aide d’Azure AD)</span><span class="sxs-lookup"><span data-stu-id="73f35-173">[Cerner Central: Publishing identity data using Azure AD](https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+Azure+AD)</span></span>
* <span data-ttu-id="73f35-174">[Tutorial: Configuring Cerner Central for single sign-on with Azure Active Directory](active-directory-saas-cernercentral-tutorial.md) (Didacticiel : Configuration de Cerner Central pour l’authentification unique avec Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="73f35-174">[Tutorial: Configuring Cerner Central for single sign-on with Azure Active Directory](active-directory-saas-cernercentral-tutorial.md)</span></span>
* [<span data-ttu-id="73f35-175">Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise</span><span class="sxs-lookup"><span data-stu-id="73f35-175">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="73f35-176">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="73f35-176">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="73f35-177">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="73f35-177">Next steps</span></span>
* <span data-ttu-id="73f35-178">[Découvrez comment consulter les journaux et obtenir des rapports sur l’activité d’approvisionnement](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="73f35-178">[Learn how to review logs and get reports on provisioning activity](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>
