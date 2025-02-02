---
title: Концерт - опис решења
---

# Концерт

Аутор: Никола Милосављевић
Текст и тест примери: Никола Милосављевић
Анализа решења: Никола Милосављевић
Тестирање: Игор Павловић

Како није дозвољено понављање поља на путу, у сваком реду се иде само у једном смеру (улево или удесно) или директно на горе. Промена стрктуре реда гурањем не утиче на даљи део пута јер није дозвољено враћање уназад.

У **Подзадатку 1** је довољно користити класично динамичко програмирање за рачунање броја одговарајућих путева у $O(nm)$ или применити мало комбинаторике: за сваки од $n$ редова можемо на $m$ начина изабрати поље у које долазимо из претходног реда (за последњи ред, то је поље из кога почињемо) а након тога је пут јединствено одређен. Дакле, одговор је $m^n$ mod $(10^9 + 7)$. За **Подзадатак 2** је довољно испробати све могуће путеве, наједноставније користећи рекурзију/бектрек у сложености $O(m\cdot m^n)$.

Задатак је најприродније решавати **динамичким програмирањем**. Дефинишимо $d[i][j] =$ број (валидних) путева који се завршавају у пољу $(i,j)$ дате матрице $a$ при чему је последњи потез "нагоре". Коначно решење је $\sum_{1 \leq j \leq m, \  a[1][j]=0} d[1][j]$ а почетне вредности су $d[n][j] = a[n][j]$ за $j=1,2,\ldots,m$. Рекурентна веза је дата са $d[i][j] =\sum_x d[i+1][x]$, где се сумирање врши по свим индексима $x$ таквих да је (гурањем) у $(i+1)$-ом реду могуће доћи од позиције $x$ (која треба бити празно поље) до позиције $j$ (која не мора нужно бити празно поље). Најједноставнији начин је испитати сваку позицију $x$ из $(i+1)$-ог реда; ако је $x_L$ позиција $(k+1)$-ве особе лево  у односу на позицију $x$ а $x_R$ позиција $(k+1)$-ве особе десно  у односу на позицију $x$, тада, са позиције $x$ можемо гурањем доћи до било које које (и само те) позиције из сегмента $[x_L+(k+1), x_R-k]$. Вредности $x_L$ и $x_R$ за свако $x$ можемо одредити у свега два пролаза кроз $(i+1)$-ви ред (слева удесно и сдесна улево) нпр. убацивајући позиције јединица на које наиђемо у неки помоћни вектор. Ово даје решење сложености $O(nm^2)$ што је довољно за **Подзадатак 4**.

У **Подзадатку 3** нема гурања па се рекурентна веза може упростити увођењем помоћних матрица, нпр. $L[i][j]=$ број путева који се завршавају у пољу $(i,j)$ при чему је последњи потез "улево" и аналогно за $R[i][j]$ и "удесно". Сада се све ове матрице могу паралено израчунати, $d[i][j] = d[i+1][j]+L[i+1][j]+R[i+1][j]$, $L[i][j] = L[i][j+1]+d[i][j+1]$, $R[i][j] = R[i][j-1]+d[i][j-1]$ (у одговарајућем редоследу i проверу заузетости поља). То је $O(1)$ по пољу тј. $O(nm)$ укупно.

За коначно решење, треба убрзати $O(nm^2)$ алгоритам. Из тог решења, знамо да ће за свако поље $(i+1,x)$, вредност $d[i+1][x]$ учествовати у формули за рачунање вредности $d[i][j]$ за свако $j\in[x_L+(k+1),x_R-k]$ (уз проверу $d[i][j]=0$ и границе за сегмент). Зато можемо, након обраде $(i+1)$-ог реда, за свако $x$ повећати све $d[i][j]$ из реда изнад који су у одговарајућем сегменту за $d[i+1][x]$. Наравно, директна имплементација овога не би смањила сложеност али можемо користити познати трик; довољно је додати елементу на почетку сегмента $+d[i+1][x]$ и додати елементу након краја сегмента $-d[i+1][x]$ (за свако $x$) и на крају ће тражене вредности у новом реду бити префиксне суме тренутних вредности. Ово даје алгоритам сложености $O(nm)$.

Алтернативно (и нешто једноставније решење) је дефинисати $d[i][j]=$број путева који *почињу* из поља $(i,j)$. Тада вредности можемо рачунати одозго надоле и, на основу претходне дискусије, важи $d[i][j] = \sum_{j_L + k + 1 \leq x \leq j_R - k} d[i-1][x]$, где се вредности $j_L$ и $j_R$ односе на тренутни, $i$-ти ред. Користећи префиксне суме, претходну суму можемо израчунати у $O(1)$ (прецизније, један ред матрице $d$ рачунамо у $O(m)$) па добијамо алгоритам сложености $O(nm)$.





