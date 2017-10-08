---
title: "Didacticiel : Intégration d’Azure Active Directory à Netsuite | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory à Netsuite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8a6d3994-ee33-4a6f-b0a2-9d0389467f16
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 5bb2989c1296b9f2abc9e8c84855731adc484aab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-netsuite-for-automatic-user-provisioning"></a><span data-ttu-id="64e71-103">Didacticiel : Configuration de Netsuite pour l’approvisionnement automatique d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="64e71-103">Tutorial: Configuring Netsuite for Automatic User Provisioning</span></span>

<span data-ttu-id="64e71-104">objectif Hello de ce didacticiel est tooshow vous hello étapes que vous devez tooperform dans Netsuite et Azure AD tooautomatically approvisionner et configurer des comptes d’utilisateur à partir d’Azure AD tooNetsuite.</span><span class="sxs-lookup"><span data-stu-id="64e71-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Netsuite and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooNetsuite.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64e71-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="64e71-105">Prerequisites</span></span>

<span data-ttu-id="64e71-106">scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="64e71-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="64e71-107">Un locataire Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="64e71-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="64e71-108">Un abonnement Netsuite pour lequel l’authentification unique est activée.</span><span class="sxs-lookup"><span data-stu-id="64e71-108">A Netsuite single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="64e71-109">Un compte utilisateur dans Netsuite avec les autorisations d’administrateur d’équipe.</span><span class="sxs-lookup"><span data-stu-id="64e71-109">A user account in Netsuite with Team Admin permissions.</span></span>

## <a name="assigning-users-toonetsuite"></a><span data-ttu-id="64e71-110">Affectation d’utilisateurs tooNetsuite</span><span class="sxs-lookup"><span data-stu-id="64e71-110">Assigning users tooNetsuite</span></span>

<span data-ttu-id="64e71-111">Azure Active Directory utilise un concept appelé toodetermine « affectations » les utilisateurs qui doivent recevoir l’accès tooselected applications.</span><span class="sxs-lookup"><span data-stu-id="64e71-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="64e71-112">Dans le contexte de hello de configuration de compte automatique d’utilisateurs, seuls les utilisateurs de hello et les groupes qui ont été « affectés » application tooan dans Azure AD sont synchronisés.</span><span class="sxs-lookup"><span data-stu-id="64e71-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD are synchronized.</span></span>

<span data-ttu-id="64e71-113">Avant de configurer et de l’activation de hello service de configuration, vous devez toodecide quels utilisateurs ou des groupes dans Azure AD représentent hello utilisateurs qui doivent accéder aux tooyour Netsuite application.</span><span class="sxs-lookup"><span data-stu-id="64e71-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Netsuite app.</span></span> <span data-ttu-id="64e71-114">Après choisi, vous pouvez attribuer à ces applications de Netsuite tooyour les utilisateurs en suivant les instructions hello ici :</span><span class="sxs-lookup"><span data-stu-id="64e71-114">Once decided, you can assign these users tooyour Netsuite app by following hello instructions here:</span></span>

