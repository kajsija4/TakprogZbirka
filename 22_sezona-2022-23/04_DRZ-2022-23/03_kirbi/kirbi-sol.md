---
title: Кирби - опис решења
---

## Кирби

Аутор: Марко Миленковић 

Текст: и тест примери: Марко Миленковић

Анализа решења: Марко Миленковић

Тестирање: Димитрије Ердељан

###  $1 \leq N,M,P \leq 5$
У овом подзадатку користимо то да су све вредности мале бројке. Можемо избрисати свако прљаво поље и затим испробати све путање да видимо која садржи највећи број упрљаних поља и да ли се то разликује од почетног максималног броја поља које Кирби може да очисти. Временска сложеност је $O(TP2^{N+M})$.
###  $N = 2$ или $M = 2$
Посматраћемо случај $N=2$, јер се други случај аналогно решава. Приметимо да ће се Кирби тачно једном спустити у други ред. Памтимо префиксни низ прљвих поља за први ред и памтимо суфиксни низ прљавих поља за други ред. Максималан број поља које Кирби може да очисти је $S = \max_{1 \leq i \leq M}\{pref_i + suf_i\}$. Нека је $i_{min}$ прва колона у којој израз $pref_{i_{min}} + suf_{i_{min}}$ достиже вредност $S$ и нека је $i_{max}$ последња колона у којој израз $pref_{i_{max}} + suf_{i_{max}}$ достиже вредност $S$. Тражено решење је $pref_{i_{min}} + suf_{i_{max}}$. Временска сложеност је $O(T(P+M))$.
### $1 \leq N,M,P \leq 100$
Нека је $S$ поново максималан број поља које Кирби може да очисти у старту. То можемо израчунати стандардним динамичким програмирањем. Стање $dp_{i,j}$ представља максималан број поља које Кирби може да очисти крећући са поља $(1,1)$ до поља $(i,j)$. Кренемо "редом" да обилазимо матрицу по редовима, па по колонама (као у улазу) и вршимо прелаз $dp_{i,j} = \max(dp_{i-1,j}, dp_{i,j-1}) + a_{i,j}$, где је $a_{i,j}$ бинарни индикатор да ли је поље $(i,j)$ урљано ($1$ ако јесте, $0$ ако није). Сада можемо да избацујемо једно по једно упрљано поље и рачунамо изнова целу $dp$ матрицу и видимо када је вредност $dp_{N,M} < S$. Временска сложеност $O(TPNM)$.   
### Решење без додатних ограничења
Можемо приметити да када посматрамо редом поља која је Кирби очистио, њихове колоне формирају неопадајући низ. Односно, уколико сортирамо упрљана поља по редовима, максималан број поља која Кирби може да очисти је најдужи неопадајући подниз колона овог низа. Дати проблем је еквивалентан налажењу најдужег растућег подниза (\emph{Longest increasing subsequence}, или скраћено LIS), што је познат проблем и може се решити/имплементирати у временској сложености $O(P\log P)$. Оно што нама треба јесу префиксни и суфиксни LIS низови. Формално, $pref_i$ представља $LIS$ од почетка низа до $i$-тог елемента, али тако да он засигурно фигурише у $LIS$-у. Слично, $suf_i$ представља $LIS$ низа од $i$-тог елемента до краја низа, тако да $i$-ти елемент учествује у $LIS$-у. За $i$-ти елемент низа упрљаних поља важи да је део неког од путања које садрже највећи број упрљаних поља ако и само ако је $pref_i + suf_i - 1 = S$. Са друге стране, елемент низа припада свим таквим путањама ако и само ако додатно важи и да је вредност $pref_i$ јединствена међу свим префиксним $LIS$-овима. Потребно је само исписати број таквих поља. Временска сложеност је $O(TP\log P)$. 
