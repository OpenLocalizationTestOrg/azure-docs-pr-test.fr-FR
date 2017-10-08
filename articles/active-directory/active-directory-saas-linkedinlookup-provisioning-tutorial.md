---
title: "Didacticiel : Configuration de LinkedIn Lookup pour l’approvisionnement automatique d’utilisateurs avec Azure Active Directory | Microsoft Docs"
description: "Découvrez comment tooconfigure Azure Active Directory tooautomatically disposition et la disposition de l’utilisateur des comptes tooLinkedIn recherche."
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
ms.date: 04/15/2017
ms.author: asmalser-msft
ms.openlocfilehash: 3e41abb8af00715f70e5a14d9d26ff600c10f492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-linkedin-lookup-for-automatic-user-provisioning"></a><span data-ttu-id="4e92d-103">Didacticiel : Configuration de LinkedIn Lookup pour approvisionner automatiquement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="4e92d-103">Tutorial: Configuring LinkedIn Lookup for Automatic User Provisioning</span></span>


<span data-ttu-id="4e92d-104">objectif Hello de ce didacticiel est tooshow vous hello étapes que vous devez tooperform dans recherche de LinkedIn et Azure AD tooautomatically approvisionner et configurer des comptes d’utilisateur à partir d’Azure AD tooLinkedIn recherche.</span><span class="sxs-lookup"><span data-stu-id="4e92d-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in LinkedIn Lookup and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooLinkedIn Lookup.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="4e92d-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4e92d-105">Prerequisites</span></span>

<span data-ttu-id="4e92d-106">scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="4e92d-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="4e92d-107">Un client Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4e92d-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="4e92d-108">Un locataire LinkedIn Lookup</span><span class="sxs-lookup"><span data-stu-id="4e92d-108">A LinkedIn Lookup tenant</span></span> 
*   <span data-ttu-id="4e92d-109">Un compte d’administrateur dans la recherche de LinkedIn avec accès toohello LinkedIn centre des comptes</span><span class="sxs-lookup"><span data-stu-id="4e92d-109">An administrator account in LinkedIn Lookup with access toohello LinkedIn Account Center</span></span>

