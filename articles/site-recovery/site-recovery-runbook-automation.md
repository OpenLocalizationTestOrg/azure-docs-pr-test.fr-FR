---
title: plans de toorecovery runbooks aaaAdd Azure Automation dans Azure Site Recovery | Documents Microsoft
description: "Découvrez comment Azure Site Recovery peut vous aider à étendre des plans de récupération à l’aide d’Azure Automation. Découvrez comment toocomplete complexe tâches pendant la récupération tooAzure."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: ecece14d-5f92-4596-bbaf-5204addb95c2
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/23/2017
ms.author: ruturajd@microsoft.com
ms.openlocfilehash: 90d517200cec5527e98a0d00da466bace587b70b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-automation-runbooks-toorecovery-plans"></a>Ajouter des plans de toorecovery runbooks Azure Automation
Dans cet article, nous décrivons comment Azure Site Recovery s’intègre à Azure Automation toohelp vous étendez vos plans de récupération. Des plans de récupération peuvent orchestrer la récupération de machines virtuelles protégées par Site Recovery. Plans de récupération fonctionnent aussi bien pour le cloud secondaire tooa de réplication et tooAzure de réplication. Plans de récupération également aider à effectuer la récupération de hello **précis et constants**, **repeatable**, et **automatisée**. Si vous basculez votre tooAzure de machines virtuelles, l’intégration avec Azure Automation étend vos plans de récupération. Vous pouvez l’utiliser tooexecute runbooks, qui offrent des tâches d’automatisation puissantes.

