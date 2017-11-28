---
title: "Didacticiel : configuration de Google Apps pour l’approvisionnement automatique d’utilisateurs dans Azure | Documents Microsoft"
description: "Découvrez comment tooautomatically approvisionner et configurer des comptes d’utilisateurs Azure AD tooGoogle applications."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6dbd50b5-589f-4132-b9eb-a53a318a64e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: d1fa8449bd6013d1627b3552aaa19db1c0f4f46f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-google-apps-for-automatic-user-provisioning"></a><span data-ttu-id="ee70c-103">Didacticiel : configuration de Google Apps pour approvisionner automatiquement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="ee70c-103">Tutorial: Configuring Google Apps for automatic user provisioning</span></span>

<span data-ttu-id="ee70c-104">objectif Hello de ce didacticiel est tooshow que vous hello étapes, vous devez tooperform dans Google Apps et Azure AD fourniture de tooautomatically et annuler la configuration des comptes d’utilisateur à partir d’Azure AD tooGoogle applications.</span><span class="sxs-lookup"><span data-stu-id="ee70c-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Google Apps and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooGoogle Apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ee70c-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ee70c-105">Prerequisites</span></span>

<span data-ttu-id="ee70c-106">scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ee70c-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="ee70c-107">Un locataire Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ee70c-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="ee70c-108">Vous devez avoir un client valide pour Google Apps pour Travailler ou Google Apps pour l’Éducation.</span><span class="sxs-lookup"><span data-stu-id="ee70c-108">You must have a valid tenant for Google Apps for Work or Google Apps for Education.</span></span> <span data-ttu-id="ee70c-109">Vous pouvez utiliser un compte d’essai gratuit pour chaque service.</span><span class="sxs-lookup"><span data-stu-id="ee70c-109">You may use a free trial account for either service.</span></span>
*   <span data-ttu-id="ee70c-110">Un compte utilisateur dans Google Apps avec les autorisations d’administrateur d’équipe.</span><span class="sxs-lookup"><span data-stu-id="ee70c-110">A user account in Google Apps with Team Admin permissions.</span></span>

## <a name="assigning-users-toogoogle-apps"></a><span data-ttu-id="ee70c-111">Affectation d’utilisateurs tooGoogle applications</span><span class="sxs-lookup"><span data-stu-id="ee70c-111">Assigning users tooGoogle Apps</span></span>

<span data-ttu-id="ee70c-112">Azure Active Directory utilise un concept appelé toodetermine « affectations » les utilisateurs qui doivent recevoir l’accès tooselected applications.</span><span class="sxs-lookup"><span data-stu-id="ee70c-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="ee70c-113">Dans le contexte de hello de configuration de compte automatique d’utilisateurs, seuls les utilisateurs de hello et les groupes qui ont été « affectés » application tooan dans Azure AD est synchronisé.</span><span class="sxs-lookup"><span data-stu-id="ee70c-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="ee70c-114">Avant de configurer et de l’activation de hello service de configuration, vous devez toodecide quels utilisateurs ou des groupes dans Azure AD qui représentent des utilisateurs qui doivent accéder aux applications de Google Apps tooyour hello.</span><span class="sxs-lookup"><span data-stu-id="ee70c-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Google Apps app.</span></span> <span data-ttu-id="ee70c-115">Une fois choisi, vous pouvez attribuer ces applications de Google Apps tooyour les utilisateurs en suivant les instructions hello ici : [affecter une application d’entreprise tooan utilisateur ou un groupe](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)</span><span class="sxs-lookup"><span data-stu-id="ee70c-115">Once decided, you can assign these users tooyour Google Apps app by following hello instructions here: [Assign a user or group tooan enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)</span></span>

