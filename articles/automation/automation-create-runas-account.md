---
title: "aaaCreate Azure Automation exécuter en tant que comptes | Documents Microsoft"
description: "Cet article décrit comment tooupdate votre automatisation compte et créez des comptes d’identification avec PowerShell ou depuis le portail de hello."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/27/2017
ms.author: magoedte
ms.openlocfilehash: 94eb54fa0b518056a726d17146c63411e248273b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-automation-account-authentication-with-run-as-accounts"></a><span data-ttu-id="b72b3-103">Mettre à jour l’authentification de votre compte Automation avec des comptes d’identification</span><span class="sxs-lookup"><span data-stu-id="b72b3-103">Update your Automation account authentication with Run As accounts</span></span> 
<span data-ttu-id="b72b3-104">Vous pouvez mettre à jour de votre compte Automation existant à partir du portail de hello ou utilisation de PowerShell si :</span><span class="sxs-lookup"><span data-stu-id="b72b3-104">You can update your existing Automation account from hello portal or use PowerShell if:</span></span>

* <span data-ttu-id="b72b3-105">Vous créez un compte Automation mais refusez toocreate hello exécuter en tant que compte.</span><span class="sxs-lookup"><span data-stu-id="b72b3-105">You create an Automation account but decline toocreate hello Run As account.</span></span>
* <span data-ttu-id="b72b3-106">Vous utilisez déjà une ressources de gestionnaire de ressources toomanage compte Automation et que vous souhaitez tooupdate hello tooinclude hello exécuter en tant que compte pour l’authentification de runbook.</span><span class="sxs-lookup"><span data-stu-id="b72b3-106">You already use an Automation account toomanage Resource Manager resources and you want tooupdate hello account tooinclude hello Run As account for runbook authentication.</span></span>
* <span data-ttu-id="b72b3-107">Vous utilisez déjà une Automation compte toomanage les ressources classiques et tooupdate il toouse hello classique compte d’identification au lieu de créer un compte et la migration de votre tooit runbooks et ressources.</span><span class="sxs-lookup"><span data-stu-id="b72b3-107">You already use an Automation account toomanage classic resources and you want tooupdate it toouse hello Classic Run As account instead of creating a new account and migrating your runbooks and assets tooit.</span></span>   
* <span data-ttu-id="b72b3-108">Vous souhaitez que toocreate une identification et classique compte d’identification à l’aide d’un certificat émis par votre autorité de certification d’entreprise (CA).</span><span class="sxs-lookup"><span data-stu-id="b72b3-108">You want toocreate a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b72b3-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b72b3-109">Prerequisites</span></span>

