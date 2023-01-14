# Алгоритмы решения заданий ЕГЭ


## 1 задание 













## 2 задание  

**Алгоритм решения 2 задания состоит всего из 2 шагов**:

❶ — перебираем все возможные комбинации из 0 и 1,  и подставляем вместо `x`, `y`, `z` и `w` в логическую функцию

❷ — выводим те значения `x`, `y`, `z`, `w`, при которых функция давала нужный результат (1 или 0)


**Общий каркас**:
```python

❶ for x in ... :
      for y in ... :
          for z in ... :
              for w in ... :
  
❷                 if ( ... ) == ... :
                      print(x, y, z, w)

```


**Реализация алгоритма**: 

❶ — перебор всегда осуществляется при помощи `for`;<a id="anchor1"></a>

все возможные подстановки 1 и 0 в `x`, `y`, `z` и `w` делаются через вложенные циклы `for`:

```python

for x in 1,0:
    for y in 1,0:
        for z in 1,0:
            for w in 1,0:
                print(x, y, z, w)
```

Если запустить данный код, получим все 16 комбинаций из 1 и 0:

<details><summary>Выглядеть будет так:</summary>

```
1 1 1 1
1 1 1 0
1 1 0 1
1 1 0 0
1 0 1 1
1 0 1 0
1 0 0 1
1 0 0 0
0 1 1 1
0 1 1 0
0 1 0 1
0 1 0 0
0 0 1 1
0 0 1 0
0 0 0 1
0 0 0 0
```

</details>
<br></br>



❷ — прямо так и пишем: "если функция такая ..., то выведи `x`, `y`, `z`, `w`"

```python

if ((y <= z) and (not((y or w) <= (z and x)))) == 1:
    print(x, y, z, w)
```


Конечно же, логическую функцию нужно переписать с учётом синтаксиса Python:

в заданиях | в Python
--- | ---
$\lor$ или $\mid$ | `or`
$\land$ или &amp; | `and`
$\to$ | `<=`
$\equiv$ | `==`
$\neg$ | `(not ... )`

Важно: заменяя $\neg$, мы пишем `not` и берём в `()` вместе с тем, к чему `not` относится. 

<details><summary>Примеры:</summary>

в задании | $(x ∨ y) ∧ ¬(y ≡ z) ∧ ¬w$
--- | ---
в Python | `(x or y) and (not(y == z)) and (not w)`

в задании | $(x → y) ∧ (y ≡ ¬z) ∧ (z ∨ w)$
--- | ---
в Python | `(x <= y) and (y == (not z)) and (z or w)`

в задании | $(¬(z ≡ w) → (w ∧ ¬x)) ∨ (x ∧ ¬y)$
--- | ---
в Python | `((not (z == w)) <= (w and (not x))) or (x and (not y))`
</details>
<br></br>










## 3 задание  













## 4 задание  













## 5 задание  













## 6 задание  













## 7 задание  













## 8 задание  













## 9 задание  













## 10 задание  













## 11 задание  













## 12 задание  













## 13 задание  













## 14 задание  

**1 тип — выражение из чисел в разных системах счисления**

Дано выражение наподобие $y04x5_{11} + 253xy_{8}$.
Нужно найти, например, при каких `x` и `y` оно делится на 99 без остатка, и вывести, что получится при таком делении. 

Алгоритм решения: 

❶ — подставляем на место `x` и `y` все возможные варианты

❷ — собираем наши числа и переводим их в 10 СС

❸ — проверяем, выполняется ли условие и выводим ответ



