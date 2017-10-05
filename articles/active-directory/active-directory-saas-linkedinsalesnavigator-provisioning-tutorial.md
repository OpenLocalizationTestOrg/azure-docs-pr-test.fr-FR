---
title: "Didacticiel : Configuration de LinkedIn Sales Navigator pour l’approvisionnement automatique d’utilisateurs avec Azure Active Directory | Microsoft Docs"
description: "Découvrez comment configurer Azure Active Directory pour approvisionner et déprovisionner automatiquement des comptes d’utilisateur sur LinkedIn Sales Navigator."
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
ms.date: 04/15/2017
ms.author: asmalser-msft
ms.openlocfilehash: 86357949c8e6927f78ca5bb8b7e20a6b88c37ef3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-configuring-linkedin-sales-navigator-for-automatic-user-provisioning"></a><span data-ttu-id="431b3-103">Didacticiel : Configuration de LinkedIn Sales Navigator pour approvisionner automatiquement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="431b3-103">Tutorial: Configuring LinkedIn Sales Navigator for Automatic User Provisioning</span></span>


<span data-ttu-id="431b3-104">L’objectif de ce didacticiel est de vous montrer les étapes à effectuer dans LinkedIn Sales Navigator et Azure AD pour approvisionner et déprovisionner automatiquement des comptes d’utilisateur d’Azure AD vers LinkedIn Sales Navigator.</span><span class="sxs-lookup"><span data-stu-id="431b3-104">The objective of this tutorial is to show you the steps you need to perform in LinkedIn Sales Navigator and Azure AD to automatically provision and de-provision user accounts from Azure AD to LinkedIn Sales Navigator.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="431b3-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="431b3-105">Prerequisites</span></span>

<span data-ttu-id="431b3-106">Le scénario décrit dans ce didacticiel part du principe que vous disposez des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="431b3-106">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

*   <span data-ttu-id="431b3-107">Un client Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="431b3-107">An Azure Active Directory tenant</span></span>
*   <span data-ttu-id="431b3-108">Un client LinkedIn Sales Navigator</span><span class="sxs-lookup"><span data-stu-id="431b3-108">A LinkedIn Sales Navigator tenant</span></span> 
*   <span data-ttu-id="431b3-109">Un compte d’administrateur dans LinkedIn Sales Navigator ayant accès au Centre des comptes LinkedIn</span><span class="sxs-lookup"><span data-stu-id="431b3-109">An administrator account in LinkedIn Sales Navigator with access to the LinkedIn Account Center</span></span>

