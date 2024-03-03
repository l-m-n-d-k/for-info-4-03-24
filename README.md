# Задача №3044 Сортировка подсчётом(2)
## Код
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