---
title: "aaaCreate réseau de votre première virtuel Azure | Documents Microsoft"
description: "Découvrez comment toocreate un réseau virtuel de Azure (VNet), connectez les deux machines virtuelles (VM) toohello réseau virtuel et connecter les machines virtuelles de toohello."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2016
ms.author: jdial
ms.openlocfilehash: 1981524cf706d5ebc83b1ff77735617550ff058a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-virtual-network"></a>Créer votre premier réseau virtuel

Découvrez comment toocreate un réseau virtuel (VNet) avec deux sous-réseaux, créer deux machines virtuelles (VM) et les connecter tooone de chaque machine virtuelle de sous-réseaux de hello, comme indiqué dans hello illustration suivante :

![Diagramme de réseau virtuel](./media/virtual-network-get-started-vnet-subnet/vnet-diagram.png)

Un réseau virtuel Azure (VNet) est une représentation de votre propre réseau dans le cloud de hello. Vous pouvez contrôler les paramètres de votre réseau Azure et définir les blocs d’adresses DHCP, les paramètres DNS, les stratégies de sécurité et le routage. toolearn plus d’informations sur les concepts de réseau virtuel, lisez hello [présentation du réseau virtuel](virtual-networks-overview.md) l’article. Hello complet suivant les étapes toocreate hello les ressources d’image de hello :