> [!NOTE]
> <span data-ttu-id="431b3-110">Azure Active Directory s’intègre à LinkedIn Sales Navigator à l’aide du protocole [SCIM](http://www.simplecloud.info/).</span><span class="sxs-lookup"><span data-stu-id="431b3-110">Azure Active Directory integrates with LinkedIn Sales Navigator using the [SCIM](http://www.simplecloud.info/) protocol.</span></span>

## <a name="assigning-users-to-linkedin-sales-navigator"></a><span data-ttu-id="431b3-111">Affectation d’utilisateurs à LinkedIn Sales Navigator</span><span class="sxs-lookup"><span data-stu-id="431b3-111">Assigning users to LinkedIn Sales Navigator</span></span>

<span data-ttu-id="431b3-112">Azure Active Directory utilise un concept appelé « affectations » pour déterminer les utilisateurs devant recevoir l’accès aux applications sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="431b3-112">Azure Active Directory uses a concept called "assignments" to determine which users should receive access to selected apps.</span></span> <span data-ttu-id="431b3-113">Dans le cadre de l’approvisionnement automatique de comptes d’utilisateur, les utilisateurs et les groupes qui ont été « affectés » à une application dans Azure AD sont synchronisés.</span><span class="sxs-lookup"><span data-stu-id="431b3-113">In the context of automatic user account provisioning, only the users and groups that have been "assigned" to an application in Azure AD will be synchronized.</span></span> 

<span data-ttu-id="431b3-114">Avant de configurer et d’activer le service d’approvisionnement, vous devez déterminer quels utilisateurs et/ou groupes dans Azure AD représentent les utilisateurs qui ont besoin d’accéder à LinkedIn Sales Navigator.</span><span class="sxs-lookup"><span data-stu-id="431b3-114">Before configuring and enabling the provisioning service, you will need to decide what users and/or groups in Azure AD represent the users who need access to LinkedIn Sales Navigator.</span></span> <span data-ttu-id="431b3-115">Une fois que vous avez choisi, vous pouvez affecter ces utilisateurs à LinkedIn Sales Navigator en suivant les instructions fournies ici :</span><span class="sxs-lookup"><span data-stu-id="431b3-115">Once decided, you can assign these users to LinkedIn Sales Navigator by following the instructions here:</span></span>

[<span data-ttu-id="431b3-116">Affecter un utilisateur ou un groupe à une application d’entreprise</span><span class="sxs-lookup"><span data-stu-id="431b3-116">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-linkedin-sales-navigator"></a><span data-ttu-id="431b3-117">Conseils importants pour l’affectation d’utilisateurs à LinkedIn Sales Navigator</span><span class="sxs-lookup"><span data-stu-id="431b3-117">Important tips for assigning users to LinkedIn Sales Navigator</span></span>

*   <span data-ttu-id="431b3-118">Il est recommandé d’affecter un seul utilisateur Azure AD à LinkedIn Sales Navigator pour tester la configuration de l’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="431b3-118">It is recommended that a single Azure AD user be assigned to LinkedIn Sales Navigator to test the provisioning configuration.</span></span> <span data-ttu-id="431b3-119">Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="431b3-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="431b3-120">Quand vous affectez un utilisateur à LinkedIn Sales Navigator, vous devez sélectionner le rôle **Utilisateur** dans la boîte de dialogue d’affectation.</span><span class="sxs-lookup"><span data-stu-id="431b3-120">When assigning a user to LinkedIn Sales Navigator, you must select the **User** role in the assignment dialog.</span></span> <span data-ttu-id="431b3-121">Le rôle « Accès par défaut » ne fonctionne pas pour l’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="431b3-121">The "Default Access" role does not work for provisioning.</span></span>


## <a name="configuring-user-provisioning-to-linkedin-sales-navigator"></a><span data-ttu-id="431b3-122">Configuration de l’approvisionnement des utilisateurs sur LinkedIn Sales Navigator</span><span class="sxs-lookup"><span data-stu-id="431b3-122">Configuring user provisioning to LinkedIn Sales Navigator</span></span>

<span data-ttu-id="431b3-123">Cette section vous guide pour connecter votre instance d’Azure AD à l’API d’approvisionnement de comptes d’utilisateur SCIM de LinkedIn Sales Navigator et configurer le service d’approvisionnement pour créer, mettre à jour et désactiver des comptes d’utilisateur affectés dans LinkedIn Sales Navigator en fonction des affectations d’utilisateurs et de groupes dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="431b3-123">This section guides you through connecting your Azure AD to LinkedIn Sales Navigator's SCIM user account provisioning API, and configuring the provisioning service to create, update and disable assigned user accounts in LinkedIn Sales Navigator based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="431b3-124">Vous pouvez également choisir d’activer l’authentification unique basée sur SAML pour LinkedIn Sales Navigator en suivant les instructions fournies dans le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="431b3-124">You may also choose to enabled SAML-based Single Sign-On for LinkedIn Sales Navigator, following the instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="431b3-125">L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que ces deux fonctionnalités se complètent.</span><span class="sxs-lookup"><span data-stu-id="431b3-125">Single sign-on can be configured independently of automatic provisioning, though these two features complement each other.</span></span>


### <a name="to-configure-automatic-user-account-provisioning-to-linkedin-sales-navigator-in-azure-ad"></a><span data-ttu-id="431b3-126">Pour configurer l’approvisionnement automatique de comptes d’utilisateur sur LinkedIn Sales Navigator dans Azure AD :</span><span class="sxs-lookup"><span data-stu-id="431b3-126">To configure automatic user account provisioning to LinkedIn Sales Navigator in Azure AD:</span></span>


<span data-ttu-id="431b3-127">La première étape consiste à récupérer votre jeton d’accès LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="431b3-127">The first step is to retrieve your LinkedIn access token.</span></span> <span data-ttu-id="431b3-128">Si vous êtes administrateur d’entreprise, vous pouvez approvisionner vous-même un jeton d’accès.</span><span class="sxs-lookup"><span data-stu-id="431b3-128">If you are an Enterprise administrator, you can self-provision an access token.</span></span> <span data-ttu-id="431b3-129">Dans le Centre des comptes, accédez à **Paramètres &gt; Paramètres globaux**, puis ouvrez le panneau de configuration **SCIM**.</span><span class="sxs-lookup"><span data-stu-id="431b3-129">In your account center, go to **Settings &gt; Global Settings** and open the **SCIM Setup** panel.</span></span>

> [!NOTE]
> <span data-ttu-id="431b3-130">Si vous ouvrez le Centre des comptes directement plutôt qu’en passant par un lien, vous pouvez y accéder en effectuant les étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="431b3-130">If you are accessing the account center directly rather than through a link, you can reach it using the following steps.</span></span>

1)  <span data-ttu-id="431b3-131">Connectez-vous au Centre des comptes.</span><span class="sxs-lookup"><span data-stu-id="431b3-131">Sign in to Account Center.</span></span>

2)  <span data-ttu-id="431b3-132">Sélectionnez **Administrateur &gt; Paramètres d’administration**.</span><span class="sxs-lookup"><span data-stu-id="431b3-132">Select **Admin &gt; Admin Settings** .</span></span>

