---
title: "aaaAzure DMZ, exemple : créer un réseau de périmètre Simple avec des groupes de sécurité réseau | Documents Microsoft"
description: "Générer une zone DMZ avec des groupes de sécurité réseau (NSG)"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: 11c5c6026da30fbc9c5e585f5c16e2d411d6fd80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-an-azure-resource-manager-template"></a>Exemple 1 – Créer une zone DMZ simple à l’aide de groupes de sécurité réseau avec un modèle Azure Resource Manager
[Retour toohello Page meilleures pratiques de sécurité limite][HOME]

> [!div class="op_single_selector"]
> * [Modèle Resource Manager](virtual-networks-dmz-nsg.md)
> * [Classic - PowerShell](virtual-networks-dmz-nsg-asm.md)
> 
>

Cet exemple crée une zone DMZ primitive avec quatre serveurs Windows et des groupes de sécurité réseau. Cet exemple décrit chacune des sections tooprovide une meilleure compréhension de chaque étape de hello modèle approprié. Il existe également un tooprovide de section de scénario de trafic détaillée approfondi comment le trafic passe par le biais des couches de défense dans hello réseau de périmètre hello. Enfin, dans la section des références hello est toobuild de code et les instructions de modèle complète hello cette tootest d’environnement et de faire des essais avec différents scénarios. 

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)] 

![Réseau de périmètre entrant avec groupe de sécurité réseau][1]

## <a name="environment-description"></a>Description de l’environnement
Dans cet exemple, un abonnement contient hello suivant des ressources :

* un seul groupe de ressources.
* un réseau virtuel avec deux sous-réseaux « FrontEnd » et « BackEnd »,
* Un groupe de sécurité réseau qui est appliquée tooboth sous-réseaux
* un serveur Windows Server représentant un serveur web d’application (« IIS01 »),
* Deux serveurs Windows Server qui représentent les serveurs principaux d’applications (« AppVM01 », « AppVM02 »)
* Un serveur Windows Server qui représente un serveur DNS (« DNS01 »),
* Une adresse IP publique associée au serveur web d’application hello

Dans la section des références de hello, il est un modèle de gestionnaire de ressources Azure de tooan de lien qui génère l’environnement hello décrite dans cet exemple. Machines virtuelles de génération hello et réseaux virtuels, bien que le fait par le modèle d’exemple hello, ne sont pas décrits en détail dans ce document. 

**toobuild cet environnement** (obtenir des instructions détaillées sont dans la section des références hello de ce document) ;

1. Déployer hello modèle du Gestionnaire de ressources Azure à : [modèles de démarrage rapide Azure][Template]
2. Installer l’application d’exemple hello sur : [Application exemple de Script][SampleApp]

>[!NOTE]
>tooRDP tooany sur les serveurs principaux dans ce cas, le serveur IIS hello est utilisé comme une zone « saut ». Serveur IIS de première RDP toohello puis à partir de serveur de hello IIS Server RDP toohello principal. Une adresse IP publique peut être associée à chaque carte réseau du serveur pour faciliter la connexion RDP.
> 
>

Hello sections suivantes fournissent une description détaillée de hello groupe de sécurité réseau et son mode de fonctionnement pour cet exemple en parcourant les lignes de clé de hello modèle du Gestionnaire de ressources Azure.

## <a name="network-security-groups-nsg"></a>Groupes de sécurité réseau (NSG)
Pour cet exemple, un groupe NSG est créé, puis chargé avec six règles. 

>[!TIP]
>En règle générale, vous devez créer vos règles « Autoriser » spécifiques tout d’abord et puis hello dernière plus générique « Refuser » règles. Hello priorité détermine les règles sont évaluées en premier. Une fois que le trafic est trouvé règle spécifique de tooapply tooa, aucune autre règle n’est évaluées. Les règles de groupe de sécurité réseau peuvent être appliquées, que ce soit dans hello direction entrante ou sortante (du point de vue hello du sous-réseau de hello).
>
>

De façon déclarative, hello suivant les règles est généré pour le trafic entrant :

1. Le trafic DNS interne (port 53) est autorisé
2. Le trafic RDP (port 3389) à partir d’Internet de hello tooany machine virtuelle est autorisé.
3. Le trafic HTTP (port 80) à partir du serveur de tooweb hello Internet (IIS01) est autorisé.
4. Tout trafic (tous les ports) à partir de IIS01 tooAppVM1 est autorisée.
5. Tout trafic (tous les ports) à partir de hello Internet toohello réseau virtuel entier (les deux sous-réseaux) est refusé.
6. Tout trafic (tous les ports) à partir du sous-réseau principal toohello hello frontal sous-réseau est refusé.

