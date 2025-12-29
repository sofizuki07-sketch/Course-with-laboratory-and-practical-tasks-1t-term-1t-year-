# Настройка вывода русского языка в VSCode

### Для Windows (MSYS2 UCRT64 / MinGW):
1. **Откройте настройки VSCode:**
   - Нажмите `Ctrl + ,` (или `File → Preferences → Settings`)
   - В правом верхнем углу нажмите на иконку "Открыть настройки (JSON)"

2. **Добавьте следующие параметры в файл `settings.json`:**
```json
{
    "terminal.integrated.defaultProfile.windows": "Command Prompt",
    "terminal.integrated.automationShell.windows": "cmd.exe",
    "code-runner.executorMap": {
        "c": "cd $dir && gcc $fileName -fexec-charset=CP866 -o $fileNameWithoutExt && $dir$fileNameWithoutExt"
    },
    "files.encoding": "utf8",
    "files.autoGuessEncoding": true
}
```

3. **Альтернативный вариант для MSYS2:**
```json
{
    "terminal.integrated.profiles.windows": {
        "MSYS2 UCRT64": {
            "path": "C:\\msys64\\msys2_shell.cmd",
            "args": ["-defterm", "-here", "-no-start", "-ucrt64"],
            "icon": "terminal-bash"
        }
    },
    "terminal.integrated.defaultProfile.windows": "MSYS2 UCRT64",
    "code-runner.executorMap": {
        "c": "cd $dir && gcc $fileName -o $fileNameWithoutExt && $dir$fileNameWithoutExt"
    }
}
```

### Для Linux и macOS:
1. **Откройте настройки VSCode (`Ctrl + ,`)**
2. **Добавьте в `settings.json`:**
```json
{
    "terminal.integrated.defaultProfile.linux": "bash",
    "terminal.integrated.defaultProfile.osx": "zsh",
    "code-runner.executorMap": {
        "c": "cd $dir && gcc $fileName -o $fileNameWithoutExt && $dir$fileNameWithoutExt"
    },
    "files.encoding": "utf8"
}
```

### Дополнительные рекомендации:

1. **Для исходных файлов .c:**
   - Убедитесь, что файлы сохраняются в кодировке UTF-8
   - В правом нижнем углу VSCode нажмите на кодировку (например, "UTF-8") и выберите "Сохранить с кодировкой" → "UTF-8"

2. **Проверка настроек:**
   - Создайте тестовую программу:
   ```c
   #include <stdio.h>
   
   int main() {
       printf("Привет, мир!\n");
       printf("Кириллица: абвгдеёжзийклмнопрстуфхцчшщъыьэюя\n");
       return 0;
   }
   ```

   ---

3. **Если проблема осталась:**
   
    **Проверьте системную локализацию:**
     - Windows: Панель управления → Язык → Административные языковые параметры → Изменить язык системы
     - Убедитесь, что стоит "Русский (Россия)"
  
   **Переустановите VS Code с правильными настройками:**
     - При установке выберите русский язык интерфейса
     - Установите все рекомендованные расширения
  


## Проверка работы:
1. Сохраните файл с расширением `.c`
2. Нажмите `Ctrl + Alt + N` (если установлен Code Runner)
3. Убедитесь, что русский текст отображается корректно в терминале VSCode

**Примечание:** Некоторые терминалы Windows могут требовать дополнительной настройки шрифтов. Рекомендуется использовать шрифты, поддерживающие кириллицу (Cascadia Code, Consolas, JetBrains Mono).
