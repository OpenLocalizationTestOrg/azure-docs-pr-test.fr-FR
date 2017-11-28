---
title: "Gestion des noms de domaine personnalisés dans Azure Active Directory | Microsoft Docs"
description: "Concepts de gestion et procédures pour gérer un domaine personnalisé dans Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cf3523bd-9ee0-439e-963d-ccea038867b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 5ae19bb370064de96cf466ca09b13d02563d65a4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a><span data-ttu-id="f91cf-103">Gestion des noms de domaine personnalisés dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f91cf-103">Managing custom domain names in your Azure Active Directory</span></span>
<span data-ttu-id="f91cf-104">Un nom de domaine peut être un identificateur important pour de nombreuses ressources de répertoire, lorsqu’il est compris dans :</span><span class="sxs-lookup"><span data-stu-id="f91cf-104">A domain name can be an important identifier for many directory resources, as part of:</span></span>

* <span data-ttu-id="f91cf-105">Un nom d’utilisateur ou une adresse e-mail d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="f91cf-105">A user name or email address for a user</span></span>
* <span data-ttu-id="f91cf-106">L’adresse d’un groupe</span><span class="sxs-lookup"><span data-stu-id="f91cf-106">The address for a group</span></span>
* <span data-ttu-id="f91cf-107">L’URI ID d’application pour une application</span><span class="sxs-lookup"><span data-stu-id="f91cf-107">The app ID URI for an application</span></span>

