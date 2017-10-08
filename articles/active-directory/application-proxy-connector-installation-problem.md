---
title: "l’installation d’aaaProblem hello Agent connecteur Proxy d’Application | Documents Microsoft"
description: "Comment tootroubleshoot les problèmes qui vous pouvez face lors de l’installation hello Agent connecteur Proxy d’Application"
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
ms.openlocfilehash: 07ac366a429083af0c9b87aa9df9cf3876132b90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="problem-installing-hello-application-proxy-agent-connector"></a><span data-ttu-id="199f2-103">Problème d’installation hello Agent connecteur Proxy d’Application</span><span class="sxs-lookup"><span data-stu-id="199f2-103">Problem installing hello Application Proxy Agent Connector</span></span>

<span data-ttu-id="199f2-104">Microsoft AAD Application Proxy Connector est un composant de domaine interne qui utilise la connectivité de connexions sortantes tooestablish hello du domaine interne de hello cloud point de terminaison disponible toohello.</span><span class="sxs-lookup"><span data-stu-id="199f2-104">Microsoft AAD Application Proxy Connector is an internal domain component that uses outbound connections tooestablish hello connectivity from hello cloud available endpoint toohello internal domain.</span></span>

## <a name="general-problem-areas-with-connector-installation"></a><span data-ttu-id="199f2-105">Problèmes généraux avec l’installation du connecteur</span><span class="sxs-lookup"><span data-stu-id="199f2-105">General Problem Areas with Connector installation</span></span>

<span data-ttu-id="199f2-106">En cas d’échec de l’installation de hello d’un connecteur, cause première hello fait généralement partie de hello suivant de zones :</span><span class="sxs-lookup"><span data-stu-id="199f2-106">When hello installation of a connector fails, hello root cause is usually one of hello following areas:</span></span>

1.  <span data-ttu-id="199f2-107">**Connectivité** – toocomplete une installation réussie, hello tooregister de besoins nouveau connecteur et établir les propriétés d’approbation futures.</span><span class="sxs-lookup"><span data-stu-id="199f2-107">**Connectivity** – toocomplete a successful installation, hello new connector needs tooregister and establish future trust properties.</span></span> <span data-ttu-id="199f2-108">Pour cela, en vous connectant toohello service de cloud de Proxy d’Application AAD.</span><span class="sxs-lookup"><span data-stu-id="199f2-108">This is done by connecting toohello AAD Application Proxy cloud service.</span></span>

2.  <span data-ttu-id="199f2-109">**Établissement d’approbation** – nouveau connecteur de hello crée un certificat auto-signé et inscrit toohello cloud service.</span><span class="sxs-lookup"><span data-stu-id="199f2-109">**Trust Establishment** – hello new connector creates a self-signed cert and registers toohello cloud service.</span></span>

3.  <span data-ttu-id="199f2-110">**L’authentification de l’administration de hello** – pendant l’installation, utilisateur de hello doit fournir des informations d’identification administrateur installation du connecteur toocomplete hello.</span><span class="sxs-lookup"><span data-stu-id="199f2-110">**Authentication of hello admin** – during installation, hello user must provide admin credentials toocomplete hello Connector installation.</span></span>

## <a name="verify-connectivity-toohello-cloud-application-proxy-service-and-microsoft-login-page"></a><span data-ttu-id="199f2-111">Vérifiez que le service de Proxy d’Application Cloud toohello de connectivité et de la page de Microsoft Login</span><span class="sxs-lookup"><span data-stu-id="199f2-111">Verify connectivity toohello Cloud Application Proxy service and Microsoft Login page</span></span>

<span data-ttu-id="199f2-112">**Objectif :** Vérifiez que l’ordinateur connecteur hello peut se connecter de point de terminaison toohello AAD Application Proxy d’inscription ainsi que la page de connexion de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="199f2-112">**Objective:** Verify that hello connector machine can connect toohello AAD Application Proxy registration endpoint as well as Microsoft login page.</span></span>

1.  <span data-ttu-id="199f2-113">Ouvrir un toohello de navigateur et allez suivant la page web : <https://aadap-portcheck.connectorporttest.msappproxy.net> et vérifiez que tooCentral de connectivité hello des États-Unis et l’utilisation de centres de données est des États-Unis avec les ports 9090 et 9091.</span><span class="sxs-lookup"><span data-stu-id="199f2-113">Open a browser and go toohello following web page: <https://aadap-portcheck.connectorporttest.msappproxy.net> , and verify that hello connectivity tooCentral US and East US datacenters with ports 9090 and 9091 is working.</span></span>

2.  <span data-ttu-id="199f2-114">Si un de ces ports ne réussit pas (ne dispose pas une coche verte), vérifiez que hello pare-feu ou proxy du serveur principal a \*. msappproxy.net avec ports 9090 et 9091 définies correctement.</span><span class="sxs-lookup"><span data-stu-id="199f2-114">If any of those ports is not successful (doesn’t have a green checkmark), verify that hello Firewall or backend proxy has \*.msappproxy.net with ports 9090 and 9091 defined correctly.</span></span>

3.  <span data-ttu-id="199f2-115">Ouvrez un navigateur (onglet séparé) et accédez toohello suivant la page web : <https://login.microsoftonline.com>, assurez-vous que vous pouvez vous connecter toothat page.</span><span class="sxs-lookup"><span data-stu-id="199f2-115">Open a browser (separate tab) and go toohello following web page: <https://login.microsoftonline.com>, make sure that you can login toothat page.</span></span>

