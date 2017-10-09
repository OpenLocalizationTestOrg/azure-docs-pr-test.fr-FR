Vous ouvrez un port ou créer un point de terminaison, tooa machine virtuelle (VM) dans Azure en créant un filtre de réseau sur un sous-réseau ou une interface réseau de machine virtuelle. Vous placez ces filtres, qui contrôlent le trafic entrant et sortant, sur une ressource de toohello de groupe de sécurité réseau associé qui reçoit le trafic de hello.

Nous allons utiliser un exemple courant de trafic web sur le port 80. Une fois que vous avez une machine virtuelle qui est configuré tooserve les demandes web sur le port TCP standard pour hello 80 (n’oubliez pas les services appropriés de toostart hello et ouvrir toutes les règles de pare-feu du système d’exploitation sur hello VM), vous :

1. créer un groupe de sécurité réseau ;
2. créer une règle de trafic entrant autorisant le trafic avec :
   * plage de ports de destination Hello de « 80 »
   * Hello la plage de ports sources de « * » (ce qui permet de n’importe quel port source)
   * une valeur de priorité de moins 65,500 (toobe supérieure priorité de règle de trafic entrant refuser hello fourre-tout par défaut)
3. Associer hello groupe de sécurité réseau à interface réseau de machine virtuelle hello ou un sous-réseau.

Votre environnement à l’aide des règles et des groupes de sécurité réseau, vous pouvez créer toosecure des configurations de réseau complexes. Notre exemple utilise seulement une ou deux règles qui autorisent le trafic HTTP ou la gestion à distance. Pour plus d’informations, voir hello ['Informations'](#more-information-on-network-security-groups) section ou [qu’est un groupe de sécurité réseau ?](../articles/virtual-network/virtual-networks-nsg.md)