> [!NOTE]
> <span data-ttu-id="4e92d-110">Azure Active Directory s’intègre à la recherche de LinkedIn à l’aide de hello [SCIM](http://www.simplecloud.info/) protocole.</span><span class="sxs-lookup"><span data-stu-id="4e92d-110">Azure Active Directory integrates with LinkedIn Lookup using hello [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-toolinkedin-lookup"></a><span data-ttu-id="4e92d-111">Affectation d’utilisateurs tooLinkedIn recherche</span><span class="sxs-lookup"><span data-stu-id="4e92d-111">Assigning users tooLinkedIn Lookup</span></span>

<span data-ttu-id="4e92d-112">Azure Active Directory utilise un concept appelé toodetermine « affectations » les utilisateurs qui doivent recevoir l’accès tooselected applications.</span><span class="sxs-lookup"><span data-stu-id="4e92d-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="4e92d-113">Dans le contexte de hello de configuration de compte automatique d’utilisateurs, seuls les utilisateurs de hello et les groupes qui ont été « affectés » application tooan dans Azure AD seront synchronisés.</span><span class="sxs-lookup"><span data-stu-id="4e92d-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="4e92d-114">Avant de configurer et de l’activation de hello service de configuration, vous devez toodecide quels utilisateurs ou des groupes dans Azure AD représentent des utilisateurs ayant besoin d’accès tooLinkedIn recherche hello.</span><span class="sxs-lookup"><span data-stu-id="4e92d-114">Before configuring and enabling hello provisioning service, you will need toodecide what users and/or groups in Azure AD represent hello users who need access tooLinkedIn Lookup.</span></span> <span data-ttu-id="4e92d-115">Une fois choisi, vous pouvez attribuer ces tooLinkedIn utilisateurs recherche en suivant les instructions hello ici :</span><span class="sxs-lookup"><span data-stu-id="4e92d-115">Once decided, you can assign these users tooLinkedIn Lookup by following hello instructions here:</span></span>

[<span data-ttu-id="4e92d-116">Affecter une application d’entreprise tooan utilisateur ou un groupe</span><span class="sxs-lookup"><span data-stu-id="4e92d-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toolinkedin-lookup"></a><span data-ttu-id="4e92d-117">Conseils importants pour l’affectation d’utilisateurs tooLinkedIn recherche</span><span class="sxs-lookup"><span data-stu-id="4e92d-117">Important tips for assigning users tooLinkedIn Lookup</span></span>

*   <span data-ttu-id="4e92d-118">Il est recommandé qu’un seul utilisateur Azure AD avoir hello de tootest tooLinkedIn recherche mise en service de configuration.</span><span class="sxs-lookup"><span data-stu-id="4e92d-118">It is recommended that a single Azure AD user be assigned tooLinkedIn Lookup tootest hello provisioning configuration.</span></span> <span data-ttu-id="4e92d-119">Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="4e92d-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="4e92d-120">Lorsque vous affectez un tooLinkedIn utilisateur recherche, vous devez sélectionner hello **utilisateur** rôle dans la boîte de dialogue attribution hello.</span><span class="sxs-lookup"><span data-stu-id="4e92d-120">When assigning a user tooLinkedIn Lookup, you must select hello **User** role in hello assignment dialog.</span></span> <span data-ttu-id="4e92d-121">rôle de « Accès par défaut » Hello ne fonctionne pas pour la configuration.</span><span class="sxs-lookup"><span data-stu-id="4e92d-121">hello "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-toolinkedin-lookup"></a><span data-ttu-id="4e92d-122">Configuration tooLinkedIn recherche de configuration de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="4e92d-122">Configuring user provisioning tooLinkedIn Lookup</span></span>

<span data-ttu-id="4e92d-123">Cette section vous guide à travers de la connexion du compte d’utilisateur de votre recherche tooLinkedIn Azure AD SCIM API de configuration et configurez hello toocreate du service de configuration, de mettre à jour et de désactiver l’utilisateur affecté comptes dans la recherche de LinkedIn basés sur des utilisateurs et de groupes affectation dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e92d-123">This section guides you through connecting your Azure AD tooLinkedIn Lookup's SCIM user account provisioning API, and configuring hello provisioning service toocreate, update and disable assigned user accounts in LinkedIn Lookup based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="4e92d-124">Vous pouvez également choisir tooenabled basé sur SAML Single Sign-On pour la recherche LinkedIn, suivant les instructions hello fournies dans [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4e92d-124">You may also choose tooenabled SAML-based Single Sign-On for LinkedIn Lookup, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4e92d-125">L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que ces deux fonctionnalités se complètent.</span><span class="sxs-lookup"><span data-stu-id="4e92d-125">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span>


### <a name="tooconfigure-automatic-user-account-provisioning-toolinkedin-lookup-in-azure-ad"></a><span data-ttu-id="4e92d-126">compte d’utilisateur automatique de tooconfigure tooLinkedIn recherche de configuration dans Azure AD :</span><span class="sxs-lookup"><span data-stu-id="4e92d-126">tooconfigure automatic user account provisioning tooLinkedIn Lookup in Azure AD:</span></span>


<span data-ttu-id="4e92d-127">première étape de Hello est tooretrieve votre jeton d’accès LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="4e92d-127">hello first step is tooretrieve your LinkedIn access token.</span></span> <span data-ttu-id="4e92d-128">Si vous êtes administrateur d’entreprise, vous pouvez approvisionner vous-même un jeton d’accès.</span><span class="sxs-lookup"><span data-stu-id="4e92d-128">If you are an Enterprise administrator, you can self-provision an access token.</span></span> <span data-ttu-id="4e92d-129">Dans votre centre de gestion, accédez trop**paramètres &gt; paramètres globaux** et ouvrez hello **SCIM le programme d’installation** Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="4e92d-129">In your account center, go too**Settings &gt; Global Settings** and open hello **SCIM Setup** panel.</span></span>

> [!NOTE]
> <span data-ttu-id="4e92d-130">Si vous accédez au centre des comptes hello directement plutôt que via un lien, vous pouvez également accéder à l’aide de hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="4e92d-130">If you are accessing hello account center directly rather than through a link, you can reach it using hello following steps.</span></span>

1)  <span data-ttu-id="4e92d-131">Connectez-vous tooAccount Center.</span><span class="sxs-lookup"><span data-stu-id="4e92d-131">Sign in tooAccount Center.</span></span>

2)  <span data-ttu-id="4e92d-132">Sélectionnez **Administrateur &gt; Paramètres d’administration**.</span><span class="sxs-lookup"><span data-stu-id="4e92d-132">Select **Admin &gt; Admin Settings** .</span></span>

