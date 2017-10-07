---
title: "plans de toorecovery aaaAdd Azure automation procédures opérationnelles dans le portail classique de hello | Documents Microsoft"
description: "Cet article décrit la façon dont Azure Site Recovery vous permet désormais de tooextend les plans de récupération à l’aide des tâches complexes Azure Automation toocomplete pendant la récupération tooAzure"
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: f24eaa62-9dea-4fce-92e1-a72513ca0289
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: 3bb7420911afbce289b656f28823b1923e8af0c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-automation-runbooks-toorecovery-plans-in-hello-classic-portal"></a>Ajouter des plans de toorecovery runbooks Azure automation dans le portail classique de hello
Ce didacticiel explique comment Azure Site Recovery s’intègre à Azure Automation tooprovide extensibilité toorecovery plans. Récupération de vos machines virtuelles protégées à l’aide d’Azure Site Recovery pour la réplication toosecondary cloud et les scénarios de réplication tooAzure peuvent organiser les plans de récupération. Ils permettent également de restauration de hello **précis et constants**, **repeatable**, et **automatisée**. Si vous basculez sur votre tooAzure de machines virtuelles, intégration à Azure Automation étend les plans de récupération et vous offre la fonctionnalité tooexecute runbooks, ce qui permet des tâches d’automatisation puissantes.