3)  <span data-ttu-id="431b3-133">Cliquez sur **Intégrations avancées** dans la barre latérale gauche.</span><span class="sxs-lookup"><span data-stu-id="431b3-133">Click **Advanced Integrations** on the left sidebar.</span></span> <span data-ttu-id="431b3-134">Vous êtes redirigé vers le Centre des comptes.</span><span class="sxs-lookup"><span data-stu-id="431b3-134">You are directed to the account center.</span></span>

4)  <span data-ttu-id="431b3-135">Cliquez sur **+ Ajouter une nouvelle configuration SCIM**, puis suivez la procédure en remplissant chaque champ.</span><span class="sxs-lookup"><span data-stu-id="431b3-135">Click **+ Add new SCIM configuration** and follow the procedure by filling in each field.</span></span>

> <span data-ttu-id="431b3-136">Si l’affectation automatique de licences n’est pas activée, cela signifie que seules les données utilisateur sont synchronisées.</span><span class="sxs-lookup"><span data-stu-id="431b3-136">When auto­assign licenses is not enabled, it means that only user data is synced.</span></span>

![Approvisionnement LinkedIn Sales Navigator](./media/active-directory-saas-linkedinsalesnavigator-provisioning-tutorial/linkedin_1.PNG)

> <span data-ttu-id="431b3-138">Quand l’affectation automatique de licences est activée, vous devez noter l’instance d’application et le type de licence.</span><span class="sxs-lookup"><span data-stu-id="431b3-138">When auto­license assignment is enabled, you need to note the application instance and license type.</span></span> <span data-ttu-id="431b3-139">Les licences sont toutes affectées sur le principe du « premier arrivé, premier servi ».</span><span class="sxs-lookup"><span data-stu-id="431b3-139">Licenses are assigned on a first come, first serve basis until all the licenses are taken.</span></span>

![Approvisionnement LinkedIn Sales Navigator](./media/active-directory-saas-linkedinsalesnavigator-provisioning-tutorial/linkedin_2.PNG)

