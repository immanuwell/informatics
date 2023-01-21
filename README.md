# Алгоритмы решения заданий ЕГЭ


## 1 задание 












<br></br>
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










<br></br>
## 3 задание  












<br></br>
## 4 задание  












<br></br>
## 5 задание  

Есть 2 основных типа 5 заданий, вот общая структура кода для каждого типа: 

**1 тип — обработка двоичной записи числа**
```python
❶ for N in range(...):
❷   N2 = bin(N)[2:]
  
❸   ...
  
❹   if ... :
      A.append()
  
❺ print(...)
```
- ❶ — берём число из какого-то диапазона, обычно `range(0, 1000)`. 
Если программа не найдёт подходящие числа в этом диапазоне, просто берём чуть больше, например `range(0, 10000)`.
Иногда диапазон указан в условии явно. 

- ❷ — создаём двоичную запись числа `N`; для этого используем `bin()`.
`bin()` создаёт двоичную запись типа `str()`, но с 2 ненужными первыми символами, поэтому берём срез со 2 элемента по конец `[2:]`.

- ❸ — какие-то преобразования двоичной записи; например, добавляем какие-то символы в конец, а какие-то в начало. 
Часто тут есть условие — значит используем `if` и `else`.

- ❹ — после преобразования двоичной записи проверяем результат. Результат обычно в 10-тичной СС, для перевода в неё используем `int(..., 2)`.
Если результат такой, какой нужно, сохраняем его — добавляем в список, например, `A`.

- ❺ — выводим итоговый ответ. 
Если нам необходимо найти наименьшее подходящее число, используем `min(A)`, наибольшее — `max(A)`.




<br></br>
**2 тип — работа с 10-тичным числом**

```python
❶ for N in range(...):
❷   A = [int(x) for x in str(N)]
  
❸   ...
  
❹   if ... :
      print(N)
      break
```

- ❶ — берём `N` из диапазона; диапазон обычно явно задаётся в условии.
Например, если сказано "все трёхзначные" — это `range(100, 1000)`

- ❷ — раскладываем число на список его цифр: `123` $\to$ `[1, 2, 3]`.
Для чего? Чтобы было удобно делать математические операции с отдельными цифрами. 

- ❸ — какие-то действия с цифрами.
Например, умножаем 1 и 2 цифры, 2 и 3 цифры и составляем новое число из этих произведений в порядке убывания. 

- ❹ — проверяем полученный результат, если это то, что нужно, выводим. 
Обычно нам нужно найти наименьшее, поэтому, после вывода числа можно выйти из цикла при помощи `break`.












<br></br>
## 6 задание  












<br></br>
## 7 задание  













<br></br>
## 8 задание  
В этом задании составляются слова известной длины из набора каких-то символов. 
Нам необходимо найти из этих слов подходящие, или узнать номер нужно слова или что-то подобное. 

Алгоритм здесь крайне простой: 

