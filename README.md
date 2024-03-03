# Задача №3044 Сортировка подсчётом(2)
## Решение (сортировка подсчётом)
```python
def counting_sort(arr):
    n = len(arr)
    count = [0] * 20001

    for num in arr:
        count[num + 10000] += 1

    sorted_arr = []
    for i in range(len(count)):
        sorted_arr.extend([i - 10000] * count[i])

    return sorted_arr

n = int(input())
elements = list(map(int, input().split()))
sorted_elements = counting_sort(elements)
print(*sorted_elements)
```
## Объяснение алгоритма
- Создаем массив count с нулевыми значениями. Размер массива выбирается таким образом, чтобы можно было учесть все возможные значения элементов входного массива arr, сдвинутых на 10000, чтобы обработать отрицательные числа.
- Проходим по всем элементам входного массива arr и увеличиваем на единицу значение в массиве count по индексу, соответствующему значению элемента с учетом сдвига. Это позволяет нам получить количество вхождений каждого значения в исходном массиве.
- Создаем пустой массив sorted_arr. Затем проходим по массиву count, и для каждого индекса, где количество (значение в count) больше нуля, добавляем в sorted_arr значение этого индекса (с учетом обратного сдвига на 10000), повторенное столько раз, сколько указано в count.

# Задача №230. Сортировка выбором максимума
## Решение (сортировка выбором)
```python
def counting_cover_thickness(L, N, M, sock_pairs, measurement_points):
    count = [0] * (L + 1)
   
    for l, r in sock_pairs:
        count[l] += 1
        count[r] -= 1
    
    for i in range(1, L + 1):
        count[i] += count[i - 1]
    
    cover_thickness = []
    for point in measurement_points:
        cover_thickness.append(count[point])

    return cover_thickness

L, N, M = map(int, input().split())
sock_pairs = []
for _ in range(N):
    l, r = map(int, input().split())
    sock_pairs.append((l, r))
measurement_points = list(map(int, input().split()))


results = counting_cover_thickness(L, N, M, sock_pairs, measurement_points)
print(*results)
```
## Объяснение алгоритма
- Создается массив count размером L + 1, где L — длина пола. Этот массив будет использоваться для подсчета "накопленной толщины" носков на каждом отрезке пола. Изначально все элементы массива установлены в 0.
- Для каждой пары (l, r) увеличиваем значение в count[l] на 1 и уменьшаем значение в count[r] на 1. Это делается для реализации техники "разностей" или "prefix sum" (префиксных сумм), где l — начало участка с носками, а r — конец. Увеличение на 1 на начале диапазона и уменьшение на 1 после окончания диапазона позволяет нам в дальнейшем быстро рассчитать "текущую толщину" слоя носков в любой точке.
- Проходим по массиву count, начиная с первого элемента, и прибавляем к текущему элементу значение предыдущего. Таким образом, каждый элемент count[i] будет содержать сумму всех предыдущих изменений, что фактически дает нам толщину слоя носков на полу до точки i включительно.
- Для каждой точки измерения из measurement_points определяем толщину слоя носков, обращаясь к соответствующему элементу массива count и добавляем эту толщину в список cover_thickness.

# Задача №754. Пирамидальная сортировка
## Решение (Пирамидальная сортировка)
```python
def heapify(arr, n, i):
    largest = i
    l = 2 * i + 1
    r = 2 * i + 2
  
    if l < n and arr[i] < arr[l]:
        largest = l
  
    if r < n and arr[largest] < arr[r]:
        largest = r
  
    if largest != i:
        arr[i], arr[largest] = arr[largest], arr[i]
        heapify(arr, n, largest)
  
def heap_sort(arr):
    n = len(arr)
  
    for i in range(n // 2 - 1, -1, -1):
        heapify(arr, n, i)
  
    for i in range(n - 1, 0, -1):
        arr[i], arr[0] = arr[0], arr[i]
        heapify(arr, i, 0)
  

size = int(input())
nums = list(map(int, input().split()))

heap_sort(nums)
print(*nums)
```
## Объяснение алгоритма