5)  <span data-ttu-id="431b3-141">Cliquez sur **Générer un jeton**.</span><span class="sxs-lookup"><span data-stu-id="431b3-141">Click **Generate token**.</span></span> <span data-ttu-id="431b3-142">Un jeton d’accès doit s’afficher sous le champ **Jeton d’accès**.</span><span class="sxs-lookup"><span data-stu-id="431b3-142">You should see your access token display under the **Access token** field.</span></span>

6)  <span data-ttu-id="431b3-143">Enregistrez votre jeton d’accès dans votre Presse-papiers ou votre ordinateur avant de quitter la page.</span><span class="sxs-lookup"><span data-stu-id="431b3-143">Save your access token to your clipboard or computer before leaving the page.</span></span>

7) <span data-ttu-id="431b3-144">Ensuite, connectez-vous au [portail Azure](https://portal.azure.com), puis accédez à la section **Azure Active Directory > Applications d’entreprise > Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="431b3-144">Next, sign in to the [Azure portal](https://portal.azure.com), and browse to the **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

8) <span data-ttu-id="431b3-145">Si vous avez déjà configuré LinkedIn Sales Navigator pour l’authentification unique, recherchez votre instance de LinkedIn Sales Navigator à l’aide du champ de recherche.</span><span class="sxs-lookup"><span data-stu-id="431b3-145">If you have already configured LinkedIn Sales Navigator for single sign-on, search for your instance of LinkedIn Sales Navigator using the search field.</span></span> <span data-ttu-id="431b3-146">Sinon, sélectionnez **Ajouter**, puis recherchez **LinkedIn Sales Navigator** dans la galerie d’applications.</span><span class="sxs-lookup"><span data-stu-id="431b3-146">Otherwise, select **Add** and search for **LinkedIn Sales Navigator** in the application gallery.</span></span> <span data-ttu-id="431b3-147">Sélectionnez LinkedIn Sales Navigator dans les résultats de la recherche, puis ajoutez-le à votre liste d’applications.</span><span class="sxs-lookup"><span data-stu-id="431b3-147">Select LinkedIn Sales Navigator from the search results, and add it to your list of applications.</span></span>

9)  <span data-ttu-id="431b3-148">Sélectionnez votre instance de LinkedIn Sales Navigator, puis sélectionnez l’onglet **Approvisionnement**.</span><span class="sxs-lookup"><span data-stu-id="431b3-148">Select your instance of LinkedIn Sales Navigator, then select the **Provisioning** tab.</span></span>

10) <span data-ttu-id="431b3-149">Définissez le **Mode d’approvisionnement** sur **Automatique**.</span><span class="sxs-lookup"><span data-stu-id="431b3-149">Set the **Provisioning Mode** to **Automatic**.</span></span>

![Approvisionnement LinkedIn Sales Navigator](./media/active-directory-saas-linkedinsalesnavigator-provisioning-tutorial/linkedin_3.PNG)

11)  <span data-ttu-id="431b3-151">Renseignez les champs suivants sous **Informations d’identification de l’administrateur** :</span><span class="sxs-lookup"><span data-stu-id="431b3-151">Fill in the following fields under **Admin Credentials** :</span></span>

* <span data-ttu-id="431b3-152">Dans l’**URL de locataire**, entrez https://api.linkedin.com.</span><span class="sxs-lookup"><span data-stu-id="431b3-152">In the **Tenant URL** field, enter https://api.linkedin.com.</span></span>

* <span data-ttu-id="431b3-153">Dans le champ **Jeton secret**, entrez le jeton d’accès que vous avez généré à l’étape 1, puis cliquez sur **Tester la connexion**.</span><span class="sxs-lookup"><span data-stu-id="431b3-153">In the **Secret Token** field, enter the access token you generated in step 1 and click **Test Connection** .</span></span>

