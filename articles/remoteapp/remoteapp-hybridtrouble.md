---
title: "aaaTroubleshoot création de regroupements hybride de RemoteApp | Documents Microsoft"
description: "Découvrez comment tootroubleshoot les échecs de création de collection hybride de RemoteApp"
services: remoteapp
documentationcenter: 
author: vkbucha
manager: mbaldwin
ms.assetid: b32033ee-8d52-4e74-bb78-86ca873c34e2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: cc426f24bd0c349a8862d54acbafa9cf84446f4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-azure-remoteapp-hybrid-collections"></a>Résolution des problèmes de création de collections hybrides Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Une collection hybride est hébergée dans et stocke des données dans hello cloud Azure, mais également permet aux utilisateurs accéder aux données et ressources stockées sur votre réseau local. Les utilisateurs peuvent accéder aux applications en se connectant avec leurs informations d'identification d'entreprise, synchronisées ou fédérées avec Azure Active Directory. Vous pouvez déployer une collection hybride qui utilise un réseau virtuel Azure existant ou vous pouvez créer un réseau virtuel. Nous vous recommandons d’utiliser une plage CIDR suffisamment étendue lorsque vous créez ou utilisez un sous-réseau de réseau virtuel afin de pouvoir prendre en compte la croissance future d’Azure RemoteApp.

Vous n’avez pas encore créé votre collection ? Consultez [créer une collection hybride](remoteapp-create-hybrid-deployment.md) pour connaître les étapes hello.

Si vous rencontrez des problèmes de création de votre collection, ou si la collection de hello ne fonctionne pas moyen hello vous pensez qu’il doit, consultez hello informations suivantes.

## <a name="your-image-is-invalid"></a>Votre image n'est pas valide
Si vous voyez un message comme « GoldImageInvalid » lorsque vous attendez Azure tooprovision votre collection, cela signifie que votre image de modèle ne répond pas aux hello [défini des exigences de l’image](remoteapp-imagereqs.md). Par conséquent, accédez à lire les [exigences](remoteapp-imagereqs.md), corrigez votre image et essayez toocreate à nouveau votre collection.

## <a name="does-your-vnet-have-network-security-groups-defined"></a>Votre réseau virtuel comporte-t-il des groupes de sécurité réseau ?
Si vous avez définis sur le sous-réseau hello vous utilisez pour votre collection de groupes de sécurité réseau, assurez-vous que ces [URL et ports](remoteapp-ports.md) sont accessibles à partir de votre sous-réseau.

Vous pouvez ajouter le réseau supplémentaires sécurité groupes toohello les ordinateurs virtuels déployés par vous dans un sous-réseau hello pour un contrôle plus strict.

## <a name="are-you-using-your-own-dns-servers-and-are-they-accessible-from-your-vnet-subnet"></a>Utilisez-vous vos propres serveurs DNS ? Et sont-ils accessibles à partir de votre sous-réseau de réseau virtuel ?
> [!NOTE]
> Vous avez toomake hello que les serveurs DNS dans votre réseau virtuel sont toujours des et toujours en mesure de tooresolve hello virtuels hébergés dans hello réseau virtuel. N'utilisez pas Google DNS pour cela.
> 
> 

Pour les collections hybrides, vous utilisez vos propres serveurs DNS. Vous spécifiez les dans votre schéma de configuration réseau ou via le portail de gestion hello lorsque vous créez votre réseau virtuel. Serveurs DNS sont utilisés dans l’ordre de hello qu’elles sont spécifiées sous forme de basculement (en opposition tooround (Round Robin)).  
Reportez-vous trop[résolution de noms pour les machines virtuelles et Instances de rôle](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) toomake que vos serveurs DNS sont correcly configuré.

Assurez-vous que les serveurs DNS hello pour votre collection sont accessibles et disponibles à partir du sous-réseau de réseau virtuel hello que vous avez spécifié pour cette collection.

Par exemple :

    <VirtualNetworkConfiguration>
    <Dns>
      <DnsServers>
        <DnsServer name="" IPAddress=""/>
      </DnsServers>
    </Dns>
    </VirtualNetworkConfiguration>

![Définition de votre serveur DNS](./media/remoteapp-hybridtrouble/dnsvpn.png)

## <a name="are-you-using-an-active-directory-domain-controller-in-your-collection"></a>Utilisez-vous un contrôleur de domaine Active Directory dans votre collection ?
Actuellement, un seul domaine Active Directory peut être associé à Azure RemoteApp. collection de hybride Hello prend en charge uniquement les comptes Azure Active Directory qui ont été synchronisés à l’aide d’outil de synchronisation d’annuaire à partir d’un déploiement de Windows Server Active Directory ; plus précisément, soit synchronisé avec l’option de synchronisation de mot de passe de hello soit synchronisé avec fédération des Services de fédération Active Directory (AD FS) configurée. Vous devez toocreate un domaine personnalisé qui correspond au suffixe de domaine hello pour votre domaine local et configurez l’intégration d’annuaire.

Consultez la page [Configuration d’Active Directory pour Azure RemoteApp](remoteapp-ad.md) pour plus d’informations.

Assurez-vous que les informations de domaine hello fournies sont valides et contrôleur de domaine hello est accessible à partir de hello que machine virtuelle créée dans le sous-réseau de hello utilisé pour l’application Azure à distance. Veillez également à ce compte de service hello informations d’identification fournies ont des autorisations tooadd ordinateurs toohello autant de domaine et qui hello nom AD fourni peut être résolu à partir de hello DNS fourni dans hello réseau virtuel.

## <a name="what-domain-name-did-you-specify-when-you-created-your-collection"></a>Quel nom de domaine avez-vous spécifié lorsque vous avez créé votre collection ?
nom de domaine Hello vous avez créé ou ajouté doit être un nom de domaine interne (pas votre nom de domaine Azure AD) et doit être au format DNS pouvant être résolu (contoso.local). Par exemple, vous avez un nom interne de Active Directory (contoso.local) et un UPN de répertoire (contoso.com) - Active que nom interne de toouse hello lorsque vous créez votre collection.

