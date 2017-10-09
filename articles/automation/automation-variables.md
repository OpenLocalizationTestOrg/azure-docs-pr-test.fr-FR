---
title: ressources aaaVariable dans Azure Automation | Documents Microsoft
description: "Les ressources de variables sont des valeurs qui sont disponibles tooall runbooks et les configurations DSC dans Azure Automation.  Cet article explique les détails de hello de variables et la manière dont toowork avec eux dans textuels et graphiques de création."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: b880c15f-46f5-4881-8e98-e034cc5a66ec
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/09/2017
ms.author: magoedte;bwren
ms.openlocfilehash: f9daa49fc1dc883ffb218a9adf26e36df1d6bb27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="variable-assets-in-azure-automation"></a>Ressources de variables dans Azure Automation

Les ressources de variables sont des valeurs qui sont disponibles tooall runbooks et les configurations DSC dans votre compte automation. Ils peuvent être créés, modifiés et récupérées à partir de hello portail Azure, Windows PowerShell et à partir d’un runbook ou la configuration DSC. Les variables Automation sont utiles pour hello les scénarios suivants :

- Partager une valeur entre plusieurs Runbooks ou configurations DSC.

- Partager une valeur entre plusieurs travaux hello même runbook ou la configuration DSC.

- Gérer une valeur à partir du portail de hello ou à partir de la ligne de commande Windows PowerShell hello qui est utilisé par les procédures opérationnelles ou les configurations DSC, comme un ensemble commun d’éléments de configuration comme liste de noms de machine virtuelle, un groupe de ressources spécifique, nom de domaine Active Directory, etc..  

Variables Automation sont conservées afin qu’ils continuent toobe disponible même en cas de hello runbook ou la configuration DSC.  Cela permet également à un toobe de valeur définie par un runbook qui est ensuite utilisé par un autre, ou qui est utilisé par hello même runbook ou hello de configuration DSC prochaine fois qu’elle est exécutée.

Quand une variable est créée, vous pouvez spécifier qu'elle doit être stockée de manière chiffrée.  Lorsqu’une variable est chiffrée, il est stocké en toute sécurité dans Azure Automation, et sa valeur ne peut pas être récupérée à partir de hello [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx) applet de commande qui est fourni en tant que partie du module Azure PowerShell de hello.  Hello uniquement une valeur chiffrée peut être récupérée que consiste à partir de hello **Get-AutomationVariable** activité dans un runbook ou la configuration DSC.

> [!NOTE]
> Les ressources sécurisées dans Azure Automation incluent les informations d'identification, les certificats, les connexions et les variables chiffrées. Ces ressources sont chiffrées et stockées Bonjour Azure Automation à l’aide d’une clé unique qui est générée pour chaque compte automation. Cette clé est chiffrée par un certificat principal et stockée dans Azure Automation. Avant de stocker une ressource sécurisée, clé hello pour le compte d’automatisation hello est déchiffré à l’aide du certificat master de hello, puis utilisé asset de hello tooencrypt.

## <a name="variable-types"></a>Types de variables

Lorsque vous créez une variable avec hello portail Azure, vous devez spécifier un type de données à partir de la liste déroulante de hello pour le portail de hello peut afficher le contrôle approprié de hello pour entrer la valeur de la variable hello. variable de Hello n’est pas restreinte toothis données type, mais vous devez définir variable hello à l’aide de Windows PowerShell si vous souhaitez toospecify une valeur d’un type différent. Si vous spécifiez **non défini**, puis hello la valeur de variable de hello sera définie trop**$null**, et vous devez affecter la valeur hello avec hello [Set-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913767.aspx) applet de commande ou **Set-AutomationVariable** activité.  Impossible de créer ou de modifier la valeur hello pour un type de variable complexe dans le portail de hello, mais vous pouvez fournir une valeur de tout type à l’aide de Windows PowerShell. Les types complexes sont retournés en tant que [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx).

Vous pouvez stocker plusieurs variable unique tooa de valeurs en créant un tableau ou une table de hachage et de l’enregistrement de toohello variable.

Hello Voici une liste des types de variables disponibles dans Automation :

* String
* Entier 
* DateTime
* Booléen
* Null

## <a name="cmdlets-and-workflow-activities"></a>Applets de commande et activités de workflow

