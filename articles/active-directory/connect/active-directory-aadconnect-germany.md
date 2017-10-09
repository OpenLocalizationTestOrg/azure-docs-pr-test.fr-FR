---
title: aaaAzure AD Connect en Allemagne de Microsoft Cloud
description: "Azure AD Connect intègre vos répertoires locaux à Azure Active Directory. Cela vous permet de tooprovide une identité commune pour les applications Office 365, Azure et SaaS intégrée à Azure AD."
keywords: "Introduction tooAzure AD Connect, vue d’ensemble de Azure AD Connect, ce qui est Azure AD Connect, installer active directory, Allemagne, noir forêt"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 2bcb0caf-5d97-46cb-8c32-bda66cc22dad
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: f32194fa6c365614f68e5d1ddcf0dac44d223292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-in-microsoft-cloud-germany---public-preview"></a>Azure AD Connect dans Microsoft Cloud Germany - Version préliminaire
## <a name="introduction"></a>Introduction
Azure AD Connect fournit la synchronisation entre Active Directory local et Azure Active Directory.
Actuellement, la plupart des scénarios de hello dans [Microsoft Cloud Allemagne](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) doit être réalisée par l’opérateur de hello. Lorsque vous utilisez Microsoft Cloud Allemagne, vous devez être conscient des éléments suivants de hello :

* Hello URL suivantes doivent être ouvert sur un serveur proxy pour la synchronisation toooccur correctement :
  
  * *.microsoftonline.de
  * *.windows.net
  * * Listes de révocation de certificat
* Lorsque vous vous connectez dans Windows Azure AD tooyour, vous devez utiliser un compte dans le domaine de onmicrosoft.de hello.
* Hello suivant les fonctionnalités n’est pas disponible :
  * Azure AD Connect Health
  * Mises à jour automatiques
 
## <a name="download"></a>Télécharger
Vous pouvez télécharger Azure AD Connect à partir du panneau d’Azure AD Connect hello dans le portail de hello.  Utilisez les instructions hello sous le panneau d’Azure AD Connect toolocate hello.

### <a name="hello-azure-ad-connect-blade"></a>Hello Panneau de connexion Azure AD
Une fois que vous avez connecté toohello portail Azure, procédez comme hello suivant :

1. Accédez tooBrowse
2. Sélectionnez Azure Active Directory
3. Puis sélectionnez Azure AD Connect

Vous devez voir s’afficher hello :

![Panneau Azure AD Connect](media/active-directory-aadconnect-germany/germany1.png)

Hello tableau suivant décrit les fonctionnalités de hello indiquées dans le panneau de hello.

| Intitulé | Description |
| --- | --- |
| ÉTAT DE LA SYNCHRONISATION |Vous indique si la synchronisation est activée ou désactivée. |
| DERNIÈRE SYNCHRONISATION |Hello la dernière fois qu’une synchronisation réussie s’est terminée. |
| DOMAINES FÉDÉRÉS |Affiche le nombre hello de domaines fédérés actuellement configuré. |

## <a name="installation"></a>Installation
tooinstall Azure AD Connect, vous pouvez utiliser la documentation de hello [ici](active-directory-aadconnect.md#install-azure-ad-connect).

## <a name="advanced-features-and-additional-information"></a>Fonctionnalités avancées et informations supplémentaires
Pour plus d’informations et des conseils sur les paramètres personnalisés ou les configurations avancées, commencez par [Intégration des identités locales avec Azure Active Directory](active-directory-aadconnect.md).  Cette page fournit des informations et des liens tooadditional Guide.