Si vous n’avez pas encore entendu parler de Microsoft Azure Automation, connectez-vous [ici](https://azure.microsoft.com/services/automation/) et téléchargez [ici](https://azure.microsoft.com/documentation/scripts/) des exemples de scripts. En savoir plus sur [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) et comment tooorchestrate tooAzure de récupération à l’aide de la récupération des plans [ici](https://azure.microsoft.com/blog/?p=166264).

Dans ce bref didacticiel, nous allons voir comment intégrer des Runbooks Microsoft Azure dans des plans de récupération. Nous automatiser des tâches simples qui précédemment requis une intervention manuelle et voir comment tooconvert un multi étape de récupération dans une action de récupération d’un simple clic. Nous verrons également comment dépanner un script simple en cas de problème.

## <a name="protect-hello-application-tooazure"></a>Protéger hello application tooAzure
Commençons par une application simple, constituée de deux machines virtuelles. Voici l’application HRweb de Fabrikam. Fabrikam-HRweb-frontend et Fabrikam-Hrweb-principaux sont hello deux des ordinateurs virtuels protégés tooAzure à l’aide d’Azure Site Recovery. machines virtuelles de tooprotect hello à l’aide d’Azure Site Recovery, suivez les étapes de hello ci-dessous.

1. Activez la protection de vos machines virtuelles.
2. Assurez-vous que les machines virtuelles de hello ont terminé la réplication initiale et sont répliqués.
3. Attendez que hello la réplication initiale se termine et hello état de réplication est protégé.

## ![](media/site-recovery-runbook-automation/01.png)
Dans ce didacticiel, nous allons créer un plan de récupération pour hello Fabrikam HRweb application toofailover hello application tooAzure. Puis nous sera l’intégrer à un runbook qui créera un point de terminaison sur hello a échoué sur une machine virtuelle Azure tooserve des pages web sur le port 80.

Commençons par créer un plan de récupération pour notre application.

## <a name="create-hello-recovery-plan"></a>Créer le plan de récupération hello
toorecover hello application tooAzure, vous devez toocreate un plan de récupération.
À l’aide d’un plan de récupération que vous pouvez spécifier la commande hello de la récupération des ordinateurs virtuels. machine virtuelle de Hello placé dans le groupe 1 se récupérer démarrage initial et suivez de machine virtuelle de hello dans le groupe 2.

Créez un plan de récupération ressemblant à ce qui suit.

![](media/site-recovery-runbook-automation/12.png)

plus d’informations sur les plans de récupération, lisez la documentation de tooread [ici](https://msdn.microsoft.com/library/azure/dn788799.aspx "ici").

Ensuite, nous allons créer hello artefacts nécessaires dans Azure Automation.

## <a name="create-hello-automation-account-and-its-assets"></a>Créer le compte d’automatisation hello et ses composants
Vous avez besoin d’un runbook toocreate du compte Azure Automation. Si vous n’avez pas déjà un compte, accédez à onglet d’Automation tooAzure dénoté par ![](media/site-recovery-runbook-automation/02.png)et créer un nouveau compte.

1. Donner le compte de hello un tooidentify nom avec.
2. Spécifiez une région géographique dans laquelle vous souhaitez que le compte de hello de tooplace.

Il est recommandé de compte de hello tooplace Bonjour même région que le coffre hello ASR.

![](media/site-recovery-runbook-automation/03.png)

Ensuite, créez hello suivant actifs Bonjour compte.

### <a name="add-a-subscription-name-as-asset"></a>Ajouter un nom d’abonnement en tant que ressource
1. Ajouter un nouveau paramètre ![](media/site-recovery-runbook-automation/04.png) dans hello actifs d’automatisation Azure et sélectionnez trop![](media/site-recovery-runbook-automation/05.png)
2. Sélectionnez le type de variable hello en tant que **chaîne**
3. Spécifiez le nom de variable **AzureSubscriptionName**

   ![](media/site-recovery-runbook-automation/06.png)
4. Spécifiez le nom de votre abonnement Azure réel en tant que valeur de la variable hello.

   ![](media/site-recovery-runbook-automation/07_1.png)

Vous pouvez identifier le nom hello de votre abonnement à partir de la page des paramètres de votre compte sur hello portail Azure hello.

### <a name="add-an-azure-login-credential-as-asset"></a>Ajouter des informations d’identification de connexion Microsoft Azure en tant que ressources
Azure Automation utilise Azure PowerShell tooconnect toothe abonnement et fonctionne sur les artefacts hello il. Pour cela, vous devez vous authentifier à l’aide de votre compte Microsoft ou d’un compte professionnel ou scolaire.
Vous pouvez stocker des informations d’identification du compte hello dans un toobe asset utilisée en toute sécurité par hello runbook.

1. Ajouter un nouveau paramètre ![](media/site-recovery-runbook-automation/04.png) dans hello actifs d’automatisation Azure, puis sélectionnez![](media/site-recovery-runbook-automation/09.png)
2. Sélectionner le type d’informations d’identification hello en tant que **informations d’identification de Windows PowerShell**
3. Nommez hello **AzureCredential**

   ![](media/site-recovery-runbook-automation/10.png)
4. Spécifiez le nom d’utilisateur hello et un mot de passe toosign à l’aide de.

Désormais, ces deux paramètres sont disponibles dans vos ressources.

![](media/site-recovery-runbook-automation/11.png)

Plus d’informations sur comment abonnement de tooyour tooconnect via PowerShell est donné [ici](/powershell/azure/overview).

Ensuite, vous allez créer un runbook dans Azure Automation que vous pouvez ajouter un point de terminaison pour la machine virtuelle frontal de hello après le basculement.

## <a name="azure-automation-context"></a>Contexte Microsoft Automation
ASR transmet un toohelp de runbook de variable toohello de contexte vous écrivez des scripts déterministes. Disent que noms hello de hello Service Cloud et hello Machine virtuelle sont prévisibles, mais se produit qu’il n’est pas toujours les cas de hello en raison de toocertain scénarios hello une où nom hello du nom d’ordinateur virtuel hello peut avoir modifié en raison d' caractères toounsupported dans Azure. Par conséquent, cette information est transmise de plan de récupération toohello ASR dans le cadre de hello *contexte*.

Voici un exemple de l’aspect de la variable de contexte hello.

        {"RecoveryPlanName":"hrweb-recovery",

        "FailoverType":"Test",

        "FailoverDirection":"PrimaryToSecondary",

        "GroupId":"1",

        "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                {"CloudServiceName":"pod02hrweb-Chicago-test",

                "RoleName":"Fabrikam-Hrweb-frontend-test"}

                }

        }


tableau Hello ci-dessous contient le nom et une description pour chaque variable dans le contexte de hello.

| **Nom de la variable** | **Description** |
| --- | --- |
| RecoveryPlanName |Nom du plan en cours d'exécution. Vous aide à vous entreprendre une action basée sur l’utilisation de nom hello même script |
| FailoverType |Spécifie si hello basculement test, planifié ou non. |
| FailoverDirection |Spécifiez si la récupération est tooprimary ou la base de données secondaire |
| GroupID |Identifier le numéro de groupe hello dans le plan de récupération hello lorsque le plan de hello est en cours d’exécution. |
| VmMap |Tableau de tous les ordinateurs virtuels hello dans le groupe de hello |
| Clé VMMap |Clé unique (GUID) pour chaque machine virtuelle. Il a hello identique hello ID VMM de machine virtuelle de hello, le cas échéant. |
| RoleName |Nom de machine virtuelle Azure qui est en cours de récupération de hello |
| CloudServiceName |Nom du Service Cloud Azure sous le hello machine virtuelle est créée. |

