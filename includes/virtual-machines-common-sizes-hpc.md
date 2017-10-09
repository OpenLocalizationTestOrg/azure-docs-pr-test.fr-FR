<!-- A-series - compute-intensive instances, H-series -->

Hello tailles A8-A11 et H-série sont également appelés *instances de calcul intensif*. matériel Hello qui exécute ces tailles est conçu et optimisé pour les calculs intensifs et applications, de modélisation et de simulations de cluster applications gourmandes en réseau, y compris informatique hautes performances (HPC). Hello A8-A11 série utilise Intel Xeon E5-2670 2,6 GHz et hello H-series v3 Intel Xeon E5-2667 @ 3,2 GHz. 

Machines virtuelles de série H sont hello prochaine génération informatiques hautes performances que machines virtuelles destinées à des besoins de calcul haut de gamme, telles que la modélisation moléculaire et fluides. Ces processeurs 8 et 16 ordinateurs virtuels reposent sur la technologie de processeur de hello Intel Haswell E5-2667 V3 avec DDR4 mémoire et le stockage temporaire basée sur SSD. 

De plus toohello substantielle puissance de l’UC, hello H-series propose diverses options de mise en réseau RDMA de latence faible à l’aide de Verification InfiniBand et plusieurs configurations toosupport mémoire intensif calcul besoins en mémoire.



## <a name="h-series"></a>Série H

ACU : 290-300

| Taille | Processeurs virtuels | Mémoire : Gio | Stockage temporaire (SSD) en Gio | Disques de données max. | Débit de disque max : E/S par seconde | Nombre max de cartes réseau |
| --- | --- | --- | --- | --- | --- | --- |
| Standard_H8 |8 |56 |1 000 |16 |16 x 500 |2  |
| Standard_H16 |16 |112 |2000 |32 |32 x 500 |4 |
| Standard_H8m |8 |112 |1 000 |16 |16 x 500 |2  |
| Standard_H16m |16 |224 |2000 |32 |32 x 500 |4  |
| Standard_H16r* |16 |112 |2000 |32 |32 x 500 |4  |
| Standard_H16mr* |16 |224 |2000 |32 |32 x 500 |4 |

*Pour les applications MPI, un réseau principal RDMA dédié est activé par un réseau InfiniBand FDR, qui garantit une très faible latence et une large bande passante.

<br>



## <a name="a-series---compute-intensive-instances"></a>Série A - Instances de calcul intensif

ACU : 225

| Taille | Processeurs virtuels | Mémoire : Gio | Stockage temporaire (HDD) : Gio | Disques de données max. | Débit de disque de données max : E/S par seconde | Nombre max de cartes réseau|
| --- | --- | --- | --- | --- | --- | --- |
| Standard_A8* |8 |56 |382 |16 |16 x 500 |2 |
| Standard_A9* |16 |112 |382 |16 |16 x 500 |4 |
| Standard_A10 |8 |56 |382 |16 |16 x 500 |2  |
| Standard_A11 |16 |112 |382 |16 |16 x 500 |4 |

*Pour les applications MPI, un réseau principal RDMA dédié est activé par un réseau InfiniBand FDR, qui garantit une très faible latence et une large bande passante.

<br>



