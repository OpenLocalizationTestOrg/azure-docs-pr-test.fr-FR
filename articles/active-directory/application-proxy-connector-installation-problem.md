---
title: "Problèmes lors de l’installation du connecteur d’agent de proxy d’application | Microsoft Docs"
description: "Comment résoudre les problèmes que vous pouvez rencontrer lors de l’installation du connecteur d’agent de proxy d’application"
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
ms.openlocfilehash: 91b3f6f3c8339647f568a509e9efd8e1fffb13dd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="problem-installing-the-application-proxy-agent-connector"></a><span data-ttu-id="5960b-103">Problèmes lors de l’installation du connecteur d’agent de proxy d’application</span><span class="sxs-lookup"><span data-stu-id="5960b-103">Problem installing the Application Proxy Agent Connector</span></span>

<span data-ttu-id="5960b-104">Le connecteur de proxy d’application Microsoft AAD est un composant de domaine interne qui utilise des connexions sortantes pour établir la connectivité à partir du point de terminaison disponible dans le cloud vers le domaine interne.</span><span class="sxs-lookup"><span data-stu-id="5960b-104">Microsoft AAD Application Proxy Connector is an internal domain component that uses outbound connections to establish the connectivity from the cloud available endpoint to the internal domain.</span></span>

## <a name="general-problem-areas-with-connector-installation"></a><span data-ttu-id="5960b-105">Problèmes généraux avec l’installation du connecteur</span><span class="sxs-lookup"><span data-stu-id="5960b-105">General Problem Areas with Connector installation</span></span>

<span data-ttu-id="5960b-106">En cas d’échec de l’installation d’un connecteur, la cause est généralement liée à l’un des aspects suivants :</span><span class="sxs-lookup"><span data-stu-id="5960b-106">When the installation of a connector fails, the root cause is usually one of the following areas:</span></span>

1.  <span data-ttu-id="5960b-107">**Connectivité** : pour une installation réussie, le nouveau connecteur doit s’inscrire et établir les propriétés d’approbation ultérieures.</span><span class="sxs-lookup"><span data-stu-id="5960b-107">**Connectivity** – to complete a successful installation, the new connector needs to register and establish future trust properties.</span></span> <span data-ttu-id="5960b-108">Pour cela, connectez-vous au service cloud du proxy d’application AAD.</span><span class="sxs-lookup"><span data-stu-id="5960b-108">This is done by connecting to the AAD Application Proxy cloud service.</span></span>

2.  <span data-ttu-id="5960b-109">**Établissement de l’approbation** : le nouveau connecteur crée un certificat auto-signé et s’inscrit auprès du service cloud.</span><span class="sxs-lookup"><span data-stu-id="5960b-109">**Trust Establishment** – the new connector creates a self-signed cert and registers to the cloud service.</span></span>

3.  <span data-ttu-id="5960b-110">**Authentification de l’administrateur** : pendant l’installation, l’utilisateur doit fournir des informations d’identification d’administrateur pour terminer l’installation du connecteur.</span><span class="sxs-lookup"><span data-stu-id="5960b-110">**Authentication of the admin** – during installation, the user must provide admin credentials to complete the Connector installation.</span></span>

## <a name="verify-connectivity-to-the-cloud-application-proxy-service-and-microsoft-login-page"></a><span data-ttu-id="5960b-111">Vérification de la connectivité vers le service de proxy d’application cloud et la page de connexion Microsoft</span><span class="sxs-lookup"><span data-stu-id="5960b-111">Verify connectivity to the Cloud Application Proxy service and Microsoft Login page</span></span>

<span data-ttu-id="5960b-112">**Objectif :** vérifier que l’ordinateur connecteur peut se connecter au point de terminaison d’inscription du proxy d’application AAD ainsi qu’à la page de connexion Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5960b-112">**Objective:** Verify that the connector machine can connect to the AAD Application Proxy registration endpoint as well as Microsoft login page.</span></span>

1.  <span data-ttu-id="5960b-113">Ouvrez un navigateur et accédez à la page web suivante : <https://aadap-portcheck.connectorporttest.msappproxy.net>. Vérifiez que la connectivité vers les centres de données des États-Unis du Centre et des États-Unis de l’Est avec les ports 9090 et 9091 fonctionne.</span><span class="sxs-lookup"><span data-stu-id="5960b-113">Open a browser and go to the following web page: <https://aadap-portcheck.connectorporttest.msappproxy.net> , and verify that the connectivity to Central US and East US datacenters with ports 9090 and 9091 is working.</span></span>

2.  <span data-ttu-id="5960b-114">En cas d’échec de l’un de ces ports (absence de coche verte), vérifiez que \*.msappproxy.net est correctement défini sur le proxy principal ou le pare-feu avec les ports 9090 et 9091.</span><span class="sxs-lookup"><span data-stu-id="5960b-114">If any of those ports is not successful (doesn’t have a green checkmark), verify that the Firewall or backend proxy has \*.msappproxy.net with ports 9090 and 9091 defined correctly.</span></span>

3.  <span data-ttu-id="5960b-115">Ouvrez un navigateur (onglet distinct) et accédez à la page web suivante : <https://login.microsoftonline.com>. Assurez-vous que vous pouvez vous connecter à cette page.</span><span class="sxs-lookup"><span data-stu-id="5960b-115">Open a browser (separate tab) and go to the following web page: <https://login.microsoftonline.com>, make sure that you can login to that page.</span></span>

