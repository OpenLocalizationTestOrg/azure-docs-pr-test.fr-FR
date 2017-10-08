---
title: "Didacticiel : Intégration d'Azure Active Directory à Dropbox for Business | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Dropbox for Business."
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
ms.openlocfilehash: 0fb01eab4f7c6c4516eac64a4343e46ea221f98d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-dropbox-for-business-for-automatic-user-provisioning"></a><span data-ttu-id="537c0-103">Didacticiel : Configuration de Dropbox for Business pour approvisionner automatiquement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="537c0-103">Tutorial: Configuring Dropbox for Business for Automatic User Provisioning</span></span>

<span data-ttu-id="537c0-104">objectif Hello de ce didacticiel est tooshow vous hello étapes que vous devez tooperform dans Dropbox pour l’entreprise et Azure AD tooautomatically approvisionner et configurer des comptes d’utilisateur à partir d’Azure AD tooDropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="537c0-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Dropbox for Business and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooDropbox for Business.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="537c0-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="537c0-105">Prerequisites</span></span>

<span data-ttu-id="537c0-106">scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="537c0-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="537c0-107">Un locataire Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="537c0-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="537c0-108">Un abonnement Dropbox for Business pour lequel l’authentification unique est activée.</span><span class="sxs-lookup"><span data-stu-id="537c0-108">A Dropbox for Business single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="537c0-109">Un compte d’utilisateur dans Dropbox for Business avec les autorisations d’administrateur d’équipe.</span><span class="sxs-lookup"><span data-stu-id="537c0-109">A user account in Dropbox for Business with Team Admin permissions.</span></span>

## <a name="assigning-users-toodropbox-for-business"></a><span data-ttu-id="537c0-110">Affectation d’utilisateurs tooDropbox for Business</span><span class="sxs-lookup"><span data-stu-id="537c0-110">Assigning users tooDropbox for Business</span></span>

<span data-ttu-id="537c0-111">Azure Active Directory utilise un concept appelé toodetermine « affectations » les utilisateurs qui doivent recevoir l’accès tooselected applications.</span><span class="sxs-lookup"><span data-stu-id="537c0-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="537c0-112">Dans le contexte de hello de configuration de compte automatique d’utilisateurs, seuls les utilisateurs de hello et les groupes qui ont été « affectés » application tooan dans Azure AD est synchronisé.</span><span class="sxs-lookup"><span data-stu-id="537c0-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="537c0-113">Avant de configurer et de l’activation de hello service de configuration, vous devez toodecide quels utilisateurs ou des groupes dans Azure AD représentent hello des utilisateurs qui doivent accéder aux tooyour Dropbox pour l’application d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="537c0-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Dropbox for Business app.</span></span> <span data-ttu-id="537c0-114">Après choisi, vous pouvez attribuer ces tooyour utilisateurs Dropbox pour l’application d’entreprise en suivant les instructions hello ici :</span><span class="sxs-lookup"><span data-stu-id="537c0-114">Once decided, you can assign these users tooyour Dropbox for Business app by following hello instructions here:</span></span>

