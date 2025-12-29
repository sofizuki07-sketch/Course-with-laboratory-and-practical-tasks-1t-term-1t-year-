# Практическая работа №2
## Тема: Многофайловые проекты на языке C

### Задача 1: Система учета книг в библиотеке

#### Описание задачи
Создайте многофайловый проект для системы учета книг в библиотеке. Проект должен состоять из следующих файлов:
- `book.h` – содержит определение структуры `Book` и прототипы функций для работы с книгами
- `book.c` – реализует функции для добавления книги, вывода информации о книгах и поиска книг по автору
- `main.c` – содержит функцию `main()`, где происходит взаимодействие с пользователем (добавление, вывод, поиск книг)
- `Makefile` – для автоматической сборки проекта

#### Частичное решение

**Файл: book.h**
```c
#ifndef BOOK_H
#define BOOK_H

// Определение структуры Book
struct Book {
    char title[100];      // Название книги
    char author[100];     // Автор книги
    int year;            // Год издания
    int pages;           // Количество страниц
    int is_available;    // Доступность (1 - доступна, 0 - выдана)
};

// Прототипы функций для работы с книгами
void addBook(struct Book *b, const char *title, const char *author, 
             int year, int pages, int is_available);
void printBook(const struct Book *b);
int findBooksByAuthor(const struct Book books[], int count, 
                      const char *author, struct Book result[]);

#endif // BOOK_H
```

**Файл: book.c**
```c
#include <stdio.h>
#include <string.h>
#include "book.h"

// Функция для заполнения данных книги
void addBook(struct Book *b, const char *title, const char *author, 
             int year, int pages, int is_available) {
    // TODO: Скопируйте название книги в поле title
    // TODO: Скопируйте автора книги в поле author
    // TODO: Заполните остальные поля структуры
}

// Функция для вывода информации о книге
void printBook(const struct Book *b) {
    // TODO: Выведите информацию о книге в формате:
    // Название: [название]
    // Автор: [автор]
    // Год: [год], Страниц: [страниц]
    // Статус: [Доступна/Выдана]
}

// Функция для поиска книг по автору
int findBooksByAuthor(const struct Book books[], int count, 
                      const char *author, struct Book result[]) {
    int found = 0;
    // TODO: Пройдите по массиву books, найдите книги указанного автора
    // и скопируйте их в массив result
    // Верните количество найденных книг
    return found;
}
```

**Файл: main.c**
```c
#include <stdio.h>
#include "book.h"

int main(void) {
    // Создание массива книг
    struct Book library[5];
    
    // Заполнение данных книг
    addBook(&library[0], "Преступление и наказание", "Фёдор Достоевский", 
            /* TODO: заполните год */, /* TODO: заполните страницы */, 1);
    addBook(&library[1], "Война и мир", "Лев Толстой", 
            /* TODO: заполните год */, /* TODO: заполните страницы */, 0);
    addBook(&library[2], "Мастер и Маргарита", "Михаил Булгаков", 
            /* TODO: заполните год */, /* TODO: заполните страницы */, 1);
    
    // Вывод информации о всех книгах
    printf("=== ВСЕ КНИГИ В БИБЛИОТЕКЕ ===\n");
    for (int i = 0; i < 3; i++) {
        printf("Книга %d:\n", i + 1);
        printBook(&library[i]);
        printf("\n");
    }
    
    // Поиск книг по автору
    struct Book foundBooks[5];
    char searchAuthor[] = "Лев Толстой";
    int foundCount = findBooksByAuthor(library, 3, searchAuthor, foundBooks);
    
    printf("=== НАЙДЕННЫЕ КНИГИ АВТОРА: %s ===\n", searchAuthor);
    for (int i = 0; i < foundCount; i++) {
        printBook(&foundBooks[i]);
        printf("\n");
    }
    
    return 0;
}
```

**Файл: Makefile**
```makefile
# Makefile для проекта "Система учета книг"

CC = gcc
CFLAGS = -Wall -O2
SRC = main.c book.c
OBJ = $(SRC:.c=.o)
TARGET = library_system.exe

all: $(TARGET)

$(TARGET): $(OBJ)
	$(CC) -o $@ $^ $(CFLAGS)

%.o: %.c
	$(CC) $(CFLAGS) -c $< -o $@

clean:
	rm -f $(OBJ) $(TARGET)

run: $(TARGET)
	./$(TARGET)

.PHONY: all clean run
```

---

### Задача 2: Калькулятор комплексных чисел

#### Описание задачи
Создайте многофайловый проект для работы с комплексными числами. Проект должен состоять из:
- `complex.h` – содержит определение структуры `Complex` и прототипы функций для операций с комплексными числами
- `complex.c` – реализует функции сложения, вычитания, умножения и деления комплексных чисел
- `main.c` – содержит функцию `main()`, демонстрирующую работу с комплексными числами
- `Makefile` – для автоматической сборки проекта