* <span data-ttu-id="431b3-154">Une notification de réussite doit s’afficher en haut à droite de votre portail.</span><span class="sxs-lookup"><span data-stu-id="431b3-154">You should see a success notification on the upper­right side of   your portal.</span></span>

12) <span data-ttu-id="431b3-155">Entrez l’adresse e-mail d’une personne ou d’un groupe qui doit recevoir les notifications d’erreur d’approvisionnement dans le champ **E-mail de notification**, puis cochez la case se trouvant en dessous.</span><span class="sxs-lookup"><span data-stu-id="431b3-155">Enter the email address of a person or group who should receive provisioning error notifications in the **Notification Email** field, and check the checkbox below.</span></span>

13) <span data-ttu-id="431b3-156">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="431b3-156">Click **Save**.</span></span> 

14) <span data-ttu-id="431b3-157">Dans la section **Mappages d’attributs**, passez en revue les attributs d’utilisateur et de groupe qui seront synchronisés d’Azure AD vers LinkedIn Sales Navigator.</span><span class="sxs-lookup"><span data-stu-id="431b3-157">In the **Attribute Mappings** section, review the user and group attributes that will be synchronized from Azure AD to LinkedIn Sales Navigator.</span></span> <span data-ttu-id="431b3-158">Notez que les attributs sélectionnés comme propriétés de **Correspondance** sont utilisés pour faire correspondre les comptes d’utilisateur et les groupes dans LinkedIn Sales Navigator pour les opérations de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="431b3-158">Note that the attributes selected as **Matching** properties will be used to match the user accounts and groups in LinkedIn Sales Navigator for update operations.</span></span> <span data-ttu-id="431b3-159">Cliquez sur le bouton Enregistrer pour valider les modifications.</span><span class="sxs-lookup"><span data-stu-id="431b3-159">Select the Save button to commit any changes.</span></span>

![Approvisionnement LinkedIn Sales Navigator](./media/active-directory-saas-linkedinsalesnavigator-provisioning-tutorial/linkedin_4.PNG)

15) <span data-ttu-id="431b3-161">Pour activer le service d’approvisionnement Azure AD pour LinkedIn Sales Navigator, définissez l’**État d’approvisionnement** sur **Activé** dans la section **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="431b3-161">To enable the Azure AD provisioning service for LinkedIn Sales Navigator, change the **Provisioning Status** to **On** in the **Settings** section</span></span>

16) <span data-ttu-id="431b3-162">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="431b3-162">Click **Save**.</span></span> 

<span data-ttu-id="431b3-163">Cette commande démarre la synchronisation initiale des utilisateurs et/ou groupes affectés à LinkedIn Sales Navigator dans la section Utilisateurs et groupes.</span><span class="sxs-lookup"><span data-stu-id="431b3-163">This will start the initial synchronization of any users and/or groups assigned to LinkedIn Sales Navigator in the Users and Groups section.</span></span> <span data-ttu-id="431b3-164">Notez que la synchronisation initiale prend plus de temps que les synchronisations suivantes, qui se produisent toutes les 20 minutes environ tant que le service est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="431b3-164">Note that the initial sync will take longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> <span data-ttu-id="431b3-165">Vous pouvez utiliser la section **Détails de la synchronisation** pour surveiller la progression et suivre les liens vers les rapports d’activité d’approvisionnement, qui décrivent toutes les actions effectuées par le service d’approvisionnement dans votre application LinkedIn Sales Navigator.</span><span class="sxs-lookup"><span data-stu-id="431b3-165">You can use the **Synchronization Details** section to monitor progress and follow links to provisioning activity reports, which describe all actions performed by the provisioning service on your LinkedIn Sales Navigator app.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="431b3-166">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="431b3-166">Additional Resources</span></span>

* [<span data-ttu-id="431b3-167">Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise</span><span class="sxs-lookup"><span data-stu-id="431b3-167">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="431b3-168">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="431b3-168">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
