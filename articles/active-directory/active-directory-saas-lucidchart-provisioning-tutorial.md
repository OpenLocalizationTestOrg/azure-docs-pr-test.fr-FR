---
title: "Didacticiel : Configuration de LucidChart pour l’approvisionnement automatique d’utilisateurs avec Azure Active Directory | Microsoft Docs"
description: "Découvrez comment tooconfigure Azure Active Directory tooautomatically disposition et la disposition de l’utilisateur des comptes tooLucidChart."
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
ms.date: 07/14/2017
ms.author: asmalser-msft
ms.openlocfilehash: d3af45141731215f2edc8942ad21b016468c1e38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-lucidchart-for-automatic-user-provisioning"></a><span data-ttu-id="81406-103">Didacticiel : configuration de LucidChart pour l’approvisionnement automatique d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="81406-103">Tutorial: Configuring LucidChart for Automatic User Provisioning</span></span>


<span data-ttu-id="81406-104">objectif Hello de ce didacticiel est tooshow vous hello étapes que vous devez tooperform dans LucidChart et Azure AD tooautomatically approvisionner et configurer des comptes d’utilisateur à partir d’Azure AD tooLucidChart.</span><span class="sxs-lookup"><span data-stu-id="81406-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in LucidChart and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooLucidChart.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="81406-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="81406-105">Prerequisites</span></span>

