---
title: "Configurer un compte d’authentification Azure | Microsoft Docs"
description: "Ce didacticiel vous guide tout au long des procédures de création et de test d’une authentification de principal de sécurité dans Azure Automation. Il est complété par un exemple d’utilisation."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
keywords: nom du principal du service, setspn, authentification azure
ms.assetid: 2f783441-15c7-4ea0-ba27-d7daa39b1dd3
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/06/2017
ms.author: magoedte
ROBOTS: NOINDEX
redirect_url: /azure/automation/
redirect_document_id: TRUE
ms.openlocfilehash: f88c775eba19bb227d0e206d6420c08b57305b92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-runbooks-with-an-azure-run-as-account"></a><span data-ttu-id="812ba-104">Authentifier des Runbooks avec un compte d’identification Azure</span><span class="sxs-lookup"><span data-stu-id="812ba-104">Authenticate runbooks with an Azure Run As account</span></span>
<span data-ttu-id="812ba-105">Cet article vous montre comment configurer un compte Azure Automation dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="812ba-105">This article shows you how to configure an Azure Automation account in the Azure portal.</span></span> <span data-ttu-id="812ba-106">Pour ce faire, utilisez la fonctionnalité Compte d’identification qui permet d’authentifier les Runbooks gérant les ressources dans Azure Resource Manager ou dans Azure Service Management.</span><span class="sxs-lookup"><span data-stu-id="812ba-106">To do so, you use the Run As account feature to authenticate runbooks managing resources in either Azure Resource Manager or Azure Service Management.</span></span>

<span data-ttu-id="812ba-107">Lorsque vous créez un compte Automation dans le portail Azure, il crée automatiquement 2 comptes :</span><span class="sxs-lookup"><span data-stu-id="812ba-107">When you create an Automation account in the Azure portal, you automatically create two accounts:</span></span>

* <span data-ttu-id="812ba-108">Compte d’identification Azure.</span><span class="sxs-lookup"><span data-stu-id="812ba-108">A Run As account.</span></span> <span data-ttu-id="812ba-109">Ce compte crée un principal de service dans Azure Active Directory (Azure AD) et un certificat.</span><span class="sxs-lookup"><span data-stu-id="812ba-109">This account creates a service principal in Azure Active Directory (Azure AD) and a certificate.</span></span> <span data-ttu-id="812ba-110">Il affecte également le rôle RBAC (contrôle d’accès en fonction du rôle) de contributeur qui gère les ressources Resource Manager à l’aide de Runbooks.</span><span class="sxs-lookup"><span data-stu-id="812ba-110">It also assigns the Contributor role-based access control (RBAC), which manages Resource Manager resources by using runbooks.</span></span>
* <span data-ttu-id="812ba-111">Compte d’identification Classic.</span><span class="sxs-lookup"><span data-stu-id="812ba-111">A Classic Run As account.</span></span> <span data-ttu-id="812ba-112">Ce compte charge un certificat de gestion, qui est utilisé pour gérer les ressources de gestion des services ou les ressources classiques à l’aide de Runbooks.</span><span class="sxs-lookup"><span data-stu-id="812ba-112">This account uploads a management certificate, which is used to manage Service Management or classic resources by using runbooks.</span></span>

<span data-ttu-id="812ba-113">Le processus de création d’un compte Automation s’en trouve ainsi simplifié, et vous êtes en mesure de commencer rapidement à générer et déployer des Runbooks pour répondre à vos besoins d’automatisation.</span><span class="sxs-lookup"><span data-stu-id="812ba-113">Creating an Automation account simplifies the process for you and helps you quickly start building and deploying runbooks to support your automation needs.</span></span>

<span data-ttu-id="812ba-114">À l’aide de comptes d’identification standard ou Classic, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="812ba-114">With Run As and Classic Run As accounts, you can:</span></span>

* <span data-ttu-id="812ba-115">Bénéficier d’une méthode d’authentification Azure standardisée lorsque vous gérez des ressources Resource Manager ou des ressources des services de gestion Azure à partir de Runbooks dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="812ba-115">Provide a standardized way to authenticate with Azure when you manage Resource Manager or Service Management resources from runbooks in the Azure portal.</span></span>
* <span data-ttu-id="812ba-116">Automatiser l’utilisation de Runbooks globaux que vous pouvez configurer dans les alertes Azure.</span><span class="sxs-lookup"><span data-stu-id="812ba-116">Automate the use of global runbooks, which you can configure in Azure Alerts.</span></span>

> [!NOTE]
> <span data-ttu-id="812ba-117">La [fonctionnalité d’intégration d’alertes](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) Azure associée aux Runbooks globaux requiert un compte Automation configuré avec un compte d’identification standard et un compte d’identification Classic.</span><span class="sxs-lookup"><span data-stu-id="812ba-117">The [Azure Alert integration feature](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) with Automation global runbooks requires an Automation account that's configured with a Run As account and a Classic Run As account.</span></span> <span data-ttu-id="812ba-118">Vous pouvez sélectionner un compte Automation pour lequel des comptes d’identification standard et Classic sont déjà définis ou choisir d’en créer un.</span><span class="sxs-lookup"><span data-stu-id="812ba-118">You can select an Automation account that already has defined Run As and Classic Run As accounts, or you can choose to create a new Automation account.</span></span>
>  

<span data-ttu-id="812ba-119">Cet article vous montre comment créer un compte Automation à partir du portail Azure, le mettre à jour à l’aide de PowerShell, gérer la configuration du compte et vous authentifier dans vos Runbooks.</span><span class="sxs-lookup"><span data-stu-id="812ba-119">This article shows how to create an Automation account from the Azure portal, update an Automation account by using Azure PowerShell, manage the account configuration, and authenticate in your runbooks.</span></span>

<span data-ttu-id="812ba-120">Avant de créer un compte Automation, il est judicieux de comprendre et de prendre en compte les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="812ba-120">Before you begin creating an Automation account, it's a good idea to understand and consider the following:</span></span>

* <span data-ttu-id="812ba-121">La création d’un compte Automation n’affecte pas les comptes Automation existants déjà créés dans le modèle de déploiement classique ou Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="812ba-121">Creating an Automation account does not affect Automation accounts you might have already created in either the classic or Resource Manager deployment model.</span></span>
* <span data-ttu-id="812ba-122">Cela fonctionne uniquement pour les comptes Automation créés via le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="812ba-122">The process works only for Automation accounts that you create in the Azure portal.</span></span> <span data-ttu-id="812ba-123">Si vous tentez de créer un compte à partir du portail Azure Classic, la configuration du compte d’identification n’est pas répliquée.</span><span class="sxs-lookup"><span data-stu-id="812ba-123">Attempting to create an account from the Azure classic portal does not replicate the Run As account configuration.</span></span>
* <span data-ttu-id="812ba-124">Si vous avez déjà des Runbooks et des ressources (telles que des planifications ou des variables) en place pour gérer les ressources classiques, et que vous souhaitez que les Runbooks s’authentifient auprès du nouveau compte d’identification Classic, effectuez l’une des actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="812ba-124">If you already have runbooks and assets (such as schedules or variables) in place to manage classic resources, and you want runbooks to authenticate with the new Classic Run As account, do either of the following:</span></span>

  * <span data-ttu-id="812ba-125">Pour créer un compte d’identification Classic, suivez les instructions de la section « Gestion de votre compte d’identification ».</span><span class="sxs-lookup"><span data-stu-id="812ba-125">To create a Classic Run As account, follow the instructions in the "Managing your Run As account" section.</span></span> 
  * <span data-ttu-id="812ba-126">Pour mettre à jour votre compte existant, utilisez le script PowerShell de la section « Mise à jour de votre compte Automation à l’aide de PowerShell ».</span><span class="sxs-lookup"><span data-stu-id="812ba-126">To update your existing account, use the PowerShell script in the "Update your Automation account by using PowerShell" section.</span></span>
