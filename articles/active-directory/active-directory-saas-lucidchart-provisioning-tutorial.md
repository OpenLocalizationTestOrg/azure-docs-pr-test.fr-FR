---
title: "Didacticiel : Configuration de LucidChart pour l’approvisionnement automatique d’utilisateurs avec Azure Active Directory | Microsoft Docs"
description: "Découvrez comment configurer Azure Active Directory pour approvisionner et retirer automatiquement des comptes utilisateur sur LucidChart."
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
ms.openlocfilehash: 1f9344a5e750360e21ed7dc8e3ed013c2c2e1a45
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-configuring-lucidchart-for-automatic-user-provisioning"></a><span data-ttu-id="8e7ee-103">Didacticiel : configuration de LucidChart pour l’approvisionnement automatique d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="8e7ee-103">Tutorial: Configuring LucidChart for Automatic User Provisioning</span></span>


<span data-ttu-id="8e7ee-104">L’objectif de ce didacticiel est de vous montrer la procédure à suivre dans LucidChart et Azure AD pour approvisionner et retirer automatiquement des comptes utilisateur Azure AD sur LucidChart.</span><span class="sxs-lookup"><span data-stu-id="8e7ee-104">The objective of this tutorial is to show you the steps you need to perform in LucidChart and Azure AD to automatically provision and de-provision user accounts from Azure AD to LucidChart.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="8e7ee-105">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="8e7ee-105">Prerequisites</span></span>

<span data-ttu-id="8e7ee-106">Le scénario décrit dans ce didacticiel part du principe que vous disposez des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="8e7ee-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="8e7ee-107">Un locataire Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8e7ee-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="8e7ee-108">Un locataire LucidChart avec le [plan d’entreprise](https://www.lucidchart.com/user/117598685#/subscriptionLevel) ou supérieur activé</span><span class="sxs-lookup"><span data-stu-id="8e7ee-108">A LucidChart tenant with the [Enterprise plan](https://www.lucidchart.com/user/117598685#/subscriptionLevel) or better enabled</span></span> 
*   <span data-ttu-id="8e7ee-109">Un compte utilisateur dans LucidChart avec des autorisations d’administrateur</span><span class="sxs-lookup"><span data-stu-id="8e7ee-109">A user account in LucidChart with Admin permissions</span></span> 

## <a name="assigning-users-to-lucidchart"></a><span data-ttu-id="8e7ee-110">Affectation d’utilisateurs à LucidChart</span><span class="sxs-lookup"><span data-stu-id="8e7ee-110">Assigning users to LucidChart</span></span>

<span data-ttu-id="8e7ee-111">Azure Active Directory utilise un concept appelé « affectations » pour déterminer les utilisateurs devant recevoir l’accès aux applications sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="8e7ee-111">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="8e7ee-112">Dans le cadre de l’approvisionnement automatique de comptes utilisateur, les utilisateurs et les groupes qui ont été « affectés » à une application dans Azure AD sont synchronisés.</span><span class="sxs-lookup"><span data-stu-id="8e7ee-112">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="8e7ee-113">Avant de configurer et d’activer le service d’approvisionnement, vous devez déterminer quels utilisateurs et/ou groupes dans Azure AD représentent les utilisateurs qui ont besoin d’accéder à votre application LucidChart.</span><span class="sxs-lookup"><span data-stu-id="8e7ee-113">Before configuring and enabling the provisioning service, you need to decide what users and/or groups in Azure AD represent the users who need access to your LucidChart app.</span></span> <span data-ttu-id="8e7ee-114">Dès que vous avez fait votre choix, vous pouvez assigner ces utilisateurs à votre application LucidChart en suivant les instructions disponibles à la page suivante :</span><span class="sxs-lookup"><span data-stu-id="8e7ee-114">Once decided, you can assign these users to your LucidChart app by following the instructions here:</span></span>

