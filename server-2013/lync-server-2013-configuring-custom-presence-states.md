---
title: Configurazione di stati presenza personalizzati
TOCTitle: Configurazione di stati presenza personalizzati
ms:assetid: e17364a8-8b93-45fc-a614-c80e45435d42
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398997(v=OCS.15)
ms:contentKeyID: 52062456
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Configurazione di stati presenza personalizzati

 

_**Ultima modifica dell'argomento:** 2013-01-10_

Per definire stati di presenza personalizzati in Lync 2013, creare un file di configurazione XML di presenza personalizzata e quindi specificarne il percorso mediante i cmdlet di Lync Server Management Shell**New-CSClientPolicy** o **Set-CSClientPolicy** con il parametro CustomStateURL.

Le proprietà dei file di configurazione sono le seguenti:

  - Gli stati di presenza personalizzati possono essere configurati con gli indicatori di presenza Disponibile, Non disponibile e Non disturbare.

  - L'attributo di disponibilità determina quale indicatore di presenza è associato al testo dello stato personalizzato. Nell'esempio riportato più avanti in questo argomento, viene visualizzato il testo di stato Lavoro da casa a destra dell'indicatore di presenza verde (Disponibile).

  - Il testo di stato può essere composto al massimo da 64 caratteri.

  - È possibile aggiungere al massimo quattro stati di presenza personalizzati.

  - Il parametro CustomStateURL specifica la posizione del file di configurazione. In Lync 2013 la modalità di sicurezza avanzata SIP è abilitata per impostazione predefinita. Sarà quindi necessario archiviare il file di configurazione della presenza personalizzato su un server Web con abilitazione per HTTPS. In caso contrario, i client di Lync 2013 non saranno in grado di connettersi al file. Ad esempio, `https://lspool.corp.contoso.com/ClientConfigFolder/CustomPresence.xml` sarebbe un indirizzo valido.


> [!NOTE]
> Benché non sia consigliabile in un ambiente di produzione, sarà possibile testare un file di configurazione disponibile un una condivisione file non HTTPS, utilizzando l'impostazione EnableSIPHighSecurityMode del Registro di sistema per disabilitare la modalità di sicurezza avanzata SIP sul client. Sarà quindi possibile usare l'impostazione CustomStateURL del Registro di sistema per specificare un percorso non HTTPS per il file di configurazione. Si noti che Lync 2013 rispetta l'impostazione del Registro di sistema Lync 2010, ma l'hive del Registro di sistema è stato aggiornato. Creare le impostazioni del Registro di sistema come indicato di seguito: 
> <UL>
> <LI>
> <P>HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Office\15.0\Lync\EnableSIPHighSecurityMode</P>
> <P>Tipo: DWORD</P>
> <P>Dati valore: 0</P>
> <LI>
> <P>HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Office\15.0\Lync\CustomStateURL</P>
> <P>Tipo: String (REG_SZ)</P>
> <P>Dati valore (esempi): file://\\lspool.corp.contoso.com\LSFileShare\ClientConfigFolder\Presence.xml or file:///c:/LSFileShare/ClientConfigFolder/Group_1_Pres.xml</P></LI></UL>



Localizzare lo stato di presenza personalizzato specificando uno o più schemi di ID impostazioni locali (LCID) nel file di configurazione XML. Nell'esempio riportato più avanti in questo argomento è illustrata la localizzazione in Inglese - Stati Uniti (1033), Norvegese - Bokmål (1044), Francese - Francia (1036) e Turco (1055). Per un elenco di LCID, vedere gli ID impostazioni locali assegnati da Microsoft all'indirizzo Web <http://go.microsoft.com/fwlink/?linkid=157331>.

## Per aggiungere stati di presenza personalizzati in Lync 2013

1.  Creare un file di configurazione XML nel formato dell'esempio seguente:
    
        <?xml version="1.0"?>
        <customStates xmlns="http://schemas.microsoft.com/09/2009/communicator/customStates">
          <customState ID="1" availability="online">
            <activity LCID="1033">Working from Home</activity>
            <activity LCID="1044">activity 2 for 1044</activity>
            <activity LCID="1055">activity 3 for 1055</activity>
          </customState>
          <customState ID="2" availability="busy">
            <activity LCID="1033">In a Live Meeting</activity>
            <activity LCID="1036">Equivalent French String for - In a Live Meeting </activity>
          </customState>
          <customState ID="3" availability="busy">
            <activity LCID="1033">Meeting with Customer</activity>
            <activity LCID="1055">meeting with client</activity>
            <activity LCID="1036">Equivalent French String for - Meeting with Customer</activity>
          </customState>
          <customState ID="4" availability="do-not-disturb">
            <activity LCID="1033">Interviewing</activity>
          </customState>
        </customStates>

2.  Salvare il file di configurazione XML in un server Web con abilitazione per HTTPS. Nell'esempio il file è denominato Presence.xml e viene salvato nel percorso https://lspool.corp.contoso.com/ClientConfigFolder/CustomPresence.xml.

3.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

4.  In Lync Server Management Shell definire il percorso del file di configurazione XML utilizzando un comando analogo al seguente:
    
        New-CsClientPolicy -Identity ContosoCustomStates 
        -CustomStateURL "https://lspool.corp.contoso.com/ClientConfigFolder/CustomPresence.xml"

5.  Utilizzare il cmdlet **Grant-CSClientPolicy** per assegnare questo nuovo criterio agli utenti.

Per informazioni dettagliate, vedere [New-CsClientPolicy](new-csclientpolicy.md) e [Grant-CsClientPolicy](grant-csclientpolicy.md) nella documentazione di Lync Server Management Shell.


> [!NOTE]
> <UL>
> <LI>
> <P>Per impostazione predefinita, Lync Server 2013&nbsp;aggiorna i criteri e le impostazioni dei client ogni tre ori.</P>
> <LI>
> <P>Se si desidera continuare a usare le impostazioni di Criteri di gruppo delle versioni precedenti, ad esempio CustomStateURL, Lync 2013 riconoscerà le impostazioni se si trovano nell'hive del Registro di sistema relativo ai nuovi criteri (HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Office\15.0\Lync). I criteri client basati su server avranno tuttavia priorità.</P></LI></UL>


