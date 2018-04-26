---
title: 'Lync Server 2013: Esecuzione della preparazione della foresta'
TOCTitle: Esecuzione della preparazione della foresta
ms:assetid: 9d62f7be-bcfe-421d-8d8a-225567102a35
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412732(v=OCS.15)
ms:contentKeyID: 49301466
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Esecuzione della preparazione della foresta per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-29_

È possibile usare il programma di installazione o i cmdlet della Lync Server Management Shell per preparare la foresta. Il cmdlet per la preparazione della foresta è **Enable-CsAdForest**.

Dopo aver eseguito la preparazione della foresta, è necessario verificare che le impostazioni globali siano state replicate prima procedere alla preparazione del dominio.

## Per utilizzare il programma di installazione per la preparazione della foresta

1.  Accedere a un computer aggiunto a un dominio come membro del gruppo Enterprise Admins per il dominio radice della foresta.

2.  Dalla cartella o dal supporto di installazione di Lync Server 2013, eseguire Setup.exe per avviare la Distribuzione guidata.

3.  Fare clic su **Prepara Active Directory** e quindi attendere che venga determinato lo stato della distribuzione.

4.  Al **Passaggio 3: Preparazione della foresta corrente** , fare clic su **Esegui** .

5.  Nella pagina **Prepara foresta** fare clic su **Avanti** .
    

    > [!NOTE]
    > La preparazione della foresta consente di scegliere dove collocare i gruppi universali per Lync Server 2013. Scegliere una posizione conforme ai requisiti dell'organizzazione.



6.  Nella pagina **Esecuzione comandi in corso** cercare il messaggio **Stato attività: Completata** e quindi fare clic su **Visualizza registro** .

7.  Nella colonna **Azione** espandere **Preparazione foresta** , cercare il risultato dell'esecuzione **\<Esito positivo\>** alla fine di ogni attività per verificare la corretta esecuzione della preparazione della foresta, chiudere il registro, quindi fare clic su **Fine** .

8.  Attendere il completamento della replica di Active Directory oppure forzare la replica in tutti i controller di dominio elencati nello snap-in **Siti e servizi di Active Directory** nel controller di dominio radice della foresta, prima di eseguire la preparazione del dominio. Forzare la replica tra i controller di dominio in tutti i siti di Active Directory perché venga eseguita la replica all'interno dei siti entro pochi minuti.

## Per utilizzare i cmdlet per la preparazione della foresta

1.  Accedere a un computer che fa parte di un dominio come membro del gruppo Domain Admins nel dominio radice della foresta.

2.  Installare i componenti di base di Lync Server nel modo seguente:
    
    1.  Dalla cartella o dal supporto di installazione di Lync Server 2013 eseguire Setup.exe per avviare la Distribuzione guidata di Lync Server.
    
    2.  Se viene chiesto di installare Microsoft Visual C++ Redistributable, fare clic su **Sì** .
    
    3.  Nella finestra di dialogo del programma di installazione di Lync Server 2013 viene chiesto il percorso di installazione dei file di Lync Server. Scegliere il percorso predefinito o **Sfoglia** per selezionare il percorso desiderato e quindi fare clic su **Installa** .
    
    4.  Nella pagina Contratto di Licenza selezionare **Accetto i termini del Contratto di Licenza** e quindi fare clic su **OK** . Il programma di installazione installerà i componenti di base di Lync Server 2013.

3.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

4.  Eseguire:
    
        Enable-CsAdForest [-GroupDomain <FQDN of the domain in which to create the universal groups>]
    
    Ad esempio:
    
        Enable-CsAdForest -GroupDomain domain1.contoso.com 
    
    Se non si specifica il parametro GroupDomain, il valore predefinito è il dominio locale. Se i gruppi universali sono stati creati in precedenza in un dominio che non è quello predefinito, è necessario specificare il parametro GroupDomain in modo esplicito.

5.  Attendere il completamento della replica di Active Directory oppure forzare la replica in tutti i controller di dominio elencati nello snap-in **Siti e servizi di Active Directory** per il controller del dominio radice della foresta, prima di eseguire la preparazione del dominio.

6.  Verificare l'esito della preparazione della foresta.
    
        Get-CsAdForest 
    
    Questo cmdlet restituisce il valore **LC\_FORESTSETTINGS\_STATE\_READY** se la preparazione della foresta è stata eseguita correttamente.

## Vedere anche

#### Attività

[Utilizzo dei cmdlet per annullare la preparazione della foresta per Lync Server 2013](lync-server-2013-using-cmdlets-to-reverse-forest-preparation.md)  

#### Ulteriori risorse

[Preparazione della foresta per Lync Server 2013](lync-server-2013-preparing-the-forest.md)

