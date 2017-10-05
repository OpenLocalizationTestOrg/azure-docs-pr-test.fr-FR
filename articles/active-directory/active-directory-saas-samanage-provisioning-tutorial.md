---
title: "Didacticiel : Configuration de Samanage pour l’approvisionnement automatique d’utilisateurs avec Azure Active Directory | Microsoft Docs"
description: "Découvrez comment configurer Azure Active Directory pour approvisionner et retirer automatiquement des comptes utilisateur sur Samanage."
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
ms.openlocfilehash: 278ebf464fbe815568fbe332f80d5ea6b29e1811
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-configuring-samanage-for-automatic-user-provisioning"></a><span data-ttu-id="7094c-103">Didacticiel : configuration de Samanage pour l’approvisionnement automatique d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="7094c-103">Tutorial: Configuring Samanage for Automatic User Provisioning</span></span>


<span data-ttu-id="7094c-104">L’objectif de ce didacticiel est de vous montrer la procédure à suivre dans Samanage et Azure AD pour approvisionner et retirer automatiquement des comptes utilisateur Azure AD vers Samanage.</span><span class="sxs-lookup"><span data-stu-id="7094c-104">The objective of this tutorial is to show you the steps you need to perform in Samanage and Azure AD to automatically provision and de-provision user accounts from Azure AD to Samanage.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="7094c-105">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="7094c-105">Prerequisites</span></span>