#### Частичное решение

**Файл: complex.h**
```c
#ifndef COMPLEX_H
#define COMPLEX_H

// Определение структуры Complex
struct Complex {
    double real;    // Действительная часть
    double imag;    // Мнимая часть
};

// Прототипы функций для работы с комплексными числами
struct Complex createComplex(double real, double imag);
struct Complex addComplex(struct Complex a, struct Complex b);
struct Complex subtractComplex(struct Complex a, struct Complex b);
struct Complex multiplyComplex(struct Complex a, struct Complex b);
struct Complex divideComplex(struct Complex a, struct Complex b);
void printComplex(struct Complex c);

#endif // COMPLEX_H
```

**Файл: complex.c**
```c
#include <stdio.h>
#include "complex.h"

// Функция создания комплексного числа
struct Complex createComplex(double real, double imag) {
    struct Complex result;
    // TODO: Заполните поля структуры
    return result;
}

// Функция сложения комплексных чисел
struct Complex addComplex(struct Complex a, struct Complex b) {
    struct Complex result;
    // TODO: Реализуйте сложение: (a.real + b.real) + i*(a.imag + b.imag)
    return result;
}

// Функция вычитания комплексных чисел
struct Complex subtractComplex(struct Complex a, struct Complex b) {
    struct Complex result;
    // TODO: Реализуйте вычитание: (a.real - b.real) + i*(a.imag - b.imag)
    return result;
}

// Функция умножения комплексных чисел
struct Complex multiplyComplex(struct Complex a, struct Complex b) {
    struct Complex result;
    // TODO: Реализуйте умножение по формуле:
    // (a.real*b.real - a.imag*b.imag) + i*(a.real*b.imag + a.imag*b.real)
    return result;
}

// Функция деления комплексных чисел
struct Complex divideComplex(struct Complex a, struct Complex b) {
    struct Complex result;
    // TODO: Реализуйте деление по формуле:
    // real = (a.real*b.real + a.imag*b.imag) / (b.real^2 + b.imag^2)
    // imag = (a.imag*b.real - a.real*b.imag) / (b.real^2 + b.imag^2)
    return result;
}

// Функция вывода комплексного числа
void printComplex(struct Complex c) {
    // TODO: Выведите число в формате: (real + imag*i)
    // Например: (3.5 + 2.1*i) или (2.0 - 1.5*i)
}
```

**Файл: main.c**
```c
#include <stdio.h>
#include "complex.h"

int main(void) {
    // Создание комплексных чисел
    struct Complex c1 = createComplex(3.0, 4.0);   // 3 + 4i
    struct Complex c2 = createComplex(1.0, -2.0);  // 1 - 2i
    
    printf("Комплексное число 1: ");
    printComplex(c1);
    printf("\n");
    
    printf("Комплексное число 2: ");
    printComplex(c2);
    printf("\n\n");
    
    // Демонстрация операций
    printf("=== ОПЕРАЦИИ С КОМПЛЕКСНЫМИ ЧИСЛАМИ ===\n");
    
    struct Complex sum = addComplex(c1, c2);
    printf("Сумма: ");
    printComplex(sum);
    printf("\n");
    
    struct Complex diff = subtractComplex(c1, c2);
    printf("Разность: ");
    printComplex(diff);
    printf("\n");
    
    struct Complex prod = multiplyComplex(c1, c2);
    printf("Произведение: ");
    printComplex(prod);
    printf("\n");
    
    struct Complex quot = divideComplex(c1, c2);
    printf("Частное: ");
    printComplex(quot);
    printf("\n");
    
    return 0;
}
```

**Файл: Makefile**
```makefile
# Makefile для проекта "Калькулятор комплексных чисел"

CC = gcc
CFLAGS = -Wall -O2 -lm
SRC = main.c complex.c
OBJ = $(SRC:.c=.o)
TARGET = complex_calculator.exe

all: $(TARGET)

$(TARGET): $(OBJ)
	$(CC) -o $@ $^ $(CFLAGS)

%.o: %.c
	$(CC) $(CFLAGS) -c $< -o $@

clean:
	rm -f $(OBJ) $(TARGET)

run: $(TARGET)
	./$(TARGET)

test: $(TARGET)
	@echo "Запуск тестовой программы..."
	./$(TARGET)

.PHONY: all clean run test
```

**Примечание:** В файле `Makefile` для проекта калькулятора комплексных чисел добавлен флаг `-lm` для подключения математической библиотеки, которая может понадобиться для некоторых операций.

