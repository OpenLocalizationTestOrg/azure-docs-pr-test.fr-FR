---
title: "architecture de connectivité de base de données SQL d’aaaAzure | Documents Microsoft"
description: "Ce document explique hello Azure SQLDB connectivité architecture d’Azure ou d’en dehors d’Azure."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: monicar
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/05/2017
ms.author: carlrab
ms.openlocfilehash: 917df6d88a16f1b841b617fb2a53025b4d14d034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-connectivity-architecture"></a>Architecture de connectivité Azure SQL Database 

Cet article explique l’architecture de connectivité de base de données SQL Azure hello et explique le fonctionnement des différents composants de hello instance de tooyour toodirect le trafic de base de données SQL Azure. Ces composants de connectivité de base de données SQL Azure fonctionnent toohello de trafic réseau toodirect de la base de données Azure avec les clients se connectant à partir d’Azure et avec les clients se connectant depuis l’extérieur d’Azure. Cet article fournit également des toochange d’exemples de script comment connectivité se produit, et les considérations hello liées paramètres de connectivité toochanging hello par défaut. Si vous avez des questions suite à la lecture de cet article, veuillez contacter Dhruv à l’adresse suivante : dmalik@microsoft.com. 

## <a name="connectivity-architecture"></a>Architecture de connectivité

Hello suivant schéma fournit une vue d’ensemble de hello architecture de connectivité de base de données SQL Azure. 

![Présentation de l’architecture](./media/sql-database-connectivity-architecture/architecture-overview.png)


Hello étapes suivantes décrivent comment une connexion est établie tooan base de données SQL Azure via hello Azure SQL Database-équilibrage de charge logiciel (SLB) et la passerelle de base de données SQL Azure hello.

- Les clients dans Azure ou en dehors de Azure connecteront toohello SLB, ce qui a une adresse IP publique et écoute le port 1433.
- Hello SLB dirige la passerelle de base de données SQL Azure toohello le trafic.
- passerelle de Hello redirige intergiciel (middleware) de hello trafic toohello proxy approprié.
- intergiciel (middleware) de Hello proxy redirige hello trafic toohello approprié SQL Azure de base de données.

> [!IMPORTANT]
> Chacun de ces composants a distribué de refus de la protection de service (distribué DDoS) intégrée au réseau de hello et à la couche d’application hello.
>

## <a name="connectivity-from-within-azure"></a>Connectivité dans Azure

Si vous vous connectez à partir d’Azure, vos connexions ont une stratégie de connexion par **redirection** par défaut. Une stratégie de **rediriger** signifie que les connexions une fois la session TCP de hello est la base de données SQL Azure toohello établie, la session de client hello est alors redirigé toohello intergiciel (middleware) pour le proxy avec une modification toohello destination adresse IP virtuelle à partir de celle de toothat de passerelle de base de données SQL Azure hello d’intergiciel (middleware) de hello proxy. Par la suite, tous les paquets suivants de flux directement via l’intergiciel proxy hello, en ignorant la passerelle de base de données SQL Azure hello. Hello suivant le diagramme illustre le flux de trafic.

![Présentation de l’architecture](./media/sql-database-connectivity-architecture/connectivity-from-within-azure.png)

## <a name="connectivity-from-outside-of-azure"></a>Connectivité en dehors d’Azure

Si vous vous connectez en dehors d’Azure, vos connexions disposent d’une stratégie de connexion de **proxy** par défaut. Une stratégie de **Proxy** signifie que hello TCP est établie via une passerelle de base de données SQL Azure hello et flux de tous les paquets suivants hello passerelle. Hello suivant le diagramme illustre le flux de trafic.

![Présentation de l’architecture](./media/sql-database-connectivity-architecture/connectivity-from-outside-azure.png)

## <a name="azure-sql-database-gateway-ip-addresses"></a>Adresses IP de la passerelle Azure SQL Database

tooconnect tooan Azure base de données SQL à partir des ressources locales, vous devez passerelle de base de données SQL Azure toohello tooallow réseau sortant du trafic de votre région Azure. Les connexions uniquement accéder via une passerelle de hello lors de la connexion en mode de Proxy, qui est la valeur par défaut hello lors de la connexion à partir des ressources locales.

Hello tableau ci-dessous répertorie hello principaux et secondaire des adresses IP de passerelle de base de données SQL Azure hello pour toutes les régions de données. Pour certaines régions, il existe deux adresses IP. Dans ces régions, l’adresse IP principale hello est hello adresse IP actuelle de passerelle de hello et adresse IP de la deuxième hello est une adresse IP de basculement. adresse de basculement Hello est toowhich d’adresse hello nous pouvons déplacer votre disponibilité du service serveur tookeep hello haute. Pour ces régions, nous vous recommandons d’autoriser des adresses IP hello tooboth sortant. adresse IP de la deuxième Hello est détenu par Microsoft et n’écoute pas tous les services jusqu'à ce qu’il est activé par des connexions de tooaccept de base de données SQL Azure.