tooidentify hello VmMap Key dans le contexte de hello, vous pouvez également atteindre la page de propriétés de machine virtuelle toohello dans ASR et examinez hello propriété VM GUID.

![](media/site-recovery-runbook-automation/13.png)

## <a name="author-an-automation-runbook"></a>Créer un Runbook Automation
Créer maintenant hello runbook tooopen port80 sur l’ordinateur virtuel frontal de hello.

1. Créer un runbook Bonjour compte Azure Automation avec le nom de hello **OpenPort80**

   ![](media/site-recovery-runbook-automation/14.png)
2. Accédez toohello vue auteur de runbook de hello et entrer en mode brouillon hello.
3. Tout d’abord spécifier toouse de variable hello comme contexte de plan de récupération hello

   ```
       param (
           [Object]$RecoveryPlanContext
       )

   ```
4. Prochaine connexion abonnement toohello à l’aide du nom d’abonnement et les informations d’identification hello

   ```
       $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

       # Connect tooAzure
       $AzureAccount = Add-AzureAccount -Credential $Cred
       $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
       Select-AzureSubscription -SubscriptionName $AzureSubscriptionName
   ```

   Notez que vous utilisez hello Azure actifs – **AzureCredential** et **AzureSubscriptionName** ici.
5. Maintenant, spécifiez les détails du point de terminaison hello et hello GUID de l’ordinateur virtuel de hello pour lequel vous souhaitez le point de terminaison tooexpose hello. Dans cet ordinateur virtuel frontal de cas hello.

   ```
       # Specify hello parameters toobe used by hello script
       $AEProtocol = "TCP"
       $AELocalPort = 80
       $AEPublicPort = 80
       $AEName = "Port 80 for HTTP"
       $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"
   ```

   Cela indique hello protocole de point de terminaison Azure, port local sur la machine virtuelle de hello et son port public mappé. Ces variables sont les paramètres requis par hello commandes Azure qui ajoutent des points de terminaison tooVMs. Hello VMGUID conserve hello GUID de l’ordinateur virtuel de hello sur que vous devez toooperate.
6. script de Hello maintenant extraire contexte hello pour hello donné VM GUID et créer un point de terminaison sur l’ordinateur virtuel de hello référencée par lui.

   ```
       #Read hello VM GUID from hello context
       $VM = $RecoveryPlanContext.VmMap.$VMGUID

       if ($VM -ne $null)
       {
           # Invoke pipeline commands within an InlineScript

           $EndpointStatus = InlineScript {
               # Invoke hello necessary pipeline commands tooadd a Azure Endpoint tooa specified Virtual Machine
               # Commands include: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including parameters)

               $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                   Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                   Update-AzureVM
               Write-Output $Status
           }
       }
   ```
7. Une fois cette opération terminée, atteint publier ![](media/site-recovery-runbook-automation/20.png) tooallow votre toobe script disponible pour l’exécution.

script complet de Hello est donné ci-dessous pour des références

```
  workflow OpenPort80
  {
    param (
        [Object]$RecoveryPlanContext
    )

    $Cred = Get-AutomationPSCredential -Name 'AzureCredential'

    # Connect tooAzure
    $AzureAccount = Add-AzureAccount -Credential $Cred
    $AzureSubscriptionName = Get-AutomationVariable –Name ‘AzureSubscriptionName’
    Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

    # Specify hello parameters toobe used by hello script
    $AEProtocol = "TCP"
    $AELocalPort = 80
    $AEPublicPort = 80
    $AEName = "Port 80 for HTTP"
    $VMGUID = "7a1069c6-c1d6-49c5-8c5d-33bfce8dd183"

    #Read hello VM GUID from hello context
    $VM = $RecoveryPlanContext.VmMap.$VMGUID

    if ($VM -ne $null)
    {
        # Invoke pipeline commands within an InlineScript

        $EndpointStatus = InlineScript {
            # Invoke hello necessary pipeline commands tooadd an Azure Endpoint tooa specified Virtual Machine
            # This set of commands includes: Get-AzureVM | Add-AzureEndpoint | Update-AzureVM (including necessary parameters)

            $Status = Get-AzureVM -ServiceName $Using:VM.CloudServiceName -Name $Using:VM.RoleName | `
                Add-AzureEndpoint -Name $Using:AEName -Protocol $Using:AEProtocol -PublicPort $Using:AEPublicPort -LocalPort $Using:AELocalPort | `
                Update-AzureVM
            Write-Output $Status
        }
    }
  }
```

