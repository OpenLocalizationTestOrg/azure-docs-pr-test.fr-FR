---
title: synchronisation de mot de passe aaaTroubleshoot avec synchronisation Azure AD Connect | Documents Microsoft
description: "Cet article fournit des informations sur la façon tootroubleshoot les problèmes de synchronisation de mot de passe."
services: active-directory
documentationcenter: 
author: AndKjell
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
ms.openlocfilehash: 390eafec792cb39251627c14cb754f8bb30035b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-password-synchronization-with-azure-ad-connect-sync"></a>Résolution des problèmes de synchronisation de mot de passe avec Azure AD Connect Sync
Cette rubrique explique comment tootroubleshoot problèmes avec la synchronisation de mot de passe. Si les mots de passe ne se synchronisent pas comme prévu, il peut s’agir d’un sous-ensemble d’utilisateurs ou de tous les utilisateurs. Pour Azure Active Directory (Azure AD) connecter le déploiement avec la version 1.1.524.0 ou une version ultérieure, il existe désormais une applet de commande de diagnostic que vous pouvez utiliser des problèmes de synchronisation de mot de passe tootroubleshoot :

* Si vous avez un problème dans lequel aucun des mots de passe ne sont synchronisés, consultez toohello [aucun mot de passe n’est synchronisés : résoudre les problèmes à l’aide d’applet de commande hello diagnostic](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet) section.

* Si vous avez un problème avec des objets individuels, consultez toohello [un objet ne synchronise pas les mots de passe : résoudre les problèmes à l’aide d’applet de commande hello diagnostic](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet) section.

Pour les versions antérieures de déploiement Azure AD Connect :

