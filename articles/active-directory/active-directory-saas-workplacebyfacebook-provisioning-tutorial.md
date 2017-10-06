---
title: "Didacticiel : Intégration d’Azure Active Directory à Workplace par Facebook | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et l’espace de travail par Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6341e67e-8ce6-42dc-a4ea-7295904a53ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 551ec353a5ec1da936373587688c299a6f4acca7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-workplace-by-facebook-for-user-provisioning"></a><span data-ttu-id="872e0-103">Didacticiel : Configuration de Workplace by Facebook pour l’approvisionnement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="872e0-103">Tutorial: Configuring Workplace by Facebook for User Provisioning</span></span>

<span data-ttu-id="872e0-104">objectif Hello de ce didacticiel est tooshow vous hello étapes que vous devez tooperform dans l’espace de travail par Facebook et Azure AD tooautomatically approvisionner et configurer des comptes d’utilisateur de tooWorkplace d’Azure AD par Facebook.</span><span class="sxs-lookup"><span data-stu-id="872e0-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Workplace by Facebook and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooWorkplace by Facebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="872e0-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="872e0-105">Prerequisites</span></span>

<span data-ttu-id="872e0-106">tooconfigure intégration d’Azure AD avec l’espace de travail par Facebook, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="872e0-106">tooconfigure Azure AD integration with Workplace by Facebook, you need hello following items:</span></span>

- <span data-ttu-id="872e0-107">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="872e0-107">An Azure AD subscription</span></span>
- <span data-ttu-id="872e0-108">Un abonnement Workplace by Facebook pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="872e0-108">A Workplace by Facebook single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="872e0-109">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="872e0-109">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="872e0-110">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="872e0-110">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="872e0-111">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="872e0-111">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="872e0-112">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="872e0-112">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="assigning-users-tooworkplace-by-facebook"></a><span data-ttu-id="872e0-113">Affectation de tooWorkplace les utilisateurs par Facebook</span><span class="sxs-lookup"><span data-stu-id="872e0-113">Assigning users tooWorkplace by Facebook</span></span>

<span data-ttu-id="872e0-114">Azure Active Directory utilise un concept appelé toodetermine « affectations » les utilisateurs qui doivent recevoir l’accès tooselected applications.</span><span class="sxs-lookup"><span data-stu-id="872e0-114">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="872e0-115">Dans le contexte de hello de configuration de compte automatique d’utilisateurs, seuls les utilisateurs de hello et les groupes qui ont été « affectés » application tooan dans Azure AD est synchronisé.</span><span class="sxs-lookup"><span data-stu-id="872e0-115">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="872e0-116">Avant de configurer et de l’activation de hello service de configuration, vous devez toodecide quels utilisateurs ou des groupes dans Azure AD représentent hello des utilisateurs qui doivent accéder aux tooyour espace de travail par application Facebook.</span><span class="sxs-lookup"><span data-stu-id="872e0-116">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="872e0-117">Après choisi, vous pouvez attribuer ces tooyour utilisateurs espace de travail par application Facebook en suivant les instructions hello ici :</span><span class="sxs-lookup"><span data-stu-id="872e0-117">Once decided, you can assign these users tooyour Workplace by Facebook app by following hello instructions here:</span></span>

