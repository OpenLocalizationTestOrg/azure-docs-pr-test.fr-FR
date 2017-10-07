---
title: "les paramètres d’entrée aaaRunbook | Documents Microsoft"
description: "Paramètres d’entrée du Runbook augmentent la flexibilité hello des procédures opérationnelles en vous toopass données tooa runbook lorsqu’il est démarré. Cet article décrit différents cas où des paramètres d’entrée sont utilisés dans des Runbooks."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 4d3dff2c-1f55-498d-9a0e-eee497e5bedb
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/11/2016
ms.author: sngun
ms.openlocfilehash: f3abaf92382e7d41019616bafb14af23cf98dd9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-input-parameters"></a>Paramètres d’entrée de Runbook
Paramètres d’entrée du Runbook augmentent la flexibilité hello des procédures opérationnelles en vous toopass données tooit lorsqu’il est démarré. Hello autorise hello runbook actions toobe ciblé pour des environnements et des scénarios spécifiques. Cet article vous guide dans différents scénarios où des paramètres d’entrée sont utilisés dans des Runbooks.

## <a name="configure-input-parameters"></a>Configurer les paramètres d’entrée
Des paramètres d’entrée peuvent être configurés dans des Runbooks PowerShell, PowerShell Workflow et graphiques. Un Runbook peut avoir plusieurs paramètres avec différents types de données, ou aucun paramètre. Des paramètres d’entrée peuvent être obligatoires ou facultatifs, et vous pouvez affecter une valeur par défaut à des paramètres facultatifs. Vous pouvez assigner des valeurs toohello des paramètres d’entrée d’un runbook lorsque vous le démarrez via une des méthodes disponibles de hello. Ces méthodes incluent le démarrage d’un runbook à partir de portail de hello ou un service web. Vous pouvez également démarrer un Runbook en tant que Runbook enfant appelé en ligne dans un autre Runbook.

## <a name="configure-input-parameters-in-powershell-and-powershell-workflow-runbooks"></a>Configurer les paramètres d’entrée dans des Runbooks PowerShell et PowerShell Workflow
PowerShell et [les runbooks PowerShell Workflow](automation-first-runbook-textual.md) dans Azure Automation prend en charge les paramètres d’entrée qui sont définis via hello suivant des attributs.  

| **Propriété** | **Description** |
|:--- |:--- |
| Type |Obligatoire. type de données Hello attendu pour la valeur du paramètre hello. Tout type .NET est valide. |
| Nom |Obligatoire. nom de Hello du paramètre hello. Cela doit être unique au sein de hello runbook et peut contenir uniquement des lettres, des chiffres ou traits de soulignement. et doit commencer par une lettre. |
| Obligatoire |facultatif. Spécifie si une valeur doit être fournie pour le paramètre hello. Si vous affectez ce trop**$true**, puis une valeur doit être fournie au démarrage hello runbook. Si vous affectez ce trop**$false**, puis une valeur est facultative. |
| Valeur par défaut |facultatif.  Spécifie une valeur qui sera utilisée pour le paramètre hello si une valeur n’est pas transmise au démarrage hello runbook. Une valeur par défaut peut être définie pour n’importe quel paramètre et est automatiquement apportées par paramètre hello facultatif, quelle que soit le paramètre obligatoire de hello. |

Windows PowerShell prend en charge d’autres attributs de paramètres d’entrée que ceux répertoriés ici, tels que la validation, les alias et les jeux de paramètres. Toutefois, Azure Automation prend actuellement en charge uniquement hello paramètres d’entrée répertoriées ci-dessus.

Une définition de paramètre dans les runbooks PowerShell Workflow a hello suivant la forme générale, où plusieurs paramètres sont séparés par des virgules.

   ```
     Param
     (
         [Parameter (Mandatory= $true/$false)]
         [Type] Name1 = <Default value>,

         [Parameter (Mandatory= $true/$false)]
         [Type] Name2 = <Default value>
     )
   ```

> [!NOTE]
> Lorsque vous définissez les paramètres, si vous ne spécifiez pas hello **obligatoire** d’attribut, par défaut, paramètre hello est considéré comme facultatif. En outre, si vous définissez une valeur par défaut pour un paramètre dans les runbooks PowerShell Workflow, il est considéré par PowerShell comme paramètre facultatif, quel que soit hello **obligatoire** valeur d’attribut.
> 
> 

