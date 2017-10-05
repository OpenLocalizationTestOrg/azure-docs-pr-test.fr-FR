---
title: "Configurer le protocole LDAPS (LDAP sécurisé) dans les services de domaine Azure AD | Microsoft Docs"
description: "Configurer le protocole LDAPS (LDAP sécurisé) pour un domaine géré par les services de domaine Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: 93afa49166c5b31d23237c308b9d34f6d6f3507d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="789e6-103">Configurer le protocole LDAPS (LDAP sécurisé) pour un domaine managé Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="789e6-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="789e6-104">Cet article explique comment activer le protocole LDAPS pour votre domaine géré par les services de domaine Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="789e6-104">This article shows how you can enable Secure Lightweight Directory Access Protocol (LDAPS) for your Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="789e6-105">Le protocole LDAP sécurisé est également appelé « protocole LDAP sur SSL (Secure Sockets Layer) / TLS (Transport Layer Security) ».</span><span class="sxs-lookup"><span data-stu-id="789e6-105">Secure LDAP is also known as 'Lightweight Directory Access Protocol (LDAP) over Secure Sockets Layer (SSL) / Transport Layer Security (TLS)'.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="789e6-106">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="789e6-106">Before you begin</span></span>
<span data-ttu-id="789e6-107">Pour exécuter les tâches indiquées dans cet article, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="789e6-107">To perform the tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="789e6-108">Un **abonnement Azure**valide.</span><span class="sxs-lookup"><span data-stu-id="789e6-108">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="789e6-109">Un **répertoire Azure AD** , synchronisé avec un répertoire local ou un répertoire cloud uniquement.</span><span class="sxs-lookup"><span data-stu-id="789e6-109">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="789e6-110">**services de domaine Azure AD** , qui doivent être activés pour le répertoire Azure AD.</span><span class="sxs-lookup"><span data-stu-id="789e6-110">**Azure AD Domain Services** must be enabled for the Azure AD directory.</span></span> <span data-ttu-id="789e6-111">Si ce n’est déjà fait, suivez l’ensemble des tâches décrites dans le [Guide de mise en route](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="789e6-111">If you haven't done so, follow all the tasks outlined in the [Getting Started guide](active-directory-ds-getting-started.md).</span></span>
4. <span data-ttu-id="789e6-112">Un **certificat à utiliser pour activer le protocole LDAP sécurisé**.</span><span class="sxs-lookup"><span data-stu-id="789e6-112">A **certificate to be used to enable secure LDAP**.</span></span>

   * <span data-ttu-id="789e6-113">**Recommandé** - Procurez-vous un certificat auprès de votre autorité de certification publique de confiance.</span><span class="sxs-lookup"><span data-stu-id="789e6-113">**Recommended** - Obtain a certificate from a trusted public certification authority.</span></span> <span data-ttu-id="789e6-114">Cette option de configuration est plus sûre.</span><span class="sxs-lookup"><span data-stu-id="789e6-114">This configuration option is more secure.</span></span>
   * <span data-ttu-id="789e6-115">Le cas échéant, vous pouvez également [créer un certificat auto-signé](#task-1---obtain-a-certificate-for-secure-ldap) comme indiqué plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="789e6-115">Alternately, you may also choose to [create a self-signed certificate](#task-1---obtain-a-certificate-for-secure-ldap) as shown later in this article.</span></span>

<br>

### <a name="requirements-for-the-secure-ldap-certificate"></a><span data-ttu-id="789e6-116">Configuration requise pour le certificat LDAP sécurisé</span><span class="sxs-lookup"><span data-stu-id="789e6-116">Requirements for the secure LDAP certificate</span></span>
<span data-ttu-id="789e6-117">Obtenez un certificat valide, en suivant les instructions ci-dessous, avant d’activer le protocole LDAP sécurisé.</span><span class="sxs-lookup"><span data-stu-id="789e6-117">Acquire a valid certificate per the following guidelines, before you enable secure LDAP.</span></span> <span data-ttu-id="789e6-118">Toute tentative d’activation du protocole LDAP sécurisé pour votre domaine géré avec un certificat non valide ou incorrect se soldera par un échec.</span><span class="sxs-lookup"><span data-stu-id="789e6-118">You encounter failures if you try to enable secure LDAP for your managed domain with an invalid/incorrect certificate.</span></span>

1. <span data-ttu-id="789e6-119">**Émetteur approuvé** : le certificat doit être émis par une autorité approuvée par les ordinateurs qui se connectent au domaine managé à l’aide du protocole LDAP sécurisé.</span><span class="sxs-lookup"><span data-stu-id="789e6-119">**Trusted issuer** - The certificate must be issued by an authority trusted by computers connecting to the managed domain using secure LDAP.</span></span> <span data-ttu-id="789e6-120">Cette autorité peut être une autorité de certification approuvée par ces ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="789e6-120">This authority may be a public certification authority trusted by these computers.</span></span>
2. <span data-ttu-id="789e6-121">**Durée de vie** : le certificat doit être valide pour les 3 à 6 mois à venir.</span><span class="sxs-lookup"><span data-stu-id="789e6-121">**Lifetime** - The certificate must be valid for at least the next 3-6 months.</span></span> <span data-ttu-id="789e6-122">L’accès du protocole LDAP sécurisé à votre domaine géré est interrompu lorsque le certificat expire.</span><span class="sxs-lookup"><span data-stu-id="789e6-122">Secure LDAP access to your managed domain is disrupted when the certificate expires.</span></span>
3. <span data-ttu-id="789e6-123">**Nom du sujet** : le nom du sujet du certificat doit correspondre à un caractère générique pour votre domaine géré.</span><span class="sxs-lookup"><span data-stu-id="789e6-123">**Subject name** - The subject name on the certificate must be a wildcard for your managed domain.</span></span> <span data-ttu-id="789e6-124">Par exemple, si le nom du domaine est « contoso100.com », le nom d’objet du certificat doit correspondre à « *.contoso100.com ».</span><span class="sxs-lookup"><span data-stu-id="789e6-124">For instance, if your domain is named 'contoso100.com', the certificate's subject name must be '*.contoso100.com'.</span></span> <span data-ttu-id="789e6-125">Définissez le nom DNS (nom alternatif du sujet) sur ce nom générique.</span><span class="sxs-lookup"><span data-stu-id="789e6-125">Set the DNS name (subject alternate name) to this wildcard name.</span></span>
4. <span data-ttu-id="789e6-126">**Utilisation de la clé** : le certificat doit être configuré pour le chiffrage de clés et les signatures numériques.</span><span class="sxs-lookup"><span data-stu-id="789e6-126">**Key usage** - The certificate must be configured for the following uses - Digital signatures and key encipherment.</span></span>
5. <span data-ttu-id="789e6-127">**Rôle du certificat** : le certificat doit être valide pour l’authentification de serveur SSL.</span><span class="sxs-lookup"><span data-stu-id="789e6-127">**Certificate purpose** - The certificate must be valid for SSL server authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="789e6-128">**Autorités de certification d’entreprise** : Azure AD Domain Services ne prend pas en charge les certificats LDAP sécurisés émis par l’autorité de certification de votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="789e6-128">**Enterprise Certification Authorities:** Azure AD Domain Services does not support using secure LDAP certificates issued by your organization's enterprise certification authority.</span></span> <span data-ttu-id="789e6-129">Ceci s’explique par le fait que le service ne reconnaît pas votre autorité de certification d’entreprise comme une autorité de certification racine.</span><span class="sxs-lookup"><span data-stu-id="789e6-129">This restriction is because the service does not trust your enterprise CA as a root certification authority.</span></span> 
>
>

<br>

## <a name="task-1---obtain-a-certificate-for-secure-ldap"></a><span data-ttu-id="789e6-130">Tâche 1 : Obtenir un certificat pour le protocole LDAP sécurisé</span><span class="sxs-lookup"><span data-stu-id="789e6-130">Task 1 - obtain a certificate for secure LDAP</span></span>
<span data-ttu-id="789e6-131">La première tâche consiste à obtenir un certificat à utiliser pour l’accès du protocole LDAP sécurisé au domaine géré.</span><span class="sxs-lookup"><span data-stu-id="789e6-131">The first task involves obtaining a certificate used for secure LDAP access to the managed domain.</span></span> <span data-ttu-id="789e6-132">Deux options s'offrent à vous :</span><span class="sxs-lookup"><span data-stu-id="789e6-132">You have two options:</span></span>

* <span data-ttu-id="789e6-133">Obtenez un certificat d’une autorité de certification.</span><span class="sxs-lookup"><span data-stu-id="789e6-133">Obtain a certificate from a certification authority.</span></span> <span data-ttu-id="789e6-134">L’autorité peut être une autorité de certification publique.</span><span class="sxs-lookup"><span data-stu-id="789e6-134">The authority may be a public certification authority.</span></span>
* <span data-ttu-id="789e6-135">Vous pouvez créer un certificat auto-signé.</span><span class="sxs-lookup"><span data-stu-id="789e6-135">Create a self-signed certificate.</span></span>

### <a name="option-a-recommended---obtain-a-secure-ldap-certificate-from-a-certification-authority"></a><span data-ttu-id="789e6-136">Option A (recommandée) : obtention d’un certificat LDAP sécurisé auprès d’une autorité de certification</span><span class="sxs-lookup"><span data-stu-id="789e6-136">Option A (Recommended) - Obtain a secure LDAP certificate from a certification authority</span></span>
<span data-ttu-id="789e6-137">Si votre organisation obtient ses certificats auprès d’une autorité de certification publique, vous devez obtenir le certificat LDAP sécurisé auprès de cette dernière.</span><span class="sxs-lookup"><span data-stu-id="789e6-137">If your organization obtains its certificates from a public certification authority, you need to obtain the secure LDAP certificate from that public certification authority.</span></span>

<span data-ttu-id="789e6-138">Quand vous demandez un certificat, veillez à satisfaire toutes les exigences détaillées dans la section [Configuration requise pour le certificat LDAP sécurisé](#requirements-for-the-secure-ldap-certificate).</span><span class="sxs-lookup"><span data-stu-id="789e6-138">When requesting a certificate, ensure that you satisfy all the requirements outlined in [Requirements for the secure LDAP certificate](#requirements-for-the-secure-ldap-certificate).</span></span>

> [!NOTE]
> <span data-ttu-id="789e6-139">Les ordinateurs clients qui doivent se connecter au domaine géré via le protocole LDAP sécurisé doivent approuver l’émetteur du certificat LDAP sécurisé.</span><span class="sxs-lookup"><span data-stu-id="789e6-139">Client computers that need to connect to the managed domain using secure LDAP must trust the issuer of the secure LDAP certificate.</span></span>
>
>

### <a name="option-b---create-a-self-signed-certificate-for-secure-ldap"></a><span data-ttu-id="789e6-140">Option B : création d’un certificat auto-signé pour le protocole LDAP sécurisé</span><span class="sxs-lookup"><span data-stu-id="789e6-140">Option B - Create a self-signed certificate for secure LDAP</span></span>
<span data-ttu-id="789e6-141">Si vous ne prévoyez pas d’utiliser un certificat d’une autorité de certification publique, vous pouvez choisir de créer un certificat auto-signé pour le protocole LDAP sécurisé.</span><span class="sxs-lookup"><span data-stu-id="789e6-141">If you do not expect to use a certificate from a public certification authority, you may choose to create a self-signed certificate for secure LDAP.</span></span>

<span data-ttu-id="789e6-142">**Créer un certificat auto-signé à l’aide de PowerShell**</span><span class="sxs-lookup"><span data-stu-id="789e6-142">**Create a self-signed certificate using PowerShell**</span></span>

<span data-ttu-id="789e6-143">Sur votre ordinateur Windows, ouvrez une nouvelle fenêtre PowerShell en tant **qu’administrateur** et saisissez les commandes suivantes, afin de créer un certificat auto-signé.</span><span class="sxs-lookup"><span data-stu-id="789e6-143">On your Windows computer, open a new PowerShell window as **Administrator** and type the following commands, to create a new self-signed certificate.</span></span>

    $lifetime=Get-Date

    New-SelfSignedCertificate -Subject *.contoso100.com -NotAfter $lifetime.AddDays(365) -KeyUsage DigitalSignature, KeyEncipherment -Type SSLServerAuthentication -DnsName *.contoso100.com

<span data-ttu-id="789e6-144">Dans l’exemple ci-dessus, remplacez « *.contoso100.com » par le nom de domaine DNS de votre domaine managé. Par exemple, si vous avez créé un domaine managé nommé « contoso100.onmicrosoft.com », remplacez «* . contoso100.com » dans le script ci-dessus par « *.contoso100.onmicrosoft.com ».</span><span class="sxs-lookup"><span data-stu-id="789e6-144">In the preceding sample, replace '*.contoso100.com' with the DNS domain name of your managed domain. For example, if you created a managed domain called 'contoso100.onmicrosoft.com', replace '*.contoso100.com' in the above script with '*.contoso100.onmicrosoft.com').</span></span>

![Sélectionner un annuaire Azure AD](./media/active-directory-domain-services-admin-guide/secure-ldap-powershell-create-self-signed-cert.png)

<span data-ttu-id="789e6-146">Le nouveau certificat auto-signé est placé dans le magasin de certificats de l’ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="789e6-146">The newly created self-signed certificate is placed in the local machine's certificate store.</span></span>


## <a name="next-step"></a><span data-ttu-id="789e6-147">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="789e6-147">Next step</span></span>
[<span data-ttu-id="789e6-148">Tâche 2 : Exporter le certificat du protocole LDAP sécurisé vers un fichier .PFX</span><span class="sxs-lookup"><span data-stu-id="789e6-148">Task 2 - export the secure LDAP certificate to a .PFX file</span></span>](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md)