<span data-ttu-id="81406-106">scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="81406-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="81406-107">Un locataire Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="81406-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="81406-108">Un locataire LucidChart avec hello [plan d’entreprise](https://www.lucidchart.com/user/117598685#/subscriptionLevel) ou mieux activé</span><span class="sxs-lookup"><span data-stu-id="81406-108">A LucidChart tenant with hello [Enterprise plan](https://www.lucidchart.com/user/117598685#/subscriptionLevel) or better enabled</span></span> 
*   <span data-ttu-id="81406-109">Un compte utilisateur dans LucidChart avec des autorisations d’administrateur</span><span class="sxs-lookup"><span data-stu-id="81406-109">A user account in LucidChart with Admin permissions</span></span> 

## <a name="assigning-users-toolucidchart"></a><span data-ttu-id="81406-110">Affectation d’utilisateurs tooLucidChart</span><span class="sxs-lookup"><span data-stu-id="81406-110">Assigning users tooLucidChart</span></span>

<span data-ttu-id="81406-111">Azure Active Directory utilise un concept appelé toodetermine « affectations » les utilisateurs qui doivent recevoir l’accès tooselected applications.</span><span class="sxs-lookup"><span data-stu-id="81406-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="81406-112">Dans le contexte de hello de configuration de compte automatique d’utilisateurs, seuls les utilisateurs de hello et les groupes qui ont été « affectés » application tooan dans Azure AD est synchronisé.</span><span class="sxs-lookup"><span data-stu-id="81406-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="81406-113">Avant de configurer et de l’activation de hello service de configuration, vous devez toodecide quels utilisateurs ou des groupes dans Azure AD représentent hello utilisateurs qui doivent accéder à application de LucidChart tooyour.</span><span class="sxs-lookup"><span data-stu-id="81406-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour LucidChart app.</span></span> <span data-ttu-id="81406-114">Après choisi, vous pouvez attribuer à ces applications de LucidChart tooyour les utilisateurs en suivant les instructions hello ici :</span><span class="sxs-lookup"><span data-stu-id="81406-114">Once decided, you can assign these users tooyour LucidChart app by following hello instructions here:</span></span>

[<span data-ttu-id="81406-115">Affecter une application d’entreprise tooan utilisateur ou un groupe</span><span class="sxs-lookup"><span data-stu-id="81406-115">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toolucidchart"></a><span data-ttu-id="81406-116">Conseils importants pour l’affectation d’utilisateurs tooLucidChart</span><span class="sxs-lookup"><span data-stu-id="81406-116">Important tips for assigning users tooLucidChart</span></span>

*   <span data-ttu-id="81406-117">Il est recommandé qu’un seul utilisateur Azure AD est attribué tooLucidChart tootest hello est mise en service de configuration.</span><span class="sxs-lookup"><span data-stu-id="81406-117">It is recommended that a single Azure AD user is assigned tooLucidChart tootest hello provisioning configuration.</span></span> <span data-ttu-id="81406-118">Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="81406-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="81406-119">Lorsque vous affectez un tooLucidChart d’utilisateur, vous devez sélectionner soit hello **utilisateur** rôle, ou un autre valide spécifique à l’application (si disponible) dans la boîte de dialogue attribution hello.</span><span class="sxs-lookup"><span data-stu-id="81406-119">When assigning a user tooLucidChart, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="81406-120">Hello **accès par défaut** rôle ne fonctionne pas pour la configuration, et ces utilisateurs sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="81406-120">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-toolucidchart"></a><span data-ttu-id="81406-121">Configuration tooLucidChart de configuration de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="81406-121">Configuring user provisioning tooLucidChart</span></span> 

<span data-ttu-id="81406-122">Cette section vous guide à travers de la connexion du compte d’utilisateur de votre tooLucidChart AD Azure API de configuration et configurez hello toocreate du service de configuration, de mettre à jour et de désactiver les comptes d’utilisateur affecté dans LucidChart en fonction de l’affectation d’utilisateurs et de groupes dans Azure AD .</span><span class="sxs-lookup"><span data-stu-id="81406-122">This section guides you through connecting your Azure AD tooLucidChart's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in LucidChart based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="81406-123">Vous pouvez également choisir tooenabled basé sur SAML Single Sign-On pour LucidChart, en suivant les instructions hello fournies dans [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="81406-123">You may also choose tooenabled SAML-based Single Sign-On for LucidChart, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="81406-124">L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que chacune de ces deux fonctionnalités compléte l’autre.</span><span class="sxs-lookup"><span data-stu-id="81406-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toolucidchart-in-azure-ad"></a><span data-ttu-id="81406-125">Configurer le compte d’automatique de l’utilisateur de configuration tooLucidChart dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="81406-125">Configure automatic user account provisioning tooLucidChart in Azure AD</span></span>


1. <span data-ttu-id="81406-126">Bonjour [portail Azure](https://portal.azure.com), parcourir toohello **Azure Active Directory > applications d’entreprise > toutes les applications** section.</span><span class="sxs-lookup"><span data-stu-id="81406-126">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="81406-127">Si vous avez déjà configuré LucidChart pour l’authentification unique, recherchez votre instance de LucidChart à l’aide du champ de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="81406-127">If you have already configured LucidChart for single sign-on, search for your instance of LucidChart using hello search field.</span></span> <span data-ttu-id="81406-128">Sinon, sélectionnez **ajouter** et recherchez **LucidChart** dans la galerie d’applications hello.</span><span class="sxs-lookup"><span data-stu-id="81406-128">Otherwise, select **Add** and search for **LucidChart** in hello application gallery.</span></span> <span data-ttu-id="81406-129">Sélectionnez LucidChart à partir des résultats de recherche hello et ajoutez-le tooyour la liste des applications.</span><span class="sxs-lookup"><span data-stu-id="81406-129">Select LucidChart from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="81406-130">Sélectionnez votre instance de LucidChart, puis hello **Provisioning** onglet.</span><span class="sxs-lookup"><span data-stu-id="81406-130">Select your instance of LucidChart, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="81406-131">Ensemble hello **Mode d’approvisionnement** trop**automatique**.</span><span class="sxs-lookup"><span data-stu-id="81406-131">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![Approvisionnement de LucidChart](./media/active-directory-saas-lucidchart-provisioning-tutorial/LucidChart1.png)

5. <span data-ttu-id="81406-133">Sous hello **informations d’identification administrateur** section, entrée hello **Secret jeton** généré par le compte de votre LucidChart (vous pouvez rechercher le jeton de hello sous votre compte : **Team**  >  **Intégration de l’application** > **SCIM**).</span><span class="sxs-lookup"><span data-stu-id="81406-133">Under hello **Admin Credentials** section, input hello **Secret Token** generated by your LucidChart's account (you can find hello token under your account: **Team** > **App Integration** > **SCIM**).</span></span> 

    ![Approvisionnement de LucidChart](./media/active-directory-saas-lucidchart-provisioning-tutorial/LucidChart2.png)

6. <span data-ttu-id="81406-135">Bonjour portail Azure, cliquez sur **tester la connexion** tooensure AD Azure peut se connecter tooyour LucidChart application.</span><span class="sxs-lookup"><span data-stu-id="81406-135">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour LucidChart app.</span></span> <span data-ttu-id="81406-136">Si hello connexion échoue, vérifiez que votre compte de LucidChart a des autorisations d’administrateur et recommencez l’étape 5.</span><span class="sxs-lookup"><span data-stu-id="81406-136">If hello connection fails, ensure your LucidChart account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="81406-137">Entrez hello adresse de messagerie d’une personne ou un groupe qui doit recevoir des notifications d’erreur approvisionnement hello **courrier électronique de Notification** champ et la case à cocher de vérification hello « envoient une notification par courrier électronique lorsqu’une défaillance se produit ».</span><span class="sxs-lookup"><span data-stu-id="81406-137">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="81406-138">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="81406-138">Click **Save**.</span></span> 

9. <span data-ttu-id="81406-139">Sous la section des mappages de hello, sélectionnez **tooLucidChart de synchronisation Azure Active Directory Users**.</span><span class="sxs-lookup"><span data-stu-id="81406-139">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooLucidChart**.</span></span>

10. <span data-ttu-id="81406-140">Bonjour **des mappages d’attributs** section, passez en revue les attributs utilisateur hello qui sont synchronisés à partir d’Azure AD tooLucidChart.</span><span class="sxs-lookup"><span data-stu-id="81406-140">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooLucidChart.</span></span> <span data-ttu-id="81406-141">Hello attributs sélectionnés en tant que **correspondance** propriétés sont des comptes d’utilisateur hello toomatch utilisés dans LucidChart pour les opérations de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="81406-141">hello attributes selected as **Matching** properties are used toomatch hello user accounts in LucidChart for update operations.</span></span> <span data-ttu-id="81406-142">Sélectionnez toocommit de bouton hello enregistrer toutes les modifications.</span><span class="sxs-lookup"><span data-stu-id="81406-142">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="81406-143">tooenable hello service de configuration d’Azure AD pour LucidChart, modification hello **état d’approvisionnement** trop**sur** Bonjour **paramètres** section</span><span class="sxs-lookup"><span data-stu-id="81406-143">tooenable hello Azure AD provisioning service for LucidChart, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="81406-144">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="81406-144">Click **Save**.</span></span> 

<span data-ttu-id="81406-145">Cette opération démarre la synchronisation initiale d’utilisateurs et/ou groupes affectés tooLucidChart Bonjour les utilisateurs et la section groupes de hello.</span><span class="sxs-lookup"><span data-stu-id="81406-145">This operation starts hello initial synchronization of any users and/or groups assigned tooLucidChart in hello Users and Groups section.</span></span> <span data-ttu-id="81406-146">la synchronisation initiale Hello prend tooperform plus de temps que les synchronisations suivantes, qui se produisent toutes les 20 minutes environ tant que service de hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="81406-146">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="81406-147">Vous pouvez utiliser hello **détails de synchronisation** section toomonitor cours et suivre des rapports d’activité tooprovisioning des liens, qui décrivent toutes les actions effectuées par hello service de configuration.</span><span class="sxs-lookup"><span data-stu-id="81406-147">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="81406-148">Pour plus d’informations sur l’approvisionnement hello Azure AD tooread du mode de connexion, consultez [création de rapports sur la configuration de compte automatique d’utilisateurs](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="81406-148">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="81406-149">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="81406-149">Additional resources</span></span>

* [<span data-ttu-id="81406-150">Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise</span><span class="sxs-lookup"><span data-stu-id="81406-150">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="81406-151">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="81406-151">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="81406-152">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="81406-152">Next steps</span></span>

* [<span data-ttu-id="81406-153">Découvrez comment tooreview se connecte et obtenir des rapports sur l’activité de configuration</span><span class="sxs-lookup"><span data-stu-id="81406-153">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
