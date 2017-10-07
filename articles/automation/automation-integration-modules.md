---
title: "aaaCreate un Module d’intégration Azure Automation | Documents Microsoft"
description: "Didacticiel qui vous guide à l’aide de la création, le test et exemple hello des modules d’intégration dans Azure Automation."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 27798efb-08b9-45d9-9b41-5ad91a3df41e
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/13/2017
ms.author: magoedte
ms.openlocfilehash: d4064d8b106496f4dab442024131886c4affccab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-integration-modules"></a>Modules d’intégration Azure Automation
PowerShell est la technologie fondamentaux hello Azure Automation. Étant donné que Azure Automation est basée sur PowerShell, modules PowerShell sont extensibilité toohello clé d’Azure Automation. Dans cet article, nous vous guidera tout au long des spécificités de hello d’utilisation d’Azure Automation de modules PowerShell visé tooas « Modules d’intégration » et meilleures pratiques pour la création de votre propre toomake de modules PowerShell assurer qu'elles fonctionnent comme des Modules d’intégration dans Azure Automation. 

## <a name="what-is-a-powershell-module"></a>Qu’est-ce qu’un module PowerShell ?
Un module PowerShell est un groupe d’applets de commande PowerShell comme **Get-Date** ou **Copy-Item**, qui peut être utilisé à partir de la console PowerShell de hello, les scripts, les flux de travail, les runbooks et les ressources DSC PowerShell telles que WindowsFeature ou fichier, qui peut être utilisé dans les configurations DSC PowerShell. Toutes les fonctionnalités de hello de PowerShell est exposée via les applets de commande et des ressources DSC, et toutes les ressources DSC / l’applet de commande sont soutenu par un module PowerShell, un grand nombre des qui sont fournis avec PowerShell. Par exemple, hello **Get-Date** applet de commande fait partie du module Microsoft.PowerShell.Utility PowerShell, de hello et **Copy-Item** applet de commande fait partie du module Microsoft.PowerShell.Management PowerShell de hello et Hello ressource DSC de Package fait partie de hello module PSDesiredStateConfiguration PowerShell. Ces deux modules sont fournis avec PowerShell. Mais un nombre de modules PowerShell ne sont pas fournis dans le cadre de PowerShell et est distribuée à la place avec les produits tiers ou première tels que System Center 2012 Configuration Manager ou de hello grande PowerShell Communauté sur emplacements tels que PowerShell Gallery.  modules de Hello sont utiles car ils simplifient les tâches complexes via la fonctionnalité encapsulée.  Vous pouvez en savoir plus sur les [modules PowerShell sur MSDN](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx). 

## <a name="what-is-an-azure-automation-integration-module"></a>Qu’est-ce qu’un module d’intégration Azure Automation ?
Un module d’intégration n’est pas très différent d’un module PowerShell. Son simplement un module PowerShell qui contient éventuellement un fichier supplémentaire - un fichier de métadonnées en spécifiant un toobe de type de connexion Azure Automation utilisé avec les applets de commande du module hello dans les runbooks. Facultatif du fichier ou non, ces modules peuvent être importés dans toomake Azure Automation des applets de commande disponibles pour les utilisent dans des procédures opérationnelles et de leurs ressources DSC disponibles pour une utilisation dans les configurations DSC de PowerShell. Coulisses de hello, Azure Automation stocke ces modules et au moment de l’exécution de travaux de compilation DSC et à la tâche du runbook, il les charge dans sandbox d’Azure Automation hello où les runbooks sont exécutés et les configurations DSC sont compilées.  Toutes les ressources DSC dans les modules sont placés automatiquement sur le serveur de collecteur hello Automation DSC, afin qu’ils peuvent être extraites par les ordinateurs de tooapply les configurations DSC.  

Nous livrer un nombre de modules Azure PowerShell en dehors de la zone hello dans Azure Automation pour vous toouse afin de commencer à automatiser la gestion de Azure immédiatement, mais vous pouvez importer des modules PowerShell pour le système, un service ou un outil que vous souhaitez utiliser toointegrate avec. 

> [!NOTE]
> Certains modules sont fournis en tant que « modules globales » dans le service d’automatisation hello. Ces modules globaux sont tooyou disponible lorsque vous créez un compte automation, et nous les mettre à jour parfois qui les envoie automatiquement les comptes d’automation tooyour. Si vous ne souhaitez pas les toobe à jour automatiquement, vous pouvez toujours importer hello même module vous-même, et qui ont priorité sur la version du module global hello de ce module nous fournis dans le service hello. 

