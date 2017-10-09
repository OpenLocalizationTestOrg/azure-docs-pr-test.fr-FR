---
title: "identité aaaCreate pour une application Azure dans le portail | Documents Microsoft"
description: "Décrit le mode d’accès des toocreate une application Azure Active Directory et le service principal qui peut être utilisé avec le contrôle d’accès basé sur rôle hello dans Azure Resource Manager toomanage tooresources."
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
ms.openlocfilehash: 9624715ac612f42df6f9e9e67b8233bd4b914174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-portal-toocreate-an-azure-active-directory-application-and-service-principal-that-can-access-resources"></a><span data-ttu-id="3bbd2-103">Utilisez le portail toocreate une application Azure Active Directory et le principal du service qui peut accéder aux ressources</span><span class="sxs-lookup"><span data-stu-id="3bbd2-103">Use portal toocreate an Azure Active Directory application and service principal that can access resources</span></span>

<span data-ttu-id="3bbd2-104">Lorsque vous avez une application qui doit tooaccess ou modifier des ressources, vous devez configurer une application Azure Active Directory (AD) et affecter tooit d’autorisations hello requis.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-104">When you have an application that needs tooaccess or modify resources, you must set up an Azure Active Directory (AD) application and assign hello required permissions tooit.</span></span> <span data-ttu-id="3bbd2-105">Cette approche est préférable toorunning hello application vos propres informations d’identification, car :</span><span class="sxs-lookup"><span data-stu-id="3bbd2-105">This approach is preferable toorunning hello app under your own credentials because:</span></span>

* <span data-ttu-id="3bbd2-106">Vous pouvez affecter des autorisations identité d’application toohello différents de vos propres autorisations.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-106">You can assign permissions toohello app identity that are different than your own permissions.</span></span> <span data-ttu-id="3bbd2-107">En règle générale, ces autorisations sont limitée tooexactly quelle application hello doit toodo.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-107">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span>
* <span data-ttu-id="3bbd2-108">Vous n’avez pas les informations d’identification de l’application toochange hello si vos responsabilités changent.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-108">You do not have toochange hello app's credentials if your responsibilities change.</span></span> 
* <span data-ttu-id="3bbd2-109">Vous pouvez utiliser une authentification de tooautomate certificat lors de l’exécution d’un script sans assistance.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-109">You can use a certificate tooautomate authentication when executing an unattended script.</span></span>

<span data-ttu-id="3bbd2-110">Cette rubrique vous montre comment tooperform ces étapes via le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-110">This topic shows you how tooperform those steps through hello portal.</span></span> <span data-ttu-id="3bbd2-111">Il se concentre sur une application à locataire unique où application hello est prévue toorun au sein d’une seule organisation.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-111">It focuses on a single-tenant application where hello application is intended toorun within only one organization.</span></span> <span data-ttu-id="3bbd2-112">Les applications à locataire unique sont généralement utilisées pour les applications métier exécutées au sein de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-112">You typically use single-tenant applications for line-of-business applications that run within your organization.</span></span>
 
## <a name="required-permissions"></a><span data-ttu-id="3bbd2-113">Autorisations requises</span><span class="sxs-lookup"><span data-stu-id="3bbd2-113">Required permissions</span></span>
<span data-ttu-id="3bbd2-114">toocomplete cette rubrique, vous devez disposer d’une application tooregister d’autorisations suffisantes à votre client Azure AD et affecter le rôle de tooa d’application hello dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-114">toocomplete this topic, you must have sufficient permissions tooregister an application with your Azure AD tenant, and assign hello application tooa role in your Azure subscription.</span></span> <span data-ttu-id="3bbd2-115">Assurons-nous que vous avez hello autorisations appropriées tooperform ces étapes.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-115">Let's make sure you have hello right permissions tooperform those steps.</span></span>

### <a name="check-azure-active-directory-permissions"></a><span data-ttu-id="3bbd2-116">Vérifier les autorisations Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3bbd2-116">Check Azure Active Directory permissions</span></span>
1. <span data-ttu-id="3bbd2-117">Connectez-vous à tooyour compte Azure via hello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3bbd2-117">Log in tooyour Azure Account through hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3bbd2-118">Sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-118">Select **Azure Active Directory**.</span></span>

     ![sélectionner azure active directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)
