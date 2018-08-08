---
title: "Lync Server 2013: Disab. eredit. autorizz. in cont. ogg. PC, User o InetOrgPerson"
TOCTitle: Ereditarietà delle autorizzazioni disabilitata nei contenitori di oggetti Computer, User o InetOrgPerson
ms:assetid: c472ad21-a93d-4fcb-a3d9-60a2134a87fa
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412970(v=OCS.15)
ms:contentKeyID: 49301887
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Ereditarietà delle autorizzazioni disabilitata nei contenitori di oggetti Computer, User o InetOrgPerson in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-12-19_

In un ambiente Servizi di dominio Active Directory bloccato gli oggetti utente e computer vengono spesso inseriti in unità organizzative specifiche in cui l'ereditarietà delle autorizzazioni è disabilitata per proteggere la delega dell'amministrazione e consentire l'utilizzo di oggetti Criteri di gruppo per l'applicazione di criteri di sicurezza.

Durante la preparazione del dominio e l'attivazione del server vengono impostate le voci di controllo di accesso necessarie per Lync Server 2013. Se l'ereditarietà delle autorizzazioni è disabilitata, i gruppi di sicurezza di Lync Server non possono ereditare tali voci di controllo di accesso. In tal caso, i gruppi di sicurezza di Lync Server non possono accedere alle impostazioni e si verificano i due problemi seguenti:

  - Per poter amministrare gli oggetti User, Contact e InetOrgPerson e poter utilizzare i server, è necessario che i gruppi di sicurezza di Lync Server dispongano di voci di controllo di accesso impostate durante la procedura di preparazione del dominio negli insiemi di proprietà, nelle comunicazioni in tempo reale (RTC), RTC User Search e Public Information di ogni utente. Quando l'ereditarietà delle autorizzazioni è disabilitata, i gruppi di sicurezza non ereditano tali voci di controllo di accesso e non possono gestire né i server né gli utenti.

  - Per individuare server e pool, i server che eseguono Lync Server si basano sulle voci di controllo di accesso impostate mediante l'attivazione in oggetti correlati al computer, tra cui il contenitore Microsoft e l'oggetto Server. Quando l'ereditarietà delle autorizzazioni è disabilitata, i gruppi di sicurezza, i server e i pool non ereditano tali voci di controllo di accesso e non possono usufruirne.

Per risolvere questi problemi, in Lync Server è disponibile il cmdlet **Grant-CsOuPermission** che imposta le voci di controllo di accesso di Lync Server necessarie direttamente in un contenitore e in un'unità organizzativa specificata, nonché negli oggetti di tale contenitore o unità organizzativa.

## Impostazione delle autorizzazioni per gli oggetti User, InetOrgPerson e Contact dopo l'esecuzione della preparazione del dominio

In un ambiente Active Directory bloccato in cui è disabilitata l'ereditarietà delle autorizzazioni, durante la preparazione del dominio non vengono impostate le voci di controllo di accesso necessarie nei contenitori o nelle unità organizzative che includono oggetti User o InetOrgPerson all'interno del dominio. In questa situazione, è necessario eseguire il cmdlet **Grant-CsOuPermission** in ogni contenitore o unità organizzativa con oggetti User o InetOrgPerson per cui è disabilitata l'ereditarietà delle autorizzazioni. Nel caso di una topologia a foresta centralizzata, è necessario eseguire questa procedura anche nei contenitori o nelle unità organizzative che contengono oggetti contatto. Per informazioni dettagliate sulle topologie a foresta centralizzata, vedere [Topologie di Active Directory supportate in Lync Server 2013](lync-server-2013-supported-active-directory-topologies.md) nella documentazione relativa al supporto. Il parametro ObjectType specifica il tipo di oggetto. Il parametro OU specifica l'unità organizzativa.

Questo cmdlet consente di aggiungere le voci di controllo di accesso necessarie direttamente nei contenitori o nelle unità organizzative specificati e negli oggetti User o InetOrgPerson all'interno di tali contenitori.

Per eseguire questo cmdlet, è necessario disporre di diritti utente equivalenti all'appartenenza al gruppo Domain Admins. Se, inoltre, nell'ambiente bloccato sono state rimosse le voci di controllo di accesso degli utenti autenticati, è necessario concedere all'account le voci di controllo di accesso per l'accesso in lettura nei contenitori appropriati nel dominio radice della foresta, come descritto in [Rimozione delle autorizzazioni degli utenti autenticati in Lync Server 2013](lync-server-2013-authenticated-user-permissions-are-removed.md) oppure utilizzare un account membro del gruppo Enterprise Admins.

**Per impostare le voci di controllo di accesso necessarie per gli oggetti User, InetOrgPerson e Contact**

