---
title: "Informations d’identification du déploiement d’Azure App Service | Microsoft Docs"
description: "Apprenez à utiliser les informations d’identification du déploiement d’Azure App Service."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/05/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 86a2cd8ae9f97c606a378452e44eec8941700531
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-deployment-credentials-for-azure-app-service"></a><span data-ttu-id="ac394-103">Configurer les informations d’identification de déploiement pour Azure App Service</span><span class="sxs-lookup"><span data-stu-id="ac394-103">Configure deployment credentials for Azure App Service</span></span>
<span data-ttu-id="ac394-104">[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) prend en charge deux types d’informations d’identification pour le [déploiement Git local](app-service-deploy-local-git.md) et le [déploiement FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="ac394-104">[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) supports two types of credentials for [local Git deployment](app-service-deploy-local-git.md) and [FTP/S deployment](app-service-deploy-ftp.md).</span></span> <span data-ttu-id="ac394-105">Ils ne sont pas les mêmes que vos informations d’identification Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ac394-105">These are not the same as your Azure Active Directory credentials.</span></span>

* <span data-ttu-id="ac394-106">**Informations d’identification au niveau de l’utilisateur** : un seul ensemble d’informations d’identification pour l’intégralité du compte Azure.</span><span class="sxs-lookup"><span data-stu-id="ac394-106">**User-level credentials**: one set of credentials for the entire Azure account.</span></span> <span data-ttu-id="ac394-107">Il peut être utilisé pour déployer sur App Service pour n’importe quelle application et dans n’importe quel abonnement auxquels le compte Azure est autorisé à accéder.</span><span class="sxs-lookup"><span data-stu-id="ac394-107">It can be used to deploy to App Service for any app, in any subscription, that the Azure account has permission to access.</span></span> <span data-ttu-id="ac394-108">Il s’agit de l’ensemble d’informations d’identification par défaut que vous configurez dans **App Services** > **&lt;nom_application>** > **Informations d’identification de déploiement**.</span><span class="sxs-lookup"><span data-stu-id="ac394-108">These are the default credentials set that you configure in **App Services** > **&lt;app_name>** > **Deployment credentials**.</span></span> <span data-ttu-id="ac394-109">C’est également l’ensemble par défaut qui est présenté dans l’interface utilisateur graphique du portail, comme la **vue d’ensemble** et les **propriétés** du [panneau Ressources](../azure-resource-manager/resource-group-portal.md#manage-resources) de votre application.</span><span class="sxs-lookup"><span data-stu-id="ac394-109">This is also the default set that's surfaced in the portal GUI (such as the **Overview** and **Properties** of your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources)).</span></span>

    > [!NOTE]
    > <span data-ttu-id="ac394-110">Lorsque vous déléguez l’accès aux ressources Azure au moyen du contrôle d’accès en fonction du rôle (RBAC) ou des autorisations de coadministrateur, chaque utilisateur Azure recevant l’accès à une application peut utiliser ses informations d’identification personnelles jusqu’à la révocation de l’accès.</span><span class="sxs-lookup"><span data-stu-id="ac394-110">When you delegate access to Azure resources via Role Based Access Control (RBAC) or co-admin permissions, each Azure user that receives access to an app can use his/her personal user-level credentials until access is revoked.</span></span> <span data-ttu-id="ac394-111">Ces informations d’identification de déploiement ne doivent pas être partagées avec d’autres utilisateurs Azure.</span><span class="sxs-lookup"><span data-stu-id="ac394-111">These deployment credentials should not be shared with other Azure users.</span></span>
    >
    >

* <span data-ttu-id="ac394-112">**Informations d’identification au niveau de l’application** : un seul ensemble d’informations d’identification pour chaque application.</span><span class="sxs-lookup"><span data-stu-id="ac394-112">**App-level credentials**: one set of credentials for each app.</span></span> <span data-ttu-id="ac394-113">Celui-ci peut être utilisé pour déployer sur cette application uniquement.</span><span class="sxs-lookup"><span data-stu-id="ac394-113">It can be used to deploy to that app only.</span></span> <span data-ttu-id="ac394-114">Les informations d’identification de chaque application sont générées automatiquement lors de la création de l’application et se trouvent dans le profil de publication de l’application.</span><span class="sxs-lookup"><span data-stu-id="ac394-114">The credentials for each app is generated automatically at app creation, and is found in the app's publish profile.</span></span> <span data-ttu-id="ac394-115">Vous ne pouvez pas configurer manuellement les informations d’identification, mais vous pouvez les réinitialiser à tout moment pour une application.</span><span class="sxs-lookup"><span data-stu-id="ac394-115">You cannot manually configure the credentials, but you can reset them for an app anytime.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ac394-116">Pour autoriser quelqu’un à accéder à ces informations d’identification via le contrôle d’accès en fonction du rôle (RBAC), vous devez lui accorder au moins le rôle Collaborateur sur l’application Web.</span><span class="sxs-lookup"><span data-stu-id="ac394-116">In order to give someone access to these credentials via Role Based Access Control (RBAC), you need to make them contributor or higher on the Web App.</span></span> <span data-ttu-id="ac394-117">Les lecteurs ne sont pas autorisés à publier et n’ont donc pas accès à ces informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="ac394-117">Readers are not allowed to publish, and hence can't access those credentials.</span></span>
    >
    >

## <span data-ttu-id="ac394-118"><a name="userscope"></a>Définir et réinitialiser les informations d’identification au niveau de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="ac394-118"><a name="userscope"></a>Set and reset user-level credentials</span></span>

<span data-ttu-id="ac394-119">Vous pouvez configurer vos informations d’identification au niveau de l’utilisateur dans le [panneau Ressources](../azure-resource-manager/resource-group-portal.md#manage-resources) d’une application.</span><span class="sxs-lookup"><span data-stu-id="ac394-119">You can configure your user-level credentials in any app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span> <span data-ttu-id="ac394-120">Quelle que soit l’application dans laquelle vous configurez ces informations d’identification, ces dernières s’appliquent à toutes les applications et à tous les abonnements de votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="ac394-120">Regardless in which app you configure these credentials, it applies to all apps and for all subscriptions in your Azure account.</span></span> 

<span data-ttu-id="ac394-121">Pour configurer les informations d’identification au niveau de l’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="ac394-121">To configure your user-level credentials:</span></span>

1. <span data-ttu-id="ac394-122">Dans le [portail Azure](https://portal.azure.com), cliquez sur App Service > **&lt;une application>** > **Informations d’identification de déploiement**.</span><span class="sxs-lookup"><span data-stu-id="ac394-122">In the [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Deployment credentials**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ac394-123">Dans le portail, vous devez disposer d’au moins une application avant de pouvoir accéder au panneau Informations d’identification de déploiement.</span><span class="sxs-lookup"><span data-stu-id="ac394-123">In the portal, you must have at least one app before you can access the deployment credentials blade.</span></span> <span data-ttu-id="ac394-124">Toutefois, avec l’[interface de ligne de commande Azure](app-service-web-app-azure-resource-manager-xplat-cli.md), vous pouvez configurer les informations d’identification au niveau de l’utilisateur sans application existante.</span><span class="sxs-lookup"><span data-stu-id="ac394-124">However, with the [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md), you can configure user-level credentials without an existing app.</span></span>

2. <span data-ttu-id="ac394-125">Configurez le nom d’utilisateur et le mot de passe, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="ac394-125">Configure the user name and password, and then click **Save**.</span></span>

    ![](./media/app-service-deployment-credentials/deployment_credentials_configure.png)

<span data-ttu-id="ac394-126">Une fois que vous avez défini vos informations d’identification de déploiement, vous pouvez trouver le nom d’utilisateur du déploiement *Git* dans la **vue d’ensemble** de votre application</span><span class="sxs-lookup"><span data-stu-id="ac394-126">Once you have set your deployment credentials, you can find the *Git* deployment username in your app's **Overview**,</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_overview.png)

<span data-ttu-id="ac394-127">et le nom d’utilisateur de déploiement *FTP* dans les **propriétés** de votre application.</span><span class="sxs-lookup"><span data-stu-id="ac394-127">and and *FTP* deployment username in your app's **Properties**.</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_properties.png)

> [!NOTE]
> <span data-ttu-id="ac394-128">Azure n’affiche pas votre mot de passe du déploiement au niveau de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ac394-128">Azure does not show your user-level deployment password.</span></span> <span data-ttu-id="ac394-129">Si vous oubliez le mot de passe, vous ne pouvez pas le récupérer.</span><span class="sxs-lookup"><span data-stu-id="ac394-129">If you forget the password, you can't retrieve it.</span></span> <span data-ttu-id="ac394-130">Toutefois, vous pouvez réinitialiser vos informations d’identification en suivant les étapes décrites dans cette section.</span><span class="sxs-lookup"><span data-stu-id="ac394-130">However, you can reset your credentials by following the steps in this section.</span></span>
>
>  

## <span data-ttu-id="ac394-131"><a name="appscope"></a>Obtenir et réinitialiser les informations d’identification au niveau de l’application</span><span class="sxs-lookup"><span data-stu-id="ac394-131"><a name="appscope"></a>Get and reset app-level credentials</span></span>
<span data-ttu-id="ac394-132">Pour chaque application dans App Service, les informations d’identification au niveau de l’application sont stockées dans le profil de publication XML.</span><span class="sxs-lookup"><span data-stu-id="ac394-132">For each app in App Service, its app-level credentials are stored in the XML publish profile.</span></span>

<span data-ttu-id="ac394-133">Pour obtenir les informations d’identification au niveau de l’application :</span><span class="sxs-lookup"><span data-stu-id="ac394-133">To get the app-level credentials:</span></span>

1. <span data-ttu-id="ac394-134">Dans le [portail Azure](https://portal.azure.com), cliquez sur App Service > **&lt;une application>** > **Vue d’ensemble**.</span><span class="sxs-lookup"><span data-stu-id="ac394-134">In the [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="ac394-135">Cliquez sur **...Plus** > **Obtenir le profil de publication**. Le téléchargement du fichier .PublishSettings démarre.</span><span class="sxs-lookup"><span data-stu-id="ac394-135">Click **...More** > **Get publish profile**, and download starts for a .PublishSettings file.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_get.png)

3. <span data-ttu-id="ac394-136">Ouvrez le fichier .PublishSettings, puis recherchez la balise `<publishProfile>` avec l’attribut `publishMethod="FTP"`.</span><span class="sxs-lookup"><span data-stu-id="ac394-136">Open the .PublishSettings file and find the `<publishProfile>` tag with the attribute `publishMethod="FTP"`.</span></span> <span data-ttu-id="ac394-137">Obtenez ensuite ses attributs `userName` et `password`.</span><span class="sxs-lookup"><span data-stu-id="ac394-137">Then, get its `userName` and `password` attributes.</span></span>
<span data-ttu-id="ac394-138">Il s’agit des informations d’identification au niveau de l’application.</span><span class="sxs-lookup"><span data-stu-id="ac394-138">These are the app-level credentials.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_editor.png)

    <span data-ttu-id="ac394-139">Comme pour les informations d’identification au niveau de l’utilisateur, le nom d’utilisateur du déploiement FTP est au format `<app_name>\<username>` et le nom d’utilisateur du déploiement Git est `<username>` sans `<app_name>\`.</span><span class="sxs-lookup"><span data-stu-id="ac394-139">Similar to the user-level credentials, the FTP deployment username is in the format of `<app_name>\<username>`, and the Git deployment username is just `<username>` without the preceding `<app_name>\`.</span></span>

<span data-ttu-id="ac394-140">Pour réinitialiser les informations d’identification au niveau de l’application :</span><span class="sxs-lookup"><span data-stu-id="ac394-140">To reset the app-level credentials:</span></span>

1. <span data-ttu-id="ac394-141">Dans le [portail Azure](https://portal.azure.com), cliquez sur App Service > **&lt;une application>** > **Vue d’ensemble**.</span><span class="sxs-lookup"><span data-stu-id="ac394-141">In the [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="ac394-142">Cliquez sur **...Plus** > **Réinitialiser le profil de publication**.</span><span class="sxs-lookup"><span data-stu-id="ac394-142">Click **...More** > **Reset publish profile**.</span></span> <span data-ttu-id="ac394-143">Cliquez sur **Oui** pour confirmer la réinitialisation.</span><span class="sxs-lookup"><span data-stu-id="ac394-143">Click **Yes** to confirm the reset.</span></span>

    <span data-ttu-id="ac394-144">L’action de réinitialisation invalide les fichiers .PublishSettings précédemment téléchargés.</span><span class="sxs-lookup"><span data-stu-id="ac394-144">The reset action invalidates any previously-downloaded .PublishSettings files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac394-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ac394-145">Next steps</span></span>

<span data-ttu-id="ac394-146">Découvrez comment utiliser ces informations d’identification pour déployer votre application à partir de [Git local](app-service-deploy-local-git.md) ou à l’aide de [FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="ac394-146">Find out how to use these credentials to deploy your app from [local Git](app-service-deploy-local-git.md) or using [FTP/S](app-service-deploy-ftp.md).</span></span>
