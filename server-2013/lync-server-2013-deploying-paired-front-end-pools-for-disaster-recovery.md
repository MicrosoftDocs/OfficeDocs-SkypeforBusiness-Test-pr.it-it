---
title: "Lync Server 2013: Distribuz. pool Front End abbinati per ripristino di emerg."
TOCTitle: Distribuzione di pool Front End abbinati per il ripristino di emergenza
ms:assetid: 2f12467c-8b90-43e6-831b-a0b096427f17
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204773(v=OCS.15)
ms:contentKeyID: 49300063
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Distribuzione di pool Front End abbinati per il ripristino di emergenza in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-21_

È possibile distribuire facilmente la topologia di ripristino di emergenza dei pool Front End accoppiati mediante il Generatore di topologie.

## Per distribuire una coppia di pool Front End

1.  Se i pool sono nuovi e non sono stati ancora definiti, usare il Generatore di topologie per crearli.

2.  Nel Generatore di topologie fare clic con il pulsante destro del mouse su uno dei due pool e scegliere **Modifica proprietà** .

3.  Fare clic su **Resilienza** nel riquadro a sinistra e selezionare **Pool di backup associato** nel riquadro a destra.

4.  Nella casella sotto **Pool di backup associato** selezionare il pool da accoppiare a questo pool. Sarà possibile selezionare solo pool esistenti che non sono già accoppiati con un altro pool.
    
    ![Finestra di dialogo Resilienza](images/JJ204773.36080581-db76-497d-bf9e-f02b39574d0e(OCS.15).png "Finestra di dialogo Resilienza")  

5.  Selezionare **Failover e failback automatico per VoIP** , quindi fare clic su **OK** .
    
    Quando vengono visualizzati i dettagli su questo pool, il pool associato apparirà nel riquadro a destra sotto **Resilienza** .

6.  Usare il Generatore di topologie per pubblicare la topologia.

7.  Se i due pool non sono stati ancora distribuiti, distribuirli ora in modo da completare la configurazione. È possibile ignorare i due passaggi finali di questa procedura.
    
    Tuttavia, se i pool erano già distribuiti prima che venisse definita la relazione accoppiata, è necessario completare i due passaggi finali che seguono.

8.  Su ogni Front End Server in entrambi i pool eseguire:
    
        <system drive>\Program Files\Microsoft Lync Server 2013\Deployment\Bootstrapper.exe 
    
    Consente di configurare altri servizi necessari per il corretto funzionamento dell'accoppiamento di backup.

9.  Da un prompt dei comandi di Lync Server Management Shell eseguire:
    
        Start-CsWindowsService -Name LYNCBACKUP

10. Forzare la sincronizzazione dei dati utente e di conferenza di entrambi i pool specificando i cmdlet seguenti:
    
    ```
    Invoke-CsBackupServiceSync -PoolFqdn <Pool1 FQDN>
    ```
    ```
    Invoke-CsBackupServiceSync -PoolFqdn <Pool2 FQDN>
    ```
    
    La sincronizzazione dei dati potrebbe richiedere alcuni minuti. Per controllare lo stato è possibile usare i cmdlet seguenti. Assicurarsi che in entrambe le direzioni lo stato sia stazionario.
    
    ```
    Get-CsBackupServiceStatus -PoolFqdn <Pool1 FQDN>
    ```
    ```
    Get-CsBackupServiceStatus -PoolFqdn <Pool2 FQDN>
    ```


> [!NOTE]
> L'opzione <STRONG>Failover e failback automatico per VoIP</STRONG> e gli intervalli di tempo associati nel Generatore di topologie sono applicabili solo alle funzionalità di resilienza vocale introdotte in Lync Server 2010. La selezione di questa opzione non implica che il failover del pool descritto in questo documento sia automatico. Il failover e il failback del pool richiedono sempre che un amministratore richiami manualmente i cmdlet di failover e di failback, rispettivamente.


