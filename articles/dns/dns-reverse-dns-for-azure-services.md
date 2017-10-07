---
title: aaaReverse DNS pour les services Azure | Documents Microsoft
description: "Découvrez comment tooconfigure DNS inversées pour les services hébergés dans Azure"
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/29/2017
ms.author: jonatul
ms.openlocfilehash: c6fe1d80232f124be86dd7fc57abc20699be7eba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-reverse-dns-for-services-hosted-in-azure"></a>Configurer des DNS inversés dans les services hébergés par Azure

Cet article explique comment tooconfigure DNS inversées pour les services hébergés dans Azure.

Les services Azure utilisent des adresses IP assignées par Azure et détenues par Microsoft. Ces enregistrements DNS inverses (enregistrements PTR) doivent être créés dans hello correspondant appartenant à Microsoft recherche les zones DNS inverses. Cet article explique comment toodo cela.

Ce scénario ne doit pas être confondu avec possibilité de hello trop[héberger des zones de recherche DNS inverses hello pour vos plages IP affectées dans Azure DNS](dns-reverse-dns-hosting.md). Dans ce cas, les plages d’adresses IP hello représentés par la zone de recherche inversée hello doivent être assignés tooyour organisation, généralement par votre fournisseur de services Internet.

Avant de lire cet article, prenez connaissance de cette [Vue d’ensemble des DNS inversés et de la prise en charge dans Azure](dns-reverse-dns-overview.md).

Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../azure-resource-manager/resource-manager-deployment-model.md).
* Dans le modèle de déploiement du Gestionnaire de ressources hello, les ressources de calcul (par exemple, les ordinateurs virtuels, machines virtuelles identiques ou clusters Service Fabric) sont exposées via une ressource d’adresse IP publique. Recherche DNS inversée est configurée à l’aide de la propriété « Valeur de ReverseFqdn » hello hello adresse IP publique.
* Dans le modèle de déploiement classique hello, les ressources de calcul sont exposées à l’aide des Services de cloud computing. Recherche DNS inversée est configurée à l’aide de la propriété de 'ReverseDnsFqdn' hello Hello Service Cloud.

DNS inverse n’est pas prise en charge pour hello du Service d’applications Azure.

## <a name="validation-of-reverse-dns-records"></a>Validation des enregistrements DNS inversés

Un tiers ne doit pas être en mesure de toocreate des enregistrements DNS inverses pour leurs service Azure mappage tooyour DNS des domaines. tooprevent, Azure n’autorise la création d’un enregistrement DNS inverse, où le nom de domaine spécifié dans l’enregistrement DNS inverse de hello est hello identique ou soit résolu en hello nom DNS ou l’adresse IP d’une adresse IP publique ou un Cloud Service Bonjour même hello abonnement Azure.

Cette validation est effectuée uniquement lors de l’enregistrement DNS inversé de hello est défini ou modifié. Aucune nouvelle validation périodique n’est effectuée.

Par exemple : supposons que hello ressource d’adresse IP publique a contosoapp1.northus.cloudapp.azure.com de nom DNS hello et l’adresse IP 23.96.52.53. Hello valeur de ReverseFqdn pour hello qu'adresse IP publique peut être spécifié en tant que :
* nom DNS Hello hello PublicIpAddress, contosoapp1.northus.cloudapp.azure.com
* Hello de noms DNS pour une autre adresse IP publique Bonjour même abonnement, par exemple contosoapp2.westus.cloudapp.azure.com
* Un personnel de nom DNS, tel que app1.contoso.com, tant que ce nom est *premier* configuré comme un CNAME toocontosoapp1.northus.cloudapp.azure.com ou tooa PublicIpAddress différents Bonjour même abonnement.
* Un personnel de nom DNS, tel que app1.contoso.com, tant que ce nom est *premier* configuré en tant qu’un enregistrement toohello IP adresse 23.96.52.53 ou adresse IP de toohello d’une adresse IP publique différents Bonjour même abonnement.

Hello mêmes contraintes s’appliquent tooreverse DNS pour les Services Cloud.


## <a name="reverse-dns-for-publicipaddress-resources"></a>Les DNS inversés pour les ressources PublicIpAddress

