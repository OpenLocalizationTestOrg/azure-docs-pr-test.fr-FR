---
title: aaaUsing PowerShell toomanage Traffic Manager dans Azure | Documents Microsoft
description: Utilisation de Powershell pour Traffic Manager avec Azure Resource Manager
services: traffic-manager
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: bc247448-1d2e-4104-ac03-42b59ebde065
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: 018c37db63beb82fdad54cfd7e13ab3cb645723a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-powershell-toomanage-traffic-manager"></a>À l’aide de PowerShell toomanage Traffic Manager

Le Gestionnaire de ressources Azure est l’interface de gestion préférés hello pour les services dans Azure. Les outils et API d’Azure Resource Manager permettent de gérer les profils Azure Traffic Manager.

## <a name="resource-model"></a>Modèle de ressource

Azure Traffic Manager est configuré à l'aide d'un ensemble de paramètres appelé profil Traffic Manager. Ce profil contient les paramètres DNS, les paramètres de routage du trafic, les paramètres de surveillance de point de terminaison, et une liste de trafic de toowhich de points de terminaison de service est routée.

Chaque profil Traffic Manager est représenté par une ressource de type « TrafficManagerProfiles ». Au niveau de l’API REST de hello, hello URI pour chaque profil est la suivante :

    https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Network/trafficManagerProfiles/{profile-name}?api-version={api-version}

## <a name="setting-up-azure-powershell"></a>Configuration d’Azure PowerShell

Ces instructions utilisent Microsoft Azure PowerShell. Hello suivant explique comment tooinstall et configurer Azure PowerShell.

* [Comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview)

exemples de Hello dans cet article supposent que vous disposez d’un groupe de ressources existant. Vous pouvez créer un groupe de ressources à l’aide de hello de commande suivante :

```powershell
New-AzureRmResourceGroup -Name MyRG -Location "West US"
```

> [!NOTE]
> Azure Resource Manager exige des groupes de ressources qu’ils disposent tous d’un emplacement. Cet emplacement est utilisé comme valeur par défaut hello pour les ressources créées dans ce groupe de ressources. Toutefois, étant donné que les ressources du profil Traffic Manager sont globales, pas régional, choix hello de l’emplacement du groupe de ressources n’a aucun impact sur Azure Traffic Manager.

## <a name="create-a-traffic-manager-profile"></a>Créer un profil Traffic Manager

toocreate un profil Traffic Manager, utilisez hello `New-AzureRmTrafficManagerProfile` applet de commande :

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName contoso -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
```

Hello tableau suivant décrit les paramètres de hello :

| Paramètre | Description |
| --- | --- |
| Nom |nom de la ressource Hello pour hello ressource de profil Traffic Manager. Profils Bonjour même groupe de ressources doive avoir des noms uniques. Ce nom est différent du nom DNS de hello utilisé pour les requêtes DNS. |
| ResourceGroupName |nom de Hello de hello groupe conteneur hello profil ressource. |
| TrafficRoutingMethod |Spécifie les hello de routage du trafic méthode utilisée toodetermine point de terminaison qui est retourné en réponse à une requête DNS. Les valeurs possibles sont « Performance », « Weighted » ou « Priority ». |
| RelativeDnsName |Spécifie la partie du nom d’hôte hello du nom DNS de hello fournie par ce profil Traffic Manager. Cette valeur est combinée avec le nom de domaine DNS hello utilisé par Azure Traffic Manager tooform hello nom de domaine complet (FQDN) du profil de hello. Par exemple, la définition de valeur hello de « contoso » devient « contoso.trafficmanager.net ». |
| TTL |Spécifie les hello DNS Time-to-Live (TTL), en secondes. Cette durée de vie indique aux résolutions DNS locales de hello et les clients DNS les réponses DNS la durée pendant laquelle toocache pour ce profil Traffic Manager. |
| MonitorProtocol |Spécifie le contrôle d’intégrité du point de terminaison de toomonitor toouse hello protocole. Les valeurs possibles sont « HTTP » et « HTTPS ». |
| MonitorPort |Spécifie hello le port TCP utilisé d’intégrité du point de terminaison toomonitor. |
| MonitorPort |Spécifie le nom de domaine de point de terminaison hello chemin d’accès relatif toohello utilisé tooprobe pour le contrôle d’intégrité du point de terminaison. |

applet de commande Hello crée un profil Traffic Manager dans Azure et renvoie un tooPowerShell objet de profil correspondant. À ce stade, le profil hello ne contient aucun point de terminaison. Pour plus d’informations sur l’ajout du profil Traffic Manager tooa points de terminaison, consultez [Ajout de points de terminaison de Traffic Manager](#adding-traffic-manager-endpoints).

## <a name="get-a-traffic-manager-profile"></a>Récupérer un profil Traffic Manager

tooretrieve un objet de profil Traffic Manager existant, utilisez hello `Get-AzureRmTrafficManagerProfle` applet de commande :

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
```

