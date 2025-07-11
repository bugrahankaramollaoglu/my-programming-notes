# python

- hata mesajlarını özelleştirebilirsin

```python
try:
    import telebot
except ImportError:
    print('This program requires the telebot module, which you')
    print('can install by following the instructions at')
    print('https://pypi.org/project/telebot/')
    sys.exit()
```

- python’da C fonksiyonları çalıştırmak için ctypes kütüphanesini kullanabilirsin.
önce c fonksiyonlarını .c uzantısı ile kaydet. mesela

```c
// add.c
int add_int(int num1, int num2){
    return num1 + num2;
}

float add_float(float num1, float num2){
    return num1 + num2;
}
```

 sonra .so uzantısıyla derlemelisin. 

```c
// linux
gcc -shared -Wl,-soname,adder -o adder.so -fPIC add.c
// mac
gcc -shared -Wl,-install_name,adder.so -o adder.so -fPIC add.c
```

daha sonra python kodunda 

```python
from ctypes import *

#load the shared object file
adder = CDLL('./adder.so')

#Find sum of integers
res_int = adder.add_int(4,5)
print "Sum of 4 and 5 = " + str(res_int)

#Find sum of floats
a = c_float(5.5)
b = c_float(4.1)

add_float = adder.add_float
add_float.restype = c_float
print "Sum of 5.5 and 4.1 = ", str(add_float(a, b))
```

- python’da yazdıgın bir koda bir textten input alıp çıktıyı da yine bir texte dökebilirsin

```python
import sys

sys.stdin = open('inputDosyasi.txt', 'r')
sys.stdout = open('outputDosyam.txt', 'w')

import solution
```

- error types in python
    - syntax error
    
    ```python
    print('hello!)
    ```
    
    - logic error (hardest)
    
    ```python
    n = 5
    total = 0
    for i in range(1, n):
        total += i ** 2
    print(total)
    ```
    
    - name error
    
    ```python
    print(x)
    ```
    
    - key error
    
    ```python
    my_dict = {"one": 1, "two": 2, "three": 3}
    print(my_dict["four"])
    ```
    
    - attribute error
    
    ```python
    my_list = [1, 2, 3]
    print(my_list.append(4))
    ```
    
    - type error
    
    ```python
    my_list = [1, 2, 3]
    my_list.sort(reverse=True)
    print(my_list)
    ```
    
    - value error
    
    ```python
    my_string = "Hello, world!"
    print(int(my_string))
    ```
    
    - IOerror (file not found)
    
    ```python
    with open("nonexistent.txt", "r") as f:
        print(f.read())
    ```
    
- bir kodun çıktısını bir dosyaya yazdırmak istiyosan

```python
with open("asd.txt", "w") as f:
	print(dir(os), file=f)
```

- import os.name metodu windowsta nt, unix’te posix yazdirir

```python
import os

if (os.name != 'nt'):
    print('Sisteminiz Windows değil, bu programı kullanamazsınız.')
```

- bilgisayar neden 2li sistemdedir? çünkü en verimli öyle çalışır. elektrik devreden ya geçer, ya da geçmez. elektrik geçerken 5~ volt, yokken 0 volt geçer.
- float sayilar için == kullanılması tavsiye edilmez.

```jsx
x = 0.1 + 0.2
y = 0.3

if x == y:
    print("Equal")
else:
    print("Not Equal") // it will print not equal
```

çünkü float sayilar tam olarak bitlerle ifade edilemez. yani 0.10000000000 diye sonsuza kadar gitmez, bir yerde 0.100000000004 gibi bir hal alir. 

- to ask for multiple inputs in one line

```python
def fun():
	nums = input("enter 3 nums: ")

	nums = nums.split()
	firstNum = int(nums[0])
	secondNum = int(nums[1])
	thirdNum = int(nums[2])
```

or you can write it as 

```python
nums = input("Enter 3 nums separated by commas: ")
x, y, z = map(int, nums.split(','))
```

- how to sort tuples in a list according to a spesific index

```python
my_list = [(3, 7, 4), (1, 2, 9), (2, 6, 5)]

sorted_list = sorted(my_list, key=lambda x: x[1])

print(sorted_list) # [(1, 2, 9), (2, 6, 5), (3, 7, 4)]
```

you can also set it to sort reversedly 

```python
reverse_sorted_list = sorted(my_list, key=lambda x: x[1], reverse=True)
```

you can also sort it also based on other indices 

```python
reverse_sorted_list = sorted(my_list, key=lambda x: (x[1],x[2]), reverse=True)
```

- how to turn a list into string

```python
lst = ['a','l','i']
return ''.join(lst)
```

-