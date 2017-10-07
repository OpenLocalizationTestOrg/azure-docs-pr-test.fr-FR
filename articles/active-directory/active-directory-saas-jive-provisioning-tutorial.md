---
title: "Didacticiel : Intégration d’Azure Active Directory à Jive | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Jive."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6fbfdbe7-d66c-4305-9fea-76d6a6a92830
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: b1c0d0bc2d79427c055f577fe5f9d30d10f1bbdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-jive-for-user-provisioning"></a><span data-ttu-id="55809-103">Didacticiel : Configuration de Jive pour l’approvisionnement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="55809-103">Tutorial: Configuring Jive for User Provisioning</span></span>

<span data-ttu-id="55809-104">objectif Hello de ce didacticiel est tooshow vous hello étapes que vous devez tooperform dans Jive et Azure AD tooautomatically approvisionner et configurer des comptes d’utilisateur à partir d’Azure AD tooJive.</span><span class="sxs-lookup"><span data-stu-id="55809-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Jive and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooJive.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="55809-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="55809-105">Prerequisites</span></span>

<span data-ttu-id="55809-106">scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="55809-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="55809-107">Un locataire Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="55809-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="55809-108">Un abonnement Jive pour lequel l’authentification unique est activée.</span><span class="sxs-lookup"><span data-stu-id="55809-108">A Jive single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="55809-109">Un compte utilisateur dans Jive avec les autorisations d’administrateur d’équipe.</span><span class="sxs-lookup"><span data-stu-id="55809-109">A user account in Jive with Team Admin permissions.</span></span>

## <a name="assigning-users-toojive"></a><span data-ttu-id="55809-110">Affectation d’utilisateurs tooJive</span><span class="sxs-lookup"><span data-stu-id="55809-110">Assigning users tooJive</span></span>

<span data-ttu-id="55809-111">Azure Active Directory utilise un concept appelé toodetermine « affectations » les utilisateurs qui doivent recevoir l’accès tooselected applications.</span><span class="sxs-lookup"><span data-stu-id="55809-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="55809-112">Dans le contexte de hello de configuration de compte automatique d’utilisateurs, seuls les utilisateurs de hello et les groupes qui ont été « affectés » application tooan dans Azure AD est synchronisé.</span><span class="sxs-lookup"><span data-stu-id="55809-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="55809-113">Avant de configurer et de l’activation de hello service de configuration, vous devez toodecide quels utilisateurs ou des groupes dans Azure AD qui représentent des utilisateurs qui doivent accéder aux tooyour Jive application hello.</span><span class="sxs-lookup"><span data-stu-id="55809-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Jive app.</span></span> <span data-ttu-id="55809-114">Après choisi, vous pouvez attribuer à ces applications de Jive tooyour les utilisateurs en suivant les instructions hello ici :</span><span class="sxs-lookup"><span data-stu-id="55809-114">Once decided, you can assign these users tooyour Jive app by following hello instructions here:</span></span>

