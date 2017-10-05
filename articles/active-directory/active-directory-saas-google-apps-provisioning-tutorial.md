---
title: "Didacticiel : configuration de Google Apps pour l’approvisionnement automatique d’utilisateurs dans Azure | Documents Microsoft"
description: "Découvrez comment approvisionner et déprovisionner automatiquement des comptes utilisateur d’Azure AD vers Google Apps."
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
ms.openlocfilehash: b061f0ddad70be4a5ca48d48d1a737d6af8afa8d
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-configuring-google-apps-for-automatic-user-provisioning"></a><span data-ttu-id="0f62c-103">Didacticiel : configuration de Google Apps pour approvisionner automatiquement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="0f62c-103">Tutorial: Configuring Google Apps for automatic user provisioning</span></span>

<span data-ttu-id="0f62c-104">L’objectif de ce didacticiel est de vous indiquer les étapes à suivre dans Google Apps et Azure AD pour approvisionner et déprovisionner automatiquement des comptes utilisateur d’Azure AD vers Google Apps.</span><span class="sxs-lookup"><span data-stu-id="0f62c-104">The objective of this tutorial is to show you the steps you need to perform in Google Apps and Azure AD to automatically provision and de-provision user accounts from Azure AD to Google Apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0f62c-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0f62c-105">Prerequisites</span></span>

<span data-ttu-id="0f62c-106">Le scénario décrit dans ce didacticiel part du principe que vous disposez des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="0f62c-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="0f62c-107">Un client Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0f62c-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="0f62c-108">Vous devez avoir un client valide pour Google Apps pour Travailler ou Google Apps pour l’Éducation.</span><span class="sxs-lookup"><span data-stu-id="0f62c-108">You must have a valid tenant for Google Apps for Work or Google Apps for Education.</span></span> <span data-ttu-id="0f62c-109">Vous pouvez utiliser un compte d’essai gratuit pour chaque service.</span><span class="sxs-lookup"><span data-stu-id="0f62c-109">You may use a free trial account for either service.</span></span>
*   <span data-ttu-id="0f62c-110">Un compte utilisateur dans Google Apps avec les autorisations d’administrateur d’équipe.</span><span class="sxs-lookup"><span data-stu-id="0f62c-110">A user account in Google Apps with Team Admin permissions.</span></span>

## <a name="assigning-users-to-google-apps"></a><span data-ttu-id="0f62c-111">Attribution d’utilisateurs à Google Apps</span><span class="sxs-lookup"><span data-stu-id="0f62c-111">Assigning users to Google Apps</span></span>

<span data-ttu-id="0f62c-112">Azure Active Directory utilise un concept appelé « affectations » pour déterminer les utilisateurs devant recevoir l’accès aux applications sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="0f62c-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="0f62c-113">Dans le cadre de l’approvisionnement automatique de comptes utilisateur, seuls les utilisateurs et les groupes qui ont été « attribués » à une application dans Azure AD sont synchronisés.</span><span class="sxs-lookup"><span data-stu-id="0f62c-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span>

<span data-ttu-id="0f62c-114">Avant de configurer et d’activer le service d’approvisionnement, vous devez déterminer quels utilisateurs et/ou groupes dans Azure AD représentent les utilisateurs qui ont besoin d’accéder à votre application Google Apps.</span><span class="sxs-lookup"><span data-stu-id="0f62c-114">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Google Apps app.</span></span> <span data-ttu-id="0f62c-115">Une fois choisi, vous pouvez attribuer ces utilisateurs à votre application Google Apps en suivant les instructions fournies ici : [Attribuer un utilisateur ou un groupe à une application d’entreprise](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)</span><span class="sxs-lookup"><span data-stu-id="0f62c-115">Once decided, you can assign these users to your Google Apps app by following the instructions here: [Assign a user or group to an enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)</span></span>

