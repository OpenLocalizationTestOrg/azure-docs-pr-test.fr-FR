---
title: "Didacticiel : Configuration de Cerner Central pour l’approvisionnement automatique d’utilisateurs avec Azure Active Directory | Microsoft Docs"
description: "Découvrez comment tooconfigure Azure Active Directory tooautomatically configurer la liste de tooa d’utilisateurs dans le centre de Cerner."
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
ms.date: 05/26/2017
ms.author: asmalser-msft
ms.openlocfilehash: e96da98e783d24e7f34ae924824f909eead75f54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-cerner-central-for-automatic-user-provisioning"></a><span data-ttu-id="7d1f0-103">Didacticiel : Configuration de Cerner Central pour l’approvisionnement automatique d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="7d1f0-103">Tutorial: Configuring Cerner Central for Automatic User Provisioning</span></span>

<span data-ttu-id="7d1f0-104">objectif Hello de ce didacticiel est tooshow vous hello étapes que vous devez tooperform dans le centre de Cerner et Azure AD tooautomatically approvisionner et configurer des comptes d’utilisateur à partir de la liste d’utilisateur Azure AD tooa Cerner central.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in Cerner Central and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooa user roster in Cerner Central.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="7d1f0-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7d1f0-105">Prerequisites</span></span>

<span data-ttu-id="7d1f0-106">scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="7d1f0-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="7d1f0-107">Un client Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7d1f0-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="7d1f0-108">Un locataire Cerner Central</span><span class="sxs-lookup"><span data-stu-id="7d1f0-108">A Cerner Central tenant</span></span> 

