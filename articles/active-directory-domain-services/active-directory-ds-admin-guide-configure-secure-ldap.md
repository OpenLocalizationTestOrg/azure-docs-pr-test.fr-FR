---
title: "aaaConfigure sécurisé LDAP (LDAPS) dans les Services de domaine Active Directory de Azure | Documents Microsoft"
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
ms.openlocfilehash: 99e44d917b115d7f7a67ff0a5e22c5c9165287e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="dd22d-103">Configurer le protocole LDAPS (LDAP sécurisé) pour un domaine managé Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="dd22d-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="dd22d-104">Cet article explique comment activer le protocole LDAPS pour votre domaine géré par les services de domaine Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dd22d-104">This article shows how you can enable Secure Lightweight Directory Access Protocol (LDAPS) for your Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="dd22d-105">Le protocole LDAP sécurisé est également appelé « protocole LDAP sur SSL (Secure Sockets Layer) / TLS (Transport Layer Security) ».</span><span class="sxs-lookup"><span data-stu-id="dd22d-105">Secure LDAP is also known as 'Lightweight Directory Access Protocol (LDAP) over Secure Sockets Layer (SSL) / Transport Layer Security (TLS)'.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="dd22d-106">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="dd22d-106">Before you begin</span></span>
<span data-ttu-id="dd22d-107">tâches de hello tooperform répertoriées dans cet article, vous devez :</span><span class="sxs-lookup"><span data-stu-id="dd22d-107">tooperform hello tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="dd22d-108">Un **abonnement Azure**valide.</span><span class="sxs-lookup"><span data-stu-id="dd22d-108">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="dd22d-109">Un **répertoire Azure AD** , synchronisé avec un répertoire local ou un répertoire cloud uniquement.</span><span class="sxs-lookup"><span data-stu-id="dd22d-109">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="dd22d-110">**Les Services de domaine Active Directory Azure** doit être activée pour le répertoire de hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd22d-110">**Azure AD Domain Services** must be enabled for hello Azure AD directory.</span></span> <span data-ttu-id="dd22d-111">Si vous n’avez pas encore fait, suivez toutes les tâches de hello présentées dans hello [guide Mise en route](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="dd22d-111">If you haven't done so, follow all hello tasks outlined in hello [Getting Started guide](active-directory-ds-getting-started.md).</span></span>
4. <span data-ttu-id="dd22d-112">A **LDAP sécurisé de certificat toobe utilisé tooenable**.</span><span class="sxs-lookup"><span data-stu-id="dd22d-112">A **certificate toobe used tooenable secure LDAP**.</span></span>

   * <span data-ttu-id="dd22d-113">**Recommandé** - Procurez-vous un certificat auprès de votre autorité de certification publique de confiance.</span><span class="sxs-lookup"><span data-stu-id="dd22d-113">**Recommended** - Obtain a certificate from a trusted public certification authority.</span></span> <span data-ttu-id="dd22d-114">Cette option de configuration est plus sûre.</span><span class="sxs-lookup"><span data-stu-id="dd22d-114">This configuration option is more secure.</span></span>
   * <span data-ttu-id="dd22d-115">Ou bien, vous pouvez également choisir trop[créer un certificat auto-signé](#task-1---obtain-a-certificate-for-secure-ldap) comme indiqué plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="dd22d-115">Alternately, you may also choose too[create a self-signed certificate](#task-1---obtain-a-certificate-for-secure-ldap) as shown later in this article.</span></span>

<br>

### <a name="requirements-for-hello-secure-ldap-certificate"></a><span data-ttu-id="dd22d-116">Configuration requise pour un certificat LDAP sécurisé de hello</span><span class="sxs-lookup"><span data-stu-id="dd22d-116">Requirements for hello secure LDAP certificate</span></span>
<span data-ttu-id="dd22d-117">Obtenir un certificat valid par hello suivant les instructions, avant d’activer le protocole LDAP sécurisé.</span><span class="sxs-lookup"><span data-stu-id="dd22d-117">Acquire a valid certificate per hello following guidelines, before you enable secure LDAP.</span></span> <span data-ttu-id="dd22d-118">Vous rencontrez des défaillances Si vous essayez de tooenable LDAP sécurisé pour votre domaine géré avec un certificat non valide/incorrect.</span><span class="sxs-lookup"><span data-stu-id="dd22d-118">You encounter failures if you try tooenable secure LDAP for your managed domain with an invalid/incorrect certificate.</span></span>

1. <span data-ttu-id="dd22d-119">**L’émetteur approuvé** -hello doit être délivré par une autorité approuvée par les ordinateurs qui se connectent toohello de domaine gérés à l’aide de LDAP sécurisé.</span><span class="sxs-lookup"><span data-stu-id="dd22d-119">**Trusted issuer** - hello certificate must be issued by an authority trusted by computers connecting toohello managed domain using secure LDAP.</span></span> <span data-ttu-id="dd22d-120">Cette autorité peut être une autorité de certification approuvée par ces ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="dd22d-120">This authority may be a public certification authority trusted by these computers.</span></span>
2. <span data-ttu-id="dd22d-121">**Durée de vie** -certificat de hello doit être valide pour au moins hello suivants 3 à 6 mois.</span><span class="sxs-lookup"><span data-stu-id="dd22d-121">**Lifetime** - hello certificate must be valid for at least hello next 3-6 months.</span></span> <span data-ttu-id="dd22d-122">Accès tooyour managé domaine LDAP sécurisé est interrompu lors de l’expiration du certificat hello.</span><span class="sxs-lookup"><span data-stu-id="dd22d-122">Secure LDAP access tooyour managed domain is disrupted when hello certificate expires.</span></span>
3. <span data-ttu-id="dd22d-123">**Nom de l’objet** -nom de l’objet sur le certificat de hello hello doit être un caractère générique pour votre domaine géré.</span><span class="sxs-lookup"><span data-stu-id="dd22d-123">**Subject name** - hello subject name on hello certificate must be a wildcard for your managed domain.</span></span> <span data-ttu-id="dd22d-124">Par exemple, si votre domaine est nommé « contoso100.com », nom du sujet du certificat hello doit être ' *. contoso100.com'.</span><span class="sxs-lookup"><span data-stu-id="dd22d-124">For instance, if your domain is named 'contoso100.com', hello certificate's subject name must be '*.contoso100.com'.</span></span> <span data-ttu-id="dd22d-125">Nom de caractère générique du nom (autre nom du sujet) toothis hello DNS du jeu.</span><span class="sxs-lookup"><span data-stu-id="dd22d-125">Set hello DNS name (subject alternate name) toothis wildcard name.</span></span>
4. <span data-ttu-id="dd22d-126">**Utilisation de la clé** - certificat de hello doit être configuré pour hello suivant utilise - chiffrage de clés et les signatures numériques.</span><span class="sxs-lookup"><span data-stu-id="dd22d-126">**Key usage** - hello certificate must be configured for hello following uses - Digital signatures and key encipherment.</span></span>
5. <span data-ttu-id="dd22d-127">**L’objet du certificat** -certificat de hello doit être valide pour l’authentification de serveur SSL.</span><span class="sxs-lookup"><span data-stu-id="dd22d-127">**Certificate purpose** - hello certificate must be valid for SSL server authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="dd22d-128">**Autorités de certification d’entreprise** : Azure AD Domain Services ne prend pas en charge les certificats LDAP sécurisés émis par l’autorité de certification de votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="dd22d-128">**Enterprise Certification Authorities:** Azure AD Domain Services does not support using secure LDAP certificates issued by your organization's enterprise certification authority.</span></span> <span data-ttu-id="dd22d-129">Cette restriction est, car le service de hello n’approuve pas votre autorité de certification comme une autorité de certification racine d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="dd22d-129">This restriction is because hello service does not trust your enterprise CA as a root certification authority.</span></span> 
>
>

<br>

## <a name="task-1---obtain-a-certificate-for-secure-ldap"></a><span data-ttu-id="dd22d-130">Tâche 1 : Obtenir un certificat pour le protocole LDAP sécurisé</span><span class="sxs-lookup"><span data-stu-id="dd22d-130">Task 1 - obtain a certificate for secure LDAP</span></span>
<span data-ttu-id="dd22d-131">tâche première Hello implique l’obtention d’un certificat utilisé pour l’accès toohello managé domaine LDAP sécurisé.</span><span class="sxs-lookup"><span data-stu-id="dd22d-131">hello first task involves obtaining a certificate used for secure LDAP access toohello managed domain.</span></span> <span data-ttu-id="dd22d-132">Deux options s'offrent à vous :</span><span class="sxs-lookup"><span data-stu-id="dd22d-132">You have two options:</span></span>

* <span data-ttu-id="dd22d-133">Obtenez un certificat d’une autorité de certification.</span><span class="sxs-lookup"><span data-stu-id="dd22d-133">Obtain a certificate from a certification authority.</span></span> <span data-ttu-id="dd22d-134">autorité de Hello peut être une autorité de certification publique.</span><span class="sxs-lookup"><span data-stu-id="dd22d-134">hello authority may be a public certification authority.</span></span>
* <span data-ttu-id="dd22d-135">Vous pouvez créer un certificat auto-signé.</span><span class="sxs-lookup"><span data-stu-id="dd22d-135">Create a self-signed certificate.</span></span>

### <a name="option-a-recommended---obtain-a-secure-ldap-certificate-from-a-certification-authority"></a><span data-ttu-id="dd22d-136">Option A (recommandée) : obtention d’un certificat LDAP sécurisé auprès d’une autorité de certification</span><span class="sxs-lookup"><span data-stu-id="dd22d-136">Option A (Recommended) - Obtain a secure LDAP certificate from a certification authority</span></span>
<span data-ttu-id="dd22d-137">Si votre organisation obtient ses certificats auprès d’une autorité de certification publique, vous devez tooobtain hello certificat LDAP sécurisé à partir de cette autorité de certification publique.</span><span class="sxs-lookup"><span data-stu-id="dd22d-137">If your organization obtains its certificates from a public certification authority, you need tooobtain hello secure LDAP certificate from that public certification authority.</span></span>

<span data-ttu-id="dd22d-138">Lorsque vous demandez un certificat, vérifiez que vous satisfont à toutes les exigences de hello décrites dans [configuration requise pour un certificat LDAP sécurisé de hello](#requirements-for-the-secure-ldap-certificate).</span><span class="sxs-lookup"><span data-stu-id="dd22d-138">When requesting a certificate, ensure that you satisfy all hello requirements outlined in [Requirements for hello secure LDAP certificate](#requirements-for-the-secure-ldap-certificate).</span></span>

> [!NOTE]
> <span data-ttu-id="dd22d-139">Ordinateurs clients qui nécessitent le domaine géré de tooconnect toohello à l’aide de LDAP sécurisé doivent approuver l’émetteur de hello du certificat LDAP sécurisé de hello.</span><span class="sxs-lookup"><span data-stu-id="dd22d-139">Client computers that need tooconnect toohello managed domain using secure LDAP must trust hello issuer of hello secure LDAP certificate.</span></span>
>
>

### <a name="option-b---create-a-self-signed-certificate-for-secure-ldap"></a><span data-ttu-id="dd22d-140">Option B : création d’un certificat auto-signé pour le protocole LDAP sécurisé</span><span class="sxs-lookup"><span data-stu-id="dd22d-140">Option B - Create a self-signed certificate for secure LDAP</span></span>
<span data-ttu-id="dd22d-141">Si vous ne prévoyez pas toouse un certificat auprès d’une autorité de certification publique, vous pouvez choisir toocreate un certificat auto-signé pour LDAP sécurisé.</span><span class="sxs-lookup"><span data-stu-id="dd22d-141">If you do not expect toouse a certificate from a public certification authority, you may choose toocreate a self-signed certificate for secure LDAP.</span></span>

<span data-ttu-id="dd22d-142">**Créer un certificat auto-signé à l’aide de PowerShell**</span><span class="sxs-lookup"><span data-stu-id="dd22d-142">**Create a self-signed certificate using PowerShell**</span></span>

<span data-ttu-id="dd22d-143">Sur votre ordinateur Windows, ouvrez une nouvelle fenêtre PowerShell en tant que **administrateur** et hello du type suivant de commandes, toocreate un nouveau certificat auto-signé.</span><span class="sxs-lookup"><span data-stu-id="dd22d-143">On your Windows computer, open a new PowerShell window as **Administrator** and type hello following commands, toocreate a new self-signed certificate.</span></span>

    $lifetime=Get-Date

    New-SelfSignedCertificate -Subject *.contoso100.com -NotAfter $lifetime.AddDays(365) -KeyUsage DigitalSignature, KeyEncipherment -Type SSLServerAuthentication -DnsName *.contoso100.com

<span data-ttu-id="dd22d-144">Bonjour précédent exemple, remplacez «*. contoso100.com' avec le nom de domaine DNS hello de votre domaine géré. Par exemple, si vous avez créé un domaine géré appelé « contoso100.onmicrosoft.com », remplacez «*. contoso100.com' Bonjour au-dessus de script avec ' *. contoso100.onmicrosoft.com').</span><span class="sxs-lookup"><span data-stu-id="dd22d-144">In hello preceding sample, replace '*.contoso100.com' with hello DNS domain name of your managed domain. For example, if you created a managed domain called 'contoso100.onmicrosoft.com', replace '*.contoso100.com' in hello above script with '*.contoso100.onmicrosoft.com').</span></span>

![Sélectionner un annuaire Azure AD](./media/active-directory-domain-services-admin-guide/secure-ldap-powershell-create-self-signed-cert.png)

<span data-ttu-id="dd22d-146">Hello nouvellement créé un certificat auto-signé est placé dans le magasin de certificats de l’ordinateur local hello.</span><span class="sxs-lookup"><span data-stu-id="dd22d-146">hello newly created self-signed certificate is placed in hello local machine's certificate store.</span></span>


## <a name="next-step"></a><span data-ttu-id="dd22d-147">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="dd22d-147">Next step</span></span>
[<span data-ttu-id="dd22d-148">Tâche 2 : exporter hello tooa du certificat LDAP sécurisé. Fichier PFX</span><span class="sxs-lookup"><span data-stu-id="dd22d-148">Task 2 - export hello secure LDAP certificate tooa .PFX file</span></span>](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md)
