---
title: "l’audit de groupe de sécurité réseau aaaAutomate avec l’affichage de groupe de sécurité de l’Observateur réseau Azure | Documents Microsoft"
description: "Cette page fournit des instructions sur la façon de tooconfigure l’audit d’un groupe de sécurité réseau"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 78a01bcf-74fe-402a-9812-285f3501f877
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 24fc418c433fceaf55a74b7c3b0e354dc46c8729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-nsg-auditing-with-azure-network-watcher-security-group-view"></a>Automatiser l’audit NSG avec la vue de groupe de sécurité réseau Network Watcher

Les clients sont souvent confrontés à hello défi de vérification posture de sécurité hello de leur infrastructure. Ce défi n’est pas différent pour leurs machines virtuelles dans Azure. Il est important toohave un profil de sécurité similaire selon les règles du groupe de sécurité réseau (NSG) hello appliquées. À l’aide de hello vue du groupe de sécurité, vous pouvez désormais obtenir la liste hello des règles appliquées tooa machine virtuelle au sein d’un groupe de sécurité réseau. Vous pouvez définir un profil de sécurité de groupe de sécurité réseau finale et lancer l’affichage du groupe de sécurité à un rythme hebdomadaire et comparer le profil de hello sortie toohello finale (Gold) et créer un rapport. Ainsi, vous pouvez identifier facilement toutes les machines virtuelles hello qui ne sont pas conforment toohello prescrit le profil de sécurité.

Si vous n’êtes pas familiarisé avec les groupes de sécurité réseau, consultez la [vue d’ensemble de la sécurité réseau](../virtual-network/virtual-networks-nsg.md)

## <a name="before-you-begin"></a>Avant de commencer

Dans ce scénario, vous comparez un groupe de sécurité connus bonne ligne de base toohello afficher les résultats retournés pour un ordinateur virtuel.

Ce scénario suppose que vous avez déjà suivi les étapes hello dans [créer un observateur réseau](network-watcher-create.md) toocreate un observateur réseau. scénario de Hello suppose également qu’un groupe de ressources avec un ordinateur virtuel valide existe toobe utilisé.

## <a name="scenario"></a>Scénario

scénario Hello abordée dans cet article Obtient l’affichage du groupe de sécurité pour un ordinateur virtuel hello.

Dans ce scénario, vous allez :

- Récupérer un ensemble de règles correct connu
- Récupérer une machine virtuelle avec l’API REST
- Obtenir la vue de groupe de sécurité pour la machine virtuelle
- Évaluer la réponse

## <a name="retrieve-rule-set"></a>Récupérer l’ensemble de règles

première étape de Hello dans cet exemple est toowork avec une ligne de base existante. exemple Hello est certains json extraite à partir d’un groupe de sécurité réseau existant à l’aide de hello `Get-AzureRmNetworkSecurityGroup` applet de commande qui est utilisée comme ligne de base hello pour cet exemple.

```json
[
    {
        "Description":  null,
        "Protocol":  "TCP",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "3389",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1000,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "default-allow-rdp",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/default-allow-rdp"
    },
    {
        "Description":  null,
        "Protocol":  "*",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "111",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1010,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "MyRuleDoNotDelete",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/MyRuleDoNotDelete"
    },
    {
        "Description":  null,
        "Protocol":  "*",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "112",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Allow",
        "Priority":  1020,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "My2ndRuleDoNotDelete",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/My2ndRuleDoNotDelete"
    },
    {
        "Description":  null,
        "Protocol":  "TCP",
        "SourcePortRange":  "*",
        "DestinationPortRange":  "5672",
        "SourceAddressPrefix":  "*",
        "DestinationAddressPrefix":  "*",
        "Access":  "Deny",
        "Priority":  1030,
        "Direction":  "Inbound",
        "ProvisioningState":  "Succeeded",
        "Name":  "ThisRuleNeedsToStay",
        "Etag":  "W/\"d8859256-1c4c-4b93-ba7d-73d9bf67c4f1\"",
        "Id":  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/testvm1-nsg/securityRules/ThisRuleNeedsToStay"
    }
]
```

## <a name="convert-rule-set-toopowershell-objects"></a>Convertir les objets tooPowerShell du jeu de règles

Dans cette étape, nous lisons un fichier json qui a été créé précédemment avec les règles hello toobe attendu sur hello groupe de sécurité réseau pour cet exemple.

```powershell
$nsgbaserules = Get-Content -Path C:\temp\testvm1-nsg.json | ConvertFrom-Json
```

## <a name="retrieve-network-watcher"></a>Récupérer Network Watcher

étape suivante de Hello est instance de l’Observateur réseau tooretrieve hello. Hello `$networkWatcher` variable est passée toohello `AzureRmNetworkWatcherSecurityGroupView` applet de commande.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a>Obtenir une machine virtuelle

Un ordinateur virtuel est requis toorun hello `Get-AzureRmNetworkWatcherSecurityGroupView` applet de commande par rapport à. Bonjour à l’exemple suivant obtient un objet ordinateur virtuel.

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="retrieve-security-group-view"></a>Récupérer la vue Groupe de sécurité

étape suivante de Hello est le résultat de vue du groupe de sécurité tooretrieve hello. Le résultat est comparé toohello « baseline » json qui a été indiqué précédemment.

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="analyzing-hello-results"></a>Analyse des résultats de hello

réponse de Hello est regroupé par les interfaces réseau. Hello différents types de règles retournées sont efficaces et règles de sécurité par défaut. résultat de Hello est davantage ventilé par comment elle est appliquée, sur un sous-réseau ou une carte réseau virtuelle.

Hello script PowerShell suivant compare les résultats de hello de hello sortie existante de tooan vue de groupe de sécurité d’un groupe de sécurité réseau. Bonjour exemple suivant est un exemple simple de la façon dont les résultats de hello puissent être comparés avec `Compare-Object` applet de commande.

```powershell
Compare-Object -ReferenceObject $nsgbaserules `
-DifferenceObject $secgroup.NetworkInterfaces[0].NetworkInterfaceSecurityRules `
-Property Name,Description,Protocol,SourcePortRange,DestinationPortRange,SourceAddressPrefix,DestinationAddressPrefix,Access,Priority,Direction
```

Bonjour à l’exemple suivant résulte hello. Vous pouvez voir deux règles hello qui étaient dans le premier ensemble de règles hello n’étaient pas présentes dans la comparaison de hello.

```
Name                     : My2ndRuleDoNotDelete
Description              : 
Protocol                 : *
SourcePortRange          : *
DestinationPortRange     : 112
SourceAddressPrefix      : *
DestinationAddressPrefix : *
Access                   : Allow
Priority                 : 1020
Direction                : Inbound
SideIndicator            : <=

Name                     : ThisRuleNeedsToStay
Description              : 
Protocol                 : TCP
SourcePortRange          : *
DestinationPortRange     : 5672
SourceAddressPrefix      : *
DestinationAddressPrefix : *
Access                   : Deny
Priority                 : 1030
Direction                : Inbound
SideIndicator            : <=
```

## <a name="next-steps"></a>Étapes suivantes

Si les paramètres ont été modifiés, consultez [gérer les groupes de sécurité réseau](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack vers le bas hello sécurité et groupe de règles de sécurité réseau qui sont en question.













