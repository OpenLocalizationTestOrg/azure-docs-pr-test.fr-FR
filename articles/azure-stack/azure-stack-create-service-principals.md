---
title: "Créer un principal de service pour Azure Stack | Microsoft Docs"
description: "Explique comment créer un principal de service utilisable avec le contrôle d’accès en fonction du rôle dans Azure Resource Manager pour gérer l’accès aux ressources."
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
ms.openlocfilehash: b3992b296d5a999601eb69b071559f9d37dacf8f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="provide-applications-access-to-azure-stack"></a><span data-ttu-id="84af4-103">Fournir l’accès des applications à Azure Stack</span><span class="sxs-lookup"><span data-stu-id="84af4-103">Provide applications access to Azure Stack</span></span>
<span data-ttu-id="84af4-104">Lorsqu’une application a besoin d’accès pour déployer ou configurer des ressources par le biais d’Azure Resource Manager dans Azure Stack, créez un principal de service qui constitue l’information d’identification de votre application.</span><span class="sxs-lookup"><span data-stu-id="84af4-104">When an application needs access to deploy or configure resources through Azure Resource Manager in Azure Stack, you create a service principal, which is a credential for your application.</span></span>  <span data-ttu-id="84af4-105">Vous pouvez ensuite lui déléguer uniquement les autorisations nécessaires.</span><span class="sxs-lookup"><span data-stu-id="84af4-105">You can then delegate only the necessary permissions to that service principal.</span></span>  

<span data-ttu-id="84af4-106">Par exemple, vous avez peut-être un outil de gestion de la configuration qui utilise Azure Resource Manager pour inventorier les ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="84af4-106">As an example, you may have a configuration management tool that uses Azure Resource Manager to inventory Azure resources.</span></span>  <span data-ttu-id="84af4-107">Dans ce scénario, vous pouvez créer un principal de service, lui accorder le rôle de lecteur et limiter l’outil de gestion de la configuration à un accès en lecture seule.</span><span class="sxs-lookup"><span data-stu-id="84af4-107">In this scenario, you can create a service principal, grant the reader role to that service principal, and limit the configuration management tool to read-only access.</span></span> 

<span data-ttu-id="84af4-108">De préférence, utilisez des principaux de service plutôt que d’exécuter l’application avec vos propres informations d’identification, car :</span><span class="sxs-lookup"><span data-stu-id="84af4-108">Service principals are preferable to running the app under your own credentials because:</span></span>

* <span data-ttu-id="84af4-109">Vous pouvez attribuer au principal de service des autorisations différentes des vôtres.</span><span class="sxs-lookup"><span data-stu-id="84af4-109">You can assign permissions to the service principal that are different than your own account permissions.</span></span> <span data-ttu-id="84af4-110">En règle générale, ces autorisations sont strictement limitées à ce que l’application doit faire.</span><span class="sxs-lookup"><span data-stu-id="84af4-110">Typically, these permissions are restricted to exactly what the app needs to do.</span></span>
* <span data-ttu-id="84af4-111">Il est inutile de modifier les informations d’identification de l’application si vos responsabilités évoluent.</span><span class="sxs-lookup"><span data-stu-id="84af4-111">You do not have to change the app's credentials if your responsibilities change.</span></span>
* <span data-ttu-id="84af4-112">Vous pouvez utiliser un certificat pour automatiser l’authentification lors de l’exécution d’un script sans assistance.</span><span class="sxs-lookup"><span data-stu-id="84af4-112">You can use a certificate to automate authentication when executing an unattended script.</span></span>  

## <a name="getting-started"></a><span data-ttu-id="84af4-113">Prise en main</span><span class="sxs-lookup"><span data-stu-id="84af4-113">Getting started</span></span>

