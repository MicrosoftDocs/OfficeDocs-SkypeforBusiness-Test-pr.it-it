---
title: 'Lync Server 2013: Configurare componenti aggiuntivi per le chat room'
TOCTitle: Configurare componenti aggiuntivi per le chat room
ms:assetid: 4eeaf19e-8369-4f6f-af65-a283cf7daa1c
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204878(v=OCS.15)
ms:contentKeyID: 49300523
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurare componenti aggiuntivi per le chat room in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2013-02-21_

Nel Pannello di controllo di Lync Server 2013 è possibile usare la sezione **Componente aggiuntivo** della pagina **Chat persistente** per associare URL alle chat di Chat persistente. Questi URL compaiono nel riquadro di estensibilità della conversazione nella chat room del client Lync 2013. Perché gli utenti possano vedere il proprio aggiornamento nel client Lync 2013, un amministratore deve aggiungere i componenti aggiuntivi all'elenco dei componenti aggiuntivi registrati e i responsabili o i creatori di chat rom devono associare le chat con uno dei componenti aggiuntivi registrati.

I componenti aggiuntivi sono usati per ampliare l'esperienza all'interno della chat. In genere i componenti aggiuntivi includono un URL che punta a un'applicazione Silverlight che intercetta l'inserimento di un codice del titolo in una chat room e mostra la cronologia del titolo azionario nel riquadro di estensibilità. Altri esempi sono l'incorporamento di un URL di OneNote 2013 nella chat room come componente aggiuntivo per includere contenuto condiviso, ad esempio "In primo piano" o "Argomento del giorno".

## Per configurare componenti aggiuntivi per le chat room

1.  Da un account utente assegnato al ruolo CsPersistentChatAdministrator o CsAdministrator, accedere a un qualsiasi computer nella distribuzione interna.

2.  Fare clic sul pulsante **Start** e scegliere Pannello di controllo di Lync Server oppure aprire una finestra del browser e quindi immettere l'URL di amministrazione. Per informazioni dettagliate sui diversi metodi che è possibile utilizzare per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>È inoltre possibile usare i cmdlet di Windows PowerShell. Per informazioni dettagliate, vedere <a href="configuring-persistent-chat-server-by-using-windows-powershell-cmdlets.md">Configurazione del server Chat persistente tramite i cmdlet di Windows PowerShell</a> nella documentazione relativa alla distribuzione.</td>
    </tr>
    </tbody>
    </table>


3.  Sulla barra di spostamento sinistra fare clic su **Chat persistente** e quindi su **Componente aggiuntivo** .
    
    Per più distribuzioni di pool di server Chat persistente, selezionare il pool appropriato dall'elenco a discesa.

4.  Nella pagina **Componente aggiuntivo** fare clic su **Nuovo** .

5.  In **Seleziona un servizio** selezionare il servizio corrispondente al pool di server Chat persistente in cui è necessario creare il componente aggiuntivo. I componenti aggiuntivi non possono essere spostati da un pool a un altro o condivisi da pool diversi.

6.  In **Nuovo componente aggiuntivo** eseguire le operazioni seguenti:
    
      - In **Nome** specificare un nome per il nuovo componente aggiuntivo.
    
      - In **URL** specificare l'URL da associare al componente aggiuntivo. Gli URL devono limitarsi ai protocolli http e https.

7.  Fare clic su **Commit** .

## Vedere anche

#### Attività

[Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md)  

#### Concetti

[Configurazione del server Chat persistente tramite i cmdlet di Windows PowerShell](configuring-persistent-chat-server-by-using-windows-powershell-cmdlets.md)

