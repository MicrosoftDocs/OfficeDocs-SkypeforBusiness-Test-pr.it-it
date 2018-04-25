---
title: 'Lync Server 2013: Query del database QoE di esempio'
TOCTitle: Query del database QoE di esempio
ms:assetid: 04e6bdd3-bbd1-47ca-8114-94a3db6beeeb
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398100(v=OCS.15)
ms:contentKeyID: 49299541
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Query del database QoE di esempio in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-17_

In questa sezione sono incluse query di esempio per il database della qualità percepita dagli utenti (QoE).

Utilizzare l'esempio seguente per ottenere l'instabilità e la perdita di pacchetti medie per tutti i flussi audio.

    select avg(cast(JitterInterArrival as bigint)) as JitterAvg, avg(PacketLossRate) as PacketLossRateAvg from AudioStream

Utilizzare l'esempio seguente per trovare i totali relativi alle conferenze per cui è stata utilizzata la console per riunioni.

    select avg(ConversationalMOS)
    from SessionView s
    inner join MediaLineView m
    on s.ConferenceDateTime = m.ConferenceDateTime
       and s.SessionSeq = m.SessionSeq
       and m.MediaLineLabel = 0 -- audio media line
       and s.CallerUserAgentType = 4 -- Lync
       and s.CalleeUserAgentType = 4 -- Lync

Utilizzare l'esempio seguente per ottenere ConversstionalMOS, SendingMOS e ListendingMOS per dispositivo di acquisizione.

    select t.DeviceName as Device, count(*) as SampleNum, avg(ConversationalMOS) as ConversationalMOS, avg(SendListenMOS) SendingMOS, avg(RecvListenMOS) as ListendingMOS
    from
    (
       select m.CallerCaptureDev as DeviceName, m.ConferenceDateTime, m.SessionSeq, a.StreamID, m.ConversationalMOS,a.SendListenMOS, a.RecvListenMOS
       from MediaLineView m
       inner join AudioStream a
       on m.ConferenceDateTime = a.ConferenceDateTime
          and m.SessionSeq = a.SessionSeq
          and m.MediaLineLabel = 0
    
       union
    
       select m.CalleeCaptureDev as DeviceName, m.ConferenceDateTime, m.SessionSeq, a.StreamID, m.ConversationalMOS,a.SendListenMOS, a.RecvListenMOS
       from MediaLineView m
       inner join AudioStream a
       on m.ConferenceDateTime = a.ConferenceDateTime
          and m.SessionSeq = a.SessionSeq
          and m.MediaLineLabel = 0
    
    )as t
    group by t.DeviceName
    order by SampleNum desc

