points de terminaison Hello approche tooAzure fonctionne un peu différemment entre les modèles de déploiement classique et le Gestionnaire de ressources hello. Dans le modèle de déploiement du Gestionnaire de ressources hello, vous avez maintenant hello flexibilité toocreate réseau des filtres qui contrôlent le flux de hello du trafic vers et depuis vos machines virtuelles. Ces filtres vous permettent de toocreate les environnements de réseau complexes au-delà d’un simple point de terminaison comme modèle de déploiement classique hello. Cet article fournit une vue d’ensemble des groupes de sécurité réseau et montre en quoi ils diffèrent de l’utilisation des points de terminaison Classic, de la création de ces règles de filtrage et des exemples de scénarios de déploiement.

## <a name="overview-of-resource-manager-deployments"></a>Vue d’ensemble des déploiements Resource Manager
Points de terminaison dans le modèle de déploiement classique de hello sont remplacés par les groupes de sécurité réseau et des règles de liste (ACL) de contrôle d’accès. Les étapes rapides d’implémentation des règles ACL du groupe de sécurité réseau sont les suivantes :

* créer un groupe de sécurité réseau ;
* tooallow ou refuser le trafic, définissez vos règles ACL de groupe de sécurité réseau.
* Affecter votre interface de réseau de groupe de sécurité réseau tooa ou d’un sous-réseau de réseau virtuel.

Si vous sont souhaitant tooalso effectuer le réacheminement de port, tooplace un équilibreur de charge devant votre machine virtuelle et d’utiliser les règles NAT. Les étapes rapides d’implémentation des règles NAT et de l’équilibrage de charge sont les suivantes :

* Créez un équilibrage de charge.
* Créer un pool principal et ajoutez votre pool toohello de machines virtuelles.
* Définir vos règles NAT de réacheminement de port hello requis.
* Affecter des machines virtuelles de tooyour vos règles NAT.

## <a name="network-security-group-overview"></a>Vue d’ensemble du groupe de sécurité réseau
Groupes de sécurité réseau fournissent une couche de sécurité pour vous tooallow des ports spécifiques et les sous-réseaux tooaccess vos machines virtuelles. Vous devez généralement toujours un groupe de sécurité réseau fournissant cette couche de sécurité entre vos machines virtuelles et les hello world à l’extérieur. Groupes de sécurité réseau peut être appliqué tooa sous-réseau du réseau virtuel ou une interface réseau spécifique pour une machine virtuelle. Au lieu de créer des règles ACL de point de terminaison, vous créez désormais des règles ACL de groupe de sécurité réseau. Ces règles ACL fournissent un contrôle que la création simplement un tooforward de point de terminaison à un port donné. Pour plus d’informations, voir [Présentation du groupe de sécurité réseau](../articles/virtual-network/virtual-networks-nsg.md)