Cette applet de commande renvoie un objet de profil Traffic Manager.

## <a name="update-a-traffic-manager-profile"></a>Mettre à jour un profil Traffic Manager

La modification des profils Traffic Manager est un processus en 3 étapes :

1. À l’aide de profil récupérer hello `Get-AzureRmTrafficManagerProfile` ou utiliser le profil hello retourné par `New-AzureRmTrafficManagerProfile`.
2. Modifier le profil de hello. Vous pouvez ajouter et supprimer des points de terminaison ou modifier les paramètres des points de terminaison ou du profil. Ces modifications sont des opérations hors connexion. Vous ne modifiez objet local de hello en mémoire qui représente le profil de hello.
3. Valider les modifications apportées à l’aide de hello `Set-AzureRmTrafficManagerProfile` applet de commande.

Toutes les propriétés de profil peuvent être modifiées à l’exception RelativeDnsName du profil hello. toochange hello RelativeDnsName, vous devez supprimer le profil et un nouveau profil avec un nouveau nom.

Bonjour à l’exemple suivant montre comment toochange hello durée de vie du profil :

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
$profile.Ttl = 300
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

Il existe trois types de points de terminaison Traffic Manager :

1. Les **points de terminaison Azure** sont des services hébergés dans Azure.
2. Les **points de terminaison externes** sont des services hébergés en dehors d’Azure.
3. **Imbriqué des points de terminaison** sont des hiérarchies utilisé tooconstruct imbriqué de profils Traffic Manager. Ils permettent de définir des configurations de routage du trafic avancées pour les applications complexes.

Dans ces trois cas, les points de terminaison peuvent être ajoutés de deux manières :

1. En suivant le processus en 3 étapes décrit précédemment. avantage Hello de cette méthode est que plusieurs modifications de point de terminaison peuvent être effectuées dans une seule mise à jour.
2. À l’aide d’applet de commande New-AzureRmTrafficManagerEndpoint hello. Cette applet de commande ajoute un point de terminaison tooan existant du profil Traffic Manager en une seule opération.

## <a name="adding-azure-endpoints"></a>Ajout de points de terminaison Azure

Les points de terminaison Azure font référence à des services hébergés dans Azure. Les types de point de terminaison Azure pris en charge sont au nombre de deux :

1. Azure Web Apps 
2. Ressources d’adresse IP publique Azure (qui peuvent être attaché tooa équilibreur de charge ou une carte réseau de machine virtuelle). Hello adresse IP publique doit avoir un nom DNS assigné toobe utilisé dans le Gestionnaire de trafic.

Dans chaque cas :

* service de Hello est spécifié à l’aide du paramètre de « targetResourceId » hello de `Add-AzureRmTrafficManagerEndpointConfig` ou `New-AzureRmTrafficManagerEndpoint`.
* Hello 'Target' et 'EndpointLocation' sont implicitement hello TargetResourceId.
* Spécification de hello « Weight » est facultative. Poids sont uniquement utilisés si le profil de hello est la méthode de routage du trafic toouse configuré hello 'Weighted'. Autrement, elles sont ignorées. Si spécifié, la valeur de hello doit être un nombre compris entre 1 et 1000. valeur par défaut de Hello est '1'.
* En spécifiant hello 'Priority' est facultatif. Les priorités sont uniquement utilisées si le profil de hello est la méthode de routage du trafic toouse configuré hello 'Priority'. Autrement, elles sont ignorées. Les valeurs valides sont de 1 too1000 ayant des valeurs inférieures indiquant une priorité plus élevée. Si elles sont spécifiées pour un point de terminaison, elles doivent l’être pour tous les points de terminaison. Si omis, les valeurs par défaut à partir de '1' sont appliquées dans l’ordre de hello que les points de terminaison hello sont répertoriés.

