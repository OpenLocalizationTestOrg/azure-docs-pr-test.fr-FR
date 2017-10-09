## <a name="scenario"></a>Scénario
toobetter illustrent comment toocreate groupes de sécurité réseau, ce document utilise scénario hello ci-dessous.

![Scénario de réseau virtuel](./media/virtual-networks-create-nsg-scenario-include/figure1.png)

Dans ce scénario, vous allez créer un groupe de sécurité réseau pour chaque sous-réseau Bonjour **TestVNet** réseau virtuel, comme décrit ci-dessous : 

* **NSG-FrontEnd**. Hello frontal NSG sera appliqué toohello *frontal* sous-réseau et contiennent deux règles :    
  * **rdp-rule**. Cette règle autorise RDP trafic toohello *frontal* sous-réseau.
  * **web-rule**. Cette règle autorise toohello du trafic HTTP *frontal* sous-réseau.
* **Back-end NSG**. Hello back-end NSG sera appliqué toohello *principal* sous-réseau et contiennent deux règles :    
  * **sql-rule**. Cette règle autorise le trafic SQL uniquement à partir de hello *frontal* sous-réseau.
  * **web-rule**. Cette règle refuse le trafic sortant de tous les internet à partir de hello *principal* sous-réseau.

combinaison de ces règles Hello créer un scénario de type de réseau de périmètre, où hello back-end sous-réseau peut uniquement recevoir le trafic entrant pour SQL à partir du sous-réseau frontal de hello et ne dispose d’aucune toohello d’accès Internet, alors que le sous-réseau frontal de hello peut communiquer avec hello Internet, et recevoir les requêtes HTTP entrantes.