Par exemple, permet de configurer les paramètres d’entrée hello pour un runbook PowerShell Workflow qui génère plus d’informations sur les ordinateurs virtuels, une seule machine virtuelle ou sur toutes les machines virtuelles au sein d’un groupe de ressources. Ce runbook possède deux paramètres comme indiqué dans hello suivant capture d’écran : nom hello de machine virtuelle et le nom hello hello du groupe de ressources.

![PowerShell Workflow d’Automation](media/automation-runbook-input-parameters/automation-01-powershellworkflow.png)

Dans cette définition de paramètre, hello paramètres **$VMName** et **$resourceGroupName** sont des paramètres simples de type chaîne. Toutefois, les Runbooks PowerShell et PowerShell Workflow prennent en charge tous les types, simples et complexes, tels que **object** ou **PSCredential** pour les paramètres d’entrée.

Si votre runbook possède un paramètre d’entrée de type objet, puis utiliser une table de hachage PowerShell avec (nom, valeur) paires toopass dans une valeur. Par exemple, si vous avez hello suit le paramètre dans un runbook :

     [Parameter (Mandatory = $true)]
     [object] $FullName

Vous pouvez passer hello suit valeur toohello paramètre :

    @{"FirstName"="Joe";"MiddleName"="Bob";"LastName"="Smith"}


## <a name="configure-input-parameters-in-graphical-runbooks"></a>Configurer des paramètres d’entrée dans des Runbooks graphiques
trop[configurer un runbook graphique](automation-first-runbook-graphical.md) avec des paramètres d’entrée, nous allons créer un runbook graphique qui renvoie les détails sur les machines virtuelles, soit une seule machine virtuelle ou tous les ordinateurs virtuels au sein d’un groupe de ressources. La configuration d'un Runbook implique deux activités principales, comme décrit ci-dessous.

[**Authentifier les procédures opérationnelles compte d’identification Azure** ](automation-sec-configure-azure-runas-account.md) tooauthenticate avec Azure.

