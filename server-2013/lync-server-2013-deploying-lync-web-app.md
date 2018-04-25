---
title: Distribuzione di Lync Web App
TOCTitle: Distribuzione di Lync Web App
ms:assetid: b6301e98-051c-4e4b-8e10-ec922a8f508a
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205190(v=OCS.15)
ms:contentKeyID: 49301739
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Distribuzione di Lync Web App

 

_**Ultima modifica dell'argomento:** 2013-07-18_

Lync Web App è un client Web IIS (Internet Information Services) che viene installato con Lync Server 2013 ed è abilitato per impostazione predefinita. Non sono necessarie operazioni aggiuntive per abilitare Lync Web App nel server o per distribuire il client Web agli utenti. Ogni volta che un utente fa clic su un URL riunione ma non ha il client Lync 2013 installato, ha la possibilità di partecipare alla riunione utilizzando la versione più recente di Lync Web App.

Le funzionalità vocali, video e di condivisione disponibili in Lync Web App richiedono un controllo Microsoft ActiveX. È possibile installare in anticipo il controllo ActiveX oppure consentire agli utenti di installarlo quando necessario, situazione che si verifica la prima volta che gli utenti utilizzano Lync Web App o la prima volta che accedono a una funzionalità che richiede il controllo ActiveX.


> [!NOTE]
> Nelle distribuzioni di server perimetrali di Lync Server 2013 è necessario un proxy inverso HTTPS nella rete perimetrale per l'accesso client a Lync Web App. È inoltre necessario pubblicare gli URL semplici. Per informazioni dettagliate, vedere <A href="lync-server-2013-setting-up-reverse-proxy-servers.md">Configurare server proxy inversi per Lync Server 2013</A> e <A href="lync-server-2013-planning-for-simple-urls.md">Pianificazione degli URL semplici in Lync Server 2013</A>.



## Abilitazione dell'autenticazione a più fattori per Lync Web App

La versione Lync Server 2013 di Lync Web App supporta l'autenticazione a più fattori. Oltre al nome e alla password utente, è perciò possibile richiedere ulteriori metodi di autenticazione, ad esempio smart card o PIN, per autenticare che partecipano alle riunioni di Lync da reti esterne. È possibile abilitare l'autenticazione a più fattori distribuendo il server federativo di Active Directory Federation Service (ADFS) e abilitando l'autenticazione passiva in Lync Server 2013. Dopo la configurazione di ADFS, agli utenti esterni che tentano di partecipare a riunioni di Lync viene visualizzata una pagina Web di autenticazione a più fattori ADFS contenente la richiesta di nome e password utente, con gli eventuali altri metodi di autenticazione configurati.

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Se si intende configurare ADFS per l'autenticazione a più fattori, è importante considerare quanto segue:
<ul>
<li><p>L'autenticazione a più fattori ADFS funziona se il partecipante e l'organizzatore della riunione fanno parte della stessa organizzazione, oppure di un'organizzazione federata ADFS. Non funziona invece per gli utenti federati di Lync, in quanto non è attualmente supportata dall'infrastruttura Web di Lync Server.</p></li>
<li><p>Se si utilizzano dispositivi di bilanciamento del carico hardware, abilitare il salvataggio permanente dei cookie in tali dispositivi, in modo che tutte le richieste provenienti dal client Lync Web App vengano gestite dallo stesso Front End Server.</p></li>
<li><p>Quando si stabilisce una relazione di trust di relying party tra i server ADFS e Lync Server, assegnare ai token una durata tale da coprire la lunghezza massima delle riunioni di Lync. 240 minuti in genere sono una durata sufficiente per i token.</p></li>
<li><p>Questa configurazione non si applica ai client mobili Lync.</p></li>
</ul></td>
</tr>
</tbody>
</table>


**Per configurare l'autenticazione a più fattori**

1.  Installare un ruolo del server federativo ADFS. Per informazioni dettagliate, vedere la guida alla distribuzione di Active Directory Federation Services 2.0 all'indirizzo [http://go.microsoft.com/fwlink/?linkid=267511\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=267511%26clcid=0x410)

