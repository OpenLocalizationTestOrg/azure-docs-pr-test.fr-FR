---
title: "Didacticiel : Configuration de Slack pour l’approvisionnement automatique d’utilisateurs avec Azure Active Directory | Microsoft Docs"
description: "Découvrez comment tooconfigure Azure Active Directory tooautomatically disposition et la disposition de l’utilisateur des comptes tooSlack."
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
ms.openlocfilehash: d0a565bbe0bd7e229b9dd99b1ebbaf67d93a2206
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-slack-for-automatic-user-provisioning"></a><span data-ttu-id="8b6cd-103">Didacticiel : Configuration de Slack pour l’approvisionnement automatique d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="8b6cd-103">Tutorial: Configuring Slack for Automatic User Provisioning</span></span>


<span data-ttu-id="8b6cd-104">objectif de ce didacticiel Hello est tooshow vous hello étapes que vous devez tooperform dans la marge et Azure AD tooautomatically approvisionner et configurer des comptes d’utilisateur à partir d’Azure AD tooSlack.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Slack and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooSlack.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="8b6cd-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8b6cd-105">Prerequisites</span></span>

<span data-ttu-id="8b6cd-106">scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="8b6cd-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="8b6cd-107">Un client Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8b6cd-107">An Azure Active Active directory tenant</span></span>
*   <span data-ttu-id="8b6cd-108">Une marge de locataire avec hello [Plus plan](https://aadsyncfabric.slack.com/pricing) ou mieux activé</span><span class="sxs-lookup"><span data-stu-id="8b6cd-108">A Slack tenant with hello [Plus plan](https://aadsyncfabric.slack.com/pricing) or better enabled</span></span> 
*   <span data-ttu-id="8b6cd-109">Un compte d’utilisateur dans Slack avec les autorisations d’administrateur d’équipe</span><span class="sxs-lookup"><span data-stu-id="8b6cd-109">A user account in Slack with Team Admin permissions</span></span> 

<span data-ttu-id="8b6cd-110">Remarque : hello mise en service d’intégration de Azure AD s’appuie sur hello [Slack SCIM API](https://api.slack.com/scim) qui est équipes tooSlack disponible sur hello Plus plan ou supérieures.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-110">Note: hello Azure AD provisioning integration relies on hello [Slack SCIM API](https://api.slack.com/scim) which is available tooSlack teams on hello Plus plan or better.</span></span>

## <a name="assigning-users-tooslack"></a><span data-ttu-id="8b6cd-111">Affectation d’utilisateurs tooSlack</span><span class="sxs-lookup"><span data-stu-id="8b6cd-111">Assigning users tooSlack</span></span>

<span data-ttu-id="8b6cd-112">Azure Active Directory utilise un concept appelé toodetermine « affectations » les utilisateurs qui doivent recevoir l’accès tooselected applications.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="8b6cd-113">Dans le contexte de hello de configuration de compte automatique d’utilisateurs, seuls les utilisateurs de hello et les groupes qui ont été « affectés » application tooan dans Azure AD seront synchronisés.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="8b6cd-114">Avant de configurer et de l’activation de hello service de configuration, vous devez toodecide quels utilisateurs ou des groupes dans Azure AD représentent hello utilisateurs qui doivent accéder à application de marge tooyour.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-114">Before configuring and enabling hello provisioning service, you will need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Slack app.</span></span> <span data-ttu-id="8b6cd-115">Après choisi, vous pouvez attribuer à ces applications de marge tooyour utilisateurs en suivant les instructions hello ici :</span><span class="sxs-lookup"><span data-stu-id="8b6cd-115">Once decided, you can assign these users tooyour Slack app by following hello instructions here:</span></span>

[<span data-ttu-id="8b6cd-116">Affecter une application d’entreprise tooan utilisateur ou un groupe</span><span class="sxs-lookup"><span data-stu-id="8b6cd-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-tooslack"></a><span data-ttu-id="8b6cd-117">Conseils importants pour l’affectation d’utilisateurs tooSlack</span><span class="sxs-lookup"><span data-stu-id="8b6cd-117">Important tips for assigning users tooSlack</span></span>

*   <span data-ttu-id="8b6cd-118">Il est recommandé qu’un seul utilisateur Azure AD avoir tooSlack tootest hello est mise en service de configuration.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-118">It is recommended that a single Azure AD user be assigned tooSlack tootest hello provisioning configuration.</span></span> <span data-ttu-id="8b6cd-119">Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="8b6cd-120">Lorsque vous affectez un tooSlack d’utilisateur, vous devez sélectionner hello **utilisateur** ou le rôle « Groupe » dans la boîte de dialogue attribution hello.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-120">When assigning a user tooSlack, you must select hello **User** or "Group" role in hello assignment dialog.</span></span> <span data-ttu-id="8b6cd-121">rôle de « Accès par défaut » Hello ne fonctionne pas pour la configuration.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-121">hello "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-tooslack"></a><span data-ttu-id="8b6cd-122">Configuration tooSlack de configuration de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="8b6cd-122">Configuring user provisioning tooSlack</span></span> 

<span data-ttu-id="8b6cd-123">Cette section vous guide à travers de la connexion du compte d’utilisateur de votre tooSlack AD Azure API de configuration et configurez hello toocreate du service de configuration, de mettre à jour et de désactiver les comptes d’utilisateur affecté dans la marge en fonction de l’affectation d’utilisateurs et de groupes dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-123">This section guides you through connecting your Azure AD tooSlack's user account provisioning API, and configuring hello provisioning service toocreate, update and disable assigned user accounts in Slack based on user and group assignment in Azure AD.</span></span>

<span data-ttu-id="8b6cd-124">**Conseil :** vous pouvez également choisir tooenabled basé sur SAML Single Sign-On pour Slack, suivant les instructions de hello fournies dans (portail Azure) [https://portal.azure.com].</span><span class="sxs-lookup"><span data-stu-id="8b6cd-124">**Tip:** You may also choose tooenabled SAML-based Single Sign-On for Slack, following hello instructions provided in (Azure portal)[https://portal.azure.com].</span></span> <span data-ttu-id="8b6cd-125">L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que chacune de ces deux fonctionnalités compléte l’autre.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="tooconfigure-automatic-user-account-provisioning-tooslack-in-azure-ad"></a><span data-ttu-id="8b6cd-126">compte d’utilisateur automatique de tooconfigure tooSlack de configuration dans Azure AD :</span><span class="sxs-lookup"><span data-stu-id="8b6cd-126">tooconfigure automatic user account provisioning tooSlack in Azure AD:</span></span>


1)  <span data-ttu-id="8b6cd-127">Bonjour [portail Azure](https://portal.azure.com), parcourir toohello **Azure Active Directory > applications d’entreprise > toutes les applications** section.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2) <span data-ttu-id="8b6cd-128">Si vous avez déjà configuré la marge pour l’authentification unique, recherchez votre instance de la marge à l’aide du champ de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-128">If you have already configured Slack for single sign-on, search for your instance of Slack using hello search field.</span></span> <span data-ttu-id="8b6cd-129">Sinon, sélectionnez **ajouter** et recherchez **Slack** dans la galerie d’applications hello.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-129">Otherwise, select **Add** and search for **Slack** in hello application gallery.</span></span> <span data-ttu-id="8b6cd-130">Sélectionnez la marge à partir des résultats de recherche hello et l’ajouter tooyour la liste des applications.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-130">Select Slack from hello search results, and add it tooyour list of applications.</span></span>

3)  <span data-ttu-id="8b6cd-131">Sélectionnez votre instance de marge, puis hello **Provisioning** onglet.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-131">Select your instance of Slack, then select hello **Provisioning** tab.</span></span>

4)  <span data-ttu-id="8b6cd-132">Ensemble hello **Mode d’approvisionnement** trop**automatique**.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-132">Set hello **Provisioning Mode** too**Automatic**.</span></span>

![Approvisionnement Slack](./media/active-directory-saas-slack-provisioning-tutorial/Slack1.PNG)

5)  <span data-ttu-id="8b6cd-134">Sous hello **informations d’identification administrateur** , cliquez sur **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-134">Under hello **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="8b6cd-135">Une boîte de dialogue d’autorisation Slack s’ouvre dans une nouvelle fenêtre de navigateur.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-135">This opens a Slack authorization dialog in a new browser window.</span></span> 

6) <span data-ttu-id="8b6cd-136">Dans la nouvelle fenêtre de hello, connectez-vous à Slack à l’aide de votre compte d’administrateur d’équipe.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-136">In hello new window, sign into Slack using your Team Admin account.</span></span> <span data-ttu-id="8b6cd-137">hello résultant d’autorisation boîte de dialogue, sélectionnez hello Slack équipe que vous souhaitez la préparation de tooenable, puis sélectionnez **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-137">in hello resulting authorization dialog, select hello Slack team that you want tooenable provisioning for, and then select **Authorize**.</span></span> <span data-ttu-id="8b6cd-138">Une fois terminée, retournez toohello toocomplete portail Azure hello est mise en service de configuration.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-138">Once completed, return toohello Azure portal toocomplete hello provisioning configuration.</span></span>

