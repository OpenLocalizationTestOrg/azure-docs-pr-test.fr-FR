---
title: "Azure AD Connect sync : tâches et examen opérationnels | Microsoft Docs"
description: "Cette rubrique décrit les tâches opérationnelles pour la synchronisation Azure AD Connect et comment tooprepare pour l’exploitation de ce composant."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: b29c1790-37a3-470f-ab69-3cee824d220d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: e6b21262e0924785808888d66f08a04a56581edc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-operational-tasks-and-consideration"></a>Azure Connect AD sync : tâches opérationnelles et examen
objectif Hello de cette rubrique est toodescribe des tâches opérationnelles pour la synchronisation Azure AD Connect.

## <a name="staging-mode"></a>Mode intermédiaire
Le mode intermédiaire peut être utilisé dans le cadre de plusieurs scénarios, notamment :

* Haute disponibilité :
* Tester et déployer de nouvelles modifications de configuration.
* Introduire un nouveau serveur et retirer hello ancien.

Avec un serveur en mode de préproduction, vous pouvez modifier modifications toohello configuration et l’aperçu hello avant d’apporter les serveur hello active. Il vous permet également de l’importation intégrale toorun et tooverify de synchronisation complète que toutes les modifications sont censées avant d’apporter ces modifications dans votre environnement de production.

Pendant l’installation, vous pouvez sélectionner toobe de serveur hello dans **mode de préproduction**. Cette action permet de serveur de hello active pour l’importation et synchronisation, mais il ne s’exécute pas des exportations. Un serveur en mode intermédiaire n’exécute pas la synchronisation de mot de passe et l’écriture différée de mot de passe même si vous avez sélectionné ces fonctions au cours de l’installation. Lorsque vous désactivez le mode de préproduction, hello server lance l’exportation, permet la synchronisation de mot de passe et l’écriture différée de mot de passe.

Vous pouvez toujours forcer une exportation à l’aide du Gestionnaire de service de synchronisation hello.

Un serveur en mode de mise en lots continue tooreceive des modifications à partir d’Active Directory et Azure AD. Il a toujours une copie des modifications les plus récentes hello et peuvent durer de très rapide sur les responsabilités hello d’un autre serveur. Si vous effectuez le serveur principal de configuration modifications tooyour, il est toomake de votre responsabilité hello même serveur toohello de modifications dans le mode de mise en lots.

Pour ceux avec des connaissances des technologies plus anciennes de synchronisation, hello en mode de mise en lots est différent, car le serveur de hello possède sa propre base de données SQL. Cette architecture permet hello mode toobe de serveur situé dans un autre centre de données de mise en lots.

### <a name="verify-hello-configuration-of-a-server"></a>Vérifier la configuration d’un serveur de hello
tooapply cette méthode, procédez comme suit :

