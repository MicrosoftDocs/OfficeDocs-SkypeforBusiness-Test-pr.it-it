---
title: 'Lync Server 2013: Associare una subnet a un sito di rete'
TOCTitle: Associare una subnet a un sito di rete
ms:assetid: aa69e3ac-542a-4ba1-9582-2e6bee29f633
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg412804(v=OCS.15)
ms:contentKeyID: 49301620
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Associare una subnet a un sito di rete in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2014-10-20_

Ogni subnet della rete deve essere associata a un sito di rete specifico. Le informazioni della subnet, infatti, vengono utilizzate per determinare il sito di rete in cui si trova un endpoint durante un tentativo di avvio di una nuova sessione. Quando è nota la posizione di ogni parte coinvolta in una sessione, tali informazioni possono essere utilizzate dalle funzionalità di VoIP aziendale avanzate per determinare come gestire la configurazione o il routing delle chiamate.

<table>
<thead>
<tr class="header">
<th><img src="images/Gg412908.important(OCS.15).gif" title="important" alt="important" />Importante:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Alle impostazioni della configurazione di rete è necessario aggiungere tutti gli indirizzi IP pubblici configurati degli Audio/Video Edge Server nella distribuzione. Tali indirizzi IP vengono aggiunti come subnet con una maschera pari a 32. Il sito di rete associato deve corrispondere al sito di rete configurato appropriato. Ad esempio, il NetworkSiteID dell'indirizzo IP pubblico corrispondente all'A/V Edge Server nel sito centrale di Chicago sarà Chicago. Per informazioni dettagliate sugli indirizzi IP pubblici, vedere <a href="lync-server-2013-determine-external-a-v-firewall-and-port-requirements.md">Determinare i requisiti di porte e firewall A/V esterni per Lync Server 2013</a> nella documentazione relativa alla pianificazione.</td>
</tr>
</tbody>
</table>



> [!NOTE]
> Viene generato un avviso KHI (Key Health Indicator) in cui è riportato un elenco di indirizzi IP presenti all'interno della rete. Tali indirizzi però non sono associati ad alcuna subnet oppure sono inclusi in una subnet, ma quest'ultima non è associata ad alcun sito di rete. Nel corso di un periodo di otto ore questo avviso viene generato solo una volta. Di seguito sono riportate le informazioni rilevanti dell'avviso con un esempio:<BR><STRONG>Origine :</STRONG> Servizio criteri larghezza di banda CS (Core)<BR><STRONG>Numero evento :</STRONG> 36034<BR><STRONG>Livello :</STRONG> 2<BR><STRONG>Descrizione :</STRONG> le subnet per gli indirizzi IP seguenti: &lt;Elenco di indirizzi IP&gt; non sono configurate oppure non sono associate a un sito di rete.<BR><STRONG>Causa :</STRONG> le subnet per gli indirizzi IP corrispondenti non sono presenti nelle impostazioni della configurazione di rete oppure non sono associate a un sito di rete.<BR><STRONG>Soluzione :</STRONG> aggiungere le subnet corrispondenti all'elenco di indirizzi IP nelle impostazioni della configurazione di rete e associare ogni subnet a un sito di rete.<BR>Se, ad esempio, gli indirizzi IP all'interno dell'avviso corrispondono a 10.121.248.226 e 10.121.249.20, tali indirizzi non sono associati ad alcuna subnet oppure la subnet a cui sono associati non appartiene a un sito di rete. Se le subnet corrispondenti agli indirizzi sono 10.121.248.0/24 e 10.121.249.0/24, è possibile risolvere il problema come segue: 
> <OL>
> <LI>
> <P>Verificare che l'indirizzo IP 10.121.248.226 sia associato alla subnet 10.121.248.0/24 e che l'indirizzo IP 10.121.249.20 sia associato alla subnet 10.121.249.0/24.</P>
> <LI>
> <P>Verificare che le subnet 10.121.248.0/24 e 10.121.249.0/24 siano associate ognuna a un sito di rete.</P></LI></OL>



Per i dettagli sull'utilizzo di subnet di rete, vedere la documentazione di Lync Server Management Shell per i cmdlet seguenti:

  - [New-CsNetworkSubnet](new-csnetworksubnet.md)

  - [Get-CsNetworkSubnet](get-csnetworksubnet.md)

  - [Set-CsNetworkSubnet](set-csnetworksubnet.md)

  - [Remove-CsNetworkSubnet](remove-csnetworksubnet.md)

