---
title: "Résolution des problèmes liés aux erreurs du pack de contenu des journaux d’activité Azure Active Directory | Microsoft Docs"
description: "Vous fournit une liste des messages d’erreur des toofix d’activité Active Directory de Azure de hello contenu de pack et suit les."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 325de65ff1572a2f8f8319c0a52350bda03af3de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-active-directory-activity-logs-content-pack-errors"></a>Résolution des problèmes liés aux erreurs du pack de contenu des journaux d’activité Azure Active Directory 


Lorsque vous travaillez hello Pack de contenu Power BI pour la version préliminaire de Azure Active Directory, il est possible que vous rencontrez hello les erreurs suivantes : 

- [Échec de l’actualisation](active-directory-reporting-troubleshoot-content-pack.md#refresh-failed) 
- [Informations d’identification de source de données tooupdate ayant échoué](active-directory-reporting-troubleshoot-content-pack.md#failed-to-update-data-source-credentials) 
- [L’importation de données prend trop de temps](active-directory-reporting-troubleshoot-content-pack.md#importing-of-data-is-taking-too-long) 
 
Cette rubrique vous fournit des informations sur les causes possibles de hello et comment toofix ces erreurs.
 
## <a name="refresh-failed"></a>Échec de l’actualisation 
 
**Comment cette erreur est apparue**: courrier électronique à partir de Power BI ou état d’échec dans l’historique d’actualisation hello. 


| Cause : | Comment toofix |
| ---   | ---        |
| Actualiser les erreurs peuvent être générées lorsque les informations d’identification hello d’utilisateurs hello connexion toohello pack de contenu ont été réinitialisées mais ne pas mis à jour dans les paramètres de connexion hello Hello du pack de contenu hello de défaillance. | Dans Power BI, recherchez hello dataset toohello correspondante du tableau de bord Azure Active Directory activité des journaux (journaux d’activité Active Directory de Azure), choisissez planifier l’actualisation, puis entrez vos informations d’identification Azure AD. |
| Une actualisation peut échouer en raison de problèmes toodata Bonjour sous-jacent du pack de contenu. | Soumettez un ticket de support. Pour plus d’informations, consultez [comment tooget prennent en charge pour Azure Active Directory](active-directory-troubleshooting-support-howto.md).|
 
 
## <a name="failed-tooupdate-data-source-credentials"></a>Informations d’identification de source de données tooupdate ayant échoué 
 
**Comment cette erreur est apparue**: dans Power BI, lorsque vous vous connectez le pack de contenu toohello activité Active Directory de Azure (aperçu) de journaux. 

| Cause : | Comment toofix |
| ---   | ---        |
| utilisateur de connexion Hello est ni un administrateur global, ni un lecteur de sécurité ou un administrateur de sécurité. | Utilisez un compte qui est un administrateur global ou d’un lecteur de sécurité ou d’une sécurité admin tooaccess hello les packs de contenu. |
| Votre locataire n’est pas de type Premium ou ne compte aucun utilisateur avec un fichier de licence Premium. | Soumettez un ticket de support. Pour plus d’informations, consultez [comment tooget prennent en charge pour Azure Active Directory](active-directory-troubleshooting-support-howto.md).|
 

 

## <a name="importing-of-data-is-taking-too-long"></a>L’importation de données prend trop de temps 
 
**Comment cette erreur est apparue**: dans Power BI, une fois que vous avez connecté votre pack de contenu, processus d’importation de données de hello démarre tooprepare votre tableau de bord pour le journal d’activité Active Directory de Azure. Vous voyez le message de type hello : «*l’importation de données...* »  

| Cause : | Comment toofix |
| ---   | ---        |
| Selon la taille de hello de votre client, cette étape peut prendre de quelques minutes too30 minutes. | Soyez patient. Si le message de type hello ne change pas tooshowing votre tableau de bord dans l’heure, veuillez soumettre un ticket de support. Pour plus d’informations, consultez [comment tooget prennent en charge pour Azure Active Directory](active-directory-troubleshooting-support-howto.md).|

## <a name="next-steps"></a>Étapes suivantes

tooinstall hello Pack de contenu Power BI pour Azure Active Directory en version préliminaire, cliquez sur [ici](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).


