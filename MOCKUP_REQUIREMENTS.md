# HomeTasks — Требования к артефакту макета

**Документ для:** дизайнер (Code Design / другой инструмент / человек-дизайнер)
**Цель:** описать **технические требования к самому файлу/артефакту макета**, чтобы AI-агенты разработки и системный аналитик могли с ним удобно работать.

> **NB:** содержательные требования к дизайну (принципы, экраны, цвета, компоненты, поведение) — в [DESIGN_REQUIREMENTS.md](DESIGN_REQUIREMENTS.md). Этот документ — **только про формат и структуру макета как артефакта**.

---

## 1. Формат файла

**Рекомендуемый:** Figma (cloud, с публичной read-only ссылкой)

**Альтернативы (если Figma недоступна):**
- Penpot — open-source аналог Figma
- Sketch (только macOS) с экспортом в Figma

**Что обязательно:**
- ✅ Cloud-based, доступ по ссылке
- ✅ Read-only ссылка для просмотра без авторизации
- ✅ Поддержка Dev Mode (или аналога) — чтобы можно было копировать стили в код
- ✅ Возможность экспорта (PNG, SVG, JSON-токены)

**Что НЕ подойдёт:**
- ❌ PDF (нельзя извлечь стили в код)
- ❌ Скриншоты в графическом редакторе (Photoshop, GIMP)
- ❌ Closed-source форматы без экспорта

---

## 2. Структура файла

### 2.1 Страницы (Pages)

Файл должен содержать минимум следующие страницы:

| Page | Назначение |
|---|---|
| **🏠 Cover** | Титульная страница: название проекта, версия, статус, дата |
| **🎨 Design Tokens** | Цвета, шрифты, отступы, скругления, тени — все переменные |
| **🧱 Components** | Переиспользуемые компоненты (Button, Input, Avatar, Card и т.д.) |
| **📱 Screens — Auth** | Sign In, Sign Up, Forgot Password |
| **📱 Screens — Main** | Главный экран, секции задач |
| **📱 Screens — Task** | Создание задачи, карточка задачи |
| **📱 Screens — Family** | Семья, добавить члена |
| **📱 Screens — Profile** | Профиль, настройки |
| **📐 Specs (опционально)** | Отступы, размеры, анотации для разработчиков |

### 2.2 Фреймы внутри страниц

Каждый экран — на **отдельном Frame**, не вложенный в группы. Размеры:

- **iPhone 14 Pro** (393×852) — основной размер
- **Опционально:** iPhone SE (375×667) — для проверки на маленьком экране
- **Опционально:** Pixel 7 (412×915) — для проверки на Android

---

## 3. Именование

### 3.1 Имена фреймов экранов

Формат: `{номер}.{категория} - {название}`

Примеры:
```
01.Auth - Sign In
02.Auth - Sign Up
03.Auth - Forgot Password
04.Main - Home
05.Main - Empty State
06.Task - Create Manual
07.Task - Card Detail
08.Family - List
09.Family - Add Member
10.Profile - Main
11.Profile - Change Password
```

### 3.2 Имена компонентов

Формат: `{Категория}/{Вариант}`

Примеры:
```
Button/Primary
Button/Secondary
Button/Danger
Input/Text
Input/Password
Input/Search
Avatar/Small
Avatar/Medium
Avatar/Large
Card/Task
Card/Comment
Icon/Microphone
Icon/Plus
```

### 3.3 Имена слоёв внутри фрейма

- **Без пробелов в начале/конце**
- **Без специальных символов** кроме `/-_`
- **Описательно** (`Submit Button`, не `Group 47`)

---

## 4. Дизайн-токены

Все стили выносятся в **Variables / Styles**. Никаких хардкоженных значений.

### 4.1 Цвета (Color Variables)

Минимальный набор:

```
color/bg/primary           = #FFFFFF (light), #0A0A0A (dark)
color/bg/secondary         = #FAFAFA (light), #1A1A1A (dark)
color/bg/elevated          = #FFFFFF (light), #2A2A2A (dark)

color/text/primary         = #0A0A0A (light), #FAFAFA (dark)
color/text/secondary       = #6B7280 (light), #9CA3AF (dark)
color/text/disabled        = #D1D5DB (light), #4B5563 (dark)

color/accent/primary       = (один синий или зелёный — на ваш выбор)
color/accent/danger        = #EF4444 (для просроченных, удаления)
color/accent/success       = #10B981

color/border/primary       = #E5E7EB (light), #374151 (dark)
```

### 4.2 Шрифты (Text Styles)

```
text/heading/large         (заголовок экрана) — 24-28pt, 600 weight
text/heading/medium        (заголовок секции) — 18-20pt, 600 weight
text/body/large            (основной) — 16pt, 400 weight
text/body/medium           (карточка задачи) — 15pt, 400 weight
text/caption               (даты, мелкое) — 13pt, 400 weight
text/button                (текст кнопки) — 16pt, 500 weight
```

