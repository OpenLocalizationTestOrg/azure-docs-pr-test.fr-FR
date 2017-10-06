---
title: "Azure Active Directory Domain Services : Activer la délégation Kerberos contrainte | Microsoft Docs"
description: "Activer la délégation Kerberos contrainte sur les domaines gérés par les services de domaine Azure Active Directory"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: d32547c8018dd1f99c992e95a01d2711d460a261
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-kerberos-constrained-delegation-kcd-on-a-managed-domain"></a>Configurer la délégation Kerberos contrainte (KCD) sur un domaine géré
De nombreuses applications doivent tooaccess des ressources dans le contexte de hello d’utilisateur de hello. Active Directory prend en charge un mécanisme, appelé délégation Kerberos, qui rend possible ce cas d’utilisation. En outre, vous pouvez limiter la délégation contrainte afin que des ressources spécifiques sont accessibles dans le contexte de hello d’utilisateur de hello. Les domaines gérés des services de domaine Azure AD diffèrent des domaines Active Directory traditionnels dans la mesure où ils sont verrouillés de façon mieux sécurisée.

Cet article vous explique comment tooconfigure kerberos délégation contrainte sur un domaine géré des Services de domaine Active Directory de Azure.

## <a name="kerberos-constrained-delegation-kcd"></a>Délégation Kerberos contrainte (KCD)
Délégation Kerberos permet un tooimpersonate compte un autre ressources tooaccess principal (par exemple, un utilisateur) de sécurité. Imaginez une application web qui accède à une API de web principal dans le contexte de hello d’un utilisateur. Dans cet exemple, hello application web (en cours d’exécution dans le contexte de hello d’un compte de service ou d’un compte d’ordinateur) emprunte l’identité hello utilisateur lors de l’accès des ressources de hello (API web principale). Délégation contrainte Kerberos n’est pas sécurisée, car elle ne restreint pas hello hello ressources empruntant l’identité du compte peut accéder dans le contexte de hello d’utilisateur de hello.

La délégation contrainte Kerberos (KCD) restreint hello serveur de ressources des services toowhich hello spécifié peut agir sur le compte hello d’un utilisateur. KCD traditionnel requiert tooconfigure de privilèges administrateur de domaine un compte de domaine pour un service et elle restreint le seul domaine hello compte tooa.

La KCD traditionnelle a également quelques problèmes qui lui sont associés. Dans les systèmes d’exploitation antérieurs où administrateur de domaine hello configuré le service de hello, administrateur de service hello n’avait aucun tooknow permettent les services frontaux déléguée toohello services de ressources qu’ils. Et tout service frontal qui pouvait effectuer une délégation tooa service des ressources représentait un point d’attaque potentiel. Si un serveur hébergeant un service frontal était compromis, et il a été configuré toodelegate tooresource services, services de ressources hello peuvent également être compromis.

> [!NOTE]
> Sur un domaine managé Azure AD Domain Services, vous n’avez pas les privilèges d’administrateur de domaine. Par conséquent, **la KCD traditionnelle ne peut pas être configurée sur un domaine géré**. Utilisez plutôt la KCD basée sur la ressource, comme décrit dans cet article. Ce mécanisme est également plus sécurisé.
>
>

## <a name="resource-based-kerberos-constrained-delegation"></a>Délégation Kerberos contrainte basée sur les ressources
Dans Windows Server 2012 R2 et Windows Server 2012, hello capacité tooconfigure limité la délégation pour service de hello a été transférée à partir de l’administrateur de service toohello hello domaine administrateur. De cette façon, administrateur de service principal hello peut autoriser ou refuser les services frontaux. Ce modèle est appelé **délégation Kerberos contrainte basée sur la ressource**.

La KCD basée sur la ressource est configurée à l’aide de PowerShell. Vous utilisez hello Set-ADComputer ou des applets de commande Set-ADUser, selon que hello empruntant l’identité du compte est un compte d’ordinateur ou un compte de service/compte d’utilisateur.

### <a name="configure-resource-based-kcd-for-a-computer-account-on-a-managed-domain"></a>Configuration d’une KCD basée sur la ressource pour un compte d’ordinateur sur un domaine géré
Supposons que vous avez une application web en cours d’exécution sur l’ordinateur de hello ' contoso100-webapp.contoso100.com ». Il a besoin de ressources de hello tooaccess (une API web en cours d’exécution ' contoso100-api.contoso100.com ») dans le contexte de hello d’utilisateurs du domaine. Voici comment configurer une KCD basée sur les ressources pour ce scénario.

```
$ImpersonatingAccount = Get-ADComputer -Identity contoso100-webapp.contoso100.com
Set-ADComputer contoso100-api.contoso100.com -PrincipalsAllowedToDelegateToAccount $ImpersonatingAccount
```

### <a name="configure-resource-based-kcd-for-a-user-account-on-a-managed-domain"></a>Configuration d’une KCD basée sur la ressource pour un compte utilisateur sur un domaine géré
Supposons que vous avez une application web en cours d’exécution sous un compte de service « appsvc » et il a besoin de ressources de hello tooaccess (une API web en cours d’exécution sous un compte de service - 'backendsvc') de contexte hello d’utilisateurs du domaine. Voici comment configurer une KCD basée sur les ressources pour ce scénario.

```
$ImpersonatingAccount = Get-ADUser -Identity appsvc
Set-ADUser backendsvc -PrincipalsAllowedToDelegateToAccount $ImpersonatingAccount
```

## <a name="related-content"></a>Contenu connexe
* [Services de domaine Azure AD : guide de prise en main](active-directory-ds-getting-started.md)
* [Présentation de la délégation Kerberos contrainte](https://technet.microsoft.com/library/jj553400.aspx)
