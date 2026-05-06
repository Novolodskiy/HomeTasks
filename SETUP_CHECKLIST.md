# HomeTasks — Чек-лист настройки инструментов

**Цель документа:** пошаговый план настройки всех инструментов и аккаунтов до начала разработки. Делать в указанном порядке.

---

## Срочность

| Что | Срочность | Время на настройку |
|---|---|---|
| Apple Developer аккаунт | 🔴 **СРОЧНО** (проверка до 2 недель) | 30 мин подача + ожидание |
| Зарубежная карта для оплаты | 🔴 **СРОЧНО** (нужно для всех платных сервисов) | 1-2 недели |
| Jira + MCP | 🟡 До декомпозиции backlog | 1 час |
| GitHub репозиторий | 🟢 Перед первой задачей кодирования | 15 минут |
| Supabase проекты | 🟢 Перед первой задачей кодирования | 15 минут |
| Google Play Developer | 🟢 За 1-2 недели до первого билда | 30 минут |
| OpenAI / Anthropic API | 🟢 Перед задачами голосового ввода | 30 минут |
| EAS Build | 🟢 Перед первой сборкой билда | 15 минут |
| Проверка имени HomeTasks | 🟡 До регистрации Apple Developer | 30 минут |

---

## 1. Проверка доступности имени HomeTasks

Перед регистрацией в Apple Developer и покупкой домена убедитесь, что имя свободно.

### Что проверить