3. <span data-ttu-id="3bbd2-120">Dans Azure Active Directory, sélectionnez **Paramètres utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-120">In Azure Active Directory, select **User settings**.</span></span>

     ![sélectionner les paramètres utilisateur](./media/resource-group-create-service-principal-portal/select-user-settings.png)
4. <span data-ttu-id="3bbd2-122">Vérifiez hello **inscriptions d’application** paramètre.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-122">Check hello **App registrations** setting.</span></span> <span data-ttu-id="3bbd2-123">Si défini trop**Oui**, les utilisateurs non administrateurs peuvent inscrire des applications AD.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-123">If set too**Yes**, non-admin users can register AD apps.</span></span> <span data-ttu-id="3bbd2-124">Ce paramètre signifie que n’importe quel utilisateur dans le locataire Azure AD de hello peut inscrire une application.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-124">This setting means any user in hello Azure AD tenant can register an app.</span></span> <span data-ttu-id="3bbd2-125">Vous pouvez passer trop[autorisations d’abonnement Azure de vérifier](#check-azure-subscription-permissions).</span><span class="sxs-lookup"><span data-stu-id="3bbd2-125">You can proceed too[Check Azure subscription permissions](#check-azure-subscription-permissions).</span></span>

     ![afficher les inscriptions d’applications](./media/resource-group-create-service-principal-portal/view-app-registrations.png)
5. <span data-ttu-id="3bbd2-127">Si les inscriptions d’application hello paramètre est défini trop**non**, seuls les utilisateurs administrateurs peuvent inscrire des applications.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-127">If hello app registrations setting is set too**No**, only admin users can register apps.</span></span> <span data-ttu-id="3bbd2-128">Vous devez toocheck si votre compte est un administrateur de locataire Azure AD de hello.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-128">You need toocheck whether your account is an admin for hello Azure AD tenant.</span></span> <span data-ttu-id="3bbd2-129">Sélectionnez **Vue d’ensemble** et **Rechercher un utilisateur** dans Tâches rapides.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-129">Select **Overview** and **Find a user** from Quick tasks.</span></span>

     ![rechercher un utilisateur](./media/resource-group-create-service-principal-portal/find-user.png)
6. <span data-ttu-id="3bbd2-131">Recherchez votre compte et sélectionnez-le lorsque vous l’avez trouvé.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-131">Search for your account, and select it when you find it.</span></span>

     ![rechercher un utilisateur](./media/resource-group-create-service-principal-portal/show-user.png)
7. <span data-ttu-id="3bbd2-133">Pour votre compte, sélectionnez **Rôle Directory**.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-133">For your account, select **Directory role**.</span></span> 

     ![rôle directory](./media/resource-group-create-service-principal-portal/select-directory-role.png)
8. <span data-ttu-id="3bbd2-135">Affichez le rôle de répertoire qui vous a été affecté dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-135">View your assigned directory role in Azure AD.</span></span> <span data-ttu-id="3bbd2-136">Si toohello rôle d’utilisateur est affecté à votre compte, mais hello paramètres d’inscription d’application (à partir des étapes précédentes de hello) est limitée tooadmin utilisateurs, demandez à votre tooeither administrateur affecter le rôle administrateur tooan ou tooenable utilisateurs tooregister applications.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-136">If your account is assigned toohello User role, but hello app registration setting (from hello preceding steps) is limited tooadmin users, ask your administrator tooeither assign you tooan administrator role, or tooenable users tooregister apps.</span></span>

     ![afficher le rôle](./media/resource-group-create-service-principal-portal/view-role.png)