Avec ces sous-réseau tooeach dépendant de règles, si une requête HTTP a été entrante à partir de hello toohello le serveur web Internet, les deux règles 3 (autoriser) et 5 (refuser) s’appliquent, mais étant donné que la règle 3 a une priorité plus élevée s’appliquerait et règle 5 ne serait pas entrent en jeu. Par conséquent, demande HTTP de hello serait autorisée serveur web de toohello. Si ce trafic même a essayé de serveur de DNS01 tooreach hello, règle 5 (Deny) serait hello premier tooapply hello le trafic et ne serait pas autorisé toopass toohello serveur. Règle 6 (Deny) bloque le sous-réseau frontal hello communique avec le sous-réseau du serveur principal toohello (à l’exception du trafic autorisé dans les règles 1 et 4), cet ensemble de règles protège le réseau principal de hello au cas où une personne malveillante compromet hello application web sur hello serveur frontal, serait de personne malveillante de hello limitée toohello d’accès réseau (uniquement tooresources exposée sur le serveur de AppVM01 hello) principal « protégé ».

Il existe une règle sortante par défaut qui autorise le trafic sortant toohello internet. Pour cet exemple, nous allons autoriser le trafic sortant sans modifier les règles de trafic sortant. tooapply sécurité stratégie tootraffic dans les deux sens, utilisateur défini par routage est obligatoire et est exploré dans « Exemple 3 » sur hello [Page meilleures pratiques de sécurité limite][HOME].

Chaque règle est décrite plus en détail comme suit :

1. Une ressource de groupe de sécurité réseau doit être instancié toohold hello règles :

    ```JSON
    "resources": [
      {
        "apiVersion": "2015-05-01-preview",
        "type": "Microsoft.Network/networkSecurityGroups",
        "name": "[variables('NSGName')]",
        "location": "[resourceGroup().location]",
        "properties": { }
      }
    ]
    ``` 

2. Hello première règle de cet exemple autorise le trafic DNS entre tous les réseaux internes toohello serveur DNS hello principal sous-réseau. règle de Hello a certains paramètres importants :
  * « destinationAddressPrefix » - les règles peuvent utiliser un type spécial de préfixe d’adresse appelée une « balise par défaut », ces balises sont des identificateurs fournis par le système qui permettent une tooaddress facilement une catégorie supérieure de préfixes d’adresses. Cette règle utilise hello balise par défaut « Internet » toosignify d’adresses en dehors de hello réseau virtuel. Les autres étiquettes de préfixe sont VirtualNetwork et AzureLoadBalancer.
  * « Direction » indique le sens du trafic qui sera appliqué à cette règle. direction de Hello est hello du point de vue de l’ordinateur virtuel ou le sous-réseau de hello (selon où ce groupe de sécurité réseau est lié). Par conséquent, si Direction est « Entrant » et le trafic est entrant sous-réseau de hello, hello règle s’applique et le trafic en laissant le sous-réseau de hello ne serait pas affecté par cette règle.
  * « Priority » définit la commande hello dans lequel un flux de trafic est évalué. Hello inférieur hello numéro hello hello prioritaires. Lorsqu’une règle s’applique le flux de trafic spécifique tooa, aucune autre règle n’est traitées. Par conséquent, si une règle avec la priorité 1 autorise le trafic et une règle de priorité 2 refuse le trafic et les deux règles s’appliquent tootraffic alors le trafic de hello serait autorisé tooflow (étant donné que la règle 1 a une priorité plus élevée qu’il a pris effet et aucune autre règle n’ont été appliquées).
  * « Accès » indique si le trafic concerné par cette règle est bloqué (« Deny ») ou autorisé (« Allow »).

    ```JSON
    "properties": {
    "securityRules": [
      {
        "name": "enable_dns_rule",
        "properties": {
          "description": "Enable Internal DNS",
          "protocol": "*",
          "sourcePortRange": "*",
          "destinationPortRange": "53",
          "sourceAddressPrefix": "VirtualNetwork",
          "destinationAddressPrefix": "10.0.2.4",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
    ```