3)  <span data-ttu-id="4e92d-133">Cliquez sur **avancé des intégrations** sur le volet gauche hello.</span><span class="sxs-lookup"><span data-stu-id="4e92d-133">Click **Advanced Integrations** on hello left sidebar.</span></span> <span data-ttu-id="4e92d-134">Vous êtes dirigé toohello centre des comptes.</span><span class="sxs-lookup"><span data-stu-id="4e92d-134">You are directed toohello account center.</span></span>

4)  <span data-ttu-id="4e92d-135">Cliquez sur **+ ajouter une nouvelle configuration de SCIM** et suivez la procédure de hello en remplissant chaque champ.</span><span class="sxs-lookup"><span data-stu-id="4e92d-135">Click **+ Add new SCIM configuration** and follow hello procedure by filling in each field.</span></span>

> <span data-ttu-id="4e92d-136">Si l’affectation automatique de licences n’est pas activée, cela signifie que seules les données utilisateur sont synchronisées.</span><span class="sxs-lookup"><span data-stu-id="4e92d-136">When auto­assign licenses is not enabled, it means that only user data is synced.</span></span>

![Approvisionnement LinkedIn Lookup](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_1.PNG)

> <span data-ttu-id="4e92d-138">Lorsque l’attribution autolicense est activée, vous devez toonote l’instance d’application et le type de licence.</span><span class="sxs-lookup"><span data-stu-id="4e92d-138">When auto­license assignment is enabled, you need toonote the application instance and license type.</span></span> <span data-ttu-id="4e92d-139">Les licences sont attribuées sur un premier arrivé, traiter tout d’abord base jusqu'à ce que toutes les licences hello sont effectuées.</span><span class="sxs-lookup"><span data-stu-id="4e92d-139">Licenses are assigned on a first come, first serve basis until all hello licenses are taken.</span></span>

![Approvisionnement LinkedIn Lookup](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_2.PNG)

5)  <span data-ttu-id="4e92d-141">Cliquez sur **Générer un jeton**.</span><span class="sxs-lookup"><span data-stu-id="4e92d-141">Click **Generate token**.</span></span> <span data-ttu-id="4e92d-142">Vous devez voir votre affichage de jeton d’accès sous hello **jeton d’accès** champ.</span><span class="sxs-lookup"><span data-stu-id="4e92d-142">You should see your access token display under hello **Access token** field.</span></span>

6)  <span data-ttu-id="4e92d-143">Enregistrez votre accès au jeton tooyour Presse-papiers ou un ordinateur avant de quitter la page de hello.</span><span class="sxs-lookup"><span data-stu-id="4e92d-143">Save your access token tooyour clipboard or computer before leaving hello page.</span></span>

7) <span data-ttu-id="4e92d-144">Ensuite, connectez-vous à toohello [portail Azure](https://portal.azure.com), puis accédez toohello **Azure Active Directory > applications d’entreprise > toutes les applications** section.</span><span class="sxs-lookup"><span data-stu-id="4e92d-144">Next, sign in toohello [Azure portal](https://portal.azure.com), and browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

8) <span data-ttu-id="4e92d-145">Si vous avez déjà configuré LinkedIn recherche pour l’authentification unique, recherchez votre instance de recherche LinkedIn à l’aide du champ de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="4e92d-145">If you have already configured LinkedIn Lookup for single sign-on, search for your instance of LinkedIn Lookup using hello search field.</span></span> <span data-ttu-id="4e92d-146">Sinon, sélectionnez **ajouter** et recherchez **LinkedIn recherche** dans la galerie d’applications hello.</span><span class="sxs-lookup"><span data-stu-id="4e92d-146">Otherwise, select **Add** and search for **LinkedIn Lookup** in hello application gallery.</span></span> <span data-ttu-id="4e92d-147">Sélectionnez LinkedIn recherche à partir des résultats de recherche hello et ajoutez-le tooyour la liste des applications.</span><span class="sxs-lookup"><span data-stu-id="4e92d-147">Select LinkedIn Lookup from hello search results, and add it tooyour list of applications.</span></span>

9)  <span data-ttu-id="4e92d-148">Sélectionnez votre instance de la recherche LinkedIn, puis hello **Provisioning** onglet.</span><span class="sxs-lookup"><span data-stu-id="4e92d-148">Select your instance of LinkedIn Lookup, then select hello **Provisioning** tab.</span></span>

10) <span data-ttu-id="4e92d-149">Ensemble hello **Mode d’approvisionnement** trop**automatique**.</span><span class="sxs-lookup"><span data-stu-id="4e92d-149">Set hello **Provisioning Mode** too**Automatic**.</span></span>