> [!TIP]
> Vous pouvez attribuer des sous-réseaux toomultiple de groupes de sécurité réseau ou aux interfaces réseau. Il n’existe aucun mappage 1:1. Vous pouvez créer un groupe de sécurité réseau avec un jeu commun de listes de contrôle et appliquer des sous-réseaux de toomultiple ou aux interfaces réseau. En outre, un groupe de sécurité réseau peut être appliqué tooresources sur votre abonnement (en fonction de [rôle en fonction des contrôles d’accès](../articles/active-directory/role-based-access-control-what-is.md).

## <a name="load-balancers-overview"></a>Vue d’ensemble des équilibrages de charge
Dans le modèle de déploiement classique hello, Azure serait effectuer toutes les hello traduction d’adresses réseau (NAT) et le port de transfert sur un Service Cloud pour vous. Lorsque vous créez un point de terminaison, vous devez spécifier tooexpose du port externe hello, ainsi que le trafic toodirect de port interne hello vers. Les groupes de sécurité réseau n’effectuent pas eux-mêmes ces tâches NAT et de réacheminement de port. 

tooallow vous toocreate les règles NAT pour ce port de transfert, créez un équilibrage de charge Azure dans votre groupe de ressources. Là encore, l’équilibrage de charge hello est granulaire suffisamment tooonly appliquer des machines virtuelles de toospecific si nécessaire. Bonjour Azure charger le travail de règles NAT équilibrage en même temps que le groupe de sécurité réseau ACL règles tooprovide beaucoup plus de souplesse et de contrôle que réalisable à l’aide de points de terminaison de Service Cloud. Pour plus d’informations, consultez hello [vue d’ensemble de l’équilibrage de charge](../articles/load-balancer/load-balancer-overview.md).

## <a name="network-security-group-acl-rules"></a>Règles ACL du groupe de sécurité réseau
Les règles ACL vous permettent de définir quel trafic peut entrer et sortir de votre machine virtuelle en fonction de ports, de plages de ports ou de protocoles spécifiques. Les règles sont affectés machines virtuelles de tooindividual ou tooa sous-réseau. Hello suivant capture d’écran est un exemple de règles ACL pour un serveur Web courantes :

![Liste des règles ACL du groupe de sécurité réseau](./media/virtual-machines-common-endpoints-in-resource-manager/example-acl-rules.png)

Règles ACL sont appliquées en fonction d’une métrique de priorité que vous spécifiez - plus la valeur hello hello, une priorité plus faible hello hello. Chaque groupe de sécurité réseau a la valeur par défaut de trois règles qui sont conçues toohandle des flux de hello du trafic de mise en réseau Azure, avec un texte explicite `DenyAllInbound` en tant que règle finale de hello. Listes de contrôle par défaut sont donné un toonot en priorité basse interférer avec les règles que vous créez.

## <a name="assigning-network-security-groups"></a>Affectation de groupes de sécurité réseau
Vous affectez un sous-réseau de tooa du groupe de sécurité réseau ou d’une interface réseau. Cette approche vous permet de toobe aussi précis que nécessaire lors de l’application de votre liste ACL règles tooonly un ordinateur virtuel spécifique, ou vous assurer un ensemble commun d’ACL les règles sont appliquée tooall partie des machines virtuelles du sous-réseau :

![Appliquer des groupes de sécurité réseau toonetwork interfaces ou aux sous-réseaux](./media/virtual-machines-common-endpoints-in-resource-manager/apply-nsg-to-resources.png)

comportement de Hello Hello groupe de sécurité réseau ne change pas selon assignée tooa sous-réseau ou une interface réseau. Un scénario de déploiement courant a hello que groupe de sécurité réseau affecté la conformité de tooensure tooa sous-réseau du sous-réseau de toothat attaché toutes les machines virtuelles. Pour plus d’informations, consultez [appliquer la sécurité du réseau regroupe tooresources](../articles/virtual-network/virtual-networks-nsg.md#associating-nsgs).

## <a name="default-behavior-of-network-security-groups"></a>Comportement par défaut des groupes de sécurité réseau
Selon comment et quand vous créez votre groupe de sécurité réseau, les règles par défaut peuvent être créés pour les machines virtuelles Windows toopermit l’accès RDP sur le port TCP 3389. Les règles par défaut des machines virtuelles Linux autorisent l’accès SSH sur le port TCP 22. Ces règles ACL automatique sont créées sous hello conditions suivantes :

* Si vous créez une machine virtuelle de Windows via le portail de hello et acceptez hello par défaut action toocreate un groupe de sécurité réseau, un liste ACL règle tooallow le port TCP 3389 (RDP) est créé.
* Si vous créez un VM Linux via le portail de hello et acceptez hello par défaut action toocreate un groupe de sécurité réseau, un liste ACL règle tooallow le port TCP 22 (SSH) est créé.

Dans toutes les autres conditions, ces règles ACL par défaut ne sont pas créées. Impossible de se connecter tooyour machine virtuelle sans créer de hello règles ACL appropriées. Ces conditions incluent hello suivant des actions courantes :

* Création d’un groupe de sécurité réseau via le portail de hello comme un Bonjour de toocreating VM action distincte.
* Créer un groupe de sécurité réseau par programmation via PowerShell, l’interface de ligne de commande Azure, les API Rest, etc.
* Création d’une machine virtuelle et en lui affectant tooan existante du groupe de sécurité réseau qui n’a pas déjà de règle ACL appropriée hello défini.

Dans tous les hello précédant le cas, vous devez toocreate listes de contrôle pour les connexions de gestion à distance appropriés de machine virtuelle tooallow hello.

## <a name="default-behavior-of-a-vm-without-a-network-security-group"></a>Comportement par défaut d’une machine virtuelle sans groupe de sécurité réseau
Vous pouvez créer une machine virtuelle sans créer un groupe de sécurité réseau. Dans ces situations, vous pouvez vous connecter tooyour machine virtuelle à l’aide de RDP ou SSH sans créer les règles ACL. De même, si vous avez installé un service web sur le port 80, ce service est automatiquement accessible à distance. Hello machine virtuelle a tous les ports à ouvrir.

> [!NOTE]
> Vous devez toujours toohave un tooa adresse attribuée de publique IP virtuelle dans l’ordre de toutes les connexions à distance. N’ayant ne pas un groupe de sécurité réseau pour l’interface de réseau ou sous-réseau hello n’expose pas le trafic externe hello VM tooany. Hello par défaut lors de la création d’une machine virtuelle via le portail de hello sont toocreate une nouvelle adresse IP publique. Pour toutes les autres formes de création d’une machine virtuelle comme PowerShell, l’interface de ligne de commande Azure ou le modèle Resource Manager, une adresse IP publique n’est pas automatiquement créée, sauf en cas de demande explicite. Hello action par défaut via le portail de hello est également toocreate un groupe de sécurité réseau. Cette action par défaut signifie que vous ne devriez pas vous retrouver dans une situation dans laquelle un une machine virtuelle exposée ne dispose d’aucun réseau de filtrage en place.

## <a name="understanding-load-balancers-and-nat-rules"></a>Présentation des règles NAT et de l’équilibrage de charge
Dans le modèle de déploiement hello classique, vous pouvez créer des points de terminaison qui également effectuées réacheminement de port. Lorsque vous créez une machine virtuelle dans le modèle de déploiement classique de hello, listes de contrôle pour RDP ou SSH sont créés automatiquement. Ces règles n’exposent pas le port TCP 3389 ou le port TCP 22 respectivement toohello en dehors du monde. Au lieu de cela, vous serait exposé un port TCP de valeur élevée qui mappe le port interne approprié toohello. Vous pouvez également créer vos propres règles ACL de la même manière, telles qu’exposent un serveur Web sur TCP port 4280 toohello en dehors du monde. Vous pouvez voir ces règles ACL et les mappages de ports Bonjour suivant capture d’écran à partir du portail classique de hello :

![Réacheminement de port avec des points de terminaison Classic](./media/virtual-machines-common-endpoints-in-resource-manager/classic-endpoints-port-forwarding.png)

Avec les groupes de sécurité réseau, cette fonction de réacheminement de port est gérée par un équilibrage de charge. Pour plus d’informations, consultez la page [Équilibrage de charge dans Azure](../articles/load-balancer/load-balancer-overview.md). Hello suivant montre un équilibreur de charge avec NAT règle tooperform réacheminement de port TCP port 4222 toohello interne le port TCP 22 une machine virtuelle :

![Règles NAT d’équilibrage de charge pour le réacheminement de port](./media/virtual-machines-common-endpoints-in-resource-manager/load-balancer-nat-rules.png)

> [!NOTE]
> Lorsque vous implémentez un équilibrage de charge, vous n’attribuez généralement hello machine virtuelle une adresse IP publique. Au lieu de cela, équilibrage de charge hello a un tooit d’adresse IP publique. Vous devez toujours toocreate votre flux groupe de sécurité réseau et la liste ACL règles toodefine hello du trafic vers et depuis votre machine virtuelle. Hello règles NAT de programme d’équilibrage de charge sont simplement des toodefine quels ports sont autorisés via l’équilibrage de charge hello et comment ils obtient distribués sur hello principales machines virtuelles. Par conséquent, vous devez toocreate une règle NAT pour tooflow le trafic via l’équilibrage de charge hello. tooallow Bonjour trafic tooreach Bonjour machine virtuelle, créez une règle de ACL de groupe de sécurité réseau.