[<span data-ttu-id="872e0-118">Affecter une application d’entreprise tooan utilisateur ou un groupe</span><span class="sxs-lookup"><span data-stu-id="872e0-118">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-tooworkplace-by-facebook"></a><span data-ttu-id="872e0-119">Conseils importants pour l’assignation tooWorkplace utilisateurs par Facebook</span><span class="sxs-lookup"><span data-stu-id="872e0-119">Important tips for assigning users tooWorkplace by Facebook</span></span>

*   <span data-ttu-id="872e0-120">Il est recommandé qu’un seul utilisateur Azure AD est affecté au tooWorkplace Facebook tootest hello est mise en service de configuration.</span><span class="sxs-lookup"><span data-stu-id="872e0-120">It is recommended that a single Azure AD user is assigned tooWorkplace by Facebook tootest hello provisioning configuration.</span></span> <span data-ttu-id="872e0-121">Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="872e0-121">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="872e0-122">Lorsque vous affectez un tooWorkplace utilisateur par Facebook, vous devez sélectionner un rôle d’utilisateur valide.</span><span class="sxs-lookup"><span data-stu-id="872e0-122">When assigning a user tooWorkplace by Facebook, you must select a valid user role.</span></span> <span data-ttu-id="872e0-123">rôle de « Accès par défaut » Hello ne fonctionne pas pour la configuration.</span><span class="sxs-lookup"><span data-stu-id="872e0-123">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="872e0-124">Activer l’approvisionnement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="872e0-124">Enable User Provisioning</span></span>

<span data-ttu-id="872e0-125">Cette section vous guide à travers de la connexion de votre tooWorkplace Azure AD par compte d’utilisateur de Facebook à l’API de configuration et configurez hello toocreate du service de configuration, de mettre à jour et de désactiver les comptes d’utilisateur affecté dans l’espace de travail par Facebook en fonction de l’utilisateur et de groupe affectation dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="872e0-125">This section guides you through connecting your Azure AD tooWorkplace by Facebook's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Workplace by Facebook based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="872e0-126">Vous pouvez également choisir tooenabled basé sur SAML Single Sign-On pour l’espace de travail par Facebook, suivant les instructions hello fournies dans [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="872e0-126">You may also choose tooenabled SAML-based Single Sign-On for Workplace by Facebook, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="872e0-127">L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que chacune de ces deux fonctionnalités compléte l’autre.</span><span class="sxs-lookup"><span data-stu-id="872e0-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning-tooworkplace-by-facebook-in-azure-ad"></a><span data-ttu-id="872e0-128">compte d’utilisateur tooconfigure configuration tooWorkplace par Facebook dans Azure AD :</span><span class="sxs-lookup"><span data-stu-id="872e0-128">tooconfigure user account provisioning tooWorkplace by Facebook in Azure AD:</span></span>

<span data-ttu-id="872e0-129">objectif Hello de cette section est toooutline comment tooenable configuration d’utilisateur Active Directory de comptes de tooWorkplace par Facebook.</span><span class="sxs-lookup"><span data-stu-id="872e0-129">hello objective of this section is toooutline how tooenable provisioning of Active Directory user accounts tooWorkplace by Facebook.</span></span>

<span data-ttu-id="872e0-130">Azure prend en charge d’AD hello capacité tooautomatically synchroniser détails du compte de hello affecté tooWorkplace utilisateurs par Facebook.</span><span class="sxs-lookup"><span data-stu-id="872e0-130">Azure AD supports hello ability tooautomatically synchronize hello account details of assigned users tooWorkplace by Facebook.</span></span> <span data-ttu-id="872e0-131">La synchronisation automatique permet d’espace de travail par les données de hello Facebook tooget lui tooauthorize des utilisateurs pour l’accès, avant leur tentative toosign dans pour hello première fois.</span><span class="sxs-lookup"><span data-stu-id="872e0-131">This automatic synchronization enables Workplace by Facebook tooget hello data it needs tooauthorize users for access, before them attempting toosign in for hello first time.</span></span> <span data-ttu-id="872e0-132">Elle annule également l’approvisionnement des utilisateurs à Workplace by Facebook lorsque l’accès a été révoqué dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="872e0-132">It also de-provisions users from Workplace by Facebook when access has been revoked in Azure AD.</span></span>

1. <span data-ttu-id="872e0-133">Bonjour [portail Azure](https://portal.azure.com), parcourir toohello **Azure Active Directory** > **applications d’entreprise** > **detouteslesapplications** section.</span><span class="sxs-lookup"><span data-stu-id="872e0-133">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory** > **Enterprise Apps** > **All applications** section.</span></span>

2. <span data-ttu-id="872e0-134">Si vous avez déjà configuré l’espace de travail par Facebook pour l’authentification unique, recherchez votre instance de l’espace de travail par Facebook à l’aide du champ de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="872e0-134">If you have already configured Workplace by Facebook for single sign-on, search for your instance of Workplace by Facebook using hello search field.</span></span> <span data-ttu-id="872e0-135">Sinon, sélectionnez **ajouter** et recherchez **espace de travail par Facebook** dans la galerie d’applications hello.</span><span class="sxs-lookup"><span data-stu-id="872e0-135">Otherwise, select **Add** and search for **Workplace by Facebook** in hello application gallery.</span></span> <span data-ttu-id="872e0-136">Sélectionnez l’espace de travail par Facebook hello résultats de recherche et l’ajouter tooyour la liste des applications.</span><span class="sxs-lookup"><span data-stu-id="872e0-136">Select Workplace by Facebook from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="872e0-137">Sélectionnez votre instance de l’espace de travail par Facebook, puis hello **Provisioning** onglet.</span><span class="sxs-lookup"><span data-stu-id="872e0-137">Select your instance of Workplace by Facebook, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="872e0-138">Ensemble hello **Mode d’approvisionnement** trop**automatique**.</span><span class="sxs-lookup"><span data-stu-id="872e0-138">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![approvisionnement](./media/active-directory-saas-workplacebyfacebook-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="872e0-140">Sous hello **informations d’identification administrateur** section, entrez hello jeton Secret et hello URL de client de votre espace de travail par un administrateur de Facebook.</span><span class="sxs-lookup"><span data-stu-id="872e0-140">Under hello **Admin Credentials** section, enter hello Secret Token and hello Tenant URL of your Workplace by Facebook administrator.</span></span>

6. <span data-ttu-id="872e0-141">Bonjour portail Azure, cliquez sur **tester la connexion** tooensure Azure AD peut se connecter tooyour espace de travail par application Facebook.</span><span class="sxs-lookup"><span data-stu-id="872e0-141">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="872e0-142">Si la connexion de hello échoue, vérifiez que votre espace de travail par compte Facebook a des autorisations d’administrateur d’équipe.</span><span class="sxs-lookup"><span data-stu-id="872e0-142">If hello connection fails, ensure your Workplace by Facebook account has Team Admin permissions.</span></span>

7. <span data-ttu-id="872e0-143">Entrez hello adresse de messagerie d’une personne ou un groupe qui doit recevoir des notifications d’erreur approvisionnement hello **courrier électronique de Notification** champ et la case à cocher hello.</span><span class="sxs-lookup"><span data-stu-id="872e0-143">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

8. <span data-ttu-id="872e0-144">Cliquez sur **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="872e0-144">Click **Save.**</span></span>

9. <span data-ttu-id="872e0-145">Sous la section des mappages de hello, sélectionnez **tooWorkplace de synchronisation Azure Active Directory Users par Facebook.**</span><span class="sxs-lookup"><span data-stu-id="872e0-145">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooWorkplace by Facebook.**</span></span>

10. <span data-ttu-id="872e0-146">Bonjour **des mappages d’attributs** section, passez en revue les attributs utilisateur hello sont synchronisées à partir d’Azure AD tooWorkplace par Facebook.</span><span class="sxs-lookup"><span data-stu-id="872e0-146">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooWorkplace by Facebook.</span></span> <span data-ttu-id="872e0-147">Hello attributs sélectionnés en tant que **correspondance** propriétés sont des comptes d’utilisateur hello toomatch utilisé dans l’espace de travail par Facebook pour les opérations de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="872e0-147">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Workplace by Facebook for update operations.</span></span> <span data-ttu-id="872e0-148">Sélectionnez toocommit de bouton hello enregistrer toutes les modifications.</span><span class="sxs-lookup"><span data-stu-id="872e0-148">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="872e0-149">tooenable hello service de configuration d’Azure AD pour l’espace de travail par Facebook, modification hello **état d’approvisionnement** trop**sur** Bonjour **paramètres** section</span><span class="sxs-lookup"><span data-stu-id="872e0-149">tooenable hello Azure AD provisioning service for Workplace by Facebook, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="872e0-150">Cliquez sur **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="872e0-150">Click **Save.**</span></span>

<span data-ttu-id="872e0-151">Pour plus d’informations sur la façon de tooconfigure automatique de configuration, consultez [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span><span class="sxs-lookup"><span data-stu-id="872e0-151">For more information on how tooconfigure automatic provisioning, see [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)</span></span>

<span data-ttu-id="872e0-152">Vous pouvez à présent créer un compte de test.</span><span class="sxs-lookup"><span data-stu-id="872e0-152">You can now create a test account.</span></span> <span data-ttu-id="872e0-153">Attendez que les minutes too20 tooverify hello compte a été synchronisé tooWorkplace par Facebook.</span><span class="sxs-lookup"><span data-stu-id="872e0-153">Wait for up too20 minutes tooverify that hello account has been synchronized tooWorkplace by Facebook.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="872e0-154">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="872e0-154">Additional resources</span></span>

* [<span data-ttu-id="872e0-155">Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise</span><span class="sxs-lookup"><span data-stu-id="872e0-155">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="872e0-156">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="872e0-156">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="872e0-157">Configurer l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="872e0-157">Configure Single Sign-on</span></span>](active-directory-saas-workplacebyfacebook-tutorial.md)

