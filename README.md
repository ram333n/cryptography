# Варіант 5
Для запуску програми введіть команду: `py [file.name]`

### 1) DSA
Вибір параметрів:
1) Обираємо хеш-функцію `H(x)`(наприклад SHA-1)
2) Обираємо велике просте число `q`, розмірність якого в бітах співпадає з виводом хеш-функції
3) Обираємо просте число `p` таке, що `p - 1` ділиться на `q` 
4) Обираємо число `h` i `g` такі, що `g = h^((p - 1)/q)`, причому `g != 1`
5) Отримуємо трійку `(p, q, g)`

Генерація відкритого і закритого ключів:
1) Закритий ключ - це випадкове число `x` в інтервалі `(0, q)`
2) Відкритий ключ обраховується за формулою `y = g^x mod p`

Підпис повідомлення(m):
1) Обираємо випадкове число `k` з інтервалу `(0, q)`
2) Обчислюємо `r=(g^k mod p) mod q`
3) Обчислюємо `s=(k^-1*(H(m) + x*r)) mod q`
Якщо r=0 або s=0, то обирається інше `k`
Підписом є пара чисел `(r, s)`

Перевірка підпису:
1) Обраховуємо `w=s^-1 mod q`
2) Обраховуємо `u=(H(m)*w) mod q`
3) Обраховуємо `z=(r*w) mod q`
4) Обраховуємо `v=((g^u * y^z) mod p) mod q`

Якщо `v=r`, то підпис вірний


### 2) AES
Алгоритм:

1) Ініціалізація ключа: визначення шифрувального ключа. Розмір ключа може бути 128 біт, 192 біти або 256 біт.

2) Крок першого раунду: дані розбиваються на блоки фіксованого розміру (зазвичай 128 біт). Кожен блок даних проходить через операцію "Додавання ключа", де блоки даних поєднуються з частинами ключа.

3) Операція заміни байтів (SubBytes): кожен байт у блоку даних замінюється на відповідний байт з S-блока (таблиці заміни).

4) Операція зсуву рядків (ShiftRows): байти в кожному рядку блоку даних циклічно зсуваються вліво на певну кількість позицій.

5) Операція змішування стовпців (MixColumns): байти в кожному стовпці блоку даних змішуються за певним алгоритмом.

6) Крок останнього раунду: аналогічний першому раунду, але без операції MixColumns.

7) Фінальний раунд: дані проходять через операцію "Додавання ключа" з розширеною версією ключа.

Залежно від розміру ключа (128, 192 або 256 біт), AES виконує різну кількість раундів шифрування. Для ключа розміром 128 біт виконується 10 раундів, для 192 біт - 12 раундів, а для 256 біт - 14 раундів.

Кожен крок алгоритму AES є незворотнім, що робить зашифровані дані безпечними. Розшифрування відбувається шляхом зворотного застосування кожного кроку у зворотному порядку, використовуючи ті ж самі ключі раундів.