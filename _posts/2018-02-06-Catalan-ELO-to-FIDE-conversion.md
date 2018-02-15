---
published: true
title: "ELO català vs ELO FIDE"
date:   2018-02-06 12:38:11 +0100
author_profile: true
mathjax: false
categories:
  - Chess
tags:
  - Ratings
---


# Motivació

Moltes de les fonts d'estudi en el mon dels escacs fan referència a l'ELO FIDE. Una gran majoria de competidors disposen d'una mesura fiable d'ELO català, però no pas d'una mesura fiable d'ELO FIDE, bàsicament degut a que majoritàriament juguen tornejos avaluats mitjançant ELO català.

Realitzem un estudi estadístic per avaluar la relació existent entre l'ELO català i l'ELO FIDE en base a la informació pública disponible a la web de la FIDE i a la de la Federació Catalana d'Escacs. D'aquesta manera aquells jugadors amb un ELO FIDE poc fiable podran disposar d'una referència per avaluar la seva força de joc mitjançant una mesura d'ELO més universal.

## Dades

Creuant la informació de la [FIDE](http://ratings.fide.com) amd la de la [Federació Catalana d'Escacs](http://www.escacs.cat), a data de 01 de Febrer de 2018, obtenim un total de 3.176 jugadors amb ELO FIDE estàndard i ELO Català estàndard.

A continuació es mostra l'histograma de les dades de ELO català estudiades:

![Histograma CAT]({{ site.url }}/assets/2018-02-06-elocat-elofide/hist-elo-cat.png)

Aquestes dades tenen un ELO mig de 1.941 i una desviació estàndard de 203 punts d'ELO català.

A continuació es mostra l'histograma de les dades d'ELO FIDE sobre la mateixa mostra poblacional:

![Histograma FIDE]({{ site.url }}/assets/2018-02-06-elocat-elofide/hist-elo-fide.png)

Aquestes dades tenen un ELO mig de 1.729 i una desviació estàndard de 274 punts d'ELO FIDE.

## Regressió lineal

Visualitzant ELO català vs ELO FIDE es veu una clara correlació lineal. A continuació es mostra el gràfic amb les dades i la regressió lineal obtinguda.

![Regressió lineal]({{ site.url }}/assets/2018-02-06-elocat-elofide/linreg-elo-cat-fide.png)

La relació obtinguda té la forma: **FIDE = -789.13 + 1.298*CAT** i un quoeficient de correlació de 0.96.

## Taula de conversió per les franges de ELO típiques:

Seguint aquesta correlació, a continuació mostrem una sèrie d'equivalències típiques:

| Català | FIDE | Equivalència |
|:----------:|:-------------:|:------|
| 1.685 | 1.400 | Jugador/a aficionat/da |
| 1.840 | 1.600 | Jugador/a de club mig |
| 2.000 | 1.800 | Jugador/a de club fort |
| 2.150 | 2.000 | Homes: Expert nacional / Dones: Women Candidate Master (WCM) |
| 2.225 | 2.100 | Homes: Expert nacional / Dones: Women FIDE Master (WFM) |
| 2.300 | 2.200 | Homes: Candidate Master (CM) / Dones: Women International Master (WIM) |
| 2.380 | 2.300 | Homes: FIDE Master (FM) / Dones: Women Grand Master (WGM) |