## <a name="add-hello-script-toohello-recovery-plan"></a>Ajouter un plan de récupération hello script toohello
Une fois le script de hello est prêt, vous pouvez l’ajouter plan de récupération toohello que vous avez créé précédemment.

1. Dans le plan de récupération hello que vous avez créé, choisissez tooadd un script après le groupe 2. ![](media/site-recovery-runbook-automation/15.png)
2. Spécifiez un nom de script. Il s’agit simplement d’un nom convivial pour ce script pour l’affichage dans le plan de récupération hello.
3. Dans le script de hello basculement tooAzure – sélectionnez le nom de compte Azure Automation hello.
4. Hello Runbooks d’Azure, sélectionnez runbook hello que vous avez créés.

![](media/site-recovery-runbook-automation/16.png)

## <a name="primary-side-scripts"></a>Scripts côté principal
Lorsque vous exécutez un tooAzure de basculement, vous pouvez également choisir tooexecute scripts du côté primaire. Ces scripts s’exécutent sur le serveur VMM de hello pendant le basculement.
Les scripts côté principal ne sont disponibles que pour les phases précédant et suivant l’arrêt. Il s’agit, car nous pensons que hello site principal toobe généralement pas disponible lorsqu’un incident ne survienne.
Pendant un basculement non planifié, uniquement si vous choisissez cette option pour les opérations de site principal, il tente les scripts côté principal toorun hello. Si elles ne sont pas accessibles ou continuera de délai d’attente, hello basculement toorecover hello des machines virtuelles.
Les scripts côté principal sont non disponibles pour les Sites de VMware/physiques/Hyper-v sans tooAzure VMM protégé - tout en vous tooAzure de basculement.
Toutefois, lorsque la restauration automatique à partir d’Azure tooon local, les scripts côté principal (Runbooks) peut servir pour toutes les cibles à l’exception de VMware.

## <a name="test-hello-recovery-plan"></a>Plan de récupération test hello
Une fois que vous avez ajouté le plan de toohello hello runbook, vous pouvez lancer un test de basculement et voir en action. Il est toujours recommandé toorun un tootest de basculement de test de votre tooensure plan de récupération d’application et hello qu’il n’y a aucune erreur.

1. Sélectionnez le plan de récupération hello et lancer un test de basculement.
2. Pendant l’exécution de plan hello, vous pouvez voir si hello runbook a été exécutée ou non par l’intermédiaire de son état.

   ![](media/site-recovery-runbook-automation/17.png)
3. Vous pouvez également voir hello l’état de l’exécution de runbook sur page de tâches Azure Automation hello pour hello runbook détaillé.

   ![](media/site-recovery-runbook-automation/18.png)
4. Une fois hello basculement terminé, indépendamment des résultats de l’exécution de runbook hello, vous pouvez voir si l’exécution de hello a réussi ou non en visitant la page de machine virtuelle Azure hello et en examinant les points de terminaison hello.

![](media/site-recovery-runbook-automation/19.png)

## <a name="sample-scripts"></a>Exemples de scripts
Pendant que nous avons passé en revue une automatisation couramment utilisé de tâche d’ajout d’un point de terminaison de tooan machine virtuelle Azure dans ce didacticiel, vous pourriez effectuer plusieurs autres tâches d’automatisation puissantes à l’aide d’Azure automation. Microsoft et hello Communauté d’Azure Automation fournissent des exemples de runbooks qui peuvent vous aider à commencer à créer vos propres solutions et les runbooks d’utilitaire, que vous pouvez utiliser comme blocs de construction de plus grandes tâches d’automatisation. Commencer à les utiliser à partir de la galerie de hello et créer des plans de récupération d’un seul clic puissantes pour vos applications à l’aide d’Azure Site Recovery.

## <a name="additional-resources"></a>Ressources supplémentaires
[Vue d’ensemble de Microsoft Azure Automation](http://msdn.microsoft.com/library/azure/dn643629.aspx "Vue d’ensemble de Microsoft Azure Automation")

[Exemples de scripts Microsoft Azure Automation](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Exemples de scripts Microsoft Azure Automation")
