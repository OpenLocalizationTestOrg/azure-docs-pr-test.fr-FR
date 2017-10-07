---
title: "Synchronisation Azure AD Connect : gérer les erreurs LargeObject provoquées par l’attribut userCertificate | Microsoft Docs"
description: "Cette rubrique fournit des étapes de mise à jour hello pour les erreurs LargeObject provoquées par l’attribut userCertificate."
services: active-directory
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 146ad5b3-74d9-4a83-b9e8-0973a19828d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: e547fb5f601b92f6f5154de9997651b1f28c51b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-handling-largeobject-errors-caused-by-usercertificate-attribute"></a>Synchronisation Azure AD Connect : gérer les erreurs LargeObject provoquées par l’attribut userCertificate

Azure AD impose une limite maximale de **15** certificat valeurs hello **userCertificate** attribut. Si Azure AD Connect exporte un objet avec plus de 15 valeurs tooAzure AD, Azure AD renvoie un **LargeObject** erreur avec le message :

>*« objet approvisionné de hello est trop grande. Trim hello plusieurs valeurs d’attribut sur cet objet. Hello opération sera retentée Bonjour prochain cycle de synchronisation... »*

Hello LargeObject erreur peut provenir d’autres attributs Active Directory. tooconfirm il est en effet provoqué par attribut userCertificate de hello, vous devez tooverify par rapport à l’objet hello dans AD local ou Bonjour [recherche de métaverse Synchronization Service Manager](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-service-manager-ui-mvsearch).

