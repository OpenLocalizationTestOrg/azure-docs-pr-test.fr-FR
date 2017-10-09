## <a name="how-toocreate-a-classic-vnet-using-azure-cli"></a>Comment toocreate un virtuel classique à l’aide de la CLI d’Azure
Vous pouvez utiliser hello CLI d’Azure toomanage vos ressources Azure à partir de l’invite de commandes hello à partir de n’importe quel ordinateur exécutant Windows, Linux ou OSX. toocreate un réseau virtuel à l’aide de hello CLI d’Azure, suivez les étapes de hello ci-dessous.

1. Si vous n’avez jamais utilisé CLI d’Azure, consultez [installer et configurer hello CLI d’Azure](../articles/cli-install-nodejs.md) et suivez les instructions de hello point toohello où vous sélectionnez votre compte Azure et votre abonnement.
2. Exécutez hello **créer un réseau virtuel du réseau azure** commande toocreate un réseau virtuel et un sous-réseau, comme indiqué ci-dessous. liste de Hello affiché après la sortie de hello explique paramètres hello utilisés.
   
            azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
   
    Sortie attendue :
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK
   
   * **--vnet**. Nom de hello toobe de réseau virtuel créé. Pour notre scénario, *TestVNet*
   * **-e (ou --address-space)**. Espace d'adressage du réseau virtuel. Pour notre scénario, *192.168.0.0*
   * **-i (ou -cidr)**. Masque de réseau au format CIDR. Pour notre scénario, *16*.
   * **-n (ou --subnet-name**). Nom du sous-réseau de première hello. Pour notre scénario, *FrontEnd*.
   * **-p (ou --subnet-start-ip)**. Adresse IP de début pour le sous-réseau, ou espace d'adressage du sous-réseau. Pour notre scénario, *192.168.1.0*.
   * **-r (ou --subnet-cidr)**. Masque de réseau au format CIDR pour le sous-réseau. Pour notre scénario, *24*.
   * **-l (ou --location)**. Région Azure où hello réseau virtuel sera créé. Pour notre scénario, *Centre des États-Unis*.
3. Exécutez hello **créer de sous-réseau de réseau virtuel azure réseau** commande toocreate un sous-réseau, comme indiqué ci-dessous. liste de Hello affiché après la sortie de hello explique paramètres hello utilisés.
   
            azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
   
    Voici la sortie hello attendu pour la commande hello ci-dessus :
   
            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK
   
   * **-t (ou --vnet-name**. Nom de hello réseau virtuel où le sous-réseau de hello doit être créé. Pour notre scénario, *TestVNet*.
   * **-n (ou --name)**. Nom du sous-réseau hello. Pour notre scénario, *BackEnd*.
   * **-a (ou --address-prefix)**. Bloc CIDR de sous-réseau. Pour notre scénario, *192.168.2.0/24*.
4. Exécutez hello **afficher de réseau virtuel azure réseau** commande tooview des propriétés de hello de hello nouveau réseau virtuel, comme indiqué ci-dessous.
   
            azure network vnet show
   
    Voici la sortie hello attendu pour la commande hello ci-dessus :
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up hello virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

