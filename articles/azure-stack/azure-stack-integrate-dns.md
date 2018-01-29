---
title: "Intégration au centre de données Azure Stack - DNS"
description: "Découvrez comment intégrer les services DNS Azure Stack au DNS de votre centre de données"
services: azure-stack
author: troettinger
ms.service: azure-stack
ms.topic: article
ms.date: 10/10/2017
ms.author: victorh
keywords: 
ms.openlocfilehash: 40d6d4858ef2e3df61d04dc68c00e09c04f000e2
ms.sourcegitcommit: 6acb46cfc07f8fade42aff1e3f1c578aa9150c73
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/18/2017
---
# <a name="azure-stack-datacenter-integration---dns"></a>Intégration au centre de données Azure Stack - DNS

*S’applique à : systèmes intégrés Azure Stack*

Pour pouvoir accéder aux points de terminaison Azure Stack (`portal`, `adminportal`, `management`, `adminmanagement`, etc.) en dehors d’Azure Stack, vous devez intégrer les services DNS Azure Stack aux serveurs DNS qui hébergent les zones DNS que vous souhaitez utiliser dans Azure Stack.

## <a name="azure-stack-dns-namespace"></a>Espace de noms DNS Azure Stack
Vous devez fournir certaines informations importantes relatives à DNS quand vous déployez Azure Stack.


|Champ  |Description  |Exemple|
|---------|---------|---------|
|Région|Emplacement géographique de votre déploiement d’Azure Stack.|`east`|
|Nom du domaine externe|Nom de la zone à utiliser pour votre déploiement d’Azure Stack.|`cloud.fabrikam.com`|
|Nom de domaine interne|Nom de la zone interne utilisée pour les services d’infrastructure dans Azure Stack.  Elle est intégrée au service d’annuaire et privée (inaccessible en dehors du déploiement d’Azure Stack).|`azurestack.local`|
|Redirecteur DNS|Serveurs DNS qui sont utilisés pour transférer les requêtes DNS, les zones DNS et les enregistrements qui sont hébergés en dehors d’Azure Stack (sur l’intranet d’entreprise ou sur l’Internet public).|`10.57.175.34`<br>`8.8.8.8`|
|Préfixe de nommage (facultatif)|Préfixe de nommage dont vous souhaitez doter les noms de machine des instances du rôle d’infrastructure d’Azure Stack.  S’il n’est pas fourni, la valeur par défaut est `azs`.|`azs`|

Le nom de domaine complet (FQDN) de votre déploiement d’Azure Stack et des points de terminaison est la combinaison du paramètre de la région et du paramètre du nom de domaine externe. D’après les valeurs des exemples dans le tableau précédent, le nom de domaine complet pour ce déploiement d’Azure Stack serait le suivant :

`east.cloud.fabrikam.com`

Ainsi, certains des points de terminaison pour ce déploiement ressembleraient, par exemple, aux URL suivantes :

`https://portal.east.cloud.fabrikam.com`

`https://adminportal.east.cloud.fabrikam.com`

Afin d’utiliser cet exemple d’espace de noms DNS pour un déploiement d’Azure Stack, les conditions suivantes sont requises :

- La zone `fabrikam.com` est inscrite auprès d’un bureau d’enregistrement de domaine et/ou d’un serveur DNS d’entreprise interne, selon vos exigences en termes de résolution de noms.
- Le domaine enfant `cloud.fabrikam.com` existe sous la zone `fabrikam.com`.
- Les serveurs DNS qui hébergent les zones `fabrikam.com` et `cloud.fabrikam.com` sont accessibles depuis le déploiement d’Azure Stack.

Afin de résoudre les noms DNS pour les points de terminaison Azure Stack et les instances en dehors d’Azure Stack, vous devez intégrer les serveurs DNS qui hébergent la zone DNS externe pour Azure Stack aux serveurs DNS qui hébergent la zone parent que vous souhaitez utiliser.


## <a name="resolution-and-delegation"></a>Résolution et délégation

Deux types de serveur DNS sont disponibles :

- Un serveur DNS faisant autorité héberge les zones DNS. Il répond aux requêtes DNS pour les enregistrements de ces zones uniquement.
- Un serveur DNS récursif n’héberge pas de zones DNS. Il répond à toutes les requêtes DNS, en appelant des serveurs DNS faisant autorité pour rassembler les données dont il a besoin.

Azure Stack comprend à la fois des serveurs DNS faisant autorité et des serveurs DNS récursifs. Les serveurs récursifs sont utilisés pour résoudre les noms de tous les éléments à l’exception de la zone privée interne et de la zone DNS publique externe pour ce déploiement d’Azure Stack. 

![Architecture DNS d’Azure Stack](media/azure-stack-integrate-dns/Integrate-DNS-01.png)

## <a name="resolving-external-dns-names-from-azure-stack"></a>Résolution des noms DNS externes à partir d’Azure Stack

Afin de résoudre les noms DNS pour les points de terminaison en dehors d’Azure Stack (par exemple : www.bing.com), vous devez fournir des serveurs DNS qu’Azure Stack peut utiliser pour transférer les requêtes DNS pour lesquelles Azure Stack ne fait pas autorité. Pour le déploiement, les serveurs DNS vers lesquels Azure Stack transfère les requêtes sont requis dans la feuille de calcul de déploiement (dans le champ du redirecteur DNS). Indiquez au moins deux serveurs dans ce champ à des fins de tolérance de panne. En l’absence de ces valeurs, le déploiement d’Azure Stack échoue.