### <a name="example-1-adding-web-app-endpoints-using-add-azurermtrafficmanagerendpointconfig"></a>Exemple 1 : ajout de points de terminaison d’application web à l’aide de `Add-AzureRmTrafficManagerEndpointConfig`

Dans cet exemple, nous créons un profil Traffic Manager et ajouter deux points de terminaison de l’application Web à l’aide de hello `Add-AzureRmTrafficManagerEndpointConfig` applet de commande.

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$webapp1 = Get-AzureRMWebApp -Name webapp1
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp1ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp1.Id -EndpointStatus Enabled
$webapp2 = Get-AzureRMWebApp -Name webapp2
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp2ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp2.Id -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```
### <a name="example-2-adding-a-publicipaddress-endpoint-using-new-azurermtrafficmanagerendpoint"></a>Exemple 2 : ajout d’un point de terminaison publicIpAddress à l’aide de `New-AzureRmTrafficManagerEndpoint`

Dans cet exemple, une ressource d’adresse IP publique est ajoutée le profil Traffic Manager toohello. adresse IP publique de Hello doit avoir un nom DNS configuré et peut être lié soit toohello carte réseau d’un équilibrage de charge de machine virtuelle ou tooa.

```powershell
$ip = Get-AzureRmPublicIpAddress -Name MyPublicIP -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name MyIpEndpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type AzureEndpoints -TargetResourceId $ip.Id -EndpointStatus Enabled
```

## <a name="adding-external-endpoints"></a>Ajout de points de terminaison externes

Traffic Manager utilise des points de terminaison externe toodirect trafic tooservices hébergé en dehors d’Azure. Comme les points de terminaison Azure, les points de terminaison externes peuvent être ajoutés à l’aide de `Add-AzureRmTrafficManagerEndpointConfig` suivi de `Set-AzureRmTrafficManagerProfile`, ou avec `New-AzureRMTrafficManagerEndpoint`.

Lors de la spécification de points de terminaison externes :

* nom de domaine du point de terminaison Hello doit être spécifié à l’aide du paramètre de 'Target' hello
* Si hello méthode de routage du trafic « Performance » est utilisé, hello 'EndpointLocation' est requis. Sinon, il est facultatif. la valeur Hello doit être un [nom de la région Azure valide](https://azure.microsoft.com/regions/).
* Hello 'Poids' et 'Priority' est facultatif.

### <a name="example-1-adding-external-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a>Exemple 1 : ajout de points de terminaison externes à l’aide de `Add-AzureRmTrafficManagerEndpointConfig` et `Set-AzureRmTrafficManagerProfile`

Dans cet exemple, nous créer un profil Traffic Manager, ajoutez les deux points de terminaison externes et valider les modifications de hello.

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName eu-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointLocation "North Europe" -EndpointStatus Enabled
Add-AzureRmTrafficManagerEndpointConfig -EndpointName us-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-us.contoso.com -EndpointLocation "Central US" -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-adding-external-endpoints-using-new-azurermtrafficmanagerendpoint"></a>Exemple 2 : ajout de points de terminaison externes à l’aide de `New-AzureRmTrafficManagerEndpoint`

Dans cet exemple, nous ajouter un profil existant tooan de point de terminaison externe. profil de Hello est spécifié à l’aide de noms de groupe de ressources et un profil de hello.

```powershell
New-AzureRmTrafficManagerEndpoint -Name eu-endpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointStatus Enabled
```

## <a name="adding-nested-endpoints"></a>Ajout de points de terminaison « imbriqués »

Chaque profil Traffic Manager spécifie une seule méthode de routage du trafic. Toutefois, il existe des scénarios qui requièrent que le routage hello fournis par un seul profil Traffic Manager le routage du trafic plus sophistiquées. Vous pouvez imbriquer des avantages de hello de toocombine de profils Traffic Manager de plusieurs méthodes de routage du trafic. Profils imbriqués permettent toooverride hello par défaut Traffic Manager comportement toosupport plus volumineux et les déploiements d’applications plus complexes. Pour obtenir des informations plus détaillées, consultez [Profils Traffic Manager imbriqués](traffic-manager-nested-profiles.md).

Points de terminaison imbriquées sont configurées au profil parent de hello, à l’aide d’un type de point de terminaison spécifique, 'NestedEndpoints'. Lors de la spécification de points de terminaison imbriqués :

* point de terminaison Hello doit être spécifié à l’aide du paramètre de 'targetResourceId' hello
* Si hello méthode de routage du trafic « Performance » est utilisé, hello 'EndpointLocation' est requis. Sinon, il est facultatif. la valeur Hello doit être un [nom de la région Azure valide](http://azure.microsoft.com/regions/).
* Hello 'Poids' et 'Priority' est facultatif, comme pour les points de terminaison Azure.
* paramètre de 'MinChildEndpoints' Hello est facultatif. valeur par défaut de Hello est '1'. Si le nombre de hello de points de terminaison disponibles tombe sous ce seuil, profil parent de hello considère que le profil enfant hello « dégradé » et dévie le trafic toohello autres points de terminaison dans le profil de hello parent.

### <a name="example-1-adding-nested-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a>Exemple 1 : ajout de points de terminaison imbriqués à l’aide de `Add-AzureRmTrafficManagerEndpointConfig` et `Set-AzureRmTrafficManagerProfile`

Dans cet exemple, nous créer des profils de parent et enfant Traffic Manager, ajouter un enfant de hello en tant que point de terminaison imbriquée toohello parent et valider les modifications de hello.

```powershell
$child = New-AzureRmTrafficManagerProfile -Name child -ResourceGroupName MyRG -TrafficRoutingMethod Priority -RelativeDnsName child -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$parent = New-AzureRmTrafficManagerProfile -Name parent -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName parent -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName child-endpoint -TrafficManagerProfile $parent -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