1. [Préparation](#prepare)
2. [Configuration](#configuration)
3. [Importer et synchroniser](#import-and-synchronize)
4. [Vérifier](#verify)
5. [Changer de serveur actif](#switch-active-server)

#### <a name="prepare"></a>Préparation
1. Installer Azure AD Connect, sélectionnez **mode de préproduction**et désélectionnez **démarrer la synchronisation** sur hello dernière page de l’Assistant installation hello. Ce mode vous permet de moteur de synchronisation hello toorun manuellement.
   ![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)
2. Connexion hors tension et à la connexion et à partir de hello démarrer menu, sélectionnez **Service de synchronisation**.

#### <a name="configuration"></a>Configuration
Si vous avez apporté des modifications personnalisées toohello principal configuration du serveur et que vous souhaitez toocompare hello avec hello serveur intermédiaire, puis utilisez [documentation de configuration Azure AD Connect](https://github.com/Microsoft/AADConnectConfigDocumenter).

#### <a name="import-and-synchronize"></a>Importer et synchroniser
1. Sélectionnez **connecteurs**, et sélectionnez hello premier connecteur avec type de hello **les Services de domaine Active Directory**. Cliquez sur **Exécuter**, sélectionnez **Importation intégrale**, puis **OK**. Répétez cette procédure pour tous les connecteurs de ce type.
2. Sélectionnez hello connecteur avec type **Azure Active Directory (Microsoft)**. Cliquez sur **Exécuter**, sélectionnez **Importation intégrale**, puis **OK**.
3. Assurez-vous que l’onglet hello connecteurs est toujours sélectionné. Pour chaque connecteur de type **Services de domaine Active Directory**, cliquez sur **Exécuter**, sélectionnez **Synchronisation Delta**, puis **OK**.
4. Sélectionnez hello connecteur avec type **Azure Active Directory (Microsoft)**. Cliquez sur **Exécuter**, sélectionnez **Synchronisation Delta**, puis **OK**.

Vous avez maintenant une exportation intermédiaire change tooAzure AD et AD local (si vous utilisez un déploiement Exchange hybride). les étapes suivantes Hello autoriser tooinspect Nouveautés sur toochange avant de commencer réellement hello exporter toohello les répertoires.

#### <a name="verify"></a>Vérifier
1. Démarrez une invite de commandes et accédez trop`%ProgramFiles%\Microsoft Azure AD Sync\bin`
2. Ensuite, exécutez : `csexport "Name of Connector" %temp%\export.xml /f:x` nom hello Hello connecteur sont accessibles dans le Service de synchronisation. Il a un too"contoso.com similaire nom – AAD » pour Azure AD.
3. Copiez le script PowerShell de hello à partir de la section de hello [CSAnalyzer](#appendix-csanalyzer) fichier tooa nommé `csanalyzer.ps1`.
4. Ouvrez une fenêtre PowerShell et parcourir le dossier toohello où vous avez créé le script PowerShell de hello.
5. Exécutez : `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`.
6. Vous disposez maintenant d’un fichier nommé **processedusers1.csv** qui peut être examiné dans Microsoft Excel. Toutes les modifications intermédiaires de toobe exporté tooAzure AD se trouvent dans ce fichier.
7. Apportez les modifications nécessaires des données de toohello ou configuration et exécuter ces étapes à nouveau (importation et synchronisation et vérifiez) jusqu'à ce que hello modifications concernent toobe exportée sont attendus.

#### <a name="switch-active-server"></a>Changer de serveur actif
1. Sur le serveur actif de hello, désactivez le serveur hello (DirSync/FIM/Azure AD Sync) afin qu’il n’exporte pas tooAzure AD ou la définir dans le mode (Azure AD Connect) de mise en lots.
2. Exécuter l’Assistant installation hello sur serveur hello **mode de préproduction** et désactiver **mode de préproduction**.
   ![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)

## <a name="disaster-recovery"></a>Récupération d'urgence
Partie de la conception de l’implémentation hello est tooplan pour le toodo en cas de sinistre dans lequel vous perdez le serveur de synchronisation hello. Il existe différents modèles toouse et l’un toouse dépend de plusieurs facteurs, notamment :

* Quelle est votre tolérance des modifications n’est ne pas en mesure de créer de tooobjects dans Azure AD au cours du temps d’arrêt hello ?
* Si vous utilisez la synchronisation de mot de passe, procédez comme hello les utilisateurs accepter que toouse hello ancien mot de passe dans Azure AD dans le cas où ils modifier localement ?
* Avez-vous une dépendance par rapport aux opérations en temps réel, notamment l’écriture différée de mot de passe ?

En fonction des questions de toothese réponses hello et la stratégie de votre organisation, un des hello suivant des stratégies peut être implémenté :

* Régénérer si nécessaire.
* Disposer d'un serveur de secours en attente, appelé **mode intermédiaire**.
* Utiliser les machines virtuelles.

Si vous n’utilisez pas hello intégrée SQL Express de base de données, vous devez également examiner hello [haute disponibilité SQL](#sql-high-availability) section.

### <a name="rebuild-when-needed"></a>Régénérer lorsque nécessaire
Une stratégie viable consiste tooplan une reconstruction du serveur si nécessaire. En règle générale, l’installation de hello du moteur de synchronisation et de hello importation initiale et la synchronisation peut être effectuée en quelques heures. S’il n’est pas un serveur de rechange disponibles, il est possible tootemporarily un moteur de synchronisation de domaine contrôleur toohost hello.

serveur du moteur de synchronisation Hello ne stocke pas d’état sur les objets de hello afin de la base de données hello peut être reconstruit à partir des données hello dans Active Directory et Azure AD. Hello **sourceAnchor** l’attribut est utilisé toojoin hello des objets du site et hello cloud. Si vous régénérez hello du serveur avec les objets locale existante et hello cloud, puis le moteur de synchronisation hello correspond à ces objets ensemble à nouveau sur la réinstallation. éléments Hello vous devez toodocument et enregistrez les modifications de configuration de hello apportées serveur toohello, tels que les règles de filtrage et de synchronisation sont. Ces configurations personnalisées doivent être réappliquées avant de commencer la synchronisation.

### <a name="have-a-spare-standby-server---staging-mode"></a>Disposer d’un serveur de secours en attente, connu sous le nom de mode intermédiaire.
Si vous disposez d’un environnement plus complexe, il est recommandé d’avoir un ou plusieurs serveurs de secours. Pendant l’installation, vous pouvez activer une toobe de serveur dans **mode de préproduction**.

Pour en savoir plus, voir [Mode intermédiaire](#staging-mode).

### <a name="use-virtual-machines"></a>Utiliser les machines virtuelles
Une méthode courante et prises en charge est le moteur de synchronisation toorun hello dans une machine virtuelle. Au cas où l’hôte de hello a un problème, image hello avec le serveur du moteur de synchronisation hello peut être migré tooanother server.

### <a name="sql-high-availability"></a>Haute disponibilité SQL
Si vous n’utilisez pas hello SQL Server Express qui est fourni avec Azure AD Connect, haute disponibilité pour SQL Server doit également à envisager. solutions de haute disponibilité Hello pris en charge incluent AOA (groupes de disponibilité AlwaysOn) et gestion de clusters SQL. Les solutions non prises en charge incluent la mise en miroir.

Une prise en charge pour SQL AOA tooAzure AD Connect version 1.1.524.0. Vous devez activer SQL AOA avant d’installer Azure AD Connect. Pendant l’installation, Azure AD Connect détecte si instance SQL de hello fournie est activée pour SQL AOA ou non. Si SQL AOA est activée, Azure AD Connect davantage détermine si SQL AOA est toouse configuré une réplication synchrone ou asynchrone. Lorsque vous configurez hello écouteur du groupe de disponibilité, il est recommandé de définir hello RegisterAllProvidersIP propriété too0. Il s’agit, car Azure AD Connect utilise actuellement SQL Native Client tooconnect tooSQL et SQL Native Client ne prend pas en charge hello propriété MultiSubNetFailover.

## <a name="appendix-csanalyzer"></a>Annexe CSAnalyzer
Consultez la section de hello [vérifier](#verify) sur la façon de toouse ce script.

```
Param(
    [Parameter(Mandatory=$true, HelpMessage="Must be a file generated using csexport 'Name of Connector' export.xml /f:x)")]
    [string]$xmltoimport="%temp%\exportedStage1a.xml",
    [Parameter(Mandatory=$false, HelpMessage="Maximum number of users per output file")][int]$batchsize=1000,
    [Parameter(Mandatory=$false, HelpMessage="Show console output")][bool]$showOutput=$false
)

#LINQ isn't loaded automatically, so force it
[Reflection.Assembly]::Load("System.Xml.Linq, Version=3.5.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089") | Out-Null

[int]$count=1
[int]$outputfilecount=1
[array]$objOutputUsers=@()

#XML must be generated using "csexport "Name of Connector" export.xml /f:x"
write-host "Importing XML" -ForegroundColor Yellow

#XmlReader.Create won't properly resolve hello file location,
#so expand and then resolve it
$resolvedXMLtoimport=Resolve-Path -Path ([Environment]::ExpandEnvironmentVariables($xmltoimport))

#use an XmlReader toodeal with even large files
$result=$reader = [System.Xml.XmlReader]::Create($resolvedXMLtoimport) 
$result=$reader.ReadToDescendant('cs-object')
do 
{
    #create hello object placeholder
    #adding them up here means we can enforce consistency
    $objOutputUser=New-Object psobject
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name ID -Value ""
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name Type -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name DN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name operation -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name UPN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name displayName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name sourceAnchor -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name alias -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name primarySMTP -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name onPremisesSamAccountName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name mail -Value ""

    $user = [System.Xml.Linq.XElement]::ReadFrom($reader)
    if ($showOutput) {Write-Host Found an exported object... -ForegroundColor Green}

    #object id
    $outID=$user.Attribute('id').Value
    if ($showOutput) {Write-Host ID: $outID}
    $objOutputUser.ID=$outID

    #object type
    $outType=$user.Attribute('object-type').Value
    if ($showOutput) {Write-Host Type: $outType}
    $objOutputUser.Type=$outType

    #dn
    $outDN= $user.Element('unapplied-export').Element('delta').Attribute('dn').Value
    if ($showOutput) {Write-Host DN: $outDN}
    $objOutputUser.DN=$outDN

    #operation
    $outOperation= $user.Element('unapplied-export').Element('delta').Attribute('operation').Value
    if ($showOutput) {Write-Host Operation: $outOperation}
    $objOutputUser.operation=$outOperation

    #now that we have hello basics, go get hello details

    foreach ($attr in $user.Element('unapplied-export-hologram').Element('entry').Elements("attr"))
    {
        $attrvalue=$attr.Attribute('name').Value
        $internalvalue= $attr.Element('value').Value

        switch ($attrvalue)
        {
            "userPrincipalName"
            {
                if ($showOutput) {Write-Host UPN: $internalvalue}
                $objOutputUser.UPN=$internalvalue
            }
            "displayName"
            {
                if ($showOutput) {Write-Host displayName: $internalvalue}
                $objOutputUser.displayName=$internalvalue
            }
            "sourceAnchor"
            {
                if ($showOutput) {Write-Host sourceAnchor: $internalvalue}
                $objOutputUser.sourceAnchor=$internalvalue
            }
            "alias"
            {
                if ($showOutput) {Write-Host alias: $internalvalue}
                $objOutputUser.alias=$internalvalue
            }
            "proxyAddresses"
            {
                if ($showOutput) {Write-Host primarySMTP: ($internalvalue -replace "SMTP:","")}
                $objOutputUser.primarySMTP=$internalvalue -replace "SMTP:",""
            }
        }
    }

    $objOutputUsers += $objOutputUser

    Write-Progress -activity "Processing ${xmltoimport} in batches of ${batchsize}" -status "Batch ${outputfilecount}: " -percentComplete (($objOutputUsers.Count / $batchsize) * 100)

    #every so often, dump hello processed users in case we blow up somewhere
    if ($count % $batchsize -eq 0)
    {
        Write-Host Hit hello maximum users processed without completion... -ForegroundColor Yellow

        #export hello collection of users as as CSV
        Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
        $objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation

        #increment hello output file counter
        $outputfilecount+=1

        #reset hello collection and hello user counter
        $objOutputUsers = $null
        $count=0
    }

    $count+=1

    #need toobail out of hello loop if no more users tooprocess
    if ($reader.NodeType -eq [System.Xml.XmlNodeType]::EndElement)
    {
        break
    }

} while ($reader.Read)

#need toowrite out any users that didn't get picked up in a batch of 1000
#export hello collection of users as as CSV
Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
$objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation
```

## <a name="next-steps"></a>Étapes suivantes
**Rubriques de présentation**  

* [Azure AD Connect Sync - Présentation et personnalisation des options de synchronisation](active-directory-aadconnectsync-whatis.md)  
* [Intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md)  
