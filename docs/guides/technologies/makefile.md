# Makefile

> На основе <https://makefiletutorial.com/#makefile-cookbook>

## Переменные

Переменными могут быть только строки. Обычно вы хотите использовать :=, но = также работает.

Вот пример использования переменных:

```makefile
files := file1 file2
some_file: $(files)
    echo "Look at this variable: " $(files)
    touch some_file

file1:
    touch file1
file2:
    touch file2

clean:
    rm -f file1 file2 some_file
```

Одинарные или двойные кавычки не имеют никакого значения. Это просто символы, которые присваиваются переменной. Однако кавычки полезны для shell /bash, и они нужны вам в таких командах, как **printf**. В этом примере две команды ведут себя одинаково:

```makefile
a := one two # a is set to the string "one two"
b := 'one two' # Not recommended. b is set to the string "'one two'"
all:
    printf '$a'
    printf $b
```

Ссылочные переменные, использующие либо ${}, либо $()

```makefile
x := dude
all:
    echo $(x)
    echo ${x}

# Bad practice, but works
echo $x
```

## Таргеты

### Запуск всех таргетов

Создаете несколько таргетов и хотите, чтобы все они были запущены? Сделайте все таргетом. Поскольку это первое правило в списке, оно будет выполняться по умолчанию, если make вызывается без указания цели.

```makefile
all: one two three

one:
	touch one
two:
	touch two
three:
	touch three

clean:
	rm -f one two three
```

### Несколько таргетов в одном

При наличии нескольких целей для правила команды будут выполняться для каждой цели. **$@** — это автоматическая переменная, содержащая имя цели.

```makefile
all: f1.o f2.o

f1.o f2.o:
	echo $@
# Equivalent to:
# f1.o:
#	 echo f1.o
# f2.o:
#	 echo f2.o
```
