---
title: "Didacticiel : Intégration d’Azure Active Directory à Citrix GoToMeeting | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Citrix GoToMeeting."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f59fedb-2cf8-48d2-a5fb-222ed943ff78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 3c6eed5309dfa384c292b0cf63f8aa58988add81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-citrix-gotomeeting-for-automatic-user-provisioning"></a><span data-ttu-id="15a78-103">Didacticiel : Configuration de Citrix GoToMeeting pour l’attribution automatique des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="15a78-103">Tutorial: Configuring Citrix GoToMeeting for Automatic User Provisioning</span></span>

<span data-ttu-id="15a78-104">objectif Hello de ce didacticiel est tooshow vous hello étapes que vous devez tooperform dans Citrix GoToMeeting et Azure AD tooautomatically approvisionner et configurer des comptes d’utilisateur à partir d’Azure AD tooCitrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="15a78-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Citrix GoToMeeting and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooCitrix GoToMeeting.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="15a78-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="15a78-105">Prerequisites</span></span>

<span data-ttu-id="15a78-106">scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="15a78-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="15a78-107">Un locataire Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="15a78-107">An Azure Active directory tenant.</span></span>
*   <span data-ttu-id="15a78-108">Un abonnement Citrix GoToMeeting pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="15a78-108">A Citrix GoToMeeting single-sign on enabled subscription.</span></span>
*   <span data-ttu-id="15a78-109">Un compte d’utilisateur Citrix GoToMeeting avec les autorisations d’administrateur d’équipe</span><span class="sxs-lookup"><span data-stu-id="15a78-109">A user account in Citrix GoToMeeting with Team Admin permissions.</span></span>

## <a name="assigning-users-toocitrix-gotomeeting"></a><span data-ttu-id="15a78-110">Affectation d’utilisateurs tooCitrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="15a78-110">Assigning users tooCitrix GoToMeeting</span></span>

<span data-ttu-id="15a78-111">Azure Active Directory utilise un concept appelé toodetermine « affectations » les utilisateurs qui doivent recevoir l’accès tooselected applications.</span><span class="sxs-lookup"><span data-stu-id="15a78-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="15a78-112">Dans le contexte de hello de configuration de compte automatique d’utilisateurs, seuls les utilisateurs de hello et les groupes qui ont été « affectés » application tooan dans Azure AD est synchronisé.</span><span class="sxs-lookup"><span data-stu-id="15a78-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span>

<span data-ttu-id="15a78-113">Avant de configurer et de l’activation de hello service de configuration, vous devez toodecide quels utilisateurs ou des groupes dans Azure AD qui représentent des utilisateurs ayant besoin d’accès tooyour Citrix GoToMeeting application hello.</span><span class="sxs-lookup"><span data-stu-id="15a78-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour Citrix GoToMeeting app.</span></span> <span data-ttu-id="15a78-114">Une fois choisi, vous pouvez attribuer ces tooyour utilisateurs Citrix GoToMeeting application en suivant les instructions hello ici :</span><span class="sxs-lookup"><span data-stu-id="15a78-114">Once decided, you can assign these users tooyour Citrix GoToMeeting app by following hello instructions here:</span></span>