### <a name="check-azure-subscription-permissions"></a><span data-ttu-id="3bbd2-138">Vérifier les autorisations d’abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="3bbd2-138">Check Azure subscription permissions</span></span>
<span data-ttu-id="3bbd2-139">Dans votre abonnement Azure, votre compte doit avoir `Microsoft.Authorization/*/Write` tooassign un rôle tooa d’application AD d’accès.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-139">In your Azure subscription, your account must have `Microsoft.Authorization/*/Write` access tooassign an AD app tooa role.</span></span> <span data-ttu-id="3bbd2-140">Cette action est accordée via hello [propriétaire](../active-directory/role-based-access-built-in-roles.md#owner) rôle ou [administrateur de l’accès utilisateur](../active-directory/role-based-access-built-in-roles.md#user-access-administrator) rôle.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-140">This action is granted through hello [Owner](../active-directory/role-based-access-built-in-roles.md#owner) role or [User Access Administrator](../active-directory/role-based-access-built-in-roles.md#user-access-administrator) role.</span></span> <span data-ttu-id="3bbd2-141">Si votre compte est affecté toohello **collaborateur** rôle, vous n’avez pas les autorisations adéquates.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-141">If your account is assigned toohello **Contributor** role, you do not have adequate permission.</span></span> <span data-ttu-id="3bbd2-142">Vous recevrez une erreur lors de la tentative de rôle de principal tooa tooassign hello service.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-142">You will receive an error when attempting tooassign hello service principal tooa role.</span></span> 

<span data-ttu-id="3bbd2-143">toocheck vos autorisations d’abonnement :</span><span class="sxs-lookup"><span data-stu-id="3bbd2-143">toocheck your subscription permissions:</span></span>

1. <span data-ttu-id="3bbd2-144">Si vous ne sont pas déjà dans votre compte Azure AD à partir des étapes précédentes de hello, sélectionnez **Azure Active Directory** hello volet de gauche.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-144">If you are not already looking at your Azure AD account from hello preceding steps, select **Azure Active Directory** from hello left pane.</span></span>

2. <span data-ttu-id="3bbd2-145">Recherchez votre compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-145">Find your Azure AD account.</span></span> <span data-ttu-id="3bbd2-146">Sélectionnez **Vue d’ensemble** et **Rechercher un utilisateur** dans Tâches rapides.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-146">Select **Overview** and **Find a user** from Quick tasks.</span></span>

     ![rechercher un utilisateur](./media/resource-group-create-service-principal-portal/find-user.png)
2. <span data-ttu-id="3bbd2-148">Recherchez votre compte et sélectionnez-le lorsque vous l’avez trouvé.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-148">Search for your account, and select it when you find it.</span></span>

     ![rechercher un utilisateur](./media/resource-group-create-service-principal-portal/show-user.png) 
     
3. <span data-ttu-id="3bbd2-150">Sélectionnez **Ressources Azure**.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-150">Select **Azure resources**.</span></span>

     ![sélectionner des ressources](./media/resource-group-create-service-principal-portal/select-azure-resources.png) 
3. <span data-ttu-id="3bbd2-152">Afficher vos rôles sont affectés et déterminer si vous disposez des autorisations adéquates tooassign un rôle tooa d’application AD.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-152">View your assigned roles, and determine if you have adequate permissions tooassign an AD app tooa role.</span></span> <span data-ttu-id="3bbd2-153">Dans le cas contraire, demandez à votre tooadd d’administrateur abonnement rôle administrateur de l’accès tooUser.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-153">If not, ask your subscription administrator tooadd you tooUser Access Administrator role.</span></span> <span data-ttu-id="3bbd2-154">Utilisateur de hello hello suivant l’image, est rôle de propriétaire toohello attribué pour les deux abonnements, ce qui signifie que l’utilisateur dispose des autorisations adéquates.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-154">In hello following image, hello user is assigned toohello Owner role for two subscriptions, which means that user has adequate permissions.</span></span> 

     ![afficher les autorisations](./media/resource-group-create-service-principal-portal/view-assigned-roles.png)

## <a name="create-an-azure-active-directory-application"></a><span data-ttu-id="3bbd2-156">Créer une application Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3bbd2-156">Create an Azure Active Directory application</span></span>
1. <span data-ttu-id="3bbd2-157">Connectez-vous à tooyour compte Azure via hello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3bbd2-157">Log in tooyour Azure Account through hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3bbd2-158">Sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-158">Select **Azure Active Directory**.</span></span>

     ![sélectionner azure active directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)

4. <span data-ttu-id="3bbd2-160">Sélectionnez **Inscriptions d’applications**.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-160">Select **App registrations**.</span></span>   

     ![sélectionner des inscriptions d’applications](./media/resource-group-create-service-principal-portal/select-app-registrations.png)
5. <span data-ttu-id="3bbd2-162">Sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-162">Select **Add**.</span></span>

     ![ajouter une application](./media/resource-group-create-service-principal-portal/select-add-app.png)

6. <span data-ttu-id="3bbd2-164">Fournissez un nom et une URL pour l’application hello.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-164">Provide a name and URL for hello application.</span></span> <span data-ttu-id="3bbd2-165">Sélectionnez **application Web / API** ou **natif** de type hello d’application, vous souhaitez toocreate.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-165">Select either **Web app / API** or **Native** for hello type of application you want toocreate.</span></span> <span data-ttu-id="3bbd2-166">Après avoir défini les valeurs hello, sélectionnez **créer**.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-166">After setting hello values, select **Create**.</span></span>

     ![nommer l’application](./media/resource-group-create-service-principal-portal/create-app.png)

<span data-ttu-id="3bbd2-168">Vous avez créé votre application.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-168">You have created your application.</span></span>

## <a name="get-application-id-and-authentication-key"></a><span data-ttu-id="3bbd2-169">Obtenir un ID d’application et une clé d’authentification</span><span class="sxs-lookup"><span data-stu-id="3bbd2-169">Get application ID and authentication key</span></span>
<span data-ttu-id="3bbd2-170">Lors de la connexion par programme, vous devez hello ID pour votre application et une clé d’authentification.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-170">When programmatically logging in, you need hello ID for your application and an authentication key.</span></span> <span data-ttu-id="3bbd2-171">tooget ces valeurs, hello utilisation comme suit :</span><span class="sxs-lookup"><span data-stu-id="3bbd2-171">tooget those values, use hello following steps:</span></span>

1. <span data-ttu-id="3bbd2-172">Dans **Inscriptions d’applications** dans Azure Active Directory, sélectionnez votre application.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-172">From **App registrations** in Azure Active Directory, select your application.</span></span>

     ![sélectionner une application](./media/resource-group-create-service-principal-portal/select-app.png)
2. <span data-ttu-id="3bbd2-174">Hello de copie **ID d’Application** et stockez-le dans votre code d’application.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-174">Copy hello **Application ID** and store it in your application code.</span></span> <span data-ttu-id="3bbd2-175">Hello applications Bonjour [exemples d’applications](#sample-applications) section font référence à valeur toothis en tant qu’id de client hello.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-175">hello applications in hello [sample applications](#sample-applications) section refer toothis value as hello client id.</span></span>

     ![ID CLIENT](./media/resource-group-create-service-principal-portal/copy-app-id.png)
3. <span data-ttu-id="3bbd2-177">toogenerate une clé d’authentification, sélectionnez **clés**.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-177">toogenerate an authentication key, select **Keys**.</span></span>

     ![sélectionner des clés](./media/resource-group-create-service-principal-portal/select-keys.png)
4. <span data-ttu-id="3bbd2-179">Fournir une description de la clé de hello et une durée de clé de hello.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-179">Provide a description of hello key, and a duration for hello key.</span></span> <span data-ttu-id="3bbd2-180">Lorsque vous avez terminé, sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-180">When done, select **Save**.</span></span>

     ![enregistrer une clé](./media/resource-group-create-service-principal-portal/save-key.png)

     <span data-ttu-id="3bbd2-182">Après avoir enregistré la clé de hello, hello clé de hello est affichée.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-182">After saving hello key, hello value of hello key is displayed.</span></span> <span data-ttu-id="3bbd2-183">Copiez cette valeur, car vous sont pas en mesure de tooretrieve hello clé plus tard.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-183">Copy this value because you are not able tooretrieve hello key later.</span></span> <span data-ttu-id="3bbd2-184">Vous fournissez les valeur de clé hello hello application ID toolog dans en tant qu’application hello.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-184">You provide hello key value with hello application ID toolog in as hello application.</span></span> <span data-ttu-id="3bbd2-185">Stockez la valeur de clé hello où votre application peut les récupérer.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-185">Store hello key value where your application can retrieve it.</span></span>

     ![clé enregistrée](./media/resource-group-create-service-principal-portal/copy-key.png)

## <a name="get-tenant-id"></a><span data-ttu-id="3bbd2-187">Obtenir l’ID de locataire</span><span class="sxs-lookup"><span data-stu-id="3bbd2-187">Get tenant ID</span></span>
<span data-ttu-id="3bbd2-188">Lors de la connexion par programme, vous avez besoin d’ID de client hello toopass avec votre demande d’authentification.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-188">When programmatically logging in, you need toopass hello tenant ID with your authentication request.</span></span> 

1. <span data-ttu-id="3bbd2-189">ID de client tooget hello, sélectionnez **propriétés** pour votre locataire Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-189">tooget hello tenant ID, select **Properties** for your Azure AD tenant.</span></span> 

     ![Sélectionnez les propriétés Azure AD](./media/resource-group-create-service-principal-portal/select-ad-properties.png)

2. <span data-ttu-id="3bbd2-191">Hello de copie **ID de répertoire**.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-191">Copy hello **Directory ID**.</span></span> <span data-ttu-id="3bbd2-192">Cette valeur est votre ID de locataire.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-192">This value is your tenant ID.</span></span>

     ![ID client](./media/resource-group-create-service-principal-portal/copy-directory-id.png)

## <a name="assign-application-toorole"></a><span data-ttu-id="3bbd2-194">Affecter l’application toorole</span><span class="sxs-lookup"><span data-stu-id="3bbd2-194">Assign application toorole</span></span>
<span data-ttu-id="3bbd2-195">tooaccess des ressources dans votre abonnement, vous devez attribuer le rôle de tooa application hello.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-195">tooaccess resources in your subscription, you must assign hello application tooa role.</span></span> <span data-ttu-id="3bbd2-196">Décider quel rôle représente les autorisations de droite hello pour une application hello.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-196">Decide which role represents hello right permissions for hello application.</span></span> <span data-ttu-id="3bbd2-197">toolearn sur les rôles disponibles de hello, consultez [RBAC : générées dans les rôles](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="3bbd2-197">toolearn about hello available roles, see [RBAC: Built in Roles](../active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="3bbd2-198">Vous pouvez définir l’étendue de hello au niveau hello d’abonnement de hello, groupe de ressources ou ressource.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-198">You can set hello scope at hello level of hello subscription, resource group, or resource.</span></span> <span data-ttu-id="3bbd2-199">Les autorisations sont héritées toolower des niveaux de portée.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-199">Permissions are inherited toolower levels of scope.</span></span> <span data-ttu-id="3bbd2-200">Par exemple, ajout d’un rôle de lecteur application toohello pour un groupe de ressources signifie qu’il peut lire toutes les ressources qu’il contient et groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-200">For example, adding an application toohello Reader role for a resource group means it can read hello resource group and any resources it contains.</span></span>

1. <span data-ttu-id="3bbd2-201">Accédez au niveau du toohello de portée qu'application hello tooassign vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-201">Navigate toohello level of scope you wish tooassign hello application to.</span></span> <span data-ttu-id="3bbd2-202">Par exemple, tooassign un rôle au niveau de l’étendue de l’abonnement hello, sélectionnez **abonnements**.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-202">For example, tooassign a role at hello subscription scope, select **Subscriptions**.</span></span> <span data-ttu-id="3bbd2-203">Vous pouvez également sélectionner un groupe de ressources ou une ressource.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-203">You could instead select a resource group or resource.</span></span>

     ![sélectionner l'abonnement](./media/resource-group-create-service-principal-portal/select-subscription.png)

2. <span data-ttu-id="3bbd2-205">Sélectionnez un abonnement spécifique (groupe de ressources ou ressource) tooassign hello application hello pour.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-205">Select hello particular subscription (resource group or resource) tooassign hello application to.</span></span>

     ![sélectionner l’abonnement pour l’affectation](./media/resource-group-create-service-principal-portal/select-one-subscription.png)

3. <span data-ttu-id="3bbd2-207">Sélectionnez **Contrôle d’accès (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-207">Select **Access Control (IAM)**.</span></span>

     ![sélectionner l’accès](./media/resource-group-create-service-principal-portal/select-access-control.png)

4. <span data-ttu-id="3bbd2-209">Sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-209">Select **Add**.</span></span>

     ![sélectionner ajouter](./media/resource-group-create-service-principal-portal/select-add.png)
6. <span data-ttu-id="3bbd2-211">Sélectionnez le rôle hello vous souhaitez tooassign toohello application.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-211">Select hello role you wish tooassign toohello application.</span></span> <span data-ttu-id="3bbd2-212">Hello image suivante montre hello **lecteur** rôle.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-212">hello following image shows hello **Reader** role.</span></span>

     ![sélectionner un rôle](./media/resource-group-create-service-principal-portal/select-role.png)

8. <span data-ttu-id="3bbd2-214">Recherchez votre application et sélectionnez-la.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-214">Search for your application, and select it.</span></span>

     ![rechercher une application](./media/resource-group-create-service-principal-portal/search-app.png)
9. <span data-ttu-id="3bbd2-216">Sélectionnez **OK** toofinish affectation hello rôle.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-216">Select **OK** toofinish assigning hello role.</span></span> <span data-ttu-id="3bbd2-217">Vous consultez votre application dans la liste de hello des utilisateurs affectés du rôle tooa pour cette étendue.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-217">You see your application in hello list of users assigned tooa role for that scope.</span></span>

## <a name="log-in-as-hello-application"></a><span data-ttu-id="3bbd2-218">Connectez-vous en tant qu’application hello</span><span class="sxs-lookup"><span data-stu-id="3bbd2-218">Log in as hello application</span></span>

<span data-ttu-id="3bbd2-219">Votre application est maintenant configurée dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-219">Your application is now set up in Azure Active Directory.</span></span> <span data-ttu-id="3bbd2-220">Vous avez un ID et la clé toouse pour vous connecter en tant qu’application hello.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-220">You have an ID and key toouse for signing in as hello application.</span></span> <span data-ttu-id="3bbd2-221">application Hello rôle tooa qui lui donne certaines actions, qu'il peut effectuer.</span><span class="sxs-lookup"><span data-stu-id="3bbd2-221">hello application is assigned tooa role that gives it certain actions it can perform.</span></span> <span data-ttu-id="3bbd2-222">Pour plus d’informations sur la connexion en tant qu’application hello via différentes plateformes, consultez :</span><span class="sxs-lookup"><span data-stu-id="3bbd2-222">For information about logging in as hello application through different platforms, see:</span></span>

* [<span data-ttu-id="3bbd2-223">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3bbd2-223">PowerShell</span></span>](resource-group-authenticate-service-principal.md#provide-credentials-through-powershell)
* [<span data-ttu-id="3bbd2-224">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="3bbd2-224">Azure CLI</span></span>](resource-group-authenticate-service-principal-cli.md#provide-credentials-through-azure-cli)
* [<span data-ttu-id="3bbd2-225">REST</span><span class="sxs-lookup"><span data-stu-id="3bbd2-225">REST</span></span>](/rest/api/#create-the-request)
* [<span data-ttu-id="3bbd2-226">.NET</span><span class="sxs-lookup"><span data-stu-id="3bbd2-226">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="3bbd2-227">Java</span><span class="sxs-lookup"><span data-stu-id="3bbd2-227">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="3bbd2-228">Node.JS</span><span class="sxs-lookup"><span data-stu-id="3bbd2-228">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="3bbd2-229">Python</span><span class="sxs-lookup"><span data-stu-id="3bbd2-229">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="3bbd2-230">Ruby</span><span class="sxs-lookup"><span data-stu-id="3bbd2-230">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)


## <a name="next-steps"></a><span data-ttu-id="3bbd2-231">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3bbd2-231">Next steps</span></span>
* <span data-ttu-id="3bbd2-232">tooset d’une application mutualisée, consultez [tooauthorization du guide du développeur avec hello API Azure Resource Manager](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="3bbd2-232">tooset up a multi-tenant application, see [Developer's guide tooauthorization with hello Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="3bbd2-233">toolearn sur la spécification des stratégies de sécurité, consultez [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="3bbd2-233">toolearn about specifying security policies, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>  
* <span data-ttu-id="3bbd2-234">Pour obtenir la liste des actions disponibles qui peuvent être accordées ou refusées toousers, consultez [opérations du fournisseur de ressources Azure Resource Manager](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="3bbd2-234">For a list of available actions that can be granted or denied toousers, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>
