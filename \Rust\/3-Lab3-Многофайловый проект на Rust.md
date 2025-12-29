# Лабораторная работа №3
## Тема: Многофайловые проекты на языке Rust

### Задача 1: Система управления задачами (To-Do List)

#### Описание задачи
Создайте многофайловый проект для системы управления задачами (To-Do List). Проект должен состоять из следующих файлов:
- `models.rs` – содержит определения структур для задач и категорий
- `lib.rs` – реализует основную логику системы управления задачами
- `main.rs` – содержит функцию `main()` с интерактивным меню для взаимодействия с пользователем
- `Cargo.toml` – файл конфигурации для сборки проекта

Проект должен позволять:
- Добавлять задачи с названием, описанием, сроком выполнения и категорией
- Отмечать задачи как выполненные
- Просматривать задачи (все, по категории, только активные)
- Удалять задачи
- Сохранять и загружать данные из JSON-файла

#### Частичное решение

**Файл: models.rs**
```rust
use serde::{Serialize, Deserialize};
use chrono::{DateTime, Utc};

/// Структура, представляющая задачу
#[derive(Serialize, Deserialize, Debug, Clone)]
pub struct Task {
    pub id: u32,
    pub title: String,
    pub description: String,
    pub due_date: Option<DateTime<Utc>>,
    pub category: String,
    pub completed: bool,
    pub created_at: DateTime<Utc>,
}

/// Структура, представляющая категорию задач
#[derive(Serialize, Deserialize, Debug, Clone)]
pub struct Category {
    pub id: u32,
    pub name: String,
    pub description: String,
}

/// Перечисление возможных ошибок системы управления задачами
#[derive(Debug)]
pub enum TaskManagerError {
    TaskNotFound,
    CategoryNotFound,
    InvalidInput,
    IoError(String),
}

/// Реализация трейта std::fmt::Display для красивого вывода ошибок
impl std::fmt::Display for TaskManagerError {
    fn fmt(&self, f: &mut std::fmt::Formatter) -> std::fmt::Result {
        match self {
            TaskManagerError::TaskNotFound => write!(f, "Задача не найдена."),
            TaskManagerError::CategoryNotFound => write!(f, "Категория не найдена."),
            TaskManagerError::InvalidInput => write!(f, "Некорректный ввод."),
            TaskManagerError::IoError(msg) => write!(f, "Ошибка ввода-вывода: {}", msg),
        }
    }
}
```

