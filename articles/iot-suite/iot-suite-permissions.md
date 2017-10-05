---
title: Azure IoT Suite et Azure Active Directory | Microsoft Docs
description: "Décrit comment Azure IoT Suite utilise Azure Active Directory pour gérer les autorisations."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 246228ba-954a-4d96-b6d6-e53e4590cb4f
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: dobett
ms.openlocfilehash: 518e6a481ab6385b03dd3ddc2e155fb724e677fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="permissions-on-the-azureiotsuitecom-site"></a><span data-ttu-id="ae91f-103">Autorisations sur le site azureiotsuite.com</span><span class="sxs-lookup"><span data-stu-id="ae91f-103">Permissions on the azureiotsuite.com site</span></span>

## <a name="what-happens-when-you-sign-in"></a><span data-ttu-id="ae91f-104">Que se passe-t-il lorsque vous vous connectez ?</span><span class="sxs-lookup"><span data-stu-id="ae91f-104">What happens when you sign in</span></span>

<span data-ttu-id="ae91f-105">Lorsque vous vous connectez pour la première fois à [azureiotsuite.com][lnk-azureiotsuite], le site détermine vos niveaux d’autorisation en fonction du client Azure Active Directory (AAD) et de l’abonnement Azure sélectionné.</span><span class="sxs-lookup"><span data-stu-id="ae91f-105">The first time you sign in at [azureiotsuite.com][lnk-azureiotsuite], the site determines the permission levels you have based on the currently selected Azure Active Directory (AAD) tenant and Azure subscription.</span></span>

1. <span data-ttu-id="ae91f-106">Tout d’abord, afin de remplir la liste des clients qui apparaît en regard de votre nom d’utilisateur, le site recherche dans Azure les clients ADD auxquels vous appartenez.</span><span class="sxs-lookup"><span data-stu-id="ae91f-106">First, to populate the list of tenants seen next to your username, the site finds out from Azure which AAD tenants you belong to.</span></span> <span data-ttu-id="ae91f-107">Actuellement, le site peut obtenir des jetons d’utilisateur pour un seul client.</span><span class="sxs-lookup"><span data-stu-id="ae91f-107">Currently, the site can only obtain user tokens for one tenant at a time.</span></span> <span data-ttu-id="ae91f-108">Par conséquent, lorsque vous basculez sur d’autres clients en utilisant la liste déroulante dans le coin supérieur droit, le site vous reconnecte à ce client pour obtenir les jetons pour ce client.</span><span class="sxs-lookup"><span data-stu-id="ae91f-108">Therefore, when you switch tenants using the dropdown in the top right corner, the site logs you in to that tenant to obtain the tokens for that tenant.</span></span>

2. <span data-ttu-id="ae91f-109">Ensuite, le site détecte à partir d’Azure, les abonnements que vous avez associés au client sélectionné.</span><span class="sxs-lookup"><span data-stu-id="ae91f-109">Next, the site finds out from Azure which subscriptions you have associated with the selected tenant.</span></span> <span data-ttu-id="ae91f-110">Vous pouvez voir les abonnements disponibles lorsque vous créez une nouvelle solution préconfigurée.</span><span class="sxs-lookup"><span data-stu-id="ae91f-110">You see the available subscriptions when you create a new preconfigured solution.</span></span>

3. <span data-ttu-id="ae91f-111">Enfin, le site extrait toutes les ressources dans les abonnements et les groupes de ressources marqués en tant que solutions préconfigurées et renseigne les mosaïques de la page d’accueil.</span><span class="sxs-lookup"><span data-stu-id="ae91f-111">Finally, the site retrieves all the resources in the subscriptions and resource groups tagged as preconfigured solutions and populates the tiles on the home page.</span></span>

<span data-ttu-id="ae91f-112">Les sections suivantes décrivent les rôles qui contrôlent l’accès aux solutions préconfigurées.</span><span class="sxs-lookup"><span data-stu-id="ae91f-112">The following sections describe the roles that control access to the preconfigured solutions.</span></span>

