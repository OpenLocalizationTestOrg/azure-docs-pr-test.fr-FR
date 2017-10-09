---
title: "aaaAzure informations d’identification de déploiement de Service application | Documents Microsoft"
description: "Découvrez comment toouse hello les informations d’identification de déploiement du Service d’applications Azure."
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
ms.openlocfilehash: d6f9f5cc1b62a17c42643266f4c9490f827c63f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-deployment-credentials-for-azure-app-service"></a><span data-ttu-id="ab690-103">Configurer les informations d’identification de déploiement pour Azure App Service</span><span class="sxs-lookup"><span data-stu-id="ab690-103">Configure deployment credentials for Azure App Service</span></span>
<span data-ttu-id="ab690-104">[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) prend en charge deux types d’informations d’identification pour le [déploiement Git local](app-service-deploy-local-git.md) et le [déploiement FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="ab690-104">[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) supports two types of credentials for [local Git deployment](app-service-deploy-local-git.md) and [FTP/S deployment](app-service-deploy-ftp.md).</span></span> <span data-ttu-id="ab690-105">Ceux-ci ne sont pas hello identique à vos informations d’identification Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ab690-105">These are not hello same as your Azure Active Directory credentials.</span></span>

* <span data-ttu-id="ab690-106">**Informations d’identification au niveau utilisateur**: un ensemble d’informations d’identification pour l’intégralité du compte Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ab690-106">**User-level credentials**: one set of credentials for hello entire Azure account.</span></span> <span data-ttu-id="ab690-107">Il peut être utilisé toodeploy tooApp Service pour n’importe quelle application, dans n’importe quel abonnement hello compte Azure a tooaccess d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="ab690-107">It can be used toodeploy tooApp Service for any app, in any subscription, that hello Azure account has permission tooaccess.</span></span> <span data-ttu-id="ab690-108">Il s’agit de jeu d’informations d’identification de par défaut hello que vous configurez dans **des Services d’application** > **&lt;nom_application >** > **informations d’identification de déploiement**.</span><span class="sxs-lookup"><span data-stu-id="ab690-108">These are hello default credentials set that you configure in **App Services** > **&lt;app_name>** > **Deployment credentials**.</span></span> <span data-ttu-id="ab690-109">Cela est hello également l’ensemble par défaut qui apparaît dans le portail hello l’interface graphique utilisateur (par exemple hello **vue d’ensemble** et **propriétés** de votre application [panneau des ressources](../azure-resource-manager/resource-group-portal.md#manage-resources)).</span><span class="sxs-lookup"><span data-stu-id="ab690-109">This is also hello default set that's surfaced in hello portal GUI (such as hello **Overview** and **Properties** of your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources)).</span></span>

    > [!NOTE]
    > <span data-ttu-id="ab690-110">Lorsque vous déléguez accéder aux ressources de tooAzure via le contrôle d’accès en fonction rôle (RBAC) ou des autorisations de coadministrateur, chaque utilisateur de Azure qui reçoit l’accès tooan application peut utiliser ses informations d’identification au niveau utilisateur personnelles jusqu'à ce que l’accès est révoqué.</span><span class="sxs-lookup"><span data-stu-id="ab690-110">When you delegate access tooAzure resources via Role Based Access Control (RBAC) or co-admin permissions, each Azure user that receives access tooan app can use his/her personal user-level credentials until access is revoked.</span></span> <span data-ttu-id="ab690-111">Ces informations d’identification de déploiement ne doivent pas être partagées avec d’autres utilisateurs Azure.</span><span class="sxs-lookup"><span data-stu-id="ab690-111">These deployment credentials should not be shared with other Azure users.</span></span>
    >
    >

* <span data-ttu-id="ab690-112">**Informations d’identification au niveau de l’application** : un seul ensemble d’informations d’identification pour chaque application.</span><span class="sxs-lookup"><span data-stu-id="ab690-112">**App-level credentials**: one set of credentials for each app.</span></span> <span data-ttu-id="ab690-113">Il peut être utilisé toodeploy toothat application uniquement.</span><span class="sxs-lookup"><span data-stu-id="ab690-113">It can be used toodeploy toothat app only.</span></span> <span data-ttu-id="ab690-114">informations d’identification Hello pour chaque application est générée automatiquement lors de la création de l’application et se trouve dans l’application hello profil de publication.</span><span class="sxs-lookup"><span data-stu-id="ab690-114">hello credentials for each app is generated automatically at app creation, and is found in hello app's publish profile.</span></span> <span data-ttu-id="ab690-115">Vous ne pouvez pas configurer manuellement les informations d’identification de hello, mais vous pouvez le réinitialiser à tout moment pour une application.</span><span class="sxs-lookup"><span data-stu-id="ab690-115">You cannot manually configure hello credentials, but you can reset them for an app anytime.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ab690-116">Dans l’ordre toogive quelqu'un d’informations d’identification de toothese via basé accès contrôle rôle (RBAC) d’accès, vous devez toomake les collaborateurs ou une version ultérieure sur hello Web App.</span><span class="sxs-lookup"><span data-stu-id="ab690-116">In order toogive someone access toothese credentials via Role Based Access Control (RBAC), you need toomake them contributor or higher on hello Web App.</span></span> <span data-ttu-id="ab690-117">Lecteurs toopublish ne sont pas autorisés et par conséquent, ne peut pas accéder à ces informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="ab690-117">Readers are not allowed toopublish, and hence can't access those credentials.</span></span>
    >
    >

## <span data-ttu-id="ab690-118"><a name="userscope"></a>Définir et réinitialiser les informations d’identification au niveau de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="ab690-118"><a name="userscope"></a>Set and reset user-level credentials</span></span>

<span data-ttu-id="ab690-119">Vous pouvez configurer vos informations d’identification au niveau de l’utilisateur dans le [panneau Ressources](../azure-resource-manager/resource-group-portal.md#manage-resources) d’une application.</span><span class="sxs-lookup"><span data-stu-id="ab690-119">You can configure your user-level credentials in any app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span> <span data-ttu-id="ab690-120">Quel que soit dans l’application, vous configurez ces informations d’identification, il applique les applications tooall et pour tous les abonnements dans votre Azure compte.</span><span class="sxs-lookup"><span data-stu-id="ab690-120">Regardless in which app you configure these credentials, it applies tooall apps and for all subscriptions in your Azure account.</span></span> 

<span data-ttu-id="ab690-121">tooconfigure vos informations d’identification au niveau de l’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="ab690-121">tooconfigure your user-level credentials:</span></span>

1. <span data-ttu-id="ab690-122">Bonjour [portail Azure](https://portal.azure.com), cliquez sur le Service d’applications >  **&lt;any_app >** > **informations d’identification de déploiement**.</span><span class="sxs-lookup"><span data-stu-id="ab690-122">In hello [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Deployment credentials**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ab690-123">Dans le portail hello, vous devez disposer au moins une application avant que vous pouvez accéder au panneau informations d’identification de déploiement hello.</span><span class="sxs-lookup"><span data-stu-id="ab690-123">In hello portal, you must have at least one app before you can access hello deployment credentials blade.</span></span> <span data-ttu-id="ab690-124">Toutefois, avec hello [CLI d’Azure](app-service-web-app-azure-resource-manager-xplat-cli.md), vous pouvez configurer les informations d’identification au niveau de l’utilisateur sans une application existante.</span><span class="sxs-lookup"><span data-stu-id="ab690-124">However, with hello [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md), you can configure user-level credentials without an existing app.</span></span>

2. <span data-ttu-id="ab690-125">Configurer le nom d’utilisateur hello et le mot de passe, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="ab690-125">Configure hello user name and password, and then click **Save**.</span></span>

    ![](./media/app-service-deployment-credentials/deployment_credentials_configure.png)

<span data-ttu-id="ab690-126">Une fois que vous avez défini vos informations d’identification de déploiement, vous pouvez trouver hello *Git* nom d’utilisateur de déploiement dans votre application **vue d’ensemble**,</span><span class="sxs-lookup"><span data-stu-id="ab690-126">Once you have set your deployment credentials, you can find hello *Git* deployment username in your app's **Overview**,</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_overview.png)

<span data-ttu-id="ab690-127">et le nom d’utilisateur de déploiement *FTP* dans les **propriétés** de votre application.</span><span class="sxs-lookup"><span data-stu-id="ab690-127">and and *FTP* deployment username in your app's **Properties**.</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_properties.png)

> [!NOTE]
> <span data-ttu-id="ab690-128">Azure n’affiche pas votre mot de passe du déploiement au niveau de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ab690-128">Azure does not show your user-level deployment password.</span></span> <span data-ttu-id="ab690-129">Si vous oubliez le mot de passe hello, vous ne pouvez pas le récupérer.</span><span class="sxs-lookup"><span data-stu-id="ab690-129">If you forget hello password, you can't retrieve it.</span></span> <span data-ttu-id="ab690-130">Toutefois, vous pouvez réinitialiser vos informations d’identification en suivant les étapes de hello dans cette section.</span><span class="sxs-lookup"><span data-stu-id="ab690-130">However, you can reset your credentials by following hello steps in this section.</span></span>
>
>  

## <span data-ttu-id="ab690-131"><a name="appscope"></a>Obtenir et réinitialiser les informations d’identification au niveau de l’application</span><span class="sxs-lookup"><span data-stu-id="ab690-131"><a name="appscope"></a>Get and reset app-level credentials</span></span>
<span data-ttu-id="ab690-132">Pour chaque application de Service de l’application, ses informations d’identification au niveau de l’application sont stockées dans hello XML le profil de publication.</span><span class="sxs-lookup"><span data-stu-id="ab690-132">For each app in App Service, its app-level credentials are stored in hello XML publish profile.</span></span>

<span data-ttu-id="ab690-133">informations d’identification de tooget hello au niveau de l’application :</span><span class="sxs-lookup"><span data-stu-id="ab690-133">tooget hello app-level credentials:</span></span>

1. <span data-ttu-id="ab690-134">Bonjour [portail Azure](https://portal.azure.com), cliquez sur le Service d’applications >  **&lt;any_app >** > **vue d’ensemble**.</span><span class="sxs-lookup"><span data-stu-id="ab690-134">In hello [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="ab690-135">Cliquez sur **...Plus** > **Obtenir le profil de publication**. Le téléchargement du fichier .PublishSettings démarre.</span><span class="sxs-lookup"><span data-stu-id="ab690-135">Click **...More** > **Get publish profile**, and download starts for a .PublishSettings file.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_get.png)

3. <span data-ttu-id="ab690-136">Ouvrez hello. Paramètres de publication de fichiers et recherche hello `<publishProfile>` balise avec l’attribut de hello `publishMethod="FTP"`.</span><span class="sxs-lookup"><span data-stu-id="ab690-136">Open hello .PublishSettings file and find hello `<publishProfile>` tag with hello attribute `publishMethod="FTP"`.</span></span> <span data-ttu-id="ab690-137">Obtenez ensuite ses attributs `userName` et `password`.</span><span class="sxs-lookup"><span data-stu-id="ab690-137">Then, get its `userName` and `password` attributes.</span></span>
<span data-ttu-id="ab690-138">Il s’agit des informations d’identification de niveau de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ab690-138">These are hello app-level credentials.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_editor.png)

    <span data-ttu-id="ab690-139">Informations d’identification d’utilisateur au niveau de toohello similaire, nom d’utilisateur du déploiement hello FTP est format hello `<app_name>\<username>`, et le nom d’utilisateur du déploiement hello Git est simplement `<username>` sans hello précédent `<app_name>\`.</span><span class="sxs-lookup"><span data-stu-id="ab690-139">Similar toohello user-level credentials, hello FTP deployment username is in hello format of `<app_name>\<username>`, and hello Git deployment username is just `<username>` without hello preceding `<app_name>\`.</span></span>

<span data-ttu-id="ab690-140">informations d’identification de tooreset hello au niveau de l’application :</span><span class="sxs-lookup"><span data-stu-id="ab690-140">tooreset hello app-level credentials:</span></span>

1. <span data-ttu-id="ab690-141">Bonjour [portail Azure](https://portal.azure.com), cliquez sur le Service d’applications >  **&lt;any_app >** > **vue d’ensemble**.</span><span class="sxs-lookup"><span data-stu-id="ab690-141">In hello [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="ab690-142">Cliquez sur **...Plus** > **Réinitialiser le profil de publication**.</span><span class="sxs-lookup"><span data-stu-id="ab690-142">Click **...More** > **Reset publish profile**.</span></span> <span data-ttu-id="ab690-143">Cliquez sur **Oui** tooconfirm hello réinitialiser.</span><span class="sxs-lookup"><span data-stu-id="ab690-143">Click **Yes** tooconfirm hello reset.</span></span>

    <span data-ttu-id="ab690-144">l’action reset Hello invalide les précédemment téléchargés. Fichiers de paramètres de publication.</span><span class="sxs-lookup"><span data-stu-id="ab690-144">hello reset action invalidates any previously-downloaded .PublishSettings files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab690-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ab690-145">Next steps</span></span>

<span data-ttu-id="ab690-146">Découvrez comment toouse ces informations d’identification toodeploy votre application à partir de [Git local](app-service-deploy-local-git.md) ou à l’aide de [FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="ab690-146">Find out how toouse these credentials toodeploy your app from [local Git](app-service-deploy-local-git.md) or using [FTP/S](app-service-deploy-ftp.md).</span></span>