❶ — Все возможные варианты из нескольких чисел всегда делаются при помощи вложенных циклов `for`, как [тут](#anchor1).
Перебор всегда связан с циклом `for`.

Получаем:

```python
for x in ... :
    for y in ... :
```       

Теперь, какой набор мы используем в `for`.
Логика проста: в обоих наших числах есть x и y, а наши числа из какой-то системы счисления. 
Любая система счисления имеет самую большую возможную цифру (гениально), выше неё цифры использовать в этой СС нельзя. 

К примеру, числа $231_2$ не существует, как и $201_2$. Просто потому, что 2-ичная СС состоит только из цифр 1, 0.

Вернёмся к нашему примеру $y04x5_{11} + 253xy_{8}$. 
Глянем на 1 число, в нём `x`, `y` могут быть только от 0 до 10 включительно. 
Смотрим на 2 число, здесь `x` и `y` могут быть только от 0 до 7 включительно. 
Какой вывод? — Мы можем брать `x` и `y` только от 0 до 7.

Так и пишем:

```python
for x in "01234567" :
    for y in "01234567" :
```   




❷ — процесс сборки и перевода числа выглядит так; тут мы используем 2 аргумент `int(..., )`; он нужен, когда мы переводим не 10-ичный объект:

<!-- <span class="math-tex">\(2x84x_{19}\)</span>&nbsp;<span class="math-tex">\(\xrightarrow{❶}\)</span> <code>&quot;2&quot; + x + &quot;84&quot; + x</code>&nbsp;<span class="math-tex">\(\xrightarrow{❷}\)</span>&nbsp;<code><span style="color:#cc0000">int(</span>&quot;2&quot; + x + &quot;84&quot; + x<span style="color:#cc0000">)</span></code>&nbsp;<span class="math-tex">\(\xrightarrow{❸}\)</span>&nbsp;<code>int(&quot;2&quot; + x + 84 + x<span style="color:#cc0000">, 19</span>)</code> -->

$2x84x_{19}$ $\xrightarrow{1}$ `"2" + x + "84" + x` $\xrightarrow{2}$ `int("2" + x + "84" + x)` $\xrightarrow{3}$ `int("2" + x + 84 + x, 19)`

- 1 — склеиваем отдельные строки

- 2 — преобразуем это в число — `int()`

- 3 — так как преобразуем в число не десятичные символы, то указываем второй аргумент в `int()` — основание системы 









<hr size="6" width="90%" align="center" color="gray">



**2 тип**

14 задания этого типа выглядят так: 

- дано выражение наподобие $125 + 25^3 + 5^9$

- нужно найти, сколько в нём каких-то цифр, если это выражение перевести в другую СС

Идея решения задания очень проста — для начала рассмотрим число $123_{10}$:
$$123_{10} = 1 \cdot 10^2 + 2 \cdot 10^1 + 3 \cdot 10^0$$

Основание этого числа и степени $10$ в его разложении связаны самым прямым образом. 
И если бы это число было в другой СС, оно бы раскладывалось не на степени 10, а на степени своего нового основания: 
$$123_{7} = 1 \cdot 7^2 + 2 \cdot 7^1 + 3 \cdot 7^0$$
$$123_{9} = 1 \cdot 9^2 + 2 \cdot 9^1 + 3 \cdot 9^0$$

Теперь, как взять из числа самую последнюю его цифру?
Помнишь, для этого мы делали `число % 10`. 
Тут число 10 только тогда, когда число 10-тичное.
Если число будет из другой СС, то и вместо 10 будет другое число. 

Например, чтобы взять последнюю цифру из числа $123_7$ мы сделаем так: `123 % 7`. 

Ок, последнюю цифру мы взяли, а как взять предпоследнюю?

Идея проста — возьмём и обрежем наше число на 1 последнюю цифру. 
Как мы обрезали число?
Делили нацело на 10:
```python
число // 10
```
Здесь тоже 10 только если число в 10-тичной СС. А если число будет из другой СС, то и делить нацело будем его на другое число:
```python
число // 7  # если число в 7-ричной СС
```

```python
число // 5  # если число в 5-ричной СС
```

В итоге, 2 основных действия (вместо 10 всегда пишем основание системы, в которую переводим число): 
1. берём последнюю цифру числа:
```python
число % 10
```

2. обрезаем число:
```python
число = число // 10
```
будем писать это короче, как пишем `+=`:
```python
число //= 10
```

Эти действия повторяются до тех пор, пока число не стало из 1 символа. 
Так и пишем:
```python
while число > 0:
    ...
```

Общая схема кода выглядит так: 
```python
❶ число = 125 + 25**3 + 5**9
  
❷ while число > 0:
❸     if число % ... == ... :
          счёт += 1 
      
❹     число //= ...
  
❺ print(счёт)    
```

- ❶ — создаём число (просто переписываем из условия)

- ❷ — действия продолжаются, пока мы совсем не укоротили наше число

- ❸ — извлекаем последнюю цифру числа при помощи `%`;
если последняя цифра — нужная нам, увеличиваем какую-нибудь переменную (`счёт`) на 1 

- ❹ — обрезаем наше число, чтобы предпоследнюю цифру тоже можно было взять через `%`; 
это делаем в любом случае, даже если цифра нам не подошла, поэтому без отступа, не внутри `if`

- ❺ — в самом конце, когда мы прошлись по всем цифрам `числа` выводим, сколько нужных цифр мы насчитали 










## 15 задание  













## 16 задание  













## 17 задание  

В этом задании мы работаем с файлами, нам нужно их открывать$^❶$ и прочитывать$^❷$. 

❶ Открытие файла происходит так: 
```python 
file = open("...")
```
`file` — это переменная, куда сохраняем результат открытия файла; разумеется, её можно назвать, как угодно. 
Внутри `open("...")` в кавычках пишем полное название файла с расширением, например `open("17.txt")`.

<!-- Строго говоря, тут нужно писать полный путь к файлу; можно обойтись только названием, когда файл лежит в одной папке с программой. -->

Одного открытия недостаточно, необходимо файл ещё и прочитать. 


❷ Прочитываем файл при помощи метода `.readlines()` (очень логично, *read* - читаем, *lines* - потому что читаем все строки, а не одну только)

Это метод, не забываем, как грамотно применять методы к строке:
```python 
file = file.readlines()
```












## 18 задание  













## 19 задание  













## 20 задание  













## 21 задание  













## 22 задание  













## 23 задание  













## 24 задание  













## 25 задание  













## 26 задание  













## 27 задание  













# Основное, что нужно знать в Python:

#### Ввод - вывод
- команда ввода `input()`
	- по умолчанию вводит всё как текст, если хотим число — нужно преобразовать
- вывод — `print()`


<br></br>
#### Типы данных <a id="anchor3"></a>
- числа 
	- целые — `int()`   
	- не целые — `float()` 
- текст, строки — `str()` 
- списки — `list()`
- логический тип — `bool()`

Тип определяет операции, которые можно делать с объектом. 
Строки нельзя делить, например. 


<br></br>
#### Условие if
- в конце строки с `if` всегда `:`
- действия, которые выполняются, только если ... — всегда с отступом после строки с `if`

```python

if <условие> :
    <действие>

```

"если" — это `if`, "а если не так" — это `else`:
```python

if число % 2 == 0:
    print("чётное")
else:
    print("нечётное")

```


- В том случае, когда "а если не так" — подразумевает несколько вариантов, выбираем конкретный при помощи `elif`.
Например, условие "число делится на 3". И если мы захотим проверить, делится ли число на 2, мы пишем не `else`, а `elif`, потому что делимость на 2 — не противоположное условие к делимости на 3. 


**Итог**: если 2 противоположных результата — `if` и `else`, если есть результат и много других — `if` и `elif`.





<br></br>
#### Цикл for

```python
for <x> in <набор> :
    <действия>
```

- в конце строки с `for` всегда `:`

- цикл `for` позволяет повторить `<действия>` сколько-то раз; количество повторов определяется длиной `<набора>` 

- в качестве `<набора>` может быть любой объект, у которого можно извлечь отдельные элементы


Примеры наборов, которые состоят из одинакового количества элементов, поэтому дадут *одинаковое количество повторов* в цикле `for`:

```python
1, 2, 3

"1", 5//2, 6.0

"a", "b", "c"

"abc"

range(3)

range(0, 3)
```


<br></br>
Полезная штука — **генератор списка**:
```python

[ <выражение> for <x> in <набор> ]
```

`<выражение>` определяет, что будет помещено в список `[]`; 
`<выражение>` выполняется для всех `<x>` в `<наборе>`


Пару примеров:
создание | результат
--- | ---
`[int(x) for x in str(123)]` | `[1, 2, 3]`
`[ 0 for x in range(2) ]` | `[0, 0]`
`[ x**0.5 for x in [4, 9, 16] ]` | `[2.0, 3.0, 4.0]`





<br></br>
#### Строки и их методы 

- строки можно складывать друг с другом: 

```python
print("a" + "b")
```
> `ab`

- строку можно умножать на целое число, при этом происходит дублирование строки:
```python
print("a" * 3)
```
> `aaa`

тот же результат можно было получить так: `print("a" + "a" + "a")`

**Основные методы строк:**

- `.find()`

- `.count()`

- `.split()`

- `.replace()`

Важно: методы к строкам мы применяем именно так: 
```python
строка = строка.метод()
```
Всё потому, что строка — неизменяемый тип. 
Применяя к ней метод, мы работаем уже не со строкой (её невозможно изменить), а с её копией, а исходная строка в процессе никак не меняется. 
Чтобы её изменить, мы перезаписываем в переменную вместо строки её изменённую копию. 


$\color{#B0E0E6}{\text{красное слово}}$







<br></br>
#### Списки и их методы




















<br></br>
<br></br>
<br></br>
<br></br>
<br></br>
<br></br>
<br></br>
<br></br>
<br></br>