[<span data-ttu-id="55809-115">Affecter une application d’entreprise tooan utilisateur ou un groupe</span><span class="sxs-lookup"><span data-stu-id="55809-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toojive"></a><span data-ttu-id="55809-116">Conseils importants pour l’affectation d’utilisateurs tooJive</span><span class="sxs-lookup"><span data-stu-id="55809-116">Important tips for assigning users tooJive</span></span>

*   <span data-ttu-id="55809-117">Il est recommandé qu’un seul utilisateur Azure AD avoir tooJive tootest hello est mise en service de configuration.</span><span class="sxs-lookup"><span data-stu-id="55809-117">It is recommended that a single Azure AD user be assigned tooJive tootest hello provisioning configuration.</span></span> <span data-ttu-id="55809-118">Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="55809-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="55809-119">Lorsque vous affectez un tooJive d’utilisateur, vous devez sélectionner un rôle d’utilisateur valide.</span><span class="sxs-lookup"><span data-stu-id="55809-119">When assigning a user tooJive, you must select a valid user role.</span></span> <span data-ttu-id="55809-120">rôle de « Accès par défaut » Hello ne fonctionne pas pour la configuration.</span><span class="sxs-lookup"><span data-stu-id="55809-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="55809-121">Activer l’approvisionnement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="55809-121">Enable User Provisioning</span></span>

<span data-ttu-id="55809-122">Cette section vous guide à travers de la connexion du compte d’utilisateur de votre tooJive AD Azure API de configuration et configurez hello toocreate du service de configuration, de mettre à jour et de désactiver les comptes d’utilisateur affecté dans Jive en fonction de l’affectation d’utilisateurs et de groupes dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="55809-122">This section guides you through connecting your Azure AD tooJive's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Jive based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="55809-123">Vous pouvez également choisir tooenabled basé sur SAML Single Sign-On pour Jive, en suivant les instructions hello fournies dans [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="55809-123">You may also choose tooenabled SAML-based Single Sign-On for Jive, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="55809-124">L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que chacune de ces deux fonctionnalités compléte l’autre.</span><span class="sxs-lookup"><span data-stu-id="55809-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning"></a><span data-ttu-id="55809-125">approvisionnement des comptes utilisateur tooconfigure :</span><span class="sxs-lookup"><span data-stu-id="55809-125">tooconfigure user account provisioning:</span></span>

<span data-ttu-id="55809-126">objectif Hello de cette section est toooutline mode tooenable l’approvisionnement des utilisateurs d’utilisateur Active Directory de comptes tooJive.</span><span class="sxs-lookup"><span data-stu-id="55809-126">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooJive.</span></span>
<span data-ttu-id="55809-127">Dans le cadre de cette procédure, vous êtes tooprovide requis un jeton de sécurité utilisateur que vous avez besoin de toorequest jive.com.</span><span class="sxs-lookup"><span data-stu-id="55809-127">As part of this procedure, you are required tooprovide a user security token you need toorequest from Jive.com.</span></span>

1. <span data-ttu-id="55809-128">Bonjour [portail Azure](https://portal.azure.com), parcourir toohello **Azure Active Directory > applications d’entreprise > toutes les applications** section.</span><span class="sxs-lookup"><span data-stu-id="55809-128">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="55809-129">Si vous avez déjà configuré Jive pour l’authentification unique, recherchez votre instance de Jive à l’aide du champ de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="55809-129">If you have already configured Jive for single sign-on, search for your instance of Jive using hello search field.</span></span> <span data-ttu-id="55809-130">Sinon, sélectionnez **ajouter** et recherchez **Jive** dans la galerie d’applications hello.</span><span class="sxs-lookup"><span data-stu-id="55809-130">Otherwise, select **Add** and search for **Jive** in hello application gallery.</span></span> <span data-ttu-id="55809-131">Sélectionnez Jive à partir des résultats de recherche hello et ajoutez-le tooyour la liste des applications.</span><span class="sxs-lookup"><span data-stu-id="55809-131">Select Jive from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="55809-132">Sélectionnez votre instance de Jive, puis hello **Provisioning** onglet.</span><span class="sxs-lookup"><span data-stu-id="55809-132">Select your instance of Jive, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="55809-133">Ensemble hello **Mode d’approvisionnement** trop**automatique**.</span><span class="sxs-lookup"><span data-stu-id="55809-133">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![approvisionnement](./media/active-directory-saas-jive-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="55809-135">Sous hello **informations d’identification administrateur** section, fournissez hello suivant les paramètres de configuration :</span><span class="sxs-lookup"><span data-stu-id="55809-135">Under hello **Admin Credentials** section, provide hello following configuration settings:</span></span>
   
    <span data-ttu-id="55809-136">a.</span><span class="sxs-lookup"><span data-stu-id="55809-136">a.</span></span> <span data-ttu-id="55809-137">Bonjour **nom d’utilisateur Admin Jive** zone de texte, tapez un Jive compte nom a hello **administrateur système** profil dans Jive.com attribué.</span><span class="sxs-lookup"><span data-stu-id="55809-137">In hello **Jive Admin User Name** textbox, type a Jive account name that has hello **System Administrator** profile in Jive.com assigned.</span></span>
   
    <span data-ttu-id="55809-138">b.</span><span class="sxs-lookup"><span data-stu-id="55809-138">b.</span></span> <span data-ttu-id="55809-139">Bonjour **mot de passe administrateur Jive** zone de texte, un mot de passe type hello pour ce compte.</span><span class="sxs-lookup"><span data-stu-id="55809-139">In hello **Jive Admin Password** textbox, type hello password for this account.</span></span>
   
    <span data-ttu-id="55809-140">c.</span><span class="sxs-lookup"><span data-stu-id="55809-140">c.</span></span> <span data-ttu-id="55809-141">Bonjour **URL du client Jive** zone de texte, tapez l’URL client Jive hello.</span><span class="sxs-lookup"><span data-stu-id="55809-141">In hello **Jive Tenant URL** textbox, type hello Jive tenant URL.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="55809-142">URL de locataire Jive Hello est utilisé par votre toolog d’organisation dans tooJive.</span><span class="sxs-lookup"><span data-stu-id="55809-142">hello Jive tenant URL is URL that is used by your organization toolog in tooJive.</span></span>  
      > <span data-ttu-id="55809-143">En règle générale, les URL hello a hello suivant le format : **www.\< organisation\>. jive.com**.</span><span class="sxs-lookup"><span data-stu-id="55809-143">Typically, hello URL has hello following format: **www.\<organization\>.jive.com**.</span></span>          

6. <span data-ttu-id="55809-144">Bonjour portail Azure, cliquez sur **tester la connexion** tooensure AD Azure peut se connecter tooyour Jive application.</span><span class="sxs-lookup"><span data-stu-id="55809-144">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Jive app.</span></span>

7. <span data-ttu-id="55809-145">Entrez hello adresse de messagerie d’une personne ou un groupe qui doit recevoir des notifications d’erreur approvisionnement hello **courrier électronique de Notification** champ et la case à cocher hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="55809-145">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox below.</span></span>

8. <span data-ttu-id="55809-146">Cliquez sur **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="55809-146">Click **Save.**</span></span>

9. <span data-ttu-id="55809-147">Sous la section des mappages de hello, sélectionnez **tooJive de synchronisation Azure Active Directory Users.**</span><span class="sxs-lookup"><span data-stu-id="55809-147">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooJive.**</span></span>

10. <span data-ttu-id="55809-148">Bonjour **des mappages d’attributs** section, passez en revue les attributs utilisateur hello qui sont synchronisés à partir d’Azure AD tooJive.</span><span class="sxs-lookup"><span data-stu-id="55809-148">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooJive.</span></span> <span data-ttu-id="55809-149">Hello attributs sélectionnés en tant que **correspondance** propriétés sont des comptes d’utilisateur hello toomatch utilisés dans Jive pour les opérations de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="55809-149">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Jive for update operations.</span></span> <span data-ttu-id="55809-150">Sélectionnez toocommit de bouton hello enregistrer toutes les modifications.</span><span class="sxs-lookup"><span data-stu-id="55809-150">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="55809-151">tooenable hello service de configuration d’Azure AD pour Jive, modification hello **état d’approvisionnement** trop**sur** Bonjour section de paramètres</span><span class="sxs-lookup"><span data-stu-id="55809-151">tooenable hello Azure AD provisioning service for Jive, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

12. <span data-ttu-id="55809-152">Cliquez sur **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="55809-152">Click **Save.**</span></span>

<span data-ttu-id="55809-153">Il démarre la synchronisation initiale d’utilisateurs et/ou groupes affectés tooJive Bonjour les utilisateurs et la section groupes de hello.</span><span class="sxs-lookup"><span data-stu-id="55809-153">It starts hello initial synchronization of any users and/or groups assigned tooJive in hello Users and Groups section.</span></span> <span data-ttu-id="55809-154">la synchronisation initiale Hello prend tooperform plus de temps que les synchronisations suivantes, qui se produisent toutes les 20 minutes environ tant que service de hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="55809-154">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="55809-155">Vous pouvez utiliser hello **détails de synchronisation** section toomonitor cours et suivre des rapports d’activité tooprovisioning des liens, qui décrivent toutes les actions effectuées par hello mise en service du service dans votre application de Jive.</span><span class="sxs-lookup"><span data-stu-id="55809-155">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Jive app.</span></span>

<span data-ttu-id="55809-156">Vous pouvez à présent créer un compte de test.</span><span class="sxs-lookup"><span data-stu-id="55809-156">You can now create a test account.</span></span> <span data-ttu-id="55809-157">Attendez que les minutes too20 tooverify hello compte a été synchronisé tooJive.</span><span class="sxs-lookup"><span data-stu-id="55809-157">Wait for up too20 minutes tooverify that hello account has been synchronized tooJive.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="55809-158">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="55809-158">Additional resources</span></span>

* [<span data-ttu-id="55809-159">Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise</span><span class="sxs-lookup"><span data-stu-id="55809-159">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="55809-160">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="55809-160">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="55809-161">Configurer l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="55809-161">Configure Single Sign-on</span></span>](active-directory-saas-jive-tutorial.md)