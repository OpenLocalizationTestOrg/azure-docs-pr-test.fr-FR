---
title: "configuration de l’appareil StorSimple hello aaaModify | Documents Microsoft"
description: "Décrit comment toouse hello tooreconfigure du service StorSimple Manager, un appareil StorSimple qui a déjà été déployé."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: bb679264-8d46-429c-9ef7-630dc3b4a423
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/19/2017
ms.author: v-sharos
ms.openlocfilehash: 10a54c191260bf1baba58d28cdbfa0ed72217f48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomodify-your-storsimple-device-configuration"></a>Utilisez hello StorSimple Manager service toomodify votre configuration de l’appareil StorSimple
## <a name="overview"></a>Vue d'ensemble
Hello portail Azure classic **configurer** page contient tous les paramètres de périphérique hello que vous pouvez reconfigurer sur un appareil StorSimple qui est géré par un service StorSimple Manager. Ce didacticiel explique comment vous pouvez utiliser hello **configurer** hello tooperform de page suivant de tâches au niveau de l’appareil :

* Modification des paramètres de l’appareil 
* Modification des paramètres d’heure 
* Modification des paramètres DNS 
* Modification des interfaces réseau
* Échange ou réaffectation d’adresses IP

## <a name="modify-device-settings"></a>Modification des paramètres de l’appareil
paramètres de périphérique Hello incluent le nom convivial de hello d’appareil que hello et la description du périphérique hello.

> [!NOTE] 
> Vous ne pouvez pas modifier le nom du périphérique hello Bonjour portail Azure classic. Changement de nom du périphérique de hello n’est pas pris en charge.

Un appareil StorSimple qui est connecté toohello service StorSimple Manager est attribué un nom par défaut. nom Hello reflète généralement hello numéro de série du périphérique de hello. Par exemple, le nom de périphérique par défaut est de 15 caractères, tels que 8600-SHX0991003G44HT, indique suivant de hello :

* **8600** – modèle de périphérique indique hello.
* **SHX** – site de fabrication indique hello.
* **0991003** : indique un produit spécifique.
* **G44HT**- hello 5 derniers chiffres sont toocreate incrémentation des numéros de série uniques. Il ne s’agit pas nécessairement d’une suite.

Vous pouvez définir une description de l’appareil. Une description de périphérique permet généralement d’identifier le propriétaire de hello et l’emplacement physique de hello du périphérique de hello. champ de description Hello doit contenir moins de 256 caractères.

## <a name="modify-time-settings"></a>Modification des paramètres d’heure
Votre appareil doit être synchronisée dans l’ordre tooauthenticate avec votre fournisseur de service de stockage cloud. Sélectionnez votre fuseau horaire à partir de la liste déroulante de hello et spécifier des serveurs de protocole NTP (Network Time) tootwo. le serveur NTP principal Hello est requis et est spécifié lorsque vous utilisez Windows PowerShell pour StorSimple tooconfigure votre appareil. Vous pouvez spécifier la valeur par défaut de hello Windows Server **time.windows.com** que votre serveur NTP. Vous pouvez afficher hello principale configuration du serveur NTP via hello portail Azure classic, mais vous devez utiliser hello Windows PowerShell interface toochange il.

configuration du serveur NTP secondaire Hello est facultative. Vous pouvez utiliser un serveur NTP secondaire à hello classique tooconfigure portail. 

Lorsque vous configurez le serveur NTP hello, assurez-vous que votre réseau permet toopass de trafic NTP hello à partir de votre toohello de centre de données Internet. Lorsque vous spécifiez un serveur NTP public, il se peut que vous devez vous assurer que vos pare-feu réseau et autres périphériques de sécurité sont configurés tooallow NTP trafic tootravel tooand de hello en dehors du réseau. Si le trafic NTP bidirectionnel n’est pas autorisé, vous devez utiliser un serveur NTP interne (un contrôleur de domaine Windows assure cette fonction). Si votre appareil ne peut pas être synchronisée, il ne peut pas être en mesure de toocommunicate avec votre fournisseur de stockage cloud.