![Boîte de dialogue d’autorisation](./media/active-directory-saas-slack-provisioning-tutorial/Slack3.PNG)

7) <span data-ttu-id="8b6cd-140">Bonjour portail Azure, cliquez sur **tester la connexion** tooensure AD Azure peut se connecter à application de marge tooyour.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-140">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Slack app.</span></span> <span data-ttu-id="8b6cd-141">Si hello connexion échoue, assurez-vous que votre compte Slack dispose d’autorisations d’administrateur d’équipe et recommencez hello à nouveau l’étape « Autoriser ».</span><span class="sxs-lookup"><span data-stu-id="8b6cd-141">If hello connection fails, ensure your Slack account has Team Admin permissions and try hello "Authorize" step again.</span></span>

8) <span data-ttu-id="8b6cd-142">Entrez hello adresse de messagerie d’une personne ou un groupe qui doit recevoir des notifications d’erreur approvisionnement hello **courrier électronique de Notification** champ et la case à cocher hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-142">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox below.</span></span>

9) <span data-ttu-id="8b6cd-143">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-143">Click **Save**.</span></span> 

10) <span data-ttu-id="8b6cd-144">Sous la section des mappages de hello, sélectionnez **tooSlack de synchronisation Azure Active Directory Users**.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-144">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooSlack**.</span></span>

