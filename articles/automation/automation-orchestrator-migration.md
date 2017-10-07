---
title: "aaaMigrating à partir d’Orchestrator tooAzure Automation | Documents Microsoft"
description: "Décrit comment intégration et toomigrate runbooks packs à partir de System Center Orchestrator tooAzure Automation."
services: automation
documentationcenter: 
author: bwren
manager: stevenka
editor: tysonn
ms.assetid: 1a7da58c-7a98-49b5-9d9d-001a9f6e631a
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/09/2016
ms.author: bwren
ms.openlocfilehash: 797b50067ef2aa68470760e99d494b89ab7baacf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-from-orchestrator-tooazure-automation-beta"></a>Migration à partir d’Orchestrator tooAzure Automation (bêta)
Dans [System Center Orchestrator](http://technet.microsoft.com/library/hh237242.aspx) , les Runbooks sont basés sur les activités de packs d'intégration spécifiquement écrits pour Orchestrator, tandis que dans Azure Automation, ils sont basés sur Windows PowerShell.  [Runbooks graphiques](automation-runbook-types.md#graphical-runbooks) dans Azure Automation ont un runbook de tooOrchestrator apparence similaire avec leurs activités représentant les applets de commande PowerShell, les runbooks enfants et les ressources.

Hello [System Center Orchestrator Migration Toolkit](http://www.microsoft.com/download/details.aspx?id=47323&WT.mc_id=rss_alldownloads_all) inclut des outils tooassist vous de la conversion des runbooks d’Orchestrator tooAzure Automation.  En outre les runbooks de hello tooconverting eux-mêmes, vous devez convertir les packs d’intégration hello avec activités hello que hello runbooks utiliser toointegration modules avec les applets de commande Windows PowerShell.  

Voici hello des processus de base pour la conversion d’Orchestrator runbook tooAzure Automation.  Chacune de ces étapes est décrite en détail dans les sections hello ci-dessous.

1. Télécharger hello [System Center Orchestrator Migration Toolkit](http://www.microsoft.com/download/details.aspx?id=47323&WT.mc_id=rss_alldownloads_all) qui contient les outils hello et les modules décrits dans cet article.
2. Importez le [module d'activités Standard](#standard-activities-module) dans Azure Automation.  Cela inclut les versions converties des activités Orchestrator standard qui peuvent être utilisées par les Runbooks convertis.
3. Importez les [modules d'intégration de System Center Orchestrator](#system-center-orchestrator-integration-modules) dans Azure Automation pour les packs d'intégration utilisés par vos Runbooks ayant accès à System Center.
4. Convertir des packs d’intégration de tiers et personnalisés à l’aide de hello [convertisseur du Pack d’intégration](#integration-pack-converter) et l’importer dans Azure Automation.
5. Convertir les runbook Orchestrator à l’aide de hello [Runbook convertisseur](#runbook-converter) et installer dans Azure Automation.
6. Créer manuellement les composants Orchestrator requis dans Azure Automation depuis hello Runbook convertisseur ne convertit pas ces ressources.
7. Configurer un [Runbook Worker hybride](#hybrid-runbook-worker) dans vos runbook de toorun converti de centre de données locales qui accèdent aux ressources locales.

## <a name="service-management-automation"></a>Service Management Automation
[Service Management Automation](http://technet.microsoft.com/library/dn469260.aspx) (SMA) stocke et exécute des procédures opérationnelles dans votre centre de données local comme Orchestrator et il utilise hello même modules d’intégration Azure Automation. Hello [Runbook convertisseur](#runbook-converter) convertit les runbooks d’Orchestrator runbook toographical cependant qui ne sont pas pris en charge dans SMA.  Vous pouvez toujours installer hello [Module activités Standard](#standard-activities-module) et [Modules d’intégration de System Center Orchestrator](#system-center-orchestrator-integration-modules) dans SMA, mais vous devez manuellement [réécrire vos runbooks](http://technet.microsoft.com/library/dn469262.aspx).

## <a name="hybrid-runbook-worker"></a>Runbook Worker hybride
Dans Orchestrator, les Runbooks sont stockés sur un serveur de base de données et s'exécutent sur des serveurs de Runbooks, les deux se trouvant dans votre centre de données local.  Runbooks d’Azure Automation sont stockés dans hello cloud Azure et peuvent s’exécuter dans votre centre de données locales à l’aide un [Runbook Worker hybride](automation-hybrid-runbook-worker.md).  Voici comment vous allez exécuter généralement des procédures opérationnelles convertie à partir d’Orchestrator, car elles sont conçue toorun sur des serveurs locaux.

## <a name="integration-pack-converter"></a>convertisseur de packs d'intégration
Hello convertisseur du Pack d’intégration convertit des packs d’intégration qui ont été créés à l’aide de hello [Orchestrator Integration Toolkit (OIT)](http://technet.microsoft.com/library/hh855853.aspx) toointegration modules basé sur Windows PowerShell qui peut être importé dans Azure Automation ou Service Management Automation.  

Lorsque vous exécutez hello convertisseur du Pack d’intégration, vous sont présentées avec un Assistant qui vous permettra de tooselect fichier de pack (oip) d’intégration.  Assistant de Hello puis répertorie les activités hello incluses dans ce pack d’intégration et vous permet de tooselect qui est migré.  Lorsque vous complétez les Assistant hello, il crée un module d’intégration qui inclut une applet de commande correspondante pour chacune des activités hello dans le pack d’intégration d’origine hello.

### <a name="parameters"></a>Paramètres
Toutes les propriétés d’une activité dans le Pack d’intégration de hello sont convertis tooparameters de hello l’applet de commande correspondante dans le module d’intégration hello.  Les applets de commande Windows PowerShell possèdent un ensemble de [paramètres communs](http://technet.microsoft.com/library/hh847884.aspx) qui peuvent être utilisés avec toutes les applets de commande.  Par exemple, hello - paramètre Verbose, une applet de commande toooutput des informations détaillées sur son fonctionnement.  Aucune applet de commande ne peut avoir un paramètre avec le même nom qu’un paramètre commun de hello.  Si une activité ne possède pas une propriété portant le même nom qu’un paramètre commun de hello, Assistant de hello invitera à vous tooprovide un autre nom pour le paramètre hello.

### <a name="monitor-activities"></a>Activités d'analyse
Surveiller les runbooks dans le démarrage d’Orchestrator avec un [surveiller l’activité](http://technet.microsoft.com/library/hh403827.aspx) et s’exécutent en continu toobe attente appelée par un événement particulier.  Azure Automation ne prend pas en charge runbook d’analyse, toutes les activités d’analyse dans le Pack d’intégration de hello ne seront pas converties.  Au lieu de cela, une applet de commande d’espace réservé est créé dans le module d’intégration hello pour surveiller l’activité hello.  Cette applet de commande n’a aucune fonctionnalité, mais elle permet à n’importe quel runbook converti qui l’utilise toobe installé.  Ce runbook ne sera pas en mesure de toorun dans Azure Automation, mais il peut être installé afin que vous puissiez le modifier.

### <a name="integration-packs-that-cannot-be-converted"></a>Packs d'intégration ne pouvant pas être convertis
Impossible de convertir les packs d’intégration qui n’ont pas été créés avec OIT avec hello convertisseur du Pack d’intégration. Il existe également des packs d'intégration fournis par Microsoft qui ne peuvent actuellement pas être convertis avec cet outil.  Les versions converties de ces packs d'intégration sont [fournies pour le téléchargement](#system-center-orchestrator-integration-modules) afin de pouvoir être installées dans Azure Automation ou Service Management Automation.

## <a name="standard-activities-module"></a>module d'activités Standard
Orchestrator inclut un ensemble d' [activités standard](http://technet.microsoft.com/library/hh403832.aspx) qui ne sont pas incluses dans un pack d'intégration, mais qui sont utilisées par de nombreux Runbooks.  module d’activités Standard Hello est un module d’intégration qui inclut une applet de commande équivalente pour chacune de ces activités.  Vous devez installer le module d'intégration dans Azure Automation avant d'importer des Runbooks convertis qui utilisent une activité standard.

En outre toosupporting convertis procédures opérationnelles, applets de commande hello dans le module d’activités standard hello peut être utilisé par une personne connaissant Orchestrator toobuild de runbooks dans Azure Automation.  Alors que la fonctionnalité hello de toutes les activités standard hello peut être effectuée avec les applets de commande, ils peuvent fonctionner différemment.  Hello applets de commande dans les activités standard hello converti module fonctionnera hello même que leurs activités et l’utilisation correspondante hello les mêmes paramètres.  Cela peut permettre d’auteur de runbook de Orchestrator existant hello dans leur tooAzure transition runbooks Automation.

## <a name="system-center-orchestrator-integration-modules"></a>modules d'intégration de System Center Orchestrator
Microsoft fournit [packs d’intégration](http://technet.microsoft.com/library/hh295851.aspx) pour la création de composants de System Center tooautomate runbooks et d’autres produits.  Certaines de ces packs d’intégration actuellement reposent sur OIT, mais ne peut pas être actuellement les modules toointegration converti en raison de problèmes connus.  [modules d'intégration de System Center Orchestrator](https://www.microsoft.com/download/details.aspx?id=49555) incluent des versions converties de ces packs d'intégration qui peuvent être importées dans Azure Automation et dans Service Management Automation.  

Version RTM de hello de cet outil, mis à jour les versions des packs d’intégration de hello selon OIT qui peut être converti par hello que convertisseur du Pack d’intégration sera publiée.  Des conseils sont fournis tooassist lors de la conversion des runbooks à l’aide des activités de packs d’intégration hello ne pas en fonction de OIT.

## <a name="runbook-converter"></a>convertisseur de Runbooks
Hello Runbook convertisseur runbooks d’Orchestrator dans [runbooks graphiques](automation-runbook-types.md#graphical-runbooks) qui peuvent être importés dans Azure Automation.  

Convertisseur de Runbook est implémenté comme un module PowerShell avec une applet de commande appelé **ConvertFrom-SCORunbook** qui effectue une conversion de hello.  Lorsque vous installez les outil hello, il crée une session de PowerShell tooa raccourci qui charge l’applet de commande hello.   

Suivante est tooconvert du processus de base hello un runbook Orchestrator et l’importer dans Azure Automation.  Hello sections suivantes fournissent des informations détaillées sur l’utilisation de hello outil et l’utilisation de procédures opérationnelles converti.

1. Exporter un ou plusieurs Runbooks depuis Orchestrator.
2. Obtenir des modules d’intégration pour toutes les activités de runbook de hello.
3. Convertir les runbooks d’Orchestrator hello dans le fichier d’exportation hello.
4. Examinez les informations de conversion de journaux toovalidate hello et toodetermine les tâches manuelles requises.
5. Importer les Runbooks convertis dans Azure Automation.
6. Créer tous les éléments requis dans Azure Automation.
7. Modifier le runbook hello dans Azure Automation toomodify toutes les activités requises.

### <a name="using-runbook-converter"></a>Utilisation du convertisseur de Runbooks
Hello syntaxe pour **ConvertFrom-SCORunbook** est comme suit :

    ConvertFrom-SCORunbook -RunbookPath <string> -Module <string[]> -OutputFolder <string>

* RunbookPath - fichier d’exportation de toohello de chemin d’accès contenant tooconvert de procédures opérationnelles hello.
* Module - virgule liste délimitée par des modules d’intégration contenant des activités dans les runbook hello.
* OutputFolder - chemin d’accès toohello dossier toocreate converti runbooks graphiques.

Hello suivant l’exemple de commande convertit hello procédures opérationnelles dans un fichier d’exportation appelé **MyRunbooks.ois_export**.  Ces procédures opérationnelles utilisent hello Active Directory et les packs d’intégration de Data Protection Manager.

    ConvertFrom-SCORunbook -RunbookPath "c:\runbooks\MyRunbooks.ois_export" -Module c:\ip\SystemCenter_IntegrationModule_ActiveDirectory.zip,c:\ip\SystemCenter_IntegrationModule_DPM.zip -OutputFolder "c:\runbooks"


### <a name="log-files"></a>Fichiers journaux
Hello Runbook convertisseur créera hello suivant des fichiers journaux dans hello même emplacement que hello converti runbook.  Si les fichiers hello existent déjà, puis ils sont remplacés avec les informations de conversion de dernière hello.

| Fichier | Sommaire |
|:--- |:--- |
| Convertisseur de Runbooks - Progress.log |Étapes détaillées de conversion hello, y compris des informations pour chaque activité correctement converties en valeurs et avertissement pour chaque activité ne pas convertie. |
| Convertisseur de Runbooks - Summary.log |Résumé de hello, y compris les avertissements de conversion de la dernière et suivi des tâches que vous devez tooperform telles que la création d’une variable requise pour les runbook hello converti. |

### <a name="exporting-runbooks-from-orchestrator"></a>Exportation de Runbooks Orchestrator
Hello Runbook convertisseur fonctionne avec un fichier d’exportation à partir d’Orchestrator qui contient un ou plusieurs runbooks.  Elle créera un runbook Azure Automation correspondant pour chaque runbook Orchestrator dans un fichier d’exportation hello.  

tooexport un runbook à partir d’Orchestrator, le bouton droit sur hello hello des runbook dans Runbook Designer et sélectionnez **exporter**.  tooexport tous les runbooks dans un dossier, le bouton droit sur hello hello et sélectionnez **exporter**.

### <a name="runbook-activities"></a>Activités de Runbook
Hello Runbook convertisseur convertit chaque activité Bonjour activité correspondante tooa runbook Orchestrator dans Azure Automation.  Pour les activités qui ne peut pas être converties, une activité de l’espace réservé est créée dans runbook hello avec le texte d’avertissement.  Après avoir importé hello converti runbook dans Azure Automation, vous devez remplacer une de ces activités avec des activités valides qui exécutent les fonctions hello requis.

Toutes les activités d’Orchestrator Bonjour [Module activités Standard](#standard-activities-module) sera convertie.  Certaines activités standard d'Orchestrator ne sont pas dans ce module et ne sont pas converties.  Par exemple, **envoyer un événement de plate-forme** n’a aucun équivalent Azure Automation, car les événements hello sont tooOrchestrator spécifique.

[Surveiller les activités](https://technet.microsoft.com/library/hh403827.aspx) ne sont pas convertis dans la mesure où il n’existe aucun équivalent toothem dans Azure Automation.  Hello exception sont analyse des activités dans [converti des packs d’intégration](#integration-pack-converter) qui sera converti toohello espace réservé activité.

Toute activité d’un [converti le Pack d’intégration](#integration-pack-converter) seront convertis si vous fournissez un module d’intégration toohello hello chemin d’accès par hello **modules** paramètre.  Pour les Packs d’intégration de System Center, vous pouvez utiliser hello [Modules d’intégration de System Center Orchestrator](#system-center-orchestrator-integration-modules).

### <a name="orchestrator-resources"></a>Ressources Orchestrator
Hello Runbook convertisseur convertit uniquement les procédures opérationnelles, pas les autres ressources des Orchestrator tels que des compteurs, variables ou les connexions.  Les compteurs ne sont pas pris en charge dans Azure Automation.  Les variables et les connexions sont pris en charge, mais vous devez les créer manuellement.  fichiers de journaux de Hello seront vous informent si hello a besoin de ces ressources et spécifier les ressources correspondantes que vous devez toocreate dans Azure Automation pour hello converti runbook toooperate correctement.

Par exemple, un runbook peut utiliser une variable toopopulate une valeur particulière dans une activité.  Hello runbook converti convertira activité hello et spécifiez une ressource de variable dans Azure Automation avec le même nom en tant que variable d’Orchestrator hello de hello.  Ce est noté dans hello **Runbook convertisseur - Summary.log** fichier créé après la conversion de hello.  Vous devez toomanually créer cette ressource de variable dans Azure Automation avant d’utiliser hello runbook.

### <a name="input-parameters"></a>Paramètres d'entrée
Runbooks d’Orchestrator accepter des paramètres d’entrée avec hello **initialiser des données** activité.  Si runbook hello en cours de conversion inclut cette activité, puis un [paramètre d’entrée](automation-graphical-authoring-intro.md#runbook-input-and-output) Bonjour Azure Automation runbook est créé pour chaque paramètre dans l’activité hello.  A [contrôle de Script de flux de travail](automation-graphical-authoring-intro.md#activities) activité est créée dans le runbook hello converti qui extrait et retourne chaque paramètre.  Toutes les activités de runbook de hello qui utilisent un paramètre d’entrée font référence toohello sortie de cette activité.

Hello que cette stratégie est utilisée parce toobest miroir hello Nouveautés du runbook Orchestrator hello.  Activités de nouveaux runbook graphique doivent faire référence directement les paramètres de tooinput à l’aide d’une source de données d’entrée du Runbook.

### <a name="invoke-runbook-activity"></a>Appeler l'activité Runbook
Runbooks d’Orchestrator démarrer d’autres runbook par hello **appeler Runbook** activité. Si runbook hello en cours de conversion inclut cette activité et le hello **attendre l’achèvement** option est définie, puis une activité de runbook est créée pour elle dans les runbook hello converti.  Si hello **attendre l’achèvement** option n’est pas définie, puis une activité de Script de flux de travail est créée qui utilise **Start-AzureAutomationRunbook** toostart hello runbook.  Après avoir importé hello converti runbook dans Azure Automation, vous devez modifier cette activité avec les informations de hello spécifiées dans l’activité de hello.

## <a name="related-articles"></a>Articles connexes
* [System Center 2012 - Orchestrator](http://technet.microsoft.com/library/hh237242.aspx)
* [Service Management Automation](https://technet.microsoft.com/library/dn469260.aspx)
* [Runbook Worker hybride](automation-hybrid-runbook-worker.md)
* [Activités standard d'Orchestrator](http://technet.microsoft.com/library/hh403832.aspx)
* [Télécharger le kit de migration System Center Orchestrator](https://www.microsoft.com/en-us/download/details.aspx?id=47323)