> [!NOTE]
> <span data-ttu-id="7d1f0-109">Azure Active Directory s’intègre à Cerner les Central à l’aide de hello [SCIM](http://www.simplecloud.info/) protocole.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-109">Azure Active Directory integrates with Cerner Central using hello [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-toocerner-central"></a><span data-ttu-id="7d1f0-110">Affectation d’utilisateurs tooCerner Central</span><span class="sxs-lookup"><span data-stu-id="7d1f0-110">Assigning users tooCerner Central</span></span>

<span data-ttu-id="7d1f0-111">Azure Active Directory utilise un concept appelé toodetermine « affectations » les utilisateurs qui doivent recevoir l’accès tooselected applications.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="7d1f0-112">Dans le contexte de hello de configuration de compte automatique d’utilisateurs, seuls les utilisateurs de hello et les groupes qui ont été « affectés » application tooan dans Azure AD sont synchronisés.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD are synchronized.</span></span> 

<span data-ttu-id="7d1f0-113">Avant de configurer et de l’activation de hello service de configuration, vous devez décider quels utilisateurs ou des groupes dans Azure AD représentent des utilisateurs hello besoin d’accès tooCerner Central.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-113">Before configuring and enabling hello provisioning service, you should decide what users and/or groups in Azure AD represent hello users who need access tooCerner Central.</span></span> <span data-ttu-id="7d1f0-114">Une fois décidé, vous pouvez attribuer ces tooCerner utilisateurs Central en suivant les instructions hello ici :</span><span class="sxs-lookup"><span data-stu-id="7d1f0-114">Once decided, you can assign these users tooCerner Central by following hello instructions here:</span></span>

[<span data-ttu-id="7d1f0-115">Affecter une application d’entreprise tooan utilisateur ou un groupe</span><span class="sxs-lookup"><span data-stu-id="7d1f0-115">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toocerner-central"></a><span data-ttu-id="7d1f0-116">Conseils importants pour l’affectation d’utilisateurs tooCerner Central</span><span class="sxs-lookup"><span data-stu-id="7d1f0-116">Important tips for assigning users tooCerner Central</span></span>

*   <span data-ttu-id="7d1f0-117">Il est recommandé qu’un seul utilisateur Azure AD avoir tooCerner tootest centrale hello est mise en service de configuration.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-117">It is recommended that a single Azure AD user be assigned tooCerner Central tootest hello provisioning configuration.</span></span> <span data-ttu-id="7d1f0-118">Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-118">Additional users and/or groups may be assigned later.</span></span>

* <span data-ttu-id="7d1f0-119">Une fois le test initial terminé pour un seul utilisateur, Cerner centre recommande d’attribuer hello intégralité de la liste des utilisateurs, tooaccess liste utilisateur de n’importe quel Cerner la solution (pas seulement Cerner Central) toobe configuré tooCerner.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-119">Once initial testing is complete for a single user, Cerner Central recommends assigning hello entire list of users intended tooaccess any Cerner solution (not just Cerner Central) toobe provisioned tooCerner’s user roster.</span></span>  <span data-ttu-id="7d1f0-120">Autres solutions Cerner tirer parti de cette liste d’utilisateurs dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-120">Other Cerner solutions leverage this list of users in hello user roster.</span></span>

*   <span data-ttu-id="7d1f0-121">Lorsque vous affectez un tooCerner utilisateur Central, vous devez sélectionner hello **utilisateur** rôle dans la boîte de dialogue attribution hello.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-121">When assigning a user tooCerner Central, you must select hello **User** role in hello assignment dialog.</span></span> <span data-ttu-id="7d1f0-122">Les utilisateurs dotés du rôle de « Accès par défaut » hello sont exclus de l’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-122">Users with hello "Default Access" role are excluded from provisioning.</span></span>


## <a name="configuring-user-provisioning-toocerner-central"></a><span data-ttu-id="7d1f0-123">Configuration tooCerner centre de configuration de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="7d1f0-123">Configuring user provisioning tooCerner Central</span></span>

<span data-ttu-id="7d1f0-124">Cette section vous guide à travers de la connexion de liste d’utilisateur de votre centre de tooCerner Azure AD à l’aide du compte d’utilisateur de Cerner SCIM API de configuration et configurez hello toocreate du service de configuration, de mettre à jour et de désactiver l’utilisateur affecté en fonction des comptes dans le centre de Cerner lors de l’attribution d’utilisateurs et de groupes dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-124">This section guides you through connecting your Azure AD tooCerner Central’s User Roster using Cerner's SCIM user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in Cerner Central based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="7d1f0-125">Vous pouvez également choisir tooenabled basé sur SAML Single Sign-On pour Cerner Central, suivant les instructions hello fournies dans [portail Azure (https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7d1f0-125">You may also choose tooenabled SAML-based Single Sign-On for Cerner Central, following hello instructions provided in [Azure portal (https://portal.azure.com).</span></span> <span data-ttu-id="7d1f0-126">L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que ces deux fonctionnalités se complètent.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-126">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span> <span data-ttu-id="7d1f0-127">Pour plus d’informations, consultez hello [didacticiel l’authentification unique de le Cerner Central](active-directory-saas-cernercentral-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="7d1f0-127">For more information, see hello [Cerner Central single sign-on tutorial](active-directory-saas-cernercentral-tutorial.md).</span></span>


### <a name="tooconfigure-automatic-user-account-provisioning-toocerner-central-in-azure-ad"></a><span data-ttu-id="7d1f0-128">compte d’utilisateur automatique de tooconfigure tooCerner centre de configuration dans Azure AD :</span><span class="sxs-lookup"><span data-stu-id="7d1f0-128">tooconfigure automatic user account provisioning tooCerner Central in Azure AD:</span></span>


<span data-ttu-id="7d1f0-129">Dans l’ordre tooprovision utilisateur comptes tooCerner Central, seront peut-être toorequest un compte de système de Cerner centre de Cerner et générer un jeton de porteur OAuth que Azure AD peut utiliser de point de terminaison de tooconnect tooCerner SCIM.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-129">In order tooprovision user accounts tooCerner Central, you’ll need toorequest a Cerner Central system account from Cerner, and generate an OAuth bearer token that Azure AD can use tooconnect tooCerner's SCIM endpoint.</span></span> <span data-ttu-id="7d1f0-130">Il est également recommandé que l’intégration de hello être effectuée dans un environnement de bac à sable Cerner avant de déployer tooproduction.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-130">It is also recommended that hello integration be performed in a Cerner sandbox environment before deploying tooproduction.</span></span>

1.  <span data-ttu-id="7d1f0-131">première étape de Hello est personnes de hello tooensure gestion hello Cerner et intégration d’Azure AD ont un compte CernerCare, qui est requis tooaccess hello documentation nécessaire toocomplete hello instructions.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-131">hello first step is tooensure hello people managing hello Cerner and Azure AD integration have a CernerCare account, which is required tooaccess hello documentation necessary toocomplete hello instructions.</span></span> <span data-ttu-id="7d1f0-132">Si nécessaire, utilisez l’URL de hello ci-dessous toocreate CernerCare comptes dans chaque environnement applicable.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-132">If necessary, use hello URLs below toocreate CernerCare accounts in each applicable environment.</span></span>

   * <span data-ttu-id="7d1f0-133">Bac à sable : https://sandboxcernercare.com/accounts/create</span><span class="sxs-lookup"><span data-stu-id="7d1f0-133">Sandbox:  https://sandboxcernercare.com/accounts/create</span></span>

   * <span data-ttu-id="7d1f0-134">Production : https://cernercare.com/accounts/create</span><span class="sxs-lookup"><span data-stu-id="7d1f0-134">Production:  https://cernercare.com/accounts/create</span></span>  

2.  <span data-ttu-id="7d1f0-135">Vous devez ensuite créer un compte système pour Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-135">Next, a system account must be created for Azure AD.</span></span> <span data-ttu-id="7d1f0-136">Utilisez les instructions de hello ci-dessous toorequest un compte système de votre environnement de bac à sable et de production.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-136">Use hello instructions below toorequest a System Account for your sandbox and production environments.</span></span>

   * <span data-ttu-id="7d1f0-137">Instructions : https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account</span><span class="sxs-lookup"><span data-stu-id="7d1f0-137">Instructions:  https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account</span></span>

   * <span data-ttu-id="7d1f0-138">Bac à sable : https://sandboxcernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="7d1f0-138">Sandbox: https://sandboxcernercentral.com/system-accounts/</span></span>

   * <span data-ttu-id="7d1f0-139">Production : https://cernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="7d1f0-139">Production:  https://cernercentral.com/system-accounts/</span></span>

3.  <span data-ttu-id="7d1f0-140">Générez ensuite un jeton du porteur OAuth pour chacun de vos comptes système.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-140">Next, generate an OAuth bearer token for each of your system accounts.</span></span> <span data-ttu-id="7d1f0-141">toodo, suivez les instructions hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-141">toodo this, follow hello instructions below.</span></span>

   * <span data-ttu-id="7d1f0-142">Instructions : https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token</span><span class="sxs-lookup"><span data-stu-id="7d1f0-142">Instructions:  https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token</span></span>

   * <span data-ttu-id="7d1f0-143">Bac à sable : https://sandboxcernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="7d1f0-143">Sandbox: https://sandboxcernercentral.com/system-accounts/</span></span>

   * <span data-ttu-id="7d1f0-144">Production : https://cernercentral.com/system-accounts/</span><span class="sxs-lookup"><span data-stu-id="7d1f0-144">Production:  https://cernercentral.com/system-accounts/</span></span>

4. <span data-ttu-id="7d1f0-145">Enfin, vous devez les ID de domaine liste tooacquire utilisateur pour les deux environnements de production et de bac à sable hello dans la configuration de Cerner toocomplete hello.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-145">Finally, you need tooacquire User Roster Realm IDs for both hello sandbox and production environments in Cerner toocomplete hello configuration.</span></span> <span data-ttu-id="7d1f0-146">Pour plus d’informations sur la façon de tooacquire, consultez : https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-146">For information on how tooacquire this, see: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM.</span></span> 

5. <span data-ttu-id="7d1f0-147">Vous pouvez maintenant configurer tooCerner de comptes utilisateur Azure AD tooprovision.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-147">Now you can configure Azure AD tooprovision user accounts tooCerner.</span></span> <span data-ttu-id="7d1f0-148">Connectez-vous à toohello [portail Azure](https://portal.azure.com)et recherchez toohello **Azure Active Directory > applications d’entreprise > toutes les applications** section.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-148">Sign in toohello [Azure portal](https://portal.azure.com), and browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

6. <span data-ttu-id="7d1f0-149">Si vous avez déjà configuré Cerner Central pour l’authentification unique, recherchez votre instance de Cerner les Central à l’aide du champ de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-149">If you have already configured Cerner Central for single sign-on, search for your instance of Cerner Central using hello search field.</span></span> <span data-ttu-id="7d1f0-150">Sinon, sélectionnez **ajouter** et recherchez **Cerner centre** dans la galerie d’applications hello.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-150">Otherwise, select **Add** and search for **Cerner Central** in hello application gallery.</span></span> <span data-ttu-id="7d1f0-151">Sélectionnez Cerner Central à partir des résultats de recherche hello et ajouter tooyour la liste des applications.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-151">Select Cerner Central from hello search results, and add it tooyour list of applications.</span></span>

7.  <span data-ttu-id="7d1f0-152">Sélectionnez votre instance de Cerner Central, puis sélectionnez hello **Provisioning** onglet.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-152">Select your instance of Cerner Central, then select hello **Provisioning** tab.</span></span>

8.  <span data-ttu-id="7d1f0-153">Ensemble hello **Mode d’approvisionnement** trop**automatique**.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-153">Set hello **Provisioning Mode** too**Automatic**.</span></span>

   ![Approvisionnement Central Cerner](./media/active-directory-saas-cernercentral-provisioning-tutorial/Cerner.PNG)

9.  <span data-ttu-id="7d1f0-155">Renseignez hello suivant champs sous **informations d’identification administrateur**:</span><span class="sxs-lookup"><span data-stu-id="7d1f0-155">Fill in hello following fields under **Admin Credentials**:</span></span>

   * <span data-ttu-id="7d1f0-156">Bonjour **URL de client** , entrez une URL au format hello ci-dessous, en remplaçant « Liste-domaine-ID utilisateur » avec l’ID de domaine hello vous avez acquis à l’étape 4 de #.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-156">In hello **Tenant URL** field, enter a URL in hello format below, replacing "User-Roster-Realm-ID" with hello realm ID you acquired in step #4.</span></span>

> <span data-ttu-id="7d1f0-157">Bac à sable : https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span><span class="sxs-lookup"><span data-stu-id="7d1f0-157">Sandbox: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span></span> 

> <span data-ttu-id="7d1f0-158">Production : https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span><span class="sxs-lookup"><span data-stu-id="7d1f0-158">Production: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/</span></span> 

   * <span data-ttu-id="7d1f0-159">Bonjour **Secret jeton** , indiquez le jeton de support OAuth hello générés à l’étape #3 et cliquez sur **tester la connexion**.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-159">In hello **Secret Token** field, enter hello OAuth bearer token you generated in step #3 and click **Test Connection**.</span></span>

   * <span data-ttu-id="7d1f0-160">Vous devez voir une notification de réussite supérieurdroit côté hello de votre portail.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-160">You should see a success notification on hello upper­right side of your portal.</span></span>

10. <span data-ttu-id="7d1f0-161">Entrez hello adresse de messagerie d’une personne ou un groupe qui doit recevoir des notifications d’erreur approvisionnement hello **courrier électronique de Notification** champ et la case à cocher hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-161">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox below.</span></span>

11. <span data-ttu-id="7d1f0-162">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-162">Click **Save**.</span></span> 

12. <span data-ttu-id="7d1f0-163">Bonjour **des mappages d’attributs** section, passez en revue les utilisateur hello et toobe d’attributs de groupe synchronisés à partir d’Azure AD tooCerner Central.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-163">In hello **Attribute Mappings** section, review hello user and group attributes toobe synchronized from Azure AD tooCerner Central.</span></span> <span data-ttu-id="7d1f0-164">Hello attributs sélectionnés en tant que **correspondance** propriétés sont utilisées toomatch hello des comptes d’utilisateur et les groupes dans Cerner Centre pour les opérations de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-164">hello attributes selected as **Matching** properties are used toomatch hello user accounts and groups in Cerner Central for update operations.</span></span> <span data-ttu-id="7d1f0-165">Sélectionnez toocommit de bouton hello enregistrer toutes les modifications.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-165">Select hello Save button toocommit any changes.</span></span>

13. <span data-ttu-id="7d1f0-166">tooenable hello service de configuration d’Azure AD pour Cerner Central, modification hello **état d’approvisionnement** trop**sur** Bonjour **paramètres** section</span><span class="sxs-lookup"><span data-stu-id="7d1f0-166">tooenable hello Azure AD provisioning service for Cerner Central, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

14. <span data-ttu-id="7d1f0-167">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-167">Click **Save**.</span></span> 

<span data-ttu-id="7d1f0-168">Cela démarre la synchronisation initiale hello de tous les utilisateurs et/ou groupes affectés tooCerner Central dans la section utilisateurs et groupes de hello.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-168">This starts hello initial synchronization of any users and/or groups assigned tooCerner Central in hello Users and Groups section.</span></span> <span data-ttu-id="7d1f0-169">la synchronisation initiale Hello prend tooperform plus de temps que les synchronisations suivantes, qui se produisent toutes les 20 minutes environ tant que hello service de configuration d’Azure AD est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-169">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello Azure AD provisioning service is running.</span></span> <span data-ttu-id="7d1f0-170">Vous pouvez utiliser hello **détails de synchronisation** section toomonitor cours et suivre des rapports d’activité tooprovisioning des liens, qui décrivent toutes les actions effectuées par hello service sur votre application de centre de Cerner l’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="7d1f0-170">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service on your Cerner Central app.</span></span>

<span data-ttu-id="7d1f0-171">Pour plus d’informations sur l’approvisionnement hello Azure AD tooread du mode de connexion, consultez [création de rapports sur la configuration de compte automatique d’utilisateurs](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="7d1f0-171">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7d1f0-172">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="7d1f0-172">Additional resources</span></span>

* <span data-ttu-id="7d1f0-173">[Cerner Central: Publishing identity data using Azure AD](https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+Azure+AD) (Cerner Central : Publication des données d’identité à l’aide d’Azure AD)</span><span class="sxs-lookup"><span data-stu-id="7d1f0-173">[Cerner Central: Publishing identity data using Azure AD](https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+Azure+AD)</span></span>
* <span data-ttu-id="7d1f0-174">[Tutorial: Configuring Cerner Central for single sign-on with Azure Active Directory](active-directory-saas-cernercentral-tutorial.md) (Didacticiel : Configuration de Cerner Central pour l’authentification unique avec Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="7d1f0-174">[Tutorial: Configuring Cerner Central for single sign-on with Azure Active Directory](active-directory-saas-cernercentral-tutorial.md)</span></span>
* [<span data-ttu-id="7d1f0-175">Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise</span><span class="sxs-lookup"><span data-stu-id="7d1f0-175">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="7d1f0-176">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="7d1f0-176">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="7d1f0-177">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7d1f0-177">Next steps</span></span>
* <span data-ttu-id="7d1f0-178">[Découvrez comment tooreview se connecte et obtenir des rapports sur l’activité de configuration](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="7d1f0-178">[Learn how tooreview logs and get reports on provisioning activity](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>
