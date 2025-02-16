![logo_ironhack_blue 7](https://user-images.githubusercontent.com/23629340/40541063-a07a0a8a-601a-11e8-91b5-2f13e4e6b441.png)

# Lab | for loops and if conditions

## Introduction

`for` loops and `if/else` statements are powerful for controlling the flow of your programs. We will practice them right here!
 
## Deliverables

- `main.ipynb`

## Submission

Upon completion, add your deliverables to git. Then commit git and push your branch to the remote.



## added a self-guided memory lab


##TASK1

```
def self_check_2():
    # Two variables pointing to the same object
    same1 = [1, 2, 3]
    same2 = same1
    
   # Two variables with equal values but different objects
    diff1 = [1, 2, 3]
    diff2 = diff1.copy()
    
   # Check object identity and value equality
    if (id(same1) == id(same2) and 
        id(diff1) != id(diff2) and 
        diff1 == diff2):
        print("🎉 You understand object identity!")
    else:
        print("🤔 Check your understanding of is vs ==")

self_check_2()
```


#TASK2 

```
def add_number(lst, num):
    # Create a new list by adding the number to the original list without modifying the original
    new_lst = lst + [num]
    return new_lst

def self_check_3():
    original = [1, 2, 3]
    
    new_list = add_number(original, 4)
```

#TASK3 

```
def sum_of_squares(n):
    # Generator function that yields the square of each number from 1 to n
    for i in range(1, n+1):
        yield i * i

def self_check_4():
    result = sum(sum_of_squares(1000000))  # Sum the squares from 1 to 1,000,000 using the generator
    expected = sum(i*i for i in range(1, 1000000+1))  # Calculate the expected sum directly
    
    if result == expected:
        print("🎉 Your function is memory efficient!")
    else:
        print("🤔 Check your calculations")

self_check_4()
```

## self-guided-iterators.md

#TASK1 
```
def self_check_1():
    # Create an iterator from the string "AI"
    text_iterator = iter("AI")
    
    # Use next() to print each character
    print(next(text_iterator))
    print(next(text_iterator))
    
    # Self-check
    import io
    import sys
    captured_output = io.StringIO()
    sys.stdout = captured_output
    
    try:
        text_iterator = iter("AI")
        print(next(text_iterator))
        print(next(text_iterator))
        sys.stdout = sys.__stdout__
        if captured_output.getvalue().strip() == "A\nI":
            print("🎉 You understand iterators!")
        else:
            print("🤔 Not quite. Make sure you're printing one character at a time")
    except:
        sys.stdout = sys.__stdout__
        print("🤔 Something went wrong. Did you create the iterator correctly?")

self_check_1()
```

#TASK2 
```
def countdown(n):
    # Generator function that counts down from n to 1
    while n > 0:
        yield n
        n -= 1

def self_check_2():
    # Test the generator
    try:
        numbers = list(countdown(3))
        if numbers == [3, 2, 1]:
            print("🎉 Your generator works perfectly!")
        else:
            print("🤔 The countdown should go from n to 1")
    except:
        print("🤔 Make sure your generator yields one number at a time")

self_check_2()
```


#TASK3

```
def self_check_3():
    # Your task:
    # Create a generator function that yields even numbers up to n
    # Do NOT create a list first!
    ###!!! Your code here !!!###
    
    # Test the generator
    try:
        even_numbers = list(even_numbers_up_to(5))
        if even_numbers == [0, 2, 4]:
            print("🎉 Your generator yields even numbers correctly!")
        else:
            print("🤔 Check your even numbers logic")
    except:
        print("🤔 Make sure your generator yields numbers one at a time")

self_check_3()
```

#TASK4
```
def self_check_4():
    # Your task:
    # Create a generator expression that yields doubled numbers
    # for numbers 1 to 5
    ###!!! Your code here !!!###
    
    # Test the generator expression
    try:
        doubled = list(doubled_numbers)
        if doubled == [2, 4, 6, 8, 10]:
            print("🎉 Your generator expression works!")
        else:
            print("🤔 The numbers should be doubled")
    except:
        print("🤔 Make sure you created a generator expression, not a list")

self_check_4()
```
## 1. Fibonacci Generator Function 
```
def fibonacci(n):
    a, b = 0, 1
    for _ in range(n):
        yield b
        a, b = b, a + b

# Example usage:
for num in fibonacci(5):
    print(num)  # Should print: 1, 1, 2, 3, 5
```

## 2. Read File in Chunks Generator Function
```
def read_in_chunks(file_path, chunk_size=1024):
    with open(file_path, 'rb') as file:  # Open the file in binary mode
        while chunk := file.read(chunk_size):
            yield chunk

# Example usage:
file_path = 'large_file.txt'  # Replace with your file path
for chunk in read_in_chunks(file_path):
    print(chunk)  # Process each chunk
```

## interleaved_generator function 

```
def interleaved_generator(list1, list2):
    i, j = 0, 0  # pointers for list1 and list2
    
    while i < len(list1) and j < len(list2):
        if list1[i] < list2[j]:
            yield list1[i]
            i += 1
        elif list1[i] > list2[j]:
            yield list2[j]
            j += 1
        else:
            yield list1[i]  # or list2[i], as they are equal
            i += 1
            j += 1

    # If there are any remaining elements in list1
    while i < len(list1):
        yield list1[i]
        i += 1
    
    # If there are any remaining elements in list2
    while j < len(list2):
        yield list2[j]
        j += 1

# Testing the solution
def test_interleaved():
    test_cases = [
        ([1, 3, 5], [2, 4, 6], [1, 2, 3, 4, 5, 6]),
        ([1, 2, 3], [1, 2, 3], [1, 2, 3]),
        ([], [1, 2, 3], [1, 2, 3]),
        ([1], [], [1])
    ]
    
    for list1, list2, expected in test_cases:
        result = list(interleaved_generator(list1, list2))
        if result == expected:
            print(f"✅ Test passed for lists {list1} and {list2}")
        else:
            print(f"❌ Test failed for lists {list1} and {list2}")
            print(f"Expected: {expected}")
            print(f"Got: {result}")

test_interleaved()
``` 



## self-guided-decorators.md 

#TASK1
```
def self_check_1():
    def double(x):
        return x * 2
    
    doubler = double  # Pointing to the 'double' function without parentheses
    result = doubler(5)  # Using 'doubler' to call the function and double the number 5
    
    # Self-check
    try:
        if result == 10 and doubler is double:
            print("🎉 You got it! You understand functions as objects!")
        else:
            print("🤔 Not quite. Remember: don't use parentheses when assigning the function")
    except NameError:
        print("Please write the code where it's indicated")

self_check_1()
```

#TASK2
```
def self_check_2():
  
    def create_greeter(greeting):
        def greeter(name):
            return f"{greeting}, {name}!"
        return greeter
    
    # 2. Use your create_greeter to make casual and formal greeters
    casual_greeter = create_greeter("Hi")
    formal_greeter = create_greeter("Good morning")
    
    # 3. Put both greetings to Bob in a list called 'results'
    results = [casual_greeter("Bob"), formal_greeter("Bob")]
    
    expected = ["Hi, Bob!", "Good morning, Bob!"]
    
    if results == expected:
        print("🎉 Perfect! You understand nested functions!")
    else:
        print("🤔 Not quite. Check how create_greeter is used in the example")

self_check_2()
```

#TASK3 
```
def self_check_3():
 def hello_world():
        print("Hello World!")
    
    # Self-check (checking print output)
    import io
    import sys
    captured_output = io.StringIO()
    sys.stdout = captured_output
    
    hello_world()
    sys.stdout = sys.__stdout__
    
    expected_output = "***\nHello World!\n***\n"
    if captured_output.getvalue() == expected_output:
        print("🎉 You've created your first decorator!")
    else:
        print("🤔 Check your output. Should be exactly: ***, Hello World!, ***")

self_check_3()
```

#TASK4
```
def self_check_4():
    def error_logger(func):
        def wrapper(*args, **kwargs):
            try:
                result = func(*args, **kwargs)
                print(f"[SUCCESS] {func.__name__}")
                wrapper.success_count += 1
                return result
            except Exception as e:
                print(f"[ERROR] {func.__name__}")
                wrapper.error_count += 1
                raise e
        wrapper.success_count = 0
        wrapper.error_count = 0
        return wrapper
    
    # 2. Use it on test_division below
    @error_logger
    def test_division(a, b):
        return a / b
    
    # Let's test both success and failure
    test_division(6, 2)  # Should print: [SUCCESS] test_division
    try:
        test_division(6, 0)  # Should print: [ERROR] test_division
    except:
        pass

    # Self-check
    if test_division.success_count == 1 and test_division.error_count == 1:
        print("🎉 Your error logger works correctly!")
    else:
        print("🤔 Make sure you're tracking both successes and errors")

self_check_4()
``` 
