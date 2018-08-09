---
title: "Lync Server 2013: Configura utilizzo foto ad alta risoluzione in MS LS 2013"
TOCTitle: "Lync Server 2013: Configura utilizzo foto ad alta risoluzione in MS LS 2013"
ms:assetid: 995da78a-dc44-45a3-908d-16fe36cfa0d9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688150(v=OCS.15)
ms:contentKeyID: 49887672
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione dell'utilizzo delle foto ad alta risoluzione in Microsoft Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-02-05_

Microsoft Lync Server 2010 offre agli utenti la possibilità di visualizzare foto dei propri contatti e di rendere disponibili le proprie agli altri. In genere, queste foto vengono archiviate come parte dell'attributo thumbnailPhoto dell'utente in Active Directory. Ciò implica una seria limitazione alle dimensioni e alle risoluzioni delle foto: l'attributo thumbnailPhoto può contenere solo una fotografia di dimensioni massime pari a 48x48 pixel.

In Microsoft Lync Server 2013, tuttavia, le foto possono essere archiviate nella cassetta postale di Microsoft Exchange Server 2013 dell'utente. In questo modo è possibile utilizzare foto di dimensioni massime pari a 648x648 pixel. Oltre a questo, Exchange 2013 può ridimensionare automaticamente le foto per l'uso nei diversi prodotti a seconda delle necessità. In genere, ciò prevede tre dimensioni e risoluzioni di foto:

  - 48x48 pixel, le dimensioni usate per l'attributo thumbnailPhoto di Active Directory. Se si carica una foto in Exchange 2013Exchange crea automaticamente una versione 48x48 pixel della foto e aggiorna l'attributo thumbnailPhoto dell'utente. Tenere presente, comunque che non è vero il contrario: se si aggiorna manualmente l'attributo thumbnailPhoto in Active Directory la foto nella cassetta postale di Exchange 2013 dell'utente non viene aggiornata automaticamente.

  - 96x96 pixel, per l'uso in Microsoft Outlook 2013 Web App, Microsoft Outlook 2013, Microsoft Lync Web App e Lync 2013.

  - 648x648 pixel per l'uso in Lync 2013 e Microsoft Lync Web App.


> [!NOTE]
> Se si dispone delle risorse, è consigliabile caricare foto nel formato 648x648 che offrono la risoluzione massima e la qualità ottimale dell'immagine in qualsiasi applicazione di Office 2013. Ogni foto JPEG di dimensioni pari a 648x648 e una profondità di 24 bit produce un file di dimensioni pari a circa 240 kilobyte. Ciò significa che sarà necessario circa 1 megabyte di spazio su disco per ogni 4 foto di utenti.



Le foto ad alta risoluzione, accessibili mediante Servizi Web di Exchange, possono essere caricate dagli utenti che usano Outlook 2013 Web App; gli utenti possono aggiornare solo proprie foto. Gli amministratori possono invece aggiornare le foto di qualsiasi utente mediante la shell di gestione di Exchange e una serie di comandi di Windows PowerShell analoghi ai seguenti:

    $photo = ([Byte[]] $(Get-Content -Path "C:\Photos\Kenmyer.jpg" -Encoding Byte -ReadCount 0))
    Set-UserPhoto -Identity "Ken Myer" -PictureData $photo -Confirm:$False
    Set-UserPhoto -Identity "Ken Myer" -Save -Confirm:$False

Il primo comando nell'esempio precedente usa il cmdlet Get-Content per leggere i contenuti del file C:\\Photos\\Kenmyer.jpg e archiviare i dati in una variabile denominata $photo. Nel secondo comando, il cmdlet Set-UserPhoto di Exchange viene usato per caricare la foto e associarla all'account utente di Ken Myer.


> [!NOTE]
> In questo esempio, il nome visualizzato di Active Directory di Ken Myer è utilizzato come identità dell'account utente. È anche possibile fare riferimento a un account utente mediante altri identificatori quali l'indirizzo SMTP dell'utente oppure il relativo nome dell'entità utente. Vedere la documentazione relativa al cmdlet Set-UserPhoto all'indirizzo <A class=uri href="http://go.microsoft.com/fwlink/?linkid=268536%26clcid=0x410">http://go.microsoft.com/fwlink/?linkid=268536&amp;clcid=0x410</A> per ulteriori informazioni



Il caricamento della foto non equivale ad assegnarla all'account utente di Ken Myer. Esso infatti produce semplicemente un'anteprima della foto da visualizzare nella pagina Opzioni di Outlook Web App. Per assegnare effettivamente la foto all'account utente, quest'ultimo deve fare clic su **Salva** nella pagina Opzioni oppure l'amministratore deve eseguire il terzo comando nell'esempio. Il terzo comando usa il parametro Save per assegnare la foto all'account utente di Ken Myer:

    Set-UserPhoto -Identity "Ken Myer" -Save -Confirm:$False

Per verificare che la nuova foto sia stata assegnata all'account utente, Ken Myer può accedere a Lync 2013, selezionare **Opzioni** e quindi scegliere **Immagine**. La nuova foto aggiunta deve essere visualizzata come foto personale di Ken. In alternativa, gli amministratori possono verificare la foto per qualsiasi utenti avviando Internet Explorer e passando a un URL analogo a questo:

    https://atl-mail-001.litwareinc.com/ews/Exchange.asmx/s/GetUserPhoto?email=kenmyer@litwareinc.com&size=HR648x648

Se l'amministratore può visualizzare la foto in Internet Explorer ma l'utente non riesce a vedere la propria foto in Lync 2013, ciò indica un problema di connettività con i servizi Web di Exchange o con il servizio Autodiscover di Exchange.

Si noti, inoltre, che non sono richieste ulteriori operazioni di configurazione per rendere questa foto disponibile in Lync 2013. La foto risulterà infatti immediatamente disponibile dopo il caricamento e una volta eseguito il cmdlet Set-UserPhoto.