Cette section fournit des instructions détaillées pour la tooconfigure DNS inverse pour les ressources d’adresse IP publique dans hello Gestionnaire de ressources du modèle de déploiement utilisant Azure PowerShell, Azure CLI 1.0 ou 2.0 de CLI d’Azure. Configuration de DNS inverse pour les ressources d’adresse IP publique n’est pas actuellement pris en charge via hello portail Azure.

Actuellement, Azure ne prend en charge les DNS inversés que pour les ressources PublicIpAddress IPv4. Non pris en charge pour IPv6.

### <a name="add-reverse-dns-tooan-existing-publicipaddresses"></a>Ajouter inverse tooan DNS existant PublicIpAddresses

#### <a name="powershell"></a>PowerShell

tooadd inversée DNS tooan existant d’adresse IP publique :

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

tooadd inverser tooan DNS existant d’adresse IP publique qui n’a pas encore un nom DNS, vous devez également spécifier un nom DNS :

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings = New-Object -TypeName "Microsoft.Azure.Commands.Network.Models.PSPublicIpAddressDnsSettings"
$pip.DnsSettings.DomainNameLabel = "contosoapp1"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a>Azure CLI 1.0

tooadd inversée DNS tooan existant d’adresse IP publique :

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -f contosoapp1.westus.cloudapp.azure.com.
```

tooadd inverser tooan DNS existant d’adresse IP publique qui n’a pas encore un nom DNS, vous devez également spécifier un nom DNS :

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -d contosoapp1 -f contosoapp1.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a>Azure CLI 2.0

tooadd inversée DNS tooan existant d’adresse IP publique :

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com.
```

tooadd inverser tooan DNS existant d’adresse IP publique qui n’a pas encore un nom DNS, vous devez également spécifier un nom DNS :

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com --dns-name contosoapp1
```

### <a name="create-a-public-ip-address-with-reverse-dns"></a>Création d’une adresse IP publique avec un DNS inversé

toocreate une nouvelle adresse IP publique avec la propriété DNS inverse hello déjà spécifiée :

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup" -Location "WestUS" -AllocationMethod Dynamic -DomainNameLabel "contosoapp2" -ReverseFqdn "contosoapp2.westus.cloudapp.azure.com."
```

#### <a name="azure-cli-10"></a>Azure CLI 1.0

```azurecli
azure network public-ip create -n PublicIp -g MyResourceGroup -l westus -d contosoapp3 -f contosoapp3.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a>Azure CLI 2.0

```azurecli
az network public-ip create --name PublicIp --resource-group MyResourceGroup --location westcentralus --dns-name contosoapp1 --reverse-fqdn contosoapp1.westcentralus.cloudapp.azure.com
```

### <a name="view-reverse-dns-for-an-existing-publicipaddress"></a>Afficher DNS inversé pour des adresses IP publiques existantes

tooview hello la valeur configurée pour une adresse IP publique existante :

#### <a name="powershell"></a>PowerShell

```powershell
Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
```

#### <a name="azure-cli-10"></a>Azure CLI 1.0

```azurecli
azure network public-ip show -n PublicIp -g MyResourceGroup
```

#### <a name="azure-cli-20"></a>Azure CLI 2.0

```azurecli
az network public-ip show --name PublicIp --resource-group MyResourceGroup
```

### <a name="remove-reverse-dns-from-existing-public-ip-addresses"></a>Suppression d’un enregistrement DNS inversé d’une adresse IP publique existante

tooremove une propriété DNS inversée à partir d’une adresse IP publique existante :

#### <a name="powershell"></a>PowerShell

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = ""
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a>Azure CLI 1.0

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup –f ""
```

#### <a name="azure-cli-20"></a>Azure CLI 2.0

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn ""
```


## <a name="configure-reverse-dns-for-cloud-services"></a>Configurer un DNS inversé pour les services Cloud

Cette section fournit des instructions détaillées pour la tooconfigure DNS inverse pour les Services de cloud computing dans le modèle de déploiement classique de hello, à l’aide d’Azure PowerShell. Configuration du service DNS inverse pour les Services Cloud n’est pas pris en charge via hello portail Azure, Azure CLI 1.0 ou 2.0 de CLI d’Azure.

### <a name="add-reverse-dns-tooexisting-cloud-services"></a>Ajouter des Services de cloud computing tooexisting DNS inverse

tooadd un tooan d’enregistrement DNS inverse existant du Service Cloud :

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="create-a-cloud-service-with-reverse-dns"></a>Création d’un service cloud avec un DNS inversé

toocreate un nouveau Service Cloud avec la propriété DNS inverse hello déjà spécifiée :

```powershell
New-AzureService –ServiceName "contosoapp1" –Location "West US" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="view-reverse-dns-for-existing-cloud-services"></a>Affichage d’un DNS inversé pour les services cloud existants

