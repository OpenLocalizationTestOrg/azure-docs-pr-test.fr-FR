---
title: aaaCreate un Principal de Service pour la pile de Azure | Documents Microsoft
description: "Décrit comment toocreate un principal de service qui peut être utilisé avec le contrôle d’accès basé sur rôle hello dans Azure Resource Manager toomanage accès tooresources."
services: azure-resource-manager
documentationcenter: na
author: heathl17
manager: byronr
ms.assetid: 7068617b-ac5e-47b3-a1de-a18c918297b6
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: helaw
ms.openlocfilehash: f090ceed941abe9255bc35ec966bc43df3bb2955
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="provide-applications-access-tooazure-stack"></a><span data-ttu-id="4e0b5-103">Fournir des applications accès tooAzure pile</span><span class="sxs-lookup"><span data-stu-id="4e0b5-103">Provide applications access tooAzure Stack</span></span>
<span data-ttu-id="4e0b5-104">Lorsqu’une application a besoin d’accès toodeploy ou configurer des ressources par le biais du Gestionnaire de ressources Azure dans la pile d’Azure, vous créez un service principal, qui est une information d’identification pour votre application.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-104">When an application needs access toodeploy or configure resources through Azure Resource Manager in Azure Stack, you create a service principal, which is a credential for your application.</span></span>  <span data-ttu-id="4e0b5-105">Vous pouvez ensuite déléguer uniquement hello autorisations nécessaires toothat principal du service.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-105">You can then delegate only hello necessary permissions toothat service principal.</span></span>  

<span data-ttu-id="4e0b5-106">Par exemple, vous avez peut-être un outil de gestion de configuration qui utilise Azure Resource Manager tooinventory ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-106">As an example, you may have a configuration management tool that uses Azure Resource Manager tooinventory Azure resources.</span></span>  <span data-ttu-id="4e0b5-107">Dans ce scénario, vous pouvez créer un principal de service, accorder lecteur de hello service toothat de rôle principal et limiter hello gestion outil tooread uniquement accès à la configuration.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-107">In this scenario, you can create a service principal, grant hello reader role toothat service principal, and limit hello configuration management tool tooread-only access.</span></span> 

<span data-ttu-id="4e0b5-108">Principaux de service sont application hello de toorunning préférable avec vos propres informations d’identification, car :</span><span class="sxs-lookup"><span data-stu-id="4e0b5-108">Service principals are preferable toorunning hello app under your own credentials because:</span></span>

* <span data-ttu-id="4e0b5-109">Vous pouvez affecter des autorisations toohello principal du service qui sont différentes des autorisations de votre propre compte.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-109">You can assign permissions toohello service principal that are different than your own account permissions.</span></span> <span data-ttu-id="4e0b5-110">En règle générale, ces autorisations sont limitée tooexactly quelle application hello doit toodo.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-110">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span>
* <span data-ttu-id="4e0b5-111">Vous n’avez pas les informations d’identification de l’application toochange hello si vos responsabilités changent.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-111">You do not have toochange hello app's credentials if your responsibilities change.</span></span>
* <span data-ttu-id="4e0b5-112">Vous pouvez utiliser une authentification de tooautomate certificat lors de l’exécution d’un script sans assistance.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-112">You can use a certificate tooautomate authentication when executing an unattended script.</span></span>  

## <a name="getting-started"></a><span data-ttu-id="4e0b5-113">Prise en main</span><span class="sxs-lookup"><span data-stu-id="4e0b5-113">Getting started</span></span>