3. Cette règle permet de tooflow de trafic RDP à partir de port RDP hello internet toohello sur n’importe quel serveur hello lié sous-réseau. 

    ```JSON
    {
      "name": "enable_rdp_rule",
      "properties": {
        "description": "Allow RDP",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "3389",
        "sourceAddressPrefix": "*",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 110,
        "direction": "Inbound"
      }
    },
    ```

4. Cette règle permet de trafic entrant du trafic toohit hello le serveur web internet. Cette règle ne modifie pas le comportement de routage hello. règle de Hello autorise uniquement le trafic destiné à IIS01 toopass. Par conséquent, si le trafic à partir de hello Internet avait le serveur web de hello comme destination cette règle est autoriser et arrêter le traitement des règles. (Dans la règle hello avec une priorité de 140 tous les autres trafic internet entrant est bloqué). Si vous traitez uniquement le trafic HTTP, cette règle pourrait être plue restreint tooonly autoriser Destination Port 80.

    ```JSON
    {
      "name": "enable_web_rule",
      "properties": {
        "description": "Enable Internet too[variables('VM01Name')]",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "80",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "10.0.1.5",
        "access": "Allow",
        "priority": 120,
        "direction": "Inbound"
        }
      },
    ```

5. Cette règle permet toopass le trafic à partir du serveur de IIS01 hello toohello AppVM01 serveur, une règle ultérieure bloque tout autre trafic tooBackend de serveur frontal. tooimprove cette règle, si le port de hello est connu, qui doit être ajoutée. Par exemple, si le serveur IIS hello accède uniquement à SQL Server sur AppVM01, plage de ports de Destination hello doit être changé de « * » (tout) too1433 (hello port SQL), permettant ainsi une surface d’attaque entrante réduite sur AppVM01 doit hello web application jamais être compromise.

    ```JSON
    {
      "name": "enable_app_rule",
      "properties": {
        "description": "Enable [variables('VM01Name')] too[variables('VM02Name')]",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "10.0.1.5",
        "destinationAddressPrefix": "10.0.2.5",
        "access": "Allow",
        "priority": 130,
        "direction": "Inbound"
      }
    },
     ```

6. Cette règle refuse le trafic à partir des serveurs de tooany hello internet sur le réseau de hello. Les règles hello avec une priorité de 110 et 120, effet de hello est tooallow uniquement internet trafic toohello pare-feu entrantes et ports RDP sur les serveurs et bloque tout le reste. Cette règle est une « sécurité intégrée » règle tooblock tous les flux inattendues.

    ```JSON
    {
      "name": "deny_internet_rule",
      "properties": {
        "description": "Isolate hello [variables('VNetName')] VNet from hello Internet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "VirtualNetwork",
        "access": "Deny",
        "priority": 140,
        "direction": "Inbound"
      }
    },
     ```

7. règle finale de Hello refuse le trafic du sous-réseau de hello frontal sous-réseau toohello back-end. Étant donné que cette règle est la seule règle de trafic entrant, le trafic inverse est autorisé (à partir de toohello de back-end hello frontal).

    ```JSON
    {
      "name": "deny_frontend_rule",
      "properties": {
        "description": "Isolate hello [variables('Subnet1Name')] subnet from hello [variables('Subnet2Name')] subnet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "[variables('Subnet1Prefix')]",
        "destinationAddressPrefix": "[variables('Subnet2Prefix')]",
        "access": "Deny",
        "priority": 150,
        "direction": "Inbound"
      }
    }
    ```

## <a name="traffic-scenarios"></a>Scénarios de trafic
#### <a name="allowed-internet-tooweb-server"></a>(*Autorisées*) Internet tooweb server
1. Un utilisateur internet demande une page HTTP à partir de l’adresse IP publique de hello Hello que NIC associée hello IIS01 NIC
2. adresse IP publique de Hello passe toohello de trafic réseau virtuel vers IIS01 (serveur web de hello)
3. Le sous-réseau du serveur frontal commence le traitement des règles de trafic entrant :
  1. Groupe de sécurité réseau règle 1 (DNS) ne s’applique pas, déplacer toonext règle
  2. Règle de groupe de sécurité réseau 2 (RDP) ne s’applique pas, déplacer toonext règle
  3. Règle de groupe de sécurité réseau 3 (tooIIS01 Internet) s’applique, le trafic est le traitement des règles autorisées, arrêter