tooview hello inverse la propriété DNS pour un Service Cloud existant :

```powershell
Get-AzureService "contosoapp1"
```

### <a name="remove-reverse-dns-from-existing-cloud-services"></a>Suppression d’un DNS inversé des services cloud existants

tooremove une propriété DNS inverse d’un Service Cloud existant :

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn ""
```

## <a name="faq"></a>Forum Aux Questions

### <a name="how-much-do-reverse-dns-records-cost"></a>Combien coûtent les enregistrements DNS inversés ?

Ils sont gratuits.  Les enregistrements DNS inversés ou les requêtes n’entraînent aucun frais supplémentaire.

### <a name="will-my-reverse-dns-records-resolve-from-hello-internet"></a>Sera mon résoudre les enregistrements DNS inverse de hello internet ?

Oui. Une fois que vous définissez la propriété DNS inverse hello pour votre service Azure, Azure gère toutes les délégations DNS de hello et zones DNS requis tooensure qui inverse l’enregistrement DNS est résolu pour tous les utilisateurs d’Internet.

### <a name="are-default-reverse-dns-records-created-for-my-azure-services"></a>Des enregistrements DNS inversés par défaut sont-ils créés pour mes services Azure ?

Non. Le DNS inversé est une fonctionnalité optionnelle. Sans valeur par défaut des enregistrements DNS inverses sont créés, si vous ne choisissez pas tooconfigure les.

### <a name="what-is-hello-format-for-hello-fully-qualified-domain-name-fqdn"></a>Quel est le format hello pour le nom de domaine complet de hello (FQDN) ?

Les noms de domaine complets sont spécifiés dans l’ordre chronologique et doivent se terminer par un point (par exemple, « app1.contoso.com. »).

### <a name="what-happens-if-hello-validation-check-for-hello-reverse-dns-ive-specified-fails"></a>Que se passe-t-il si le contrôle de validation hello pour hello inverse DNS j’ai spécifié échoue ?

Où hello inversée DNS validation échoue, hello tooconfigure hello inversée DNS enregistrement de l’opération échoue. Corrigez la valeur DNS inverse hello en fonction des besoins et réessayez.

### <a name="can-i-configure-reverse-dns-for-azure-app-service"></a>Puis-je configurer un DNS inversé pour Azure App Service ?

Non. DNS inverse n’est pas pris en charge pour hello du Service d’applications Azure.

### <a name="can-i-configure-multiple-reverse-dns-records-for-my-azure-service"></a>Puis-je configurer plusieurs enregistrements DNS inversés pour mon service Azure ?

Non. Azure ne prend en charge qu’un seul enregistrement DNS inversé pour chaque service cloud Azure ou adresse IP publique.

### <a name="can-i-configure-reverse-dns-for-ipv6-publicipaddress-resources"></a>Puis-je configurer un DNS inversé pour des ressources PublicIpAddress IPv6 ?

Non. Actuellement, Azure ne prend en charge le DNS inversé que pour les ressources PublicIpAddress IPv4.

### <a name="can-i-send-emails-tooexternal-domains-from-my-azure-compute-services"></a>Puis-je envoyer des messages électroniques tooexternal domaines à partir de mes services de calcul Azure ?

Non. [Les services de calcul Azure ne prennent pas en charge les domaines de tooexternal envoi des messages électroniques](https://blogs.msdn.microsoft.com/mast/2016/04/04/sending-e-mail-from-azure-compute-resource-to-external-domains/)

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur le DNS inversé, consultez [Recherche DNS inversée sur Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).
<br>
Découvrez comment trop[zone de recherche inversée hello hôte pour votre plage IP affectée par le fournisseur de services Internet dans Azure DNS](dns-reverse-dns-for-azure-services.md).

