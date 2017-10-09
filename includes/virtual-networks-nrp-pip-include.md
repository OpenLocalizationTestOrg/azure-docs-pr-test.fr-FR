## <a name="public-ip-address"></a>Adresse IP publique
Une ressource d’adresse IP publique fournit une adresse IP réservée ou une adresse IP dynamique accessible sur Internet. Vous pouvez créer une adresse IP publique en tant qu’objet autonome, vous devez tooassociate il tooanother objet tooactually utiliser l’adresse de hello. Vous pouvez associer un équilibreur de charge tooa d’adresse IP publique, passerelle d’application ou un réseau tooprovide Internet access toothose des ressources.  

| Propriété | Description | Exemples de valeurs |
| --- | --- | --- |
| **publicIPAllocationMethod** |Définit si l’adresse IP de hello est *statique* ou *dynamique*. |static, dynamic |
| **idleTimeoutInMinutes** |Définit hello inactif délai d’expiration, valeur par défaut est de 4 minutes. Si aucun autre paquet pour une session donnée n’est reçue dans ce délai, hello est arrêtée. |Toute valeur aléatoire comprise entre 4 et 30. |
| **ipAddress** |Adresse IP affectée tooobject. Il s’agit d’une propriété en lecture seule. |104.42.233.77 |

### <a name="dns-settings"></a>Paramètres DNS
Les adresses IP publiques ont un objet enfant nommé **dnsSettings** contenant hello propriétés suivantes :

| Propriété | Description | Exemples de valeurs |
| --- | --- | --- |
| **domainNameLabel** |Ordinateur hôte nommé utilisé pour la résolution de nom. |www, ftp, vm1 |
| **fqdn** |Nom qualifié complet pour l’adresse IP publique hello. |www.westus.cloudapp.azure.com |
| **reverseFqdn** |Nom de domaine complet qui résout l’adresse IP de toohello et qui est enregistré dans DNS comme un enregistrement PTR. |www.contoso.com. |

Exemple d’adresse IP publique au format JSON :

    {
       "name": "PIP01",
       "location": "North US",
       "tags": { "key": "value" },
       "properties": {
          "publicIPAllocationMethod": "Static",
          "idleTimeoutInMinutes": 4,
          "ipAddress": "104.42.233.77",
          "dnsSettings": {
             "domainNameLabel": "mylabel",
             "fqdn": "mylabel.westus.cloudapp.azure.com",
             "reverseFqdn": "contoso.com."
          }
       }
    } 

### <a name="additional-resources"></a>Ressources supplémentaires
* Obtenez davantage d’informations sur les [adresses IP publiques](../articles/virtual-network/virtual-networks-reserved-public-ip.md).
* En savoir plus sur les [adresses IP publiques de niveau d’instance](../articles/virtual-network/virtual-networks-instance-level-public-ip.md).
* Hello de lecture [documentation de référence API REST](https://msdn.microsoft.com/library/azure/mt163638.aspx) des adresses pour l’adresse IP publique.

