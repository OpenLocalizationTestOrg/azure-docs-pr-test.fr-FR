---
title: "aaaAccess applications du Proxy d’application Azure AD dans des équipes | Documents Microsoft"
description: "Utiliser le Proxy d’Application Azure AD tooaccess votre application sur site via Microsoft Teams."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 13c36e43ae6349df09272e308ad4f40451cbbeb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="access-your-on-premises-applications-through-microsoft-teams"></a><span data-ttu-id="73e76-103">Accéder aux applications locales via Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="73e76-103">Access your on-premises applications through Microsoft Teams</span></span>

<span data-ttu-id="73e76-104">Azure Proxy d’Application Active Directory vous donne un seul signe-tooon applications locales où que vous soyez et Teams Microsoft rationalise vos efforts de collaboration en un seul emplacement.</span><span class="sxs-lookup"><span data-stu-id="73e76-104">Azure Active Directory Application Proxy gives you single sign-on tooon-premises applications no matter where you are, and Microsoft Teams streamlines your collaborative efforts in one place.</span></span> <span data-ttu-id="73e76-105">Intégration hello deux ensemble signifie que vos utilisateurs peuvent être productifs avec leurs coéquipiers dans tous les cas.</span><span class="sxs-lookup"><span data-stu-id="73e76-105">Integrating hello two together means that your users can be productive with their teammates in any situation.</span></span> 

