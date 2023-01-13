# Самая основная теория для ЕГЭ


## 1 задание 













## 2 задание  

#### Алгоритм решения 2 задания состоит всего из 2 шагов:

❶ — перебираем все возможные комбинации из 0 и 1,  и подставляем вместо `x`, `y`, `z` и `w` в логической функции

❷ — выводим те значения `x`, `y`, `z`, `w`, при которых функция давала нужный результат (1 или 0)


#### Реализация алгоритма: 

❶ — перебор всегда осуществляется при помощи `for`;

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
$\land$ или $\&$ | `and`
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













## 15 задание  













## 16 задание  













## 17 задание  













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



#### Типы данных
- числа 
	- целые — `int()`   
	- не целые — `float()` 
- текст, строки — `str()` 
- списки — `list()`
- логический тип — `bool()`

Тип определяет операции, которые можно делать с объектом. 
Строки нельзя делить, например. 



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