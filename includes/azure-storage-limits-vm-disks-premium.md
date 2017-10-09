**Disques de machine virtuelle non gérés Premium : par limites de compte**

| Ressource | Limite par défaut |
| --- | --- |
| Capacité totale des disques par compte |35 To |
| Capacité totale des instantanés par compte |10 To |
| Bande passante maximale par compte (entrée + sortie<sup>1</sup>) |<=50 Gbits/s |

<sup>1</sup>*entrée* fait référence à des données tooall (demandes) envoyées compte de stockage tooa. *Sortie* fait référence tooall des données (réponses) reçues d’un compte de stockage.

**Disques de machine virtuelle non gérés Premium : par limites de disques**

| Type de disque de stockage Premium | P10 | P20 | P30 | P40 | P50 |
| --- | --- | --- | --- | --- | --- |
| Taille du disque |128 Go |512 Go |1024 Go (1 To) |2 048 Gio (2 To)|4 095 Gio (4 To)|
| Nb max. d'E/S par seconde par disque |500 |2 300 |5 000 |7500 |7500 |
| Débit max. par disque |100 Mo/s | 150 Mo/s |200 Mo/s |250 Mo/s |250 Mo/s |
| Nombre maximal de disques par compte de stockage |280 |70 |35 | 17 | 8 |

**Disques de machine virtuelle non gérés Premium : par limites de machines virtuelles**

| Ressource | Limite par défaut |
| --- | --- |
| Nb max. d'E/S par seconde par machine virtuelle |80 000 E/S par seconde avec la machine virtuelle GS5<sup>1</sup> |
| Débit max. par machine virtuelle |2 000 Mo/s avec la machine virtuelle GS5<sup>1</sup> |

<sup>1</sup>reportez-vous trop[taille de machine virtuelle](../articles/virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) des limites sur les tailles de machine virtuelle. 

