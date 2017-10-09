

## <a name="multi-and-single-instance-vms"></a>Machines virtuelles à instance unique ou multi-instance
De nombreux clients en cours d’exécution sur un compte Azure il critiques qu’ils peuvent planifier lorsque leurs ordinateurs virtuels subir une maintenance planifiée en raison de temps d’arrêt toohello--environ 15 minutes, qui se produit lors de la maintenance. Vous pouvez utiliser le contrôle de disponibilité définit toohelp lors de la maintenance planifiée de réception des machines virtuelles configurées.

Il existe deux configurations possibles pour les machines virtuelles s’exécutant sur Azure : en tant qu’instance unique ou multi-instance. Si les machines virtuelles sont dans un groupe à haute disponibilité, elles sont configurées en tant que multi-instance. Notez que même si des machines virtuelles uniques sont déployées dans un groupe à haute disponibilité, elles sont traitées comme si elles étaient des machines virtuelles multi-instances. Si les machines virtuelles ne sont PAS dans un groupe à haute disponibilité, elles sont configurées en tant qu’instance unique.  Pour plus d’informations sur les groupes à haute disponibilité, consultez [hello de gérer la disponibilité de vos Machines virtuelles de Windows](../articles/virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ou [hello de gérer la disponibilité de vos Machines virtuelles de Linux](../articles/virtual-machines/linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Instance toosingle des mises à jour de maintenance planifiée et machines virtuelles d’instances multiples se produisent séparément. Reconfigurer vos machines virtuelles toobe à instance unique (si elles sont des instances multiples) ou toobe multi-instance (s’ils sont uniques), vous pouvez contrôler lorsque leurs ordinateurs virtuels de réception hello planifié maintenance. Consultez [Maintenance planifiée des machines virtuelles Linux dans Azure](../articles/virtual-machines/linux/planned-maintenance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [Maintenance planifiée des machines virtuelles dans Azure](../articles/virtual-machines/windows/planned-maintenance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) pour plus d’informations sur la maintenance planifiée des machines virtuelles Azure.

## <a name="for-multi-instance-configuration"></a>Pour la configuration multi-instance
Vous pouvez sélectionner l’heure hello maintenance planifiée a un impact sur vos ordinateurs virtuels qui sont déployés dans une configuration à haute disponibilité en supprimant ces machines virtuelles à partir de la haute disponibilité.

1. Un e-mail est envoyé à tooyou sept jours du calendrier avant hello planifié tooyour de gestion des ordinateurs virtuels dans une configuration à plusieurs instances. Hello ID d’abonnement et noms de machines virtuelles de hello affectée à plusieurs instances sont inclus dans le corps hello de courrier électronique de hello.
2. Pendant les sept jours, vous pouvez choisir les temps hello vos instances sont mises à jour en supprimant vos machines virtuelles à plusieurs instances de cette région à partir de leur jeu de disponibilité. Cette modification dans les causes de configuration un redémarrage, en tant que Machine virtuelle de hello concerne le déplacement d’un hôte physique, ciblé pour la maintenance, tooanother physique hôte qui n’est pas ciblé pour maintenance.
3. Vous pouvez supprimer hello machine virtuelle à partir de son groupe à haute disponibilité hello portail Azure.

   1. Dans le portail de hello, sélectionnez hello VM tooremove hello à haute disponibilité.  

   2. Sous **Paramètres**, cliquez sur **Groupe à haute disponibilité**.

      ![Sélection du groupe à haute disponibilité](./media/virtual-machines-planned-maintenance-schedule/availabilitysetselection.png)

   3. Disponibilité de hello définir le menu déroulant, sélectionnez « Fait pas partie d’un ensemble de disponibilité. »

      ![Supprimer du groupe](./media/virtual-machines-planned-maintenance-schedule/availabilitysetwarning.png)

   4. En haut de hello, cliquez sur **enregistrer**. Cliquez sur **Oui** tooacknowledge cette action redémarre hello machine virtuelle.

   >[!TIP]
   >Vous pouvez reconfigurer hello toomulti-instance de machine virtuelle plus tard en sélectionnant un des groupes à haute disponibilité hello répertorié.

4. Supprimé de la haute disponibilité de machines virtuelles sont des hôtes de l’Instance tooSingle déplacé et ne sont pas mis à jour au cours de hello planifié maintenance tooAvailability définir des Configurations.
5. Une fois terminé hello mise à jour tooAvailability définir les machines virtuelles (selon tooschedule décrite dans l’e-mail d’origine de hello), vous devez ajouter hello VM dans leurs groupes à haute disponibilité. Devenant partie d’un ensemble de disponibilité reconfigure les machines virtuelles de hello comme instances multiples et entraîne un redémarrage. En règle générale, une fois que toutes les mises à jour de plusieurs instances sont effectuées sur tout environnement de Azure hello, maintenance d’instance unique suit.

Supprimer une machine virtuelle d’un groupe à haute disponibilité est également possible à l’aide d’Azure PowerShell :

```
Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Remove-AzureAvailabilitySet | Update-AzureVM
```

## <a name="for-single-instance-configuration"></a>Pour la configuration en instance unique
Vous pouvez sélectionner l’heure hello maintenance planifiée a un impact sur vous machines virtuelles dans une configuration d’instance unique en ajoutant ces ordinateurs virtuels à haute disponibilité.

Procédure pas à pas

1. Un e-mail est envoyé à tooyou sept jours du calendrier avant hello planifié tooVMs de maintenance dans une configuration d’instance unique. Hello ID d’abonnement et noms de machines virtuelles de hello affecté à Instance unique sont inclus dans le corps hello de courrier électronique de hello.
2. Pendant les sept jours, vous pouvez choisir les temps hello à votre instance de redémarrages en ajoutant votre disponibilité tooan de machines virtuelles d’instance unique est défini dans ce même région. Cette modification dans les causes de configuration un redémarrage, en tant que Machine virtuelle de hello concerne le déplacement d’un hôte physique, ciblé pour la maintenance, tooanother physique hôte qui n’est pas ciblé pour maintenance.
3. Suivez les instructions ici tooadd existant de machines virtuelles dans des groupes à haute disponibilité à l’aide de hello portail Azure et Azure PowerShell. (Voir exemple hello Azure PowerShell qui suit les étapes ci-après.)
4. Une fois que ces machines virtuelles sont reconfigurées comme instances multiples, ils sont exclus de la maintenance de hello planifié tooSingle-instance VM.
5. Une fois la mise à jour de la machine virtuelle hello à instance unique est terminée (selon le tooschedule par courrier électronique d’origine de hello), vous pouvez retourner toosingle instance hello machines virtuelles en supprimant les machines virtuelles de hello de leurs groupes à haute disponibilité.

Ajout d’une machine virtuelle tooan disponibilité également définie peut être obtenue à l’aide d’Azure PowerShell :

    Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Set-AzureAvailabilitySet -AvailabilitySetName "<AvSetName>" | Update-AzureVM

<!--Anchors-->



<!--Link references-->
[Virtual Machines Manage Availability]: virtual-machines-windows-tutorial.md
[Understand planned versus unplanned maintenance]: virtual-machines-manage-availability.md#Understand-planned-versus-unplanned-maintenance/
