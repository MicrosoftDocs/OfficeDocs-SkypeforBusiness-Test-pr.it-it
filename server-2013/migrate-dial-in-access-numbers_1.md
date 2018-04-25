---
title: Eseguire la migrazione dei numeri di accesso esterno
TOCTitle: Eseguire la migrazione dei numeri di accesso esterno
ms:assetid: 568a94b7-a697-4ab2-9008-dc9ecc1c87c8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204898(v=OCS.15)
ms:contentKeyID: 49300580
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Eseguire la migrazione dei numeri di accesso esterno

 

_**Ultima modifica dell'argomento:** 2012-09-26_

Per la migrazione dei numeri di accesso esterno è necessario eseguire due operazioni: eseguire il cmdlet **Import-CsLegacyConfiguration** (completato precedentemente in [Importare criteri e impostazioni](import-policies-and-settings.md)) per la migrazione dei dial plan e di altre impostazioni dei numeri di accesso esterno ed eseguire il cmdlet **Move-CsApplicationEndpoint** per la migrazione degli oggetti contatto.

## Per eseguire la migrazione dei numeri di accesso esterno

1.  Aprire lo strumento di amministrazione di Office Communications Server 2007 R2.

2.  Nell'albero della console fare clic con il pulsante destro del mouse sul nodo della foresta, scegliere **Proprietà** e quindi fare clic su **Proprietà Operatore Conferenza** .

3.  Nella scheda **Numeri di accesso** fare clic su **Servito dal pool** per ordinare i numeri telefonici di accesso in base al pool associato e identificare tutti i numeri di accesso per il pool da cui si sta eseguendo la migrazione.

4.  Per identificare l'URI SIP per ogni numero di accesso, fare doppio clic sul numero di accesso per aprire la finestra di dialogo **Modifica numero Operatore Conferenza** . L'URI è indicato in **URI SIP** .

5.  Aprire Lync Server Management Shell.

6.  Per spostare ogni numero di accesso esterno in un pool ospitato in Lync Server 2013, eseguire:
    
        Move-CsApplicationEndpoint -Identity <SIP URI of the access number to be moved> -Target <FQDN of the pool to which the access number is moving>

7.  Nello strumento di amministrazione di Office Communications Server 2007 R2, nella scheda **Numeri di accesso** , verificare che non rimangano numeri di accesso esterno per il pool di Office Communications Server 2007 R2 da cui si sta eseguendo la migrazione.