<span data-ttu-id="4e0b5-114">Selon la façon dont vous avez déployé Azure Stack, commencez par créer un principal de service.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-114">Depending on how you have deployed Azure Stack, you start by creating a service principal.</span></span>  <span data-ttu-id="4e0b5-115">Ce document vous guide tout au long de la création d’un principal de service à la fois pour [Azure Active Directory (Azure AD)](azure-stack-create-service-principals.md#create-service-principal-for-azure-ad) et pour [Active Directory Federation Services (AD FS)](azure-stack-create-service-principals.md#create-service-principal-for-ad-fs).</span><span class="sxs-lookup"><span data-stu-id="4e0b5-115">This document guides you through creating a service principal for both [Azure Active Directory (Azure AD)](azure-stack-create-service-principals.md#create-service-principal-for-azure-ad) and [Active Directory Federation Services(AD FS)](azure-stack-create-service-principals.md#create-service-principal-for-ad-fs).</span></span>  <span data-ttu-id="4e0b5-116">Une fois que vous avez créé hello principal du service, un ensemble d’étapes de tooboth common AD FS et l’Azure Active Directory sont utilisées trop[déléguer des autorisations](azure-stack-create-service-principals.md#assign-role-to-service-principal) toohello rôle.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-116">Once you've created hello service principal, a set of steps common tooboth AD FS and Azure Active Directory are used too[delegate permissions](azure-stack-create-service-principals.md#assign-role-to-service-principal) toohello role.</span></span>     

## <a name="create-service-principal-for-azure-ad"></a><span data-ttu-id="4e0b5-117">Créer un principal de service pour Azure AD</span><span class="sxs-lookup"><span data-stu-id="4e0b5-117">Create service principal for Azure AD</span></span>

