---
title: "aaaWindows l’authentification et le serveur Azure MFA | Documents Microsoft"
description: "Il s’agit de page d’authentification multifacteur Azure hello qui va vous aider à déployer l’authentification Windows et le serveur Azure multi-Factor Authentication."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 19a4043f-c4ce-43c0-80e7-2548ee92cb74
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/06/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 0fc38fd751966bf883d4eae7c48055988922af80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-authentication-and-azure-multi-factor-authentication-server"></a><span data-ttu-id="2a7e1-103">Authentification Windows et serveur Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="2a7e1-103">Windows Authentication and Azure Multi-Factor Authentication Server</span></span>
<span data-ttu-id="2a7e1-104">Utiliser la section de l’authentification Windows hello de tooenable du serveur Azure multi-Factor Authentication hello et configurer l’authentification Windows pour les applications.</span><span class="sxs-lookup"><span data-stu-id="2a7e1-104">Use hello Windows Authentication section of hello Azure Multi-Factor Authentication Server tooenable and configure Windows authentication for applications.</span></span> <span data-ttu-id="2a7e1-105">Avant de configurer l’authentification Windows, gardez hello suivant liste à l’esprit :</span><span class="sxs-lookup"><span data-stu-id="2a7e1-105">Before you set up Windows Authentication, keep hello following list in mind:</span></span>

* <span data-ttu-id="2a7e1-106">Après l’installation, redémarrez hello Azure multi-Factor Authentication pour effet de tootake Services Terminal Server.</span><span class="sxs-lookup"><span data-stu-id="2a7e1-106">After setup, reboot hello Azure Multi-Factor Authentication for Terminal Services tootake effect.</span></span>
* <span data-ttu-id="2a7e1-107">Si « Correspondance d’utilisateur nécessitent Azure multi-Factor Authentication » est activée et que vous n’êtes pas dans la liste des utilisateurs hello, vous ne serez pas en mesure de toolog dans une machine de hello après le redémarrage.</span><span class="sxs-lookup"><span data-stu-id="2a7e1-107">If ‘Require Azure Multi-Factor Authentication user match’ is checked and you are not in hello user list, you will not be able toolog into hello machine after reboot.</span></span>
* <span data-ttu-id="2a7e1-108">Adresses IP approuvées que sont dépend de si application hello fournir hello IP du client avec l’authentification de hello.</span><span class="sxs-lookup"><span data-stu-id="2a7e1-108">Trusted IPs is dependent on whether hello application can provide hello client IP with hello authentication.</span></span> <span data-ttu-id="2a7e1-109">Actuellement, seul Terminal Services est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="2a7e1-109">Currently only Terminal Services is supported.</span></span>  

> [!NOTE]
> <span data-ttu-id="2a7e1-110">Cette fonctionnalité n’est pas pris en charge toosecure Terminal Server sur Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="2a7e1-110">This feature is not supported toosecure Terminal Services on Windows Server 2012 R2.</span></span>

## <a name="toosecure-an-application-with-windows-authentication-use-hello-following-procedure"></a><span data-ttu-id="2a7e1-111">toosecure une application avec l’authentification Windows, hello utilisation suivant la procédure.</span><span class="sxs-lookup"><span data-stu-id="2a7e1-111">toosecure an application with Windows Authentication, use hello following procedure.</span></span>
1. <span data-ttu-id="2a7e1-112">Bonjour serveur Azure multi-Factor Authentication, cliquez sur icône de l’authentification Windows hello.</span><span class="sxs-lookup"><span data-stu-id="2a7e1-112">In hello Azure Multi-Factor Authentication Server click hello Windows Authentication icon.</span></span>
   <span data-ttu-id="2a7e1-113">![Authentification Windows](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)</span><span class="sxs-lookup"><span data-stu-id="2a7e1-113">![Windows Authentication](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)</span></span>
