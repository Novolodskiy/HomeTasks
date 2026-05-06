# HomeTasks — Design Handoff

Эта папка предназначена для дизайн-артефактов от Code Design.

## Ожидаемая структура (после получения handoff-пакета)

```
docs/design/
├── README.md                     ← этот файл
├── prototype/                    ← живой HTML/JSX прототип
│   ├── index.html
│   ├── app.jsx
│   └── *.jsx
├── tokens/
│   ├── tokens.json               ← нейтральный формат
│   └── tokens.ts                 ← типизированный для Expo/TS
├── components.md                 ← список компонентов с props и состояниями
├── flows.md                      ← карта экранов: тап → переход
├── screens/                      ← скриншоты ключевых экранов
│   ├── 01-home.png
│   ├── 02-create-task.png
│   └── ...
└── assets/
    ├── icons/                    ← SVG-иконки отдельными файлами
    └── images/                   ← растровые ассеты (если есть)
```

## Как пользоваться

**При разработке:**
1. Открыть `prototype/index.html` в браузере — живой кликабельный референс
2. Импортировать `tokens/tokens.ts` напрямую в Expo-проект
3. Использовать `components.md` как спецификацию props компонентов
4. Использовать `flows.md` для понимания навигации
5. Иконки из `assets/icons/` — через `react-native-svg`

**Маппинг HTML → React Native:**
- `div` → `View`
- `span` / `p` / `h*` → `Text`
- `button` → `Pressable` или `TouchableOpacity`
- CSS / inline-style → NativeWind classes (см. tokens) или `StyleSheet.create`

Прототип — это **визуальная и поведенческая спецификация**, не готовый код для копи-паста. Все стили и логика переписываются под React Native + NativeWind.

## Версии

История версий ведётся через git-теги в этом репозитории. Финальные версии помечаются:
- `design/v1.0` — initial approved mockup
- `design/v1.1` — first iteration after dev feedback
- ...