[<span data-ttu-id="8e7ee-115">Affecter un utilisateur ou un groupe à une application d’entreprise</span><span class="sxs-lookup"><span data-stu-id="8e7ee-115">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-lucidchart"></a><span data-ttu-id="8e7ee-116">Conseils importants concernant l’assignation d’utilisateurs à LucidChart</span><span class="sxs-lookup"><span data-stu-id="8e7ee-116">Important tips for assigning users to LucidChart</span></span>

*   <span data-ttu-id="8e7ee-117">Il est recommandé de n’assigner qu’un seul utilisateur Azure AD à LucidChart afin de tester la configuration de l’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="8e7ee-117">It is recommended that a single Azure AD user is assigned to LucidChart to test the provisioning configuration.</span></span> <span data-ttu-id="8e7ee-118">Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="8e7ee-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="8e7ee-119">Lorsque vous affectez un utilisateur à LucidChart, vous devez sélectionner le rôle **utilisateur** ou un autre rôle valide spécifique de l’application (si disponible) dans la boîte de dialogue d’affectation.</span><span class="sxs-lookup"><span data-stu-id="8e7ee-119">When assigning a user to LucidChart, you must select either the **User** role, or another valid application-specific role (if available) in the assignment dialog.</span></span> <span data-ttu-id="8e7ee-120">Le rôle **Accès par défaut** ne fonctionne pas pour l’approvisionnement, et ces utilisateurs sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="8e7ee-120">The **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-to-lucidchart"></a><span data-ttu-id="8e7ee-121">Configuration de l’approvisionnement des utilisateurs sur LucidChart</span><span class="sxs-lookup"><span data-stu-id="8e7ee-121">Configuring user provisioning to LucidChart</span></span> 

<span data-ttu-id="8e7ee-122">Cette section vous guide afin de connecter votre instance Azure AD à votre compte utilisateur LucidChart qui fournit l’API. À l’aide de ce guide, découvrez aussi comment configurer le service d’approvisionnement afin de créer, mettre à jour et désactiver des comptes utilisateur assignés dans LucidChart, en fonction des attributions d’utilisateur et de groupe dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e7ee-122">This section guides you through connecting your Azure AD to LucidChart's user account provisioning API, and configuring the provisioning service to create, update, and disable assigned user accounts in LucidChart based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="8e7ee-123">Vous pouvez également choisir d’activer l’authentification unique basée sur SAML pour LucidChart, grâce aux instructions disponibles dans le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8e7ee-123">You may also choose to enabled SAML-based Single Sign-On for LucidChart, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="8e7ee-124">L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que chacune de ces deux fonctionnalités compléte l’autre.</span><span class="sxs-lookup"><span data-stu-id="8e7ee-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-to-lucidchart-in-azure-ad"></a><span data-ttu-id="8e7ee-125">Configurer l’approvisionnement automatique de comptes utilisateur vers LucidChart dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e7ee-125">Configure automatic user account provisioning to LucidChart in Azure AD</span></span>


1. <span data-ttu-id="8e7ee-126">Dans le [portail Azure](https://portal.azure.com), accédez à la section **Azure Active Directory > Applications d’entreprise > Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8e7ee-126">In the [Azure portal](https://portal.azure.com), browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="8e7ee-127">Si vous avez déjà configuré LucidChart pour l’authentification unique, recherchez votre instance de LucidChart à l’aide du champ de recherche.</span><span class="sxs-lookup"><span data-stu-id="8e7ee-127">If you have already configured LucidChart for single sign-on, search for your instance of LucidChart using the search field.</span></span> <span data-ttu-id="8e7ee-128">Sinon, sélectionnez **Ajouter** et effectuer une recherche pour **LucidChart** dans la galerie d’applications.</span><span class="sxs-lookup"><span data-stu-id="8e7ee-128">Otherwise, select **Add** and search for **LucidChart** in the application gallery.</span></span> <span data-ttu-id="8e7ee-129">Dans les résultats de la recherche, sélectionnez LucidChart, puis ajoutez-le à votre liste d’applications.</span><span class="sxs-lookup"><span data-stu-id="8e7ee-129">Select LucidChart from the search results, and add it to your list of applications.</span></span>

3. <span data-ttu-id="8e7ee-130">Sélectionnez votre instance de LucidChart, puis sélectionnez l’onglet **Approvisionnement**.</span><span class="sxs-lookup"><span data-stu-id="8e7ee-130">Select your instance of LucidChart, then select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="8e7ee-131">Définissez le **Mode d’approvisionnement** sur **Automatique**.</span><span class="sxs-lookup"><span data-stu-id="8e7ee-131">Set the **Provisioning Mode** to **Automatic**.</span></span>

    ![Approvisionnement de LucidChart](./media/active-directory-saas-lucidchart-provisioning-tutorial/LucidChart1.png)

5. <span data-ttu-id="8e7ee-133">Dans la section **Informations d’identification de l’administrateur**, entrez le **Jeton secret** généré par votre compte LucidChart (vous pouvez rechercher le jeton sous votre compte : **Team (Équipe)** > **App Integration (Intégration de l’application)** > **SCIM**).</span><span class="sxs-lookup"><span data-stu-id="8e7ee-133">Under the **Admin Credentials** section, input the **Secret Token** generated by your LucidChart's account (you can find the token under your account: **Team** > **App Integration** > **SCIM**).</span></span> 

    ![Approvisionnement de LucidChart](./media/active-directory-saas-lucidchart-provisioning-tutorial/LucidChart2.png)

6. <span data-ttu-id="8e7ee-135">Dans le portail Azure, cliquez sur **Tester la connexion** pour vérifier qu’Azure AD peut se connecter à votre application LucidChart.</span><span class="sxs-lookup"><span data-stu-id="8e7ee-135">In the Azure portal, click **Test Connection** to ensure Azure AD can connect to your LucidChart app.</span></span> <span data-ttu-id="8e7ee-136">Si la connexion échoue, vérifiez que votre compte LucidChart dispose des autorisations d’administrateur et réessayez l’étape 5.</span><span class="sxs-lookup"><span data-stu-id="8e7ee-136">If the connection fails, ensure your LucidChart account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="8e7ee-137">Entrez l’adresse de courrier d’une personne ou d’un groupe qui doit recevoir les notifications d’erreur d’approvisionnement dans le champ **E-mail de notification**, puis cochez la case « Envoyer une notification par e-mail en cas de défaillance ».</span><span class="sxs-lookup"><span data-stu-id="8e7ee-137">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="8e7ee-138">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="8e7ee-138">Click **Save**.</span></span> 

9. <span data-ttu-id="8e7ee-139">Dans la section Mappages, sélectionnez **Synchroniser les utilisateurs Azure Active Directory avec LucidChart**.</span><span class="sxs-lookup"><span data-stu-id="8e7ee-139">Under the Mappings section, select **Synchronize Azure Active Directory Users to LucidChart**.</span></span>

10. <span data-ttu-id="8e7ee-140">Dans la section **Mappages d’attributs**, passez en revue les attributs utilisateur qui sont synchronisés d’Azure AD vers LucidChart.</span><span class="sxs-lookup"><span data-stu-id="8e7ee-140">In the **Attribute Mappings** section, review the user attributes that are synchronized from Azure AD to LucidChart.</span></span> <span data-ttu-id="8e7ee-141">Les attributs sélectionnés en tant que propriétés de **Correspondance** sont utilisés pour faire correspondre les comptes utilisateur dans LucidChart pour les opérations de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="8e7ee-141">The attributes selected as **Matching** properties are used to match the user accounts in LucidChart for update operations.</span></span> <span data-ttu-id="8e7ee-142">Cliquez sur le bouton Enregistrer pour valider les modifications.</span><span class="sxs-lookup"><span data-stu-id="8e7ee-142">Select the Save button to commit any changes.</span></span>

11. <span data-ttu-id="8e7ee-143">Pour activer le service d’approvisionnement Azure AD pour LucidChart, accédez à la section **Paramètres** et définissez l’**État de l’approvisionnement** sur **Activé**.</span><span class="sxs-lookup"><span data-stu-id="8e7ee-143">To enable the Azure AD provisioning service for LucidChart, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

12. <span data-ttu-id="8e7ee-144">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="8e7ee-144">Click **Save**.</span></span> 

<span data-ttu-id="8e7ee-145">Cette commande démarre la synchronisation initiale des utilisateurs et/ou des groupes affectés à LucidChart dans la section Utilisateurs et Groupes.</span><span class="sxs-lookup"><span data-stu-id="8e7ee-145">This operation starts the initial synchronization of any users and/or groups assigned to LucidChart in the Users and Groups section.</span></span> <span data-ttu-id="8e7ee-146">La synchronisation initiale prend plus de temps que les synchronisations suivantes, qui se produisent environ toutes les 20 minutes, tant que le service est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="8e7ee-146">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="8e7ee-147">Vous pouvez utiliser la section **Détails de la synchronisation** pour surveiller la progression et suivre les liens vers les rapports d’activité d’approvisionnement, qui décrivent toutes les actions effectuées par le service d’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="8e7ee-147">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service.</span></span>

<span data-ttu-id="8e7ee-148">Pour plus d’informations sur la lecture des journaux d’approvisionnement Azure AD, consultez [Création de rapports sur l’approvisionnement automatique de comptes d’utilisateur](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="8e7ee-148">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="8e7ee-149">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="8e7ee-149">Additional resources</span></span>

* [<span data-ttu-id="8e7ee-150">Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise</span><span class="sxs-lookup"><span data-stu-id="8e7ee-150">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="8e7ee-151">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="8e7ee-151">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="8e7ee-152">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8e7ee-152">Next steps</span></span>

* [<span data-ttu-id="8e7ee-153">Découvrez comment consulter les journaux et obtenir des rapports sur l’activité d’approvisionnement</span><span class="sxs-lookup"><span data-stu-id="8e7ee-153">Learn how to review logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