2. <span data-ttu-id="2a7e1-114">Vérifiez hello **activer l’authentification Windows** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="2a7e1-114">Check hello **Enable Windows Authentication** checkbox.</span></span> <span data-ttu-id="2a7e1-115">Par défaut, cette case est désactivée.</span><span class="sxs-lookup"><span data-stu-id="2a7e1-115">By default, this box is unchecked.</span></span>
3. <span data-ttu-id="2a7e1-116">onglet Applications de Hello permet hello administrateur tooconfigure une ou plusieurs applications pour l’authentification Windows.</span><span class="sxs-lookup"><span data-stu-id="2a7e1-116">hello Applications tab allows hello administrator tooconfigure one or more applications for Windows Authentication.</span></span>
4. <span data-ttu-id="2a7e1-117">Sélectionnez un serveur ou une application – permet de spécifier si le serveur ou l’application hello est activée.</span><span class="sxs-lookup"><span data-stu-id="2a7e1-117">Select a server or application – specify whether hello server/application is enabled.</span></span> <span data-ttu-id="2a7e1-118">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="2a7e1-118">Click **OK**.</span></span>
5. <span data-ttu-id="2a7e1-119">Cliquez sur **Ajouter…**.</span><span class="sxs-lookup"><span data-stu-id="2a7e1-119">Click **Add…**</span></span>
6. <span data-ttu-id="2a7e1-120">onglet adresses IP approuvées de Hello vous permet de tooskip Azure multi-Factor Authentication pour les sessions Windows provenant d’adresses IP spécifique.</span><span class="sxs-lookup"><span data-stu-id="2a7e1-120">hello Trusted IPs tab allows you tooskip Azure Multi-Factor Authentication for Windows sessions originating from specific IPs.</span></span> <span data-ttu-id="2a7e1-121">Par exemple, si les employés utilisent l’application hello hello bureau et à domicile, vous pouvez décider de que vous ne souhaitez pas leur téléphone sonne pour Azure multi-Factor Authentication au bureau de hello.</span><span class="sxs-lookup"><span data-stu-id="2a7e1-121">For example, if employees use hello application from hello office and from home, you may decide you don't want their phones ringing for Azure Multi-Factor Authentication while at hello office.</span></span> <span data-ttu-id="2a7e1-122">Pour ce faire, vous spécifiez hello office sous-réseau en tant qu’adresse IP approuvée.</span><span class="sxs-lookup"><span data-stu-id="2a7e1-122">For this, you would specify hello office subnet as Trusted IPs entry.</span></span>
7. <span data-ttu-id="2a7e1-123">Cliquez sur **Ajouter…**.</span><span class="sxs-lookup"><span data-stu-id="2a7e1-123">Click **Add…**</span></span>
8. <span data-ttu-id="2a7e1-124">Sélectionnez **adresse IP unique** si vous souhaitez que tooskip une adresse IP unique.</span><span class="sxs-lookup"><span data-stu-id="2a7e1-124">Select **Single IP** if you would like tooskip a single IP address.</span></span>
9. <span data-ttu-id="2a7e1-125">Sélectionnez **plage d’adresses IP** si vous souhaitez que tooskip une plage entière d’IP.</span><span class="sxs-lookup"><span data-stu-id="2a7e1-125">Select **IP Range** if you would like tooskip an entire IP range.</span></span> <span data-ttu-id="2a7e1-126">Exemple 10.63.193.1-10.63.193.100.</span><span class="sxs-lookup"><span data-stu-id="2a7e1-126">Example 10.63.193.1-10.63.193.100.</span></span>
10. <span data-ttu-id="2a7e1-127">Sélectionnez **sous-réseau** si vous souhaitez que toospecify une plage d’adresses IP à l’aide de la notation de sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="2a7e1-127">Select **Subnet** if you would like toospecify a range of IPs using subnet notation.</span></span> <span data-ttu-id="2a7e1-128">Entrez l’adresse IP de début du sous-réseau hello et choisissez hello un masque de réseau approprié à partir de la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="2a7e1-128">Enter hello subnet's starting IP and pick hello appropriate netmask from hello drop-down list.</span></span>
11. <span data-ttu-id="2a7e1-129">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="2a7e1-129">Click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a7e1-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2a7e1-130">Next steps</span></span>

- [<span data-ttu-id="2a7e1-131">Configurer des appareils VPN tiers pour Azure MFA Server</span><span class="sxs-lookup"><span data-stu-id="2a7e1-131">Configure third-party VPN appliances for Azure MFA Server</span></span>](multi-factor-authentication-advanced-vpn-configurations.md)

- [<span data-ttu-id="2a7e1-132">Améliorer votre infrastructure d’authentification existante avec hello extension du serveur NPS pour Azure MFA</span><span class="sxs-lookup"><span data-stu-id="2a7e1-132">Augment your existing authentication infrastructure with hello NPS extension for Azure MFA</span></span>](multi-factor-authentication-nps-extension.md)
