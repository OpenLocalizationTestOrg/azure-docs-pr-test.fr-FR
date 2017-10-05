---
title: "Créer une identité pour une application Azure dans le portail | Microsoft Docs"
description: "Décrit comment créer une application et un principal du service Azure Active Directory qui peuvent être utilisés avec le contrôle d'accès basé sur les rôles dans Azure Resource Manager pour gérer l'accès aux ressources."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 7068617b-ac5e-47b3-a1de-a18c918297b6
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 5d24fb99e1095d53e5ea547e53b80178d9cb77c0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="use-portal-to-create-an-azure-active-directory-application-and-service-principal-that-can-access-resources"></a><span data-ttu-id="79a84-103">Utiliser le portail pour créer une application et un principal du service Azure Active Directory pouvant accéder aux ressources</span><span class="sxs-lookup"><span data-stu-id="79a84-103">Use portal to create an Azure Active Directory application and service principal that can access resources</span></span>

<span data-ttu-id="79a84-104">Si une application doit accéder à des ressources ou les modifier, vous devez configurer une application Azure Active Directory (AD) et lui accorder les autorisations nécessaires.</span><span class="sxs-lookup"><span data-stu-id="79a84-104">When you have an application that needs to access or modify resources, you must set up an Azure Active Directory (AD) application and assign the required permissions to it.</span></span> <span data-ttu-id="79a84-105">Cette approche est préférable à l’exécution de l’application avec vos propres informations d’identification, car :</span><span class="sxs-lookup"><span data-stu-id="79a84-105">This approach is preferable to running the app under your own credentials because:</span></span>

* <span data-ttu-id="79a84-106">Vous pouvez affecter à l’identité de l’application des autorisations différentes de vos propres autorisations.</span><span class="sxs-lookup"><span data-stu-id="79a84-106">You can assign permissions to the app identity that are different than your own permissions.</span></span> <span data-ttu-id="79a84-107">En règle générale, ces autorisations sont strictement limitées à ce que l’application doit faire.</span><span class="sxs-lookup"><span data-stu-id="79a84-107">Typically, these permissions are restricted to exactly what the app needs to do.</span></span>
* <span data-ttu-id="79a84-108">Il est inutile de modifier les informations d’identification de l’application si vos responsabilités évoluent.</span><span class="sxs-lookup"><span data-stu-id="79a84-108">You do not have to change the app's credentials if your responsibilities change.</span></span> 
* <span data-ttu-id="79a84-109">Vous pouvez utiliser un certificat pour automatiser l’authentification lors de l’exécution d’un script sans assistance.</span><span class="sxs-lookup"><span data-stu-id="79a84-109">You can use a certificate to automate authentication when executing an unattended script.</span></span>

<span data-ttu-id="79a84-110">Cette rubrique explique comment effectuer ces étapes via le portail.</span><span class="sxs-lookup"><span data-stu-id="79a84-110">This topic shows you how to perform those steps through the portal.</span></span> <span data-ttu-id="79a84-111">Elle se concentre sur une application à locataire unique conçue pour s’exécuter au sein d’une seule organisation.</span><span class="sxs-lookup"><span data-stu-id="79a84-111">It focuses on a single-tenant application where the application is intended to run within only one organization.</span></span> <span data-ttu-id="79a84-112">Les applications à locataire unique sont généralement utilisées pour les applications métier exécutées au sein de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="79a84-112">You typically use single-tenant applications for line-of-business applications that run within your organization.</span></span>
 
## <a name="required-permissions"></a><span data-ttu-id="79a84-113">Autorisations requises</span><span class="sxs-lookup"><span data-stu-id="79a84-113">Required permissions</span></span>
<span data-ttu-id="79a84-114">Pour cette rubrique, vous devez disposer des autorisations suffisantes pour enregistrer une application auprès de votre client Azure AD et affecter l’application à un rôle dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="79a84-114">To complete this topic, you must have sufficient permissions to register an application with your Azure AD tenant, and assign the application to a role in your Azure subscription.</span></span> <span data-ttu-id="79a84-115">Vérifions que vous disposez des droits suffisants pour effectuer ces étapes.</span><span class="sxs-lookup"><span data-stu-id="79a84-115">Let's make sure you have the right permissions to perform those steps.</span></span>

