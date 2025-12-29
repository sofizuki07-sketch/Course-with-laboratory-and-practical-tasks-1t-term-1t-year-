# Памятка: Установка Rust с поддержкой IDE

## 1. Установка Rust
```bash
# Универсальная установка
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

# Выберите вариант установки:
# 1) Proceed with installation (default) - рекомендуется
# 2) Customize installation
# 3) Cancel installation

# После установки:
source $HOME/.cargo/env  # или перезапустите терминал
```

## 2. Проверка установки
```bash
rustc --version  # компилятор
cargo --version  # менеджер пакетов
rustup --version # менеджер версий
```

## 3. Настройка VS Code (рекомендуемая IDE)

### Установите расширения:
1. **rust-analyzer** — основной инструмент (автодополнение, проверка типов, рефакторинг)
2. **Better TOML** — подсветка Cargo.toml
3. **CodeLLDB** или **Native Debug** — отладчик
4. **crates** — управление зависимостями в Cargo.toml

### Настройки для VS Code (settings.json):
```json
{
    "rust-analyzer.check.command": "clippy",
    "rust-analyzer.checkOnSave": true,
    "rust-analyzer.completion.autoimport.enable": true,
    "editor.formatOnSave": true,
    "[rust]": {
        "editor.defaultFormatter": "rust-lang.rust-analyzer"
    }
}
```