4. Le trafic atteint l’adresse IP interne du serveur web de hello IIS01 (10.0.1.5)
5. IIS01 écoute pour le trafic web, reçoit la requête et démarre le traitement de demande de hello
6. IIS01 demande hello SQL Server sur AppVM01 pour plus d’informations
7. Aucune règle sur le trafic sortant sur le sous-réseau du serveur frontal. Le trafic est autorisé.
8. sous-réseau du serveur principal Hello commence le traitement de la règle de trafic entrant :
  1. Groupe de sécurité réseau règle 1 (DNS) ne s’applique pas, déplacer toonext règle
  2. Règle de groupe de sécurité réseau 2 (RDP) ne s’applique pas, déplacer toonext règle
  3. Règle de groupe de sécurité réseau 3 (tooFirewall Internet) ne s’applique pas, déplacer toonext règle
  4. Règle de groupe de sécurité réseau 4 (IIS01 tooAppVM01) s’applique, le trafic est le traitement des règles autorisées, arrêter
9. AppVM01 reçoit hello requête SQL et répond
10. Dans la mesure où il n’y a aucune règles de trafic sortant sur le sous-réseau du serveur principal hello, réponse de hello est autorisée.
11. Le sous-réseau du serveur frontal commence le traitement des règles de trafic entrant :
  1. Il n’existe aucune règle de groupe de sécurité réseau qui applique des tooInbound trafic de sous-réseau du serveur frontal de toohello de sous-réseau hello back-end, donc aucune des règles du groupe de sécurité réseau hello s’appliquent
  2. règle du système par défaut Hello autorisant le trafic entre sous-réseaux permettrait ce trafic donc hello le trafic est autorisé.
12. le serveur IIS Hello reçoit la réponse SQL hello et termine la réponse HTTP de hello et envoie toohello demandeur
13. Dans la mesure où il n’y a aucune règles de trafic sortant sur le sous-réseau du serveur frontal hello, hello réponse soit autorisée et hello utilisateur Internet reçoit hello web page est demandée.

#### <a name="allowed-rdp-tooiis-server"></a>(*Autorisées*) serveur de tooIIS RDP
1. Un administrateur de serveur sur internet demande un tooIIS01 de session RDP sur hello adresse IP publique de hello que NIC associée hello NIC IIS01 (cette adresse IP publique accessible via hello portail ou PowerShell)
2. adresse IP publique de Hello passe toohello de trafic réseau virtuel vers IIS01 (serveur web de hello)
3. Le sous-réseau du serveur frontal commence le traitement des règles de trafic entrant :
  1. Groupe de sécurité réseau règle 1 (DNS) ne s’applique pas, déplacer toonext règle
  2. La règle NSG 2 (RDP) s’applique, le trafic est autorisé, arrêter le traitement des règles
4. En l’absence de réseau sortant, les règles par défaut s’appliquent et le retour de trafic est autorisé
5. La Session RDP est activée.
6. Invites IIS01 hello nom d’utilisateur et mot de passe

>[!NOTE]
>tooRDP tooany sur les serveurs principaux dans ce cas, le serveur IIS hello est utilisé comme une zone « saut ». Serveur IIS de première RDP toohello puis à partir de serveur de hello IIS Server RDP toohello principal.
>
>

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a>(*Autorisé*) recherche DNS du serveur web sur le serveur DNS
1. Web des besoins du serveur, IIS01, de flux de données à www.data.gov, mais doit tooresolve hello adresse.
2. Hello configuration réseau pour les listes de réseau virtuel hello DNS01 (10.0.2.4 sur le sous-réseau du serveur principal hello) en tant que serveur DNS principal de hello, IIS01 envoie hello DNS demande tooDNS01
3. Aucune règle sur le trafic sortant sur le sous-réseau du serveur frontal. Le trafic est autorisé.
4. Le sous-réseau du serveur principal entame le traitement du réseau entrant :
  * La règle NSG 1 (DNS) s’applique, le trafic est autorisé, arrêter le traitement des règles
5. Serveur DNS reçoit la demande de hello
6. Serveur DNS n’a pas adresse hello mis en cache et demande à un serveur DNS racine sur hello internet
7. Aucune règle sortante sur le sous-réseau du serveur principal, le trafic est autorisé
8. Serveur DNS Internet répond, étant donné que cette session a été lancée en interne, réponse de hello est autorisée.
9. Le serveur DNS met en cache la réponse de hello et répond tooIIS01 arrière de demande initiale toohello
10. Aucune règle sortante sur le sous-réseau du serveur principal, le trafic est autorisé
11. Le sous-réseau du serveur frontal commence le traitement des règles de trafic entrant :
  1. Il n’existe aucune règle de groupe de sécurité réseau qui applique des tooInbound trafic de sous-réseau du serveur frontal de toohello de sous-réseau hello back-end, donc aucune des règles du groupe de sécurité réseau hello s’appliquent
  2. règle du système par défaut Hello autorisant le trafic entre sous-réseaux permet ce trafic donc hello le trafic est autorisé