## <a name="verify-machine-and-backend-components-support-for-application-proxy-trust-cert"></a><span data-ttu-id="199f2-116">Vérification de la prise en charge du certificat de confiance du proxy d’application par la machine et les composants principaux</span><span class="sxs-lookup"><span data-stu-id="199f2-116">Verify Machine and backend components support for Application Proxy trust cert</span></span>

<span data-ttu-id="199f2-117">**Objectif :** Vérifiez qu’ordinateur de connecteur hello, de pare-feu et de proxy de serveur principal peuvent prendre en charge de certificat hello créé par le connecteur hello pour approbation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="199f2-117">**Objective:** Verify that hello connector machine, backend proxy and firewall can support hello certificate created by hello connector for future trust.</span></span>

>[!NOTE]
><span data-ttu-id="199f2-118">connecteur de Hello tente toocreate un certificat SHA512 est pris en charge par TLS 1.2.</span><span class="sxs-lookup"><span data-stu-id="199f2-118">hello connector tries toocreate a SHA512 cert that is supported by TLS1.2.</span></span> <span data-ttu-id="199f2-119">Si l’ordinateur de hello ou de proxy et de pare-feu de serveur principal hello ne prend pas en charge TLS 1.2, hello installation d’échouer.</span><span class="sxs-lookup"><span data-stu-id="199f2-119">If hello machine or hello backend firewall and proxy does not support TLS1.2, hello installation fail.</span></span>
>
>

<span data-ttu-id="199f2-120">**problème de hello tooresolve :**</span><span class="sxs-lookup"><span data-stu-id="199f2-120">**tooresolve hello issue:**</span></span>

1.  <span data-ttu-id="199f2-121">Vérifiez l’ordinateur de hello prend en charge TLS 1.2 – les versions de toutes les fenêtres après 2012 R2 doivent prendre en charge TLS 1.2.</span><span class="sxs-lookup"><span data-stu-id="199f2-121">Verify hello machine supports TLS1.2 – All Windows versions after 2012 R2 should support TLS 1.2.</span></span> <span data-ttu-id="199f2-122">Si votre ordinateur de connecteur à partir d’une version de 2012 R2 ou les avant, assurez-vous que hello Kbits/s suivants sont installés sur l’ordinateur de hello : <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2></span><span class="sxs-lookup"><span data-stu-id="199f2-122">If your connector machine is from a version of 2012 R2 or prior, make sure that hello following KBs are installed on hello machine: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2></span></span>

2.  <span data-ttu-id="199f2-123">Contactez votre administrateur réseau et demander tooverify que hello principal proxy et pare-feu ne bloquent pas SHA512 pour le trafic sortant.</span><span class="sxs-lookup"><span data-stu-id="199f2-123">Contact your network admin and ask tooverify that hello backend proxy and firewall do not block SHA512 for outgoing traffic.</span></span>

## <a name="verify-admin-is-used-tooinstall-hello-connector"></a><span data-ttu-id="199f2-124">Vérifiez qu’admin est utilisé tooinstall hello connecteur</span><span class="sxs-lookup"><span data-stu-id="199f2-124">Verify admin is used tooinstall hello connector</span></span>

<span data-ttu-id="199f2-125">**Objectif :** Vérifiez que cet utilisateur hello qui tente de connecteur de hello tooinstall est un administrateur disposant des informations d’identification correctes.</span><span class="sxs-lookup"><span data-stu-id="199f2-125">**Objective:** Verify that hello user who tries tooinstall hello connector is an administrator with correct credentials.</span></span> <span data-ttu-id="199f2-126">Actuellement, les utilisateurs hello doivent être un administrateur global pour hello installation toosucceed.</span><span class="sxs-lookup"><span data-stu-id="199f2-126">Currently, hello user must be a global administrator for hello installation toosucceed.</span></span>

<span data-ttu-id="199f2-127">**informations d’identification de tooverify hello sont correctes :**</span><span class="sxs-lookup"><span data-stu-id="199f2-127">**tooverify hello credentials are correct:**</span></span>

<span data-ttu-id="199f2-128">Vous connecter trop<https://login.microsoftonline.com> et utilisation hello les mêmes informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="199f2-128">Connect too<https://login.microsoftonline.com> and use hello same credentials.</span></span> <span data-ttu-id="199f2-129">Vérifiez que hello connexion est établie.</span><span class="sxs-lookup"><span data-stu-id="199f2-129">Make sure hello login is successful.</span></span> <span data-ttu-id="199f2-130">Vous pouvez vérifier le rôle d’utilisateur hello en accédant trop**Azure Active Directory**  - &gt; **utilisateurs et groupes**  - &gt; **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="199f2-130">You can check hello user role by going too**Azure Active Directory** -&gt; **Users and Groups** -&gt; **All Users**.</span></span> 

<span data-ttu-id="199f2-131">Sélectionnez votre compte d’utilisateur, puis « rôle active » dans le menu résultant de hello.</span><span class="sxs-lookup"><span data-stu-id="199f2-131">Select your user account, then “Directory Role” in hello resulting menu.</span></span> <span data-ttu-id="199f2-132">Vérifiez que ce rôle sélectionné hello est « Administrateur général ».</span><span class="sxs-lookup"><span data-stu-id="199f2-132">Verify that hello selected role is “Global administrator”.</span></span> <span data-ttu-id="199f2-133">Si vous êtes tooaccess impossible des hello pages le long de ces étapes, vous n’êtes pas un administrateur global.</span><span class="sxs-lookup"><span data-stu-id="199f2-133">If you are unable tooaccess any of hello pages along these steps, you are not a global administrator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="199f2-134">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="199f2-134">Next steps</span></span>
[<span data-ttu-id="199f2-135">Présentation des connecteurs de proxy d’application Azure AD</span><span class="sxs-lookup"><span data-stu-id="199f2-135">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
