---
title: aaaTroubleshoot un objet qui ne se synchronise pas tooAzure AD | Des documents Microsoft
description: "Résolution des problèmes un objet ne synchronise pas tooAzure AD."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 81e0a0793a1d5ec76cfcaec6e974726d7854f58e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-an-object-that-is-not-synchronizing-tooazure-ad"></a>Résoudre les problèmes d’un objet qui ne se synchronise pas tooAzure AD

Si un objet ne se synchronise pas comme attendu tooAzure AD, il peut être dû à plusieurs raisons. Si vous avez reçu un message d’erreur d’Azure AD ou que vous voyez l’erreur hello dans Azure AD Connect Health, puis lire [résoudre les erreurs d’exportation](active-directory-aadconnect-troubleshoot-sync-errors.md) à la place. Mais si vous dépannez un problème où les objets hello ne sont pas dans Azure AD, puis cette rubrique pour vous. Il décrit comment synchroniser les erreurs toofind dans le composant de local hello Azure AD Connect.

erreurs de hello toofind, vous allez toolook à plusieurs endroits dans hello suivant l’ordre :

1. Hello [journaux des opérations](#operations) pour rechercher les erreurs identifiées par le moteur de synchronisation hello pendant l’importation et synchronisation.
2. Hello [espace connecteur](#connector-space-object-properties) pour rechercher des objets manquants et les erreurs de synchronisation.
3. Hello [métaverse](#metaverse-object-properties) pour rechercher les problèmes liés aux données.

Démarrez [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md) avant de commencer ces étapes.

## <a name="operations"></a>Opérations
onglet opérations Hello hello Synchronization Service Manager est où vous devez commencer le dépannage. onglet d’opérations Hello montre les résultats de hello des opérations les plus récentes de hello.  
![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/operations.png)  

moitié supérieure de Hello affiche toutes les exécutions de chronique. Par défaut, journal des opérations hello conserve les informations relatives hello sept derniers jours, mais ce paramètre peut être modifié par hello [planificateur](active-directory-aadconnectsync-feature-scheduler.md). Vous souhaitez toolook pour une exécution qui n’affiche pas un état de réussite. Vous pouvez modifier hello tri en cliquant sur les en-têtes hello.

Hello **état** colonne est informations les plus importantes hello et montre hello plus grave problème pour une exécution. Voici un résumé des États de hello plus courantes dans l’ordre de priorité tooinvestigate (où * indiquer plusieurs chaînes d’erreur possible).

| État | Commentaire |
| --- | --- |
| stopped-* |Hello exécuter n’a pas pu se terminer. Par exemple, si hello système distant est arrêté et ne peut pas être contacté. |
| stopped-error-limit |Il existe plus de 5 000 erreurs. Hello exécuter a été automatiquement arrêté en raison de toohello un grand nombre d’erreurs. |
| completed-\*-errors |Hello exécution, mais il existe des erreurs (moins de 5 000) qui doivent être examinés. |
| completed-\*-warnings |Hello exécution terminée, mais certaines données ne sont pas en état de hello attendu. Si vous avez des erreurs, alors ce message n’est, en général, qu’un symptôme. N’examinez pas les avertissements avant d’avoir résolu les erreurs. |
| réussi |Aucun problème. |

Lorsque vous sélectionnez une ligne, en bas de hello met à jour les détails de hello tooshow de qui s’exécutent. toohello à gauche de la partie inférieure de hello, vous disposez d’un message de la liste **étape #**. Cette liste ne s’affiche que si votre forêt contient plusieurs domaines et que chaque domaine est représenté par une étape. nom de domaine Hello se trouve sous le titre de hello **Partition**. Sous **statistiques de synchronisation**, vous pouvez trouver plus d’informations sur le nombre de hello de modifications qui ont été traités. Vous pouvez cliquer sur hello liens tooget une liste d’objets de hello modifié. Si vous avez des objets comportant des erreurs, celles-ci s’affichent sous **Erreurs de synchronisation**.

### <a name="troubleshoot-errors-in-operations-tab"></a>Résoudre les erreurs dans l’onglet des opérations
![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/errorsync.png)  
Lorsque vous avez des erreurs, à la fois objet hello dans l’erreur et l’erreur hello lui-même sont des liens qui fournissent des informations supplémentaires.

Commencez par cliquer sur la chaîne d’erreur hello (**synchronisation-règle-erreur-fonction-déclenchée** dans l’image de hello). Tout d’abord, vous sont présentées avec une vue d’ensemble de l’objet de hello. toosee hello erreur, cliquez sur le bouton de hello **Trace de la pile**. Ce suivi fournit les informations de débogage au niveau de l’erreur de hello.

Vous pouvez cliquer sur Bonjour **les informations de pile d’appels** , choisissez **sélectionner tout**, et **copie**. Vous pouvez copier la pile de hello et examinez les erreurs hello dans votre éditeur favori, tel que le bloc-notes.

* Si l’erreur de hello provient **SyncRulesEngine**, puis les informations de pile des appels hello sont tout d’abord une liste de tous les attributs sur l’objet de hello. Faites défiler jusqu'à ce que vous voyez hello en-tête **InnerException = >**.  
  ![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/errorinnerexception.png)  
  ligne Hello affiche hello erreur. Dans l’image hello ci-dessus, erreur de hello est d’un Fabrikam de règle de synchronisation personnalisé créé.

Si l’erreur hello lui-même ne donne pas de suffisamment d’informations, il est toolook heure données hello lui-même. Vous pouvez cliquez sur le lien hello avec l’identificateur d’objet hello et poursuivez le dépannage hello [objet importé l’espace connecteur](#cs-import).

## <a name="connector-space-object-properties"></a>Propriétés de l’objet espace connecteur
Si vous n’avez pas les erreurs détectées dans hello [operations](#operations) onglet, l’étape suivante de hello est l’objet d’espace connecteur toofollow hello à partir d’Active Directory, toohello métaverse et tooAzure AD. Dans ce chemin d’accès, vous devez rechercher où le problème de hello est.

### <a name="search-for-an-object-in-hello-cs"></a>Rechercher un objet Bonjour CS

Dans **Synchronization Service Manager**, cliquez sur **connecteurs**, sélectionnez hello connecteur Active Directory, et **espace de connecteur de recherche**.

Dans **étendue**, sélectionnez **RDN** (lorsque vous souhaitez toosearch sur l’attribut CN hello) ou **DN ou ancre** (lorsque vous souhaitez toosearch sur l’attribut de distinguishedName hello). Entrez une valeur et cliquez sur **Rechercher**.  
![Espace de connecteur de recherche](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cssearch.png)  

Si vous ne trouvez pas l’objet de hello vous recherchez, puis elle peut ont été filtrée avec [filtrage basé sur le domaine](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering) ou [filtrage basé sur une unité d’organisation](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering). Hello de lecture [configurer le filtrage](active-directory-aadconnectsync-configure-filtering.md) tooverify de rubrique hello le filtrage est configuré comme prévu.

Une autre recherche utile est tooselect hello connecteur Azure AD, dans **étendue** sélectionnez **en attente importation**et sélectionnez hello **ajouter** case à cocher. Cette recherche vous propose tous les objets synchronisés dans Azure AD qui ne peuvent pas être associés à un objet local.  
![Recherche d’espace de connecteur orphelin](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cssearchorphan.png)  
Ces objets ont été créés par un autre moteur de synchronisation ou un moteur de synchronisation avec une autre configuration de filtrage. Cette vue est une liste d’objets **orphelins** qui ne sont plus gérés. Vous devez examiner cette liste et envisagez de supprimer ces objets à l’aide de hello [Azure AD PowerShell](http://aka.ms/aadposh) applets de commande.

### <a name="cs-import"></a>Importation de CS
Lorsque vous ouvrez un objet cs, il existe plusieurs onglets en haut de hello. Hello **importer** onglet affiche les données de salutation qui sont préparées après une importation.  
![Objet CS](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/csobject.png)    
Hello **ancienne valeur** montre ce qui est stocké dans se connecter et hello **nouvelle valeur** ce qui a été reçu à partir du système source de hello et n’a pas encore été appliqué. S’il existe une erreur sur l’objet de hello, modifications ne sont pas traitées.

**Erreur**  
![Objet CS](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cssyncerror.png)  
Hello **erreur de synchronisation** onglet est uniquement visible s’il existe un problème avec l’objet de hello. Pour plus d’informations, consultez [Résolution des problèmes de synchronisation](#troubleshoot-errors-in-operations-tab).

### <a name="cs-lineage"></a>Lignage CS
onglet de lignage Hello montre comment objet d’espace connecteur hello objet de métaverse toohello connexes. Vous pouvez voir lors de la dernière importation d’une modification de hello connecteur hello système connecté et les données de toopopulate règles appliquées dans hello métaverse.  
![Lignage CS](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cslineage.png)  
Bonjour **Action** colonne, vous pouvez voir une **entrant** la règle de synchronisation avec l’action de hello **configurer**. Qui indique que, tant que cet objet d’espace de connecteur est présent, objet de métaverse hello reste. Si la liste hello des règles de synchronisation affiche à la place une règle de synchronisation avec la direction **sortant** et **configurer**, il indique que cet objet est supprimé lors de l’objet de métaverse hello est supprimé.  
![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cslineageout.png)  
Vous pouvez également voir Bonjour **PasswordSync** colonne hello espace connecteur entrant peut contribuer à mot de passe toohello modifications, car une règle de synchronisation a la valeur de hello **True**. Ce mot de passe est ensuite envoyé tooAzure AD via la règle de trafic sortant hello.

À partir de l’onglet de lignage hello, vous pouvez obtenir toohello métaverse en cliquant sur [propriétés d’objet métaverse](#mv-attributes).

Au bas de hello de tous les onglets sont deux boutons : **aperçu** et **journal**.

### <a name="preview"></a>VERSION PRÉLIMINAIRE
page d’aperçu Hello est toosynchronize utilisé un seul objet. Il est utile si vous dépannez certaines règles de synchronisation et que vous souhaitez l’effet de hello toosee d’une modification sur un seul objet. Vous pouvez choisir entre **Synchronisation complète** et **Synchronisation delta**. Vous pouvez également choisir entre **générer l’aperçu**, qui conserve uniquement hello modification en mémoire, et **valider la version préliminaire**, qui hello métaverse de mise à jour et étapes toutes les modifications des espaces du connecteur tootarget.  
![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/preview.png)  
Vous pouvez inspecter les objets hello et la règle qui ont été appliqués pour un flux d’attribut particulier.  
![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/previewresult.png)

### <a name="log"></a>Journal
page du journal Hello est l’état de synchronisation de mot de passe utilisé toosee hello et l’historique. Pour plus d’informations, consultez [Résolution des problèmes de synchronisation de mot de passe](active-directory-aadconnectsync-troubleshoot-password-synchronization.md).

## <a name="metaverse-object-properties"></a>Propriétés de l’objet métaverse
Il est généralement préférable de toostart recherche à partir de la source de hello Active Directory [espace connecteur](#connector-space). Mais vous pouvez également démarrer la recherche à partir de hello métaverse.

### <a name="search-for-an-object-in-hello-mv"></a>Recherche d’un objet Bonjour MV
Dans **Synchronization Service Manager**, cliquez sur **Recherche de métaverse**. Créer une requête que vous connaissez recherche hello utilisateur. Vous pouvez rechercher des attributs communs, comme le nom de compte (sAMAccountName) et userPrincipalName. Pour plus d’informations, voir [Recherche de métaverses](active-directory-aadconnectsync-service-manager-ui-mvsearch.md).
![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/mvsearch.png)  

Bonjour **résultats de la recherche** fenêtre, cliquez sur l’objet hello.

Si vous ne trouvez pas l’objet de hello, puis il n’a pas encore atteint hello métaverse. Continuer toosearch pour l’objet de hello Bonjour Active Directory [espace connecteur](#connector-space-object-properties). Il peut y avoir une erreur de synchronisation qui bloque objet hello venir toohello métaverse ou il peut y avoir un filtre est appliqué.

### <a name="mv-attributes"></a>Attributs MV
Sous l’onglet attributs de hello, vous pouvez voir les valeurs hello et quel connecteur ont contribué à elle.  
![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/mvobject.png)  

Si un objet est not synchronizing, puis examinez hello suivant des attributs dans le métaverse de hello :
- Attribut de hello **cloudFiltered** présentes et définies trop**true**? Si elle est, il a été filtrée selon les étapes toohello dans [le filtrage par attribut](active-directory-aadconnectsync-configure-filtering.md#attribute-based-filtering).
- Attribut de hello **sourceAnchor** présent ? Si ce n’est pas le cas, utilisez-vous une topologie de forêt compte-ressource ? Si un objet est identifié comme une boîte aux lettres liée (attribut de hello **msExchRecipientTypeDetails** a la valeur de hello 2), puis hello sourceAnchor est obtenue par la forêt hello avec un compte Active Directory activé. Assurez-vous que le compte principal de hello a été importé et correctement synchronisée. compte de principal Hello doit être répertorié dans hello [connecteurs](#mv-connectors) pour l’objet de hello.

### <a name="mv-connectors"></a>Connecteurs MV
onglet de connecteurs Hello affiche tous les espaces de connecteur qui ont une représentation d’objet de hello.  
![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/mvconnectors.png)  
Vous devez disposer d’un connecteur pour :

- Chaque utilisateur hello de forêt Active Directory est représentée dans. Cette représentation peut inclure foreignSecurityPrincipals et les objets contact.
- Un connecteur dans Azure AD.

S’il manque des hello tooAzure de connecteur Active Directory, puis lire [les attributs MV](#MV-attributes) tooverify les critères de hello pour pouvoir être mis en service tooAzure AD.

Cet onglet vous permet également toonavigate toohello [objet espace connecteur](#connector-space-object-properties). Sélectionnez une ligne et cliquez sur **Propriétés**.

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur hello [synchronisation Azure AD Connect](active-directory-aadconnectsync-whatis.md) configuration.

En savoir plus sur l’ [intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).
