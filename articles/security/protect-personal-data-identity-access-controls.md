---
title: "les données personnelles aaaProtect avec des contrôles d’accès et des identités Azure | Documents Microsoft"
description: "À l’aide d’Azure toohelp de contrôles identités et des accès, vous protégez vos données personnelles"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 3132c2af25f86662668e5b555eab1d81de7f2e6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-and-multi-factor-authentication-protect-personal-data-with-identity-and-access-controls"></a><span data-ttu-id="780d7-103">Azure Active Directory et Multi-Factor Authentication : protéger les données personnelles avec des contrôles d’accès et d’identité</span><span class="sxs-lookup"><span data-stu-id="780d7-103">Azure Active Directory and Multi-Factor Authentication: Protect personal data with identity and access controls</span></span>

<span data-ttu-id="780d7-104">Cet article fournit des informations et des procédures que vous pouvez utiliser les données personnelles tooprotect via les services et les fonctionnalités de sécurité de l’authentification Azure Active Directory et de plusieurs facteurs.</span><span class="sxs-lookup"><span data-stu-id="780d7-104">This article provides information and procedures you can use tooprotect personal data using Azure Active Directory and Multi-factor authentication security features and services.</span></span>

## <a name="scenario"></a><span data-ttu-id="780d7-105">Scénario</span><span class="sxs-lookup"><span data-stu-id="780d7-105">Scenario</span></span>

<span data-ttu-id="780d7-106">Une société de croisière volumineux en hello États-Unis, étend ses itinéraires de toooffer d’opérations dans hello Méditerranée, Adriatique et mer Baltique, ainsi que hello britanniques.</span><span class="sxs-lookup"><span data-stu-id="780d7-106">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, Adriatic, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="780d7-107">toosupport ces efforts, elle a acquis plusieurs lignes croisière plus petits exercées en Italie, Allemagne, Danemark et hello Royaume-Uni</span><span class="sxs-lookup"><span data-stu-id="780d7-107">toosupport those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and hello U.K.</span></span> 

<span data-ttu-id="780d7-108">la société de Hello utilise des données d’entreprise de Microsoft Azure toostore dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="780d7-108">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="780d7-109">Ces dernières incluent des informations d’identification personnelle telles que les noms, les adresses, les numéros de téléphone et les informations de carte de crédit de sa base de clients globale.</span><span class="sxs-lookup"><span data-stu-id="780d7-109">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information of its global customer base.</span></span> <span data-ttu-id="780d7-110">Il inclut également des informations de ressources humaines traditionnelles telles que les adresses et numéros de téléphone, numéros d’identification de taxe médicales plus d’informations sur les employés de la société dans tous les emplacements.</span><span class="sxs-lookup"><span data-stu-id="780d7-110">It also includes traditional Human Resources information such as addresses, phone numbers, tax identification numbers and medical information about company employees in all locations.</span></span> <span data-ttu-id="780d7-111">ligne de croisière Hello gère également les bases de données volumineuses de membres du programme de récompense et fidélité qui inclut des informations personnelles tootrack des relations avec les clients en cours et passées.</span><span class="sxs-lookup"><span data-stu-id="780d7-111">hello cruise line also maintains a large database of reward and loyalty program members that includes personal information tootrack relationships with current and past customers.</span></span>

<span data-ttu-id="780d7-112">Réseau de hello accès employés de l’entreprise à partir de sites distants et les agents de voyage société hello situés dans Bonjour tout le monde ont accès aux ressources de l’entreprise toosome.</span><span class="sxs-lookup"><span data-stu-id="780d7-112">Corporate employees access hello network from hello company’s remote offices and travel agents located around hello world have access toosome company resources.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="780d7-113">Définition du problème</span><span class="sxs-lookup"><span data-stu-id="780d7-113">Problem statement</span></span>