## <a name="verify-machine-and-backend-components-support-for-application-proxy-trust-cert"></a><span data-ttu-id="5960b-116">Vérification de la prise en charge du certificat de confiance du proxy d’application par la machine et les composants principaux</span><span class="sxs-lookup"><span data-stu-id="5960b-116">Verify Machine and backend components support for Application Proxy trust cert</span></span>

<span data-ttu-id="5960b-117">**Objectif :** vérifier que l’ordinateur connecteur, le pare-feu et le proxy principal peuvent prendre en charge le certificat créé par le connecteur en vue d’une approbation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="5960b-117">**Objective:** Verify that the connector machine, backend proxy and firewall can support the certificate created by the connector for future trust.</span></span>

>[!NOTE]
><span data-ttu-id="5960b-118">Le connecteur tente de créer un certificat SHA512 pris en charge par TLS1.2.</span><span class="sxs-lookup"><span data-stu-id="5960b-118">The connector tries to create a SHA512 cert that is supported by TLS1.2.</span></span> <span data-ttu-id="5960b-119">Si l’ordinateur ou le pare-feu principal et le proxy ne prennent pas en charge TLS1.2, l’installation échoue.</span><span class="sxs-lookup"><span data-stu-id="5960b-119">If the machine or the backend firewall and proxy does not support TLS1.2, the installation fail.</span></span>
>
>

<span data-ttu-id="5960b-120">**Résolution du problème :**</span><span class="sxs-lookup"><span data-stu-id="5960b-120">**To resolve the issue:**</span></span>

1.  <span data-ttu-id="5960b-121">Vérifiez que l’ordinateur prend en charge TLS1.2 (toutes les versions de Windows supérieures à 2012 R2 doivent prendre en charge TLS 1.2).</span><span class="sxs-lookup"><span data-stu-id="5960b-121">Verify the machine supports TLS1.2 – All Windows versions after 2012 R2 should support TLS 1.2.</span></span> <span data-ttu-id="5960b-122">Si votre ordinateur connecteur dispose de la version 2012 R2 ou d’une version inférieure, assurez-vous que les bases de connaissances suivantes sont installées sur l’ordinateur : <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2></span><span class="sxs-lookup"><span data-stu-id="5960b-122">If your connector machine is from a version of 2012 R2 or prior, make sure that the following KBs are installed on the machine: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2></span></span>

2.  <span data-ttu-id="5960b-123">Contactez votre administrateur réseau et demandez-lui de vérifier que le proxy principal et le pare-feu ne bloquent par SHA512 pour le trafic sortant.</span><span class="sxs-lookup"><span data-stu-id="5960b-123">Contact your network admin and ask to verify that the backend proxy and firewall do not block SHA512 for outgoing traffic.</span></span>

## <a name="verify-admin-is-used-to-install-the-connector"></a><span data-ttu-id="5960b-124">Vérification de l’utilisation d’une connexion administrateur pour l’installation du connecteur</span><span class="sxs-lookup"><span data-stu-id="5960b-124">Verify admin is used to install the connector</span></span>

<span data-ttu-id="5960b-125">**Objectif :** vérifier que l’utilisateur qui tente d’installer le connecteur est un administrateur disposant des informations d’identification correctes.</span><span class="sxs-lookup"><span data-stu-id="5960b-125">**Objective:** Verify that the user who tries to install the connector is an administrator with correct credentials.</span></span> <span data-ttu-id="5960b-126">Actuellement, l’installation requiert que l’utilisateur soit un administrateur général.</span><span class="sxs-lookup"><span data-stu-id="5960b-126">Currently, the user must be a global administrator for the installation to succeed.</span></span>

<span data-ttu-id="5960b-127">**Pour vérifier que les informations d’identification sont correctes :**</span><span class="sxs-lookup"><span data-stu-id="5960b-127">**To verify the credentials are correct:**</span></span>

<span data-ttu-id="5960b-128">Connectez-vous à <https://login.microsoftonline.com> et utilisez les mêmes informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="5960b-128">Connect to <https://login.microsoftonline.com> and use the same credentials.</span></span> <span data-ttu-id="5960b-129">Vérifiez que la connexion a réussi.</span><span class="sxs-lookup"><span data-stu-id="5960b-129">Make sure the login is successful.</span></span> <span data-ttu-id="5960b-130">Vous pouvez vérifier le rôle utilisateur en sélectionnant **Azure Active Directory** -&gt; **Utilisateurs et groupes** -&gt; **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="5960b-130">You can check the user role by going to **Azure Active Directory** -&gt; **Users and Groups** -&gt; **All Users**.</span></span> 

<span data-ttu-id="5960b-131">Sélectionnez votre compte d’utilisateur, puis sélectionnez « Rôle d’annuaire » dans le menu qui s’affiche.</span><span class="sxs-lookup"><span data-stu-id="5960b-131">Select your user account, then “Directory Role” in the resulting menu.</span></span> <span data-ttu-id="5960b-132">Vérifiez que le rôle sélectionné est « Administrateur général ».</span><span class="sxs-lookup"><span data-stu-id="5960b-132">Verify that the selected role is “Global administrator”.</span></span> <span data-ttu-id="5960b-133">Si vous ne pouvez accéder à aucune des pages de cette procédure, cela signifie que vous n’êtes pas administrateur général.</span><span class="sxs-lookup"><span data-stu-id="5960b-133">If you are unable to access any of the pages along these steps, you are not a global administrator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5960b-134">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5960b-134">Next steps</span></span>
[<span data-ttu-id="5960b-135">Présentation des connecteurs de proxy d’application Azure AD</span><span class="sxs-lookup"><span data-stu-id="5960b-135">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
