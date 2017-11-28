---
title: "Didacticiel : Configuration de ThousandEyes pour l’approvisionnement automatique d’utilisateurs avec Azure Active Directory | Microsoft Docs"
description: "Découvrez comment configurer Azure Active Directory pour approvisionner et retirer automatiquement des comptes d’utilisateur sur ThousandEyes."
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
ms.openlocfilehash: e6bc2eab3cc1adcf26857ed98d920177a51455ea
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-configuring-thousandeyes-for-automatic-user-provisioning"></a><span data-ttu-id="1ba24-103">Didacticiel : Configuration de ThousandEyes pour approvisionner automatiquement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="1ba24-103">Tutorial: Configuring ThousandEyes for Automatic User Provisioning</span></span>


<span data-ttu-id="1ba24-104">L’objectif de ce didacticiel est de vous montrer les étapes à effectuer dans ThousandEyes et Azure AD pour approvisionner et retirer automatiquement des comptes d’utilisateur entre Azure AD et ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="1ba24-104">The objective of this tutorial is to show you the steps you need to perform in ThousandEyes and Azure AD to automatically provision and de-provision user accounts from Azure AD to ThousandEyes.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="1ba24-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1ba24-105">Prerequisites</span></span>

<span data-ttu-id="1ba24-106">Le scénario décrit dans ce didacticiel part du principe que vous disposez des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1ba24-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="1ba24-107">Un locataire Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1ba24-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="1ba24-108">Un locataire ThousandEyes pour lequel au moins le [plan standard](https://www.thousandeyes.com/pricing) est activé</span><span class="sxs-lookup"><span data-stu-id="1ba24-108">A ThousandEyes tenant with the [Standard plan](https://www.thousandeyes.com/pricing) or better enabled</span></span> 
*   <span data-ttu-id="1ba24-109">Un compte d’utilisateur dans ThousandEyes doté d’autorisations d’administrateur</span><span class="sxs-lookup"><span data-stu-id="1ba24-109">A user account in ThousandEyes with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="1ba24-110">L’intégration de l’approvisionnement d’Azure AD repose sur l’[API ThousandEyes SCIM](https://success.thousandeyes.com/PublicArticlePage?articleIdParam=kA044000000CnWrCAK), mise à la disposition des équipes de ThousandEyes qui relèvent au moins du plan standard.</span><span class="sxs-lookup"><span data-stu-id="1ba24-110">The Azure AD provisioning integration relies on the [ThousandEyes SCIM API](https://success.thousandeyes.com/PublicArticlePage?articleIdParam=kA044000000CnWrCAK), which is available to ThousandEyes teams on the Standard plan or better.</span></span>

## <a name="assigning-users-to-thousandeyes"></a><span data-ttu-id="1ba24-111">Affectation d’utilisateurs à ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="1ba24-111">Assigning users to ThousandEyes</span></span>

<span data-ttu-id="1ba24-112">Azure Active Directory utilise un concept appelé « affectations » pour déterminer les utilisateurs devant recevoir l’accès aux applications sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="1ba24-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="1ba24-113">Dans le cadre de l’approvisionnement automatique de comptes d’utilisateur, les utilisateurs et les groupes qui ont été « affectés » à une application dans Azure AD sont synchronisés.</span><span class="sxs-lookup"><span data-stu-id="1ba24-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="1ba24-114">Avant de configurer et d’activer le service d’approvisionnement, vous devez déterminer quels utilisateurs et/ou groupes dans Azure AD représentent les utilisateurs qui ont besoin d’accéder à votre application ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="1ba24-114">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your ThousandEyes app.</span></span> <span data-ttu-id="1ba24-115">Dès que vous avez fait votre choix, vous pouvez assigner ces utilisateurs à votre application ThousandEyes en suivant les instructions disponibles à la page suivante :</span><span class="sxs-lookup"><span data-stu-id="1ba24-115">Once decided, you can assign these users to your ThousandEyes app by following the instructions here:</span></span>

[<span data-ttu-id="1ba24-116">Affecter un utilisateur ou un groupe à une application d’entreprise</span><span class="sxs-lookup"><span data-stu-id="1ba24-116">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-thousandeyes"></a><span data-ttu-id="1ba24-117">Conseils importants concernant l’affectation d’utilisateurs à ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="1ba24-117">Important tips for assigning users to ThousandEyes</span></span>

*   <span data-ttu-id="1ba24-118">Il est recommandé de n’affecter qu’un seul utilisateur Azure AD à ThousandEyes afin de tester la configuration de l’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="1ba24-118">It is recommended that a single Azure AD user is assigned to ThousandEyes to test the provisioning configuration.</span></span> <span data-ttu-id="1ba24-119">Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="1ba24-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="1ba24-120">Quand vous affectez un utilisateur à ThousandEyes, vous devez sélectionner le rôle **utilisateur** ou un autre rôle valide propre à l’application (si disponible) dans la boîte de dialogue d’affectation.</span><span class="sxs-lookup"><span data-stu-id="1ba24-120">When assigning a user to ThousandEyes, you must select either the **User** role, or another valid application-specific role (if available) in the assignment dialog.</span></span> <span data-ttu-id="1ba24-121">Le rôle **Accès par défaut** ne fonctionne pas pour l’approvisionnement, et ces utilisateurs sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="1ba24-121">The **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-to-thousandeyes"></a><span data-ttu-id="1ba24-122">Configuration de l'approvisionnement d’utilisateurs pour ThousandEyes</span><span class="sxs-lookup"><span data-stu-id="1ba24-122">Configuring user provisioning to ThousandEyes</span></span> 

<span data-ttu-id="1ba24-123">Cette section va vous guider afin de connecter votre instance Azure AD à l’API d’approvisionnement de comptes d’utilisateur de ThousandEyes, puis configurer le service d’approvisionnement pour créer, mettre à jour et désactiver des comptes d’utilisateur affectés dans ThousandEyes, en fonction des affectations d’utilisateurs et de groupes dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1ba24-123">This section guides you through connecting your Azure AD to ThousandEyes's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in ThousandEyes based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="1ba24-124">Vous pouvez également choisir d’activer l’authentification unique basée sur SAML pour ThousandEyes, grâce aux instructions disponibles dans le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1ba24-124">You may also choose to enabled SAML-based Single Sign-On for ThousandEyes, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="1ba24-125">L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que chacune de ces deux fonctionnalités compléte l’autre.</span><span class="sxs-lookup"><span data-stu-id="1ba24-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-to-thousandeyes-in-azure-ad"></a><span data-ttu-id="1ba24-126">Configurer l’approvisionnement automatique de comptes d’utilisateur pour ThousandEyes dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ba24-126">Configure automatic user account provisioning to ThousandEyes in Azure AD</span></span>


1. <span data-ttu-id="1ba24-127">Dans le [portail Azure](https://portal.azure.com), accédez à la section **Azure Active Directory > Applications d’entreprise > Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1ba24-127">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="1ba24-128">Si vous avez déjà configuré ThousandEyes pour l’authentification unique, recherchez votre instance de ThousandEyes à l’aide du champ de recherche.</span><span class="sxs-lookup"><span data-stu-id="1ba24-128">If you have already configured ThousandEyes for single sign-on, search for your instance of ThousandEyes using the search field.</span></span> <span data-ttu-id="1ba24-129">Sinon, sélectionnez **Ajouter** et recherchez **ThousandEyes** dans la galerie d’applications.</span><span class="sxs-lookup"><span data-stu-id="1ba24-129">Otherwise, select **Add** and search for **ThousandEyes** in the application gallery.</span></span> <span data-ttu-id="1ba24-130">Dans les résultats de la recherche, sélectionnez ThousandEyes, puis ajoutez-le à votre liste d’applications.</span><span class="sxs-lookup"><span data-stu-id="1ba24-130">Select ThousandEyes from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="1ba24-131">Sélectionnez votre instance de ThousandEyes, puis sélectionnez l’onglet **Approvisionnement**.</span><span class="sxs-lookup"><span data-stu-id="1ba24-131">Select your instance of ThousandEyes, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="1ba24-132">Définissez le **Mode d’approvisionnement** sur **Automatique**.</span><span class="sxs-lookup"><span data-stu-id="1ba24-132">Set the **Provisioning Mode** to **Automatic**.</span></span>

    ![Approvisionnement de ThousandEyes](./media/active-directory-saas-thousandeyes-provisioning-tutorial/ThousandEyes1.png)

5. <span data-ttu-id="1ba24-134">Dans la section **Informations d’identification de l’administrateur**, entrez le **jeton secret** généré par votre compte ThousandEyes (ce dernier se trouve dans votre compte ThousandEyes : **Sécurité et authentification**).</span><span class="sxs-lookup"><span data-stu-id="1ba24-134">Under the **Admin Credentials** section, input the **Secret Token** generated by your ThousandEyes's account (you can find the token under your ThousandEyes account: **Security & Authentication**).</span></span> 

    ![Approvisionnement de ThousandEyes](./media/active-directory-saas-thousandeyes-provisioning-tutorial/ThousandEyes2.png)

6. <span data-ttu-id="1ba24-136">Dans le portail Azure, cliquez sur **Tester la connexion** pour vous assurer qu’Azure AD peut se connecter à votre application ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="1ba24-136">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your ThousandEyes app.</span></span> <span data-ttu-id="1ba24-137">Si la connexion échoue, vérifiez que votre compte ThousandEyes dispose des autorisations d’administrateur et réessayez l’étape 5.</span><span class="sxs-lookup"><span data-stu-id="1ba24-137">If the connection fails, ensure your ThousandEyes account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="1ba24-138">Entrez l’adresse e-mail d’une personne ou d’un groupe qui doit recevoir les notifications d’erreur d’approvisionnement dans le champ **E-mail de notification**, puis cochez la case « Envoyer une notification par e-mail en cas de défaillance ».</span><span class="sxs-lookup"><span data-stu-id="1ba24-138">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="1ba24-139">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="1ba24-139">Click **Save**.</span></span> 

9. <span data-ttu-id="1ba24-140">Dans la section Mappages, sélectionnez **Synchroniser les utilisateurs Azure Active Directory avec ThousandEyes**.</span><span class="sxs-lookup"><span data-stu-id="1ba24-140">Under the Mappings section, select **Synchronize Azure Active Directory Users to ThousandEyes**.</span></span>

10. <span data-ttu-id="1ba24-141">Dans la section **Mappages d’attributs**, passez en revue les attributs utilisateur qui sont synchronisés à partir d’Azure AD vers ThousandEyes.</span><span class="sxs-lookup"><span data-stu-id="1ba24-141">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to ThousandEyes.</span></span> <span data-ttu-id="1ba24-142">Les attributs sélectionnés en tant que propriétés de **Correspondance** sont utilisés pour faire correspondre les comptes d’utilisateur dans ThousandEyes pour les opérations de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="1ba24-142">The attributes selected as **Matching** properties are used to match the user accounts in ThousandEyes for update operations.</span></span> <span data-ttu-id="1ba24-143">Cliquez sur le bouton Enregistrer pour valider les modifications.</span><span class="sxs-lookup"><span data-stu-id="1ba24-143">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="1ba24-144">Pour activer le service d’approvisionnement Azure AD pour ThousandEyes, accédez à la section **Paramètres** et définissez le **Statut de l’approvisionnement** sur **Activé**.</span><span class="sxs-lookup"><span data-stu-id="1ba24-144">To enable the Azure AD provisioning service for ThousandEyes, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

12. <span data-ttu-id="1ba24-145">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="1ba24-145">Click **Save**.</span></span> 

<span data-ttu-id="1ba24-146">Cette opération démarre la synchronisation initiale des utilisateurs et/ou des groupes affectés à ThousandEyes dans la section Utilisateurs et groupes.</span><span class="sxs-lookup"><span data-stu-id="1ba24-146">This operation starts the initial synchronization of any users and/or groups assigned to ThousandEyes in the Users and Groups section.</span></span> <span data-ttu-id="1ba24-147">La synchronisation initiale prend plus de temps que les synchronisations suivantes, qui se produisent environ toutes les 20 minutes, tant que le service est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="1ba24-147">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="1ba24-148">Vous pouvez utiliser la section **Détails de la synchronisation** pour surveiller la progression et suivre les liens vers les rapports d’activité d’approvisionnement, qui décrivent toutes les actions effectuées par le service d’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="1ba24-148">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service.</span></span>

<span data-ttu-id="1ba24-149">Pour plus d’informations sur la lecture des journaux d’approvisionnement Azure AD, consultez [Création de rapports sur l’approvisionnement automatique de comptes d’utilisateur](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="1ba24-149">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="1ba24-150">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="1ba24-150">Additional resources</span></span>

* [<span data-ttu-id="1ba24-151">Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise</span><span class="sxs-lookup"><span data-stu-id="1ba24-151">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="1ba24-152">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="1ba24-152">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="1ba24-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1ba24-153">Next steps</span></span>

* [<span data-ttu-id="1ba24-154">Découvrez comment consulter les journaux et obtenir des rapports sur l’activité d’approvisionnement</span><span class="sxs-lookup"><span data-stu-id="1ba24-154">Learn how to review logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
