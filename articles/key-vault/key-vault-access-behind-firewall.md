---
title: "aaaAccess le coffre de clés derrière un pare-feu | Documents Microsoft"
description: "Découvrez comment tooaccess Azure Key Vault à partir d’une application derrière un pare-feu"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 50d21774-2ee1-4212-8995-570c9de603c5
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: ambapat
ms.openlocfilehash: ab4bb0c27a41fef878a20dace6cab203df04e579
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="access-azure-key-vault-behind-a-firewall"></a>Accès à Azure Key Vault derrière un pare-feu
### <a name="q-my-key-vault-client-application-needs-toobe-behind-a-firewall-what-ports-hosts-or-ip-addresses-should-i-open-tooenable-access-tooa-key-vault"></a>Q : mon application cliente de coffre de clés doit toobe derrière un pare-feu. Les ports, les hôtes ou des adresses IP dois-je ouvrir le coffre de clés tooenable accès tooa ?
tooaccess un coffre de clés, votre application cliente de coffre de clés a tooaccess plusieurs points de terminaison pour diverses fonctionnalités :

* Authentification via Azure Active Directory (Azure AD).
* Gestion d’un coffre Azure Key Vault. Cela inclut la création, la lecture, la mise à jour, la suppression et la définition de stratégies d’accès par le biais d’Azure Resource Manager.
* Accès et gestion des objets (clés et les secrets) stockés dans le coffre de clés lui-même, traverser hello de point de terminaison spécifique de coffre de clé (par exemple, [https://yourvaultname.vault.azure.net](https://yourvaultname.vault.azure.net)).  

Il existe des variantes selon votre configuration et l’environnement.   

## <a name="ports"></a>Ports
Tous les coffre de clés de tooa le trafic pour les trois fonctions (accès de plan d’authentification, de gestion et de données) passe via le protocole HTTPS : le port 443. Cependant, il faut compter occasionnellement sur un trafic HTTP (port 80) pour les CRL. Les clients qui prennent en charge le protocole OCSP ne doivent pas atteindre les CRL, mais peuvent occasionnellement atteindre [http://cdp1.public-trust.com/CRL/Omniroot2025.crl](http://cdp1.public-trust.com/CRL/Omniroot2025.crl).  

## <a name="authentication"></a>Authentification
Applications clientes de coffre de clés doivent tooaccess points de terminaison Azure Active Directory pour l’authentification. point de terminaison Hello utilisé dépend de la configuration de client Azure AD hello, de type hello du principal (UPN ou principal de service) et hello type de compte--par exemple, un compte Microsoft ou un professionnel ou scolaire compte.  

| Type de principal | Point de terminaison:port |
| --- | --- |
| Utilisateur utilisant un compte Microsoft<br> (par exemple, user@hotmail.com) |**Mondial :**<br> login.microsoftonline.com:443<br><br> **Azure en Chine :**<br> login.chinacloudapi.cn:443<br><br>**Azure US Government :**<br> login-us.microsoftonline.com:443<br><br>**Azure Germany :**<br> login.microsoftonline.de:443<br><br> and <br>login.live.com:443 |
| Utilisateur ou au principal de service à l’aide d’un compte professionnel ou scolaire avec Azure AD (par exemple, user@contoso.com) |**Mondial :**<br> login.microsoftonline.com:443<br><br> **Azure en Chine :**<br> login.chinacloudapi.cn:443<br><br>**Azure US Government :**<br> login-us.microsoftonline.com:443<br><br>**Azure Germany :**<br> login.microsoftonline.de:443 |
| Utilisateur ou au principal de service à l’aide d’un travail ou compte scolaire, ainsi que les Services de fédération Active Directory (AD FS) ou autre point de terminaison fédéré (par exemple, user@contoso.com) |Tous les points de terminaison correspondant à un compte professionnel ou scolaire, plus AD FS ou d’autres points de terminaison fédérés |

D’autres scénarios complexes sont possibles. Consultez trop[Active Directory flux d’authentification Azure](/documentation/articles/active-directory-authentication-scenarios/), [intégration d’Applications avec Azure Active Directory](/documentation/articles/active-directory-integrating-applications/), et [des protocoles d’authentification Active Directory](https://msdn.microsoft.com/library/azure/dn151124.aspx) Pour plus d’informations.  

## <a name="key-vault-management"></a>Gestion de Key Vault
Pour la gestion de coffre de clés (CRUD et la définition de la stratégie d’accès), application cliente de coffre de clés hello doit tooaccess un point de terminaison Azure Resource Manager.  

| Type d’opération | Point de terminaison:port |
| --- | --- |
| Opérations du plan de contrôle Key Vault<br> via Azure Resource Manager |**Mondial :**<br> management.azure.com:443<br><br> **Azure China :**<br> management.chinacloudapi.cn:443<br><br> **Azure US Government :**<br> management.usgovcloudapi.net:443<br><br> **Azure Germany :**<br> management.microsoftazure.de:443 |
| API Graph Azure Active Directory |**Mondial :**<br> graph.windows.net:443<br><br> **Azure en Chine :**<br> graph.chinacloudapi.cn:443<br><br> **Azure US Government :**<br> graph.windows.net:443<br><br> **Azure Germany :**<br> graph.cloudapi.de:443 |

## <a name="key-vault-operations"></a>Opérations Key Vault
Pour toute la gestion d’objet (clés et les secrets) de coffre de clés et opérations de chiffrement, client de coffre de clés de hello nécessite un point de terminaison tooaccess hello coffre de clés. suffixe DNS de point de terminaison Hello varie en fonction de l’emplacement de hello de votre coffre de clés. point de terminaison de coffre de clés Hello est hello format *-nom du coffre*. *spécifique à la région-suffixe dns*, comme décrit dans hello tableau suivant.  

| Type d’opération | Point de terminaison:port |
| --- | --- |
| Opérations telles que le chiffrement sur les clés, création/lecture/mise à jour/suppression de clés et de secrets, définition/obtention de mots-clés et autres attributs sur objets de coffre de clés (clés ou secrets) |**Mondial :**<br> &lt;nom du coffre&gt;.vault.azure.net:443<br><br> **Azure China :**<br> &lt;nom du coffre&gt;.vault.azure.cn:443<br><br> **Azure US Government :**<br> &lt;nom du coffre&gt;.vault.usgovcloudapi.net:443<br><br> **Azure Germany :**<br> &lt;nom du coffre&gt;.vault.microsoftazure.de:443 |

## <a name="ip-address-ranges"></a>Plages d’adresse IP
Hello service Key Vault utilise d’autres ressources Azure comme infrastructure de PaaS. Il est donc pas possible de tooprovide un spécifique plage d’adresses IP que le coffre de clés auront des points de terminaison de service à un moment donné. Si votre pare-feu prend en charge uniquement les plages d’adresses IP, consultez toohello [plages d’adresses IP Microsoft Azure Datacenter](https://www.microsoft.com/download/details.aspx?id=41653) document. Pour l’authentification et l’identité (Azure Active Directory), votre application doit être en mesure de tooconnect points de terminaison de toohello décrites dans [l’authentification et identité des adresses](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).

## <a name="next-steps"></a>Étapes suivantes
Si vous avez des questions sur le coffre de clés, visitez hello [Azure Key Vault Forums](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).

