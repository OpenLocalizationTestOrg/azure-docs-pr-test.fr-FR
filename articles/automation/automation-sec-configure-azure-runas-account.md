---
title: "aaaConfigure une exécution en tant que compte Azure | Documents Microsoft"
description: "Ce didacticiel vous guide à l’aide de la création, le test et exemple hello d’authentification principal de sécurité dans Azure Automation."
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
redirect_document_id: True
ms.openlocfilehash: 06675d2f6b9d8e7260ffaead4f2b2f61c2b98d13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-runbooks-with-an-azure-run-as-account"></a><span data-ttu-id="2641a-104">Authentifier des Runbooks avec un compte d’identification Azure</span><span class="sxs-lookup"><span data-stu-id="2641a-104">Authenticate runbooks with an Azure Run As account</span></span>
<span data-ttu-id="2641a-105">Cet article vous explique comment tooconfigure un Azure Automation compte Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2641a-105">This article shows you how tooconfigure an Azure Automation account in hello Azure portal.</span></span> <span data-ttu-id="2641a-106">toodo par conséquent, vous utilisez hello exécuter en tant que compte fonctionnalité tooauthenticate runbooks la gestion des ressources dans le Gestionnaire de ressources Azure ou de gestion des services Azure.</span><span class="sxs-lookup"><span data-stu-id="2641a-106">toodo so, you use hello Run As account feature tooauthenticate runbooks managing resources in either Azure Resource Manager or Azure Service Management.</span></span>

<span data-ttu-id="2641a-107">Lorsque vous créez un compte Automation Bonjour portail Azure, vous créez automatiquement deux comptes :</span><span class="sxs-lookup"><span data-stu-id="2641a-107">When you create an Automation account in hello Azure portal, you automatically create two accounts:</span></span>

* <span data-ttu-id="2641a-108">Compte d’identification Azure.</span><span class="sxs-lookup"><span data-stu-id="2641a-108">A Run As account.</span></span> <span data-ttu-id="2641a-109">Ce compte crée un principal de service dans Azure Active Directory (Azure AD) et un certificat.</span><span class="sxs-lookup"><span data-stu-id="2641a-109">This account creates a service principal in Azure Active Directory (Azure AD) and a certificate.</span></span> <span data-ttu-id="2641a-110">Il assigne également hello collaborateur basée sur le rôle de contrôle d’accès (RBAC), qui gère les ressources de gestionnaire de ressources à l’aide de procédures opérationnelles.</span><span class="sxs-lookup"><span data-stu-id="2641a-110">It also assigns hello Contributor role-based access control (RBAC), which manages Resource Manager resources by using runbooks.</span></span>
* <span data-ttu-id="2641a-111">Compte d’identification Classic.</span><span class="sxs-lookup"><span data-stu-id="2641a-111">A Classic Run As account.</span></span> <span data-ttu-id="2641a-112">Ce compte télécharge un certificat de gestion, qui est utilisé toomanage de gestion des services ou des ressources classiques à l’aide de procédures opérationnelles.</span><span class="sxs-lookup"><span data-stu-id="2641a-112">This account uploads a management certificate, which is used toomanage Service Management or classic resources by using runbooks.</span></span>

<span data-ttu-id="2641a-113">Création d’un objet Automation compte simplifie hello pour vous et vous aide à que commencer rapidement générer et déployer des procédures opérationnelles toosupport votre automatisation a besoin.</span><span class="sxs-lookup"><span data-stu-id="2641a-113">Creating an Automation account simplifies hello process for you and helps you quickly start building and deploying runbooks toosupport your automation needs.</span></span>

<span data-ttu-id="2641a-114">À l’aide de comptes d’identification standard ou Classic, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="2641a-114">With Run As and Classic Run As accounts, you can:</span></span>

* <span data-ttu-id="2641a-115">Fournir une méthode standardisée de tooauthenticate avec Azure lorsque vous gérez le Gestionnaire de ressources ou des ressources de gestion de Service à partir de procédures opérationnelles Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2641a-115">Provide a standardized way tooauthenticate with Azure when you manage Resource Manager or Service Management resources from runbooks in hello Azure portal.</span></span>
* <span data-ttu-id="2641a-116">Automatisez l’utilisation de hello des procédures opérationnelles globales, vous pouvez les configurer dans Azure Alerts.</span><span class="sxs-lookup"><span data-stu-id="2641a-116">Automate hello use of global runbooks, which you can configure in Azure Alerts.</span></span>

> [!NOTE]
> <span data-ttu-id="2641a-117">Hello [fonctionnalité d’intégration Azure alerte](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) avec l’Automation des procédures opérationnelles globales nécessite un compte Automation est configuré avec un compte d’identification et classique compte d’identification.</span><span class="sxs-lookup"><span data-stu-id="2641a-117">hello [Azure Alert integration feature](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) with Automation global runbooks requires an Automation account that's configured with a Run As account and a Classic Run As account.</span></span> <span data-ttu-id="2641a-118">Vous pouvez sélectionner un compte Automation a déjà défini des comptes d’identification et Classic exécuter en tant que, ou vous pouvez choisir toocreate un compte Automation.</span><span class="sxs-lookup"><span data-stu-id="2641a-118">You can select an Automation account that already has defined Run As and Classic Run As accounts, or you can choose toocreate a new Automation account.</span></span>
>  

<span data-ttu-id="2641a-119">Cet article explique comment toocreate un compte Automation à partir de hello portail Azure, mettre à jour un compte Automation à l’aide d’Azure PowerShell, gérer la configuration de compte hello et s’authentifier dans vos runbook.</span><span class="sxs-lookup"><span data-stu-id="2641a-119">This article shows how toocreate an Automation account from hello Azure portal, update an Automation account by using Azure PowerShell, manage hello account configuration, and authenticate in your runbooks.</span></span>

<span data-ttu-id="2641a-120">Avant de commencer la création d’un compte Automation, elle est une bonne idée toounderstand et tenez compte hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="2641a-120">Before you begin creating an Automation account, it's a good idea toounderstand and consider hello following:</span></span>

* <span data-ttu-id="2641a-121">Création d’un compte Automation n’affecte pas les comptes Automation que vous avez peut-être déjà créé dans hello classique ou modèle de déploiement de gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="2641a-121">Creating an Automation account does not affect Automation accounts you might have already created in either hello classic or Resource Manager deployment model.</span></span>
* <span data-ttu-id="2641a-122">processus de Hello fonctionne uniquement pour les comptes Automation que vous créez dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2641a-122">hello process works only for Automation accounts that you create in hello Azure portal.</span></span> <span data-ttu-id="2641a-123">Tentative de toocreate un compte à partir de hello portail Azure classic ne réplique pas hello exécuter en tant que compte configuration.</span><span class="sxs-lookup"><span data-stu-id="2641a-123">Attempting toocreate an account from hello Azure classic portal does not replicate hello Run As account configuration.</span></span>
* <span data-ttu-id="2641a-124">Si vous avez déjà des procédures opérationnelles et ressources (telles que des planifications ou des variables) dans toomanage place les ressources classiques, et vous souhaitez tooauthenticate runbooks avec hello classique compte d’identification, procéder de hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="2641a-124">If you already have runbooks and assets (such as schedules or variables) in place toomanage classic resources, and you want runbooks tooauthenticate with hello new Classic Run As account, do either of hello following:</span></span>

  * <span data-ttu-id="2641a-125">toocreate classique compte d’identification, suivez les instructions de hello dans la section « Gestion de votre compte d’identification » de hello.</span><span class="sxs-lookup"><span data-stu-id="2641a-125">toocreate a Classic Run As account, follow hello instructions in hello "Managing your Run As account" section.</span></span> 
  * <span data-ttu-id="2641a-126">votre compte existant, utilisez hello PowerShell tooupdate un script dans la section « Mise à jour de votre compte Automation à l’aide de PowerShell » de hello.</span><span class="sxs-lookup"><span data-stu-id="2641a-126">tooupdate your existing account, use hello PowerShell script in hello "Update your Automation account by using PowerShell" section.</span></span>