**Файл: lib.rs**
```rust
use std::collections::HashMap;
use serde::{Serialize, Deserialize};
use chrono::{Utc, DateTime};
use std::fs::File;
use std::io::{Read, Write};

pub mod models;
use models::{Task, Category, TaskManagerError};

/// Основная структура системы управления задачами
#[derive(Serialize, Deserialize)]
pub struct TaskManager {
    tasks: Vec<Task>,
    categories: HashMap<u32, Category>,
    next_task_id: u32,
    next_category_id: u32,
}

impl TaskManager {
    /// Создает новую пустую систему управления задачами
    pub fn new() -> Self {
        Self {
            tasks: Vec::new(),
            categories: HashMap::new(),
            next_task_id: 1,
            next_category_id: 1,
        }
    }
    
    /// Добавляет новую задачу
    /// TODO: Реализуйте этот метод
    /// - Создайте новую задачу с уникальным ID
    /// - Проверьте, существует ли указанная категория
    /// - Установите created_at в текущее время
    /// - Добавьте задачу в вектор tasks
    /// - Увеличьте next_task_id
    /// - Верните ссылку на добавленную задачу
    pub fn add_task(
        &mut self,
        title: String,
        description: String,
        due_date: Option<DateTime<Utc>>,
        category_name: String,
    ) -> Result<&Task, TaskManagerError> {
        // TODO: Реализуйте добавление задачи
        unimplemented!()
    }
    
    /// Находит задачу по ID и возвращает изменяемую ссылку
    /// TODO: Реализуйте этот метод
    /// - Найдите задачу с указанным ID в векторе tasks
    /// - Верните Option<&mut Task>
    pub fn find_task_by_id(&mut self, id: u32) -> Option<&mut Task> {
        // TODO: Реализуйте поиск задачи по ID
        unimplemented!()
    }
    
    /// Отмечает задачу как выполненную
    /// TODO: Реализуйте этот метод
    /// - Найдите задачу по ID
    /// - Если задача найдена, установите completed = true
    /// - Верните Result<(), TaskManagerError>
    pub fn mark_task_completed(&mut self, id: u32) -> Result<(), TaskManagerError> {
        // TODO: Реализуйте отметку задачи как выполненной
        unimplemented!()
    }
    
    /// Добавляет новую категорию
    /// TODO: Реализуйте этот метод
    pub fn add_category(&mut self, name: String, description: String) -> &Category {
        // TODO: Реализуйте добавление категории
        unimplemented!()
    }
    
    /// Возвращает список всех задач
    pub fn list_all_tasks(&self) -> &Vec<Task> {
        &self.tasks
    }
    
    /// Возвращает список активных (не выполненных) задач
    /// TODO: Реализуйте этот метод
    pub fn list_active_tasks(&self) -> Vec<&Task> {
        // TODO: Реализуйте фильтрацию активных задач
        unimplemented!()
    }
    
    /// Возвращает задачи определенной категории
    /// TODO: Реализуйте этот метод
    pub fn list_tasks_by_category(&self, category_name: &str) -> Vec<&Task> {
        // TODO: Реализуйте фильтрацию задач по категории
        unimplemented!()
    }
    
    /// Удаляет задачу по ID
    /// TODO: Реализуйте этот метод
    pub fn delete_task(&mut self, id: u32) -> Result<(), TaskManagerError> {
        // TODO: Реализуйте удаление задачи
        unimplemented!()
    }
    
    /// Сохраняет данные в JSON-файл
    /// TODO: Реализуйте этот метод
    pub fn save_to_file(&self, path: &str) -> Result<(), TaskManagerError> {
        // TODO: Реализуйте сохранение данных в файл
        unimplemented!()
    }
    
    /// Загружает данные из JSON-файла
    /// TODO: Реализуйте этот метод
    pub fn load_from_file(path: &str) -> Result<Self, TaskManagerError> {
        // TODO: Реализуйте загрузку данных из файла
        unimplemented!()
    }
}
```

