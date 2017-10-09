## <a name="scenario"></a>Scénario
toobetter illustrent comment toocreate UDRs, ce document utilise scénario hello ci-dessous.

![DESCRIPTION DE L'IMAGE](./media/virtual-network-create-udr-scenario-include/figure1.png)

Dans ce scénario, vous allez créer un UDR pour hello *sous-réseau de fin avant* et un autre UDR pour hello *sous-réseau de fin précédent* , comme décrit ci-dessous : 

* **UDR-FrontEnd**. Hello frontal UDR sera appliqué toohello *frontal* sous-réseau et contenir un itinéraire :    
  * **RouteToBackend**. Cet itinéraire envoie tout le trafic toohello back-end sous-réseau toohello **FW1** machine virtuelle.
* **UDR-BackEnd**. Hello back-end UDR sera appliqué toohello *principal* sous-réseau et contenir un itinéraire :    
  * **RouteToFrontend**. Cet itinéraire envoie tout le trafic toohello frontal sous-réseau toohello **FW1** machine virtuelle.

combinaison de Hello de ces itinéraires garantit que tout le trafic destiné à partir d’un seul sous-réseau tooanother sera routé toohello **FW1** machine virtuelle, qui est utilisé comme un équipement virtuel. Vous devez également tooturn transfert IP pour cette machine virtuelle, tooensure peuvent recevoir du trafic destinés aux machines virtuelles de tooother.