| Nom de la région | Adresse IP principale | Adresse IP secondaire |
| --- | --- |--- |
| Est de l’Australie | 191.238.66.109 | 13.75.149.87 |
| Sud-Est de l’Australie | 191.239.192.109 | 13.73.109.251 |
| Sud du Brésil | 104.41.11.5 | |    
| Centre du Canada | 40.85.224.249 | |    
| Est du Canada | 40.86.226.166 | |
| Centre des États-Unis | 23.99.160.139 | 13.67.215.62 |
| Est de l'Asie | 191.234.2.139 | 52.175.33.150 |
| Est des États-Unis 1 | 191.238.6.43 | 40.121.158.30 |
| Est des États-Unis 2 | 191.239.224.107 | 40.79.84.180 |
| Inde-Centre | 104.211.96.159  | |   
| Sud de l'Inde | 104.211.224.146  | |
| Inde-Ouest | 104.211.160.80 | |
| Est du Japon | 191.237.240.43 | 13.78.61.196 |
| Ouest du Japon | 191.238.68.11 | 104.214.148.156 |
| Centre de la Corée | 52.231.32.42 | |
| Corée du Sud | 52.231.200.86 |  |
| États-Unis - partie centrale septentrionale | 23.98.55.75 | 23.96.178.199 |
| Europe du Nord | 191.235.193.75 | 40.113.93.91 |
| Centre-Sud des États-Unis | 23.98.162.75 | 13.66.62.124 |
| Asie du Sud-Est | 23.100.117.95 | 104.43.15.0 |
| Nord du Royaume-Uni | 13.87.97.210 | |
| Sud du Royaume-Uni 1 | 51.140.184.11 | |    
| Sud du Royaume-Uni 2 | 13.87.34.7 | |
| Ouest du Royaume-Uni | 51.141.8.11  | |
| Centre-Ouest des États-Unis | 13.78.145.25 | |
| Europe de l'Ouest | 191.237.232.75 | 40.68.37.158 |
| Ouest des États-Unis 1 | 23.99.34.75 | 104.42.238.205 |
| Ouest des États-Unis 2 | 13.66.226.202  | |
||||

## <a name="change-azure-sql-database-connection-policy"></a>Modifier la stratégie de connexion Azure SQL Database

toochange hello stratégie de connexion de base de données SQL Azure pour un serveur de base de données SQL Azure, utilisez hello [API REST](https://msdn.microsoft.com/library/azure/mt604439.aspx). 

- Si votre stratégie de connexion est défini trop**Proxy**, tous les flux de paquets via une passerelle de base de données SQL Azure hello du réseau. Pour ce paramètre, vous devez IP de passerelle de base de données SQL Azure tooallow tooonly sortant hello. L’utilisation d’un paramètre de **Proxy** offre plus de latence qu’un paramètre de **redirection**. 
- Si la définition de votre stratégie de connexion **rediriger**, tous les paquets réseau flux directement toohello intergiciel (middleware) proxy. Pour ce paramètre, vous devez toomultiple sortant de tooallow des adresses IP. 

## <a name="script-toochange-connection-settings"></a>Paramètres de script de connexion toochange

> [!IMPORTANT]
> Ce script nécessite hello [module Azure PowerShell](/powershell/azure/install-azurerm-ps).
>

Hello PowerShell script suivant montre comment toochange hello stratégie de connexion.

```powershell
import-module azureRm
Login-AzureRmAccount

$tenantId =  #your AAD tenant ID
$subscriptionId = #Azure SubscriptionID
$uri = #AAD uri
$authUrl = "https://login.microsoftonline.com/$tenantId"
$serverName = #sqldb server name 
$resourceGroupName=#sqldb resource group
$AuthContext = [Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext]$authUrl

$result = $AuthContext.AcquireToken("https://management.core.windows.net/",
$clientId,
[Uri]$uri, 
[Microsoft.IdentityModel.Clients.ActiveDirectory.PromptBehavior]::Auto)

$authHeader = @{
'Content-Type'='application\json; '
'Authorization'=$result.CreateAuthorizationHeader()
}

#getting hello current connection property
Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method GET -Headers $authHeader

#setting hello property too‘Proxy’
$connectionType=”Proxy” <#Redirect / Default are other options#>
$body = @{properties=@{connectionType=$connectionType}} | ConvertTo-Json

Invoke-RestMethod -Uri "https://management.azure.com/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Sql/servers/$serverName/connectionPolicies/Default?api-version=2014-04-01-preview" -Method PUT -Headers $authHeader -Body $body -ContentType "application/json"
```

## <a name="next-steps"></a>Étapes suivantes

- Pour plus d’informations sur la façon dont toochange hello stratégie de connexion de base de données SQL Azure pour un serveur de base de données SQL Azure, consultez [à l’aide de Create ou de la stratégie de mise à jour de connexion serveur hello API REST](https://msdn.microsoft.com/library/azure/mt604439.aspx).
- Pour plus d’informations sur le comportement de connexion d’Azure SQL Database pour les clients qui utilisent ADO.NET version 4.5 ou ultérieure, consultez [Ports au-delà de 1433 pour ADO.NET 4.5](sql-database-develop-direct-route-ports-adonet-v12.md).
- Pour en savoir plus sur la vue d’ensemble du développement d’applications générales, consultez [Vue d’ensemble du développement de base de données SQL](sql-database-develop-overview.md).