### <a name="check-azure-active-directory-permissions"></a><span data-ttu-id="79a84-116">Vérifier les autorisations Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="79a84-116">Check Azure Active Directory permissions</span></span>
1. <span data-ttu-id="79a84-117">Connectez-vous à votre compte Azure via le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="79a84-117">Log in to your Azure Account through the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="79a84-118">Sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="79a84-118">Select **Azure Active Directory**.</span></span>

     ![sélectionner azure active directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)
3. <span data-ttu-id="79a84-120">Dans Azure Active Directory, sélectionnez **Paramètres utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="79a84-120">In Azure Active Directory, select **User settings**.</span></span>

     ![sélectionner les paramètres utilisateur](./media/resource-group-create-service-principal-portal/select-user-settings.png)
4. <span data-ttu-id="79a84-122">Vérifiez le paramètre **Inscriptions d’applications**.</span><span class="sxs-lookup"><span data-stu-id="79a84-122">Check the **App registrations** setting.</span></span> <span data-ttu-id="79a84-123">S’il est défini sur **Oui**, les utilisateurs non administrateurs peuvent inscrire des applications AD.</span><span class="sxs-lookup"><span data-stu-id="79a84-123">If set to **Yes**, non-admin users can register AD apps.</span></span> <span data-ttu-id="79a84-124">Ce paramètre signifie que n’importe quel utilisateur dans Azure AD peut inscrire une application.</span><span class="sxs-lookup"><span data-stu-id="79a84-124">This setting means any user in the Azure AD tenant can register an app.</span></span> <span data-ttu-id="79a84-125">Vous pouvez passer à [Vérifier les autorisations d’abonnement Azure](#check-azure-subscription-permissions).</span><span class="sxs-lookup"><span data-stu-id="79a84-125">You can proceed to [Check Azure subscription permissions](#check-azure-subscription-permissions).</span></span>

     ![afficher les inscriptions d’applications](./media/resource-group-create-service-principal-portal/view-app-registrations.png)
5. <span data-ttu-id="79a84-127">Si le paramètre d’inscriptions d’applications est défini sur **Non**, seuls les utilisateurs administrateurs peuvent inscrire des applications.</span><span class="sxs-lookup"><span data-stu-id="79a84-127">If the app registrations setting is set to **No**, only admin users can register apps.</span></span> <span data-ttu-id="79a84-128">Vous devez vérifier si votre compte est un administrateur du client Azure AD.</span><span class="sxs-lookup"><span data-stu-id="79a84-128">You need to check whether your account is an admin for the Azure AD tenant.</span></span> <span data-ttu-id="79a84-129">Sélectionnez **Vue d’ensemble** et **Rechercher un utilisateur** dans Tâches rapides.</span><span class="sxs-lookup"><span data-stu-id="79a84-129">Select **Overview** and **Find a user** from Quick tasks.</span></span>

     ![rechercher un utilisateur](./media/resource-group-create-service-principal-portal/find-user.png)
6. <span data-ttu-id="79a84-131">Recherchez votre compte et sélectionnez-le lorsque vous l’avez trouvé.</span><span class="sxs-lookup"><span data-stu-id="79a84-131">Search for your account, and select it when you find it.</span></span>

     ![rechercher un utilisateur](./media/resource-group-create-service-principal-portal/show-user.png)
7. <span data-ttu-id="79a84-133">Pour votre compte, sélectionnez **Rôle Directory**.</span><span class="sxs-lookup"><span data-stu-id="79a84-133">For your account, select **Directory role**.</span></span> 

     ![rôle directory](./media/resource-group-create-service-principal-portal/select-directory-role.png)
8. <span data-ttu-id="79a84-135">Affichez le rôle de répertoire qui vous a été affecté dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="79a84-135">View your assigned directory role in Azure AD.</span></span> <span data-ttu-id="79a84-136">Si le rôle Utilisateur est affecté à votre compte mais que le paramètre d’inscription d’application (de la procédure précédente) est limité aux utilisateurs administrateurs, demandez à votre administrateur de vous affecter rôle administrateur ou d’autoriser les utilisateurs à inscrire des applications.</span><span class="sxs-lookup"><span data-stu-id="79a84-136">If your account is assigned to the User role, but the app registration setting (from the preceding steps) is limited to admin users, ask your administrator to either assign you to an administrator role, or to enable users to register apps.</span></span>

     ![afficher le rôle](./media/resource-group-create-service-principal-portal/view-role.png)

### <a name="check-azure-subscription-permissions"></a><span data-ttu-id="79a84-138">Vérifier les autorisations d’abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="79a84-138">Check Azure subscription permissions</span></span>
<span data-ttu-id="79a84-139">Dans votre abonnement Azure, votre compte doit disposer d’un accès `Microsoft.Authorization/*/Write` pour affecter un rôle à une application AD.</span><span class="sxs-lookup"><span data-stu-id="79a84-139">In your Azure subscription, your account must have `Microsoft.Authorization/*/Write` access to assign an AD app to a role.</span></span> <span data-ttu-id="79a84-140">Cette action est accordée par le biais du rôle [Propriétaire](../active-directory/role-based-access-built-in-roles.md#owner) ou [Administrateur de l’accès utilisateur](../active-directory/role-based-access-built-in-roles.md#user-access-administrator).</span><span class="sxs-lookup"><span data-stu-id="79a84-140">This action is granted through the [Owner](../active-directory/role-based-access-built-in-roles.md#owner) role or [User Access Administrator](../active-directory/role-based-access-built-in-roles.md#user-access-administrator) role.</span></span> <span data-ttu-id="79a84-141">Si le rôle **Collaborateur** est affecté à votre compte, vous ne disposez pas de l’autorisation appropriée.</span><span class="sxs-lookup"><span data-stu-id="79a84-141">If your account is assigned to the **Contributor** role, you do not have adequate permission.</span></span> <span data-ttu-id="79a84-142">Vous recevez un message d’erreur lorsque vous tentez d’affecter un rôle au principal du service.</span><span class="sxs-lookup"><span data-stu-id="79a84-142">You will receive an error when attempting to assign the service principal to a role.</span></span> 

<span data-ttu-id="79a84-143">Pour vérifier vos autorisations d’abonnement :</span><span class="sxs-lookup"><span data-stu-id="79a84-143">To check your subscription permissions:</span></span>

1. <span data-ttu-id="79a84-144">Si vous n’avez pas déjà recherché votre compte Azure AD dans le cadre de la procédure précédente, sélectionnez **Azure Active Directory** dans le volet gauche.</span><span class="sxs-lookup"><span data-stu-id="79a84-144">If you are not already looking at your Azure AD account from the preceding steps, select **Azure Active Directory** from the left pane.</span></span>

2. <span data-ttu-id="79a84-145">Recherchez votre compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="79a84-145">Find your Azure AD account.</span></span> <span data-ttu-id="79a84-146">Sélectionnez **Vue d’ensemble** et **Rechercher un utilisateur** dans Tâches rapides.</span><span class="sxs-lookup"><span data-stu-id="79a84-146">Select **Overview** and **Find a user** from Quick tasks.</span></span>

     ![rechercher un utilisateur](./media/resource-group-create-service-principal-portal/find-user.png)
2. <span data-ttu-id="79a84-148">Recherchez votre compte et sélectionnez-le lorsque vous l’avez trouvé.</span><span class="sxs-lookup"><span data-stu-id="79a84-148">Search for your account, and select it when you find it.</span></span>

     ![rechercher un utilisateur](./media/resource-group-create-service-principal-portal/show-user.png) 
     
3. <span data-ttu-id="79a84-150">Sélectionnez **Ressources Azure**.</span><span class="sxs-lookup"><span data-stu-id="79a84-150">Select **Azure resources**.</span></span>

     ![sélectionner des ressources](./media/resource-group-create-service-principal-portal/select-azure-resources.png) 
3. <span data-ttu-id="79a84-152">Affichez les rôles qui vous sont affectés et déterminez si vous disposez des autorisations appropriées pour affecter un rôle à une application AD.</span><span class="sxs-lookup"><span data-stu-id="79a84-152">View your assigned roles, and determine if you have adequate permissions to assign an AD app to a role.</span></span> <span data-ttu-id="79a84-153">Si ce n’est pas le cas, demandez à votre administrateur d’abonnement de vous ajouter un rôle Administrateur de l’accès utilisateur.</span><span class="sxs-lookup"><span data-stu-id="79a84-153">If not, ask your subscription administrator to add you to User Access Administrator role.</span></span> <span data-ttu-id="79a84-154">Dans l’image suivante, le rôle Propriétaire est affecté à l’utilisateur pour deux abonnements, ce qui signifie que l’utilisateur dispose des autorisations appropriées.</span><span class="sxs-lookup"><span data-stu-id="79a84-154">In the following image, the user is assigned to the Owner role for two subscriptions, which means that user has adequate permissions.</span></span> 

     ![afficher les autorisations](./media/resource-group-create-service-principal-portal/view-assigned-roles.png)

## <a name="create-an-azure-active-directory-application"></a><span data-ttu-id="79a84-156">Créer une application Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="79a84-156">Create an Azure Active Directory application</span></span>
1. <span data-ttu-id="79a84-157">Connectez-vous à votre compte Azure via le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="79a84-157">Log in to your Azure Account through the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="79a84-158">Sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="79a84-158">Select **Azure Active Directory**.</span></span>

     ![sélectionner azure active directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)

4. <span data-ttu-id="79a84-160">Sélectionnez **Inscriptions d’applications**.</span><span class="sxs-lookup"><span data-stu-id="79a84-160">Select **App registrations**.</span></span>   

     ![sélectionner des inscriptions d’applications](./media/resource-group-create-service-principal-portal/select-app-registrations.png)
5. <span data-ttu-id="79a84-162">Sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="79a84-162">Select **Add**.</span></span>

     ![ajouter une application](./media/resource-group-create-service-principal-portal/select-add-app.png)

6. <span data-ttu-id="79a84-164">Fournissez un nom et une URL pour l’application.</span><span class="sxs-lookup"><span data-stu-id="79a84-164">Provide a name and URL for the application.</span></span> <span data-ttu-id="79a84-165">Sélectionnez **Application Web / API** ou **Native** pour le type d’application que vous souhaitez créer.</span><span class="sxs-lookup"><span data-stu-id="79a84-165">Select either **Web app / API** or **Native** for the type of application you want to create.</span></span> <span data-ttu-id="79a84-166">Après avoir défini les valeurs, sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="79a84-166">After setting the values, select **Create**.</span></span>

     ![nommer l’application](./media/resource-group-create-service-principal-portal/create-app.png)

<span data-ttu-id="79a84-168">Vous avez créé votre application.</span><span class="sxs-lookup"><span data-stu-id="79a84-168">You have created your application.</span></span>

## <a name="get-application-id-and-authentication-key"></a><span data-ttu-id="79a84-169">Obtenir un ID d’application et une clé d’authentification</span><span class="sxs-lookup"><span data-stu-id="79a84-169">Get application ID and authentication key</span></span>
<span data-ttu-id="79a84-170">Lors d’une connexion par programmation, vous aurez besoin de l’ID de votre application et d’une clé d’authentification.</span><span class="sxs-lookup"><span data-stu-id="79a84-170">When programmatically logging in, you need the ID for your application and an authentication key.</span></span> <span data-ttu-id="79a84-171">Pour obtenir ces valeurs, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="79a84-171">To get those values, use the following steps:</span></span>

1. <span data-ttu-id="79a84-172">Dans **Inscriptions d’applications** dans Azure Active Directory, sélectionnez votre application.</span><span class="sxs-lookup"><span data-stu-id="79a84-172">From **App registrations** in Azure Active Directory, select your application.</span></span>

     ![sélectionner une application](./media/resource-group-create-service-principal-portal/select-app.png)
2. <span data-ttu-id="79a84-174">Copiez l’**ID d’application** et stockez-le dans votre code d’application.</span><span class="sxs-lookup"><span data-stu-id="79a84-174">Copy the **Application ID** and store it in your application code.</span></span> <span data-ttu-id="79a84-175">Les applications de la section [Exemples d’applications](#sample-applications) font référence à cette valeur en tant qu’ID de locataire.</span><span class="sxs-lookup"><span data-stu-id="79a84-175">The applications in the [sample applications](#sample-applications) section refer to this value as the client id.</span></span>

     ![ID CLIENT](./media/resource-group-create-service-principal-portal/copy-app-id.png)
3. <span data-ttu-id="79a84-177">Pour générer une clé d’authentification, sélectionnez **Clés**.</span><span class="sxs-lookup"><span data-stu-id="79a84-177">To generate an authentication key, select **Keys**.</span></span>

     ![sélectionner des clés](./media/resource-group-create-service-principal-portal/select-keys.png)
4. <span data-ttu-id="79a84-179">Fournissez une description de la clé et la durée de la clé.</span><span class="sxs-lookup"><span data-stu-id="79a84-179">Provide a description of the key, and a duration for the key.</span></span> <span data-ttu-id="79a84-180">Lorsque vous avez terminé, sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="79a84-180">When done, select **Save**.</span></span>

     ![enregistrer une clé](./media/resource-group-create-service-principal-portal/save-key.png)

     <span data-ttu-id="79a84-182">Après avoir enregistré la clé, la valeur de la clé s’affiche.</span><span class="sxs-lookup"><span data-stu-id="79a84-182">After saving the key, the value of the key is displayed.</span></span> <span data-ttu-id="79a84-183">Copiez cette valeur car vous ne pourrez pas récupérer la clé ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="79a84-183">Copy this value because you are not able to retrieve the key later.</span></span> <span data-ttu-id="79a84-184">Vous fournissez la valeur de la clé avec l’ID d’application pour vous connecter en tant qu’application.</span><span class="sxs-lookup"><span data-stu-id="79a84-184">You provide the key value with the application ID to log in as the application.</span></span> <span data-ttu-id="79a84-185">Stockez la valeur de la clé à un emplacement où votre application peut la récupérer.</span><span class="sxs-lookup"><span data-stu-id="79a84-185">Store the key value where your application can retrieve it.</span></span>

     ![clé enregistrée](./media/resource-group-create-service-principal-portal/copy-key.png)

## <a name="get-tenant-id"></a><span data-ttu-id="79a84-187">Obtenir l’ID de locataire</span><span class="sxs-lookup"><span data-stu-id="79a84-187">Get tenant ID</span></span>
<span data-ttu-id="79a84-188">Lors d’une connexion par programmation, vous devez transmettre l’ID de locataire avec votre demande d’authentification.</span><span class="sxs-lookup"><span data-stu-id="79a84-188">When programmatically logging in, you need to pass the tenant ID with your authentication request.</span></span> 

1. <span data-ttu-id="79a84-189">Pour obtenir l’ID de locataire, sélectionnez **Propriétés** pour votre client Azure AD.</span><span class="sxs-lookup"><span data-stu-id="79a84-189">To get the tenant ID, select **Properties** for your Azure AD tenant.</span></span> 

     ![Sélectionnez les propriétés Azure AD](./media/resource-group-create-service-principal-portal/select-ad-properties.png)

2. <span data-ttu-id="79a84-191">Copiez l’**ID Directory**.</span><span class="sxs-lookup"><span data-stu-id="79a84-191">Copy the **Directory ID**.</span></span> <span data-ttu-id="79a84-192">Cette valeur est votre ID de locataire.</span><span class="sxs-lookup"><span data-stu-id="79a84-192">This value is your tenant ID.</span></span>

     ![ID client](./media/resource-group-create-service-principal-portal/copy-directory-id.png)

## <a name="assign-application-to-role"></a><span data-ttu-id="79a84-194">Affecter l’application à un rôle</span><span class="sxs-lookup"><span data-stu-id="79a84-194">Assign application to role</span></span>
<span data-ttu-id="79a84-195">Pour accéder aux ressources de votre abonnement, vous devez affecter un rôle à l’application.</span><span class="sxs-lookup"><span data-stu-id="79a84-195">To access resources in your subscription, you must assign the application to a role.</span></span> <span data-ttu-id="79a84-196">Vous devez décider du rôle qui doit représenter les autorisations appropriées pour l’application.</span><span class="sxs-lookup"><span data-stu-id="79a84-196">Decide which role represents the right permissions for the application.</span></span> <span data-ttu-id="79a84-197">Pour en savoir plus sur les rôles disponibles, consultez [RBAC : rôles intégrés](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="79a84-197">To learn about the available roles, see [RBAC: Built in Roles](../active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="79a84-198">Vous pouvez définir l’étendue au niveau de l’abonnement, du groupe de ressources ou de la ressource.</span><span class="sxs-lookup"><span data-stu-id="79a84-198">You can set the scope at the level of the subscription, resource group, or resource.</span></span> <span data-ttu-id="79a84-199">Les autorisations sont héritées des niveaux inférieurs de l’étendue</span><span class="sxs-lookup"><span data-stu-id="79a84-199">Permissions are inherited to lower levels of scope.</span></span> <span data-ttu-id="79a84-200">(par exemple, l’ajout d’une application au rôle Lecteur pour un groupe de ressources signifie qu’elle peut lire le groupe de ressources et toutes les ressources qu’il contient).</span><span class="sxs-lookup"><span data-stu-id="79a84-200">For example, adding an application to the Reader role for a resource group means it can read the resource group and any resources it contains.</span></span>

1. <span data-ttu-id="79a84-201">Accédez au niveau d’étendue que vous souhaitez affecter à l’application.</span><span class="sxs-lookup"><span data-stu-id="79a84-201">Navigate to the level of scope you wish to assign the application to.</span></span> <span data-ttu-id="79a84-202">Par exemple, pour affecter un rôle sur l’étendue de l’abonnement, sélectionnez **Abonnements**.</span><span class="sxs-lookup"><span data-stu-id="79a84-202">For example, to assign a role at the subscription scope, select **Subscriptions**.</span></span> <span data-ttu-id="79a84-203">Vous pouvez également sélectionner un groupe de ressources ou une ressource.</span><span class="sxs-lookup"><span data-stu-id="79a84-203">You could instead select a resource group or resource.</span></span>

     ![sélectionner l'abonnement](./media/resource-group-create-service-principal-portal/select-subscription.png)

2. <span data-ttu-id="79a84-205">Sélectionnez l’abonnement (groupe de ressources ou ressource) auquel l’application doit être affectée.</span><span class="sxs-lookup"><span data-stu-id="79a84-205">Select the particular subscription (resource group or resource) to assign the application to.</span></span>

     ![sélectionner l’abonnement pour l’affectation](./media/resource-group-create-service-principal-portal/select-one-subscription.png)

3. <span data-ttu-id="79a84-207">Sélectionnez **Contrôle d’accès (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="79a84-207">Select **Access Control (IAM)**.</span></span>

     ![sélectionner l’accès](./media/resource-group-create-service-principal-portal/select-access-control.png)

4. <span data-ttu-id="79a84-209">Sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="79a84-209">Select **Add**.</span></span>

     ![sélectionner ajouter](./media/resource-group-create-service-principal-portal/select-add.png)
6. <span data-ttu-id="79a84-211">Sélectionnez le rôle que vous souhaitez affecter à l’application.</span><span class="sxs-lookup"><span data-stu-id="79a84-211">Select the role you wish to assign to the application.</span></span> <span data-ttu-id="79a84-212">L’image suivante montre le code **Lecteur**.</span><span class="sxs-lookup"><span data-stu-id="79a84-212">The following image shows the **Reader** role.</span></span>

     ![sélectionner un rôle](./media/resource-group-create-service-principal-portal/select-role.png)

8. <span data-ttu-id="79a84-214">Recherchez votre application et sélectionnez-la.</span><span class="sxs-lookup"><span data-stu-id="79a84-214">Search for your application, and select it.</span></span>

     ![rechercher une application](./media/resource-group-create-service-principal-portal/search-app.png)
9. <span data-ttu-id="79a84-216">Sélectionnez **OK** pour finaliser l’affectation du rôle.</span><span class="sxs-lookup"><span data-stu-id="79a84-216">Select **OK** to finish assigning the role.</span></span> <span data-ttu-id="79a84-217">Votre application apparaît dans la liste des utilisateurs affectés à un rôle pour cette étendue.</span><span class="sxs-lookup"><span data-stu-id="79a84-217">You see your application in the list of users assigned to a role for that scope.</span></span>

## <a name="log-in-as-the-application"></a><span data-ttu-id="79a84-218">Se connecter en tant qu’application</span><span class="sxs-lookup"><span data-stu-id="79a84-218">Log in as the application</span></span>

<span data-ttu-id="79a84-219">Votre application est maintenant configurée dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="79a84-219">Your application is now set up in Azure Active Directory.</span></span> <span data-ttu-id="79a84-220">Vous disposez d’un ID et d’une clé à utiliser pour la connexion en tant qu’application.</span><span class="sxs-lookup"><span data-stu-id="79a84-220">You have an ID and key to use for signing in as the application.</span></span> <span data-ttu-id="79a84-221">L’application se voit affecter un rôle qui lui permet d’effectuer certaines actions.</span><span class="sxs-lookup"><span data-stu-id="79a84-221">The application is assigned to a role that gives it certain actions it can perform.</span></span> <span data-ttu-id="79a84-222">Pour plus d’informations sur la connexion en tant qu’application via différentes plateformes, voir :</span><span class="sxs-lookup"><span data-stu-id="79a84-222">For information about logging in as the application through different platforms, see:</span></span>

* [<span data-ttu-id="79a84-223">PowerShell</span><span class="sxs-lookup"><span data-stu-id="79a84-223">PowerShell</span></span>](resource-group-authenticate-service-principal.md#provide-credentials-through-powershell)
* [<span data-ttu-id="79a84-224">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="79a84-224">Azure CLI</span></span>](resource-group-authenticate-service-principal-cli.md#provide-credentials-through-azure-cli)
* [<span data-ttu-id="79a84-225">REST</span><span class="sxs-lookup"><span data-stu-id="79a84-225">REST</span></span>](/rest/api/#create-the-request)
* [<span data-ttu-id="79a84-226">.NET</span><span class="sxs-lookup"><span data-stu-id="79a84-226">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="79a84-227">Java</span><span class="sxs-lookup"><span data-stu-id="79a84-227">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="79a84-228">Node.JS</span><span class="sxs-lookup"><span data-stu-id="79a84-228">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="79a84-229">Python</span><span class="sxs-lookup"><span data-stu-id="79a84-229">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="79a84-230">Ruby</span><span class="sxs-lookup"><span data-stu-id="79a84-230">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)


## <a name="next-steps"></a><span data-ttu-id="79a84-231">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="79a84-231">Next steps</span></span>
* <span data-ttu-id="79a84-232">Pour configurer une application mutualisée, consultez le [Guide du développeur pour l’authentification avec l’API Azure Resource Manager](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="79a84-232">To set up a multi-tenant application, see [Developer's guide to authorization with the Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="79a84-233">Pour en savoir plus sur la spécification de stratégies de sécurité, consultez la rubrique [Contrôle d’accès en fonction du rôle](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="79a84-233">To learn about specifying security policies, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>  
* <span data-ttu-id="79a84-234">Pour une liste des actions disponibles qui peuvent être autorisées ou refusées aux utilisateurs, consultez [Opérations du fournisseur de ressources Azure Resource Manager](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="79a84-234">For a list of available actions that can be granted or denied to users, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>
