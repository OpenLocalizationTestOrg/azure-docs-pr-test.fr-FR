---
title: "rôles de contrôle d’accès basée sur les rôles personnalisés aaaCreate et affecter des utilisateurs externes dans Azure et des toointernal | Documents Microsoft"
description: "Attribuer des rôles RBAC personnalisés créés à l’aide de PowerShell et d’Azure CLI à des utilisateurs internes et externes"
services: active-directory
documentationcenter: 
author: andreicradu
manager: catadinu
editor: kgremban
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/10/2017
ms.author: a-crradu
ms.openlocfilehash: 26793a66d6ca2f771338eed87d10ce2b3b431841
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
## <a name="intro-on-role-based-access-control"></a><span data-ttu-id="23e25-103">Contrôle d’accès en fonction du rôle Azure</span><span class="sxs-lookup"><span data-stu-id="23e25-103">Intro on role-based access control</span></span>

<span data-ttu-id="23e25-104">Contrôle d’accès basé sur le rôle est une fonctionnalité uniquement du portail Azure autorisant les propriétaires de hello d’un abonnement tooassign granulaires rôles tooother auxquels les utilisateurs qui peuvent gérer les étendues de ressource spécifique dans leur environnement.</span><span class="sxs-lookup"><span data-stu-id="23e25-104">Role-based access control is an Azure portal only feature allowing hello owners of a subscription tooassign granular roles tooother users who can manage specific resource scopes in their environment.</span></span>

<span data-ttu-id="23e25-105">RBAC permet une meilleure gestion de la sécurité pour les grandes entreprises et pour les blocs SMB fonctionne avec des collaborateurs externes, des fournisseurs ou indépendants qui doivent accéder aux ressources toospecific dans votre environnement, mais pas nécessairement toohello ensemble de l’infrastructure ou l’une étendues associées à la facturation.</span><span class="sxs-lookup"><span data-stu-id="23e25-105">RBAC allows better security management for large organizations and for SMBs working with external collaborators, vendors or freelancers which need access toospecific resources in your environment but not necessarily toohello entire infrastructure or any billing-related scopes.</span></span> <span data-ttu-id="23e25-106">RBAC souplesse hello de propriétaire d’un abonnement Azure géré par le compte d’administrateur hello (rôle d’administrateur de service à un niveau d’abonnement) et ont plusieurs toowork utilisateurs invités sous hello même abonnement, mais sans tout d’administration droits pour celle-ci.</span><span class="sxs-lookup"><span data-stu-id="23e25-106">RBAC allows hello flexibility of owning one Azure subscription managed by hello administrator account (service administrator role at a subscription level) and have multiple users invited toowork under hello same subscription but without any administrative rights for it.</span></span> <span data-ttu-id="23e25-107">De gestion et de facturation, fonctionnalité RBAC de hello prouve toobe une option efficace temps et de gestion pour l’utilisation d’Azure dans divers scénarios.</span><span class="sxs-lookup"><span data-stu-id="23e25-107">From a management and billing perspective, hello RBAC feature proves toobe a time and management efficient option for using Azure in various scenarios.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="23e25-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="23e25-108">Prerequisites</span></span>
<span data-ttu-id="23e25-109">L’utilisation de RBAC Bonjour environnement Azure requiert :</span><span class="sxs-lookup"><span data-stu-id="23e25-109">Using RBAC in hello Azure environment requires:</span></span>

