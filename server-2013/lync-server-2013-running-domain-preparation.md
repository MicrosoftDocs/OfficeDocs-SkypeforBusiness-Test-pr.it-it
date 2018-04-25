---
title: 'Lync Server 2013: Esecuzione della preparazione del dominio'
TOCTitle: Esecuzione della preparazione del dominio
ms:assetid: 95dab800-1f2c-4506-b36c-99986643b149
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398761(v=OCS.15)
ms:contentKeyID: 49301372
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Esecuzione della preparazione del dominio per Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-04-16_

È possibile usare il programma di installazione o i cmdlet della Lync Server Management Shell per preparare i domini. Il cmdlet per la preparazione di un dominio è **Enable-CsAdDomain**.

La preparazione del dominio è l'ultima operazione per la preparazione di Servizi di dominio Active Directory per Lync Server 2013.

## Per utilizzare il programma di installazione per la preparazione dei domini

1.  Accedere a qualsiasi server del dominio come membro del gruppo Domain Admins.

2.  Dalla cartella o dal supporto di installazione di Lync Server 2013 eseguire Setup.exe per avviare la Distribuzione guidata di Lync Server.

3.  Fare clic su **Prepara Active Directory** e quindi attendere che venga determinato lo stato della distribuzione.

4.  Al **Passaggio 5: Preparazione del dominio corrente** , fare clic su **Esegui** .

5.  Nella pagina **Prepara dominio** fare clic su **Avanti** .

6.  Nella pagina **Esecuzione comandi in corso** cercare il messaggio **Stato attività: Completata** e quindi fare clic su **Visualizza registro** .

7.  Nella colonna **Azione** espandere **Preparazione dominio** , cercare il risultato dell'esecuzione **\<Esito positivo\>** alla fine di ogni attività per verificare la corretta esecuzione della preparazione del dominio, chiudere il registro, quindi fare clic su **Fine** .

8.  Attendere il completamento della replica di Active Directory o forzare la replica in tutti i controller di dominio elencati nello snap-in Siti e servizi di Active Directory per il controller di dominio radice della foresta.

## Per usare i cmdlet per preparare il dominio

1.  Accedere a qualsiasi server del dominio come membro del gruppo Domain Admins.

2.  Installare i componenti di base di Lync Server nel modo seguente:
    
    1.  Dalla cartella o dal supporto di installazione di Lync Server 2013 eseguire Setup.exe per avviare la Distribuzione guidata di Lync Server.
    
    2.  Se viene chiesto di installare Microsoft Visual C++ Redistributable, fare clic su **Sì** .
    
    3.  Nella finestra di dialogo del programma di installazione di Lync Server 2013 viene chiesto il percorso di installazione dei file di Lync Server. Scegliere il percorso predefinito o **Sfoglia** per selezionare il percorso desiderato e quindi fare clic su **Installa** .
    
    4.  Nella pagina Contratto di Licenza selezionare **Accetto i termini del Contratto di Licenza** e quindi fare clic su **OK** . Il programma di installazione installerà i componenti di base di Lync Server 2013.

3.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

4.  Eseguire:
    
        Enable-CsAdDomain [-Domain <DomainFQDN>] 
    
    Ad esempio:
    
        Enable-CsAdDomain -Domain domain1.contoso.net 
    
    Se non si specifica il parametro Domain, per impostazione predefinita verrà utilizzato il dominio locale.

5.  Verificare l'esito della preparazione del dominio. Eseguire:
    
        Get-CsAdDomain [-Domain <Domain FQDN>] [-DomainController <Domain controller FQDN>] [-GlobalCatalog <Global catalog server FQDN>] [-GlobalSettingsDomainController <Domain controller FQDN where global settings are stored>] 
    
    Ad esempio:
    
        Get-CsAdDomain -Domain domain1.contoso.net -GlobalSettingsDomainController dc01.domain1.contoso.com
    

    > [!NOTE]
    > Il parametro GlobalSettingsDomainController consente di indicare dove vengono archiviate le impostazioni globali. Se le impostazioni sono archiviate nel contenitore System, come avviene in genere con le distribuzioni di aggiornamento per cui non è stata eseguita la migrazione dell'impostazione globale nel contenitore Configuration, definire un controller di dominio nella radice della foresta di Active Directory. Se invece le impostazioni globali sono incluse nel contenitore Configuration, come avviene in genere con le distribuzioni nuove o di aggiornamento per cui è stata eseguita la migrazione delle impostazioni nel contenitore Configuration, definire un controller di dominio nella foresta. Se non si specifica questo parametro, il cmdlet presuppone che le impostazioni siano archiviate nel contenitore Configuration a fa riferimento a un controller di dominio qualsiasi in Servizi di dominio Active Directory.

    
    Se non si specifica il parametro **Domain**, per impostazione predefinita viene usato il dominio locale.
    
    Se la preparazione del dominio ha avuto esito positivo, questo cmdlet restituisce un valore **LC\_DOMAINSETTINGS\_STATE\_READY** .

## Vedere anche

#### Attività

[Utilizzo di cmdlet per ripristinare la preparazione del dominio per Lync Server 2013](lync-server-2013-using-cmdlets-to-reverse-domain-preparation.md)  

#### Ulteriori risorse

[Preparazione dei domini per Lync Server 2013](lync-server-2013-preparing-domains.md)