[<span data-ttu-id="15a78-115">Affecter une application d’entreprise tooan utilisateur ou un groupe</span><span class="sxs-lookup"><span data-stu-id="15a78-115">Assign a user or group tooan enterprise app</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toocitrix-gotomeeting"></a><span data-ttu-id="15a78-116">Conseils importants pour l’affectation d’utilisateurs tooCitrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="15a78-116">Important tips for assigning users tooCitrix GoToMeeting</span></span>

*   <span data-ttu-id="15a78-117">Il est recommandé qu’un seul utilisateur Azure AD est attribué tooCitrix GoToMeeting tootest hello service de la configuration.</span><span class="sxs-lookup"><span data-stu-id="15a78-117">It is recommended that a single Azure AD user is assigned tooCitrix GoToMeeting tootest hello provisioning configuration.</span></span> <span data-ttu-id="15a78-118">Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="15a78-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="15a78-119">Lorsque vous affectez un tooCitrix utilisateur GoToMeeting, vous devez sélectionner un rôle d’utilisateur valide.</span><span class="sxs-lookup"><span data-stu-id="15a78-119">When assigning a user tooCitrix GoToMeeting, you must select a valid user role.</span></span> <span data-ttu-id="15a78-120">rôle de « Accès par défaut » Hello ne fonctionne pas pour la configuration.</span><span class="sxs-lookup"><span data-stu-id="15a78-120">hello "Default Access" role does not work for provisioning.</span></span>

## <a name="enable-automated-user-provisioning"></a><span data-ttu-id="15a78-121">Activer l’approvisionnement automatique des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="15a78-121">Enable Automated User Provisioning</span></span>

<span data-ttu-id="15a78-122">Cette section vous guide à travers de la connexion du compte d’utilisateur de votre GoToMeeting tooCitrix AD Azure API de configuration et configurez hello toocreate du service de configuration, de mettre à jour et de désactiver l’utilisateur affecté comptes dans Citrix GoToMeeting en fonction de l’utilisateur et de groupe affectation dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="15a78-122">This section guides you through connecting your Azure AD tooCitrix GoToMeeting's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Citrix GoToMeeting based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="15a78-123">Vous pouvez également choisir tooenabled basé sur SAML Single Sign-On pour Citrix GoToMeeting, suivant les instructions hello fournies dans [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="15a78-123">You may also choose tooenabled SAML-based Single Sign-On for Citrix GoToMeeting, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="15a78-124">L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que chacune de ces deux fonctionnalités compléte l’autre.</span><span class="sxs-lookup"><span data-stu-id="15a78-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>

### <a name="tooconfigure-automatic-user-account-provisioning"></a><span data-ttu-id="15a78-125">tooconfigure compte le provisionnement utilisateur automatique :</span><span class="sxs-lookup"><span data-stu-id="15a78-125">tooconfigure automatic user account provisioning:</span></span>

1. <span data-ttu-id="15a78-126">Bonjour [portail Azure](https://portal.azure.com), parcourir toohello **Azure Active Directory > applications d’entreprise > toutes les applications** section.</span><span class="sxs-lookup"><span data-stu-id="15a78-126">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications** section.</span></span>

2. <span data-ttu-id="15a78-127">Si vous avez déjà configuré Citrix GoToMeeting pour l’authentification unique, recherchez votre instance de Citrix GoToMeeting à l’aide du champ de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="15a78-127">If you have already configured Citrix GoToMeeting for single sign-on, search for your instance of Citrix GoToMeeting using hello search field.</span></span> <span data-ttu-id="15a78-128">Sinon, sélectionnez **ajouter** et recherchez **Citrix GoToMeeting** dans la galerie d’applications hello.</span><span class="sxs-lookup"><span data-stu-id="15a78-128">Otherwise, select **Add** and search for **Citrix GoToMeeting** in hello application gallery.</span></span> <span data-ttu-id="15a78-129">Sélectionnez Citrix GoToMeeting à partir des résultats de recherche hello et ajoutez-le tooyour la liste des applications.</span><span class="sxs-lookup"><span data-stu-id="15a78-129">Select Citrix GoToMeeting from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="15a78-130">Sélectionnez votre instance de Citrix GoToMeeting, puis hello **Provisioning** onglet.</span><span class="sxs-lookup"><span data-stu-id="15a78-130">Select your instance of Citrix GoToMeeting, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="15a78-131">Ensemble hello **Provisioning** Mode trop**automatique**.</span><span class="sxs-lookup"><span data-stu-id="15a78-131">Set hello **Provisioning** Mode too**Automatic**.</span></span> 

    ![approvisionnement](./media/active-directory-saas-citrixgotomeeting-provisioning-tutorial/provisioning.png)

5. <span data-ttu-id="15a78-133">Sous la section informations d’identification d’administrateur de hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="15a78-133">Under hello Admin Credentials section, perform hello following steps:</span></span>
   
    <span data-ttu-id="15a78-134">a.</span><span class="sxs-lookup"><span data-stu-id="15a78-134">a.</span></span> <span data-ttu-id="15a78-135">Bonjour **nom d’utilisateur Admin Citrix GoToMeeting** zone de texte, nom d’utilisateur de type hello d’un administrateur.</span><span class="sxs-lookup"><span data-stu-id="15a78-135">In hello **Citrix GoToMeeting Admin User Name** textbox, type hello user name of an administrator.</span></span>

    <span data-ttu-id="15a78-136">b.</span><span class="sxs-lookup"><span data-stu-id="15a78-136">b.</span></span> <span data-ttu-id="15a78-137">Bonjour **mot de passe Admin Citrix GoToMeeting** zone de texte, hello mot de passe administrateur.</span><span class="sxs-lookup"><span data-stu-id="15a78-137">In hello **Citrix GoToMeeting Admin Password** textbox, hello administrator's password.</span></span>

6. <span data-ttu-id="15a78-138">Bonjour portail Azure, cliquez sur **tester la connexion** tooensure Azure AD peut se connecter tooyour Citrix GoToMeeting application.</span><span class="sxs-lookup"><span data-stu-id="15a78-138">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour Citrix GoToMeeting app.</span></span> <span data-ttu-id="15a78-139">Si hello connexion échoue, assurez-vous que votre compte Citrix GoToMeeting dispose des autorisations d’administrateur d’équipe et essayez hello **« Informations d’identification d’administration »** pas à pas.</span><span class="sxs-lookup"><span data-stu-id="15a78-139">If hello connection fails, ensure your Citrix GoToMeeting account has Team Admin permissions and try hello **"Admin Credentials"** step again.</span></span>

7. <span data-ttu-id="15a78-140">Entrez hello adresse de messagerie d’une personne ou un groupe qui doit recevoir des notifications d’erreur approvisionnement hello **courrier électronique de Notification** champ et la case à cocher hello.</span><span class="sxs-lookup"><span data-stu-id="15a78-140">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox.</span></span>

8. <span data-ttu-id="15a78-141">Cliquez sur **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="15a78-141">Click **Save.**</span></span>

9. <span data-ttu-id="15a78-142">Sous la section des mappages de hello, sélectionnez **tooCitrix de synchronisation Azure Active Directory Users GoToMeeting.**</span><span class="sxs-lookup"><span data-stu-id="15a78-142">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooCitrix GoToMeeting.**</span></span>

10. <span data-ttu-id="15a78-143">Bonjour **des mappages d’attributs** section, passez en revue les attributs utilisateur hello qui sont synchronisés à partir d’Azure AD tooCitrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="15a78-143">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooCitrix GoToMeeting.</span></span> <span data-ttu-id="15a78-144">Hello attributs sélectionnés en tant que **correspondance** propriétés sont des comptes d’utilisateur hello toomatch utilisés dans Citrix GoToMeeting pour les opérations de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="15a78-144">hello attributes selected as **Matching** properties are used toomatch hello user accounts in Citrix GoToMeeting for update operations.</span></span> <span data-ttu-id="15a78-145">Sélectionnez toocommit de bouton hello enregistrer toutes les modifications.</span><span class="sxs-lookup"><span data-stu-id="15a78-145">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="15a78-146">tooenable hello service de configuration d’Azure AD pour Citrix GoToMeeting, modification hello **état d’approvisionnement** trop**sur** Bonjour section de paramètres</span><span class="sxs-lookup"><span data-stu-id="15a78-146">tooenable hello Azure AD provisioning service for Citrix GoToMeeting, change hello **Provisioning Status** too**On** in hello Settings section</span></span>

12. <span data-ttu-id="15a78-147">Cliquez sur **Enregistrer.**</span><span class="sxs-lookup"><span data-stu-id="15a78-147">Click **Save.**</span></span>

<span data-ttu-id="15a78-148">Il démarre la synchronisation initiale de hello de tous les utilisateurs et/ou groupes affectés tooCitrix GoToMeeting dans la section utilisateurs et groupes de hello.</span><span class="sxs-lookup"><span data-stu-id="15a78-148">It starts hello initial synchronization of any users and/or groups assigned tooCitrix GoToMeeting in hello Users and Groups section.</span></span> <span data-ttu-id="15a78-149">la synchronisation initiale Hello prend tooperform plus de temps que les synchronisations suivantes, qui se produisent toutes les 20 minutes environ tant que service de hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="15a78-149">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="15a78-150">Vous pouvez utiliser hello **détails de synchronisation** section toomonitor cours et suivre des rapports d’activité tooprovisioning des liens, qui décrivent toutes les actions effectuées par hello mise en service du service sur votre application Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="15a78-150">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Citrix GoToMeeting app.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="15a78-151">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="15a78-151">Additional resources</span></span>

* [<span data-ttu-id="15a78-152">Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise</span><span class="sxs-lookup"><span data-stu-id="15a78-152">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="15a78-153">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="15a78-153">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="15a78-154">Configurer l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="15a78-154">Configure Single Sign-on</span></span>](active-directory-saas-citrix-gotomeeting-tutorial.md)