- [ ] Домены: `hometasks.com`, `hometasks.app`, `hometasks.io`, `hometasks.family`
  - Через [Namecheap](https://namecheap.com) или [Cloudflare Registrar](https://cloudflare.com/products/registrar/)
- [ ] App Store: поиск «HomeTasks» в App Store на iPhone — есть ли точно совпадающие приложения?
- [ ] Google Play: то же самое в Play Store
- [ ] Товарный знак: проверить на [TMView](https://www.tmview.europa.eu) и [Rospatent](https://rospatent.gov.ru)
- [ ] Соцсети: `@hometasks` в Twitter, Instagram, TikTok

### Если имя занято

Возможные альтернативы (предлагал ранее в обсуждении):
- Hearth, Nest, Kin, Tide, Beam, Pace, Tally, Knot
- Toga, Tova, Nara, Mira, Lumi, Domi

---

## 2. Зарубежная карта (если нет)

Все платные сервисы (Apple, Google, OpenAI, Anthropic, Supabase Pro, Stripe) требуют зарубежную карту, российские карты не принимаются.

### Варианты

- **Freedom Finance Bank (Казахстан)** — самый популярный путь у российских разработчиков. Открывается удалённо, занимает ~1 неделю.
- **Wise / Revolut** — если есть зарубежная резиденция или счёт
- **Карта в Армении / Грузии / Турции** — если есть возможность выехать или связи
- **Банк Pyypl, Easy Card** — виртуальные карты-перепродавцы (риск что сервис заблокирует)

Без этого нельзя:
- Зарегистрироваться в Apple Developer ($99/год)
- Зарегистрироваться в Google Play ($25 разово)
- Платить за Supabase Pro
- Платить за OpenAI / Anthropic API

---

## 3. Apple Developer аккаунт ($99/год)

🔴 **СРОЧНО** — регистрация и проверка занимают до 2 недель. Без аккаунта невозможно собирать билды для iPhone.

### Шаги

- [ ] Открыть https://developer.apple.com/programs/enroll/
- [ ] Войти под своим Apple ID (или создать новый)
- [ ] Выбрать тип аккаунта: **Individual** (физическое лицо) или **Organization** (юр. лицо)
- [ ] Заполнить данные (паспорт, адрес, телефон)
- [ ] Оплатить $99 зарубежной картой
- [ ] Дождаться проверки (от 1 дня до 2 недель)

### После одобрения

- [ ] Зайти в App Store Connect
- [ ] Создать App ID для `com.hometasks` (production), `com.hometasks.master` (стейдж)
- [ ] Создать Provisioning Profiles
- [ ] Сгенерировать API Key для EAS Build (Issuer ID, Key ID, .p8 файл)

Эти данные понадобятся системному аналитику для настройки EAS Build.

---

## 4. Google Play Developer аккаунт ($25 разово)

🟢 За 1-2 недели до планируемого первого билда.

### Шаги

- [ ] Открыть https://play.google.com/console/signup
- [ ] Войти под Google аккаунтом
- [ ] Тип: **Individual**
- [ ] Заполнить данные
- [ ] Оплатить $25 зарубежной картой
- [ ] Дождаться проверки (часы)

### После одобрения

- [ ] Создать App в Play Console (`HomeTasks`)
- [ ] Подготовить Service Account для EAS submit (нужен JSON файл с ключом)

### Важно (новое требование 2024+)

Google требует от новых аккаунтов **закрытое тестирование с минимум 12 тестерами в течение 14 дней** перед первой публикацией. Заранее найти 12 тестеров среди семьи и друзей — потребуется их Gmail адреса.

---

## 5. Jira (Free tier, $0)

🟡 До декомпозиции backlog.

### Шаги

- [ ] Открыть https://www.atlassian.com/software/jira/free
- [ ] Зарегистрироваться (свой email или новый)
- [ ] Выбрать **Free tier** (без оплаты)
- [ ] Создать новый workspace, например `hometasks.atlassian.net`

### Создать проект

- [ ] Project name: `HomeTasks`
- [ ] Project key: `HT`
- [ ] Type: **Software Development**
- [ ] Template: **Kanban** (проще чем Scrum)

### Создать пользователей (User Management → Invite User)

- [ ] **Дмитрий (вы)** — основной аккаунт, role: Admin
- [ ] **Claude Analyst** — отдельный пользователь с email типа `your-name+claude@gmail.com`
- [ ] **Agent-1** — пользователь для разработчика-агента, email типа `your-name+agent1@gmail.com`

(Gmail распознаёт `+` как алиасы — все приходят на ваш основной адрес, но в Atlassian это разные пользователи. Free tier держит до 10.)

### Создать API tokens

Для каждого пользователя:
- [ ] Войти под ним в Jira
- [ ] Account Settings → Security → API tokens
- [ ] Create API token, имя «HomeTasks MCP»
- [ ] Сохранить токен (показывается один раз)

Сохранить:
- Email + token для Claude Analyst
- Email + token для Agent-1
- URL workspace (например, `https://hometasks.atlassian.net`)

### Создать тикет HT-1: Agent Communication Hub

- [ ] Issue Type: Task
- [ ] Summary: `Agent Communication Hub`
- [ ] Description: «Здесь агенты пишут статусы, когда нет активных задач, или когда что-то непонятно. Это общий чат команды.»
- [ ] Status: In Progress (всегда)
- [ ] Assignee: Claude Analyst

### Настроить Automation Rules

Project Settings → Automation:

- [ ] **Email при Done:** Trigger «Issue transitioned to Done» → Action «Send email» к Claude Analyst
- [ ] **Email при Testing:** Trigger «Issue transitioned to Testing» → Email Дмитрию (для тестирования)
- [ ] **Email при комментарии в HT-1:** Trigger «Comment added to issue» (filter: Issue = HT-1) → Email Claude Analyst
- [ ] **Email при упоминании analyst:** Trigger «Comment added» containing `@analyst` → Email Claude Analyst

---

## 6. MCP-сервер для Jira

После настройки Jira — установить MCP-сервер.

### Рекомендуемый: `mcp-atlassian` (community)

- [ ] Открыть https://github.com/sooperset/mcp-atlassian
- [ ] Установить:
  ```bash
  npm install -g mcp-atlassian
  ```
- [ ] Открыть файл конфигурации Claude Code:
  - macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`
  - Или через UI настроек Claude Code
- [ ] Добавить блок:
  ```json
  {
    "mcpServers": {
      "atlassian": {
        "command": "mcp-atlassian",
        "env": {
          "JIRA_URL": "https://hometasks.atlassian.net",
          "JIRA_USERNAME": "your-name+claude@gmail.com",
          "JIRA_API_TOKEN": "ваш-claude-api-token"
        }
      }
    }
  }
  ```
- [ ] Перезапустить Claude Code
- [ ] Проверить подключение: спросить Claude «дай список тикетов проекта HT»

---

## 7. GitHub репозиторий

🟢 Перед первой задачей кодирования.

### Шаги

- [x] Зарегистрироваться или войти на https://github.com — **готово**
- [x] Create new repository — **готово:** https://github.com/Novolodskiy/HomeTasks
  - Name: `HomeTasks`
  - Visibility: **Public** (можно сменить на Private в Settings → Change visibility если нужно)
  - Главная ветка: `main`

### Branch protection для main

- [x] Settings → Branches → Branch protection rules — **настроено через gh CLI:**
  - ✅ Require a pull request before merging
  - ✅ Require approvals: 1
  - ✅ Dismiss stale reviews on push
  - ✅ Block force pushes
  - ✅ Block deletions
  - Enforce_admins: false (admin может обходить — для одного разработчика удобно)

### GitHub Actions (CI)

Будет настраиваться в первой задаче `HT-2: Setup проекта`. Пока ничего делать не нужно.

### GitHub MCP (опционально)

Можно подключить GitHub MCP-сервер для управления PR из Claude Code:
- https://github.com/modelcontextprotocol/servers/tree/main/src/github

---

## 8. Supabase проекты

🟢 Перед первой задачей кодирования.

### Создать два проекта

- [ ] Зайти на https://supabase.com и зарегистрироваться (Google OAuth)
- [ ] Free tier — без карты
- [ ] Create New Project:
  - Name: `hometasks-stage`
  - Region: **Frankfurt (Europe West)** — оптимально для русскоязычной аудитории
  - Database password: **сохранить в безопасном месте**
- [ ] Подождать 2-3 минуты пока проект инициализируется
- [ ] Повторить для второго проекта:
  - Name: `hometasks-prod`
  - Тот же регион, та же логика

### Сохранить ключи каждого проекта

В Project Settings → API:
- **Project URL** (например, `https://abcde.supabase.co`)
- **anon (public) key** — публичный, можно зашить в приложение
- **service_role (secret) key** — секретный, **только для сервера**

### Установить Supabase CLI локально

```bash
brew install supabase/tap/supabase
```

Логин:
```bash
supabase login
```

### Связать локальный проект (когда будет код)

Будет в первой задаче `HT-2`.

---

## 9. OpenAI и Anthropic API

🟢 Перед задачами голосового ввода (эпик 4).

### OpenAI

- [ ] Открыть https://platform.openai.com
- [ ] Зарегистрироваться (зарубежная карта обязательна)
- [ ] Пополнить баланс на $5-10 для старта
- [ ] Settings → API keys → Create new key
- [ ] **Сохранить ключ** — показывается один раз
- [ ] Установить лимит расходов (Settings → Limits): $20/мес для безопасности на старте

### Anthropic

- [ ] Открыть https://console.anthropic.com
- [ ] Зарегистрироваться (зарубежная карта обязательна)
- [ ] Пополнить баланс на $5-10
- [ ] Settings → API Keys → Create Key
- [ ] **Сохранить ключ**
- [ ] Установить лимит расходов

Эти ключи попадут в **Supabase secrets** для Edge Function, не в код приложения.

---

## 10. EAS Build (Expo)

🟢 Перед первой сборкой.

### Шаги

- [ ] Зарегистрироваться на https://expo.dev (бесплатно)
- [ ] Установить CLI:
  ```bash
  npm install -g eas-cli
  ```
- [ ] Логин:
  ```bash
  eas login
  ```

Free tier: 30 сборок в месяц. На старте этого хватит. Дальше — $30/мес если не хватит.

---

## 11. Подключение Apple/Google к EAS

После того как Apple Developer одобрен и Google Play зарегистрирован:

### Apple

- [ ] Сгенерировать App Store Connect API Key (раздел 3, шаг «После одобрения»)
- [ ] Сохранить:
  - Issuer ID
  - Key ID
  - .p8 файл

### Google

- [ ] Создать Service Account в Google Cloud Console
- [ ] Сохранить JSON-ключ

Эти ключи понадобятся для команды `eas submit` (автоматическая публикация в сторы). Будут использоваться в задачах эпика 8 «Подготовка беты».

---

## 12. После всех настроек — отправить системному аналитику

Когда всё настроено, пришлите системному аналитику следующее:

### Jira
- URL workspace (`https://hometasks.atlassian.net`)
- Project key (`HT`)
- API tokens для пользователей Claude Analyst и Agent-1
- Email-адреса этих пользователей

### Supabase
- URL и anon key для **stage** проекта
- URL и anon key для **prod** проекта
- (service_role keys — НЕ присылать публично, кладите в Supabase secrets через CLI)

### GitHub
- URL репозитория
- Личный access token с правами на репо (для создания PR через MCP)

### Apple / Google (когда готовы)
- Issuer ID, Key ID для App Store Connect
- JSON для Google Service Account

После получения этих данных я смогу:
1. Создать структуру backlog в Jira
2. Создать первый эпик и задачи
3. Подготовить системную аналитику в `docs/epics/`
4. Назначить первые задачи агентам

---

## Бюджет в первый год

| Сервис | Стоимость |
|---|---|
| Apple Developer | $99/год |
| Google Play | $25 разово |
| Supabase | $0 (Free tier хватит на бету) |
| OpenAI Whisper API | ~$10-50/мес (зависит от использования) |
| Anthropic Claude Haiku | ~$5-20/мес |
| EAS Build | $0 (Free tier) |
| Jira | $0 (Free tier) |
| GitHub | $0 (Private repos бесплатно) |
| RevenueCat (на платный релиз) | $0 (Free tier до $2.5K MTR) |
| Домен (опционально) | ~$15/год |
| **Итого первый год** | **~$200-500** |

---

**Документ держать актуальным.** Когда что-то настроено — отметить в чек-листе. Когда ситуация меняется (новый сервис, изменение тарифа) — обновить.
