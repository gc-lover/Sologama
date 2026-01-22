# Настройка среды разработки Evolution Fantasy

## Обзор

Этот гайд поможет настроить среду разработки для проекта **Evolution Fantasy** в Cursor IDE.

## Структура проекта

Проект организован следующим образом:

```
SoloGama/                    # Основной проект UE
├── Plugins/                 # Плагины проекта
├── Content/                 # Игровой контент
├── Source/                  # Исходный код
└── *.uproject               # Файл проекта UE

docs/                        # Документация проекта
├── project/                 # Общая информация
├── architecture/            # Архитектура
├── game_design/             # Игровой дизайн
├── development/             # Разработка
└── cursor/                  # Cursor IDE настройки

.cursor/                     # Cursor IDE конфигурация
├── commands/                # Кастомные команды
├── rules/                   # Правила для агентов
└── workflows/               # Рабочие процессы
```

## Настройка Cursor IDE

### 1. Установка необходимых расширений

Убедитесь, что установлены следующие расширения:
- **C/C++** (Microsoft)
- **Unreal Engine** (Custom)
- **Git Graph** (mhutchie)
- **Markdown Preview** (Microsoft)

### 2. Конфигурация агентов

#### Основные команды:
Посмотрите доступные команды в папке `.cursor/commands/`:
- `main-agent-command.md` - Основные команды разработки
- `game-design-commands.md` - Команды игрового дизайна
- `technical-commands.md` - Технические команды

#### Доступные команды в чате:
- `/design-ability` - Дизайн новой способности
- `/implement-ability` - Реализация способности
- `/create-level` - Создание уровня
- `/balance-ability` - Баланс способности

### 3. Правила агентов

Правила агентов находятся в папке `.cursor/rules/`:
- `main-agent-rule.mdc` - Основные правила разработки (всегда применяются)
- `game-design-rules.mdc` - Правила игрового дизайна
- `technical-rules.mdc` - Технические правила
- `content-rules.mdc` - Правила создания контента

Все агенты следуют строгим правилам:
- **SOLID принципы** для архитектуры кода
- **Максимум 350 строк** на класс
- **Полная документация** публичных методов
- **Unreal Engine best practices**

## Разработка с Unreal Engine

### Системные требования
- **Unreal Engine 5.3+**
- **Visual Studio 2022**
- **Windows 10/11**
- **16GB+ RAM**
- **SSD диск**

### Первоначальная настройка

1. **Клонирование репозитория:**
   ```bash
   git clone https://github.com/gc-lover/EvolutionFantasy.git
   cd EvolutionFantasy
   ```

2. **Запуск Setup:**
   ```bash
   # Запустить GenerateProjectFiles.bat
   # Или через командную строку:
   .Engine\Binaries\DotNET\UnrealBuildTool.exe -projectfiles -project="SoloGama/SoloGama.uproject"
   ```

3. **Открытие проекта:**
   - Запустить `SoloGama.uproject`
   - Дождаться компиляции шейдеров

### Структура кода

#### Основные модули:
```
Source/
├── SoloGama/               # Основной модуль
│   ├── Private/           # Приватные классы
│   ├── Public/            # Публичные заголовки
│   ├── Characters/        # Персонажи
│   ├── Abilities/         # Способности
│   ├── Items/             # Предметы
│   └── World/             # Мир игры
```

#### Правила именования:
- **Классы**: `U[Prefix][Name]` (UAbilitySystem, UCharacterBase)
- **Акторы**: `A[Name]` (ACharacter, AWeapon)
- **Компоненты**: `[Name]Component` (AbilityComponent)
- **Перечисления**: `E[Name]` (EAbilityType, EElementType)

## Рабочий процесс

### Ежедневная разработка

1. **Обновление репозитория:**
   ```bash
   git pull origin main
   ```

2. **Создание ветки:**
   ```bash
   git checkout -b feature/[feature-name]
   ```

3. **Работа в Cursor:**
   - Использование команд агентов для генерации кода
   - Следование правилам из `.cursor/rules/`
   - Документирование изменений

4. **Коммит изменений:**
   ```bash
   git add .
   git commit -m "feat: [описание изменения]"
   git push origin feature/[feature-name]
   ```

### Code Review

- Все изменения проходят review
- Минимум 2 аппрува для критических систем
- Автоматические проверки качества
- Тестирование перед мерджем

## Тестирование

### Типы тестов:
- **Unit тесты**: Для отдельных систем
- **Integration тесты**: Для взаимодействия систем
- **Performance тесты**: На целевых платформах
- **Playtesting**: С реальными игроками

### Запуск тестов:
```bash
# В UE Editor: Window → Test Automation
# Или через командную строку:
RunUAT BuildCookRun -project="SoloGama/SoloGama.uproject" -targetplatform=Win64 -clientconfig=Development -build -cook -stage -pak -archive
```

## Документация

### Обновление документации:
- Все изменения документируются
- Использование стандартизированного формата
- Добавление примеров использования
- Поддержание актуальности

### Структура документации:
```
docs/
├── project/                 # Концепция, roadmap
├── architecture/            # Техническая архитектура
├── game_design/             # Игровой дизайн
├── development/             # Гайды по разработке
└── cursor/                  # Cursor IDE настройки
```

## Troubleshooting

### Распространенные проблемы:

#### 1. Ошибки компиляции
```
Решение: Очистить Intermediate/ и Binaries/
Действия:
- Закрыть UE Editor
- Удалить папки Intermediate/ и Binaries/
- Перегенерировать project files
- Перезапустить UE Editor
```

#### 2. Проблемы с Git LFS
```
Решение: Проверить установку Git LFS
Команды:
git lfs install
git lfs pull
```

#### 3. Недостаточно памяти
```
Решение: Увеличить размер виртуальной памяти
Или: Использовать более производительный ПК
```

### Получение помощи:
- **Документация**: `docs/development/troubleshooting.md`
- **Команда**: Создать issue в GitHub
- **Сообщество**: Discord/Forum

## Следующие шаги

1. **Изучить документацию** проекта
2. **Освоить команды Cursor** для генерации кода
3. **Познакомиться с архитектурой** игры
4. **Начать разработку** первой фичи

---

*"От идеи к реализации - шаг за шагом!"*