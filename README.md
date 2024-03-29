# Test-task-
Ответы на 3 вопроса.

Вопрос №1  
На языке Python написать алгоритм (функцию) определения четности целого числа, который будет аналогичен нижеприведенному по функциональности, но отличен по своей сути. Объяснить плюсы и минусы обеих реализаций. 

Пример: 
    
    def isEven(value):
       return value % 2 == 0

Плюсы:
+ Код короче и более компактный;
+ Не требуется дополнительных проверок или условий, просто вызывается функция isEven с числом в качестве аргумента;
+ Обрабатывает 0 - True.

Минусы:
- Отсутствие обработки ошибок.Не содержат обработки ошибок, например, пользователь может ввести нечисловое значение или отрицательное число, что может привести к неожиданным результатам;
- Minor минус (оформление): Если пользователь использует функцию, то он будет получать True или False - алгоритм (функцию) определения четности целого числа - мне кажется, что во втором варианте лучше.

def isEven(value):
      return value % 2 == 0

  res = isEven(5)
  print(res)

  >>> False
  

Ответ:

    def even_number(number):
        if (number >= 0):
            return (number % 2 == 0)

    number = int(input("Введите число:"))
    if (even_number(number) == True):
        print("Число четное!")

    else:
        print("Число нечетное!")

Тут несколько отметок оставлю:

1. Функция будет реагировать на 0, так как 0 = Если число оканчивается на ноль, то это признак четности. Соответственно и сам 0 относится к четным. Ноль делится на два без остатка. Поэтому его относят к четным числам;

2. Не будет работать с отрицательными числами;

3. Второй алгоритм, реализован с помощью рекурсии - соответственно, издержки по памяти будет немного выше - O(1) (константная память)
Скорость выполнения: O(1) (константное время);

4. Когда пользователь вводит нецелое (дробное число или строку). В этом случае произойдет ошибка при попытке преобразования входных данных в целое число с помощью функции int().

+ Когда пользователь вводит специальные символы (напр, буквы, знаки препинания) или ничего не вводит вообще. В этом случае также может произойти ошибка при попытке преобразования входных данных в целое число с помощью функции int().

Плюсы данной реализации:
+ Данный алгоритм может работать с 0, т.е. если пользователь введет 0, то он получит - число четное;
+ Данный алгоритм рабротает за костантное время;
+ В данный алгоритм для удобства истользования добавлены, при запуске, отображения "Введите число:" - что удобно для взаимодействия пользователя с кодом, а так же после ввода числа, пользователь видит тестом - "Число четное!" или "Число нечетное!";
+ Расширяемость и гибкость. 

Минусы: 
- Использоватенеи рекурсии- Рекурсивные алгоритмы могут быть очень эффективными, но также могут вызывать проблемы с производительностью;
- Отсутствие обработки ошибок. Реализации не содержат обработки ошибок, например, пользователь может ввести нечисловое значение или отрицательное число, что может привести к неожиданным результатам.

Дополнительно: Тут функция с добавлением обработчика ошибок

    def even_number(number):
        return number % 2 == 0

    try:
        number = list(map(int, input("Введите число: ").split()))
    except ValueError:
       ("Ошибка: введите корректное число")

    for i in number:
        if even_number(i):
            print("Число четное!")
        else:
            print("Число нечетное!")

res = all(even_number(i) for i in number)
print(res)

Тут добавили обаботку исключения: Если пользователь введет буквы, а не цифры;
Так же модифицировала ввод: Пользователь может ввести строкой цифры через пробел – далее функция обработает эту последовательность и выведет список с обозначение четное каждое число или нечетное.  


Вопрос №2  
На языке Python написать минимум по 2 класса реализовывающих циклический буфер FIFO. Объяснить плюсы и минусы каждой реализации.
Оценивается:
 1 Полнота и качество реализации
 2 Оформление кода
 3 Наличие сравнения и пояснения по быстродействию

Ответ:
Вариант 1: Циклический буфер FIFO с использованием списка


    class RingBuffer():
        def __init__(self, size):
            self.queue = [None] * size
            self.size = size
            self.head = 0  # идекс первого элемента в очереди
            self.tail = 0  # индекс последнего элемента в очереди
            self.count = 0  # текущее количество элементов в очереди

        def append(self, value):
            self.queue.append(value)
            if self.count >= self.size:
                    raise Exception("Очередь перолнена")

            self.queue[self.tail] = value
            self.tail = (self.tail + 1) % self.size
            self.count += 1

        def remove(self):
            if self.count == 0:
                raise Exception("Очередь пуста")

            value = self.queue[self.head]
            self.head = (self.head + 1) % self.size
            self.count -= 1
            return value

        def __repr__(self):
            return f"RingBuffer(size={self.size}, head={self.head}, tail={self.tail}, count={self.count})"

