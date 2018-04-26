---
title: 'Lync Server 2013: Esecuzione della preparazione dello schema'
TOCTitle: Esecuzione della preparazione dello schema
ms:assetid: 9d02bdb1-ff29-417a-bcce-b068b31207d8
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412729(v=OCS.15)
ms:contentKeyID: 49301463
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Esecuzione della preparazione dello schema in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-29_

È possibile usare il programma di installazione o i cmdlet della Lync Server Management Shell per preparare lo schema di Active Directory. Il cmdlet che estende lo schema di Active Directory è **Install-CsAdServerSchema**.


> [!NOTE]
> Il cmdlet per la preparazione dello schema (<STRONG>Install-CsAdServerSchema</STRONG>) deve accedere al master schema. A tale scopo, è necessario che il servizio Registro di sistema remoto sia in esecuzione e che la chiave del Registro di sistema remoto sia abilitata. Se non è possibile abilitare il servizio Registro di sistema remoto nel master schema, è possibile eseguire il cmdlet in locale nel master schema. Per informazioni dettagliate sull'accesso remoto al Registro di sistema, vedere l'articolo 314837 della Microsoft Knowledge Base "Gestione dell'accesso remoto al Registro di sistema" all'indirizzo <A href="http://go.microsoft.com/fwlink/p/?linkid=125769">http://go.microsoft.com/fwlink/p/?linkId=125769</A>.



Dopo aver completato la preparazione dello schema, verificare manualmente che la partizione dello schema sia stata replicata prima di procedere alla preparazione della foresta. Per informazioni dettagliate, vedere [Verifica della replica dello schema in Lync Server 2013](lync-server-2013-verifying-schema-replication.md).

## Per utilizzare il programma di installazione per preparare lo schema della foresta corrente

1.  Accedere a un server nella foresta con un account membro del gruppo Schema Admins e con diritti di amministratore per il master schema.

2.  Dalla cartella o dal supporto di installazione di Lync Server 2013, eseguire Setup.exe per avviare la Distribuzione guidata.

3.  Se viene chiesto di installare Microsoft Visual C++ Redistributable, fare clic su **Sì** .

4.  Nella finestra di dialogo del programma di installazione di Lync Server 2013 viene chiesto il percorso di installazione dei file di Lync Server. Scegliere il percorso predefinito o **Sfoglia** per selezionare il percorso desiderato e quindi fare clic su **Installa** .

5.  Nella pagina Contratto di Licenza selezionare **Accetto i termini del Contratto di Licenza** e quindi fare clic su **OK** .

6.  Il programma di installazione installerà i componenti di base di Lync Server.

7.  Quando la Distribuzione guidata è pronta, fare clic su **Prepara Active Directory** e quindi attendere che venga determinato lo stato della distribuzione.

8.  Al **Passaggio 1: Prepara schema** , fare clic su **Esegui** .

9.  Nella pagina **Prepara schema** fare clic su **Avanti** .

10. Nella pagina **Esecuzione comandi in corso** cercare il messaggio **Stato attività: Completata** e quindi fare clic su **Visualizza registro** .

11. Nella colonna **Azione** espandere **Preparazione schema** , cercare il risultato dell'esecuzione **\<Esito positivo\>** alla fine di ogni attività per verificare la corretta esecuzione della preparazione della foresta, chiudere il registro, quindi fare clic su **Fine** .

12. Attendere il completamento della replica di Active Directory o forzare la replica.

13. Verificare manualmente che le modifiche allo schema siano state replicate in tutti gli altri controller di dominio. Per informazioni dettagliate, vedere [Verifica della replica dello schema in Lync Server 2013](lync-server-2013-verifying-schema-replication.md).

## Per usare i cmdlet di preparazione dello schema della foresta corrente

1.  Accedere a un computer nella foresta con un account membro del gruppo Schema Admins e con diritti di amministratore per il master schema.

2.  Installare i componenti di base di Lync Server nel modo seguente:
    
    1.  Dalla cartella o dal supporto di installazione di Lync Server 2013 eseguire Setup.exe per avviare la Distribuzione guidata di Lync Server.
    
    2.  Se viene chiesto di installare Microsoft Visual C++ Redistributable, fare clic su **Sì** .
    
    3.  Nella finestra di dialogo del programma di installazione di Lync Server 2013 viene chiesto il percorso di installazione dei file di Lync Server. Scegliere il percorso predefinito o **Sfoglia** per selezionare il percorso desiderato e quindi fare clic su **Installa** .
    
    4.  Nella pagina Contratto di Licenza selezionare **Accetto i termini del Contratto di Licenza** e quindi fare clic su **OK** . Il programma di installazione installerà i componenti di base di Lync Server 2013.

3.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

4.  Eseguire:
    
        Install-CsAdServerSchema [-Ldf <directory where the .ldf file is located>] 
    
    Se non si specifica il parametro Ldf, il valore predefinito è il percorso di installazione di Lync Server 2013 letto da Registro di sistema.
    
    Ad esempio:
    
        Install-CsAdServerSchema -Ldf "C:\Program Files\Microsoft Lync Server 2013\Deployment\Setup"

5.  Utilizzare il cmdlet seguente per verificare la corretta esecuzione della preparazione dello schema.
    
        Get-CsAdServerSchema 
    
    Questo cmdlet restituisce il valore **SCHEMA\_VERSION\_STATE\_CURRENT** se la preparazione dello schema è stata eseguita correttamente.

6.  Attendere il completamento della replica di Active Directory o forzare la replica.

7.  Verificare manualmente che le modifiche allo schema siano state replicate in tutti gli altri controller di dominio. Per informazioni dettagliate, vedere [Verifica della replica dello schema in Lync Server 2013](lync-server-2013-verifying-schema-replication.md).

## Vedere anche

#### Attività

[Verifica della replica dello schema in Lync Server 2013](lync-server-2013-verifying-schema-replication.md)  

#### Concetti

[Preparazione dello schema di Active Directory in Lync Server 2013](lync-server-2013-preparing-the-active-directory-schema.md)

