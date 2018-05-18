- Le réseau virtuel doit se trouver dans la même **région** et le même **abonnement** Azure que le compte Batch.

- Pour les pools créés avec une configuration de machine virtuelle, seuls les réseaux virtuels basés sur Azure Resource Manager sont pris en charge. Pour les pools créés avec une configuration de services cloud, seuls les réseaux virtuels classiques sont pris en charge. 
  
- Pour utiliser un réseau virtuel classique, le principal du service `MicrosoftAzureBatch` doit jouer le rôle de contrôle d’accès en fonction du rôle (RBAC) `Classic Virtual Machine Contributor` pour le réseau virtuel spécifié. Toutefois, pour utiliser un réseau virtuel basé sur Azure Resource Manager, aucune configuration d’autorisation supplémentaire n’est requise.

- Le sous-réseau spécifié pour le pool doit avoir suffisamment d’adresses IP non attribuées pour contenir le nombre de machines virtuelles ciblées pour le pool, autrement dit, la somme des propriétés `targetDedicatedNodes` et `targetLowPriorityNodes` du pool. Si le sous-réseau ne dispose pas de suffisamment d’adresses IP non attribuées, le pool alloue partiellement les nœuds de calcul, et une erreur de redimensionnement se produit. 

- Le réseau virtuel doit autoriser les communications à partir du service Batch pour pouvoir planifier des tâches sur les nœuds de calcul. Vous pouvez le vérifier en déterminant si le réseau virtuel comprend des groupes de sécurité réseau associés (NSG). Si la communication vers les nœuds de calcul dans le sous-réseau spécifié est refusée par un groupe de sécurité réseau, alors le service Batch définit l’état des nœuds de calcul sur **inutilisable**. 

- Si le réseau virtuel spécifié comporte des groupes de sécurité réseau (NSG) associés et/ou un pare-feu, configurez les ports entrants et sortants comme indiqué dans les tableaux suivants :


  |    Port(s) de destination    |    Adresse IP source      |   Port source    |    Azure Batch ajoute-t-il des NSG ?    |    Élément requis pour permettre l’utilisation des machines virtuelles ?    |    Action que l’utilisateur doit effectuer   |
  |---------------------------|---------------------------|----------------------------|----------------------------|-------------------------------------|-----------------------|
  |   <ul><li>Pour les pools créés avec la configuration de machines virtuelles : 29876, 29877</li><li>Pour les pools créés avec une configuration de services cloud : 10100, 20100, 30100</li></ul>        |    Adresses IP du rôle de service Batch uniquement | * ou 443 |    Oui. Azure Batch ajoute des NSG au niveau des cartes réseau jointes aux machines virtuelles. Ces NSG autorisent le trafic uniquement à partir d’adresses IP du rôle de service Batch. Même si vous ouvrez ces ports au web tout entier, le trafic sera bloqué au niveau de la carte réseau. |    Oui  |  Vous n’avez pas besoin de spécifier un NSG, car Azure Batch autorise uniquement les adresses IP Batch. <br /><br /> Toutefois, si vous ne spécifiez pas de NSG, assurez-vous que ces ports sont ouverts pour le trafic entrant. <br /><br /> Si vous spécifiez le caractère * en tant qu’adresse IP source de votre NSG, Batch ajoute des NSG au niveau des cartes réseau attachées aux machines virtuelles. |
  |    3389 (Windows), 22 (Linux)               |    Ordinateurs de l’utilisateur, utilisés à des fins de débogage, afin que vous puissiez accéder à distance aux machines virtuelles.    |   *  | Non                                    |    Non                    |    Ajoutez des NSG si vous souhaitez autoriser les utilisateurs à accéder à distance aux machines virtuelles (via RDP ou SSH).   |                                


  |    Port(s) sortant(s)    |    Destination    |    Azure Batch ajoute-t-il des NSG ?    |    Élément requis pour permettre l’utilisation des machines virtuelles ?    |    Action que l’utilisateur doit effectuer    |
  |------------------------|-------------------|----------------------------|-------------------------------------|------------------------|
  |    443    |    Azure Storage    |    Non    |    Oui    |    Si vous ajoutez des NSG, vérifiez que ce port est ouvert pour le trafic sortant.    |

   Aussi, assurez-vous que votre point de terminaison de Stockage Azure peut être résolu par tous les serveurs DNS personnalisés qui traitent votre réseau virtuel. Plus précisément, les URL sous la forme `<account>.table.core.windows.net`, `<account>.queue.core.windows.net` et `<account>.blob.core.windows.net` doivent être résolvables. 

   Si vous ajoutez un NSG basé sur le Gestionnaire des ressources, vous pouvez utiliser des [balises de service](../articles/virtual-network/security-overview.md#service-tags) pour sélectionner les adresses IP de Stockage correspondant à la région spécifique des connexions sortantes. Notez que les adresses IP de Stockage doivent se trouver dans la même région que votre compte Batch et votre réseau virtuel. Les balises de service sont actuellement en préversion dans certaines régions Azure.