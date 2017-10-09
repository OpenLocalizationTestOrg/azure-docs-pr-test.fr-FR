Ensuite, si tous les serveurs sur le cluster de hello exécutent Windows Server 2008 R2 ou Windows Server 2012, vous devez vérifier ce correctif hello [KB2854082](http://support.microsoft.com/kb/2854082) est installé sur chaque hello sur des serveurs locaux ou des machines virtuelles Azure qui font partie du cluster de hello. N’importe quel serveur ou la machine virtuelle qui est dans un cluster de hello, mais pas dans le groupe de disponibilité hello, également ce correctif logiciel doit être installé.

Dans la session de bureau à distance hello pour chacun des nœuds de cluster hello, téléchargez [KB2854082](http://support.microsoft.com/kb/2854082) tooa les répertoire local. Ensuite, installez séquentiellement hello correctif sur chaque nœud du cluster. Si le service de cluster hello est en cours d’exécution sur le nœud de cluster hello, serveur de hello est redémarré à fin hello d’installation du correctif logiciel hello.

> [!WARNING]
> L’arrêt du service de cluster hello ou hello serveur affecte l’intégrité de quorum hello votre cluster et hello du groupe de disponibilité, et peut entraîner le votre toogo de cluster hors connexion. toomaintain hello haute disponibilité de votre cluster pendant l’installation, assurez-vous que :
> 
> * Hello cluster est l’intégrité du quorum optimal. 
> * Avant d’installer les correctifs hello sur n’importe quel nœud, tous les nœuds de cluster sont en ligne.
> * Avant d’installer les correctifs hello sur n’importe quel nœud du cluster de hello, autoriser hello correctif installation toorun toocompletion sur un nœud, notamment redémarrage hello serveur.
> 
> 

