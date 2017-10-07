---
title: "Azure AD Connect : Bien démarrer avec les paramètres express | Microsoft Docs"
description: "Découvrez comment toodownload, installer et exécuter l’Assistant Installation de hello pour Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: curtand
ms.assetid: b6ce45fd-554d-4f4d-95d1-47996d561c9f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 79f796fa7738b85e9236e856bddb529379f60390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-ad-connect-using-express-settings"></a>Prise en main d’Azure AD Connect à l’aide de paramètres express
La **configuration rapide** d’Azure AD Connect est utilisée lorsque vous disposez d’une topologie à une forêt unique et la [synchronisation de mot de passe](active-directory-aadconnectsync-implement-password-synchronization.md) est utilisée pour l’authentification. **Configuration rapide** est l’option par défaut de hello et est utilisé pour le scénario de hello couramment déployé. Vous est uniquement quelques tooextend rangement clics court votre cloud toohello de répertoire local.

Avant de commencer l’installation d’Azure AD Connect, assurez-vous que trop[Téléchargez Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771) préalable hello terminé les étapes [Azure AD Connect : conditions matérielles et](active-directory-aadconnect-prerequisites.md).

Si la configuration rapide ne correspond pas à votre topologie, consultez la [documentation connexe](#related-documentation) pour d’autres scénarios.

## <a name="express-installation-of-azure-ad-connect"></a>Installation rapide pour Azure AD Connect
Vous pouvez voir ces étapes dans l’action Bonjour [vidéos](#videos) section.

1. Connectez-vous en tant qu’un administrateur local toohello serveur tooinstall Azure AD Connect sur. Vous devez le faire sur un serveur de hello vous souhaitez le serveur de synchronisation toobe hello.
2. Accédez de double-clic tooand **AzureADConnect.msi**.
3. Sur l’écran d’accueil hello, sélectionnez les toohello acceptant boîte hello contrat de licence, puis cliquez sur **continuer**.  
4. Dans l’écran des paramètres hello Express, cliquez sur **utiliser express paramètres**.  
   ![Bienvenue dans tooAzure AD Connect](./media/active-directory-aadconnect-get-started-express/express.png)
5. Sur l’écran tooAzure AD de se connecter hello, entrez le nom d’utilisateur hello et un mot de passe d’un administrateur général pour votre annuaire Azure AD. Cliquez sur **Suivant**.  
   ![Se connecter tooAzure AD](./media/active-directory-aadconnect-get-started-express/connectaad.png) si vous recevez une erreur et que vous avez des problèmes de connectivité, consultez [résoudre les problèmes de connectivité](active-directory-aadconnect-troubleshoot-connectivity.md).
6. À l’écran de DS tooAD hello se connecter, entrez hello username et password pour un compte administrateur d’entreprise. Vous pouvez entrer une partie du domaine hello au format NetBios ou nom de domaine complet, c'est-à-dire que FABRIKAM\administrator ou fabrikam.com\administrator. Cliquez sur **Suivant**.  
   ![Se connecter tooAD DS](./media/active-directory-aadconnect-get-started-express/connectad.png)
7. Hello [ **configuration d’authentification dans Azure AD** ](active-directory-aadconnect-user-signin.md#azure-ad-sign-in-configuration) page affiche uniquement si vous n’avez pas effectué [vérifier vos domaines](../active-directory-add-domain.md) Bonjour [conditions préalables](active-directory-aadconnect-prerequisites.md).
   ![Domaines non vérifiés](./media/active-directory-aadconnect-get-started-express/unverifieddomain.png)  
   Si vous voyez cette page, passez en revue chaque domaine marqué **Non ajouté** et **Non vérifié**. Assurez-vous que les domaines que vous utilisez ont été vérifiés dans Azure AD. Lorsque vous avez vérifié vos domaines, cliquez sur symboles d’actualisation hello.
8. Sur hello tooconfigure prêt, cliquez sur **installer**.
   * Si vous le souhaitez sur la page de prêt tooconfigure hello, vous pouvez désélectionner hello **démarrer le processus de synchronisation hello dès la fin de la configuration** case à cocher. Vous devez désélectionner cette case à cocher si vous voulez toodo une configuration supplémentaire, tel que [filtrage](active-directory-aadconnectsync-configure-filtering.md). Si vous désélectionnez cette option, Assistant de hello configure la synchronisation, mais laisse de planificateur hello désactivé. Il ne s’exécute pas jusqu'à ce que vous l’activiez manuellement [réexécuter l’Assistant installation hello](active-directory-aadconnectsync-installation-wizard.md).
   * Si vous avez Exchange dans votre annuaire Active Directory local, puis que vous avez également une option tooenable [ **déploiement Exchange hybride**](https://technet.microsoft.com/library/jj200581.aspx). Activez cette option si vous envisagez toohave boîtes aux lettres Exchange à la fois dans le cloud de hello et localement au hello même temps.
     ![Prêt tooconfigure Azure AD Connect](./media/active-directory-aadconnect-get-started-express/readytoconfigure.png)
9. Fin de l’installation de hello, cliquez sur **Exit**.
10. Après installation Bonjour, déconnectez-vous et reconnectez-vous avant d’utiliser le Gestionnaire de Service de synchronisation ou l’éditeur de règles de synchronisation.

## <a name="videos"></a>Vidéos
Pour une vidéo sur l’installation d’express hello, consultez :

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Express-Settings/player]
> 
> 

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez Azure AD Connect installée, vous pouvez [vérifier l’installation de hello et attribuer des licences](active-directory-aadconnect-whats-next.md).

En savoir plus sur ces fonctionnalités, qui ont été activées avec l’installation de hello : [mise à niveau automatique](active-directory-aadconnect-feature-automatic-upgrade.md), [empêcher des suppressions accidentelles](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md), et [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md).

En savoir plus sur ces sujets courants : [planificateur et comment synchroniser les tootrigger](active-directory-aadconnectsync-feature-scheduler.md).

En savoir plus sur l’ [intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).

## <a name="related-documentation"></a>documentation connexe
| Rubrique |
| --- | --- |
| Présentation d’Azure AD Connect |
| Installation à l’aide des paramètres personnalisés |
| Mise à niveau à partir de DirSync |
| Comptes utilisés pour l’installation |

