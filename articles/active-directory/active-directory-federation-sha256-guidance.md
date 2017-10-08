---
title: algorithme de hachage de signature aaaChange pour Office 365 confiance | Documents Microsoft
description: "Cette page fournit des instructions permettant de modifier l’algorithme SHA pour l’approbation de fédération avec Office 365"
keywords: "SHA1, SHA256, O365, fédération, aadconnect, adfs, ad fs, modifier sha, approbation de fédération, approbation de partie de confiance"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: samueld
editor: 
ms.assetid: cf6880e2-af78-4cc9-91bc-b64de4428bbd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: anandy
ms.openlocfilehash: 3333d1384aff8bdf6b3bcc894f8c633fd9ccc3a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="change-signature-hash-algorithm-for-office-365-relying-party-trust"></a>Modifier l’algorithme de hachage de signature pour l’approbation de partie de confiance Office 365
## <a name="overview"></a>Vue d'ensemble
Services de fédération Active Directory (AD FS) se connecte à son tooensure d’Azure Active Directory tooMicrosoft jetons qui ne peut pas être falsifiées. Cette signature peut reposer sur SHA1 ou SHA256. Azure Active Directory prend désormais en charge les jetons signés avec un algorithme SHA256, et nous vous recommandons de définir hello tooSHA256 d’algorithme signature de jetons pour hello plus haut niveau de sécurité. Cet article décrit les étapes hello nécessaire toohello des algorithme de signature de jetons hello tooset plus sécurisée au niveau du SHA256.

>[!NOTE]
>Microsoft recommande l’utilisation de SHA256 comme algorithme de hello pour signer les jetons qu’il est plus sécurisé que SHA1 mais SHA1 reste toujours une option de prise en charge.

## <a name="change-hello-token-signing-algorithm"></a>Modifier l’algorithme de signature de jetons hello
Une fois que vous avez défini l’algorithme de signature hello avec l’un des deux processus hello ci-dessous, AD FS signe les jetons hello pour Office 365 confiance avec SHA256. Vous n’avez pas besoin toomake toutes les modifications de configuration supplémentaire, et cette modification n’a aucun impact sur votre capacité de tooaccess Office 365 ou d’autres applications Azure AD.

### <a name="ad-fs-management-console"></a>Console de gestion AD FS
1. Ouvrez la console de gestion hello AD FS sur le serveur de hello principal AD FS.
2. Développez le nœud de hello AD FS et cliquez sur **confiance**.
3. Faites un clic droit sur votre approbation de partie de confiance Office 365/Azure et sélectionnez **Propriétés**.
4. Sélectionnez hello **avancé** onglet et l’algorithme de hachage sécurisé hello sélectionnez SHA256.
5. Cliquez sur **OK**.

![Algorithme de signature SHA256 - MMC](./media/active-directory-aadconnectfed-sha256guidance/mmc.png)

### <a name="ad-fs-powershell-cmdlets"></a>Applets de commande PowerShell d’AD FS
1. Sur un serveur AD FS, ouvrez PowerShell avec des privilèges d’administrateur.
2. Algorithme de hachage sécurisé hello ensemble à l’aide de hello **Set-AdfsRelyingPartyTrust** applet de commande.
   
   <code>Set-AdfsRelyingPartyTrust -TargetName 'Microsoft Office 365 Identity Platform' -SignatureAlgorithm 'http://www.w3.org/2001/04/xmldsig-more#rsa-sha256'</code>

## <a name="also-read"></a>À lire également
* [Réparation de l’approbation Office 365 avec Azure AD Connect](connect/active-directory-aadconnect-federation-management.md#repairthetrust)