12. IIS01 reçoit hello réponse DNS01

#### <a name="allowed-web-server-access-file-on-appvm01"></a>(*Autorisé*) fichier d’accès de serveur Web sur AppVM01
1. IIS01 demande un fichier sur AppVM01
2. Aucune règle sur le trafic sortant sur le sous-réseau du serveur frontal. Le trafic est autorisé.
3. sous-réseau du serveur principal Hello commence le traitement de la règle de trafic entrant :
  1. Groupe de sécurité réseau règle 1 (DNS) ne s’applique pas, déplacer toonext règle
  2. Règle de groupe de sécurité réseau 2 (RDP) ne s’applique pas, déplacer toonext règle
  3. Règle de groupe de sécurité réseau 3 (tooIIS01 Internet) ne s’applique pas, déplacer toonext règle
  4. Règle de groupe de sécurité réseau 4 (IIS01 tooAppVM01) s’applique, le trafic est le traitement des règles autorisées, arrêter
4. AppVM01 reçoit la demande de hello et répond avec le fichier (en supposant que l’accès est autorisé)
5. Dans la mesure où il n’y a aucune règles de trafic sortant sur le sous-réseau du serveur principal hello, réponse de hello est autorisée.
6. Le sous-réseau du serveur frontal commence le traitement des règles de trafic entrant :
  1. Il n’existe aucune règle de groupe de sécurité réseau qui applique des tooInbound trafic de sous-réseau du serveur frontal de toohello de sous-réseau hello back-end, donc aucune des règles du groupe de sécurité réseau hello s’appliquent
  2. règle du système par défaut Hello autorisant le trafic entre sous-réseaux permettrait ce trafic donc hello le trafic est autorisé.
7. le serveur IIS Hello reçoit le fichier de hello

#### <a name="denied-rdp-toobackend"></a>(*Refusé*) RDP toobackend
1. Un utilisateur internet tente de tooRDP tooserver AppVM01
2. Étant donné qu’aucune adresse IP publique associée à cette carte réseau de serveurs, ce trafic ne doivent jamais entrer hello réseau virtuel et ne fait de joindre le serveur de hello
3. Toutefois, si une adresse IP publique a été activée pour une raison quelconque, la règle du groupe de sécurité réseau 2 (RDP) autorise ce trafic

>[!NOTE]
>tooRDP tooany sur les serveurs principaux dans ce cas, le serveur IIS hello est utilisé comme une zone « saut ». Serveur IIS de première RDP toohello puis à partir de serveur de hello IIS Server RDP toohello principal.
>
>

#### <a name="denied-web-toobackend-server"></a>(*Refusé*) serveur de toobackend Web
1. Un utilisateur internet tente de tooaccess un fichier sur AppVM01
2. Étant donné qu’aucune adresse IP publique associée à cette carte réseau de serveurs, ce trafic ne doivent jamais entrer hello réseau virtuel et ne fait de joindre le serveur de hello
3. Si une adresse IP publique a été activée pour une raison quelconque, la règle de groupe de sécurité réseau 5 (tooVNet Internet) susceptibles de bloquer ce trafic

#### <a name="denied-web-dns-look-up-on-dns-server"></a>(*Refusé*) recherche DNS web sur le serveur DNS
1. Un utilisateur internet tente de toolook d’un enregistrement DNS interne sur DNS01
2. Étant donné qu’aucune adresse IP publique associée à cette carte réseau de serveurs, ce trafic ne doivent jamais entrer hello réseau virtuel et ne fait de joindre le serveur de hello
3. Si une adresse IP publique a été activée pour une raison quelconque, la règle de groupe de sécurité réseau 5 (tooVNet Internet) susceptibles de bloquer ce trafic (Remarque : que règle 1 (DNS) s’appliquera pas car hello demande adresse source est hello internet et 1 de la règle s’applique uniquement toohello réseau local en tant que source de hello)