applets de commande Hello Bonjour tableau suivant sont utilisée toocreate et gérer les variables Automation avec Windows PowerShell. Elles font partie de hello [module Azure PowerShell](../powershell-install-configure.md) qui est disponible pour une utilisation dans les runbooks d’automatisation et de configuration DSC.

|Applets de commande|Description|
|:---|:---|
|[Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx)|Récupère la valeur hello d’une variable existante.|
|[New-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx)|Crée une variable et définit sa valeur.|
|[Remove-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt619354.aspx)|Supprime une variable existante.|
|[Set-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603601.aspx)|Définit la valeur hello d’une variable existante.|

activités de flux de travail Hello Bonjour tableau suivant sont utilisées tooaccess variables Automation dans un runbook. Ils sont uniquement disponibles pour une utilisation dans un runbook ou la configuration DSC et ne sont pas fournis dans le cadre du module Azure PowerShell de hello.

|Activités de workflow|Description|
|:---|:---|
|Get-AutomationVariable|Récupère la valeur hello d’une variable existante.|
|Set-AutomationVariable|Définit la valeur hello d’une variable existante.|

> [!NOTE] 
> Vous devez éviter d’utiliser des variables dans hello : paramètre de nom de **Get-AutomationVariable** dans un runbook ou la configuration DSC, car cela complique la découverte des dépendances entre les procédures opérationnelles ou d’automatisation et de configuration DSC variables au moment du design.

## <a name="creating-a-new-automation-variable"></a>Création d'une variable Automation

### <a name="toocreate-a-new-variable-with-hello-azure-portal"></a>toocreate une nouvelle variable avec hello portail Azure

1. À partir de votre compte Automation, cliquez sur hello **actifs** vignette et puis sur hello **actifs** panneau, sélectionnez **Variables**.
2. Sur hello **Variables** vignette, sélectionnez **ajouter une variable**.
3. Choisissez les options de hello sur hello **nouvelle Variable** panneau, cliquez sur **créer** enregistrer hello nouvelle variable.

### <a name="toocreate-a-new-variable-with-windows-powershell"></a>toocreate une nouvelle variable avec Windows PowerShell

Hello [New-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx) applet de commande crée une variable et définit sa valeur initiale. Vous pouvez récupérer à l’aide de valeur hello [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx). Si la valeur de hello est un type simple, ce même type est retourné. S'il s'agit d'un type complexe, un **PSCustomObject** est retourné.

