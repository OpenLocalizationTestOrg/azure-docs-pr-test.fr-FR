---
title: "Comment configurer une application de proxy d’application pour utiliser PingAccess | Microsoft Docs"
description: "Découvrez comment utiliser PingAccess pour apporter les avantages du proxy d’application aux applications utilisant l’authentification basée sur l’en-tête"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: a9da67373465cebbdbecae5c8fb8bd0a0ee3c171
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-an-application-proxy-application-to-use-pingaccess"></a><span data-ttu-id="52619-103">Comment configurer une application de proxy d’application pour utiliser PingAccess</span><span class="sxs-lookup"><span data-stu-id="52619-103">How to configure an Application Proxy application to use PingAccess</span></span>

<span data-ttu-id="52619-104">Grâce à notre collaboration avec PingAccess, vous pouvez désormais apporter les avantages du proxy d’application aux applications utilisant l’authentification basée sur l’en-tête.</span><span class="sxs-lookup"><span data-stu-id="52619-104">Our collaboration with PingAccess now allows you to extend the benefits of Application Proxy to applications using header-based authentication.</span></span> <span data-ttu-id="52619-105">Si vos applications n’utilisent pas d’en-têtes, vous trouverez des informations sur les alternatives disponibles dans notre [documentation sur l’authentification unique](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd).</span><span class="sxs-lookup"><span data-stu-id="52619-105">If your applications do not use headers, see our [Single Sign-On documentation](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) for details on other options.</span></span>

## <a name="overview-of-steps-and-recommended-documents"></a><span data-ttu-id="52619-106">Vue d’ensemble des étapes et documents recommandés</span><span class="sxs-lookup"><span data-stu-id="52619-106">Overview of steps and recommended documents</span></span>

<span data-ttu-id="52619-107">Vous devez suivre les quatre étapes suivantes pour configurer une application avec PingAccess :</span><span class="sxs-lookup"><span data-stu-id="52619-107">To configure an application with PingAccess, there are four steps:</span></span>

1.  <span data-ttu-id="52619-108">Configurer les connecteurs de proxy d’application</span><span class="sxs-lookup"><span data-stu-id="52619-108">Configure Application Proxy Connectors</span></span>

2.  <span data-ttu-id="52619-109">Créer une application de proxy d’application Azure AD</span><span class="sxs-lookup"><span data-stu-id="52619-109">Create an Azure AD Application Proxy Application</span></span>

3.  <span data-ttu-id="52619-110">Télécharger et configurer PingAccess</span><span class="sxs-lookup"><span data-stu-id="52619-110">Download & Configure PingAccess</span></span>

4.  <span data-ttu-id="52619-111">Configuration les applications dans PingAccess</span><span class="sxs-lookup"><span data-stu-id="52619-111">Configure Applications in PingAccess</span></span>

<span data-ttu-id="52619-112">Pour plus d’informations sur chacune de ces étapes, consultez notre [documentation sur l’authentification unique basée sur les en-têtes](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access).</span><span class="sxs-lookup"><span data-stu-id="52619-112">For details on each of these steps, see our [Single Sign-On with Headers documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access).</span></span>
