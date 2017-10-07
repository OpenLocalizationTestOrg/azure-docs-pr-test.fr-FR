---
title: "Configurer une passerelle VPN : portail classique : Azure | Microsoft Docs"
description: "Cet article vous indique comment configurer votre passerelle VPN de réseau virtuel et comment modifier un type de routage VPN de passerelle. Ces étapes s’appliquent toohello déploiement classique modèle et hello portail classique."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: fbe59ba8-b11f-4d21-9bb1-225ec6c6d351
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/04/2017
ms.author: cherylmc
ms.openlocfilehash: 00d2fa18bab6eb24b33ddb18113f2a557db638d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vpn-gateway-in-hello-classic-portal"></a>Configurez une passerelle VPN dans le portail classique de hello 
Si vous souhaitez toocreate une connexion intersite sécurisée entre Azure et votre emplacement local, vous devez toocreate une passerelle de réseau virtuel. Une passerelle VPN est un type spécifique de passerelle de réseau virtuel. Dans le modèle de déploiement classique de hello, une passerelle VPN peut être un des deux types de routage VPN : statique ou dynamique. Hello type VPN que vous choisissez dépend de votre plan de conception de réseau et hello local VPN périphérique toouse. Pour plus d’informations sur les périphériques VPN, voir [À propos des périphériques VPN](vpn-gateway-about-vpn-devices.md).

**À propos des modèles de déploiement Azure**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-overview"></a>Présentation de la configuration
Hello étapes suivantes vous guident portail de configurer la passerelle VPN de hello classique. Ces étapes s’appliquent toogateways pour les réseaux virtuels qui ont été créés à l’aide du modèle de déploiement classique hello. Actuellement, tous les paramètres de configuration hello pour les passerelles sont disponibles dans hello portail Azure. Lorsqu’ils sont, nous allons créer un nouvel ensemble d’instructions qui s’appliquent toohello portail Azure.

### <a name="before-you-begin"></a>Avant de commencer
Avant de configurer votre passerelle, vous devez tout d’abord toocreate votre réseau virtuel. Pour les étapes toocreate un réseau virtuel pour la connectivité intersite, consultez [configurer un réseau virtuel avec une connexion VPN de site à site](vpn-gateway-site-to-site-create.md), ou [configurer un réseau virtuel avec une connexion VPN de point-to-site](vpn-gateway-point-to-site-create.md). Ensuite, utilisez hello suivant de passerelle VPN d’étapes tooconfigure hello et rassembler les informations de hello nécessaires tooconfigure votre périphérique VPN. 

