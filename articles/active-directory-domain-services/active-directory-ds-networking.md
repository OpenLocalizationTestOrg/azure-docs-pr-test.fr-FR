---
title: "Services de domaine Azure AD : instructions de mise en réseau | Microsoft Docs"
description: "Considérations relatives à la mise en réseau pour les services de domaine Azure Active Directory"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 23a857a5-2720-400a-ab9b-1ba61e7b145a
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: maheshu
ms.openlocfilehash: 804d4ea7d1b3b07b6d224855c7adb90bdfe24022
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="networking-considerations-for-azure-ad-domain-services"></a>Considérations relatives à la mise en réseau pour les services de domaine Azure AD
## <a name="how-tooselect-an-azure-virtual-network"></a>Comment tooselect un réseau virtuel Azure
Hello indications suivantes vous aider à sélectionner un toouse de réseau virtuel avec les Services de domaine Active Directory de Azure.

### <a name="type-of-azure-virtual-network"></a>Type de réseau virtuel Azure
* Vous pouvez activer les services de domaine Azure AD dans un réseau virtuel Azure Classic.
* Les services de domaine Azure AD **ne peuvent pas être activés dans les réseaux virtuels créés à l’aide d’Azure Resource Manager**.
* Vous pouvez connecter un réseau virtuel basée sur le Gestionnaire de ressources tooa classique réseau virtuel dans lequel les Services de domaine Active Directory Azure est activée. Par la suite, vous pouvez utiliser les Services de domaine Active Directory de Azure dans le réseau virtuel hello Gestionnaire de ressources. Pour plus d’informations, consultez hello [connectivité réseau](active-directory-ds-networking.md#network-connectivity) section.
* **Réseaux virtuels régionaux**: Si vous envisagez de toouse un réseau virtuel existant, assurez-vous qu’il est un réseau virtuel régional.

  * Les réseaux virtuels qui utilisent le mécanisme de groupes d’affinités hérités hello ne peut pas être utilisés avec les Services de domaine Active Directory de Azure.
  * toouse Services de domaine Active Directory de Azure, [migrer des réseaux virtuels de réseaux virtuels hérités tooregional](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).

### <a name="azure-region-for-hello-virtual-network"></a>Région Azure pour le réseau virtuel de hello
* Votre domaine géré est déployé dans les Services de domaine Azure AD hello même région Azure que vous choisissez service hello tooenable réseaux hello.
* Sélectionnez un réseau virtuel dans une région Azure prise en charge par les services de domaine Azure AD.
* Consultez hello [des services Azure par région](https://azure.microsoft.com/regions/#services/) page tooknow hello régions Azure dans lequel les Services de domaine Active Directory de Azure est disponible.

### <a name="requirements-for-hello-virtual-network"></a>Configuration requise pour le réseau virtuel de hello
* **Proximité tooyour Azure les charges de travail**: sélectionnez hello réseau virtuel qui héberge actuellement/de destiné à héberger des ordinateurs virtuels qui doivent accéder aux Services de domaine Active Directory de tooAzure.
* **Custom/mettre vos propres des serveurs DNS**: Vérifiez qu’il n’y a aucun serveur DNS personnalisé configuré pour le réseau virtuel de hello.
* **Les domaines existants avec hello le même nom de domaine**: Vérifiez que vous n’avez pas un domaine existant avec hello même nom de domaine disponible sur ce réseau virtuel. Par exemple, supposons que vous avez un domaine appelé « contoso.com » déjà disponible sur le réseau virtuel sélectionné de hello. Une version ultérieure, vous essayez de tooenable un domaine géré des Services de domaine Active Directory de Azure avec hello même nom de domaine (qui est « contoso.com ») sur ce réseau virtuel. Une défaillance se produit lors de la tentative de Services de domaine tooenable Azure AD. Cet échec est dû tooname des conflits de nom de domaine hello sur ce réseau virtuel. Dans ce cas, vous devez utiliser un nom différent de tooset votre domaine géré des Services de domaine Active Directory de Azure. Ou bien, vous pouvez annuler la configuration domaine hello et puis continuer les Services de domaine tooenable Azure AD.

> [!WARNING]
> Impossible de déplacer le réseau virtuel tooa Services de domaine une fois que vous avez activé le service de hello.
>
>

## <a name="network-security-groups-and-subnet-design"></a>Conception de groupes de sécurité et de sous-réseaux
A [groupe de sécurité réseau (NSG)](../virtual-network/virtual-networks-nsg.md) contient une liste de règles de liste de contrôle d’accès (ACL) qui autorisent ou refusent le trafic réseau tooyour des instances de machine virtuelle dans un réseau virtuel. Des groupes de sécurité réseau peuvent être associés à des sous-réseaux ou à des instances de machine virtuelle au sein de ce sous-réseau. Lorsqu’un groupe de sécurité réseau est associé à un sous-réseau, listes de contrôle hello appliquent instances de machine virtuelle tooall hello dans ce sous-réseau. En outre, le trafic tooan machine virtuelle individuelle peut être limité par l’association d’un groupe de sécurité réseau directement toothat machine virtuelle.

![Conception de sous-réseau recommandée](./media/active-directory-domain-services-design-guide/vnet-subnet-design.png)

### <a name="best-practices-for-choosing-a-subnet"></a>Meilleures pratiques pour le choix d’un sous-réseau
* Déployer des Services de domaine Active Directory de Azure tooa **séparer sous-réseau dédié** au sein de votre réseau virtuel Azure.
* N’appliquez pas de sous-réseau toohello dédié de groupes de sécurité réseau pour votre domaine géré. Si vous devez appliquer le sous-réseau toohello dédié de groupes de sécurité réseau, vérifiez que vous **ne pas bloquer tooservice requis de ports hello et gérer votre domaine**.
* Ne limitent pas trop nombre hello d’adresses IP disponibles au sein du sous-réseau hello dédié pour votre domaine géré. Cette restriction empêche le service de hello à partir de la disposition des deux contrôleurs de domaine pour votre domaine géré.
* **N’activez pas les Services de domaine Active Directory de Azure dans le sous-réseau de passerelle hello** de votre réseau virtuel.

> [!WARNING]
> Lorsque vous associez un groupe de sécurité réseau avec un sous-réseau dans lequel des Services de domaine Active Directory de Azure est activé, vous pouvez interrompre tooservice de capacité de Microsoft et gérer le domaine de hello. En outre, la synchronisation entre votre client Azure AD et votre domaine géré est interrompue. **Hello SLA ne s’applique pas toodeployments où un groupe de sécurité réseau a été appliqué qui bloque les Services de domaine Active Directory de Azure à partir de la mise à jour et la gestion de votre domaine.**
>
>

### <a name="ports-required-for-azure-ad-domain-services"></a>Ports requis pour les services de domaine Azure AD
Hello ports suivants sont requis pour les Services de domaine Active Directory Azure tooservice et mettre à jour de votre domaine géré. Assurez-vous que ces ports ne sont pas bloqués pour le sous-réseau hello dans lequel vous avez activé votre domaine géré.

| Numéro de port | Objectif |
| --- | --- |
| 443 |Synchronisation avec votre client Azure AD |
| 3389 |Gestion de votre domaine |
| 5986 |Gestion de votre domaine |
| 636 |Accès tooyour managé domaine LDAP (LDAPS) sécurisé |

### <a name="sample-nsg-for-virtual-networks-with-azure-ad-domain-services"></a>Exemple de groupe de sécurité réseau pour les réseaux virtuels avec Azure AD Domain Services
Hello tableau suivant illustre un exemple de groupe de sécurité réseau que vous pouvez configurer pour un réseau virtuel avec un domaine géré des Services de domaine Active Directory de Azure. Cette règle permet le trafic entrant de hello au-dessus des ports spécifiés tooensure votre domaine géré reste corrigés, mis à jour et peut être surveillée par Microsoft. Hello par défaut 'DenyAll' règle s’applique tooall reste du trafic entrant de hello internet.

En outre, hello NSG illustre également comment toolock vers le bas un accès LDAP sécurisé sur hello internet. Ignorer cette règle si vous n’avez pas activé l’accès tooyour managé domaine LDAP sécurisé sur hello internet. Hello NSG contient un ensemble de règles qui autorisent l’accès LDAPS entrant sur le port TCP 636 uniquement à partir d’un ensemble spécifique d’adresses IP. Hello NSG règle tooallow LDAPS d’accès sur hello internet à partir d’adresses IP spécifiées a une priorité supérieure à la règle de DenyAll NSG de hello.

![Exemple NSG toosecure LDAPS d’accès sur hello internet](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

**Informations supplémentaires** - [Créer un groupe de sécurité réseau](../virtual-network/virtual-networks-create-nsg-arm-pportal.md).


## <a name="network-connectivity"></a>Connectivité réseau
Un domaine géré par les services de domaine Azure AD peut être activé uniquement au sein d’un seul réseau virtuel Classic dans Azure. Les réseaux virtuels créés à l’aide d’Azure Resource Manager ne sont pas pris en charge.

### <a name="scenarios-for-connecting-azure-networks"></a>Scénarios de connexion de réseaux Azure
Connecter des réseaux virtuels Azure toouse hello domaine géré dans un des hello les scénarios de déploiement suivants :

#### <a name="use-hello-managed-domain-in-more-than-one-azure-classic-virtual-network"></a>Hello d’utilisation gérés domaine dans plus d’un réseau virtuel Azure classic
Vous pouvez vous connecter d’autres toohello des réseaux virtuels Azure classique Azure classic réseau virtuel dans lequel vous avez activé les Services de domaine Active Directory de Azure. Cette connexion VPN permet un domaine géré de hello toouse avec vos charges de travail déployées dans d’autres réseaux virtuels.

![Connexion entre des réseaux virtuels Classic](./media/active-directory-domain-services-design-guide/classic-vnet-connectivity.png)

#### <a name="use-hello-managed-domain-in-a-resource-manager-based-virtual-network"></a>Utilise le domaine géré hello dans un réseau virtuel basé sur le Gestionnaire de ressources
Vous pouvez vous connecter à un toohello basée sur le Gestionnaire de ressources de réseau virtuel Azure classic réseau virtuel dans lequel vous avez activé les Services de domaine Active Directory de Azure. Cette connexion permet un domaine géré de hello toouse avec vos charges de travail déployées dans hello basée sur le Gestionnaire de ressources de réseau virtuel.

![Connectivité de réseau virtuel tooclassic du Gestionnaire de ressources](./media/active-directory-domain-services-design-guide/classic-arm-vnet-connectivity.png)

### <a name="network-connection-options"></a>Options de connexion réseau
* **Connexions de réseau virtuel à réseau virtuel à l’aide de connexions VPN site à site**: connexion d’un réseau virtuel de réseau virtuel tooanother (au réseau) est tooconnecting comme emplacement d’un site réseau virtuel tooan local. Les deux types de connectivité utilisent un tooprovide de passerelle VPN un tunnel sécurisé utilisant IPsec/IKE.

    ![Connexion entre des réseaux virtuels à l’aide d’une passerelle VPN](./media/active-directory-domain-services-design-guide/vnet-connection-vpn-gateway.jpg)

    [Plus d’informations : connecter des réseaux virtuels à l’aide d’une passerelle VPN](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)
* **Connexions de réseau virtuel à réseau virtuel à l’aide de virtual network d’homologation**: réseau virtuel d’homologation est un mécanisme qui connecte deux réseaux virtuels Bonjour même région via le réseau d’Azure backbone hello. Une fois homologuer, les réseaux virtuels deux hello apparaissent sous forme d’une toutes les fins de connectivité. Ils sont toujours gérés comme des ressources distinctes, mais les machines virtuelles se trouvant dans ces réseaux virtuels peuvent communiquer directement entre elles à l’aide d’adresses IP privées.

    ![Connexion entre des réseaux virtuels à l’aide d’une homologation](./media/active-directory-domain-services-design-guide/vnet-peering.png)

    [Plus d’informations : homologation de réseaux virtuels](../virtual-network/virtual-network-peering-overview.md)

<br>

## <a name="related-content"></a>Contenu connexe
* [Homologation de réseaux virtuels Azure](../virtual-network/virtual-network-peering-overview.md)
* [Configurer une connexion au réseau pour le modèle de déploiement classique de hello](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)
* [Groupes de sécurité réseau Azure](../virtual-network/virtual-networks-nsg.md)
* [Créer des groupes de sécurité réseau à l’aide du portail Azure](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