11) <span data-ttu-id="8b6cd-145">Bonjour **des mappages d’attributs** section, passez en revue les attributs utilisateur hello qui seront synchronisés à partir d’Azure AD tooSlack.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-145">In hello **Attribute Mappings** section, review hello user attributes that will be synchronized from Azure AD tooSlack.</span></span> <span data-ttu-id="8b6cd-146">Notez que hello attributs sélectionnés en tant que **correspondance** propriétés se trouvent les comptes d’utilisateur hello toomatch utilisé dans la marge pour les opérations de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-146">Note that hello attributes selected as **Matching** properties will be used toomatch hello user accounts in Slack for update operations.</span></span> <span data-ttu-id="8b6cd-147">Sélectionnez toocommit de bouton hello enregistrer toutes les modifications.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-147">Select hello Save button toocommit any changes.</span></span>

12) <span data-ttu-id="8b6cd-148">tooenable hello service de configuration d’Azure AD pour Slack, modification hello **état d’approvisionnement** trop**sur** Bonjour **paramètres** section</span><span class="sxs-lookup"><span data-stu-id="8b6cd-148">tooenable hello Azure AD provisioning service for Slack, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

13) <span data-ttu-id="8b6cd-149">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-149">Click **Save**.</span></span> 

<span data-ttu-id="8b6cd-150">Ceci démarrera la synchronisation initiale d’utilisateurs et/ou groupes affectés tooSlack Bonjour les utilisateurs et la section groupes de hello.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-150">This will start hello initial synchronization of any users and/or groups assigned tooSlack in hello Users and Groups section.</span></span> <span data-ttu-id="8b6cd-151">Notez que la synchronisation initiale hello a tooperform plus de temps que les synchronisations suivantes, qui se produisent toutes les 10 minutes environ, tant que service de hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-151">Note that hello initial sync will take longer tooperform than subsequent syncs, which occur approximately every 10 minutes as long as hello service is running.</span></span> <span data-ttu-id="8b6cd-152">Vous pouvez utiliser hello **détails de synchronisation** section toomonitor cours et suivre des rapports d’activité tooprovisioning des liens, qui décrivent toutes les actions effectuées par hello mise en service du service dans votre application de marge.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-152">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Slack app.</span></span>

