---
title: Requisiti relativi al routing in base alla posizione per le conferenze
TOCTitle: Requisiti relativi al routing in base alla posizione per le conferenze
ms:assetid: 766d9286-2c34-4faf-bb3e-f0ca478a70cf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Dn362806(v=OCS.15)
ms:contentKeyID: 56269933
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Requisiti relativi al routing in base alla posizione per le conferenze

 

_**Ultima modifica dell'argomento:** 2015-03-09_

Di seguito sono riportati i requisiti necessari per installare e configurare l'applicazione per conferenze con routing in base alla posizione.

  - È necessario distribuire l'aggiornamento cumulativo 2 per Lync Server 2013 in tutti i server e pool della topologia.


> [!NOTE]
> Se in un server o pool di Lync della topologia non è installato l'aggiornamento cumulativo 2 per Lync Server 2013 o versione successiva, l'applicazione del routing in base alla posizione per le riunioni Lync non potrà essere garantita.



  - Il routing in base alla posizione di Lync Server 2013 è un prerequisito dell'applicazione per conferenze con routing in base alla posizione. Per altre informazioni sulla configurazione del routing in base alla posizione di Lync Server 2013, vedere [Configurazione del routing in base alla posizione](lync-server-2013-configuring-location-based-routing.md).

  - I requisiti per l'applicazione per conferenze con routing in base alla posizione sono gli stessi richiesti per il routing in base alla posizione di Lync Server 2013. Per altre informazioni, vedere [Pianificazione del routing in base alla posizione](lync-server-2013-planning-for-location-based-routing.md).

## Server supportati

Per l'applicazione per conferenze con routing in base alla posizione è necessaria la distribuzione dell'aggiornamento cumulativo 2 per Lync Server 2013 in tutti i pool Front End e server Standard Edition presenti nella topologia. Se l'aggiornamento cumulativo 2 per Lync Server 2013 non viene installato in alcuni dei server Lync nella topologia, le restrizioni del routing in base alla posizione non potranno essere applicate alle riunioni Lync e ai trasferimenti di chiamata con consultazione.

Nella tabella seguente è illustrata la combinazione dei ruoli di server e delle versioni che supportano il routing in base alla posizione.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Versione pool Front End</p></td>
<td><p>Versione Mediation Server</p></td>
<td><p>Supportata</p></td>
</tr>
<tr class="even">
<td><p>Aggiornamento cumulativo 2 per Lync Server 2013</p></td>
<td><p>Aggiornamento cumulativo 2 per Lync Server 2013</p></td>
<td><p>Sì</p></td>
</tr>
<tr class="odd">
<td><p>Aggiornamento cumulativo 2 per Lync Server 2013</p></td>
<td><p>Aggiornamento cumulativo 1 per Lync Server 2013</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Aggiornamento cumulativo 2 per Lync Server 2013</p></td>
<td><p>Lync Server 2010</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Aggiornamento cumulativo 2 per Lync Server 2013</p></td>
<td><p>Office Communications Server 2007 R2</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Aggiornamento cumulativo 1 per Lync Server 2013</p></td>
<td><p>Qualsiasi</p></td>
<td><p>No</p></td>
</tr>
<tr class="odd">
<td><p>Lync Server 2010</p></td>
<td><p>Qualsiasi</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Office Communications Server 2007 R2</p></td>
<td><p>Qualsiasi</p></td>
<td><p>No</p></td>
</tr>
</tbody>
</table>


## Client supportati

I client Lync che supportano il routing in base alla posizione per le riunioni Lync sono gli stessi client che supportano il routing in base alla posizione di Lync Server 2013. Per altre informazioni, vedere [Supporto per client e server per il routing in base alla posizione](lync-server-2013-client-and-server-support-for-location-based-routing.md).

## Requisiti del Mediation Server per i trasferimenti di chiamata con consultazione

L'applicazione per conferenze con routing in base alla posizione richiede la distribuzione di Mediation Server autonomi per garantire l'applicazione delle restrizioni del routing in base alla posizione sui trasferimenti di chiamata con consultazione.

