---
title: Луксор - опис решења
---

# Луксор

Аутор: Иван Стошић
Текст и тест примери: Иван Стошић, Лазар Корсић
Анализа решења: Иван Стошић
Тестер: Александар Златески

## Подзадатак 1

Приметимо да је један од бројева $X,Y$ мањи или једнак $\sqrt{A}$, па је довољно извршити претрагу по свим бројевима $X$ до $\sqrt{A}$, где проверавамо да је $Y = \frac{A}{X}$ цео број и да је $X \text{ XOR } Y = B$. Временска сложеност по примеру је $O(\sqrt{A})$.

## Подзадатак 2

Да би се смањио број кандидата за број $X$ приметимо да $X$ мора бити делилац броја $A$. Може се искористити било који брзи алгоритам за факторизацију целих бројева. Један такав алгоритам је *Pollard-Rho* алгоритам, који се најчешће имплементира заједно са *Miller-Rabin* алгоритмом за проверу да ли је број прост. Овај алгоритам има временску сложеност $O(\sqrt[4]{n})$ за налажење једног фактора броја $n$, али има велику скривену константу и из тог разлога није довољно брз.

## Главно решење

Најпре, приметимо да при рачунању XOR вредности и производа два броја, најнижих $n$ битова резултата зависе само од најнижих $n$ битова операнада. Ако посматрамо фиксне вредности $n, a, b$, где је $0 \leq a, b < 2^n$ и $a$ је непарно, показује се да постоји највише $2^{\lfloor\frac{n+3}{2}\rfloor}$ решења једначине

$xy \equiv a \mod 2^n, x \text{ XOR } y = b$,

где су $x,y$ непознате, такође бројеви из скупа $[0, 2^n)$. Из тог разлога, ако фиксирамо најнижих $n$ битова броја $X$, оваквих валидних парцијалних решења неће бити више од $2^{\lfloor\frac{n+3}{2}\rfloor}$. Ова парцијална решења можемо генерисати рекурзивно. У $n$ том нивоу рекурзије имамо не више од $2^{\lfloor\frac{n+3}{2}\rfloor}$ позива. Довољно је пронаћи само првих $31$ битова броја $X$, јер је због услова $XY=A$ бар један од бројева $X,Y$ мањи или једнак $A$, а увек можемо да претпоставимо да је то број $X$. Сумирањем по $n$ добијамо да има $O(\sqrt[4]{A})$ рекурзивних позива, па је управо ово временска сложеност решавања једног тест примера.