1.  Accedere a un computer appartenente al dominio con un account membro del gruppo Domain Admins o che disponga di diritti utente equivalenti.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Eseguire:
    
        Grant-CsOuPermission -ObjectType <User | Computer | InetOrgPerson | Contact | AppContact | Device> 
        -OU <DN name for the OU container relative to the domain root container DN> [-Domain <Domain FQDN>]
    
    Se non si specifica il parametro Domain, per impostazione predefinita verrà utilizzato il dominio locale.
    
    Ad esempio:
    
        Grant-CsOuPermission -ObjectType "User" -OU "cn=Redmond,dc=contoso,dc=net" -Domain "contoso.net"

4.  Nel file di log cercare il risultato di esecuzione **\<Esito positivo\>** alla fine di ogni attività per verificare la corretta impostazione delle autorizzazioni, quindi chiudere la finestra del log. In alternativa, è possibile eseguire il comando seguente per determinare se le autorizzazioni sono state impostate:
    
        Test-CsOuPermission -ObjectType <type of object> 
        -OU <DN name for the OU container relative to the domain root container DN> 
        [-Domain <Domain FQDN>] [-Report <fully qualified path and name of file to create>]
    
    Ad esempio:
    
        Test-CsOuPermission -ObjectType "User" -OU "cn=Redmond,dc=contoso,dc=net" -Domain "contoso.net" -Report "C:\Log\OUPermissionsTest.html"

## Impostazione delle autorizzazioni per oggetti Computer dopo l'esecuzione della preparazione del dominio

In un ambiente Active Directory bloccato in cui è disabilitata l'ereditarietà delle autorizzazioni, durante la preparazione del dominio non vengono impostate le voci di controllo di accesso necessarie nei contenitori o nelle unità organizzative che includono oggetti Computer all'interno del dominio. In questa situazione, è necessario eseguire il cmdlet **Grant-CsOuPermission** in ogni contenitore o unità organizzativa con computer che eseguono Lync Server per cui è disabilitata l'ereditarietà delle autorizzazioni. Il parametro ObjectType specifica il tipo di oggetto.

Questa procedura consente di aggiungere le voci di controllo di accesso necessarie direttamente nei contenitori specificati.

Per eseguire questo cmdlet, è necessario disporre di diritti utente equivalenti all'appartenenza al gruppo Domain Admins. Se sono state inoltre rimosse le voci di controllo di accesso degli utenti autenticati, è necessario concedere all'account le voci di controllo di accesso per l'accesso in lettura nei contenitori appropriati nel dominio radice della foresta, come descritto in [Rimozione delle autorizzazioni degli utenti autenticati in Lync Server 2013](lync-server-2013-authenticated-user-permissions-are-removed.md) oppure utilizzare un account membro del gruppo Enterprise Admins.

**Per impostare le voci di controllo di accesso necessarie per gli oggetti computer**

1.  Accedere al computer del dominio con un account membro del gruppo Domain Admins o che disponga di diritti utente equivalenti.

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Eseguire:
    
        Grant-CsOuPermission -ObjectType <Computer> 
        -OU <DN name for the computer OU container relative to the domain root container DN> 
        [-Domain <Domain FQDN>][-Report <fully qualified path and name of output report>]
    
    Se non si specifica il parametro Domain, per impostazione predefinita verrà utilizzato il dominio locale.
    
    Ad esempio:
    
        Grant-CsOuPermission -ObjectType "Computer" -OU "ou=Lync Servers,dc=litwareinc,dc=com" -Report "C:\Logs\OUPermissions.xml"

4.  Nel file di log di esempio C:\\Logs\\OUPermissions.xml, si dovrebbe poi cercare il risultato di esecuzione **\<Esito positivo\>** alla fine di ogni attività per verificare che non vi siano errori, quindi chiudere il log. È possibile eseguire il cmdlet seguente per verificare le autorizzazioni:
    
        Test-CsOuPermission -ObjectType <type of object> 
        -OU <DN name for the OU container relative to the domain root container DN> [-Domain <Domain FQDN>]
    
    Ad esempio:
    
        Test-CsOuPermission -ObjectType "user","contact" -OU "cn=Bellevue,dc=contoso,dc=net" -Domain "contoso.net"
    

    > [!NOTE]
    > Se si esegue la preparazione del dominio nel dominio radice della foresta in un ambiente Active Directory bloccato, tenere presente che Lync Server richiede l'accesso ai contenitori Schema e Configuration di Active Directory.<BR>Se l'autorizzazione degli utenti autenticati predefinita viene rimossa dai contenitori Schema o Configuration in Servizi di dominio Active Directory, solo i membri del gruppo Schema Admins (per il contenitore Schema) o Enterprise Admins (per il contenitore Configuration) potranno accedere al contenitore specificato. Poiché Setup.exe, i cmdlet di Lync Server Management Shell e il Pannello di controllo di Lync Server devono poter accedere a tali contenitori, si verificherà un errore durante l'installazione e la configurazione degli strumenti di amministrazione, a meno che l'utente che esegue l'installazione non disponga di diritti utente equivalenti all'appartenenza ai gruppi Schema Admins ed Enterprise Admins.<BR>Per risolvere questo problema, sarà necessario concedere al gruppo RTCUniversalGlobalWriteGroup l'accesso in lettura e scrittura ai contenitori dello schema e della configurazione.