Per applicare il routing in base alla posizione dei trasferimenti di chiamata con consultazione, il Mediation Server deve essere associato a un solo peer Mediation Server (ad esempio PBX, gateway SIP e così via) in aree di rete in cui è richiesto il routing in base alla posizione. Se vengono distribuiti peer Mediation Server aggiuntivi nella stessa area di rete, il peer Mediation Server deve essere associato a un Mediation Server diverso. I dettagli di questo requisito sono riportati di seguito.

  - Mediation Server singolo per più peer Mediation Server. Quando un trasferimento di chiamata con consultazione viene instradato a un peer Mediation Server tramite un Mediation Server configurato con più trunk SIP su più peer (ad esempio PBX e gateway), il trasferimento di chiamata con consultazione viene bloccato in modo da impedire il bypass delle chiamate a tariffa PSTN se il trasferimento di chiamata con consultazione è consentito tramite alcuni trunk SIP ma non consentito tramite altri trunk SIP.
    
    Nel caso di un singolo Mediation Server che gestisce un peer Mediation Server di gateway PSTN e un peer Mediation Server di PBX, si osserverà il comportamento seguente:
    
      - Quando un utente di Lync di un determinato sito, ad esempio sito 1, tenta di trasferire una chiamata con un endpoint PSTN a un utente di Lync di un diverso sito, ad esempio sito 2, tramite un trasferimento con consultazione, la chiamata non viene consentita per impedire il bypass delle chiamate a tariffa PSTN.
    
      - Quando un utente di Lync di un determinato sito, ad esempio sito 1, tenta di trasferire una chiamata con un endpoint PBX nello stesso sito (sito 1) a un utente di Lync di un diverso sito, ad esempio sito 2, tramite un trasferimento con consultazione, la chiamata non viene consentita anche qualora non determini il bypass delle chiamate a tariffa PSTN.

  - Mediation Server distinti per peer Mediation Server
    
    Quando un trasferimento con consultazione viene indirizzato a un peer Mediation Server, tale trasferimento verrà valutato in base al peer Mediation Server singolo gestito dal Mediation Server. La chiamata viene o meno consentita in base il suo potenziale di dare luogo a bypass delle chiamate a tariffa PSTN, indipendentemente dalla presenza degli altri peer Mediation Server nel sito, poiché questi ultimi sono gestiti da Mediation Server distinti.
    
    Nel caso di un Mediation Server distinto che gestisce un peer Mediation Server di gateway PSTN e un peer Mediation Server di PBX, si osserverà il comportamento seguente:
    
      - Quando un utente di Lync di un determinato sito, ad esempio sito 1, tenta di trasferire una chiamata con un endpoint PSTN a un utente di Lync di un diverso sito, ad esempio sito 2, tramite un trasferimento con consultazione, la chiamata non viene consentita per impedire il bypass delle chiamate a tariffa PSTN.
    
      - Quando un utente di Lync di un determinato sito, ad esempio sito 1, tenta di trasferire una chiamata con un endpoint PBX nello stesso sito (sito 1) a un utente di Lync di un diverso sito, ad esempio sito 2, tramite un trasferimento con consultazione, la chiamata viene consentita poiché non determina alcun bypass delle chiamate a tariffa PSTN.

## Funzionalità non supportate dall'applicazione per conferenze con routing in base alla posizione

Le seguenti funzionalità non sono supportate dall'applicazione per conferenze con routing in base alla posizione:

  - Conferenza telefonica con accesso esterno. Per la conferenza telefonica con accesso esterno non è possibile applicare il routing in base alla posizione. Qualsiasi richiesta di accesso esterno a una determinata conferenza non verrà limitato dal routing in base alla posizione anche qualora l'organizzatore della conferenza sia un utente Lync abilitato per il routing in base alla posizione.

  - È consigliabile evitare di fornire numeri di accesso per le conferenze telefoniche in aree in cui è necessaria l'applicazione delle restrizioni di routing in base alla posizione.

