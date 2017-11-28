---
title: "Didacticiel : configurer Workplace by Facebook pour l’approvisionnement des utilisateurs | Documents Microsoft"
description: "Découvrez comment tooautomatically approvisionner et configurer des comptes d’utilisateurs tooWorkplace Azure AD par Facebook."
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
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 33d294dbc8f441b29138408b3c9ca41f2141f8af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configure-workplace-by-facebook-for-user-provisioning"></a><span data-ttu-id="9c5cc-103">Didactiel : configurer Workplace by Facebook pour l’approvisionnement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="9c5cc-103">Tutorial: Configure Workplace by Facebook for user provisioning</span></span>

<span data-ttu-id="9c5cc-104">Ce didacticiel montre que vous hello tooautomatically nécessaire d’étapes configurer et annuler la configuration des comptes d’utilisateur de tooWorkplace d’Azure Active Directory (Azure AD) par Facebook.</span><span class="sxs-lookup"><span data-stu-id="9c5cc-104">This tutorial shows you hello steps necessary tooautomatically provision and de-provision user accounts from Azure Active Directory (Azure AD) tooWorkplace by Facebook.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9c5cc-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9c5cc-105">Prerequisites</span></span>

<span data-ttu-id="9c5cc-106">tooconfigure intégration d’Azure AD avec l’espace de travail par Facebook, hello éléments suivants sont nécessaires :</span><span class="sxs-lookup"><span data-stu-id="9c5cc-106">tooconfigure Azure AD integration with Workplace by Facebook, you need hello following:</span></span>

- <span data-ttu-id="9c5cc-107">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="9c5cc-107">An Azure AD subscription</span></span>
- <span data-ttu-id="9c5cc-108">Un abonnement Workplace by Facebook pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="9c5cc-108">A Workplace by Facebook single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="9c5cc-109">étapes de hello tootest dans ce didacticiel, suivez ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="9c5cc-109">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="9c5cc-110">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="9c5cc-110">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9c5cc-111">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir une [offre d’essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9c5cc-111">If you don't have an Azure AD trial environment, you can get a [one-month trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="assign-users-tooworkplace-by-facebook"></a><span data-ttu-id="9c5cc-112">Affecter les utilisateurs des tooWorkplace par Facebook</span><span class="sxs-lookup"><span data-stu-id="9c5cc-112">Assign users tooWorkplace by Facebook</span></span>

<span data-ttu-id="9c5cc-113">Azure AD utilise un concept appelé toodetermine « affectations » les utilisateurs qui doivent recevoir l’accès tooselected applications.</span><span class="sxs-lookup"><span data-stu-id="9c5cc-113">Azure AD uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="9c5cc-114">Dans le contexte de hello de configuration de compte automatique d’utilisateurs, seuls les utilisateurs de hello et les groupes qui ont été attribuées application tooan dans Azure AD sont synchronisés.</span><span class="sxs-lookup"><span data-stu-id="9c5cc-114">In hello context of automatic user account provisioning, only hello users and groups that have been assigned tooan application in Azure AD are synchronized.</span></span>