[**Get-AzureRmVm** ](https://msdn.microsoft.com/library/mt603718.aspx) tooget les propriétés de hello d’une machine virtuelle.

Vous pouvez utiliser hello [ **Write-Output** ](https://technet.microsoft.com/library/hh849921.aspx) noms de hello toooutput activité des ordinateurs virtuels. Hello activité **Get-AzureRmVm** accepte deux paramètres, hello **nom de machine virtuelle** et hello **nom de groupe de ressources**. Étant donné que ces paramètres peut nécessiter des valeurs différentes à chaque fois que vous démarrez hello runbook, vous pouvez ajouter des paramètres d’entrée tooyour runbook. Voici les paramètres d’entrée de hello étapes tooadd :

1. Sélectionnez hello runbook graphique de hello **Runbooks** panneau, puis cliquez sur [ **modifier** ](automation-graphical-authoring-intro.md) il.
2. À partir de l’éditeur de runbook hello, cliquez sur **d’entrée et de sortie** tooopen hello **d’entrée et de sortie** panneau.
   
    ![Runbook graphique d’Automation](media/automation-runbook-input-parameters/automation-02-graphical-runbok-editor.png)
3. Hello **d’entrée et de sortie** panneau affiche la liste des paramètres d’entrée qui sont définis pour les runbook hello. Dans ce panneau, vous pouvez ajouter un nouveau paramètre d’entrée ou modifier la configuration de hello d’un paramètre d’entrée existant. tooadd un nouveau paramètre hello runbook, cliquez sur **Ajout de l’entrée** tooopen hello **paramètre d’entrée du Runbook** panneau. Là, vous pouvez configurer hello paramètres suivants :
   
   | **Propriété** | **Description** |
   |:--- |:--- |
   | Nom |Obligatoire.  nom de Hello du paramètre hello. Cela doit être unique au sein de hello runbook et peut contenir uniquement des lettres, des chiffres ou traits de soulignement. et doit commencer par une lettre. |
   | Description |facultatif. Description de l’objectif de hello du paramètre d’entrée. |
   | Type |facultatif. type de données de Hello est attendu pour la valeur du paramètre hello. Les types de paramètres pris en charge sont **String**, **Int32**, **Int64**, **Decimal**, **Boolean**, **DateTime** et **Object**. Si un type de données n’est pas sélectionné, la valeur par défaut trop**chaîne**. |
   | Obligatoire |facultatif. Spécifie si une valeur doit être fournie pour le paramètre hello. Si vous choisissez **Oui**, puis une valeur doit être fournie au démarrage hello runbook. Si vous choisissez **aucune**, puis une valeur n’est pas requise lorsque hello runbook est démarré, et une valeur par défaut peut être définie. |
   | Valeur par défaut |facultatif. Spécifie une valeur qui sera utilisée pour le paramètre hello si une valeur n’est pas transmise au démarrage hello runbook. Une valeur par défaut peut être définie pour un paramètre qui n’est pas obligatoire. tooset une valeur par défaut, choisissez **personnalisé**. Cette valeur est utilisée, sauf si une autre valeur est fournie au démarrage hello runbook. Choisissez **aucun** si vous ne souhaitez pas tooprovide une valeur par défaut. |
   
    ![Ajouter une nouvelle entrée](media/automation-runbook-input-parameters/automation-runbook-input-parameter-new.png)
4. Créer les deux paramètres avec hello propriétés qui seront utilisées par hello suivantes **Get-AzureRmVm** activité :
   
   * **Paramètre 1 :**
     
     * Nom - VMName
     * Type : Chaîne
     * Obligatoire : Non
   * **Paramètre 2 :**
     
     * Nom : resourceGroupName
     * Type : Chaîne
     * Obligatoire : Non
     * Valeur par défaut : Personnalisé
     * Valeur par défaut personnalisée - \<nom hello du groupe de ressources qui contient des machines virtuelles de hello >
5. Une fois que vous ajoutez des paramètres de hello, cliquez sur **OK**.  Vous pouvez désormais afficher Bonjour **entrée et sortie lame**. Cliquez de nouveau sur **OK**, puis sur **Enregistrer** et **Publier** pour publier votre Runbook.

## <a name="assign-values-tooinput-parameters-in-runbooks"></a>Affecter des valeurs tooinput des paramètres dans les runbooks
Vous pouvez passer des valeurs tooinput paramètres dans des procédures opérationnelles dans les scénarios suivants de hello.

### <a name="start-a-runbook-and-assign-parameters"></a>Démarrer un Runbook et affecter des paramètres
Un runbook peut être démarré de plusieurs façons : via hello portail Azure, avec un webhook, avec les applets de commande PowerShell, hello API REST ou avec le Kit de développement logiciel de hello. Nous abordons ci-dessous différentes méthodes pour démarrer un Runbook et affecter des paramètres.

#### <a name="start-a-published-runbook-by-using-hello-azure-portal-and-assign-parameters"></a>Démarrer un runbook publié à l’aide de hello portail Azure et affecter des paramètres
Lorsque vous [démarrer hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), hello **démarrer le Runbook** panneau s’ouvre et vous pouvez configurer les valeurs des paramètres hello que vous venez de créer.

![Démarrer à l’aide du portail de hello](media/automation-runbook-input-parameters/automation-04-startrunbookusingportal.png)

Dans l’étiquette de hello sous la zone d’entrée de hello, vous pouvez voir les attributs hello qui ont été définies pour le paramètre hello. Les attributs incluent Obligatoire ou Facultatif, Type et Valeur par défaut. Dans hello aide bulle suivant toohello nom du paramètre, vous pouvez voir toutes les informations de clé hello vous devez toomake des décisions sur les valeurs de paramètre d’entrée. Ces informations indiquent si un paramètre est obligatoire ou facultatif. Il inclut également le type de hello et la valeur par défaut (le cas échéant) et autres notes utiles.

![Bulle d'aide](media/automation-runbook-input-parameters/automation-05-helpbaloon.png)

> [!NOTE]
> Les paramètres de type String prennent en charge les valeurs de chaîne **vides** .  Saisie **[EmptyString]** dans le paramètre d’entrée hello zone passe un paramètre de toohello une chaîne vide. De même, les paramètres de type String ne prennent pas en charge la transmission de valeurs **Null** . Si vous ne transmettez pas n’importe quel paramètre de chaîne de valeur toohello, puis PowerShell interprète la valeur null.
> 
> 

#### <a name="start-a-published-runbook-by-using-powershell-cmdlets-and-assign-parameters"></a>Démarrer un Runbook publié à l’aide d’applets de commande PowerShell et affecter des paramètres
* **Applets de commande d’Azure Resource Manager :** vous pouvez démarrer un Runbook Automation créé dans un groupe de ressources à l’aide de l’applet de commande [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).
  
  **Exemple :**
  
  ```
  $params = @{“VMName”=”WSVMClassic”;”resourceGroupeName”=”WSVMClassicSG”}
  
  Start-AzureRmAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” –ResourceGroupName $resourceGroupName -Parameters $params
  ```
* **Applets de commande de gestion des services Azure :** vous pouvez démarrer un Runbook Automation créé dans un groupe de ressources par défaut à l’aide de l’applet de commande [Start-AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx).
  
  **Exemple :**
  
  ```
  $params = @{“VMName”=”WSVMClassic”; ”ServiceName”=”WSVMClassicSG”}
  
  Start-AzureAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” -Parameters $params
  ```

> [!NOTE]
> Lorsque vous démarrez un runbook à l’aide des applets de commande PowerShell, un paramètre par défaut, **MicrosoftApplicationManagementStartedBy** est créée avec la valeur de hello **PowerShell**. Vous pouvez afficher ce paramètre Bonjour **détails de la tâche** panneau.  
> 
> 

#### <a name="start-a-runbook-by-using-an-sdk-and-assign-parameters"></a>Démarrer un Runbook à l’aide d’un Kit de développement logiciel (SDK) et affecter des paramètres
* **Méthode de gestionnaire de ressources Azure :** vous pouvez démarrer un runbook à l’aide du Kit de développement logiciel d’un langage de programmation de hello. Voici un extrait de code C# permettant de démarrer un Runbook dans votre compte Automation. Vous pouvez afficher tout code hello à notre [référentiel GitHub](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).  
  
  ```
   public Job StartRunbook(string runbookName, IDictionary<string, string> parameters = null)
      {
        var response = AutomationClient.Jobs.Create(resourceGroupName, automationAccount, new JobCreateParameters
         {
            Properties = new JobCreateProperties
             {
                Runbook = new RunbookAssociationProperty
                 {
                   Name = runbookName
                 },
                   Parameters = parameters
             }
         });
      return response.Job;
      }
  ```
* **Méthode de gestion des services Azure :** vous pouvez démarrer un runbook à l’aide du Kit de développement logiciel d’un langage de programmation de hello. Voici un extrait de code C# permettant de démarrer un Runbook dans votre compte Automation. Vous pouvez afficher tout code hello à notre [référentiel GitHub](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).
  
  ```      
  public Job StartRunbook(string runbookName, IDictionary<string, string> parameters = null)
    {
      var response = AutomationClient.Jobs.Create(automationAccount, new JobCreateParameters
    {
      Properties = new JobCreateProperties
         {
           Runbook = new RunbookAssociationProperty
         {
           Name = runbookName
              },
                Parameters = parameters
              }
       });
      return response.Job;
    }
  ```
  
  toostart cette méthode, créez un Bonjour toostore de dictionnaire des paramètres de runbook, **VMName** et **resourceGroupName**et leurs valeurs. Ensuite, démarrez runbook de hello. Voici hello c# extrait de code pour appeler la méthode hello définie ci-dessus.
  
  ```
  IDictionary<string, string> RunbookParameters = new Dictionary<string, string>();
  
  // Add parameters toohello dictionary.
  RunbookParameters.Add("VMName", "WSVMClassic");
  RunbookParameters.Add("resourceGroupName", "WSSC1");
  
  //Call hello StartRunbook method with parameters
  StartRunbook(“Get-AzureVMGraphical”, RunbookParameters);
  ```

#### <a name="start-a-runbook-by-using-hello-rest-api-and-assign-parameters"></a>Démarrer un runbook à l’aide des API REST de hello et affecter des paramètres
Une tâche de runbook peut être créée et démarrée par hello les API REST Azure Automation à l’aide de hello **PUT** URI de demande de méthode avec hello suivant.

    https://management.core.windows.net/<subscription-id>/cloudServices/<cloud-service-name>/resources/automation/~/automationAccounts/<automation-account-name>/jobs/<job-id>?api-version=2014-12-08`

Dans l’URI de la demande hello, remplacez hello paramètres suivants :

* **subscription-id** : ID de votre abonnement Azure.  
* **nom du service de cloud :** nom hello de demande de hello toowhich hello cloud service doit être envoyé.  
* **Automation-account-name :** hello le nom de votre compte automation qui est hébergé dans hello spécifié service cloud.  
* **id de tâche :** hello GUID pour le travail de hello. GUID dans PowerShell peut être créés à l’aide de hello **[GUID] ::NewGuid(). ToString()** commande.

Dans la tâche de runbook toohello commande toopass paramètres, utilisez le corps de requête de hello. Il prend hello deux propriétés fournies au format JSON suivantes :

* **Runbook Name :** obligatoire. nom de Hello du runbook de hello pour hello travail toostart.  
* **Runbook Parameters :** facultatif. Un dictionnaire de liste des paramètres hello (nom, valeur) format où nom doit être de type String et de valeur peut être toute valeur JSON valide.

Si vous souhaitez toostart hello **Get-AzureVMTextual** runbook qui a été créé précédemment avec **VMName** et **resourceGroupName** en tant que paramètres, utilisez hello suivant le format JSON pour le corps de demande hello.

   ```
    {
      "properties":{
        "runbook":{
        "name":"Get-AzureVMTextual"},
      "parameters":{
         "VMName":"WSVMClassic",
         "resourceGroupName":”WSCS1”}
        }
    }
   ```

Un code d’état HTTP 201 est retourné si le travail de hello est créé avec succès. Pour plus d’informations sur les en-têtes de réponse et corps de réponse hello, reportez-vous à l’article de toohello sur la façon trop[créer une tâche de runbook à l’aide des API REST de hello.](https://msdn.microsoft.com/library/azure/mt163849.aspx)

### <a name="test-a-runbook-and-assign-parameters"></a>Tester un Runbook et affecter des paramètres
Lorsque vous [brouillon hello de test de votre runbook](automation-testing-runbook.md) en utilisant l’option de test hello, hello **Test** panneau s’ouvre et vous pouvez configurer les valeurs des paramètres hello que vous venez de créer.

![Tester et affecter des paramètres](media/automation-runbook-input-parameters/automation-06-testandassignparameters.png)

### <a name="link-a-schedule-tooa-runbook-and-assign-parameters"></a>Liez un runbook tooa de planification et d’affecter des paramètres
Vous pouvez [lier une planification](automation-schedules.md) tooyour runbook afin que runbook hello commence à une heure spécifique. Pour affecter des paramètres d’entrée lorsque vous créez la planification de hello, et hello runbook utilise ces valeurs lorsqu’il est démarré par la planification de hello. Impossible d’enregistrer la planification de hello jusqu'à ce que toutes les valeurs de paramètre obligatoires sont fournies.

![Planifier et affecter des paramètres](media/automation-runbook-input-parameters/automation-07-scheduleandassignparameters.png)

### <a name="create-a-webhook-for-a-runbook-and-assign-parameters"></a>Créer un WebHook pour un Runbook et affecter des paramètres
Vous pouvez créer un [WebHook](automation-webhooks.md) pour votre Runbook, puis configurer les paramètres d’entrée de celui-ci. Impossible d’enregistrer hello webhook jusqu'à ce que toutes les valeurs de paramètre obligatoires sont fournies.

![Créer un WebHook et affecter des paramètres](media/automation-runbook-input-parameters/automation-08-createwebhookandassignparameters.png)

Lorsque vous exécutez un runbook à l’aide d’un webhook, hello prédéfinis de paramètre d’entrée  **[Webhookdata](automation-webhooks.md#details-of-a-webhook)**  est envoyé, ainsi que les paramètres d’entrée hello que vous avez définie. Vous pouvez cliquer sur tooexpand hello **WebhookData** paramètre pour plus de détails.

![Paramètre WebhookData](media/automation-runbook-input-parameters/automation-09-webhook-data-parameters.png)

## <a name="next-steps"></a>Étapes suivantes
* Pour plus d’informations sur l’entrée et la sortie du Runbook, voir [Azure Automation : entrée et sortie de Runbook, et Runbook imbriqués](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/)
* Pour plus d’informations sur les différentes façons toostart un runbook, consultez [démarrage d’un runbook](automation-starting-a-runbook.md).
* tooedit un runbook textuels, consultez trop[modification des procédures opérationnelles textuelle](automation-edit-textual-runbook.md).
* tooedit un runbook graphique, consultez trop[de création graphique dans Azure Automation](automation-graphical-authoring-intro.md).