1. [Créer un réseau virtuel avec deux sous-réseaux](#create-vnet)
2. [Créer deux machines virtuelles, chacune avec une interface réseau (NIC)](#create-vms)et associer un tooeach de groupe (NSG) de sécurité réseau NIC
3. [Se connecter tooand de hello machines virtuelles](#connect-to-from-vms)
4. [Supprimer toutes les ressources](#delete-resources) Peut occasionner des frais pour certaines des ressources hello créés dans cet exercice vous d’approvisionnement. frais de hello toominimize, après avoir terminé l’exercice de hello, veillez toocomplete hello les étapes dans cette section de ressources de hello toodelete vous créez.

Vous devez comprendre comment vous pouvez utiliser un réseau virtuel une fois hello effectuer les étapes de cet article. Étapes suivantes sont fournies pour plus d’informations sur la toouse réseaux virtuels à un niveau inférieur.

## <a name="create-vnet"></a>Créer un réseau virtuel avec deux sous-réseaux

toocreate un réseau virtuel avec deux sous-réseaux, les étapes hello complète qui suivent. Des sous-réseaux différents sont généralement utilisé des flux de hello toocontrol du trafic entre sous-réseaux.

1. Connectez-vous à toohello [portail Azure](<https://portal.azure.com>). Si vous ne possédez pas encore de compte, vous pouvez [vous inscrire pour bénéficier d’un essai gratuit d’un mois](https://azure.microsoft.com/free). 
2. Bonjour **favoris** volet, du portail de hello, cliquez sur **nouveau**.
3. Bonjour **nouveau** panneau, cliquez sur **réseau**. Bonjour **réseau** panneau, cliquez sur **réseau virtuel**, comme indiqué dans hello illustration suivante :

    ![Diagramme de réseau virtuel](./media/virtual-network-get-started-vnet-subnet/virtual-network.png)

4.  Bonjour **réseau virtuel** panneau, laissez le champ *le Gestionnaire de ressources* sélectionné en tant que modèle de déploiement hello, puis cliquez sur **créer**.
5.  Bonjour **Panneau de réseau virtuel créer** qui s’affiche, entrez hello valeurs suivantes, puis cliquez sur **créer**:

    |**Paramètre**|**Valeur**|**Détails**|
    |---|---|---|
    |**Nom**|*MyVNet*|nom de Hello doit être unique au sein du groupe de ressources hello.|
    |**Espace d’adressage**|*10.0.0.0/16*|Vous pouvez spécifier l’espace d’adressage de votre choix en notation CIDR.|
    |**Nom du sous-réseau**|*Front-end*|nom du sous-réseau Hello doit être unique au sein du réseau virtuel de hello.|
    |**Plage d’adresses de sous-réseau**|*10.0.0.0/24*| plage Hello que vous spécifiez doit exister dans l’espace d’adressage hello que vous avez défini pour le réseau virtuel de hello.|
    |**Abonnement**|*[Votre abonnement]*|Sélectionnez un Bonjour de toocreate abonnement réseau virtuel dans. Un réseau virtuel existe dans un seul abonnement.|
    |**Groupe de ressources**|**Créer :***MyRG*|Créez un groupe de ressources. nom de groupe de ressources Hello doit être unique au sein de l’abonnement hello sélectionné. toolearn plus d’informations sur les groupes de ressources, lire hello [le Gestionnaire de ressources](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-groups) l’article de vue d’ensemble.|
    |**Emplacement**|*Ouest des États-Unis*| En général, emplacement hello qui est l’emplacement physique des tooyour le plus proche est sélectionné.|

    Bonjour réseau virtuel prend quelques secondes toocreate. Une fois qu’il est créé, vous voyez hello Azure tableau de bord de portail.

6. Avec un réseau virtuel hello créé, Bonjour Azure portal **favoris** volet, cliquez sur **toutes les ressources**. Cliquez sur hello **MyVNet** réseau virtuel dans hello **toutes les ressources** panneau. Si l’abonnement hello déjà sélectionné comporte plusieurs ressources, vous pouvez entrer *MyVNet* Bonjour **filtrer par nom...** hello de zone tooeasily accès réseau virtuel.
7. Hello **MyVNet** panneau s’ouvre et affiche des informations sur hello réseau virtuel, comme indiqué dans hello illustration suivante :

    ![Diagramme de réseau virtuel](./media/virtual-network-get-started-vnet-subnet/myvnet.png)

8. Comme indiqué dans l’image précédente de hello, cliquez sur **sous-réseaux** toodisplay une liste de sous-réseaux hello dans hello réseau virtuel. Bonjour uniquement sur le sous-réseau existant est **frontal**, hello sous-réseau que vous avez créé à l’étape 5.
9. Bonjour MyVNet - Panneau de sous-réseaux, cliquez sur **+ sous-réseau** toocreate un sous-réseau avec hello suivant des informations et cliquez sur **OK** sous-réseau de hello toocreate :

    |**Paramètre**|**Valeur**|**Détails**|
    |---|---|---|
    |**Nom**|*Back-end*|nom de Hello doit être unique au sein du réseau virtuel de hello.|
    |**Plage d’adresses**|*10.0.1.0/24*|plage Hello que vous spécifiez doit exister dans l’espace d’adressage hello que vous avez défini pour le réseau virtuel de hello.|
    |**Groupe de sécurité réseau** et **Table de routage**|*Aucun* (par défaut)|Les groupes de sécurité réseau (NSG) sont traités plus loin dans cet article. toolearn plus d’informations sur les itinéraires définis par l’utilisateur, lecture hello [itinéraires définis par l’utilisateur](virtual-networks-udr-overview.md) l’article.|

10. Une fois hello nouveau sous-réseau est ajouté toohello réseau virtuel, vous pouvez fermer hello **MyVNet – sous-réseaux** panneau, puis fermer hello **toutes les ressources** panneau.

## <a name="create-vms"></a>Créer des machines virtuelles

Avec hello réseau virtuel et sous-réseaux créés, vous pouvez créer des machines virtuelles de hello. Bien que dans cet exercice, les deux ordinateurs virtuels exécuter hello système d’exploitation Windows, ils peuvent exécuter n’importe quel système d’exploitation pris en charge par Azure, y compris plusieurs différentes distributions de Linux.

### <a name="create-web-server-vm"></a>Créer la machine virtuelle du serveur web hello

toocreate hello web server machine virtuelle, hello complète comme suit :

1. Dans le volet des Favoris portail Azure hello, cliquez sur **nouveau**, **de calcul**, puis **Windows Server 2016 Datacenter**.
2. Bonjour **Windows Server 2016 Datacenter** panneau, cliquez sur **créer**.
3. Bonjour **notions de base** panneau qui s’affiche, entrez ou sélectionnez hello valeurs suivantes, puis cliquez sur **OK**:

    |**Paramètre**| **Valeur**|**Détails**|
    |---|---|---|
    |**Nom**|*MyWebServer*|Cette machine virtuelle fonctionne comme un serveur web auquel les ressources Internet se connectent.|
    |**Type de disque de machine virtuelle**|*SSD*|
    |**Nom d'utilisateur**|*Votre choix*|
    |**Mot de passe et Confirmer le mot de passe**|*Votre choix*|
    | **Abonnement**|*<Your subscription>*|Hello abonnement doit être hello même abonnement que vous avez sélectionné à l’étape 5 de hello [créer un réseau virtuel avec deux sous-réseaux](#create-vnet) section de cet article. Hello réseau virtuel que vous vous connectez un ordinateur virtuel toomust existe Bonjour même abonnement que hello de machine virtuelle.|
    |**Groupe de ressources**|**Utiliser existant :** sélectionnez *MyRG*|Bien que nous utilisons hello même groupe de ressources comme nous l’avons fait pour hello réseau virtuel, hello ressources n’ont pas tooexist dans hello même groupe de ressources.|
    |**Emplacement**|*Ouest des États-Unis*|Hello emplacement doit être hello même emplacement que vous avez spécifié à l’étape 5 de hello [créer un réseau virtuel avec deux sous-réseaux](#create-vnet) section de cet article. Machines virtuelles et hello qu’ils connectent toomust des réseaux virtuels existent dans hello même emplacement.|

4. Bonjour **choisir une taille** panneau, cliquez sur *DS1_V2 Standard*, puis cliquez sur **sélectionnez**. Hello de lecture [tailles de machine virtuelle Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) l’article pour obtenir la liste de toutes les tailles de machine virtuelle Windows pris en charge par Azure.
5. Bonjour **paramètres** panneau, entrez ou sélectionnez hello valeurs suivantes, puis cliquez sur **OK**:

    |**Paramètre**|**Valeur**|**Détails**|
    |---|---|---|
    |**Stockage : Utiliser des disques gérés**|*Oui*||
    |**Réseau virtuel**| Sélectionner *MyVNet*|Vous pouvez sélectionner n’importe quel réseau virtuel qui existe dans hello même emplacement que hello machine virtuelle que vous créez. toolearn plus d’informations sur les réseaux virtuels et des sous-réseaux, lire hello [réseau virtuel](virtual-networks-overview.md) l’article.|
    |**Sous-réseau**|Sélectionner *Front-end*|Vous pouvez sélectionner n’importe quel sous-réseau existe dans hello réseau virtuel.|
    |**Adresse IP publique**|Accepter la valeur par défaut de hello|Une adresse IP publique permet de vous tooconnect toohello machine virtuelle à partir de hello Internet. toolearn plus d’informations sur les adresses IP publiques, lire hello [des adresses IP](virtual-network-ip-addresses-overview-arm.md#public-ip-addresses) l’article.|
    |**Groupe de sécurité réseau (pare-feu)**|Accepter la valeur par défaut de hello|Cliquez sur hello **MyWebServer (nouvelle)-nsg** portail hello de groupe de sécurité réseau par défaut créé tooview ses paramètres. Bonjour **créer un groupe de sécurité réseau** panneau qui s’ouvre, notez qu’il en a un règle qui autorise le trafic TCP/3389 (RDP) à partir de n’importe quelle adresse IP de source de trafic entrant.|
    |**Toutes les autres valeurs**|Acceptez les valeurs par défaut hello|toolearn plus en détail hello restant de paramètres, lire hello [sur les machines virtuelles](../virtual-machines/windows/overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json) l’article.|

    Groupes de sécurité réseau (NSG) permettent de toocreate des règles entrantes/sortantes de type hello du trafic réseau qui peut circuler tooand à partir de la machine virtuelle de hello. Par défaut, tout le trafic entrant toohello machine virtuelle est refusé. Vous pouvez ajouter d’autres règles de trafic entrant pour TCP/80 (HTTP) et TCP/443 (HTTPS) pour un serveur web de production. Il n’existe aucune règle pour le trafic sortant car, par défaut, tout le trafic sortant est autorisé. Vous pouvez ajouter ou supprimer le trafic de règles toocontrol par vos stratégies. Hello de lecture [groupes de sécurité réseau](virtual-networks-nsg.md) toolearn article plus d’informations sur les groupes de sécurité réseau.

6.  Bonjour **Résumé** panneau, passez en revue les paramètres hello et cliquez sur **OK** toocreate hello machine virtuelle. Une vignette de l’état est affichée sur le tableau de bord de portail hello comme hello crée de la machine virtuelle. Il peut prendre quelques minutes toocreate. Vous n’avez pas besoin toowait pour qu’il toocomplete. Vous pouvez continuer toohello prochaine étape lors hello que machine virtuelle est créée.

### <a name="create-database-server-vm"></a>Créer la machine virtuelle du serveur de base de données hello

toocreate hello serveur base de données machine virtuelle, hello complète comme suit :

1.  Dans le volet des Favoris hello, cliquez sur **nouveau**, **de calcul**, puis **Windows Server 2016 Datacenter**.
2.  Bonjour **Windows Server 2016 Datacenter** panneau, cliquez sur **créer**.
3.  Bonjour **panneau des notions de base**, entrez ou sélectionnez hello valeurs suivantes, puis cliquez sur **OK**:

    |**Paramètre**|**Valeur**|**Détails**|
    |---|---|---|
    |**Nom**|*MyDBServer*|Cet ordinateur virtuel sert que hello web server se connecte à, mais ce hello Internet ne peut pas se connecter à un serveur de base.|
    |**Type de disque de machine virtuelle**|*SSD*||
    |**Nom d'utilisateur**|Votre choix||
    |**Mot de passe et Confirmer le mot de passe**|Votre choix||
    |**Abonnement**|<Your subscription>|Hello abonnement doit être hello même abonnement que vous avez sélectionné à l’étape 5 de hello [créer un réseau virtuel avec deux sous-réseaux](#create-vnet) section de cet article.|
    |**Groupe de ressources**|**Utiliser existant :** sélectionnez *MyRG*|Bien que nous utilisons hello même groupe de ressources comme nous l’avons fait pour hello réseau virtuel, hello ressources n’ont pas tooexist dans hello même groupe de ressources.|
    |**Emplacement**|*Ouest des États-Unis*|Hello emplacement doit être hello même emplacement que vous avez spécifié à l’étape 5 de hello [créer un réseau virtuel avec deux sous-réseaux](#create-vnet) section de cet article.|

4.  Bonjour **choisir une taille** panneau, cliquez sur *DS1_V2 Standard*, puis cliquez sur **sélectionnez**.
5.  Bonjour **paramètres** panneau, entrez ou sélectionnez hello valeurs suivantes, puis cliquez sur **OK**:

    |**Paramètre**|**Valeur**|**Détails**|
    |----|----|---|
    |**Stockage : Utiliser des disques gérés**|*Oui*||
    |**Réseau virtuel**|Sélectionner *MyVNet*|Vous pouvez sélectionner n’importe quel réseau virtuel qui existe dans hello même emplacement que hello machine virtuelle que vous créez.|
    |**Sous-réseau**|Sélectionnez *Back-end* en cliquant sur hello **sous-réseau** zone, puis en sélectionnant **Back-end** de hello **choisissez un sous-réseau** panneau|Vous pouvez sélectionner n’importe quel sous-réseau existe dans hello réseau virtuel.|
    |**Adresse IP publique**|None : cliquez sur l’adresse hello par défaut, puis cliquez sur **aucun** de hello **choisir une adresse IP publique** panneau|Sans une adresse IP publique, vous ne pouvez connecter toohello machine virtuelle à partir d’une autre machine virtuelle connectée toohello même réseau virtuel. Tooit Impossible de se connecter directement à partir de hello Internet.|
    |**Groupe de sécurité réseau (pare-feu)**|Accepter la valeur par défaut de hello| Comme valeur par défaut de hello que NSG créée pour hello MyWebServer VM, ce groupe de sécurité réseau, également a hello même par défaut de règle de trafic entrant. Vous pouvez ajouter une nouvelle règle de trafic entrant pour TCP/1433 (MS SQL) pour un serveur de base de données. Il n’existe aucune règle pour le trafic sortant car, par défaut, tout le trafic sortant est autorisé. Vous pouvez ajouter ou supprimer le trafic de règles toocontrol par vos stratégies.|
    |**Toutes les autres valeurs**|Acceptez les valeurs par défaut hello||

6.  Bonjour **Résumé** panneau, passez en revue les paramètres hello et cliquez sur **OK** toocreate hello machine virtuelle. Une vignette de l’état est affichée sur le tableau de bord de portail hello comme hello crée de la machine virtuelle. Il peut prendre quelques minutes toocreate. Vous n’avez pas besoin toowait pour qu’il toocomplete. Vous pouvez continuer toohello prochaine étape lors hello que machine virtuelle est créée.

## <a name="review"></a>Passer en revue les ressources

Si vous avez créé un réseau virtuel et deux machines virtuelles, hello portail Azure créé plusieurs ressources supplémentaires pour vous dans le groupe de ressources MyRG hello. Passez en revue le contenu hello hello MyRG du groupe de ressources en effectuant hello comme suit :

1. Bonjour **favoris** volet, cliquez sur **davantage de services**.
2. Bonjour **davantage de services** volet, tapez *groupes de ressources* dans zone de hello comportant des analyseurs de hello *filtre* qu’il contient. Cliquez sur **groupes de ressources** lorsque vous voyez Bonjour liste filtrée.
3. Bonjour **groupes de ressources** volet, cliquez sur hello *MyRG* groupe de ressources. Si vous avez plusieurs groupes de ressources existant dans votre abonnement, vous pouvez taper *MyRG* dans la zone hello qui contient le texte hello *filtrer par nom...* groupe de ressources MyRG tooquickly accès hello.
4.  Bonjour **MyRG** panneau, vous voyez ce groupe de ressources hello contienne 12 ressources, comme indiqué dans hello illustration suivante :

    ![Contenu du groupe de ressources](./media/virtual-network-get-started-vnet-subnet/resource-group-contents.png)

toolearn plus d’informations sur les machines virtuelles, les disques et les comptes de stockage, lire hello [virtuels](../virtual-machines/windows/overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [disque](../virtual-machines/windows/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-network%2ftoc.json), et [compte de stockage](../storage/common/storage-introduction.md?toc=%2fazure%2fvirtual-network%2ftoc.json) articles de vue d’ensemble. Vous pouvez voir hello deux groupes de sécurité réseau hello portail de par défaut créé pour vous. Vous pouvez également voir ce portail hello créé deux ressources d’interface (NIC) de réseau. Une carte réseau permet à un ordinateur virtuel tooconnect tooother des ressources sur hello réseau virtuel. Hello de lecture [NIC](virtual-network-network-interface.md) toolearn article plus d’informations sur les cartes réseau. portail Hello également créé une ressource d’adresse IP publique. Les adresses IP publiques correspondent à un paramètre de configuration d’une ressource d’adresse IP publique. toolearn plus d’informations sur les adresses IP publiques, lire hello [des adresses IP](virtual-network-ip-addresses-overview-arm.md#public-ip-addresses) l’article.

## <a name="connect-to-from-vms"></a>Connecter les machines virtuelles de toohello

Avec votre réseau virtuel et deux machines virtuelles créées, vous pouvez désormais connecter des machines virtuelles de toohello en effectuant les étapes hello Bonjour les sections suivantes :

### <a name="connect-from-internet"></a>Se connecter toohello machine virtuelle du serveur web à partir de hello Internet

tooconnect toohello web machine virtuelle du serveur à partir de hello Internet, hello complète comme suit :

1. Dans le portail hello, groupe de ressources MyRG hello ouvert en effectuant hello étapes Bonjour [passez en revue les ressources](#review) section de cet article.
2. Bonjour **MyRG** panneau, cliquez sur hello **MyWebServer** machine virtuelle.
3. Bonjour **MyWebServer** panneau, cliquez sur **connexion**, comme indiqué dans hello illustration suivante :

    ![Connecter la machine virtuelle du serveur tooweb](./media/virtual-network-get-started-vnet-subnet/webserver.png)

4. Autoriser votre hello toodownload de navigateur *MyWebServer.rdp* de fichier, puis ouvrez-le.
5. Si vous recevez une boîte dialogue informant vous cet éditeur hello de connexion à distance de hello ne peut pas être vérifié, cliquez sur **connexion**.
6. Lorsque vous entrez vos informations d’identification, assurez-vous de vous connecter avec un nom d’utilisateur hello et un mot de passe spécifié à l’étape 3 de hello [machine virtuelle du serveur web créer hello](#create-web-server-vm) section de cet article. Si hello **sécurité Windows** boîte qui apparaît n’affiche pas les informations d’identification correctes hello, vous devrez peut-être tooclick **plus de choix**, puis **utiliser un autre compte**, de sorte que vous pouvez Spécifiez un mot de passe et nom d’utilisateur hello). Cliquez sur **OK** tooconnect toohello machine virtuelle.
7. Si vous recevez un **connexion Bureau à distance** zone indique que hello l’identité de l’ordinateur distant de hello ne peut pas être vérifié, cliquez sur **Oui**.
8. Vous êtes maintenant connecté toohello MyWebServer VM à partir de hello Internet. Laissez des étapes de hello toocomplete ouvrir Connexion Bureau à distance de hello dans la section suivante de hello.

connexion à distance de Hello est l’adresse IP publique toohello affecté toohello publique IP adresse ressource hello portail créé à l’étape 5 de hello [créer un réseau virtuel avec deux sous-réseaux](#create-vnet) section de cet article. connexion de Hello est autorisée, car il est créé de règle par défaut de hello Bonjour **MyWebServer-nsg** NSG autorisé TCP/3389 (RDP) entrants toohello machine virtuelle à partir de toute adresse IP source. Si vous essayez tooconnect toohello machine virtuelle sur un autre port, connexion de hello échoue, sauf si vous ajoutez des règles de trafic entrant supplémentaires toohello NSG autoriser hello des ports supplémentaires.

>[!NOTE]
>Si vous ajoutez des règles de trafic entrant supplémentaires toohello groupe de sécurité réseau, vérifiez que hello mêmes ports sont ouverts sur le pare-feu Windows hello ou hello de connexion échoue.
>

### <a name="connect-to-internet"></a>Se connecter toohello Internet à partir de la machine virtuelle du serveur web hello

tooconnect toohello Internet sortant à partir du serveur web de hello machine virtuelle, hello complète comme suit :

1. Si vous n’avez pas encore un toohello de connexion à distance MyWebServerVM ouvrir, rendre un ordinateur virtuel de toohello connexion à distance en procédant comme hello Bonjour [Connect toohello web machine virtuelle du serveur à partir de hello Internet](#connect-from-internet) section de cet article.
2. À partir du bureau de Windows hello, ouvrez Internet Explorer. Bonjour **le programme d’installation Internet Explorer 11** boîte de dialogue, cliquez sur **n’utilisez pas les paramètres recommandés**, puis cliquez sur **OK**. Il est hello tooaccept recommandée paramètres recommandé pour un serveur de production.
3. Dans la barre d’adresses hello Internet Explorer, entrez [bing.com](http:www.bing.com). Si vous recevez une boîte de dialogue Internet Explorer, cliquez sur **ajouter**, puis **ajouter** Bonjour **sites de confiance** boîte de dialogue et cliquez sur **fermer**. Répétez ce processus pour les autres boîtes de dialogue Internet Explorer.
4. Page de recherche à hello Bing, entrez *whatsmyipaddress*, puis cliquez sur le bouton de loupe hello. Bing retourne hello publique IP adresse affectée toohello publique ressource d’adresse IP créée par le portail de hello lorsque vous avez créé hello machine virtuelle. Si vous examinez les paramètres de hello pour hello **MyWebServer-ip** ressource, vous voyez hello la même adresse IP affectée de ressource d’adresse IP publique toohello, comme indiqué dans l’image hello qui suit. Hello IP adresse affectée tooyour machine virtuelle est toutefois différentes.

    ![Connecter la machine virtuelle du serveur tooweb](./media/virtual-network-get-started-vnet-subnet/webserver-pip.png)

5.  Laissez des étapes de hello toocomplete ouvrir Connexion Bureau à distance de hello dans la section suivante de hello.

Vous êtes en mesure de tooconnect toohello Internet à partir de la machine virtuelle de hello, car toutes les connexion sortante à partir de la machine virtuelle de hello est autorisée par défaut. Vous pouvez limiter la connectivité sortante en ajoutant l’ajout des règles toohello NSG appliqué toohello NIC, hello de sous-réseau toohello carte réseau est connecté, ou les deux.

Si hello VM est placé dans hello arrêtée (désallouée) état à l’aide du portail de hello, adresse IP publique de hello peut changer. Si vous avez besoin que d’adresses IP publiques de hello jamais modifiées, vous pouvez utiliser la méthode d’allocation statique hello pour l’adresse IP de hello, plutôt que la méthode d’allocation dynamique hello (qui est la valeur par défaut hello). toolearn en savoir plus sur hello des différences entre les méthodes d’allocation, lire hello [types et méthodes d’allocation d’adresses IP](virtual-network-ip-addresses-overview-arm.md) l’article.

### <a name="webserver-to-dbserver"></a>Connecter la machine virtuelle du serveur de base de données toohello à partir de la machine virtuelle du serveur web hello

tooconnect toohello de base de données machine virtuelle du serveur à partir du serveur web de hello machine virtuelle, hello complète comme suit :

1. Si vous n’avez pas encore un toohello de connexion à distance MyWebServer VM ouvrir, rendre un ordinateur virtuel de toohello connexion à distance en procédant comme hello Bonjour [Connect toohello web machine virtuelle du serveur à partir de hello Internet](#connect-from-internet) section de cet article.
2. Cliquez sur le bouton Démarrer de hello dans le coin inférieur gauche de hello du bureau de Windows hello, puis commencez à taper *Bureau à distance*. Lorsque la liste du menu Démarrer hello affiche **connexion Bureau à distance**, cliquez dessus.
3. Bonjour **connexion Bureau à distance** boîte de dialogue, entrez *MONSERVEURBD* hello nom d’ordinateur et cliquez sur **connexion**.
4. Entrez le nom d’utilisateur hello et mots de passe entrés à l’étape 3 de hello [machine virtuelle du serveur de base de données créer hello](#create-database-server-vm) section de cet article, puis cliquez sur **OK**.
5. Si vous recevez une boîte de dialogue informant vous cette identité hello de l’ordinateur distant de hello ne peut pas être vérifié, cliquez sur **Oui**.
6. Laissez connexion Bureau à distance de salutation serveurs tooboth toocomplete ouvrir hello les étapes dans la section suivante de hello.

Vous êtes toomake en mesure de hello connexion toohello de base de données machine virtuelle du serveur à partir de hello web machine virtuelle du serveur pour hello suivant raisons :

- TCP/3389 les connexions entrantes sont activées pour toutes les adresses IP source dans par défaut de hello NSG créé à l’étape 5 de hello [machine virtuelle du serveur de base de données créer hello](#create-database-server-vm) section de cet article.
- Vous avez lancé la connexion hello à partir du serveur web de hello machine virtuelle, qui est connecté toohello même réseau virtuel en tant que machine virtuelle du serveur de base de données hello. tooconnect tooa machine virtuelle qui n’a pas un tooit d’adresse IP publique, vous devez vous connecter à partir d’une autre machine virtuelle connectée toohello même réseau virtuel, même si hello machine virtuelle est connectée tooa autre sous-réseau.
- Bien que les machines virtuelles de hello sont les sous-réseaux connectés toodifferent, Azure crée des itinéraires par défaut qui activent la connectivité entre les sous-réseaux. Vous pouvez remplacer les itinéraires par défaut hello en créant votre propre toutefois. Hello de lecture [itinéraires définis par l’utilisateur](virtual-networks-udr-overview.md) toolearn article plus sur le routage dans Azure.

Si vous essayez de tooinitiate un serveur de base de données connexion à distance toohello machine virtuelle à partir de hello Internet, comme vous le faisiez hello [Connect toohello web machine virtuelle du serveur à partir de hello Internet](#connect-from-internet) section de cet article, vous voyez que hello **Connect** option est grisée. Se connecter est grisé, car il n’existe aucune toohello d’adresse IP publique machine virtuelle, tooit les connexions entrantes à partir de hello Internet ne sont pas possibles.

### <a name="connect-toohello-internet-from-hello-database-server-vm"></a>Se connecter toohello Internet à partir de la machine virtuelle du serveur de base de données hello

Connexion sortante toohello Internet à partir de la machine virtuelle du serveur de base de données hello en effectuant hello comme suit :

1. Si vous n’avez pas encore un toohello de connexion à distance MyDBServer VM ouvrir à partir de hello MyWebServer VM, hello terminé les étapes Bonjour [serveur de base de données se connecter toohello machine virtuelle à partir de la machine virtuelle du serveur web hello](#webserver-to-dbserver) section de cet article.
2. À partir du bureau de Windows hello sur hello MyDBServer VM, ouvrez Internet Explorer et répondre de boîtes de dialogue toohello comme vous le faisiez dans les étapes 2 et 3 de hello [connecter toohello Internet à partir de la machine virtuelle du serveur web hello](#connect-to-internet) section de cet article.
3. Dans la barre d’adresses hello, entrez [bing.com](http:www.bing.com).
4. Cliquez sur **ajouter** dans la boîte de dialogue Internet Explorer hello qui s’affiche, puis **ajouter**, puis **fermer** Bonjour **confiance** boîte de dialogue de sites. Effectuez ces étapes dans les boîtes de dialogue qui s’affichent.
5. Page de recherche à hello Bing, entrez *whatsmyipaddress*, puis cliquez sur le bouton de loupe hello. Bing retourne hello publique IP adresse actuellement affectée toohello VM par hello infrastructure Azure. 6. Fermez hello distant bureau toohello MyDBServer VM à partir de hello MyWebServer VM, puis toohello de connexion à distance hello MyWebServer VM.

Hello connexion sortante toohello Internet est autorisée, car tout le trafic sortant est autorisé par défaut, même si une ressource d’adresse IP publique n’est pas attribuée toohello MyDBServer VM. Tous les ordinateurs virtuels, par défaut, sont en mesure de tooconnect sortant toohello Internet, avec ou sans un toohello de ressource affectée adresse IP publique machine virtuelle. Vous n’êtes pas toohello tooconnect en mesure de public d’adresses IP à partir de hello Internet Toutefois, comme vous hello toofor en mesure de ressource affectée d’adresses MyWebServer VM qui a une adresse IP publique.

## <a name="delete-resources"></a>Supprimer toutes les ressources

toodelete toutes les ressources créées dans cet article, hello complète comme suit :

1. groupe de ressources tooview hello MyRG créé dans cet article, complète les étapes 1-3 les hello en [passez en revue les ressources](#review) section de cet article. Une fois encore, passez en revue les ressources hello dans le groupe de ressources hello. Si vous avez créé le groupe de ressources MyRG hello, par les étapes précédentes, vous consultez hello 12 ressources illustrées hello à l’étape 4.
2. Dans le panneau de MyRG hello, cliquez sur hello **supprimer** bouton.
3. Hello portail requiert vous tootype hello nom du tooconfirm de groupe de ressources hello que vous souhaitez toodelete il. Si vous consultez ressources autres que les ressources à l’étape 4 de hello hello [passez en revue les ressources](#review) section de cet article, cliquez sur **Annuler**. Si vous voyez uniquement les ressources hello 12 créées dans le cadre de cet article, tapez *MyRG* pour le nom du groupe de ressources de hello, puis cliquez sur **supprimer**. La suppression d’un groupe de ressources supprime toutes les ressources dans le groupe de ressources hello, toujours que tooconfirm contenu hello d’un groupe de ressources avant de le supprimer. portail de Hello supprime toutes les ressources contenues dans le groupe de ressources hello, puis supprime le groupe de ressources hello lui-même. Cette opération prend plusieurs minutes.

## <a name="next-steps"></a>Étapes suivantes

Dans cet exercice, vous avez créé un réseau virtuel et deux machines virtuelles. Vous avez spécifié des paramètres personnalisés lors de la création des machines virtuelles et accepté plusieurs paramètres par défaut. Nous vous recommandons de lire hello suivant des articles, avant le déploiement de production des réseaux virtuels et des machines virtuelles, tooensure vous comprenez tous les paramètres disponibles :

- [Réseaux virtuels](virtual-networks-overview.md)
- [Adresses IP publiques](virtual-network-ip-addresses-overview-arm.md#public-ip-addresses)
- [Interfaces réseau](virtual-network-network-interface.md)
- [Groupes de sécurité réseau](virtual-networks-nsg.md)
- [Machines virtuelles](../virtual-machines/windows/overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
