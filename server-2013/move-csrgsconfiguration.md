---
title: Move-CsRgsConfiguration
TOCTitle: Move-CsRgsConfiguration
ms:assetid: 983eadb8-baee-41ba-bba4-2f2b01471250
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398782(v=OCS.15)
ms:contentKeyID: 49301427
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Move-CsRgsConfiguration

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Consente di eseguire la migrazione delle impostazioni di configurazione di Response Group da Microsoft Office Communications Server 2007 R2 o Microsoft Lync Server 2010 a Microsoft Lync Server 2013. Questo cmdlet è stato introdotto in Lync Server 2010.

## Sintassi

    Move-CsRgsConfiguration -Destination <String> -Source <String> [-Force <SwitchParameter>]

## Esempi

## ESEMPIO 1

Il comando mostrato nell'esempio 1 esegue la migrazione dell'applicazione Response Group da atl-ocsrgs-001.litwareinc.com a redmond-lyncrgs-001.litwareinc.com.

    Move-CsRgsConfiguration -Source atl-ocsrgs-001.litwareinc.com -Destination redmond-lyncrgs-001.litwareinc.com 

## Descrizione dettagliata

L'applicazione Response Group consente di instradare automaticamente le chiamate telefoniche a entità come il supporto tecnico o la linea del servizio clienti. Quando qualcuno chiama un numero di telefono designato, la chiamata può essere automaticamente indirizzata all'insieme appropriato di agenti di Response Group. In alternativa, la chiamata può essere instradata a una coda del sistema IVR (Interactive Voice Response). In questa coda potrebbe essere posta una serie di domande (ad esempio, "Sta chiamando per un ordine ﻿in corso?") e quindi il chiamante, in base alle risposte date, potrebbe ottenere le informazioni desiderate o essere instradato a un agente di Response Group.

Se attualmente l'applicazione Response Group viene eseguita in Office Communications Server 2007 R2 o in Lync Server 2010, il cmdlet **Move-CsRgsConfiguration** consente di eseguire la migrazione di tale servizio in Lync Server 2013. Per eseguire la migrazione, è necessario chiamare il cmdlet **Move-CsRgsConfiguration** e specificare 1) il nome di dominio completo (FQDN) della versione esistente dell'applicazione Response Group (origine) e 2) l'FQDN della nuova versione Lync Server 2013 del servizio (destinazione). **Move-CsRgsConfiguration** quindi sposterà tutte le impostazioni di configurazione, i file audio e gli oggetti contatto dalla versione esistente (Office Communications Server 2007 R2 o Lync Server 2010) in Lync Server 2013. Dopo la migrazione del servizio, tutte le chiamate a un numero di telefono di Response Group verranno gestite da Lync Server 2013 e non saranno più gestite dalla versione precedente del servizio.

Prima di poter eseguire **Move-CsRgsConfiguration**, è necessario installare il pacchetto di interfacce per la compatibilità con le versioni precedenti di WMI. Tale applicazione viene installata eseguendo il file OCSWMIBC.msi, disponibile nella cartella Setup del DVD di installazione.

Se Office Communications Server 2007 esegue Microsoft SQL Server 2005, prima di tentare di eseguire la migrazione dell'applicazione Response Group, sarà necessario installare il client nativo Microsoft SQL Server 2005 nel computer in cui verrà eseguito il cmdlet **Move-CsRgsConfiguration**. Se il client nativo non è installato, verrà visualizzato il messaggio di errore "Impossibile accedere alle impostazioni WMI" quando viene chiamato **Move-CsRgsConfiguration**.

Il cmdlet **Move-CsRgsConfiguration** consente esclusivamente di eseguire la migrazione da Office Communications Server 2007 R2 o Lync Server 2010 a Lync Server 2013. Non può essere utilizzato per eseguire la migrazione da un'istanza di Lync Server 2013 a una nuova istanza di Lync Server 2013. Questo tipo di migrazione può essere eseguito soltanto mediante i nuovi cmdlet **Import-CsRgsConfiguration** e **Export-CsRgsConfiguration**.

Utenti autorizzati a eseguire il cmdlet: per impostazione predefinita, sono autorizzati a eseguire localmente il cmdlet **Move-CsRgsConfiguration** i membri dei seguenti gruppi: RTCUniversalServerAdmins. Per restituire un elenco di tutti i ruoli RBAC (Role-Based Access Control) a cui è stato assegnato questo cmdlet, inclusi gli eventuali ruoli RBAC personalizzati creati dall'utente, dal prompt di Windows PowerShell eseguire il seguente comando:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Move-CsRgsConfiguration"}

## Parametri


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Parametro</th>
<th>Obbligatorio</th>
<th>Tipo</th>
<th>Descrizione</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Destination</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>FQDN del computer in cui deve essere ospitata l'applicazione Response GroupLync Server 2013 (percorso di destinazione della copia).</p></td>
</tr>
<tr class="even">
<td><p><em>Source</em></p></td>
<td><p>Obbligatorio</p></td>
<td><p>System.String</p></td>
<td><p>FQDN del pool in cui è attualmente ospitata l'applicazione Response GroupOffice Communications Server 2007 R2 o Lync Server 2010 (percorso di origine della copia).</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Facoltativo</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Consente di non visualizzare i messaggi relativi agli errori non irreversibili che possono verificarsi durante l'esecuzione del comando.</p></td>
</tr>
</tbody>
</table>


## Tipi di input

Nessuno. **Move-CsRgsConfiguration** non accetta l'input da pipeline.

## Tipi restituiti

**Move-CsRgsConfiguration** sposta le istanze di Microsoft.Rtc.Management.WritableSettings.ServiceSettings da un servizio all'altro.

## Vedere anche

#### Ulteriori risorse

[Get-CsRgsConfiguration](get-csrgsconfiguration.md)  
[Move-CsRgsConfiguration](move-csrgsconfiguration.md)