* Si vous avez un problème dans lequel aucun des mots de passe ne sont synchronisés, consultez toohello [aucun mot de passe n’est synchronisés : manuel des étapes de dépannage](#no-passwords-are-synchronized-manual-troubleshooting-steps) section.

* Si vous avez un problème avec des objets individuels, consultez toohello [un objet ne synchronise pas les mots de passe : manuel des étapes de dépannage](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps) section.

## <a name="no-passwords-are-synchronized-troubleshoot-by-using-hello-diagnostic-cmdlet"></a>Aucun mot de passe n’est synchronisés : résoudre les problèmes à l’aide d’applet de commande hello diagnostic
Vous pouvez utiliser hello `Invoke-ADSyncDiagnostics` toofigure d’applet de commande out pour lesquelles aucun mot de passe n’est synchronisés.

> [!NOTE]
> Hello `Invoke-ADSyncDiagnostics` applet de commande est uniquement disponible pour Azure AD Connect version 1.1.524.0 ou version ultérieure.

### <a name="run-hello-diagnostics-cmdlet"></a>Exécutez l’applet de commande hello diagnostics
problèmes tootroubleshoot où aucun mot de passe n’est synchronisés :

1. Ouvrez une nouvelle session Windows PowerShell sur votre serveur Azure AD Connect avec hello **exécuter en tant qu’administrateur** option.

2. Exécutez `Set-ExecutionPolicy RemoteSigned` ou `Set-ExecutionPolicy Unrestricted`.

3. Exécutez `Import-Module ADSyncDiagnostics`.

4. Exécutez `Invoke-ADSyncDiagnostics -PasswordSync`.

### <a name="understand-hello-results-of-hello-cmdlet"></a>Comprendre les résultats hello d’applet de commande hello
applet de commande Hello diagnostic exécute hello contrôles :

* Valide que hello fonctionnalité de synchronisation de mot de passe est activée pour votre locataire Azure AD.

* Valide que hello Azure AD Connect serveur n’est pas en mode de mise en lots.

* Pour chaque locales existantes connecteur Active Directory (ce qui correspond à la forêt Active Directory existant tooan) :

   * Valide que hello fonctionnalité de synchronisation de mot de passe est activée.
   
   * Les journaux d’événements d’Application de Windows recherche les événements de pulsation de synchronisation de mot de passe Bonjour.

   * Pour chaque domaine Active Directory sous le connecteur Active Directory hello local :

      * Valide que hello domaine est accessible à partir du serveur de connexion hello Azure AD.

      * Valide que les comptes de Services de domaine Active Directory (AD DS) hello utilisés par le connecteur Active Directory hello local a hello correct nom d’utilisateur, mot de passe et les autorisations requises pour la synchronisation de mot de passe.

Hello suivant schéma illustre les résultats de hello d’applet de commande hello pour une topologie de Active Directory de domaine unique, sur site :

![Sortie de diagnostic pour la synchronisation de mot de passe](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalgeneral.png)

Hello le reste de cette section décrit des résultats spécifiques qui sont retournées par l’applet de commande hello et les problèmes correspondants.

#### <a name="password-synchronization-feature-isnt-enabled"></a>La fonctionnalité de synchronisation de mot de passe n’est pas activée
Si vous n’avez pas activé la synchronisation de mot de passe à l’aide d’Assistant de hello Azure AD Connect, hello l’erreur suivante est retournée :

![La synchronisation de mot de passe n’est pas activée](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobaldisabled.png)

#### <a name="azure-ad-connect-server-is-in-staging-mode"></a>Le serveur Azure AD Connect est en mode intermédiaire
Si le serveur de Azure AD Connect de hello est en mode de préproduction, synchronisation de mot de passe est temporairement désactivée, et hello erreur suivante est retournée :

![Le serveur Azure AD Connect est en mode intermédiaire](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalstaging.png)

#### <a name="no-password-synchronization-heartbeat-events"></a>Aucun événement de pulsation de synchronisation de mot de passe
Chaque connecteur Active Directory local a son propre canal de synchronisation de mot de passe. Lorsque le canal de synchronisation de mot de passe hello est établie et il n’existe pas de n’importe quel toobe de modifications de mot de passe synchronisé, un événement de pulsation (ID d’événement 654) est généré une fois toutes les 30 minutes sous hello journal des événements Windows. Pour chaque connecteur Active Directory local, hello applet de commande recherche les événements de pulsation correspondants dans hello les trois dernières heures. Si aucun événement de pulsation n’est trouvée, hello erreur suivante est retournée :

![Aucun événement de pulsation de synchronisation de mot de passe](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalnoheartbeat.png)

#### <a name="ad-ds-account-does-not-have-correct-permissions"></a>Le compte AD DS n’a pas les autorisations appropriées
Si le compte hello AD DS qui est utilisé par hello local hachages de mot de passe de toosynchronize de connecteur Active Directory n’a pas les autorisations appropriées hello, hello erreur suivante est retournée :

![Informations d’identification incorrectes](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectpermission.png)

#### <a name="incorrect-ad-ds-account-username-or-password"></a>Nom d’utilisateur ou mot de passe du compte AD DS incorrect
Si hello AD DS le compte utilisé par hello hachages de mot de passe local Active Directory connector toosynchronize dispose d’un nom d’utilisateur incorrect ou le mot de passe, hello erreur suivante est retournée :

![Informations d’identification incorrectes](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectcredential.png)

## <a name="one-object-is-not-synchronizing-passwords-troubleshoot-by-using-hello-diagnostic-cmdlet"></a>Un objet ne synchronise pas les mots de passe : résoudre les problèmes à l’aide d’applet de commande hello diagnostic
Vous pouvez utiliser hello `Invoke-ADSyncDiagnostics` toodetermine d’applet de commande pourquoi un objet ne synchronise pas les mots de passe.

> [!NOTE]
> Hello `Invoke-ADSyncDiagnostics` applet de commande est uniquement disponible pour Azure AD Connect version 1.1.524.0 ou version ultérieure.

### <a name="run-hello-diagnostics-cmdlet"></a>Exécutez l’applet de commande hello diagnostics
problèmes tootroubleshoot où aucun mot de passe n’est synchronisés :

1. Ouvrez une nouvelle session Windows PowerShell sur votre serveur Azure AD Connect avec hello **exécuter en tant qu’administrateur** option.

2. Exécutez `Set-ExecutionPolicy RemoteSigned` ou `Set-ExecutionPolicy Unrestricted`.

3. Exécutez `Import-Module ADSyncDiagnostics`.

4. Exécutez hello suivant l’applet de commande :
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName <Name-of-AD-Connector> -DistinguishedName <DistinguishedName-of-AD-object>
   ```
   Par exemple :
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName "contoso.com" -DistinguishedName "CN=TestUserCN=Users,DC=contoso,DC=com"
   ```

### <a name="understand-hello-results-of-hello-cmdlet"></a>Comprendre les résultats hello d’applet de commande hello
applet de commande Hello diagnostic exécute hello contrôles :

* Examine l’état hello d’objet Active Directory de hello dans l’espace de connecteur Active Directory hello métaverse et Azure espace de connecteur Active Directory.

* Vérifie qu’il n’y a des règles de synchronisation avec la synchronisation de mot de passe activée et appliquer l’objet d’Active Directory toohello.

* Tente de tooretrieve et l’affichage des résultats hello hello dernière tentative toosynchronize hello mot de passe pour l’objet de hello.

Hello suivant schéma illustre les résultats de hello d’applet de commande hello lors de la résolution des problèmes de synchronisation de mot de passe pour un seul objet :

![Sortie de diagnostic pour la synchronisation de mot de passe - objet unique](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectgeneral.png)

Hello le reste de cette section décrit des résultats spécifiques retournés par l’applet de commande hello et les problèmes correspondants.

#### <a name="hello-active-directory-object-isnt-exported-tooazure-ad"></a>objet d’Active Directory Hello n’est pas exporté tooAzure AD
Synchronisation de mot de passe pour ce compte d’Active Directory local échoue, car il n’existe aucun objet correspondant dans le locataire Azure AD de hello. Hello, l’erreur suivante est retournée :

![Objet Azure Active Directory manquant](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnotexported.png)

#### <a name="user-has-a-temporary-password"></a>L’utilisateur a un mot de passe temporaire
Actuellement, Azure AD Connect ne prend pas en charge la synchronisation des mots de passe temporaires avec Azure AD. Un mot de passe est considéré comme toobe temporaire si hello **modification de mot de passe à la prochaine ouverture de session** option est définie sur l’utilisateur de Active Directory local hello. Hello, l’erreur suivante est retournée :

![Le mot de passe temporaire n’est pas exporté](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjecttemporarypassword.png)

#### <a name="results-of-last-attempt-toosynchronize-password-arent-available"></a>Résultats de la dernière tentative de toosynchronize un mot de passe ne sont pas disponibles
Par défaut, Azure AD Connect stocke les résultats de hello de tentatives de synchronisation de mot de passe pendant sept jours. Si aucun résultat n’est disponible pour l’objet d’Active Directory hello sélectionné, hello suivant l’avertissement est retourné :

![Sortie de diagnostic pour un seul objet - aucun historique de synchronisation de mot de passe](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnohistory.png)


## <a name="no-passwords-are-synchronized-manual-troubleshooting-steps"></a>Aucun mot de passe n’est synchronisé : étapes de dépannage manuel
Suivez ces toodetermine étapes pour lesquelles aucun mot de passe n’est synchronisés :

1. Serveur de se connecter hello dans [mode de préproduction](active-directory-aadconnectsync-operations.md#staging-mode)? Un serveur en mode intermédiaire ne synchronise pas les mots de passe.

2. Exécutez le script de hello dans hello [obtenir l’état de hello de paramètres de synchronisation de mot de passe](#get-the-status-of-password-sync-settings) section. Il vous donne une vue d’ensemble de la configuration de la synchronisation de mot de passe hello.  

    ![Sortie de script PowerShell à partir des paramètres de synchronisation de mot de passe](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/psverifyconfig.png)  

3. Si la fonctionnalité de hello n’est pas activée dans Azure AD, ou si l’état de canal de synchronisation hello n’est pas activé, exécuter l’Assistant installation de se connecter hello. Sélectionnez **Personnaliser les options de synchronisation** et désélectionnez la synchronisation de mot de passe. Cette modification désactive temporairement la fonctionnalité de hello. Ensuite, réexécutez hello et réactiver la synchronisation de mot de passe. Exécutez le script de hello nouveau tooverify qui hello configuration est correcte.

4. Recherchez dans le journal des événements hello pour les erreurs. Recherchez hello suivant des événements, qui indiquent un problème :
    * Source : « Synchronisation d’annuaires » ID : 0, 611, 652, 655 Si vous voyez ces événements, vous avez un problème de connectivité. message du journal des événements Hello contient des informations de forêt où vous avez un problème. Pour plus d’informations, consultez [Problème de connectivité](#connectivity problem).

5. Si vous ne voyez aucune pulsation ou que rien d’autre n’a fonctionné, exécutez [Déclencher une synchronisation complète de tous les mots de passe](#trigger-a-full-sync-of-all-passwords). Exécutez le script de hello qu’une seule fois.

6. Consultez hello [résoudre les problèmes d’un objet qui ne se synchronise pas les mots de passe](#one-object-is-not-synchronizing-passwords) section.

### <a name="connectivity-problems"></a>Problèmes de connectivité

Avez-vous une connectivité avec Azure AD ?

Compte de hello ont requis des hachages de mot de passe autorisations tooread hello dans tous les domaines ? Si vous avez installé de se connecter à l’aide de paramètres Express, hello autorisations doivent déjà être correctes. 

Si vous avez utilisé une installation personnalisée, définir des autorisations de hello manuellement en procédant comme suit de hello :
    
1. compte de hello toofind utilisé par le connecteur Active Directory de hello, début **Synchronization Service Manager**. 
 
2. Accédez trop**connecteurs**, puis recherchez forêt Active Directory de hello local vous dépannez. 
 
3. Sélectionnez hello connecteur, puis cliquez sur **propriétés**. 
 
4. Accédez trop**connecter tooActive Directory forêt**.  
    
    ![Compte utilisé par le connecteur Active Directory](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/connectoraccount.png)  
    Notez le nom d’utilisateur hello et domaine hello où se trouve le compte de hello.
    
5. Démarrer **Active Directory Users and Computers**, puis vérifiez que compte hello trouvés précédemment dispose des autorisations de suivi hello définie au niveau racine hello de tous les domaines de votre forêt :
    * Répliquer les changements d’annuaires
    * Répliquer les changements d’annuaire Tout

6. Est des contrôleurs de domaine est accessibles par Azure AD Connect hello ? Si le serveur de se connecter de hello ne peut pas se connecter à des contrôleurs de domaine tooall, configurez **uniquement utiliser le contrôleur de domaine par défaut**.  
    
    ![Contrôleur de domaine utilisé par le connecteur Active Directory](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/preferreddc.png)  
    
7. Revenir en arrière trop**Synchronization Service Manager** et **configurer la Partition de répertoire**. 
 
8. Sélectionnez votre domaine dans **sélectionner les partitions d’annuaire**, sélectionnez hello **utiliser uniquement les contrôleurs de domaine par défaut** case à cocher, puis cliquez sur **configurer**. 

9. Dans la liste hello, entrez les contrôleurs de domaine hello que connexion doit utiliser pour la synchronisation de mot de passe. Hello même liste est utilisée pour importer et exporter également. Effectuez ces étapes pour tous vos domaines.

10. Si le script de hello montre qu’il n’y a aucune pulsation, exécutez le script de hello [déclencher une synchronisation complète de tous les mots de passe](#trigger-a-full-sync-of-all-passwords).

## <a name="one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps"></a>Un objet ne synchronise pas les mots de passe : étapes de dépannage manuel
Vous pouvez facilement résoudre les problèmes de synchronisation de mot de passe en consultant l’état hello d’un objet.

1. Dans **Active Directory Users and Computers**, recherchez hello utilisateur, puis vérifiez que hello **utilisateur doit changer de mot de passe à la prochaine ouverture de session** case à cocher est désactivée.  

    ![Mots de passe productifs Active Directory](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/adprodpassword.png)  

    Si la case à cocher hello est sélectionné, poser toosign d’utilisateur hello dans et modifier le mot de passe hello. Les mots de passe temporaires ne sont pas synchronisés avec Azure AD.

2. Si le mot de passe hello est correct dans Active Directory, procédez comme utilisateur hello dans le moteur de synchronisation hello. Par utilisateur hello suivant à partir de tooAzure d’Active Directory sur site Active Directory, vous pouvez voir s’il existe une erreur descriptive sur l’objet de hello.

    a. Démarrer hello [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md).

    b. Cliquez sur **Connecteurs**.

    c. Sélectionnez hello **connecteur Active Directory** où se trouve hello utilisateur.

    d. Sélectionnez **Search Connector Space**(Rechercher l’espace de connecteur).

    e. Bonjour **étendue** boîte, sélectionnez **DN ou ancre**, puis entrez le nom unique complet de hello d’utilisateur hello vous dépannez.

    ![Rechercher un utilisateur dans l’espace de connecteur avec le nom unique](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/searchcs.png)  

    f. Recherchez l’utilisateur hello vous recherchez, puis cliquez sur **propriétés** toosee tous hello d’attributs. Si l’utilisateur de hello n’est pas dans le résultat de la recherche hello, vérifiez votre [règles de filtrage](active-directory-aadconnectsync-configure-filtering.md) et vérifiez que vous exécutez [appliquer et vérifier les modifications](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) pour tooappear d’utilisateur hello dans se connecter.

    g. Cliquez sur la semaine dernière, détails de synchronisation de mot de passe de hello toosee d’objet hello pour hello **journal**.  

    ![Détails d’un journal d’objet](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/csobjectlog.png)  

    Si le journal d’objet hello est vide, Azure AD Connect a été le hachage de mot de passe hello tooread impossible à partir d’Active Directory. Continuez la résolution des problèmes avec [Erreurs de connectivité](#connectivity-errors). Si vous voyez une valeur autre que **réussite**, consultez la table toohello dans [journal de synchronisation de mot de passe](#password-sync-log).

    h. Sélectionnez hello **lignage** onglet et vérifiez que cette règle de synchronisation au moins un Bonjour **PasswordSync** colonne est **True**. Dans la configuration par défaut de hello, nom hello de la règle de synchronisation hello est **dans depuis AD - utilisateur AccountEnabled**.  

    ![Informations de lignage sur un utilisateur](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync.png)  

    i. Cliquez sur **propriétés d’objet métaverse** toodisplay une liste d’attributs de l’utilisateur.  

    ![Informations de métaverse](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvpasswordsync.png)  

    Vérifiez qu’aucun attribut **cloudFiltered** n’est présent. Assurez-vous que les attributs de domaine hello (domainFQDN et domainNetBios) ont des valeurs attendues de hello.

    j. Cliquez sur hello **connecteurs** onglet. Assurez-vous que les connecteurs tooboth locale Active Directory et Azure AD.

    ![Informations de métaverse](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvconnectors.png)  

    k. Sélectionnez hello ligne représentant Azure AD, cliquez sur **propriétés**, puis cliquez sur hello **lignage** objet d’espace connecteur onglet hello doit avoir une règle sortante Bonjour **PasswordSync** jeu de colonnes trop**True**. Dans la configuration par défaut de hello, nom hello de la règle de synchronisation hello est **hors tooAAD - jointure utilisateur**.  

    ![Boîte de dialogue Propriétés de l’objet espace connecteur](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync2.png)  

### <a name="password-sync-log"></a>Journal de synchronisation de mot de passe
colonne d’état Hello peut avoir hello valeurs suivantes :

| État | Description |
| --- | --- |
| Succès |Le mot de passe a été correctement synchronisé. |
| FilteredByTarget |Mot de passe est défini trop**utilisateur doit changer de mot de passe à la prochaine ouverture de session**. Mot de passe n'a pas été synchronisé. |
| NoTargetConnection |Aucun objet de métaverse de hello ou dans l’espace de connecteur hello Azure AD. |
| SourceConnectorNotPresent |Aucun objet trouvé dans l’espace de connecteur Active Directory hello localement. |
| TargetNotExportedToDirectory |objet Hello Bonjour espace du connecteur Azure AD n’a pas été exporté. |
| MigratedCheckDetailsForMoreInfo |L'entrée de journal a été créée avant la version 1.0.9125.0 et est affichée dans son état hérité. |
| Error |Le service a renvoyé une erreur inconnue. |
| Unknown |Une erreur s’est produite lors de la tentative de tooprocess un lot de hachages de mot de passe.  |
| MissingAttribute |Des attributs spécifiques (par exemple, le hachage Kerberos) requis par Azure AD Domain Services ne sont pas disponibles. |
| RetryRequestedByTarget |Des attributs spécifiques (par exemple, le hachage Kerberos) requis par Azure AD Domain Services n’étaient pas disponibles précédemment. Hachage de mot de passe d’une tentative de tooresynchronize hello utilisateur est établie. |

## <a name="scripts-toohelp-troubleshooting"></a>Dépannage de scripts toohelp

### <a name="get-hello-status-of-password-sync-settings"></a>Obtenir l’état de hello de paramètres de synchronisation de mot de passe
```
Import-Module ADSync
$connectors = Get-ADSyncConnector
$aadConnectors = $connectors | Where-Object {$_.SubType -eq "Windows Azure Active Directory (Microsoft)"}
$adConnectors = $connectors | Where-Object {$_.ConnectorTypeName -eq "AD"}
if ($aadConnectors -ne $null -and $adConnectors -ne $null)
{
    if ($aadConnectors.Count -eq 1)
    {
        $features = Get-ADSyncAADCompanyFeature -ConnectorName $aadConnectors[0].Name
        Write-Host
        Write-Host "Password sync feature enabled in your Azure AD directory: "  $features.PasswordHashSync
        foreach ($adConnector in $adConnectors)
        {
            Write-Host
            Write-Host "Password sync channel status BEGIN ------------------------------------------------------- "
            Write-Host
            Get-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector.Name
            Write-Host
            $pingEvents =
                Get-EventLog -LogName "Application" -Source "Directory Synchronization" -InstanceId 654  -After (Get-Date).AddHours(-3) |
                    Where-Object { $_.Message.ToUpperInvariant().Contains($adConnector.Identifier.ToString("D").ToUpperInvariant()) } |
                    Sort-Object { $_.Time } -Descending
            if ($pingEvents -ne $null)
            {
                Write-Host "Latest heart beat event (within last 3 hours). Time " $pingEvents[0].TimeWritten
            }
            else
            {
                Write-Warning "No ping event found within last 3 hours."
            }
            Write-Host
            Write-Host "Password sync channel status END ------------------------------------------------------- "
            Write-Host
        }
    }
    else
    {
        Write-Warning "More than one Azure AD Connectors found. Please update hello script toouse hello appropriate Connector."
    }
}
Write-Host
if ($aadConnectors -eq $null)
{
    Write-Warning "No Azure AD Connector was found."
}
if ($adConnectors -eq $null)
{
    Write-Warning "No AD DS Connector was found."
}
Write-Host
```

#### <a name="trigger-a-full-sync-of-all-passwords"></a>Déclencher une synchronisation complète de tous les mots de passe
> [!NOTE]
> Exécutez ce script une seule fois. Si vous devez toorun il plusieurs fois, problème est ailleurs hello. problème de hello tootroubleshoot, contactez le support technique Microsoft.

Vous pouvez déclencher une synchronisation complète de tous les mots de passe à l’aide de hello script suivant :

```
$adConnector = "<CASE SENSITIVE AD CONNECTOR NAME>"
$aadConnector = "<CASE SENSITIVE AAD CONNECTOR NAME>"
Import-Module adsync
$c = Get-ADSyncConnector -Name $adConnector
$p = New-Object Microsoft.IdentityManagement.PowerShell.ObjectModel.ConfigurationParameter "Microsoft.Synchronize.ForceFullPasswordSync", String, ConnectorGlobal, $null, $null, $null
$p.Value = 1
$c.GlobalParameters.Remove($p.Name)
$c.GlobalParameters.Add($p)
$c = Add-ADSyncConnector -Connector $c
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $false
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $true
```

## <a name="next-steps"></a>Étapes suivantes
* [Implémentation de la synchronisation de mot de passe avec Azure AD Connect Sync](active-directory-aadconnectsync-implement-password-synchronization.md)
* [Azure AD Connect Sync : Personnalisation des options de synchronisation](active-directory-aadconnectsync-whatis.md)
* [Intégration des identités locales dans Azure Active Directory](active-directory-aadconnect.md)
