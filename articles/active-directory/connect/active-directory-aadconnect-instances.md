---
title: 'Azure AD Connect : Instances de service Sync | Microsoft Docs'
description: "Cette page décrit des considérations spéciales relatives aux instances d’Azure AD."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: f340ea11-8ff5-4ae6-b09d-e939c76355a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2a0d8a599cf84cd6530bdbb24951156510d2cf3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-special-considerations-for-instances"></a>Azure AD Connect : considérations spéciales relatives aux instances
Azure AD Connect est plus couramment utilisé avec hello world-wide instance de Azure AD et Office 365. Mais il existe également d’autres instances, qui ont des exigences différentes en matière d’URL et autres considérations spéciales.

## <a name="microsoft-cloud-germany"></a>Microsoft Cloud Allemagne
Hello [Microsoft Cloud Allemagne](http://www.microsoft.de/cloud-deutschland) est un cloud souverain exploité par un tiers de confiance de données en allemand.

| Tooopen URL de serveur proxy |
| --- |
| \*.microsoftonline.de |
| \*.windows.net |
| + Listes de révocation de certificat |

Lorsque vous vous connectez dans le locataire Azure AD de tooyour, vous devez utiliser un compte dans le domaine de onmicrosoft.de hello.

Fonctionnalités qui ne sont pas présentes dans hello Microsoft Cloud Allemagne :

* **Azure AD Connect Health** n’est pas disponible.
* Les **mises à jour automatiques** ne sont pas disponibles.
* L’**écriture différée de mot de passe** est disponible en préversion avec Azure AD Connect version 1.1.570.0 et ultérieures.
* Les autres services Azure AD Premium ne sont pas disponibles.

## <a name="microsoft-azure-government-cloud"></a>Cloud Microsoft Azure Government
Hello [cloud de Microsoft Azure Government](https://azure.microsoft.com/features/gov/) est un cloud pour le gouvernement des États-Unis.

Ce cloud a été pris en charge par des versions antérieures de DirSync. À partir de la build 1.1.180 d’Azure AD Connect, hello nouvelle génération de cloud de hello est pris en charge. Cette génération à l’aide de points de terminaison en fonction des États-Unis uniquement et avoir une autre liste de tooopen de l’URL de votre serveur proxy.

| Tooopen URL de serveur proxy |
| --- |
| \**.microsoftonline.com |
| \*.microsoftonline.us |
| \*.gov.us.microsoftonline.com |
| + Listes de révocation de certificat |

Azure AD Connect n’est pas en mesure de détecter les tooautomatically que votre client Azure AD se trouve dans le cloud de gouvernement hello. Au lieu de cela, vous devez hello tootake suivant des actions lorsque vous installez Azure AD Connect.

1. Démarrer l’installation d’Azure AD Connect hello.
2. Lorsque vous voyez hello première page où vous êtes supposé tooaccept hello CLUF, ne continuez pas, mais laissez l’Assistant installation de hello en cours d’exécution.
3. Démarrez regedit et modifier la clé de Registre hello `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` toohello valeur `2`.
4. Assistant d’installation toohello Azure AD Connect revenir en arrière, accepter hello CLUF et continuer. Pendant l’installation, assurez-vous que toouse hello **configuration personnalisée** chemin d’accès de l’installation (et non l’installation Express). Poursuivez les installation Bonjour comme d’habitude.

Fonctionnalités qui ne sont pas présentes dans le cloud de Microsoft Azure Government hello :

* **Azure AD Connect Health** n’est pas disponible.
* Les **mises à jour automatiques** ne sont pas disponibles.
* L’**écriture différée de mot de passe** est disponible en préversion avec Azure AD Connect version 1.1.570.0 et ultérieures.
* Les autres services Azure AD Premium ne sont pas disponibles.

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur l’ [intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).