**Файл: main.rs**
```rust
use std::io::{self, Write};
use task_manager::{TaskManager, TaskManagerError};
use chrono::{Utc, DateTime};

const DATA_FILE: &str = "tasks.json";

fn main() {
    // Загружаем данные из файла или создаем новый менеджер
    let mut manager = TaskManager::load_from_file(DATA_FILE).unwrap_or_else(|e| {
        println!("Не удалось загрузить данные: {}. Создана новая система.", e);
        TaskManager::new()
    });
    
    println!("=== Система управления задачами (To-Do List) ===");
    
    loop {
        print_menu();
        let choice = read_line().trim().to_string();
        
        match choice.as_str() {
            "1" => add_task(&mut manager),
            "2" => mark_task_completed(&mut manager),
            "3" => list_all_tasks(&manager),
            "4" => list_active_tasks(&manager),
            "5" => delete_task(&mut manager),
            "6" => add_category(&mut manager),
            "7" => save_and_exit(&mut manager),
            _ => println!("Неверный выбор. Попробуйте снова."),
        }
    }
}

fn print_menu() {
    println!("\n=== МЕНЮ ===");
    println!("1. Добавить задачу");
    println!("2. Отметить задачу как выполненную");
    println!("3. Показать все задачи");
    println!("4. Показать активные задачи");
    println!("5. Удалить задачу");
    println!("6. Добавить категорию");
    println!("7. Сохранить и выйти");
    print!("Ваш выбор: ");
    io::stdout().flush().unwrap();
}

fn read_line() -> String {
    let mut input = String::new();
    io::stdin().read_line(&mut input).expect("Ошибка чтения строки");
    input
}

fn add_task(manager: &mut TaskManager) {
    println!("\n--- Добавление задачи ---");
    
    print!("Введите название задачи: ");
    io::stdout().flush().unwrap();
    let title = read_line().trim().to_string();
    
    print!("Введите описание задачи: ");
    io::stdout().flush().unwrap();
    let description = read_line().trim().to_string();
    
    // TODO: Добавьте ввод срока выполнения (опционально)
    // TODO: Добавьте ввод или выбор категории
    
    match manager.add_task(title, description, None, "Общая".to_string()) {
        Ok(task) => println!("Задача '{}' успешно добавлена с ID {}", task.title, task.id),
        Err(e) => println!("Ошибка: {}", e),
    }
}

fn mark_task_completed(manager: &mut TaskManager) {
    println!("\n--- Отметка задачи как выполненной ---");
    
    print!("Введите ID задачи: ");
    io::stdout().flush().unwrap();
    
    // TODO: Реализуйте ввод ID и вызов mark_task_completed
}

fn list_all_tasks(manager: &TaskManager) {
    println!("\n--- Все задачи ---");
    
    let tasks = manager.list_all_tasks();
    
    // TODO: Реализуйте вывод списка задач в табличном формате
    if tasks.is_empty() {
        println!("Нет задач.");
    }
}

fn list_active_tasks(manager: &TaskManager) {
    println!("\n--- Активные задачи ---");
    
    // TODO: Реализуйте вывод активных задач
}

fn delete_task(manager: &mut TaskManager) {
    println!("\n--- Удаление задачи ---");
    
    // TODO: Реализуйте удаление задачи
}

fn add_category(manager: &mut TaskManager) {
    println!("\n--- Добавление категории ---");
    
    // TODO: Реализуйте добавление категории
}

fn save_and_exit(manager: &mut TaskManager) {
    println!("\nСохранение данных...");
    
    match manager.save_to_file(DATA_FILE) {
        Ok(_) => println!("Данные успешно сохранены в {}", DATA_FILE),
        Err(e) => println!("Ошибка при сохранении: {}", e),
    }
    
    println!("До свидания!");
    std::process::exit(0);
}
```

**Файл: Cargo.toml**
```toml
[package]
name = "task_manager"
version = "0.1.0"
edition = "2021"

[dependencies]
serde = { version = "1.0", features = ["derive"] }
serde_json = "1.0"
chrono = { version = "0.4", features = ["serde"] }
```

---

## Памятка для работы с проектами на Rust

## Установка
см. файл "Памятка по установке Rust в VS Code"

## Основные команды Cargo
```bash
cargo new имя_проекта      # создать проект
cargo new имя --lib        # создать библиотеку
cargo run                  # собрать и запустить
cargo build                # собрать
cargo check               # проверить компиляцию
cargo test                # запустить тесты
cargo add пакет           # добавить зависимость
cargo fmt                # форматировать код
```

## Cargo.toml (структура)
```toml
[package]
name = "проект"     # обязательно
version = "0.1.0"   # обязательно  
edition = "2021"    # обязательно (2021, 2018, 2015)

[dependencies]
serde = "1.0"       # зависимости
serde_json = "1.0"
```

## Структура проекта
```
проект/
├── Cargo.toml      # конфигурация
├── Cargo.lock      # версии зависимостей
└── src/
    ├── main.rs     # точка входа (исполняемый)
    ├── lib.rs      # точка входа (библиотека)
    └── модуль.rs   # дополнительные модули
```

## Модули в коде
```rust
// В lib.rs/main.rs:
pub mod модуль;           // подключить модуль
use модуль::Функция;      // импортировать

// В модуль.rs:
pub struct Структура {    // публичная структура
    pub поле: Тип,        // публичное поле
}
pub fn функция() {}       // публичная функция
```

## Быстрый старт
```bash
cargo new приложение
cd приложение
cargo add serde
# пишем код в src/
cargo run
```

Ключевое: `cargo.toml` — настройки, `cargo` — команды, `mod` — модули, `pub` — видимость.
