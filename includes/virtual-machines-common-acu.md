



Nous avons créé le concept de hello de hello unité de calcul de Azure (ACU) tooprovide un moyen de comparer les performances de calcul (processeur) entre les références (SKU) de Azure. Cela vous aidera à identifier facilement la référence est probablement toosatisfy vos besoins de performances.  L’unité ACU est actuellement normalisée sur une machine virtuelle de petite taille (Standard_A1) correspondant à 100, et toutes les autres références représentent ensuite approximativement la rapidité avec laquelle la référence en question peut exécuter un test d’évaluation. 

> [!IMPORTANT]
> Hello ACU n'est qu’une indication.  résultats Hello pour votre charge de travail peuvent varier. 
> 
> 

<br>

| Famille de références | ACU \ Processeur virtuel |
| --- | --- |
| [A0](../articles/virtual-machines/windows/sizes-general.md) |50 |
| [A1-A4](../articles/virtual-machines/windows/sizes-general.md) |100 |
| [A5-A7](../articles/virtual-machines/windows/sizes-general.md) |100 |
| [A1_v2-A8_v2](../articles/virtual-machines/windows/sizes-general.md) |100 |
| [A2m_v2-A8m_v2](../articles/virtual-machines/windows/sizes-general.md) |100 |
| [A8-A11](../articles/virtual-machines/windows/sizes-hpc.md) |225* |
| [D1-D14](../articles/virtual-machines/windows/sizes-general.md) |160 |
| [D1_v2-D15_v2](../articles/virtual-machines/windows/sizes-general.md) |210 - 250* |
| [DS1-DS14](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) |160 |
| [DS1_v2-DS15_v2](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) |210-250* |
| [D_v3](../articles/virtual-machines/virtual-machines-windows-sizes-general.md) |160-190* ** |
| [Ds_v3](../articles/virtual-machines/virtual-machines-windows-sizes-general.md) |160-190* ** |
| [E_v3](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) |160-190* ** |
| [Es_v3](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) |160-190* ** |
| [F1-F16](../articles/virtual-machines/windows/sizes-compute.md) |210-250* |
| [F1s-F16s](../articles/virtual-machines/windows/sizes-compute.md) |210-250* |
| [G1-G5](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) |180 - 240* |
| [GS1-GS5](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) |180 - 240* |
| [H](../articles/virtual-machines/windows/sizes-hpc.md) |290 - 300* |
| [L4s-L32s](../articles/virtual-machines/windows/sizes-storage.md) |180 - 240* |
| [M](../articles/virtual-machines/virtual-machines-windows-sizes-memory.md) | 160-180** |

ACUs marqués avec un * utiliser Intel® Turbo technologie tooincrease processeur fréquence et fournir une amélioration des performances.  Hello quantité de renforcement de hello peut varier en fonction de la taille de machine virtuelle hello, de charge de travail et d’autres charges de travail en cours d’exécution sur hello même hôte.

** Avec technologie Hyper-thread. 