* <span data-ttu-id="23e25-110">Abonnement Azure ayant un autonome affecté toohello utilisateur comme propriétaire (rôle de l’abonnement)</span><span class="sxs-lookup"><span data-stu-id="23e25-110">Having a standalone Azure subscription assigned toohello user as owner (subscription role)</span></span>
* <span data-ttu-id="23e25-111">Rôle de propriétaire hello Hello abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="23e25-111">Have hello Owner role of hello Azure subscription</span></span>
* <span data-ttu-id="23e25-112">Avoir accès toohello [portail Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="23e25-112">Have access toohello [Azure portal](https://portal.azure.com)</span></span>
* <span data-ttu-id="23e25-113">Vérifiez que hello toohave suivant des fournisseurs de ressources inscrit pour l’abonnement d’utilisateur hello : **Microsoft.Authorization**.</span><span class="sxs-lookup"><span data-stu-id="23e25-113">Make sure toohave hello following Resource Providers registered for hello user subscription: **Microsoft.Authorization**.</span></span> <span data-ttu-id="23e25-114">Pour plus d’informations sur la façon dont tooregister hello des fournisseurs de ressources, consultez [fournisseurs du Gestionnaire de ressources, des régions, des versions d’API et des schémas](/azure-resource-manager/resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="23e25-114">For more information on how tooregister hello resource providers, see [Resource Manager providers, regions, API versions and schemas](/azure-resource-manager/resource-manager-supported-services.md).</span></span>

> [!NOTE]
> <span data-ttu-id="23e25-115">Les abonnements Office 365 ni aucune licence Azure Active Directory (par exemple : accès tooAzure Active Directory) configuré à partir du portail ne qualité l’utilisation de RBAC de hello O365.</span><span class="sxs-lookup"><span data-stu-id="23e25-115">Office 365 subscriptions or Azure Active Directory licenses (for example: Access tooAzure Active Directory) provisioned from hello O365 portal don't quality for using RBAC.</span></span>

## <a name="how-can-rbac-be-used"></a><span data-ttu-id="23e25-116">Comment la fonctionnalité RBAC peut être utilisée</span><span class="sxs-lookup"><span data-stu-id="23e25-116">How can RBAC be used</span></span>
<span data-ttu-id="23e25-117">La fonctionnalité RBAC peut être appliquée à trois étendues différentes dans Azure.</span><span class="sxs-lookup"><span data-stu-id="23e25-117">RBAC can be applied at three different scopes in Azure.</span></span> <span data-ttu-id="23e25-118">À partir de hello plus élevés étendue toohello plus basse, ils sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="23e25-118">From hello highest scope toohello lowest one, they are as follows:</span></span>

* <span data-ttu-id="23e25-119">Abonnement (la plus élevée)</span><span class="sxs-lookup"><span data-stu-id="23e25-119">Subscription (highest)</span></span>
* <span data-ttu-id="23e25-120">Groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="23e25-120">Resource group</span></span>
* <span data-ttu-id="23e25-121">Portée de la ressource (hello plus bas niveau d’accès offre des autorisations ciblées étendue de ressource Azure tooan)</span><span class="sxs-lookup"><span data-stu-id="23e25-121">Resource scope (hello lowest access level offering targeted permissions tooan individual Azure resource scope)</span></span>

## <a name="assign-rbac-roles-at-hello-subscription-scope"></a><span data-ttu-id="23e25-122">Attribuer des rôles au niveau de l’étendue de l’abonnement hello RBAC</span><span class="sxs-lookup"><span data-stu-id="23e25-122">Assign RBAC roles at hello subscription scope</span></span>
<span data-ttu-id="23e25-123">Il existe notamment deux cas courants d’utilisation de la fonctionnalité RBAC :</span><span class="sxs-lookup"><span data-stu-id="23e25-123">There are two common examples when RBAC is used (but not limited to):</span></span>

* <span data-ttu-id="23e25-124">Utilisateurs externes d’organisations de hello (n’appartenant pas à client Azure Active Directory de l’utilisateur admin de hello) invité toomanage certaines ressources ou l’abonnement entier de hello</span><span class="sxs-lookup"><span data-stu-id="23e25-124">Having external users from hello organizations (not part of hello admin user's Azure Active Directory tenant) invited toomanage certain resources or hello whole subscription</span></span>
* <span data-ttu-id="23e25-125">Utilisation avec des utilisateurs à l’intérieur d’organisation hello (qu’ils appartiennent client Azure Active Directory de l’utilisateur hello) mais la partie de différentes équipes ou les groupes qui ont besoin d’un accès granulaire soit toohello abonnement entière ou les groupes de ressources toocertain ou ressource étendues Bonjour environnement</span><span class="sxs-lookup"><span data-stu-id="23e25-125">Working with users inside hello organization (they are part of hello user's Azure Active Directory tenant) but part of different teams or groups which need granular access either toohello whole subscription or toocertain resource groups or resource scopes in hello environment</span></span>

## <a name="grant-access-at-a-subscription-level-for-a-user-outside-of-azure-active-directory"></a><span data-ttu-id="23e25-126">Octroyer l’accès au niveau d’un abonnement à un utilisateur extérieur à Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="23e25-126">Grant access at a subscription level for a user outside of Azure Active Directory</span></span>
<span data-ttu-id="23e25-127">Rôles RBAC peuvent être accordées uniquement par **propriétaires** d’abonnement de hello par conséquent l’utilisateur admin hello doit être enregistré avec un nom d’utilisateur qui a ce rôle déjà affecté ou qui a créé l’abonnement Azure de hello.</span><span class="sxs-lookup"><span data-stu-id="23e25-127">RBAC roles can be granted only by **Owners** of hello subscription therefore hello admin user must be logged with a username which has this role pre-assigned or has created hello Azure subscription.</span></span>

<span data-ttu-id="23e25-128">À partir de hello portail Azure, après avoir connectez-vous en tant qu’administrateur, sélectionnez « Abonnements » et choisissez hello souhaitée une.</span><span class="sxs-lookup"><span data-stu-id="23e25-128">From hello Azure portal, after you sign-in as admin, select “Subscriptions” and chose hello desired one.</span></span>
<span data-ttu-id="23e25-129">![panneau d’abonnement dans le portail Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) par défaut, si l’utilisateur admin hello a acheté hello abonnement Azure, utilisateur de hello apparaîtront en tant que **Admin. compte**, ce rôle d’abonnement hello.</span><span class="sxs-lookup"><span data-stu-id="23e25-129">![subscription blade in Azure portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) By default, if hello admin user has purchased hello Azure subscription, hello user will show up as **Account Admin**, this being hello subscription role.</span></span> <span data-ttu-id="23e25-130">Pour plus d’informations sur les rôles d’abonnement Azure hello, consultez [ajouter ou modifier les rôles administrateur Azure qui gèrent les abonnement hello ou services](/billing/billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="23e25-130">For more details on hello Azure subscription roles, see [Add or change Azure administrator roles that manage hello subscription or services](/billing/billing-add-change-azure-subscription-administrator.md).</span></span>

<span data-ttu-id="23e25-131">Dans cet exemple, hello utilisateur »alflanigan@outlook.com» est hello **propriétaire** Hello « Version d’évaluation gratuite » abonnement Bonjour AAD locataire « Par défaut le locataire Azure ».</span><span class="sxs-lookup"><span data-stu-id="23e25-131">In this example, hello user "alflanigan@outlook.com" is hello **Owner** of hello "Free Trial" subscription in hello AAD tenant "Default tenant Azure".</span></span> <span data-ttu-id="23e25-132">Étant donné que cet utilisateur est le créateur de hello Hello abonnement Azure avec hello initiale Account Microsoft « Outlook » (Account Microsoft = Outlook, etc. de Live) hello nom de domaine par défaut pour tous les autres utilisateurs ajoutés dans ce locataire sera **«@alflaniganuoutlook.onmicrosoft.com»**.</span><span class="sxs-lookup"><span data-stu-id="23e25-132">Since this user is hello creator of hello Azure subscription with hello initial Microsoft Account “Outlook” (Microsoft Account = Outlook, Live etc.) hello default domain name for all other users added in this tenant will be **"@alflaniganuoutlook.onmicrosoft.com"**.</span></span> <span data-ttu-id="23e25-133">Par conception, syntaxe hello du nouveau domaine de hello est formé par assembler hello nom d’utilisateur et nom de domaine de l’utilisateur hello qui a créé le locataire de hello et l’extension de hello ajout **«. onmicrosoft.com »**.</span><span class="sxs-lookup"><span data-stu-id="23e25-133">By design, hello syntax of hello new domain is formed by putting together hello username and domain name of hello user who created hello tenant and adding hello extension **".onmicrosoft.com"**.</span></span>
<span data-ttu-id="23e25-134">En outre, les utilisateurs peuvent connectez-vous avec un nom de domaine personnalisé dans le locataire de hello après l’ajout et la vérification de sa locataire hello.</span><span class="sxs-lookup"><span data-stu-id="23e25-134">Furthermore, users can sign-in with a custom domain name in hello tenant after adding and verifying it for hello new tenant.</span></span> <span data-ttu-id="23e25-135">Pour plus d’informations sur comment tooverify un nom de domaine personnalisé dans un locataire Azure Active Directory, voir [ajouter un répertoire de tooyour de nom de domaine personnalisé](/active-directory/active-directory-add-domain).</span><span class="sxs-lookup"><span data-stu-id="23e25-135">For more details on how tooverify a custom domain name in an Azure Active Directory tenant, see [Add a custom domain name tooyour directory](/active-directory/active-directory-add-domain).</span></span>

<span data-ttu-id="23e25-136">Dans cet exemple, l’annuaire hello » par défaut locataire Azure » contient uniquement les utilisateurs avec le nom de domaine hello «@alflanigan.onmicrosoft.com».</span><span class="sxs-lookup"><span data-stu-id="23e25-136">In this example, hello "Default tenant Azure" directory contains only users with hello domain name "@alflanigan.onmicrosoft.com".</span></span>

<span data-ttu-id="23e25-137">Après avoir sélectionné un abonnement de hello, l’utilisateur admin hello doit cliquer sur **contrôle d’accès (IAM)** , puis **ajouter un nouveau rôle**.</span><span class="sxs-lookup"><span data-stu-id="23e25-137">After selecting hello subscription, hello admin user must click **Access Control (IAM)** and then **Add a new role**.</span></span>





![fonctionnalité de contrôle d’accès IAM dans le portail Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/1.png)





![ajouter un utilisateur dans la fonctionnalité de contrôle d’accès IAM dans le portail Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/2.png)

<span data-ttu-id="23e25-140">étape suivante de Hello est tooselect hello rôle toobe affecté et utilisateur hello auxquels le rôle RBAC hello sera assigné à.</span><span class="sxs-lookup"><span data-stu-id="23e25-140">hello next step is tooselect hello role toobe assigned and hello user whom hello RBAC role will be assigned to.</span></span> <span data-ttu-id="23e25-141">Bonjour **rôle** utilisateur admin de liste déroulante menu hello voit uniquement hello RBAC rôles intégrés qui sont disponibles dans Azure.</span><span class="sxs-lookup"><span data-stu-id="23e25-141">In hello **Role** dropdown menu hello admin user sees only hello built-in RBAC roles which are available in Azure.</span></span> <span data-ttu-id="23e25-142">Pour plus d’explications sur chaque rôle et les étendues qui peuvent lui être attribuées, voir [Rôles intégrés pour contrôle d’accès en fonction du rôle Azure](/active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="23e25-142">For more detailed explanations of each role and their assignable scopes, see [Built-in roles for Azure Role-Based Access Control](/active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="23e25-143">l’utilisateur admin Hello doit ensuite l’adresse de messagerie tooadd hello d’utilisateur externe de hello.</span><span class="sxs-lookup"><span data-stu-id="23e25-143">hello admin user then needs tooadd hello email address of hello external user.</span></span> <span data-ttu-id="23e25-144">Hello attendu de comportement pour hello utilisateur externe toonot qui s’affichent dans hello existant du client.</span><span class="sxs-lookup"><span data-stu-id="23e25-144">hello expected behavior is for hello external user toonot show up in hello existing tenant.</span></span> <span data-ttu-id="23e25-145">Une fois que l’utilisateur externe de hello a été invité, il sera visible sous **abonnements > contrôle d’accès (IAM)** avec tous les utilisateurs actuels hello, qui sont actuellement attribués un rôle RBAC au hello étendue de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="23e25-145">After hello external user has been invited, he will be visible under **Subscriptions > Access Control (IAM)** with all hello current users which are currently assigned an RBAC role at hello Subscription scope.</span></span>





![ajouter le rôle RBAC toonew autorisations](./media/role-based-access-control-create-custom-roles-for-internal-external-users/3.png)





![liste des rôles RBAC au niveau abonnement](./media/role-based-access-control-create-custom-roles-for-internal-external-users/4.png)

<span data-ttu-id="23e25-148">utilisateur de Hello »chessercarlton@gmail.com» a été invitée toobe un **propriétaire** pour hello abonnement « D’essai gratuit ».</span><span class="sxs-lookup"><span data-stu-id="23e25-148">hello user "chessercarlton@gmail.com" has been invited toobe an **Owner** for hello “Free Trial” subscription.</span></span> <span data-ttu-id="23e25-149">Après l’envoi d’invitation hello, utilisateur externe de hello recevra un e-mail de confirmation avec un lien d’activation.</span><span class="sxs-lookup"><span data-stu-id="23e25-149">After sending hello invitation, hello external user will receive an email confirmation with an activation link.</span></span>
<span data-ttu-id="23e25-150">![e-mail d'invitation pour le rôles RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)</span><span class="sxs-lookup"><span data-stu-id="23e25-150">![email invitation for RBAC role](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)</span></span>

<span data-ttu-id="23e25-151">En cours toohello externe organisation, utilisateur hello n’a pas les tous les attributs existants dans le répertoire de « Par défaut le locataire Azure » hello.</span><span class="sxs-lookup"><span data-stu-id="23e25-151">Being external toohello organization, hello new user does not have any existing attributes in hello "Default tenant Azure" directory.</span></span> <span data-ttu-id="23e25-152">Ils sont créés après toobe consentement enregistré dans le répertoire hello qui est associé à abonnement hello qui lui ont été affectées à un rôle à utilisateur externe de hello.</span><span class="sxs-lookup"><span data-stu-id="23e25-152">They will be created after hello external user has given consent toobe recorded in hello directory which is associated with hello subscription which he has been assigned a role to.</span></span>





![e-mail d’invitation pour le rôle RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/6.png)

<span data-ttu-id="23e25-154">les utilisateurs externes Hello montre Bonjour client Azure Active Directory dès lors que l’utilisateur externe et cela peut être affiché dans hello portail Azure et dans le portail classique de hello.</span><span class="sxs-lookup"><span data-stu-id="23e25-154">hello external user shows in hello Azure Active Directory tenant from now on as external user and this can be viewed both in hello Azure portal and in hello classic portal.</span></span>





![panneau des utilisateurs azure active directory sur le portail azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/7.png)





![panneau des utilisateurs azure active directory sur le portail azure classic](./media/role-based-access-control-create-custom-roles-for-internal-external-users/8.png)

<span data-ttu-id="23e25-157">Bonjour **utilisateurs** vue dans les deux utilisateurs externes de portails hello peut être reconnu par :</span><span class="sxs-lookup"><span data-stu-id="23e25-157">In hello **Users** view in both portals hello external users can be recognized by:</span></span>

* <span data-ttu-id="23e25-158">type d’icône différents Hello Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="23e25-158">hello different icon type in hello Azure portal</span></span>
* <span data-ttu-id="23e25-159">Hello différent approvisionnement point dans le portail classique de hello</span><span class="sxs-lookup"><span data-stu-id="23e25-159">hello different sourcing point in hello classic portal</span></span>

<span data-ttu-id="23e25-160">Toutefois, l’octroi **propriétaire** ou **collaborateur** utilisateur externe de l’accès tooan à hello **abonnement** portée, n’autorise pas de répertoire de l’utilisateur admin hello accès toohello, à moins que hello **administrateur Global** l’autorise.</span><span class="sxs-lookup"><span data-stu-id="23e25-160">However, granting **Owner** or **Contributor** access tooan external user at hello **Subscription** scope, does not allow hello access toohello admin user's directory, unless hello **Global Admin** allows it.</span></span> <span data-ttu-id="23e25-161">Dans les propriétés d’utilisateur hello, hello **Type utilisateur** qui a deux paramètres communs, **membre** et **invité** peut être identifiée.</span><span class="sxs-lookup"><span data-stu-id="23e25-161">In hello user proprieties,  hello **User Type** which has two common parameters, **Member** and **Guest** can be identified.</span></span> <span data-ttu-id="23e25-162">Un membre est un utilisateur qui est enregistré dans le répertoire de hello lors de l’invité est un répertoire de toohello utilisateur invité d’une source externe.</span><span class="sxs-lookup"><span data-stu-id="23e25-162">A member is a user which is registered in hello directory while a guest is a user invited toohello directory from an external source.</span></span> <span data-ttu-id="23e25-163">Pour plus d’informations, voir [Comment les administrateurs Azure Active Directory ajoutent des utilisateurs B2B Collaboration](/active-directory/active-directory-b2b-admin-add-users).</span><span class="sxs-lookup"><span data-stu-id="23e25-163">For more information, see [How do Azure Active Directory admins add B2B collaboration users](/active-directory/active-directory-b2b-admin-add-users).</span></span>

> [!NOTE]
> <span data-ttu-id="23e25-164">Assurez-vous qu’après avoir entré les informations d’identification hello dans le portail de hello, utilisateur externe de hello sélectionne le répertoire approprié de hello toosign dans.</span><span class="sxs-lookup"><span data-stu-id="23e25-164">Make sure that after entering hello credentials in hello portal, hello external user selects hello correct directory toosign-in to.</span></span> <span data-ttu-id="23e25-165">Hello même utilisateur peut avoir accès toomultiple répertoires et peuvent sélectionner le des deux d'entre eux en cliquant sur le nom d’utilisateur de hello dans hello partie supérieure droite Bonjour portail Azure, puis choisissez répertoire approprié de hello à partir de la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="23e25-165">hello same user can have access toomultiple directories and can select either one of  them by clicking hello username in hello top right-hand side in hello Azure portal and then choose hello appropriate directory from hello dropdown list.</span></span>

<span data-ttu-id="23e25-166">Tout en étant un invité dans le répertoire de hello, utilisateur externe de hello peut gérer toutes les ressources pour hello abonnement Azure, mais ne peut pas accéder au répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="23e25-166">While being a guest in hello directory, hello external user can manage all resources for hello Azure subscription, but can't access hello directory.</span></span>





![accéder au portail Azure active directory de tooazure restreint](./media/role-based-access-control-create-custom-roles-for-internal-external-users/9.png)

<span data-ttu-id="23e25-168">Azure Active Directory et un abonnement Azure n’ont pas de relation enfant-parent comme l’ont d’autres ressources Azure (par exemple, Azure Virtual Machines, Azure Virtual Networks, Web Apps, Stockage Azure, etc.).</span><span class="sxs-lookup"><span data-stu-id="23e25-168">Azure Active Directory and an Azure subscription don't have a child-parent relation like other Azure resources (for example: virtual machines, virtual networks, web apps, storage etc.) have with an Azure subscription.</span></span> <span data-ttu-id="23e25-169">Tous les hello ce dernier est créé, gérés et facturés sous un abonnement Azure, alors qu’un abonnement Azure est utilisé toomanage hello accès tooan Azure active.</span><span class="sxs-lookup"><span data-stu-id="23e25-169">All hello latter is created, managed and billed under an Azure subscription while an Azure subscription is used toomanage hello access tooan Azure directory.</span></span> <span data-ttu-id="23e25-170">Pour plus d’informations, consultez [abonnement de la manière dont un Azure est connexe tooAzure AD](/active-directory/active-directory-how-subscriptions-associated-directory).</span><span class="sxs-lookup"><span data-stu-id="23e25-170">For more details, see [How an Azure subscription is related tooAzure AD](/active-directory/active-directory-how-subscriptions-associated-directory).</span></span>

<span data-ttu-id="23e25-171">À partir de tous les hello RBAC rôles intégrés **propriétaire** et **collaborateur** offrent un accès de gestion complète des ressources de tooall dans l’environnement de hello, hello différence qu’un collaborateur ne peut créer et supprimer les nouveaux Rôles RBAC.</span><span class="sxs-lookup"><span data-stu-id="23e25-171">From all hello built-in RBAC roles, **Owner** and **Contributor** offer full management access tooall resources in hello environment, hello difference being that a Contributor can't create and delete new RBAC roles.</span></span> <span data-ttu-id="23e25-172">Hello autres rôles intégrés tels que **contributeur de l’ordinateur virtuel** offrent un accès de gestion complète uniquement les ressources toohello indiqués par le nom hello, quel que soit hello **groupe de ressources** qu’ils sont en cours de création dans.</span><span class="sxs-lookup"><span data-stu-id="23e25-172">hello other built-in roles like **Virtual Machine Contributor** offer full management access only toohello resources indicated by hello name, regardless of hello **Resource Group** they are being created into.</span></span>

<span data-ttu-id="23e25-173">Rôle affectation RBAC d’intégré hello de **contributeur de l’ordinateur virtuel** à un niveau d’abonnement, signifie que ce rôle de hello hello utilisateur affecté :</span><span class="sxs-lookup"><span data-stu-id="23e25-173">Assigning hello built-in RBAC role of **Virtual Machine Contributor** at a subscription level, means that hello user assigned hello role:</span></span>

* <span data-ttu-id="23e25-174">Peut afficher tous les ordinateurs virtuels quelle que soit leurs déploiement date hello groupes de ressources et qu’ils font partie de</span><span class="sxs-lookup"><span data-stu-id="23e25-174">Can view all virtual machines regardless their deployment date and hello resource groups they are part of</span></span>
* <span data-ttu-id="23e25-175">A des machines virtuelles de gestion complète accès toohello dans l’abonnement de hello</span><span class="sxs-lookup"><span data-stu-id="23e25-175">Has full management access toohello virtual machines in hello subscription</span></span>
* <span data-ttu-id="23e25-176">Ne peut pas afficher d’autres types de ressource dans l’abonnement de hello</span><span class="sxs-lookup"><span data-stu-id="23e25-176">Can't view any other resource types in hello subscription</span></span>
* <span data-ttu-id="23e25-177">ne peut apporter aucune modification sur le plan de la facturation.</span><span class="sxs-lookup"><span data-stu-id="23e25-177">Can't operate any changes from a billing perspective</span></span>

> [!NOTE]
> <span data-ttu-id="23e25-178">RBAC en cours d’une seule fonctionnalité portail Azure, elle n’accorde pas portail classique d’accès toohello.</span><span class="sxs-lookup"><span data-stu-id="23e25-178">RBAC being an Azure portal only feature, it doesn't grant access toohello classic portal.</span></span>

## <a name="assign-a-built-in-rbac-role-tooan-external-user"></a><span data-ttu-id="23e25-179">Affecter un intégrée RBAC rôle tooan utilisateur externe</span><span class="sxs-lookup"><span data-stu-id="23e25-179">Assign a built-in RBAC role tooan external user</span></span>
<span data-ttu-id="23e25-180">Pour un scénario différent dans ce test, hello utilisateur externe «alflanigan@gmail.com» est ajouté en tant qu’un **contributeur de l’ordinateur virtuel**.</span><span class="sxs-lookup"><span data-stu-id="23e25-180">For a different scenario in this test, hello external user "alflanigan@gmail.com" is added as a **Virtual Machine Contributor**.</span></span>




![rôle prédéfini de contributeur de machines virtuelles](./media/role-based-access-control-create-custom-roles-for-internal-external-users/11.png)

<span data-ttu-id="23e25-182">comportement normal de Hello pour cet utilisateur externe avec ce rôle intégré est toosee et gérer uniquement les ordinateurs virtuels et leur adjacents Gestionnaire de ressources uniquement ressources nécessaire lors du déploiement.</span><span class="sxs-lookup"><span data-stu-id="23e25-182">hello normal behavior for this external user with this built-in role is toosee and manage only virtual machines and their adjacent Resource Manager only resources necessary while deploying.</span></span> <span data-ttu-id="23e25-183">Par défaut, ces rôles limités offrent un accès seules ressources correspondant tootheir créés Bonjour portail Azure, quel que soit certaines peuvent toujours être déployé dans le portail classique hello et (par exemple : machines virtuelles).</span><span class="sxs-lookup"><span data-stu-id="23e25-183">By design, these limited roles offer access only tootheir correspondent resources created in hello Azure portal, regardless some can still be deployed in hello classic portal as well (for example: virtual machines).</span></span>





![présentation du rôle contributeur de machines virtuelles dans le portail azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/12.png)

## <a name="grant-access-at-a-subscription-level-for-a-user-in-hello-same-directory"></a><span data-ttu-id="23e25-185">Octroi d’accès à un niveau d’abonnement pour un utilisateur dans hello même répertoire</span><span class="sxs-lookup"><span data-stu-id="23e25-185">Grant access at a subscription level for a user in hello same directory</span></span>
<span data-ttu-id="23e25-186">flux de processus Hello est identique tooadding un utilisateur externe, à la fois de hello rôle admin de perspective qui accord hello RBAC, ainsi que des utilisateur hello accordées rôle toohello d’accès.</span><span class="sxs-lookup"><span data-stu-id="23e25-186">hello process flow is identical tooadding an external user, both from hello admin perspective granting hello RBAC role as well as hello user being granted access toohello role.</span></span> <span data-ttu-id="23e25-187">Hello différence est que l’utilisateur invité de hello ne recevra pas les invitations de messagerie car toutes les portées de ressource hello au sein de l’abonnement de hello sera disponibles dans le tableau de bord hello après l’ouverture de session.</span><span class="sxs-lookup"><span data-stu-id="23e25-187">hello difference here is that hello invited user will not receive any email invitations as all hello resource scopes within hello subscription will be available in hello dashboard after signing in.</span></span>

## <a name="assign-rbac-roles-at-hello-resource-group-scope"></a><span data-ttu-id="23e25-188">Attribuer des rôles au niveau de l’étendue de groupe de ressources hello RBAC</span><span class="sxs-lookup"><span data-stu-id="23e25-188">Assign RBAC roles at hello resource group scope</span></span>
<span data-ttu-id="23e25-189">Affectation d’un rôle RBAC à un **groupe de ressources** étendue a un processus identiques pour l’attribution de rôle hello au niveau d’abonnement hello, pour les deux types d’utilisateurs - internes ou externes (dans le cadre du hello même répertoire).</span><span class="sxs-lookup"><span data-stu-id="23e25-189">Assigning an RBAC role at a **Resource Group** scope has an identical process for assigning hello role at hello subscription level, for both types of users - either external or internal (part of hello same directory).</span></span> <span data-ttu-id="23e25-190">Bonjour les utilisateurs qui sont affectés des rôles RBAC de hello est toosee dans leur environnement uniquement le groupe de ressources hello leur a été attribué l’accès à partir de hello **groupes de ressources** icône Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="23e25-190">hello users which are assigned hello RBAC role is toosee in their environment only hello resource group they have been assigned access from hello **Resource Groups** icon in hello Azure portal.</span></span>

## <a name="assign-rbac-roles-at-hello-resource-scope"></a><span data-ttu-id="23e25-191">Affecter des rôles RBAC à portée de la ressource hello</span><span class="sxs-lookup"><span data-stu-id="23e25-191">Assign RBAC roles at hello resource scope</span></span>
<span data-ttu-id="23e25-192">Affectation d’un rôle RBAC dans une étendue de ressources dans Azure dispose d’un processus identiques pour l’attribution de rôle hello au niveau d’abonnement hello ou au niveau de groupe de ressources hello, suivant hello même flux de travail pour les deux scénarios.</span><span class="sxs-lookup"><span data-stu-id="23e25-192">Assigning an RBAC role at a resource scope in Azure has an identical process for assigning hello role at hello subscription level or at hello resource group level, following hello same workflow for both scenarios.</span></span> <span data-ttu-id="23e25-193">Là encore, les utilisateurs hello qui sont affectés à hello RBAC rôle peuvent voir uniquement les éléments de hello qu’ils ont reçu accès, soit hello en **toutes les ressources** onglet ou directement dans leur tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="23e25-193">Again, hello users which are assigned hello RBAC role can see only hello items that they have been assigned access to, either in hello **All Resources** tab or directly in their dashboard.</span></span>

<span data-ttu-id="23e25-194">Un aspect important de RBAC à la fois à l’étendue de groupe de ressources ou de la portée de la ressource est pour le répertoire approprié de hello utilisateurs toomake que dans le toosign toohello.</span><span class="sxs-lookup"><span data-stu-id="23e25-194">An important aspect for RBAC both at resource group scope or resource scope is for hello users toomake sure toosign-in toohello correct directory.</span></span>





![connexion à un annuaire dans le portail azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/13.png)

## <a name="assign-rbac-roles-for-an-azure-active-directory-group"></a><span data-ttu-id="23e25-196">Attribuer des rôles RBAC pour un groupe Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="23e25-196">Assign RBAC roles for an Azure Active Directory group</span></span>
<span data-ttu-id="23e25-197">Tous les scénarios de hello à l’aide de RBAC dans hello trois différentes portées d’Azure offre des privilèges de hello de gérer, déployer et administrer les différentes ressources en tant qu’un utilisateur affecté sans hello ont besoin de gérer un abonnement personnel.</span><span class="sxs-lookup"><span data-stu-id="23e25-197">All hello scenarios using RBAC at hello three different scopes in Azure offer hello privilege of managing, deploying and administering various resources as an assigned user without hello need of managing a personal subscription.</span></span> <span data-ttu-id="23e25-198">Rôle RBAC hello quel que soit attribué pour un abonnement, le groupe de ressources ou la portée de la ressource, toutes les ressources hello créées davantage par les utilisateurs de hello affecté sont facturées sous hello un abonnement Azure où les utilisateurs de hello ont accès à.</span><span class="sxs-lookup"><span data-stu-id="23e25-198">Regardless hello RBAC role is assigned for a subscription, resource group or resource scope, all hello resources created further on by hello assigned users are billed under hello one Azure subscription where hello users have access to.</span></span> <span data-ttu-id="23e25-199">De cette manière, hello les utilisateurs disposant d’autorisations d’administrateur pour que tout abonnement Azure de facturation a une vue d’ensemble complète sur la consommation hello, quel que soit le qui gère les ressources hello.</span><span class="sxs-lookup"><span data-stu-id="23e25-199">This way, hello users who have billing administrator permissions for that entire Azure subscription has a complete overview on hello consumption, regardless who is managing hello resources.</span></span>

<span data-ttu-id="23e25-200">Pour les grandes entreprises, les rôles RBAC peuvent être appliquées dans hello identique pour les groupes Azure Active Directory tenant compte du point de vue hello utilisateur admin hello veut toogrant hello granulaire de l’accès pour les équipes ou les départements entiers, non pas individuellement pour chaque utilisateur, par conséquent, sa prise en compte en tant qu’extrêmement heure et la gestion efficace option.</span><span class="sxs-lookup"><span data-stu-id="23e25-200">For larger organizations, RBAC roles can be applied in hello same way for Azure Active Directory groups considering hello perspective that hello admin user wants toogrant hello granular access for teams or entire departments, not individually for each user, thus considering it as an extremely time and management efficient option.</span></span> <span data-ttu-id="23e25-201">tooillustrate cet exemple, le hello **collaborateur** rôle a été ajouté à tooone des groupes de hello dans client hello au niveau d’abonnement hello.</span><span class="sxs-lookup"><span data-stu-id="23e25-201">tooillustrate this example, hello **Contributor** role has been added tooone of hello groups in hello tenant at hello subscription level.</span></span>





![ajouter un rôle RBAC pour les groupes AAD](./media/role-based-access-control-create-custom-roles-for-internal-external-users/14.png)

<span data-ttu-id="23e25-203">Ces groupes sont des groupes de sécurité qui sont approvisionnés et gérés uniquement dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="23e25-203">These groups are security groups which are provisioned and managed only within Azure Active Directory.</span></span>

## <a name="create-a-custom-rbac-role-tooopen-support-requests-using-powershell"></a><span data-ttu-id="23e25-204">Créer un support de tooopen rôle RBAC personnalisé demandes à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="23e25-204">Create a custom RBAC role tooopen support requests using PowerShell</span></span>
<span data-ttu-id="23e25-205">rôles RBAC intégrés Hello, qui sont disponibles dans Azure Vérifiez certains niveaux d’autorisation basée sur les ressources disponibles hello dans l’environnement de hello.</span><span class="sxs-lookup"><span data-stu-id="23e25-205">hello built-in RBAC roles which are available in Azure ensure certain permission levels based on hello available resources in hello environment.</span></span> <span data-ttu-id="23e25-206">Toutefois, si aucun de ces rôles de besoins de l’utilisateur admin de hello, a hello option toolimit accès davantage en créant des rôles RBAC personnalisés.</span><span class="sxs-lookup"><span data-stu-id="23e25-206">However, if none of these roles suit hello admin user's needs, there is hello option toolimit access even more by creating custom RBAC roles.</span></span>

<span data-ttu-id="23e25-207">Création des rôles personnalisés RBAC nécessite tootake un rôle d’intégrés, modifier et puis l’importer dans un environnement de hello.</span><span class="sxs-lookup"><span data-stu-id="23e25-207">Creating custom RBAC roles requires tootake one built-in role, edit it and then import it back in hello environment.</span></span> <span data-ttu-id="23e25-208">transfert de Hello et téléchargement du rôle de hello sont gérés à l’aide de PowerShell ou CLI.</span><span class="sxs-lookup"><span data-stu-id="23e25-208">hello download and upload of hello role are managed using either PowerShell or CLI.</span></span>

<span data-ttu-id="23e25-209">Il est important toounderstand hello conditions préalables de la création d’un rôle personnalisé qui peuvent accorder un accès granulaire au niveau d’abonnement hello et également autoriser hello invité utilisateur hello flexibilité de l’ouverture de demandes de support.</span><span class="sxs-lookup"><span data-stu-id="23e25-209">It is important toounderstand hello prerequisites of creating a custom role which can grant granular access at hello subscription level and also allow hello invited user hello flexibility of opening support requests.</span></span>

<span data-ttu-id="23e25-210">Pour ce rôle intégré d’exemple hello **lecteur** qui permet aux utilisateurs accès tooview toutes les ressources hello étendues mais pas tooedit les ou créer de nouveaux a été personnalisé tooallow hello utilisateur hello le choix de prise en charge des demandes d’ouverture.</span><span class="sxs-lookup"><span data-stu-id="23e25-210">For this example hello built-in role **Reader** which allows users access tooview all hello resource scopes but not tooedit them or create new ones has been customized tooallow hello user hello option of opening support requests.</span></span>

<span data-ttu-id="23e25-211">Hello première action d’exportation hello **lecteur** toobe de besoins de rôle s’est terminée dans PowerShell a exécuté avec des autorisations élevées en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="23e25-211">hello first action of exporting hello **Reader** role needs toobe completed in PowerShell ran with elevated permissions as administrator.</span></span>

```
Login-AzureRMAccount

Get-AzureRMRoleDefinition -Name "Reader"

Get-AzureRMRoleDefinition -Name "Reader" | ConvertTo-Json | Out-File C:\rbacrole2.json

```





![Capture d’écran de PowerShell pour le rôle RBAC Lecteur](./media/role-based-access-control-create-custom-roles-for-internal-external-users/15.png)

<span data-ttu-id="23e25-213">Vous devez tooextract modèle JSON hello du rôle de hello.</span><span class="sxs-lookup"><span data-stu-id="23e25-213">Then you need tooextract hello JSON template of hello role.</span></span>





![Modèle JSON pour le rôle RBAC Lecteur personnalisé](./media/role-based-access-control-create-custom-roles-for-internal-external-users/16.png)

<span data-ttu-id="23e25-215">Un rôle RBAC classique comprend trois sections principales, **Actions**, **NotActions** et **AssignableScopes**.</span><span class="sxs-lookup"><span data-stu-id="23e25-215">A typical RBAC role is composed out of three main sections, **Actions**, **NotActions** and **AssignableScopes**.</span></span>

<span data-ttu-id="23e25-216">Bonjour **Action** section figurent tous hello opérations autorisées pour ce rôle.</span><span class="sxs-lookup"><span data-stu-id="23e25-216">In hello **Action** section are listed all hello permitted operations for this role.</span></span> <span data-ttu-id="23e25-217">Il est important toounderstand que chaque action est attribuée à partir d’un fournisseur de ressources.</span><span class="sxs-lookup"><span data-stu-id="23e25-217">It's important toounderstand that each action is assigned from a resource provider.</span></span> <span data-ttu-id="23e25-218">Dans ce cas, pour la création de prise en charge des tickets hello **Microsoft.Support** fournisseur de ressources doit être répertorié.</span><span class="sxs-lookup"><span data-stu-id="23e25-218">In this case, for creating support tickets hello **Microsoft.Support** resource provider must be listed.</span></span>

<span data-ttu-id="23e25-219">toosee en mesure de toobe tous hello des fournisseurs de ressources disponibles et enregistrés dans votre abonnement, vous pouvez utiliser PowerShell.</span><span class="sxs-lookup"><span data-stu-id="23e25-219">toobe able toosee all hello resource providers available and registered in your subscription, you can use PowerShell.</span></span>
```
Get-AzureRMResourceProvider

```
<span data-ttu-id="23e25-220">En outre, vous pouvez vérifier hello les hello disponible PowerShell applets de commande toomanage hello fournisseurs de ressources.</span><span class="sxs-lookup"><span data-stu-id="23e25-220">Additionally, you can check for hello all hello available PowerShell cmdlets toomanage hello resource providers.</span></span>
    <span data-ttu-id="23e25-221">![Capture d’écran de PowerShell pour la gestion de fournisseur de ressources](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)</span><span class="sxs-lookup"><span data-stu-id="23e25-221">![PowerShell screenshot for resource provider management](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)</span></span>

<span data-ttu-id="23e25-222">toorestrict tous hello actions pour un rôle RBAC particulier, les ressources fournisseurs sont répertoriés sous la section de hello **NotActions**.</span><span class="sxs-lookup"><span data-stu-id="23e25-222">toorestrict all hello actions for a particular RBAC role, resource providers are listed under hello section **NotActions**.</span></span>
<span data-ttu-id="23e25-223">Il est obligatoire de que ce rôle RBAC hello contient l’ID où il est utilisé d’un abonnement explicite hello.</span><span class="sxs-lookup"><span data-stu-id="23e25-223">Last, it's mandatory that hello RBAC role contains hello explicit subscription IDs where it is used.</span></span> <span data-ttu-id="23e25-224">ID d’abonnement Hello sont répertoriés sous hello **AssignableScopes**, sinon vous ne serez pas autorisé rôle de hello tooimport dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="23e25-224">hello subscription IDs are listed under hello **AssignableScopes**, otherwise you will not be allowed tooimport hello role in your subscription.</span></span>

<span data-ttu-id="23e25-225">Après la création et personnalisation du rôle RBAC hello, il a besoin d’un environnement de hello arrière importés de toobe.</span><span class="sxs-lookup"><span data-stu-id="23e25-225">After creating and customizing hello RBAC role, it needs toobe imported back hello environment.</span></span>

```
New-AzureRMRoleDefinition -InputFile "C:\rbacrole2.json"

```

<span data-ttu-id="23e25-226">Dans cet exemple, un nom personnalisé pour ce rôle RBAC hello est « lecteur prise en charge des tickets niveau d’accès « autorisant hello utilisateur tooview tous les éléments dans l’abonnement de hello et également les demandes de support tooopen.</span><span class="sxs-lookup"><span data-stu-id="23e25-226">In this example, hello custom name for this RBAC role is "Reader support tickets access level" allowing hello user tooview everything in hello subscription and also tooopen support requests.</span></span>

> [!NOTE]
> <span data-ttu-id="23e25-227">Hello uniquement deux rôles RBAC intégrés, autorisant ainsi une action hello d’ouverture de demandes de support sont **propriétaire** et **collaborateur**.</span><span class="sxs-lookup"><span data-stu-id="23e25-227">hello only two built-in RBAC roles allowing hello action of opening of support requests are **Owner** and **Contributor**.</span></span> <span data-ttu-id="23e25-228">Pour un utilisateur toobe tooopen en mesure de prise en charge les requêtes, il doit être affecté un rôle RBAC uniquement à l’étendue de l’abonnement hello, étant donné que toutes les demandes de prise en charge sont créées d’après un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="23e25-228">For a user toobe able tooopen support requests, he must be assigned an RBAC role only at hello subscription scope, because all support requests are created based on an Azure subscription.</span></span>

<span data-ttu-id="23e25-229">Ce nouveau rôle personnalisé a été affecté tooan utilisateur hello même répertoire.</span><span class="sxs-lookup"><span data-stu-id="23e25-229">This new custom role has been assigned tooan user from hello same directory.</span></span>





![capture d’écran du rôle RBAC personnalisé importé Bonjour portail Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/18.png)





![capture d’écran d’attribution personnalisée importé toouser de rôle RBAC Bonjour même répertoire](./media/role-based-access-control-create-custom-roles-for-internal-external-users/19.png)





![capture d’écran d’autorisations pour un rôle RBAC importé personnalisé](./media/role-based-access-control-create-custom-roles-for-internal-external-users/20.png)

<span data-ttu-id="23e25-233">exemple de Hello a été plus limites de hello tooemphasize détaillées de ce rôle RBAC personnalisé comme suit :</span><span class="sxs-lookup"><span data-stu-id="23e25-233">hello example has been further detailed tooemphasize hello limits of this custom RBAC role as follows:</span></span>
* <span data-ttu-id="23e25-234">Peut créer des demandes de support</span><span class="sxs-lookup"><span data-stu-id="23e25-234">Can create new support requests</span></span>
* <span data-ttu-id="23e25-235">Ne peut pas créer d’étendues de ressource (par exemple, machine virtuelle)</span><span class="sxs-lookup"><span data-stu-id="23e25-235">Can't create new resource scopes (for example: virtual machine)</span></span>
* <span data-ttu-id="23e25-236">Ne peut pas créer de groupes de ressources</span><span class="sxs-lookup"><span data-stu-id="23e25-236">Can't create new resource groups</span></span>





![capture d’écran d’un rôle RBAC personnalisé créant des demandes de support](./media/role-based-access-control-create-custom-roles-for-internal-external-users/21.png)





![capture d’écran du rôle RBAC personnalisé n’a pas pu toocreate machines virtuelles](./media/role-based-access-control-create-custom-roles-for-internal-external-users/22.png)





![capture d’écran du rôle RBAC personnalisé n’a pas pu toocreate RGs nouveau](./media/role-based-access-control-create-custom-roles-for-internal-external-users/23.png)

## <a name="create-a-custom-rbac-role-tooopen-support-requests-using-azure-cli"></a><span data-ttu-id="23e25-240">Créer un support de tooopen rôle RBAC personnalisé demandes à l’aide de CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="23e25-240">Create a custom RBAC role tooopen support requests using Azure CLI</span></span>
<span data-ttu-id="23e25-241">En cours d’exécution sur un Mac et sans avoir accès tooPowerShell, CLI d’Azure est toogo de façon hello.</span><span class="sxs-lookup"><span data-stu-id="23e25-241">Running on a Mac and without having access tooPowerShell, Azure CLI is hello way toogo.</span></span>

<span data-ttu-id="23e25-242">Hello étapes toocreate un rôle personnalisé sont hello identiques, avec hello seule exception que vous utilisez interface CLI rôle de hello ne peut être téléchargé dans un modèle JSON, mais il peuvent être affiché dans hello CLI.</span><span class="sxs-lookup"><span data-stu-id="23e25-242">hello steps toocreate a custom role are hello same, with hello sole exception that using CLI hello role can't be downloaded in a JSON template, but it can be viewed in hello CLI.</span></span>

<span data-ttu-id="23e25-243">Pour cet exemple, j’ai choisi rôle intégré de hello de **lecteur de sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="23e25-243">For this example I have chosen hello built-in role of **Backup Reader**.</span></span>

```

azure role show "backup reader" --json

```





![Capture d’écran d’interface de ligne de commande pour l’affichage du rôle Lecteur de secours (Backup Reader)](./media/role-based-access-control-create-custom-roles-for-internal-external-users/24.png)

<span data-ttu-id="23e25-245">Modifiez le rôle hello dans Visual Studio après avoir copié les propriétés hello dans un modèle JSON, hello **Microsoft.Support** fournisseur de ressources a été ajouté dans hello **Actions** sections afin que cet utilisateur peut ouvrir. demandes de support tout en continuant toobe un lecteur de coffres de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="23e25-245">Editing hello role in Visual Studio after copying hello proprieties in a JSON template, hello **Microsoft.Support** resource provider has been added in hello **Actions** sections so that this user can open support requests while continuing toobe a reader for hello backup vaults.</span></span> <span data-ttu-id="23e25-246">Là encore il est ID d’abonnement nécessaire tooadd hello où ce rôle sera utilisé dans hello **AssignableScopes** section.</span><span class="sxs-lookup"><span data-stu-id="23e25-246">Again it is necessary tooadd hello subscription ID where this role will be used in hello **AssignableScopes** section.</span></span>

```

azure role create --inputfile <path>

```





![Capture d’écran de l’Interface de ligne de commande pour l’importation de rôle RBAC personnalisé](./media/role-based-access-control-create-custom-roles-for-internal-external-users/25.png)

<span data-ttu-id="23e25-248">nouveau rôle de Hello est désormais disponible dans hello portail Azure et le processus d’attribution hello est hello même que dans les exemples précédents hello.</span><span class="sxs-lookup"><span data-stu-id="23e25-248">hello new role is now available in hello Azure portal and hello assignation process is hello same as in hello previous examples.</span></span>





![Capture d’écran du portail Azure montrant le rôle RBAC personnalisé créé à l’aide d’Azure CLI 1.0](./media/role-based-access-control-create-custom-roles-for-internal-external-users/26.png)

<span data-ttu-id="23e25-250">À compter de hello dernière Build 2017, hello Azure Cloud Shell est généralement disponible.</span><span class="sxs-lookup"><span data-stu-id="23e25-250">As of hello latest Build 2017, hello Azure Cloud Shell is generally available.</span></span> <span data-ttu-id="23e25-251">Azure Cloud Shell est un complément tooIDE et hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="23e25-251">Azure Cloud Shell is a complement tooIDE and hello Azure Portal.</span></span> <span data-ttu-id="23e25-252">Avec ce service, vous bénéficiez d’un interpréteur de commandes basé sur un navigateur, qui est authentifié et hébergé dans Azure, et que vous pouvez utiliser à la place de l’interface de ligne de commande installée sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="23e25-252">With this service, you get a browser-based shell that is authenticated and hosted within Azure and you can use it instead of CLI installed on your machine.</span></span>





![Azure Cloud Shell](./media/role-based-access-control-create-custom-roles-for-internal-external-users/27.png)