Плюсы:
- Реализован с помощью списка;
- О-натация: О(1) - за констанстное время (Мы храним индексы, но меняем);
- Тут мы переносим циклически указатель головы и хвоста, что позволяет избежать перезаписи элементов при добавлении новых элементов.

Минусы:
- Раздемер должен быть заранее задан. Если понадобится увеличить размер, то нужно будет создать отдельно вовый экзкпляр класса большего размера.

Для реализации первого варианта использовалась теория: "Теория кольцевого буфера
Ключевая особенность в работе кольцевого буфера — возможность добавлять и удалять элементы без перераспределения массива. Действительно, если предположить, что количество элементов в массиве всегда является константой (что для расчетов в скользящем окне так и есть), то добавление нового элемента сопровождается удалением старого. Таким образом, общее количество элементов не изменяется, но меняется их индексация при добавлении каждого нового элемента.   Последний элемент становится предпоследним, второй элемент занимает место первого, а первый безвозвратно уходит из очереди."

Вариант 2: Более сложнаяруктура -> Использование связного списка

    class CircularBuffer:
        def __init__(self, size):
            self.size = size
            self.head = None
            self.tail = None
            self.count = 0

        def enqueue(self, value):
            if self.count == self.size:
                raise Exception("Буфер переполнен")

            node = Node(value)
            if self == 0:
                self.head = node
                self.tail = node
            else:
                self.tail.next = node
                self.tail = node
                self.tail.next = self.head

            self.count += 1

        def dequeue(self):
            if self.count == 0:
                raise Exception("Буфер пуст")

            value = self.head.value
            if self.count > 1:
                self = self.head.next
                self.tail.next = self.head
            else:
                self.head = None
                self.tail = None

            self.count -= 1
            return value

        def __repr__(self):
            return f"CircularBuffer(size={self.size}, head={self.head}, tail={self.tail}, count={self.count})"


    class Node:
        def __init__(self, value):
            self.value = value
            self.next = None

Плюсы:
- Динамическое изменение размера;
- Для доступа к голове и хвосту используются указатели;

Минусы:
- Более сложнаяруктура. Требуется следить за указателями.

О связных списках в этой реализации подробнее: В приведенном коде self.head и self.tail являются ссылками на первый и последний элементы списка соответственно. Они используются для обозначения начала и конца циклического буфера. При добавлении нового элемента в буфер (enqueue), новый узел создается и присваивается self.tail.next. Затем self.tail обляется, чтобы указывать на новый узел. Наконец, self.tail.next устанавливается на self.head, образуя цикл.

Вопрос №3

На языке Python предложить алгоритм, который быстрее всего (по процессорным тикам) отсортирует данный ей массив чисел. Массив может быть любого размера со случайным порядком чисел (в том числе и отсортированным). Объяснить, почему вы считаете, что функция соответствует заданным критериям.
Можно предположить 2 варианта: Один, наверное, то что и нужно предложить, обычно про них говорят на первых курсах в университете - и это Быстрая сортировка. Почему быстра: Почему я считаю QuickSort самым быстрым алгоритмом для сортировки в данном случае?

    •	QuickSort имеет среднюю временную сложность O(n log n) и лучшую временную сложность O(n log n) в среднем случае.
    •	Алгоритм эффективно использует память, не требуя дополнительного выделения массивов.
    •	Он хорошо справляется с массивами любого размера, включая случайные и уже отсортированные массивы.
    •	QuickSort является одним из самых распространенных и широко используемых алгоритмов сортировки, и его реализация в Python довольно эффективна.

Я бы хотела отметить, что, конечно, все зависит от исходных данных. Оптимальность алгоритма тесно зависит от типа списков/массивов, которые вы собираетесь сортировать, и даже от модели ЭВМ. Чем больше информации в вашем распоряжении, тем более точным будет выбор. При очень слабых предположениях о факторах оптимальной сложностью худшего случая может быть О(n!). Данный ответ касается только сложностей. Фактическое время выполнения алгоритмов зависит от огромного количества факторов.
Но, вариант второй, мне кажется уже реализованный и очень удобный: использовать функции sorted() с параметром key (с operator.itemgetter()) Почему второй вариант: Уже реализованная сортировка в sorted, которая на оптимальном уровне использует оптимизированные алгоритмы сортировки внутри - очень удобно.
