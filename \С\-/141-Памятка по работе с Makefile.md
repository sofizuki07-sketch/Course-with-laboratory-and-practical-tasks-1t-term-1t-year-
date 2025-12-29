## Памятка по работе с Makefile

### Что такое Makefile?
Makefile – это файл с инструкциями для утилиты `make`, которая автоматизирует сборку проектов. Она определяет зависимости между файлами и команды для их компиляции.

### Установка make:

**Windows (MSYS2):**

**Для разных окружений**

MSYS2 MSYS (синий):
```bash
pacman -S make
```
MSYS2 MINGW64 (зеленый):
```bash
pacman -S mingw-w64-x86_64-make
```
MSYS2 MINGW32 (красный):
```bash
pacman -S mingw-w64-i686-make
```

**macOS:**
```bash
brew install make
```

**Linux (Ubuntu/Debian):**
```bash
sudo apt install make
```

### Базовая структура Makefile:
```makefile
# Переменные
CC = gcc
CFLAGS = -Wall -Wextra -std=c11
TARGET = program
SOURCES = main.c functions.c
OBJECTS = $(SOURCES:.c=.o)

# Цель по умолчанию
all: $(TARGET)

# Сборка исполняемого файла
$(TARGET): $(OBJECTS)
	$(CC) $(OBJECTS) -o $(TARGET)

# Компиляция .c файлов в .o
%.o: %.c
	$(CC) $(CFLAGS) -c $< -o $@

# Очистка
clean:
	rm -f $(OBJECTS) $(TARGET)

# Запуск программы
run: $(TARGET)
	./$(TARGET)

# Флаг .PHONY указывает, что цель не является файлом
.PHONY: all clean run
```

### Основные правила:
1. **Цель (target)** – что нужно создать
2. **Зависимости (dependencies)** – файлы, от которых зависит цель
3. **Команды (commands)** – действия для создания цели (начинаются с табуляции!)
4. **Переменные** – для упрощения изменения параметров
5. **Автоматические переменные**:
   - `$@` – имя цели
   - `$<` – первая зависимость
   - `$^` – все зависимости

### Пример использования:
```bash
# Сборка проекта
make

# Сборка с конкретной целью
make all

# Очистка скомпилированных файлов
make clean

# Сборка и запуск
make run
```