<span data-ttu-id="84af4-114">Selon la façon dont vous avez déployé Azure Stack, commencez par créer un principal de service.</span><span class="sxs-lookup"><span data-stu-id="84af4-114">Depending on how you have deployed Azure Stack, you start by creating a service principal.</span></span>  <span data-ttu-id="84af4-115">Ce document vous guide tout au long de la création d’un principal de service à la fois pour [Azure Active Directory (Azure AD)](azure-stack-create-service-principals.md#create-service-principal-for-azure-ad) et pour [Active Directory Federation Services (AD FS)](azure-stack-create-service-principals.md#create-service-principal-for-ad-fs).</span><span class="sxs-lookup"><span data-stu-id="84af4-115">This document guides you through creating a service principal for both [Azure Active Directory (Azure AD)](azure-stack-create-service-principals.md#create-service-principal-for-azure-ad) and [Active Directory Federation Services(AD FS)](azure-stack-create-service-principals.md#create-service-principal-for-ad-fs).</span></span>  <span data-ttu-id="84af4-116">Une fois que vous avez créé le principal de service, une série d’étapes communes à AD FS et à Azure Active Directory permet de [déléguer des autorisations](azure-stack-create-service-principals.md#assign-role-to-service-principal) à ce rôle.</span><span class="sxs-lookup"><span data-stu-id="84af4-116">Once you've created the service principal, a set of steps common to both AD FS and Azure Active Directory are used to [delegate permissions](azure-stack-create-service-principals.md#assign-role-to-service-principal) to the role.</span></span>     

## <a name="create-service-principal-for-azure-ad"></a><span data-ttu-id="84af4-117">Créer un principal de service pour Azure AD</span><span class="sxs-lookup"><span data-stu-id="84af4-117">Create service principal for Azure AD</span></span>

<span data-ttu-id="84af4-118">Si vous avez déployé Azure Stack avec Azure AD comme magasin d’identités, vous pouvez créer des principaux de service de la même façon que pour Azure.</span><span class="sxs-lookup"><span data-stu-id="84af4-118">If you've deployed Azure Stack using Azure AD as the identity store, you can create service principals just like you do for Azure.</span></span>  <span data-ttu-id="84af4-119">Cette rubrique explique comment suivre ces étapes sur le portail.</span><span class="sxs-lookup"><span data-stu-id="84af4-119">This section shows you how to perform the steps through the portal.</span></span>  <span data-ttu-id="84af4-120">Vérifiez que vous disposez des [autorisations Azure AD requises](../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="84af4-120">Check that you have the [required Azure AD permissions](../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions) before beginning.</span></span>

### <a name="create-service-principal"></a><span data-ttu-id="84af4-121">Créer un principal du service</span><span class="sxs-lookup"><span data-stu-id="84af4-121">Create service principal</span></span>
<span data-ttu-id="84af4-122">Dans cette section, vous allez créer une application (principal de service) dans Azure AD qui représentera votre application.</span><span class="sxs-lookup"><span data-stu-id="84af4-122">In this section, you create an application (service principal) in Azure AD that will represent your application.</span></span>

1. <span data-ttu-id="84af4-123">Connectez-vous à votre compte Azure via le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="84af4-123">Log in to your Azure Account through the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="84af4-124">Sélectionnez **Azure Active Directory** > **Enregistrement d’applications** > **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="84af4-124">Select **Azure Active Directory** > **App registrations** > **Add**</span></span>   
3. <span data-ttu-id="84af4-125">Fournissez un nom et une URL pour l’application.</span><span class="sxs-lookup"><span data-stu-id="84af4-125">Provide a name and URL for the application.</span></span> <span data-ttu-id="84af4-126">Sélectionnez **Application Web / API** ou **Native** pour le type d’application que vous souhaitez créer.</span><span class="sxs-lookup"><span data-stu-id="84af4-126">Select either **Web app / API** or **Native** for the type of application you want to create.</span></span> <span data-ttu-id="84af4-127">Après avoir défini les valeurs, sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="84af4-127">After setting the values, select **Create**.</span></span>

<span data-ttu-id="84af4-128">Vous avez créé un principal de service pour votre application.</span><span class="sxs-lookup"><span data-stu-id="84af4-128">You have created a service principal for your application.</span></span>

### <a name="get-credentials"></a><span data-ttu-id="84af4-129">Récupérer les informations d’identification</span><span class="sxs-lookup"><span data-stu-id="84af4-129">Get credentials</span></span>
<span data-ttu-id="84af4-130">Si vous vous connectez par programmation, utilisez l’ID de votre application et une clé d’authentification.</span><span class="sxs-lookup"><span data-stu-id="84af4-130">When programmatically logging in, you use the ID for your application and an authentication key.</span></span> <span data-ttu-id="84af4-131">Pour obtenir ces valeurs, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="84af4-131">To get those values, use the following steps:</span></span>

1. <span data-ttu-id="84af4-132">Dans **Inscriptions d’applications** dans Active Directory, sélectionnez votre application.</span><span class="sxs-lookup"><span data-stu-id="84af4-132">From **App registrations** in Active Directory, select your application.</span></span>

2. <span data-ttu-id="84af4-133">Copiez l’**ID d’application** et stockez-le dans votre code d’application.</span><span class="sxs-lookup"><span data-stu-id="84af4-133">Copy the **Application ID** and store it in your application code.</span></span> <span data-ttu-id="84af4-134">Les applications de la section [Exemples d’applications](#sample-applications) font référence à cette valeur en tant qu’ID de locataire.</span><span class="sxs-lookup"><span data-stu-id="84af4-134">The applications in the [sample applications](#sample-applications) section refer to this value as the client id.</span></span>

     ![ID CLIENT](./media/azure-stack-create-service-principal/image12.png)
3. <span data-ttu-id="84af4-136">Pour générer une clé d’authentification, sélectionnez **Clés**.</span><span class="sxs-lookup"><span data-stu-id="84af4-136">To generate an authentication key, select **Keys**.</span></span>

4. <span data-ttu-id="84af4-137">Fournissez une description de la clé et la durée de la clé.</span><span class="sxs-lookup"><span data-stu-id="84af4-137">Provide a description of the key, and a duration for the key.</span></span> <span data-ttu-id="84af4-138">Lorsque vous avez terminé, sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="84af4-138">When done, select **Save**.</span></span>

<span data-ttu-id="84af4-139">Après avoir enregistré la clé, la valeur de la clé s’affiche.</span><span class="sxs-lookup"><span data-stu-id="84af4-139">After saving the key, the value of the key is displayed.</span></span> <span data-ttu-id="84af4-140">Copiez cette valeur car vous ne pourrez pas récupérer la clé ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="84af4-140">Copy this value because you are not able to retrieve the key later.</span></span> <span data-ttu-id="84af4-141">Vous fournissez la valeur de la clé avec l’ID d’application pour vous connecter en tant qu’application.</span><span class="sxs-lookup"><span data-stu-id="84af4-141">You provide the key value with the application ID to sign as the application.</span></span> <span data-ttu-id="84af4-142">Stockez la valeur de la clé à un emplacement où votre application peut la récupérer.</span><span class="sxs-lookup"><span data-stu-id="84af4-142">Store the key value where your application can retrieve it.</span></span>

![clé enregistrée](./media/azure-stack-create-service-principal/image15.png)


<span data-ttu-id="84af4-144">Lorsque c’est fait, [attribuez un rôle à votre application](azure-stack-create-service-principals.md#assign-role-to-service-principal).</span><span class="sxs-lookup"><span data-stu-id="84af4-144">Once complete, proceed to [assigning your application a role](azure-stack-create-service-principals.md#assign-role-to-service-principal).</span></span>

## <a name="create-service-principal-for-ad-fs"></a><span data-ttu-id="84af4-145">Créer un principal de service pour AD FS</span><span class="sxs-lookup"><span data-stu-id="84af4-145">Create service principal for AD FS</span></span>
<span data-ttu-id="84af4-146">Si vous avez déployé Azure Stack avec AD FS, vous pouvez utiliser PowerShell pour créer un principal de service, attribuer un rôle pour l’accès et vous connecter à partir de PowerShell avec cette identité.</span><span class="sxs-lookup"><span data-stu-id="84af4-146">If you have deployed Azure Stack with AD FS, you can use PowerShell to create a service principal, assign a role for access, and sign in from PowerShell using that identity.</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="84af4-147">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="84af4-147">Before you begin</span></span>

[<span data-ttu-id="84af4-148">Téléchargez les outils nécessaires pour travailler avec Azure Stack sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="84af4-148">Download the tools required to work with Azure Stack to your local computer.</span></span>](azure-stack-powershell-download.md)

### <a name="import-the-identity-powershell-module"></a><span data-ttu-id="84af4-149">Importer le module Identity PowerShell</span><span class="sxs-lookup"><span data-stu-id="84af4-149">Import the Identity PowerShell module</span></span>
<span data-ttu-id="84af4-150">Après avoir téléchargé les outils, accédez au dossier téléchargé et importez le module Identity PowerShell avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="84af4-150">After you download the tools, navigate to the downloaded folder and import the Identity PowerShell module by using the following command:</span></span>

```PowerShell
Import-Module .\Identity\AzureStack.Identity.psm1
```

<span data-ttu-id="84af4-151">Lorsque vous importez le module, il est possible que vous receviez une erreur indiquant « AzureStack.Connect.psm1 is not digitally signed.</span><span class="sxs-lookup"><span data-stu-id="84af4-151">When you import the module, you may receive an error that says “AzureStack.Connect.psm1 is not digitally signed.</span></span> <span data-ttu-id="84af4-152">The script will not execute on the system » (AzureStack.Connect.psm1 n’est pas signé numériquement. Le script ne s’exécutera pas sur le système).</span><span class="sxs-lookup"><span data-stu-id="84af4-152">The script will not execute on the system”.</span></span> <span data-ttu-id="84af4-153">Pour résoudre ce problème, vous pouvez définir la stratégie d’exécution de façon à permettre l’exécution du script avec la commande suivante dans une session PowerShell avec élévation de privilèges :</span><span class="sxs-lookup"><span data-stu-id="84af4-153">To resolve this issue, you can set execution policy to allow running the script with the following command in an elevated PowerShell session:</span></span>

```PowerShell
Set-ExecutionPolicy Unrestricted
```

### <a name="create-the-service-principal"></a><span data-ttu-id="84af4-154">Créer le principal du service</span><span class="sxs-lookup"><span data-stu-id="84af4-154">Create the service principal</span></span>
<span data-ttu-id="84af4-155">Vous pouvez créer un principal de service avec la commande suivante, en veillant à mettre à jour le paramètre *DisplayName* :</span><span class="sxs-lookup"><span data-stu-id="84af4-155">You can create a Service Principal by executing the following command, making sure to update the *DisplayName* parameter:</span></span>
```powershell
$servicePrincipal = New-AzSADGraphServicePrincipal `
 -DisplayName "<YourServicePrincipalName>" `
 -AdminCredential $(Get-Credential) `
 -AdfsMachineName "AZS-ADFS01" `
 -Verbose
```
### <a name="assign-a-role"></a><span data-ttu-id="84af4-156">Attribuer un rôle</span><span class="sxs-lookup"><span data-stu-id="84af4-156">Assign a role</span></span>
<span data-ttu-id="84af4-157">Une fois le principal de service créé, vous devez [lui attribuer un rôle](azure-stack-create-service-principals.md#assign-role-to-service-principal)</span><span class="sxs-lookup"><span data-stu-id="84af4-157">Once the Service Principal is created, you must [assign it to a role](azure-stack-create-service-principals.md#assign-role-to-service-principal)</span></span>

### <a name="sign-in-through-powershell"></a><span data-ttu-id="84af4-158">Se connecter avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="84af4-158">Sign in through PowerShell</span></span>
<span data-ttu-id="84af4-159">Une fois que vous avez attribué un rôle, vous pouvez vous connecter à Azure Stack à l’aide du principal de service avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="84af4-159">Once you've assigned a role, you can sign in to Azure Stack using the service principal with the following command:</span></span>

```powershell
Add-AzureRmAccount -EnvironmentName "<AzureStackEnvironmentName>" `
 -ServicePrincipal `
 -CertificateThumbprint $servicePrincipal.Thumbprint `
 -ApplicationId $servicePrincipal.ApplicationId ` 
 -TenantId $directoryTenantId
```

## <a name="assign-role-to-service-principal"></a><span data-ttu-id="84af4-160">Attribuer un rôle au principal de service</span><span class="sxs-lookup"><span data-stu-id="84af4-160">Assign role to service principal</span></span>
<span data-ttu-id="84af4-161">Pour accéder aux ressources de votre abonnement, vous devez affecter un rôle à l’application.</span><span class="sxs-lookup"><span data-stu-id="84af4-161">To access resources in your subscription, you must assign the application to a role.</span></span> <span data-ttu-id="84af4-162">Vous devez décider du rôle qui doit représenter les autorisations appropriées pour l’application.</span><span class="sxs-lookup"><span data-stu-id="84af4-162">Decide which role represents the right permissions for the application.</span></span> <span data-ttu-id="84af4-163">Pour en savoir plus sur les rôles disponibles, consultez [RBAC : rôles intégrés](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="84af4-163">To learn about the available roles, see [RBAC: Built in Roles](../active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="84af4-164">Vous pouvez définir l’étendue au niveau de l’abonnement, du groupe de ressources ou de la ressource.</span><span class="sxs-lookup"><span data-stu-id="84af4-164">You can set the scope at the level of the subscription, resource group, or resource.</span></span> <span data-ttu-id="84af4-165">Les autorisations sont héritées des niveaux inférieurs de l’étendue</span><span class="sxs-lookup"><span data-stu-id="84af4-165">Permissions are inherited to lower levels of scope.</span></span> <span data-ttu-id="84af4-166">(par exemple, l’ajout d’une application au rôle Lecteur pour un groupe de ressources signifie qu’elle peut lire le groupe de ressources et toutes les ressources qu’il contient).</span><span class="sxs-lookup"><span data-stu-id="84af4-166">For example, adding an application to the Reader role for a resource group means it can read the resource group and any resources it contains.</span></span>

1. <span data-ttu-id="84af4-167">Sur le portail Azure Stack, accédez au niveau d’étendue que vous souhaitez attribuer à l’application.</span><span class="sxs-lookup"><span data-stu-id="84af4-167">In the Azure Stack portal, navigate to the level of scope you wish to assign the application to.</span></span> <span data-ttu-id="84af4-168">Par exemple, pour affecter un rôle sur l’étendue de l’abonnement, sélectionnez **Abonnements**.</span><span class="sxs-lookup"><span data-stu-id="84af4-168">For example, to assign a role at the subscription scope, select **Subscriptions**.</span></span> <span data-ttu-id="84af4-169">Vous pouvez également sélectionner un groupe de ressources ou une ressource.</span><span class="sxs-lookup"><span data-stu-id="84af4-169">You could instead select a resource group or resource.</span></span>

2. <span data-ttu-id="84af4-170">Sélectionnez l’abonnement (groupe de ressources ou ressource) auquel l’application doit être affectée.</span><span class="sxs-lookup"><span data-stu-id="84af4-170">Select the particular subscription (resource group or resource) to assign the application to.</span></span>

     ![sélectionner l’abonnement pour l’affectation](./media/azure-stack-create-service-principal/image16.png)

3. <span data-ttu-id="84af4-172">Sélectionnez **Contrôle d’accès (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="84af4-172">Select **Access Control (IAM)**.</span></span>

     ![sélectionner l’accès](./media/azure-stack-create-service-principal/image17.png)

4. <span data-ttu-id="84af4-174">Sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="84af4-174">Select **Add**.</span></span>

5. <span data-ttu-id="84af4-175">Sélectionnez le rôle que vous souhaitez affecter à l’application.</span><span class="sxs-lookup"><span data-stu-id="84af4-175">Select the role you wish to assign to the application.</span></span>

6. <span data-ttu-id="84af4-176">Recherchez votre application et sélectionnez-la.</span><span class="sxs-lookup"><span data-stu-id="84af4-176">Search for your application, and select it.</span></span>

7. <span data-ttu-id="84af4-177">Sélectionnez **OK** pour finaliser l’affectation du rôle.</span><span class="sxs-lookup"><span data-stu-id="84af4-177">Select **OK** to finish assigning the role.</span></span> <span data-ttu-id="84af4-178">Votre application apparaît dans la liste des utilisateurs affectés à un rôle pour cette étendue.</span><span class="sxs-lookup"><span data-stu-id="84af4-178">You see your application in the list of users assigned to a role for that scope.</span></span>

<span data-ttu-id="84af4-179">Maintenant que vous avez créé un principal de service et que vous lui avez attribué un rôle, vous pouvez commencer à l’utiliser au sein de votre application pour accéder aux ressources Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="84af4-179">Now that you've created a service principal and assigned a role, you can begin using this within your application to access Azure Stack resources.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="84af4-180">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="84af4-180">Next steps</span></span>

<span data-ttu-id="84af4-181">[Ajouter des utilisateurs pour ADFS](azure-stack-add-users-adfs.md)
[Gérer les autorisations des utilisateurs](azure-stack-manage-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="84af4-181">[Add users for ADFS](azure-stack-add-users-adfs.md)
[Manage user permissions](azure-stack-manage-permissions.md)</span></span>