## <a name="scenario"></a>Scénario
toobetter illustrent comment toocreate un réseau virtuel et sous-réseaux, ce document Utilisez scénario hello ci-dessous.

![Scénario de réseau virtuel](./media/virtual-networks-create-vnet-scenario-include/vnet-scenario.png)

Dans ce scénario, vous allez créer un réseau virtuel nommé **TestVNet** avec un bloc CIDR réservé de **192.168.0.0./16**. Votre réseau virtuel contiendra hello suivant sous-réseaux : 

* **FrontEnd**, qui utilise **192.168.1.0/24** comme bloc CIDR.
* **BackEnd**, qui utilise **192.168.2.0/24** comme bloc CIDR.