> [!IMPORTANT]
>*   <span data-ttu-id="0f62c-116">Nous vous recommandons de n’attribuer qu’un seul utilisateur Azure AD à Google Apps pour tester la configuration de l’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="0f62c-116">It is recommended that a single Azure AD user be assigned to Google Apps to test the provisioning configuration.</span></span> <span data-ttu-id="0f62c-117">Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="0f62c-117">Additional users and/or groups may be assigned later.</span></span>
>*   <span data-ttu-id="0f62c-118">Lorsque vous attribuez un utilisateur à Google Apps, vous devez sélectionner le rôle Utilisateur ou Groupe dans la boîte de dialogue d’attribution.</span><span class="sxs-lookup"><span data-stu-id="0f62c-118">When assigning a user to Google Apps, you must select the User or "Group" role in the assignment dialog.</span></span> <span data-ttu-id="0f62c-119">Le rôle « Accès par défaut » ne fonctionne pas pour l’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="0f62c-119">The "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="0f62c-120">Activer l’approvisionnement automatique des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="0f62c-120">Enable automated user provisioning</span></span>

<span data-ttu-id="0f62c-121">Cette section vous guide afin de connecter votre instance Azure AD à votre compte utilisateur Google Apps qui fournit l’API et configurer le service d’approvisionnement afin de créer, mettre à jour et désactiver des comptes utilisateur attribués dans Google Apps, en fonction des attributions d’utilisateur et de groupe dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0f62c-121">This section guides you through connecting your Azure AD to Google Apps's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Google Apps based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="0f62c-122">Vous pouvez également choisir d’activer l’authentification unique basée sur SAML pour Google Apps, en suivant les instructions disponibles dans le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0f62c-122">You may also choose to enabled SAML-based Single Sign-On for Google Apps, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="0f62c-123">L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que chacune de ces deux fonctionnalités compléte l’autre.</span><span class="sxs-lookup"><span data-stu-id="0f62c-123">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="configure-automatic-user-account-provisioning"></a><span data-ttu-id="0f62c-124">Configurer l’approvisionnement automatique d’un compte utilisateur</span><span class="sxs-lookup"><span data-stu-id="0f62c-124">Configure automatic user account provisioning</span></span>