<span data-ttu-id="9c5cc-115">Avant de configurer et activer hello service, l’approvisionnement décider quels utilisateurs et groupes dans Azure AD représentent les utilisateurs de hello qui a besoin d’accès tooyour espace de travail par application Facebook.</span><span class="sxs-lookup"><span data-stu-id="9c5cc-115">Before configuring and enabling hello provisioning service, decide what users and groups in Azure AD represent hello users who need access tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="9c5cc-116">Vous pouvez ensuite affecter ces tooyour utilisateurs espace de travail par application Facebook en suivant hello les instructions de [affecter un utilisateur ou groupe d’applications d’entreprise tooan](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="9c5cc-116">You can then assign these users tooyour Workplace by Facebook app by following hello instructions in [Assign a user or group tooan enterprise app](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).</span></span>

>[!IMPORTANT]
>*   <span data-ttu-id="9c5cc-117">Hello de test configuration de configuration en affectant une seule tooWorkplace d’utilisateur Azure AD par Facebook.</span><span class="sxs-lookup"><span data-stu-id="9c5cc-117">Test hello provisioning configuration by assigning a single Azure AD user tooWorkplace by Facebook.</span></span> <span data-ttu-id="9c5cc-118">Affectez des groupes et des utilisateurs supplémentaires ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="9c5cc-118">Assign additional users and groups later.</span></span>
>*   <span data-ttu-id="9c5cc-119">Lorsque vous affectez un tooWorkplace utilisateur par Facebook, vous devez sélectionner un rôle d’utilisateur valide.</span><span class="sxs-lookup"><span data-stu-id="9c5cc-119">When you assign a user tooWorkplace by Facebook, you must select a valid user role.</span></span> <span data-ttu-id="9c5cc-120">rôle d’accès par défaut Hello ne fonctionne pas pour la configuration.</span><span class="sxs-lookup"><span data-stu-id="9c5cc-120">hello Default Access role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="9c5cc-121">Activer l’approvisionnement automatique des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="9c5cc-121">Enable automated user provisioning</span></span>

<span data-ttu-id="9c5cc-122">Cette section vous guide tout au long de la connexion de votre compte d’utilisateur Azure AD toohello provisionnement des API d’espace de travail par Facebook.</span><span class="sxs-lookup"><span data-stu-id="9c5cc-122">This section guides you through connecting your Azure AD toohello user account provisioning API of Workplace by Facebook.</span></span> <span data-ttu-id="9c5cc-123">Vous apprendrez également comment tooconfigure hello configuration service toocreate, mettre à jour et désactiver les comptes d’utilisateur affecté dans l’espace de travail par Facebook.</span><span class="sxs-lookup"><span data-stu-id="9c5cc-123">You also learn how tooconfigure hello provisioning service toocreate, update, and disable assigned user accounts in Workplace by Facebook.</span></span> <span data-ttu-id="9c5cc-124">Cela est fondé sur l’affectation d’utilisateurs et de groupes dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9c5cc-124">This is based on user and group assignment in Azure AD.</span></span>

>[!Tip]
><span data-ttu-id="9c5cc-125">Vous pouvez également choisir tooenabled authentification SAML pour l’espace de travail par Facebook, en suivant les instructions hello prévues hello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9c5cc-125">You can also choose tooenabled SAML-based SSO for Workplace by Facebook, by following hello instructions provided in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="9c5cc-126">L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que ces deux fonctionnalités se complètent.</span><span class="sxs-lookup"><span data-stu-id="9c5cc-126">SSO can be configured independently of automatic provisioning, though these two features complement each other.</span></span>

### <a name="configure-user-account-provisioning-tooworkplace-by-facebook-in-azure-ad"></a><span data-ttu-id="9c5cc-127">Configurer le compte d’utilisateur de configuration tooWorkplace par Facebook dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="9c5cc-127">Configure user account provisioning tooWorkplace by Facebook in Azure AD</span></span>

<span data-ttu-id="9c5cc-128">Azure prend en charge d’AD hello capacité tooautomatically synchroniser détails du compte de hello affecté tooWorkplace utilisateurs par Facebook.</span><span class="sxs-lookup"><span data-stu-id="9c5cc-128">Azure AD supports hello ability tooautomatically synchronize hello account details of assigned users tooWorkplace by Facebook.</span></span> <span data-ttu-id="9c5cc-129">La synchronisation automatique permet d’espace de travail par les données de hello Facebook tooget lui tooauthorize des utilisateurs pour l’accès, avant leur tentative toosign dans pour hello première fois.</span><span class="sxs-lookup"><span data-stu-id="9c5cc-129">This automatic synchronization enables Workplace by Facebook tooget hello data it needs tooauthorize users for access, before them attempting toosign in for hello first time.</span></span> <span data-ttu-id="9c5cc-130">Elle annule également l’approvisionnement des utilisateurs à Workplace by Facebook lorsque l’accès a été révoqué dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9c5cc-130">It also de-provisions users from Workplace by Facebook when access has been revoked in Azure AD.</span></span>

1. <span data-ttu-id="9c5cc-131">Bonjour [portail Azure](https://portal.azure.com), sélectionnez **Azure Active Directory** > **applications d’entreprise** > **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="9c5cc-131">In hello [Azure portal](https://portal.azure.com), select **Azure Active Directory** > **Enterprise Apps** > **All applications**.</span></span>

2. <span data-ttu-id="9c5cc-132">Si vous avez déjà configuré l’espace de travail par Facebook pour l’authentification unique, recherchez votre instance de l’espace de travail par Facebook à l’aide du champ de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="9c5cc-132">If you have already configured Workplace by Facebook for SSO, search for your instance of Workplace by Facebook by using hello search field.</span></span> <span data-ttu-id="9c5cc-133">Sinon, sélectionnez **ajouter** et recherchez **espace de travail par Facebook** dans la galerie d’applications hello.</span><span class="sxs-lookup"><span data-stu-id="9c5cc-133">Otherwise, select **Add** and search for **Workplace by Facebook** in hello application gallery.</span></span> <span data-ttu-id="9c5cc-134">Sélectionnez **espace de travail par Facebook** de hello résultats de la recherche, puis l’ajouter tooyour la liste des applications.</span><span class="sxs-lookup"><span data-stu-id="9c5cc-134">Select **Workplace by Facebook** from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="9c5cc-135">Sélectionnez votre instance de l’espace de travail par Facebook, puis hello **Provisioning** onglet.</span><span class="sxs-lookup"><span data-stu-id="9c5cc-135">Select your instance of Workplace by Facebook, and then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="9c5cc-136">Définissez **Mode d’approvisionnement** trop**automatique**.</span><span class="sxs-lookup"><span data-stu-id="9c5cc-136">Set **Provisioning Mode** too**Automatic**.</span></span> 

    ![Capture instantanée des options d’approvisionnement de Workspace by Facebook](./media/active-directory-saas-facebook-at-work-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="9c5cc-138">Sous hello **informations d’identification administrateur** section, entrez hello **Secret jeton** et hello **URL de client** votre espace de travail par un administrateur de Facebook.</span><span class="sxs-lookup"><span data-stu-id="9c5cc-138">Under hello **Admin Credentials** section, enter hello **Secret Token** and hello **Tenant URL** of your Workplace by Facebook administrator.</span></span>

6. <span data-ttu-id="9c5cc-139">Bonjour portail Azure, sélectionnez **tester la connexion** tooensure Azure AD peut se connecter tooyour espace de travail par application Facebook.</span><span class="sxs-lookup"><span data-stu-id="9c5cc-139">In hello Azure portal, select **Test Connection** tooensure Azure AD can connect tooyour Workplace by Facebook app.</span></span> <span data-ttu-id="9c5cc-140">Si la connexion de hello échoue, assurez-vous que votre espace de travail par compte Facebook dispose d’autorisations d’administrateur d’équipe.</span><span class="sxs-lookup"><span data-stu-id="9c5cc-140">If hello connection fails, ensure that your Workplace by Facebook account has Team Admin permissions.</span></span>

7. <span data-ttu-id="9c5cc-141">Entrez hello adresse de messagerie d’une personne ou un groupe qui doit recevoir des notifications d’erreur approvisionnement hello **courrier électronique de Notification** champ et la case à cocher hello.</span><span class="sxs-lookup"><span data-stu-id="9c5cc-141">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello check box.</span></span>

8. <span data-ttu-id="9c5cc-142">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="9c5cc-142">Select **Save**.</span></span>

9. <span data-ttu-id="9c5cc-143">Sous la section des mappages de hello, sélectionnez **tooWorkplace de synchronisation Azure Active Directory Users par Facebook**.</span><span class="sxs-lookup"><span data-stu-id="9c5cc-143">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooWorkplace by Facebook**.</span></span>

10. <span data-ttu-id="9c5cc-144">Bonjour **des mappages d’attributs** section, passez en revue les attributs utilisateur hello sont synchronisées à partir d’Azure AD tooWorkplace par Facebook.</span><span class="sxs-lookup"><span data-stu-id="9c5cc-144">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooWorkplace by Facebook.</span></span> <span data-ttu-id="9c5cc-145">Hello attributs sélectionnés en tant que **correspondance** propriétés sont des comptes d’utilisateur hello toomatch utilisé dans l’espace de travail par Facebook pour les opérations de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="9c5cc-145">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Workplace by Facebook for update operations.</span></span> <span data-ttu-id="9c5cc-146">sélectionner de toutes les modifications, toocommit **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="9c5cc-146">toocommit any changes, select **Save**.</span></span>

11. <span data-ttu-id="9c5cc-147">tooenable hello service de configuration Azure AD pour l’espace de travail par Facebook, Bonjour **paramètres** section, modifier hello **état d’approvisionnement** trop**sur**.</span><span class="sxs-lookup"><span data-stu-id="9c5cc-147">tooenable hello Azure AD provisioning service for Workplace by Facebook, in hello **Settings** section, change hello **Provisioning Status** too**On**.</span></span>

12. <span data-ttu-id="9c5cc-148">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="9c5cc-148">Select **Save**.</span></span>

<span data-ttu-id="9c5cc-149">Pour plus d’informations sur la façon de tooconfigure automatique de configuration, consultez [hello Facebook documentation](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers).</span><span class="sxs-lookup"><span data-stu-id="9c5cc-149">For more information on how tooconfigure automatic provisioning, see [hello Facebook documentation](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers).</span></span>

<span data-ttu-id="9c5cc-150">Vous pouvez à présent créer un compte de test.</span><span class="sxs-lookup"><span data-stu-id="9c5cc-150">You can now create a test account.</span></span> <span data-ttu-id="9c5cc-151">Attendez que les minutes too20 tooverify hello compte a été synchronisé tooWorkplace par Facebook.</span><span class="sxs-lookup"><span data-stu-id="9c5cc-151">Wait for up too20 minutes tooverify that hello account has been synchronized tooWorkplace by Facebook.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9c5cc-152">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="9c5cc-152">Additional resources</span></span>

* [<span data-ttu-id="9c5cc-153">Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise</span><span class="sxs-lookup"><span data-stu-id="9c5cc-153">Managing user account provisioning for enterprise apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9c5cc-154">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="9c5cc-154">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="9c5cc-155">Configurer l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="9c5cc-155">Configure single sign-on</span></span>](active-directory-saas-facebook-at-work-tutorial.md)

