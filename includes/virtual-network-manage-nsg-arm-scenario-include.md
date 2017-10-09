## <a name="sample-scenario"></a>Exemple de scénario
toobetter illustrent comment toomanage groupes de sécurité réseau, cet article utilise scénario hello ci-dessous.

![Scénario de réseau virtuel](./media/virtual-networks-create-nsg-scenario-include/figure1.png)

Dans ce scénario, vous allez créer un groupe de sécurité réseau pour chaque sous-réseau Bonjour **TestVNet** réseau virtuel, comme décrit ci-dessous : 

* **NSG-FrontEnd**. Hello frontal NSG sera appliqué toohello *frontal* sous-réseau et contiennent deux règles :    
  * **rdp-rule**. Cette règle autorise RDP trafic toohello *frontal* sous-réseau.
  * **web-rule**. Cette règle autorise toohello du trafic HTTP *frontal* sous-réseau.
* **Back-end NSG**. Hello back-end NSG sera appliqué toohello *principal* sous-réseau et contiennent deux règles :    
  * **sql-rule**. Cette règle autorise le trafic SQL uniquement à partir de hello *frontal* sous-réseau.
  * **web-rule**. Cette règle refuse le trafic sortant de tous les internet à partir de hello *principal* sous-réseau.

combinaison Hello de ces règles créer un scénario de type de réseau de périmètre, où sous-réseau du back-end hello peut recevoir uniquement le trafic entrant pour le trafic SQL à partir du sous-réseau frontal de hello et n’a aucune toohello d’accès Internet, alors que le sous-réseau frontal de hello peut communiquer avec hello Internet et recevoir les requêtes HTTP entrantes.

scénario de hello toodeploy décrit ci-dessus, procédez comme [ce lien](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG), cliquez sur **déployer tooAzure**, remplacez les valeurs de paramètre par défaut hello si nécessaire et suivez les instructions de hello dans le portail de hello. Dans les instructions pour l’exemple ci-dessous, le modèle de hello hello a été utilisé toodeploy une ressource, les noms de groupe **RG-NSG**. 

