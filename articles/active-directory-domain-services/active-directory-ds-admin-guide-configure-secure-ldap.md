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
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a>Configurer le protocole LDAPS (LDAP sécurisé) pour un domaine managé Azure AD Domain Services
Cet article explique comment activer le protocole LDAPS pour votre domaine géré par les services de domaine Azure Active Directory. Le protocole LDAP sécurisé est également appelé « protocole LDAP sur SSL (Secure Sockets Layer) / TLS (Transport Layer Security) ».

## <a name="before-you-begin"></a>Avant de commencer
tâches de hello tooperform répertoriées dans cet article, vous devez :

1. Un **abonnement Azure**valide.
2. Un **répertoire Azure AD** , synchronisé avec un répertoire local ou un répertoire cloud uniquement.
3. **Les Services de domaine Active Directory Azure** doit être activée pour le répertoire de hello Azure AD. Si vous n’avez pas encore fait, suivez toutes les tâches de hello présentées dans hello [guide Mise en route](active-directory-ds-getting-started.md).
4. A **LDAP sécurisé de certificat toobe utilisé tooenable**.

   * **Recommandé** - Procurez-vous un certificat auprès de votre autorité de certification publique de confiance. Cette option de configuration est plus sûre.
   * Ou bien, vous pouvez également choisir trop[créer un certificat auto-signé](#task-1---obtain-a-certificate-for-secure-ldap) comme indiqué plus loin dans cet article.

<br>

### <a name="requirements-for-hello-secure-ldap-certificate"></a>Configuration requise pour un certificat LDAP sécurisé de hello
Obtenir un certificat valid par hello suivant les instructions, avant d’activer le protocole LDAP sécurisé. Vous rencontrez des défaillances Si vous essayez de tooenable LDAP sécurisé pour votre domaine géré avec un certificat non valide/incorrect.

1. **L’émetteur approuvé** -hello doit être délivré par une autorité approuvée par les ordinateurs qui se connectent toohello de domaine gérés à l’aide de LDAP sécurisé. Cette autorité peut être une autorité de certification approuvée par ces ordinateurs.
2. **Durée de vie** -certificat de hello doit être valide pour au moins hello suivants 3 à 6 mois. Accès tooyour managé domaine LDAP sécurisé est interrompu lors de l’expiration du certificat hello.
3. **Nom de l’objet** -nom de l’objet sur le certificat de hello hello doit être un caractère générique pour votre domaine géré. Par exemple, si votre domaine est nommé « contoso100.com », nom du sujet du certificat hello doit être ' *. contoso100.com'. Nom de caractère générique du nom (autre nom du sujet) toothis hello DNS du jeu.
4. **Utilisation de la clé** - certificat de hello doit être configuré pour hello suivant utilise - chiffrage de clés et les signatures numériques.
5. **L’objet du certificat** -certificat de hello doit être valide pour l’authentification de serveur SSL.

> [!NOTE]
> **Autorités de certification d’entreprise** : Azure AD Domain Services ne prend pas en charge les certificats LDAP sécurisés émis par l’autorité de certification de votre entreprise. Cette restriction est, car le service de hello n’approuve pas votre autorité de certification comme une autorité de certification racine d’entreprise. 
>
>

<br>

## <a name="task-1---obtain-a-certificate-for-secure-ldap"></a>Tâche 1 : Obtenir un certificat pour le protocole LDAP sécurisé
tâche première Hello implique l’obtention d’un certificat utilisé pour l’accès toohello managé domaine LDAP sécurisé. Deux options s'offrent à vous :

* Obtenez un certificat d’une autorité de certification. autorité de Hello peut être une autorité de certification publique.
* Vous pouvez créer un certificat auto-signé.

### <a name="option-a-recommended---obtain-a-secure-ldap-certificate-from-a-certification-authority"></a>Option A (recommandée) : obtention d’un certificat LDAP sécurisé auprès d’une autorité de certification
Si votre organisation obtient ses certificats auprès d’une autorité de certification publique, vous devez tooobtain hello certificat LDAP sécurisé à partir de cette autorité de certification publique.

Lorsque vous demandez un certificat, vérifiez que vous satisfont à toutes les exigences de hello décrites dans [configuration requise pour un certificat LDAP sécurisé de hello](#requirements-for-the-secure-ldap-certificate).

> [!NOTE]
> Ordinateurs clients qui nécessitent le domaine géré de tooconnect toohello à l’aide de LDAP sécurisé doivent approuver l’émetteur de hello du certificat LDAP sécurisé de hello.
>
>

### <a name="option-b---create-a-self-signed-certificate-for-secure-ldap"></a>Option B : création d’un certificat auto-signé pour le protocole LDAP sécurisé
Si vous ne prévoyez pas toouse un certificat auprès d’une autorité de certification publique, vous pouvez choisir toocreate un certificat auto-signé pour LDAP sécurisé.

**Créer un certificat auto-signé à l’aide de PowerShell**

Sur votre ordinateur Windows, ouvrez une nouvelle fenêtre PowerShell en tant que **administrateur** et hello du type suivant de commandes, toocreate un nouveau certificat auto-signé.

    $lifetime=Get-Date

    New-SelfSignedCertificate -Subject *.contoso100.com -NotAfter $lifetime.AddDays(365) -KeyUsage DigitalSignature, KeyEncipherment -Type SSLServerAuthentication -DnsName *.contoso100.com

Bonjour précédent exemple, remplacez «*. contoso100.com' avec le nom de domaine DNS hello de votre domaine géré. Par exemple, si vous avez créé un domaine géré appelé « contoso100.onmicrosoft.com », remplacez «*. contoso100.com' Bonjour au-dessus de script avec ' *. contoso100.onmicrosoft.com').

![Sélectionner un annuaire Azure AD](./media/active-directory-domain-services-admin-guide/secure-ldap-powershell-create-self-signed-cert.png)

Hello nouvellement créé un certificat auto-signé est placé dans le magasin de certificats de l’ordinateur local hello.


## <a name="next-step"></a>Étape suivante
[Tâche 2 : exporter hello tooa du certificat LDAP sécurisé. Fichier PFX](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md)