[<span data-ttu-id="537c0-115">Affecter une application d’entreprise tooan utilisateur ou un groupe</span><span class="sxs-lookup"><span data-stu-id="537c0-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toodropbox-for-business"></a><span data-ttu-id="537c0-116">Conseils importants pour l’affectation d’utilisateurs tooDropbox for Business</span><span class="sxs-lookup"><span data-stu-id="537c0-116">Important tips for assigning users tooDropbox for Business</span></span>

*   <span data-ttu-id="537c0-117">Il est recommandé qu’un seul utilisateur Azure AD est attribué tooDropbox pour hello de tootest entreprise service de la configuration.</span><span class="sxs-lookup"><span data-stu-id="537c0-117">It is recommended that a single Azure AD user is assigned tooDropbox for Business tootest hello provisioning configuration.</span></span> <span data-ttu-id="537c0-118">Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="537c0-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="537c0-119">Lorsque vous affectez un tooDropbox utilisateur pour l’entreprise, vous devez sélectionner un rôle d’utilisateur valide.</span><span class="sxs-lookup"><span data-stu-id="537c0-119">When assigning a user tooDropbox for Business, you must select a valid user role.</span></span> <span data-ttu-id="537c0-120">rôle de « Accès par défaut » Hello ne fonctionne pas pour la configuration...</span><span class="sxs-lookup"><span data-stu-id="537c0-120">hello "Default Access" role does not work for provisioning..</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="537c0-121">Activer l’approvisionnement automatique des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="537c0-121">Enable Automated User Provisioning</span></span>

<span data-ttu-id="537c0-122">Cette section vous guide à travers de la connexion de votre tooDropbox Azure AD pour le compte d’utilisateur d’entreprise à l’API de configuration et configurez hello toocreate du service de configuration, de mettre à jour et de désactiver les comptes d’utilisateur affecté dans Dropbox for Business en fonction de l’utilisateur et de groupe affectation dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="537c0-122">This section guides you through connecting your Azure AD tooDropbox for Business's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Dropbox for Business based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="537c0-123">Vous pouvez également choisir tooenabled basé sur SAML Single Sign-On pour Dropbox for Business, en suivant les instructions hello fournies dans [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="537c0-123">You may also choose tooenabled SAML-based Single Sign-On for Dropbox for Business, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="537c0-124">L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que chacune de ces deux fonctionnalités compléte l’autre.</span><span class="sxs-lookup"><span data-stu-id="537c0-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-automatic-user-account-provisioning"></a><span data-ttu-id="537c0-125">tooconfigure compte le provisionnement utilisateur automatique :</span><span class="sxs-lookup"><span data-stu-id="537c0-125">tooconfigure automatic user account provisioning:</span></span>

1. <span data-ttu-id="537c0-126">Bonjour [portail Azure](https://portal.azure.com), parcourir toohello **Azure Active Directory > applications d’entreprise > toutes les applications** section.</span><span class="sxs-lookup"><span data-stu-id="537c0-126">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="537c0-127">Si vous avez déjà configuré Dropbox for Business pour l’authentification unique, recherchez votre instance de Dropbox for Business à l’aide du champ de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="537c0-127">If you have already configured Dropbox for Business for single sign-on, search for your instance of Dropbox for Business using hello search field.</span></span> <span data-ttu-id="537c0-128">Sinon, sélectionnez **ajouter** et recherchez **Dropbox for Business** dans la galerie d’applications hello.</span><span class="sxs-lookup"><span data-stu-id="537c0-128">Otherwise, select **Add** and search for **Dropbox for Business** in hello application gallery.</span></span> <span data-ttu-id="537c0-129">Sélectionnez Dropbox for Business à partir des résultats de recherche hello et ajoutez-le tooyour la liste des applications.</span><span class="sxs-lookup"><span data-stu-id="537c0-129">Select Dropbox for Business from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="537c0-130">Sélectionnez votre instance de Dropbox for Business, puis hello **Provisioning** onglet.</span><span class="sxs-lookup"><span data-stu-id="537c0-130">Select your instance of Dropbox for Business, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="537c0-131">Ensemble hello **Mode d’approvisionnement** trop**automatique**.</span><span class="sxs-lookup"><span data-stu-id="537c0-131">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![approvisionnement](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="537c0-133">Sous hello **informations d’identification administrateur** , cliquez sur **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="537c0-133">Under hello **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="537c0-134">Cela permet d’ouvrir une boîte de dialogue de connexion à Dropbox for Business dans une nouvelle fenêtre de navigateur.</span><span class="sxs-lookup"><span data-stu-id="537c0-134">It opens a Dropbox for Business login dialog in a new browser window.</span></span>

6. <span data-ttu-id="537c0-135">Sur hello **connexion toolink de tooDropbox avec Azure AD** boîte de dialogue de connexion tooyour Dropbox pour le client de l’entreprise.</span><span class="sxs-lookup"><span data-stu-id="537c0-135">On hello **Sign-in tooDropbox toolink with Azure AD** dialog, sign in tooyour Dropbox for Business tenant.</span></span>

     <span data-ttu-id="537c0-136">![Approvisionnement d'utilisateurs](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "Approvisionnement d’utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="537c0-136">![User provisioning](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "User provisioning")</span></span>

7. <span data-ttu-id="537c0-137">Vérifiez que vous aimeriez toogive Azure Active Directory autorisation toomake modifications tooyour Dropbox pour le client de l’entreprise.</span><span class="sxs-lookup"><span data-stu-id="537c0-137">Confirm that you would like toogive Azure Active Directory permission toomake changes tooyour Dropbox for Business tenant.</span></span> <span data-ttu-id="537c0-138">Cliquez sur **Autoriser**.</span><span class="sxs-lookup"><span data-stu-id="537c0-138">Click **Allow**.</span></span>
    
      <span data-ttu-id="537c0-139">![Approvisionnement d'utilisateurs](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "Approvisionnement d’utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="537c0-139">![User provisioning](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "User provisioning")</span></span>

8. <span data-ttu-id="537c0-140">Bonjour portail Azure, cliquez sur **tester la connexion** tooensure Azure AD peut se connecter tooyour Dropbox pour l’application d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="537c0-140">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Dropbox for Business app.</span></span> <span data-ttu-id="537c0-141">Si hello connexion échoue, vérifiez votre Dropbox pour le compte d’entreprise a des autorisations d’administrateur d’équipe et essayez de hello **« Autoriser »** pas à pas.</span><span class="sxs-lookup"><span data-stu-id="537c0-141">If hello connection fails, ensure your Dropbox for Business account has Team Admin permissions and try hello **"Authorize"** step again.</span></span>

9. <span data-ttu-id="537c0-142">Entrez hello adresse de messagerie d’une personne ou un groupe qui doit recevoir des notifications d’erreur approvisionnement hello **courrier électronique de Notification** champ et la case à cocher hello.</span><span class="sxs-lookup"><span data-stu-id="537c0-142">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

10. <span data-ttu-id="537c0-143">Cliquez sur **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="537c0-143">Click **Save.**</span></span>

11. <span data-ttu-id="537c0-144">Sous la section des mappages de hello, sélectionnez **tooDropbox de synchronisation Azure Active Directory Users pour entreprises.**</span><span class="sxs-lookup"><span data-stu-id="537c0-144">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooDropbox for Business.**</span></span>

12. <span data-ttu-id="537c0-145">Bonjour **des mappages d’attributs** section, passez en revue les attributs utilisateur hello qui sont synchronisés à partir de Azure AD tooDropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="537c0-145">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooDropbox for Business.</span></span> <span data-ttu-id="537c0-146">Hello attributs sélectionnés en tant que **correspondance** propriétés sont des comptes d’utilisateur hello toomatch utilisés dans Dropbox for Business pour les opérations de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="537c0-146">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Dropbox for Business for update operations.</span></span> <span data-ttu-id="537c0-147">Sélectionnez toocommit de bouton hello enregistrer toutes les modifications.</span><span class="sxs-lookup"><span data-stu-id="537c0-147">Select hello Save button toocommit any changes.</span></span>

13. <span data-ttu-id="537c0-148">tooenable hello service de configuration d’Azure AD pour Dropbox for Business, modification hello **état d’approvisionnement** trop**sur** Bonjour section de paramètres</span><span class="sxs-lookup"><span data-stu-id="537c0-148">tooenable hello Azure AD provisioning service for Dropbox for Business, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

14. <span data-ttu-id="537c0-149">Cliquez sur **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="537c0-149">Click **Save.**</span></span>

<span data-ttu-id="537c0-150">Il démarre la synchronisation initiale d’utilisateurs et/ou groupes affectés tooDropbox entreprise Bonjour les utilisateurs et la section groupes de hello.</span><span class="sxs-lookup"><span data-stu-id="537c0-150">It starts hello initial synchronization of any users and/or groups assigned tooDropbox for Business in hello Users and Groups section.</span></span> <span data-ttu-id="537c0-151">la synchronisation initiale Hello prend tooperform plus de temps que les synchronisations suivantes, qui se produisent toutes les 20 minutes environ tant que service de hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="537c0-151">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="537c0-152">Vous pouvez utiliser hello **détails de synchronisation** section toomonitor cours et suivre des rapports d’activité tooprovisioning des liens, qui décrivent toutes les actions effectuées par hello mise en service du service sur votre Dropbox pour l’application d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="537c0-152">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Dropbox for Business app.</span></span>

<span data-ttu-id="537c0-153">Vous pouvez à présent créer un compte de test.</span><span class="sxs-lookup"><span data-stu-id="537c0-153">You can now create a test account.</span></span> <span data-ttu-id="537c0-154">Attendez que les minutes too20 tooverify hello compte a été synchronisé tooDropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="537c0-154">Wait for up too20 minutes tooverify that hello account has been synchronized tooDropbox for Business.</span></span>

<span data-ttu-id="537c0-155">Si le cycle d'approvisionnement d'utilisateur a abouti, l'état associé est indiqué.</span><span class="sxs-lookup"><span data-stu-id="537c0-155">A successfully completed user provisioning cycle is indicated by a related status.</span></span>

<span data-ttu-id="537c0-156">![Affecter des utilisateurs](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "Affecter des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="537c0-156">![Assign users](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "Assign users")</span></span>


## <a name="additional-resources"></a><span data-ttu-id="537c0-157">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="537c0-157">Additional resources</span></span>

* [<span data-ttu-id="537c0-158">Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise</span><span class="sxs-lookup"><span data-stu-id="537c0-158">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="537c0-159">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="537c0-159">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="537c0-160">Configurer l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="537c0-160">Configure Single Sign-on</span></span>](active-directory-saas-dropboxforbusiness-tutorial.md)