![Approvisionnement LinkedIn Lookup](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_3.PNG)

11)  <span data-ttu-id="4e92d-151">Renseignez hello suivant champs sous **informations d’identification administrateur** :</span><span class="sxs-lookup"><span data-stu-id="4e92d-151">Fill in hello following fields under **Admin Credentials** :</span></span>

* <span data-ttu-id="4e92d-152">Bonjour **URL de client** , saisissez https://api.linkedin.com.</span><span class="sxs-lookup"><span data-stu-id="4e92d-152">In hello **Tenant URL** field, enter https://api.linkedin.com.</span></span>

* <span data-ttu-id="4e92d-153">Bonjour **Secret jeton** , indiquez le jeton d’accès hello générés à l’étape 1 et cliquez sur **tester la connexion** .</span><span class="sxs-lookup"><span data-stu-id="4e92d-153">In hello **Secret Token** field, enter hello access token you generated in step 1 and click **Test Connection** .</span></span>

* <span data-ttu-id="4e92d-154">Vous devez voir une notification de réussite supérieurdroit côté hello de votre portail.</span><span class="sxs-lookup"><span data-stu-id="4e92d-154">You should see a success notification on hello upper­right side of   your portal.</span></span>

12) <span data-ttu-id="4e92d-155">Entrez hello adresse de messagerie d’une personne ou un groupe qui doit recevoir des notifications d’erreur approvisionnement hello **courrier électronique de Notification** champ et la case à cocher hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="4e92d-155">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox below.</span></span>

13) <span data-ttu-id="4e92d-156">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="4e92d-156">Click **Save**.</span></span> 

14) <span data-ttu-id="4e92d-157">Bonjour **des mappages d’attributs** section, passez en revue les attributs d’utilisateur et groupe hello qui seront synchronisés à partir d’Azure AD tooLinkedIn recherche.</span><span class="sxs-lookup"><span data-stu-id="4e92d-157">In hello **Attribute Mappings** section, review hello user and group attributes that will be synchronized from Azure AD tooLinkedIn Lookup.</span></span> <span data-ttu-id="4e92d-158">Notez que hello attributs sélectionnés en tant que **correspondance** propriétés seront utilisées toomatch hello des comptes d’utilisateur et les groupes dans LinkedIn recherche pour les opérations de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="4e92d-158">Note that hello attributes selected as **Matching** properties will be used toomatch hello user accounts and groups in LinkedIn Lookup for update operations.</span></span> <span data-ttu-id="4e92d-159">Sélectionnez toocommit de bouton hello enregistrer toutes les modifications.</span><span class="sxs-lookup"><span data-stu-id="4e92d-159">Select hello Save button toocommit any changes.</span></span>

![Approvisionnement LinkedIn Lookup](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_4.PNG)

15) <span data-ttu-id="4e92d-161">tooenable hello service de configuration d’Azure AD pour la recherche LinkedIn, modification hello **état d’approvisionnement** trop**sur** Bonjour **paramètres** section</span><span class="sxs-lookup"><span data-stu-id="4e92d-161">tooenable hello Azure AD provisioning service for LinkedIn Lookup, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

16) <span data-ttu-id="4e92d-162">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="4e92d-162">Click **Save**.</span></span> 

<span data-ttu-id="4e92d-163">Cela permet de démarrer la synchronisation initiale hello de tous les utilisateurs et/ou groupes affectés tooLinkedIn recherche dans la section utilisateurs et groupes de hello.</span><span class="sxs-lookup"><span data-stu-id="4e92d-163">This will start hello initial synchronization of any users and/or groups assigned tooLinkedIn Lookup in hello Users and Groups section.</span></span> <span data-ttu-id="4e92d-164">Notez que la synchronisation initiale hello a tooperform plus de temps que les synchronisations suivantes, qui se produisent toutes les 20 minutes environ tant que service de hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="4e92d-164">Note that hello initial sync will take longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="4e92d-165">Vous pouvez utiliser hello **détails de synchronisation** section toomonitor cours et suivre des rapports d’activité tooprovisioning des liens, qui décrivent toutes les actions effectuées par hello mise en service du service dans votre application de recherche de LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="4e92d-165">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your LinkedIn Lookup app.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="4e92d-166">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="4e92d-166">Additional Resources</span></span>

* [<span data-ttu-id="4e92d-167">Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise</span><span class="sxs-lookup"><span data-stu-id="4e92d-167">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="4e92d-168">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="4e92d-168">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