### <a name="configure-conditional-dns-forwarding"></a>Configurer la redirection DNS conditionnelle

> [!IMPORTANT]
> Cela s’applique uniquement à un déploiement AD FS.

Pour activer la résolution de noms de votre infrastructure DNS existante, configurez le transfert conditionnel.

Pour ajouter un redirecteur conditionnel, vous devez utiliser le point de terminaison privilégié.

Pour cette procédure, utilisez un ordinateur de votre réseau de centre de données qui peut communiquer avec le point de terminaison privilégié dans Azure Stack.

1. Ouvrez une session Windows PowerShell avec élévation de privilèges (exécuter en tant qu’administrateur) et connectez-vous à l’adresse IP du point de terminaison privilégié. Utilisez les informations d’identification pour l’authentification de l’administrateur du cloud.

   ```
   $cred=Get-Credential 
   Enter-PSSession -ComputerName <IP Address of ERCS> -ConfigurationName PrivilegedEndpoint -Credential $cred
   ```

2. Une fois connecté au point de terminaison privilégié, exécutez la commande PowerShell suivante. Remplacez les exemples de valeur fournis par votre nom de domaine et les adresses IP des serveurs DNS que vous souhaitez utiliser.

   ```
   Register-CustomDnsServer -CustomDomainName "contoso.com" -CustomDnsIPAddresses "192.168.1.1","192.168.1.2"
   ```

## <a name="resolving-azure-stack-dns-names-from-outside-azure-stack"></a>Résolution des noms DNS Azure Stack en dehors d’Azure Stack
Ce sont les serveurs faisant autorité qui hébergent les informations des zones DNS externes et toutes les zones créées par l’utilisateur. Effectuez une intégration à ces serveurs afin que la délégation de zone ou le transfert conditionnel puisse résoudre les noms DNS Azure Stack en dehors d’Azure Stack.

## <a name="get-dns-server-external-endpoint-information"></a>Obtenir les informations de point de terminaison externe des serveurs DNS

Pour intégrer votre déploiement d’Azure Stack à votre infrastructure DNS, vous avez besoin des informations suivantes :

- Noms de domaine complets des serveurs DNS
- Adresses IP des serveurs DNS

Les noms de domaine complets des serveurs DNS Azure Stack ont le format suivant :

`<NAMINGPREFIX>-ns01.<REGION>.<EXTERNALDOMAINNAME>`

`<NAMINGPREFIX>-ns02.<REGION>.<EXTERNALDOMAINNAME>`

D’après les exemples de valeur, les noms de domaine complets des serveurs DNS sont les suivants :

`azs-ns01.east.cloud.fabrikam.com`

`azs-ns02.east.cloud.fabrikam.com`


Ces informations sont également créées à la fin de tous les déploiements d’Azure Stack dans un fichier nommé `AzureStackStampDeploymentInfo.json`. Ce fichier se trouve dans le dossier `C:\CloudDeployment\logs` de la machine virtuelle de déploiement. Si vous n’êtes pas sûr des valeurs qui ont été utilisées pour votre déploiement d’Azure Stack, vous pouvez les y retrouver.

Si la machine virtuelle de déploiement n’est plus disponible ou n’est pas accessible, vous pouvez obtenir les valeurs en vous connectant au point de terminaison privilégié, puis en exécutant l’applet de commande PowerShell `Get-AzureStackInfo`. Pour plus d’informations sur le point de terminaison privilégié, consulter (insérer le lien vers l’article ici).

## <a name="setting-up-conditional-forwarding-to-azure-stack"></a>Configuration du transfert conditionnel vers Azure Stack

La façon la plus simple et la plus sûre d’intégrer Azure Stack à votre infrastructure DNS consiste à effectuer un transfert conditionnel de la zone à partir du serveur qui héberge la zone parente. Nous vous recommandons cette approche si vous contrôlez directement les serveurs DNS qui hébergent la zone parente pour votre espace de noms DNS externe Azure Stack.

Si vous n’êtes pas familiarisé avec la façon d’effectuer un transfert conditionnel avec DNS, consultez l’article TechNet suivant : [Assign a Conditional Forwarder for a Domain Name](https://technet.microsoft.com/library/cc794735) (Affecter un redirecteur conditionnel pour un nom de domaine), ou la documentation relative à votre solution DNS.

Dans les scénarios où vous avez spécifié votre zone DNS Azure Stack externe de telle façon qu’elle s’apparente à un domaine enfant de votre nom de domaine d’entreprise, vous ne pouvez pas utiliser le transfert conditionnel. Vous devez configurer la délégation DNS.

Exemple :

- Nom de domaine DNS d’entreprise : `contoso.com`
- Nom de domaine DNS externe Azure Stack : `azurestack.contoso.com`

## <a name="delegating-the-external-dns-zone-to-azure-stack"></a>Délégation de la zone DNS externe à Azure Stack

Pour permettre la résolution des noms DNS en dehors d’un déploiement d’Azure Stack, vous devez configurer la délégation DNS.

Chaque bureau d’enregistrement a ses propres outils de gestion DNS pour modifier les enregistrements de serveur de noms pour un domaine. Dans la page de gestion du bureau d’enregistrement DNS, modifiez les enregistrements NS et remplacez les enregistrements NS pour la zone par ceux créés dans Azure Stack.

La plupart des bureaux d’enregistrement DNS requièrent que vous fournissiez au minimum deux serveurs DNS pour effectuer la délégation.

## <a name="next-steps"></a>Étapes suivantes

[Intégration au centre de données Azure Stack - Identité](azure-stack-integrate-identity.md)
