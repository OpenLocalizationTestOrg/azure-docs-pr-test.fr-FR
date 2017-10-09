---
title: "Didacticiel : Configuration de ThousandEyes pour l’approvisionnement automatique d’utilisateurs avec Azure Active Directory | Microsoft Docs"
description: "Découvrez comment tooconfigure Azure Active Directory tooautomatically disposition et la disposition de l’utilisateur des comptes tooThousandEyes."
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
ms.openlocfilehash: f31883ab685d0ffcd9a830aa4a7d43c056f5f4cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-thousandeyes-for-automatic-user-provisioning"></a><span data-ttu-id="103d9-103">Didacticiel : Configuration de ThousandEyes pour approvisionner automatiquement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="103d9-103">Tutorial: Configuring ThousandEyes for Automatic User Provisioning</span></span>


<span data-ttu-id="103d9-104">objectif Hello de ce didacticiel est tooshow que vous hello étapes, vous devez tooperform dans une disposition de tooautomatically ThousandEyes et Azure AD et annuler la configuration des comptes d’utilisateur à partir d’Azure AD tooThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="103d9-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in ThousandEyes and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooThousandEyes.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="103d9-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="103d9-105">Prerequisites</span></span>

<span data-ttu-id="103d9-106">scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="103d9-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="103d9-107">Un locataire Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="103d9-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="103d9-108">Un locataire ThousandEyes avec hello [plan Standard](https://www.thousandeyes.com/pricing) ou mieux activé</span><span class="sxs-lookup"><span data-stu-id="103d9-108">A ThousandEyes tenant with hello [Standard plan](https://www.thousandeyes.com/pricing) or better enabled</span></span> 
*   <span data-ttu-id="103d9-109">Un compte d’utilisateur dans ThousandEyes doté d’autorisations d’administrateur</span><span class="sxs-lookup"><span data-stu-id="103d9-109">A user account in ThousandEyes with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="103d9-110">Hello mise en service d’intégration de Azure AD s’appuie sur hello [ThousandEyes SCIM API](https://success.thousandeyes.com/PublicArticlePage?articleIdParam=kA044000000CnWrCAK), qui est équipes tooThousandEyes disponible sur le plan Standard de hello ou supérieures.</span><span class="sxs-lookup"><span data-stu-id="103d9-110">hello Azure AD provisioning integration relies on hello [ThousandEyes SCIM API](https://success.thousandeyes.com/PublicArticlePage?articleIdParam=kA044000000CnWrCAK), which is available tooThousandEyes teams on hello Standard plan or better.</span></span>

## <a name="assigning-users-toothousandeyes"></a><span data-ttu-id="103d9-111">Affectation d’utilisateurs tooThousandEyes</span><span class="sxs-lookup"><span data-stu-id="103d9-111">Assigning users tooThousandEyes</span></span>

<span data-ttu-id="103d9-112">Azure Active Directory utilise un concept appelé toodetermine « affectations » les utilisateurs qui doivent recevoir l’accès tooselected applications.</span><span class="sxs-lookup"><span data-stu-id="103d9-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="103d9-113">Dans le contexte de hello de configuration de compte automatique d’utilisateurs, seuls les utilisateurs de hello et les groupes qui ont été « affectés » application tooan dans Azure AD est synchronisé.</span><span class="sxs-lookup"><span data-stu-id="103d9-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="103d9-114">Avant de configurer et de l’activation de hello service de configuration, vous devez toodecide quels utilisateurs ou des groupes dans Azure AD représentent hello utilisateurs qui doivent accéder à application de ThousandEyes tooyour.</span><span class="sxs-lookup"><span data-stu-id="103d9-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour ThousandEyes app.</span></span> <span data-ttu-id="103d9-115">Après choisi, vous pouvez attribuer à ces applications de ThousandEyes tooyour les utilisateurs en suivant les instructions hello ici :</span><span class="sxs-lookup"><span data-stu-id="103d9-115">Once decided, you can assign these users tooyour ThousandEyes app by following hello instructions here:</span></span>

[<span data-ttu-id="103d9-116">Affecter une application d’entreprise tooan utilisateur ou un groupe</span><span class="sxs-lookup"><span data-stu-id="103d9-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toothousandeyes"></a><span data-ttu-id="103d9-117">Conseils importants pour l’affectation d’utilisateurs tooThousandEyes</span><span class="sxs-lookup"><span data-stu-id="103d9-117">Important tips for assigning users tooThousandEyes</span></span>

*   <span data-ttu-id="103d9-118">Il est recommandé qu’un seul utilisateur Azure AD est attribué tooThousandEyes tootest hello est mise en service de configuration.</span><span class="sxs-lookup"><span data-stu-id="103d9-118">It is recommended that a single Azure AD user is assigned tooThousandEyes tootest hello provisioning configuration.</span></span> <span data-ttu-id="103d9-119">Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="103d9-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="103d9-120">Lorsque vous affectez un tooThousandEyes d’utilisateur, vous devez sélectionner soit hello **utilisateur** rôle, ou un autre valide spécifique à l’application (si disponible) dans la boîte de dialogue attribution hello.</span><span class="sxs-lookup"><span data-stu-id="103d9-120">When assigning a user tooThousandEyes, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="103d9-121">Hello **accès par défaut** rôle ne fonctionne pas pour la configuration, et ces utilisateurs sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="103d9-121">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-toothousandeyes"></a><span data-ttu-id="103d9-122">Configuration tooThousandEyes de configuration de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="103d9-122">Configuring user provisioning tooThousandEyes</span></span> 

<span data-ttu-id="103d9-123">Cette section vous guide à travers de la connexion du compte d’utilisateur de votre tooThousandEyes AD Azure API de configuration et configurez hello toocreate du service de configuration, de mettre à jour et de désactiver les comptes d’utilisateur affecté dans ThousandEyes en fonction de l’affectation d’utilisateurs et de groupes dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="103d9-123">This section guides you through connecting your Azure AD tooThousandEyes's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in ThousandEyes based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="103d9-124">Vous pouvez également choisir tooenabled basé sur SAML Single Sign-On pour ThousandEyes, en suivant les instructions hello fournies dans [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="103d9-124">You may also choose tooenabled SAML-based Single Sign-On for ThousandEyes, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="103d9-125">L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que chacune de ces deux fonctionnalités compléte l’autre.</span><span class="sxs-lookup"><span data-stu-id="103d9-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toothousandeyes-in-azure-ad"></a><span data-ttu-id="103d9-126">Configurer le compte d’automatique de l’utilisateur de configuration tooThousandEyes dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="103d9-126">Configure automatic user account provisioning tooThousandEyes in Azure AD</span></span>


1. <span data-ttu-id="103d9-127">Bonjour [portail Azure](https://portal.azure.com), parcourir toohello **Azure Active Directory > applications d’entreprise > toutes les applications** section.</span><span class="sxs-lookup"><span data-stu-id="103d9-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="103d9-128">Si vous avez déjà configuré ThousandEyes pour l’authentification unique, recherchez votre instance de ThousandEyes à l’aide du champ de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="103d9-128">If you have already configured ThousandEyes for single sign-on, search for your instance of ThousandEyes using hello search field.</span></span> <span data-ttu-id="103d9-129">Sinon, sélectionnez **ajouter** et recherchez **ThousandEyes** dans la galerie d’applications hello.</span><span class="sxs-lookup"><span data-stu-id="103d9-129">Otherwise, select **Add** and search for **ThousandEyes** in hello application gallery.</span></span> <span data-ttu-id="103d9-130">Sélectionnez ThousandEyes à partir des résultats de recherche hello et ajoutez-le tooyour la liste des applications.</span><span class="sxs-lookup"><span data-stu-id="103d9-130">Select ThousandEyes from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="103d9-131">Sélectionnez votre instance de ThousandEyes, puis hello **Provisioning** onglet.</span><span class="sxs-lookup"><span data-stu-id="103d9-131">Select your instance of ThousandEyes, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="103d9-132">Ensemble hello **Mode d’approvisionnement** trop**automatique**.</span><span class="sxs-lookup"><span data-stu-id="103d9-132">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![Approvisionnement de ThousandEyes](./media/active-directory-saas-thousandeyes-provisioning-tutorial/ThousandEyes1.png)

5. <span data-ttu-id="103d9-134">Sous hello **informations d’identification d’administrateur** section, hello d’entrée **Secret jeton** générés par les comptes de votre ThousandEyes (vous pouvez rechercher le jeton de hello sous votre compte ThousandEyes : **sécurité & Authentification**).</span><span class="sxs-lookup"><span data-stu-id="103d9-134">Under hello **Admin Credentials** section, input hello **Secret Token** generated by your ThousandEyes's account (you can find hello token under your ThousandEyes account: **Security & Authentication**).</span></span> 

    ![Approvisionnement de ThousandEyes](./media/active-directory-saas-thousandeyes-provisioning-tutorial/ThousandEyes2.png)

6. <span data-ttu-id="103d9-136">Bonjour portail Azure, cliquez sur **tester la connexion** tooensure AD Azure peut se connecter tooyour ThousandEyes application.</span><span class="sxs-lookup"><span data-stu-id="103d9-136">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour ThousandEyes app.</span></span> <span data-ttu-id="103d9-137">Si hello connexion échoue, vérifiez que votre compte de ThousandEyes a des autorisations d’administrateur et recommencez l’étape 5.</span><span class="sxs-lookup"><span data-stu-id="103d9-137">If hello connection fails, ensure your ThousandEyes account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="103d9-138">Entrez hello adresse de messagerie d’une personne ou un groupe qui doit recevoir des notifications d’erreur approvisionnement hello **courrier électronique de Notification** champ et la case à cocher de vérification hello « envoient une notification par courrier électronique lorsqu’une défaillance se produit ».</span><span class="sxs-lookup"><span data-stu-id="103d9-138">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="103d9-139">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="103d9-139">Click **Save**.</span></span> 

9. <span data-ttu-id="103d9-140">Sous la section des mappages de hello, sélectionnez **tooThousandEyes de synchronisation Azure Active Directory Users**.</span><span class="sxs-lookup"><span data-stu-id="103d9-140">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooThousandEyes**.</span></span>

10. <span data-ttu-id="103d9-141">Bonjour **des mappages d’attributs** section, passez en revue les attributs utilisateur hello qui sont synchronisés à partir d’Azure AD tooThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="103d9-141">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooThousandEyes.</span></span> <span data-ttu-id="103d9-142">Hello attributs sélectionnés en tant que **correspondance** propriétés sont des comptes d’utilisateur hello toomatch utilisés dans ThousandEyes pour les opérations de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="103d9-142">hello attributes selected as **Matching** properties are used toomatch hello user accounts in ThousandEyes for update operations.</span></span> <span data-ttu-id="103d9-143">Sélectionnez toocommit de bouton hello enregistrer toutes les modifications.</span><span class="sxs-lookup"><span data-stu-id="103d9-143">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="103d9-144">tooenable hello service de configuration d’Azure AD pour ThousandEyes, la modification hello **état d’approvisionnement** trop**sur** Bonjour **paramètres** section</span><span class="sxs-lookup"><span data-stu-id="103d9-144">tooenable hello Azure AD provisioning service for ThousandEyes, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="103d9-145">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="103d9-145">Click **Save**.</span></span> 

<span data-ttu-id="103d9-146">Cette opération démarre la synchronisation initiale d’utilisateurs et/ou groupes affectés tooThousandEyes Bonjour les utilisateurs et la section groupes de hello.</span><span class="sxs-lookup"><span data-stu-id="103d9-146">This operation starts hello initial synchronization of any users and/or groups assigned tooThousandEyes in hello Users and Groups section.</span></span> <span data-ttu-id="103d9-147">la synchronisation initiale Hello prend tooperform plus de temps que les synchronisations suivantes, qui se produisent toutes les 20 minutes environ tant que service de hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="103d9-147">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="103d9-148">Vous pouvez utiliser hello **détails de synchronisation** section toomonitor cours et suivre des rapports d’activité tooprovisioning des liens, qui décrivent toutes les actions effectuées par hello service de configuration.</span><span class="sxs-lookup"><span data-stu-id="103d9-148">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="103d9-149">Pour plus d’informations sur l’approvisionnement hello Azure AD tooread du mode de connexion, consultez [création de rapports sur la configuration de compte automatique d’utilisateurs](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="103d9-149">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="103d9-150">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="103d9-150">Additional resources</span></span>

* [<span data-ttu-id="103d9-151">Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise</span><span class="sxs-lookup"><span data-stu-id="103d9-151">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="103d9-152">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="103d9-152">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="103d9-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="103d9-153">Next steps</span></span>

* [<span data-ttu-id="103d9-154">Découvrez comment tooreview se connecte et obtenir des rapports sur l’activité de configuration</span><span class="sxs-lookup"><span data-stu-id="103d9-154">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