> [!IMPORTANT]
>*   <span data-ttu-id="ee70c-116">Il est recommandé qu’un seul utilisateur Azure AD avoir hello de tootest tooGoogle applications service de la configuration.</span><span class="sxs-lookup"><span data-stu-id="ee70c-116">It is recommended that a single Azure AD user be assigned tooGoogle Apps tootest hello provisioning configuration.</span></span> <span data-ttu-id="ee70c-117">Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="ee70c-117">Additional users and/or groups may be assigned later.</span></span>
>*   <span data-ttu-id="ee70c-118">Lorsque vous affectez un tooGoogle utilisateur applications, vous devez sélectionner hello utilisateur ou rôle de « Groupe » dans la boîte de dialogue attribution hello.</span><span class="sxs-lookup"><span data-stu-id="ee70c-118">When assigning a user tooGoogle Apps, you must select hello User or "Group" role in hello assignment dialog.</span></span> <span data-ttu-id="ee70c-119">rôle de « Accès par défaut » Hello ne fonctionne pas pour la configuration.</span><span class="sxs-lookup"><span data-stu-id="ee70c-119">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="ee70c-120">Activer l’approvisionnement automatique des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="ee70c-120">Enable automated user provisioning</span></span>

<span data-ttu-id="ee70c-121">Cette section vous guide à travers de la connexion du compte d’utilisateur de vos applications Azure AD tooGoogle API de configuration et configurez hello toocreate du service de configuration, de mettre à jour et de désactiver les comptes d’utilisateur affecté dans Google Apps, en fonction de l’affectation d’utilisateurs et de groupes dans Azure AD .</span><span class="sxs-lookup"><span data-stu-id="ee70c-121">This section guides you through connecting your Azure AD tooGoogle Apps's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Google Apps based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="ee70c-122">Vous pouvez également choisir tooenabled basé sur SAML Single Sign-On pour Google Apps, en suivant les instructions hello fournies dans [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ee70c-122">You may also choose tooenabled SAML-based Single Sign-On for Google Apps, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ee70c-123">L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que chacune de ces deux fonctionnalités compléte l’autre.</span><span class="sxs-lookup"><span data-stu-id="ee70c-123">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="configure-automatic-user-account-provisioning"></a><span data-ttu-id="ee70c-124">Configurer l’approvisionnement automatique d’un compte utilisateur</span><span class="sxs-lookup"><span data-stu-id="ee70c-124">Configure automatic user account provisioning</span></span>