Si vous êtes de nouveau tooAzure Automation, vous pouvez [inscrire](https://azure.microsoft.com/services/automation/) et [télécharger des exemples de scripts](https://azure.microsoft.com/documentation/scripts/). Pour plus d’informations, toolearn comment tooAzure de récupération tooorchestrate à l’aide de [plans de récupération](https://azure.microsoft.com/blog/?p=166264), consultez [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/).

Cet article explique comment intégrer des runbooks Azure Automation dans vos plans de récupération. Nous utilisons des exemples tooautomate tâches de base qui nécessitaient auparavant une intervention manuelle. Nous expliquons également comment tooconvert un tooa de récupération en plusieurs étapes par simple clic action de récupération.

## <a name="customize-hello-recovery-plan"></a>Personnaliser le plan de récupération hello
1. Accédez toohello **Site Recovery** panneau des ressources plan de récupération. Pour cet exemple, le plan de récupération hello a deux tooit ajouté machines virtuelles pour la récupération. toobegin Ajout d’un runbook, cliquez sur hello **personnaliser** onglet.

    ![Cliquez sur le bouton de personnaliser hello](media/site-recovery-runbook-automation-new/essentials-rp.png)


2. Cliquez avec le bouton droit sur **Group 1: Start**, puis sélectionnez **Ajouter une action postérieure**.

    ![Cliquer avec le bouton droit sur Group 1: Start, puis ajouter une action postérieure](media/site-recovery-runbook-automation-new/customize-rp.png)

3. Cliquez sur **Choisir un script**.

4. Sur hello **action mettre à jour** panneau, le script de nom hello **Hello World**.

    ![panneau d’action Hello mise à jour](media/site-recovery-runbook-automation-new/update-rp.png)

5. Choisissez un nom de compte Automation.
    >[!NOTE]
    > Hello compte Automation peut être dans n’importe quelle région Azure. Hello compte Automation doit être Bonjour même abonnement que le coffre Azure Site Recovery hello.

6. Dans votre compte Automation, sélectionnez un runbook. Ce runbook est hello du script qui s’exécute pendant l’exécution de hello hello du plan de récupération, après la récupération hello du premier groupe de hello.

7. script de hello toosave, cliquez sur **OK**. script de Hello est ajouté trop**groupe 1 : POST-étapes**.

    ![Action postérieure Group 1:Start](media/site-recovery-runbook-automation-new/addedscript-rp.PNG)


## <a name="considerations-for-adding-a-script"></a>Considérations relatives à l’ajout d’un script

* Pour les options trop**supprimer une étape** ou **mettre à jour hello script**, avec le bouton droit de script de hello.
* Un script peut s’exécuter sur Azure pendant le basculement à partir d’un tooAzure d’ordinateur local. Il peut s’exécutent également sur Azure en tant que site principal script avant l’arrêt, pendant la restauration à partir de l’ordinateur local, Azure tooan.
* Lorsqu’un script s’exécute, il injecte un contexte de plan de récupération. Bonjour à l’exemple suivant montre une variable de contexte :

    ```
            {"RecoveryPlanName":"hrweb-recovery",

            "FailoverType":"Test",

            "FailoverDirection":"PrimaryToSecondary",

            "GroupId":"1",

            "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                    { "SubscriptionId":"7a1111111-c1d6-49c5-8c5d-111ce8dd183",

                    "ResourceGroupName":"ContosoRG",

                    "CloudServiceName":"pod02hrweb-Chicago-test",

                    "RoleName":"Fabrikam-Hrweb-frontend-test",

                    "RecoveryPointId":"TimeStamp"}

                    }

            }
    ```

    Hello tableau suivant répertorie le nom de hello et une description de chaque variable dans le contexte de hello.

    | **Nom de la variable** | **Description** |
    | --- | --- |
    | RecoveryPlanName |nom de Hello du plan hello en cours d’exécution. Cette variable vous permet de prendre des mesures différentes selon le nom de plan de récupération hello. Vous pouvez également réutiliser le script de hello. |
    | FailoverType |Spécifie si le basculement de hello est un test, planifié ou non planifié. |
    | FailoverDirection |Spécifie si la récupération est le site principal ou secondaire de tooa. |
    | GroupID |Identifie le numéro de groupe hello dans le plan de récupération hello lorsque le plan de hello est en cours d’exécution. |
    | VmMap |Un tableau de tous les ordinateurs virtuels dans le groupe de hello. |
    | Clé VMMap |Clé unique (GUID) pour chaque machine virtuelle. Son hello identique hello ID Azure Virtual Machine Manager (VMM) de hello machine virtuelle, le cas échéant. |
    | SubscriptionId |ID d’abonnement Azure Hello dans lequel hello machine virtuelle a été créé. |
    | RoleName |nom Hello Hello machine virtuelle Azure qui est en cours de récupération. |
    | CloudServiceName |nom du service cloud Azure Hello que sous lequel hello machine virtuelle a été créé. |
    | ResourceGroupName|nom de groupe de ressources Azure Hello que sous lequel hello machine virtuelle a été créé. |
    | RecoveryPointId|horodateur de Hello pour lorsque hello machine virtuelle est récupérée. |

* Vérifiez que ce compte Automation hello a hello suivant des modules :
    * AzureRM.profile
    * AzureRM.Resources
    * AzureRM.Automation
    * AzureRM.Network
    * AzureRM.Compute

Les versions de tous les modules doivent être compatibles. Un tooensure facilement que tous les modules sont compatibles est toouse hello dernières versions de tous les modules hello.

### <a name="access-all-vms-of-hello-vmmap-in-a-loop"></a>Accéder à tous les ordinateurs virtuels de hello VMMap dans une boucle
Utilisez hello les de code tooloop sur tous les ordinateurs virtuels de hello Microsoft VMMap :

```
$VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
$vmMap = $RecoveryPlanContext.VmMap
 foreach($VMID in $VMinfo)
 {
     $VM = $vmMap.$VMID                
             if( !(($VM -eq $Null) -Or ($VM.ResourceGroupName -eq $Null) -Or ($VM.RoleName -eq $Null))) {
         #this check is tooensure that we skip when some data is not available else it will fail
 Write-output "Resource group name ", $VM.ResourceGroupName
 Write-output "Rolename " = $VM.RoleName
     }
 }

```

> [!NOTE]
> Hello ressource groupe nom et le rôle de valeurs de nom sont vides quand le script de hello est un groupe de démarrage pré tooa. les valeurs Hello sont remplies uniquement si hello machine virtuelle de ce groupe réussit au basculement. script de Hello est une post-action du groupe de démarrage hello.

## <a name="use-hello-same-automation-runbook-in-multiple-recovery-plans"></a>Utilisez hello même runbook Automation dans plusieurs plans de récupération

Vous pouvez utiliser un même script dans plusieurs plans de récupération à l’aide de variables externes. Vous pouvez utiliser [variables Azure Automation](../automation/automation-variables.md) toostore les paramètres que vous pouvez passer d’une récupération de l’exécution du plan. En ajoutant le nom de plan de récupération hello en tant que préfixe toohello variable, vous pouvez créer des variables individuelles pour chaque plan de récupération. Ensuite, utilisez les variables hello en tant que paramètres. Vous pouvez modifier un paramètre sans modifier le script de hello, mais toujours modifier hello hello façon script fonctionne.

### <a name="use-a-simple-string-variable-in-a-runbook-script"></a>Utiliser une variable chaîne simple dans un script de runbook

Dans cet exemple, un script accepte l’entrée d’un groupe de sécurité réseau (NSG) hello et elle applique des machines virtuelles de toohello d’un plan de récupération.

Pour toodetect de script hello le plan de récupération est en cours d’exécution, utilisez le contexte hello du plan de récupération :

```
workflow AddPublicIPAndNSG {
    param (
          [parameter(Mandatory=$false)]
          [Object]$RecoveryPlanContext
    )

    $RPName = $RecoveryPlanContext.RecoveryPlanName
```

tooapply un groupe de sécurité réseau existant, vous devez connaître les nom de groupe de sécurité réseau hello et le nom de groupe de ressources de groupe de sécurité réseau hello. Utilisez ces variables en tant qu’entrées pour les scripts de plan de récupération. toodo, créez deux variables Bonjour ressources du compte Automation. Ajouter le nom hello hello du plan de récupération que vous créez des paramètres hello pour qu’un nom de variable toohello préfixe.

1. Créer un nom de groupe de sécurité réseau toostore variable hello. Ajouter un nom de variable toohello préfixe à l’aide du nom hello hello du plan de récupération.

    ![Créer la variable du nom de groupe de sécurité réseau](media/site-recovery-runbook-automation-new/var1.png)

2. Créer un nom de groupe de ressources d’un NSG hello toostore variable. Ajouter un nom de variable toohello préfixe à l’aide du nom hello hello du plan de récupération.

    ![Créer un nom de groupe de ressources de groupe de sécurité réseau](media/site-recovery-runbook-automation-new/var2.png)


3.  Dans le script de hello, utilisez hello référence code tooget hello variable valeurs suivantes :

    ```
    $NSGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSG"
    $NSGRGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSGRG"

    $NSGnameVar = Get-AutomationVariable -Name $NSGValue
    $RGnameVar = Get-AutomationVariable -Name $NSGRGValue
    ```

4.  Utilisez les variables hello dans hello runbook tooapply hello NSG toohello interface réseau de hello basculéent machine virtuelle :

    ```
    InlineScript {
    if (($Using:NSGname -ne $Null) -And ($Using:NSGRGname -ne $Null)) {
            $NSG = Get-AzureRmNetworkSecurityGroup -Name $Using:NSGname -ResourceGroupName $Using:NSGRGname
            Write-output $NSG.Id
            #Apply hello NSG tooa network interface
            #$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
            #Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
            #  -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $NSG
        }
    }
    ```

Pour chaque plan de récupération, créez des variables indépendantes afin que vous puissiez réutiliser les script hello. Ajouter un préfixe à l’aide du nom de plan de récupération hello. Pour obtenir un script complète, de bout en bout pour ce scénario, consultez [ajouter un tooVMs publique de l’adresse IP et le groupe de sécurité réseau pendant le test de basculement d’un plan de récupération de Site Recovery](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).


### <a name="use-a-complex-variable-toostore-more-information"></a>Utilisez une variable complexe de toostore plus d’informations

Considérez un scénario dans lequel vous souhaitez un tooturn script unique sur une adresse IP publique sur des machines virtuelles spécifiques. Dans un autre scénario, vous pourriez tooapply différents groupes de sécurité réseau sur différentes machines virtuelles (et non sur tous les ordinateurs virtuels). Vous pouvez créer un script réutilisable pour tout plan de récupération. Chaque plan de récupération peut avoir un nombre variable de machines virtuelles. Par exemple, une récupération SharePoint a deux serveurs frontaux. Une application métier n’a qu’un seul serveur frontal. Vous ne pouvez pas créer des variables distinctes pour chaque plan de récupération. 

Bonjour l’exemple suivant, nous utiliser une technique de nouveau et créer un [variable complexe](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) dans les ressources de compte Azure Automation hello. Pour ce faire, spécifiez plusieurs valeurs. Vous devez utiliser Azure PowerShell toocomplete hello est comme suit :

1. Dans PowerShell, la connexion tooyour abonnement Azure :

    ```
    login-azurermaccount
    $sub = Get-AzureRmSubscription -Name <SubscriptionName>
    $sub | Select-AzureRmSubscription
    ```

2. paramètres de hello toostore, créer hello complexe variable à l’aide du nom hello hello du plan de récupération :

    ```
    $VMDetails = @{"VMGUID"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"};"VMGUID2"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"}}
        New-AzureRmAutomationVariable -ResourceGroupName <RG of Automation Account> -AutomationAccountName <AA Name> -Name <RecoveryPlanName> -Value $VMDetails -Encrypted $false
    ```

3. Dans cette variable complexe, **VMDetails** est hello ID de machine virtuelle pour hello protégé la machine virtuelle. tooget hello ID de machine virtuelle, Bonjour portail Azure, afficher les propriétés de machine virtuelle hello. Hello capture d’écran suivante montre une variable qui stocke les détails de hello de deux machines virtuelles :

    ![Utilisez hello ID de machine virtuelle comme hello GUID](media/site-recovery-runbook-automation-new/vmguid.png)

4. Utilisez cette variable dans votre runbook. Si hello indiqué que VM GUID se trouve dans le contexte du plan de récupération hello, appliquez hello NSG sur hello machine virtuelle :

    ```
    $VMDetailsObj = Get-AutomationVariable -Name $RecoveryPlanContext.RecoveryPlanName
    ```

4. Dans votre runbook, parcourir les ordinateurs virtuels de hello du contexte du plan de récupération hello. Vérifier l’existence de hello VM dans **$VMDetailsObj**. Si elle existe, accéder aux propriétés de hello Hello de variable tooapply hello groupe de sécurité réseau :

    ```
        $VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
        $vmMap = $RecoveryPlanContext.VmMap

        foreach($VMID in $VMinfo) {
            Write-output $VMDetailsObj.value.$VMID

            if ($VMDetailsObj.value.$VMID -ne $Null) { #If hello VM exists in hello context, this will not b Null
                $VM = $vmMap.$VMID
                # Access hello properties of hello variable
                $NSGname = $VMDetailsObj.value.$VMID.'NSGName'
                $NSGRGname = $VMDetailsObj.value.$VMID.'NSGResourceGroupName'

                # Add code tooapply hello NSG properties toohello VM
            }
        }
    ```

Vous pouvez utiliser hello même générer un script pour les plans de récupération différent. Entrez des paramètres différents en stockant la valeur hello qui correspond le plan de récupération tooa dans des variables différentes.

## <a name="sample-scripts"></a>Exemples de scripts

toodeploy exemple scripts tooyour compte Automation, cliquez sur hello **déployer tooAzure** bouton.

[![Déployer tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)

Pour un autre exemple, consultez hello suivant vidéo. Il montre comment toorecover un tooAzure d’application de WordPress à deux niveaux :


> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/One-click-failover-of-a-2-tier-WordPress-application-using-Azure-Site-Recovery/player]



## <a name="additional-resources"></a>Ressources supplémentaires
* [Documentation Automation](../automation/automation-sec-configure-azure-runas-account.md)
* [Vue d’ensemble d’Azure Automation](http://msdn.microsoft.com/library/azure/dn643629.aspx "Vue d’ensemble d’Azure Automation")
* [Ressources de script pour les professionnels de l'informatique](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "Ressources de script pour les professionnels de l'informatique")