* <span data-ttu-id="812ba-127">Pour vous authentifier à l’aide du nouveau compte d’identification ou du compte Automation d’identification Classic, vous devez modifier les Runbooks existants avec l’exemple de code indiqué dans la section [Exemples de code d’authentification](#authentication-code-examples).</span><span class="sxs-lookup"><span data-stu-id="812ba-127">To authenticate by using the new Run As account and Classic Run As Automation account, you  need to modify your existing runbooks with the example code provided in the section [Authentication code examples](#authentication-code-examples).</span></span>

    >[!NOTE]
    ><span data-ttu-id="812ba-128">Le compte d’identification sert à l’authentification des ressources Resource Manager à l’aide du principal de service basé sur les certificats.</span><span class="sxs-lookup"><span data-stu-id="812ba-128">The Run As account is for authentication against Resource Manager resources using the certificate-based service principal.</span></span> <span data-ttu-id="812ba-129">Le compte d’identification Classic sert à l’authentification des ressources de gestion des services avec un certificat de gestion.</span><span class="sxs-lookup"><span data-stu-id="812ba-129">The Classic Run As account is for authenticating against Service Management resources with a management certificate.</span></span>

## <a name="create-an-automation-account-from-the-azure-portal"></a><span data-ttu-id="812ba-130">Créer un compte Automation à partir du portail Azure</span><span class="sxs-lookup"><span data-stu-id="812ba-130">Create an Automation account from the Azure portal</span></span>
<span data-ttu-id="812ba-131">Dans cette section, vous créez un compte Azure Automation à partir du portail Azure, qui à son tour crée un compte d’identification standard et un compte d’identification Classic.</span><span class="sxs-lookup"><span data-stu-id="812ba-131">In this section, you create an Azure Automation account from the Azure portal, which in turn creates both a Run As account and a Classic Run As account.</span></span>

>[!NOTE]
><span data-ttu-id="812ba-132">Pour créer un compte Automation, vous devez posséder le rôle Administrateurs de services ou être coadministrateur de l’abonnement, ce qui permet d’accéder à l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="812ba-132">To create an Automation account, you must be a member of the Service Admins role or co-administrator of the subscription that is granting access to the subscription.</span></span> <span data-ttu-id="812ba-133">Vous devez également être ajouté en tant qu’utilisateur à l’instance Active Directory par défaut de cet abonnement.</span><span class="sxs-lookup"><span data-stu-id="812ba-133">You must also be added as a user to that subscription's default Active Directory instance.</span></span> <span data-ttu-id="812ba-134">Il n’est pas nécessaire d’attribuer au compte un rôle doté de privilèges.</span><span class="sxs-lookup"><span data-stu-id="812ba-134">The account does not need to be assigned a privileged role.</span></span>
>
><span data-ttu-id="812ba-135">Si vous n’êtes pas membre de l’instance d’Active Directory de l’abonnement au moment d’être ajouté au rôle Coadministrateur de l’abonnement, vous serez ajouté à Active Directory en tant qu’invité.</span><span class="sxs-lookup"><span data-stu-id="812ba-135">If you are not a member of the subscription’s Active Directory instance before you are added to the co-administrator role of the subscription, you will be added to Active Directory as a guest.</span></span> <span data-ttu-id="812ba-136">Dans ce cas, vous recevrez le message d’avertissement « Vous n’avez pas les autorisations pour créer... »</span><span class="sxs-lookup"><span data-stu-id="812ba-136">In this instance, you will receive a “You do not have permissions to create…”</span></span> <span data-ttu-id="812ba-137">dans le panneau **Ajouter un compte Automation**.</span><span class="sxs-lookup"><span data-stu-id="812ba-137">warning on the **Add Automation Account** blade.</span></span>
>
><span data-ttu-id="812ba-138">Les utilisateurs qui ont d’abord reçu le rôle Coadministrateur peuvent être supprimés de l’instance Active Directory de l’abonnement, puis rajoutés pour en faire des utilisateurs complets dans Active Directory.</span><span class="sxs-lookup"><span data-stu-id="812ba-138">Users who were added to the co-administrator role first can be removed from the subscription's Active Directory instance and re-added to make them a full User in Active Directory.</span></span> <span data-ttu-id="812ba-139">Pour vérifier si tel est le cas, dans le volet **Azure Active Directory** du portail Azure, sélectionnez **Utilisateurs et groupes** et **Tous les utilisateurs**, choisissez l’utilisateur concerné, puis sélectionnez **Profil**.</span><span class="sxs-lookup"><span data-stu-id="812ba-139">To verify this situation from the **Azure Active Directory** pane in the Azure portal by selecting **Users and groups**, selecting **All users** and, after you select the specific user, selecting **Profile**.</span></span> <span data-ttu-id="812ba-140">La valeur de l’attribut **Type d’utilisateur** sous le profil de l’utilisateur ne doit pas être **Invité**.</span><span class="sxs-lookup"><span data-stu-id="812ba-140">The value of the **User type** attribute under the users profile should not equal **Guest**.</span></span>
>

1. <span data-ttu-id="812ba-141">Connectez-vous au portail Azure avec un compte membre du rôle Administrateurs des abonnements et coadministrateur de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="812ba-141">Sign in to the Azure portal with an account that is a member of the subscription administrators role and co-administrator of the subscription.</span></span>

2. <span data-ttu-id="812ba-142">Sélectionnez **Comptes Automation**.</span><span class="sxs-lookup"><span data-stu-id="812ba-142">Select **Automation Accounts**.</span></span>

3. <span data-ttu-id="812ba-143">Dans le panneau **Comptes Automation**, cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="812ba-143">On the **Automation Accounts** blade, click **Add**.</span></span>
<span data-ttu-id="812ba-144">Le panneau **Ajouter un compte Automation** s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="812ba-144">The **Add Automation Account** blade opens.</span></span>

 ![Panneau « Ajouter un compte Automation »](media/automation-sec-configure-azure-runas-account/create-automation-account-properties-b.png)

   > [!NOTE]
   > <span data-ttu-id="812ba-146">Si votre compte n’est ni membre du rôle Administrateurs des abonnements ni coadministrateur de l’abonnement, l’avertissement suivant s’affiche dans le panneau **Ajouter un compte Automation** :</span><span class="sxs-lookup"><span data-stu-id="812ba-146">If your account is not a member of the subscription administrators role and co-administrator of the subscription, the following warning is displayed on the **Add Automation Account** blade:</span></span>
   >
   >![Avertissement Ajouter un compte Automation](media/automation-sec-configure-azure-runas-account/create-account-without-perms.png)
   >
   >

4. <span data-ttu-id="812ba-148">Dans le panneau **Ajouter un compte Automation**, entrez le nom de votre nouveau compte Automation dans la zone **Nom**.</span><span class="sxs-lookup"><span data-stu-id="812ba-148">On the **Add Automation Account** blade, in the **Name** box, type a name for your new Automation account.</span></span>

5. <span data-ttu-id="812ba-149">Si vous avez plusieurs abonnements, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="812ba-149">If you have more than one subscription, do the following:</span></span>

    <span data-ttu-id="812ba-150">a.</span><span class="sxs-lookup"><span data-stu-id="812ba-150">a.</span></span> <span data-ttu-id="812ba-151">Sous **Abonnement**, spécifiez-en un pour le nouveau compte.</span><span class="sxs-lookup"><span data-stu-id="812ba-151">Under **Subscription**, specify one for the new account.</span></span>

    <span data-ttu-id="812ba-152">b.</span><span class="sxs-lookup"><span data-stu-id="812ba-152">b.</span></span> <span data-ttu-id="812ba-153">Sous **Groupe de ressources**, cliquez sur **Créer** ou **Utiliser l’existant**.</span><span class="sxs-lookup"><span data-stu-id="812ba-153">Under **Resource Group**, click **Create new** or **Use existing**.</span></span>

    <span data-ttu-id="812ba-154">c.</span><span class="sxs-lookup"><span data-stu-id="812ba-154">c.</span></span> <span data-ttu-id="812ba-155">Sous **Emplacement**, indiquez un centre de données Azure.</span><span class="sxs-lookup"><span data-stu-id="812ba-155">Under **Location**, specify an Azure datacenter.</span></span>

6. <span data-ttu-id="812ba-156">Sous **Créer un compte d’identification Azure**, sélectionnez **Oui**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="812ba-156">Under **Create Azure Run As account**, select **Yes**, and then click **Create**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="812ba-157">Si vous choisissez de ne pas créer de compte d’identification en sélectionnant l’option **Non**, un message d’avertissement s’affiche dans le panneau **Ajouter un compte Automation**.</span><span class="sxs-lookup"><span data-stu-id="812ba-157">If you choose not to create the Run As account by selecting **No**, a warning message is displayed the **Add Automation Account** blade.</span></span> <span data-ttu-id="812ba-158">Même si le compte est créé dans le portail Azure, il n’aura pas d’identité d’authentification correspondante au sein de votre service de répertoire des abonnements classique ou Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="812ba-158">Although the account is created in the Azure portal, it does not have a corresponding authentication identity within your classic or Resource Manager subscription directory service.</span></span> <span data-ttu-id="812ba-159">Par conséquent, le compte n’a aucun accès aux ressources de votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="812ba-159">Consequently, the account has no access to resources in your subscription.</span></span> <span data-ttu-id="812ba-160">Ce scénario empêche tous les Runbooks faisant référence à ce compte de pouvoir s’authentifier et d’effectuer des tâches sur les ressources de ces modèles de déploiement.</span><span class="sxs-lookup"><span data-stu-id="812ba-160">This scenario prevents any runbooks that reference this account from authenticating and performing tasks against resources in those deployment models.</span></span>
   >
   > ![Message d’avertissement dans le panneau « Ajouter un compte Automation »](media/automation-sec-configure-azure-runas-account/create-account-decline-create-runas-msg.png)
   >
   > <span data-ttu-id="812ba-162">En outre, étant donné que le principal du service n’est pas créé, le rôle Collaborateur n’est pas attribué.</span><span class="sxs-lookup"><span data-stu-id="812ba-162">Additionally, because the service principal is not created, the Contributor role is not assigned.</span></span>
   >

7. <span data-ttu-id="812ba-163">Pour suivre la progression de la création du compte Automation, accédez à l’onglet **Notifications** du menu.</span><span class="sxs-lookup"><span data-stu-id="812ba-163">While Azure creates the Automation account, you can track the progress under **Notifications** from the menu.</span></span>

### <a name="resources"></a><span data-ttu-id="812ba-164">les ressources</span><span class="sxs-lookup"><span data-stu-id="812ba-164">Resources</span></span>
<span data-ttu-id="812ba-165">Une fois le compte Automation créé, plusieurs ressources vous sont automatiquement créées.</span><span class="sxs-lookup"><span data-stu-id="812ba-165">When the Automation account is successfully created, several resources are automatically created for you.</span></span> <span data-ttu-id="812ba-166">Les ressources sont récapitulées dans les 2 tableaux ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="812ba-166">The resources are summarized in the following two tables:</span></span>

#### <a name="run-as-account-resources"></a><span data-ttu-id="812ba-167">Ressources de compte d’identification</span><span class="sxs-lookup"><span data-stu-id="812ba-167">Run As account resources</span></span>

| <span data-ttu-id="812ba-168">Ressource</span><span class="sxs-lookup"><span data-stu-id="812ba-168">Resource</span></span> | <span data-ttu-id="812ba-169">Description</span><span class="sxs-lookup"><span data-stu-id="812ba-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="812ba-170">Runbook AzureAutomationTutorial</span><span class="sxs-lookup"><span data-stu-id="812ba-170">AzureAutomationTutorial Runbook</span></span> | <span data-ttu-id="812ba-171">Exemple de Runbook Graphical qui illustre l’authentification à l’aide du compte d’identification et l’accès à l’ensemble des ressources Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="812ba-171">An example graphical runbook that demonstrates how to authenticate by using the Run As account and gets all the Resource Manager resources.</span></span> |
| <span data-ttu-id="812ba-172">Runbook AzureAutomationTutorialScript</span><span class="sxs-lookup"><span data-stu-id="812ba-172">AzureAutomationTutorialScript Runbook</span></span> | <span data-ttu-id="812ba-173">Exemple de Runbook PowerShell qui illustre l’authentification à l’aide du compte d’identification et l’accès à l’ensemble des ressources Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="812ba-173">An example PowerShell runbook that demonstrates how to authenticate by using the Run As account and gets all the Resource Manager resources.</span></span> |
| <span data-ttu-id="812ba-174">AzureRunAsCertificate</span><span class="sxs-lookup"><span data-stu-id="812ba-174">AzureRunAsCertificate</span></span> | <span data-ttu-id="812ba-175">La ressource de certificat créée automatiquement lors de la création du compte Automation ou à l’aide du script PowerShell ci-dessous pour un compte existant.</span><span class="sxs-lookup"><span data-stu-id="812ba-175">The certificate asset that's automatically created when you create an Automation account or use the following PowerShell script for an existing account.</span></span> <span data-ttu-id="812ba-176">Le certificat permet de vous authentifier auprès d’Azure afin de pouvoir gérer les ressources Azure Resource Manager des Runbooks.</span><span class="sxs-lookup"><span data-stu-id="812ba-176">The certificate allows you to authenticate with Azure so that you can manage Azure Resource Manager resources from runbooks.</span></span> <span data-ttu-id="812ba-177">Ce certificat a une durée de vie d’1 an.</span><span class="sxs-lookup"><span data-stu-id="812ba-177">The certificate has a one-year lifespan.</span></span> |
| <span data-ttu-id="812ba-178">AzureRunAsConnection</span><span class="sxs-lookup"><span data-stu-id="812ba-178">AzureRunAsConnection</span></span> | <span data-ttu-id="812ba-179">La ressource de connexion créée automatiquement lors de la création du compte Automation ou à l’aide du script PowerShell pour un compte existant.</span><span class="sxs-lookup"><span data-stu-id="812ba-179">The connection asset that's automatically created when you create an Automation account or use the PowerShell script for an existing account.</span></span> |

#### <a name="classic-run-as-account-resources"></a><span data-ttu-id="812ba-180">Ressources de compte d’identification Classic</span><span class="sxs-lookup"><span data-stu-id="812ba-180">Classic Run As account resources</span></span>

| <span data-ttu-id="812ba-181">Ressource</span><span class="sxs-lookup"><span data-stu-id="812ba-181">Resource</span></span> | <span data-ttu-id="812ba-182">Description</span><span class="sxs-lookup"><span data-stu-id="812ba-182">Description</span></span> |
| --- | --- |
| <span data-ttu-id="812ba-183">Runbook AzureClassicAutomationTutorial</span><span class="sxs-lookup"><span data-stu-id="812ba-183">AzureClassicAutomationTutorial Runbook</span></span> | <span data-ttu-id="812ba-184">Exemple de Runbook Graphical qui accède à toutes les machines virtuelles créées sur le modèle de déploiement classique dans un abonnement à l’aide du compte d’identification Classic (certificat), puis indique leur nom et état.</span><span class="sxs-lookup"><span data-stu-id="812ba-184">An example graphical runbook that gets all the VMs that are created using the classic deployment model in a subscription by using the Classic Run As account (certificate), and then writes the VM name and status.</span></span> |
| <span data-ttu-id="812ba-185">Runbook AzureClassicAutomationTutorialScript</span><span class="sxs-lookup"><span data-stu-id="812ba-185">AzureClassicAutomationTutorial Script Runbook</span></span> | <span data-ttu-id="812ba-186">Exemple de Runbook PowerShell qui accède à toutes les machines virtuelles Classic d’un abonnement à l’aide du compte d’identification Classic (certificat), puis écrit leur nom et leur état.</span><span class="sxs-lookup"><span data-stu-id="812ba-186">An example PowerShell runbook that gets all the classic VMs in a subscription by using the Classic Run As account (certificate), and then writes the VM name and status.</span></span> |
| <span data-ttu-id="812ba-187">AzureClassicRunAsCertificate</span><span class="sxs-lookup"><span data-stu-id="812ba-187">AzureClassicRunAsCertificate</span></span> | <span data-ttu-id="812ba-188">Ressource de certificat créée automatiquement et utilisée pour l’authentification auprès d’Azure afin que vous puissiez gérer les ressources Azure Classic des Runbooks.</span><span class="sxs-lookup"><span data-stu-id="812ba-188">The automatically created certificate asset that you use to authenticate with Azure so that you can manage Azure classic resources from runbooks.</span></span> <span data-ttu-id="812ba-189">Ce certificat a une durée de vie d’1 an.</span><span class="sxs-lookup"><span data-stu-id="812ba-189">The certificate has a one-year lifespan.</span></span> |
| <span data-ttu-id="812ba-190">AzureClassicRunAsConnection</span><span class="sxs-lookup"><span data-stu-id="812ba-190">AzureClassicRunAsConnection</span></span> | <span data-ttu-id="812ba-191">Ressource de connexion créée automatiquement et utilisée pour l’authentification auprès d’Azure afin que vous puissiez gérer les ressources Azure Classic des Runbooks.</span><span class="sxs-lookup"><span data-stu-id="812ba-191">The automatically created connection asset that you use to authenticate with Azure so that you can manage Azure classic resources from runbooks.</span></span> |

## <a name="verify-run-as-authentication"></a><span data-ttu-id="812ba-192">Vérifier l’authentification d’identification</span><span class="sxs-lookup"><span data-stu-id="812ba-192">Verify Run As authentication</span></span>
<span data-ttu-id="812ba-193">Effectuez un test rapide afin de vérifier que vous êtes en mesure de vous authentifier à l’aide du nouveau compte d’identification.</span><span class="sxs-lookup"><span data-stu-id="812ba-193">Perform a small test to confirm that you can successfully authenticate by using the new Run As account.</span></span>

1. <span data-ttu-id="812ba-194">Dans le portail Azure, ouvrez le compte Automation que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="812ba-194">In the Azure portal, open the Automation account that you created earlier.</span></span>

2. <span data-ttu-id="812ba-195">Cliquez sur la vignette **Runbooks** pour ouvrir la liste des runbooks.</span><span class="sxs-lookup"><span data-stu-id="812ba-195">Click the **Runbooks** tile to open the list of runbooks.</span></span>

3. <span data-ttu-id="812ba-196">Sélectionnez le Runbook **AzureAutomationTutorialScript**, puis cliquez sur **Démarrer** pour le lancer.</span><span class="sxs-lookup"><span data-stu-id="812ba-196">Select the **AzureAutomationTutorialScript** runbook, and then click **Start** to start the runbook.</span></span> <span data-ttu-id="812ba-197">Les événements suivants se produisent :</span><span class="sxs-lookup"><span data-stu-id="812ba-197">The following events occur:</span></span>
 * <span data-ttu-id="812ba-198">Un [travail du Runbook](automation-runbook-execution.md) est créé. Le panneau **Travail** s’affiche alors et l’état du travail est affiché dans la mosaïque **Résumé du travail**.</span><span class="sxs-lookup"><span data-stu-id="812ba-198">A [runbook job](automation-runbook-execution.md) is created, the **Job** blade is displayed, and the job status is displayed in the **Job Summary** tile.</span></span>
 * <span data-ttu-id="812ba-199">L’état initial du travail est **Mis en file d’attente** pour indiquer qu’il attend la disponibilité d’un Runbook Worker dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="812ba-199">The job status begins as **Queued**, indicating that it is waiting for a runbook worker in the cloud to become available.</span></span>
 * <span data-ttu-id="812ba-200">L’état passe ensuite à **Démarrage en cours** lorsqu’un Worker sélectionne le travail.</span><span class="sxs-lookup"><span data-stu-id="812ba-200">The status becomes **Starting** when a worker claims the job.</span></span>
 * <span data-ttu-id="812ba-201">L’état passe à **En cours d’exécution** lorsque le Runbook commence à s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="812ba-201">The status becomes **Running** when the runbook starts running.</span></span>
 * <span data-ttu-id="812ba-202">Lorsque le travail de Runbook a fini de s’exécuter,l’état est **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="812ba-202">When the runbook job has finished running, you should see a status of **Completed**.</span></span>

       ![Security Principal Runbook Test](media/automation-sec-configure-azure-runas-account/job-summary-automationtutorialscript.png)
4. <span data-ttu-id="812ba-203">Pour afficher les résultats détaillés du Runbook, cliquez sur la mosaïque **Sortie**.</span><span class="sxs-lookup"><span data-stu-id="812ba-203">To see the detailed results of the runbook, click the **Output** tile.</span></span>  
<span data-ttu-id="812ba-204">Le panneau **Sortie** est affiché, indiquant que le Runbook a authentifié et retourné la liste de toutes les ressources disponibles dans le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="812ba-204">The **Output** blade is displayed, showing that the runbook has successfully authenticated and returned a list of all resources available in the resource group.</span></span>

5. <span data-ttu-id="812ba-205">Fermez le panneau **Sortie** pour revenir au panneau **Résumé du travail**.</span><span class="sxs-lookup"><span data-stu-id="812ba-205">Close the **Output** blade to return to the **Job Summary** blade.</span></span>

6. <span data-ttu-id="812ba-206">Fermez le panneau **Résumé du travail** et le panneau du Runbook **AzureAutomationTutorialScript** correspondant.</span><span class="sxs-lookup"><span data-stu-id="812ba-206">Close the **Job Summary** blade and the corresponding **AzureAutomationTutorialScript** runbook blade.</span></span>

## <a name="verify-classic-run-as-authentication"></a><span data-ttu-id="812ba-207">Vérifier l’authentification d’identification Classic</span><span class="sxs-lookup"><span data-stu-id="812ba-207">Verify Classic Run As authentication</span></span>
<span data-ttu-id="812ba-208">Effectuez un test rapide similaire afin de vérifier que vous êtes en mesure de vous authentifier à l’aide du nouveau compte d’identification Classic.</span><span class="sxs-lookup"><span data-stu-id="812ba-208">Perform a similar small test to confirm that you can successfully authenticate by using the new Classic Run As account.</span></span>

1. <span data-ttu-id="812ba-209">Dans le portail Azure, ouvrez le compte Automation que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="812ba-209">In the Azure portal, open the Automation account that you created earlier.</span></span>

2. <span data-ttu-id="812ba-210">Cliquez sur la vignette **Runbooks** pour ouvrir la liste des runbooks.</span><span class="sxs-lookup"><span data-stu-id="812ba-210">Click the **Runbooks** tile to open the list of runbooks.</span></span>

3. <span data-ttu-id="812ba-211">Sélectionnez le Runbook **AzureClassicAutomationTutorialScript**, puis cliquez sur **Démarrer** pour le lancer.</span><span class="sxs-lookup"><span data-stu-id="812ba-211">Select the **AzureClassicAutomationTutorialScript** runbook, and then click **Start** to  start the runbook.</span></span> <span data-ttu-id="812ba-212">Les événements suivants se produisent :</span><span class="sxs-lookup"><span data-stu-id="812ba-212">The following events occur:</span></span>

 * <span data-ttu-id="812ba-213">Un [travail du Runbook](automation-runbook-execution.md) est créé. Le panneau **Travail** s’affiche alors et l’état du travail est affiché dans la mosaïque **Résumé du travail**.</span><span class="sxs-lookup"><span data-stu-id="812ba-213">A [runbook job](automation-runbook-execution.md) is created, the **Job** blade is displayed, and the job status is displayed in the **Job Summary** tile.</span></span>
 * <span data-ttu-id="812ba-214">L’état initial du travail est **Mis en file d’attente** pour indiquer qu’il attend la disponibilité d’un Runbook Worker dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="812ba-214">The job status begins as **Queued**, indicating that it is waiting for a runbook worker in the cloud to become available.</span></span>
 * <span data-ttu-id="812ba-215">L’état passe ensuite à **Démarrage en cours** lorsqu’un Worker sélectionne le travail.</span><span class="sxs-lookup"><span data-stu-id="812ba-215">The status becomes **Starting** when a worker claims the job.</span></span>
 * <span data-ttu-id="812ba-216">L’état passe à **En cours d’exécution** lorsque le Runbook commence à s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="812ba-216">The status becomes **Running** when the runbook starts running.</span></span>
 * <span data-ttu-id="812ba-217">Lorsque le travail de Runbook a fini de s’exécuter, l’état est **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="812ba-217">When the runbook job has finished running, you should see a status of **Completed**.</span></span>

    ![Test de Runbook du principal de sécurité](media/automation-sec-configure-azure-runas-account/job-summary-automationclassictutorialscript.png)<br>
4. <span data-ttu-id="812ba-219">Pour afficher les résultats détaillés du Runbook, cliquez sur la mosaïque **Sortie**.</span><span class="sxs-lookup"><span data-stu-id="812ba-219">To see the detailed results of the runbook, click the **Output** tile.</span></span>  
<span data-ttu-id="812ba-220">Le panneau **Sortie** est affiché, indiquant que le Runbook a authentifié et retourné la liste de toutes les machines virtuelles Classic de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="812ba-220">The **Output** blade is displayed, showing that the runbook has successfully authenticated and returned a list of all classic VMs in the subscription.</span></span>

5. <span data-ttu-id="812ba-221">Fermez le panneau **Sortie** pour revenir au panneau **Résumé du travail**.</span><span class="sxs-lookup"><span data-stu-id="812ba-221">Close the **Output** blade to return to the **Job Summary** blade.</span></span>

6. <span data-ttu-id="812ba-222">Fermez le panneau **Résumé du travail** et le panneau du Runbook **AzureAutomationTutorialScript** correspondant.</span><span class="sxs-lookup"><span data-stu-id="812ba-222">Close the **Job Summary** blade and the corresponding **AzureAutomationTutorialScript** runbook blade.</span></span>

## <a name="managing-your-run-as-account"></a><span data-ttu-id="812ba-223">Gestion de votre compte d’identification</span><span class="sxs-lookup"><span data-stu-id="812ba-223">Managing your Run As account</span></span>
<span data-ttu-id="812ba-224">Avant que votre compte Automation n’expire, vous devez renouveler le certificat.</span><span class="sxs-lookup"><span data-stu-id="812ba-224">At some point before your Automation account expires, you will need to renew the certificate.</span></span> <span data-ttu-id="812ba-225">Si vous pensez que le compte d’identification a été compromis, vous pouvez le supprimer et le recréer.</span><span class="sxs-lookup"><span data-stu-id="812ba-225">If you believe that the Run As account has been compromised, you can delete and re-create it.</span></span> <span data-ttu-id="812ba-226">Cette section décrit comment effectuer ces opérations.</span><span class="sxs-lookup"><span data-stu-id="812ba-226">This section discusses how to perform these operations.</span></span>

### <a name="self-signed-certificate-renewal"></a><span data-ttu-id="812ba-227">Renouvellement de certificat auto-signé</span><span class="sxs-lookup"><span data-stu-id="812ba-227">Self-signed certificate renewal</span></span>
<span data-ttu-id="812ba-228">Le certificat auto-signé que vous avez créé pour le compte d’identification expire 1 an après la date de création.</span><span class="sxs-lookup"><span data-stu-id="812ba-228">The self-signed certificate that you created for the Run As account expires one year from the date of creation.</span></span> <span data-ttu-id="812ba-229">Vous pouvez le renouveler à tout moment avant qu’il n’expire.</span><span class="sxs-lookup"><span data-stu-id="812ba-229">You can renew it at any time before it expires.</span></span> <span data-ttu-id="812ba-230">Lorsque vous le renouvelez, le certificat valide en cours est conservé afin de garantir que les Runbooks en file d’attente ou en cours d’exécution, qui s’authentifient avec le compte d’identification, ne sont pas affectés.</span><span class="sxs-lookup"><span data-stu-id="812ba-230">When you renew it, the current valid certificate is retained to ensure that any runbooks that are queued up or actively running, and that authenticate with the Run As account, are not negatively affected.</span></span> <span data-ttu-id="812ba-231">Le certificat reste valide jusqu’à sa date d’expiration.</span><span class="sxs-lookup"><span data-stu-id="812ba-231">The certificate remains valid until its expiration date.</span></span>

> [!NOTE]
> <span data-ttu-id="812ba-232">Si vous avez configuré votre compte d’identification Automation pour utiliser un certificat émis par votre autorité de certification d’entreprise et que vous utilisez cette option, ce certificat sera remplacé par un certificat auto-signé.</span><span class="sxs-lookup"><span data-stu-id="812ba-232">If you have configured your Automation Run As account to use a certificate issued by your enterprise certificate authority and you use this option, the enterprise certificate will be replaced by a self-signed certificate.</span></span>

<span data-ttu-id="812ba-233">Pour renouveler le certificat, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="812ba-233">To renew the certificate, do the following:</span></span>

1. <span data-ttu-id="812ba-234">Dans le portail Azure, ouvrez le compte Automation.</span><span class="sxs-lookup"><span data-stu-id="812ba-234">In the Azure portal, open the Automation account.</span></span>

2. <span data-ttu-id="812ba-235">Dans le panneau **Compte Automation**, dans le volet **Propriétés du compte**, sous **Paramètres du compte**, sélectionnez **Comptes d’identification**.</span><span class="sxs-lookup"><span data-stu-id="812ba-235">On the **Automation Account** blade, in the **Account properties** pane, under **Account Settings**, select **Run As Accounts**.</span></span>

    ![Panneau des propriétés du compte Automation](media/automation-sec-configure-azure-runas-account/automation-account-properties-pane.png)
3. <span data-ttu-id="812ba-237">Dans le panneau des propriétés des **Comptes d’identification**, sélectionnez le compte d’identification standard ou le compte d’identification Classic pour lequel vous souhaitez renouveler le certificat.</span><span class="sxs-lookup"><span data-stu-id="812ba-237">On the **Run As Accounts** properties blade, select either the Run As account or the Classic Run As account that you want to renew the certificate for.</span></span>

4. <span data-ttu-id="812ba-238">Sur le panneau **Propriétés** du compte sélectionné, cliquez sur **Renouveler le certificat**.</span><span class="sxs-lookup"><span data-stu-id="812ba-238">On the **Properties** blade for the selected account, click **Renew certificate**.</span></span>

    ![Renouveler le certificat pour le compte d’identification](media/automation-sec-configure-azure-runas-account/automation-account-renew-runas-certificate.png)

5. <span data-ttu-id="812ba-240">Pour suivre la progression du renouvellement du certificat, accédez à l’onglet **Notifications** du menu.</span><span class="sxs-lookup"><span data-stu-id="812ba-240">While the certificate is being renewed, you can track the progress under **Notifications** from the menu.</span></span>

### <a name="delete-a-run-as-or-classic-run-as-account"></a><span data-ttu-id="812ba-241">Supprimer un compte d’identification standard ou Classic</span><span class="sxs-lookup"><span data-stu-id="812ba-241">Delete a Run As or Classic Run As account</span></span>
<span data-ttu-id="812ba-242">Cette section décrit comment supprimer et recréer votre compte d’identification standard ou Classic.</span><span class="sxs-lookup"><span data-stu-id="812ba-242">This section describes how to delete and re-create a Run As or Classic Run As account.</span></span> <span data-ttu-id="812ba-243">Lorsque vous effectuez cette opération, le compte Automation est conservé.</span><span class="sxs-lookup"><span data-stu-id="812ba-243">When you perform this action, the Automation account is retained.</span></span> <span data-ttu-id="812ba-244">Après avoir supprimé le compte d’identification standard ou le compte d’identification Classic, vous pouvez le recréer dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="812ba-244">After you delete a Run As or Classic Run As account, you can re-create it in the Azure portal.</span></span>

1. <span data-ttu-id="812ba-245">Dans le portail Azure, ouvrez le compte Automation.</span><span class="sxs-lookup"><span data-stu-id="812ba-245">In the Azure portal, open the Automation account.</span></span>

2. <span data-ttu-id="812ba-246">Dans le panneau **Compte Automation**, dans le volet des propriétés du compte, sélectionnez **Comptes d’identification**.</span><span class="sxs-lookup"><span data-stu-id="812ba-246">On the **Automation account** blade, in the account properties pane, select **Run As Accounts**.</span></span>

3. <span data-ttu-id="812ba-247">Dans le panneau des propriétés des **Comptes d’identification**, sélectionnez le compte d’identification standard ou le compte d’identification Classic que vous voulez supprimer.</span><span class="sxs-lookup"><span data-stu-id="812ba-247">On the **Run As Accounts** properties blade, select either the Run As account or Classic Run As account that you want to delete.</span></span> <span data-ttu-id="812ba-248">Ensuite, dans le panneau **Propriétés** du compte sélectionné, cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="812ba-248">Then, on the **Properties** blade for the selected account, click **Delete**.</span></span>

 ![Supprimer un compte d’identification](media/automation-sec-configure-azure-runas-account/automation-account-delete-runas.png)

4. <span data-ttu-id="812ba-250">Pour suivre la progression de la suppression du compte, accédez à l’onglet **Notifications** du menu.</span><span class="sxs-lookup"><span data-stu-id="812ba-250">While the account is being deleted, you can track the progress under **Notifications** from the menu.</span></span>

5. <span data-ttu-id="812ba-251">Une fois le compte supprimé, vous pouvez le recréer sur le panneau des propriétés **Comptes d’identification** en sélectionnant l’option de création **Compte d’identification Azure**.</span><span class="sxs-lookup"><span data-stu-id="812ba-251">After the account has been deleted, you can re-create it on the **Run As Accounts** properties blade by selecting the create option **Azure Run As Account**.</span></span>

 ![Recréer le compte d’identification Automation](media/automation-sec-configure-azure-runas-account/automation-account-create-runas.png)

### <a name="misconfiguration"></a><span data-ttu-id="812ba-253">Configuration incorrecte</span><span class="sxs-lookup"><span data-stu-id="812ba-253">Misconfiguration</span></span>
<span data-ttu-id="812ba-254">Certains éléments de configuration nécessaires pour que le compte d’identification standard ou le compte d’identification Classic fonctionne correctement ont peut-être été supprimés ou n’ont pas été créés correctement lors de l’installation initiale.</span><span class="sxs-lookup"><span data-stu-id="812ba-254">Some configuration items necessary for the Run As or Classic Run As account to function properly might have been deleted or created improperly during initial setup.</span></span> <span data-ttu-id="812ba-255">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="812ba-255">The items include:</span></span>

* <span data-ttu-id="812ba-256">Ressource de certificat</span><span class="sxs-lookup"><span data-stu-id="812ba-256">Certificate asset</span></span>
* <span data-ttu-id="812ba-257">Ressource de connexion</span><span class="sxs-lookup"><span data-stu-id="812ba-257">Connection asset</span></span>
* <span data-ttu-id="812ba-258">Compte d’identification supprimé du rôle Contributeur</span><span class="sxs-lookup"><span data-stu-id="812ba-258">Run As account has been removed from the contributor role</span></span>
* <span data-ttu-id="812ba-259">Principal du service ou application dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="812ba-259">Service principal or application in Azure AD</span></span>

<span data-ttu-id="812ba-260">Dans les cas précédents et dans d’autres instances de configuration incorrecte, le compte Automation détecte les modifications et affiche l’état *Incomplet* dans le panneau des propriétés **Comptes d’identification** du compte.</span><span class="sxs-lookup"><span data-stu-id="812ba-260">In the preceding and other instances of misconfiguration, the Automation account detects the changes and displays a status of *Incomplete* on the **Run As Accounts** properties blade for the account.</span></span>

![État Incomplet pour la configuration du compte d’identification](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config.png)

<span data-ttu-id="812ba-262">Lorsque vous sélectionnez le compte d’identification, le volet **Propriétés** du compte affiche le message d’erreur suivant :</span><span class="sxs-lookup"><span data-stu-id="812ba-262">When you select the Run As account, the account **Properties** pane displays the following error message:</span></span>

![Message d’avertissement Incomplet pour la configuration du compte d’identification](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config-msg.png)<span data-ttu-id="812ba-264">.</span><span class="sxs-lookup"><span data-stu-id="812ba-264">.</span></span>

<span data-ttu-id="812ba-265">Vous pouvez rapidement résoudre ces problèmes liés au compte d’identification en supprimant et en recréant le compte.</span><span class="sxs-lookup"><span data-stu-id="812ba-265">You can quickly resolve these Run As account issues by deleting and re-creating the account.</span></span>

## <a name="update-your-automation-account-by-using-powershell"></a><span data-ttu-id="812ba-266">Mise à jour de votre compte Automation à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="812ba-266">Update your Automation account by using PowerShell</span></span>
<span data-ttu-id="812ba-267">Vous pouvez utiliser PowerShell pour mettre à jour votre compte Automation existant si :</span><span class="sxs-lookup"><span data-stu-id="812ba-267">You can use PowerShell to update your existing Automation account if:</span></span>

* <span data-ttu-id="812ba-268">Vous créez un compte Automation sans compte d’identification.</span><span class="sxs-lookup"><span data-stu-id="812ba-268">You create an Automation account but decline to create the Run As account.</span></span>
* <span data-ttu-id="812ba-269">Vous possédez déjà un compte Automation pour gérer les ressources Resource Manager et vous voulez le mettre à jour pour inclure le compte d’identification pour l’authentification du Runbook.</span><span class="sxs-lookup"><span data-stu-id="812ba-269">You already use an Automation account to manage Resource Manager resources and you want to update the account to include the Run As account for runbook authentication.</span></span>
* <span data-ttu-id="812ba-270">Vous possédez déjà un compte Automation pour gérer les ressources classiques et souhaitez le mettre à jour pour utiliser le compte d’identification Classic au lieu de créer un compte et d’y migrer vos Runbooks et ressources.</span><span class="sxs-lookup"><span data-stu-id="812ba-270">You already use an Automation account to manage classic resources and you want to update it to use the Classic Run As account instead of creating a new account and migrating your runbooks and assets to it.</span></span>   
* <span data-ttu-id="812ba-271">Vous souhaitez créer un compte d’identification standard et un compte d’identification Classic à l’aide d’un certificat émis par votre AC d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="812ba-271">You want to create a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

<span data-ttu-id="812ba-272">Le script nécessite les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="812ba-272">The script has the following prerequisites:</span></span>

* <span data-ttu-id="812ba-273">Ce script peut uniquement être exécuté sur Windows 10 et sur Windows Server 2016 avec les modules Azure Resource Manager 2.01 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="812ba-273">The script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 2.01 and later.</span></span> <span data-ttu-id="812ba-274">Il n’est pas pris en charge dans les versions antérieures de Windows.</span><span class="sxs-lookup"><span data-stu-id="812ba-274">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="812ba-275">Azure PowerShell 1.0 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="812ba-275">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="812ba-276">Pour plus d’informations sur la version PowerShell 1.0, voir [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="812ba-276">For information about the PowerShell 1.0 release, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="812ba-277">Un compte Automation, référencé en tant que valeur des paramètres *–AutomationAccountName* et *-ApplicationDisplayName* dans le script PowerShell suivant.</span><span class="sxs-lookup"><span data-stu-id="812ba-277">An Automation account, which is referenced as the value for the *–AutomationAccountName* and *-ApplicationDisplayName* parameters in the following PowerShell script.</span></span>

<span data-ttu-id="812ba-278">Pour obtenir les valeurs des paramètres *SubscriptionID*, *ResourceGroup* et *AutomationAccountName*, qui sont des paramètres requis pour les scripts, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="812ba-278">To get the values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for the scripts, do the following:</span></span>
1. <span data-ttu-id="812ba-279">Sélectionnez votre compte Automation à partir du panneau **Compte Automation** du portail Azure, puis sélectionnez **Tous les paramètres**.</span><span class="sxs-lookup"><span data-stu-id="812ba-279">In the Azure portal, select your Automation account on the **Automation account** blade, and then select **All settings**.</span></span> 
2. <span data-ttu-id="812ba-280">Dans le panneau **Tous les paramètres**, sous **Paramètres du compte**, sélectionnez **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="812ba-280">On the **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="812ba-281">Notez les valeurs dans le panneau **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="812ba-281">Note the values on the **Properties** blade.</span></span>

![Panneau Propriétés du compte Automation](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

### <a name="create-a-run-as-account-powershell-script"></a><span data-ttu-id="812ba-283">Créer le script PowerShell d’un compte d’identification</span><span class="sxs-lookup"><span data-stu-id="812ba-283">Create a Run As account PowerShell script</span></span>
<span data-ttu-id="812ba-284">Ce script PowerShell prend en charge les configurations suivantes :</span><span class="sxs-lookup"><span data-stu-id="812ba-284">This PowerShell script includes support for the following configurations:</span></span>

* <span data-ttu-id="812ba-285">Créez un compte d’identification à l’aide d’un certificat auto-signé.</span><span class="sxs-lookup"><span data-stu-id="812ba-285">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="812ba-286">Créez un compte d’identification standard et un compte d’identification Classic à l’aide d’un certificat auto-signé.</span><span class="sxs-lookup"><span data-stu-id="812ba-286">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="812ba-287">Créez un compte d’identification standard et un compte d’identification Classic à l’aide d’un certificat d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="812ba-287">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="812ba-288">Créez un compte d’identification standard et un compte d’identification Classic à l’aide d’un certificat auto-signé dans le cloud Azure Government.</span><span class="sxs-lookup"><span data-stu-id="812ba-288">Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud.</span></span>

<span data-ttu-id="812ba-289">Selon l’option de configuration que vous sélectionnez, le script crée les éléments suivants.</span><span class="sxs-lookup"><span data-stu-id="812ba-289">Depending on the configuration option you select, the script creates the following items.</span></span>

<span data-ttu-id="812ba-290">**Pour les comptes d’identification :**</span><span class="sxs-lookup"><span data-stu-id="812ba-290">**For Run As accounts:**</span></span>

* <span data-ttu-id="812ba-291">Crée une application Azure AD qui sera exportée avec la clé publique du certificat auto-signé ou du certificat d’entreprise, crée un compte de principal de service pour cette application dans Azure AD et affecte le rôle Collaborateur pour le compte dans votre abonnement actuel.</span><span class="sxs-lookup"><span data-stu-id="812ba-291">Creates an Azure AD application to be exported with either the self-signed or enterprise certificate public key, creates a service principal account for the application in Azure AD, and assigns the Contributor role for the account in your current subscription.</span></span> <span data-ttu-id="812ba-292">Vous pouvez remplacer ce paramètre par un rôle de propriétaire ou par tout autre rôle.</span><span class="sxs-lookup"><span data-stu-id="812ba-292">You can change this setting to Owner or any other role.</span></span> <span data-ttu-id="812ba-293">Pour plus d’informations, voir [Contrôle d’accès en fonction du rôle dans Azure Automation](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="812ba-293">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="812ba-294">Crée une ressource de certificat Automation nommée *AzureRunAsCertificate* dans le compte Automation spécifié.</span><span class="sxs-lookup"><span data-stu-id="812ba-294">Creates an Automation certificate asset named *AzureRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="812ba-295">La ressource de certificat conserve la clé privée du certificat utilisée par l’application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="812ba-295">The certificate asset holds the certificate private key that's used by the Azure AD application.</span></span>
* <span data-ttu-id="812ba-296">Crée une ressource de connexion Automation nommée *AzureRunAsConnection* dans le compte Automation spécifié.</span><span class="sxs-lookup"><span data-stu-id="812ba-296">Creates an Automation connection asset named *AzureRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="812ba-297">La ressource de connexion conserve les ID applicationId, tenantId et subscriptionId, et l’empreinte de certificat.</span><span class="sxs-lookup"><span data-stu-id="812ba-297">The connection asset holds the applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="812ba-298">**Pour les comptes d’identification Classic :**</span><span class="sxs-lookup"><span data-stu-id="812ba-298">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="812ba-299">Crée une ressource de certificat Automation nommée *AzureClassicRunAsCertificate*dans le compte Automation spécifié.</span><span class="sxs-lookup"><span data-stu-id="812ba-299">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in the specified Automation account.</span></span> <span data-ttu-id="812ba-300">La ressource de certificat conserve la clé privée du certificat utilisée par le certificat de gestion.</span><span class="sxs-lookup"><span data-stu-id="812ba-300">The certificate asset holds the certificate private key used by the management certificate.</span></span>
* <span data-ttu-id="812ba-301">Crée une ressource de connexion Automation nommée *AzureClassicRunAsConnection* dans le compte Automation spécifié.</span><span class="sxs-lookup"><span data-stu-id="812ba-301">Creates an Automation connection asset named *AzureClassicRunAsConnection* in the specified Automation account.</span></span> <span data-ttu-id="812ba-302">La ressource de connexion conserve le nom de l’abonnement, l’ID subscriptionId et le nom de ressource de certificat.</span><span class="sxs-lookup"><span data-stu-id="812ba-302">The connection asset holds the subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="812ba-303">Si vous sélectionnez l’option permettant de créer un compte d’identification Classic, après l’exécution du script, vous devez charger le certificat public (extension de nom de fichier .cer) dans le magasin de gestion de l’abonnement dans lequel le compte Automation a été créé.</span><span class="sxs-lookup"><span data-stu-id="812ba-303">If you select either option for creating a Classic Run As account, after the script is executed, upload the public certificate (.cer file name extension) to the management store for the subscription that the Automation account was created in.</span></span>
> 

<span data-ttu-id="812ba-304">Pour exécuter le script et télécharger le certificat, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="812ba-304">To execute the script and upload the certificate, do the following:</span></span>

1. <span data-ttu-id="812ba-305">Enregistrez le script suivant sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="812ba-305">Save the following script on your computer.</span></span> <span data-ttu-id="812ba-306">Dans cet exemple, enregistrez-le sous le nom de fichier *New-RunAsAccount.ps1*.</span><span class="sxs-lookup"><span data-stu-id="812ba-306">In this example, save it with the filename *New-RunAsAccount.ps1*.</span></span>

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
        $KeyCredential.EndDate= [DateTime]$PfxCert.GetExpirationDateString()
        $KeyCredential.EndDate = $KeyCredential.EndDate.AddDays(-1)
        $KeyCredential.KeyId = $KeyId
        $KeyCredential.CertValue  = $keyValue

        # Use key credentials and create an Azure AD application
        $Application = New-AzureRmADApplication -DisplayName $ApplicationDisplayName -HomePage ("http://" + $applicationDisplayName) -IdentifierUris ("http://" + $KeyId) -KeyCredentials $KeyCredential
        $ServicePrincipal = New-AzureRMADServicePrincipal -ApplicationId $Application.ApplicationId
        $GetServicePrincipal = Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id

        # Sleep here for a few seconds to allow the service principal application to become active (ordinarily takes a few seconds)
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
        if (!(($AzureRMProfileVersion.Major -ge 2 -and $AzureRMProfileVersion.Minor -ge 1) -or ($AzureRMProfileVersion.Major -gt 2)))
        {
           Write-Error -Message "Please install the latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
           return
        }

        Login-AzureRmAccount -EnvironmentName $EnvironmentName
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

        # Create the Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

        # Populate the ConnectionFieldValues
        $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
        $TenantID = $SubscriptionInfo | Select TenantId -First 1
        $Thumbprint = $PfxCert.Thumbprint
        $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

        # Create an Automation connection asset named AzureRunAsConnection in the Automation account. This connection uses the service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

        if ($CreateClassicRunAsAccount) {
            # Create a Run As account by using a service principal
            $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
            $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
            $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
            $UploadMessage = "Please upload the .cer format of #CERT# to the Management store by following the steps below." + [Environment]::NewLine +
                    "Log in to the Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                    "Then click Upload and upload the .cer format of #CERT#"

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

        # Create the Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate the ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.SubscriptionName
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in the Automation account. This connection uses the service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="812ba-307">Sur votre ordinateur, cliquez sur **Démarrer**, puis démarrez **Windows PowerShell** avec des droits de l’utilisateur élevés.</span><span class="sxs-lookup"><span data-stu-id="812ba-307">On your computer, click **Start**, and then start **Windows PowerShell** with elevated user rights.</span></span>

3. <span data-ttu-id="812ba-308">À partir de l’interface de ligne de commande PowerShell avec élévation de privilèges, accédez au dossier contenant le script que vous avez créé à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="812ba-308">From the elevated PowerShell command-line shell, go to the folder that contains the script you created in step 1.</span></span>

4. <span data-ttu-id="812ba-309">Exécutez le script en utilisant les valeurs de paramètre pour la configuration dont vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="812ba-309">Execute the script by using the parameter values for the configuration you require.</span></span>

    <span data-ttu-id="812ba-310">**Créer un compte d’identification à l’aide d’un certificat auto-signé**</span><span class="sxs-lookup"><span data-stu-id="812ba-310">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="812ba-311">**Créer un compte d’identification standard et un compte d’identification Classic à l’aide d’un certificat auto-signé**</span><span class="sxs-lookup"><span data-stu-id="812ba-311">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="812ba-312">**Créer un compte d’identification standard et un compte d’identification Classic à l’aide d’un certificat d’entreprise**</span><span class="sxs-lookup"><span data-stu-id="812ba-312">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="812ba-313">**Créer un compte d’identification standard et un compte d’identification Classic à l’aide d’un certificat auto-signé dans le cloud Azure Government**</span><span class="sxs-lookup"><span data-stu-id="812ba-313">**Create a Run As account and a Classic Run As account by using a self-signed certificate in the Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="812ba-314">Une fois le script exécuté, vous êtes invité à vous authentifier auprès d’Azure.</span><span class="sxs-lookup"><span data-stu-id="812ba-314">After the script has executed, you will be prompted to authenticate with Azure.</span></span> <span data-ttu-id="812ba-315">Connectez-vous avec un compte membre du rôle Administrateurs des abonnements et coadministrateur de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="812ba-315">Sign in with an account that is a member of the subscription administrators role and co-administrator of the subscription.</span></span>
    >
    >

<span data-ttu-id="812ba-316">Une fois le script exécuté, notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="812ba-316">After the script has executed successfully, note the following:</span></span>
* <span data-ttu-id="812ba-317">Si vous avez créé un compte d’identification Classic avec un certificat public auto-signé (fichier .cer), le script le crée et l’enregistre dans le dossier de fichiers temporaires sur votre ordinateur, sous le profil d’utilisateur *%USERPROFILE%\AppData\Local\Temp* utilisé pour exécuter la session PowerShell.</span><span class="sxs-lookup"><span data-stu-id="812ba-317">If you created a Classic Run As account with a self-signed public certificate (.cer file), the script creates and saves it to the temporary files folder on your computer under the user profile *%USERPROFILE%\AppData\Local\Temp*, which you used to execute the PowerShell session.</span></span>
* <span data-ttu-id="812ba-318">Si vous avez créé un compte d’identification Classic avec un certificat public d’entreprise (fichier .cer), utilisez ce certificat.</span><span class="sxs-lookup"><span data-stu-id="812ba-318">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="812ba-319">Suivez les instructions pour [charger un certificat d’API de gestion vers le portail Azure Classic](../azure-api-management-certs.md), puis validez la configuration des informations d’identification avec les ressources de gestion des services à l’aide de [l’exemple de code pour l’authentification avec les ressources de gestion des services](#sample-code-to-authenticate-with-service-management-resources).</span><span class="sxs-lookup"><span data-stu-id="812ba-319">Follow the instructions for [uploading a management API certificate to the Azure classic portal](../azure-api-management-certs.md), and then validate the credential configuration with Service Management resources by using the [sample code to authenticate with Service Management Resources](#sample-code-to-authenticate-with-service-management-resources).</span></span> 
* <span data-ttu-id="812ba-320">Si vous n’avez *pas* créé de compte d’identification Classic, authentifiez-vous avec des ressources Resource Manager et validez la configuration des informations d’identification à l’aide [l’exemple de code pour l’authentification avec les ressources de gestion des services](#sample-code-to-authenticate-with-resource-manager-resources).</span><span class="sxs-lookup"><span data-stu-id="812ba-320">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate the credential configuration by using the [sample code for authenticating with Service Management resources](#sample-code-to-authenticate-with-resource-manager-resources).</span></span>

## <a name="sample-code-to-authenticate-with-resource-manager-resources"></a><span data-ttu-id="812ba-321">Exemple de code pour l’authentification avec des ressources Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="812ba-321">Sample code to authenticate with Resource Manager resources</span></span>
<span data-ttu-id="812ba-322">Vous pouvez utiliser l’exemple de code mis à jour suivant, extrait de l’exemple de Runbook *AzureAutomationTutorialScript*, pour procéder à une authentification avec le compte d’identification pour gérer les ressources Azure Resource Manager avec vos Runbooks.</span><span class="sxs-lookup"><span data-stu-id="812ba-322">You can use the following updated sample code, taken from the *AzureAutomationTutorialScript* example runbook, to authenticate by using the Run As account to manage Resource Manager resources with your runbooks.</span></span>

    $connectionName = "AzureRunAsConnection"
    $SubId = Get-AutomationVariable -Name 'SubscriptionId'
    try
    {
       # Get the connection "AzureRunAsConnection "
       $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

       "Signing in to Azure..."
       Add-AzureRmAccount `
         -ServicePrincipal `
         -TenantId $servicePrincipalConnection.TenantId `
         -ApplicationId $servicePrincipalConnection.ApplicationId `
         -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
       "Setting context to a specific subscription"     
       Set-AzureRmContext -SubscriptionId $SubId              
    }
    catch {
        if (!$servicePrincipalConnection)
        {
           $ErrorMessage = "Connection $connectionName not found."
           throw $ErrorMessage
         } else{
            Write-Error -Message $_.Exception
            throw $_.Exception
         }
    }

<span data-ttu-id="812ba-323">Afin de faciliter le travail entre plusieurs abonnements, le script inclut deux lignes de code supplémentaires pour prendre en charge le référencement d’un contexte d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="812ba-323">To help you to easily work between multiple subscriptions, the script includes two additional lines of code that support referencing a subscription context.</span></span> <span data-ttu-id="812ba-324">La ressource variable *SubscriptionId* contient l’ID de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="812ba-324">A variable asset named *SubscriptionId* contains the ID of the subscription.</span></span> <span data-ttu-id="812ba-325">Après l’instruction d’applet de commande `Add-AzureRmAccount`, l’applet de commande [`Set-AzureRmContext`](/powershell/module/azurerm.profile/set-azurermcontext) est indiqué avec le jeu de paramètres *-SubscriptionId*.</span><span class="sxs-lookup"><span data-stu-id="812ba-325">After the `Add-AzureRmAccount` cmdlet statement, the [`Set-AzureRmContext`](/powershell/module/azurerm.profile/set-azurermcontext) cmdlet is stated with the parameter set *-SubscriptionId*.</span></span> <span data-ttu-id="812ba-326">Si le nom de la variable est trop générique, vous pouvez le modifier afin qu’il comprenne un préfixe ou utiliser une autre convention d’affectation de noms pour faciliter son identification.</span><span class="sxs-lookup"><span data-stu-id="812ba-326">If the variable name is too generic, you can revise it to include a prefix or use another naming convention to make it easier to identify.</span></span> <span data-ttu-id="812ba-327">Vous pouvez également utiliser le jeu de paramètres *-SubscriptionName* au lieu de *-SubscriptionId* avec la ressource de variable correspondante.</span><span class="sxs-lookup"><span data-stu-id="812ba-327">Alternatively, you can use the parameter set *-SubscriptionName* instead of *-SubscriptionId* with a corresponding variable asset.</span></span>

<span data-ttu-id="812ba-328">L’applet de commande utilisée pour l’authentification dans le Runbook, `Add-AzureRmAccount`, utilise le jeu de paramètres *ServicePrincipalCertificate*.</span><span class="sxs-lookup"><span data-stu-id="812ba-328">The cmdlet that you use for authenticating in the runbook, `Add-AzureRmAccount`, uses the *ServicePrincipalCertificate* parameter set.</span></span> <span data-ttu-id="812ba-329">Elle effectue l’authentification à l’aide du certificat du principal du service, et non des informations d’identification de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="812ba-329">It authenticates by using the service principal certificate, not the user credentials.</span></span>

## <a name="sample-code-to-authenticate-with-service-management-resources"></a><span data-ttu-id="812ba-330">Exemple de code pour l’authentification avec les ressources de gestion des services</span><span class="sxs-lookup"><span data-stu-id="812ba-330">Sample code to authenticate with Service Management resources</span></span>
<span data-ttu-id="812ba-331">Vous pouvez utiliser l’exemple de code mis à jour suivant, extrait de l’exemple de Runbook *AzureClassicAutomationTutorialScript*, pour procéder à une authentification avec le compte d’identification Classic pour gérer les ressources classiques avec vos Runbooks.</span><span class="sxs-lookup"><span data-stu-id="812ba-331">You can use the following updated sample code, which is taken from the *AzureClassicAutomationTutorialScript* example runbook, to authenticate by using the Classic Run As account to manage classic resources with your runbooks.</span></span>

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get the connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate to Azure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in the Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting the certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in the Automation account."
    }

    Write-Verbose "Authenticating to Azure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID

## <a name="next-steps"></a><span data-ttu-id="812ba-332">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="812ba-332">Next steps</span></span>
* [<span data-ttu-id="812ba-333">Objets application et principal du service dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="812ba-333">Application and service principal objects in Azure AD</span></span>](../active-directory/active-directory-application-objects.md)
* [<span data-ttu-id="812ba-334">Contrôle d’accès en fonction du rôle dans Azure Automation</span><span class="sxs-lookup"><span data-stu-id="812ba-334">Role-based access control in Azure Automation</span></span>](automation-role-based-access-control.md)
* [<span data-ttu-id="812ba-335">Vue d’ensemble des certificats pour Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="812ba-335">Certificates overview for Azure Cloud Services</span></span>](../cloud-services/cloud-services-certs-create.md)