#### <a name="denied-sql-access-on-hello-web-server"></a>(*Refusé*) sur le serveur web de hello l’accès à SQL
1. Un utilisateur Internet demande des données SQL à partir de IIS01
2. Étant donné qu’aucune adresse IP publique associée à cette carte réseau de serveurs, ce trafic ne doivent jamais entrer hello réseau virtuel et ne fait de joindre le serveur de hello
3. Si une adresse IP publique a été activée pour une raison quelconque, sous-réseau du serveur frontal hello commence le traitement de la règle de trafic entrant :
  1. Groupe de sécurité réseau règle 1 (DNS) ne s’applique pas, déplacer toonext règle
  2. Règle de groupe de sécurité réseau 2 (RDP) ne s’applique pas, déplacer toonext règle
  3. Règle de groupe de sécurité réseau 3 (tooIIS01 Internet) s’applique, le trafic est le traitement des règles autorisées, arrêter
4. Le trafic atteint l’adresse IP interne de hello IIS01 (10.0.1.5)
5. IIS01 n’est pas à l’écoute sur le port 1433, par conséquent, aucune demande toohello de réponse

## <a name="conclusion"></a>Conclusion
Cet exemple est un moyen relativement simple et direct d’isoler le sous-réseau principal hello le trafic entrant.

Vous trouverez d’autres exemples et une vue d’ensemble des frontières de sécurité réseau [ici][HOME].

## <a name="references"></a>Références
### <a name="azure-resource-manager-template"></a>Modèle Azure Resource Manager
Cet exemple utilise un modèle Azure Resource Manager prédéfini dans un référentiel GitHub maintenu par Microsoft et ouvrez toohello Communauté. Ce modèle peut être déployé directement GitHub, ou téléchargé et modifié toofit à vos besoins. 

les modèles principal Hello sont dans le fichier hello nommé « azuredeploy.json ». Ce modèle peut être envoyé via PowerShell ou CLI (avec le fichier de « azuredeploy.parameters.json » associé de hello) toodeploy ce modèle. Je pense que hello plus simple est de façon toouse hello « Déployer tooAzure » sur bouton hello README.md page à GitHub.

modèle hello toodeploy qui génère cet exemple à partir de GitHub et hello portail Azure, procédez comme suit :

1. À partir d’un navigateur, accédez à toohello [modèle][Template]
2. Cliquez sur le bouton de « Déployer tooAzure » hello (ou bouton toosee une représentation graphique de ce modèle de hello « Visualiser »)
3. Puis entrez hello compte de stockage, le nom d’utilisateur et mot de passe dans le panneau de paramètres hello **OK**
5. Créez un groupe de ressources pour ce déploiement (vous pouvez utiliser un groupe existant, mais il est recommandé d'en créer un nouveau pour obtenir de meilleurs résultats)
6. Si nécessaire, modifiez les paramètres d’abonnement et l’emplacement hello pour votre réseau virtuel.
7. Cliquez sur **passez en revue les conditions juridiques**, lisez les termes du contrat de hello, puis cliquez sur **achat** tooagree.
8. Cliquez sur **créer** déploiement de hello toobegin de ce modèle.
9. Une fois le déploiement de hello se termine correctement, accédez à toohello que groupe de ressources créé pour ce déploiement toosee hello les ressources configurées à l’intérieur.

>[!NOTE]
>Ce modèle permet de RDP toohello IIS01 serveur uniquement (hello Rechercher adresse IP publique pour IIS01 sur hello portail). tooRDP tooany sur les serveurs principaux dans ce cas, le serveur IIS hello est utilisé comme une zone « saut ». Serveur IIS de première RDP toohello puis à partir de serveur de hello IIS Server RDP toohello principal.
>
>

tooremove cette suppression hello du déploiement, groupe de ressources et toutes les ressources enfants seront également supprimés.

#### <a name="sample-application-scripts"></a>Exemples de scripts d’application
Une fois le modèle de hello s’exécute correctement, vous pouvez définir les serveur web de hello et le serveur d’applications avec un tooallow d’application web simple test avec cette configuration de réseau de périmètre. tooinstall un exemple d’application pour ce, ainsi que d’autres exemples de réseau de périmètre, un a été fourni au lien de hello : [Application exemple de Script][SampleApp]

## <a name="next-steps"></a>Étapes suivantes

* Déployer cet exemple
* Générer l’exemple d’application hello
* Tester différents flux de trafic via cette zone DMZ

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-arm/example1design.png "Zone DMZ avec groupe de sécurité réseau (NSG)"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[Template]: https://github.com/Azure/azure-quickstart-templates/tree/master/301-dmz-nsg
[SampleApp]: ./virtual-networks-sample-app.md