<span data-ttu-id="f91cf-108">Une ressource dans Azure Active Directory (Azure AD) peut inclure un nom de domaine déjà vérifié comme appartenant au répertoire qui contient la ressource.</span><span class="sxs-lookup"><span data-stu-id="f91cf-108">A resource in Azure Active Directory (Azure AD) can include a domain name that is already verified to be owned by the directory that contains the resource.</span></span> <span data-ttu-id="f91cf-109">Seul un administrateur général peut effectuer des tâches de gestion de domaine dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f91cf-109">Only a global administrator can perform domain management tasks in Azure AD.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f91cf-110">Microsoft recommande de gérer Azure AD à l’aide du [Centre d’administration Azure AD](https://aad.portal.azure.com) dans le portail Azure au lieu d’utiliser le portail Azure classique référencé dans cet article.</span><span class="sxs-lookup"><span data-stu-id="f91cf-110">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> <span data-ttu-id="f91cf-111">Pour savoir comment gérer vos noms de domaine dans le centre d’administration Azure AD, consultez la section [Gestion des noms de domaines personnalisés dans Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f91cf-111">For how to manage your domain names in the Azure AD admin center, see [Managing custom domain names in your Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span></span>

## <a name="set-the-primary-domain-name-for-your-azure-ad-directory"></a><span data-ttu-id="f91cf-112">Définir le nom de domaine principal pour votre répertoire Azure AD</span><span class="sxs-lookup"><span data-stu-id="f91cf-112">Set the primary domain name for your Azure AD directory</span></span>
<span data-ttu-id="f91cf-113">Lors de la création du répertoire, le nom de domaine initial, par exemple « contoso.onmicrosoft.com », est également le nom de domaine principal de votre répertoire.</span><span class="sxs-lookup"><span data-stu-id="f91cf-113">When your directory is created, the initial domain name, such as ‘contoso.onmicrosoft.com,’ is also the primary domain name for your directory.</span></span> <span data-ttu-id="f91cf-114">Le domaine principal est le nom de domaine par défaut pour un nouvel utilisateur lorsque vous créez un utilisateur dans le [portail Azure Classic](https://manage.windowsazure.com/), ou dans d’autres portails, tels que le portail d’administration d’Office 365.</span><span class="sxs-lookup"><span data-stu-id="f91cf-114">The primary domain is the default domain name for a new user when you create a new user in the [Azure classic portal](https://manage.windowsazure.com/), or other portals such as the Office 365 admin portal.</span></span> <span data-ttu-id="f91cf-115">Cela simplifie le processus permettant à un administrateur de créer des utilisateurs dans le portail.</span><span class="sxs-lookup"><span data-stu-id="f91cf-115">This streamlines the process for an administrator to create new users in the portal.</span></span>

<span data-ttu-id="f91cf-116">Pour modifier le nom de domaine principal dans votre répertoire, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f91cf-116">To change the primary domain name for your directory:</span></span>

1. <span data-ttu-id="f91cf-117">Connectez-vous au [portail Azure Classic](https://manage.windowsazure.com/) avec un compte d’administrateur général pour votre répertoire Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f91cf-117">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) with a user account that is a global administrator of your Azure AD directory.</span></span>
2. <span data-ttu-id="f91cf-118">Sélectionnez **Active Directory** dans le volet de navigation gauche.</span><span class="sxs-lookup"><span data-stu-id="f91cf-118">Select **Active Directory** on the left navigation bar.</span></span>
3. <span data-ttu-id="f91cf-119">Ouvrez votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="f91cf-119">Open your directory.</span></span>
4. <span data-ttu-id="f91cf-120">Sélectionnez l’onglet **Domaines** .</span><span class="sxs-lookup"><span data-stu-id="f91cf-120">Select the **Domains** tab.</span></span>
5. <span data-ttu-id="f91cf-121">Sélectionnez le bouton **Modifier le principal** sur la barre de commandes.</span><span class="sxs-lookup"><span data-stu-id="f91cf-121">Select the **Change primary** button on the command bar.</span></span>
6. <span data-ttu-id="f91cf-122">Sélectionnez le domaine que vous souhaitez utiliser comme nouveau domaine principal pour votre répertoire.</span><span class="sxs-lookup"><span data-stu-id="f91cf-122">Select the domain that you want to be the new primary domain for your directory.</span></span>

<span data-ttu-id="f91cf-123">Vous pouvez modifier le nom de domaine principal de votre répertoire en n’importe quel domaine personnalisé vérifié qui n’est pas fédéré.</span><span class="sxs-lookup"><span data-stu-id="f91cf-123">You can change the primary domain name for your directory to be any verified custom domain that is not federated.</span></span> <span data-ttu-id="f91cf-124">La modification du domaine principal de votre répertoire ne changera pas les noms des utilisateurs existants.</span><span class="sxs-lookup"><span data-stu-id="f91cf-124">Changing the primary domain for your directory will not change the user names for any existing users.</span></span>

## <a name="add-custom-domain-names-to-your-azure-ad"></a><span data-ttu-id="f91cf-125">Ajouter des noms de domaine personnalisés à Azure AD</span><span class="sxs-lookup"><span data-stu-id="f91cf-125">Add custom domain names to your Azure AD</span></span>
<span data-ttu-id="f91cf-126">Vous pouvez ajouter jusqu’à 900 noms de domaine personnalisés à chaque répertoire Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f91cf-126">You can add up to 900 custom domain names to each Azure AD directory.</span></span> <span data-ttu-id="f91cf-127">Le processus permettant d’ [ajouter un nom de domaine personnalisé supplémentaire](active-directory-add-domain.md) est le même pour le premier nom de domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="f91cf-127">The process to [add an additional custom domain name](active-directory-add-domain.md) is the same for the first custom domain name.</span></span>

## <a name="add-subdomains-of-a-custom-domain"></a><span data-ttu-id="f91cf-128">Ajouter des sous-domaines d’un domaine personnalisé</span><span class="sxs-lookup"><span data-stu-id="f91cf-128">Add subdomains of a custom domain</span></span>
<span data-ttu-id="f91cf-129">Si vous souhaitez ajouter un nom de domaine de troisième niveau, tel que « europe.contoso.com » à votre répertoire, vous devez tout d’abord ajouter et vérifier le domaine de second niveau, tel que contoso.com.</span><span class="sxs-lookup"><span data-stu-id="f91cf-129">If you want to add a third-level domain name such as ‘europe.contoso.com’ to your directory, you should first add and verify the second-level domain, such as contoso.com.</span></span> <span data-ttu-id="f91cf-130">Le sous-domaine est automatiquement vérifié par Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f91cf-130">The subdomain will be automatically verified by Azure AD.</span></span> <span data-ttu-id="f91cf-131">Pour voir que le sous-domaine que vous venez d’ajouter a été vérifié, actualisez la page dans le navigateur qui répertorie les domaines de votre répertoire.</span><span class="sxs-lookup"><span data-stu-id="f91cf-131">To see that the subdomain that you just added has been verified, refresh the page in the browser that lists the domains in your directory.</span></span>

## <a name="what-to-do-if-you-change-the-dns-registrar-for-your-custom-domain-name"></a><span data-ttu-id="f91cf-132">Que faire en cas de modification du bureau d’enregistrement DNS pour votre nom de domaine personnalisé ?</span><span class="sxs-lookup"><span data-stu-id="f91cf-132">What to do if you change the DNS registrar for your custom domain name</span></span>
<span data-ttu-id="f91cf-133">Si vous modifiez le bureau d’enregistrement DNS de votre nom de domaine personnalisé, vous pouvez continuer à utiliser votre nom de domaine personnalisé sans interruption et sans tâches de configuration supplémentaires dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f91cf-133">If you change the DNS registrar for your custom domain name, you can continue to use your custom domain name with Azure AD itself without interruption and without additional configuration tasks.</span></span> <span data-ttu-id="f91cf-134">Si vous utilisez votre nom de domaine personnalisé avec Office 365, Intune ou autres services s’appuyant sur des noms de domaine personnalisés dans Azure AD, reportez-vous à la documentation de ces services.</span><span class="sxs-lookup"><span data-stu-id="f91cf-134">If you use your custom domain name with Office 365, Intune, or other services that rely on custom domain names in Azure AD, refer to the documentation for those services.</span></span>

## <a name="delete-a-custom-domain-name"></a><span data-ttu-id="f91cf-135">Supprimer un nom de domaine personnalisé</span><span class="sxs-lookup"><span data-stu-id="f91cf-135">Delete a custom domain name</span></span>
<span data-ttu-id="f91cf-136">Vous pouvez supprimer un nom de domaine personnalisé de votre répertoire Azure AD si votre organisation n’utilise plus ce nom de domaine ou si vous souhaitez l’utiliser avec un autre répertoire Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f91cf-136">You can delete a custom domain name from your Azure AD if your organization no longer uses that domain name, or if you need to use that domain name with another Azure AD.</span></span>

<span data-ttu-id="f91cf-137">Pour supprimer un nom de domaine personnalisé, vous devez d’abord vous assurer qu’aucune des ressources de votre répertoire ne s’appuie sur le nom de domaine.</span><span class="sxs-lookup"><span data-stu-id="f91cf-137">To delete a custom domain name, you must first ensure that no resources in your directory rely on the domain name.</span></span> <span data-ttu-id="f91cf-138">Vous ne pouvez pas supprimer un nom de domaine de votre répertoire si :</span><span class="sxs-lookup"><span data-stu-id="f91cf-138">You can't delete a domain name from your directory if:</span></span>

* <span data-ttu-id="f91cf-139">L’utilisateur dispose d’un nom d’utilisateur, d’une adresse de messagerie ou d’une adresse de proxy qui incluent le nom de domaine.</span><span class="sxs-lookup"><span data-stu-id="f91cf-139">Any user has a user name, email address, or proxy address that include the domain name.</span></span>
* <span data-ttu-id="f91cf-140">Le groupe dispose d’une adresse de messagerie ou d’une adresse de proxy qui incluent le nom de domaine.</span><span class="sxs-lookup"><span data-stu-id="f91cf-140">Any group has an email address or proxy address that includes the domain name.</span></span>
* <span data-ttu-id="f91cf-141">Une application dans Azure AD dispose d’une URI ID d’application qui inclut le nom de domaine.</span><span class="sxs-lookup"><span data-stu-id="f91cf-141">Any application in your Azure AD has an app ID URI that includes the domain name.</span></span>

<span data-ttu-id="f91cf-142">Vous devez modifier ou supprimer n’importe quelle ressource de ce type dans votre répertoire Azure AD pour pouvoir supprimer le nom de domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="f91cf-142">You must change or delete any such resource in your Azure AD directory before you can delete the custom domain name.</span></span>

## <a name="use-powershell-or-graph-api-to-manage-domain-names"></a><span data-ttu-id="f91cf-143">Utiliser PowerShell ou API Graph pour gérer les noms de domaine</span><span class="sxs-lookup"><span data-stu-id="f91cf-143">Use PowerShell or Graph API to manage domain names</span></span>
<span data-ttu-id="f91cf-144">La plupart des tâches de gestion des noms de domaine dans Azure Active Directory peuvent également être accomplies à l’aide de Microsoft PowerShell, ou encore par programmation à l’aide d’API Graph d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f91cf-144">Most management tasks for domain names in Azure Active Directory can also be completed using Microsoft PowerShell, or programmatically using Azure AD Graph API.</span></span>

* [<span data-ttu-id="f91cf-145">Utilisation de PowerShell pour gérer les noms de domaine dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="f91cf-145">Using PowerShell to manage domain names in Azure AD</span></span>](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [<span data-ttu-id="f91cf-146">Utilisation d’API Graph pour gérer les noms de domaine dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="f91cf-146">Using Graph API to manage domain names in Azure AD</span></span>](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a><span data-ttu-id="f91cf-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f91cf-147">Next steps</span></span>
* [<span data-ttu-id="f91cf-148">En savoir plus sur les noms de domaine dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="f91cf-148">Learn about domain names in Azure AD</span></span>](active-directory-add-domain-concepts.md)
* [<span data-ttu-id="f91cf-149">Gérer les noms de domaine personnalisés</span><span class="sxs-lookup"><span data-stu-id="f91cf-149">Manage custom domain names</span></span>](active-directory-add-manage-domain-names.md)