<table>
<thead>
<tr class="header">
<th><img src="images/Gg398201.tip(OCS.15).gif" title="tip" alt="tip" />Suggerimento:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Se si utilizza un elevato numero di subnet, per associare queste ultime ai siti è consigliabile utilizzare un file con valori delimitati da virgole (CSV). Il file CSV deve contenere le quattro colonne seguenti: <strong>IPAddress</strong>, <strong>mask</strong>, <strong>description</strong> e <strong>NetworkSiteID</strong>.</td>
</tr>
</tbody>
</table>


## Per associare una subnet a un sito di rete utilizzando Management Shell

1.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

2.  Per associare una subnet a un sito di rete, eseguire il cmdlet **New-CsNetworkSubnet**:
    
        New-CsNetworkSubnet -SubnetID <String> -MaskBits <Int32> -NetworkSiteID <String>
    
    Ad esempio:
    
        New-CsNetworkSubnet -SubnetID 172.11.12.13 - MaskBits 20 -NetworkSiteID Chicago
    
    In questo esempio viene creata un'associazione tra la subnet 172.11.12.13 e il sito di rete “Chicago”.

3.  Ripetere il passaggio 2 per tutte le subnet della topologia.

## Per associare subnet a siti di rete mediante l'importazione di un file CSV

1.  Creare un file CSV contenente tutte le subnet che si desidera aggiungere. Creare ad esempio un file denominato **subnet.csv** con il contenuto seguente:
    
    `IPAddress, mask, description, NetworkSiteID`
    
    `172.11.12.0, 24, "NA:Subnet in Portland", Portland`
    
    `172.11.13.0, 24, "NA:Subnet in Reno", Reno`
    
    `172.11.14.0, 25, "EMEA:Subnet in Warsaw", Warsaw`
    
    `172.11.15.0, 31, "EMEA:Subnet in Paris", Paris`

2.  Avviare Lync Server Management Shell: fare clic sul pulsante **Start**, scegliere **Tutti i programmi**, **Microsoft Lync Server 2013** e quindi **Lync Server Management Shell**.

3.  Eseguire il cmdlet seguente per importare **subnet.csv** e quindi archiviarne il contenuto nell'archivio di gestione di Lync Server:
    
        import-csv subnet.csv | foreach {New-CsNetworkSubnet $_IPAddress -MaskBits $_.mask -Description $_.description -NetworkSiteID $_.NetworkSiteID}

## Per associare una subnet a un sito di rete utilizzando il Pannello di controllo di Lync Server

1.  Aprire una finestra del browser e quindi immettere l'URL di amministrazione per aprire il Pannello di controllo di Lync Server. Per informazioni dettagliate sui diversi metodi disponibili per avviare il Pannello di controllo di Lync Server, vedere [Aprire gli strumenti di amministrazione di Lync Server](lync-server-2013-open-lync-server-administrative-tools.md).

2.  Sulla barra di spostamento sinistra fare clic su **Configurazione di rete** .

3.  Fare clic sul pulsante di spostamento **Subnet** .

4.  Fare clic su **Nuovo** .

5.  Nella pagina **Nuova subnet** fare clic su **ID subnet** e quindi digitare il primo indirizzo dell'intervallo di indirizzi IP definito dalla subnet che si desidera associare a un sito di rete.

6.  Fare clic su **Maschera** e quindi digitare la maschera di bit da applicare alla subnet.

7.  Fare clic su **ID sito di rete** e quindi selezionare l'ID del sito al quale si desidera aggiungere la subnet.
    

    > [!NOTE]
    > Se non sono stati ancora creati siti di rete, l'elenco sarà vuoto. Per informazioni dettagliate sulla procedura, vedere <A href="lync-server-2013-create-or-modify-a-network-site.md">Creare o modificare un sito di rete in Lync Server 2013</A>. È inoltre possibile recuperare gli ID sito per la distribuzione eseguendo il cmdlet <STRONG>Get-CsNetworkSite</STRONG>. Per informazioni dettagliate, vedere la documentazione di Lync Server Management Shell.



8.  Se si desidera, fare clic su **Descrizione** e quindi digitare ulteriori informazioni per descrivere la subnet.

9.  Fare clic su **Commit** .

Ripetere questi passaggi per aggiungere altre subnet a un sito di rete.