Par souci de concision dans cet exemple, nous n’avez pas ajouté de tous les autres points de terminaison toohello enfant ou parent profils.

### <a name="example-2-adding-nested-endpoints-using-new-azurermtrafficmanagerendpoint"></a>Exemple 2 : ajout de points de terminaison imbriqués à l’aide de `New-AzureRmTrafficManagerEndpoint`

Dans cet exemple, nous ajouter un profil enfant existant comme point de terminaison imbriquée tooan existant parent profil. profil de Hello est spécifié à l’aide de noms de groupe de ressources et un profil de hello.

```powershell
$child = Get-AzureRmTrafficManagerEndpoint -Name child -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name child-endpoint -ProfileName parent -ResourceGroupName MyRG -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
```

## <a name="update-a-traffic-manager-endpoint"></a>Mettre à jour un point de terminaison Traffic Manager

Il existe deux façons tooupdate un point de terminaison Traffic Manager existant :

1. Obtenir à l’aide de profil Traffic Manager hello `Get-AzureRmTrafficManagerProfile`, mettre à jour les propriétés du point de terminaison hello dans le profil de hello et valider les modifications hello à l’aide de `Set-AzureRmTrafficManagerProfile`. Cette méthode présente un avantage hello d’être en mesure de tooupdate plus d’un point de terminaison en une seule opération.
2. Obtenir à l’aide de point de terminaison de Traffic Manager hello `Get-AzureRmTrafficManagerEndpoint`, mettre à jour les propriétés du point de terminaison hello et valider les modifications hello à l’aide de `Set-AzureRmTrafficManagerEndpoint`. Cette méthode est plus simple, car il ne nécessite pas l’indexation dans un tableau de points de terminaison hello dans le profil de hello.

### <a name="example-1-updating-endpoints-using-get-azurermtrafficmanagerprofile-and-set-azurermtrafficmanagerprofile"></a>Exemple 1 : mise à jour des points de terminaison à l’aide de `Get-AzureRmTrafficManagerProfile` et `Set-AzureRmTrafficManagerProfile`

Dans cet exemple, nous modifions la priorité de hello deux points de terminaison au sein d’un profil existant.

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG
$profile.Endpoints[0].Priority = 2
$profile.Endpoints[1].Priority = 1
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-updating-an-endpoint-using-get-azurermtrafficmanagerendpoint-and-set-azurermtrafficmanagerendpoint"></a>Exemple 2 : mise à jour d’un point de terminaison à l’aide de `Get-AzureRmTrafficManagerEndpoint` et `Set-AzureRmTrafficManagerEndpoint`