format Hello dans laquelle importer un package de Module d’intégration est un fichier compressé portant le même nom de module de hello et l’extension .zip de hello. Il contient le module Windows PowerShell de hello et tous les fichiers de prise en charge, y compris un fichier manifeste (.psd1) si le module de hello a un.

Si le module de hello doit contenir un type de connexion Azure Automation, il doit également contenir un fichier portant le nom de hello `<ModuleName>-Automation.json` qui spécifie les propriétés de type de connexion hello. Ceci est un fichier json placé dans le dossier du module hello de votre fichier .zip compressé et contient des champs de hello d’une « connexion », qui est requis tooconnect toohello système ou service hello module représente. Ceci créera un type de connexion dans Azure Automation. À l’aide de ce fichier, vous pouvez définir des noms de champ de hello, types, et indique si les champs de hello doivent être chiffrées et/ou facultatifs pour le type de connexion hello du module de hello. Hello Voici un modèle au format json hello :

```
{ 
   "ConnectionFields": [
   {
      "IsEncrypted":  false,
      "IsOptional":  false,
      "Name":  "ComputerName",
      "TypeName":  "System.String"
   },
   {
      "IsEncrypted":  false,
      "IsOptional":  true,
      "Name":  "Username",
      "TypeName":  "System.String"
   },
   {
      "IsEncrypted":  true,
      "IsOptional":  false,
      "Name":  "Password",
   "TypeName":  "System.String"
   }],
   "ConnectionTypeName":  "DataProtectionManager",
   "IntegrationModuleName":  "DataProtectionManager"
}
```

Si vous avez déployé le Service Management Automation et créé les packages de Modules d’intégration de vos runbooks automation, cela doit ressembler tooyou très familier. 

## <a name="authoring-best-practices"></a>Établissement de meilleures pratiques
Bien que les Modules d’intégration sont essentiellement des modules PowerShell, il est toujours un nombre de choses que nous vous recommandons d’envisager lors de la création d’un module PowerShell, toomake il est plus utilisable dans Azure Automation. Certaines sont spécifiques à Azure Automation, et certaines d'entre elles sont utile toomake simplement vos modules fonctionnent correctement dans les flux de travail PowerShell, indépendamment de si vous utilisez l’Automation. 