Si vous disposez déjà d’une passerelle VPN et que vous souhaitez que le type de routage VPN hello toochange, consultez [comment toochange hello type de routage VPN pour votre passerelle](#how-to-change-the-vpn-routing-type-for-your-gateway).

## <a name="create-a-vpn-gateway"></a>Créer une passerelle VPN
1. Bonjour [portail Azure classic](https://manage.windowsazure.com), sur hello **réseaux** , vérifiez cette colonne de statut hello pour votre réseau virtuel est **créé**.
2. Bonjour **nom** colonne, cliquez sur nom hello de votre réseau virtuel.
3. Sur hello **tableau de bord** page, notez que ce réseau virtuel aucune passerelle n’est encore configurée. Vous verrez ce statut tout au long de hello étapes tooconfigure votre passerelle.

![Passerelle non créée](./media/vpn-gateway-configure-vpn-gateway-mp/IC717025.png)

Ensuite, hello en bas de page de hello, cliquez sur **créer une passerelle**. Vous pouvez sélectionner *Routage statique* ou *Routage dynamique*. Hello type routage VPN que vous sélectionnez dépend de plusieurs facteurs. Par exemple, que votre périphérique VPN prend en charge et si vous avez besoin de connexions de point-to-site toosupport. Vérifiez [sur des périphériques VPN pour la connectivité de réseau virtuel](vpn-gateway-about-vpn-devices.md) tooverify hello type de routage VPN dont vous avez besoin. Une fois que la passerelle de hello a été créé, vous ne pouvez pas modifier entre types routage de passerelle VPN sans supprimer et recréer hello passerelle. Lorsque hello système vous demande tooconfirm que vous souhaitez hello passerelle créée, cliquez sur **Oui**.

![Type de routage VPN de passerelle](./media/vpn-gateway-configure-vpn-gateway-mp/IC717026.png)

Lors de la création de la passerelle, notez le graphique de la passerelle hello sur la page de hello modifie tooyellow et indique *création d’une passerelle*. Cela peut prendre jusqu'à minutes too45 hello passerelle toocreate. Attendez que la passerelle de hello est terminée avant de pouvoir déplacer vers l’avant avec d’autres paramètres de configuration.

![Création de passerelle](./media/vpn-gateway-configure-vpn-gateway-mp/IC717027.png)

Lorsque de trop hello modifications de la passerelle*connexion*, vous pouvez collecter des informations de hello vous aurez besoin pour votre périphérique VPN.

![Connexion de passerelle](./media/vpn-gateway-configure-vpn-gateway-mp/IC717028.png)

## <a name="site-to-site-connections"></a>Connexions site à site

### <a name="step-1-gather-information-for-your-vpn-device-configuration"></a>Étape 1. Collecter des informations pour la configuration de votre périphérique VPN
Si vous créez une connexion Site à Site, une fois hello passerelle a été créée, collecter des informations pour la configuration de votre périphérique VPN. Ces informations se trouvent sur hello **tableau de bord** page de votre réseau virtuel :

1. **Adresse IP de passerelle -** adresse hello se trouvent sur hello **tableau de bord** page. Vous ne serez pas en mesure de toosee il jusqu'à ce que votre passerelle a terminé la création.
2. **Clé partagée -** cliquez sur **gérer la clé** bas hello écran hello. Cliquez sur hello icône suivant toohello clé toocopy il tooyour Presse-papiers, puis coller et enregistrer la clé de hello. Ce bouton ne fonctionne qu’avec un tunnel VPN S2S unique. Si vous avez plusieurs tunnels VPN de S2S, utilisez hello *Get Virtual Network Gateway Shared Key* API ou une cmdlet PowerShell.

![Gérer la clé](./media/vpn-gateway-configure-vpn-gateway-mp/IC717029.png)

### <a name="step-2--configure-your-vpn-device"></a>Étape 2.  Configuration de votre périphérique VPN
Réseau local de tooan connexions site à Site requièrent un périphérique VPN. Pendant que nous ne fournissent pas les étapes de configuration pour tous les périphériques VPN, vous trouverez des informations de hello Bonjour suivant liens utiles :

- Pour plus d’informations sur les périphériques VPN compatibles, consultez la page [Périphériques VPN](vpn-gateway-about-vpn-devices.md). 
- Pour les paramètres de configuration toodevice liens, consultez [des périphériques VPN validés](vpn-gateway-about-vpn-devices.md#devicetable). Ces liens sont fournis dans la mesure du possible. Il est toujours meilleure toocheck avec le fabricant de votre appareil pour les dernières informations de configuration hello.
- Pour plus d’informations sur la modification des exemples de configuration des périphériques, consultez la page [Modifier les exemples](vpn-gateway-about-vpn-devices.md#editing).
- En ce qui concerne les paramètres IPsec/IKE, consultez la page [Paramètres](vpn-gateway-about-vpn-devices.md#ipsec).
- Avant de configurer votre périphérique VPN, recherchez les [des problèmes de compatibilité des appareils](vpn-gateway-about-vpn-devices.md#known) pour le périphérique VPN de hello que vous souhaitez toouse.

Lorsque vous configurez votre périphérique VPN, vous devez hello éléments suivants :

- Hello adresse IP publique de votre passerelle de réseau virtuel. Vous pouvez localiser l’il en va de toohello **vue d’ensemble** panneau pour votre réseau virtuel.
- Une clé partagée. Cela est hello même partagé clé que vous spécifiez lors de la création de votre connexion VPN de Site à Site. Dans nos exemples, nous utilisons une clé partagée très basique. Vous devez générer un toouse de clé plus complexe.

Une fois le périphérique VPN de hello a été configuré, vous pouvez afficher vos informations de connexion mises à jour sur la page du tableau de bord hello pour votre réseau virtuel.

### <a name="step-3-verify-your-local-network-ranges-and-vpn-gateway-ip-address"></a>Étape 3. Vérifier vos plages de réseau local et l’adresse IP de la passerelle VPN
#### <a name="verify-your-vpn-gateway-ip-address"></a>Vérifier votre adresse IP de passerelle VPN
Pour la passerelle tooconnect correctement, hello adresse IP de votre périphérique VPN doit être correctement configurée pour hello réseau Local que vous avez spécifié pour votre configuration entre différents locaux. En règle générale, il est configuré au cours du processus de configuration de site à site hello. Toutefois, si vous avez déjà utilisé ce réseau local avec un autre périphérique ou adresse IP de hello a été modifiée pour ce réseau local, modifiez hello paramètres toospecify hello passerelle une adresse IP correcte.

1. tooverify votre adresse IP de passerelle, cliquez sur **réseaux** sur hello du volet gauche du portail, puis sélectionnez **réseaux locaux** en hello haut hello. Vous verrez hello adresse de passerelle VPN pour chaque réseau local que vous avez créés. adresse IP de hello tooedit, sélectionnez hello réseau virtuel et cliquez sur **modifier** bas hello de page de hello.
2. Sur hello **spécifier les détails de votre réseau local** page, modifier l’adresse IP de hello, puis cliquez sur la flèche suivant de hello bas hello de page de hello.
3. Sur hello **spécifier l’espace d’adressage hello** , cliquez sur coche hello sur toosave de droite inférieure hello vos paramètres.

#### <a name="verify-hello-address-ranges-for-your-local-networks"></a>Vérifiez que les plages d’adresses hello pour vos réseaux locaux
Hello tooflow de trafic approprié via l’emplacement hello passerelle tooyour local, vous devez tooverify que chaque plage d’adresses IP est spécifiée. Chaque plage doit être répertoriée dans la configuration **Réseaux locaux** d’Azure. Selon la configuration de réseau hello de votre emplacement local, cela peut être une tâche laborieuse. Le trafic qui est lié à une adresse IP qui figure dans les plages hello répertorié sera envoyé via la passerelle VPN de réseau virtuel hello. Hello les plages que vous répertoriez ne doivent pas nécessairement toobe des plages privées, bien que vous pouvez tooverify votre configuration locale peut recevoir hello le trafic entrant.

les plages hello tooadd ou de modification d’un réseau Local, utilisez hello comme suit :

1. plages d’adresses IP tooedit hello pour un réseau local, cliquez sur **réseaux** sur hello du volet gauche du portail, puis sélectionnez **réseaux locaux** en hello haut hello. Dans le portail hello, hello plus simple façon tooview hello plages répertoriées est sur hello **modifier** page. toosee vos plages, sélectionnez hello réseau virtuel et cliquez sur **modifier** bas hello de page de hello.
2. Sur hello **spécifier les détails de votre réseau local** page, n’apportez aucune modification. Cliquez sur hello de flèche suivant en bas de hello de page de hello.
3. Sur hello **spécifier l’espace d’adressage hello** page, apportez vos modifications d’espace d’adresse réseau. Cliquez ensuite sur hello coche toosave votre configuration.

## <a name="how-tooview-gateway-traffic"></a>Comment le trafic de passerelle tooview
Vous pouvez afficher votre passerelle et le trafic de la passerelle depuis la page **Tableau de bord** de votre réseau virtuel.

Sur hello **tableau de bord** page, vous pouvez afficher les informations suivantes hello :

* quantité de Hello de données qui traversent votre passerelle, les données d’et de données sortantes.
* noms de Hello des serveurs DNS hello qui sont spécifiées pour votre réseau virtuel.
* connexion Hello entre votre passerelle et votre périphérique VPN.
* Hello partagé clé tooconfigure utilisé votre périphérique VPN de passerelle connexion tooyour.

## <a name="how-toochange-hello-vpn-routing-type-for-your-gateway"></a>Comment toochange hello type de routage VPN pour votre passerelle
Étant donné que certaines configurations de connectivité sont uniquement disponibles pour certains types de routage de passerelle, vous découvrirez peut-être que vous devez toochange hello passerelle VPN type de routage d’une passerelle VPN existante. Par exemple, vous voudrez tooadd connectivité de point-to-site tooan déjà site-à-site connexion existante qui possède une passerelle statique. Les connexions point à site nécessitent une passerelle dynamique. Cela signifie tooconfigure une connexion P2S, vous avez toochange votre type de routage VPN gateway toodynamic statique.

Si vous avez besoin de toochange une type de routage VPN de passerelle, vous allez supprimer la passerelle existante de hello et puis créer une passerelle avec un nouveau type de routage hello. Vous n’avez pas besoin toodelete hello entière toochange hello passerelle routage type de réseau virtuel.

Avant de modifier votre type de routage VPN de passerelle, être tooverify sûr que votre périphérique VPN prend en charge le type de routage hello que vous souhaitez toouse. exemples de configuration de routage nouvelle toodownload et vérification de spécifications de périphérique VPN, consultez [sur des périphériques VPN pour la connectivité de réseau virtuel](vpn-gateway-about-vpn-devices.md).

> [!IMPORTANT]
> Lorsque vous supprimez une passerelle VPN de réseau virtuel, hello adresse IP virtuelle affectée toohello passerelle est libérée. Lorsque vous recréez la passerelle de hello, une nouvelle adresse VIP est assignée tooit.
> 
> 

1. **Supprimer la passerelle VPN existante de hello.**
   
    Sur hello **tableau de bord** page de votre réseau virtuel, accédez bas toohello de page de hello et cliquez sur **Delete Gateway**. Attente de notification hello hello passerelle a été supprimé. Une fois que vous recevez une notification de hello sur l’écran hello que votre passerelle a été supprimée, vous pouvez créer une nouvelle passerelle.
2. **Création d'une passerelle VPN.**
   
    Hello, procédez haut hello hello page toocreate une nouvelle passerelle : [créer une passerelle VPN](#create-a-vpn-gateway).

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez ajouter le réseau virtuel tooyour de machines virtuelles. Consultez [comment toocreate une machine virtuelle personnalisée](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Si vous voulez tooconfigure un point-to-site VPN, consultez [configurer une connexion VPN de point-to-site](vpn-gateway-point-to-site-create.md).