Dans cet exemple, nous modifions poids hello d’un point de terminaison unique dans un profil existant.

```powershell
$endpoint = Get-AzureRmTrafficManagerEndpoint -Name myendpoint -ProfileName myprofile -ResourceGroupName MyRG -Type ExternalEndpoints
$endpoint.Weight = 20
Set-AzureRmTrafficManagerEndpoint -TrafficManagerEndpoint $endpoint
```

## <a name="enabling-and-disabling-endpoints-and-profiles"></a>Activation et désactivation des points de terminaison et des profils

Traffic Manager permet de points de terminaison individuels toobe activé et désactivé, tout en permettant l’activation et désactivation des profils de l’ensemble.
Ces modifications peuvent être apportées par les ressources de point de terminaison ou le profil de l’obtention/la mise à jour/définition hello. toostreamline ces opérations courantes, elles sont également prises en charge via les applets de commande dédiées.

### <a name="example-1-enabling-and-disabling-a-traffic-manager-profile"></a>Exemple 1 : activation et désactivation d’un profil Traffic Manager

tooenable un profil Traffic Manager, utilisez `Enable-AzureRmTrafficManagerProfile`. profil de Hello peut être spécifié à l’aide d’un objet de profil. Hello objet de profil peut être transmis via le pipeline de hello ou à l’aide de hello '-TrafficManagerProfile' paramètre. Dans cet exemple, nous spécifions le profil de hello par nom de groupe de ressources et un profil de hello.

```powershell
Enable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

toodisable un profil Traffic Manager :

```powershell
Disable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

applet de commande Disable-AzureRmTrafficManagerProfile Hello demande confirmation. Ce message peut être supprimé à l’aide de hello '-Force' paramètre.

### <a name="example-2-enabling-and-disabling-a-traffic-manager-endpoint"></a>Exemple 2 : activation et désactivation d’un point de terminaison Traffic Manager

tooenable un point de terminaison Traffic Manager, utilisez `Enable-AzureRmTrafficManagerEndpoint`. Il existe deux points de terminaison hello de toospecify façons

1. À l’aide d’un objet TrafficManagerEndpoint transmis via le pipeline de hello ou hello '-TrafficManagerEndpoint' paramètre
2. À l’aide du nom de point de terminaison hello, type de point de terminaison, nom du profil et nom de groupe de ressources :

```powershell
Enable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

De même, toodisable un point de terminaison Traffic Manager :

```powershell
Disable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG -Force
```

Comme avec `Disable-AzureRmTrafficManagerProfile`, hello `Disable-AzureRmTrafficManagerEndpoint` applet de commande vous demande confirmation. Ce message peut être supprimé à l’aide de hello '-Force' paramètre.

## <a name="delete-a-traffic-manager-endpoint"></a>Supprimer un point de terminaison Traffic Manager

tooremove des points de terminaison individuels, utilisez hello `Remove-AzureRmTrafficManagerEndpoint` applet de commande :

```powershell
Remove-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

Cette applet de commande vous demande de confirmer l’opération. Ce message peut être supprimé à l’aide de hello '-Force' paramètre.

## <a name="delete-a-traffic-manager-profile"></a>Supprimer un profil Traffic Manager

toodelete un profil Traffic Manager, utilisez hello `Remove-AzureRmTrafficManagerProfile` applet de commande, en spécifiant les noms de groupe de ressources et un profil de hello :

```powershell
Remove-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG [-Force]
```

Cette applet de commande vous demande de confirmer l’opération. Ce message peut être supprimé à l’aide de hello '-Force' paramètre.

toobe de profil Hello supprimé peut également être spécifié à l’aide d’un objet de profil :

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
Remove-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile [-Force]
```

Cette séquence peut également être canalisée :

```powershell
Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG | Remove-AzureRmTrafficManagerProfile [-Force]
```

## <a name="next-steps"></a>Étapes suivantes

[Surveillance avec Traffic Manager](traffic-manager-monitoring.md)

[Considérations sur les performances de Traffic Manager](traffic-manager-performance-considerations.md)