* <span data-ttu-id="2641a-127">tooauthenticate à l’aide de hello nouveau compte d’identification et compte classique exécuter en tant que Automation, vous devez toomodify vos runbooks existants avec hello l’exemple de code fourni dans la section de hello [exemples de code d’authentification](#authentication-code-examples).</span><span class="sxs-lookup"><span data-stu-id="2641a-127">tooauthenticate by using hello new Run As account and Classic Run As Automation account, you  need toomodify your existing runbooks with hello example code provided in hello section [Authentication code examples](#authentication-code-examples).</span></span>

    >[!NOTE]
    ><span data-ttu-id="2641a-128">Exécuter en tant que compte de Hello est pour l’authentification par rapport aux ressources du Gestionnaire de ressources à l’aide de principal du service de basée sur certificat hello.</span><span class="sxs-lookup"><span data-stu-id="2641a-128">hello Run As account is for authentication against Resource Manager resources using hello certificate-based service principal.</span></span> <span data-ttu-id="2641a-129">est de Hello classique compte d’identification pour s’authentifier auprès des ressources de gestion de Service avec un certificat de gestion.</span><span class="sxs-lookup"><span data-stu-id="2641a-129">hello Classic Run As account is for authenticating against Service Management resources with a management certificate.</span></span>

## <a name="create-an-automation-account-from-hello-azure-portal"></a><span data-ttu-id="2641a-130">Créer un compte Automation à partir de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="2641a-130">Create an Automation account from hello Azure portal</span></span>
<span data-ttu-id="2641a-131">Dans cette section, vous créer un compte Azure Automation à partir de hello portail Azure, qui crée ensuite un compte d’identification et classique compte d’identification.</span><span class="sxs-lookup"><span data-stu-id="2641a-131">In this section, you create an Azure Automation account from hello Azure portal, which in turn creates both a Run As account and a Classic Run As account.</span></span>

>[!NOTE]
><span data-ttu-id="2641a-132">toocreate un compte Automation, vous devez être membre du rôle des administrateurs de Service hello ou coadministrateur de l’abonnement hello qui accorde l’accès toohello abonnement.</span><span class="sxs-lookup"><span data-stu-id="2641a-132">toocreate an Automation account, you must be a member of hello Service Admins role or co-administrator of hello subscription that is granting access toohello subscription.</span></span> <span data-ttu-id="2641a-133">Vous devez également être ajouté en tant qu’instance d’Active Directory d’un abonnement toothat utilisateur par défaut.</span><span class="sxs-lookup"><span data-stu-id="2641a-133">You must also be added as a user toothat subscription's default Active Directory instance.</span></span> <span data-ttu-id="2641a-134">compte de Hello n’a pas besoin toobe affecté un rôle privilégié.</span><span class="sxs-lookup"><span data-stu-id="2641a-134">hello account does not need toobe assigned a privileged role.</span></span>
>
><span data-ttu-id="2641a-135">Si vous n’êtes pas un membre d’instance d’Active Directory de l’abonnement hello avant que vous êtes ajouté le rôle de coadministrateur toohello d’abonnement de hello, vous ajouterez tooActive active en tant qu’invité.</span><span class="sxs-lookup"><span data-stu-id="2641a-135">If you are not a member of hello subscription’s Active Directory instance before you are added toohello co-administrator role of hello subscription, you will be added tooActive Directory as a guest.</span></span> <span data-ttu-id="2641a-136">Dans ce cas, vous recevrez un « vous n’avez pas toocreate autorisations... »</span><span class="sxs-lookup"><span data-stu-id="2641a-136">In this instance, you will receive a “You do not have permissions toocreate…”</span></span> <span data-ttu-id="2641a-137">avertissement sur hello **ajouter un compte Automation** panneau.</span><span class="sxs-lookup"><span data-stu-id="2641a-137">warning on hello **Add Automation Account** blade.</span></span>
>
><span data-ttu-id="2641a-138">Les utilisateurs qui ont été ajoutés tout d’abord, rôle de coadministrateur toohello peut être supprimé de l’instance d’Active Directory de l’abonnement hello et rajouté toomake les un utilisateur complète dans Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2641a-138">Users who were added toohello co-administrator role first can be removed from hello subscription's Active Directory instance and re-added toomake them a full User in Active Directory.</span></span> <span data-ttu-id="2641a-139">tooverify cette situation hello **Azure Active Directory** volet Bonjour portail Azure en sélectionnant **utilisateurs et groupes**, en sélectionnant **tous les utilisateurs** et, après avoir sélectionné utilisateur spécifique de Hello, en sélectionnant **profil**.</span><span class="sxs-lookup"><span data-stu-id="2641a-139">tooverify this situation from hello **Azure Active Directory** pane in hello Azure portal by selecting **Users and groups**, selecting **All users** and, after you select hello specific user, selecting **Profile**.</span></span> <span data-ttu-id="2641a-140">Hello valeur Hello **type utilisateur** attribut sous le profil de l’utilisateur hello doit être **invité**.</span><span class="sxs-lookup"><span data-stu-id="2641a-140">hello value of hello **User type** attribute under hello users profile should not equal **Guest**.</span></span>
>

1. <span data-ttu-id="2641a-141">Connectez-vous toohello portail Azure avec un compte qui est membre du rôle Administrateurs d’abonnement hello et coadministrateur de l’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="2641a-141">Sign in toohello Azure portal with an account that is a member of hello subscription administrators role and co-administrator of hello subscription.</span></span>

2. <span data-ttu-id="2641a-142">Sélectionnez **Comptes Automation**.</span><span class="sxs-lookup"><span data-stu-id="2641a-142">Select **Automation Accounts**.</span></span>

3. <span data-ttu-id="2641a-143">Sur hello **comptes Automation** panneau, cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="2641a-143">On hello **Automation Accounts** blade, click **Add**.</span></span>
<span data-ttu-id="2641a-144">Hello **ajouter un compte Automation** panneau s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="2641a-144">hello **Add Automation Account** blade opens.</span></span>

 ![panneau de « Ajouter un compte Automation » Hello](media/automation-sec-configure-azure-runas-account/create-automation-account-properties-b.png)

   > [!NOTE]
   > <span data-ttu-id="2641a-146">Si votre compte n’est pas membre du rôle Administrateurs d’abonnement aux hello et coadministrateur de l’abonnement de hello, hello suivant d’avertissement s’affiche sur hello **ajouter un compte Automation** panneau :</span><span class="sxs-lookup"><span data-stu-id="2641a-146">If your account is not a member of hello subscription administrators role and co-administrator of hello subscription, hello following warning is displayed on hello **Add Automation Account** blade:</span></span>
   >
   >![Avertissement Ajouter un compte Automation](media/automation-sec-configure-azure-runas-account/create-account-without-perms.png)
   >
   >

4. <span data-ttu-id="2641a-148">Sur hello **ajouter un compte Automation** panneau, Bonjour **nom** , tapez un nom pour votre nouveau compte Automation.</span><span class="sxs-lookup"><span data-stu-id="2641a-148">On hello **Add Automation Account** blade, in hello **Name** box, type a name for your new Automation account.</span></span>

5. <span data-ttu-id="2641a-149">Si vous avez plusieurs abonnements, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="2641a-149">If you have more than one subscription, do hello following:</span></span>

    <span data-ttu-id="2641a-150">a.</span><span class="sxs-lookup"><span data-stu-id="2641a-150">a.</span></span> <span data-ttu-id="2641a-151">Sous **abonnement**, spécifiez un nouveau compte de hello.</span><span class="sxs-lookup"><span data-stu-id="2641a-151">Under **Subscription**, specify one for hello new account.</span></span>

    <span data-ttu-id="2641a-152">b.</span><span class="sxs-lookup"><span data-stu-id="2641a-152">b.</span></span> <span data-ttu-id="2641a-153">Sous **Groupe de ressources**, cliquez sur **Créer** ou **Utiliser l’existant**.</span><span class="sxs-lookup"><span data-stu-id="2641a-153">Under **Resource Group**, click **Create new** or **Use existing**.</span></span>

    <span data-ttu-id="2641a-154">c.</span><span class="sxs-lookup"><span data-stu-id="2641a-154">c.</span></span> <span data-ttu-id="2641a-155">Sous **Emplacement**, indiquez un centre de données Azure.</span><span class="sxs-lookup"><span data-stu-id="2641a-155">Under **Location**, specify an Azure datacenter.</span></span>

6. <span data-ttu-id="2641a-156">Sous **Créer un compte d’identification Azure**, sélectionnez **Oui**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="2641a-156">Under **Create Azure Run As account**, select **Yes**, and then click **Create**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2641a-157">Si vous ne choisissez pas toocreate hello compte d’identification en sélectionnant **non**, un message d’avertissement s’affiche hello **ajouter un compte Automation** panneau.</span><span class="sxs-lookup"><span data-stu-id="2641a-157">If you choose not toocreate hello Run As account by selecting **No**, a warning message is displayed hello **Add Automation Account** blade.</span></span> <span data-ttu-id="2641a-158">Bien que le compte de hello est créé dans hello portail Azure, il n’a pas une identité d’authentification correspondant au sein de votre classique ou le service d’annuaire abonnement Gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="2641a-158">Although hello account is created in hello Azure portal, it does not have a corresponding authentication identity within your classic or Resource Manager subscription directory service.</span></span> <span data-ttu-id="2641a-159">En conséquence, le compte de hello n’a aucune tooresources d’accès dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="2641a-159">Consequently, hello account has no access tooresources in your subscription.</span></span> <span data-ttu-id="2641a-160">Ce scénario empêche tous les Runbooks faisant référence à ce compte de pouvoir s’authentifier et d’effectuer des tâches sur les ressources de ces modèles de déploiement.</span><span class="sxs-lookup"><span data-stu-id="2641a-160">This scenario prevents any runbooks that reference this account from authenticating and performing tasks against resources in those deployment models.</span></span>
   >
   > ![Message d’avertissement sur le panneau de « Ajouter un compte Automation » hello](media/automation-sec-configure-azure-runas-account/create-account-decline-create-runas-msg.png)
   >
   > <span data-ttu-id="2641a-162">En outre, étant donné que le principal du service hello n’est pas créée, rôle de collaborateur hello n’est pas affecté.</span><span class="sxs-lookup"><span data-stu-id="2641a-162">Additionally, because hello service principal is not created, hello Contributor role is not assigned.</span></span>
   >

7. <span data-ttu-id="2641a-163">Alors que Azure crée le compte d’automatisation hello, vous pouvez suivre la progression de hello sous **Notifications** à partir du menu de hello.</span><span class="sxs-lookup"><span data-stu-id="2641a-163">While Azure creates hello Automation account, you can track hello progress under **Notifications** from hello menu.</span></span>

### <a name="resources"></a><span data-ttu-id="2641a-164">Ressources</span><span class="sxs-lookup"><span data-stu-id="2641a-164">Resources</span></span>
<span data-ttu-id="2641a-165">Lorsque hello compte Automation a été créé, plusieurs ressources sont automatiquement créées pour vous.</span><span class="sxs-lookup"><span data-stu-id="2641a-165">When hello Automation account is successfully created, several resources are automatically created for you.</span></span> <span data-ttu-id="2641a-166">ressources de Hello sont résumées dans hello les deux tableaux suivants :</span><span class="sxs-lookup"><span data-stu-id="2641a-166">hello resources are summarized in hello following two tables:</span></span>

#### <a name="run-as-account-resources"></a><span data-ttu-id="2641a-167">Ressources de compte d’identification</span><span class="sxs-lookup"><span data-stu-id="2641a-167">Run As account resources</span></span>

| <span data-ttu-id="2641a-168">Ressource</span><span class="sxs-lookup"><span data-stu-id="2641a-168">Resource</span></span> | <span data-ttu-id="2641a-169">Description</span><span class="sxs-lookup"><span data-stu-id="2641a-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2641a-170">Runbook AzureAutomationTutorial</span><span class="sxs-lookup"><span data-stu-id="2641a-170">AzureAutomationTutorial Runbook</span></span> | <span data-ttu-id="2641a-171">Runbook graphique exemple qui montre comment tooauthenticate à l’aide de hello compte d’identification et obtient toutes les ressources du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="2641a-171">An example graphical runbook that demonstrates how tooauthenticate by using hello Run As account and gets all hello Resource Manager resources.</span></span> |
| <span data-ttu-id="2641a-172">Runbook AzureAutomationTutorialScript</span><span class="sxs-lookup"><span data-stu-id="2641a-172">AzureAutomationTutorialScript Runbook</span></span> | <span data-ttu-id="2641a-173">Un exemple de runbook PowerShell qui montre comment tooauthenticate à l’aide de hello compte d’identification et obtient toutes les ressources du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="2641a-173">An example PowerShell runbook that demonstrates how tooauthenticate by using hello Run As account and gets all hello Resource Manager resources.</span></span> |
| <span data-ttu-id="2641a-174">AzureRunAsCertificate</span><span class="sxs-lookup"><span data-stu-id="2641a-174">AzureRunAsCertificate</span></span> | <span data-ttu-id="2641a-175">ressource de certificat Hello qui est créé automatiquement lorsque vous créez un compte Automation ou que vous utilisez hello suite du script PowerShell pour un compte existant.</span><span class="sxs-lookup"><span data-stu-id="2641a-175">hello certificate asset that's automatically created when you create an Automation account or use hello following PowerShell script for an existing account.</span></span> <span data-ttu-id="2641a-176">certificat de Hello vous permet de tooauthenticate avec Azure afin que vous puissiez gérer les ressources Azure Resource Manager à partir de procédures opérationnelles.</span><span class="sxs-lookup"><span data-stu-id="2641a-176">hello certificate allows you tooauthenticate with Azure so that you can manage Azure Resource Manager resources from runbooks.</span></span> <span data-ttu-id="2641a-177">certificat de Hello a une durée de vie d’un an.</span><span class="sxs-lookup"><span data-stu-id="2641a-177">hello certificate has a one-year lifespan.</span></span> |
| <span data-ttu-id="2641a-178">AzureRunAsConnection</span><span class="sxs-lookup"><span data-stu-id="2641a-178">AzureRunAsConnection</span></span> | <span data-ttu-id="2641a-179">ressource de connexion Hello qui est créé automatiquement lorsque vous créez un compte Automation ou utilisez un script PowerShell de hello pour un compte existant.</span><span class="sxs-lookup"><span data-stu-id="2641a-179">hello connection asset that's automatically created when you create an Automation account or use hello PowerShell script for an existing account.</span></span> |

#### <a name="classic-run-as-account-resources"></a><span data-ttu-id="2641a-180">Ressources de compte d’identification Classic</span><span class="sxs-lookup"><span data-stu-id="2641a-180">Classic Run As account resources</span></span>

| <span data-ttu-id="2641a-181">Ressource</span><span class="sxs-lookup"><span data-stu-id="2641a-181">Resource</span></span> | <span data-ttu-id="2641a-182">Description</span><span class="sxs-lookup"><span data-stu-id="2641a-182">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2641a-183">Runbook AzureClassicAutomationTutorial</span><span class="sxs-lookup"><span data-stu-id="2641a-183">AzureClassicAutomationTutorial Runbook</span></span> | <span data-ttu-id="2641a-184">Exemple de runbook graphique qui obtient tous les ordinateurs virtuels de hello qui sont créés à l’aide du modèle de déploiement classique hello dans un abonnement à l’aide de hello classique compte d’identification (certificat), puis écrit l’état et le nom de machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="2641a-184">An example graphical runbook that gets all hello VMs that are created using hello classic deployment model in a subscription by using hello Classic Run As account (certificate), and then writes hello VM name and status.</span></span> |
| <span data-ttu-id="2641a-185">Runbook AzureClassicAutomationTutorialScript</span><span class="sxs-lookup"><span data-stu-id="2641a-185">AzureClassicAutomationTutorial Script Runbook</span></span> | <span data-ttu-id="2641a-186">Exemple de runbook PowerShell qui obtient tous les hello classiques machines virtuelles dans un abonnement à l’aide de hello classique compte d’identification (certificat), puis écritures hello état et le nom de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2641a-186">An example PowerShell runbook that gets all hello classic VMs in a subscription by using hello Classic Run As account (certificate), and then writes hello VM name and status.</span></span> |
| <span data-ttu-id="2641a-187">AzureClassicRunAsCertificate</span><span class="sxs-lookup"><span data-stu-id="2641a-187">AzureClassicRunAsCertificate</span></span> | <span data-ttu-id="2641a-188">ressource de certificat Hello créé automatiquement utiliser tooauthenticate avec Azure afin que vous puissiez gérer les ressources classiques Azure à partir de procédures opérationnelles.</span><span class="sxs-lookup"><span data-stu-id="2641a-188">hello automatically created certificate asset that you use tooauthenticate with Azure so that you can manage Azure classic resources from runbooks.</span></span> <span data-ttu-id="2641a-189">certificat de Hello a une durée de vie d’un an.</span><span class="sxs-lookup"><span data-stu-id="2641a-189">hello certificate has a one-year lifespan.</span></span> |
| <span data-ttu-id="2641a-190">AzureClassicRunAsConnection</span><span class="sxs-lookup"><span data-stu-id="2641a-190">AzureClassicRunAsConnection</span></span> | <span data-ttu-id="2641a-191">ressource de connexion créés automatiquement de Hello utiliser tooauthenticate avec Azure afin que vous puissiez gérer les ressources classiques Azure à partir de procédures opérationnelles.</span><span class="sxs-lookup"><span data-stu-id="2641a-191">hello automatically created connection asset that you use tooauthenticate with Azure so that you can manage Azure classic resources from runbooks.</span></span> |

## <a name="verify-run-as-authentication"></a><span data-ttu-id="2641a-192">Vérifier l’authentification d’identification</span><span class="sxs-lookup"><span data-stu-id="2641a-192">Verify Run As authentication</span></span>
<span data-ttu-id="2641a-193">Effectuer un tooconfirm de test peu que vous pouvez vous authentifier avec succès à l’aide de hello nouveau compte d’identification.</span><span class="sxs-lookup"><span data-stu-id="2641a-193">Perform a small test tooconfirm that you can successfully authenticate by using hello new Run As account.</span></span>

1. <span data-ttu-id="2641a-194">Bonjour portail Azure, ouvrez le compte Automation hello que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="2641a-194">In hello Azure portal, open hello Automation account that you created earlier.</span></span>

2. <span data-ttu-id="2641a-195">Cliquez sur hello **Runbooks** vignette tooopen hello liste des runbooks.</span><span class="sxs-lookup"><span data-stu-id="2641a-195">Click hello **Runbooks** tile tooopen hello list of runbooks.</span></span>

3. <span data-ttu-id="2641a-196">Sélectionnez hello **AzureAutomationTutorialScript** runbook, puis cliquez sur **Démarrer** toostart hello runbook.</span><span class="sxs-lookup"><span data-stu-id="2641a-196">Select hello **AzureAutomationTutorialScript** runbook, and then click **Start** toostart hello runbook.</span></span> <span data-ttu-id="2641a-197">Hello suivant des événements se produire :</span><span class="sxs-lookup"><span data-stu-id="2641a-197">hello following events occur:</span></span>
 * <span data-ttu-id="2641a-198">A [tâche du runbook](automation-runbook-execution.md) est créé, hello **travail** panneau s’affiche, et état de la tâche hello est affiché dans hello **récapitulatif** vignette.</span><span class="sxs-lookup"><span data-stu-id="2641a-198">A [runbook job](automation-runbook-execution.md) is created, hello **Job** blade is displayed, and hello job status is displayed in hello **Job Summary** tile.</span></span>
 * <span data-ttu-id="2641a-199">état de la tâche Hello commence en tant que **en file d’attente**, indiquant qu’il est en attente d’un runbook worker dans hello toobecome de cloud disponible.</span><span class="sxs-lookup"><span data-stu-id="2641a-199">hello job status begins as **Queued**, indicating that it is waiting for a runbook worker in hello cloud toobecome available.</span></span>
 * <span data-ttu-id="2641a-200">l’état de Hello devient **départ** lorsqu’un travailleur de revendications travail de hello.</span><span class="sxs-lookup"><span data-stu-id="2641a-200">hello status becomes **Starting** when a worker claims hello job.</span></span>
 * <span data-ttu-id="2641a-201">l’état de Hello devient **en cours d’exécution** lorsque hello runbook démarre l’exécution.</span><span class="sxs-lookup"><span data-stu-id="2641a-201">hello status becomes **Running** when hello runbook starts running.</span></span>
 * <span data-ttu-id="2641a-202">Lors de la tâche du runbook hello est terminée, vous devez voir un état de **terminé**.</span><span class="sxs-lookup"><span data-stu-id="2641a-202">When hello runbook job has finished running, you should see a status of **Completed**.</span></span>

       ![Security Principal Runbook Test](media/automation-sec-configure-azure-runas-account/job-summary-automationtutorialscript.png)
4. <span data-ttu-id="2641a-203">toosee hello les résultats détaillés de hello runbook, cliquez sur hello **sortie** vignette.</span><span class="sxs-lookup"><span data-stu-id="2641a-203">toosee hello detailed results of hello runbook, click hello **Output** tile.</span></span>  
<span data-ttu-id="2641a-204">Hello **sortie** panneau s’affiche, indiquant que runbook hello a authentifié et a renvoyé une liste de toutes les ressources disponibles dans le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="2641a-204">hello **Output** blade is displayed, showing that hello runbook has successfully authenticated and returned a list of all resources available in hello resource group.</span></span>

5. <span data-ttu-id="2641a-205">Fermer hello **sortie** panneau tooreturn toohello **récapitulatif** panneau.</span><span class="sxs-lookup"><span data-stu-id="2641a-205">Close hello **Output** blade tooreturn toohello **Job Summary** blade.</span></span>

6. <span data-ttu-id="2641a-206">Fermer hello **récapitulatif** lame et hello correspondant **AzureAutomationTutorialScript** panneau runbook.</span><span class="sxs-lookup"><span data-stu-id="2641a-206">Close hello **Job Summary** blade and hello corresponding **AzureAutomationTutorialScript** runbook blade.</span></span>

## <a name="verify-classic-run-as-authentication"></a><span data-ttu-id="2641a-207">Vérifier l’authentification d’identification Classic</span><span class="sxs-lookup"><span data-stu-id="2641a-207">Verify Classic Run As authentication</span></span>
<span data-ttu-id="2641a-208">Effectuer un petit semblables tests tooconfirm que vous pouvez vous authentifier avec succès à l’aide de hello classique compte d’identification.</span><span class="sxs-lookup"><span data-stu-id="2641a-208">Perform a similar small test tooconfirm that you can successfully authenticate by using hello new Classic Run As account.</span></span>

1. <span data-ttu-id="2641a-209">Bonjour portail Azure, ouvrez le compte Automation hello que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="2641a-209">In hello Azure portal, open hello Automation account that you created earlier.</span></span>

2. <span data-ttu-id="2641a-210">Cliquez sur hello **Runbooks** vignette tooopen hello liste des runbooks.</span><span class="sxs-lookup"><span data-stu-id="2641a-210">Click hello **Runbooks** tile tooopen hello list of runbooks.</span></span>

3. <span data-ttu-id="2641a-211">Sélectionnez hello **AzureClassicAutomationTutorialScript** runbook, puis cliquez sur **Démarrer** trop démarrer hello runbook.</span><span class="sxs-lookup"><span data-stu-id="2641a-211">Select hello **AzureClassicAutomationTutorialScript** runbook, and then click **Start** too start hello runbook.</span></span> <span data-ttu-id="2641a-212">Hello suivant des événements se produire :</span><span class="sxs-lookup"><span data-stu-id="2641a-212">hello following events occur:</span></span>

 * <span data-ttu-id="2641a-213">A [tâche du runbook](automation-runbook-execution.md) est créé, hello **travail** panneau s’affiche, et état de la tâche hello est affiché dans hello **récapitulatif** vignette.</span><span class="sxs-lookup"><span data-stu-id="2641a-213">A [runbook job](automation-runbook-execution.md) is created, hello **Job** blade is displayed, and hello job status is displayed in hello **Job Summary** tile.</span></span>
 * <span data-ttu-id="2641a-214">état de la tâche Hello commence en tant que **en file d’attente**, indiquant qu’il est en attente d’un runbook worker dans hello toobecome de cloud disponible.</span><span class="sxs-lookup"><span data-stu-id="2641a-214">hello job status begins as **Queued**, indicating that it is waiting for a runbook worker in hello cloud toobecome available.</span></span>
 * <span data-ttu-id="2641a-215">l’état de Hello devient **départ** lorsqu’un travailleur de revendications travail de hello.</span><span class="sxs-lookup"><span data-stu-id="2641a-215">hello status becomes **Starting** when a worker claims hello job.</span></span>
 * <span data-ttu-id="2641a-216">l’état de Hello devient **en cours d’exécution** lorsque hello runbook démarre l’exécution.</span><span class="sxs-lookup"><span data-stu-id="2641a-216">hello status becomes **Running** when hello runbook starts running.</span></span>
 * <span data-ttu-id="2641a-217">Lors de la tâche du runbook hello est terminée, vous devez voir un état de **terminé**.</span><span class="sxs-lookup"><span data-stu-id="2641a-217">When hello runbook job has finished running, you should see a status of **Completed**.</span></span>

    ![Test de Runbook du principal de sécurité](media/automation-sec-configure-azure-runas-account/job-summary-automationclassictutorialscript.png)<br>
4. <span data-ttu-id="2641a-219">toosee hello les résultats détaillés de hello runbook, cliquez sur hello **sortie** vignette.</span><span class="sxs-lookup"><span data-stu-id="2641a-219">toosee hello detailed results of hello runbook, click hello **Output** tile.</span></span>  
<span data-ttu-id="2641a-220">Hello **sortie** panneau s’affiche, indiquant que runbook hello a authentifié et retourné une liste de toutes les machines virtuelles classiques dans l’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="2641a-220">hello **Output** blade is displayed, showing that hello runbook has successfully authenticated and returned a list of all classic VMs in hello subscription.</span></span>

5. <span data-ttu-id="2641a-221">Fermer hello **sortie** panneau tooreturn toohello **récapitulatif** panneau.</span><span class="sxs-lookup"><span data-stu-id="2641a-221">Close hello **Output** blade tooreturn toohello **Job Summary** blade.</span></span>

6. <span data-ttu-id="2641a-222">Fermer hello **récapitulatif** lame et hello correspondant **AzureAutomationTutorialScript** panneau runbook.</span><span class="sxs-lookup"><span data-stu-id="2641a-222">Close hello **Job Summary** blade and hello corresponding **AzureAutomationTutorialScript** runbook blade.</span></span>

## <a name="managing-your-run-as-account"></a><span data-ttu-id="2641a-223">Gestion de votre compte d’identification</span><span class="sxs-lookup"><span data-stu-id="2641a-223">Managing your Run As account</span></span>
<span data-ttu-id="2641a-224">À un moment donné avant l’expiration de votre compte Automation, vous devez le certificat de hello toorenew.</span><span class="sxs-lookup"><span data-stu-id="2641a-224">At some point before your Automation account expires, you will need toorenew hello certificate.</span></span> <span data-ttu-id="2641a-225">Si vous pensez que ce compte d’identification hello a été compromise, vous pouvez supprimer et recréer.</span><span class="sxs-lookup"><span data-stu-id="2641a-225">If you believe that hello Run As account has been compromised, you can delete and re-create it.</span></span> <span data-ttu-id="2641a-226">Cette section explique comment tooperform ces opérations.</span><span class="sxs-lookup"><span data-stu-id="2641a-226">This section discusses how tooperform these operations.</span></span>

### <a name="self-signed-certificate-renewal"></a><span data-ttu-id="2641a-227">Renouvellement de certificat auto-signé</span><span class="sxs-lookup"><span data-stu-id="2641a-227">Self-signed certificate renewal</span></span>
<span data-ttu-id="2641a-228">Hello un certificat auto-signé que vous avez créé pour hello exécuter en tant que compte expire un an à partir de la date de hello de création.</span><span class="sxs-lookup"><span data-stu-id="2641a-228">hello self-signed certificate that you created for hello Run As account expires one year from hello date of creation.</span></span> <span data-ttu-id="2641a-229">Vous pouvez le renouveler à tout moment avant qu’il n’expire.</span><span class="sxs-lookup"><span data-stu-id="2641a-229">You can renew it at any time before it expires.</span></span> <span data-ttu-id="2641a-230">Lors du renouvellement, il certificat valide de hello actuelle est retenue tooensure que les runbooks qui sont en attente jusqu'à ou activement en cours d’exécution, et qui s’authentifient avec hello compte d’identification, ne sont pas affectés négativement.</span><span class="sxs-lookup"><span data-stu-id="2641a-230">When you renew it, hello current valid certificate is retained tooensure that any runbooks that are queued up or actively running, and that authenticate with hello Run As account, are not negatively affected.</span></span> <span data-ttu-id="2641a-231">certificat de Hello reste valide jusqu'à ce que sa date d’expiration.</span><span class="sxs-lookup"><span data-stu-id="2641a-231">hello certificate remains valid until its expiration date.</span></span>

> [!NOTE]
> <span data-ttu-id="2641a-232">Si vous avez configuré votre toouse de compte Automation s’exécuter en tant qu’un certificat émis par votre autorité de certification d’entreprise et que vous utilisez cette option, le certificat d’entreprise hello est remplacé par un certificat auto-signé.</span><span class="sxs-lookup"><span data-stu-id="2641a-232">If you have configured your Automation Run As account toouse a certificate issued by your enterprise certificate authority and you use this option, hello enterprise certificate will be replaced by a self-signed certificate.</span></span>

<span data-ttu-id="2641a-233">toorenew hello certificat, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="2641a-233">toorenew hello certificate, do hello following:</span></span>

1. <span data-ttu-id="2641a-234">Bonjour portail Azure, ouvrez le compte Automation de hello.</span><span class="sxs-lookup"><span data-stu-id="2641a-234">In hello Azure portal, open hello Automation account.</span></span>

2. <span data-ttu-id="2641a-235">Sur hello **compte Automation** panneau, Bonjour **compte propriétés** volet, sous **les paramètres de compte**, sélectionnez **exécuter en tant que comptes**.</span><span class="sxs-lookup"><span data-stu-id="2641a-235">On hello **Automation Account** blade, in hello **Account properties** pane, under **Account Settings**, select **Run As Accounts**.</span></span>

    ![Panneau des propriétés du compte Automation](media/automation-sec-configure-azure-runas-account/automation-account-properties-pane.png)
3. <span data-ttu-id="2641a-237">Sur hello **comptes d’identification** panneau des propriétés, sélectionnez soit hello d’identification de compte ou hello classique exécuter en tant que compte de certificat de hello toorenew pour.</span><span class="sxs-lookup"><span data-stu-id="2641a-237">On hello **Run As Accounts** properties blade, select either hello Run As account or hello Classic Run As account that you want toorenew hello certificate for.</span></span>

4. <span data-ttu-id="2641a-238">Sur hello **propriétés** panneau pourquoi le compte sélectionné, cliquez sur **renouveler certificat**.</span><span class="sxs-lookup"><span data-stu-id="2641a-238">On hello **Properties** blade for hello selected account, click **Renew certificate**.</span></span>

    ![Renouveler le certificat pour le compte d’identification](media/automation-sec-configure-azure-runas-account/automation-account-renew-runas-certificate.png)

5. <span data-ttu-id="2641a-240">Pendant le renouvellement de certificat de hello, vous pouvez suivre la progression de hello sous **Notifications** à partir du menu de hello.</span><span class="sxs-lookup"><span data-stu-id="2641a-240">While hello certificate is being renewed, you can track hello progress under **Notifications** from hello menu.</span></span>

### <a name="delete-a-run-as-or-classic-run-as-account"></a><span data-ttu-id="2641a-241">Supprimer un compte d’identification standard ou Classic</span><span class="sxs-lookup"><span data-stu-id="2641a-241">Delete a Run As or Classic Run As account</span></span>
<span data-ttu-id="2641a-242">Cette section décrit comment toodelete et recréer un compte d’identification ou classique exécuter en tant que.</span><span class="sxs-lookup"><span data-stu-id="2641a-242">This section describes how toodelete and re-create a Run As or Classic Run As account.</span></span> <span data-ttu-id="2641a-243">Lorsque vous effectuez cette action, hello compte Automation est conservée.</span><span class="sxs-lookup"><span data-stu-id="2641a-243">When you perform this action, hello Automation account is retained.</span></span> <span data-ttu-id="2641a-244">Après avoir supprimé un compte d’identification ou classique exécuter en tant que, vous pouvez le recréer dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2641a-244">After you delete a Run As or Classic Run As account, you can re-create it in hello Azure portal.</span></span>

1. <span data-ttu-id="2641a-245">Bonjour portail Azure, ouvrez le compte Automation de hello.</span><span class="sxs-lookup"><span data-stu-id="2641a-245">In hello Azure portal, open hello Automation account.</span></span>

2. <span data-ttu-id="2641a-246">Sur hello **compte Automation** lame, hello compte volet Propriétés, sélectionnez **exécuter en tant que comptes**.</span><span class="sxs-lookup"><span data-stu-id="2641a-246">On hello **Automation account** blade, in hello account properties pane, select **Run As Accounts**.</span></span>

3. <span data-ttu-id="2641a-247">Sur hello **comptes d’identification** panneau des propriétés, sélectionnez soit hello d’identification de compte ou classique exécuter en tant que le compte que vous souhaitez toodelete.</span><span class="sxs-lookup"><span data-stu-id="2641a-247">On hello **Run As Accounts** properties blade, select either hello Run As account or Classic Run As account that you want toodelete.</span></span> <span data-ttu-id="2641a-248">Ensuite, sous hello **propriétés** panneau pourquoi le compte sélectionné, cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="2641a-248">Then, on hello **Properties** blade for hello selected account, click **Delete**.</span></span>

 ![Supprimer un compte d’identification](media/automation-sec-configure-azure-runas-account/automation-account-delete-runas.png)

4. <span data-ttu-id="2641a-250">Lors de la suppression du compte de hello, vous pouvez suivre la progression de hello sous **Notifications** à partir du menu de hello.</span><span class="sxs-lookup"><span data-stu-id="2641a-250">While hello account is being deleted, you can track hello progress under **Notifications** from hello menu.</span></span>

5. <span data-ttu-id="2641a-251">Une fois que le compte de hello a été supprimé, vous pouvez recréer il sur hello **comptes d’identification** option de création du panneau des propriétés en sélectionnant hello **exécuter en tant que compte Azure**.</span><span class="sxs-lookup"><span data-stu-id="2641a-251">After hello account has been deleted, you can re-create it on hello **Run As Accounts** properties blade by selecting hello create option **Azure Run As Account**.</span></span>

 ![Recréez le compte d’identification Automation hello](media/automation-sec-configure-azure-runas-account/automation-account-create-runas.png)

### <a name="misconfiguration"></a><span data-ttu-id="2641a-253">Configuration incorrecte</span><span class="sxs-lookup"><span data-stu-id="2641a-253">Misconfiguration</span></span>
<span data-ttu-id="2641a-254">Certains éléments de configuration nécessaires pour toofunction de compte Exécuter en tant qu’ou classique en hello peuvent correctement ont été supprimés ou créés correctement lors de l’installation initiale.</span><span class="sxs-lookup"><span data-stu-id="2641a-254">Some configuration items necessary for hello Run As or Classic Run As account toofunction properly might have been deleted or created improperly during initial setup.</span></span> <span data-ttu-id="2641a-255">éléments de Hello sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="2641a-255">hello items include:</span></span>

* <span data-ttu-id="2641a-256">Ressource de certificat</span><span class="sxs-lookup"><span data-stu-id="2641a-256">Certificate asset</span></span>
* <span data-ttu-id="2641a-257">Ressource de connexion</span><span class="sxs-lookup"><span data-stu-id="2641a-257">Connection asset</span></span>
* <span data-ttu-id="2641a-258">Compte d’identification a été supprimé de rôle de collaborateur hello</span><span class="sxs-lookup"><span data-stu-id="2641a-258">Run As account has been removed from hello contributor role</span></span>
* <span data-ttu-id="2641a-259">Principal du service ou application dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="2641a-259">Service principal or application in Azure AD</span></span>

<span data-ttu-id="2641a-260">Hello précédent et les autres instances d’une configuration incorrecte, hello compte Automation détecte hello modifie et affiche l’état *incomplet* sur hello **comptes d’identification** panneau des propriétés pour hello compte.</span><span class="sxs-lookup"><span data-stu-id="2641a-260">In hello preceding and other instances of misconfiguration, hello Automation account detects hello changes and displays a status of *Incomplete* on hello **Run As Accounts** properties blade for hello account.</span></span>

![État Incomplet pour la configuration du compte d’identification](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config.png)

<span data-ttu-id="2641a-262">Lorsque vous sélectionnez le compte d’identification hello, hello compte **propriétés** volet affiche hello message d’erreur suivant :</span><span class="sxs-lookup"><span data-stu-id="2641a-262">When you select hello Run As account, hello account **Properties** pane displays hello following error message:</span></span>

![Message d’avertissement Incomplet pour la configuration du compte d’identification](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config-msg.png)<span data-ttu-id="2641a-264">.</span><span class="sxs-lookup"><span data-stu-id="2641a-264">.</span></span>

<span data-ttu-id="2641a-265">Vous pouvez rapidement résoudre ces problèmes de compte Exécuter en tant qu’à supprimer et recréer le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="2641a-265">You can quickly resolve these Run As account issues by deleting and re-creating hello account.</span></span>

## <a name="update-your-automation-account-by-using-powershell"></a><span data-ttu-id="2641a-266">Mise à jour de votre compte Automation à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="2641a-266">Update your Automation account by using PowerShell</span></span>
<span data-ttu-id="2641a-267">Vous pouvez utiliser PowerShell tooupdate votre compte Automation existant si :</span><span class="sxs-lookup"><span data-stu-id="2641a-267">You can use PowerShell tooupdate your existing Automation account if:</span></span>

* <span data-ttu-id="2641a-268">Vous créez un compte Automation mais refusez toocreate hello exécuter en tant que compte.</span><span class="sxs-lookup"><span data-stu-id="2641a-268">You create an Automation account but decline toocreate hello Run As account.</span></span>
* <span data-ttu-id="2641a-269">Vous utilisez déjà une ressources de gestionnaire de ressources toomanage compte Automation et que vous souhaitez tooupdate hello tooinclude hello exécuter en tant que compte pour l’authentification de runbook.</span><span class="sxs-lookup"><span data-stu-id="2641a-269">You already use an Automation account toomanage Resource Manager resources and you want tooupdate hello account tooinclude hello Run As account for runbook authentication.</span></span>
* <span data-ttu-id="2641a-270">Vous utilisez déjà une Automation compte toomanage les ressources classiques et tooupdate il toouse hello classique compte d’identification au lieu de créer un compte et la migration de votre tooit runbooks et ressources.</span><span class="sxs-lookup"><span data-stu-id="2641a-270">You already use an Automation account toomanage classic resources and you want tooupdate it toouse hello Classic Run As account instead of creating a new account and migrating your runbooks and assets tooit.</span></span>   
* <span data-ttu-id="2641a-271">Vous souhaitez que toocreate une identification et classique compte d’identification à l’aide d’un certificat émis par votre autorité de certification d’entreprise (CA).</span><span class="sxs-lookup"><span data-stu-id="2641a-271">You want toocreate a Run As and a Classic Run As account by using a certificate issued by your enterprise certification authority (CA).</span></span>

<span data-ttu-id="2641a-272">script de Hello a hello suivant des conditions préalables :</span><span class="sxs-lookup"><span data-stu-id="2641a-272">hello script has hello following prerequisites:</span></span>

* <span data-ttu-id="2641a-273">script de Hello peut exécuter uniquement sur Windows 10 et Windows Server 2016 avec des modules Azure Resource Manager 2.01 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="2641a-273">hello script can be run only on Windows 10 and Windows Server 2016 with Azure Resource Manager modules 2.01 and later.</span></span> <span data-ttu-id="2641a-274">Il n’est pas pris en charge dans les versions antérieures de Windows.</span><span class="sxs-lookup"><span data-stu-id="2641a-274">It is not supported on earlier versions of Windows.</span></span>
* <span data-ttu-id="2641a-275">Azure PowerShell 1.0 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="2641a-275">Azure PowerShell 1.0 and later.</span></span> <span data-ttu-id="2641a-276">Pour plus d’informations sur la mise en production hello PowerShell 1.0, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2641a-276">For information about hello PowerShell 1.0 release, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="2641a-277">Un compte Automation, qui est référencé en tant que valeur hello pour hello *– AutomationAccountName* et *- ApplicationDisplayName* paramètres Bonjour suite du script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2641a-277">An Automation account, which is referenced as hello value for hello *–AutomationAccountName* and *-ApplicationDisplayName* parameters in hello following PowerShell script.</span></span>

<span data-ttu-id="2641a-278">les valeurs tooget hello pour *SubscriptionID*, *ResourceGroup*, et *AutomationAccountName*, qui sont des paramètres requis pour les scripts de hello, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="2641a-278">tooget hello values for *SubscriptionID*, *ResourceGroup*, and *AutomationAccountName*, which are required parameters for hello scripts, do hello following:</span></span>
1. <span data-ttu-id="2641a-279">Dans l’hello portail Azure, sélectionnez votre compte Automation sur hello **compte Automation** panneau, puis sélectionnez **tous les paramètres**.</span><span class="sxs-lookup"><span data-stu-id="2641a-279">In hello Azure portal, select your Automation account on hello **Automation account** blade, and then select **All settings**.</span></span> 
2. <span data-ttu-id="2641a-280">Sur hello **tous les paramètres** panneau, sous **les paramètres de compte**, sélectionnez **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="2641a-280">On hello **All settings** blade, under **Account Settings**, select **Properties**.</span></span> 
3. <span data-ttu-id="2641a-281">Notez les valeurs hello sur hello **propriétés** panneau.</span><span class="sxs-lookup"><span data-stu-id="2641a-281">Note hello values on hello **Properties** blade.</span></span>

![Panneau de Hello Automation compte « Propriétés »](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

### <a name="create-a-run-as-account-powershell-script"></a><span data-ttu-id="2641a-283">Créer le script PowerShell d’un compte d’identification</span><span class="sxs-lookup"><span data-stu-id="2641a-283">Create a Run As account PowerShell script</span></span>
<span data-ttu-id="2641a-284">Ce script PowerShell prend en charge hello suivant configurations :</span><span class="sxs-lookup"><span data-stu-id="2641a-284">This PowerShell script includes support for hello following configurations:</span></span>

* <span data-ttu-id="2641a-285">Créez un compte d’identification à l’aide d’un certificat auto-signé.</span><span class="sxs-lookup"><span data-stu-id="2641a-285">Create a Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="2641a-286">Créez un compte d’identification standard et un compte d’identification Classic à l’aide d’un certificat auto-signé.</span><span class="sxs-lookup"><span data-stu-id="2641a-286">Create a Run As account and a Classic Run As account by using a self-signed certificate.</span></span>
* <span data-ttu-id="2641a-287">Créez un compte d’identification standard et un compte d’identification Classic à l’aide d’un certificat d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="2641a-287">Create a Run As account and a Classic Run As account by using an enterprise certificate.</span></span>
* <span data-ttu-id="2641a-288">Créer un compte d’identification et classique compte d’identification à l’aide d’un certificat auto-signé Bonjour cloud d’Azure Government.</span><span class="sxs-lookup"><span data-stu-id="2641a-288">Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud.</span></span>

<span data-ttu-id="2641a-289">En fonction de l’option de configuration hello sélectionnée, le script de hello crée hello éléments suivants.</span><span class="sxs-lookup"><span data-stu-id="2641a-289">Depending on hello configuration option you select, hello script creates hello following items.</span></span>

<span data-ttu-id="2641a-290">**Pour les comptes d’identification :**</span><span class="sxs-lookup"><span data-stu-id="2641a-290">**For Run As accounts:**</span></span>

* <span data-ttu-id="2641a-291">Crée un Azure AD application toobe exporté avec soit hello auto-signé ou clé publique du certificat enterprise, crée un compte de principal du service pour l’application hello dans Azure AD, et assigne hello compte hello dans votre rôle de collaborateur abonnement.</span><span class="sxs-lookup"><span data-stu-id="2641a-291">Creates an Azure AD application toobe exported with either hello self-signed or enterprise certificate public key, creates a service principal account for hello application in Azure AD, and assigns hello Contributor role for hello account in your current subscription.</span></span> <span data-ttu-id="2641a-292">Vous pouvez modifier ce paramètre tooOwner ou tout autre rôle.</span><span class="sxs-lookup"><span data-stu-id="2641a-292">You can change this setting tooOwner or any other role.</span></span> <span data-ttu-id="2641a-293">Pour plus d’informations, voir [Contrôle d’accès en fonction du rôle dans Azure Automation](automation-role-based-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="2641a-293">For more information, see [Role-based access control in Azure Automation](automation-role-based-access-control.md).</span></span>
* <span data-ttu-id="2641a-294">Crée une ressource de certificat Automation nommée *AzureRunAsCertificate* Bonjour spécifié le compte Automation.</span><span class="sxs-lookup"><span data-stu-id="2641a-294">Creates an Automation certificate asset named *AzureRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="2641a-295">ressource de certificat Hello conserve la clé privée hello certificat utilisé par l’application hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2641a-295">hello certificate asset holds hello certificate private key that's used by hello Azure AD application.</span></span>
* <span data-ttu-id="2641a-296">Crée une ressource de connexion d’Automation nommée *AzureRunAsConnection* Bonjour spécifié le compte Automation.</span><span class="sxs-lookup"><span data-stu-id="2641a-296">Creates an Automation connection asset named *AzureRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="2641a-297">ressource de connexion Hello conserve hello applicationId, tenantId, ID d’abonnement et l’empreinte numérique du certificat.</span><span class="sxs-lookup"><span data-stu-id="2641a-297">hello connection asset holds hello applicationId, tenantId, subscriptionId, and certificate thumbprint.</span></span>

<span data-ttu-id="2641a-298">**Pour les comptes d’identification Classic :**</span><span class="sxs-lookup"><span data-stu-id="2641a-298">**For Classic Run As accounts:**</span></span>

* <span data-ttu-id="2641a-299">Crée une ressource de certificat Automation nommée *AzureClassicRunAsCertificate* Bonjour spécifié le compte Automation.</span><span class="sxs-lookup"><span data-stu-id="2641a-299">Creates an Automation certificate asset named *AzureClassicRunAsCertificate* in hello specified Automation account.</span></span> <span data-ttu-id="2641a-300">ressource de certificat Hello conserve la clé privée du certificat hello utilisé par le certificat de gestion hello.</span><span class="sxs-lookup"><span data-stu-id="2641a-300">hello certificate asset holds hello certificate private key used by hello management certificate.</span></span>
* <span data-ttu-id="2641a-301">Crée une ressource de connexion d’Automation nommée *AzureClassicRunAsConnection* Bonjour spécifié le compte Automation.</span><span class="sxs-lookup"><span data-stu-id="2641a-301">Creates an Automation connection asset named *AzureClassicRunAsConnection* in hello specified Automation account.</span></span> <span data-ttu-id="2641a-302">ressource de connexion Hello conserve hello abonnement nom, ID d’abonnement et nom de ressource de certificat.</span><span class="sxs-lookup"><span data-stu-id="2641a-302">hello connection asset holds hello subscription name, subscriptionId, and certificate asset name.</span></span>

>[!NOTE]
> <span data-ttu-id="2641a-303">Si vous sélectionnez l’option de création d’un compte classique exécuter en tant qu’après l’exécution de script de hello, téléchargement hello publique magasin de certificats de gestion de toohello (extension de nom de fichier .cer) pour l’abonnement de hello que hello compte Automation a été créé dans.</span><span class="sxs-lookup"><span data-stu-id="2641a-303">If you select either option for creating a Classic Run As account, after hello script is executed, upload hello public certificate (.cer file name extension) toohello management store for hello subscription that hello Automation account was created in.</span></span>
> 

<span data-ttu-id="2641a-304">tooexecute hello script et télécharger le certificat de hello, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="2641a-304">tooexecute hello script and upload hello certificate, do hello following:</span></span>

1. <span data-ttu-id="2641a-305">Enregistrez hello script suivant sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="2641a-305">Save hello following script on your computer.</span></span> <span data-ttu-id="2641a-306">Dans cet exemple, enregistrez-le sous le nom de fichier hello *New-RunAsAccount.ps1*.</span><span class="sxs-lookup"><span data-stu-id="2641a-306">In this example, save it with hello filename *New-RunAsAccount.ps1*.</span></span>

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
        if (!(($AzureRMProfileVersion.Major -ge 2 -and $AzureRMProfileVersion.Minor -ge 1) -or ($AzureRMProfileVersion.Major -gt 2)))
        {
           Write-Error -Message "Please install hello latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
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
        $SubscriptionName = $subscription.Subscription.SubscriptionName
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. <span data-ttu-id="2641a-307">Sur votre ordinateur, cliquez sur **Démarrer**, puis démarrez **Windows PowerShell** avec des droits de l’utilisateur élevés.</span><span class="sxs-lookup"><span data-stu-id="2641a-307">On your computer, click **Start**, and then start **Windows PowerShell** with elevated user rights.</span></span>

3. <span data-ttu-id="2641a-308">À partir de hello élevé PowerShell interpréteur de commandes, accédez toohello dossier qui contient le script hello créé à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="2641a-308">From hello elevated PowerShell command-line shell, go toohello folder that contains hello script you created in step 1.</span></span>

4. <span data-ttu-id="2641a-309">Exécuter le script de hello à l’aide des valeurs de paramètre hello pour configuration hello que vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="2641a-309">Execute hello script by using hello parameter values for hello configuration you require.</span></span>

    <span data-ttu-id="2641a-310">**Créer un compte d’identification à l’aide d’un certificat auto-signé**</span><span class="sxs-lookup"><span data-stu-id="2641a-310">**Create a Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    <span data-ttu-id="2641a-311">**Créer un compte d’identification standard et un compte d’identification Classic à l’aide d’un certificat auto-signé**</span><span class="sxs-lookup"><span data-stu-id="2641a-311">**Create a Run As account and a Classic Run As account by using a self-signed certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    <span data-ttu-id="2641a-312">**Créer un compte d’identification standard et un compte d’identification Classic à l’aide d’un certificat d’entreprise**</span><span class="sxs-lookup"><span data-stu-id="2641a-312">**Create a Run As account and a Classic Run As account by using an enterprise certificate**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    <span data-ttu-id="2641a-313">**Créer un compte d’identification et classique compte d’identification à l’aide d’un certificat auto-signé Bonjour cloud d’Azure Government**</span><span class="sxs-lookup"><span data-stu-id="2641a-313">**Create a Run As account and a Classic Run As account by using a self-signed certificate in hello Azure Government cloud**</span></span>  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > <span data-ttu-id="2641a-314">Après l’exécution de script de hello, vous serez invité à tooauthenticate avec Azure.</span><span class="sxs-lookup"><span data-stu-id="2641a-314">After hello script has executed, you will be prompted tooauthenticate with Azure.</span></span> <span data-ttu-id="2641a-315">Connectez-vous avec un compte qui est membre du rôle Administrateurs d’abonnement hello et coadministrateur de l’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="2641a-315">Sign in with an account that is a member of hello subscription administrators role and co-administrator of hello subscription.</span></span>
    >
    >

<span data-ttu-id="2641a-316">Une fois le script de hello a été exécutée correctement, notez hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="2641a-316">After hello script has executed successfully, note hello following:</span></span>
* <span data-ttu-id="2641a-317">Si vous avez créé un classique compte d’identification avec un certificat auto-signé de public (fichier .cer), le script de hello crée et enregistre toohello dossier des fichiers temporaires sur votre ordinateur sous le profil utilisateur hello *%USERPROFILE%\AppData\Local\Temp*, que vous avez utilisé la session de PowerShell tooexecute hello.</span><span class="sxs-lookup"><span data-stu-id="2641a-317">If you created a Classic Run As account with a self-signed public certificate (.cer file), hello script creates and saves it toohello temporary files folder on your computer under hello user profile *%USERPROFILE%\AppData\Local\Temp*, which you used tooexecute hello PowerShell session.</span></span>
* <span data-ttu-id="2641a-318">Si vous avez créé un compte d’identification Classic avec un certificat public d’entreprise (fichier .cer), utilisez ce certificat.</span><span class="sxs-lookup"><span data-stu-id="2641a-318">If you created a Classic Run As account with an enterprise public certificate (.cer file), use this certificate.</span></span> <span data-ttu-id="2641a-319">Suivez les instructions de hello pour [téléchargement un toohello de certificat d’API de gestion portail Azure classic](../azure-api-management-certs.md), puis validez de configuration des informations d’identification hello avec les ressources de gestion des services à l’aide de hello [exemple de code tooauthenticate avec le Service de gestion des ressources](#sample-code-to-authenticate-with-service-management-resources).</span><span class="sxs-lookup"><span data-stu-id="2641a-319">Follow hello instructions for [uploading a management API certificate toohello Azure classic portal](../azure-api-management-certs.md), and then validate hello credential configuration with Service Management resources by using hello [sample code tooauthenticate with Service Management Resources](#sample-code-to-authenticate-with-service-management-resources).</span></span> 
* <span data-ttu-id="2641a-320">Si vous l’avez fait *pas* créer classique compte d’identification, de s’authentifier auprès des ressources du Gestionnaire de ressources et de valider la configuration des informations d’identification hello à l’aide de hello [exemple de code pour s’authentifier auprès de gestion des services ressources](#sample-code-to-authenticate-with-resource-manager-resources).</span><span class="sxs-lookup"><span data-stu-id="2641a-320">If you did *not* create a Classic Run As account, authenticate with Resource Manager resources and validate hello credential configuration by using hello [sample code for authenticating with Service Management resources](#sample-code-to-authenticate-with-resource-manager-resources).</span></span>

## <a name="sample-code-tooauthenticate-with-resource-manager-resources"></a><span data-ttu-id="2641a-321">Tooauthenticate de code d’exemple avec des ressources du Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="2641a-321">Sample code tooauthenticate with Resource Manager resources</span></span>
<span data-ttu-id="2641a-322">Vous pouvez utiliser suivante hello mis à jour exemple de code, obtenue à partir de hello *AzureAutomationTutorialScript* exemple de runbook, tooauthenticate à l’aide des ressources de gestionnaire de ressources de toomanage hello exécuter en tant que compte avec les procédures opérationnelles.</span><span class="sxs-lookup"><span data-stu-id="2641a-322">You can use hello following updated sample code, taken from hello *AzureAutomationTutorialScript* example runbook, tooauthenticate by using hello Run As account toomanage Resource Manager resources with your runbooks.</span></span>

    $connectionName = "AzureRunAsConnection"
    $SubId = Get-AutomationVariable -Name 'SubscriptionId'
    try
    {
       # Get hello connection "AzureRunAsConnection "
       $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

       "Signing in tooAzure..."
       Add-AzureRmAccount `
         -ServicePrincipal `
         -TenantId $servicePrincipalConnection.TenantId `
         -ApplicationId $servicePrincipalConnection.ApplicationId `
         -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
       "Setting context tooa specific subscription"     
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

<span data-ttu-id="2641a-323">toohelp vous tooeasily de travail entre plusieurs abonnements, script de hello inclut deux lignes supplémentaires de code qui prennent en charge le référencement d’un contexte de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="2641a-323">toohelp you tooeasily work between multiple subscriptions, hello script includes two additional lines of code that support referencing a subscription context.</span></span> <span data-ttu-id="2641a-324">Une ressource de variable nommée *SubscriptionId* contient hello des ID d’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="2641a-324">A variable asset named *SubscriptionId* contains hello ID of hello subscription.</span></span> <span data-ttu-id="2641a-325">Après avoir hello `Add-AzureRmAccount` instruction de l’applet de commande, hello [ `Set-AzureRmContext` ](/powershell/module/azurerm.profile/set-azurermcontext) applet de commande est établi avec le jeu de paramètres hello *- SubscriptionId*.</span><span class="sxs-lookup"><span data-stu-id="2641a-325">After hello `Add-AzureRmAccount` cmdlet statement, hello [`Set-AzureRmContext`](/powershell/module/azurerm.profile/set-azurermcontext) cmdlet is stated with hello parameter set *-SubscriptionId*.</span></span> <span data-ttu-id="2641a-326">Si le nom de la variable hello est trop générique, vous pouvez réviser tooinclude un préfixe ou utiliser un autre toomake de convention d’affectation de noms il tooidentify plus facile.</span><span class="sxs-lookup"><span data-stu-id="2641a-326">If hello variable name is too generic, you can revise it tooinclude a prefix or use another naming convention toomake it easier tooidentify.</span></span> <span data-ttu-id="2641a-327">Vous pouvez également utiliser le jeu de paramètres hello *- SubscriptionName* au lieu de *- SubscriptionId* avec une ressource de variable correspondante.</span><span class="sxs-lookup"><span data-stu-id="2641a-327">Alternatively, you can use hello parameter set *-SubscriptionName* instead of *-SubscriptionId* with a corresponding variable asset.</span></span>

<span data-ttu-id="2641a-328">Hello applet de commande que vous utilisez pour l’authentification dans les runbook hello, `Add-AzureRmAccount`, utilise hello *ServicePrincipalCertificate* jeu de paramètres.</span><span class="sxs-lookup"><span data-stu-id="2641a-328">hello cmdlet that you use for authenticating in hello runbook, `Add-AzureRmAccount`, uses hello *ServicePrincipalCertificate* parameter set.</span></span> <span data-ttu-id="2641a-329">Il s’authentifie à l’aide du certificat hello service principal, pas hello informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="2641a-329">It authenticates by using hello service principal certificate, not hello user credentials.</span></span>

## <a name="sample-code-tooauthenticate-with-service-management-resources"></a><span data-ttu-id="2641a-330">Tooauthenticate de code d’exemple avec les ressources de gestion des services</span><span class="sxs-lookup"><span data-stu-id="2641a-330">Sample code tooauthenticate with Service Management resources</span></span>
<span data-ttu-id="2641a-331">Vous pouvez utiliser hello après mise à jour des exemples de code provient de hello *AzureClassicAutomationTutorialScript* exemple de runbook, tooauthenticate à l’aide de hello classique exécuter en tant que compte toomanage ressources classiques avec votre procédures opérationnelles.</span><span class="sxs-lookup"><span data-stu-id="2641a-331">You can use hello following updated sample code, which is taken from hello *AzureClassicAutomationTutorialScript* example runbook, tooauthenticate by using hello Classic Run As account toomanage classic resources with your runbooks.</span></span>

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get hello connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate tooAzure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in hello Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting hello certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in hello Automation account."
    }

    Write-Verbose "Authenticating tooAzure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID

## <a name="next-steps"></a><span data-ttu-id="2641a-332">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2641a-332">Next steps</span></span>
* [<span data-ttu-id="2641a-333">Objets application et principal du service dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="2641a-333">Application and service principal objects in Azure AD</span></span>](../active-directory/active-directory-application-objects.md)
* [<span data-ttu-id="2641a-334">Contrôle d’accès en fonction du rôle dans Azure Automation</span><span class="sxs-lookup"><span data-stu-id="2641a-334">Role-based access control in Azure Automation</span></span>](automation-role-based-access-control.md)
* [<span data-ttu-id="2641a-335">Vue d’ensemble des certificats pour Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="2641a-335">Certificates overview for Azure Cloud Services</span></span>](../cloud-services/cloud-services-certs-create.md)