Шрифт: **System Font** (San Francisco на iOS, Roboto на Android).

### 4.3 Отступы (Spacing Variables)

```
spacing/xs        = 4
spacing/sm        = 8
spacing/md        = 12
spacing/lg        = 16
spacing/xl        = 24
spacing/2xl       = 32
spacing/3xl       = 48
```

### 4.4 Скругления (Corner Radius Variables)

```
radius/sm         = 6
radius/md         = 12
radius/lg         = 16
radius/full       = 9999 (для круглых аватаров)
```

### 4.5 Тени (Shadow Variables)

```
shadow/sm         (для кнопок и карточек)
shadow/md         (для модалок)
shadow/lg         (для overlay типа push-to-talk)
```

### 4.6 Экспорт токенов

Дополнительно: токены экспортируются в **JSON-файл** (через плагин Figma Tokens или встроенный экспорт), чтобы потом импортировать в NativeWind / Tailwind config:

```json
{
  "color": {
    "bg": { "primary": { "value": "#FFFFFF" } },
    ...
  }
}
```

---

## 5. Auto Layout и адаптивность

### 5.1 Все элементы в Auto Layout

- Кнопки — Auto Layout с padding токенами
- Карточки — Auto Layout вертикальный
- Формы — Auto Layout вертикальный с gap
- Списки — Auto Layout вертикальный

### 5.2 Constraints для адаптивности

- Главный контейнер экрана — `Fill container` по ширине
- Header — `Pinned to top`
- FAB-кнопки — `Pinned to bottom right`
- Списки — `Fill container` с прокруткой

### 5.3 Safe Areas

На каждом фрейме обозначены:
- Top safe area (под челкой / индикаторами)
- Bottom safe area (над home indicator)

Можно через layer `Safe Area Top` / `Safe Area Bottom` с фиксированной высотой.

---

## 6. Компоненты (Component Instances)

### 6.1 Все переиспользуемые элементы — компоненты

- Кнопки — компонент `Button` с вариантами (Primary, Secondary, Danger)
- Поля ввода — компонент `Input` с состояниями
- Аватары — компонент `Avatar` с размерами
- Карточка задачи в списке — компонент `TaskCardListItem`
- Карточка комментария — компонент `CommentCard`
- Иконки — каждая иконка отдельный компонент

### 6.2 Не копировать вручную

Если на двух экранах одна и та же кнопка — это **instance** одного компонента, не две независимые копии. Изменение мастера автоматически меняет на всех экранах.

### 6.3 Пропсы компонентов (Component Properties)

Использовать Component Properties для вариантов:
- `Button` → property `variant` (primary/secondary/danger), `size` (sm/md/lg), `state` (default/hover/disabled)
- `Input` → property `state` (default/focus/error/disabled), `hasIcon` (boolean)

---

## 7. Состояния каждого экрана

Для каждого экрана из раздела 5 [DESIGN_REQUIREMENTS.md](DESIGN_REQUIREMENTS.md) должны быть отдельные фреймы для всех состояний:

| Состояние | Когда показывается |
|---|---|
| **Default** | Стандартное отображение с данными |
| **Loading** | Когда данные загружаются (skeleton screens) |
| **Empty** (только если PO просил) | Когда данных нет — НЕ требуется по нашему PRD, но может быть для тестирования |
| **Error** | Когда запрос упал |
| **Offline** | С баннером «Нет интернета» |

Имя фрейма с состоянием: `04.Main - Home (Loading)`, `04.Main - Home (Error)`.

---

## 8. Прототипирование (связи между экранами)

В Figma Prototype mode настроены связи:

- Sign In → Sign Up (по ссылке «Зарегистрироваться»)
- Sign In → Forgot Password (по ссылке «Забыли пароль»)
- Sign Up → Main Screen (после успешной регистрации)
- Main Screen → Task Card (по тапу на задачу)
- Main Screen → Create Task Manual (по кнопке «+»)
- Main Screen → Profile (по тапу на свой аватар)
- Main Screen → Family (по тапу на чужой аватар)
- Family → Add Member (по кнопке «Добавить»)

Это нужно чтобы агент мог проследить **флоу пользователя** и понять навигацию.

---

## 9. Экспорт ассетов

### 9.1 Иконки

- Формат: **SVG**
- Имена: `icon-microphone.svg`, `icon-plus.svg`, `icon-arrow-back.svg`
- Размер: 24×24 (стандарт)

### 9.2 Изображения (если будут)

- Формат: **PNG** или **WebP**
- Размеры: **1x, 2x, 3x** для retina-дисплеев
- Имена: `image-onboarding-1@2x.png`, `image-onboarding-1@3x.png`

### 9.3 Иллюстрации (если будут)

- Предпочтительно SVG (масштабируемо)
- Альтернативно — PNG с альфа-каналом