## <a name="optional-configuring-group-object-provisioning-tooslack"></a><span data-ttu-id="8b6cd-153">[Facultatif] Configuration d’objet groupe tooSlack de configuration</span><span class="sxs-lookup"><span data-stu-id="8b6cd-153">[Optional] Configuring group object provisioning tooSlack</span></span> 

<span data-ttu-id="8b6cd-154">Si vous le souhaitez, vous pouvez activer l’approvisionnement des objets de groupe à partir d’Azure AD tooSlack hello.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-154">Optionally, you can enable hello provisioning of group objects from Azure AD tooSlack.</span></span> <span data-ttu-id="8b6cd-155">Cela est différent de « affectation de groupes d’utilisateurs », dans cet objet de groupe réel hello en outre tooits membres seront répliquées à partir d’Azure AD tooSlack.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-155">This is different from "assigning groups of users", in that hello actual group object in addition tooits members will be replicated from Azure AD tooSlack.</span></span> <span data-ttu-id="8b6cd-156">Par exemple, si vous avez un groupe nommé « Mon groupe » dans Azure AD, un groupe identique nommé « Mon groupe » est créé dans Slack.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-156">For example, if you have a group named "My Group" in Azure AD, an identitical group named "My Group" will be created inside Slack.</span></span>

### <a name="tooenable-provisioning-of-group-objects"></a><span data-ttu-id="8b6cd-157">tooenable mise en service des objets de groupe :</span><span class="sxs-lookup"><span data-stu-id="8b6cd-157">tooenable provisioning of group objects:</span></span>

1) <span data-ttu-id="8b6cd-158">Sous la section des mappages de hello, sélectionnez **tooSlack de synchroniser les groupes Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-158">Under hello Mappings section, select **Synchronize Azure Active Directory Groups tooSlack**.</span></span>

2) <span data-ttu-id="8b6cd-159">Dans le panneau de mappage d’attribut hello, définissez activé tooYes.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-159">In hello Attribute Mapping blade, set Enabled tooYes.</span></span>

3) <span data-ttu-id="8b6cd-160">Bonjour **des mappages d’attributs** section, passez en revue les attributs de groupe hello qui seront synchronisés à partir d’Azure AD tooSlack.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-160">In hello **Attribute Mappings** section, review hello group attributes that will be synchronized from Azure AD tooSlack.</span></span> <span data-ttu-id="8b6cd-161">Notez que hello attributs sélectionnés en tant que **correspondance** propriétés seront des groupes de hello toomatch utilisé dans la marge pour les opérations de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-161">Note that hello attributes selected as **Matching** properties will be used toomatch hello groups in Slack for update operations.</span></span> 

4) <span data-ttu-id="8b6cd-162">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-162">Click **Save**.</span></span>

<span data-ttu-id="8b6cd-163">Ce résultat dans n’importe quel tooSlack d’objets attribués groupe Bonjour **utilisateurs et groupes** section complètement synchronisés à partir d’Azure AD tooSlack.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-163">This result in any group objects assigned tooSlack in hello **Users and Groups** section being fully synchronized from Azure AD tooSlack.</span></span> <span data-ttu-id="8b6cd-164">Vous pouvez utiliser hello **détails de synchronisation** section toomonitor cours et suivre des rapports d’activité tooprovisioning des liens, qui décrivent toutes les actions effectuées par hello mise en service du service dans votre application de marge.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-164">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Slack app.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="8b6cd-165">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="8b6cd-165">Additional Resources</span></span>

* [<span data-ttu-id="8b6cd-166">Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise</span><span class="sxs-lookup"><span data-stu-id="8b6cd-166">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="8b6cd-167">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="8b6cd-167">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