<span data-ttu-id="4e0b5-118">Si vous avez déployé la pile de Azure à l’aide de Azure AD en tant que magasin d’identités hello, vous pouvez créer des principaux de service comme vous le feriez pour Azure.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-118">If you've deployed Azure Stack using Azure AD as hello identity store, you can create service principals just like you do for Azure.</span></span>  <span data-ttu-id="4e0b5-119">Cette section vous montre comment les étapes tooperform hello via le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-119">This section shows you how tooperform hello steps through hello portal.</span></span>  <span data-ttu-id="4e0b5-120">Vérifiez que vous avez hello [AD Azure autorisations requises](../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-120">Check that you have hello [required Azure AD permissions](../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions) before beginning.</span></span>

### <a name="create-service-principal"></a><span data-ttu-id="4e0b5-121">Créer un principal du service</span><span class="sxs-lookup"><span data-stu-id="4e0b5-121">Create service principal</span></span>
<span data-ttu-id="4e0b5-122">Dans cette section, vous allez créer une application (principal de service) dans Azure AD qui représentera votre application.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-122">In this section, you create an application (service principal) in Azure AD that will represent your application.</span></span>

1. <span data-ttu-id="4e0b5-123">Connectez-vous à tooyour compte Azure via hello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4e0b5-123">Log in tooyour Azure Account through hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4e0b5-124">Sélectionnez **Azure Active Directory** > **Enregistrement d’applications** > **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-124">Select **Azure Active Directory** > **App registrations** > **Add**</span></span>   
3. <span data-ttu-id="4e0b5-125">Fournissez un nom et une URL pour l’application hello.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-125">Provide a name and URL for hello application.</span></span> <span data-ttu-id="4e0b5-126">Sélectionnez **application Web / API** ou **natif** de type hello d’application, vous souhaitez toocreate.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-126">Select either **Web app / API** or **Native** for hello type of application you want toocreate.</span></span> <span data-ttu-id="4e0b5-127">Après avoir défini les valeurs hello, sélectionnez **créer**.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-127">After setting hello values, select **Create**.</span></span>

<span data-ttu-id="4e0b5-128">Vous avez créé un principal de service pour votre application.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-128">You have created a service principal for your application.</span></span>

### <a name="get-credentials"></a><span data-ttu-id="4e0b5-129">Récupérer les informations d’identification</span><span class="sxs-lookup"><span data-stu-id="4e0b5-129">Get credentials</span></span>
<span data-ttu-id="4e0b5-130">Lors de la connexion par programme, vous utilisez hello ID pour votre application et une clé d’authentification.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-130">When programmatically logging in, you use hello ID for your application and an authentication key.</span></span> <span data-ttu-id="4e0b5-131">tooget ces valeurs, hello utilisation comme suit :</span><span class="sxs-lookup"><span data-stu-id="4e0b5-131">tooget those values, use hello following steps:</span></span>

1. <span data-ttu-id="4e0b5-132">Dans **Inscriptions d’applications** dans Active Directory, sélectionnez votre application.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-132">From **App registrations** in Active Directory, select your application.</span></span>

2. <span data-ttu-id="4e0b5-133">Hello de copie **ID d’Application** et stockez-le dans votre code d’application.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-133">Copy hello **Application ID** and store it in your application code.</span></span> <span data-ttu-id="4e0b5-134">Hello applications Bonjour [exemples d’applications](#sample-applications) section font référence à valeur toothis en tant qu’id de client hello.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-134">hello applications in hello [sample applications](#sample-applications) section refer toothis value as hello client id.</span></span>

     ![ID CLIENT](./media/azure-stack-create-service-principal/image12.png)
3. <span data-ttu-id="4e0b5-136">toogenerate une clé d’authentification, sélectionnez **clés**.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-136">toogenerate an authentication key, select **Keys**.</span></span>

4. <span data-ttu-id="4e0b5-137">Fournir une description de la clé de hello et une durée de clé de hello.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-137">Provide a description of hello key, and a duration for hello key.</span></span> <span data-ttu-id="4e0b5-138">Lorsque vous avez terminé, sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-138">When done, select **Save**.</span></span>

<span data-ttu-id="4e0b5-139">Après avoir enregistré la clé de hello, hello clé de hello est affichée.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-139">After saving hello key, hello value of hello key is displayed.</span></span> <span data-ttu-id="4e0b5-140">Copiez cette valeur, car vous sont pas en mesure de tooretrieve hello clé plus tard.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-140">Copy this value because you are not able tooretrieve hello key later.</span></span> <span data-ttu-id="4e0b5-141">Vous fournissez les valeur de clé hello hello application ID toosign en tant qu’application hello.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-141">You provide hello key value with hello application ID toosign as hello application.</span></span> <span data-ttu-id="4e0b5-142">Stockez la valeur de clé hello où votre application peut les récupérer.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-142">Store hello key value where your application can retrieve it.</span></span>

![clé enregistrée](./media/azure-stack-create-service-principal/image15.png)


<span data-ttu-id="4e0b5-144">Une fois terminé, passez trop[affectation d’un rôle de votre application](azure-stack-create-service-principals.md#assign-role-to-service-principal).</span><span class="sxs-lookup"><span data-stu-id="4e0b5-144">Once complete, proceed too[assigning your application a role](azure-stack-create-service-principals.md#assign-role-to-service-principal).</span></span>

## <a name="create-service-principal-for-ad-fs"></a><span data-ttu-id="4e0b5-145">Créer un principal de service pour AD FS</span><span class="sxs-lookup"><span data-stu-id="4e0b5-145">Create service principal for AD FS</span></span>
<span data-ttu-id="4e0b5-146">Si vous avez déployé la pile d’Azure avec AD FS, vous pouvez utiliser PowerShell toocreate un principal de service, attribuez un rôle pour l’accès et de connexion à partir de PowerShell à l’aide de cette identité.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-146">If you have deployed Azure Stack with AD FS, you can use PowerShell toocreate a service principal, assign a role for access, and sign in from PowerShell using that identity.</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="4e0b5-147">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="4e0b5-147">Before you begin</span></span>

[<span data-ttu-id="4e0b5-148">Téléchargez toowork requis de hello outils avec l’ordinateur local de Azure pile tooyour.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-148">Download hello tools required toowork with Azure Stack tooyour local computer.</span></span>](azure-stack-powershell-download.md)

### <a name="import-hello-identity-powershell-module"></a><span data-ttu-id="4e0b5-149">Module PowerShell de l’identité d’importation hello</span><span class="sxs-lookup"><span data-stu-id="4e0b5-149">Import hello Identity PowerShell module</span></span>
<span data-ttu-id="4e0b5-150">Après avoir téléchargé les outils hello, accédez toohello téléchargé dossier et d’importation du module PowerShell de l’identité de hello à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4e0b5-150">After you download hello tools, navigate toohello downloaded folder and import hello Identity PowerShell module by using hello following command:</span></span>

```PowerShell
Import-Module .\Identity\AzureStack.Identity.psm1
```

<span data-ttu-id="4e0b5-151">Lorsque vous importez le module de hello, vous pouvez recevoir une erreur indiquant que « AzureStack.Connect.psm1 n’est pas numériquement signé.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-151">When you import hello module, you may receive an error that says “AzureStack.Connect.psm1 is not digitally signed.</span></span> <span data-ttu-id="4e0b5-152">script de Hello s’exécute pas sur le système de hello ».</span><span class="sxs-lookup"><span data-stu-id="4e0b5-152">hello script will not execute on hello system”.</span></span> <span data-ttu-id="4e0b5-153">tooresolve ce problème, vous pouvez définir tooallow de stratégie de l’exécution du script de hello en cours d’exécution avec la commande suivante dans une session PowerShell avec élévation de privilèges de hello :</span><span class="sxs-lookup"><span data-stu-id="4e0b5-153">tooresolve this issue, you can set execution policy tooallow running hello script with hello following command in an elevated PowerShell session:</span></span>

```PowerShell
Set-ExecutionPolicy Unrestricted
```

### <a name="create-hello-service-principal"></a><span data-ttu-id="4e0b5-154">Créer hello principal de service</span><span class="sxs-lookup"><span data-stu-id="4e0b5-154">Create hello service principal</span></span>
<span data-ttu-id="4e0b5-155">Vous pouvez créer un Principal de Service en exécutant hello suit commande, effectuant que tooupdate hello *DisplayName* paramètre :</span><span class="sxs-lookup"><span data-stu-id="4e0b5-155">You can create a Service Principal by executing hello following command, making sure tooupdate hello *DisplayName* parameter:</span></span>
```powershell
$servicePrincipal = New-AzSADGraphServicePrincipal `
 -DisplayName "<YourServicePrincipalName>" `
 -AdminCredential $(Get-Credential) `
 -AdfsMachineName "AZS-ADFS01" `
 -Verbose
```
### <a name="assign-a-role"></a><span data-ttu-id="4e0b5-156">Attribuer un rôle</span><span class="sxs-lookup"><span data-stu-id="4e0b5-156">Assign a role</span></span>
<span data-ttu-id="4e0b5-157">Une fois hello Principal du Service est créé, vous devez [lui attribue le rôle de tooa](azure-stack-create-service-principals.md#assign-role-to-service-principal)</span><span class="sxs-lookup"><span data-stu-id="4e0b5-157">Once hello Service Principal is created, you must [assign it tooa role](azure-stack-create-service-principals.md#assign-role-to-service-principal)</span></span>

### <a name="sign-in-through-powershell"></a><span data-ttu-id="4e0b5-158">Se connecter avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e0b5-158">Sign in through PowerShell</span></span>
<span data-ttu-id="4e0b5-159">Une fois que vous avez affecté un rôle, vous pouvez vous connecter tooAzure pile à l’aide de principal du service hello avec hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4e0b5-159">Once you've assigned a role, you can sign in tooAzure Stack using hello service principal with hello following command:</span></span>

```powershell
Add-AzureRmAccount -EnvironmentName "<AzureStackEnvironmentName>" `
 -ServicePrincipal `
 -CertificateThumbprint $servicePrincipal.Thumbprint `
 -ApplicationId $servicePrincipal.ApplicationId ` 
 -TenantId $directoryTenantId
```

## <a name="assign-role-tooservice-principal"></a><span data-ttu-id="4e0b5-160">Affecter le rôle tooservice principal</span><span class="sxs-lookup"><span data-stu-id="4e0b5-160">Assign role tooservice principal</span></span>
<span data-ttu-id="4e0b5-161">tooaccess des ressources dans votre abonnement, vous devez attribuer le rôle de tooa application hello.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-161">tooaccess resources in your subscription, you must assign hello application tooa role.</span></span> <span data-ttu-id="4e0b5-162">Décider quel rôle représente les autorisations de droite hello pour une application hello.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-162">Decide which role represents hello right permissions for hello application.</span></span> <span data-ttu-id="4e0b5-163">toolearn sur les rôles disponibles de hello, consultez [RBAC : générées dans les rôles](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="4e0b5-163">toolearn about hello available roles, see [RBAC: Built in Roles](../active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="4e0b5-164">Vous pouvez définir l’étendue de hello au niveau hello d’abonnement de hello, groupe de ressources ou ressource.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-164">You can set hello scope at hello level of hello subscription, resource group, or resource.</span></span> <span data-ttu-id="4e0b5-165">Les autorisations sont héritées toolower des niveaux de portée.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-165">Permissions are inherited toolower levels of scope.</span></span> <span data-ttu-id="4e0b5-166">Par exemple, ajout d’un rôle de lecteur application toohello pour un groupe de ressources signifie qu’il peut lire toutes les ressources qu’il contient et groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-166">For example, adding an application toohello Reader role for a resource group means it can read hello resource group and any resources it contains.</span></span>

1. <span data-ttu-id="4e0b5-167">Dans le portail Azure pile hello, accédez au niveau du toohello de portée qu'application hello tooassign vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-167">In hello Azure Stack portal, navigate toohello level of scope you wish tooassign hello application to.</span></span> <span data-ttu-id="4e0b5-168">Par exemple, tooassign un rôle au niveau de l’étendue de l’abonnement hello, sélectionnez **abonnements**.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-168">For example, tooassign a role at hello subscription scope, select **Subscriptions**.</span></span> <span data-ttu-id="4e0b5-169">Vous pouvez également sélectionner un groupe de ressources ou une ressource.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-169">You could instead select a resource group or resource.</span></span>

2. <span data-ttu-id="4e0b5-170">Sélectionnez un abonnement spécifique (groupe de ressources ou ressource) tooassign hello application hello pour.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-170">Select hello particular subscription (resource group or resource) tooassign hello application to.</span></span>

     ![sélectionner l’abonnement pour l’affectation](./media/azure-stack-create-service-principal/image16.png)

3. <span data-ttu-id="4e0b5-172">Sélectionnez **Contrôle d’accès (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-172">Select **Access Control (IAM)**.</span></span>

     ![sélectionner l’accès](./media/azure-stack-create-service-principal/image17.png)

4. <span data-ttu-id="4e0b5-174">Sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-174">Select **Add**.</span></span>

5. <span data-ttu-id="4e0b5-175">Sélectionnez le rôle hello vous souhaitez tooassign toohello application.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-175">Select hello role you wish tooassign toohello application.</span></span>

6. <span data-ttu-id="4e0b5-176">Recherchez votre application et sélectionnez-la.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-176">Search for your application, and select it.</span></span>

7. <span data-ttu-id="4e0b5-177">Sélectionnez **OK** toofinish affectation hello rôle.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-177">Select **OK** toofinish assigning hello role.</span></span> <span data-ttu-id="4e0b5-178">Vous consultez votre application dans la liste de hello des utilisateurs affectés du rôle tooa pour cette étendue.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-178">You see your application in hello list of users assigned tooa role for that scope.</span></span>

<span data-ttu-id="4e0b5-179">Maintenant que vous avez créé un principal de service et affecté un rôle, vous pouvez commencer à l’aide de ce au sein de votre application de tooaccess ressources de la pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="4e0b5-179">Now that you've created a service principal and assigned a role, you can begin using this within your application tooaccess Azure Stack resources.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="4e0b5-180">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4e0b5-180">Next steps</span></span>

<span data-ttu-id="4e0b5-181">[Ajouter des utilisateurs pour ADFS](azure-stack-add-users-adfs.md)
[Gérer les autorisations des utilisateurs](azure-stack-manage-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="4e0b5-181">[Add users for ADFS](azure-stack-add-users-adfs.md)
[Manage user permissions](azure-stack-manage-permissions.md)</span></span>