<span data-ttu-id="73e76-106">Vos utilisateurs peuvent ajouter des canaux d’équipes cloud applications tootheir [à l’aide des onglets](https://support.office.com/article/Video-Using-Tabs-7350a03e-017a-4a00-a6ae-1c9fe8c497b3?ui=en-US&rs=en-US&ad=US), mais que se passe-t-il si ce site SharePoint ou l’outil de planification elles utilisent toutes est hébergée sur site ?</span><span class="sxs-lookup"><span data-stu-id="73e76-106">Your users can add cloud apps tootheir Teams channels [using tabs](https://support.office.com/article/Video-Using-Tabs-7350a03e-017a-4a00-a6ae-1c9fe8c497b3?ui=en-US&rs=en-US&ad=US), but what happens if that SharePoint site or planning tool they all use is hosted on-premises?</span></span> <span data-ttu-id="73e76-107">Proxy d’application est la solution de hello.</span><span class="sxs-lookup"><span data-stu-id="73e76-107">Application Proxy is hello solution.</span></span> <span data-ttu-id="73e76-108">Ils peuvent ajouter des applications publiées via le Proxy d’Application tootheir à l’aide de canaux hello mêmes URL externes, ils utilisent toujours tooaccess leurs applications à distance.</span><span class="sxs-lookup"><span data-stu-id="73e76-108">They can add apps published through Application Proxy tootheir channels using hello same external URLs they always use tooaccess their apps remotely.</span></span> <span data-ttu-id="73e76-109">Et, étant donné que le Proxy d’Application s’authentifie via Azure Active Directory, hello même seule expérience d’authentification s’effectue.</span><span class="sxs-lookup"><span data-stu-id="73e76-109">And because Application Proxy authenticates through Azure Active Directory, hello same single sign-on experience carries through.</span></span>


## <a name="install-hello-application-proxy-connector-and-publish-your-app"></a><span data-ttu-id="73e76-110">Installer le connecteur de Proxy d’Application hello et publier votre application</span><span class="sxs-lookup"><span data-stu-id="73e76-110">Install hello Application Proxy connector and publish your app</span></span>

<span data-ttu-id="73e76-111">Si vous n’avez pas déjà fait, [configurer le Proxy d’Application pour votre client et installer le connecteur de hello](active-directory-application-proxy-enable.md).</span><span class="sxs-lookup"><span data-stu-id="73e76-111">If you haven't already, [configure Application Proxy for your tenant and install hello connector](active-directory-application-proxy-enable.md).</span></span> <span data-ttu-id="73e76-112">Ensuite, [publiez votre application locale](application-proxy-publish-azure-portal.md) pour l’accès à distance.</span><span class="sxs-lookup"><span data-stu-id="73e76-112">Then, [publish your on-premises application](application-proxy-publish-azure-portal.md) for remote access.</span></span> <span data-ttu-id="73e76-113">Lorsque vous publiez une application hello, notez les URL externe hello, car vos utilisateurs finaux ont besoin de ces informations lorsqu’elles ajoutent hello application tooTeams.</span><span class="sxs-lookup"><span data-stu-id="73e76-113">When you're publishing hello app, make note of hello external URL because your end users need that information when they add hello app tooTeams.</span></span>

<span data-ttu-id="73e76-114">Si vous avez déjà vos aurez publiées mais que vous ne connaissez pas leurs URL externes, recherchez-les dans hello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="73e76-114">If you already have your apps published but don't remember their external URLs, look them up in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="73e76-115">Connectez-vous, puis accédez trop**Azure Active Directory** > **des applications d’entreprise** > **toutes les applications** > sélectionner votre application > **Le proxy d’application**.</span><span class="sxs-lookup"><span data-stu-id="73e76-115">Sign in, then navigate too**Azure Active Directory** > **Enterprise applications** > **All applications** > select your app > **Application proxy**.</span></span>

## <a name="add-your-app-tooteams"></a><span data-ttu-id="73e76-116">Ajouter votre tooTeams d’application</span><span class="sxs-lookup"><span data-stu-id="73e76-116">Add your app tooTeams</span></span>

<span data-ttu-id="73e76-117">Une fois que vous publiez application hello via le Proxy d’Application, informez vos utilisateurs que vous pouvez l’ajouter en tant qu’un onglet directement dans leurs canaux équipes.</span><span class="sxs-lookup"><span data-stu-id="73e76-117">Once you publish hello app through Application Proxy, let your users know that they can add it as a tab directly in their Teams channels.</span></span> <span data-ttu-id="73e76-118">Demandez-leur d’effectuer les trois étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="73e76-118">Have them follow these three steps:</span></span>

1. <span data-ttu-id="73e76-119">Accédez toohello équipes de canal où vous souhaitez tooadd cette application et sélectionnent  **+**  tooadd un onglet.</span><span class="sxs-lookup"><span data-stu-id="73e76-119">Navigate toohello Teams channel where you want tooadd this app and select **+** tooadd a tab.</span></span>

   ![Sélectionner Ajouter un onglet](./media/application-proxy-teams/add-tab.png)

2. <span data-ttu-id="73e76-121">Sélectionnez **site Web** à partir des options de l’onglet hello.</span><span class="sxs-lookup"><span data-stu-id="73e76-121">Select **Website** from hello tab options.</span></span>

   ![Ajouter un site web](./media/application-proxy-teams/website.png)

3. <span data-ttu-id="73e76-123">Donnez un nom à onglet de hello et définir l’URL externe du Proxy d’Application toohello URL hello.</span><span class="sxs-lookup"><span data-stu-id="73e76-123">Give hello tab a name and set hello URL toohello Application Proxy external URL.</span></span> 

   ![Configurer le nom et l’URL de l’onglet](./media/application-proxy-teams/tab-name-url.png)

<span data-ttu-id="73e76-125">Une fois qu’un membre de l’équipe ajoute un onglet de hello, il s’affiche pour tout le monde dans le canal de hello.</span><span class="sxs-lookup"><span data-stu-id="73e76-125">Once one member of a team adds hello tab, it shows up for everyone in hello channel.</span></span> <span data-ttu-id="73e76-126">Tous les utilisateurs qui ont accès toohello application obtiennent l’accès d’authentification unique avec informations d’identification hello qu’ils utilisent pour Teams Microsoft.</span><span class="sxs-lookup"><span data-stu-id="73e76-126">Any users who have access toohello app get single sign-on access with hello credentials they use for Microsoft Teams.</span></span> <span data-ttu-id="73e76-127">Tous les utilisateurs qui n’ont pas accès toohello application onglet hello dans des équipes s’affiche, mais sont bloquées jusqu'à ce que vous leur attribuer des autorisations toohello local application hello Azure version publiée portail de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="73e76-127">Any users who don't have access toohello app will see hello tab in Teams, but are blocked until you give them permissions toohello on-premises app and hello Azure portal published version of hello app.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="73e76-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="73e76-128">Next steps</span></span>

- <span data-ttu-id="73e76-129">Découvrez comment trop[publier des sites SharePoint locaux](application-proxy-enable-remote-access-sharepoint.md) avec le Proxy d’Application.</span><span class="sxs-lookup"><span data-stu-id="73e76-129">Learn how too[publish on-premises SharePoint sites](application-proxy-enable-remote-access-sharepoint.md) with Application Proxy.</span></span>
- <span data-ttu-id="73e76-130">Configurer votre toouse applications [des domaines personnalisés](active-directory-application-proxy-custom-domains.md) pour leur URL externe.</span><span class="sxs-lookup"><span data-stu-id="73e76-130">Configure your apps toouse [custom domains](active-directory-application-proxy-custom-domains.md) for their external URL.</span></span> 