<span data-ttu-id="780d7-114">société de Hello doit protection hello des employés et les clients des données personnelles à partir des attaquants qui toouse compromis identités toogain accèdent.</span><span class="sxs-lookup"><span data-stu-id="780d7-114">hello company must protect hello privacy of customers’ and employees’ personal data from attackers seeking toouse compromised identities toogain access.</span></span> <span data-ttu-id="780d7-115">Ils doivent également vous assurer que toopersonal accès aux données par les utilisateurs légitimes sont limitées à ceux qui en ont besoin toodo leur travail.</span><span class="sxs-lookup"><span data-stu-id="780d7-115">They also must ensure that access toopersonal data by legitimate users is restricted to only those who need it toodo their jobs.</span></span>

## <a name="company-goal"></a><span data-ttu-id="780d7-116">Objectif de l’entreprise</span><span class="sxs-lookup"><span data-stu-id="780d7-116">Company goal</span></span>

<span data-ttu-id="780d7-117">objectif de l’entreprise Hello est contrôlé tooensure qui accèdent aux données de toopersonal.</span><span class="sxs-lookup"><span data-stu-id="780d7-117">hello company’s goal is tooensure that access toopersonal data is strictly controlled.</span></span> <span data-ttu-id="780d7-118">Il est essentiel que les identités des utilisateurs à accéder à des données toopersonal soit protégé par l’authentification forte.</span><span class="sxs-lookup"><span data-stu-id="780d7-118">It is essential that identities of users with access toopersonal data be protected by strong authentication.</span></span> <span data-ttu-id="780d7-119">Une stratégie de [privilège minimum] (https://en.wikipedia.org/wiki/Principle_of_least_privilege) doit être appliquée afin que les utilisateurs légitimes ont seul niveau hello d’accès dont ils ont besoin et pas plus.</span><span class="sxs-lookup"><span data-stu-id="780d7-119">A policy of [least privilege] (https://en.wikipedia.org/wiki/Principle_of_least_privilege) must be enforced so that legitimate users have only hello level of  access they need, and no more.</span></span>

## <a name="solutions"></a><span data-ttu-id="780d7-120">Solutions</span><span class="sxs-lookup"><span data-stu-id="780d7-120">Solutions</span></span>

<span data-ttu-id="780d7-121">Microsoft Azure fournit des outils de gestion des identités et des accès toohelp sociétés contrôler l’accès tooresources qui contiennent des données personnelles.</span><span class="sxs-lookup"><span data-stu-id="780d7-121">Microsoft Azure provides identity and access management tools toohelp companies control who has access tooresources that contain personal data.</span></span>

### <a name="azure-active-directory"></a><span data-ttu-id="780d7-122">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="780d7-122">Azure Active Directory</span></span>

<span data-ttu-id="780d7-123">[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) (AAD) gère les identités et contrôle l’accès tooAzure ainsi que les autres localement et autres ressources de cloud, les données et les applications.</span><span class="sxs-lookup"><span data-stu-id="780d7-123">[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) (AAD) manages identities and controls access tooAzure as well as other on-premises and other cloud resources, data, and applications.</span></span> <span data-ttu-id="780d7-124">[Azure Active Directory Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access) aide les administrateurs Azure toominimize hello différents aux personnes qui ont accès toocertain plus d’informations, telles que les données personnelles.</span><span class="sxs-lookup"><span data-stu-id="780d7-124">[Azure Active Directory Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access) helps Azure administrators toominimize hello number of people who have access toocertain information such as personal data.</span></span> <span data-ttu-id="780d7-125">Il leur permet de toodiscover, restreindre et surveiller des identités privilégiées et leurs accès tooresources et tooassign temporaire, juste à temps (JIT) des droits d’administration tooeligible les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="780d7-125">It enables them toodiscover, restrict, and monitor privileged identities and their access tooresources, and tooassign temporary, Just-In-Time (JIT) administrative rights tooeligible users.</span></span> <span data-ttu-id="780d7-126">Il fournit également des informations sur les personnes dotées de privilèges Administrateur AAD.</span><span class="sxs-lookup"><span data-stu-id="780d7-126">It also provides insight into those who have AAD administrative privileges.</span></span>

<span data-ttu-id="780d7-127">Hello les activités liées à l’utilisation de AAD PIM incluent :</span><span class="sxs-lookup"><span data-stu-id="780d7-127">hello activities involved in using AAD PIM include:</span></span>

- <span data-ttu-id="780d7-128">Activation de Privileged Identity Management pour votre annuaire</span><span class="sxs-lookup"><span data-stu-id="780d7-128">Enabling Privileged Identity Management for your directory</span></span>

- <span data-ttu-id="780d7-129">À l’aide des informations importantes Privileged Identity Management Administration du tableau de bord toosee un coup de œil</span><span class="sxs-lookup"><span data-stu-id="780d7-129">Using Privileged Identity Management admin dashboard toosee important information at a glance</span></span>

- <span data-ttu-id="780d7-130">Gestion des identités hello privilégié (administrateurs) en ajoutant ou supprimant le rôle d’administrateurs permanents ou éligibles tooeach</span><span class="sxs-lookup"><span data-stu-id="780d7-130">Managing hello privileged identities (administrators) by adding or removing permanent or eligible administrators tooeach role</span></span>

- <span data-ttu-id="780d7-131">Configurer les paramètres d’activation de rôle hello</span><span class="sxs-lookup"><span data-stu-id="780d7-131">Configuring hello role activation settings</span></span>

- <span data-ttu-id="780d7-132">Activation des rôles</span><span class="sxs-lookup"><span data-stu-id="780d7-132">Activating roles</span></span>

- <span data-ttu-id="780d7-133">Révision des activités de rôle</span><span class="sxs-lookup"><span data-stu-id="780d7-133">Reviewing role activity</span></span>

#### <a name="how-do-i-enable-aad-pim"></a><span data-ttu-id="780d7-134">Comment activer AAD PIM ?</span><span class="sxs-lookup"><span data-stu-id="780d7-134">How do I enable AAD PIM?</span></span>

<span data-ttu-id="780d7-135">toostart à l’aide de PIM pour votre annuaire, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="780d7-135">toostart using PIM for your directory, do hello following:</span></span>

1. <span data-ttu-id="780d7-136">Se connecter toohello portail Azure en tant qu’administrateur général de votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="780d7-136">Sign in toohello Azure portal as a global administrator of your directory.</span></span>

2. <span data-ttu-id="780d7-137">Si votre organisation a plusieurs répertoires, sélectionnez votre nom d’utilisateur dans le coin supérieur droit hello Hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="780d7-137">If your organization has more than one directory, select your username in hello upper right-hand corner of hello Azure portal.</span></span> <span data-ttu-id="780d7-138">Sélectionnez le répertoire hello où vous allez utiliser Azure AD Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="780d7-138">Select hello directory where you will use Azure AD Privileged Identity Management.</span></span>

3. <span data-ttu-id="780d7-139">Sélectionnez **davantage de services** et utiliser hello **filtre** toosearch de zone de texte pour Azure AD Privileged Identity Management.</span><span class="sxs-lookup"><span data-stu-id="780d7-139">Select **More services** and use hello **Filter** textbox toosearch for Azure AD Privileged Identity Management.</span></span>

4. <span data-ttu-id="780d7-140">Vérifiez **code confidentiel toodashboard** puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="780d7-140">Check **Pin toodashboard** and then click **Create**.</span></span> <span data-ttu-id="780d7-141">Hello application de Privileged Identity Management s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="780d7-141">hello Privileged Identity Management application opens.</span></span>

<span data-ttu-id="780d7-142">Une fois Azure AD Privileged Identity Management est configuré, vous voyez Panneau de navigation hello lorsque vous ouvrez l’application hello.</span><span class="sxs-lookup"><span data-stu-id="780d7-142">Once Azure AD Privileged Identity Management is set up, you see hello navigation blade whenever you open hello application.</span></span>

![](media/protect-personal-data-identity-access-controls/azure-pim.png)

<span data-ttu-id="780d7-143">Pour plus d’informations et pour obtenir des instructions sur la mise en route avec AAD PIM, consultez [Commencer à utiliser Azure AD Privileged Identity Management.](https://docs.microsoft.com/active-directory/active-directory-privileged-identity-management-getting-started)</span><span class="sxs-lookup"><span data-stu-id="780d7-143">For more information and instructions on getting started with AAD PIM, see [Start Using Azure AD Privileged Identity Management.](https://docs.microsoft.com/active-directory/active-directory-privileged-identity-management-getting-started)</span></span>

### <a name="azure-role-based-access-control"></a><span data-ttu-id="780d7-144">Contrôle d’accès en fonction du rôle Azure</span><span class="sxs-lookup"><span data-stu-id="780d7-144">Azure Role-based Access Control</span></span>

<span data-ttu-id="780d7-145">[Role-Based Access Control de Azure](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) (RBAC) permet de gérer tooAzure d’accéder aux ressources en activant hello octroi d’accès basé sur le rôle d’utilisateur hello administrateurs Azure.</span><span class="sxs-lookup"><span data-stu-id="780d7-145">[Azure Role-Based Access Control](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) (RBAC) helps Azure administrators manage access tooAzure resources by enabling hello granting of access based on hello user’s assigned role.</span></span> <span data-ttu-id="780d7-146">Vous pouvez séparer les tâches au sein d’une équipe et accorder uniquement hello quantité toousers d’accès, les groupes et les applications dont ils ont besoin tooperform leur travail.</span><span class="sxs-lookup"><span data-stu-id="780d7-146">You can segregate duties within a team and grant only hello amount of access toousers, groups and applications that they need tooperform their jobs.</span></span>

<span data-ttu-id="780d7-147">Accès en fonction du rôle peuvent être accordé toousers à l’aide de hello portail Azure, les outils de ligne de commande Azure ou les API de gestion Azure.</span><span class="sxs-lookup"><span data-stu-id="780d7-147">Role-based access can be granted toousers using hello Azure portal, Azure Command-Line tools or Azure Management APIs.</span></span>

<span data-ttu-id="780d7-148">Pour plus d’informations sur les concepts de base Azure RBAC, consultez [prise en main le contrôle d’accès en fonction du rôle Bonjour portail Azure.](https://docs.microsoft.com/active-directory/role-based-access-control-what-is)</span><span class="sxs-lookup"><span data-stu-id="780d7-148">For more information about Azure RBAC basics, see [Get started with Role-Based Access Control in hello Azure Portal.](https://docs.microsoft.com/active-directory/role-based-access-control-what-is)</span></span>

#### <a name="how-do-i-manage-azure-rbac-with-powershell"></a><span data-ttu-id="780d7-149">Comment gérer le contrôle d’accès en fonction du rôle Azure avec PowerShell ?</span><span class="sxs-lookup"><span data-stu-id="780d7-149">How do I manage Azure RBAC with PowerShell?</span></span>

<span data-ttu-id="780d7-150">Vous pouvez utiliser toomanage d’applets de commande PowerShell Azure RBAC, y compris hello les tâches de gestion suivantes :</span><span class="sxs-lookup"><span data-stu-id="780d7-150">You can use PowerShell cmdlets toomanage Azure RBAC, including hello following management tasks:</span></span>

- <span data-ttu-id="780d7-151">Répertorier les rôles</span><span class="sxs-lookup"><span data-stu-id="780d7-151">List roles</span></span>

- <span data-ttu-id="780d7-152">Voir quel utilisateur a des autorisations d’accès</span><span class="sxs-lookup"><span data-stu-id="780d7-152">See who has access</span></span>

- <span data-ttu-id="780d7-153">Accorder l'accès</span><span class="sxs-lookup"><span data-stu-id="780d7-153">Grant access</span></span>

- <span data-ttu-id="780d7-154">Suppression d'accès</span><span class="sxs-lookup"><span data-stu-id="780d7-154">Remove access</span></span>

- <span data-ttu-id="780d7-155">Créer un rôle personnalisé</span><span class="sxs-lookup"><span data-stu-id="780d7-155">Create a custom role</span></span>

- <span data-ttu-id="780d7-156">Actions Get pour un fournisseur de ressources</span><span class="sxs-lookup"><span data-stu-id="780d7-156">Get Actions for a Resource Provider</span></span>

- <span data-ttu-id="780d7-157">Modifier un rôle personnalisé</span><span class="sxs-lookup"><span data-stu-id="780d7-157">Modify a custom role</span></span>

- <span data-ttu-id="780d7-158">Supprimer un rôle personnalisé</span><span class="sxs-lookup"><span data-stu-id="780d7-158">Delete a custom role</span></span>

- <span data-ttu-id="780d7-159">Répertorier les rôles personnalisés</span><span class="sxs-lookup"><span data-stu-id="780d7-159">List custom roles</span></span>

<span data-ttu-id="780d7-160">Pour obtenir des instructions sur toomanage RBAC Azure avec PowerShell, voir [en fonction du rôle de gérer l’accès avec Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell).</span><span class="sxs-lookup"><span data-stu-id="780d7-160">For instructions on how toomanage Azure RBAC with PowerShell, see [Manage Role-based Access with Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell).</span></span>

### <a name="azure-multi-factor-authentication"></a><span data-ttu-id="780d7-161">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="780d7-161">Azure Multi-Factor Authentication</span></span>

<span data-ttu-id="780d7-162">[L’authentification multifacteur Azure](https://docs.microsoft.com/azure/multi-factor-authentication/) (MFA) est une solution de vérification en deux étapes qui vous aide à toodata d’accès de sauvegarde et les applications, tout en répondant à la demande de l’utilisateur pour un processus de connexion simple.</span><span class="sxs-lookup"><span data-stu-id="780d7-162">[Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/) (MFA) is a two-step verification solution that helps safeguard access toodata and applications, while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="780d7-163">Il fournit une authentification forte au moyen de diverses méthodes de vérification, notamment les appels téléphoniques, l’envoi de SMS ou la vérification sur l’application mobile.</span><span class="sxs-lookup"><span data-stu-id="780d7-163">It delivers strong authentication via a range of verification methods, including phone call, text message, or mobile app verification.</span></span>

<span data-ttu-id="780d7-164">l’authentification Multifacteur toodeploy Bonjour cloud Azure, vous devez toofirst l’activer et réactivez la vérification en deux étapes pour les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="780d7-164">toodeploy MFA in hello Azure cloud, you need toofirst enable it and then turn on two-step verification for users.</span></span>

#### <a name="how-do-i-enable-azure-toouse-mfa"></a><span data-ttu-id="780d7-165">Comment faire pour activer toouse Azure MFA ?</span><span class="sxs-lookup"><span data-stu-id="780d7-165">How do I enable Azure toouse MFA?</span></span>

<span data-ttu-id="780d7-166">Si vos utilisateurs disposent de licences qui incluent l’authentification multifacteur Azure, aucune n’est que vous avez besoin de tooturn toodo sur Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="780d7-166">If your users have licenses that include Azure Multi-Factor Authentication, there's nothing that you need toodo tooturn on Azure MFA.</span></span> <span data-ttu-id="780d7-167">Si ce n’est pas le cas, vous devez toocreate un fournisseur d’authentification multifacteur dans votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="780d7-167">If not, you need toocreate a Multi-Factor Auth provider in your directory.</span></span> <span data-ttu-id="780d7-168">toodo, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="780d7-168">toodo this, follow these steps:</span></span>

1. <span data-ttu-id="780d7-169">Sélectionnez **Active Directory** Bonjour portail Azure classic (connecté en tant qu’administrateur).</span><span class="sxs-lookup"><span data-stu-id="780d7-169">Select **Active Directory** in hello Azure classic portal (logged on as an administrator).</span></span>

2. <span data-ttu-id="780d7-170">Sélectionnez **Fournisseurs Multi-Factor Authentication.**</span><span class="sxs-lookup"><span data-stu-id="780d7-170">Select **Multi-Factor Authentication Providers.**</span></span>

3. <span data-ttu-id="780d7-171">Sélectionnez **Nouveau**, puis sous **App Services**, sélectionnez **Fournisseur d’authentification multifacteur.**</span><span class="sxs-lookup"><span data-stu-id="780d7-171">Select **New,** and then under **App Services,** select **Multi-Factor Auth Provider.**</span></span>

4. <span data-ttu-id="780d7-172">Sélectionnez **Création rapide.**</span><span class="sxs-lookup"><span data-stu-id="780d7-172">Select **Quick Create.**</span></span>

5. <span data-ttu-id="780d7-173">Renseignez le champ de nom hello et sélectionnez un modèle d’utilisation (par authentification ou par utilisateur activé).</span><span class="sxs-lookup"><span data-stu-id="780d7-173">Fill in hello name field and select a usage model (per authentication or per enabled user).</span></span>

6. <span data-ttu-id="780d7-174">Désignez un répertoire qui hello fournisseur d’authentification Multifacteur est associé.</span><span class="sxs-lookup"><span data-stu-id="780d7-174">Designate a directory with which hello MFA Provider is associated.</span></span>

7. <span data-ttu-id="780d7-175">Cliquez sur hello **créer** bouton.</span><span class="sxs-lookup"><span data-stu-id="780d7-175">Click hello **Create** button.</span></span>

![](media/protect-personal-data-identity-access-controls/quick-create.png)

<span data-ttu-id="780d7-176">Pour plus d’informations sur la façon de toomanage votre fournisseur d’authentification multifacteur, consultez [mise en route avec un fournisseur d’authentification multifacteur Azure.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-auth-provider)</span><span class="sxs-lookup"><span data-stu-id="780d7-176">For more instructions on how toomanage your Multi-Factor Auth Provider, see [Getting Started with an Azure Multi-Factor Auth Provider.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-auth-provider)</span></span>

#### <a name="how-do-i-turn-on-two-step-verification-for-users"></a><span data-ttu-id="780d7-177">Comment activer la vérification en deux étapes pour les utilisateurs ?</span><span class="sxs-lookup"><span data-stu-id="780d7-177">How do I turn on two-step verification for users?</span></span>

<span data-ttu-id="780d7-178">Vous pouvez imposer la vérification en deux étapes pour toutes les connexions, ou vous pouvez créer de vérification en deux étapes de l’accès conditionnel stratégies toorequire uniquement lorsque des conditions spécifiques s’appliquent.</span><span class="sxs-lookup"><span data-stu-id="780d7-178">You can enforce two-step verification for all sign-ins, or you can create conditional access policies toorequire two-step verification only when specific conditions apply.</span></span>

<span data-ttu-id="780d7-179">L’activation de l’authentification Multifacteur Azure en modifiant des États utilisateur est approche traditionnelle de hello pour exiger une vérification en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="780d7-179">Enabling Azure MFA by changing user states is hello traditional approach for requiring two-step verification.</span></span> <span data-ttu-id="780d7-180">Tous les utilisateurs de hello que vous activez hello vérification en deux étapes de même exigence tooperform chaque fois qu’ils se connectent.</span><span class="sxs-lookup"><span data-stu-id="780d7-180">All hello users that you enable will have hello same requirement tooperform two-step verification every time they sign in.</span></span> <span data-ttu-id="780d7-181">L’activation d’un utilisateur remplace toutes les stratégies d’accès conditionnel appliquées à cet utilisateur.</span><span class="sxs-lookup"><span data-stu-id="780d7-181">Enabling a user overrides any conditional access policies that may affect that user.</span></span>

<span data-ttu-id="780d7-182">L’activation de l’authentification multifacteur Azure avec une stratégie d’accès conditionnel est une approche plus souple pour exiger une vérification en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="780d7-182">Enabling Azure MFA with a conditional access policy is a more flexible approach for requiring two-step verification.</span></span> <span data-ttu-id="780d7-183">Vous pouvez créer des stratégies d’accès conditionnel qui s’appliquent toogroups, ainsi que des utilisateurs individuels.</span><span class="sxs-lookup"><span data-stu-id="780d7-183">You can create conditional access policies that apply toogroups as well as individual users.</span></span> <span data-ttu-id="780d7-184">Vous pouvez appliquer davantage de restrictions aux groupes à haut risque par rapport aux groupes à faible risque, ou exiger la vérification en deux étapes uniquement pour les applications cloud à haut risque tout en ignorant celles à faible risque.</span><span class="sxs-lookup"><span data-stu-id="780d7-184">High-risk groups can be given more restrictions than low-risk groups, or two-step verification can be required only for high-risk cloud apps and skipped for low-risk ones.</span></span> <span data-ttu-id="780d7-185">Toutefois, l’accès conditionnel est une fonctionnalité payante d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="780d7-185">However, conditional access is a paid feature of Azure Active Directory.</span></span>

<span data-ttu-id="780d7-186">tooenable l’authentification Multifacteur en modifiant l’état utilisateur, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="780d7-186">tooenable MFA by changing user state, do hello following:</span></span>

1. <span data-ttu-id="780d7-187">Se connecter toohello portail Azure en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="780d7-187">Sign in toohello Azure portal as an administrator.</span></span>
2. <span data-ttu-id="780d7-188">Accédez trop**Azure Active Directory \> utilisateurs et groupes \> tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="780d7-188">Go too**Azure Active Directory \> Users and groups \> All users**.</span></span>
3. <span data-ttu-id="780d7-189">Sélectionnez **Multi-Factor Authentication**.</span><span class="sxs-lookup"><span data-stu-id="780d7-189">Select **Multi-Factor Authentication**.</span></span>
4. <span data-ttu-id="780d7-190">Rechercher un utilisateur hello que vous souhaitez tooenable pour Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="780d7-190">Find hello user that you want tooenable for Azure MFA.</span></span> <span data-ttu-id="780d7-191">Vous devrez peut-être toochange hello vue haut hello.</span><span class="sxs-lookup"><span data-stu-id="780d7-191">You may need toochange hello view at hello top.</span></span>
5. <span data-ttu-id="780d7-192">Vérifiez hello boîte suivant toohello nom de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="780d7-192">Check hello box next toohello user’s name.</span></span>
6. <span data-ttu-id="780d7-193">Sur la droite, sous étapes rapides de hello, choisissez **activer**.</span><span class="sxs-lookup"><span data-stu-id="780d7-193">On hello right, under quick steps, choose **Enable**.</span></span>

   ![](media/protect-personal-data-identity-access-controls/quick-create.png)

7. <span data-ttu-id="780d7-194">Confirmez votre sélection dans la fenêtre contextuelle hello qui s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="780d7-194">Confirm your selection in hello pop-up window that opens.</span></span>  <span data-ttu-id="780d7-195">Les utilisateurs pour lesquels l’authentification Multifacteur a été activé demandera tooregister hello leur prochaine dans que connexion.</span><span class="sxs-lookup"><span data-stu-id="780d7-195">Users for whom MFA has been enabled will be asked tooregister hello next time they sign in.</span></span>

<span data-ttu-id="780d7-196">tooenable Azure MFA avec une stratégie d’accès conditionnel, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="780d7-196">tooenable Azure MFA with a conditional access policy, do hello following:</span></span>

1. <span data-ttu-id="780d7-197">Se connecter toohello portail Azure en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="780d7-197">Sign in toohello Azure portal as an administrator.</span></span>

2. <span data-ttu-id="780d7-198">Accédez trop**Azure Active Directory \> accès conditionnel**.</span><span class="sxs-lookup"><span data-stu-id="780d7-198">Go too**Azure Active Directory \> Conditional access**.</span></span>

3. <span data-ttu-id="780d7-199">Sélectionnez **Nouvelle stratégie**.</span><span class="sxs-lookup"><span data-stu-id="780d7-199">Select **New policy**.</span></span>

4. <span data-ttu-id="780d7-200">Sous **Affectations**, sélectionnez **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="780d7-200">Under **Assignments**, select **Users and groups**.</span></span> <span data-ttu-id="780d7-201">Hello d’utilisation **Include** et **exclure** onglets toospecify quels utilisateurs et groupes qui est géré par la stratégie de hello.</span><span class="sxs-lookup"><span data-stu-id="780d7-201">Use hello **Include** and     **Exclude** tabs toospecify which users and groups will be managed by hello policy.</span></span>

5. <span data-ttu-id="780d7-202">Sous **Affectations**, sélectionnez **Applications cloud.**</span><span class="sxs-lookup"><span data-stu-id="780d7-202">Under **Assignments**, select **Cloud apps.**</span></span> <span data-ttu-id="780d7-203">Choisissez trop**inclure toutes les applications cloud**.</span><span class="sxs-lookup"><span data-stu-id="780d7-203">Choose too**include All cloud apps**.</span></span>
6.  <span data-ttu-id="780d7-204">Sous **Contrôles d’accès**, sélectionnez **Accorder**.</span><span class="sxs-lookup"><span data-stu-id="780d7-204">Under **Access controls**, select **Grant**.</span></span> <span data-ttu-id="780d7-205">Choisissez **Exiger une authentification multifacteur**.</span><span class="sxs-lookup"><span data-stu-id="780d7-205">Choose **Require multi-factor authentication**.</span></span>
7.  <span data-ttu-id="780d7-206">Activer **activer la stratégie** trop**sur** , puis sélectionnez **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="780d7-206">Turn **Enable policy** too**On** and then select **Save**.</span></span>

<span data-ttu-id="780d7-207">Pour plus d’informations sur comment tooconfigure Azure MFA paramètres tooset des alertes de fraude, créer un contournement à usage unique, utiliser des messages vocaux personnalisés, configurer la mise en cache, spécifiez les adresses IP approuvées, créer des mots de passe d’application, activer la mémorisation de l’authentification Multifacteur pour les appareils auxquels les utilisateurs faites confiance, puis sélectionnez méthodes de vérification, consultez [configurer les paramètres d’authentification multifacteur Azure.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)</span><span class="sxs-lookup"><span data-stu-id="780d7-207">For information on how tooconfigure Azure MFA settings tooset up fraud alerts, create a one-time bypass, use custom voice messages, configure caching, specify trusted IPs, create app passwords, enable remembering MFA for devices that users trust, and select verification methods, see [Configure Azure Multi-Factor Authentication Settings.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)</span></span>

## <a name="next-steps"></a><span data-ttu-id="780d7-208">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="780d7-208">Next steps</span></span>

- [<span data-ttu-id="780d7-209">Sécurisation de l’accès privilégié dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="780d7-209">Securing privileged access in Azure AD</span></span>](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access)

- [<span data-ttu-id="780d7-210">Forum aux questions sur Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="780d7-210">Frequently asked questions about Azure Multi-Factor Authentication</span></span>](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-faq)

- [<span data-ttu-id="780d7-211">Résolution des problèmes de contrôle d’accès en fonction du rôle</span><span class="sxs-lookup"><span data-stu-id="780d7-211">Role-based Access Control troubleshooting</span></span>](https://docs.microsoft.com/azure/active-directory/role-based-access-control-troubleshooting)

- [<span data-ttu-id="780d7-212">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="780d7-212">Azure Active Directory Identity Protection</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection)