liste de hello tooobtain d’objets dans votre locataire avec des erreurs de LargeObject, utilisez une des méthodes suivantes de hello :

 * Si votre client est activé pour Azure AD Connect Health pour la synchronisation, vous pouvez faire référence à toohello [rapport d’erreurs de synchronisation](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health-sync#object-level-synchronization-error-report-preview) fourni.
 
 * Hello courrier électronique de notification pour les erreurs de synchronisation d’annuaire qui est envoyé à la fin de hello de chaque cycle de synchronisation a liste hello d’objets avec des erreurs de LargeObject. 
 * Hello [onglet opérations du Gestionnaire de Service de synchronisation](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-service-manager-ui-operations) affiche la liste de hello des objets avec des erreurs de LargeObject si vous cliquez sur la dernière opération de tooAzure AD exportation hello.
 
## <a name="mitigation-options"></a>Options de correction
Jusqu'à la résolution de l’erreur de LargeObject hello, autres toohello de modifications d’attribut même objet ne peut pas être exportée tooAzure AD. Erreur de hello tooresolve, vous pouvez envisager de hello options suivantes :

 * Mise à niveau d’Azure AD Connect toobuild 1.1.524.0 ou après. Dans Azure AD Connect build 1.1.524.0, règles de synchronisation d’out-of-box hello ont été mis à jour toonot exportation attributs userCertificate et userSMIMECertificate si les attributs de hello ont des valeurs de plus de 15. Pour plus d’informations sur la façon de tooupgrade Azure AD Connect, consultez tooarticle [Azure AD Connect : mise à niveau à partir d’une précédente toohello de version plus récente](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-upgrade-previous-version).

 * Implémentez un **la règle de synchronisation sortants** dans Azure AD Connect qui exporte un **valeur au lieu des valeurs de réel hello pour les objets avec les valeurs des certificats plus de 15 null**. Cette option est appropriée si vous ne requièrent pas de hello certificat valeurs toobe exporté tooAzure AD pour les objets avec des valeurs de plus de 15. Pour plus d’informations sur la façon de tooimplement cette synchronisation de règle, consultez la section de toonext [exportation de toolimit de règle d’implémentation de la synchronisation de l’attribut userCertificate](#implementing-sync-rule-to-limit-export-of-usercertificate-attribute).

 * Réduire le nombre hello de valeurs de certificat sur hello localement l’objet Active Directory (15 ou moins) par la suppression des valeurs qui ne sont plus en cours d’utilisation par votre organisation. Ce choix convient si encombrement d’attribut hello est provoqué par les certificats expirés ou non utilisés. Vous pouvez utiliser hello [disponible ici de script PowerShell](https://gallery.technet.microsoft.com/Remove-Expired-Certificates-0517e34f) toohelp rechercher, sauvegarde et supprimer les certificats expirés dans votre site Active Directory. Avant de supprimer les certificats hello, il est recommandé de vérifier avec les administrateurs d’Infrastructure de clé publique hello dans votre organisation.

 * Configurer Azure AD Connect tooexclude hello userCertificate attribut qui est exporté tooAzure AD. En règle générale, nous déconseillons cette option comme attribut de hello peut être utilisé par les scénarios spécifiques de Microsoft Online Services tooenable. notamment :
    * l’attribut userCertificate Hello sur objet utilisateur de hello est utilisé par Exchange Online et les clients Outlook pour le chiffrement et la signature des messages. toolearn en savoir plus sur cette fonctionnalité, consultez tooarticle [S/MIME pour le chiffrement et la signature des messages](https://technet.microsoft.com/library/dn626158(v=exchg.150).aspx).

    * attribut userCertificate de Hello sur l’objet d’ordinateur hello est utilisé par les périphériques joints au domaine tooconnect tooAzure AD Azure AD tooallow Windows 10 sur site. toolearn en savoir plus sur cette fonctionnalité, consultez tooarticle [connecter tooAzure de périphériques joints au domaine Active Directory pour Windows 10 rencontre](https://docs.microsoft.com/azure/active-directory/active-directory-azureadjoin-devices-group-policy).

## <a name="implementing-sync-rule-toolimit-export-of-usercertificate-attribute"></a>Implémentation d’exportation de toolimit de règle de synchronisation de l’attribut userCertificate
Erreur de LargeObject hello tooresolve dû à l’attribut userCertificate de hello, vous pouvez implémenter une règle de synchronisation sortants dans Azure AD Connect qui exporte un **valeur au lieu des valeurs de réel hello pour les objets avec des valeurs de certificat plus de 15null**. Cette section décrit la règle de synchronisation hello hello étapes tooimplement requis pour **utilisateur** objets. Hello étapes peuvent être adaptés pour **Contact** et **ordinateur** objets.

> [!IMPORTANT]
> Exportation de valeur null supprime les valeurs précédemment exportée avec succès tooAzure AD de certificat.

étapes de Hello peuvent se résumer ainsi :

1. Désactiver le planificateur de synchronisation et vérifier qu'aucune synchronisation n’est en cours.
3. Trouver règle de synchronisation sortants hello existante pour l’attribut userCertificate.
4. Créer la règle de synchronisation sortants hello requise.
5. Vérifiez la nouvelle règle de synchronisation hello sur un objet existant avec l’erreur de LargeObject.
6. Appliquer hello nouvelle règle tooremaining objets synchronisation avec l’erreur de LargeObject.
7. Vérifiez aucune modification inattendue en attente toobe exporté tooAzure AD.
8. Exporter hello modifications tooAzure AD.
9. Réactiver le planificateur de synchronisation.

### <a name="step-1-disable-sync-scheduler-and-verify-there-is-no-synchronization-in-progress"></a>Étape 1. Désactiver le planificateur de synchronisation et vérifier qu'aucune synchronisation n’est en cours
Vérifiez aucune synchronisation n’a lieu lorsque vous vous trouvez au milieu de hello d’implémentation d’une nouvelle synchronisation tooavoid règle involontaire change étant exportés tooAzure AD. Planificateur de synchronisation intégré toodisable hello :
1. Démarrez la session PowerShell sur le serveur d’Azure AD Connect hello.

2. Désactivez la synchronisation planifiée en exécutant l’applet de commande : `Set-ADSyncScheduler -SyncCycleEnabled $false`

> [!Note]
> Hello étapes ci-dessus sont uniquement applicables toonewer versions (1.1.xxx.x) d’Azure AD Connect avec le Planificateur intégré de hello. Si vous utilisez des versions plus anciennes (1.0.xxx.x) d’Azure AD Connect qui utilise le Planificateur de tâches Windows, ou à l’aide de votre propre synchronisation périodique de tootrigger planificateur personnalisé (rare), vous devez toodisable les en conséquence.

3. Démarrer hello **Synchronization Service Manager** par → de tooSTART va Service de synchronisation.

4. Accédez toohello **Operations** onglet et confirmer aucune opération dont le statut est *« en cours. »*

### <a name="step-2-find-hello-existing-outbound-sync-rule-for-usercertificate-attribute"></a>Étape 2. Rechercher la règle de synchronisation sortants hello existante pour l’attribut userCertificate
Il doit y avoir une règle de synchronisation existant qui est activée et configuré l’attribut userCertificate tooexport tooAzure des objets utilisateur Active Directory. Recherchez ce toofind de règle de synchronisation à son **priorité** et **filtre d’étendue** configuration :

1. Démarrer hello **Éditeur des règles de synchronisation** par → de tooSTART va synchronisation éditeur de règles.

2. Configurer des filtres de recherche hello avec hello valeurs suivantes :

    | Attribut | Valeur |
    | --- | --- |
    | Direction |**Sortante** |
    | Type d'objet MV |**Person** |
    | Connecteur |*nom de votre connecteur Azure AD* |
    | Type d’objet de connecteur |**user** |
    | Attribut MV |**userCertificate** |

3. Si vous utilisez tooexport userCertficiate attribut du connecteur tooAzure AD OOB (out-of-box) synchronisation des règles pour les objets utilisateur, vous devez revenir hello *« sortie tooAAD – utilisateur ExchangeOnline »* règle.
4. Notez les hello **priorité** la valeur de cette règle de synchronisation.
5. Sélectionnez la règle de synchronisation hello et cliquez sur **modifier**.
6. Bonjour *« Modifier réservé Confirmation de règle »* boîte de dialogue contextuelle, cliquez sur **non**. (Ne vous inquiétez pas, nous n’allons pas toomake toute modification de la règle de synchronisation toothis).
7. Dans l’écran Modifier hello, sélectionnez hello **Scoping filter** onglet.
8. Notez hello l’étendue de configuration du filtre. Si vous utilisez la règle de synchronisation hello OOB, il doit exactement être **une portée filtre contenant deux clauses**, y compris :

    | Attribut | Opérateur  | Valeur |
    | --- | --- | --- |
    | sourceObjectType | EQUAL | Utilisateur |
    | cloudMastered | NOTEQUAL | true |

### <a name="step-3-create-hello-outbound-sync-rule-required"></a>Étape 3. Créer la règle de synchronisation sortants hello requise
Hello nouvelle règle de synchronisation doit avoir hello même **filtre d’étendue** et **une priorité plus élevée** que hello la règle de synchronisation existant. Cela garantit que hello nouvelle la règle de synchronisation s’applique toohello même ensemble d’objets en tant que la règle de synchronisation existant hello et la règle de synchronisation existant remplacements hello pour l’attribut userCertificate de hello. règle de synchronisation hello toocreate :
1. Bonjour Éditeur des règles de synchronisation, cliquez sur hello **ajouter une nouvelle règle** bouton.
2. Sous hello **onglet Description**, fournir hello configuration suivante :

    | Attribut | Valeur | Détails |
    | --- | --- | --- |
    | Nom | *Donnez-lui un nom* | Par exemple, *« Out tooAAD – personnalisé substitution pour userCertificate »* |
    | Description | *Fournissez une description* | Ex. *« Si l’attribut userCertificate comporte plus de 15 valeurs, exporter NULL »* |
    | Système connecté | *Sélectionnez hello connecteur Azure AD* |
    | Type d’objet système connecté | **user** | |
    | Type d’objet métaverse | **person** | |
    | Type de lien | **Join** | |
    | Precedence | *Choisissez un nombre compris entre 1 et 99* | Hello choisi nombre ne doit pas être utilisé par aucune règle de synchronisation existant et a une valeur inférieure (et par conséquent, une priorité plus élevée) que hello la règle de synchronisation existant. |

3. Accédez toohello **Scoping filter** onglet et implémenter hello à l’aide de la même portée filtre hello synchronisation règle existante.
4. Hello de Skip **règles de jointure** onglet.
5. Accédez toohello **Transformations** onglet tooadd une nouvelle transformation à l’aide après la configuration :

    | Attribut | Valeur |
    | --- | --- |
    | Type de flux |**Expression** |
    | Attribut cible |**userCertificate** |
    | Attribut source |*Hello Utilisez expression suivante*:`IIF(IsNullOrEmpty([userCertificate]), NULL, IIF((Count([userCertificate])> 15),AuthoritativeNull,[userCertificate]))` |
    
6. Cliquez sur hello **ajouter** la règle de synchronisation bouton toocreate hello.

### <a name="step-4-verify-hello-new-sync-rule-on-an-existing-object-with-largeobject-error"></a>Étape 4. Vérifiez que la nouvelle règle de synchronisation hello sur un objet existant avec l’erreur de LargeObject
Il s’agit de tooverify qui hello synchronisation règle créée fonctionne correctement sur un objet Active Directory existant avec l’erreur de LargeObject avant de l’appliquer tooother objets :
1. Accédez toohello **Operations** onglet Bonjour Synchronization Service Manager.
2. Sélectionnez l’opération tooAzure AD exportation plus récente hello et cliquez sur l’un des objets hello avec des erreurs de LargeObject.
3.  Dans l’écran contextuel de l’objet propriétés de l’espace connecteur hello, cliquez sur hello **aperçu** bouton.
4. Dans l’écran contextuel Aperçu de hello, sélectionnez **synchronisation complète** et cliquez sur **valider la version préliminaire**.
5. Fermez l’aperçu hello et l’écran de propriétés de l’objet espace connecteur hello.
6. Accédez toohello **connecteurs** onglet Bonjour Synchronization Service Manager.
7. Avec le bouton droit sur hello **Azure AD** connecteur, puis sélectionnez **exécuter...**
8. Dans le menu contextuel exécuter le connecteur de hello, sélectionnez **exporter** pas à pas, puis cliquez sur **OK**.
9. Attendez d’exportation tooAzure AD toocomplete et confirmer qu'aucune erreur n’est plus LargeObject sur cet objet.

### <a name="step-5-apply-hello-new-sync-rule-tooremaining-objects-with-largeobject-error"></a>Étape 5. Appliquer hello nouvelle règle tooremaining objets synchronisation avec l’erreur de LargeObject
Une fois que la règle de synchronisation hello a été ajoutée, vous devez toorun une étape de synchronisation complète sur hello Connecteur AD :
1. Accédez toohello **connecteurs** onglet Bonjour Synchronization Service Manager.
2. Avec le bouton droit sur hello **AD** connecteur, puis sélectionnez **exécuter...**
3. Dans le menu contextuel exécuter le connecteur de hello, sélectionnez **synchronisation complète** pas à pas, puis cliquez sur **OK**.
4. Attendez que hello synchronisation complète étape toocomplete.
5. Répétez hello étapes ci-dessus pour hello restant AD connecteurs si vous avez plusieurs connecteurs d’Active Directory. En règle générale, plusieurs connecteurs sont requis si vous avez plusieurs annuaires locaux.

### <a name="step-6-verify-there-are-no-unexpected-changes-waiting-toobe-exported-tooazure-ad"></a>Étape 6. Vérifiez aucune modification inattendue en attente toobe exporté tooAzure AD
1. Accédez toohello **connecteurs** onglet Bonjour Synchronization Service Manager.
2. Avec le bouton droit sur hello **Azure AD** connecteur, puis sélectionnez **espace de connecteur de recherche**.
3. Dans la fenêtre contextuelle de recherche d’espace connecteur hello :
    1. Définir l’étendue de trop**exporter en attente**.
    2. Cochez les trois cases : **Ajouter**, **Modifier** et **Supprimer**.
    3. Cliquez sur **recherche** tooreturn bouton tous les objets avec des modifications en attente toobe exporté tooAzure AD.
    4. Vérifiez l’absence de modification inattendue. modifications de hello tooexamine pour un objet donné, double-cliquez sur les objet hello.

### <a name="step-7-export-hello-changes-tooazure-ad"></a>Étape 7. Exportation hello modifications tooAzure AD
tooexport hello modifications tooAzure AD :
1. Accédez toohello **connecteurs** onglet Bonjour Synchronization Service Manager.
2. Avec le bouton droit sur hello **Azure AD** connecteur, puis sélectionnez **exécuter...**
4. Dans le menu contextuel exécuter le connecteur de hello, sélectionnez **exporter** pas à pas, puis cliquez sur **OK**.
5. Patientez exportation tooAzure AD toocomplete et confirmer qu'aucun message d’erreur LargeObject plus.

### <a name="step-8-re-enable-sync-scheduler"></a>Étape 8 : Réactiver le planificateur de synchronisation
Maintenant que hello est résolu, réactivez le Planificateur de synchronisation intégré hello :
1. Lancez une session PowerShell.
2. Réactivez la synchronisation planifiée en exécutant l’applet de commande : `Set-ADSyncScheduler -SyncCycleEnabled $true`

> [!Note]
> Hello étapes ci-dessus sont uniquement applicables toonewer versions (1.1.xxx.x) d’Azure AD Connect avec le Planificateur intégré de hello. Si vous utilisez des versions plus anciennes (1.0.xxx.x) d’Azure AD Connect qui utilise le Planificateur de tâches Windows, ou à l’aide de votre propre synchronisation périodique de tootrigger planificateur personnalisé (rare), vous devez toodisable les en conséquence.

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur l’ [intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).