> [!NOTE]
> <span data-ttu-id="0f62c-125">Il existe une autre option pour automatiser l’approvisionnement des utilisateurs avec Google Apps : il s’agit d’utiliser [Google Apps Active Sync (GADS)](https://support.google.com/a/answer/106368?hl=en) , qui approvisionne vos identités Active Directory en local pour Google Apps.</span><span class="sxs-lookup"><span data-stu-id="0f62c-125">Another viable option for automating user provisioning to Google Apps is to use [Google Apps Directory Sync (GADS)](https://support.google.com/a/answer/106368?hl=en) which provisions your on-premises Active Directory identities to Google Apps.</span></span> <span data-ttu-id="0f62c-126">En revanche, la solution proposée dans ce didacticiel approvisionne vos utilisateurs Azure Active Directory (cloud) et vos groupes à extension messagerie pour Google Apps.</span><span class="sxs-lookup"><span data-stu-id="0f62c-126">In contrast, the solution in this tutorial provisions your Azure Active Directory (cloud) users and mail-enabled groups to Google Apps.</span></span> 

1. <span data-ttu-id="0f62c-127">Connectez-vous à la [Console d'administration de Google Apps](http://admin.google.com/) avec votre compte d'administrateur, puis cliquez sur **Sécurité**.</span><span class="sxs-lookup"><span data-stu-id="0f62c-127">Sign into the [Google Apps Admin Console](http://admin.google.com/) using your administrator account, and click **Security**.</span></span> <span data-ttu-id="0f62c-128">Si le lien ne s'affiche pas, il est peut-être masqué par le menu **Autres contrôles** situé en bas de l'écran.</span><span class="sxs-lookup"><span data-stu-id="0f62c-128">If you don't see the link, it may be hidden under the **More Controls** menu at the bottom of the screen.</span></span>
   
    ![Cliquez sur Sécurité.][10]

2. <span data-ttu-id="0f62c-130">Sur la page **Sécurité**, cliquez sur **Référence de l’API**.</span><span class="sxs-lookup"><span data-stu-id="0f62c-130">On the **Security** page, click **API Reference**.</span></span>
   
    ![Cliquez sur Référence d’API.][15]

3. <span data-ttu-id="0f62c-132">Sélectionnez **Activer l'accès à l'API**.</span><span class="sxs-lookup"><span data-stu-id="0f62c-132">Select **Enable API access**.</span></span>
   
    ![Cliquez sur Référence d’API.][16]

    > [!IMPORTANT]
    > <span data-ttu-id="0f62c-134">Le nom d'utilisateur Azure Active Directory de chaque utilisateur que vous souhaitez approvisionner pour Google Apps *doit* être associé à un domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="0f62c-134">For every user that you intend to provision to Google Apps, their username in Azure Active Directory *must* be tied to a custom domain.</span></span> <span data-ttu-id="0f62c-135">Par exemple, les noms d'utilisateur qui ressemblent à bob@contoso.onmicrosoft.com ne sont pas acceptés par Google Apps, tandis que ceux ressemblant à bob@contoso.com sont acceptés.</span><span class="sxs-lookup"><span data-stu-id="0f62c-135">For example, usernames that look like bob@contoso.onmicrosoft.com is not accepted by Google Apps, whereas bob@contoso.com is accepted.</span></span> <span data-ttu-id="0f62c-136">Vous pouvez modifier le domaine d’un utilisateur existant en modifiant ses propriétés dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0f62c-136">You can change an existing user's domain by editing their properties in Azure AD.</span></span> <span data-ttu-id="0f62c-137">Vous trouverez ci-dessous des instructions sur la définition d’un domaine personnalisé pour Azure Active Directory et Google Apps.</span><span class="sxs-lookup"><span data-stu-id="0f62c-137">Instructions for how to set a custom domain for both Azure Active Directory and Google Apps are included in following steps.</span></span>
      
4. <span data-ttu-id="0f62c-138">Si vous n’avez pas encore ajouté un nom de domaine personnalisé pour Azure Active Directory, suivez la procédure ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="0f62c-138">If you haven't added a custom domain name to your Azure Active Directory yet, then follow the following steps:</span></span>
  
    <span data-ttu-id="0f62c-139">a.</span><span class="sxs-lookup"><span data-stu-id="0f62c-139">a.</span></span> <span data-ttu-id="0f62c-140">Dans le volet de navigation gauche du [portail Azure](https://portal.azure.com), cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0f62c-140">In the [Azure portal](https://portal.azure.com), on the left navigation pane, click **Active Directory**.</span></span> <span data-ttu-id="0f62c-141">Dans la liste Annuaire, sélectionnez votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="0f62c-141">In the directory list, select your directory.</span></span> 

    <span data-ttu-id="0f62c-142">b.</span><span class="sxs-lookup"><span data-stu-id="0f62c-142">b.</span></span> <span data-ttu-id="0f62c-143">Cliquez sur **nom des domaines** dans le volet de navigation gauche, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="0f62c-143">Click **Domains name** on the left navigation pane, and then click **Add**.</span></span>
     
     ![domaine](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_1.png)

     ![ajout de domaine](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_2.png)

    <span data-ttu-id="0f62c-146">c.</span><span class="sxs-lookup"><span data-stu-id="0f62c-146">c.</span></span> <span data-ttu-id="0f62c-147">Saisissez votre nom de domaine dans le champ **Nom de domaine** .</span><span class="sxs-lookup"><span data-stu-id="0f62c-147">Type your domain name into the **Domain name** field.</span></span> <span data-ttu-id="0f62c-148">Ce nom de domaine doit être identique à celui que vous souhaitez utiliser pour Google Apps.</span><span class="sxs-lookup"><span data-stu-id="0f62c-148">This domain name should be the same domain name that you intend to use for Google Apps.</span></span> <span data-ttu-id="0f62c-149">Lorsque vous êtes prêt, cliquez sur le bouton **Ajouter un domaine** .</span><span class="sxs-lookup"><span data-stu-id="0f62c-149">When ready, click the **Add Domain** button.</span></span>
     
     ![nom de domaine](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_3.png)

    <span data-ttu-id="0f62c-151">d.</span><span class="sxs-lookup"><span data-stu-id="0f62c-151">d.</span></span> <span data-ttu-id="0f62c-152">Cliquez sur **Suivant** pour accéder à la page de vérification.</span><span class="sxs-lookup"><span data-stu-id="0f62c-152">Click **Next** to go to the verification page.</span></span> <span data-ttu-id="0f62c-153">Pour vérifier que vous possédez ce domaine, vous devez modifier les enregistrements DNS du domaine en fonction des valeurs fournies dans cette page.</span><span class="sxs-lookup"><span data-stu-id="0f62c-153">To verify that you own this domain, you must edit the domain's DNS records according to the values provided on this page.</span></span> <span data-ttu-id="0f62c-154">Vous pouvez choisir d'effectuer la vérification en utilisant des **enregistrements MX** ou des **enregistrements TXT**, selon l’option de **Type d'enregistrement** sélectionné.</span><span class="sxs-lookup"><span data-stu-id="0f62c-154">You may choose to verify using either **MX records** or **TXT records**, depending on what you select for the **Record Type** option.</span></span> <span data-ttu-id="0f62c-155">Pour obtenir des instructions plus complètes sur la vérification de nom de domaine avec Azure AD, consultez [Ajout de votre propre domaine à Azure AD](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="0f62c-155">For more comprehensive instructions on how to verify domain name with Azure AD, refer [Add your own domain name to Azure AD](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).</span></span>
     
     ![domaine](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_4.png)

    <span data-ttu-id="0f62c-157">e.</span><span class="sxs-lookup"><span data-stu-id="0f62c-157">e.</span></span> <span data-ttu-id="0f62c-158">Répétez la procédure précédente pour tous les domaines que vous souhaitez ajouter à votre répertoire.</span><span class="sxs-lookup"><span data-stu-id="0f62c-158">Repeat the preceding steps for all the domains that you intend to add to your directory.</span></span>

5. <span data-ttu-id="0f62c-159">Maintenant que vous avez vérifié tous vos domaines avec Azure AD, vous devez maintenant les vérifier à nouveau avec Google Apps.</span><span class="sxs-lookup"><span data-stu-id="0f62c-159">Now that you have verified all your domains with Azure AD, you must now verify them again with Google Apps.</span></span> <span data-ttu-id="0f62c-160">Pour chaque domaine qui n’est pas déjà inscrit auprès de Google Apps, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0f62c-160">For each domain that isn't already registered with Google Apps, perform the following steps:</span></span>
   
    <span data-ttu-id="0f62c-161">a.</span><span class="sxs-lookup"><span data-stu-id="0f62c-161">a.</span></span> <span data-ttu-id="0f62c-162">Dans la [Console d'administration de Google Apps](http://admin.google.com/), cliquez sur **Domaines**.</span><span class="sxs-lookup"><span data-stu-id="0f62c-162">In the [Google Apps Admin Console](http://admin.google.com/), click **Domains**.</span></span>
     
     ![Cliquer sur Domaines][20]

    <span data-ttu-id="0f62c-164">b.</span><span class="sxs-lookup"><span data-stu-id="0f62c-164">b.</span></span> <span data-ttu-id="0f62c-165">Cliquez sur **Ajouter un domaine ou un alias de domaine**.</span><span class="sxs-lookup"><span data-stu-id="0f62c-165">Click **Add a domain or a domain alias**.</span></span>
     
     ![Ajouter un nouveau domaine][21]

    <span data-ttu-id="0f62c-167">c.</span><span class="sxs-lookup"><span data-stu-id="0f62c-167">c.</span></span> <span data-ttu-id="0f62c-168">Sélectionnez **Ajouter un autre domaine**, puis tapez le nom du domaine que vous souhaitez ajouter.</span><span class="sxs-lookup"><span data-stu-id="0f62c-168">Select **Add another domain**, and type in the name of the domain that you would like to add.</span></span>
     
     ![Entrer votre nom de domaine][22]

    <span data-ttu-id="0f62c-170">d.</span><span class="sxs-lookup"><span data-stu-id="0f62c-170">d.</span></span> <span data-ttu-id="0f62c-171">Cliquez sur **Continuer et vérifier la propriété du domaine**.</span><span class="sxs-lookup"><span data-stu-id="0f62c-171">Click **Continue and verify domain ownership**.</span></span> <span data-ttu-id="0f62c-172">Puis suivez les étapes pour vérifier que vous possédez le nom de domaine.</span><span class="sxs-lookup"><span data-stu-id="0f62c-172">Then follow the steps to verify that you own the domain name.</span></span> <span data-ttu-id="0f62c-173">Pour obtenir des instructions complètes sur la vérification de votre domaine avec Google Apps, consultez.</span><span class="sxs-lookup"><span data-stu-id="0f62c-173">For comprehensive instructions on how to verify your domain with Google Apps, see.</span></span> <span data-ttu-id="0f62c-174">[Vérifiez que le propriétaire de votre site avec Google Apps](https://support.google.com/webmasters/answer/35179).</span><span class="sxs-lookup"><span data-stu-id="0f62c-174">[Verify your site ownership with Google Apps](https://support.google.com/webmasters/answer/35179).</span></span>

    <span data-ttu-id="0f62c-175">e.</span><span class="sxs-lookup"><span data-stu-id="0f62c-175">e.</span></span> <span data-ttu-id="0f62c-176">Répétez la procédure précédente pour tous les domaines supplémentaires que vous souhaitez ajouter à Google Apps.</span><span class="sxs-lookup"><span data-stu-id="0f62c-176">Repeat the preceding steps for any additional domains that you intend to add to Google Apps.</span></span>
     
     > [!WARNING]
     > <span data-ttu-id="0f62c-177">Si vous modifiez le domaine principal pour votre client Google Apps tout en ayant déjà configuré l’authentification unique avec Azure AD, vous devez répéter l’étape 3 sous [Étape 2 : activation de l’authentification unique](#step-two-enable-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="0f62c-177">If you change the primary domain for your Google Apps tenant, and if you have already configured single sign-on with Azure AD, then you have to repeat step #3 under [Step Two: Enable Single Sign-On](#step-two-enable-single-sign-on).</span></span>
       
6. <span data-ttu-id="0f62c-178">Dans la [Console d'administration de Google Apps](http://admin.google.com/), cliquez sur **Rôles d'administrateur**.</span><span class="sxs-lookup"><span data-stu-id="0f62c-178">In the [Google Apps Admin Console](http://admin.google.com/), click **Admin Roles**.</span></span>
   
     ![Cliquer sur Google Apps][26]

7. <span data-ttu-id="0f62c-180">Déterminez le compte d’administrateur à utiliser pour gérer l’approvisionnement de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0f62c-180">Determine which admin account you would like to use to manage user provisioning.</span></span> <span data-ttu-id="0f62c-181">Pour le **Rôle d’administrateur** de ce compte, modifiez les **Privilèges** pour ce rôle.</span><span class="sxs-lookup"><span data-stu-id="0f62c-181">For the **admin role** of that account, edit the **Privileges** for that role.</span></span> <span data-ttu-id="0f62c-182">Vérifiez qu'il possède tous les **Privilèges d'administrateur d'API** activés pour que ce compte puisse être utilisé pour l'approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="0f62c-182">Make sure it has all the **Admin API Privileges** enabled so that this account can be used for provisioning.</span></span>
   
     ![Cliquer sur Google Apps][27]
   
    > [!NOTE]
    > <span data-ttu-id="0f62c-184">Si vous configurez un environnement de production, la meilleure pratique est de créer un compte d’administrateur dans Google Apps spécialement pour cette étape.</span><span class="sxs-lookup"><span data-stu-id="0f62c-184">If you are configuring a production environment, the best practice is to create an admin account in Google Apps specifically for this step.</span></span> <span data-ttu-id="0f62c-185">Ce compte doit avoir un rôle d’administrateur associé qui possède les privilèges d’API nécessaires.</span><span class="sxs-lookup"><span data-stu-id="0f62c-185">These accounts must have an admin role associated with it that has the necessary API privileges.</span></span>
     
8. <span data-ttu-id="0f62c-186">Dans le [portail Azure](https://portal.azure.com), accédez à la section **Azure Active Directory > Applications d’entreprise > Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="0f62c-186">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

9. <span data-ttu-id="0f62c-187">Si vous avez déjà configuré Google Apps pour l’authentification unique, recherchez votre instance de Google Apps à l’aide du champ de recherche.</span><span class="sxs-lookup"><span data-stu-id="0f62c-187">If you have already configured Google Apps for single sign-on, search for your instance of Google Apps using the search field.</span></span> <span data-ttu-id="0f62c-188">Sinon, sélectionnez **Ajouter** et recherchez **Google Apps** dans la galerie d’applications.</span><span class="sxs-lookup"><span data-stu-id="0f62c-188">Otherwise, select **Add** and search for **Google Apps** in the application gallery.</span></span> <span data-ttu-id="0f62c-189">Dans les résultats de la recherche, sélectionnez Google Apps, puis ajoutez-le à votre liste d’applications.</span><span class="sxs-lookup"><span data-stu-id="0f62c-189">Select Google Apps from the search results, and add it to your list of applications.</span></span>

10. <span data-ttu-id="0f62c-190">Sélectionnez votre instance de Google Apps, puis sélectionnez l’onglet **Approvisionnement**.</span><span class="sxs-lookup"><span data-stu-id="0f62c-190">Select your instance of Google Apps, then select the **Provisioning** tab.</span></span>

11. <span data-ttu-id="0f62c-191">Définissez le **Mode d’approvisionnement** sur **Automatique**.</span><span class="sxs-lookup"><span data-stu-id="0f62c-191">Set the **Provisioning Mode** to **Automatic**.</span></span> 

     ![approvisionnement](./media/active-directory-saas-google-apps-provisioning-tutorial/provisioning.png)

12. <span data-ttu-id="0f62c-193">Sous la section **informations d’identification de l’administrateur**, cliquez sur **Autoriser**.</span><span class="sxs-lookup"><span data-stu-id="0f62c-193">Under the **Admin Credentials** section, click **Authorize**.</span></span> <span data-ttu-id="0f62c-194">Une boîte de dialogue d’autorisation Google Apps s’ouvre dans une nouvelle fenêtre du navigateur.</span><span class="sxs-lookup"><span data-stu-id="0f62c-194">It opens a Google Apps authorization dialog in a new browser window.</span></span>

13. <span data-ttu-id="0f62c-195">Confirmez que vous souhaitez permettre à Azure Active Directory d’apporter des modifications à votre client Google Apps.</span><span class="sxs-lookup"><span data-stu-id="0f62c-195">Confirm that you would like to give Azure Active Directory permission to make changes to your Google Apps tenant.</span></span> <span data-ttu-id="0f62c-196">Cliquez sur **Accepter**.</span><span class="sxs-lookup"><span data-stu-id="0f62c-196">Click **Accept**.</span></span>
    
     ![Confirmez les autorisations.][28]

14. <span data-ttu-id="0f62c-198">Dans le portail Azure, cliquez sur **Tester la connexion** pour vous assurer qu’Azure AD peut se connecter à votre application Google Apps.</span><span class="sxs-lookup"><span data-stu-id="0f62c-198">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Google Apps app.</span></span> <span data-ttu-id="0f62c-199">Si la connexion échoue, vérifiez que votre compte Google Apps dispose des autorisations d’administrateur d’équipe et réessayez l’étape **« Autoriser »**.</span><span class="sxs-lookup"><span data-stu-id="0f62c-199">If the connection fails, ensure your Google Apps account has Team Admin permissions and try the **"Authorize"** step again.</span></span>

15. <span data-ttu-id="0f62c-200">Entrez l’adresse e-mail d’une personne ou d’un groupe qui doit recevoir les notifications d’erreur d’approvisionnement dans le champ **E-mail de notification** et cochez la case.</span><span class="sxs-lookup"><span data-stu-id="0f62c-200">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox.</span></span>

16. <span data-ttu-id="0f62c-201">Cliquez sur **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="0f62c-201">Click **Save.**</span></span>

17. <span data-ttu-id="0f62c-202">Dans la section Mappages, sélectionnez **Synchroniser les utilisateurs Azure Active Directory avec Google Apps.**</span><span class="sxs-lookup"><span data-stu-id="0f62c-202">Under the Mappings section, select **Synchronize Azure Active Directory Users to Google Apps.**</span></span>

18. <span data-ttu-id="0f62c-203">Dans la section **Mappages d’attributs**, passez en revue les attributs utilisateur qui sont synchronisés à partir d’Azure AD vers Google Apps.</span><span class="sxs-lookup"><span data-stu-id="0f62c-203">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Google Apps.</span></span> <span data-ttu-id="0f62c-204">Les attributs sélectionnés en tant que propriétés de **Correspondance** sont utilisés pour faire correspondre les comptes utilisateur dans Google Apps pour les opérations de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="0f62c-204">The attributes selected as **Matching** properties are used to match the user accounts in Google Apps for update operations.</span></span> <span data-ttu-id="0f62c-205">Cliquez sur le bouton Enregistrer pour valider les modifications.</span><span class="sxs-lookup"><span data-stu-id="0f62c-205">Select the Save button to commit any changes.</span></span>

19. <span data-ttu-id="0f62c-206">Pour activer le service d’approvisionnement Azure AD pour Google Apps, définissez **l’état de l’approvisionnement** sur **Activé** dans la section Paramètres</span><span class="sxs-lookup"><span data-stu-id="0f62c-206">To enable the Azure AD provisioning service for Google Apps, change the **Provisioning Status** to **On** in the Settings section</span></span>

20. <span data-ttu-id="0f62c-207">Cliquez sur **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="0f62c-207">Click **Save.**</span></span>

<span data-ttu-id="0f62c-208">Cette commande démarre la synchronisation initiale des utilisateurs et/ou des groupes affectés à Google Apps dans la section Utilisateurs et Groupes.</span><span class="sxs-lookup"><span data-stu-id="0f62c-208">It starts the initial synchronization of any users and/or groups assigned to Google Apps in the Users and Groups section.</span></span> <span data-ttu-id="0f62c-209">La synchronisation initiale prend plus de temps que les synchronisations suivantes, qui se produisent environ toutes les 20 minutes, tant que le service est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="0f62c-209">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="0f62c-210">Vous pouvez utiliser la section **Détails de synchronisation** pour surveiller la progression et les liens vers les rapports d’activité d’approvisionnement, qui décrivent toutes les actions effectuées par le service d’approvisionnement dans votre application Google Apps.</span><span class="sxs-lookup"><span data-stu-id="0f62c-210">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your Google Apps app.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0f62c-211">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="0f62c-211">Additional resources</span></span>

* [<span data-ttu-id="0f62c-212">Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise</span><span class="sxs-lookup"><span data-stu-id="0f62c-212">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0f62c-213">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="0f62c-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="0f62c-214">Configurer l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="0f62c-214">Configure Single Sign-on</span></span>](active-directory-saas-google-apps-tutorial.md)



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