### 9.4 Где экспорт

Все ассеты для экспорта помечены **Export Settings** в Figma — чтобы можно было одним кликом выгрузить весь набор.

---

## 10. Тёмная и светлая темы

### 10.1 Обе темы в одном файле

Через **Figma Variables Modes**:

```
Light Mode  ← color/bg/primary = #FFFFFF
Dark Mode   ← color/bg/primary = #0A0A0A
```

Каждый фрейм автоматически переключается между темами через Mode Switcher.

### 10.2 Оба варианта на каждом экране

Опционально: для каждого экрана два фрейма — один светлый, один тёмный, рядом для визуального сравнения.

---

## 11. Аннотации и спецификации

### 11.1 Анотации к экранам

На каждом экране (или отдельной странице Specs) — текстовые заметки:

- Какие поля обязательные / опциональные
- Что происходит при тапе на каждый элемент
- Триггеры анимаций
- Условия отображения (например, кнопка «Удалить» только у создателя)
- Связь с тикетами Jira (когда будут — `HT-12`)

### 11.2 Спецификации для разработки

Через Figma Dev Mode разработчик может:
- Видеть точные размеры и отступы
- Копировать CSS / React Native стили
- Видеть имена цветов и шрифтов из токенов

Дизайнер должен убедиться что Dev Mode корректно показывает значения (то есть все стили — токены, не хардкод).

---

## 12. Доступ для агентов

### 12.1 Read-only ссылка

Файл должен быть доступен по **публичной read-only ссылке**:

```
https://www.figma.com/design/XXXXX/HomeTasks?node-id=...
```

Эту ссылку добавить в:
- `README.md` проекта
- `DESIGN_REQUIREMENTS.md`
- В тикеты Jira как ссылку на дизайн

### 12.2 Возможность копирования стилей

Через Figma Dev Mode (входит в Free план для read-only доступа) разработчик / агент может:
- Скопировать цвета как hex или Tailwind classes
- Скопировать отступы
- Скопировать структуру Auto Layout как React/RN компонент

### 12.3 MCP-сервер для Figma (опционально, для агентов)

Если есть Figma API token — можно настроить **Figma MCP-сервер**, чтобы агенты могли программно читать дизайн:
- https://github.com/GLips/Figma-Context-MCP

Это даст возможность агенту сказать «дай мне разметку экрана Sign In» — и получить структуру в JSON.

---

## 13. Версионирование

### 13.1 История версий в Figma

Включена автоматически. После каждого крупного изменения — **создать Named Version** через Version History:

```
v0.1 — Initial mockups
v0.2 — Updated voice recording overlay
v1.0 — Approved for development
```

### 13.2 Связь с тикетами

Если макет меняется по запросу из Jira — указать в Named Version номер тикета: `v1.1 — HT-25 fix archive section`.

---

## 14. Передача в разработку

Когда макет готов — дизайнер делает следующее:

1. Создаёт Named Version `v1.0 — Approved for development`
2. Делает экспорт всех иконок (SVG) и изображений в zip-архив
3. Делает экспорт design tokens в JSON-файл
4. Шарит read-only ссылку на Figma
5. Передаёт всё в `docs/design/` папку проекта (опционально, как backup)

---

## 15. Чек-лист для дизайнера

Перед передачей в разработку убедиться:

**Структура:**
- [ ] Все 9+ экранов на отдельных Frames
- [ ] Каждое состояние экрана (default/loading/error) на отдельном Frame
- [ ] Frames организованы по страницам (Auth / Main / Task / Family / Profile)
- [ ] Имена Frames следуют формату `{номер}.{категория} - {название}`

**Стили:**
- [ ] Все цвета — через Color Variables, нет хардкода
- [ ] Все шрифты — через Text Styles, нет хардкода
- [ ] Отступы и скругления — через Variables
- [ ] Тёмная и светлая темы настроены через Modes

**Компоненты:**
- [ ] Все переиспользуемые элементы — Components с Properties
- [ ] Никаких копий компонентов — только instances

**Auto Layout:**
- [ ] Все списки и формы в Auto Layout
- [ ] Safe Areas обозначены
- [ ] Адаптивность через Constraints

**Прототипирование:**
- [ ] Связи между экранами настроены
- [ ] Можно проследить флоу пользователя через Prototype Mode

**Экспорт:**
- [ ] Иконки настроены на экспорт SVG
- [ ] Design tokens экспортированы в JSON
- [ ] Ассеты настроены на экспорт в нужных форматах

**Доступ:**
- [ ] Файл публичный по read-only ссылке
- [ ] Dev Mode работает корректно
- [ ] Ссылка добавлена в README.md проекта

---

**Этот документ описывает только техническое устройство макета. Содержательные требования (что должно быть на экране, какое поведение, какие состояния) — в DESIGN_REQUIREMENTS.md.**
