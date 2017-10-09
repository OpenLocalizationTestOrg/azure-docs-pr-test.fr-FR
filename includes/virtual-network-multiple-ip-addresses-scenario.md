## <a name="scenario"></a>Scénario
Une machine virtuelle avec une seule carte réseau est un réseau virtuel de tooa créé et connecté. Hello machine virtuelle nécessite trois différentes *privé* IP adresses et deux *public* des adresses IP. les adresses IP Hello assignés toohello suivant des configurations IP :

* **IPConfig-1 :** attribue une adresse IP privée *statique* et une adresse IP publique *statique*.
* **IPConfig-2 :** attribue une adresse IP privée *statique* et une adresse IP publique *statique*.
* **IPConfig-3 :** attribue une adresse IP privée *statique* et aucune adresse IP publique.
  
    ![Plusieurs adresses IP](./media/virtual-network-multiple-ip-addresses-scenario/multiple-ipconfigs.png)

les configurations IP Hello sont associé toohello NIC lorsque hello NIC est créée et hello NIC est attaché toohello machine virtuelle lors de la création de hello machine virtuelle. types de Hello d’adresses IP utilisées pour le scénario de hello sont à titre d’illustration. Vous pouvez affecter les types d’adresses IP et d’affectations dont vous avez besoin.

> [!NOTE]
> Bien que les étapes hello cet article affecte tous les tooa de configurations IP carte réseau unique, vous pouvez également affecter tooany de configurations IP plusieurs cartes réseau dans une machine virtuelle multi-NIC. toolearn comment toocreate une machine virtuelle avec plusieurs cartes réseau, lire hello [créer une machine virtuelle avec plusieurs cartes réseau](../articles/virtual-network/virtual-network-deploy-multinic-arm-ps.md) l’article.