exemple de Hello suivant commandes indiquent comment toocreate une variable de type chaîne et puis de retourner sa valeur.

    New-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" 
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable' `
    –Encrypted $false –Value 'My String'
    $string = (Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable').Value

exemple de Hello suivant commandes indiquent comment toocreate une variable avec un type complexe de type, puis retourner ses propriétés. Dans ce cas, une machine virtuelle à partir de **Get-AzureRmVm** est utilisée.

    $vm = Get-AzureRmVm -ResourceGroupName "ResourceGroup01" –Name "VM01"
    New-AzureRmAutomationVariable –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable" –Encrypted $false –Value $vm
    
    $vmValue = (Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable").Value
    $vmName = $vmValue.Name
    $vmIpAddress = $vmValue.IpAddress



## <a name="using-a-variable-in-a-runbook-or-dsc-configuration"></a>Utilisation d’une variable dans un Runbook ou une configuration DSC

Hello d’utilisation **Set-AutomationVariable** valeur hello de tooset l’activité d’une variable Automation dans un runbook ou la configuration DSC et le hello **Get-AutomationVariable** tooretrieve il.  Vous ne devez pas utiliser hello **Set-AzureAutomationVariable** ou **Get-AzureAutomationVariable** applets de commande dans un runbook ou la configuration DSC, car elles sont moins efficaces que les activités de flux de travail hello.  Vous ne peut pas également récupérer la valeur hello de variables sécurisées avec **Get-AzureAutomationVariable**.  Hello uniquement moyen toocreate une variable à partir d’un runbook ou la configuration DSC est toouse hello [New-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913771.aspx) applet de commande.


### <a name="textual-runbook-samples"></a>Exemple de Runbooks textuels

#### <a name="setting-and-retrieving-a-simple-value-from-a-variable"></a>Définition et récupération d'une valeur simple à partir d'une variable

exemple de Hello suivant commandes indiquent comment tooset et récupérer une variable dans un runbook textuelle. Dans cet exemple, il est supposé que les variables de type entier nommées *NumberOfIterations* et *NumberOfRunnings* et une variable de type chaîne nommée *SampleMessage* ont déjà été créées.

    $NumberOfIterations = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfIterations'
    $NumberOfRunnings = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfRunnings'
    $SampleMessage = Get-AutomationVariable -Name 'SampleMessage'
    
    Write-Output "Runbook has been run $NumberOfRunnings times."
    
    for ($i = 1; $i -le $NumberOfIterations; $i++) {
       Write-Output "$i`: $SampleMessage"
    }
    Set-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" –Name NumberOfRunnings –Value ($NumberOfRunnings += 1)

#### <a name="setting-and-retrieving-a-complex-object-in-a-variable"></a>Définition et récupération d'un objet complexe dans une variable

exemple de Hello suivant de code montre comment tooupdate une variable avec une valeur complexe dans un runbook textuelle. Dans cet exemple, une machine virtuelle Azure est récupérée avec **Get-AzureVM** et tooan enregistré les variable Automation existante.  Comme expliqué dans [Types de variables](#variable-types), il est stocké comme PSCustomObject.

    $vm = Get-AzureVM -ServiceName "MyVM" -Name "MyVM"
    Set-AutomationVariable -Name "MyComplexVariable" -Value $vm


Bonjour suivant de code, les valeur de hello est extraite de la machine virtuelle de hello toostart variable et utilisé hello.

    $vmObject = Get-AutomationVariable -Name "MyComplexVariable"
    if ($vmObject.PowerState -eq 'Stopped') {
       Start-AzureVM -ServiceName $vmObject.ServiceName -Name $vmObject.Name
    }


#### <a name="setting-and-retrieving-a-collection-in-a-variable"></a>Définition et récupération d'une collection dans une variable

exemple de Hello suivant de code montre comment toouse une variable avec une collection de valeurs complexes dans un runbook textuels. Dans cet exemple, plusieurs machines virtuelles Azure sont récupérés avec **Get-AzureVM** et tooan enregistré les variable Automation existante.  Comme expliqué dans [Types de variables](#variable-types), elles sont stockées comme collection de PSCustomObject.

    $vms = Get-AzureVM | Where -FilterScript {$_.Name -match "my"}     
    Set-AutomationVariable -Name 'MyComplexVariable' -Value $vms

Bonjour suivant de code, collection de hello est extraite de la variable de hello et utilisé toostart chaque ordinateur virtuel.

    $vmValues = Get-AutomationVariable -Name "MyComplexVariable"
    ForEach ($vmValue in $vmValues)
    {
       if ($vmValue.PowerState -eq 'Stopped') {
          Start-AzureVM -ServiceName $vmValue.ServiceName -Name $vmValue.Name
       }
    }


### <a name="graphical-runbook-samples"></a>Exemples de Runbook graphiques

Dans un runbook graphique, vous ajoutez hello **Get-AutomationVariable** ou **Set-AutomationVariable** en cliquant sur variable hello dans le volet Bibliothèque de hello de l’éditeur graphique de hello et en sélectionnant hello activité de que votre choix.

![Ajoutez la variable toocanvas](media/automation-variables/runbook-variable-add-canvas.png)

#### <a name="setting-values-in-a-variable"></a>Définition de valeurs dans une variable
Hello image suivante montre exemple activités tooupdate une variable avec une valeur simple dans un runbook graphique. Dans cet exemple, une seule machine virtuelle Azure est récupérée avec **Get-AzureRmVM** et nom de l’ordinateur hello est enregistrée variable Automation existante de tooan avec un type de chaîne.  Peu importe si hello [lien est un pipeline ou une séquence](automation-graphical-authoring-intro.md#links-and-workflow) étant donné que nous n'espérons qu’un seul objet dans la sortie de hello.

![Définir une variable simple](media/automation-variables/runbook-set-simple-variable.png)

## <a name="next-steps"></a>Étapes suivantes

* toolearn en savoir plus sur les reliant les activités de création graphique, consultez [liens dans le graphique de création](automation-graphical-authoring-intro.md#links-and-workflow)
* tooget main runbooks graphiques, consultez [mon premier runbook graphique](automation-first-runbook-graphical.md) 