❶ — собираем слова из букв;
по сути, генерируем все возможные комбинации из букв данного набора — разумеется, это происходит при помощи вложенных циклов `for` (подробнее про `for` [тут](#anchor5))

Количество вложенных циклов `for` равно количеству букв в слове (1 цикл подставляет по очереди буквы на 1 позицию в слове)


набор, который помещаем в цикле `for`, составляем из уникальных букв (берём каждую по одной)

❷ — добавляем проверку условий. Для этого либо изменяем наборы в циклах `for`, либо пишем внутри циклов условие `if`


**Общая структура кода:** 

```python
❶ for a in "..." :
    for b in "...":
        for c in "...":
            ... 
❷             if () :
                  счёт += 1 
  
❸ print(счёт)
```
- ❶ — подставляем все возможные варианты на каждую позицию в слове; 
сколько букв в слове — столько и вложенных циклов `for`

- ❷ — при помощи `if` считаем, сколько слов подходит под условие; 
когда слово подходит, увеличиваем переменную `счёт` на 1 — так мы считаем 

- ❸ — выводим количество подходящих слов

<details><summary>Пару примеров</summary>

> Сколько слов длины 4, начинающихся с согласной буквы и заканчивающихся гласной буквой, можно составить из букв М, Е, Т, Р, О? Каждая буква может входить в слово несколько раз.

```python
счёт = 0

for a in "МТР":
  for b in "МЕТРО":
    for c in "МЕТРО":
      for d in "ЕО":

        счёт += 1 

print(счёт)
```


> Шифр замка — это последовательность из пяти символов, каждый из которых является цифрой от 1 до 5. Сколько различных вариантов шифра можно задать, если известно, что цифра 1 встречается ровно три раза?

```python
счёт = 0

for a in "12345":
  for b in "12345":
    for c in "12345":
      for d in "12345":
        for e in "12345":

          word = a + b + c + d + e
          if word.count("1") == 3:
            счёт += 1

print(счёт)
```


</details>
<br></br>












<br></br>
## 9 задание  












<br></br>
## 10 задание  












<br></br>
## 11 задание  












<br></br>
## 12 задание  


**Общая структура кода для решения такая:** 
```python
❶ for x in range(...):
    for y in range(...):
      for z in range(...):
  
❷       a = ... + "..."*x + "..."*y + "..."*z + ...
❸       a0 = a
  
❹       while "..." in a:
❺         a = a.replace("...", "...", 1)
          ...
        
❻       if ... :
          print(...)
```

❶ — эти вложенные циклы появляются, когда в строке `a` есть неизвестное количество каких-то символов;
1 цикл отвечает за количество конкретного символа в строке `a`. 

❷ — собираем исходную строку `a` из разных символов по условию. 
Например, `a` начинается и заканчивается `"0"` и в ней сколько-то символов `"1"`:
```python
a = "0" + "1"*x + "0"
```
`x` — это переменная из цикла, она будет отвечать за количество символов `"1"` в строке `a`.

❸ — копируем исходную строку `a` в какую-нибудь переменную (например, в `a0`), если нужно

❹ — дальше полностью переписываем программу из условия на язык Python, например:
`ПОКА НЕ нашлось (00)`
```python
while "00" not in a:
```

`заменить (01, 210)`
```python
a = a.replace("02", "320", 1)
```









<br></br>
## 13 задание  















<br></br>
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









<br></br>
## 15 задание  















<br></br>
## 16 задание  
Так мы делаем 16 задание

![](https://ucarecdn.com/2881b304-637f-456c-a612-64ae44a78776/16_задание_списки_теория_1.png)


![](https://ucarecdn.com/229d7bf4-2964-4ae9-bf06-5a1a9e444d06/16_задание_списки_теория_2.png)


"С номерами 3 и больше" — значит, используем `range(3, ...)`, где на месте многоточия ставим номер последнего интересующего нас элемента + 1

Значения из `range(3, ...)` мы будем записывать в `n`, то есть `n` будет меняться от 3 и до того, что нам нужно 

Чтобы `n` постоянно перезаписывалась, помещаем всё это в цикл `for`

На данный момент имеем:
```python
for n in range(3, ...):
```

"вписываем значения" — значит, используем метод добавления в конец списка — `F.append()`

Вписываем мы в конец то, что вычисляется по формуле F(n-1) * n ; помним, что F(n-1) хранится в нашем списке `F` на месте `n-1` то есть тут — `F[n-1]`

Получается так: `F.append( F[n-1] * n )`

В итоге имеем такую полную программу:
```python
F = [0, 1, 3]
for n in range(3, ...):
    F.append(F[n-1] * n)
```

И теперь, если в задании нам необходимо найти значение функции F(120), мы просто в конце пишем `print(F[120])`

При этом не забываем, что тогда 2 аргумент в `range()` должен быть на 1 больше — `range(3, 121)`














<br></br>
## 17 задание  

В этом задании мы работаем с файлами, нам нужно их открывать $^❶$ и прочитывать $^❷$. 

❶ Открытие файла происходит так: 
```python 
file = open("...")
```
`file` — это переменная, куда сохраняем результат открытия файла; разумеется, её можно назвать, как угодно. 
Внутри `open("...")` в кавычках пишем полное название файла с расширением, например `open("17.txt")`.

<!-- Строго говоря, тут нужно писать полный путь к файлу; можно обойтись только названием, когда файл лежит в одной папке с программой. -->

Одного открытия недостаточно, необходимо файл ещё и прочитать. 


❷ Прочитываем файл при помощи метода `.readlines()` (очень логично, *read* - читаем, *lines* - потому что читаем все строки, а не одну только)

Это метод, не забываем, [как](#anchor4) грамотно применять методы к строке:
```python 
file = file.readlines()
```


На данный момент имеем 2 строки кода:
```python
file = open("17.txt")
file = file.readlines()

print(file)
```
получим примерно: 
> `["12\n", "9\n", "8\n"]`

Разумеется, необходимо это преобразовать в вид `[12, 9, 8]`

Проще всего это сделать при помощи генератора:
```python
[int(x) for x in file]
```

`file` — полученный нами список при помощи `open()` и `.readlines()`












<br></br>
## 18 задание  












<br></br>
## 19 задание  












<br></br>
## 20 задание  












<br></br>
## 21 задание  












<br></br>
## 22 задание  












<br></br>
## 23 задание  












<br></br>
## 24 задание  












<br></br>
## 25 задание  












<br></br>
## 26 задание  












<br></br>
## 27 задание  












<br></br>
<br></br>
<br></br>
<br></br>
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
#### Цикл for <a id="anchor5"></a>

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
аргумент — символ, номер которого в строке ищем

- `.count()`
аргумент — символ, количество которых ищем 

- `.split()`
аргумент — символ, по которому делится исходная строка и записывается в список; если аргумент не пишем, по умолчанию делится по пробелам

    <details><summary>пример</summary>

    ```python
    A = "a b c".split()
    print(A)
    ```
    > `["a", "b", "c"]`

    </details>

- `.replace()`
1 аргумент — что берём, 2 аргумент — на что заменяем (ещё есть 3 аргумент — сколько найденных элементов заменяем)

**Важно:** методы к строкам мы применяем именно так: <a id="anchor4"></a>

```python
строка = строка.метод()
```
Всё потому, что строка — неизменяемый тип. 
Применяя к ней метод, мы работаем уже не со строкой (её невозможно изменить), а с её копией; исходная строка в процессе никак не меняется. 
Чтобы её изменить, мы перезаписываем в переменную `строка` вместо строки её изменённую копию. 

По этой же причине невозможно изменить элемент строки:
```python
s = "abc"
s[0] = "b"
```
> ошибка 






<br></br>
#### Списки и их методы

Списки можно складывать и умножать на целое число:
```python
print([1] + [2])
```
> `[1, 2]`

```python
print(["a"] * 3)
```
> `["a", "a", "a"]`

Можно брать отдельные элементы списка и срезы

**Методы списков:** 
- `.append()` 
добавляет элемент в конец списка

- `.count()`
считаем, сколько есть таких элементов в списке

- `.sort()`
расставляет элементы списка по возрастанию; причём работает не только со списками из чисел, но и с текстовыми списками, поскольку все буквы тоже имеют свой номер


Список — это изменяемый тип данных. 
Когда мы применяем метод к списку, то меняется сам список. 
Поэтому применение метода к списку выглядит так ([сравни со строками](#anchor4)): 
```python
список.метод()
```

















<br></br>
<br></br>
<br></br>
<br></br>
<br></br>
<br></br>
<br></br>
<br></br>
<br></br>

# Ошибки Python и что они означают

- `invalid syntax`

Что означает? | Ошибка синтаксиса — где-то пропущен или стоит не в том месте `:` или `,` или `()` или ещё другой похожий символ
--- | ---
Как исправить? | Часто нужно поставить `:` в конце строки с `if` или `for`, добавить парную скобку `()`, поставить `,` где мы перечисляем разные элементы, например, в `print()`
Где может быть? | Везде


<br></br>
- `unexpected indent`

Что означает? | Неожиданный отступ — отступ без какой-либо причины
--- | ---
Как исправить? | Просто убрать этот отступ
Где может быть? | Везде


<br></br>
- `index out of range`

Что означает? | Выход за пределы набора — мы пытаемся взять из набора элемент под слишком большим номером
--- | ---
Как исправить? | Поменять 2 аргумент в `range()` на такое число, каким может быть номер последнего элемента в наборе (в строке, списке и т.д.)
Где может быть? | Везде, где работаем с наборами (строками, списками и т.д.) при помощи функции `range()` и цикла `for`


<br></br>
- `unsupported operand type(s)...`

Что означает? | Неподдерживаемая операция — мы пытаемся делать с объектом что-то невозможное, например, складываем строку с числом
--- | ---
Как исправить? | Если операция должна быть именно такая, нужно преобразовать всё, к чему она применяется, в один тип
Где может быть? | Везде


<br></br>
- `No such file or directory`

Что означает? | Не найден файл, который мы пытаемся открыть
--- | ---
Как исправить? | Важно правильно написать внутри функции `open()` имя файла. Если файл находится в той же папке, что и программа, то имя — это просто полное название файла вместе с расширением (например, вместе с функцией выглядит так: `open("17.txt")`)
Где может быть? | Везде, где есть работа с файлами и используется функция `open`, например, в 17 и 24