[<span data-ttu-id="64e71-115">Affecter une application d’entreprise tooan utilisateur ou un groupe</span><span class="sxs-lookup"><span data-stu-id="64e71-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toonetsuite"></a><span data-ttu-id="64e71-116">Conseils importants pour l’affectation d’utilisateurs tooNetsuite</span><span class="sxs-lookup"><span data-stu-id="64e71-116">Important tips for assigning users tooNetsuite</span></span>

*   <span data-ttu-id="64e71-117">Il est recommandé qu’un seul utilisateur Azure AD est attribué tooNetsuite tootest hello est mise en service de configuration.</span><span class="sxs-lookup"><span data-stu-id="64e71-117">It is recommended that a single Azure AD user is assigned tooNetsuite tootest hello provisioning configuration.</span></span> <span data-ttu-id="64e71-118">Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="64e71-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="64e71-119">Lorsque vous affectez un tooNetsuite d’utilisateur, vous devez sélectionner un rôle d’utilisateur valide.</span><span class="sxs-lookup"><span data-stu-id="64e71-119">When assigning a user tooNetsuite, you must select a valid user role.</span></span> <span data-ttu-id="64e71-120">rôle de « Accès par défaut » Hello ne fonctionne pas pour la configuration.</span><span class="sxs-lookup"><span data-stu-id="64e71-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-user-provisioning"></a><span data-ttu-id="64e71-121">Activer l’approvisionnement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="64e71-121">Enable User Provisioning</span></span>

<span data-ttu-id="64e71-122">Cette section vous guide à travers de la connexion du compte d’utilisateur de votre tooNetsuite AD Azure API de configuration et configurez hello toocreate du service de configuration, de mettre à jour et de désactiver les comptes d’utilisateur affecté dans Netsuite en fonction de l’affectation d’utilisateurs et de groupes dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64e71-122">This section guides you through connecting your Azure AD tooNetsuite's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Netsuite based on user and group assignment in Azure AD.</span></span>

> [!TIP] 
> <span data-ttu-id="64e71-123">Vous pouvez également choisir tooenabled basé sur SAML Single Sign-On pour Netsuite, en suivant les instructions hello fournies dans [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="64e71-123">You may also choose tooenabled SAML-based Single Sign-On for Netsuite, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="64e71-124">L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que chacune de ces deux fonctionnalités compléte l’autre.</span><span class="sxs-lookup"><span data-stu-id="64e71-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-user-account-provisioning"></a><span data-ttu-id="64e71-125">approvisionnement des comptes utilisateur tooconfigure :</span><span class="sxs-lookup"><span data-stu-id="64e71-125">tooconfigure user account provisioning:</span></span>

<span data-ttu-id="64e71-126">objectif Hello de cette section est toooutline mode tooenable l’approvisionnement des utilisateurs d’utilisateur Active Directory de comptes tooNetsuite.</span><span class="sxs-lookup"><span data-stu-id="64e71-126">hello objective of this section is toooutline how tooenable user provisioning of Active Directory user accounts tooNetsuite.</span></span>

1. <span data-ttu-id="64e71-127">Bonjour [portail Azure](https://portal.azure.com), parcourir toohello **Azure Active Directory > applications d’entreprise > toutes les applications** section.</span><span class="sxs-lookup"><span data-stu-id="64e71-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="64e71-128">Si vous avez déjà configuré Netsuite pour l’authentification unique, recherchez votre instance de Netsuite à l’aide du champ de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="64e71-128">If you have already configured Netsuite for single sign-on, search for your instance of Netsuite using hello search field.</span></span> <span data-ttu-id="64e71-129">Sinon, sélectionnez **ajouter** et recherchez **Netsuite** dans la galerie d’applications hello.</span><span class="sxs-lookup"><span data-stu-id="64e71-129">Otherwise, select **Add** and search for **Netsuite** in hello application gallery.</span></span> <span data-ttu-id="64e71-130">Sélectionnez Netsuite à partir des résultats de recherche hello et ajoutez-le tooyour la liste des applications.</span><span class="sxs-lookup"><span data-stu-id="64e71-130">Select Netsuite from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="64e71-131">Sélectionnez votre instance de Netsuite, puis hello **Provisioning** onglet.</span><span class="sxs-lookup"><span data-stu-id="64e71-131">Select your instance of Netsuite, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="64e71-132">Ensemble hello **Mode d’approvisionnement** trop**automatique**.</span><span class="sxs-lookup"><span data-stu-id="64e71-132">Set hello **Provisioning Mode** too**Automatic**.</span></span> 

    ![approvisionnement](./media/active-directory-saas-netsuite-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="64e71-134">Sous hello **informations d’identification administrateur** section, fournissez hello suivant les paramètres de configuration :</span><span class="sxs-lookup"><span data-stu-id="64e71-134">Under hello **Admin Credentials** section, provide hello following configuration settings:</span></span>
   
    <span data-ttu-id="64e71-135">a.</span><span class="sxs-lookup"><span data-stu-id="64e71-135">a.</span></span> <span data-ttu-id="64e71-136">Bonjour **nom d’utilisateur Admin** zone de texte, tapez un Netsuite compte nom a hello **administrateur système** profil dans Netsuite.com attribué.</span><span class="sxs-lookup"><span data-stu-id="64e71-136">In hello **Admin User Name** textbox, type a Netsuite account name that has hello **System Administrator** profile in Netsuite.com assigned.</span></span>
   
    <span data-ttu-id="64e71-137">b.</span><span class="sxs-lookup"><span data-stu-id="64e71-137">b.</span></span> <span data-ttu-id="64e71-138">Bonjour **mot de passe administrateur** zone de texte, un mot de passe type hello pour ce compte.</span><span class="sxs-lookup"><span data-stu-id="64e71-138">In hello **Admin Password** textbox, type hello password for this account.</span></span>
      
6. <span data-ttu-id="64e71-139">Bonjour portail Azure, cliquez sur **tester la connexion** tooensure AD Azure peut se connecter tooyour Netsuite application.</span><span class="sxs-lookup"><span data-stu-id="64e71-139">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Netsuite app.</span></span>

7. <span data-ttu-id="64e71-140">Bonjour **Notification par courrier électronique** , entrez l’adresse de messagerie hello d’une personne ou un groupe qui doit recevoir des notifications de d’erreur et case à cocher hello.</span><span class="sxs-lookup"><span data-stu-id="64e71-140">In hello **Notification Email** field, enter hello email address of a person or group who should receive provisioning error notifications, and check hello checkbox.</span></span>

8. <span data-ttu-id="64e71-141">Cliquez sur **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="64e71-141">Click **Save.**</span></span>

9. <span data-ttu-id="64e71-142">Sous la section des mappages de hello, sélectionnez **tooNetsuite de synchronisation Azure Active Directory Users.**</span><span class="sxs-lookup"><span data-stu-id="64e71-142">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooNetsuite.**</span></span>

10. <span data-ttu-id="64e71-143">Bonjour **des mappages d’attributs** section, passez en revue les attributs utilisateur hello qui sont synchronisés à partir d’Azure AD tooNetsuite.</span><span class="sxs-lookup"><span data-stu-id="64e71-143">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooNetsuite.</span></span> <span data-ttu-id="64e71-144">Notez que hello attributs sélectionnés en tant que **correspondance** propriétés sont des comptes d’utilisateur hello toomatch utilisés dans Netsuite pour les opérations de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="64e71-144">Note that hello attributes selected as **Matching** properties are used toomatch hello user accounts in Netsuite for update operations.</span></span> <span data-ttu-id="64e71-145">Sélectionnez toocommit de bouton hello enregistrer toutes les modifications.</span><span class="sxs-lookup"><span data-stu-id="64e71-145">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="64e71-146">tooenable hello service de configuration d’Azure AD pour Netsuite, modification hello **état d’approvisionnement** trop**sur** Bonjour section de paramètres</span><span class="sxs-lookup"><span data-stu-id="64e71-146">tooenable hello Azure AD provisioning service for Netsuite, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

12. <span data-ttu-id="64e71-147">Cliquez sur **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="64e71-147">Click **Save.**</span></span>

<span data-ttu-id="64e71-148">Il démarre la synchronisation initiale d’utilisateurs et/ou groupes affectés tooNetsuite Bonjour les utilisateurs et la section groupes de hello.</span><span class="sxs-lookup"><span data-stu-id="64e71-148">It starts hello initial synchronization of any users and/or groups assigned tooNetsuite in hello Users and Groups section.</span></span> <span data-ttu-id="64e71-149">Notez que la synchronisation initiale hello prend tooperform plus de temps que les synchronisations suivantes, qui se produisent toutes les 20 minutes environ tant que service de hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="64e71-149">Note that hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="64e71-150">Vous pouvez utiliser hello **détails de synchronisation** section toomonitor cours et suivre des rapports d’activité tooprovisioning des liens, qui décrivent toutes les actions effectuées par hello mise en service du service sur votre application Netsuite.</span><span class="sxs-lookup"><span data-stu-id="64e71-150">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Netsuite app.</span></span>

<span data-ttu-id="64e71-151">Vous pouvez à présent créer un compte de test.</span><span class="sxs-lookup"><span data-stu-id="64e71-151">You can now create a test account.</span></span> <span data-ttu-id="64e71-152">Attendez que les minutes too20 tooverify hello compte a été synchronisé tooNetsuite.</span><span class="sxs-lookup"><span data-stu-id="64e71-152">Wait for up too20 minutes tooverify that hello account has been synchronized tooNetsuite.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="64e71-153">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="64e71-153">Additional resources</span></span>

* [<span data-ttu-id="64e71-154">Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise</span><span class="sxs-lookup"><span data-stu-id="64e71-154">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="64e71-155">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="64e71-155">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="64e71-156">Configurer l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="64e71-156">Configure Single Sign-on</span></span>](active-directory-saas-netsuite-tutorial.md)