## <a name="aad-roles"></a><span data-ttu-id="ae91f-113">Rôles AAD</span><span class="sxs-lookup"><span data-stu-id="ae91f-113">AAD roles</span></span>

<span data-ttu-id="ae91f-114">Les rôles AAD contrôlent la possibilité d’approvisionnement de solutions préconfigurées et gèrent les utilisateurs dans une solution préconfigurée.</span><span class="sxs-lookup"><span data-stu-id="ae91f-114">The AAD roles control the ability provision preconfigured solutions and manage users in a preconfigured solution.</span></span>

<span data-ttu-id="ae91f-115">Pour plus d’informations sur les rôles d’administrateur dans ADD, consultez la page [Attribution de rôles d’administrateur dans Azure AD][lnk-aad-admin].</span><span class="sxs-lookup"><span data-stu-id="ae91f-115">You can find more information about administrator roles in AAD in [Assigning administrator roles in Azure AD][lnk-aad-admin].</span></span> <span data-ttu-id="ae91f-116">Cet article se concentre sur les rôles d’annuaire **Administrateur général** et **Utilisateur** tels qu’utilisés par les solutions préconfigurées.</span><span class="sxs-lookup"><span data-stu-id="ae91f-116">The current article focuses on the **Global Administrator** and the **User** directory roles as used by the preconfigured solutions.</span></span>

### <a name="global-administrator"></a><span data-ttu-id="ae91f-117">Administrateur général</span><span class="sxs-lookup"><span data-stu-id="ae91f-117">Global administrator</span></span>

<span data-ttu-id="ae91f-118">Il peut y avoir de nombreux administrateurs généraux pour chaque locataire AAD :</span><span class="sxs-lookup"><span data-stu-id="ae91f-118">There can be many global administrators per AAD tenant:</span></span>