1. Inclure un résumé des différentes, description et aider à des URI pour chaque applet de commande dans le module de hello. Dans PowerShell, vous pouvez définir certaines informations d’aide pour l’aide d’applets de commande tooallow hello utilisateur tooreceive sur leur utilisation avec hello **Get-Help** applet de commande. Par exemple, voici comment définir un synopsis et l’URI d’aide pour un module PowerShell écrit dans un fichier .psm1.<br>  
   
    ```
    <#
        .SYNOPSIS
         Gets all outgoing phone numbers for this Twilio account 
    #>
    function Get-TwilioPhoneNumbers {
    [CmdletBinding(DefaultParameterSetName='SpecifyConnectionFields', `
    HelpUri='http://www.twilio.com/docs/api/rest/outgoing-caller-ids')]
    param(
       [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [string]
       $AccountSid,
   
       [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [string]
       $AuthToken,
   
       [Parameter(ParameterSetName='UseConnectionObject', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [Hashtable]
       $Connection
    )
   
    $cred = CreateTwilioCredential -Connection $Connection -AccountSid $AccountSid -AuthToken $AuthToken
   
    $uri = "$TWILIO_BASE_URL/Accounts/" + $cred.UserName + "/IncomingPhoneNumbers"
   
    $response = Invoke-RestMethod -Method Get -Uri $uri -Credential $cred
   
    $response.TwilioResponse.IncomingPhoneNumbers.IncomingPhoneNumber
    }
    ```
   <br> Fournir ces informations uniquement n’affichera pas cette aide à l’aide de hello **Get-Help** applet de commande hello console PowerShell, il expose également cette fonctionnalité d’aide dans Azure Automation.  Par exemple, lors de l’insertion d’activités lors de la création de runbook. Cliquez sur « Afficher une aide détaillée » sera aide hello ouvrir URI dans un autre onglet de hello navigateur web à l’aide de tooaccess Azure Automation.<br>![Aide du module d’intégration](media/automation-integration-modules/automation-integration-module-activitydesc.png)
2. Si le module de hello s’exécute sur un système distant,

    a. Elle doit contenir un fichier de métadonnées du Module d’intégration qui définit hello informations nécessaires tooconnect toothat système distant, ce qui signifie le type de connexion hello.  
    b. Chaque applet de commande dans le module de hello doit être en mesure de tootake dans un objet de connexion (il s’agit d’une instance de ce type de connexion) en tant que paramètre.  

    Applets de commande hello module deviennent toouse plus facile dans Azure Automation si vous autorisez le passage d’un objet avec des champs hello hello du type de connexion en tant qu’une applet de commande de toohello de paramètre. Ainsi, les utilisateurs n’ont pas les paramètres de toomap de paramètres correspondants de hello connexion asset toohello l’applet de commande chaque fois qu’ils appellent une applet de commande. En fonction de l’exemple de runbook hello ci-dessus, il utilise une ressource de connexion Twilio appelée CorpTwilio tooaccess Twilio et retourner tous les numéros de téléphone hello dans le compte de hello.  Notez comment il consiste à mapper les champs hello hello toohello des paramètres de connexion de l’applet de commande hello ?<br>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers 
        -AccountSid $CorpTwilio.AccountSid  
        -AuthToken $CorptTwilio.AuthToken
    }
    ```
  
    Un tooapproach de manière plus simple et une meilleure cela est directement le passage d’applet de commande de toohello de hello connexion object-
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers -Connection $CorpTwilio
    }
    ```
   
    Vous pouvez activer le comportement comme suit pour vos applets de commande en les autorisant tooaccept un objet de connexion directement en tant que paramètre, au lieu de simplement les champs de connexion pour les paramètres. Vous souhaiterez généralement un jeu de paramètres pour chacun, afin que l’utilisateur ne pas à l’aide d’Azure Automation peut appeler vos applets de commande sans faire appel à une tooact de la table de hachage en tant qu’objet de connexion hello. Jeu de paramètres **SpecifyConnectionFields** Voici toopass utilisé les propriétés de champ de connexion hello un par un. **UseConnectionObject** vous permet de transmettre hello directement par le biais de la connexion. Comme vous pouvez le voir, hello applet de commande Send-TwilioSMS Bonjour [module PowerShell de Twilio](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) permet le passage dans les deux cas : 
   
    ```
    function Send-TwilioSMS {
      [CmdletBinding(DefaultParameterSetName='SpecifyConnectionFields', `
      HelpUri='http://www.twilio.com/docs/api/rest/sending-sms')]
      param(
         [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [string]
         $AccountSid,
   
         [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [string]
         $AuthToken,
   
         [Parameter(ParameterSetName='UseConnectionObject', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [Hashtable]
         $Connection
   
       )
    }
    ```
   <br>
3. Définir le type de sortie pour toutes les applets de commande dans le module de hello. Définition d’un type de sortie pour une applet de commande permet à IntelliSense au moment du design toohelp vous hello Déterminez les propriétés de l’applet de commande hello, pour une utilisation lors de la création de sortie. Cela est particulièrement utile lors de l’Automation runbook graphique de création, où les connaissances des temps de conception est tooan clé facile confort d’utilisation avec le module.<br><br> ![Type de sortie de Runbook graphique](media/automation-integration-modules/runbook-graphical-module-output-type.png)<br> Cela s’apparente toohello « de type avance » de fonctionnalité d’applet de commande de sortie dans PowerShell ISE sans avoir toorun il.<br><br> ![POSH IntelliSense](media/automation-integration-modules/automation-posh-ise-intellisense.png)<br>
4. Applets de commande hello module ne nécessite pas de types d’objet complexe pour les paramètres. La différence entre PowerShell et le Workflow PowerShell réside dans le fait que ce dernier stocke des types complexes sous forme désérialisée. Les types primitifs resteront en tant que primitives, mais les types complexes sont les versions tootheir converti désérialisé, qui sont essentiellement des conteneurs de propriétés. Par exemple, si vous avez utilisé hello **Get-Process** applet de commande dans un runbook (ou un flux de travail PowerShell quel), il serait retournent un objet de type [Deserialized.System.Diagnostic.Process], pas hello [attendu Type de System.diagnostic.Process retournés]. Ce type possède toutes les hello les mêmes propriétés que hello non désérialiser le type, mais aucune des méthodes de hello. Et si vous essayez de toopass cette valeur comme paramètre tooa applet de commande, où hello applet de commande attend une valeur de [System.diagnostic.Process retournés] pour ce paramètre, vous recevez hello l’erreur suivante : *ne peut pas traiter de transformation d’argument sur le paramètre « processus » . Erreur : « Impossible de convertir hello les valeur de « System.Diagnostics.Process (CcmExec) » de type « Deserialized.System.Diagnostics.Process » tootype « System.Diagnostics.Process ».*   Il s’agit, car il existe qu'une incompatibilité de type entre hello attendu [System.diagnostic.Process retournés] type et hello [Deserialized.System.Diagnostic.Process] type donné. Hello corriger ce problème consiste tooensure hello applets de commande de votre module ne prennent pas de types complexes pour les paramètres. Voici hello mauvaise méthode toodo il.
   
    ```
    function Get-ProcessDescription {
      param (
            [System.Diagnostic.Process] $process
      )
      $process.Description
    }
    ``` 
    <br>
    Et Voici hello droite, dans une primitive qui peut être utilisée en interne par l’applet de commande hello toograb hello objet complexe et l’utiliser. Étant donné que les applets de commande s’exécutent dans le contexte de hello de PowerShell, pas PowerShell Workflow, à l’intérieur d’applet de commande hello $process est de type hello correcte [System.diagnostic.Process retournés].  
   
    ```
    function Get-ProcessDescription {
      param (
            [String] $processName
      )
      $process = Get-Process -Name $processName
   
      $process.Description
    }
    ```
   <br>
   Ressources de connexion dans les runbooks sont des tables de hachage, qui sont un type complexe, et encore ces tables de hachage semblent toobe en mesure de toobe passé dans les applets de commande pour leurs : paramètre de connexion parfaitement, avec aucune exception de cast. Techniquement, certains types de PowerShell sont en mesure de toocast correctement à partir de leur forme tootheir désérialisé de formulaire sérialisé et peuvent donc être passés dans les applets de commande pour les paramètres d’accepter le type de non désérialisé hello. La table de hachage fait partie de ces types. Il est possible pour toobe de types définis de l’auteur d’un module implémentée de manière à ce qu’ils capable de désérialiser correctement également, mais il existe certaines tooconsider compromis. Hello type besoins toohave un constructeur par défaut, ont toutes ses propriétés de public et avoir un PSTypeConverter. Toutefois, pour les types déjà définis par cet auteur de module hello non propriétaire, il existe trop ne « corriger » les, donc hello recommandation tooavoid des types complexes pour l’ensemble de paramètres. Création de runbooks de Conseil : si pour une raison quelconque vos applets de commande avez besoin de paramètre de type tootake un type complexe, ou à l’aide de module d’une autre personne qui requiert un paramètre de type complexe, la solution de contournement hello dans les runbooks PowerShell Workflow et les flux de travail PowerShell local PowerShell, est l’applet de commande toowrap hello qui génère le type complexe de hello et l’applet de commande hello qui utilise le type complexe de hello Bonjour même activité InlineScript. Étant donné que InlineScript s’exécute à son contenu en tant que PowerShell plutôt que le flux de travail PowerShell, applet de commande hello génération de type complexe de hello génère ce type correct, pas hello désérialisé type complexe.
5. Vérifiez toutes les applets de commande dans le module de hello sans état. Flux de travail PowerShell s’exécute chaque applet de commande appelé dans le flux de travail hello dans une autre session. Cela signifie que toutes les applets de commande qui dépendent de l’état de session créé / modifié par d’autres applets de commande Bonjour même module ne fonctionnera pas dans les runbooks PowerShell Workflow.  Voici un exemple de ce que toodo pas.
   
    ```
    $globalNum = 0
    function Set-GlobalNum {
       param(
           [int] $num
       )
   
       $globalNum = $num
    }
    function Get-GlobalNumTimesTwo {
       $output = $globalNum * 2
   
       $output
    }
    ```
   <br>
6. module de Hello doit être entièrement contenue dans un package en mesure de Xcopy. Modules d’automatisation d’Azure sont distribuées toohello Automation sandbox lorsque runbooks devez tooexecute, il est nécessaire toowork indépendamment hôte hello sur que s’exécutent. Cela signifie que vous devez être en mesure de tooZip package de module hello, déplacez-le tooany autre hôte avec hello identique ou plus récente version de PowerShell, et qu’il fonctionne normalement lors de l’importation dans l’environnement PowerShell de l’ordinateur hôte. Afin que toohappen, hello module ne doit pas dépendre des fichiers en dehors du dossier de module hello (dossier hello qui obtient compressé lors de l’importation dans Azure Automation) ou sur tous les paramètres de Registre unique sur un ordinateur hôte, telles que celles définies par hello installation d’un produit. Si cela n’est pas suivie, il se peut que hello module ne sera pas utilisable dans Azure Automation.  

## <a name="next-steps"></a>Étapes suivantes

* tooget a démarré avec des runbooks de flux de travail PowerShell, consultez [mon premier runbook de flux de travail PowerShell](automation-first-runbook-textual.md)
* toolearn plus sur la création de Modules PowerShell, consultez [l’écriture d’un Module Windows PowerShell](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)