toosee une liste des serveurs NTP publics, accédez toohello [Web des serveurs NTP](http://support.ntp.org/bin/view/Servers/WebHome). 

### <a name="what-happens-if-hello-device-is-deployed-in-a-different-time-zone"></a>Que se passe-t-il si l’appareil de hello est déployé dans un fuseau horaire différent ?
Si l’appareil de hello est déployé dans un autre fuseau horaire, fuseau horaire hello change. Étant donné que toutes les stratégies de sauvegarde hello utilisent hello fuseau horaire, les stratégies de sauvegarde hello seront ajustent en fonction de hello du nouveau fuseau horaire. Aucune intervention de l’utilisateur n’est nécessaire.

## <a name="modify-dns-settings"></a>Modification des paramètres DNS
Un serveur DNS est utilisé lorsque votre appareil tente de toocommunicate avec votre fournisseur de service de stockage cloud. Pour la haute disponibilité, vous tooconfigure requis à la fois hello principal et hello des serveurs DNS secondaires durant le déploiement de périphérique initial hello. tooreconfigure hello serveur DNS principal, vous devez interface Windows PowerShell de hello toouse sur votre appareil StorSimple.

toomodify hello serveur DNS secondaire, vous pouvez utiliser hello portail Azure classic.

## <a name="modify-network-interfaces"></a>Modification des interfaces réseau
Votre appareil dispose de six interfaces réseau, dont quatre sont de type 1 Gigabit Ethernet, les deux autres étant de type 10 Gigabit Ethernet. Ces interfaces sont désignées par les intitulés DATA 0 à DATA 5. Ainsi, DATA 0, DATA 1, DATA 4 et DATA 5 sont des interfaces réseau 1 Gigabit Ethernet, tandis que DATA 2 et DATA 3 sont de type 10 Gigabit Ethernet.

Configurer **paramètres d’Interface réseau** pour chacun des hello interfaces toobe est utilisé. tooensure haute disponibilité, nous vous recommandons d’avoir au moins deux interfaces iSCSI et deux interfaces activé pour le cloud sur votre appareil. Nous vous recommandons, sans que cela soit obligatoire, de désactiver les interfaces non utilisées.

Lorsque vous configurez une des interfaces réseau de hello, vous devez configurer un IP virtuelle (VIP).

Par défaut, DATA 0 est compatible cloud. Lorsque vous configurez DATA 0, vous sont également requis tooconfigure deux adresses IP fixes, une pour chaque contrôleur. Ces adresses IP fixes peuvent être des contrôleurs de périphérique hello tooaccess utilisés directement et sont utiles lorsque vous installez des mises à jour sur l’appareil de hello ou lorsque vous accédez aux contrôleurs hello pour objectif hello.

Dans StorSimple 8000 Series Update 1, métrique de routage hello de DATA 0 a la valeur toohello plus bas ; Par conséquent, si votre appareil est en cours d’exécution StorSimple 8000 Series Update 1, tout le trafic de nuage hello sera routé via DATA 0. Prenez-en note au cas où vous disposeriez de plusieurs interfaces réseau compatibles cloud sur votre appareil StorSimple.

> [!NOTE]
> Hello fixe d’adresses IP pour le contrôleur de hello sont utilisées pour la maintenance des appareils de toohello hello mises à jour. Par conséquent, hello adresses IP fixé doit être routables et capables de tooconnect toohello Internet.
> 
> 

Pour chaque interface réseau, hello paramètres suivants s’affichent :

* **Vitesse** : paramètre non configurable par l’utilisateur. DATA 0, DATA 1, DATA 4 et DATA 5 sont toujours des interfaces réseau 1 Gigabit Ethernet, tandis que DATA 2 et DATA 3 sont des interfaces 10 Gigabit Ethernet.
  
  > [!NOTE]
  > La vitesse et le mode duplex sont toujours autonégociés. Les trames Jumbo ne sont pas prises en charge.
  > 
  > 
* **État de l’interface** : une interface peut être activée ou désactivée. S’il est activé, interface de hello toouse va tenter de périphérique de hello. Nous vous recommandons d’activer qu’uniquement les interfaces qui sont connectés toohello réseau et utilisés. Désactivez celles que vous n’utilisez pas.
* **Type d’interface** – ce paramètre vous permet de tooisolate le trafic iSCSI du trafic de stockage cloud. Ce paramètre peut être hello suivantes :
  
  * **Cloud activé** – activé, les appareils hello utilisera cette toocommunicate interface avec cloud de hello.
  * **compatible iSCSI** – activé, les appareils hello utilisera cette toocommunicate interface avec hôte iSCSI de hello.
    
    Nous vous recommandons d’isoler le trafic iSCSI du trafic de stockage cloud. Notez également si votre hôte est dans hello même sous-réseau que votre appareil, vous n’avez pas besoin de tooassign une passerelle ; Toutefois, si votre hôte est dans un sous-réseau différent de celui de votre appareil, vous devez tooassign une passerelle.
* **Adresse IP** : il peut s’agir d’une adresse IPv4 ou IPv6 ou les deux à la fois. Hello IPv4 et familles d’adresses IPv6 sont prises en charge pour les interfaces réseau hello. Quand vous utilisez IPv4, spécifiez une adresse IP 32 bits (*xxx.xxx.xxx.xxx*) en notation décimale à point. Quand vous utilisez IPv6, indiquez simplement un préfixe à 4 chiffres. Une adresse 128 bits sera alors générée automatiquement pour l’interface réseau de votre appareil à partir de ce préfixe.
* **Sous-réseau** – cela fait référence toohello le masque de sous-réseau et est configuré via l’interface Windows PowerShell de hello.
* **Passerelle** – il s’agit passerelle par défaut hello qui doit être utilisée par cette interface lorsqu’il tente de toocommunicate avec des nœuds qui ne sont pas dans hello même espace d’adressage IP (sous-réseau). Hello passerelle par défaut doit être Bonjour même espace d’adressage (sous-réseau) en tant qu’adresse IP de l’interface hello, comme déterminé par le masque de sous-réseau hello.
* **Adresse IP fixe** : ce champ est disponible uniquement lorsque vous configurez des hello DATA 0 interface. Pour les opérations telles que les mises à jour ou un périphérique de hello résolution des problèmes, vous devrez peut-être tooconnect directement le contrôleur de périphérique toohello. Hello, adresse IP fixé peut être utilisé tooaccess hello active et contrôleur passif de hello sur votre appareil.

Vous pouvez reconfigurer les contrôleurs 0 et 1 via hello portail Azure classic.

> [!NOTE]
> * tooensure un bon fonctionnement, vérifiez que la vitesse de l’interface hello et duplex sur le commutateur de hello chaque interface de l’appareil est connecté à. Les interfaces du commutateur doivent négocier avec Gigabit Ethernet (1 000 Mbits/s) ou être configurées en conséquence et être en mode duplex intégral. Les interfaces fonctionnant à des vitesses plus lentes ou en mode semi-duplex entraîneront des problèmes de performances.
> * toominimize interruptions et autres interruptions de service, nous vous recommandons d’activer portfast sur chaque commutateur hello ports hello interface de réseau iSCSI de votre appareil doit se connecter à. Cela garantit que la connectivité réseau peut être établie rapidement en cas de hello d’un basculement.
> 
> 

## <a name="swap-or-reassign-ips"></a>Échange ou réaffectation d’adresses IP
Actuellement, si une interface réseau sur le contrôleur de hello est affecté une adresse IP virtuelle qui est en cours d’utilisation (par hello même appareil ou un autre périphérique de réseau de hello), puis hello contrôleur bascule. Par conséquent, vous devez procédure toofollow hello si vous échangez des adresses IP virtuelles pour l’interface de réseau du périphérique hello, car vous allez créer une situation IP en double.

Effectuer hello suivant les étapes tooswap ou réassigner les adresses IP virtuelles pour une des interfaces réseau de hello hello :

#### <a name="tooreassign-ips"></a>tooreassign des adresses IP
1. Adresse IP de hello clair pour les deux interfaces.
2. Une fois que les adresses IP de hello sont désactivées, affecter des adresses IP de la nouvelle hello toohello des interfaces correspondantes.

## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment trop[configurer MPIO pour votre appareil StorSimple](storsimple-configure-mpio-windows-server.md).
* Découvrez comment trop[utilisez hello tooadminister du service StorSimple Manager de votre appareil StorSimple](storsimple-manager-service-administration.md).