* <span data-ttu-id="ae91f-119">Lorsque vous créez un client AAD, vous en devenez par défaut l’administrateur.</span><span class="sxs-lookup"><span data-stu-id="ae91f-119">When you create an AAD tenant, you are by default the global administrator of that tenant.</span></span>
* <span data-ttu-id="ae91f-120">L’administrateur général peut approvisionner une solution préconfigurée et se voir attribuer le rôle **Administrateur** de l’application au sein de son locataire AAD.</span><span class="sxs-lookup"><span data-stu-id="ae91f-120">The global administrator can provision a preconfigured solution and is assigned an **Admin** role for the application inside their AAD tenant.</span></span>
* <span data-ttu-id="ae91f-121">Si un autre utilisateur du même locataire AAD crée une application, le rôle attribué par défaut à l’administrateur général est **Lecture seule**.</span><span class="sxs-lookup"><span data-stu-id="ae91f-121">If another user in the same AAD tenant creates an application, the default role granted to the global administrator is **ReadOnly**.</span></span>
* <span data-ttu-id="ae91f-122">Les administrateurs généraux peuvent attribuer des rôles aux utilisateurs pour les applications à l’aide du [Portail Azure][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="ae91f-122">A global administrator can assign users to roles for applications using the [Azure portal][lnk-portal].</span></span>

### <a name="domain-user"></a><span data-ttu-id="ae91f-123">Utilisateur de domaine</span><span class="sxs-lookup"><span data-stu-id="ae91f-123">Domain user</span></span>

<span data-ttu-id="ae91f-124">Il peut y avoir de nombreux utilisateurs de domaine pour chaque locataire AAD :</span><span class="sxs-lookup"><span data-stu-id="ae91f-124">There can be many domain users per AAD tenant:</span></span>

* <span data-ttu-id="ae91f-125">Un utilisateur de domaine peut approvisionner une solution préconfigurée via le site [azureiotsuite.com][lnk-azureiotsuite].</span><span class="sxs-lookup"><span data-stu-id="ae91f-125">A domain user can provision a preconfigured solution through the [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="ae91f-126">Par défaut, l’utilisateur de domaine se voit accorder le rôle **Administrateur** dans l’application approvisionnée.</span><span class="sxs-lookup"><span data-stu-id="ae91f-126">By default, the domain user is granted the **Admin** role in the provisioned application.</span></span>
* <span data-ttu-id="ae91f-127">Un utilisateur de domaine peut créer une application à l’aide du script build.cmd qui se trouve dans le référentiel [azure-iot-remote-monitoring][lnk-rm-github-repo], [azure-iot-predictive-maintenance][lnk-pm-github-repo] ou [azure-iot-connected-factory][lnk-cf-github-repo].</span><span class="sxs-lookup"><span data-stu-id="ae91f-127">A domain user can create an application using the build.cmd script in the [azure-iot-remote-monitoring][lnk-rm-github-repo],  [azure-iot-predictive-maintenance][lnk-pm-github-repo], or [azure-iot-connected-factory][lnk-cf-github-repo] repository.</span></span> <span data-ttu-id="ae91f-128">Toutefois, le rôle accordé par défaut à l’utilisateur de domaine est **Lecture seule**, car un utilisateur de domaine n’est pas autorisé à attribuer des rôles.</span><span class="sxs-lookup"><span data-stu-id="ae91f-128">However, the default role granted to the domain user is **ReadOnly**, because a domain user does not have permission to assign roles.</span></span>
* <span data-ttu-id="ae91f-129">Si un autre utilisateur du locataire AAD crée une application, l’utilisateur de domaine se voit attribuer le rôle **Lecture seule** par défaut pour cette application.</span><span class="sxs-lookup"><span data-stu-id="ae91f-129">If another user in the AAD tenant creates an application, the domain user is assigned the **ReadOnly** role by default for that application.</span></span>
* <span data-ttu-id="ae91f-130">Un utilisateur de domaine ne peut pas attribuer des rôles pour des applications ; par conséquent, il ne peut pas ajouter des utilisateurs ou des rôles pour les utilisateurs d’une application, même s’ils l’ont approvisionnée.</span><span class="sxs-lookup"><span data-stu-id="ae91f-130">A domain user cannot assign roles for applications; therefore a domain user cannot add users or roles for users for an application even if they provisioned it.</span></span>

### <a name="guest-user"></a><span data-ttu-id="ae91f-131">Utilisateur invité</span><span class="sxs-lookup"><span data-stu-id="ae91f-131">Guest User</span></span>

<span data-ttu-id="ae91f-132">Il peut y avoir de nombreux utilisateurs invités pour chaque locataire AAD.</span><span class="sxs-lookup"><span data-stu-id="ae91f-132">There can be many guest users per AAD tenant.</span></span> <span data-ttu-id="ae91f-133">Les utilisateurs invités disposent d’un ensemble limité de droits au sein du client AAD.</span><span class="sxs-lookup"><span data-stu-id="ae91f-133">Guest users have a limited set of rights in the AAD tenant.</span></span> <span data-ttu-id="ae91f-134">Par conséquent, les utilisateurs invités ne peuvent pas approvisionner une solution préconfigurée dans le client AAD.</span><span class="sxs-lookup"><span data-stu-id="ae91f-134">As a result, guest users cannot provision a preconfigured solution in the AAD tenant.</span></span>

<span data-ttu-id="ae91f-135">Pour plus d’informations sur les utilisateurs et les rôles dans AAD, consultez les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="ae91f-135">For more information about users and roles in AAD, see the following resources:</span></span>

* <span data-ttu-id="ae91f-136">[Créer des utilisateurs dans Azure AD][lnk-create-edit-users]</span><span class="sxs-lookup"><span data-stu-id="ae91f-136">[Create users in Azure AD][lnk-create-edit-users]</span></span>
* <span data-ttu-id="ae91f-137">[Affecter des utilisateurs aux applications][lnk-assign-app-roles]</span><span class="sxs-lookup"><span data-stu-id="ae91f-137">[Assign users to apps][lnk-assign-app-roles]</span></span>

## <a name="azure-subscription-administrator-roles"></a><span data-ttu-id="ae91f-138">Rôles de l’administrateur d’abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="ae91f-138">Azure subscription administrator roles</span></span>

<span data-ttu-id="ae91f-139">Les rôles d’administration Azure permettent de contrôler la fonctionnalité de mappage d’un abonnement Azure sur un client AD.</span><span class="sxs-lookup"><span data-stu-id="ae91f-139">The Azure admin roles control the ability to map an Azure subscription to an AD tenant.</span></span>

<span data-ttu-id="ae91f-140">Pour plus d’informations sur les rôles d’administrateur Azure, consultez l’article [Guide pratique pour ajouter ou modifier le coadministrateur, l’administrateur de services fédérés et l’administrateur de compte][lnk-admin-roles].</span><span class="sxs-lookup"><span data-stu-id="ae91f-140">Find out more about the Azure admin roles in the article [How to add or change Azure Co-Administrator, Service Administrator, and Account Administrator][lnk-admin-roles].</span></span>

## <a name="application-roles"></a><span data-ttu-id="ae91f-141">Rôles d’application</span><span class="sxs-lookup"><span data-stu-id="ae91f-141">Application roles</span></span>

<span data-ttu-id="ae91f-142">Les rôles d’application contrôlent l’accès aux périphériques de votre solution préconfigurée.</span><span class="sxs-lookup"><span data-stu-id="ae91f-142">The application roles control access to devices in your preconfigured solution.</span></span>

<span data-ttu-id="ae91f-143">Une application approvisionnée comporte deux rôles définis et un rôle implicite défini :</span><span class="sxs-lookup"><span data-stu-id="ae91f-143">There are two defined roles and one implicit role defined in a provisioned application:</span></span>

* <span data-ttu-id="ae91f-144">**Administrateur :** contrôle totalement l’ajout, la gestion et la suppression des appareils, ainsi que la modification des paramètres.</span><span class="sxs-lookup"><span data-stu-id="ae91f-144">**Admin:** Has full control to add, manage, remove devices, and modify settings.</span></span>
* <span data-ttu-id="ae91f-145">**Lecture seule :** peut afficher les appareils, actions, règles, travaux et télémétrie.</span><span class="sxs-lookup"><span data-stu-id="ae91f-145">**ReadOnly:** Can view devices, rules, actions, jobs, and telemetry.</span></span>

<span data-ttu-id="ae91f-146">Vous pouvez trouver les autorisations attribuées à chaque rôle dans le fichier source [RolePermissions.cs][lnk-resource-cs].</span><span class="sxs-lookup"><span data-stu-id="ae91f-146">You can find the permissions assigned to each role in the [RolePermissions.cs][lnk-resource-cs] source file.</span></span>

### <a name="changing-application-roles-for-a-user"></a><span data-ttu-id="ae91f-147">Modification des rôles d’application pour un utilisateur</span><span class="sxs-lookup"><span data-stu-id="ae91f-147">Changing application roles for a user</span></span>

<span data-ttu-id="ae91f-148">Vous pouvez utiliser la procédure suivante pour définir un utilisateur dans Active Directory en tant qu’administrateur de votre solution préconfigurée.</span><span class="sxs-lookup"><span data-stu-id="ae91f-148">You can use the following procedure to make a user in your Active Directory an administrator of your preconfigured solution.</span></span>

<span data-ttu-id="ae91f-149">Vous devez être un administrateur général AAD pour modifier les rôles d’un utilisateur :</span><span class="sxs-lookup"><span data-stu-id="ae91f-149">You must be an AAD global administrator to change roles for a user:</span></span>

1. <span data-ttu-id="ae91f-150">Accédez au [portail Azure][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="ae91f-150">Go to the [Azure portal][lnk-portal].</span></span>
2. <span data-ttu-id="ae91f-151">Sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ae91f-151">Select **Azure Active Directory**.</span></span>
3. <span data-ttu-id="ae91f-152">Veillez à utiliser l’annuaire que vous avez choisi sur azureiotsuite.com lorsque vous avez approvisionné votre solution.</span><span class="sxs-lookup"><span data-stu-id="ae91f-152">Make sure you are using the directory you chose on azureiotsuite.com when you provisioned your solution.</span></span> <span data-ttu-id="ae91f-153">Si vous avez plusieurs annuaires associés à votre abonnement, vous pouvez basculer entre eux si vous cliquez sur le nom de votre compte en haut à droite du portail.</span><span class="sxs-lookup"><span data-stu-id="ae91f-153">If you have multiple directories associated with your subscription, you can switch between them if you click your account name at the top-right of the portal.</span></span>
4. <span data-ttu-id="ae91f-154">Cliquez sur **Applications d’entreprise**, puis sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="ae91f-154">Click **Enterprise applications**, then **All applications**.</span></span>
4. <span data-ttu-id="ae91f-155">Affichez **toutes les applications** avec **n’importe quel** état.</span><span class="sxs-lookup"><span data-stu-id="ae91f-155">Show **All applications** with **Any** status.</span></span> <span data-ttu-id="ae91f-156">Recherchez ensuite une application avec le nom de votre solution préconfigurée.</span><span class="sxs-lookup"><span data-stu-id="ae91f-156">Then search for an application with name of your preconfigured solution.</span></span>
5. <span data-ttu-id="ae91f-157">Cliquez sur le nom de l’application qui correspond au nom de votre solution préconfigurée.</span><span class="sxs-lookup"><span data-stu-id="ae91f-157">Click the name of the application that matches your preconfigured solution name.</span></span>
6. <span data-ttu-id="ae91f-158">Cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="ae91f-158">Click **Users and groups**.</span></span>
7. <span data-ttu-id="ae91f-159">Sélectionnez l’utilisateur dont vous souhaitez permuter les rôles.</span><span class="sxs-lookup"><span data-stu-id="ae91f-159">Select the user you want to switch roles.</span></span>
8. <span data-ttu-id="ae91f-160">Cliquez sur **Attribuer**, puis sélectionnez le rôle (par exemple, **Admin**) que vous souhaitez attribuer à l’utilisateur en cochant la case correspondante.</span><span class="sxs-lookup"><span data-stu-id="ae91f-160">Click **Assign** and select the role (such as **Admin**) you'd like to assign to the user, click the check mark.</span></span>

## <a name="faq"></a><span data-ttu-id="ae91f-161">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="ae91f-161">FAQ</span></span>

### <a name="im-a-service-administrator-and-id-like-to-change-the-directory-mapping-between-my-subscription-and-a-specific-aad-tenant-how-do-i-complete-this-task"></a><span data-ttu-id="ae91f-162">Je suis un administrateur de service et je souhaite modifier le mappage d’annuaire entre mon abonnement et un client AAD spécifique.</span><span class="sxs-lookup"><span data-stu-id="ae91f-162">I'm a service administrator and I'd like to change the directory mapping between my subscription and a specific AAD tenant.</span></span> <span data-ttu-id="ae91f-163">Comment mener à bien cette tâche ?</span><span class="sxs-lookup"><span data-stu-id="ae91f-163">How do I complete this task?</span></span>

1. <span data-ttu-id="ae91f-164">Accédez au [portail Azure Classic][lnk-classic-portal] et cliquez sur **Paramètres** dans la liste des services sur le côté gauche.</span><span class="sxs-lookup"><span data-stu-id="ae91f-164">Go to the [Azure classic portal][lnk-classic-portal], click **Settings** in the list of services on the left-hand side.</span></span>
2. <span data-ttu-id="ae91f-165">Sélectionnez l’abonnement dont vous souhaitez modifier le mappage d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="ae91f-165">Select the subscription you'd like to change the directory mapping to.</span></span>
3. <span data-ttu-id="ae91f-166">Cliquez sur **Modifier l’annuaire**.</span><span class="sxs-lookup"><span data-stu-id="ae91f-166">Click **Edit Directory**.</span></span>
4. <span data-ttu-id="ae91f-167">Sélectionnez l’ **annuaire** que vous souhaitez utiliser dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="ae91f-167">Select the **Directory** you would like to use in the dropdown.</span></span> <span data-ttu-id="ae91f-168">Cliquez sur la flèche Suivant.</span><span class="sxs-lookup"><span data-stu-id="ae91f-168">Click the forward arrow.</span></span>
5. <span data-ttu-id="ae91f-169">Vérifiez le mappage d’annuaire et les coadministrateurs affectés.</span><span class="sxs-lookup"><span data-stu-id="ae91f-169">Confirm the directory mapping and affected co-administrators.</span></span> <span data-ttu-id="ae91f-170">Si vous migrez depuis un autre annuaire, tous les coadministrateurs de l’annuaire d’origine sont supprimés.</span><span class="sxs-lookup"><span data-stu-id="ae91f-170">If you are moving from another directory, all the co-administrators from the original directory are removed.</span></span>

### <a name="im-a-domain-usermember-on-the-aad-tenant-and-ive-created-a-preconfigured-solution-how-do-i-get-assigned-a-role-for-my-application"></a><span data-ttu-id="ae91f-171">Je suis un utilisateur/membre du domaine sur le client AAD et j’ai créé une solution préconfigurée.</span><span class="sxs-lookup"><span data-stu-id="ae91f-171">I'm a domain user/member on the AAD tenant and I've created a preconfigured solution.</span></span> <span data-ttu-id="ae91f-172">Comment puis-je me voir attribuer un rôle pour mon application ?</span><span class="sxs-lookup"><span data-stu-id="ae91f-172">How do I get assigned a role for my application?</span></span>

<span data-ttu-id="ae91f-173">Demandez à un administrateur général de vous faire passer administrateur général du locataire AAD, puis attribuez vous-même des rôles aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="ae91f-173">Ask a global administrator to make you a global administrator on the AAD tenant and then assign roles to users yourself.</span></span> <span data-ttu-id="ae91f-174">Vous pouvez également demander à un administrateur général d’attribuer directement un rôle.</span><span class="sxs-lookup"><span data-stu-id="ae91f-174">Alternatively, ask a global administrator to assign you a role directly.</span></span> <span data-ttu-id="ae91f-175">Si vous souhaitez modifier le client AAD sur lequel votre solution préconfigurée a été déployée, passez à la question suivante.</span><span class="sxs-lookup"><span data-stu-id="ae91f-175">If you'd like to change the AAD tenant your preconfigured solution has been deployed to, see the next question.</span></span>

### <a name="how-do-i-switch-the-aad-tenant-my-remote-monitoring-preconfigured-solution-and-application-are-assigned-to"></a><span data-ttu-id="ae91f-176">Comment puis-je activer le client AAD auquel la solution préconfigurée de contrôle à distance et l’application sont affectées ?</span><span class="sxs-lookup"><span data-stu-id="ae91f-176">How do I switch the AAD tenant my remote monitoring preconfigured solution and application are assigned to?</span></span>

<span data-ttu-id="ae91f-177">Vous pouvez exécuter un déploiement cloud à partir de <https://github.com/Azure/azure-iot-remote-monitoring>, puis redéployer avec un client AAD nouvellement créé.</span><span class="sxs-lookup"><span data-stu-id="ae91f-177">You can run a cloud deployment from <https://github.com/Azure/azure-iot-remote-monitoring> and redeploy with a newly created AAD tenant.</span></span> <span data-ttu-id="ae91f-178">Comme vous êtes, par défaut, administrateur général, lorsque vous créez un locataire AAD, vous disposez des autorisations nécessaires pour ajouter des utilisateurs et leur attribuer des rôles.</span><span class="sxs-lookup"><span data-stu-id="ae91f-178">Because you are, by default, a global administrator when you create an AAD tenant, you have permissions to add users and assign roles to those users.</span></span>

1. <span data-ttu-id="ae91f-179">Créez un annuaire ADD dans le [portail Azure ][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="ae91f-179">Create an AAD directory in the [Azure portal][lnk-portal].</span></span>
2. <span data-ttu-id="ae91f-180">Accédez à <https://github.com/Azure/azure-iot-remote-monitoring>.</span><span class="sxs-lookup"><span data-stu-id="ae91f-180">Go to <https://github.com/Azure/azure-iot-remote-monitoring>.</span></span>
3. <span data-ttu-id="ae91f-181">Exécutez `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` (par exemple, `build.cmd cloud debug myRMSolution`)</span><span class="sxs-lookup"><span data-stu-id="ae91f-181">Run `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` (For example, `build.cmd cloud debug myRMSolution`)</span></span>
4. <span data-ttu-id="ae91f-182">Lorsque vous y êtes invité, définissez le **tenantid** du client que vous venez de créer et non celui du client précédent.</span><span class="sxs-lookup"><span data-stu-id="ae91f-182">When prompted, set the **tenantid** to be your newly created tenant instead of your previous tenant.</span></span>

### <a name="i-want-to-change-a-service-administrator-or-co-administrator-when-logged-in-with-an-organisational-account"></a><span data-ttu-id="ae91f-183">Je souhaite modifier la fonctionnalité administrateur de service ou coadministrateur lors d’une connexion avec un compte de société</span><span class="sxs-lookup"><span data-stu-id="ae91f-183">I want to change a Service Administrator or Co-Administrator when logged in with an organisational account</span></span>

<span data-ttu-id="ae91f-184">Voir l’article de support [Modification de la fonctionnalité Administrateur de service et Coadministrateur lors d’une connexion avec un compte de société][lnk-service-admins].</span><span class="sxs-lookup"><span data-stu-id="ae91f-184">See the support article [Changing Service Administrator and Co-Administrator when logged in with an organisational account][lnk-service-admins].</span></span>

### <a name="why-am-i-seeing-this-error-your-account-does-not-have-the-proper-permissions-to-create-a-solution-please-check-with-your-account-administrator-or-try-with-a-different-account"></a><span data-ttu-id="ae91f-185">Pourquoi est-ce que je reçois cette erreur ?</span><span class="sxs-lookup"><span data-stu-id="ae91f-185">Why am I seeing this error?</span></span> <span data-ttu-id="ae91f-186">« Votre compte n’a pas les autorisations suffisantes pour créer une solution.</span><span class="sxs-lookup"><span data-stu-id="ae91f-186">"Your account does not have the proper permissions to create a solution.</span></span> <span data-ttu-id="ae91f-187">Veuillez contacter votre administrateur de compte ou essayer avec un autre compte. »</span><span class="sxs-lookup"><span data-stu-id="ae91f-187">Please check with your account administrator or try with a different account."</span></span>

<span data-ttu-id="ae91f-188">Examinez le schéma suivant pour obtenir des conseils :</span><span class="sxs-lookup"><span data-stu-id="ae91f-188">Look at the following diagram for guidance:</span></span>

![][img-flowchart]

> [!NOTE]
> <span data-ttu-id="ae91f-189">Si l’erreur persiste après votre validation en tant qu’administrateur global sur le client AAD et que coadministrateur sur l’abonnement, demandez à votre administrateur de compte de supprimer l’utilisateur et de réattribuer les autorisations nécessaires dans l’ordre suivant :</span><span class="sxs-lookup"><span data-stu-id="ae91f-189">If you continue to see the error after validating you are a global administrator on the AAD tenant and a co-administrator on the subscription, have your account administrator remove the user and reassign necessary permissions in this order.</span></span> <span data-ttu-id="ae91f-190">tout d’abord, ajoutez l’utilisateur en tant qu’administrateur global, puis ajoutez un utilisateur en tant que coadministrateur sur l’abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="ae91f-190">First, add the user as a global administrator and then add user as a co-administrator on the Azure subscription.</span></span> <span data-ttu-id="ae91f-191">Si les problèmes persistent, contactez le service [Aide et support][lnk-help-support].</span><span class="sxs-lookup"><span data-stu-id="ae91f-191">If issues persist, contact [Help & Support][lnk-help-support].</span></span>

### <a name="why-am-i-seeing-this-error-when-i-have-an-azure-subscription-an-azure-subscription-is-required-to-create-pre-configured-solutions-you-can-create-a-free-trial-account-in-just-a-couple-of-minutes"></a><span data-ttu-id="ae91f-192">Pourquoi affiche-t-il cette erreur alors que j’ai un abonnement Azure ?</span><span class="sxs-lookup"><span data-stu-id="ae91f-192">Why am I seeing this error when I have an Azure subscription?</span></span> <span data-ttu-id="ae91f-193">« Vous devez avoir un abonnement Azure pour créer des solutions préconfigurées.</span><span class="sxs-lookup"><span data-stu-id="ae91f-193">"An Azure subscription is required to create pre-configured solutions.</span></span> <span data-ttu-id="ae91f-194">Vous pouvez créer un compte d'essai gratuit en quelques minutes seulement. »</span><span class="sxs-lookup"><span data-stu-id="ae91f-194">You can create a free trial account in just a couple of minutes."</span></span>

<span data-ttu-id="ae91f-195">Si vous êtes sûr de disposer d’un abonnement Azure, validez le mappage de votre abonnement client et assurez-vous que c’est le bon client qui est sélectionné dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="ae91f-195">If you're certain you have an Azure subscription, validate the tenant mapping for your subscription and ensure the correct tenant is selected in the dropdown.</span></span> <span data-ttu-id="ae91f-196">Si vous avez validé le locataire souhaité, suivez le schéma ci-dessus et validez le mappage de votre abonnement et de ce locataire AAD.</span><span class="sxs-lookup"><span data-stu-id="ae91f-196">If you’ve validated the desired tenant is correct, follow the preceding diagram and validate the mapping of your subscription and this AAD tenant.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae91f-197">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ae91f-197">Next steps</span></span>
<span data-ttu-id="ae91f-198">Pour poursuivre votre formation concernant IoT Suite, découvrez comment [personnaliser une solution préconfigurée][lnk-customize].</span><span class="sxs-lookup"><span data-stu-id="ae91f-198">To continue learning about IoT Suite, see how you can [customize a preconfigured solution][lnk-customize].</span></span>

[img-flowchart]: media/iot-suite-permissions/flowchart.png

[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-rm-github-repo]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-pm-github-repo]: https://github.com/Azure/azure-iot-predictive-maintenance
[lnk-cf-github-repo]: https://github.com/Azure/azure-iot-connected-factory
[lnk-aad-admin]: ../active-directory/active-directory-assign-admin-roles.md
[lnk-classic-portal]: https://manage.windowsazure.com/
[lnk-portal]: https://portal.azure.com/
[lnk-create-edit-users]: ../active-directory/active-directory-create-users.md
[lnk-assign-app-roles]: ../active-directory/active-directory-coreapps-assign-user-azure-portal.md
[lnk-service-admins]: https://azure.microsoft.com/support/changing-service-admin-and-co-admin/
[lnk-admin-roles]: ../billing/billing-add-change-azure-subscription-administrator.md
[lnk-resource-cs]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/DeviceAdministration/Web/Security/RolePermissions.cs
[lnk-help-support]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