<span data-ttu-id="7094c-106">Le scénario décrit dans ce didacticiel part du principe que vous disposez des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="7094c-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="7094c-107">Un locataire Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7094c-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="7094c-108">Un locataire Samanage avec le [plan professionnel](https://www.samanage.com/pricing/) ou mieux activé</span><span class="sxs-lookup"><span data-stu-id="7094c-108">A Samanage tenant with the [Professional plan](https://www.samanage.com/pricing/) or better enabled</span></span> 
*   <span data-ttu-id="7094c-109">Un compte d’utilisateur dans Samanage avec des autorisations d’administrateur</span><span class="sxs-lookup"><span data-stu-id="7094c-109">A user account in Samanage with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="7094c-110">L’intégration de l’approvisionnement Azure AD s’appuie sur l’[API REST Samanage](https://www.samanage.com/api/), qui est disponible pour les équipes Samanage disposant du plan professionnel ou mieux.</span><span class="sxs-lookup"><span data-stu-id="7094c-110">The Azure AD provisioning integration relies on the [Samanage REST API](https://www.samanage.com/api/), which is available to Samanage teams on the Professional plan or better.</span></span>

## <a name="assigning-users-to-samanage"></a><span data-ttu-id="7094c-111">Affectation d’utilisateurs à Samanage</span><span class="sxs-lookup"><span data-stu-id="7094c-111">Assigning users to Samanage</span></span>

<span data-ttu-id="7094c-112">Azure Active Directory utilise un concept appelé « affectations » pour déterminer les utilisateurs devant recevoir l’accès aux applications sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="7094c-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="7094c-113">Dans le cadre de l’approvisionnement automatique de comptes utilisateur, les utilisateurs et les groupes qui ont été « affectés » à une application dans Azure AD sont synchronisés.</span><span class="sxs-lookup"><span data-stu-id="7094c-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="7094c-114">Avant de configurer et d’activer le service d’approvisionnement, vous devez déterminer quels utilisateurs et/ou groupes dans Azure AD représentent les utilisateurs qui ont besoin d’accéder à votre application Samanage.</span><span class="sxs-lookup"><span data-stu-id="7094c-114">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your Samanage app.</span></span> <span data-ttu-id="7094c-115">Une fois que vous avez choisi, vous pouvez affecter ces utilisateurs à votre application Samanage en suivant les instructions fournies ici :</span><span class="sxs-lookup"><span data-stu-id="7094c-115">Once decided, you can assign these users to your Samanage app by following the instructions here:</span></span>

[<span data-ttu-id="7094c-116">Affecter un utilisateur ou un groupe à une application d’entreprise</span><span class="sxs-lookup"><span data-stu-id="7094c-116">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-samanage"></a><span data-ttu-id="7094c-117">Conseils importants pour l’affectation d’utilisateurs à Samanage</span><span class="sxs-lookup"><span data-stu-id="7094c-117">Important tips for assigning users to Samanage</span></span>

*   <span data-ttu-id="7094c-118">Il est recommandé de n’assigner qu’un seul utilisateur Azure AD à Samanage afin de tester la configuration de l’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="7094c-118">It is recommended that a single Azure AD user is assigned to Samanage to test the provisioning configuration.</span></span> <span data-ttu-id="7094c-119">Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="7094c-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="7094c-120">Quand vous affectez un utilisateur à Samanage, vous devez sélectionner le rôle **utilisateur** ou un autre rôle valide propre à l’application (si disponible) dans la boîte de dialogue d’affectation.</span><span class="sxs-lookup"><span data-stu-id="7094c-120">When assigning a user to Samanage, you must select either the **User** role, or another valid application-specific role (if available) in the assignment dialog.</span></span> <span data-ttu-id="7094c-121">Le rôle **Accès par défaut** ne fonctionne pas pour l’approvisionnement, et ces utilisateurs sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="7094c-121">The **Default Access** role does not work for provisioning, and these users are skipped.</span></span>

> [!NOTE]
> <span data-ttu-id="7094c-122">En guise de fonctionnalité ajoutée, le service d’approvisionnement lit les rôles personnalisés définis dans Samanage et les importe dans Azure AD où vous pouvez les sélectionner dans la boîte de dialogue Select Role.</span><span class="sxs-lookup"><span data-stu-id="7094c-122">As an added feature, the provisioning service reads any custom roles defined in Samanage, and imports them into Azure AD where they can be selected in the Select Role dialog.</span></span> <span data-ttu-id="7094c-123">Ces rôles sont visibles dans le portail Azure une fois que le service d’approvisionnement a été activé et qu’un cycle de synchronisation s’est achevé.</span><span class="sxs-lookup"><span data-stu-id="7094c-123">These roles will be visible in the Azure portal after the provisioning service is enabled and one synchronization cycle has completed.</span></span>

## <a name="configuring-user-provisioning-to-samanage"></a><span data-ttu-id="7094c-124">Configuration de l'approvisionnement des utilisateurs sur Samanage</span><span class="sxs-lookup"><span data-stu-id="7094c-124">Configuring user provisioning to Samanage</span></span> 

<span data-ttu-id="7094c-125">Cette section vous guide à travers la connexion de votre Azure AD au compte d’utilisateur de Samanage fournissant l’API et la configuration du service d’approvisionnement pour créer, mettre à jour et désactiver les comptes utilisateur affectés dans Samanage en fonction des attributions d’utilisateurs et de groupes dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7094c-125">This section guides you through connecting your Azure AD to Samanage's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in Samanage based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="7094c-126">Vous pouvez également choisir d’activer l’authentification unique basée sur SAML pour Samanage, grâce aux instructions disponibles dans le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7094c-126">You may also choose to enabled SAML-based Single Sign-On for Samanage, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="7094c-127">L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que chacune de ces deux fonctionnalités compléte l’autre.</span><span class="sxs-lookup"><span data-stu-id="7094c-127">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-to-samanage-in-azure-ad"></a><span data-ttu-id="7094c-128">Configurer l’approvisionnement automatique de comptes utilisateur vers Samanage dans Azure AD :</span><span class="sxs-lookup"><span data-stu-id="7094c-128">Configure automatic user account provisioning to Samanage in Azure AD:</span></span>


1. <span data-ttu-id="7094c-129">Dans le [portail Azure](https://portal.azure.com), accédez à la section **Azure Active Directory > Applications d’entreprise > Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="7094c-129">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="7094c-130">Si vous avez déjà configuré Samanage pour l’authentification unique, recherchez votre instance de Samanage à l’aide du champ de recherche.</span><span class="sxs-lookup"><span data-stu-id="7094c-130">If you have already configured Samanage for single sign-on, search for your instance of Samanage using the search field.</span></span> <span data-ttu-id="7094c-131">Sinon, sélectionnez **Ajouter** et effectuer une recherche pour **Samanage** dans la galerie d’applications.</span><span class="sxs-lookup"><span data-stu-id="7094c-131">Otherwise, select **Add** and search for **Samanage** in the application gallery.</span></span> <span data-ttu-id="7094c-132">Dans les résultats de la recherche, sélectionnez Samanage, puis ajoutez-le à votre liste d’applications.</span><span class="sxs-lookup"><span data-stu-id="7094c-132">Select Samanage from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="7094c-133">Sélectionnez votre instance de Samanage, puis sélectionnez l’onglet **Approvisionnement**.</span><span class="sxs-lookup"><span data-stu-id="7094c-133">Select your instance of Samanage, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="7094c-134">Définissez le **Mode d’approvisionnement** sur **Automatique**.</span><span class="sxs-lookup"><span data-stu-id="7094c-134">Set the **Provisioning Mode** to **Automatic**.</span></span>

    ![Approvisionnement de Samanage](./media/active-directory-saas-samanage-provisioning-tutorial/Samanage1.png)

5. <span data-ttu-id="7094c-136">Dans la section **Informations d’identification de l’administrateur**, entrez le **Nom d'utilisateur de l'administrateur et le Mot de passe d'administrateur** de votre compte Samanage.</span><span class="sxs-lookup"><span data-stu-id="7094c-136">Under the **Admin Credentials** section, input the **Admin Username&Admin Password** of your Samanage's account.</span></span> 

6. <span data-ttu-id="7094c-137">Dans le portail Azure, cliquez sur **Tester la connexion** pour vous assurer qu’Azure AD peut se connecter à votre application Samanage.</span><span class="sxs-lookup"><span data-stu-id="7094c-137">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your Samanage app.</span></span> <span data-ttu-id="7094c-138">Si la connexion échoue, vérifiez que votre compte Samanage dispose des autorisations d’administrateur et réessayez l’étape 5.</span><span class="sxs-lookup"><span data-stu-id="7094c-138">If the connection fails, ensure your Samanage account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="7094c-139">Entrez l’adresse de courrier d’une personne ou d’un groupe qui doit recevoir les notifications d’erreur d’approvisionnement dans le champ **E-mail de notification**, puis cochez la case « Envoyer une notification par e-mail en cas de défaillance ».</span><span class="sxs-lookup"><span data-stu-id="7094c-139">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="7094c-140">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="7094c-140">Click **Save**.</span></span> 

9. <span data-ttu-id="7094c-141">Dans la section Mappages, sélectionnez **Synchroniser les utilisateurs Azure Active Directory avec Samanage**.</span><span class="sxs-lookup"><span data-stu-id="7094c-141">Under the Mappings section, select **Synchronize Azure Active Directory Users to Samanage**.</span></span>

10. <span data-ttu-id="7094c-142">Dans la section **Mappages des attributs**, passez en revue les attributs utilisateur qui sont synchronisés d’Azure AD vers Samanage.</span><span class="sxs-lookup"><span data-stu-id="7094c-142">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to Samanage.</span></span> <span data-ttu-id="7094c-143">Les attributs sélectionnés en tant que propriétés de **Correspondance** sont utilisés pour faire correspondre les comptes d’utilisateur dans Samanage pour les opérations de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="7094c-143">The attributes selected as **Matching** properties are used to match the user accounts in Samanage for update operations.</span></span> <span data-ttu-id="7094c-144">Cliquez sur le bouton Enregistrer pour valider les modifications.</span><span class="sxs-lookup"><span data-stu-id="7094c-144">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="7094c-145">Pour activer le service d’approvisionnement Azure AD pour Samanage, modifiez le paramètre **État d’approvisionnement** sur **Activé** dans la section **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="7094c-145">To enable the Azure AD provisioning service for Samanage, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

12. <span data-ttu-id="7094c-146">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="7094c-146">Click **Save**.</span></span> 

<span data-ttu-id="7094c-147">Cette opération démarre la synchronisation initiale des utilisateurs et/ou des groupes affectés à Samanage dans la section Utilisateurs et Groupes.</span><span class="sxs-lookup"><span data-stu-id="7094c-147">This operation starts the initial synchronization of any users and/or groups assigned to Samanage in the Users and Groups section.</span></span> <span data-ttu-id="7094c-148">La synchronisation initiale prend plus de temps que les synchronisations suivantes, qui se produisent environ toutes les 20 minutes, tant que le service est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="7094c-148">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="7094c-149">Vous pouvez utiliser la section **Détails de la synchronisation** pour surveiller la progression et suivre les liens vers les rapports d’activité d’approvisionnement, qui décrivent toutes les actions effectuées par le service d’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="7094c-149">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service.</span></span>

<span data-ttu-id="7094c-150">Pour plus d’informations sur la lecture des journaux d’approvisionnement Azure AD, consultez [Création de rapports sur l’approvisionnement automatique de comptes d’utilisateur](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="7094c-150">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="7094c-151">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="7094c-151">Additional resources</span></span>

* [<span data-ttu-id="7094c-152">Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise</span><span class="sxs-lookup"><span data-stu-id="7094c-152">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="7094c-153">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="7094c-153">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="7094c-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7094c-154">Next steps</span></span>

* [<span data-ttu-id="7094c-155">Découvrez comment consulter les journaux et obtenir des rapports sur l’activité d’approvisionnement</span><span class="sxs-lookup"><span data-stu-id="7094c-155">Learn how to review logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