* <span data-ttu-id="b72b3-110">script de Hello peut être exécutée que sur Windows 10 et Windows Server 2016 avec des modules Azure Resource Manager 3.0.0 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="b72b3-110">hello script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 3.0.0 and later.</span></span> <span data-ttu-id="b72b3-111">Il n’est pas pris en charge dans les versions antérieures de Windows.</span><span class="sxs-lookup"><span data-stu-id="b72b3-111">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="b72b3-112">Azure PowerShell 1.0 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="b72b3-112">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="b72b3-113">Pour plus d’informations sur la mise en production hello PowerShell 1.0, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="b72b3-113">For information about hello PowerShell 1.0 release, see [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>
* <span data-ttu-id="b72b3-114">Un compte Automation, qui est référencé en tant que valeur hello pour hello *– AutomationAccountName* et *- ApplicationDisplayName* paramètres Bonjour suite du script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b72b3-114">An Automation account, which is referenced as hello value for hello *–AutomationAccountName* and *-ApplicationDisplayName* parameters in hello following PowerShell script.</span></span>

<span data-ttu-id="b72b3-115">les valeurs tooget hello pour *SubscriptionID*, *ResourceGroup*, et *AutomationAccountName*, qui sont des paramètres requis pour le script de hello, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="b72b3-115">tooget hello values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for hello script, do hello following:</span></span>

1. <span data-ttu-id="b72b3-116">Dans l’hello portail Azure, sélectionnez votre compte Automation sur hello **compte Automation** panneau, puis sélectionnez **tous les paramètres**.</span><span class="sxs-lookup"><span data-stu-id="b72b3-116">In hello Azure portal, select your Automation account on hello **Automation account** blade, and then select **All settings**.</span></span>  
2. <span data-ttu-id="b72b3-117">Sur hello **tous les paramètres** panneau, sous **les paramètres de compte**, sélectionnez **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="b72b3-117">On hello **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="b72b3-118">Notez les valeurs hello sur hello **propriétés** panneau.</span><span class="sxs-lookup"><span data-stu-id="b72b3-118">Note hello values on hello **Properties** blade.</span></span><br><br> <span data-ttu-id="b72b3-119">![Panneau de Hello Automation compte « Propriétés »](media/automation-create-runas-account/automation-account-properties.png)</span><span class="sxs-lookup"><span data-stu-id="b72b3-119">![hello Automation account "Properties" blade](media/automation-create-runas-account/automation-account-properties.png)</span></span>  

### <a name="required-permissions-tooupdate-your-automation-account"></a><span data-ttu-id="b72b3-120">Requis tooupdate d’autorisations de votre compte Automation</span><span class="sxs-lookup"><span data-stu-id="b72b3-120">Required permissions tooupdate your Automation account</span></span>
<span data-ttu-id="b72b3-121">tooupdate un compte Automation, vous devez avoir hello suivant des privilèges spécifiques et des autorisations requises toocomplete de cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="b72b3-121">tooupdate an Automation account, you must have hello following specific privileges and permissions required toocomplete this topic.</span></span>   
 
* <span data-ttu-id="b72b3-122">Votre compte d’utilisateur Active Directory doit être rôle tooa ajouté de toobe avec le rôle de collaborateur équivalent toohello autorisations pour les ressources Microsoft.Automation comme indiqué dans l’article [contrôle d’accès basé sur un rôle dans Azure Automation](automation-role-based-access-control.md#contributor-role-permissions).</span><span class="sxs-lookup"><span data-stu-id="b72b3-122">Your AD user account needs toobe added tooa role with permissions equivalent toohello Contributor role for Microsoft.Automation resources as outlined in article [Role-based access control in Azure Automation](automation-role-based-access-control.md#contributor-role-permissions).</span></span>  
* <span data-ttu-id="b72b3-123">Les utilisateurs non administrateurs dans votre locataire Azure AD peuvent [inscrire des applications AD](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions) si les inscriptions d’application hello paramètre est défini trop**Oui**.</span><span class="sxs-lookup"><span data-stu-id="b72b3-123">Non-admin users in your Azure AD tenant can [register AD applications](../azure-resource-manager/resource-group-create-service-principal-portal.md#check-azure-subscription-permissions) if hello App registrations setting is set too**Yes**.</span></span>  <span data-ttu-id="b72b3-124">Si les inscriptions d’application hello paramètre est défini trop**non**, utilisateur hello effectuer cette action doit être un administrateur global dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b72b3-124">If hello app registrations setting is set too**No**, hello user performing this action must be a global administrator in Azure AD.</span></span> 

<span data-ttu-id="b72b3-125">Si vous n’êtes pas un membre d’instance d’Active Directory de l’abonnement hello avant que vous êtes ajouté toohello global administrateur ou le co-administrateur rôle d’abonnement de hello, vous êtes ajouté tooActive active en tant qu’invité.</span><span class="sxs-lookup"><span data-stu-id="b72b3-125">If you are not a member of hello subscription’s Active Directory instance before you are added toohello global administrator/co-administrator role of hello subscription, you are added tooActive Directory as a guest.</span></span> <span data-ttu-id="b72b3-126">Dans ce cas, vous recevez un « vous n’avez pas toocreate autorisations... »</span><span class="sxs-lookup"><span data-stu-id="b72b3-126">In this situation, you receive a “You do not have permissions toocreate…”</span></span> <span data-ttu-id="b72b3-127">avertissement sur hello **ajouter un compte Automation** panneau.</span><span class="sxs-lookup"><span data-stu-id="b72b3-127">warning on hello **Add Automation Account** blade.</span></span> <span data-ttu-id="b72b3-128">Les utilisateurs qui ont été ajoutées toohello global administrateur ou le co-administrateur rôle tout d’abord peut être supprimé de l’instance d’Active Directory de l’abonnement hello et rajouté toomake les un utilisateur complète dans Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b72b3-128">Users who were added toohello global administrator/co-administrator role first can be removed from hello subscription's Active Directory instance and re-added toomake them a full User in Active Directory.</span></span> <span data-ttu-id="b72b3-129">tooverify cette situation, hello **Azure Active Directory** volet Bonjour portail Azure, sélectionnez **utilisateurs et groupes**, sélectionnez **tous les utilisateurs** et, après avoir sélectionné hello utilisateur spécifique, sélectionnez **profil**.</span><span class="sxs-lookup"><span data-stu-id="b72b3-129">tooverify this situation, from hello **Azure Active Directory** pane in hello Azure portal, select **Users and groups**, select **All users** and, after you select hello specific user, select **Profile**.</span></span> <span data-ttu-id="b72b3-130">Hello valeur Hello **type utilisateur** attribut sous le profil de l’utilisateur hello doit être **invité**.</span><span class="sxs-lookup"><span data-stu-id="b72b3-130">hello value of hello **User type** attribute under hello users profile should not equal **Guest**.</span></span>

## <a name="create-run-as-account-from-hello-portal"></a><span data-ttu-id="b72b3-131">Créer un compte d’identification à partir du portail de hello</span><span class="sxs-lookup"><span data-stu-id="b72b3-131">Create Run As account from hello portal</span></span>
<span data-ttu-id="b72b3-132">Dans cette section, effectuez hello suivant les étapes tooupdate votre compte Azure Automation hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b72b3-132">In this section, perform hello following steps tooupdate your Azure Automation account from  hello Azure portal.</span></span>  <span data-ttu-id="b72b3-133">Vous créez des comptes d’identification et Classic exécuter en tant que hello individuellement, et si vous n’avez pas besoin des ressources de toomanage dans le portail Azure classic de hello, vous pouvez simplement créer un compte d’identification Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b72b3-133">You create hello Run As and Classic Run As accounts individually, and if you don't need toomanage resources in hello classic Azure portal, you can just create hello Azure Run As account.</span></span>  

<span data-ttu-id="b72b3-134">processus de Hello crée hello éléments ci-après dans votre compte Automation.</span><span class="sxs-lookup"><span data-stu-id="b72b3-134">hello process creates hello following items in your Automation account.</span></span>

<span data-ttu-id="b72b3-135">**Pour les comptes d’identification :**</span><span class="sxs-lookup"><span data-stu-id="b72b3-135">**For Run As accounts:**</span></span>

* <span data-ttu-id="b72b3-136">Crée une application Azure AD avec un certificat auto-signé, crée un compte de principal du service pour l’application hello dans Azure AD et attribue le rôle de collaborateur hello compte hello dans votre abonnement actuel.</span><span class="sxs-lookup"><span data-stu-id="b72b3-136">Creates an Azure AD application with a self-signed certificate, creates a service principal account for hello application in Azure AD, and assigns hello Contributor role for hello account in your current subscription.</span></span> <span data-ttu-id="b72b3-137">Vous pouvez modifier ce paramètre tooOwner ou tout autre rôle.</span><span class="sxs-lookup"><span data-stu-id="b72b3-137">You can change this setting tooOwner or any other role.</span></span> <span data-ttu-id="b72b3-138">Pour plus d’informations, voir [Contrôle d’accès en fonction du rôle dans Azure Automation](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="b72b3-138">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="b72b3-139">Crée une ressource de certificat Automation nommée *AzureRunAsCertificate* Bonjour spécifié le compte Automation.</span><span class="sxs-lookup"><span data-stu-id="b72b3-139">Creates an Automation certificate asset named *AzureRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="b72b3-140">ressource de certificat Hello conserve la clé privée hello certificat utilisé par l’application hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b72b3-140">hello certificate asset holds hello certificate private key that's used by hello Azure AD application.</span></span>
* <span data-ttu-id="b72b3-141">Crée une ressource de connexion d’Automation nommée *AzureRunAsConnection* Bonjour spécifié le compte Automation.</span><span class="sxs-lookup"><span data-stu-id="b72b3-141">Creates an Automation connection asset named *AzureRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="b72b3-142">ressource de connexion Hello conserve hello applicationId, tenantId, ID d’abonnement et l’empreinte numérique du certificat.</span><span class="sxs-lookup"><span data-stu-id="b72b3-142">hello connection asset holds hello applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="b72b3-143">**Pour les comptes d’identification Classic :**</span><span class="sxs-lookup"><span data-stu-id="b72b3-143">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="b72b3-144">Crée une ressource de certificat Automation nommée *AzureClassicRunAsCertificate* Bonjour spécifié le compte Automation.</span><span class="sxs-lookup"><span data-stu-id="b72b3-144">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="b72b3-145">ressource de certificat Hello conserve la clé privée du certificat hello utilisé par le certificat de gestion hello.</span><span class="sxs-lookup"><span data-stu-id="b72b3-145">hello certificate asset holds hello certificate private key used by hello management certificate.</span></span>
* <span data-ttu-id="b72b3-146">Crée une ressource de connexion d’Automation nommée *AzureClassicRunAsConnection* Bonjour spécifié le compte Automation.</span><span class="sxs-lookup"><span data-stu-id="b72b3-146">Creates an Automation connection asset named *AzureClassicRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="b72b3-147">ressource de connexion Hello conserve hello abonnement nom, ID d’abonnement et nom de ressource de certificat.</span><span class="sxs-lookup"><span data-stu-id="b72b3-147">hello connection asset holds hello subscription name, subscriptionId, and certificate asset name.</span></span>

1. <span data-ttu-id="b72b3-148">Se connecter toohello portail Azure avec un compte qui est membre du rôle des administrateurs d’abonnements hello et coadministrateur de l’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="b72b3-148">Sign in toohello Azure portal with an account that is a member of hello Subscription Admins role and co-administrator of hello subscription.</span></span>
2. <span data-ttu-id="b72b3-149">Dans le panneau de compte Automation hello, sélectionnez **comptes d’identification** section hello **les paramètres de compte**.</span><span class="sxs-lookup"><span data-stu-id="b72b3-149">From hello Automation account blade, select **Run As Accounts** under hello section **Account Settings**.</span></span>  
3. <span data-ttu-id="b72b3-150">Selon le compte dont vous avez besoin, sélectionnez **Compte d’identification Azure** ou **Compte d’identification Azure Classic**.</span><span class="sxs-lookup"><span data-stu-id="b72b3-150">Depending on which account you require, select either **Azure Run As Account** or **Azure Classic Run As Account**.</span></span>  <span data-ttu-id="b72b3-151">Après avoir sélectionné soit hello **ajouter Azure exécuter en tant que** ou **ajouter Azure Classic compte d’identification** panneau s’affiche et après avoir examiné les informations de vue d’ensemble de hello, cliquez sur **créer** tooproceed avec exécuter en tant que la création du compte.</span><span class="sxs-lookup"><span data-stu-id="b72b3-151">After selecting either hello **Add Azure Run As** or **Add Azure Classic Run As Account** blade appears and after reviewing hello overview information, click **Create** tooproceed with Run As account creation.</span></span>  
4. <span data-ttu-id="b72b3-152">Alors que Azure crée le compte d’identification hello, vous pouvez suivre la progression de hello sous **Notifications** de hello menu et une bannière s’affiche indiquant hello compte doit être créé.</span><span class="sxs-lookup"><span data-stu-id="b72b3-152">While Azure creates hello Run As account, you can track hello progress under **Notifications** from hello menu and a banner is displayed stating hello account is being created.</span></span>  <span data-ttu-id="b72b3-153">Ce processus peut prendre quelques minutes toocomplete.</span><span class="sxs-lookup"><span data-stu-id="b72b3-153">This process can take a few minutes toocomplete.</span></span>  

## <a name="create-run-as-account-using-powershell-script"></a><span data-ttu-id="b72b3-154">Créer un compte d’identification à l’aide d’un script PowerShell</span><span class="sxs-lookup"><span data-stu-id="b72b3-154">Create Run As account using PowerShell script</span></span>
<span data-ttu-id="b72b3-155">Ce script PowerShell prend en charge hello suivant configurations :</span><span class="sxs-lookup"><span data-stu-id="b72b3-155">This PowerShell script includes support for hello following configurations:</span></span>

* <span data-ttu-id="b72b3-156">Créez un compte d’identification à l’aide d’un certificat auto-signé.</span><span class="sxs-lookup"><span data-stu-id="b72b3-156">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="b72b3-157">Créez un compte d’identification standard et un compte d’identification Classic à l’aide d’un certificat auto-signé.</span><span class="sxs-lookup"><span data-stu-id="b72b3-157">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="b72b3-158">Créez un compte d’identification standard et un compte d’identification Classic à l’aide d’un certificat d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="b72b3-158">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="b72b3-159">Créer un compte d’identification et classique compte d’identification à l’aide d’un certificat auto-signé Bonjour cloud d’Azure Government.</span><span class="sxs-lookup"><span data-stu-id="b72b3-159">Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud.</span></span>

<span data-ttu-id="b72b3-160">En fonction de l’option de configuration hello sélectionnée, le script de hello crée hello éléments suivants.</span><span class="sxs-lookup"><span data-stu-id="b72b3-160">Depending on hello configuration option you select, hello script creates hello following items.</span></span>

<span data-ttu-id="b72b3-161">**Pour les comptes d’identification :**</span><span class="sxs-lookup"><span data-stu-id="b72b3-161">**For Run As accounts:**</span></span>

* <span data-ttu-id="b72b3-162">Crée un Azure AD application toobe exporté avec soit hello auto-signé ou clé publique du certificat enterprise, crée un compte de principal du service pour l’application hello dans Azure AD, et assigne hello compte hello dans votre rôle de collaborateur abonnement.</span><span class="sxs-lookup"><span data-stu-id="b72b3-162">Creates an Azure AD application toobe exported with either hello self-signed or enterprise certificate public key, creates a service principal account for hello application in Azure AD, and assigns hello Contributor role for hello account in your current subscription.</span></span> <span data-ttu-id="b72b3-163">Vous pouvez modifier ce paramètre tooOwner ou tout autre rôle.</span><span class="sxs-lookup"><span data-stu-id="b72b3-163">You can change this setting tooOwner or any other role.</span></span> <span data-ttu-id="b72b3-164">Pour plus d’informations, voir [Contrôle d’accès en fonction du rôle dans Azure Automation](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="b72b3-164">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="b72b3-165">Crée une ressource de certificat Automation nommée *AzureRunAsCertificate* Bonjour spécifié le compte Automation.</span><span class="sxs-lookup"><span data-stu-id="b72b3-165">Creates an Automation certificate asset named *AzureRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="b72b3-166">ressource de certificat Hello conserve la clé privée hello certificat utilisé par l’application hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b72b3-166">hello certificate asset holds hello certificate private key that's used by hello Azure AD application.</span></span>
* <span data-ttu-id="b72b3-167">Crée une ressource de connexion d’Automation nommée *AzureRunAsConnection* Bonjour spécifié le compte Automation.</span><span class="sxs-lookup"><span data-stu-id="b72b3-167">Creates an Automation connection asset named *AzureRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="b72b3-168">ressource de connexion Hello conserve hello applicationId, tenantId, ID d’abonnement et l’empreinte numérique du certificat.</span><span class="sxs-lookup"><span data-stu-id="b72b3-168">hello connection asset holds hello applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="b72b3-169">**Pour les comptes d’identification Classic :**</span><span class="sxs-lookup"><span data-stu-id="b72b3-169">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="b72b3-170">Crée une ressource de certificat Automation nommée *AzureClassicRunAsCertificate* Bonjour spécifié le compte Automation.</span><span class="sxs-lookup"><span data-stu-id="b72b3-170">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="b72b3-171">ressource de certificat Hello conserve la clé privée du certificat hello utilisé par le certificat de gestion hello.</span><span class="sxs-lookup"><span data-stu-id="b72b3-171">hello certificate asset holds hello certificate private key used by hello management certificate.</span></span>
* <span data-ttu-id="b72b3-172">Crée une ressource de connexion d’Automation nommée *AzureClassicRunAsConnection* Bonjour spécifié le compte Automation.</span><span class="sxs-lookup"><span data-stu-id="b72b3-172">Creates an Automation connection asset named *AzureClassicRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="b72b3-173">ressource de connexion Hello conserve hello abonnement nom, ID d’abonnement et nom de ressource de certificat.</span><span class="sxs-lookup"><span data-stu-id="b72b3-173">hello connection asset holds hello subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="b72b3-174">Si vous sélectionnez l’option de création d’un compte classique exécuter en tant qu’après l’exécution de script de hello, téléchargement hello publique magasin de certificats de gestion de toohello (extension de nom de fichier .cer) pour l’abonnement de hello que hello compte Automation a été créé dans.</span><span class="sxs-lookup"><span data-stu-id="b72b3-174">If you select either option for creating a Classic Run As account, after hello script is executed, upload hello public certificate (.cer file name extension) toohello management store for hello subscription that hello Automation account was created in.</span></span>
> 

1. <span data-ttu-id="b72b3-175">Enregistrez hello script suivant sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="b72b3-175">Save hello following script on your computer.</span></span> <span data-ttu-id="b72b3-176">Dans cet exemple, enregistrez-le sous le nom de fichier hello *New-RunAsAccount.ps1*.</span><span class="sxs-lookup"><span data-stu-id="b72b3-176">In this example, save it with hello filename *New-RunAsAccount.ps1*.</span></span>

        #Requires -RunAsAdministrator
        Param (
        [Parameter(Mandatory=$true)]
        [String] $ResourceGroup,

        [Parameter(Mandatory=$true)]
        [String] $AutomationAccountName,

        [Parameter(Mandatory=$true)]
        [String] $ApplicationDisplayName,

        [Parameter(Mandatory=$true)]
        [String] $SubscriptionId,

        [Parameter(Mandatory=$true)]
        [Boolean] $CreateClassicRunAsAccount,

        [Parameter(Mandatory=$true)]
        [String] $SelfSignedCertPlainPassword,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$EnvironmentName="AzureCloud",

        [Parameter(Mandatory=$false)]
        [int] $SelfSignedCertNoOfMonthsUntilExpired = 12
        )

        function CreateSelfSignedCertificate([string] $keyVaultName, [string] $certificateName, [string] $selfSignedCertPlainPassword,
                                       [string] $certPath, [string] $certPathCer, [string] $selfSignedCertNoOfMonthsUntilExpired ) {
        $Cert = New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation cert:\LocalMachine\My `
            -KeyExportPolicy Exportable -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
            -NotAfter (Get-Date).AddMonths($selfSignedCertNoOfMonthsUntilExpired)

        $CertPassword = ConvertTo-SecureString $selfSignedCertPlainPassword -AsPlainText -Force
        Export-PfxCertificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPath -Password $CertPassword -Force | Write-Verbose
        Export-Certificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPathCer -Type CERT | Write-Verbose
        }

        function CreateServicePrincipal([System.Security.Cryptography.X509Certificates.X509Certificate2] $PfxCert, [string] $applicationDisplayName) {  
        $CurrentDate = Get-Date
        $keyValue = [System.Convert]::ToBase64String($PfxCert.GetRawCertData())
        $KeyId = (New-Guid).Guid

        $KeyCredential = New-Object  Microsoft.Azure.Commands.Resources.Models.ActiveDirectory.PSADKeyCredential
        $KeyCredential.StartDate = $CurrentDate
        $KeyCredential.EndDate = Get-Date $PfxCert.GetExpirationDateString()
        $KeyCredential.EndDate = $KeyCredential.EndDate.AddDays(-1)
        $KeyCredential.KeyId = $KeyId
        $KeyCredential.CertValue  = $keyValue

        # Use key credentials and create an Azure AD application
        $Application = New-AzureRmADApplication -DisplayName $ApplicationDisplayName -HomePage ("http://" + $applicationDisplayName) -IdentifierUris ("http://" + $KeyId) -KeyCredentials $KeyCredential
        $ServicePrincipal = New-AzureRMADServicePrincipal -ApplicationId $Application.ApplicationId
        $GetServicePrincipal = Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id

        # Sleep here for a few seconds tooallow hello service principal application toobecome active (ordinarily takes a few seconds)
        Sleep -s 15
        $NewRole = New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
        $Retries = 0;
        While ($NewRole -eq $null -and $Retries -le 6)
        {
            Sleep -s 10
            New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
            $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
            $Retries++;
        }
            return $Application.ApplicationId.ToString();
        }

        function CreateAutomationCertificateAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $certifcateAssetName,[string] $certPath, [string] $certPlainPassword, [Boolean] $Exportable) {
        $CertPassword = ConvertTo-SecureString $certPlainPassword -AsPlainText -Force   
        Remove-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $certifcateAssetName -ErrorAction SilentlyContinue
        New-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Path $certPath -Name $certifcateAssetName -Password $CertPassword -Exportable:$Exportable  | write-verbose
        }

        function CreateAutomationConnectionAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $connectionAssetName, [string] $connectionTypeName, [System.Collections.Hashtable] $connectionFieldValues ) {
        Remove-AzureRmAutomationConnection -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -Force -ErrorAction SilentlyContinue
        New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -ConnectionTypeName $connectionTypeName -ConnectionFieldValues $connectionFieldValues
        }

        Import-Module AzureRM.Profile
        Import-Module AzureRM.Resources

        $AzureRMProfileVersion= (Get-Module AzureRM.Profile).Version
        if (!(($AzureRMProfileVersion.Major -ge 3 -and $AzureRMProfileVersion.Minor -ge 0) -or ($AzureRMProfileVersion.Major -gt 3)))
        {
            Write-Error -Message "Please install hello latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
            return
        }

        Login-AzureRmAccount -Environment $EnvironmentName 
        $Subscription = Select-AzureRmSubscription -SubscriptionId $SubscriptionId

        # Create a Run As account by using a service principal
        $CertifcateAssetName = "AzureRunAsCertificate"
        $ConnectionAssetName = "AzureRunAsConnection"
        $ConnectionTypeName = "AzureServicePrincipal"

        if ($EnterpriseCertPathForRunAsAccount -and $EnterpriseCertPlainPasswordForRunAsAccount) {
        $PfxCertPathForRunAsAccount = $EnterpriseCertPathForRunAsAccount
        $PfxCertPlainPasswordForRunAsAccount = $EnterpriseCertPlainPasswordForRunAsAccount
        } else {
           $CertificateName = $AutomationAccountName+$CertifcateAssetName
           $PfxCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".pfx")
           $PfxCertPlainPasswordForRunAsAccount = $SelfSignedCertPlainPassword
           $CerCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".cer")
           CreateSelfSignedCertificate $KeyVaultName $CertificateName $PfxCertPlainPasswordForRunAsAccount $PfxCertPathForRunAsAccount $CerCertPathForRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create a service principal
        $PfxCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($PfxCertPathForRunAsAccount, $PfxCertPlainPasswordForRunAsAccount)
        $ApplicationId=CreateServicePrincipal $PfxCert $ApplicationDisplayName

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

        # Populate hello ConnectionFieldValues
        $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
        $TenantID = $SubscriptionInfo | Select TenantId -First 1
        $Thumbprint = $PfxCert.Thumbprint
        $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

        if ($CreateClassicRunAsAccount) {
             # Create a Run As account by using a service principal
             $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
             $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
             $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
             $UploadMessage = "Please upload hello .cer format of #CERT# toohello Management store by following hello steps below." + [Environment]::NewLine +
                     "Log in toohello Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                     "Then click Upload and upload hello .cer format of #CERT#"

              if ($EnterpriseCertPathForClassicRunAsAccount -and $EnterpriseCertPlainPasswordForClassicRunAsAccount ) {
              $PfxCertPathForClassicRunAsAccount = $EnterpriseCertPathForClassicRunAsAccount
              $PfxCertPlainPasswordForClassicRunAsAccount = $EnterpriseCertPlainPasswordForClassicRunAsAccount
              $UploadMessage = $UploadMessage.Replace("#CERT#", $PfxCertPathForClassicRunAsAccount)
        } else {
              $ClassicRunAsAccountCertificateName = $AutomationAccountName+$ClassicRunAsAccountCertifcateAssetName
              $PfxCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".pfx")
              $PfxCertPlainPasswordForClassicRunAsAccount = $SelfSignedCertPlainPassword
              $CerCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".cer")
              $UploadMessage = $UploadMessage.Replace("#CERT#", $CerCertPathForClassicRunAsAccount)
              CreateSelfSignedCertificate $KeyVaultName $ClassicRunAsAccountCertificateName $PfxCertPlainPasswordForClassicRunAsAccount $PfxCertPathForClassicRunAsAccount $CerCertPathForClassicRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate hello ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.Name
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="b72b3-177">Sur votre ordinateur, démarrez **Windows PowerShell** de hello **Démarrer** écran avec des droits utilisateur élevés.</span><span class="sxs-lookup"><span data-stu-id="b72b3-177">On your computer, start **Windows PowerShell** from hello **Start** screen with elevated user rights.</span></span>
3. <span data-ttu-id="b72b3-178">À partir de hello élevé interpréteur de commandes, accédez toohello dossier qui contient le script hello créé à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="b72b3-178">From hello elevated command-line shell, go toohello folder that contains hello script you created in step 1.</span></span>  
4. <span data-ttu-id="b72b3-179">Exécuter le script de hello à l’aide des valeurs de paramètre hello pour configuration hello que vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="b72b3-179">Execute hello script by using hello parameter values for hello configuration you require.</span></span>

    <span data-ttu-id="b72b3-180">**Créer un compte d’identification à l’aide d’un certificat auto-signé**</span><span class="sxs-lookup"><span data-stu-id="b72b3-180">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="b72b3-181">**Créer un compte d’identification standard et un compte d’identification Classic à l’aide d’un certificat auto-signé**</span><span class="sxs-lookup"><span data-stu-id="b72b3-181">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="b72b3-182">**Créer un compte d’identification standard et un compte d’identification Classic à l’aide d’un certificat d’entreprise**</span><span class="sxs-lookup"><span data-stu-id="b72b3-182">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="b72b3-183">**Créer un compte d’identification et classique compte d’identification à l’aide d’un certificat auto-signé Bonjour cloud d’Azure Government**</span><span class="sxs-lookup"><span data-stu-id="b72b3-183">**Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="b72b3-184">Après l’exécution de script de hello, vous serez invité à tooauthenticate avec Azure.</span><span class="sxs-lookup"><span data-stu-id="b72b3-184">After hello script has executed, you will be prompted tooauthenticate with Azure.</span></span> <span data-ttu-id="b72b3-185">Connectez-vous avec un compte qui est membre du rôle Administrateurs d’abonnement hello et coadministrateur de l’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="b72b3-185">Sign in with an account that is a member of hello subscription administrators role and co-administrator of hello subscription.</span></span>
    >
    >

<span data-ttu-id="b72b3-186">Une fois le script de hello a été exécutée correctement, notez hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="b72b3-186">After hello script has executed successfully, note hello following:</span></span>
* <span data-ttu-id="b72b3-187">Si vous avez créé un classique compte d’identification avec un certificat auto-signé de public (fichier .cer), le script de hello crée et enregistre toohello dossier des fichiers temporaires sur votre ordinateur sous le profil utilisateur hello *%USERPROFILE%\AppData\Local\Temp*, que vous avez utilisé la session de PowerShell tooexecute hello.</span><span class="sxs-lookup"><span data-stu-id="b72b3-187">If you created a Classic Run As account with a self-signed public certificate (.cer file), hello script creates and saves it toohello temporary files folder on your computer under hello user profile *%USERPROFILE%\AppData\Local\Temp*, which you used tooexecute hello PowerShell session.</span></span>
* <span data-ttu-id="b72b3-188">Si vous avez créé un compte d’identification Classic avec un certificat public d’entreprise (fichier .cer), utilisez ce certificat.</span><span class="sxs-lookup"><span data-stu-id="b72b3-188">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="b72b3-189">Suivez les instructions de hello pour [téléchargement un toohello de certificat d’API de gestion portail Azure classic](../azure-api-management-certs.md), puis validez de configuration des informations d’identification hello avec des ressources de déploiement classique à l’aide de hello [exemple de code tooauthenticate avec des ressources de déploiement classique Azure](automation-verify-runas-authentication.md#classic-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="b72b3-189">Follow hello instructions for [uploading a management API certificate toohello Azure classic portal](../azure-api-management-certs.md), and then validate hello credential configuration with classic deployment resources by using hello [sample code tooauthenticate with Azure Classic Deployment Resources](automation-verify-runas-authentication.md#classic-run-as-authentication).</span></span> 
* <span data-ttu-id="b72b3-190">Si vous l’avez fait *pas* créer classique compte d’identification, de s’authentifier auprès des ressources du Gestionnaire de ressources et de valider la configuration des informations d’identification hello à l’aide de hello [exemple de code pour s’authentifier auprès de gestion des services ressources](automation-verify-runas-authentication.md#automation-run-as-authentication).</span><span class="sxs-lookup"><span data-stu-id="b72b3-190">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate hello credential configuration by using hello [sample code for authenticating with Service Management resources](automation-verify-runas-authentication.md#automation-run-as-authentication).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b72b3-191">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b72b3-191">Next steps</span></span>
* <span data-ttu-id="b72b3-192">Pour plus d’informations sur les principaux de Service, voir la rubrique trop[les objets de Principal du Service et Application](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="b72b3-192">For more information about Service Principals, refer too[Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span>
* <span data-ttu-id="b72b3-193">Pour plus d’informations sur les certificats et les services Azure, consultez trop[vue d’ensemble des certificats pour les Services de Cloud Azure](../cloud-services/cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="b72b3-193">For more information about certificates and Azure services, refer too[Certificates overview for Azure Cloud Services](../cloud-services/cloud-services-certs-create.md).</span></span>