> [!NOTE]
> <span data-ttu-id="ee70c-125">Une autre option viable pour automatiser la configuration des applications de tooGoogle de l’utilisateur est toouse [Google Apps Active Sync (GADS)](https://support.google.com/a/answer/106368?hl=en) qui configure votre ordinateur local Active Directory identités tooGoogle applications.</span><span class="sxs-lookup"><span data-stu-id="ee70c-125">Another viable option for automating user provisioning tooGoogle Apps is toouse [Google Apps Directory Sync (GADS)](https://support.google.com/a/answer/106368?hl=en) which provisions your on-premises Active Directory identities tooGoogle Apps.</span></span> <span data-ttu-id="ee70c-126">En revanche, la solution hello dans ce didacticiel configure vos utilisateurs Active Directory de Azure (cloud) et les groupes à extension messagerie tooGoogle applications.</span><span class="sxs-lookup"><span data-stu-id="ee70c-126">In contrast, hello solution in this tutorial provisions your Azure Active Directory (cloud) users and mail-enabled groups tooGoogle Apps.</span></span> 

1. <span data-ttu-id="ee70c-127">L’authentification à hello [Google Apps Admin Console](http://admin.google.com/) à l’aide de votre compte d’administrateur, puis cliquez sur **sécurité**.</span><span class="sxs-lookup"><span data-stu-id="ee70c-127">Sign into hello [Google Apps Admin Console](http://admin.google.com/) using your administrator account, and click **Security**.</span></span> <span data-ttu-id="ee70c-128">Si vous ne voyez pas le lien de hello, il peut être masquée sous hello **plus de contrôles** menu bas hello écran hello.</span><span class="sxs-lookup"><span data-stu-id="ee70c-128">If you don't see hello link, it may be hidden under hello **More Controls** menu at hello bottom of hello screen.</span></span>
   
    ![Cliquez sur Sécurité.][10]

2. <span data-ttu-id="ee70c-130">Sur hello **sécurité** , cliquez sur **référence de l’API**.</span><span class="sxs-lookup"><span data-stu-id="ee70c-130">On hello **Security** page, click **API Reference**.</span></span>
   
    ![Cliquez sur Référence d’API.][15]

3. <span data-ttu-id="ee70c-132">Sélectionnez **Activer l'accès à l'API**.</span><span class="sxs-lookup"><span data-stu-id="ee70c-132">Select **Enable API access**.</span></span>
   
    ![Cliquez sur Référence d’API.][16]

    > [!IMPORTANT]
    > <span data-ttu-id="ee70c-134">Pour chaque utilisateur que vous avez l’intention tooprovision tooGoogle applications, leur nom d’utilisateur dans Azure Active Directory *doit* être liée tooa des domaines personnalisés.</span><span class="sxs-lookup"><span data-stu-id="ee70c-134">For every user that you intend tooprovision tooGoogle Apps, their username in Azure Active Directory *must* be tied tooa custom domain.</span></span> <span data-ttu-id="ee70c-135">Par exemple, les noms d'utilisateur qui ressemblent à bob@contoso.onmicrosoft.com ne sont pas acceptés par Google Apps, tandis que ceux ressemblant à bob@contoso.com sont acceptés.</span><span class="sxs-lookup"><span data-stu-id="ee70c-135">For example, usernames that look like bob@contoso.onmicrosoft.com is not accepted by Google Apps, whereas bob@contoso.com is accepted.</span></span> <span data-ttu-id="ee70c-136">Vous pouvez modifier le domaine d’un utilisateur existant en modifiant ses propriétés dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ee70c-136">You can change an existing user's domain by editing their properties in Azure AD.</span></span> <span data-ttu-id="ee70c-137">Instructions pour la tooset un domaine personnalisé pour Azure Active Directory et Google Apps sont inclus dans comme suit.</span><span class="sxs-lookup"><span data-stu-id="ee70c-137">Instructions for how tooset a custom domain for both Azure Active Directory and Google Apps are included in following steps.</span></span>
      
4. <span data-ttu-id="ee70c-138">Si vous n’avez pas encore ajouté un tooyour de nom de domaine personnalisé Azure Active Directory, puis suivez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="ee70c-138">If you haven't added a custom domain name tooyour Azure Active Directory yet, then follow hello following steps:</span></span>
  
    <span data-ttu-id="ee70c-139">a.</span><span class="sxs-lookup"><span data-stu-id="ee70c-139">a.</span></span> <span data-ttu-id="ee70c-140">Bonjour [portail Azure](https://portal.azure.com), on hello du volet de navigation gauche, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ee70c-140">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span> <span data-ttu-id="ee70c-141">Dans la liste de répertoires hello, sélectionnez votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="ee70c-141">In hello directory list, select your directory.</span></span> 

    <span data-ttu-id="ee70c-142">b.</span><span class="sxs-lookup"><span data-stu-id="ee70c-142">b.</span></span> <span data-ttu-id="ee70c-143">Cliquez sur **nom de domaine** sur hello du volet de navigation gauche, puis cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="ee70c-143">Click **Domains name** on hello left navigation pane, and then click **Add**.</span></span>
     
     ![domaine](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_1.png)

     ![ajout de domaine](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_2.png)

    <span data-ttu-id="ee70c-146">c.</span><span class="sxs-lookup"><span data-stu-id="ee70c-146">c.</span></span> <span data-ttu-id="ee70c-147">Tapez votre nom de domaine dans hello **nom de domaine** champ.</span><span class="sxs-lookup"><span data-stu-id="ee70c-147">Type your domain name into hello **Domain name** field.</span></span> <span data-ttu-id="ee70c-148">Ce nom de domaine doit être hello même nom de domaine que vous avez l’intention de toouse pour Google Apps.</span><span class="sxs-lookup"><span data-stu-id="ee70c-148">This domain name should be hello same domain name that you intend toouse for Google Apps.</span></span> <span data-ttu-id="ee70c-149">Lorsque vous êtes prêt, cliquez sur hello **ajouter un domaine** bouton.</span><span class="sxs-lookup"><span data-stu-id="ee70c-149">When ready, click hello **Add Domain** button.</span></span>
     
     ![nom de domaine](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_3.png)

    <span data-ttu-id="ee70c-151">d.</span><span class="sxs-lookup"><span data-stu-id="ee70c-151">d.</span></span> <span data-ttu-id="ee70c-152">Cliquez sur **suivant** page de vérification toogo toohello.</span><span class="sxs-lookup"><span data-stu-id="ee70c-152">Click **Next** toogo toohello verification page.</span></span> <span data-ttu-id="ee70c-153">tooverify que vous possédez ce domaine, vous devez modifier les enregistrements DNS du domaine hello selon les valeurs toohello fournis sur cette page.</span><span class="sxs-lookup"><span data-stu-id="ee70c-153">tooverify that you own this domain, you must edit hello domain's DNS records according toohello values provided on this page.</span></span> <span data-ttu-id="ee70c-154">Vous pouvez choisir tooverify à l’aide **les enregistrements MX** ou **enregistrements TXT**, selon ce que vous sélectionnez pour hello **Type d’enregistrement** option.</span><span class="sxs-lookup"><span data-stu-id="ee70c-154">You may choose tooverify using either **MX records** or **TXT records**, depending on what you select for hello **Record Type** option.</span></span> <span data-ttu-id="ee70c-155">Pour obtenir des instructions plus complètes sur le mode de nom de domaine de tooverify avec Azure AD, consultez [ajouter vos propres tooAzure de nom de domaine Active Directory](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="ee70c-155">For more comprehensive instructions on how tooverify domain name with Azure AD, refer [Add your own domain name tooAzure AD](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).</span></span>
     
     ![domaine](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_4.png)

    <span data-ttu-id="ee70c-157">e.</span><span class="sxs-lookup"><span data-stu-id="ee70c-157">e.</span></span> <span data-ttu-id="ee70c-158">Répétez hello étapes pour tous les domaines hello que vous avez l’intention de tooadd tooyour répertoire précédentes.</span><span class="sxs-lookup"><span data-stu-id="ee70c-158">Repeat hello preceding steps for all hello domains that you intend tooadd tooyour directory.</span></span>

5. <span data-ttu-id="ee70c-159">Maintenant que vous avez vérifié tous vos domaines avec Azure AD, vous devez maintenant les vérifier à nouveau avec Google Apps.</span><span class="sxs-lookup"><span data-stu-id="ee70c-159">Now that you have verified all your domains with Azure AD, you must now verify them again with Google Apps.</span></span> <span data-ttu-id="ee70c-160">Pour chaque domaine qui n’est pas déjà inscrit avec Google Apps, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="ee70c-160">For each domain that isn't already registered with Google Apps, perform hello following steps:</span></span>
   
    <span data-ttu-id="ee70c-161">a.</span><span class="sxs-lookup"><span data-stu-id="ee70c-161">a.</span></span> <span data-ttu-id="ee70c-162">Bonjour [Google Apps Admin Console](http://admin.google.com/), cliquez sur **domaines**.</span><span class="sxs-lookup"><span data-stu-id="ee70c-162">In hello [Google Apps Admin Console](http://admin.google.com/), click **Domains**.</span></span>
     
     ![Cliquer sur Domaines][20]

    <span data-ttu-id="ee70c-164">b.</span><span class="sxs-lookup"><span data-stu-id="ee70c-164">b.</span></span> <span data-ttu-id="ee70c-165">Cliquez sur **Ajouter un domaine ou un alias de domaine**.</span><span class="sxs-lookup"><span data-stu-id="ee70c-165">Click **Add a domain or a domain alias**.</span></span>
     
     ![Ajouter un nouveau domaine][21]

    <span data-ttu-id="ee70c-167">c.</span><span class="sxs-lookup"><span data-stu-id="ee70c-167">c.</span></span> <span data-ttu-id="ee70c-168">Sélectionnez **ajouter un autre domaine**et tapez Bonjour nom de domaine hello que vous aimeriez tooadd.</span><span class="sxs-lookup"><span data-stu-id="ee70c-168">Select **Add another domain**, and type in hello name of hello domain that you would like tooadd.</span></span>
     
     ![Entrer votre nom de domaine][22]

    <span data-ttu-id="ee70c-170">d.</span><span class="sxs-lookup"><span data-stu-id="ee70c-170">d.</span></span> <span data-ttu-id="ee70c-171">Cliquez sur **Continuer et vérifier la propriété du domaine**.</span><span class="sxs-lookup"><span data-stu-id="ee70c-171">Click **Continue and verify domain ownership**.</span></span> <span data-ttu-id="ee70c-172">Suivez ensuite tooverify d’étapes hello que vous possédez le nom de domaine hello.</span><span class="sxs-lookup"><span data-stu-id="ee70c-172">Then follow hello steps tooverify that you own hello domain name.</span></span> <span data-ttu-id="ee70c-173">Pour obtenir des instructions complètes sur tooverify votre domaine avec Google Apps, voir.</span><span class="sxs-lookup"><span data-stu-id="ee70c-173">For comprehensive instructions on how tooverify your domain with Google Apps, see.</span></span> <span data-ttu-id="ee70c-174">[Vérifiez que le propriétaire de votre site avec Google Apps](https://support.google.com/webmasters/answer/35179).</span><span class="sxs-lookup"><span data-stu-id="ee70c-174">[Verify your site ownership with Google Apps](https://support.google.com/webmasters/answer/35179).</span></span>

    <span data-ttu-id="ee70c-175">e.</span><span class="sxs-lookup"><span data-stu-id="ee70c-175">e.</span></span> <span data-ttu-id="ee70c-176">Répétez hello étapes pour tous les domaines supplémentaires que vous avez l’intention de tooadd tooGoogle applications précédentes.</span><span class="sxs-lookup"><span data-stu-id="ee70c-176">Repeat hello preceding steps for any additional domains that you intend tooadd tooGoogle Apps.</span></span>
     
     > [!WARNING]
     > <span data-ttu-id="ee70c-177">Si vous modifiez le domaine principal de hello pour votre client Google Apps, et si vous avez déjà configuré l’authentification unique avec Azure AD, puis vous avez toorepeat étape #3 sous [deuxième étape : activer l’authentification unique sur](#step-two-enable-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="ee70c-177">If you change hello primary domain for your Google Apps tenant, and if you have already configured single sign-on with Azure AD, then you have toorepeat step #3 under [Step Two: Enable Single Sign-On](#step-two-enable-single-sign-on).</span></span>
       
6. <span data-ttu-id="ee70c-178">Bonjour [Google Apps Admin Console](http://admin.google.com/), cliquez sur **rôles d’administrateur**.</span><span class="sxs-lookup"><span data-stu-id="ee70c-178">In hello [Google Apps Admin Console](http://admin.google.com/), click **Admin Roles**.</span></span>
   
     ![Cliquer sur Google Apps][26]

7. <span data-ttu-id="ee70c-180">Déterminer quels admin compte toouse toomanage de la configuration de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ee70c-180">Determine which admin account you would like toouse toomanage user provisioning.</span></span> <span data-ttu-id="ee70c-181">Pourquoi **rôle admin** de ce compte, modifier hello **des privilèges** pour ce rôle.</span><span class="sxs-lookup"><span data-stu-id="ee70c-181">For hello **admin role** of that account, edit hello **Privileges** for that role.</span></span> <span data-ttu-id="ee70c-182">Vérifiez qu’elle a hello tous les **des privilèges d’administration API** activée afin que ce compte peut être utilisé pour la configuration.</span><span class="sxs-lookup"><span data-stu-id="ee70c-182">Make sure it has all hello **Admin API Privileges** enabled so that this account can be used for provisioning.</span></span>
   
     ![Cliquer sur Google Apps][27]
   
    > [!NOTE]
    > <span data-ttu-id="ee70c-184">Si vous configurez un environnement de production, il est recommandé de hello est toocreate un compte d’administrateur dans Google Apps spécifiquement pour cette étape.</span><span class="sxs-lookup"><span data-stu-id="ee70c-184">If you are configuring a production environment, hello best practice is toocreate an admin account in Google Apps specifically for this step.</span></span> <span data-ttu-id="ee70c-185">Ces comptes doivent disposer d’un rôle d’administrateur associé qui possède les privilèges API nécessaires hello.</span><span class="sxs-lookup"><span data-stu-id="ee70c-185">These accounts must have an admin role associated with it that has hello necessary API privileges.</span></span>
     
8. <span data-ttu-id="ee70c-186">Bonjour [portail Azure](https://portal.azure.com), parcourir toohello **Azure Active Directory > applications d’entreprise > toutes les applications** section.</span><span class="sxs-lookup"><span data-stu-id="ee70c-186">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

9. <span data-ttu-id="ee70c-187">Si vous avez déjà configuré Google Apps pour l’authentification unique, recherchez votre instance de Google Apps à l’aide du champ de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="ee70c-187">If you have already configured Google Apps for single sign-on, search for your instance of Google Apps using hello search field.</span></span> <span data-ttu-id="ee70c-188">Sinon, sélectionnez **ajouter** et recherchez **Google Apps** dans la galerie d’applications hello.</span><span class="sxs-lookup"><span data-stu-id="ee70c-188">Otherwise, select **Add** and search for **Google Apps** in hello application gallery.</span></span> <span data-ttu-id="ee70c-189">Sélectionnez Google Apps à partir des résultats de recherche hello et ajoutez-le tooyour la liste des applications.</span><span class="sxs-lookup"><span data-stu-id="ee70c-189">Select Google Apps from hello search results, and add it tooyour list of applications.</span></span>

10. <span data-ttu-id="ee70c-190">Sélectionnez votre instance de Google Apps, puis hello **Provisioning** onglet.</span><span class="sxs-lookup"><span data-stu-id="ee70c-190">Select your instance of Google Apps, then select hello **Provisioning** tab.</span></span>

11. <span data-ttu-id="ee70c-191">Ensemble hello **Mode d’approvisionnement** trop**automatique**.</span><span class="sxs-lookup"><span data-stu-id="ee70c-191">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

     ![approvisionnement](./media/active-directory-saas-google-apps-provisioning-tutorial/provisioning.png)

12. <span data-ttu-id="ee70c-193">Sous hello **informations d’identification administrateur** , cliquez sur **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="ee70c-193">Under hello **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="ee70c-194">Une boîte de dialogue d’autorisation Google Apps s’ouvre dans une nouvelle fenêtre du navigateur.</span><span class="sxs-lookup"><span data-stu-id="ee70c-194">It opens a Google Apps authorization dialog in a new browser window.</span></span>

13. <span data-ttu-id="ee70c-195">Confirmez que vous souhaitez que les modifications de toomake autorisations Azure Active Directory toogive que tooyour Google Apps locataire.</span><span class="sxs-lookup"><span data-stu-id="ee70c-195">Confirm that you would like toogive Azure Active Directory permission toomake changes tooyour Google Apps tenant.</span></span> <span data-ttu-id="ee70c-196">Cliquez sur **Accepter**.</span><span class="sxs-lookup"><span data-stu-id="ee70c-196">Click **Accept**.</span></span>
    
     ![Confirmez les autorisations.][28]

14. <span data-ttu-id="ee70c-198">Bonjour portail Azure, cliquez sur **tester la connexion** tooensure AD Azure peut se connecter tooyour Google Apps application.</span><span class="sxs-lookup"><span data-stu-id="ee70c-198">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Google Apps app.</span></span> <span data-ttu-id="ee70c-199">Si hello connexion échoue, assurez-vous que votre compte Google Apps a des autorisations d’administrateur d’équipe et essayez hello **« Autoriser »** pas à pas.</span><span class="sxs-lookup"><span data-stu-id="ee70c-199">If hello connection fails, ensure your Google Apps account has Team Admin permissions and try hello **"Authorize"** step again.</span></span>

15. <span data-ttu-id="ee70c-200">Entrez hello adresse de messagerie d’une personne ou un groupe qui doit recevoir des notifications d’erreur approvisionnement hello **courrier électronique de Notification** champ et la case à cocher hello.</span><span class="sxs-lookup"><span data-stu-id="ee70c-200">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

16. <span data-ttu-id="ee70c-201">Cliquez sur **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="ee70c-201">Click **Save.**</span></span>

17. <span data-ttu-id="ee70c-202">Sous la section des mappages de hello, sélectionnez **tooGoogle de synchronisation Azure Active Directory Users applications.**</span><span class="sxs-lookup"><span data-stu-id="ee70c-202">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooGoogle Apps.**</span></span>

18. <span data-ttu-id="ee70c-203">Bonjour **des mappages d’attributs** section, passez en revue les attributs utilisateur hello qui sont synchronisés à partir d’Azure AD tooGoogle applications.</span><span class="sxs-lookup"><span data-stu-id="ee70c-203">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooGoogle Apps.</span></span> <span data-ttu-id="ee70c-204">Hello attributs sélectionnés en tant que **correspondance** propriétés sont des comptes d’utilisateur hello toomatch utilisés dans Google Apps pour les opérations de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="ee70c-204">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Google Apps for update operations.</span></span> <span data-ttu-id="ee70c-205">Sélectionnez toocommit de bouton hello enregistrer toutes les modifications.</span><span class="sxs-lookup"><span data-stu-id="ee70c-205">Select hello Save button toocommit any changes.</span></span>

19. <span data-ttu-id="ee70c-206">tooenable hello service de configuration d’Azure AD pour Google Apps, modification hello **état d’approvisionnement** trop**sur** Bonjour section de paramètres</span><span class="sxs-lookup"><span data-stu-id="ee70c-206">tooenable hello Azure AD provisioning service for Google Apps, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

20. <span data-ttu-id="ee70c-207">Cliquez sur **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="ee70c-207">Click **Save.**</span></span>

<span data-ttu-id="ee70c-208">Il démarre la synchronisation initiale de hello de tous les utilisateurs et/ou groupes affectés tooGoogle des applications dans la section utilisateurs et groupes de hello.</span><span class="sxs-lookup"><span data-stu-id="ee70c-208">It starts hello initial synchronization of any users and/or groups assigned tooGoogle Apps in hello Users and Groups section.</span></span> <span data-ttu-id="ee70c-209">la synchronisation initiale Hello prend tooperform plus de temps que les synchronisations suivantes, qui se produisent toutes les 20 minutes environ tant que service de hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="ee70c-209">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="ee70c-210">Vous pouvez utiliser hello **détails de synchronisation** section toomonitor cours et suivre des rapports d’activité tooprovisioning des liens, qui décrivent toutes les actions effectuées par hello mise en service du service sur votre application Google Apps.</span><span class="sxs-lookup"><span data-stu-id="ee70c-210">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Google Apps app.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ee70c-211">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="ee70c-211">Additional resources</span></span>

* [<span data-ttu-id="ee70c-212">Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise</span><span class="sxs-lookup"><span data-stu-id="ee70c-212">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ee70c-213">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="ee70c-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="ee70c-214">Configurer l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="ee70c-214">Configure Single Sign-on</span></span>](active-directory-saas-google-apps-tutorial.md)



<!--Image references-->

[10]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-security.png
[15]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-api-enabled.png
[20]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-add-another.png
[24]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-auth.png