2.  Creare certificati per ADFS. Per ulteriori informazioni, vedere la sezione "Certificati server federativi" dell'argomento Pianificazione e distribuzione di ADFS per l'utilizzo con l'accesso Single Sign-On all'indirizzo [http://go.microsoft.com/fwlink/p/?LinkId=285376](http://go.microsoft.com/fwlink/p/?linkid=285376).

3.  Nell'interfaccia della riga di comando Windows PowerShell eseguire il comando seguente:
    
        add-pssnapin Microsoft.Adfs.powershell

4.  Stabilire una relazione eseguendo il comando seguente:
    
        Add-ADFSRelyingPartyTrust -Name ContosoApp -MetadataURL https://lyncpool.contoso.com/passiveauth/federationmetadata/2007-06/federationmetadata.xml

5.  Impostare le regole di relying party seguenti:
    
        $IssuanceAuthorizationRules = '@RuleTemplate = "AllowAllAuthzRule" => issue(Type = "http://schemas.contoso.com/authorization/claims/permit", Value = "true");'
        $IssuanceTransformRules = '@RuleTemplate = "PassThroughClaims" @RuleName = "Sid" c:[Type == "http://schemas.contoso.com/ws/2008/06/identity/claims/primarysid"]=> issue(claim = c);'
    
        Set-ADFSRelyingPartyTrust -TargetName ContosoApp -IssuanceAuthorizationRules $IssuanceAuthorizationRules -IssuanceTransformRules $IssuanceTransformRules
    
        Set-CsWebServiceConfiguration -UseWsFedPassiveAuth $true -WsFedPassiveMetadataUri https://dc.contoso.com/federationmetadata/2007-06/federationmetadata.xml

## Configurazione di BranchCache

La funzionalità BranchCache in Windows 7 e Windows Server 2008 R2 può interferire con i componenti Web di Lync Web App. Per evitare problemi agli utenti di Lync Web App, verificare che la funzionalità BranchCache non sia abilitata.

Per informazioni dettagliate sulla disabilitazione di BranchCache, vedere la relativa Guida alla distribuzione, disponibile in formato Word nell'Area download Microsoft all'indirizzo [http://go.microsoft.com/fwlink/?linkid=268788\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=268788%26clcid=0x410) e in formato HTML nella raccolta di documentazione tecnica TechNet su Windows Server 2008 R2 all'indirizzo [http://go.microsoft.com/fwlink/?linkid=268789\&clcid=0x410](http://go.microsoft.com/fwlink/?linkid=268789%26clcid=0x410).

## Verifica della distribuzione di Lync Web App

È possibile usare il cmdlet Test-CsUcwaConference per verificare che una coppia di utenti di test possa partecipare a una conferenza tramite UCWA (Unified Communications Web API). Per informazioni dettagliate su questo cmdlet, vedere [Test-CsUcwaConference](test-csucwaconference.md) nella documentazione di Lync Server Management Shell.

## Risoluzione dei problemi relativi all'installazione del plug-in in Windows Server 2008 R2

Se l'installazione del plug-in ha esito negativo in un computer che esegue Windows Server 2008 R2, potrebbe essere necessario modificare l'impostazione di sicurezza di Internet Explorer oppure l'impostazione della chiave DisableMSI del Registro di sistema.

**Per modificare l'impostazione di sicurezza in Internet Explorer**

1.  Aprire Internet Explorer.

2.  Fare clic su **Strumenti**, su **Opzioni Internet** e quindi su **Avanzate**.

3.  Scorrere verso il basso fino alla sezione **Sicurezza**.

4.  Deselezionare **Non salvare pagine crittografate su disco** e quindi fare clic su **OK**.
    

    > [!NOTE]
    > Se selezionata, questa impostazione inoltre causerà un errore durante il tentativo di scaricare un allegato da Lync Web App.



5.  Tornare a partecipare alla riunione. Il download del plug-in dovrebbe avere luogo senza errori.

**Per modificare l'impostazione DisableMSI del Registro di sistema**

1.  Fare clic sul pulsante **Start** e quindi scegliere **Esegui**.

2.  Per accedere all'editor del Registro di sistema, digitare **regedit**.

3.  Passare a HKEY\_LOCAL\_MACHINE\\Software\\Policies\\Microsoft\\Windows\\Installer.

4.  Modificare o aggiungere la chiave DisableMSI di tipo REG\_DWORD del Registro di sistema e impostarla su 0.

5.  Tornare a partecipare alla riunione.

## Vedere anche

#### Concetti

[Configurazione della pagina di partecipazione alle riunioni in Lync Server 2013](lync-server-2013-configuring-the-meeting-join-page.md)  
[Piattaforme supportate da Lync Web App per Lync Server 2013](lync-server-2013-lync-web-app-supported-platforms.md)

