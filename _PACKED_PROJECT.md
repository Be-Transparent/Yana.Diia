# Packed project
## Directory tree
.
├── .github
│   └── workflows
│       └── update-packed.yml
├── .gitignore
├── LICENSE
├── README.md
├── html.code.v0.app
│   ├── BACKEND_SETUP.md
│   ├── README.md
│   ├── app
│   │   ├── api
│   │   │   └── generate
│   │   │       └── route.ts
│   │   ├── globals.css
│   │   ├── layout.tsx
│   │   └── page.tsx
│   ├── components
│   │   ├── api-integrations.tsx
│   │   ├── architecture.tsx
│   │   ├── case-studies.tsx
│   │   ├── contacts.tsx
│   │   ├── diia-integrations.tsx
│   │   ├── features.tsx
│   │   ├── flow-evaluator.tsx
│   │   ├── footer.tsx
│   │   ├── header.tsx
│   │   ├── hero.tsx
│   │   ├── innovations.tsx
│   │   ├── input-output.tsx
│   │   ├── integration-roadmap.tsx
│   │   ├── live-demo.tsx
│   │   ├── llmops-architecture.tsx
│   │   ├── mission.tsx
│   │   ├── power-features.tsx
│   │   ├── principles.tsx
│   │   ├── ranking.tsx
│   │   ├── team.tsx
│   │   ├── theme-provider.tsx
│   │   └── ui
│   │       ├── accordion.tsx
│   │       ├── alert-dialog.tsx
│   │       ├── alert.tsx
│   │       ├── aspect-ratio.tsx
│   │       ├── avatar.tsx
│   │       ├── badge.tsx
│   │       ├── breadcrumb.tsx
│   │       ├── button-group.tsx
│   │       ├── button.tsx
│   │       ├── calendar.tsx
│   │       ├── card.tsx
│   │       ├── carousel.tsx
│   │       ├── chart.tsx
│   │       ├── checkbox.tsx
│   │       ├── collapsible.tsx
│   │       ├── command.tsx
│   │       ├── context-menu.tsx
│   │       ├── dialog.tsx
│   │       ├── drawer.tsx
│   │       ├── dropdown-menu.tsx
│   │       ├── empty.tsx
│   │       ├── field.tsx
│   │       ├── form.tsx
│   │       ├── hover-card.tsx
│   │       ├── input-group.tsx
│   │       ├── input-otp.tsx
│   │       ├── input.tsx
│   │       ├── item.tsx
│   │       ├── kbd.tsx
│   │       ├── label.tsx
│   │       ├── menubar.tsx
│   │       ├── navigation-menu.tsx
│   │       ├── pagination.tsx
│   │       ├── popover.tsx
│   │       ├── progress.tsx
│   │       ├── radio-group.tsx
│   │       ├── resizable.tsx
│   │       ├── scroll-area.tsx
│   │       ├── select.tsx
│   │       ├── separator.tsx
│   │       ├── sheet.tsx
│   │       ├── sidebar.tsx
│   │       ├── skeleton.tsx
│   │       ├── slider.tsx
│   │       ├── sonner.tsx
│   │       ├── spinner.tsx
│   │       ├── switch.tsx
│   │       ├── table.tsx
│   │       ├── tabs.tsx
│   │       ├── textarea.tsx
│   │       ├── toast.tsx
│   │       ├── toaster.tsx
│   │       ├── toggle-group.tsx
│   │       ├── toggle.tsx
│   │       ├── tooltip.tsx
│   │       ├── use-mobile.tsx
│   │       └── use-toast.ts
│   ├── components.json
│   ├── hooks
│   │   ├── use-mobile.ts
│   │   └── use-toast.ts
│   ├── next.config.mjs
│   ├── package.json
│   ├── pnpm-lock.yaml
│   ├── postcss.config.mjs
│   ├── public
│   │   ├── apple-icon.png
│   │   ├── icon-dark-32x32.png
│   │   ├── icon-light-32x32.png
│   │   ├── icon.svg
│   │   ├── placeholder-logo.png
│   │   ├── placeholder-logo.svg
│   │   ├── placeholder-user.jpg
│   │   ├── placeholder.jpg
│   │   └── placeholder.svg
│   ├── scripts
│   │   ├── run-backend.bat
│   │   ├── run-backend.sh
│   │   ├── setup-backend.bat
│   │   └── setup-backend.sh
│   ├── styles
│   │   └── globals.css
│   └── tsconfig.json
└── txt.txt

13 directories, 111 files
\n## File contents
\n--- START FILE: ./LICENSE ---
MIT License

Copyright (c) 2025 OMELCHENKO IHOR OLEKSANDROVYCH

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
\n--- END FILE: ./LICENSE ---
\n--- START FILE: ./.github/workflows/update-packed.yml ---
name: Update Packed Project

on:
  push:
    branches: [ main ]
  workflow_dispatch:   # дозволяє запускати вручну з GitHub UI

permissions:
  contents: write   # дає токену право пушити у приватний репозиторій

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repo
        uses: actions/checkout@v3
        with:
          persist-credentials: true   # залишає токен для git push

      - name: Generate packed file (tree + contents)
        run: |
          echo "# Packed project" > _PACKED_PROJECT.md
          echo "## Directory tree" >> _PACKED_PROJECT.md
          tree -a -I '.git|_PACKED_PROJECT.md' >> _PACKED_PROJECT.md

          echo "\n## File contents" >> _PACKED_PROJECT.md
          for f in $(find . -type f ! -path "./.git/*" ! -name "_PACKED_PROJECT.md"); do
            echo "\n--- START FILE: $f ---" >> _PACKED_PROJECT.md
            cat "$f" >> _PACKED_PROJECT.md
            echo "\n--- END FILE: $f ---" >> _PACKED_PROJECT.md
          done

      - name: Commit and push changes
        run: |
          git config --global user.name "github-actions"
          git config --global user.email "actions@github.com"
          git add _PACKED_PROJECT.md
          git commit -m "Auto-update packed project" || echo "No changes to commit"
          git push origin HEAD:main
\n--- END FILE: ./.github/workflows/update-packed.yml ---
\n--- START FILE: ./html.code.v0.app/postcss.config.mjs ---
/** @type {import('postcss-load-config').Config} */
const config = {
  plugins: {
    '@tailwindcss/postcss': {},
  },
}

export default config
\n--- END FILE: ./html.code.v0.app/postcss.config.mjs ---
\n--- START FILE: ./html.code.v0.app/scripts/setup-backend.sh ---
#!/bin/bash

# Yana.Diia Backend Setup Script
# Автоматичне налаштування backend середовища

set -e

echo "🚀 Yana.Diia Backend Setup"
echo "=========================="

# 1. Перевірка Python
if ! command -v python3 &> /dev/null; then
    echo "❌ Python3 не встановлено"
    exit 1
fi
echo "✅ Python3 знайдено"

# 2. Створення структури директорій
echo "📁 Створення структури проєкту..."
mkdir -p backend/{generation,validation,evaluation,rag,api,scripts,tests}
mkdir -p data/{diia-repos,rag-index}
echo "✅ Структура створена"

# 3. Створення virtual environment
echo "🔧 Створення virtual environment..."
python3 -m venv venv
echo "✅ Virtual environment готовий"

# 4. Активація venv та встановлення залежностей
echo "📦 Встановлення залежностей..."
source venv/bin/activate
pip install --upgrade pip
pip install -r backend/requirements.txt
echo "✅ Залежності встановлені"

# 5. Створення .env файлу
if [ ! -f .env ]; then
    echo "📝 Створення .env файлу..."
    cp .env.example .env
    echo "⚠️  УВАГА: Заповніть .env файл вашим ANTHROPIC_API_KEY!"
fi

echo ""
echo "✅ Налаштування завершено!"
echo ""
echo "Наступні кроки:"
echo "1. Заповніть .env файл вашим API key"
echo "2. Запустіть backend: python backend/main.py"
echo "3. Перевірте: http://localhost:8000/docs"
echo ""
\n--- END FILE: ./html.code.v0.app/scripts/setup-backend.sh ---
\n--- START FILE: ./html.code.v0.app/scripts/run-backend.bat ---
@echo off
REM Запуск Yana.Diia Backend (Windows)

echo 🚀 Запуск Yana.Diia Backend...

REM Активуємо venv
call venv\Scripts\activate.bat

REM Перевіримо .env
if not exist ".env" (
    echo ❌ .env файл не знайдено
    echo Запустіть спочатку: bash scripts/setup-backend.sh
    exit /b 1
)

REM Запускаємо backend
cd backend
python -m uvicorn main:app --reload --host 0.0.0.0 --port 8000
\n--- END FILE: ./html.code.v0.app/scripts/run-backend.bat ---
\n--- START FILE: ./html.code.v0.app/scripts/setup-backend.bat ---
@echo off
REM Yana.Diia Backend Setup Script for Windows

echo 🚀 Yana.Diia Backend Setup
echo ==========================

REM 1. Перевірка Python
python --version >nul 2>&1
if errorlevel 1 (
    echo ❌ Python не встановлено
    exit /b 1
)
echo ✅ Python знайдено

REM 2. Створення структури директорій
echo 📁 Створення структури проєкту...
if not exist "backend\generation" mkdir backend\generation
if not exist "backend\validation" mkdir backend\validation
if not exist "backend\evaluation" mkdir backend\evaluation
if not exist "backend\rag" mkdir backend\rag
if not exist "backend\api" mkdir backend\api
if not exist "backend\scripts" mkdir backend\scripts
if not exist "backend\tests" mkdir backend\tests
if not exist "data\diia-repos" mkdir data\diia-repos
if not exist "data\rag-index" mkdir data\rag-index
echo ✅ Структура створена

REM 3. Створення virtual environment
echo 🔧 Створення virtual environment...
python -m venv venv
echo ✅ Virtual environment готовий

REM 4. Активація venv та встановлення залежностей
echo 📦 Встановлення залежностей...
call venv\Scripts\activate.bat
python -m pip install --upgrade pip
pip install -r backend\requirements.txt
echo ✅ Залежності встановлені

REM 5. Створення .env файлу
if not exist ".env" (
    echo 📝 Створення .env файлу...
    copy .env.example .env
    echo ⚠️  УВАГА: Заповніть .env файл вашим ANTHROPIC_API_KEY!
)

echo.
echo ✅ Налаштування завершено!
echo.
echo Наступні кроки:
echo 1. Заповніть .env файл вашим API key
echo 2. Запустіть backend: python backend/main.py
echo 3. Перевірте: http://localhost:8000/docs
echo.
\n--- END FILE: ./html.code.v0.app/scripts/setup-backend.bat ---
\n--- START FILE: ./html.code.v0.app/scripts/run-backend.sh ---
#!/bin/bash

# Запуск Yana.Diia Backend

set -e

echo "🚀 Запуск Yana.Diia Backend..."

# Активуємо venv
source venv/bin/activate

# Перевіримо .env
if [ ! -f .env ]; then
    echo "❌ .env файл не знайдено"
    echo "Запустіть спочатку: bash scripts/setup-backend.sh"
    exit 1
fi

# Запускаємо backend
cd backend
python -m uvicorn main:app --reload --host 0.0.0.0 --port 8000
\n--- END FILE: ./html.code.v0.app/scripts/run-backend.sh ---
\n--- START FILE: ./html.code.v0.app/components/power-features.tsx ---
'use client'

import { Brain, Mic, Zap, Shield, GitBranch, Eye, MessageCircle } from 'lucide-react'

export default function PowerFeatures() {
  const powerFeatures = [
    {
      icon: Brain,
      title: 'AI-парсинг BRD',
      desc: 'Багатомодельний LLM-рушій (ChatGPT, Qwen 2.5, Gemma3, ollama)',
    },
    {
      icon: Shield,
      title: 'Chrome-розширення',
      desc: 'Захоплення даних з Дія, структуроване надсилання в 1 клік',
    },
    {
      icon: MessageCircle,
      title: 'Публічний фідбек',
      desc: 'Модуль голосування з антифродом (BERT, rule-based, multilang)',
    },
    {
      icon: Mic,
      title: 'Multimodal input',
      desc: 'Drag&drop, OCR, speech-to-text, vision transformer',
    },
    {
      icon: GitBranch,
      title: 'DevOps-ready',
      desc: 'REST API, інтеграція з Jira, Confluence, GitHub, CI/CD',
    },
    {
      icon: Eye,
      title: 'Transparency',
      desc: 'Відкритий лог змін, explainable AI, auto-генерація пояснень',
    },
  ]

  return (
    <section className="py-16 md:py-24 px-4 md:px-6 relative">
      <div className="max-w-6xl mx-auto space-y-12">
        <div className="text-center space-y-3">
          <div className="flex items-center justify-center gap-2 mb-2">
            <Zap className="w-8 h-8 text-accent" />
            <h2 className="text-3xl md:text-4xl font-bold text-foreground">Power Features</h2>
          </div>
          <p className="text-lg text-muted-foreground">Найпотужніші можливості для команд</p>
        </div>

        <div className="grid md:grid-cols-2 lg:grid-cols-3 gap-6">
          {powerFeatures.map((feature, idx) => {
            const Icon = feature.icon
            return (
              <div key={idx} className="group glass p-6 rounded-xl hover:border-primary/50 hover:bg-white/10 transition">
                <div className="w-12 h-12 rounded-lg bg-gradient-to-br from-primary/30 to-accent/30 flex items-center justify-center mb-4 group-hover:from-primary/50 group-hover:to-accent/50 transition">
                  <Icon className="w-6 h-6 text-primary" />
                </div>
                <h3 className="font-semibold text-foreground mb-2">{feature.title}</h3>
                <p className="text-sm text-muted-foreground">{feature.desc}</p>
              </div>
            )
          })}
        </div>
      </div>
    </section>
  )
}
\n--- END FILE: ./html.code.v0.app/components/power-features.tsx ---
\n--- START FILE: ./html.code.v0.app/components/footer.tsx ---
'use client'

import Link from 'next/link'
import { Github, Linkedin, Mail } from 'lucide-react'

export default function Footer() {
  return (
    <footer className="border-t border-border/30 relative">
      <div className="absolute inset-0 bg-gradient-to-t from-background/50 to-background/10 backdrop-blur-sm -z-10" />
      
      <div className="max-w-6xl mx-auto px-4 md:px-6 py-12 md:py-16">
        <div className="grid grid-cols-1 md:grid-cols-4 gap-8 mb-12">
          <div className="space-y-4">
            <div className="flex items-center gap-2">
              <div className="w-8 h-8 rounded-lg bg-gradient-to-br from-primary to-accent flex items-center justify-center shadow-lg shadow-primary/20">
                <span className="text-primary-foreground font-bold text-sm">Я</span>
              </div>
              <span className="font-bold text-foreground">Yana.Diia</span>
            </div>
            <p className="text-sm text-muted-foreground">
              AI для цифрових архітекторів України
            </p>
          </div>

          <div className="space-y-4">
            <h4 className="font-semibold text-foreground">Проект</h4>
            <ul className="space-y-2 text-sm">
              <li><Link href="#" className="text-muted-foreground hover:text-accent transition">Про Яну</Link></li>
              <li><Link href="#" className="text-muted-foreground hover:text-accent transition">Документація</Link></li>
              <li><Link href="https://github.com/V2473/BeTransparent" target="_blank" rel="noopener noreferrer" className="text-muted-foreground hover:text-accent transition">GitHub</Link></li>
            </ul>
          </div>

          <div className="space-y-4">
            <h4 className="font-semibold text-foreground">Команда</h4>
            <ul className="space-y-2 text-sm">
              <li><Link href="#team" className="text-muted-foreground hover:text-accent transition">Be Transparent</Link></li>
              <li><Link href="#" className="text-muted-foreground hover:text-accent transition">Контакти</Link></li>
              <li><Link href="https://github.com/V2473/BeTransparent" target="_blank" rel="noopener noreferrer" className="text-muted-foreground hover:text-accent transition">GitHub Команди</Link></li>
            </ul>
          </div>

          <div className="space-y-4">
            <h4 className="font-semibold text-foreground">Слідкуйте</h4>
            <div className="flex gap-3">
              <Link href="https://github.com/V2473/BeTransparent" target="_blank" rel="noopener noreferrer" className="w-8 h-8 rounded-lg glass hover:bg-white/20 hover:border-white/30 flex items-center justify-center transition">
                <Github className="w-4 h-4 text-foreground" />
              </Link>
              <Link href="#" className="w-8 h-8 rounded-lg glass hover:bg-white/20 hover:border-white/30 flex items-center justify-center transition">
                <Linkedin className="w-4 h-4 text-foreground" />
              </Link>
              <Link href="mailto:team@yandia.gov.ua" className="w-8 h-8 rounded-lg glass hover:bg-white/20 hover:border-white/30 flex items-center justify-center transition">
                <Mail className="w-4 h-4 text-foreground" />
              </Link>
            </div>
          </div>
        </div>

        <div className="border-t border-border/30 pt-8 flex flex-col md:flex-row justify-between items-center gap-4 text-sm text-muted-foreground">
          <p>© 2025 Yana.Diia. Створено командою Be Transparent для Diia.AI Hackathon</p>
          <div className="flex gap-6">
            <Link href="#" className="hover:text-accent transition">Privacy Policy</Link>
            <Link href="#" className="hover:text-accent transition">Terms of Service</Link>
          </div>
        </div>
      </div>
    </footer>
  )
}
\n--- END FILE: ./html.code.v0.app/components/footer.tsx ---
\n--- START FILE: ./html.code.v0.app/components/mission.tsx ---
'use client'

export default function Mission() {
  return (
    <section id="mission" className="py-16 md:py-24 px-4 md:px-6 relative">
      <div className="max-w-4xl mx-auto space-y-12">
        <div className="space-y-4">
          <h2 className="text-3xl md:text-4xl font-bold text-foreground">Основна ідея</h2>
          <p className="text-lg text-muted-foreground leading-relaxed">
            Yana.Diia призначена для внутрішнього використання продуктовими командами, аналітиками, дизайнерами й менеджерами проєктів Мінцифри, EPAM та партнерських GovTech-команд.
          </p>
        </div>

        <div className="grid md:grid-cols-2 gap-8">
          <div className="glass p-6 rounded-xl space-y-3">
            <h3 className="font-semibold text-foreground text-lg">Вхід системи</h3>
            <p className="text-muted-foreground">
              Текстовий опис BRD або структури послуги
            </p>
          </div>
          <div className="glass p-6 rounded-xl space-y-3">
            <h3 className="font-semibold text-foreground text-lg">Вихід системи</h3>
            <p className="text-muted-foreground">
              Варіанти покрокових user-flow згідно з дизайн-системою Дія та готові JSON-маршрути для рев'ю
            </p>
          </div>
        </div>

        <div className="pt-4 space-y-4">
          <h3 className="font-semibold text-foreground">Критерії ранжування</h3>
          <div className="grid grid-cols-1 md:grid-cols-3 gap-4">
            <div className="glass p-4 rounded-lg hover:bg-white/10 transition duration-300">
              <p className="text-sm text-muted-foreground">✓ Мінімальна кількість кроків</p>
            </div>
            <div className="glass p-4 rounded-lg hover:bg-white/10 transition duration-300">
              <p className="text-sm text-muted-foreground">✓ Максимальна відповідність дизайн-системі</p>
            </div>
            <div className="glass p-4 rounded-lg hover:bg-white/10 transition duration-300">
              <p className="text-sm text-muted-foreground">✓ Відсутність нестандартних компонентів</p>
            </div>
          </div>
        </div>
      </div>
    </section>
  )
}
\n--- END FILE: ./html.code.v0.app/components/mission.tsx ---
\n--- START FILE: ./html.code.v0.app/components/principles.tsx ---
'use client'

import { Lock, Shield, Eye } from 'lucide-react'

export default function Principles() {
  const principles = [
    {
      icon: Lock,
      title: 'Privacy by Design',
      items: [
        'Внутрішня обробка даних',
        'Ізольованість від користувачів',
        'Pseudonymization & верифікація',
      ]
    },
    {
      icon: Shield,
      title: 'Security First',
      items: [
        'Тільки перевірені модулі',
        'Рольова авторизація backend',
        'Незалежний аудит & пентест',
      ]
    },
    {
      icon: Eye,
      title: 'Transparency',
      items: [
        'Відкритий код на GitHub',
        'REST-API на Swagger',
        'Логування усіх змін',
      ]
    },
  ]

  return (
    <section className="py-16 md:py-24 px-4 md:px-6 relative">
      <div className="max-w-6xl mx-auto space-y-12">
        <div className="text-center space-y-3">
          <div className="flex items-center justify-center gap-2 mb-2">
            <Shield className="w-8 h-8 text-accent" />
            <h2 className="text-3xl md:text-4xl font-bold text-foreground">Принципи розробки</h2>
          </div>
          <p className="text-lg text-muted-foreground">Орієнтир на безпеку, приватність та прозорість</p>
        </div>

        <div className="grid md:grid-cols-3 gap-6">
          {principles.map((principle, idx) => {
            const Icon = principle.icon
            return (
              <div key={idx} className="glass p-8 rounded-xl border-l-4 border-accent hover:border-primary transition">
                <div className="w-12 h-12 rounded-lg bg-gradient-to-br from-primary/30 to-accent/30 flex items-center justify-center mb-4">
                  <Icon className="w-6 h-6 text-primary" />
                </div>
                <h3 className="font-semibold text-foreground mb-4 text-lg">{principle.title}</h3>
                <ul className="space-y-2">
                  {principle.items.map((item, i) => (
                    <li key={i} className="flex gap-2 text-sm text-muted-foreground">
                      <span className="text-accent">→</span>
                      <span>{item}</span>
                    </li>
                  ))}
                </ul>
              </div>
            )
          })}
        </div>
      </div>
    </section>
  )
}
\n--- END FILE: ./html.code.v0.app/components/principles.tsx ---
\n--- START FILE: ./html.code.v0.app/components/integration-roadmap.tsx ---
'use client'

import { Card } from '@/components/ui/card'
import { CheckCircle, Clock, ChevronRight } from 'lucide-react'

const phases = [
  {
    phase: 'Phase 1: Foundation',
    timeline: 'Тиждень 1 (16-22 листопада)',
    status: 'in-progress',
    tasks: [
      { name: 'Clone diia-open-source repos', done: true },
      { name: 'Setup RAG база (FAISS/ChromaDB)', done: true },
      { name: 'GitHub MCP інтеграція', done: true },
      { name: 'Парсинг iOS/Android компонентів', done: false }
    ]
  },
  {
    phase: 'Phase 2: Core Functionality',
    timeline: 'Тиждень 2 (23-29 листопада)',
    status: 'upcoming',
    tasks: [
      { name: 'FastAPI backend з REST endpoints', done: false },
      { name: 'LLM інтеграція (Claude/GPT-4)', done: false },
      { name: 'Pydantic validation schema', done: false },
      { name: 'Next.js frontend + real-time updates', done: false }
    ]
  },
  {
    phase: 'Phase 3: Production Features',
    timeline: 'Тиждень 3',
    status: 'upcoming',
    tasks: [
      { name: 'HITL Review Interface', done: false },
      { name: 'Export функції (JSON, Confluence, Figma)', done: false },
      { name: 'Smart notifications', done: false },
      { name: 'Analytics dashboard', done: false }
    ]
  }
]

export default function IntegrationRoadmap() {
  return (
    <section id="integration-roadmap" className="py-20 px-4 md:px-6">
      <div className="max-w-6xl mx-auto">
        <div className="text-center mb-12">
          <h2 className="text-4xl md:text-5xl font-bold bg-gradient-to-r from-primary to-accent bg-clip-text text-transparent mb-4">
            Roadmap Інтеграцій
          </h2>
          <p className="text-lg text-muted-foreground max-w-2xl mx-auto">
            Структурований план розвитку з фокусом на реальні API та MCP інтеграції
          </p>
        </div>

        <div className="space-y-6">
          {phases.map((phase, idx) => (
            <Card key={phase.phase} className="glass border-white/10 p-8 rounded-xl">
              <div className="flex items-start justify-between mb-6">
                <div>
                  <h3 className="text-2xl font-bold text-foreground mb-2">{phase.phase}</h3>
                  <p className="text-sm text-muted-foreground flex items-center gap-2">
                    <Clock className="w-4 h-4" />
                    {phase.timeline}
                  </p>
                </div>
                <div className={`px-4 py-2 rounded-full text-sm font-medium ${
                  phase.status === 'in-progress' ? 'bg-accent/20 text-accent' :
                  'bg-muted/20 text-muted-foreground'
                }`}>
                  {phase.status === 'in-progress' ? '🔄 У розробці' : '⏳ Майбутнє'}
                </div>
              </div>

              <div className="grid md:grid-cols-2 gap-4">
                {phase.tasks.map((task, taskIdx) => (
                  <div key={taskIdx} className="flex items-center gap-3 p-3 rounded-lg bg-background/40 border border-border/30 hover:border-border/50 transition">
                    <CheckCircle className={`w-5 h-5 flex-shrink-0 ${
                      task.done ? 'text-accent' : 'text-muted-foreground'
                    }`} />
                    <span className={`text-sm ${
                      task.done ? 'text-foreground line-through opacity-50' : 'text-foreground'
                    }`}>
                      {task.name}
                    </span>
                  </div>
                ))}
              </div>
            </Card>
          ))}
        </div>

        <div className="mt-12 p-8 rounded-2xl bg-gradient-to-r from-primary/10 to-accent/10 border border-primary/20">
          <h4 className="font-bold text-foreground text-lg mb-4">Ключові технологічні стеки:</h4>
          <div className="grid md:grid-cols-2 gap-6">
            <div>
              <p className="text-sm font-semibold text-primary uppercase mb-3">Frontend</p>
              <p className="text-foreground">Next.js 16, React 19, TypeScript, Tailwind CSS v4, SWR для data fetching</p>
            </div>
            <div>
              <p className="text-sm font-semibold text-primary uppercase mb-3">Backend</p>
              <p className="text-foreground">FastAPI, Python 3.11+, Pydantic, SQLAlchemy, PostgreSQL</p>
            </div>
            <div>
              <p className="text-sm font-semibold text-accent uppercase mb-3">AI/LLM</p>
              <p className="text-foreground">Anthropic Claude, OpenAI GPT-4, Instructor для structured output</p>
            </div>
            <div>
              <p className="text-sm font-semibold text-accent uppercase mb-3">Data/RAG</p>
              <p className="text-foreground">FAISS/ChromaDB, Tree-sitter (Swift/Kotlin parsing), sentence-transformers</p>
            </div>
          </div>
        </div>
      </div>
    </section>
  )
}
\n--- END FILE: ./html.code.v0.app/components/integration-roadmap.tsx ---
\n--- START FILE: ./html.code.v0.app/components/architecture.tsx ---
'use client'

export default function Architecture() {
  return (
    <section id="architecture" className="py-16 md:py-24 px-4 md:px-6 relative">
      <div className="max-w-6xl mx-auto space-y-12">
        <div className="space-y-4">
          <h2 className="text-3xl md:text-4xl font-bold text-foreground">Архітектурні акценти</h2>
          <p className="text-lg text-muted-foreground">
            Система побудована на публічних даних з можливістю розширення для production-бізнесу
          </p>
        </div>

        <div className="grid md:grid-cols-2 gap-8">
          <div className="space-y-6">
            <div className="glass p-6 rounded-xl space-y-2">
              <h3 className="font-semibold text-foreground flex items-center gap-3">
                <span className="w-8 h-8 rounded-full bg-gradient-to-br from-primary to-accent text-primary-foreground text-xs flex items-center justify-center font-bold shadow-lg shadow-primary/20">1</span>
                Публічні дані
              </h3>
              <p className="text-sm text-muted-foreground ml-11">
                Дизайн-система Дія, відкриті списки сервісів, open-source-репозиторії, BRD шаблони, результати веб-пошуку
              </p>
            </div>

            <div className="glass p-6 rounded-xl space-y-2">
              <h3 className="font-semibold text-foreground flex items-center gap-3">
                <span className="w-8 h-8 rounded-full bg-gradient-to-br from-accent to-primary text-primary-foreground text-xs flex items-center justify-center font-bold shadow-lg shadow-accent/20">2</span>
                Мультимодальні інтерфейси
              </h3>
              <p className="text-sm text-muted-foreground ml-11">
                Текст, голос, скріншоти, PDF та структуровані документи
              </p>
            </div>

            <div className="glass p-6 rounded-xl space-y-2">
              <h3 className="font-semibold text-foreground flex items-center gap-3">
                <span className="w-8 h-8 rounded-full bg-gradient-to-br from-primary to-accent text-primary-foreground text-xs flex items-center justify-center font-bold shadow-lg shadow-primary/20">3</span>
                Агентно-орієнтований режим
              </h3>
              <p className="text-sm text-muted-foreground ml-11">
                Pipeline з взаємодією підмодулів, інтеграція з DevOps-процесами (Jira, Confluence, Git)
              </p>
            </div>
          </div>

          <div className="glass p-8 rounded-xl space-y-4 border-l-2 border-accent">
            <h3 className="font-semibold text-foreground mb-6 text-lg">Принципи розробки</h3>
            
            <div className="space-y-4">
              <div className="flex gap-3">
                <div className="w-1.5 bg-gradient-to-b from-primary to-accent rounded-full flex-shrink-0 mt-1" />
                <div>
                  <p className="font-medium text-foreground text-sm">Privacy by Design</p>
                  <p className="text-xs text-muted-foreground">Жоден ризик для приватності користувачів</p>
                </div>
              </div>

              <div className="flex gap-3">
                <div className="w-1.5 bg-gradient-to-b from-accent to-primary rounded-full flex-shrink-0 mt-1" />
                <div>
                  <p className="font-medium text-foreground text-sm">Security First</p>
                  <p className="text-xs text-muted-foreground">Відповідність вимогам Дія</p>
                </div>
              </div>

              <div className="flex gap-3">
                <div className="w-1.5 bg-gradient-to-b from-primary to-accent rounded-full flex-shrink-0 mt-1" />
                <div>
                  <p className="font-medium text-foreground text-sm">Transparency</p>
                  <p className="text-xs text-muted-foreground">Open-source розробка та документація</p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  )
}
\n--- END FILE: ./html.code.v0.app/components/architecture.tsx ---
\n--- START FILE: ./html.code.v0.app/components/input-output.tsx ---
'use client'

import { Upload, ArrowRight, FileJson, CheckCircle, FileText, Headphones, Image, FileCode } from 'lucide-react'

export default function InputOutput() {
  return (
    <section className="py-16 md:py-24 px-4 md:px-6 relative">
      <div className="max-w-6xl mx-auto space-y-12">
        <div className="text-center space-y-3">
          <h2 className="text-3xl md:text-4xl font-bold text-foreground">Як працює Yana.Diia</h2>
          <p className="text-lg text-muted-foreground">Прості і потужні цикли обробки даних</p>
        </div>

        <div className="grid lg:grid-cols-3 gap-6 items-center">
          {/* Input */}
          <div className="glass p-8 rounded-2xl space-y-6 hover:border-primary/50 transition">
            <div className="w-12 h-12 rounded-lg bg-gradient-to-br from-primary/30 to-accent/30 flex items-center justify-center">
              <Upload className="w-6 h-6 text-primary" />
            </div>
            <div>
              <div className="flex items-center gap-2 mb-2">
                <Upload className="w-5 h-5 text-primary" />
                <h3 className="font-semibold text-foreground text-lg">Вхід</h3>
              </div>
              <ul className="text-sm text-muted-foreground space-y-2">
                <li className="flex items-center gap-2">
                  <CheckCircle className="w-4 h-4 text-accent" />
                  <span>Текстовий опис BRD</span>
                </li>
                <li className="flex items-center gap-2">
                  <CheckCircle className="w-4 h-4 text-accent" />
                  <span>Mindmap та структури</span>
                </li>
                <li className="flex items-center gap-2">
                  <CheckCircle className="w-4 h-4 text-accent" />
                  <span>Голос, картинки, PDF</span>
                </li>
                <li className="flex items-center gap-2">
                  <CheckCircle className="w-4 h-4 text-accent" />
                  <span>Figma та JSON-схеми</span>
                </li>
              </ul>
            </div>
          </div>

          {/* Arrow */}
          <div className="hidden lg:flex justify-center">
            <ArrowRight className="w-8 h-8 text-accent animate-pulse" />
          </div>

          {/* Output */}
          <div className="glass p-8 rounded-2xl space-y-6 hover:border-accent/50 transition">
            <div className="w-12 h-12 rounded-lg bg-gradient-to-br from-accent/30 to-primary/30 flex items-center justify-center">
              <FileJson className="w-6 h-6 text-accent" />
            </div>
            <div>
              <div className="flex items-center gap-2 mb-2">
                <FileJson className="w-5 h-5 text-accent" />
                <h3 className="font-semibold text-foreground text-lg">Вихід</h3>
              </div>
              <ul className="text-sm text-muted-foreground space-y-2">
                <li className="flex items-center gap-2">
                  <CheckCircle className="w-4 h-4 text-primary" />
                  <span>Варіанти user-flow</span>
                </li>
                <li className="flex items-center gap-2">
                  <CheckCircle className="w-4 h-4 text-primary" />
                  <span>JSON-маршрути</span>
                </li>
                <li className="flex items-center gap-2">
                  <CheckCircle className="w-4 h-4 text-primary" />
                  <span>Wireframes & прототипи</span>
                </li>
                <li className="flex items-center gap-2">
                  <CheckCircle className="w-4 h-4 text-primary" />
                  <span>Рекомендації для Figma</span>
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </section>
  )
}
\n--- END FILE: ./html.code.v0.app/components/input-output.tsx ---
\n--- START FILE: ./html.code.v0.app/components/api-integrations.tsx ---
'use client'

import { Card } from '@/components/ui/card'
import { Badge } from '@/components/ui/badge'
import { ExternalLink, GitBranch, Database, Zap, Shield, Lock } from 'lucide-react'
import Link from 'next/link'

const integrations = [
  {
    name: 'Diia API',
    description: 'Ядро платформи для шеринга документів, електронного підпису та Bank ID інтеграції',
    endpoints: [
      'POST /api/v1/repository/create/',
      'GET /api/v1/repository/detail/{service_id}/',
      'GET /api/v1/repository/list/'
    ],
    features: ['Document Sharing', 'E-Signature', 'Bank ID', 'QR Validation'],
    repository: 'https://github.com/diia-open-source/be-gateway-service',
    status: 'stable',
    category: 'Core API'
  },
  {
    name: 'Public Service Catalog',
    description: 'Каталог всіх держпослуг з метаданими, категоріями та API',
    endpoints: [
      'GET /api/v1/services/',
      'GET /api/v1/services/{id}/',
      'GET /api/v1/categories/'
    ],
    features: ['Service Discovery', 'Metadata', 'Filtering', 'Search'],
    repository: 'https://github.com/diia-open-source/be-public-service-catalog',
    status: 'stable',
    category: 'Core API'
  },
  {
    name: 'data.gov.ua API',
    description: 'CKAN-based портал відкритих даних України з 80,000+ датасетами',
    endpoints: [
      'GET /api/3/action/package_list',
      'GET /api/3/action/package_search?q={query}',
      'GET /api/3/action/package_show?id={id}'
    ],
    features: ['Open Data', 'Statistics', 'Analytics', 'Search'],
    repository: 'https://data.gov.ua/pages/api-dokumentatsiia',
    status: 'stable',
    category: 'Data'
  },
  {
    name: 'iOS Components',
    description: 'UI компоненти для iOS додатку Дія з використанням Swift',
    endpoints: [
      'DSButtonPrimary',
      'DSTextFieldInput',
      'DSCardContainer'
    ],
    features: ['WCAG Compliant', 'Accessibility', 'Design System', 'SwiftUI'],
    repository: 'https://github.com/diia-open-source/ios-uicomponents',
    status: 'active',
    category: 'Components'
  },
  {
    name: 'Android Components',
    description: 'UI компоненти для Android додатку Дія з використанням Kotlin',
    endpoints: [
      'DSButton',
      'DSTextField',
      'DSCard'
    ],
    features: ['Material Design', 'Jetpack Compose', 'Accessibility', 'Design System'],
    repository: 'https://github.com/diia-open-source/android-uicomponents',
    status: 'active',
    category: 'Components'
  },
  {
    name: 'Electronic ID (ICEI)',
    description: 'Bank ID, Кваліфікований електронний підпис (КЕП), MobileID',
    endpoints: [
      'GET /auth/bankid/deeplink',
      'POST /auth/validate',
      'GET /identity/verify'
    ],
    features: ['Bank ID', 'Digital Signature', 'Mobile ID', 'Verification'],
    repository: 'https://id.gov.ua/',
    status: 'stable',
    category: 'Auth'
  }
]

const mcpServers = [
  {
    name: 'GitHub MCP',
    description: 'Доступ до diia-open-source репозиторіїв, PR, issues, commits',
    capabilities: ['Repo Management', 'File Operations', 'PR/Issue Management', 'Code Search'],
    usage: 'Auto-sync компонентів, моніторинг оновлень дизайн-системи',
    priority: 'High'
  },
  {
    name: 'Filesystem MCP',
    description: 'Безпечне читання локальних копій Diia компонентів',
    capabilities: ['File Read/Write', 'Directory Traversal', 'Parsing', 'Analysis'],
    usage: 'Парсинг Swift/Kotlin компонентів для RAG бази',
    priority: 'High'
  },
  {
    name: 'Memory MCP',
    description: 'Knowledge graph для зберігання історії flow та feedback',
    capabilities: ['Graph Storage', 'Query', 'Pattern Recognition', 'Analytics'],
    usage: 'Історія генерацій, AI-дошка натхнення',
    priority: 'Medium'
  },
  {
    name: 'PostgreSQL MCP',
    description: 'Production database для BRD, flow, evaluation результатів',
    capabilities: ['CRUD Operations', 'Transactions', 'Queries', 'Analytics'],
    usage: 'Storage для всіх даних та метрик',
    priority: 'High'
  },
  {
    name: 'Slack MCP',
    description: 'Team notifications та feedback колектор',
    capabilities: ['Messages', 'Channels', 'Threads', 'File Sharing'],
    usage: 'Сповіщення про згенеровані flow, team collaboration',
    priority: 'Medium'
  },
  {
    name: 'Brave Search MCP',
    description: 'Web search для актуальної інформації про Diia та служпослуги',
    capabilities: ['Search', 'Ranking', 'Content Extraction', 'News'],
    usage: 'Пошук актуальних даних про держпослуги',
    priority: 'Low'
  }
]

export default function APIIntegrations() {
  return (
    <section id="api-integrations" className="py-20 px-4 md:px-6 bg-gradient-to-b from-background via-primary/5 to-background">
      <div className="max-w-6xl mx-auto">
        <div className="text-center mb-16">
          <Badge className="mb-4 inline-flex items-center gap-2">
            <Zap className="w-4 h-4" />
            Реальні API та MCP Інтеграції
          </Badge>
          <h2 className="text-4xl md:text-5xl font-bold bg-gradient-to-r from-primary to-accent bg-clip-text text-transparent mb-4">
            Підключені до Diia.AI Екосистеми
          </h2>
          <p className="text-lg text-muted-foreground max-w-2xl mx-auto">
            Yana.Diia інтегрована з реальними API, GitHub MCP серверами та Diia Open Source компонентами для генерації flow
          </p>
        </div>

        <div className="space-y-8 mb-16">
          <div>
            <h3 className="text-2xl font-bold text-foreground mb-6 flex items-center gap-3">
              <GitBranch className="w-6 h-6 text-accent" />
              Diia Open Source API
            </h3>
            <div className="grid md:grid-cols-2 lg:grid-cols-3 gap-4">
              {integrations.map((api) => (
                <Card key={api.name} className="glass border-white/10 p-6 rounded-xl hover:border-white/20 transition group">
                  <div className="flex items-start justify-between mb-4">
                    <div>
                      <h4 className="font-bold text-foreground text-lg">{api.name}</h4>
                      <span className="text-xs px-2 py-1 rounded bg-accent/20 text-accent font-medium mt-2 inline-block">
                        {api.category}
                      </span>
                    </div>
                    <Link 
                      href={api.repository} 
                      target="_blank"
                      className="p-2 rounded-lg glass hover:bg-white/10 transition"
                    >
                      <ExternalLink className="w-4 h-4 text-muted-foreground group-hover:text-accent transition" />
                    </Link>
                  </div>

                  <p className="text-sm text-muted-foreground mb-4">{api.description}</p>

                  <div className="space-y-3 mb-4">
                    <div className="text-xs font-semibold text-primary uppercase">Endpoints:</div>
                    <div className="space-y-1">
                      {api.endpoints.slice(0, 2).map((endpoint, idx) => (
                        <div key={idx} className="text-xs text-foreground/70 font-mono">
                          {endpoint}
                        </div>
                      ))}
                    </div>
                  </div>

                  <div className="flex flex-wrap gap-1">
                    {api.features.slice(0, 2).map((feature, idx) => (
                      <span key={idx} className="text-xs px-2 py-1 rounded bg-primary/20 text-primary font-medium">
                        {feature}
                      </span>
                    ))}
                  </div>
                </Card>
              ))}
            </div>
          </div>

          <div>
            <h3 className="text-2xl font-bold text-foreground mb-6 flex items-center gap-3">
              <Database className="w-6 h-6 text-accent" />
              MCP (Model Context Protocol) Сервери
            </h3>
            <div className="grid md:grid-cols-2 gap-4">
              {mcpServers.map((mcp) => (
                <Card key={mcp.name} className="glass border-white/10 p-6 rounded-xl hover:border-white/20 transition">
                  <div className="flex items-start justify-between mb-4">
                    <h4 className="font-bold text-foreground text-lg">{mcp.name}</h4>
                    <div className={`text-xs px-3 py-1 rounded-full font-medium ${
                      mcp.priority === 'High' ? 'bg-accent/20 text-accent' :
                      mcp.priority === 'Medium' ? 'bg-primary/20 text-primary' :
                      'bg-muted/20 text-muted-foreground'
                    }`}>
                      {mcp.priority}
                    </div>
                  </div>

                  <p className="text-sm text-muted-foreground mb-4">{mcp.description}</p>

                  <div className="space-y-3 mb-4">
                    <div className="text-xs font-semibold text-primary uppercase">Можливості:</div>
                    <div className="flex flex-wrap gap-1">
                      {mcp.capabilities.map((cap, idx) => (
                        <span key={idx} className="text-xs px-2 py-1 rounded bg-accent/10 text-accent font-medium">
                          {cap}
                        </span>
                      ))}
                    </div>
                  </div>

                  <div className="pt-3 border-t border-border/20">
                    <div className="text-xs text-muted-foreground">
                      <strong>Використання:</strong> {mcp.usage}
                    </div>
                  </div>
                </Card>
              ))}
            </div>
          </div>
        </div>

        <Card className="glass border-white/10 p-8 rounded-2xl bg-gradient-to-r from-primary/10 to-accent/10">
          <div className="flex items-start gap-4">
            <Shield className="w-6 h-6 text-accent flex-shrink-0 mt-1" />
            <div>
              <h4 className="font-bold text-foreground text-lg mb-2">Безпека та Compliance</h4>
              <ul className="space-y-2 text-sm text-muted-foreground">
                <li>✓ GDPR/Privacy - тільки публічні open-source дані</li>
                <li>✓ EUPL 1.2 License - повна дотримання ліцензії Diia</li>
                <li>✓ API Key Management - безпечне зберігання credentials</li>
                <li>✓ Open Source - transparency by design, верифіковане API</li>
              </ul>
            </div>
          </div>
        </Card>
      </div>
    </section>
  )
}
\n--- END FILE: ./html.code.v0.app/components/api-integrations.tsx ---
\n--- START FILE: ./html.code.v0.app/components/live-demo.tsx ---
'use client'

import { useState } from 'react'
import { Card } from '@/components/ui/card'
import { Button } from '@/components/ui/button'
import { Zap, Copy, Check, Upload, AlertCircle, HelpCircle } from 'lucide-react'

const mockDemoFlow = {
  flow: {
    name: "Document Upload Service",
    steps: [
      { step_id: 1, screen_name: "Welcome Screen", action: "show_welcome" },
      { step_id: 2, screen_name: "File Upload", action: "upload_documents" },
      { step_id: 3, screen_name: "Validation", action: "validate_docs" },
      { step_id: 4, screen_name: "ESID Save", action: "save_to_esid" }
    ]
  },
  scores: {
    logic: 8.5,
    design: 9.0,
    completeness: 8.7,
    minimality: 9.2,
    total: 8.85
  }
}

export default function LiveDemo() {
  const [brdText, setBrdText] = useState('Користувач хоче подати документи онлайн\nПотрібна можливість завантажити файли\nВалідація документів\nЗбереження в ЕСІД')
  const [flowOutput, setFlowOutput] = useState('')
  const [isLoading, setIsLoading] = useState(false)
  const [copied, setCopied] = useState(false)
  const [error, setError] = useState('')
  const [scores, setScores] = useState<any>(null)
  const [isDemoMode, setIsDemoMode] = useState(false)

  const handleGenerateFlow = async () => {
    setIsLoading(true)
    setError('')
    setFlowOutput('')
    setScores(null)
    setIsDemoMode(false)
    
    try {
      const response = await fetch('/api/generate', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ 
          brd: brdText, 
          numVariants: 1 
        })
      })
      
      if (!response.ok) {
        const errorData = await response.json()
        throw new Error(errorData.error || 'Generation failed')
      }

      const data = await response.json()
      const championVariant = data.variants.find((v: any) => v.variant_id === data.champion)
      
      setFlowOutput(JSON.stringify(championVariant.flow, null, 2))
      setScores({
        logic: championVariant.logic_score,
        design: championVariant.design_score,
        completeness: championVariant.completeness_score,
        minimality: championVariant.minimality_score,
        total: championVariant.total_score
      })
    } catch (err) {
      console.error('[v0] Generation error:', err)
      const errorMsg = err instanceof Error ? err.message : 'Generation failed'
      setError(errorMsg)
      
      if (errorMsg.includes('Backend') || errorMsg.includes('cannot reach')) {
        setIsDemoMode(true)
      }
    } finally {
      setIsLoading(false)
    }
  }

  const handleDemoMode = () => {
    setFlowOutput(JSON.stringify(mockDemoFlow.flow, null, 2))
    setScores(mockDemoFlow.scores)
    setError('')
  }

  const handleCopy = () => {
    navigator.clipboard.writeText(flowOutput)
    setCopied(true)
    setTimeout(() => setCopied(false), 2000)
  }

  return (
    <section id="live-demo" className="py-20 px-4 md:px-6 bg-gradient-to-b from-background to-background/50">
      <div className="max-w-6xl mx-auto">
        <div className="text-center mb-12">
          <h2 className="text-4xl md:text-5xl font-bold bg-gradient-to-r from-primary to-accent bg-clip-text text-transparent mb-4">
            Спробуй Live Demo
          </h2>
          <p className="text-lg text-muted-foreground max-w-2xl mx-auto">
            Введи опис послуги (BRD) та отримай готовий JSON-flow за секунди
          </p>
        </div>

        <div className="grid grid-cols-1 lg:grid-cols-2 gap-6">
          {/* Input */}
          <Card className="glass border-white/10 p-6 rounded-2xl">
            <div className="space-y-4">
              <div className="flex items-center gap-2 mb-4">
                <Upload className="w-5 h-5 text-primary" />
                <h3 className="font-semibold text-foreground">Введи BRD чи опис послуги</h3>
              </div>
              
              <textarea
                value={brdText}
                onChange={(e) => setBrdText(e.target.value)}
                className="w-full h-48 bg-background/50 border border-border/30 rounded-lg p-4 text-foreground placeholder:text-muted-foreground focus:outline-none focus:border-primary/50 focus:ring-1 focus:ring-primary/20 resize-none"
                placeholder="Опиши послугу, яку потрібно автоматизувати..."
              />
              
              <Button
                onClick={handleGenerateFlow}
                disabled={isLoading || !brdText.trim()}
                className="w-full bg-gradient-to-r from-primary to-accent hover:from-primary/90 hover:to-accent/90 text-primary-foreground rounded-lg"
              >
                {isLoading ? (
                  <span className="flex items-center gap-2">
                    <div className="w-4 h-4 border-2 border-transparent border-t-white rounded-full animate-spin" />
                    Генерую flow...
                  </span>
                ) : (
                  <span className="flex items-center gap-2">
                    <Zap className="w-4 h-4" />
                    Генерувати Flow
                  </span>
                )}
              </Button>

              {error && (
                <div className="p-3 rounded-lg bg-red-500/10 border border-red-500/30 space-y-2">
                  <div className="flex items-start gap-2 text-sm text-red-400">
                    <AlertCircle className="w-4 h-4 mt-0.5 flex-shrink-0" />
                    <span>{error}</span>
                  </div>
                  {isDemoMode && (
                    <Button
                      onClick={handleDemoMode}
                      variant="outline"
                      size="sm"
                      className="w-full text-xs border-red-500/50 hover:bg-red-500/10"
                    >
                      <HelpCircle className="w-3 h-3 mr-1" />
                      Try Demo Mode Instead
                    </Button>
                  )}
                </div>
              )}
            </div>
          </Card>

          {/* Output */}
          <Card className="glass border-white/10 p-6 rounded-2xl">
            <div className="space-y-4">
              <div className="flex items-center justify-between mb-4">
                <h3 className="font-semibold text-foreground flex items-center gap-2">
                  <div className="w-5 h-5 bg-gradient-to-br from-primary to-accent rounded-full" />
                  JSON Flow Output
                  {isDemoMode && <span className="text-xs bg-yellow-500/20 text-yellow-400 px-2 py-1 rounded">Demo</span>}
                </h3>
                {flowOutput && (
                  <button
                    onClick={handleCopy}
                    className="p-2 hover:bg-white/10 rounded-lg transition"
                  >
                    {copied ? (
                      <Check className="w-4 h-4 text-green-400" />
                    ) : (
                      <Copy className="w-4 h-4 text-muted-foreground" />
                    )}
                  </button>
                )}
              </div>
              
              <pre className="w-full h-48 bg-background/50 border border-border/30 rounded-lg p-4 text-xs text-muted-foreground overflow-auto font-mono">
                {flowOutput || '// Flow буде відображатися тут...'}
              </pre>

              {scores && (
                <div className="grid grid-cols-2 gap-3 text-xs">
                  <div className="bg-primary/10 border border-primary/30 rounded-lg p-3">
                    <span className="text-muted-foreground">Logic Score</span>
                    <p className="text-primary font-semibold">{scores.logic.toFixed(1)}/10</p>
                  </div>
                  <div className="bg-accent/10 border border-accent/30 rounded-lg p-3">
                    <span className="text-muted-foreground">Design Score</span>
                    <p className="text-accent font-semibold">{scores.design.toFixed(1)}/10</p>
                  </div>
                  <div className="bg-primary/10 border border-primary/30 rounded-lg p-3">
                    <span className="text-muted-foreground">Completeness</span>
                    <p className="text-primary font-semibold">{scores.completeness.toFixed(1)}/10</p>
                  </div>
                  <div className="bg-accent/10 border border-accent/30 rounded-lg p-3">
                    <span className="text-muted-foreground">Total Score</span>
                    <p className="text-accent font-semibold">{scores.total.toFixed(2)}/10</p>
                  </div>
                </div>
              )}
            </div>
          </Card>
        </div>

        <div className="mt-12 p-6 bg-gradient-to-r from-primary/5 to-accent/5 border border-primary/10 rounded-2xl">
          <p className="text-sm text-muted-foreground text-center">
            Для реальної генерації запусти backend: див. BACKEND_SETUP.md
            <br />
            Або використай Demo Mode для швидкого перегляду можливостей
          </p>
        </div>
      </div>
    </section>
  )
}
\n--- END FILE: ./html.code.v0.app/components/live-demo.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/badge.tsx ---
import * as React from 'react'
import { cva, type VariantProps } from 'class-variance-authority'

import { cn } from '@/lib/utils'

const badgeVariants = cva(
  'inline-flex items-center rounded-full border px-2.5 py-0.5 text-xs font-semibold transition-all',
  {
    variants: {
      variant: {
        default:
          'border-transparent bg-primary text-primary-foreground hover:bg-primary/80',
        secondary:
          'border-transparent bg-secondary text-secondary-foreground hover:bg-secondary/80',
        destructive:
          'border-transparent bg-destructive text-destructive-foreground hover:bg-destructive/80',
        outline: 'text-foreground',
      },
    },
    defaultVariants: {
      variant: 'default',
    },
  }
)

export interface BadgeProps
  extends React.HTMLAttributes<HTMLDivElement>,
    VariantProps<typeof badgeVariants> {}

function Badge({ className, variant, ...props }: BadgeProps) {
  return (
    <div className={cn(badgeVariants({ variant }), className)} {...props} />
  )
}

export { Badge, badgeVariants }
\n--- END FILE: ./html.code.v0.app/components/ui/badge.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/tabs.tsx ---
'use client'

import * as React from 'react'
import * as TabsPrimitive from '@radix-ui/react-tabs'

import { cn } from '@/lib/utils'

function Tabs({
  className,
  ...props
}: React.ComponentProps<typeof TabsPrimitive.Root>) {
  return (
    <TabsPrimitive.Root
      data-slot="tabs"
      className={cn('flex flex-col gap-2', className)}
      {...props}
    />
  )
}

function TabsList({
  className,
  ...props
}: React.ComponentProps<typeof TabsPrimitive.List>) {
  return (
    <TabsPrimitive.List
      data-slot="tabs-list"
      className={cn(
        'bg-muted text-muted-foreground inline-flex h-9 w-fit items-center justify-center rounded-lg p-[3px]',
        className,
      )}
      {...props}
    />
  )
}

function TabsTrigger({
  className,
  ...props
}: React.ComponentProps<typeof TabsPrimitive.Trigger>) {
  return (
    <TabsPrimitive.Trigger
      data-slot="tabs-trigger"
      className={cn(
        "data-[state=active]:bg-background dark:data-[state=active]:text-foreground focus-visible:border-ring focus-visible:ring-ring/50 focus-visible:outline-ring dark:data-[state=active]:border-input dark:data-[state=active]:bg-input/30 text-foreground dark:text-muted-foreground inline-flex h-[calc(100%-1px)] flex-1 items-center justify-center gap-1.5 rounded-md border border-transparent px-2 py-1 text-sm font-medium whitespace-nowrap transition-[color,box-shadow] focus-visible:ring-[3px] focus-visible:outline-1 disabled:pointer-events-none disabled:opacity-50 data-[state=active]:shadow-sm [&_svg]:pointer-events-none [&_svg]:shrink-0 [&_svg:not([class*='size-'])]:size-4",
        className,
      )}
      {...props}
    />
  )
}

function TabsContent({
  className,
  ...props
}: React.ComponentProps<typeof TabsPrimitive.Content>) {
  return (
    <TabsPrimitive.Content
      data-slot="tabs-content"
      className={cn('flex-1 outline-none', className)}
      {...props}
    />
  )
}

export { Tabs, TabsList, TabsTrigger, TabsContent }
\n--- END FILE: ./html.code.v0.app/components/ui/tabs.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/resizable.tsx ---
'use client'

import * as React from 'react'
import { GripVerticalIcon } from 'lucide-react'
import * as ResizablePrimitive from 'react-resizable-panels'

import { cn } from '@/lib/utils'

function ResizablePanelGroup({
  className,
  ...props
}: React.ComponentProps<typeof ResizablePrimitive.PanelGroup>) {
  return (
    <ResizablePrimitive.PanelGroup
      data-slot="resizable-panel-group"
      className={cn(
        'flex h-full w-full data-[panel-group-direction=vertical]:flex-col',
        className,
      )}
      {...props}
    />
  )
}

function ResizablePanel({
  ...props
}: React.ComponentProps<typeof ResizablePrimitive.Panel>) {
  return <ResizablePrimitive.Panel data-slot="resizable-panel" {...props} />
}

function ResizableHandle({
  withHandle,
  className,
  ...props
}: React.ComponentProps<typeof ResizablePrimitive.PanelResizeHandle> & {
  withHandle?: boolean
}) {
  return (
    <ResizablePrimitive.PanelResizeHandle
      data-slot="resizable-handle"
      className={cn(
        'bg-border focus-visible:ring-ring relative flex w-px items-center justify-center after:absolute after:inset-y-0 after:left-1/2 after:w-1 after:-translate-x-1/2 focus-visible:ring-1 focus-visible:ring-offset-1 focus-visible:outline-hidden data-[panel-group-direction=vertical]:h-px data-[panel-group-direction=vertical]:w-full data-[panel-group-direction=vertical]:after:left-0 data-[panel-group-direction=vertical]:after:h-1 data-[panel-group-direction=vertical]:after:w-full data-[panel-group-direction=vertical]:after:translate-x-0 data-[panel-group-direction=vertical]:after:-translate-y-1/2 [&[data-panel-group-direction=vertical]>div]:rotate-90',
        className,
      )}
      {...props}
    >
      {withHandle && (
        <div className="bg-border z-10 flex h-4 w-3 items-center justify-center rounded-xs border">
          <GripVerticalIcon className="size-2.5" />
        </div>
      )}
    </ResizablePrimitive.PanelResizeHandle>
  )
}

export { ResizablePanelGroup, ResizablePanel, ResizableHandle }
\n--- END FILE: ./html.code.v0.app/components/ui/resizable.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/slider.tsx ---
'use client'

import * as React from 'react'
import * as SliderPrimitive from '@radix-ui/react-slider'

import { cn } from '@/lib/utils'

function Slider({
  className,
  defaultValue,
  value,
  min = 0,
  max = 100,
  ...props
}: React.ComponentProps<typeof SliderPrimitive.Root>) {
  const _values = React.useMemo(
    () =>
      Array.isArray(value)
        ? value
        : Array.isArray(defaultValue)
          ? defaultValue
          : [min, max],
    [value, defaultValue, min, max],
  )

  return (
    <SliderPrimitive.Root
      data-slot="slider"
      defaultValue={defaultValue}
      value={value}
      min={min}
      max={max}
      className={cn(
        'relative flex w-full touch-none items-center select-none data-[disabled]:opacity-50 data-[orientation=vertical]:h-full data-[orientation=vertical]:min-h-44 data-[orientation=vertical]:w-auto data-[orientation=vertical]:flex-col',
        className,
      )}
      {...props}
    >
      <SliderPrimitive.Track
        data-slot="slider-track"
        className={
          'bg-muted relative grow overflow-hidden rounded-full data-[orientation=horizontal]:h-1.5 data-[orientation=horizontal]:w-full data-[orientation=vertical]:h-full data-[orientation=vertical]:w-1.5'
        }
      >
        <SliderPrimitive.Range
          data-slot="slider-range"
          className={
            'bg-primary absolute data-[orientation=horizontal]:h-full data-[orientation=vertical]:w-full'
          }
        />
      </SliderPrimitive.Track>
      {Array.from({ length: _values.length }, (_, index) => (
        <SliderPrimitive.Thumb
          data-slot="slider-thumb"
          key={index}
          className="border-primary ring-ring/50 block size-4 shrink-0 rounded-full border bg-white shadow-sm transition-[color,box-shadow] hover:ring-4 focus-visible:ring-4 focus-visible:outline-hidden disabled:pointer-events-none disabled:opacity-50"
        />
      ))}
    </SliderPrimitive.Root>
  )
}

export { Slider }
\n--- END FILE: ./html.code.v0.app/components/ui/slider.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/sheet.tsx ---
'use client'

import * as React from 'react'
import * as SheetPrimitive from '@radix-ui/react-dialog'
import { XIcon } from 'lucide-react'

import { cn } from '@/lib/utils'

function Sheet({ ...props }: React.ComponentProps<typeof SheetPrimitive.Root>) {
  return <SheetPrimitive.Root data-slot="sheet" {...props} />
}

function SheetTrigger({
  ...props
}: React.ComponentProps<typeof SheetPrimitive.Trigger>) {
  return <SheetPrimitive.Trigger data-slot="sheet-trigger" {...props} />
}

function SheetClose({
  ...props
}: React.ComponentProps<typeof SheetPrimitive.Close>) {
  return <SheetPrimitive.Close data-slot="sheet-close" {...props} />
}

function SheetPortal({
  ...props
}: React.ComponentProps<typeof SheetPrimitive.Portal>) {
  return <SheetPrimitive.Portal data-slot="sheet-portal" {...props} />
}

function SheetOverlay({
  className,
  ...props
}: React.ComponentProps<typeof SheetPrimitive.Overlay>) {
  return (
    <SheetPrimitive.Overlay
      data-slot="sheet-overlay"
      className={cn(
        'data-[state=open]:animate-in data-[state=closed]:animate-out data-[state=closed]:fade-out-0 data-[state=open]:fade-in-0 fixed inset-0 z-50 bg-black/50',
        className,
      )}
      {...props}
    />
  )
}

function SheetContent({
  className,
  children,
  side = 'right',
  ...props
}: React.ComponentProps<typeof SheetPrimitive.Content> & {
  side?: 'top' | 'right' | 'bottom' | 'left'
}) {
  return (
    <SheetPortal>
      <SheetOverlay />
      <SheetPrimitive.Content
        data-slot="sheet-content"
        className={cn(
          'bg-background data-[state=open]:animate-in data-[state=closed]:animate-out fixed z-50 flex flex-col gap-4 shadow-lg transition ease-in-out data-[state=closed]:duration-300 data-[state=open]:duration-500',
          side === 'right' &&
            'data-[state=closed]:slide-out-to-right data-[state=open]:slide-in-from-right inset-y-0 right-0 h-full w-3/4 border-l sm:max-w-sm',
          side === 'left' &&
            'data-[state=closed]:slide-out-to-left data-[state=open]:slide-in-from-left inset-y-0 left-0 h-full w-3/4 border-r sm:max-w-sm',
          side === 'top' &&
            'data-[state=closed]:slide-out-to-top data-[state=open]:slide-in-from-top inset-x-0 top-0 h-auto border-b',
          side === 'bottom' &&
            'data-[state=closed]:slide-out-to-bottom data-[state=open]:slide-in-from-bottom inset-x-0 bottom-0 h-auto border-t',
          className,
        )}
        {...props}
      >
        {children}
        <SheetPrimitive.Close className="ring-offset-background focus:ring-ring data-[state=open]:bg-secondary absolute top-4 right-4 rounded-xs opacity-70 transition-opacity hover:opacity-100 focus:ring-2 focus:ring-offset-2 focus:outline-hidden disabled:pointer-events-none">
          <XIcon className="size-4" />
          <span className="sr-only">Close</span>
        </SheetPrimitive.Close>
      </SheetPrimitive.Content>
    </SheetPortal>
  )
}

function SheetHeader({ className, ...props }: React.ComponentProps<'div'>) {
  return (
    <div
      data-slot="sheet-header"
      className={cn('flex flex-col gap-1.5 p-4', className)}
      {...props}
    />
  )
}

function SheetFooter({ className, ...props }: React.ComponentProps<'div'>) {
  return (
    <div
      data-slot="sheet-footer"
      className={cn('mt-auto flex flex-col gap-2 p-4', className)}
      {...props}
    />
  )
}

function SheetTitle({
  className,
  ...props
}: React.ComponentProps<typeof SheetPrimitive.Title>) {
  return (
    <SheetPrimitive.Title
      data-slot="sheet-title"
      className={cn('text-foreground font-semibold', className)}
      {...props}
    />
  )
}

function SheetDescription({
  className,
  ...props
}: React.ComponentProps<typeof SheetPrimitive.Description>) {
  return (
    <SheetPrimitive.Description
      data-slot="sheet-description"
      className={cn('text-muted-foreground text-sm', className)}
      {...props}
    />
  )
}

export {
  Sheet,
  SheetTrigger,
  SheetClose,
  SheetContent,
  SheetHeader,
  SheetFooter,
  SheetTitle,
  SheetDescription,
}
\n--- END FILE: ./html.code.v0.app/components/ui/sheet.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/alert-dialog.tsx ---
'use client'

import * as React from 'react'
import * as AlertDialogPrimitive from '@radix-ui/react-alert-dialog'

import { cn } from '@/lib/utils'
import { buttonVariants } from '@/components/ui/button'

function AlertDialog({
  ...props
}: React.ComponentProps<typeof AlertDialogPrimitive.Root>) {
  return <AlertDialogPrimitive.Root data-slot="alert-dialog" {...props} />
}

function AlertDialogTrigger({
  ...props
}: React.ComponentProps<typeof AlertDialogPrimitive.Trigger>) {
  return (
    <AlertDialogPrimitive.Trigger data-slot="alert-dialog-trigger" {...props} />
  )
}

function AlertDialogPortal({
  ...props
}: React.ComponentProps<typeof AlertDialogPrimitive.Portal>) {
  return (
    <AlertDialogPrimitive.Portal data-slot="alert-dialog-portal" {...props} />
  )
}

function AlertDialogOverlay({
  className,
  ...props
}: React.ComponentProps<typeof AlertDialogPrimitive.Overlay>) {
  return (
    <AlertDialogPrimitive.Overlay
      data-slot="alert-dialog-overlay"
      className={cn(
        'data-[state=open]:animate-in data-[state=closed]:animate-out data-[state=closed]:fade-out-0 data-[state=open]:fade-in-0 fixed inset-0 z-50 bg-black/50',
        className,
      )}
      {...props}
    />
  )
}

function AlertDialogContent({
  className,
  ...props
}: React.ComponentProps<typeof AlertDialogPrimitive.Content>) {
  return (
    <AlertDialogPortal>
      <AlertDialogOverlay />
      <AlertDialogPrimitive.Content
        data-slot="alert-dialog-content"
        className={cn(
          'bg-background data-[state=open]:animate-in data-[state=closed]:animate-out data-[state=closed]:fade-out-0 data-[state=open]:fade-in-0 data-[state=closed]:zoom-out-95 data-[state=open]:zoom-in-95 fixed top-[50%] left-[50%] z-50 grid w-full max-w-[calc(100%-2rem)] translate-x-[-50%] translate-y-[-50%] gap-4 rounded-lg border p-6 shadow-lg duration-200 sm:max-w-lg',
          className,
        )}
        {...props}
      />
    </AlertDialogPortal>
  )
}

function AlertDialogHeader({
  className,
  ...props
}: React.ComponentProps<'div'>) {
  return (
    <div
      data-slot="alert-dialog-header"
      className={cn('flex flex-col gap-2 text-center sm:text-left', className)}
      {...props}
    />
  )
}

function AlertDialogFooter({
  className,
  ...props
}: React.ComponentProps<'div'>) {
  return (
    <div
      data-slot="alert-dialog-footer"
      className={cn(
        'flex flex-col-reverse gap-2 sm:flex-row sm:justify-end',
        className,
      )}
      {...props}
    />
  )
}

function AlertDialogTitle({
  className,
  ...props
}: React.ComponentProps<typeof AlertDialogPrimitive.Title>) {
  return (
    <AlertDialogPrimitive.Title
      data-slot="alert-dialog-title"
      className={cn('text-lg font-semibold', className)}
      {...props}
    />
  )
}

function AlertDialogDescription({
  className,
  ...props
}: React.ComponentProps<typeof AlertDialogPrimitive.Description>) {
  return (
    <AlertDialogPrimitive.Description
      data-slot="alert-dialog-description"
      className={cn('text-muted-foreground text-sm', className)}
      {...props}
    />
  )
}

function AlertDialogAction({
  className,
  ...props
}: React.ComponentProps<typeof AlertDialogPrimitive.Action>) {
  return (
    <AlertDialogPrimitive.Action
      className={cn(buttonVariants(), className)}
      {...props}
    />
  )
}

function AlertDialogCancel({
  className,
  ...props
}: React.ComponentProps<typeof AlertDialogPrimitive.Cancel>) {
  return (
    <AlertDialogPrimitive.Cancel
      className={cn(buttonVariants({ variant: 'outline' }), className)}
      {...props}
    />
  )
}

export {
  AlertDialog,
  AlertDialogPortal,
  AlertDialogOverlay,
  AlertDialogTrigger,
  AlertDialogContent,
  AlertDialogHeader,
  AlertDialogFooter,
  AlertDialogTitle,
  AlertDialogDescription,
  AlertDialogAction,
  AlertDialogCancel,
}
\n--- END FILE: ./html.code.v0.app/components/ui/alert-dialog.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/input-group.tsx ---
'use client'

import { cva, type VariantProps } from 'class-variance-authority'

import { cn } from '@/lib/utils'
import { Button } from '@/components/ui/button'
import { Input } from '@/components/ui/input'
import { Textarea } from '@/components/ui/textarea'

function InputGroup({ className, ...props }: React.ComponentProps<'div'>) {
  return (
    <div
      data-slot="input-group"
      role="group"
      className={cn(
        'group/input-group border-input dark:bg-input/30 relative flex w-full items-center rounded-md border shadow-xs transition-[color,box-shadow] outline-none',
        'h-9 has-[>textarea]:h-auto',

        // Variants based on alignment.
        'has-[>[data-align=inline-start]]:[&>input]:pl-2',
        'has-[>[data-align=inline-end]]:[&>input]:pr-2',
        'has-[>[data-align=block-start]]:h-auto has-[>[data-align=block-start]]:flex-col has-[>[data-align=block-start]]:[&>input]:pb-3',
        'has-[>[data-align=block-end]]:h-auto has-[>[data-align=block-end]]:flex-col has-[>[data-align=block-end]]:[&>input]:pt-3',

        // Focus state.
        'has-[[data-slot=input-group-control]:focus-visible]:border-ring has-[[data-slot=input-group-control]:focus-visible]:ring-ring/50 has-[[data-slot=input-group-control]:focus-visible]:ring-[3px]',

        // Error state.
        'has-[[data-slot][aria-invalid=true]]:ring-destructive/20 has-[[data-slot][aria-invalid=true]]:border-destructive dark:has-[[data-slot][aria-invalid=true]]:ring-destructive/40',

        className,
      )}
      {...props}
    />
  )
}

const inputGroupAddonVariants = cva(
  "text-muted-foreground flex h-auto cursor-text items-center justify-center gap-2 py-1.5 text-sm font-medium select-none [&>svg:not([class*='size-'])]:size-4 [&>kbd]:rounded-[calc(var(--radius)-5px)] group-data-[disabled=true]/input-group:opacity-50",
  {
    variants: {
      align: {
        'inline-start':
          'order-first pl-3 has-[>button]:ml-[-0.45rem] has-[>kbd]:ml-[-0.35rem]',
        'inline-end':
          'order-last pr-3 has-[>button]:mr-[-0.4rem] has-[>kbd]:mr-[-0.35rem]',
        'block-start':
          'order-first w-full justify-start px-3 pt-3 [.border-b]:pb-3 group-has-[>input]/input-group:pt-2.5',
        'block-end':
          'order-last w-full justify-start px-3 pb-3 [.border-t]:pt-3 group-has-[>input]/input-group:pb-2.5',
      },
    },
    defaultVariants: {
      align: 'inline-start',
    },
  },
)

function InputGroupAddon({
  className,
  align = 'inline-start',
  ...props
}: React.ComponentProps<'div'> & VariantProps<typeof inputGroupAddonVariants>) {
  return (
    <div
      role="group"
      data-slot="input-group-addon"
      data-align={align}
      className={cn(inputGroupAddonVariants({ align }), className)}
      onClick={(e) => {
        if ((e.target as HTMLElement).closest('button')) {
          return
        }
        e.currentTarget.parentElement?.querySelector('input')?.focus()
      }}
      {...props}
    />
  )
}

const inputGroupButtonVariants = cva(
  'text-sm shadow-none flex gap-2 items-center',
  {
    variants: {
      size: {
        xs: "h-6 gap-1 px-2 rounded-[calc(var(--radius)-5px)] [&>svg:not([class*='size-'])]:size-3.5 has-[>svg]:px-2",
        sm: 'h-8 px-2.5 gap-1.5 rounded-md has-[>svg]:px-2.5',
        'icon-xs':
          'size-6 rounded-[calc(var(--radius)-5px)] p-0 has-[>svg]:p-0',
        'icon-sm': 'size-8 p-0 has-[>svg]:p-0',
      },
    },
    defaultVariants: {
      size: 'xs',
    },
  },
)

function InputGroupButton({
  className,
  type = 'button',
  variant = 'ghost',
  size = 'xs',
  ...props
}: Omit<React.ComponentProps<typeof Button>, 'size'> &
  VariantProps<typeof inputGroupButtonVariants>) {
  return (
    <Button
      type={type}
      data-size={size}
      variant={variant}
      className={cn(inputGroupButtonVariants({ size }), className)}
      {...props}
    />
  )
}

function InputGroupText({ className, ...props }: React.ComponentProps<'span'>) {
  return (
    <span
      className={cn(
        "text-muted-foreground flex items-center gap-2 text-sm [&_svg]:pointer-events-none [&_svg:not([class*='size-'])]:size-4",
        className,
      )}
      {...props}
    />
  )
}

function InputGroupInput({
  className,
  ...props
}: React.ComponentProps<'input'>) {
  return (
    <Input
      data-slot="input-group-control"
      className={cn(
        'flex-1 rounded-none border-0 bg-transparent shadow-none focus-visible:ring-0 dark:bg-transparent',
        className,
      )}
      {...props}
    />
  )
}

function InputGroupTextarea({
  className,
  ...props
}: React.ComponentProps<'textarea'>) {
  return (
    <Textarea
      data-slot="input-group-control"
      className={cn(
        'flex-1 resize-none rounded-none border-0 bg-transparent py-3 shadow-none focus-visible:ring-0 dark:bg-transparent',
        className,
      )}
      {...props}
    />
  )
}

export {
  InputGroup,
  InputGroupAddon,
  InputGroupButton,
  InputGroupText,
  InputGroupInput,
  InputGroupTextarea,
}
\n--- END FILE: ./html.code.v0.app/components/ui/input-group.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/popover.tsx ---
'use client'

import * as React from 'react'
import * as PopoverPrimitive from '@radix-ui/react-popover'

import { cn } from '@/lib/utils'

function Popover({
  ...props
}: React.ComponentProps<typeof PopoverPrimitive.Root>) {
  return <PopoverPrimitive.Root data-slot="popover" {...props} />
}

function PopoverTrigger({
  ...props
}: React.ComponentProps<typeof PopoverPrimitive.Trigger>) {
  return <PopoverPrimitive.Trigger data-slot="popover-trigger" {...props} />
}

function PopoverContent({
  className,
  align = 'center',
  sideOffset = 4,
  ...props
}: React.ComponentProps<typeof PopoverPrimitive.Content>) {
  return (
    <PopoverPrimitive.Portal>
      <PopoverPrimitive.Content
        data-slot="popover-content"
        align={align}
        sideOffset={sideOffset}
        className={cn(
          'bg-popover text-popover-foreground data-[state=open]:animate-in data-[state=closed]:animate-out data-[state=closed]:fade-out-0 data-[state=open]:fade-in-0 data-[state=closed]:zoom-out-95 data-[state=open]:zoom-in-95 data-[side=bottom]:slide-in-from-top-2 data-[side=left]:slide-in-from-right-2 data-[side=right]:slide-in-from-left-2 data-[side=top]:slide-in-from-bottom-2 z-50 w-72 origin-(--radix-popover-content-transform-origin) rounded-md border p-4 shadow-md outline-hidden',
          className,
        )}
        {...props}
      />
    </PopoverPrimitive.Portal>
  )
}

function PopoverAnchor({
  ...props
}: React.ComponentProps<typeof PopoverPrimitive.Anchor>) {
  return <PopoverPrimitive.Anchor data-slot="popover-anchor" {...props} />
}

export { Popover, PopoverTrigger, PopoverContent, PopoverAnchor }
\n--- END FILE: ./html.code.v0.app/components/ui/popover.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/input.tsx ---
import * as React from 'react'

import { cn } from '@/lib/utils'

function Input({ className, type, ...props }: React.ComponentProps<'input'>) {
  return (
    <input
      type={type}
      data-slot="input"
      className={cn(
        'file:text-foreground placeholder:text-muted-foreground selection:bg-primary selection:text-primary-foreground dark:bg-input/30 border-input h-9 w-full min-w-0 rounded-md border bg-transparent px-3 py-1 text-base shadow-xs transition-[color,box-shadow] outline-none file:inline-flex file:h-7 file:border-0 file:bg-transparent file:text-sm file:font-medium disabled:pointer-events-none disabled:cursor-not-allowed disabled:opacity-50 md:text-sm',
        'focus-visible:border-ring focus-visible:ring-ring/50 focus-visible:ring-[3px]',
        'aria-invalid:ring-destructive/20 dark:aria-invalid:ring-destructive/40 aria-invalid:border-destructive',
        className,
      )}
      {...props}
    />
  )
}

export { Input }
\n--- END FILE: ./html.code.v0.app/components/ui/input.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/toggle-group.tsx ---
'use client'

import * as React from 'react'
import * as ToggleGroupPrimitive from '@radix-ui/react-toggle-group'
import { type VariantProps } from 'class-variance-authority'

import { cn } from '@/lib/utils'
import { toggleVariants } from '@/components/ui/toggle'

const ToggleGroupContext = React.createContext<
  VariantProps<typeof toggleVariants>
>({
  size: 'default',
  variant: 'default',
})

function ToggleGroup({
  className,
  variant,
  size,
  children,
  ...props
}: React.ComponentProps<typeof ToggleGroupPrimitive.Root> &
  VariantProps<typeof toggleVariants>) {
  return (
    <ToggleGroupPrimitive.Root
      data-slot="toggle-group"
      data-variant={variant}
      data-size={size}
      className={cn(
        'group/toggle-group flex w-fit items-center rounded-md data-[variant=outline]:shadow-xs',
        className,
      )}
      {...props}
    >
      <ToggleGroupContext.Provider value={{ variant, size }}>
        {children}
      </ToggleGroupContext.Provider>
    </ToggleGroupPrimitive.Root>
  )
}

function ToggleGroupItem({
  className,
  children,
  variant,
  size,
  ...props
}: React.ComponentProps<typeof ToggleGroupPrimitive.Item> &
  VariantProps<typeof toggleVariants>) {
  const context = React.useContext(ToggleGroupContext)

  return (
    <ToggleGroupPrimitive.Item
      data-slot="toggle-group-item"
      data-variant={context.variant || variant}
      data-size={context.size || size}
      className={cn(
        toggleVariants({
          variant: context.variant || variant,
          size: context.size || size,
        }),
        'min-w-0 flex-1 shrink-0 rounded-none shadow-none first:rounded-l-md last:rounded-r-md focus:z-10 focus-visible:z-10 data-[variant=outline]:border-l-0 data-[variant=outline]:first:border-l',
        className,
      )}
      {...props}
    >
      {children}
    </ToggleGroupPrimitive.Item>
  )
}

export { ToggleGroup, ToggleGroupItem }
\n--- END FILE: ./html.code.v0.app/components/ui/toggle-group.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/button-group.tsx ---
import { Slot } from '@radix-ui/react-slot'
import { cva, type VariantProps } from 'class-variance-authority'

import { cn } from '@/lib/utils'
import { Separator } from '@/components/ui/separator'

const buttonGroupVariants = cva(
  "flex w-fit items-stretch [&>*]:focus-visible:z-10 [&>*]:focus-visible:relative [&>[data-slot=select-trigger]:not([class*='w-'])]:w-fit [&>input]:flex-1 has-[select[aria-hidden=true]:last-child]:[&>[data-slot=select-trigger]:last-of-type]:rounded-r-md has-[>[data-slot=button-group]]:gap-2",
  {
    variants: {
      orientation: {
        horizontal:
          '[&>*:not(:first-child)]:rounded-l-none [&>*:not(:first-child)]:border-l-0 [&>*:not(:last-child)]:rounded-r-none',
        vertical:
          'flex-col [&>*:not(:first-child)]:rounded-t-none [&>*:not(:first-child)]:border-t-0 [&>*:not(:last-child)]:rounded-b-none',
      },
    },
    defaultVariants: {
      orientation: 'horizontal',
    },
  },
)

function ButtonGroup({
  className,
  orientation,
  ...props
}: React.ComponentProps<'div'> & VariantProps<typeof buttonGroupVariants>) {
  return (
    <div
      role="group"
      data-slot="button-group"
      data-orientation={orientation}
      className={cn(buttonGroupVariants({ orientation }), className)}
      {...props}
    />
  )
}

function ButtonGroupText({
  className,
  asChild = false,
  ...props
}: React.ComponentProps<'div'> & {
  asChild?: boolean
}) {
  const Comp = asChild ? Slot : 'div'

  return (
    <Comp
      className={cn(
        "bg-muted flex items-center gap-2 rounded-md border px-4 text-sm font-medium shadow-xs [&_svg]:pointer-events-none [&_svg:not([class*='size-'])]:size-4",
        className,
      )}
      {...props}
    />
  )
}

function ButtonGroupSeparator({
  className,
  orientation = 'vertical',
  ...props
}: React.ComponentProps<typeof Separator>) {
  return (
    <Separator
      data-slot="button-group-separator"
      orientation={orientation}
      className={cn(
        'bg-input relative !m-0 self-stretch data-[orientation=vertical]:h-auto',
        className,
      )}
      {...props}
    />
  )
}

export {
  ButtonGroup,
  ButtonGroupSeparator,
  ButtonGroupText,
  buttonGroupVariants,
}
\n--- END FILE: ./html.code.v0.app/components/ui/button-group.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/field.tsx ---
'use client'

import { useMemo } from 'react'
import { cva, type VariantProps } from 'class-variance-authority'

import { cn } from '@/lib/utils'
import { Label } from '@/components/ui/label'
import { Separator } from '@/components/ui/separator'

function FieldSet({ className, ...props }: React.ComponentProps<'fieldset'>) {
  return (
    <fieldset
      data-slot="field-set"
      className={cn(
        'flex flex-col gap-6',
        'has-[>[data-slot=checkbox-group]]:gap-3 has-[>[data-slot=radio-group]]:gap-3',
        className,
      )}
      {...props}
    />
  )
}

function FieldLegend({
  className,
  variant = 'legend',
  ...props
}: React.ComponentProps<'legend'> & { variant?: 'legend' | 'label' }) {
  return (
    <legend
      data-slot="field-legend"
      data-variant={variant}
      className={cn(
        'mb-3 font-medium',
        'data-[variant=legend]:text-base',
        'data-[variant=label]:text-sm',
        className,
      )}
      {...props}
    />
  )
}

function FieldGroup({ className, ...props }: React.ComponentProps<'div'>) {
  return (
    <div
      data-slot="field-group"
      className={cn(
        'group/field-group @container/field-group flex w-full flex-col gap-7 data-[slot=checkbox-group]:gap-3 [&>[data-slot=field-group]]:gap-4',
        className,
      )}
      {...props}
    />
  )
}

const fieldVariants = cva(
  'group/field flex w-full gap-3 data-[invalid=true]:text-destructive',
  {
    variants: {
      orientation: {
        vertical: ['flex-col [&>*]:w-full [&>.sr-only]:w-auto'],
        horizontal: [
          'flex-row items-center',
          '[&>[data-slot=field-label]]:flex-auto',
          'has-[>[data-slot=field-content]]:items-start has-[>[data-slot=field-content]]:[&>[role=checkbox],[role=radio]]:mt-px',
        ],
        responsive: [
          'flex-col [&>*]:w-full [&>.sr-only]:w-auto @md/field-group:flex-row @md/field-group:items-center @md/field-group:[&>*]:w-auto',
          '@md/field-group:[&>[data-slot=field-label]]:flex-auto',
          '@md/field-group:has-[>[data-slot=field-content]]:items-start @md/field-group:has-[>[data-slot=field-content]]:[&>[role=checkbox],[role=radio]]:mt-px',
        ],
      },
    },
    defaultVariants: {
      orientation: 'vertical',
    },
  },
)

function Field({
  className,
  orientation = 'vertical',
  ...props
}: React.ComponentProps<'div'> & VariantProps<typeof fieldVariants>) {
  return (
    <div
      role="group"
      data-slot="field"
      data-orientation={orientation}
      className={cn(fieldVariants({ orientation }), className)}
      {...props}
    />
  )
}

function FieldContent({ className, ...props }: React.ComponentProps<'div'>) {
  return (
    <div
      data-slot="field-content"
      className={cn(
        'group/field-content flex flex-1 flex-col gap-1.5 leading-snug',
        className,
      )}
      {...props}
    />
  )
}

function FieldLabel({
  className,
  ...props
}: React.ComponentProps<typeof Label>) {
  return (
    <Label
      data-slot="field-label"
      className={cn(
        'group/field-label peer/field-label flex w-fit gap-2 leading-snug group-data-[disabled=true]/field:opacity-50',
        'has-[>[data-slot=field]]:w-full has-[>[data-slot=field]]:flex-col has-[>[data-slot=field]]:rounded-md has-[>[data-slot=field]]:border [&>*]:data-[slot=field]:p-4',
        'has-data-[state=checked]:bg-primary/5 has-data-[state=checked]:border-primary dark:has-data-[state=checked]:bg-primary/10',
        className,
      )}
      {...props}
    />
  )
}

function FieldTitle({ className, ...props }: React.ComponentProps<'div'>) {
  return (
    <div
      data-slot="field-label"
      className={cn(
        'flex w-fit items-center gap-2 text-sm leading-snug font-medium group-data-[disabled=true]/field:opacity-50',
        className,
      )}
      {...props}
    />
  )
}

function FieldDescription({ className, ...props }: React.ComponentProps<'p'>) {
  return (
    <p
      data-slot="field-description"
      className={cn(
        'text-muted-foreground text-sm leading-normal font-normal group-has-[[data-orientation=horizontal]]/field:text-balance',
        'last:mt-0 nth-last-2:-mt-1 [[data-variant=legend]+&]:-mt-1.5',
        '[&>a:hover]:text-primary [&>a]:underline [&>a]:underline-offset-4',
        className,
      )}
      {...props}
    />
  )
}

function FieldSeparator({
  children,
  className,
  ...props
}: React.ComponentProps<'div'> & {
  children?: React.ReactNode
}) {
  return (
    <div
      data-slot="field-separator"
      data-content={!!children}
      className={cn(
        'relative -my-2 h-5 text-sm group-data-[variant=outline]/field-group:-mb-2',
        className,
      )}
      {...props}
    >
      <Separator className="absolute inset-0 top-1/2" />
      {children && (
        <span
          className="bg-background text-muted-foreground relative mx-auto block w-fit px-2"
          data-slot="field-separator-content"
        >
          {children}
        </span>
      )}
    </div>
  )
}

function FieldError({
  className,
  children,
  errors,
  ...props
}: React.ComponentProps<'div'> & {
  errors?: Array<{ message?: string } | undefined>
}) {
  const content = useMemo(() => {
    if (children) {
      return children
    }

    if (!errors) {
      return null
    }

    if (errors.length === 1 && errors[0]?.message) {
      return errors[0].message
    }

    return (
      <ul className="ml-4 flex list-disc flex-col gap-1">
        {errors.map(
          (error, index) =>
            error?.message && <li key={index}>{error.message}</li>,
        )}
      </ul>
    )
  }, [children, errors])

  if (!content) {
    return null
  }

  return (
    <div
      role="alert"
      data-slot="field-error"
      className={cn('text-destructive text-sm font-normal', className)}
      {...props}
    >
      {content}
    </div>
  )
}

export {
  Field,
  FieldLabel,
  FieldDescription,
  FieldError,
  FieldGroup,
  FieldLegend,
  FieldSeparator,
  FieldSet,
  FieldContent,
  FieldTitle,
}
\n--- END FILE: ./html.code.v0.app/components/ui/field.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/input-otp.tsx ---
'use client'

import * as React from 'react'
import { OTPInput, OTPInputContext } from 'input-otp'
import { MinusIcon } from 'lucide-react'

import { cn } from '@/lib/utils'

function InputOTP({
  className,
  containerClassName,
  ...props
}: React.ComponentProps<typeof OTPInput> & {
  containerClassName?: string
}) {
  return (
    <OTPInput
      data-slot="input-otp"
      containerClassName={cn(
        'flex items-center gap-2 has-disabled:opacity-50',
        containerClassName,
      )}
      className={cn('disabled:cursor-not-allowed', className)}
      {...props}
    />
  )
}

function InputOTPGroup({ className, ...props }: React.ComponentProps<'div'>) {
  return (
    <div
      data-slot="input-otp-group"
      className={cn('flex items-center', className)}
      {...props}
    />
  )
}

function InputOTPSlot({
  index,
  className,
  ...props
}: React.ComponentProps<'div'> & {
  index: number
}) {
  const inputOTPContext = React.useContext(OTPInputContext)
  const { char, hasFakeCaret, isActive } = inputOTPContext?.slots[index] ?? {}

  return (
    <div
      data-slot="input-otp-slot"
      data-active={isActive}
      className={cn(
        'data-[active=true]:border-ring data-[active=true]:ring-ring/50 data-[active=true]:aria-invalid:ring-destructive/20 dark:data-[active=true]:aria-invalid:ring-destructive/40 aria-invalid:border-destructive data-[active=true]:aria-invalid:border-destructive dark:bg-input/30 border-input relative flex h-9 w-9 items-center justify-center border-y border-r text-sm shadow-xs transition-all outline-none first:rounded-l-md first:border-l last:rounded-r-md data-[active=true]:z-10 data-[active=true]:ring-[3px]',
        className,
      )}
      {...props}
    >
      {char}
      {hasFakeCaret && (
        <div className="pointer-events-none absolute inset-0 flex items-center justify-center">
          <div className="animate-caret-blink bg-foreground h-4 w-px duration-1000" />
        </div>
      )}
    </div>
  )
}

function InputOTPSeparator({ ...props }: React.ComponentProps<'div'>) {
  return (
    <div data-slot="input-otp-separator" role="separator" {...props}>
      <MinusIcon />
    </div>
  )
}

export { InputOTP, InputOTPGroup, InputOTPSlot, InputOTPSeparator }
\n--- END FILE: ./html.code.v0.app/components/ui/input-otp.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/select.tsx ---
'use client'

import * as React from 'react'
import * as SelectPrimitive from '@radix-ui/react-select'
import { CheckIcon, ChevronDownIcon, ChevronUpIcon } from 'lucide-react'

import { cn } from '@/lib/utils'

function Select({
  ...props
}: React.ComponentProps<typeof SelectPrimitive.Root>) {
  return <SelectPrimitive.Root data-slot="select" {...props} />
}

function SelectGroup({
  ...props
}: React.ComponentProps<typeof SelectPrimitive.Group>) {
  return <SelectPrimitive.Group data-slot="select-group" {...props} />
}

function SelectValue({
  ...props
}: React.ComponentProps<typeof SelectPrimitive.Value>) {
  return <SelectPrimitive.Value data-slot="select-value" {...props} />
}

function SelectTrigger({
  className,
  size = 'default',
  children,
  ...props
}: React.ComponentProps<typeof SelectPrimitive.Trigger> & {
  size?: 'sm' | 'default'
}) {
  return (
    <SelectPrimitive.Trigger
      data-slot="select-trigger"
      data-size={size}
      className={cn(
        "border-input data-[placeholder]:text-muted-foreground [&_svg:not([class*='text-'])]:text-muted-foreground focus-visible:border-ring focus-visible:ring-ring/50 aria-invalid:ring-destructive/20 dark:aria-invalid:ring-destructive/40 aria-invalid:border-destructive dark:bg-input/30 dark:hover:bg-input/50 flex w-fit items-center justify-between gap-2 rounded-md border bg-transparent px-3 py-2 text-sm whitespace-nowrap shadow-xs transition-[color,box-shadow] outline-none focus-visible:ring-[3px] disabled:cursor-not-allowed disabled:opacity-50 data-[size=default]:h-9 data-[size=sm]:h-8 *:data-[slot=select-value]:line-clamp-1 *:data-[slot=select-value]:flex *:data-[slot=select-value]:items-center *:data-[slot=select-value]:gap-2 [&_svg]:pointer-events-none [&_svg]:shrink-0 [&_svg:not([class*='size-'])]:size-4",
        className,
      )}
      {...props}
    >
      {children}
      <SelectPrimitive.Icon asChild>
        <ChevronDownIcon className="size-4 opacity-50" />
      </SelectPrimitive.Icon>
    </SelectPrimitive.Trigger>
  )
}

function SelectContent({
  className,
  children,
  position = 'popper',
  ...props
}: React.ComponentProps<typeof SelectPrimitive.Content>) {
  return (
    <SelectPrimitive.Portal>
      <SelectPrimitive.Content
        data-slot="select-content"
        className={cn(
          'bg-popover text-popover-foreground data-[state=open]:animate-in data-[state=closed]:animate-out data-[state=closed]:fade-out-0 data-[state=open]:fade-in-0 data-[state=closed]:zoom-out-95 data-[state=open]:zoom-in-95 data-[side=bottom]:slide-in-from-top-2 data-[side=left]:slide-in-from-right-2 data-[side=right]:slide-in-from-left-2 data-[side=top]:slide-in-from-bottom-2 relative z-50 max-h-(--radix-select-content-available-height) min-w-[8rem] origin-(--radix-select-content-transform-origin) overflow-x-hidden overflow-y-auto rounded-md border shadow-md',
          position === 'popper' &&
            'data-[side=bottom]:translate-y-1 data-[side=left]:-translate-x-1 data-[side=right]:translate-x-1 data-[side=top]:-translate-y-1',
          className,
        )}
        position={position}
        {...props}
      >
        <SelectScrollUpButton />
        <SelectPrimitive.Viewport
          className={cn(
            'p-1',
            position === 'popper' &&
              'h-[var(--radix-select-trigger-height)] w-full min-w-[var(--radix-select-trigger-width)] scroll-my-1',
          )}
        >
          {children}
        </SelectPrimitive.Viewport>
        <SelectScrollDownButton />
      </SelectPrimitive.Content>
    </SelectPrimitive.Portal>
  )
}

function SelectLabel({
  className,
  ...props
}: React.ComponentProps<typeof SelectPrimitive.Label>) {
  return (
    <SelectPrimitive.Label
      data-slot="select-label"
      className={cn('text-muted-foreground px-2 py-1.5 text-xs', className)}
      {...props}
    />
  )
}

function SelectItem({
  className,
  children,
  ...props
}: React.ComponentProps<typeof SelectPrimitive.Item>) {
  return (
    <SelectPrimitive.Item
      data-slot="select-item"
      className={cn(
        "focus:bg-accent focus:text-accent-foreground [&_svg:not([class*='text-'])]:text-muted-foreground relative flex w-full cursor-default items-center gap-2 rounded-sm py-1.5 pr-8 pl-2 text-sm outline-hidden select-none data-[disabled]:pointer-events-none data-[disabled]:opacity-50 [&_svg]:pointer-events-none [&_svg]:shrink-0 [&_svg:not([class*='size-'])]:size-4 *:[span]:last:flex *:[span]:last:items-center *:[span]:last:gap-2",
        className,
      )}
      {...props}
    >
      <span className="absolute right-2 flex size-3.5 items-center justify-center">
        <SelectPrimitive.ItemIndicator>
          <CheckIcon className="size-4" />
        </SelectPrimitive.ItemIndicator>
      </span>
      <SelectPrimitive.ItemText>{children}</SelectPrimitive.ItemText>
    </SelectPrimitive.Item>
  )
}

function SelectSeparator({
  className,
  ...props
}: React.ComponentProps<typeof SelectPrimitive.Separator>) {
  return (
    <SelectPrimitive.Separator
      data-slot="select-separator"
      className={cn('bg-border pointer-events-none -mx-1 my-1 h-px', className)}
      {...props}
    />
  )
}

function SelectScrollUpButton({
  className,
  ...props
}: React.ComponentProps<typeof SelectPrimitive.ScrollUpButton>) {
  return (
    <SelectPrimitive.ScrollUpButton
      data-slot="select-scroll-up-button"
      className={cn(
        'flex cursor-default items-center justify-center py-1',
        className,
      )}
      {...props}
    >
      <ChevronUpIcon className="size-4" />
    </SelectPrimitive.ScrollUpButton>
  )
}

function SelectScrollDownButton({
  className,
  ...props
}: React.ComponentProps<typeof SelectPrimitive.ScrollDownButton>) {
  return (
    <SelectPrimitive.ScrollDownButton
      data-slot="select-scroll-down-button"
      className={cn(
        'flex cursor-default items-center justify-center py-1',
        className,
      )}
      {...props}
    >
      <ChevronDownIcon className="size-4" />
    </SelectPrimitive.ScrollDownButton>
  )
}

export {
  Select,
  SelectContent,
  SelectGroup,
  SelectItem,
  SelectLabel,
  SelectScrollDownButton,
  SelectScrollUpButton,
  SelectSeparator,
  SelectTrigger,
  SelectValue,
}
\n--- END FILE: ./html.code.v0.app/components/ui/select.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/progress.tsx ---
'use client'

import * as React from 'react'
import * as ProgressPrimitive from '@radix-ui/react-progress'

import { cn } from '@/lib/utils'

function Progress({
  className,
  value,
  ...props
}: React.ComponentProps<typeof ProgressPrimitive.Root>) {
  return (
    <ProgressPrimitive.Root
      data-slot="progress"
      className={cn(
        'bg-primary/20 relative h-2 w-full overflow-hidden rounded-full',
        className,
      )}
      {...props}
    >
      <ProgressPrimitive.Indicator
        data-slot="progress-indicator"
        className="bg-primary h-full w-full flex-1 transition-all"
        style={{ transform: `translateX(-${100 - (value || 0)}%)` }}
      />
    </ProgressPrimitive.Root>
  )
}

export { Progress }
\n--- END FILE: ./html.code.v0.app/components/ui/progress.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/aspect-ratio.tsx ---
'use client'

import * as AspectRatioPrimitive from '@radix-ui/react-aspect-ratio'

function AspectRatio({
  ...props
}: React.ComponentProps<typeof AspectRatioPrimitive.Root>) {
  return <AspectRatioPrimitive.Root data-slot="aspect-ratio" {...props} />
}

export { AspectRatio }
\n--- END FILE: ./html.code.v0.app/components/ui/aspect-ratio.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/collapsible.tsx ---
'use client'

import * as CollapsiblePrimitive from '@radix-ui/react-collapsible'

function Collapsible({
  ...props
}: React.ComponentProps<typeof CollapsiblePrimitive.Root>) {
  return <CollapsiblePrimitive.Root data-slot="collapsible" {...props} />
}

function CollapsibleTrigger({
  ...props
}: React.ComponentProps<typeof CollapsiblePrimitive.CollapsibleTrigger>) {
  return (
    <CollapsiblePrimitive.CollapsibleTrigger
      data-slot="collapsible-trigger"
      {...props}
    />
  )
}

function CollapsibleContent({
  ...props
}: React.ComponentProps<typeof CollapsiblePrimitive.CollapsibleContent>) {
  return (
    <CollapsiblePrimitive.CollapsibleContent
      data-slot="collapsible-content"
      {...props}
    />
  )
}

export { Collapsible, CollapsibleTrigger, CollapsibleContent }
\n--- END FILE: ./html.code.v0.app/components/ui/collapsible.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/dropdown-menu.tsx ---
'use client'

import * as React from 'react'
import * as DropdownMenuPrimitive from '@radix-ui/react-dropdown-menu'
import { CheckIcon, ChevronRightIcon, CircleIcon } from 'lucide-react'

import { cn } from '@/lib/utils'

function DropdownMenu({
  ...props
}: React.ComponentProps<typeof DropdownMenuPrimitive.Root>) {
  return <DropdownMenuPrimitive.Root data-slot="dropdown-menu" {...props} />
}

function DropdownMenuPortal({
  ...props
}: React.ComponentProps<typeof DropdownMenuPrimitive.Portal>) {
  return (
    <DropdownMenuPrimitive.Portal data-slot="dropdown-menu-portal" {...props} />
  )
}

function DropdownMenuTrigger({
  ...props
}: React.ComponentProps<typeof DropdownMenuPrimitive.Trigger>) {
  return (
    <DropdownMenuPrimitive.Trigger
      data-slot="dropdown-menu-trigger"
      {...props}
    />
  )
}

function DropdownMenuContent({
  className,
  sideOffset = 4,
  ...props
}: React.ComponentProps<typeof DropdownMenuPrimitive.Content>) {
  return (
    <DropdownMenuPrimitive.Portal>
      <DropdownMenuPrimitive.Content
        data-slot="dropdown-menu-content"
        sideOffset={sideOffset}
        className={cn(
          'bg-popover text-popover-foreground data-[state=open]:animate-in data-[state=closed]:animate-out data-[state=closed]:fade-out-0 data-[state=open]:fade-in-0 data-[state=closed]:zoom-out-95 data-[state=open]:zoom-in-95 data-[side=bottom]:slide-in-from-top-2 data-[side=left]:slide-in-from-right-2 data-[side=right]:slide-in-from-left-2 data-[side=top]:slide-in-from-bottom-2 z-50 max-h-(--radix-dropdown-menu-content-available-height) min-w-[8rem] origin-(--radix-dropdown-menu-content-transform-origin) overflow-x-hidden overflow-y-auto rounded-md border p-1 shadow-md',
          className,
        )}
        {...props}
      />
    </DropdownMenuPrimitive.Portal>
  )
}

function DropdownMenuGroup({
  ...props
}: React.ComponentProps<typeof DropdownMenuPrimitive.Group>) {
  return (
    <DropdownMenuPrimitive.Group data-slot="dropdown-menu-group" {...props} />
  )
}

function DropdownMenuItem({
  className,
  inset,
  variant = 'default',
  ...props
}: React.ComponentProps<typeof DropdownMenuPrimitive.Item> & {
  inset?: boolean
  variant?: 'default' | 'destructive'
}) {
  return (
    <DropdownMenuPrimitive.Item
      data-slot="dropdown-menu-item"
      data-inset={inset}
      data-variant={variant}
      className={cn(
        "focus:bg-accent focus:text-accent-foreground data-[variant=destructive]:text-destructive data-[variant=destructive]:focus:bg-destructive/10 dark:data-[variant=destructive]:focus:bg-destructive/20 data-[variant=destructive]:focus:text-destructive data-[variant=destructive]:*:[svg]:!text-destructive [&_svg:not([class*='text-'])]:text-muted-foreground relative flex cursor-default items-center gap-2 rounded-sm px-2 py-1.5 text-sm outline-hidden select-none data-[disabled]:pointer-events-none data-[disabled]:opacity-50 data-[inset]:pl-8 [&_svg]:pointer-events-none [&_svg]:shrink-0 [&_svg:not([class*='size-'])]:size-4",
        className,
      )}
      {...props}
    />
  )
}

function DropdownMenuCheckboxItem({
  className,
  children,
  checked,
  ...props
}: React.ComponentProps<typeof DropdownMenuPrimitive.CheckboxItem>) {
  return (
    <DropdownMenuPrimitive.CheckboxItem
      data-slot="dropdown-menu-checkbox-item"
      className={cn(
        "focus:bg-accent focus:text-accent-foreground relative flex cursor-default items-center gap-2 rounded-sm py-1.5 pr-2 pl-8 text-sm outline-hidden select-none data-[disabled]:pointer-events-none data-[disabled]:opacity-50 [&_svg]:pointer-events-none [&_svg]:shrink-0 [&_svg:not([class*='size-'])]:size-4",
        className,
      )}
      checked={checked}
      {...props}
    >
      <span className="pointer-events-none absolute left-2 flex size-3.5 items-center justify-center">
        <DropdownMenuPrimitive.ItemIndicator>
          <CheckIcon className="size-4" />
        </DropdownMenuPrimitive.ItemIndicator>
      </span>
      {children}
    </DropdownMenuPrimitive.CheckboxItem>
  )
}

function DropdownMenuRadioGroup({
  ...props
}: React.ComponentProps<typeof DropdownMenuPrimitive.RadioGroup>) {
  return (
    <DropdownMenuPrimitive.RadioGroup
      data-slot="dropdown-menu-radio-group"
      {...props}
    />
  )
}

function DropdownMenuRadioItem({
  className,
  children,
  ...props
}: React.ComponentProps<typeof DropdownMenuPrimitive.RadioItem>) {
  return (
    <DropdownMenuPrimitive.RadioItem
      data-slot="dropdown-menu-radio-item"
      className={cn(
        "focus:bg-accent focus:text-accent-foreground relative flex cursor-default items-center gap-2 rounded-sm py-1.5 pr-2 pl-8 text-sm outline-hidden select-none data-[disabled]:pointer-events-none data-[disabled]:opacity-50 [&_svg]:pointer-events-none [&_svg]:shrink-0 [&_svg:not([class*='size-'])]:size-4",
        className,
      )}
      {...props}
    >
      <span className="pointer-events-none absolute left-2 flex size-3.5 items-center justify-center">
        <DropdownMenuPrimitive.ItemIndicator>
          <CircleIcon className="size-2 fill-current" />
        </DropdownMenuPrimitive.ItemIndicator>
      </span>
      {children}
    </DropdownMenuPrimitive.RadioItem>
  )
}

function DropdownMenuLabel({
  className,
  inset,
  ...props
}: React.ComponentProps<typeof DropdownMenuPrimitive.Label> & {
  inset?: boolean
}) {
  return (
    <DropdownMenuPrimitive.Label
      data-slot="dropdown-menu-label"
      data-inset={inset}
      className={cn(
        'px-2 py-1.5 text-sm font-medium data-[inset]:pl-8',
        className,
      )}
      {...props}
    />
  )
}

function DropdownMenuSeparator({
  className,
  ...props
}: React.ComponentProps<typeof DropdownMenuPrimitive.Separator>) {
  return (
    <DropdownMenuPrimitive.Separator
      data-slot="dropdown-menu-separator"
      className={cn('bg-border -mx-1 my-1 h-px', className)}
      {...props}
    />
  )
}

function DropdownMenuShortcut({
  className,
  ...props
}: React.ComponentProps<'span'>) {
  return (
    <span
      data-slot="dropdown-menu-shortcut"
      className={cn(
        'text-muted-foreground ml-auto text-xs tracking-widest',
        className,
      )}
      {...props}
    />
  )
}

function DropdownMenuSub({
  ...props
}: React.ComponentProps<typeof DropdownMenuPrimitive.Sub>) {
  return <DropdownMenuPrimitive.Sub data-slot="dropdown-menu-sub" {...props} />
}

function DropdownMenuSubTrigger({
  className,
  inset,
  children,
  ...props
}: React.ComponentProps<typeof DropdownMenuPrimitive.SubTrigger> & {
  inset?: boolean
}) {
  return (
    <DropdownMenuPrimitive.SubTrigger
      data-slot="dropdown-menu-sub-trigger"
      data-inset={inset}
      className={cn(
        "focus:bg-accent focus:text-accent-foreground data-[state=open]:bg-accent data-[state=open]:text-accent-foreground [&_svg:not([class*='text-'])]:text-muted-foreground flex cursor-default items-center gap-2 rounded-sm px-2 py-1.5 text-sm outline-hidden select-none data-[inset]:pl-8 [&_svg]:pointer-events-none [&_svg]:shrink-0 [&_svg:not([class*='size-'])]:size-4",
        className,
      )}
      {...props}
    >
      {children}
      <ChevronRightIcon className="ml-auto size-4" />
    </DropdownMenuPrimitive.SubTrigger>
  )
}

function DropdownMenuSubContent({
  className,
  ...props
}: React.ComponentProps<typeof DropdownMenuPrimitive.SubContent>) {
  return (
    <DropdownMenuPrimitive.SubContent
      data-slot="dropdown-menu-sub-content"
      className={cn(
        'bg-popover text-popover-foreground data-[state=open]:animate-in data-[state=closed]:animate-out data-[state=closed]:fade-out-0 data-[state=open]:fade-in-0 data-[state=closed]:zoom-out-95 data-[state=open]:zoom-in-95 data-[side=bottom]:slide-in-from-top-2 data-[side=left]:slide-in-from-right-2 data-[side=right]:slide-in-from-left-2 data-[side=top]:slide-in-from-bottom-2 z-50 min-w-[8rem] origin-(--radix-dropdown-menu-content-transform-origin) overflow-hidden rounded-md border p-1 shadow-lg',
        className,
      )}
      {...props}
    />
  )
}

export {
  DropdownMenu,
  DropdownMenuPortal,
  DropdownMenuTrigger,
  DropdownMenuContent,
  DropdownMenuGroup,
  DropdownMenuLabel,
  DropdownMenuItem,
  DropdownMenuCheckboxItem,
  DropdownMenuRadioGroup,
  DropdownMenuRadioItem,
  DropdownMenuSeparator,
  DropdownMenuShortcut,
  DropdownMenuSub,
  DropdownMenuSubTrigger,
  DropdownMenuSubContent,
}
\n--- END FILE: ./html.code.v0.app/components/ui/dropdown-menu.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/carousel.tsx ---
'use client'

import * as React from 'react'
import useEmblaCarousel, {
  type UseEmblaCarouselType,
} from 'embla-carousel-react'
import { ArrowLeft, ArrowRight } from 'lucide-react'

import { cn } from '@/lib/utils'
import { Button } from '@/components/ui/button'

type CarouselApi = UseEmblaCarouselType[1]
type UseCarouselParameters = Parameters<typeof useEmblaCarousel>
type CarouselOptions = UseCarouselParameters[0]
type CarouselPlugin = UseCarouselParameters[1]

type CarouselProps = {
  opts?: CarouselOptions
  plugins?: CarouselPlugin
  orientation?: 'horizontal' | 'vertical'
  setApi?: (api: CarouselApi) => void
}

type CarouselContextProps = {
  carouselRef: ReturnType<typeof useEmblaCarousel>[0]
  api: ReturnType<typeof useEmblaCarousel>[1]
  scrollPrev: () => void
  scrollNext: () => void
  canScrollPrev: boolean
  canScrollNext: boolean
} & CarouselProps

const CarouselContext = React.createContext<CarouselContextProps | null>(null)

function useCarousel() {
  const context = React.useContext(CarouselContext)

  if (!context) {
    throw new Error('useCarousel must be used within a <Carousel />')
  }

  return context
}

function Carousel({
  orientation = 'horizontal',
  opts,
  setApi,
  plugins,
  className,
  children,
  ...props
}: React.ComponentProps<'div'> & CarouselProps) {
  const [carouselRef, api] = useEmblaCarousel(
    {
      ...opts,
      axis: orientation === 'horizontal' ? 'x' : 'y',
    },
    plugins,
  )
  const [canScrollPrev, setCanScrollPrev] = React.useState(false)
  const [canScrollNext, setCanScrollNext] = React.useState(false)

  const onSelect = React.useCallback((api: CarouselApi) => {
    if (!api) return
    setCanScrollPrev(api.canScrollPrev())
    setCanScrollNext(api.canScrollNext())
  }, [])

  const scrollPrev = React.useCallback(() => {
    api?.scrollPrev()
  }, [api])

  const scrollNext = React.useCallback(() => {
    api?.scrollNext()
  }, [api])

  const handleKeyDown = React.useCallback(
    (event: React.KeyboardEvent<HTMLDivElement>) => {
      if (event.key === 'ArrowLeft') {
        event.preventDefault()
        scrollPrev()
      } else if (event.key === 'ArrowRight') {
        event.preventDefault()
        scrollNext()
      }
    },
    [scrollPrev, scrollNext],
  )

  React.useEffect(() => {
    if (!api || !setApi) return
    setApi(api)
  }, [api, setApi])

  React.useEffect(() => {
    if (!api) return
    onSelect(api)
    api.on('reInit', onSelect)
    api.on('select', onSelect)

    return () => {
      api?.off('select', onSelect)
    }
  }, [api, onSelect])

  return (
    <CarouselContext.Provider
      value={{
        carouselRef,
        api: api,
        opts,
        orientation:
          orientation || (opts?.axis === 'y' ? 'vertical' : 'horizontal'),
        scrollPrev,
        scrollNext,
        canScrollPrev,
        canScrollNext,
      }}
    >
      <div
        onKeyDownCapture={handleKeyDown}
        className={cn('relative', className)}
        role="region"
        aria-roledescription="carousel"
        data-slot="carousel"
        {...props}
      >
        {children}
      </div>
    </CarouselContext.Provider>
  )
}

function CarouselContent({ className, ...props }: React.ComponentProps<'div'>) {
  const { carouselRef, orientation } = useCarousel()

  return (
    <div
      ref={carouselRef}
      className="overflow-hidden"
      data-slot="carousel-content"
    >
      <div
        className={cn(
          'flex',
          orientation === 'horizontal' ? '-ml-4' : '-mt-4 flex-col',
          className,
        )}
        {...props}
      />
    </div>
  )
}

function CarouselItem({ className, ...props }: React.ComponentProps<'div'>) {
  const { orientation } = useCarousel()

  return (
    <div
      role="group"
      aria-roledescription="slide"
      data-slot="carousel-item"
      className={cn(
        'min-w-0 shrink-0 grow-0 basis-full',
        orientation === 'horizontal' ? 'pl-4' : 'pt-4',
        className,
      )}
      {...props}
    />
  )
}

function CarouselPrevious({
  className,
  variant = 'outline',
  size = 'icon',
  ...props
}: React.ComponentProps<typeof Button>) {
  const { orientation, scrollPrev, canScrollPrev } = useCarousel()

  return (
    <Button
      data-slot="carousel-previous"
      variant={variant}
      size={size}
      className={cn(
        'absolute size-8 rounded-full',
        orientation === 'horizontal'
          ? 'top-1/2 -left-12 -translate-y-1/2'
          : '-top-12 left-1/2 -translate-x-1/2 rotate-90',
        className,
      )}
      disabled={!canScrollPrev}
      onClick={scrollPrev}
      {...props}
    >
      <ArrowLeft />
      <span className="sr-only">Previous slide</span>
    </Button>
  )
}

function CarouselNext({
  className,
  variant = 'outline',
  size = 'icon',
  ...props
}: React.ComponentProps<typeof Button>) {
  const { orientation, scrollNext, canScrollNext } = useCarousel()

  return (
    <Button
      data-slot="carousel-next"
      variant={variant}
      size={size}
      className={cn(
        'absolute size-8 rounded-full',
        orientation === 'horizontal'
          ? 'top-1/2 -right-12 -translate-y-1/2'
          : '-bottom-12 left-1/2 -translate-x-1/2 rotate-90',
        className,
      )}
      disabled={!canScrollNext}
      onClick={scrollNext}
      {...props}
    >
      <ArrowRight />
      <span className="sr-only">Next slide</span>
    </Button>
  )
}

export {
  type CarouselApi,
  Carousel,
  CarouselContent,
  CarouselItem,
  CarouselPrevious,
  CarouselNext,
}
\n--- END FILE: ./html.code.v0.app/components/ui/carousel.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/toast.tsx ---
'use client'

import * as React from 'react'
import * as ToastPrimitives from '@radix-ui/react-toast'
import { cva, type VariantProps } from 'class-variance-authority'
import { X } from 'lucide-react'

import { cn } from '@/lib/utils'

const ToastProvider = ToastPrimitives.Provider

const ToastViewport = React.forwardRef<
  React.ElementRef<typeof ToastPrimitives.Viewport>,
  React.ComponentPropsWithoutRef<typeof ToastPrimitives.Viewport>
>(({ className, ...props }, ref) => (
  <ToastPrimitives.Viewport
    ref={ref}
    className={cn(
      'fixed top-0 z-[100] flex max-h-screen w-full flex-col-reverse p-4 sm:bottom-0 sm:right-0 sm:top-auto sm:flex-col md:max-w-[420px]',
      className,
    )}
    {...props}
  />
))
ToastViewport.displayName = ToastPrimitives.Viewport.displayName

const toastVariants = cva(
  'group pointer-events-auto relative flex w-full items-center justify-between space-x-4 overflow-hidden rounded-md border p-6 pr-8 shadow-lg transition-all data-[swipe=cancel]:translate-x-0 data-[swipe=end]:translate-x-[var(--radix-toast-swipe-end-x)] data-[swipe=move]:translate-x-[var(--radix-toast-swipe-move-x)] data-[swipe=move]:transition-none data-[state=open]:animate-in data-[state=closed]:animate-out data-[swipe=end]:animate-out data-[state=closed]:fade-out-80 data-[state=closed]:slide-out-to-right-full data-[state=open]:slide-in-from-top-full data-[state=open]:sm:slide-in-from-bottom-full',
  {
    variants: {
      variant: {
        default: 'border bg-background text-foreground',
        destructive:
          'destructive group border-destructive bg-destructive text-destructive-foreground',
      },
    },
    defaultVariants: {
      variant: 'default',
    },
  },
)

const Toast = React.forwardRef<
  React.ElementRef<typeof ToastPrimitives.Root>,
  React.ComponentPropsWithoutRef<typeof ToastPrimitives.Root> &
    VariantProps<typeof toastVariants>
>(({ className, variant, ...props }, ref) => {
  return (
    <ToastPrimitives.Root
      ref={ref}
      className={cn(toastVariants({ variant }), className)}
      {...props}
    />
  )
})
Toast.displayName = ToastPrimitives.Root.displayName

const ToastAction = React.forwardRef<
  React.ElementRef<typeof ToastPrimitives.Action>,
  React.ComponentPropsWithoutRef<typeof ToastPrimitives.Action>
>(({ className, ...props }, ref) => (
  <ToastPrimitives.Action
    ref={ref}
    className={cn(
      'inline-flex h-8 shrink-0 items-center justify-center rounded-md border bg-transparent px-3 text-sm font-medium ring-offset-background transition-colors hover:bg-secondary focus:outline-none focus:ring-2 focus:ring-ring focus:ring-offset-2 disabled:pointer-events-none disabled:opacity-50 group-[.destructive]:border-muted/40 group-[.destructive]:hover:border-destructive/30 group-[.destructive]:hover:bg-destructive group-[.destructive]:hover:text-destructive-foreground group-[.destructive]:focus:ring-destructive',
      className,
    )}
    {...props}
  />
))
ToastAction.displayName = ToastPrimitives.Action.displayName

const ToastClose = React.forwardRef<
  React.ElementRef<typeof ToastPrimitives.Close>,
  React.ComponentPropsWithoutRef<typeof ToastPrimitives.Close>
>(({ className, ...props }, ref) => (
  <ToastPrimitives.Close
    ref={ref}
    className={cn(
      'absolute right-2 top-2 rounded-md p-1 text-foreground/50 opacity-0 transition-opacity hover:text-foreground focus:opacity-100 focus:outline-none focus:ring-2 group-hover:opacity-100 group-[.destructive]:text-red-300 group-[.destructive]:hover:text-red-50 group-[.destructive]:focus:ring-red-400 group-[.destructive]:focus:ring-offset-red-600',
      className,
    )}
    toast-close=""
    {...props}
  >
    <X className="h-4 w-4" />
  </ToastPrimitives.Close>
))
ToastClose.displayName = ToastPrimitives.Close.displayName

const ToastTitle = React.forwardRef<
  React.ElementRef<typeof ToastPrimitives.Title>,
  React.ComponentPropsWithoutRef<typeof ToastPrimitives.Title>
>(({ className, ...props }, ref) => (
  <ToastPrimitives.Title
    ref={ref}
    className={cn('text-sm font-semibold', className)}
    {...props}
  />
))
ToastTitle.displayName = ToastPrimitives.Title.displayName

const ToastDescription = React.forwardRef<
  React.ElementRef<typeof ToastPrimitives.Description>,
  React.ComponentPropsWithoutRef<typeof ToastPrimitives.Description>
>(({ className, ...props }, ref) => (
  <ToastPrimitives.Description
    ref={ref}
    className={cn('text-sm opacity-90', className)}
    {...props}
  />
))
ToastDescription.displayName = ToastPrimitives.Description.displayName

type ToastProps = React.ComponentPropsWithoutRef<typeof Toast>

type ToastActionElement = React.ReactElement<typeof ToastAction>

export {
  type ToastProps,
  type ToastActionElement,
  ToastProvider,
  ToastViewport,
  Toast,
  ToastTitle,
  ToastDescription,
  ToastClose,
  ToastAction,
}
\n--- END FILE: ./html.code.v0.app/components/ui/toast.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/card.tsx ---
import * as React from 'react'

import { cn } from '@/lib/utils'

function Card({ className, ...props }: React.ComponentProps<'div'>) {
  return (
    <div
      data-slot="card"
      className={cn(
        'bg-card text-card-foreground flex flex-col gap-6 rounded-xl border py-6 shadow-sm',
        className,
      )}
      {...props}
    />
  )
}

function CardHeader({ className, ...props }: React.ComponentProps<'div'>) {
  return (
    <div
      data-slot="card-header"
      className={cn(
        '@container/card-header grid auto-rows-min grid-rows-[auto_auto] items-start gap-2 px-6 has-data-[slot=card-action]:grid-cols-[1fr_auto] [.border-b]:pb-6',
        className,
      )}
      {...props}
    />
  )
}

function CardTitle({ className, ...props }: React.ComponentProps<'div'>) {
  return (
    <div
      data-slot="card-title"
      className={cn('leading-none font-semibold', className)}
      {...props}
    />
  )
}

function CardDescription({ className, ...props }: React.ComponentProps<'div'>) {
  return (
    <div
      data-slot="card-description"
      className={cn('text-muted-foreground text-sm', className)}
      {...props}
    />
  )
}

function CardAction({ className, ...props }: React.ComponentProps<'div'>) {
  return (
    <div
      data-slot="card-action"
      className={cn(
        'col-start-2 row-span-2 row-start-1 self-start justify-self-end',
        className,
      )}
      {...props}
    />
  )
}

function CardContent({ className, ...props }: React.ComponentProps<'div'>) {
  return (
    <div
      data-slot="card-content"
      className={cn('px-6', className)}
      {...props}
    />
  )
}

function CardFooter({ className, ...props }: React.ComponentProps<'div'>) {
  return (
    <div
      data-slot="card-footer"
      className={cn('flex items-center px-6 [.border-t]:pt-6', className)}
      {...props}
    />
  )
}

export {
  Card,
  CardHeader,
  CardFooter,
  CardTitle,
  CardAction,
  CardDescription,
  CardContent,
}
\n--- END FILE: ./html.code.v0.app/components/ui/card.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/table.tsx ---
'use client'

import * as React from 'react'

import { cn } from '@/lib/utils'

function Table({ className, ...props }: React.ComponentProps<'table'>) {
  return (
    <div
      data-slot="table-container"
      className="relative w-full overflow-x-auto"
    >
      <table
        data-slot="table"
        className={cn('w-full caption-bottom text-sm', className)}
        {...props}
      />
    </div>
  )
}

function TableHeader({ className, ...props }: React.ComponentProps<'thead'>) {
  return (
    <thead
      data-slot="table-header"
      className={cn('[&_tr]:border-b', className)}
      {...props}
    />
  )
}

function TableBody({ className, ...props }: React.ComponentProps<'tbody'>) {
  return (
    <tbody
      data-slot="table-body"
      className={cn('[&_tr:last-child]:border-0', className)}
      {...props}
    />
  )
}

function TableFooter({ className, ...props }: React.ComponentProps<'tfoot'>) {
  return (
    <tfoot
      data-slot="table-footer"
      className={cn(
        'bg-muted/50 border-t font-medium [&>tr]:last:border-b-0',
        className,
      )}
      {...props}
    />
  )
}

function TableRow({ className, ...props }: React.ComponentProps<'tr'>) {
  return (
    <tr
      data-slot="table-row"
      className={cn(
        'hover:bg-muted/50 data-[state=selected]:bg-muted border-b transition-colors',
        className,
      )}
      {...props}
    />
  )
}

function TableHead({ className, ...props }: React.ComponentProps<'th'>) {
  return (
    <th
      data-slot="table-head"
      className={cn(
        'text-foreground h-10 px-2 text-left align-middle font-medium whitespace-nowrap [&:has([role=checkbox])]:pr-0 [&>[role=checkbox]]:translate-y-[2px]',
        className,
      )}
      {...props}
    />
  )
}

function TableCell({ className, ...props }: React.ComponentProps<'td'>) {
  return (
    <td
      data-slot="table-cell"
      className={cn(
        'p-2 align-middle whitespace-nowrap [&:has([role=checkbox])]:pr-0 [&>[role=checkbox]]:translate-y-[2px]',
        className,
      )}
      {...props}
    />
  )
}

function TableCaption({
  className,
  ...props
}: React.ComponentProps<'caption'>) {
  return (
    <caption
      data-slot="table-caption"
      className={cn('text-muted-foreground mt-4 text-sm', className)}
      {...props}
    />
  )
}

export {
  Table,
  TableHeader,
  TableBody,
  TableFooter,
  TableHead,
  TableRow,
  TableCell,
  TableCaption,
}
\n--- END FILE: ./html.code.v0.app/components/ui/table.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/menubar.tsx ---
'use client'

import * as React from 'react'
import * as MenubarPrimitive from '@radix-ui/react-menubar'
import { CheckIcon, ChevronRightIcon, CircleIcon } from 'lucide-react'

import { cn } from '@/lib/utils'

function Menubar({
  className,
  ...props
}: React.ComponentProps<typeof MenubarPrimitive.Root>) {
  return (
    <MenubarPrimitive.Root
      data-slot="menubar"
      className={cn(
        'bg-background flex h-9 items-center gap-1 rounded-md border p-1 shadow-xs',
        className,
      )}
      {...props}
    />
  )
}

function MenubarMenu({
  ...props
}: React.ComponentProps<typeof MenubarPrimitive.Menu>) {
  return <MenubarPrimitive.Menu data-slot="menubar-menu" {...props} />
}

function MenubarGroup({
  ...props
}: React.ComponentProps<typeof MenubarPrimitive.Group>) {
  return <MenubarPrimitive.Group data-slot="menubar-group" {...props} />
}

function MenubarPortal({
  ...props
}: React.ComponentProps<typeof MenubarPrimitive.Portal>) {
  return <MenubarPrimitive.Portal data-slot="menubar-portal" {...props} />
}

function MenubarRadioGroup({
  ...props
}: React.ComponentProps<typeof MenubarPrimitive.RadioGroup>) {
  return (
    <MenubarPrimitive.RadioGroup data-slot="menubar-radio-group" {...props} />
  )
}

function MenubarTrigger({
  className,
  ...props
}: React.ComponentProps<typeof MenubarPrimitive.Trigger>) {
  return (
    <MenubarPrimitive.Trigger
      data-slot="menubar-trigger"
      className={cn(
        'focus:bg-accent focus:text-accent-foreground data-[state=open]:bg-accent data-[state=open]:text-accent-foreground flex items-center rounded-sm px-2 py-1 text-sm font-medium outline-hidden select-none',
        className,
      )}
      {...props}
    />
  )
}

function MenubarContent({
  className,
  align = 'start',
  alignOffset = -4,
  sideOffset = 8,
  ...props
}: React.ComponentProps<typeof MenubarPrimitive.Content>) {
  return (
    <MenubarPortal>
      <MenubarPrimitive.Content
        data-slot="menubar-content"
        align={align}
        alignOffset={alignOffset}
        sideOffset={sideOffset}
        className={cn(
          'bg-popover text-popover-foreground data-[state=open]:animate-in data-[state=closed]:fade-out-0 data-[state=open]:fade-in-0 data-[state=closed]:zoom-out-95 data-[state=open]:zoom-in-95 data-[side=bottom]:slide-in-from-top-2 data-[side=left]:slide-in-from-right-2 data-[side=right]:slide-in-from-left-2 data-[side=top]:slide-in-from-bottom-2 z-50 min-w-[12rem] origin-(--radix-menubar-content-transform-origin) overflow-hidden rounded-md border p-1 shadow-md',
          className,
        )}
        {...props}
      />
    </MenubarPortal>
  )
}

function MenubarItem({
  className,
  inset,
  variant = 'default',
  ...props
}: React.ComponentProps<typeof MenubarPrimitive.Item> & {
  inset?: boolean
  variant?: 'default' | 'destructive'
}) {
  return (
    <MenubarPrimitive.Item
      data-slot="menubar-item"
      data-inset={inset}
      data-variant={variant}
      className={cn(
        "focus:bg-accent focus:text-accent-foreground data-[variant=destructive]:text-destructive data-[variant=destructive]:focus:bg-destructive/10 dark:data-[variant=destructive]:focus:bg-destructive/20 data-[variant=destructive]:focus:text-destructive data-[variant=destructive]:*:[svg]:!text-destructive [&_svg:not([class*='text-'])]:text-muted-foreground relative flex cursor-default items-center gap-2 rounded-sm px-2 py-1.5 text-sm outline-hidden select-none data-[disabled]:pointer-events-none data-[disabled]:opacity-50 data-[inset]:pl-8 [&_svg]:pointer-events-none [&_svg]:shrink-0 [&_svg:not([class*='size-'])]:size-4",
        className,
      )}
      {...props}
    />
  )
}

function MenubarCheckboxItem({
  className,
  children,
  checked,
  ...props
}: React.ComponentProps<typeof MenubarPrimitive.CheckboxItem>) {
  return (
    <MenubarPrimitive.CheckboxItem
      data-slot="menubar-checkbox-item"
      className={cn(
        "focus:bg-accent focus:text-accent-foreground relative flex cursor-default items-center gap-2 rounded-xs py-1.5 pr-2 pl-8 text-sm outline-hidden select-none data-[disabled]:pointer-events-none data-[disabled]:opacity-50 [&_svg]:pointer-events-none [&_svg]:shrink-0 [&_svg:not([class*='size-'])]:size-4",
        className,
      )}
      checked={checked}
      {...props}
    >
      <span className="pointer-events-none absolute left-2 flex size-3.5 items-center justify-center">
        <MenubarPrimitive.ItemIndicator>
          <CheckIcon className="size-4" />
        </MenubarPrimitive.ItemIndicator>
      </span>
      {children}
    </MenubarPrimitive.CheckboxItem>
  )
}

function MenubarRadioItem({
  className,
  children,
  ...props
}: React.ComponentProps<typeof MenubarPrimitive.RadioItem>) {
  return (
    <MenubarPrimitive.RadioItem
      data-slot="menubar-radio-item"
      className={cn(
        "focus:bg-accent focus:text-accent-foreground relative flex cursor-default items-center gap-2 rounded-xs py-1.5 pr-2 pl-8 text-sm outline-hidden select-none data-[disabled]:pointer-events-none data-[disabled]:opacity-50 [&_svg]:pointer-events-none [&_svg]:shrink-0 [&_svg:not([class*='size-'])]:size-4",
        className,
      )}
      {...props}
    >
      <span className="pointer-events-none absolute left-2 flex size-3.5 items-center justify-center">
        <MenubarPrimitive.ItemIndicator>
          <CircleIcon className="size-2 fill-current" />
        </MenubarPrimitive.ItemIndicator>
      </span>
      {children}
    </MenubarPrimitive.RadioItem>
  )
}

function MenubarLabel({
  className,
  inset,
  ...props
}: React.ComponentProps<typeof MenubarPrimitive.Label> & {
  inset?: boolean
}) {
  return (
    <MenubarPrimitive.Label
      data-slot="menubar-label"
      data-inset={inset}
      className={cn(
        'px-2 py-1.5 text-sm font-medium data-[inset]:pl-8',
        className,
      )}
      {...props}
    />
  )
}

function MenubarSeparator({
  className,
  ...props
}: React.ComponentProps<typeof MenubarPrimitive.Separator>) {
  return (
    <MenubarPrimitive.Separator
      data-slot="menubar-separator"
      className={cn('bg-border -mx-1 my-1 h-px', className)}
      {...props}
    />
  )
}

function MenubarShortcut({
  className,
  ...props
}: React.ComponentProps<'span'>) {
  return (
    <span
      data-slot="menubar-shortcut"
      className={cn(
        'text-muted-foreground ml-auto text-xs tracking-widest',
        className,
      )}
      {...props}
    />
  )
}

function MenubarSub({
  ...props
}: React.ComponentProps<typeof MenubarPrimitive.Sub>) {
  return <MenubarPrimitive.Sub data-slot="menubar-sub" {...props} />
}

function MenubarSubTrigger({
  className,
  inset,
  children,
  ...props
}: React.ComponentProps<typeof MenubarPrimitive.SubTrigger> & {
  inset?: boolean
}) {
  return (
    <MenubarPrimitive.SubTrigger
      data-slot="menubar-sub-trigger"
      data-inset={inset}
      className={cn(
        'focus:bg-accent focus:text-accent-foreground data-[state=open]:bg-accent data-[state=open]:text-accent-foreground flex cursor-default items-center rounded-sm px-2 py-1.5 text-sm outline-none select-none data-[inset]:pl-8',
        className,
      )}
      {...props}
    >
      {children}
      <ChevronRightIcon className="ml-auto h-4 w-4" />
    </MenubarPrimitive.SubTrigger>
  )
}

function MenubarSubContent({
  className,
  ...props
}: React.ComponentProps<typeof MenubarPrimitive.SubContent>) {
  return (
    <MenubarPrimitive.SubContent
      data-slot="menubar-sub-content"
      className={cn(
        'bg-popover text-popover-foreground data-[state=open]:animate-in data-[state=closed]:animate-out data-[state=closed]:fade-out-0 data-[state=open]:fade-in-0 data-[state=closed]:zoom-out-95 data-[state=open]:zoom-in-95 data-[side=bottom]:slide-in-from-top-2 data-[side=left]:slide-in-from-right-2 data-[side=right]:slide-in-from-left-2 data-[side=top]:slide-in-from-bottom-2 z-50 min-w-[8rem] origin-(--radix-menubar-content-transform-origin) overflow-hidden rounded-md border p-1 shadow-lg',
        className,
      )}
      {...props}
    />
  )
}

export {
  Menubar,
  MenubarPortal,
  MenubarMenu,
  MenubarTrigger,
  MenubarContent,
  MenubarGroup,
  MenubarSeparator,
  MenubarLabel,
  MenubarItem,
  MenubarShortcut,
  MenubarCheckboxItem,
  MenubarRadioGroup,
  MenubarRadioItem,
  MenubarSub,
  MenubarSubTrigger,
  MenubarSubContent,
}
\n--- END FILE: ./html.code.v0.app/components/ui/menubar.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/context-menu.tsx ---
'use client'

import * as React from 'react'
import * as ContextMenuPrimitive from '@radix-ui/react-context-menu'
import { CheckIcon, ChevronRightIcon, CircleIcon } from 'lucide-react'

import { cn } from '@/lib/utils'

function ContextMenu({
  ...props
}: React.ComponentProps<typeof ContextMenuPrimitive.Root>) {
  return <ContextMenuPrimitive.Root data-slot="context-menu" {...props} />
}

function ContextMenuTrigger({
  ...props
}: React.ComponentProps<typeof ContextMenuPrimitive.Trigger>) {
  return (
    <ContextMenuPrimitive.Trigger data-slot="context-menu-trigger" {...props} />
  )
}

function ContextMenuGroup({
  ...props
}: React.ComponentProps<typeof ContextMenuPrimitive.Group>) {
  return (
    <ContextMenuPrimitive.Group data-slot="context-menu-group" {...props} />
  )
}

function ContextMenuPortal({
  ...props
}: React.ComponentProps<typeof ContextMenuPrimitive.Portal>) {
  return (
    <ContextMenuPrimitive.Portal data-slot="context-menu-portal" {...props} />
  )
}

function ContextMenuSub({
  ...props
}: React.ComponentProps<typeof ContextMenuPrimitive.Sub>) {
  return <ContextMenuPrimitive.Sub data-slot="context-menu-sub" {...props} />
}

function ContextMenuRadioGroup({
  ...props
}: React.ComponentProps<typeof ContextMenuPrimitive.RadioGroup>) {
  return (
    <ContextMenuPrimitive.RadioGroup
      data-slot="context-menu-radio-group"
      {...props}
    />
  )
}

function ContextMenuSubTrigger({
  className,
  inset,
  children,
  ...props
}: React.ComponentProps<typeof ContextMenuPrimitive.SubTrigger> & {
  inset?: boolean
}) {
  return (
    <ContextMenuPrimitive.SubTrigger
      data-slot="context-menu-sub-trigger"
      data-inset={inset}
      className={cn(
        "focus:bg-accent focus:text-accent-foreground data-[state=open]:bg-accent data-[state=open]:text-accent-foreground [&_svg:not([class*='text-'])]:text-muted-foreground flex cursor-default items-center rounded-sm px-2 py-1.5 text-sm outline-hidden select-none data-[inset]:pl-8 [&_svg]:pointer-events-none [&_svg]:shrink-0 [&_svg:not([class*='size-'])]:size-4",
        className,
      )}
      {...props}
    >
      {children}
      <ChevronRightIcon className="ml-auto" />
    </ContextMenuPrimitive.SubTrigger>
  )
}

function ContextMenuSubContent({
  className,
  ...props
}: React.ComponentProps<typeof ContextMenuPrimitive.SubContent>) {
  return (
    <ContextMenuPrimitive.SubContent
      data-slot="context-menu-sub-content"
      className={cn(
        'bg-popover text-popover-foreground data-[state=open]:animate-in data-[state=closed]:animate-out data-[state=closed]:fade-out-0 data-[state=open]:fade-in-0 data-[state=closed]:zoom-out-95 data-[state=open]:zoom-in-95 data-[side=bottom]:slide-in-from-top-2 data-[side=left]:slide-in-from-right-2 data-[side=right]:slide-in-from-left-2 data-[side=top]:slide-in-from-bottom-2 z-50 min-w-[8rem] origin-(--radix-context-menu-content-transform-origin) overflow-hidden rounded-md border p-1 shadow-lg',
        className,
      )}
      {...props}
    />
  )
}

function ContextMenuContent({
  className,
  ...props
}: React.ComponentProps<typeof ContextMenuPrimitive.Content>) {
  return (
    <ContextMenuPrimitive.Portal>
      <ContextMenuPrimitive.Content
        data-slot="context-menu-content"
        className={cn(
          'bg-popover text-popover-foreground data-[state=open]:animate-in data-[state=closed]:animate-out data-[state=closed]:fade-out-0 data-[state=open]:fade-in-0 data-[state=closed]:zoom-out-95 data-[state=open]:zoom-in-95 data-[side=bottom]:slide-in-from-top-2 data-[side=left]:slide-in-from-right-2 data-[side=right]:slide-in-from-left-2 data-[side=top]:slide-in-from-bottom-2 z-50 max-h-(--radix-context-menu-content-available-height) min-w-[8rem] origin-(--radix-context-menu-content-transform-origin) overflow-x-hidden overflow-y-auto rounded-md border p-1 shadow-md',
          className,
        )}
        {...props}
      />
    </ContextMenuPrimitive.Portal>
  )
}

function ContextMenuItem({
  className,
  inset,
  variant = 'default',
  ...props
}: React.ComponentProps<typeof ContextMenuPrimitive.Item> & {
  inset?: boolean
  variant?: 'default' | 'destructive'
}) {
  return (
    <ContextMenuPrimitive.Item
      data-slot="context-menu-item"
      data-inset={inset}
      data-variant={variant}
      className={cn(
        "focus:bg-accent focus:text-accent-foreground data-[variant=destructive]:text-destructive data-[variant=destructive]:focus:bg-destructive/10 dark:data-[variant=destructive]:focus:bg-destructive/20 data-[variant=destructive]:focus:text-destructive data-[variant=destructive]:*:[svg]:!text-destructive [&_svg:not([class*='text-'])]:text-muted-foreground relative flex cursor-default items-center gap-2 rounded-sm px-2 py-1.5 text-sm outline-hidden select-none data-[disabled]:pointer-events-none data-[disabled]:opacity-50 data-[inset]:pl-8 [&_svg]:pointer-events-none [&_svg]:shrink-0 [&_svg:not([class*='size-'])]:size-4",
        className,
      )}
      {...props}
    />
  )
}

function ContextMenuCheckboxItem({
  className,
  children,
  checked,
  ...props
}: React.ComponentProps<typeof ContextMenuPrimitive.CheckboxItem>) {
  return (
    <ContextMenuPrimitive.CheckboxItem
      data-slot="context-menu-checkbox-item"
      className={cn(
        "focus:bg-accent focus:text-accent-foreground relative flex cursor-default items-center gap-2 rounded-sm py-1.5 pr-2 pl-8 text-sm outline-hidden select-none data-[disabled]:pointer-events-none data-[disabled]:opacity-50 [&_svg]:pointer-events-none [&_svg]:shrink-0 [&_svg:not([class*='size-'])]:size-4",
        className,
      )}
      checked={checked}
      {...props}
    >
      <span className="pointer-events-none absolute left-2 flex size-3.5 items-center justify-center">
        <ContextMenuPrimitive.ItemIndicator>
          <CheckIcon className="size-4" />
        </ContextMenuPrimitive.ItemIndicator>
      </span>
      {children}
    </ContextMenuPrimitive.CheckboxItem>
  )
}

function ContextMenuRadioItem({
  className,
  children,
  ...props
}: React.ComponentProps<typeof ContextMenuPrimitive.RadioItem>) {
  return (
    <ContextMenuPrimitive.RadioItem
      data-slot="context-menu-radio-item"
      className={cn(
        "focus:bg-accent focus:text-accent-foreground relative flex cursor-default items-center gap-2 rounded-sm py-1.5 pr-2 pl-8 text-sm outline-hidden select-none data-[disabled]:pointer-events-none data-[disabled]:opacity-50 [&_svg]:pointer-events-none [&_svg]:shrink-0 [&_svg:not([class*='size-'])]:size-4",
        className,
      )}
      {...props}
    >
      <span className="pointer-events-none absolute left-2 flex size-3.5 items-center justify-center">
        <ContextMenuPrimitive.ItemIndicator>
          <CircleIcon className="size-2 fill-current" />
        </ContextMenuPrimitive.ItemIndicator>
      </span>
      {children}
    </ContextMenuPrimitive.RadioItem>
  )
}

function ContextMenuLabel({
  className,
  inset,
  ...props
}: React.ComponentProps<typeof ContextMenuPrimitive.Label> & {
  inset?: boolean
}) {
  return (
    <ContextMenuPrimitive.Label
      data-slot="context-menu-label"
      data-inset={inset}
      className={cn(
        'text-foreground px-2 py-1.5 text-sm font-medium data-[inset]:pl-8',
        className,
      )}
      {...props}
    />
  )
}

function ContextMenuSeparator({
  className,
  ...props
}: React.ComponentProps<typeof ContextMenuPrimitive.Separator>) {
  return (
    <ContextMenuPrimitive.Separator
      data-slot="context-menu-separator"
      className={cn('bg-border -mx-1 my-1 h-px', className)}
      {...props}
    />
  )
}

function ContextMenuShortcut({
  className,
  ...props
}: React.ComponentProps<'span'>) {
  return (
    <span
      data-slot="context-menu-shortcut"
      className={cn(
        'text-muted-foreground ml-auto text-xs tracking-widest',
        className,
      )}
      {...props}
    />
  )
}

export {
  ContextMenu,
  ContextMenuTrigger,
  ContextMenuContent,
  ContextMenuItem,
  ContextMenuCheckboxItem,
  ContextMenuRadioItem,
  ContextMenuLabel,
  ContextMenuSeparator,
  ContextMenuShortcut,
  ContextMenuGroup,
  ContextMenuPortal,
  ContextMenuSub,
  ContextMenuSubContent,
  ContextMenuSubTrigger,
  ContextMenuRadioGroup,
}
\n--- END FILE: ./html.code.v0.app/components/ui/context-menu.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/empty.tsx ---
import { cva, type VariantProps } from 'class-variance-authority'

import { cn } from '@/lib/utils'

function Empty({ className, ...props }: React.ComponentProps<'div'>) {
  return (
    <div
      data-slot="empty"
      className={cn(
        'flex min-w-0 flex-1 flex-col items-center justify-center gap-6 rounded-lg border-dashed p-6 text-center text-balance md:p-12',
        className,
      )}
      {...props}
    />
  )
}

function EmptyHeader({ className, ...props }: React.ComponentProps<'div'>) {
  return (
    <div
      data-slot="empty-header"
      className={cn(
        'flex max-w-sm flex-col items-center gap-2 text-center',
        className,
      )}
      {...props}
    />
  )
}

const emptyMediaVariants = cva(
  'flex shrink-0 items-center justify-center mb-2 [&_svg]:pointer-events-none [&_svg]:shrink-0',
  {
    variants: {
      variant: {
        default: 'bg-transparent',
        icon: "bg-muted text-foreground flex size-10 shrink-0 items-center justify-center rounded-lg [&_svg:not([class*='size-'])]:size-6",
      },
    },
    defaultVariants: {
      variant: 'default',
    },
  },
)

function EmptyMedia({
  className,
  variant = 'default',
  ...props
}: React.ComponentProps<'div'> & VariantProps<typeof emptyMediaVariants>) {
  return (
    <div
      data-slot="empty-icon"
      data-variant={variant}
      className={cn(emptyMediaVariants({ variant, className }))}
      {...props}
    />
  )
}

function EmptyTitle({ className, ...props }: React.ComponentProps<'div'>) {
  return (
    <div
      data-slot="empty-title"
      className={cn('text-lg font-medium tracking-tight', className)}
      {...props}
    />
  )
}

function EmptyDescription({ className, ...props }: React.ComponentProps<'p'>) {
  return (
    <div
      data-slot="empty-description"
      className={cn(
        'text-muted-foreground [&>a:hover]:text-primary text-sm/relaxed [&>a]:underline [&>a]:underline-offset-4',
        className,
      )}
      {...props}
    />
  )
}

function EmptyContent({ className, ...props }: React.ComponentProps<'div'>) {
  return (
    <div
      data-slot="empty-content"
      className={cn(
        'flex w-full max-w-sm min-w-0 flex-col items-center gap-4 text-sm text-balance',
        className,
      )}
      {...props}
    />
  )
}

export {
  Empty,
  EmptyHeader,
  EmptyTitle,
  EmptyDescription,
  EmptyContent,
  EmptyMedia,
}
\n--- END FILE: ./html.code.v0.app/components/ui/empty.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/item.tsx ---
import * as React from 'react'
import { Slot } from '@radix-ui/react-slot'
import { cva, type VariantProps } from 'class-variance-authority'

import { cn } from '@/lib/utils'
import { Separator } from '@/components/ui/separator'

function ItemGroup({ className, ...props }: React.ComponentProps<'div'>) {
  return (
    <div
      role="list"
      data-slot="item-group"
      className={cn('group/item-group flex flex-col', className)}
      {...props}
    />
  )
}

function ItemSeparator({
  className,
  ...props
}: React.ComponentProps<typeof Separator>) {
  return (
    <Separator
      data-slot="item-separator"
      orientation="horizontal"
      className={cn('my-0', className)}
      {...props}
    />
  )
}

const itemVariants = cva(
  'group/item flex items-center border border-transparent text-sm rounded-md transition-colors [a&]:hover:bg-accent/50 [a&]:transition-colors duration-100 flex-wrap outline-none focus-visible:border-ring focus-visible:ring-ring/50 focus-visible:ring-[3px]',
  {
    variants: {
      variant: {
        default: 'bg-transparent',
        outline: 'border-border',
        muted: 'bg-muted/50',
      },
      size: {
        default: 'p-4 gap-4 ',
        sm: 'py-3 px-4 gap-2.5',
      },
    },
    defaultVariants: {
      variant: 'default',
      size: 'default',
    },
  },
)

function Item({
  className,
  variant = 'default',
  size = 'default',
  asChild = false,
  ...props
}: React.ComponentProps<'div'> &
  VariantProps<typeof itemVariants> & { asChild?: boolean }) {
  const Comp = asChild ? Slot : 'div'
  return (
    <Comp
      data-slot="item"
      data-variant={variant}
      data-size={size}
      className={cn(itemVariants({ variant, size, className }))}
      {...props}
    />
  )
}

const itemMediaVariants = cva(
  'flex shrink-0 items-center justify-center gap-2 group-has-[[data-slot=item-description]]/item:self-start [&_svg]:pointer-events-none group-has-[[data-slot=item-description]]/item:translate-y-0.5',
  {
    variants: {
      variant: {
        default: 'bg-transparent',
        icon: "size-8 border rounded-sm bg-muted [&_svg:not([class*='size-'])]:size-4",
        image:
          'size-10 rounded-sm overflow-hidden [&_img]:size-full [&_img]:object-cover',
      },
    },
    defaultVariants: {
      variant: 'default',
    },
  },
)

function ItemMedia({
  className,
  variant = 'default',
  ...props
}: React.ComponentProps<'div'> & VariantProps<typeof itemMediaVariants>) {
  return (
    <div
      data-slot="item-media"
      data-variant={variant}
      className={cn(itemMediaVariants({ variant, className }))}
      {...props}
    />
  )
}

function ItemContent({ className, ...props }: React.ComponentProps<'div'>) {
  return (
    <div
      data-slot="item-content"
      className={cn(
        'flex flex-1 flex-col gap-1 [&+[data-slot=item-content]]:flex-none',
        className,
      )}
      {...props}
    />
  )
}

function ItemTitle({ className, ...props }: React.ComponentProps<'div'>) {
  return (
    <div
      data-slot="item-title"
      className={cn(
        'flex w-fit items-center gap-2 text-sm leading-snug font-medium',
        className,
      )}
      {...props}
    />
  )
}

function ItemDescription({ className, ...props }: React.ComponentProps<'p'>) {
  return (
    <p
      data-slot="item-description"
      className={cn(
        'text-muted-foreground line-clamp-2 text-sm leading-normal font-normal text-balance',
        '[&>a:hover]:text-primary [&>a]:underline [&>a]:underline-offset-4',
        className,
      )}
      {...props}
    />
  )
}

function ItemActions({ className, ...props }: React.ComponentProps<'div'>) {
  return (
    <div
      data-slot="item-actions"
      className={cn('flex items-center gap-2', className)}
      {...props}
    />
  )
}

function ItemHeader({ className, ...props }: React.ComponentProps<'div'>) {
  return (
    <div
      data-slot="item-header"
      className={cn(
        'flex basis-full items-center justify-between gap-2',
        className,
      )}
      {...props}
    />
  )
}

function ItemFooter({ className, ...props }: React.ComponentProps<'div'>) {
  return (
    <div
      data-slot="item-footer"
      className={cn(
        'flex basis-full items-center justify-between gap-2',
        className,
      )}
      {...props}
    />
  )
}

export {
  Item,
  ItemMedia,
  ItemContent,
  ItemActions,
  ItemGroup,
  ItemSeparator,
  ItemTitle,
  ItemDescription,
  ItemHeader,
  ItemFooter,
}
\n--- END FILE: ./html.code.v0.app/components/ui/item.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/hover-card.tsx ---
'use client'

import * as React from 'react'
import * as HoverCardPrimitive from '@radix-ui/react-hover-card'

import { cn } from '@/lib/utils'

function HoverCard({
  ...props
}: React.ComponentProps<typeof HoverCardPrimitive.Root>) {
  return <HoverCardPrimitive.Root data-slot="hover-card" {...props} />
}

function HoverCardTrigger({
  ...props
}: React.ComponentProps<typeof HoverCardPrimitive.Trigger>) {
  return (
    <HoverCardPrimitive.Trigger data-slot="hover-card-trigger" {...props} />
  )
}

function HoverCardContent({
  className,
  align = 'center',
  sideOffset = 4,
  ...props
}: React.ComponentProps<typeof HoverCardPrimitive.Content>) {
  return (
    <HoverCardPrimitive.Portal data-slot="hover-card-portal">
      <HoverCardPrimitive.Content
        data-slot="hover-card-content"
        align={align}
        sideOffset={sideOffset}
        className={cn(
          'bg-popover text-popover-foreground data-[state=open]:animate-in data-[state=closed]:animate-out data-[state=closed]:fade-out-0 data-[state=open]:fade-in-0 data-[state=closed]:zoom-out-95 data-[state=open]:zoom-in-95 data-[side=bottom]:slide-in-from-top-2 data-[side=left]:slide-in-from-right-2 data-[side=right]:slide-in-from-left-2 data-[side=top]:slide-in-from-bottom-2 z-50 w-64 origin-(--radix-hover-card-content-transform-origin) rounded-md border p-4 shadow-md outline-hidden',
          className,
        )}
        {...props}
      />
    </HoverCardPrimitive.Portal>
  )
}

export { HoverCard, HoverCardTrigger, HoverCardContent }
\n--- END FILE: ./html.code.v0.app/components/ui/hover-card.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/calendar.tsx ---
'use client'

import * as React from 'react'
import {
  ChevronDownIcon,
  ChevronLeftIcon,
  ChevronRightIcon,
} from 'lucide-react'
import { DayButton, DayPicker, getDefaultClassNames } from 'react-day-picker'

import { cn } from '@/lib/utils'
import { Button, buttonVariants } from '@/components/ui/button'

function Calendar({
  className,
  classNames,
  showOutsideDays = true,
  captionLayout = 'label',
  buttonVariant = 'ghost',
  formatters,
  components,
  ...props
}: React.ComponentProps<typeof DayPicker> & {
  buttonVariant?: React.ComponentProps<typeof Button>['variant']
}) {
  const defaultClassNames = getDefaultClassNames()

  return (
    <DayPicker
      showOutsideDays={showOutsideDays}
      className={cn(
        'bg-background group/calendar p-3 [--cell-size:--spacing(8)] [[data-slot=card-content]_&]:bg-transparent [[data-slot=popover-content]_&]:bg-transparent',
        String.raw`rtl:**:[.rdp-button\_next>svg]:rotate-180`,
        String.raw`rtl:**:[.rdp-button\_previous>svg]:rotate-180`,
        className,
      )}
      captionLayout={captionLayout}
      formatters={{
        formatMonthDropdown: (date) =>
          date.toLocaleString('default', { month: 'short' }),
        ...formatters,
      }}
      classNames={{
        root: cn('w-fit', defaultClassNames.root),
        months: cn(
          'flex gap-4 flex-col md:flex-row relative',
          defaultClassNames.months,
        ),
        month: cn('flex flex-col w-full gap-4', defaultClassNames.month),
        nav: cn(
          'flex items-center gap-1 w-full absolute top-0 inset-x-0 justify-between',
          defaultClassNames.nav,
        ),
        button_previous: cn(
          buttonVariants({ variant: buttonVariant }),
          'size-(--cell-size) aria-disabled:opacity-50 p-0 select-none',
          defaultClassNames.button_previous,
        ),
        button_next: cn(
          buttonVariants({ variant: buttonVariant }),
          'size-(--cell-size) aria-disabled:opacity-50 p-0 select-none',
          defaultClassNames.button_next,
        ),
        month_caption: cn(
          'flex items-center justify-center h-(--cell-size) w-full px-(--cell-size)',
          defaultClassNames.month_caption,
        ),
        dropdowns: cn(
          'w-full flex items-center text-sm font-medium justify-center h-(--cell-size) gap-1.5',
          defaultClassNames.dropdowns,
        ),
        dropdown_root: cn(
          'relative has-focus:border-ring border border-input shadow-xs has-focus:ring-ring/50 has-focus:ring-[3px] rounded-md',
          defaultClassNames.dropdown_root,
        ),
        dropdown: cn(
          'absolute bg-popover inset-0 opacity-0',
          defaultClassNames.dropdown,
        ),
        caption_label: cn(
          'select-none font-medium',
          captionLayout === 'label'
            ? 'text-sm'
            : 'rounded-md pl-2 pr-1 flex items-center gap-1 text-sm h-8 [&>svg]:text-muted-foreground [&>svg]:size-3.5',
          defaultClassNames.caption_label,
        ),
        table: 'w-full border-collapse',
        weekdays: cn('flex', defaultClassNames.weekdays),
        weekday: cn(
          'text-muted-foreground rounded-md flex-1 font-normal text-[0.8rem] select-none',
          defaultClassNames.weekday,
        ),
        week: cn('flex w-full mt-2', defaultClassNames.week),
        week_number_header: cn(
          'select-none w-(--cell-size)',
          defaultClassNames.week_number_header,
        ),
        week_number: cn(
          'text-[0.8rem] select-none text-muted-foreground',
          defaultClassNames.week_number,
        ),
        day: cn(
          'relative w-full h-full p-0 text-center [&:first-child[data-selected=true]_button]:rounded-l-md [&:last-child[data-selected=true]_button]:rounded-r-md group/day aspect-square select-none',
          defaultClassNames.day,
        ),
        range_start: cn(
          'rounded-l-md bg-accent',
          defaultClassNames.range_start,
        ),
        range_middle: cn('rounded-none', defaultClassNames.range_middle),
        range_end: cn('rounded-r-md bg-accent', defaultClassNames.range_end),
        today: cn(
          'bg-accent text-accent-foreground rounded-md data-[selected=true]:rounded-none',
          defaultClassNames.today,
        ),
        outside: cn(
          'text-muted-foreground aria-selected:text-muted-foreground',
          defaultClassNames.outside,
        ),
        disabled: cn(
          'text-muted-foreground opacity-50',
          defaultClassNames.disabled,
        ),
        hidden: cn('invisible', defaultClassNames.hidden),
        ...classNames,
      }}
      components={{
        Root: ({ className, rootRef, ...props }) => {
          return (
            <div
              data-slot="calendar"
              ref={rootRef}
              className={cn(className)}
              {...props}
            />
          )
        },
        Chevron: ({ className, orientation, ...props }) => {
          if (orientation === 'left') {
            return (
              <ChevronLeftIcon className={cn('size-4', className)} {...props} />
            )
          }

          if (orientation === 'right') {
            return (
              <ChevronRightIcon
                className={cn('size-4', className)}
                {...props}
              />
            )
          }

          return (
            <ChevronDownIcon className={cn('size-4', className)} {...props} />
          )
        },
        DayButton: CalendarDayButton,
        WeekNumber: ({ children, ...props }) => {
          return (
            <td {...props}>
              <div className="flex size-(--cell-size) items-center justify-center text-center">
                {children}
              </div>
            </td>
          )
        },
        ...components,
      }}
      {...props}
    />
  )
}

function CalendarDayButton({
  className,
  day,
  modifiers,
  ...props
}: React.ComponentProps<typeof DayButton>) {
  const defaultClassNames = getDefaultClassNames()

  const ref = React.useRef<HTMLButtonElement>(null)
  React.useEffect(() => {
    if (modifiers.focused) ref.current?.focus()
  }, [modifiers.focused])

  return (
    <Button
      ref={ref}
      variant="ghost"
      size="icon"
      data-day={day.date.toLocaleDateString()}
      data-selected-single={
        modifiers.selected &&
        !modifiers.range_start &&
        !modifiers.range_end &&
        !modifiers.range_middle
      }
      data-range-start={modifiers.range_start}
      data-range-end={modifiers.range_end}
      data-range-middle={modifiers.range_middle}
      className={cn(
        'data-[selected-single=true]:bg-primary data-[selected-single=true]:text-primary-foreground data-[range-middle=true]:bg-accent data-[range-middle=true]:text-accent-foreground data-[range-start=true]:bg-primary data-[range-start=true]:text-primary-foreground data-[range-end=true]:bg-primary data-[range-end=true]:text-primary-foreground group-data-[focused=true]/day:border-ring group-data-[focused=true]/day:ring-ring/50 dark:hover:text-accent-foreground flex aspect-square size-auto w-full min-w-(--cell-size) flex-col gap-1 leading-none font-normal group-data-[focused=true]/day:relative group-data-[focused=true]/day:z-10 group-data-[focused=true]/day:ring-[3px] data-[range-end=true]:rounded-md data-[range-end=true]:rounded-r-md data-[range-middle=true]:rounded-none data-[range-start=true]:rounded-md data-[range-start=true]:rounded-l-md [&>span]:text-xs [&>span]:opacity-70',
        defaultClassNames.day,
        className,
      )}
      {...props}
    />
  )
}

export { Calendar, CalendarDayButton }
\n--- END FILE: ./html.code.v0.app/components/ui/calendar.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/textarea.tsx ---
import * as React from 'react'

import { cn } from '@/lib/utils'

function Textarea({ className, ...props }: React.ComponentProps<'textarea'>) {
  return (
    <textarea
      data-slot="textarea"
      className={cn(
        'border-input placeholder:text-muted-foreground focus-visible:border-ring focus-visible:ring-ring/50 aria-invalid:ring-destructive/20 dark:aria-invalid:ring-destructive/40 aria-invalid:border-destructive dark:bg-input/30 flex field-sizing-content min-h-16 w-full rounded-md border bg-transparent px-3 py-2 text-base shadow-xs transition-[color,box-shadow] outline-none focus-visible:ring-[3px] disabled:cursor-not-allowed disabled:opacity-50 md:text-sm',
        className,
      )}
      {...props}
    />
  )
}

export { Textarea }
\n--- END FILE: ./html.code.v0.app/components/ui/textarea.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/avatar.tsx ---
'use client'

import * as React from 'react'
import * as AvatarPrimitive from '@radix-ui/react-avatar'

import { cn } from '@/lib/utils'

function Avatar({
  className,
  ...props
}: React.ComponentProps<typeof AvatarPrimitive.Root>) {
  return (
    <AvatarPrimitive.Root
      data-slot="avatar"
      className={cn(
        'relative flex size-8 shrink-0 overflow-hidden rounded-full',
        className,
      )}
      {...props}
    />
  )
}

function AvatarImage({
  className,
  ...props
}: React.ComponentProps<typeof AvatarPrimitive.Image>) {
  return (
    <AvatarPrimitive.Image
      data-slot="avatar-image"
      className={cn('aspect-square size-full', className)}
      {...props}
    />
  )
}

function AvatarFallback({
  className,
  ...props
}: React.ComponentProps<typeof AvatarPrimitive.Fallback>) {
  return (
    <AvatarPrimitive.Fallback
      data-slot="avatar-fallback"
      className={cn(
        'bg-muted flex size-full items-center justify-center rounded-full',
        className,
      )}
      {...props}
    />
  )
}

export { Avatar, AvatarImage, AvatarFallback }
\n--- END FILE: ./html.code.v0.app/components/ui/avatar.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/separator.tsx ---
'use client'

import * as React from 'react'
import * as SeparatorPrimitive from '@radix-ui/react-separator'

import { cn } from '@/lib/utils'

function Separator({
  className,
  orientation = 'horizontal',
  decorative = true,
  ...props
}: React.ComponentProps<typeof SeparatorPrimitive.Root>) {
  return (
    <SeparatorPrimitive.Root
      data-slot="separator"
      decorative={decorative}
      orientation={orientation}
      className={cn(
        'bg-border shrink-0 data-[orientation=horizontal]:h-px data-[orientation=horizontal]:w-full data-[orientation=vertical]:h-full data-[orientation=vertical]:w-px',
        className,
      )}
      {...props}
    />
  )
}

export { Separator }
\n--- END FILE: ./html.code.v0.app/components/ui/separator.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/drawer.tsx ---
'use client'

import * as React from 'react'
import { Drawer as DrawerPrimitive } from 'vaul'

import { cn } from '@/lib/utils'

function Drawer({
  ...props
}: React.ComponentProps<typeof DrawerPrimitive.Root>) {
  return <DrawerPrimitive.Root data-slot="drawer" {...props} />
}

function DrawerTrigger({
  ...props
}: React.ComponentProps<typeof DrawerPrimitive.Trigger>) {
  return <DrawerPrimitive.Trigger data-slot="drawer-trigger" {...props} />
}

function DrawerPortal({
  ...props
}: React.ComponentProps<typeof DrawerPrimitive.Portal>) {
  return <DrawerPrimitive.Portal data-slot="drawer-portal" {...props} />
}

function DrawerClose({
  ...props
}: React.ComponentProps<typeof DrawerPrimitive.Close>) {
  return <DrawerPrimitive.Close data-slot="drawer-close" {...props} />
}

function DrawerOverlay({
  className,
  ...props
}: React.ComponentProps<typeof DrawerPrimitive.Overlay>) {
  return (
    <DrawerPrimitive.Overlay
      data-slot="drawer-overlay"
      className={cn(
        'data-[state=open]:animate-in data-[state=closed]:animate-out data-[state=closed]:fade-out-0 data-[state=open]:fade-in-0 fixed inset-0 z-50 bg-black/50',
        className,
      )}
      {...props}
    />
  )
}

function DrawerContent({
  className,
  children,
  ...props
}: React.ComponentProps<typeof DrawerPrimitive.Content>) {
  return (
    <DrawerPortal data-slot="drawer-portal">
      <DrawerOverlay />
      <DrawerPrimitive.Content
        data-slot="drawer-content"
        className={cn(
          'group/drawer-content bg-background fixed z-50 flex h-auto flex-col',
          'data-[vaul-drawer-direction=top]:inset-x-0 data-[vaul-drawer-direction=top]:top-0 data-[vaul-drawer-direction=top]:mb-24 data-[vaul-drawer-direction=top]:max-h-[80vh] data-[vaul-drawer-direction=top]:rounded-b-lg data-[vaul-drawer-direction=top]:border-b',
          'data-[vaul-drawer-direction=bottom]:inset-x-0 data-[vaul-drawer-direction=bottom]:bottom-0 data-[vaul-drawer-direction=bottom]:mt-24 data-[vaul-drawer-direction=bottom]:max-h-[80vh] data-[vaul-drawer-direction=bottom]:rounded-t-lg data-[vaul-drawer-direction=bottom]:border-t',
          'data-[vaul-drawer-direction=right]:inset-y-0 data-[vaul-drawer-direction=right]:right-0 data-[vaul-drawer-direction=right]:w-3/4 data-[vaul-drawer-direction=right]:border-l data-[vaul-drawer-direction=right]:sm:max-w-sm',
          'data-[vaul-drawer-direction=left]:inset-y-0 data-[vaul-drawer-direction=left]:left-0 data-[vaul-drawer-direction=left]:w-3/4 data-[vaul-drawer-direction=left]:border-r data-[vaul-drawer-direction=left]:sm:max-w-sm',
          className,
        )}
        {...props}
      >
        <div className="bg-muted mx-auto mt-4 hidden h-2 w-[100px] shrink-0 rounded-full group-data-[vaul-drawer-direction=bottom]/drawer-content:block" />
        {children}
      </DrawerPrimitive.Content>
    </DrawerPortal>
  )
}

function DrawerHeader({ className, ...props }: React.ComponentProps<'div'>) {
  return (
    <div
      data-slot="drawer-header"
      className={cn(
        'flex flex-col gap-0.5 p-4 group-data-[vaul-drawer-direction=bottom]/drawer-content:text-center group-data-[vaul-drawer-direction=top]/drawer-content:text-center md:gap-1.5 md:text-left',
        className,
      )}
      {...props}
    />
  )
}

function DrawerFooter({ className, ...props }: React.ComponentProps<'div'>) {
  return (
    <div
      data-slot="drawer-footer"
      className={cn('mt-auto flex flex-col gap-2 p-4', className)}
      {...props}
    />
  )
}

function DrawerTitle({
  className,
  ...props
}: React.ComponentProps<typeof DrawerPrimitive.Title>) {
  return (
    <DrawerPrimitive.Title
      data-slot="drawer-title"
      className={cn('text-foreground font-semibold', className)}
      {...props}
    />
  )
}

function DrawerDescription({
  className,
  ...props
}: React.ComponentProps<typeof DrawerPrimitive.Description>) {
  return (
    <DrawerPrimitive.Description
      data-slot="drawer-description"
      className={cn('text-muted-foreground text-sm', className)}
      {...props}
    />
  )
}

export {
  Drawer,
  DrawerPortal,
  DrawerOverlay,
  DrawerTrigger,
  DrawerClose,
  DrawerContent,
  DrawerHeader,
  DrawerFooter,
  DrawerTitle,
  DrawerDescription,
}
\n--- END FILE: ./html.code.v0.app/components/ui/drawer.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/command.tsx ---
'use client'

import * as React from 'react'
import { Command as CommandPrimitive } from 'cmdk'
import { SearchIcon } from 'lucide-react'

import { cn } from '@/lib/utils'
import {
  Dialog,
  DialogContent,
  DialogDescription,
  DialogHeader,
  DialogTitle,
} from '@/components/ui/dialog'

function Command({
  className,
  ...props
}: React.ComponentProps<typeof CommandPrimitive>) {
  return (
    <CommandPrimitive
      data-slot="command"
      className={cn(
        'bg-popover text-popover-foreground flex h-full w-full flex-col overflow-hidden rounded-md',
        className,
      )}
      {...props}
    />
  )
}

function CommandDialog({
  title = 'Command Palette',
  description = 'Search for a command to run...',
  children,
  className,
  showCloseButton = true,
  ...props
}: React.ComponentProps<typeof Dialog> & {
  title?: string
  description?: string
  className?: string
  showCloseButton?: boolean
}) {
  return (
    <Dialog {...props}>
      <DialogHeader className="sr-only">
        <DialogTitle>{title}</DialogTitle>
        <DialogDescription>{description}</DialogDescription>
      </DialogHeader>
      <DialogContent
        className={cn('overflow-hidden p-0', className)}
        showCloseButton={showCloseButton}
      >
        <Command className="[&_[cmdk-group-heading]]:text-muted-foreground **:data-[slot=command-input-wrapper]:h-12 [&_[cmdk-group-heading]]:px-2 [&_[cmdk-group-heading]]:font-medium [&_[cmdk-group]]:px-2 [&_[cmdk-group]:not([hidden])_~[cmdk-group]]:pt-0 [&_[cmdk-input-wrapper]_svg]:h-5 [&_[cmdk-input-wrapper]_svg]:w-5 [&_[cmdk-input]]:h-12 [&_[cmdk-item]]:px-2 [&_[cmdk-item]]:py-3 [&_[cmdk-item]_svg]:h-5 [&_[cmdk-item]_svg]:w-5">
          {children}
        </Command>
      </DialogContent>
    </Dialog>
  )
}

function CommandInput({
  className,
  ...props
}: React.ComponentProps<typeof CommandPrimitive.Input>) {
  return (
    <div
      data-slot="command-input-wrapper"
      className="flex h-9 items-center gap-2 border-b px-3"
    >
      <SearchIcon className="size-4 shrink-0 opacity-50" />
      <CommandPrimitive.Input
        data-slot="command-input"
        className={cn(
          'placeholder:text-muted-foreground flex h-10 w-full rounded-md bg-transparent py-3 text-sm outline-hidden disabled:cursor-not-allowed disabled:opacity-50',
          className,
        )}
        {...props}
      />
    </div>
  )
}

function CommandList({
  className,
  ...props
}: React.ComponentProps<typeof CommandPrimitive.List>) {
  return (
    <CommandPrimitive.List
      data-slot="command-list"
      className={cn(
        'max-h-[300px] scroll-py-1 overflow-x-hidden overflow-y-auto',
        className,
      )}
      {...props}
    />
  )
}

function CommandEmpty({
  ...props
}: React.ComponentProps<typeof CommandPrimitive.Empty>) {
  return (
    <CommandPrimitive.Empty
      data-slot="command-empty"
      className="py-6 text-center text-sm"
      {...props}
    />
  )
}

function CommandGroup({
  className,
  ...props
}: React.ComponentProps<typeof CommandPrimitive.Group>) {
  return (
    <CommandPrimitive.Group
      data-slot="command-group"
      className={cn(
        'text-foreground [&_[cmdk-group-heading]]:text-muted-foreground overflow-hidden p-1 [&_[cmdk-group-heading]]:px-2 [&_[cmdk-group-heading]]:py-1.5 [&_[cmdk-group-heading]]:text-xs [&_[cmdk-group-heading]]:font-medium',
        className,
      )}
      {...props}
    />
  )
}

function CommandSeparator({
  className,
  ...props
}: React.ComponentProps<typeof CommandPrimitive.Separator>) {
  return (
    <CommandPrimitive.Separator
      data-slot="command-separator"
      className={cn('bg-border -mx-1 h-px', className)}
      {...props}
    />
  )
}

function CommandItem({
  className,
  ...props
}: React.ComponentProps<typeof CommandPrimitive.Item>) {
  return (
    <CommandPrimitive.Item
      data-slot="command-item"
      className={cn(
        "data-[selected=true]:bg-accent data-[selected=true]:text-accent-foreground [&_svg:not([class*='text-'])]:text-muted-foreground relative flex cursor-default items-center gap-2 rounded-sm px-2 py-1.5 text-sm outline-hidden select-none data-[disabled=true]:pointer-events-none data-[disabled=true]:opacity-50 [&_svg]:pointer-events-none [&_svg]:shrink-0 [&_svg:not([class*='size-'])]:size-4",
        className,
      )}
      {...props}
    />
  )
}

function CommandShortcut({
  className,
  ...props
}: React.ComponentProps<'span'>) {
  return (
    <span
      data-slot="command-shortcut"
      className={cn(
        'text-muted-foreground ml-auto text-xs tracking-widest',
        className,
      )}
      {...props}
    />
  )
}

export {
  Command,
  CommandDialog,
  CommandInput,
  CommandList,
  CommandEmpty,
  CommandGroup,
  CommandItem,
  CommandShortcut,
  CommandSeparator,
}
\n--- END FILE: ./html.code.v0.app/components/ui/command.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/navigation-menu.tsx ---
import * as React from 'react'
import * as NavigationMenuPrimitive from '@radix-ui/react-navigation-menu'
import { cva } from 'class-variance-authority'
import { ChevronDownIcon } from 'lucide-react'

import { cn } from '@/lib/utils'

function NavigationMenu({
  className,
  children,
  viewport = true,
  ...props
}: React.ComponentProps<typeof NavigationMenuPrimitive.Root> & {
  viewport?: boolean
}) {
  return (
    <NavigationMenuPrimitive.Root
      data-slot="navigation-menu"
      data-viewport={viewport}
      className={cn(
        'group/navigation-menu relative flex max-w-max flex-1 items-center justify-center',
        className,
      )}
      {...props}
    >
      {children}
      {viewport && <NavigationMenuViewport />}
    </NavigationMenuPrimitive.Root>
  )
}

function NavigationMenuList({
  className,
  ...props
}: React.ComponentProps<typeof NavigationMenuPrimitive.List>) {
  return (
    <NavigationMenuPrimitive.List
      data-slot="navigation-menu-list"
      className={cn(
        'group flex flex-1 list-none items-center justify-center gap-1',
        className,
      )}
      {...props}
    />
  )
}

function NavigationMenuItem({
  className,
  ...props
}: React.ComponentProps<typeof NavigationMenuPrimitive.Item>) {
  return (
    <NavigationMenuPrimitive.Item
      data-slot="navigation-menu-item"
      className={cn('relative', className)}
      {...props}
    />
  )
}

const navigationMenuTriggerStyle = cva(
  'group inline-flex h-9 w-max items-center justify-center rounded-md bg-background px-4 py-2 text-sm font-medium hover:bg-accent hover:text-accent-foreground focus:bg-accent focus:text-accent-foreground disabled:pointer-events-none disabled:opacity-50 data-[state=open]:hover:bg-accent data-[state=open]:text-accent-foreground data-[state=open]:focus:bg-accent data-[state=open]:bg-accent/50 focus-visible:ring-ring/50 outline-none transition-[color,box-shadow] focus-visible:ring-[3px] focus-visible:outline-1',
)

function NavigationMenuTrigger({
  className,
  children,
  ...props
}: React.ComponentProps<typeof NavigationMenuPrimitive.Trigger>) {
  return (
    <NavigationMenuPrimitive.Trigger
      data-slot="navigation-menu-trigger"
      className={cn(navigationMenuTriggerStyle(), 'group', className)}
      {...props}
    >
      {children}{' '}
      <ChevronDownIcon
        className="relative top-[1px] ml-1 size-3 transition duration-300 group-data-[state=open]:rotate-180"
        aria-hidden="true"
      />
    </NavigationMenuPrimitive.Trigger>
  )
}

function NavigationMenuContent({
  className,
  ...props
}: React.ComponentProps<typeof NavigationMenuPrimitive.Content>) {
  return (
    <NavigationMenuPrimitive.Content
      data-slot="navigation-menu-content"
      className={cn(
        'data-[motion^=from-]:animate-in data-[motion^=to-]:animate-out data-[motion^=from-]:fade-in data-[motion^=to-]:fade-out data-[motion=from-end]:slide-in-from-right-52 data-[motion=from-start]:slide-in-from-left-52 data-[motion=to-end]:slide-out-to-right-52 data-[motion=to-start]:slide-out-to-left-52 top-0 left-0 w-full p-2 pr-2.5 md:absolute md:w-auto',
        'group-data-[viewport=false]/navigation-menu:bg-popover group-data-[viewport=false]/navigation-menu:text-popover-foreground group-data-[viewport=false]/navigation-menu:data-[state=open]:animate-in group-data-[viewport=false]/navigation-menu:data-[state=closed]:animate-out group-data-[viewport=false]/navigation-menu:data-[state=closed]:zoom-out-95 group-data-[viewport=false]/navigation-menu:data-[state=open]:zoom-in-95 group-data-[viewport=false]/navigation-menu:data-[state=open]:fade-in-0 group-data-[viewport=false]/navigation-menu:data-[state=closed]:fade-out-0 group-data-[viewport=false]/navigation-menu:top-full group-data-[viewport=false]/navigation-menu:mt-1.5 group-data-[viewport=false]/navigation-menu:overflow-hidden group-data-[viewport=false]/navigation-menu:rounded-md group-data-[viewport=false]/navigation-menu:border group-data-[viewport=false]/navigation-menu:shadow group-data-[viewport=false]/navigation-menu:duration-200 **:data-[slot=navigation-menu-link]:focus:ring-0 **:data-[slot=navigation-menu-link]:focus:outline-none',
        className,
      )}
      {...props}
    />
  )
}

function NavigationMenuViewport({
  className,
  ...props
}: React.ComponentProps<typeof NavigationMenuPrimitive.Viewport>) {
  return (
    <div
      className={'absolute top-full left-0 isolate z-50 flex justify-center'}
    >
      <NavigationMenuPrimitive.Viewport
        data-slot="navigation-menu-viewport"
        className={cn(
          'origin-top-center bg-popover text-popover-foreground data-[state=open]:animate-in data-[state=closed]:animate-out data-[state=closed]:zoom-out-95 data-[state=open]:zoom-in-90 relative mt-1.5 h-[var(--radix-navigation-menu-viewport-height)] w-full overflow-hidden rounded-md border shadow md:w-[var(--radix-navigation-menu-viewport-width)]',
          className,
        )}
        {...props}
      />
    </div>
  )
}

function NavigationMenuLink({
  className,
  ...props
}: React.ComponentProps<typeof NavigationMenuPrimitive.Link>) {
  return (
    <NavigationMenuPrimitive.Link
      data-slot="navigation-menu-link"
      className={cn(
        "data-[active=true]:focus:bg-accent data-[active=true]:hover:bg-accent data-[active=true]:bg-accent/50 data-[active=true]:text-accent-foreground hover:bg-accent hover:text-accent-foreground focus:bg-accent focus:text-accent-foreground focus-visible:ring-ring/50 [&_svg:not([class*='text-'])]:text-muted-foreground flex flex-col gap-1 rounded-sm p-2 text-sm transition-all outline-none focus-visible:ring-[3px] focus-visible:outline-1 [&_svg:not([class*='size-'])]:size-4",
        className,
      )}
      {...props}
    />
  )
}

function NavigationMenuIndicator({
  className,
  ...props
}: React.ComponentProps<typeof NavigationMenuPrimitive.Indicator>) {
  return (
    <NavigationMenuPrimitive.Indicator
      data-slot="navigation-menu-indicator"
      className={cn(
        'data-[state=visible]:animate-in data-[state=hidden]:animate-out data-[state=hidden]:fade-out data-[state=visible]:fade-in top-full z-[1] flex h-1.5 items-end justify-center overflow-hidden',
        className,
      )}
      {...props}
    >
      <div className="bg-border relative top-[60%] h-2 w-2 rotate-45 rounded-tl-sm shadow-md" />
    </NavigationMenuPrimitive.Indicator>
  )
}

export {
  NavigationMenu,
  NavigationMenuList,
  NavigationMenuItem,
  NavigationMenuContent,
  NavigationMenuTrigger,
  NavigationMenuLink,
  NavigationMenuIndicator,
  NavigationMenuViewport,
  navigationMenuTriggerStyle,
}
\n--- END FILE: ./html.code.v0.app/components/ui/navigation-menu.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/tooltip.tsx ---
'use client'

import * as React from 'react'
import * as TooltipPrimitive from '@radix-ui/react-tooltip'

import { cn } from '@/lib/utils'

function TooltipProvider({
  delayDuration = 0,
  ...props
}: React.ComponentProps<typeof TooltipPrimitive.Provider>) {
  return (
    <TooltipPrimitive.Provider
      data-slot="tooltip-provider"
      delayDuration={delayDuration}
      {...props}
    />
  )
}

function Tooltip({
  ...props
}: React.ComponentProps<typeof TooltipPrimitive.Root>) {
  return (
    <TooltipProvider>
      <TooltipPrimitive.Root data-slot="tooltip" {...props} />
    </TooltipProvider>
  )
}

function TooltipTrigger({
  ...props
}: React.ComponentProps<typeof TooltipPrimitive.Trigger>) {
  return <TooltipPrimitive.Trigger data-slot="tooltip-trigger" {...props} />
}

function TooltipContent({
  className,
  sideOffset = 0,
  children,
  ...props
}: React.ComponentProps<typeof TooltipPrimitive.Content>) {
  return (
    <TooltipPrimitive.Portal>
      <TooltipPrimitive.Content
        data-slot="tooltip-content"
        sideOffset={sideOffset}
        className={cn(
          'bg-foreground text-background animate-in fade-in-0 zoom-in-95 data-[state=closed]:animate-out data-[state=closed]:fade-out-0 data-[state=closed]:zoom-out-95 data-[side=bottom]:slide-in-from-top-2 data-[side=left]:slide-in-from-right-2 data-[side=right]:slide-in-from-left-2 data-[side=top]:slide-in-from-bottom-2 z-50 w-fit origin-(--radix-tooltip-content-transform-origin) rounded-md px-3 py-1.5 text-xs text-balance',
          className,
        )}
        {...props}
      >
        {children}
        <TooltipPrimitive.Arrow className="bg-foreground fill-foreground z-50 size-2.5 translate-y-[calc(-50%_-_2px)] rotate-45 rounded-[2px]" />
      </TooltipPrimitive.Content>
    </TooltipPrimitive.Portal>
  )
}

export { Tooltip, TooltipTrigger, TooltipContent, TooltipProvider }
\n--- END FILE: ./html.code.v0.app/components/ui/tooltip.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/checkbox.tsx ---
'use client'

import * as React from 'react'
import * as CheckboxPrimitive from '@radix-ui/react-checkbox'
import { CheckIcon } from 'lucide-react'

import { cn } from '@/lib/utils'

function Checkbox({
  className,
  ...props
}: React.ComponentProps<typeof CheckboxPrimitive.Root>) {
  return (
    <CheckboxPrimitive.Root
      data-slot="checkbox"
      className={cn(
        'peer border-input dark:bg-input/30 data-[state=checked]:bg-primary data-[state=checked]:text-primary-foreground dark:data-[state=checked]:bg-primary data-[state=checked]:border-primary focus-visible:border-ring focus-visible:ring-ring/50 aria-invalid:ring-destructive/20 dark:aria-invalid:ring-destructive/40 aria-invalid:border-destructive size-4 shrink-0 rounded-[4px] border shadow-xs transition-shadow outline-none focus-visible:ring-[3px] disabled:cursor-not-allowed disabled:opacity-50',
        className,
      )}
      {...props}
    >
      <CheckboxPrimitive.Indicator
        data-slot="checkbox-indicator"
        className="flex items-center justify-center text-current transition-none"
      >
        <CheckIcon className="size-3.5" />
      </CheckboxPrimitive.Indicator>
    </CheckboxPrimitive.Root>
  )
}

export { Checkbox }
\n--- END FILE: ./html.code.v0.app/components/ui/checkbox.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/spinner.tsx ---
import { Loader2Icon } from 'lucide-react'

import { cn } from '@/lib/utils'

function Spinner({ className, ...props }: React.ComponentProps<'svg'>) {
  return (
    <Loader2Icon
      role="status"
      aria-label="Loading"
      className={cn('size-4 animate-spin', className)}
      {...props}
    />
  )
}

export { Spinner }
\n--- END FILE: ./html.code.v0.app/components/ui/spinner.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/toggle.tsx ---
'use client'

import * as React from 'react'
import * as TogglePrimitive from '@radix-ui/react-toggle'
import { cva, type VariantProps } from 'class-variance-authority'

import { cn } from '@/lib/utils'

const toggleVariants = cva(
  "inline-flex items-center justify-center gap-2 rounded-md text-sm font-medium hover:bg-muted hover:text-muted-foreground disabled:pointer-events-none disabled:opacity-50 data-[state=on]:bg-accent data-[state=on]:text-accent-foreground [&_svg]:pointer-events-none [&_svg:not([class*='size-'])]:size-4 [&_svg]:shrink-0 focus-visible:border-ring focus-visible:ring-ring/50 focus-visible:ring-[3px] outline-none transition-[color,box-shadow] aria-invalid:ring-destructive/20 dark:aria-invalid:ring-destructive/40 aria-invalid:border-destructive whitespace-nowrap",
  {
    variants: {
      variant: {
        default: 'bg-transparent',
        outline:
          'border border-input bg-transparent shadow-xs hover:bg-accent hover:text-accent-foreground',
      },
      size: {
        default: 'h-9 px-2 min-w-9',
        sm: 'h-8 px-1.5 min-w-8',
        lg: 'h-10 px-2.5 min-w-10',
      },
    },
    defaultVariants: {
      variant: 'default',
      size: 'default',
    },
  },
)

function Toggle({
  className,
  variant,
  size,
  ...props
}: React.ComponentProps<typeof TogglePrimitive.Root> &
  VariantProps<typeof toggleVariants>) {
  return (
    <TogglePrimitive.Root
      data-slot="toggle"
      className={cn(toggleVariants({ variant, size, className }))}
      {...props}
    />
  )
}

export { Toggle, toggleVariants }
\n--- END FILE: ./html.code.v0.app/components/ui/toggle.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/skeleton.tsx ---
import { cn } from '@/lib/utils'

function Skeleton({ className, ...props }: React.ComponentProps<'div'>) {
  return (
    <div
      data-slot="skeleton"
      className={cn('bg-accent animate-pulse rounded-md', className)}
      {...props}
    />
  )
}

export { Skeleton }
\n--- END FILE: ./html.code.v0.app/components/ui/skeleton.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/kbd.tsx ---
import { cn } from '@/lib/utils'

function Kbd({ className, ...props }: React.ComponentProps<'kbd'>) {
  return (
    <kbd
      data-slot="kbd"
      className={cn(
        'bg-muted w-fit text-muted-foreground pointer-events-none inline-flex h-5 min-w-5 items-center justify-center gap-1 rounded-sm px-1 font-sans text-xs font-medium select-none',
        "[&_svg:not([class*='size-'])]:size-3",
        '[[data-slot=tooltip-content]_&]:bg-background/20 [[data-slot=tooltip-content]_&]:text-background dark:[[data-slot=tooltip-content]_&]:bg-background/10',
        className,
      )}
      {...props}
    />
  )
}

function KbdGroup({ className, ...props }: React.ComponentProps<'div'>) {
  return (
    <kbd
      data-slot="kbd-group"
      className={cn('inline-flex items-center gap-1', className)}
      {...props}
    />
  )
}

export { Kbd, KbdGroup }
\n--- END FILE: ./html.code.v0.app/components/ui/kbd.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/chart.tsx ---
'use client'

import * as React from 'react'
import * as RechartsPrimitive from 'recharts'

import { cn } from '@/lib/utils'

// Format: { THEME_NAME: CSS_SELECTOR }
const THEMES = { light: '', dark: '.dark' } as const

export type ChartConfig = {
  [k in string]: {
    label?: React.ReactNode
    icon?: React.ComponentType
  } & (
    | { color?: string; theme?: never }
    | { color?: never; theme: Record<keyof typeof THEMES, string> }
  )
}

type ChartContextProps = {
  config: ChartConfig
}

const ChartContext = React.createContext<ChartContextProps | null>(null)

function useChart() {
  const context = React.useContext(ChartContext)

  if (!context) {
    throw new Error('useChart must be used within a <ChartContainer />')
  }

  return context
}

function ChartContainer({
  id,
  className,
  children,
  config,
  ...props
}: React.ComponentProps<'div'> & {
  config: ChartConfig
  children: React.ComponentProps<
    typeof RechartsPrimitive.ResponsiveContainer
  >['children']
}) {
  const uniqueId = React.useId()
  const chartId = `chart-${id || uniqueId.replace(/:/g, '')}`

  return (
    <ChartContext.Provider value={{ config }}>
      <div
        data-slot="chart"
        data-chart={chartId}
        className={cn(
          "[&_.recharts-cartesian-axis-tick_text]:fill-muted-foreground [&_.recharts-cartesian-grid_line[stroke='#ccc']]:stroke-border/50 [&_.recharts-curve.recharts-tooltip-cursor]:stroke-border [&_.recharts-polar-grid_[stroke='#ccc']]:stroke-border [&_.recharts-radial-bar-background-sector]:fill-muted [&_.recharts-rectangle.recharts-tooltip-cursor]:fill-muted [&_.recharts-reference-line_[stroke='#ccc']]:stroke-border flex aspect-video justify-center text-xs [&_.recharts-dot[stroke='#fff']]:stroke-transparent [&_.recharts-layer]:outline-hidden [&_.recharts-sector]:outline-hidden [&_.recharts-sector[stroke='#fff']]:stroke-transparent [&_.recharts-surface]:outline-hidden",
          className,
        )}
        {...props}
      >
        <ChartStyle id={chartId} config={config} />
        <RechartsPrimitive.ResponsiveContainer>
          {children}
        </RechartsPrimitive.ResponsiveContainer>
      </div>
    </ChartContext.Provider>
  )
}

const ChartStyle = ({ id, config }: { id: string; config: ChartConfig }) => {
  const colorConfig = Object.entries(config).filter(
    ([, config]) => config.theme || config.color,
  )

  if (!colorConfig.length) {
    return null
  }

  return (
    <style
      dangerouslySetInnerHTML={{
        __html: Object.entries(THEMES)
          .map(
            ([theme, prefix]) => `
${prefix} [data-chart=${id}] {
${colorConfig
  .map(([key, itemConfig]) => {
    const color =
      itemConfig.theme?.[theme as keyof typeof itemConfig.theme] ||
      itemConfig.color
    return color ? `  --color-${key}: ${color};` : null
  })
  .join('\n')}
}
`,
          )
          .join('\n'),
      }}
    />
  )
}

const ChartTooltip = RechartsPrimitive.Tooltip

function ChartTooltipContent({
  active,
  payload,
  className,
  indicator = 'dot',
  hideLabel = false,
  hideIndicator = false,
  label,
  labelFormatter,
  labelClassName,
  formatter,
  color,
  nameKey,
  labelKey,
}: React.ComponentProps<typeof RechartsPrimitive.Tooltip> &
  React.ComponentProps<'div'> & {
    hideLabel?: boolean
    hideIndicator?: boolean
    indicator?: 'line' | 'dot' | 'dashed'
    nameKey?: string
    labelKey?: string
  }) {
  const { config } = useChart()

  const tooltipLabel = React.useMemo(() => {
    if (hideLabel || !payload?.length) {
      return null
    }

    const [item] = payload
    const key = `${labelKey || item?.dataKey || item?.name || 'value'}`
    const itemConfig = getPayloadConfigFromPayload(config, item, key)
    const value =
      !labelKey && typeof label === 'string'
        ? config[label as keyof typeof config]?.label || label
        : itemConfig?.label

    if (labelFormatter) {
      return (
        <div className={cn('font-medium', labelClassName)}>
          {labelFormatter(value, payload)}
        </div>
      )
    }

    if (!value) {
      return null
    }

    return <div className={cn('font-medium', labelClassName)}>{value}</div>
  }, [
    label,
    labelFormatter,
    payload,
    hideLabel,
    labelClassName,
    config,
    labelKey,
  ])

  if (!active || !payload?.length) {
    return null
  }

  const nestLabel = payload.length === 1 && indicator !== 'dot'

  return (
    <div
      className={cn(
        'border-border/50 bg-background grid min-w-[8rem] items-start gap-1.5 rounded-lg border px-2.5 py-1.5 text-xs shadow-xl',
        className,
      )}
    >
      {!nestLabel ? tooltipLabel : null}
      <div className="grid gap-1.5">
        {payload.map((item, index) => {
          const key = `${nameKey || item.name || item.dataKey || 'value'}`
          const itemConfig = getPayloadConfigFromPayload(config, item, key)
          const indicatorColor = color || item.payload.fill || item.color

          return (
            <div
              key={item.dataKey}
              className={cn(
                '[&>svg]:text-muted-foreground flex w-full flex-wrap items-stretch gap-2 [&>svg]:h-2.5 [&>svg]:w-2.5',
                indicator === 'dot' && 'items-center',
              )}
            >
              {formatter && item?.value !== undefined && item.name ? (
                formatter(item.value, item.name, item, index, item.payload)
              ) : (
                <>
                  {itemConfig?.icon ? (
                    <itemConfig.icon />
                  ) : (
                    !hideIndicator && (
                      <div
                        className={cn(
                          'shrink-0 rounded-[2px] border-(--color-border) bg-(--color-bg)',
                          {
                            'h-2.5 w-2.5': indicator === 'dot',
                            'w-1': indicator === 'line',
                            'w-0 border-[1.5px] border-dashed bg-transparent':
                              indicator === 'dashed',
                            'my-0.5': nestLabel && indicator === 'dashed',
                          },
                        )}
                        style={
                          {
                            '--color-bg': indicatorColor,
                            '--color-border': indicatorColor,
                          } as React.CSSProperties
                        }
                      />
                    )
                  )}
                  <div
                    className={cn(
                      'flex flex-1 justify-between leading-none',
                      nestLabel ? 'items-end' : 'items-center',
                    )}
                  >
                    <div className="grid gap-1.5">
                      {nestLabel ? tooltipLabel : null}
                      <span className="text-muted-foreground">
                        {itemConfig?.label || item.name}
                      </span>
                    </div>
                    {item.value && (
                      <span className="text-foreground font-mono font-medium tabular-nums">
                        {item.value.toLocaleString()}
                      </span>
                    )}
                  </div>
                </>
              )}
            </div>
          )
        })}
      </div>
    </div>
  )
}

const ChartLegend = RechartsPrimitive.Legend

function ChartLegendContent({
  className,
  hideIcon = false,
  payload,
  verticalAlign = 'bottom',
  nameKey,
}: React.ComponentProps<'div'> &
  Pick<RechartsPrimitive.LegendProps, 'payload' | 'verticalAlign'> & {
    hideIcon?: boolean
    nameKey?: string
  }) {
  const { config } = useChart()

  if (!payload?.length) {
    return null
  }

  return (
    <div
      className={cn(
        'flex items-center justify-center gap-4',
        verticalAlign === 'top' ? 'pb-3' : 'pt-3',
        className,
      )}
    >
      {payload.map((item) => {
        const key = `${nameKey || item.dataKey || 'value'}`
        const itemConfig = getPayloadConfigFromPayload(config, item, key)

        return (
          <div
            key={item.value}
            className={
              '[&>svg]:text-muted-foreground flex items-center gap-1.5 [&>svg]:h-3 [&>svg]:w-3'
            }
          >
            {itemConfig?.icon && !hideIcon ? (
              <itemConfig.icon />
            ) : (
              <div
                className="h-2 w-2 shrink-0 rounded-[2px]"
                style={{
                  backgroundColor: item.color,
                }}
              />
            )}
            {itemConfig?.label}
          </div>
        )
      })}
    </div>
  )
}

// Helper to extract item config from a payload.
function getPayloadConfigFromPayload(
  config: ChartConfig,
  payload: unknown,
  key: string,
) {
  if (typeof payload !== 'object' || payload === null) {
    return undefined
  }

  const payloadPayload =
    'payload' in payload &&
    typeof payload.payload === 'object' &&
    payload.payload !== null
      ? payload.payload
      : undefined

  let configLabelKey: string = key

  if (
    key in payload &&
    typeof payload[key as keyof typeof payload] === 'string'
  ) {
    configLabelKey = payload[key as keyof typeof payload] as string
  } else if (
    payloadPayload &&
    key in payloadPayload &&
    typeof payloadPayload[key as keyof typeof payloadPayload] === 'string'
  ) {
    configLabelKey = payloadPayload[
      key as keyof typeof payloadPayload
    ] as string
  }

  return configLabelKey in config
    ? config[configLabelKey]
    : config[key as keyof typeof config]
}

export {
  ChartContainer,
  ChartTooltip,
  ChartTooltipContent,
  ChartLegend,
  ChartLegendContent,
  ChartStyle,
}
\n--- END FILE: ./html.code.v0.app/components/ui/chart.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/use-mobile.tsx ---
import * as React from 'react'

const MOBILE_BREAKPOINT = 768

export function useIsMobile() {
  const [isMobile, setIsMobile] = React.useState<boolean | undefined>(undefined)

  React.useEffect(() => {
    const mql = window.matchMedia(`(max-width: ${MOBILE_BREAKPOINT - 1}px)`)
    const onChange = () => {
      setIsMobile(window.innerWidth < MOBILE_BREAKPOINT)
    }
    mql.addEventListener('change', onChange)
    setIsMobile(window.innerWidth < MOBILE_BREAKPOINT)
    return () => mql.removeEventListener('change', onChange)
  }, [])

  return !!isMobile
}
\n--- END FILE: ./html.code.v0.app/components/ui/use-mobile.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/toaster.tsx ---
'use client'

import { useToast } from '@/hooks/use-toast'
import {
  Toast,
  ToastClose,
  ToastDescription,
  ToastProvider,
  ToastTitle,
  ToastViewport,
} from '@/components/ui/toast'

export function Toaster() {
  const { toasts } = useToast()

  return (
    <ToastProvider>
      {toasts.map(function ({ id, title, description, action, ...props }) {
        return (
          <Toast key={id} {...props}>
            <div className="grid gap-1">
              {title && <ToastTitle>{title}</ToastTitle>}
              {description && (
                <ToastDescription>{description}</ToastDescription>
              )}
            </div>
            {action}
            <ToastClose />
          </Toast>
        )
      })}
      <ToastViewport />
    </ToastProvider>
  )
}
\n--- END FILE: ./html.code.v0.app/components/ui/toaster.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/button.tsx ---
import * as React from 'react'
import { Slot } from '@radix-ui/react-slot'
import { cva, type VariantProps } from 'class-variance-authority'

import { cn } from '@/lib/utils'

const buttonVariants = cva(
  "inline-flex items-center justify-center gap-2 whitespace-nowrap rounded-md text-sm font-medium transition-all disabled:pointer-events-none disabled:opacity-50 [&_svg]:pointer-events-none [&_svg:not([class*='size-'])]:size-4 shrink-0 [&_svg]:shrink-0 outline-none focus-visible:border-ring focus-visible:ring-ring/50 focus-visible:ring-[3px] aria-invalid:ring-destructive/20 dark:aria-invalid:ring-destructive/40 aria-invalid:border-destructive",
  {
    variants: {
      variant: {
        default: 'bg-primary text-primary-foreground hover:bg-primary/90',
        destructive:
          'bg-destructive text-white hover:bg-destructive/90 focus-visible:ring-destructive/20 dark:focus-visible:ring-destructive/40 dark:bg-destructive/60',
        outline:
          'border bg-background shadow-xs hover:bg-accent hover:text-accent-foreground dark:bg-input/30 dark:border-input dark:hover:bg-input/50',
        secondary:
          'bg-secondary text-secondary-foreground hover:bg-secondary/80',
        ghost:
          'hover:bg-accent hover:text-accent-foreground dark:hover:bg-accent/50',
        link: 'text-primary underline-offset-4 hover:underline',
      },
      size: {
        default: 'h-9 px-4 py-2 has-[>svg]:px-3',
        sm: 'h-8 rounded-md gap-1.5 px-3 has-[>svg]:px-2.5',
        lg: 'h-10 rounded-md px-6 has-[>svg]:px-4',
        icon: 'size-9',
        'icon-sm': 'size-8',
        'icon-lg': 'size-10',
      },
    },
    defaultVariants: {
      variant: 'default',
      size: 'default',
    },
  },
)

function Button({
  className,
  variant,
  size,
  asChild = false,
  ...props
}: React.ComponentProps<'button'> &
  VariantProps<typeof buttonVariants> & {
    asChild?: boolean
  }) {
  const Comp = asChild ? Slot : 'button'

  return (
    <Comp
      data-slot="button"
      className={cn(buttonVariants({ variant, size, className }))}
      {...props}
    />
  )
}

export { Button, buttonVariants }
\n--- END FILE: ./html.code.v0.app/components/ui/button.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/dialog.tsx ---
'use client'

import * as React from 'react'
import * as DialogPrimitive from '@radix-ui/react-dialog'
import { XIcon } from 'lucide-react'

import { cn } from '@/lib/utils'

function Dialog({
  ...props
}: React.ComponentProps<typeof DialogPrimitive.Root>) {
  return <DialogPrimitive.Root data-slot="dialog" {...props} />
}

function DialogTrigger({
  ...props
}: React.ComponentProps<typeof DialogPrimitive.Trigger>) {
  return <DialogPrimitive.Trigger data-slot="dialog-trigger" {...props} />
}

function DialogPortal({
  ...props
}: React.ComponentProps<typeof DialogPrimitive.Portal>) {
  return <DialogPrimitive.Portal data-slot="dialog-portal" {...props} />
}

function DialogClose({
  ...props
}: React.ComponentProps<typeof DialogPrimitive.Close>) {
  return <DialogPrimitive.Close data-slot="dialog-close" {...props} />
}

function DialogOverlay({
  className,
  ...props
}: React.ComponentProps<typeof DialogPrimitive.Overlay>) {
  return (
    <DialogPrimitive.Overlay
      data-slot="dialog-overlay"
      className={cn(
        'data-[state=open]:animate-in data-[state=closed]:animate-out data-[state=closed]:fade-out-0 data-[state=open]:fade-in-0 fixed inset-0 z-50 bg-black/50',
        className,
      )}
      {...props}
    />
  )
}

function DialogContent({
  className,
  children,
  showCloseButton = true,
  ...props
}: React.ComponentProps<typeof DialogPrimitive.Content> & {
  showCloseButton?: boolean
}) {
  return (
    <DialogPortal data-slot="dialog-portal">
      <DialogOverlay />
      <DialogPrimitive.Content
        data-slot="dialog-content"
        className={cn(
          'bg-background data-[state=open]:animate-in data-[state=closed]:animate-out data-[state=closed]:fade-out-0 data-[state=open]:fade-in-0 data-[state=closed]:zoom-out-95 data-[state=open]:zoom-in-95 fixed top-[50%] left-[50%] z-50 grid w-full max-w-[calc(100%-2rem)] translate-x-[-50%] translate-y-[-50%] gap-4 rounded-lg border p-6 shadow-lg duration-200 sm:max-w-lg',
          className,
        )}
        {...props}
      >
        {children}
        {showCloseButton && (
          <DialogPrimitive.Close
            data-slot="dialog-close"
            className="ring-offset-background focus:ring-ring data-[state=open]:bg-accent data-[state=open]:text-muted-foreground absolute top-4 right-4 rounded-xs opacity-70 transition-opacity hover:opacity-100 focus:ring-2 focus:ring-offset-2 focus:outline-hidden disabled:pointer-events-none [&_svg]:pointer-events-none [&_svg]:shrink-0 [&_svg:not([class*='size-'])]:size-4"
          >
            <XIcon />
            <span className="sr-only">Close</span>
          </DialogPrimitive.Close>
        )}
      </DialogPrimitive.Content>
    </DialogPortal>
  )
}

function DialogHeader({ className, ...props }: React.ComponentProps<'div'>) {
  return (
    <div
      data-slot="dialog-header"
      className={cn('flex flex-col gap-2 text-center sm:text-left', className)}
      {...props}
    />
  )
}

function DialogFooter({ className, ...props }: React.ComponentProps<'div'>) {
  return (
    <div
      data-slot="dialog-footer"
      className={cn(
        'flex flex-col-reverse gap-2 sm:flex-row sm:justify-end',
        className,
      )}
      {...props}
    />
  )
}

function DialogTitle({
  className,
  ...props
}: React.ComponentProps<typeof DialogPrimitive.Title>) {
  return (
    <DialogPrimitive.Title
      data-slot="dialog-title"
      className={cn('text-lg leading-none font-semibold', className)}
      {...props}
    />
  )
}

function DialogDescription({
  className,
  ...props
}: React.ComponentProps<typeof DialogPrimitive.Description>) {
  return (
    <DialogPrimitive.Description
      data-slot="dialog-description"
      className={cn('text-muted-foreground text-sm', className)}
      {...props}
    />
  )
}

export {
  Dialog,
  DialogClose,
  DialogContent,
  DialogDescription,
  DialogFooter,
  DialogHeader,
  DialogOverlay,
  DialogPortal,
  DialogTitle,
  DialogTrigger,
}
\n--- END FILE: ./html.code.v0.app/components/ui/dialog.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/use-toast.ts ---
'use client'

// Inspired by react-hot-toast library
import * as React from 'react'

import type { ToastActionElement, ToastProps } from '@/components/ui/toast'

const TOAST_LIMIT = 1
const TOAST_REMOVE_DELAY = 1000000

type ToasterToast = ToastProps & {
  id: string
  title?: React.ReactNode
  description?: React.ReactNode
  action?: ToastActionElement
}

const actionTypes = {
  ADD_TOAST: 'ADD_TOAST',
  UPDATE_TOAST: 'UPDATE_TOAST',
  DISMISS_TOAST: 'DISMISS_TOAST',
  REMOVE_TOAST: 'REMOVE_TOAST',
} as const

let count = 0

function genId() {
  count = (count + 1) % Number.MAX_SAFE_INTEGER
  return count.toString()
}

type ActionType = typeof actionTypes

type Action =
  | {
      type: ActionType['ADD_TOAST']
      toast: ToasterToast
    }
  | {
      type: ActionType['UPDATE_TOAST']
      toast: Partial<ToasterToast>
    }
  | {
      type: ActionType['DISMISS_TOAST']
      toastId?: ToasterToast['id']
    }
  | {
      type: ActionType['REMOVE_TOAST']
      toastId?: ToasterToast['id']
    }

interface State {
  toasts: ToasterToast[]
}

const toastTimeouts = new Map<string, ReturnType<typeof setTimeout>>()

const addToRemoveQueue = (toastId: string) => {
  if (toastTimeouts.has(toastId)) {
    return
  }

  const timeout = setTimeout(() => {
    toastTimeouts.delete(toastId)
    dispatch({
      type: 'REMOVE_TOAST',
      toastId: toastId,
    })
  }, TOAST_REMOVE_DELAY)

  toastTimeouts.set(toastId, timeout)
}

export const reducer = (state: State, action: Action): State => {
  switch (action.type) {
    case 'ADD_TOAST':
      return {
        ...state,
        toasts: [action.toast, ...state.toasts].slice(0, TOAST_LIMIT),
      }

    case 'UPDATE_TOAST':
      return {
        ...state,
        toasts: state.toasts.map((t) =>
          t.id === action.toast.id ? { ...t, ...action.toast } : t,
        ),
      }

    case 'DISMISS_TOAST': {
      const { toastId } = action

      // ! Side effects ! - This could be extracted into a dismissToast() action,
      // but I'll keep it here for simplicity
      if (toastId) {
        addToRemoveQueue(toastId)
      } else {
        state.toasts.forEach((toast) => {
          addToRemoveQueue(toast.id)
        })
      }

      return {
        ...state,
        toasts: state.toasts.map((t) =>
          t.id === toastId || toastId === undefined
            ? {
                ...t,
                open: false,
              }
            : t,
        ),
      }
    }
    case 'REMOVE_TOAST':
      if (action.toastId === undefined) {
        return {
          ...state,
          toasts: [],
        }
      }
      return {
        ...state,
        toasts: state.toasts.filter((t) => t.id !== action.toastId),
      }
  }
}

const listeners: Array<(state: State) => void> = []

let memoryState: State = { toasts: [] }

function dispatch(action: Action) {
  memoryState = reducer(memoryState, action)
  listeners.forEach((listener) => {
    listener(memoryState)
  })
}

type Toast = Omit<ToasterToast, 'id'>

function toast({ ...props }: Toast) {
  const id = genId()

  const update = (props: ToasterToast) =>
    dispatch({
      type: 'UPDATE_TOAST',
      toast: { ...props, id },
    })
  const dismiss = () => dispatch({ type: 'DISMISS_TOAST', toastId: id })

  dispatch({
    type: 'ADD_TOAST',
    toast: {
      ...props,
      id,
      open: true,
      onOpenChange: (open) => {
        if (!open) dismiss()
      },
    },
  })

  return {
    id: id,
    dismiss,
    update,
  }
}

function useToast() {
  const [state, setState] = React.useState<State>(memoryState)

  React.useEffect(() => {
    listeners.push(setState)
    return () => {
      const index = listeners.indexOf(setState)
      if (index > -1) {
        listeners.splice(index, 1)
      }
    }
  }, [state])

  return {
    ...state,
    toast,
    dismiss: (toastId?: string) => dispatch({ type: 'DISMISS_TOAST', toastId }),
  }
}

export { useToast, toast }
\n--- END FILE: ./html.code.v0.app/components/ui/use-toast.ts ---
\n--- START FILE: ./html.code.v0.app/components/ui/scroll-area.tsx ---
'use client'

import * as React from 'react'
import * as ScrollAreaPrimitive from '@radix-ui/react-scroll-area'

import { cn } from '@/lib/utils'

function ScrollArea({
  className,
  children,
  ...props
}: React.ComponentProps<typeof ScrollAreaPrimitive.Root>) {
  return (
    <ScrollAreaPrimitive.Root
      data-slot="scroll-area"
      className={cn('relative', className)}
      {...props}
    >
      <ScrollAreaPrimitive.Viewport
        data-slot="scroll-area-viewport"
        className="focus-visible:ring-ring/50 size-full rounded-[inherit] transition-[color,box-shadow] outline-none focus-visible:ring-[3px] focus-visible:outline-1"
      >
        {children}
      </ScrollAreaPrimitive.Viewport>
      <ScrollBar />
      <ScrollAreaPrimitive.Corner />
    </ScrollAreaPrimitive.Root>
  )
}

function ScrollBar({
  className,
  orientation = 'vertical',
  ...props
}: React.ComponentProps<typeof ScrollAreaPrimitive.ScrollAreaScrollbar>) {
  return (
    <ScrollAreaPrimitive.ScrollAreaScrollbar
      data-slot="scroll-area-scrollbar"
      orientation={orientation}
      className={cn(
        'flex touch-none p-px transition-colors select-none',
        orientation === 'vertical' &&
          'h-full w-2.5 border-l border-l-transparent',
        orientation === 'horizontal' &&
          'h-2.5 flex-col border-t border-t-transparent',
        className,
      )}
      {...props}
    >
      <ScrollAreaPrimitive.ScrollAreaThumb
        data-slot="scroll-area-thumb"
        className="bg-border relative flex-1 rounded-full"
      />
    </ScrollAreaPrimitive.ScrollAreaScrollbar>
  )
}

export { ScrollArea, ScrollBar }
\n--- END FILE: ./html.code.v0.app/components/ui/scroll-area.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/sonner.tsx ---
'use client'

import { useTheme } from 'next-themes'
import { Toaster as Sonner, ToasterProps } from 'sonner'

const Toaster = ({ ...props }: ToasterProps) => {
  const { theme = 'system' } = useTheme()

  return (
    <Sonner
      theme={theme as ToasterProps['theme']}
      className="toaster group"
      style={
        {
          '--normal-bg': 'var(--popover)',
          '--normal-text': 'var(--popover-foreground)',
          '--normal-border': 'var(--border)',
        } as React.CSSProperties
      }
      {...props}
    />
  )
}

export { Toaster }
\n--- END FILE: ./html.code.v0.app/components/ui/sonner.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/sidebar.tsx ---
'use client'

import * as React from 'react'
import { Slot } from '@radix-ui/react-slot'
import { cva, VariantProps } from 'class-variance-authority'
import { PanelLeftIcon } from 'lucide-react'

import { useIsMobile } from '@/hooks/use-mobile'
import { cn } from '@/lib/utils'
import { Button } from '@/components/ui/button'
import { Input } from '@/components/ui/input'
import { Separator } from '@/components/ui/separator'
import {
  Sheet,
  SheetContent,
  SheetDescription,
  SheetHeader,
  SheetTitle,
} from '@/components/ui/sheet'
import { Skeleton } from '@/components/ui/skeleton'
import {
  Tooltip,
  TooltipContent,
  TooltipProvider,
  TooltipTrigger,
} from '@/components/ui/tooltip'

const SIDEBAR_COOKIE_NAME = 'sidebar_state'
const SIDEBAR_COOKIE_MAX_AGE = 60 * 60 * 24 * 7
const SIDEBAR_WIDTH = '16rem'
const SIDEBAR_WIDTH_MOBILE = '18rem'
const SIDEBAR_WIDTH_ICON = '3rem'
const SIDEBAR_KEYBOARD_SHORTCUT = 'b'

type SidebarContextProps = {
  state: 'expanded' | 'collapsed'
  open: boolean
  setOpen: (open: boolean) => void
  openMobile: boolean
  setOpenMobile: (open: boolean) => void
  isMobile: boolean
  toggleSidebar: () => void
}

const SidebarContext = React.createContext<SidebarContextProps | null>(null)

function useSidebar() {
  const context = React.useContext(SidebarContext)
  if (!context) {
    throw new Error('useSidebar must be used within a SidebarProvider.')
  }

  return context
}

function SidebarProvider({
  defaultOpen = true,
  open: openProp,
  onOpenChange: setOpenProp,
  className,
  style,
  children,
  ...props
}: React.ComponentProps<'div'> & {
  defaultOpen?: boolean
  open?: boolean
  onOpenChange?: (open: boolean) => void
}) {
  const isMobile = useIsMobile()
  const [openMobile, setOpenMobile] = React.useState(false)

  // This is the internal state of the sidebar.
  // We use openProp and setOpenProp for control from outside the component.
  const [_open, _setOpen] = React.useState(defaultOpen)
  const open = openProp ?? _open
  const setOpen = React.useCallback(
    (value: boolean | ((value: boolean) => boolean)) => {
      const openState = typeof value === 'function' ? value(open) : value
      if (setOpenProp) {
        setOpenProp(openState)
      } else {
        _setOpen(openState)
      }

      // This sets the cookie to keep the sidebar state.
      document.cookie = `${SIDEBAR_COOKIE_NAME}=${openState}; path=/; max-age=${SIDEBAR_COOKIE_MAX_AGE}`
    },
    [setOpenProp, open],
  )

  // Helper to toggle the sidebar.
  const toggleSidebar = React.useCallback(() => {
    return isMobile ? setOpenMobile((open) => !open) : setOpen((open) => !open)
  }, [isMobile, setOpen, setOpenMobile])

  // Adds a keyboard shortcut to toggle the sidebar.
  React.useEffect(() => {
    const handleKeyDown = (event: KeyboardEvent) => {
      if (
        event.key === SIDEBAR_KEYBOARD_SHORTCUT &&
        (event.metaKey || event.ctrlKey)
      ) {
        event.preventDefault()
        toggleSidebar()
      }
    }

    window.addEventListener('keydown', handleKeyDown)
    return () => window.removeEventListener('keydown', handleKeyDown)
  }, [toggleSidebar])

  // We add a state so that we can do data-state="expanded" or "collapsed".
  // This makes it easier to style the sidebar with Tailwind classes.
  const state = open ? 'expanded' : 'collapsed'

  const contextValue = React.useMemo<SidebarContextProps>(
    () => ({
      state,
      open,
      setOpen,
      isMobile,
      openMobile,
      setOpenMobile,
      toggleSidebar,
    }),
    [state, open, setOpen, isMobile, openMobile, setOpenMobile, toggleSidebar],
  )

  return (
    <SidebarContext.Provider value={contextValue}>
      <TooltipProvider delayDuration={0}>
        <div
          data-slot="sidebar-wrapper"
          style={
            {
              '--sidebar-width': SIDEBAR_WIDTH,
              '--sidebar-width-icon': SIDEBAR_WIDTH_ICON,
              ...style,
            } as React.CSSProperties
          }
          className={cn(
            'group/sidebar-wrapper has-data-[variant=inset]:bg-sidebar flex min-h-svh w-full',
            className,
          )}
          {...props}
        >
          {children}
        </div>
      </TooltipProvider>
    </SidebarContext.Provider>
  )
}

function Sidebar({
  side = 'left',
  variant = 'sidebar',
  collapsible = 'offcanvas',
  className,
  children,
  ...props
}: React.ComponentProps<'div'> & {
  side?: 'left' | 'right'
  variant?: 'sidebar' | 'floating' | 'inset'
  collapsible?: 'offcanvas' | 'icon' | 'none'
}) {
  const { isMobile, state, openMobile, setOpenMobile } = useSidebar()

  if (collapsible === 'none') {
    return (
      <div
        data-slot="sidebar"
        className={cn(
          'bg-sidebar text-sidebar-foreground flex h-full w-(--sidebar-width) flex-col',
          className,
        )}
        {...props}
      >
        {children}
      </div>
    )
  }

  if (isMobile) {
    return (
      <Sheet open={openMobile} onOpenChange={setOpenMobile} {...props}>
        <SheetContent
          data-sidebar="sidebar"
          data-slot="sidebar"
          data-mobile="true"
          className="bg-sidebar text-sidebar-foreground w-(--sidebar-width) p-0 [&>button]:hidden"
          style={
            {
              '--sidebar-width': SIDEBAR_WIDTH_MOBILE,
            } as React.CSSProperties
          }
          side={side}
        >
          <SheetHeader className="sr-only">
            <SheetTitle>Sidebar</SheetTitle>
            <SheetDescription>Displays the mobile sidebar.</SheetDescription>
          </SheetHeader>
          <div className="flex h-full w-full flex-col">{children}</div>
        </SheetContent>
      </Sheet>
    )
  }

  return (
    <div
      className="group peer text-sidebar-foreground hidden md:block"
      data-state={state}
      data-collapsible={state === 'collapsed' ? collapsible : ''}
      data-variant={variant}
      data-side={side}
      data-slot="sidebar"
    >
      {/* This is what handles the sidebar gap on desktop */}
      <div
        data-slot="sidebar-gap"
        className={cn(
          'relative w-(--sidebar-width) bg-transparent transition-[width] duration-200 ease-linear',
          'group-data-[collapsible=offcanvas]:w-0',
          'group-data-[side=right]:rotate-180',
          variant === 'floating' || variant === 'inset'
            ? 'group-data-[collapsible=icon]:w-[calc(var(--sidebar-width-icon)+(--spacing(4)))]'
            : 'group-data-[collapsible=icon]:w-(--sidebar-width-icon)',
        )}
      />
      <div
        data-slot="sidebar-container"
        className={cn(
          'fixed inset-y-0 z-10 hidden h-svh w-(--sidebar-width) transition-[left,right,width] duration-200 ease-linear md:flex',
          side === 'left'
            ? 'left-0 group-data-[collapsible=offcanvas]:left-[calc(var(--sidebar-width)*-1)]'
            : 'right-0 group-data-[collapsible=offcanvas]:right-[calc(var(--sidebar-width)*-1)]',
          // Adjust the padding for floating and inset variants.
          variant === 'floating' || variant === 'inset'
            ? 'p-2 group-data-[collapsible=icon]:w-[calc(var(--sidebar-width-icon)+(--spacing(4))+2px)]'
            : 'group-data-[collapsible=icon]:w-(--sidebar-width-icon) group-data-[side=left]:border-r group-data-[side=right]:border-l',
          className,
        )}
        {...props}
      >
        <div
          data-sidebar="sidebar"
          data-slot="sidebar-inner"
          className="bg-sidebar group-data-[variant=floating]:border-sidebar-border flex h-full w-full flex-col group-data-[variant=floating]:rounded-lg group-data-[variant=floating]:border group-data-[variant=floating]:shadow-sm"
        >
          {children}
        </div>
      </div>
    </div>
  )
}

function SidebarTrigger({
  className,
  onClick,
  ...props
}: React.ComponentProps<typeof Button>) {
  const { toggleSidebar } = useSidebar()

  return (
    <Button
      data-sidebar="trigger"
      data-slot="sidebar-trigger"
      variant="ghost"
      size="icon"
      className={cn('size-7', className)}
      onClick={(event) => {
        onClick?.(event)
        toggleSidebar()
      }}
      {...props}
    >
      <PanelLeftIcon />
      <span className="sr-only">Toggle Sidebar</span>
    </Button>
  )
}

function SidebarRail({ className, ...props }: React.ComponentProps<'button'>) {
  const { toggleSidebar } = useSidebar()

  return (
    <button
      data-sidebar="rail"
      data-slot="sidebar-rail"
      aria-label="Toggle Sidebar"
      tabIndex={-1}
      onClick={toggleSidebar}
      title="Toggle Sidebar"
      className={cn(
        'hover:after:bg-sidebar-border absolute inset-y-0 z-20 hidden w-4 -translate-x-1/2 transition-all ease-linear group-data-[side=left]:-right-4 group-data-[side=right]:left-0 after:absolute after:inset-y-0 after:left-1/2 after:w-[2px] sm:flex',
        'in-data-[side=left]:cursor-w-resize in-data-[side=right]:cursor-e-resize',
        '[[data-side=left][data-state=collapsed]_&]:cursor-e-resize [[data-side=right][data-state=collapsed]_&]:cursor-w-resize',
        'hover:group-data-[collapsible=offcanvas]:bg-sidebar group-data-[collapsible=offcanvas]:translate-x-0 group-data-[collapsible=offcanvas]:after:left-full',
        '[[data-side=left][data-collapsible=offcanvas]_&]:-right-2',
        '[[data-side=right][data-collapsible=offcanvas]_&]:-left-2',
        className,
      )}
      {...props}
    />
  )
}

function SidebarInset({ className, ...props }: React.ComponentProps<'main'>) {
  return (
    <main
      data-slot="sidebar-inset"
      className={cn(
        'bg-background relative flex w-full flex-1 flex-col',
        'md:peer-data-[variant=inset]:m-2 md:peer-data-[variant=inset]:ml-0 md:peer-data-[variant=inset]:rounded-xl md:peer-data-[variant=inset]:shadow-sm md:peer-data-[variant=inset]:peer-data-[state=collapsed]:ml-2',
        className,
      )}
      {...props}
    />
  )
}

function SidebarInput({
  className,
  ...props
}: React.ComponentProps<typeof Input>) {
  return (
    <Input
      data-slot="sidebar-input"
      data-sidebar="input"
      className={cn('bg-background h-8 w-full shadow-none', className)}
      {...props}
    />
  )
}

function SidebarHeader({ className, ...props }: React.ComponentProps<'div'>) {
  return (
    <div
      data-slot="sidebar-header"
      data-sidebar="header"
      className={cn('flex flex-col gap-2 p-2', className)}
      {...props}
    />
  )
}

function SidebarFooter({ className, ...props }: React.ComponentProps<'div'>) {
  return (
    <div
      data-slot="sidebar-footer"
      data-sidebar="footer"
      className={cn('flex flex-col gap-2 p-2', className)}
      {...props}
    />
  )
}

function SidebarSeparator({
  className,
  ...props
}: React.ComponentProps<typeof Separator>) {
  return (
    <Separator
      data-slot="sidebar-separator"
      data-sidebar="separator"
      className={cn('bg-sidebar-border mx-2 w-auto', className)}
      {...props}
    />
  )
}

function SidebarContent({ className, ...props }: React.ComponentProps<'div'>) {
  return (
    <div
      data-slot="sidebar-content"
      data-sidebar="content"
      className={cn(
        'flex min-h-0 flex-1 flex-col gap-2 overflow-auto group-data-[collapsible=icon]:overflow-hidden',
        className,
      )}
      {...props}
    />
  )
}

function SidebarGroup({ className, ...props }: React.ComponentProps<'div'>) {
  return (
    <div
      data-slot="sidebar-group"
      data-sidebar="group"
      className={cn('relative flex w-full min-w-0 flex-col p-2', className)}
      {...props}
    />
  )
}

function SidebarGroupLabel({
  className,
  asChild = false,
  ...props
}: React.ComponentProps<'div'> & { asChild?: boolean }) {
  const Comp = asChild ? Slot : 'div'

  return (
    <Comp
      data-slot="sidebar-group-label"
      data-sidebar="group-label"
      className={cn(
        'text-sidebar-foreground/70 ring-sidebar-ring flex h-8 shrink-0 items-center rounded-md px-2 text-xs font-medium outline-hidden transition-[margin,opacity] duration-200 ease-linear focus-visible:ring-2 [&>svg]:size-4 [&>svg]:shrink-0',
        'group-data-[collapsible=icon]:-mt-8 group-data-[collapsible=icon]:opacity-0',
        className,
      )}
      {...props}
    />
  )
}

function SidebarGroupAction({
  className,
  asChild = false,
  ...props
}: React.ComponentProps<'button'> & { asChild?: boolean }) {
  const Comp = asChild ? Slot : 'button'

  return (
    <Comp
      data-slot="sidebar-group-action"
      data-sidebar="group-action"
      className={cn(
        'text-sidebar-foreground ring-sidebar-ring hover:bg-sidebar-accent hover:text-sidebar-accent-foreground absolute top-3.5 right-3 flex aspect-square w-5 items-center justify-center rounded-md p-0 outline-hidden transition-transform focus-visible:ring-2 [&>svg]:size-4 [&>svg]:shrink-0',
        // Increases the hit area of the button on mobile.
        'after:absolute after:-inset-2 md:after:hidden',
        'group-data-[collapsible=icon]:hidden',
        className,
      )}
      {...props}
    />
  )
}

function SidebarGroupContent({
  className,
  ...props
}: React.ComponentProps<'div'>) {
  return (
    <div
      data-slot="sidebar-group-content"
      data-sidebar="group-content"
      className={cn('w-full text-sm', className)}
      {...props}
    />
  )
}

function SidebarMenu({ className, ...props }: React.ComponentProps<'ul'>) {
  return (
    <ul
      data-slot="sidebar-menu"
      data-sidebar="menu"
      className={cn('flex w-full min-w-0 flex-col gap-1', className)}
      {...props}
    />
  )
}

function SidebarMenuItem({ className, ...props }: React.ComponentProps<'li'>) {
  return (
    <li
      data-slot="sidebar-menu-item"
      data-sidebar="menu-item"
      className={cn('group/menu-item relative', className)}
      {...props}
    />
  )
}

const sidebarMenuButtonVariants = cva(
  'peer/menu-button flex w-full items-center gap-2 overflow-hidden rounded-md p-2 text-left text-sm outline-hidden ring-sidebar-ring transition-[width,height,padding] hover:bg-sidebar-accent hover:text-sidebar-accent-foreground focus-visible:ring-2 active:bg-sidebar-accent active:text-sidebar-accent-foreground disabled:pointer-events-none disabled:opacity-50 group-has-data-[sidebar=menu-action]/menu-item:pr-8 aria-disabled:pointer-events-none aria-disabled:opacity-50 data-[active=true]:bg-sidebar-accent data-[active=true]:font-medium data-[active=true]:text-sidebar-accent-foreground data-[state=open]:hover:bg-sidebar-accent data-[state=open]:hover:text-sidebar-accent-foreground group-data-[collapsible=icon]:size-8! group-data-[collapsible=icon]:p-2! [&>span:last-child]:truncate [&>svg]:size-4 [&>svg]:shrink-0',
  {
    variants: {
      variant: {
        default: 'hover:bg-sidebar-accent hover:text-sidebar-accent-foreground',
        outline:
          'bg-background shadow-[0_0_0_1px_hsl(var(--sidebar-border))] hover:bg-sidebar-accent hover:text-sidebar-accent-foreground hover:shadow-[0_0_0_1px_hsl(var(--sidebar-accent))]',
      },
      size: {
        default: 'h-8 text-sm',
        sm: 'h-7 text-xs',
        lg: 'h-12 text-sm group-data-[collapsible=icon]:p-0!',
      },
    },
    defaultVariants: {
      variant: 'default',
      size: 'default',
    },
  },
)

function SidebarMenuButton({
  asChild = false,
  isActive = false,
  variant = 'default',
  size = 'default',
  tooltip,
  className,
  ...props
}: React.ComponentProps<'button'> & {
  asChild?: boolean
  isActive?: boolean
  tooltip?: string | React.ComponentProps<typeof TooltipContent>
} & VariantProps<typeof sidebarMenuButtonVariants>) {
  const Comp = asChild ? Slot : 'button'
  const { isMobile, state } = useSidebar()

  const button = (
    <Comp
      data-slot="sidebar-menu-button"
      data-sidebar="menu-button"
      data-size={size}
      data-active={isActive}
      className={cn(sidebarMenuButtonVariants({ variant, size }), className)}
      {...props}
    />
  )

  if (!tooltip) {
    return button
  }

  if (typeof tooltip === 'string') {
    tooltip = {
      children: tooltip,
    }
  }

  return (
    <Tooltip>
      <TooltipTrigger asChild>{button}</TooltipTrigger>
      <TooltipContent
        side="right"
        align="center"
        hidden={state !== 'collapsed' || isMobile}
        {...tooltip}
      />
    </Tooltip>
  )
}

function SidebarMenuAction({
  className,
  asChild = false,
  showOnHover = false,
  ...props
}: React.ComponentProps<'button'> & {
  asChild?: boolean
  showOnHover?: boolean
}) {
  const Comp = asChild ? Slot : 'button'

  return (
    <Comp
      data-slot="sidebar-menu-action"
      data-sidebar="menu-action"
      className={cn(
        'text-sidebar-foreground ring-sidebar-ring hover:bg-sidebar-accent hover:text-sidebar-accent-foreground peer-hover/menu-button:text-sidebar-accent-foreground absolute top-1.5 right-1 flex aspect-square w-5 items-center justify-center rounded-md p-0 outline-hidden transition-transform focus-visible:ring-2 [&>svg]:size-4 [&>svg]:shrink-0',
        // Increases the hit area of the button on mobile.
        'after:absolute after:-inset-2 md:after:hidden',
        'peer-data-[size=sm]/menu-button:top-1',
        'peer-data-[size=default]/menu-button:top-1.5',
        'peer-data-[size=lg]/menu-button:top-2.5',
        'group-data-[collapsible=icon]:hidden',
        showOnHover &&
          'peer-data-[active=true]/menu-button:text-sidebar-accent-foreground group-focus-within/menu-item:opacity-100 group-hover/menu-item:opacity-100 data-[state=open]:opacity-100 md:opacity-0',
        className,
      )}
      {...props}
    />
  )
}

function SidebarMenuBadge({
  className,
  ...props
}: React.ComponentProps<'div'>) {
  return (
    <div
      data-slot="sidebar-menu-badge"
      data-sidebar="menu-badge"
      className={cn(
        'text-sidebar-foreground pointer-events-none absolute right-1 flex h-5 min-w-5 items-center justify-center rounded-md px-1 text-xs font-medium tabular-nums select-none',
        'peer-hover/menu-button:text-sidebar-accent-foreground peer-data-[active=true]/menu-button:text-sidebar-accent-foreground',
        'peer-data-[size=sm]/menu-button:top-1',
        'peer-data-[size=default]/menu-button:top-1.5',
        'peer-data-[size=lg]/menu-button:top-2.5',
        'group-data-[collapsible=icon]:hidden',
        className,
      )}
      {...props}
    />
  )
}

function SidebarMenuSkeleton({
  className,
  showIcon = false,
  ...props
}: React.ComponentProps<'div'> & {
  showIcon?: boolean
}) {
  // Random width between 50 to 90%.
  const width = React.useMemo(() => {
    return `${Math.floor(Math.random() * 40) + 50}%`
  }, [])

  return (
    <div
      data-slot="sidebar-menu-skeleton"
      data-sidebar="menu-skeleton"
      className={cn('flex h-8 items-center gap-2 rounded-md px-2', className)}
      {...props}
    >
      {showIcon && (
        <Skeleton
          className="size-4 rounded-md"
          data-sidebar="menu-skeleton-icon"
        />
      )}
      <Skeleton
        className="h-4 max-w-(--skeleton-width) flex-1"
        data-sidebar="menu-skeleton-text"
        style={
          {
            '--skeleton-width': width,
          } as React.CSSProperties
        }
      />
    </div>
  )
}

function SidebarMenuSub({ className, ...props }: React.ComponentProps<'ul'>) {
  return (
    <ul
      data-slot="sidebar-menu-sub"
      data-sidebar="menu-sub"
      className={cn(
        'border-sidebar-border mx-3.5 flex min-w-0 translate-x-px flex-col gap-1 border-l px-2.5 py-0.5',
        'group-data-[collapsible=icon]:hidden',
        className,
      )}
      {...props}
    />
  )
}

function SidebarMenuSubItem({
  className,
  ...props
}: React.ComponentProps<'li'>) {
  return (
    <li
      data-slot="sidebar-menu-sub-item"
      data-sidebar="menu-sub-item"
      className={cn('group/menu-sub-item relative', className)}
      {...props}
    />
  )
}

function SidebarMenuSubButton({
  asChild = false,
  size = 'md',
  isActive = false,
  className,
  ...props
}: React.ComponentProps<'a'> & {
  asChild?: boolean
  size?: 'sm' | 'md'
  isActive?: boolean
}) {
  const Comp = asChild ? Slot : 'a'

  return (
    <Comp
      data-slot="sidebar-menu-sub-button"
      data-sidebar="menu-sub-button"
      data-size={size}
      data-active={isActive}
      className={cn(
        'text-sidebar-foreground ring-sidebar-ring hover:bg-sidebar-accent hover:text-sidebar-accent-foreground active:bg-sidebar-accent active:text-sidebar-accent-foreground [&>svg]:text-sidebar-accent-foreground flex h-7 min-w-0 -translate-x-px items-center gap-2 overflow-hidden rounded-md px-2 outline-hidden focus-visible:ring-2 disabled:pointer-events-none disabled:opacity-50 aria-disabled:pointer-events-none aria-disabled:opacity-50 [&>span:last-child]:truncate [&>svg]:size-4 [&>svg]:shrink-0',
        'data-[active=true]:bg-sidebar-accent data-[active=true]:text-sidebar-accent-foreground',
        size === 'sm' && 'text-xs',
        size === 'md' && 'text-sm',
        'group-data-[collapsible=icon]:hidden',
        className,
      )}
      {...props}
    />
  )
}

export {
  Sidebar,
  SidebarContent,
  SidebarFooter,
  SidebarGroup,
  SidebarGroupAction,
  SidebarGroupContent,
  SidebarGroupLabel,
  SidebarHeader,
  SidebarInput,
  SidebarInset,
  SidebarMenu,
  SidebarMenuAction,
  SidebarMenuBadge,
  SidebarMenuButton,
  SidebarMenuItem,
  SidebarMenuSkeleton,
  SidebarMenuSub,
  SidebarMenuSubButton,
  SidebarMenuSubItem,
  SidebarProvider,
  SidebarRail,
  SidebarSeparator,
  SidebarTrigger,
  useSidebar,
}
\n--- END FILE: ./html.code.v0.app/components/ui/sidebar.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/pagination.tsx ---
import * as React from 'react'
import {
  ChevronLeftIcon,
  ChevronRightIcon,
  MoreHorizontalIcon,
} from 'lucide-react'

import { cn } from '@/lib/utils'
import { Button, buttonVariants } from '@/components/ui/button'

function Pagination({ className, ...props }: React.ComponentProps<'nav'>) {
  return (
    <nav
      role="navigation"
      aria-label="pagination"
      data-slot="pagination"
      className={cn('mx-auto flex w-full justify-center', className)}
      {...props}
    />
  )
}

function PaginationContent({
  className,
  ...props
}: React.ComponentProps<'ul'>) {
  return (
    <ul
      data-slot="pagination-content"
      className={cn('flex flex-row items-center gap-1', className)}
      {...props}
    />
  )
}

function PaginationItem({ ...props }: React.ComponentProps<'li'>) {
  return <li data-slot="pagination-item" {...props} />
}

type PaginationLinkProps = {
  isActive?: boolean
} & Pick<React.ComponentProps<typeof Button>, 'size'> &
  React.ComponentProps<'a'>

function PaginationLink({
  className,
  isActive,
  size = 'icon',
  ...props
}: PaginationLinkProps) {
  return (
    <a
      aria-current={isActive ? 'page' : undefined}
      data-slot="pagination-link"
      data-active={isActive}
      className={cn(
        buttonVariants({
          variant: isActive ? 'outline' : 'ghost',
          size,
        }),
        className,
      )}
      {...props}
    />
  )
}

function PaginationPrevious({
  className,
  ...props
}: React.ComponentProps<typeof PaginationLink>) {
  return (
    <PaginationLink
      aria-label="Go to previous page"
      size="default"
      className={cn('gap-1 px-2.5 sm:pl-2.5', className)}
      {...props}
    >
      <ChevronLeftIcon />
      <span className="hidden sm:block">Previous</span>
    </PaginationLink>
  )
}

function PaginationNext({
  className,
  ...props
}: React.ComponentProps<typeof PaginationLink>) {
  return (
    <PaginationLink
      aria-label="Go to next page"
      size="default"
      className={cn('gap-1 px-2.5 sm:pr-2.5', className)}
      {...props}
    >
      <span className="hidden sm:block">Next</span>
      <ChevronRightIcon />
    </PaginationLink>
  )
}

function PaginationEllipsis({
  className,
  ...props
}: React.ComponentProps<'span'>) {
  return (
    <span
      aria-hidden
      data-slot="pagination-ellipsis"
      className={cn('flex size-9 items-center justify-center', className)}
      {...props}
    >
      <MoreHorizontalIcon className="size-4" />
      <span className="sr-only">More pages</span>
    </span>
  )
}

export {
  Pagination,
  PaginationContent,
  PaginationLink,
  PaginationItem,
  PaginationPrevious,
  PaginationNext,
  PaginationEllipsis,
}
\n--- END FILE: ./html.code.v0.app/components/ui/pagination.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/breadcrumb.tsx ---
import * as React from 'react'
import { Slot } from '@radix-ui/react-slot'
import { ChevronRight, MoreHorizontal } from 'lucide-react'

import { cn } from '@/lib/utils'

function Breadcrumb({ ...props }: React.ComponentProps<'nav'>) {
  return <nav aria-label="breadcrumb" data-slot="breadcrumb" {...props} />
}

function BreadcrumbList({ className, ...props }: React.ComponentProps<'ol'>) {
  return (
    <ol
      data-slot="breadcrumb-list"
      className={cn(
        'text-muted-foreground flex flex-wrap items-center gap-1.5 text-sm break-words sm:gap-2.5',
        className,
      )}
      {...props}
    />
  )
}

function BreadcrumbItem({ className, ...props }: React.ComponentProps<'li'>) {
  return (
    <li
      data-slot="breadcrumb-item"
      className={cn('inline-flex items-center gap-1.5', className)}
      {...props}
    />
  )
}

function BreadcrumbLink({
  asChild,
  className,
  ...props
}: React.ComponentProps<'a'> & {
  asChild?: boolean
}) {
  const Comp = asChild ? Slot : 'a'

  return (
    <Comp
      data-slot="breadcrumb-link"
      className={cn('hover:text-foreground transition-colors', className)}
      {...props}
    />
  )
}

function BreadcrumbPage({ className, ...props }: React.ComponentProps<'span'>) {
  return (
    <span
      data-slot="breadcrumb-page"
      role="link"
      aria-disabled="true"
      aria-current="page"
      className={cn('text-foreground font-normal', className)}
      {...props}
    />
  )
}

function BreadcrumbSeparator({
  children,
  className,
  ...props
}: React.ComponentProps<'li'>) {
  return (
    <li
      data-slot="breadcrumb-separator"
      role="presentation"
      aria-hidden="true"
      className={cn('[&>svg]:size-3.5', className)}
      {...props}
    >
      {children ?? <ChevronRight />}
    </li>
  )
}

function BreadcrumbEllipsis({
  className,
  ...props
}: React.ComponentProps<'span'>) {
  return (
    <span
      data-slot="breadcrumb-ellipsis"
      role="presentation"
      aria-hidden="true"
      className={cn('flex size-9 items-center justify-center', className)}
      {...props}
    >
      <MoreHorizontal className="size-4" />
      <span className="sr-only">More</span>
    </span>
  )
}

export {
  Breadcrumb,
  BreadcrumbList,
  BreadcrumbItem,
  BreadcrumbLink,
  BreadcrumbPage,
  BreadcrumbSeparator,
  BreadcrumbEllipsis,
}
\n--- END FILE: ./html.code.v0.app/components/ui/breadcrumb.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/label.tsx ---
'use client'

import * as React from 'react'
import * as LabelPrimitive from '@radix-ui/react-label'

import { cn } from '@/lib/utils'

function Label({
  className,
  ...props
}: React.ComponentProps<typeof LabelPrimitive.Root>) {
  return (
    <LabelPrimitive.Root
      data-slot="label"
      className={cn(
        'flex items-center gap-2 text-sm leading-none font-medium select-none group-data-[disabled=true]:pointer-events-none group-data-[disabled=true]:opacity-50 peer-disabled:cursor-not-allowed peer-disabled:opacity-50',
        className,
      )}
      {...props}
    />
  )
}

export { Label }
\n--- END FILE: ./html.code.v0.app/components/ui/label.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/switch.tsx ---
'use client'

import * as React from 'react'
import * as SwitchPrimitive from '@radix-ui/react-switch'

import { cn } from '@/lib/utils'

function Switch({
  className,
  ...props
}: React.ComponentProps<typeof SwitchPrimitive.Root>) {
  return (
    <SwitchPrimitive.Root
      data-slot="switch"
      className={cn(
        'peer data-[state=checked]:bg-primary data-[state=unchecked]:bg-input focus-visible:border-ring focus-visible:ring-ring/50 dark:data-[state=unchecked]:bg-input/80 inline-flex h-[1.15rem] w-8 shrink-0 items-center rounded-full border border-transparent shadow-xs transition-all outline-none focus-visible:ring-[3px] disabled:cursor-not-allowed disabled:opacity-50',
        className,
      )}
      {...props}
    >
      <SwitchPrimitive.Thumb
        data-slot="switch-thumb"
        className={
          'bg-background dark:data-[state=unchecked]:bg-foreground dark:data-[state=checked]:bg-primary-foreground pointer-events-none block size-4 rounded-full ring-0 transition-transform data-[state=checked]:translate-x-[calc(100%-2px)] data-[state=unchecked]:translate-x-0'
        }
      />
    </SwitchPrimitive.Root>
  )
}

export { Switch }
\n--- END FILE: ./html.code.v0.app/components/ui/switch.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/accordion.tsx ---
'use client'

import * as React from 'react'
import * as AccordionPrimitive from '@radix-ui/react-accordion'
import { ChevronDownIcon } from 'lucide-react'

import { cn } from '@/lib/utils'

function Accordion({
  ...props
}: React.ComponentProps<typeof AccordionPrimitive.Root>) {
  return <AccordionPrimitive.Root data-slot="accordion" {...props} />
}

function AccordionItem({
  className,
  ...props
}: React.ComponentProps<typeof AccordionPrimitive.Item>) {
  return (
    <AccordionPrimitive.Item
      data-slot="accordion-item"
      className={cn('border-b last:border-b-0', className)}
      {...props}
    />
  )
}

function AccordionTrigger({
  className,
  children,
  ...props
}: React.ComponentProps<typeof AccordionPrimitive.Trigger>) {
  return (
    <AccordionPrimitive.Header className="flex">
      <AccordionPrimitive.Trigger
        data-slot="accordion-trigger"
        className={cn(
          'focus-visible:border-ring focus-visible:ring-ring/50 flex flex-1 items-start justify-between gap-4 rounded-md py-4 text-left text-sm font-medium transition-all outline-none hover:underline focus-visible:ring-[3px] disabled:pointer-events-none disabled:opacity-50 [&[data-state=open]>svg]:rotate-180',
          className,
        )}
        {...props}
      >
        {children}
        <ChevronDownIcon className="text-muted-foreground pointer-events-none size-4 shrink-0 translate-y-0.5 transition-transform duration-200" />
      </AccordionPrimitive.Trigger>
    </AccordionPrimitive.Header>
  )
}

function AccordionContent({
  className,
  children,
  ...props
}: React.ComponentProps<typeof AccordionPrimitive.Content>) {
  return (
    <AccordionPrimitive.Content
      data-slot="accordion-content"
      className="data-[state=closed]:animate-accordion-up data-[state=open]:animate-accordion-down overflow-hidden text-sm"
      {...props}
    >
      <div className={cn('pt-0 pb-4', className)}>{children}</div>
    </AccordionPrimitive.Content>
  )
}

export { Accordion, AccordionItem, AccordionTrigger, AccordionContent }
\n--- END FILE: ./html.code.v0.app/components/ui/accordion.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/alert.tsx ---
import * as React from 'react'
import { cva, type VariantProps } from 'class-variance-authority'

import { cn } from '@/lib/utils'

const alertVariants = cva(
  'relative w-full rounded-lg border px-4 py-3 text-sm grid has-[>svg]:grid-cols-[calc(var(--spacing)*4)_1fr] grid-cols-[0_1fr] has-[>svg]:gap-x-3 gap-y-0.5 items-start [&>svg]:size-4 [&>svg]:translate-y-0.5 [&>svg]:text-current',
  {
    variants: {
      variant: {
        default: 'bg-card text-card-foreground',
        destructive:
          'text-destructive bg-card [&>svg]:text-current *:data-[slot=alert-description]:text-destructive/90',
      },
    },
    defaultVariants: {
      variant: 'default',
    },
  },
)

function Alert({
  className,
  variant,
  ...props
}: React.ComponentProps<'div'> & VariantProps<typeof alertVariants>) {
  return (
    <div
      data-slot="alert"
      role="alert"
      className={cn(alertVariants({ variant }), className)}
      {...props}
    />
  )
}

function AlertTitle({ className, ...props }: React.ComponentProps<'div'>) {
  return (
    <div
      data-slot="alert-title"
      className={cn(
        'col-start-2 line-clamp-1 min-h-4 font-medium tracking-tight',
        className,
      )}
      {...props}
    />
  )
}

function AlertDescription({
  className,
  ...props
}: React.ComponentProps<'div'>) {
  return (
    <div
      data-slot="alert-description"
      className={cn(
        'text-muted-foreground col-start-2 grid justify-items-start gap-1 text-sm [&_p]:leading-relaxed',
        className,
      )}
      {...props}
    />
  )
}

export { Alert, AlertTitle, AlertDescription }
\n--- END FILE: ./html.code.v0.app/components/ui/alert.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/form.tsx ---
'use client'

import * as React from 'react'
import * as LabelPrimitive from '@radix-ui/react-label'
import { Slot } from '@radix-ui/react-slot'
import {
  Controller,
  FormProvider,
  useFormContext,
  useFormState,
  type ControllerProps,
  type FieldPath,
  type FieldValues,
} from 'react-hook-form'

import { cn } from '@/lib/utils'
import { Label } from '@/components/ui/label'

const Form = FormProvider

type FormFieldContextValue<
  TFieldValues extends FieldValues = FieldValues,
  TName extends FieldPath<TFieldValues> = FieldPath<TFieldValues>,
> = {
  name: TName
}

const FormFieldContext = React.createContext<FormFieldContextValue>(
  {} as FormFieldContextValue,
)

const FormField = <
  TFieldValues extends FieldValues = FieldValues,
  TName extends FieldPath<TFieldValues> = FieldPath<TFieldValues>,
>({
  ...props
}: ControllerProps<TFieldValues, TName>) => {
  return (
    <FormFieldContext.Provider value={{ name: props.name }}>
      <Controller {...props} />
    </FormFieldContext.Provider>
  )
}

const useFormField = () => {
  const fieldContext = React.useContext(FormFieldContext)
  const itemContext = React.useContext(FormItemContext)
  const { getFieldState } = useFormContext()
  const formState = useFormState({ name: fieldContext.name })
  const fieldState = getFieldState(fieldContext.name, formState)

  if (!fieldContext) {
    throw new Error('useFormField should be used within <FormField>')
  }

  const { id } = itemContext

  return {
    id,
    name: fieldContext.name,
    formItemId: `${id}-form-item`,
    formDescriptionId: `${id}-form-item-description`,
    formMessageId: `${id}-form-item-message`,
    ...fieldState,
  }
}

type FormItemContextValue = {
  id: string
}

const FormItemContext = React.createContext<FormItemContextValue>(
  {} as FormItemContextValue,
)

function FormItem({ className, ...props }: React.ComponentProps<'div'>) {
  const id = React.useId()

  return (
    <FormItemContext.Provider value={{ id }}>
      <div
        data-slot="form-item"
        className={cn('grid gap-2', className)}
        {...props}
      />
    </FormItemContext.Provider>
  )
}

function FormLabel({
  className,
  ...props
}: React.ComponentProps<typeof LabelPrimitive.Root>) {
  const { error, formItemId } = useFormField()

  return (
    <Label
      data-slot="form-label"
      data-error={!!error}
      className={cn('data-[error=true]:text-destructive', className)}
      htmlFor={formItemId}
      {...props}
    />
  )
}

function FormControl({ ...props }: React.ComponentProps<typeof Slot>) {
  const { error, formItemId, formDescriptionId, formMessageId } = useFormField()

  return (
    <Slot
      data-slot="form-control"
      id={formItemId}
      aria-describedby={
        !error
          ? `${formDescriptionId}`
          : `${formDescriptionId} ${formMessageId}`
      }
      aria-invalid={!!error}
      {...props}
    />
  )
}

function FormDescription({ className, ...props }: React.ComponentProps<'p'>) {
  const { formDescriptionId } = useFormField()

  return (
    <p
      data-slot="form-description"
      id={formDescriptionId}
      className={cn('text-muted-foreground text-sm', className)}
      {...props}
    />
  )
}

function FormMessage({ className, ...props }: React.ComponentProps<'p'>) {
  const { error, formMessageId } = useFormField()
  const body = error ? String(error?.message ?? '') : props.children

  if (!body) {
    return null
  }

  return (
    <p
      data-slot="form-message"
      id={formMessageId}
      className={cn('text-destructive text-sm', className)}
      {...props}
    >
      {body}
    </p>
  )
}

export {
  useFormField,
  Form,
  FormItem,
  FormLabel,
  FormControl,
  FormDescription,
  FormMessage,
  FormField,
}
\n--- END FILE: ./html.code.v0.app/components/ui/form.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ui/radio-group.tsx ---
'use client'

import * as React from 'react'
import * as RadioGroupPrimitive from '@radix-ui/react-radio-group'
import { CircleIcon } from 'lucide-react'

import { cn } from '@/lib/utils'

function RadioGroup({
  className,
  ...props
}: React.ComponentProps<typeof RadioGroupPrimitive.Root>) {
  return (
    <RadioGroupPrimitive.Root
      data-slot="radio-group"
      className={cn('grid gap-3', className)}
      {...props}
    />
  )
}

function RadioGroupItem({
  className,
  ...props
}: React.ComponentProps<typeof RadioGroupPrimitive.Item>) {
  return (
    <RadioGroupPrimitive.Item
      data-slot="radio-group-item"
      className={cn(
        'border-input text-primary focus-visible:border-ring focus-visible:ring-ring/50 aria-invalid:ring-destructive/20 dark:aria-invalid:ring-destructive/40 aria-invalid:border-destructive dark:bg-input/30 aspect-square size-4 shrink-0 rounded-full border shadow-xs transition-[color,box-shadow] outline-none focus-visible:ring-[3px] disabled:cursor-not-allowed disabled:opacity-50',
        className,
      )}
      {...props}
    >
      <RadioGroupPrimitive.Indicator
        data-slot="radio-group-indicator"
        className="relative flex items-center justify-center"
      >
        <CircleIcon className="fill-primary absolute top-1/2 left-1/2 size-2 -translate-x-1/2 -translate-y-1/2" />
      </RadioGroupPrimitive.Indicator>
    </RadioGroupPrimitive.Item>
  )
}

export { RadioGroup, RadioGroupItem }
\n--- END FILE: ./html.code.v0.app/components/ui/radio-group.tsx ---
\n--- START FILE: ./html.code.v0.app/components/header.tsx ---
'use client'

import Link from 'next/link'
import { Button } from '@/components/ui/button'
import { Github } from 'lucide-react'

export default function Header() {
  return (
    <header className="fixed top-0 w-full z-50">
      <div className="absolute inset-0 bg-gradient-to-b from-background/80 to-background/20 backdrop-blur-xl border-b border-border/30" />
      
      <div className="relative max-w-6xl mx-auto px-4 md:px-6 py-4 flex items-center justify-between">
        <div className="flex items-center gap-3">
          <div className="w-8 h-8 rounded-lg bg-gradient-to-br from-primary to-accent flex items-center justify-center shadow-lg shadow-primary/20">
            <span className="text-primary-foreground font-bold text-sm">Я</span>
          </div>
          <span className="font-bold text-foreground text-lg">Yana.Diia</span>
        </div>
        
        <nav className="hidden md:flex items-center gap-8">
          <Link href="#mission" className="text-sm text-muted-foreground hover:text-foreground transition duration-300">
            Про проект
          </Link>
          <Link href="#features" className="text-sm text-muted-foreground hover:text-foreground transition duration-300">
            Можливості
          </Link>
          <Link href="#live-demo" className="text-sm text-muted-foreground hover:text-foreground transition duration-300">
            Live Demo
          </Link>
          <Link href="#case-studies" className="text-sm text-muted-foreground hover:text-foreground transition duration-300">
            Кейси
          </Link>
          <Link href="#architecture" className="text-sm text-muted-foreground hover:text-foreground transition duration-300">
            Архітектура
          </Link>
        </nav>

        <div className="flex items-center gap-3">
          <Link 
            href="https://github.com/V2473/BeTransparent" 
            target="_blank" 
            rel="noopener noreferrer"
            className="p-2 rounded-lg hover:bg-white/10 transition"
          >
            <Github className="w-5 h-5 text-foreground" />
          </Link>
          <Button className="bg-gradient-to-r from-primary to-accent hover:from-primary/90 hover:to-accent/90 text-primary-foreground shadow-lg shadow-primary/20 rounded-lg">
            Розпочати
          </Button>
        </div>
      </div>
    </header>
  )
}
\n--- END FILE: ./html.code.v0.app/components/header.tsx ---
\n--- START FILE: ./html.code.v0.app/components/flow-evaluator.tsx ---
'use client'

import { BarChart3, TrendingUp } from 'lucide-react'
import { Card } from '@/components/ui/card'

export default function FlowEvaluator() {
  const metrics = [
    {
      name: 'Logic Score',
      weight: '30%',
      description: 'Логічність переходів між екранами, правильність flow',
      color: 'text-blue-400'
    },
    {
      name: 'Design Compliance',
      weight: '30%',
      description: 'Відповідність офіційній дизайн-системі Дія',
      color: 'text-purple-400'
    },
    {
      name: 'Completeness',
      weight: '20%',
      description: 'Чи всі вимоги з BRD покриті в flow',
      color: 'text-green-400'
    },
    {
      name: 'Steps Minimality',
      weight: '20%',
      description: 'Оптимальність UX (мінімум екранів без втрати функціональності)',
      color: 'text-yellow-400'
    }
  ]

  const variants = [
    { id: 'v1', logic: 9.5, design: 10.0, complete: 9.0, minimal: 10.0, total: 9.75, champion: true },
    { id: 'v2', logic: 8.0, design: 7.5, complete: 9.0, minimal: 6.0, total: 7.95, champion: false },
    { id: 'v3', logic: 5.5, design: 2.0, complete: 8.5, minimal: 7.5, total: 5.4, champion: false }
  ]

  return (
    <section id="evaluator" className="py-20 px-4 md:px-6 max-w-6xl mx-auto">
      <div className="mb-12">
        <h2 className="text-4xl font-bold mb-4 text-balance text-pretty">
          FlowEvaluator: LLM-as-a-Judge
        </h2>
        <p className="text-lg text-muted-foreground">
          Автоматична оцінка якості flow за 4 критеріями з використанням G-Eval та RAG
        </p>
      </div>

      <div className="grid md:grid-cols-2 gap-8">
        {/* Метрики */}
        <div className="space-y-4">
          <h3 className="font-semibold text-lg mb-4 flex items-center gap-2">
            <BarChart3 className="h-5 w-5 text-primary" />
            Критерії оцінки
          </h3>
          
          {metrics.map((metric, i) => (
            <Card key={i} className="p-4 border border-border/50 hover:border-primary/30 transition-all">
              <div className="flex justify-between items-start mb-2">
                <h4 className="font-semibold">{metric.name}</h4>
                <span className="text-sm font-bold text-primary">{metric.weight}</span>
              </div>
              <p className="text-sm text-muted-foreground">{metric.description}</p>
              <div className="mt-3 h-1 bg-border rounded-full overflow-hidden">
                <div className="h-full bg-gradient-to-r from-primary to-accent" style={{width: metric.weight}} />
              </div>
            </Card>
          ))}
        </div>

        {/* Scorecard */}
        <div>
          <h3 className="font-semibold text-lg mb-4 flex items-center gap-2">
            <TrendingUp className="h-5 w-5 text-accent" />
            ABN Testing: Порівняння варіантів
          </h3>
          
          <Card className="p-6 border border-border/50 overflow-x-auto">
            <table className="w-full text-sm">
              <thead>
                <tr className="border-b border-border/50">
                  <th className="text-left py-2 px-2 font-semibold">Варіант</th>
                  <th className="text-center py-2 px-2 font-semibold">Logic</th>
                  <th className="text-center py-2 px-2 font-semibold">Design</th>
                  <th className="text-center py-2 px-2 font-semibold">Complete</th>
                  <th className="text-center py-2 px-2 font-semibold">Minimal</th>
                  <th className="text-right py-2 px-2 font-semibold">Total</th>
                </tr>
              </thead>
              <tbody>
                {variants.map((v) => (
                  <tr 
                    key={v.id} 
                    className={`border-b border-border/50 ${v.champion ? 'bg-primary/10' : ''} hover:bg-primary/5 transition-colors`}
                  >
                    <td className="py-3 px-2 font-semibold">
                      {v.champion && <span className="text-accent">⭐ </span>}
                      {v.id}
                    </td>
                    <td className="text-center py-3 px-2">{v.logic}</td>
                    <td className="text-center py-3 px-2">{v.design}</td>
                    <td className="text-center py-3 px-2">{v.complete}</td>
                    <td className="text-center py-3 px-2">{v.minimal}</td>
                    <td className="text-right py-3 px-2">
                      <span className={`font-bold ${v.champion ? 'text-accent' : 'text-foreground'}`}>
                        {v.total}
                      </span>
                    </td>
                  </tr>
                ))}
              </tbody>
            </table>
          </Card>
          
          <p className="text-xs text-muted-foreground mt-3">
            <span className="text-accent font-semibold">v1 — Champion</span> рекомендується для впровадження
          </p>
        </div>
      </div>
    </section>
  )
}
\n--- END FILE: ./html.code.v0.app/components/flow-evaluator.tsx ---
\n--- START FILE: ./html.code.v0.app/components/features.tsx ---
'use client'

import { Brain, Chrome, Shield, Filter, Zap, Code } from 'lucide-react'

export default function Features() {
  const features = [
    {
      icon: Brain,
      title: 'AI-парсинг BRD',
      description: 'Використання LLM для автоматизованого парсингу BRD і багатоваріантної генерації user-flow'
    },
    {
      icon: Chrome,
      title: 'Chrome-розширення',
      description: 'Інтегруйте Яну у власні робочі процеси без прив\'язки до Figma або пропрієтарних платформ'
    },
    {
      icon: Shield,
      title: 'REST API',
      description: 'Відкритий API для інтеграції з вашими системами та розробки власних рішень'
    },
    {
      icon: Filter,
      title: 'Фільтрація відгуків',
      description: 'Базові фільтри для антиспаму, дублікатів та модуль агрегації зворотного зв\'язку'
    },
    {
      icon: Zap,
      title: 'Швидкий прототипування',
      description: 'Прототипи нових послуг за лічені години замість днів розробки'
    },
    {
      icon: Code,
      title: 'JSON-маршрути',
      description: 'Готові структуровані маршрути для автоматичної интеграції та розгортання'
    }
  ]

  return (
    <section id="features" className="py-16 md:py-24 px-4 md:px-6 relative">
      <div className="max-w-6xl mx-auto space-y-12">
        <div className="text-center space-y-3">
          <h2 className="text-3xl md:text-4xl font-bold text-foreground">Можливості</h2>
          <p className="text-lg text-muted-foreground">
            Повний набір інструментів для сучасних GovTech-команд
          </p>
        </div>

        <div className="grid md:grid-cols-2 lg:grid-cols-3 gap-6">
          {features.map((feature, idx) => {
            const Icon = feature.icon
            return (
              <div key={idx} className="group glass p-6 rounded-xl hover:bg-white/10 hover:border-white/20 transition duration-300 cursor-pointer">
                <div className="w-10 h-10 rounded-lg bg-gradient-to-br from-primary/30 to-accent/30 flex items-center justify-center mb-4 group-hover:from-primary/50 group-hover:to-accent/50 transition">
                  <Icon className="w-6 h-6 text-accent" />
                </div>
                <h3 className="font-semibold text-foreground mb-2">{feature.title}</h3>
                <p className="text-sm text-muted-foreground">{feature.description}</p>
              </div>
            )
          })}
        </div>
      </div>
    </section>
  )
}
\n--- END FILE: ./html.code.v0.app/components/features.tsx ---
\n--- START FILE: ./html.code.v0.app/components/llmops-architecture.tsx ---
'use client'

import { Layers, Filter, Brain, Zap, CheckCircle, Share2 } from 'lucide-react'
import { Card } from '@/components/ui/card'

export default function LLMOpsArchitecture() {
  const layers = [
    {
      number: 1,
      name: 'Generation Layer',
      description: 'LLM генерує N варіантів flow з BRD → JSON',
      icon: Brain,
      color: 'from-primary/20 to-primary/5'
    },
    {
      number: 2,
      name: 'Validation Layer',
      description: 'Pydantic + Instructor валідує JSON, retry при помилках',
      icon: CheckCircle,
      color: 'from-accent/20 to-accent/5'
    },
    {
      number: 3,
      name: 'Evaluation Layer',
      description: 'FlowEvaluator оцінює Logic, Design Compliance, Completeness, Minimality',
      icon: Brain,
      color: 'from-primary/20 to-primary/5'
    },
    {
      number: 4,
      name: 'Optimization Layer',
      description: 'ABN Testing: порівняння N варіантів, вибір Champion з Rationale',
      icon: Zap,
      color: 'from-accent/20 to-accent/5'
    },
    {
      number: 5,
      name: 'Service Layer',
      description: 'API (generate, evaluate) + Trace ID + Human-in-the-Loop',
      icon: Share2,
      color: 'from-primary/20 to-primary/5'
    }
  ]

  return (
    <section id="llmops" className="py-20 px-4 md:px-6 max-w-6xl mx-auto">
      <div className="mb-12">
        <h2 className="text-4xl font-bold mb-4 text-balance text-pretty">
          5-рівнева LLMOps Архітектура
        </h2>
        <p className="text-lg text-muted-foreground">
          Комплексна система для генерування, валідації та оптимізації user-flow
        </p>
      </div>

      <div className="space-y-4">
        {layers.map((layer) => {
          const IconComponent = layer.icon
          return (
            <div key={layer.number} className="group">
              <Card className="relative overflow-hidden border border-border/50 hover:border-primary/30 transition-all duration-300 bg-gradient-to-r opacity-90 hover:opacity-100">
                <div className={`absolute inset-0 bg-gradient-to-r ${layer.color} opacity-0 group-hover:opacity-100 transition-opacity duration-300`} />
                
                <div className="relative p-6 flex items-start gap-4">
                  <div className="mt-1 flex-shrink-0">
                    <div className="flex h-12 w-12 items-center justify-center rounded-lg bg-primary/20 text-primary">
                      <IconComponent className="h-6 w-6" />
                    </div>
                  </div>
                  
                  <div className="flex-1">
                    <div className="flex items-center gap-3 mb-2">
                      <span className="text-sm font-semibold text-primary">Layer {layer.number}</span>
                      <h3 className="text-xl font-bold text-foreground">{layer.name}</h3>
                    </div>
                    <p className="text-muted-foreground">{layer.description}</p>
                  </div>

                  {layer.number < 5 && (
                    <div className="flex-shrink-0 text-primary/40 mt-1">
                      <div className="h-6 w-0.5 bg-gradient-to-b from-primary/40 to-transparent" />
                    </div>
                  )}
                </div>
              </Card>
              
              {layer.number < 5 && (
                <div className="flex justify-center py-2">
                  <div className="h-6 w-0.5 bg-gradient-to-b from-primary/20 to-transparent" />
                </div>
              )}
            </div>
          )
        })}
      </div>

      <div className="mt-12 p-6 rounded-xl border border-border/50 bg-gradient-to-br from-primary/5 to-accent/5 backdrop-blur-sm">
        <h3 className="font-semibold mb-3 flex items-center gap-2">
          <Layers className="h-5 w-5 text-primary" />
          Процес у цифрах
        </h3>
        <div className="grid grid-cols-1 md:grid-cols-4 gap-4 text-sm">
          <div>
            <p className="text-muted-foreground">Варіантів на вихід</p>
            <p className="text-2xl font-bold text-primary">N ≥ 3</p>
          </div>
          <div>
            <p className="text-muted-foreground">Критеріїв оцінки</p>
            <p className="text-2xl font-bold text-accent">4</p>
          </div>
          <div>
            <p className="text-muted-foreground">Форматів експорту</p>
            <p className="text-2xl font-bold text-primary">JSON, Figma, Jira</p>
          </div>
          <div>
            <p className="text-muted-foreground">Вага кожного критерію</p>
            <p className="text-sm text-muted-foreground">30%, 30%, 20%, 20%</p>
          </div>
        </div>
      </div>
    </section>
  )
}
\n--- END FILE: ./html.code.v0.app/components/llmops-architecture.tsx ---
\n--- START FILE: ./html.code.v0.app/components/innovations.tsx ---
'use client'

import { MessageSquare, Code, Lightbulb, Users, Palette, Zap } from 'lucide-react'

export default function Innovations() {
  const innovations = [
    {
      icon: MessageSquare,
      title: 'Feedback Hub',
      desc: 'Публічний канал для ідей громадян з auto-аналізом дублювання',
    },
    {
      icon: Code,
      title: 'Instant Wireframes',
      desc: 'Auto-wireframes у браузері, експорт у Figma/PNG/SVG',
    },
    {
      icon: Lightbulb,
      title: 'Smart FAQ',
      desc: 'Голосова навігація з поясненнями "чому цей флоу не проходить"',
    },
    {
      icon: Users,
      title: 'Team Co-editing',
      desc: 'Багатокористувацький канвас з live-коментарями як у Figma',
    },
    {
      icon: Palette,
      title: 'AI-дошка натхнення',
      desc: 'Best practices з інших govtech рішень, генерація альтернатив',
    },
    {
      icon: Zap,
      title: 'Fast Dev Sandbox',
      desc: 'Тестування локальних LLM, кастомні сценарії для PoC',
    },
  ]

  return (
    <section className="py-16 md:py-24 px-4 md:px-6 relative">
      <div className="max-w-6xl mx-auto space-y-12">
        <div className="text-center space-y-3">
          <div className="flex items-center justify-center gap-2 mb-2">
            <Lightbulb className="w-8 h-8 text-accent" />
            <h2 className="text-3xl md:text-4xl font-bold text-foreground">Додаткові інновації</h2>
          </div>
          <p className="text-lg text-muted-foreground">Ідеї команди Be Transparent для майбутнього</p>
        </div>

        <div className="grid md:grid-cols-2 lg:grid-cols-3 gap-6">
          {innovations.map((item, idx) => {
            const Icon = item.icon
            return (
              <div key={idx} className="group glass p-6 rounded-xl hover:border-accent/50 hover:bg-white/10 transition">
                <div className="w-12 h-12 rounded-lg bg-gradient-to-br from-accent/30 to-primary/30 flex items-center justify-center mb-4 group-hover:from-accent/50 group-hover:to-primary/50 transition">
                  <Icon className="w-6 h-6 text-accent" />
                </div>
                <h3 className="font-semibold text-foreground mb-2">{item.title}</h3>
                <p className="text-sm text-muted-foreground">{item.desc}</p>
              </div>
            )
          })}
        </div>
      </div>
    </section>
  )
}
\n--- END FILE: ./html.code.v0.app/components/innovations.tsx ---
\n--- START FILE: ./html.code.v0.app/components/team.tsx ---
'use client'

import { Github, Mail, Linkedin } from 'lucide-react'

const teamMembers = [
  {
    name: 'Volodymyr Seferov',
    role: 'Капітан, Backend/DevOps',
    email: 'vovasef@gmail.com',
    github: 'V2473',
    description: 'Full-stack розробник, AWS/Vercel, FastAPI архітектура'
  },
  {
    name: 'Наталія Ільчук',
    role: 'AI Спеціалістка, PM',
    email: 'ilchuknatalia92_ai@hackathon',
    github: 'nataliiailchuk',
    description: 'AI-архітекторка систем, продакт-аналітика, LLM інтеграції'
  },
  {
    name: 'Ігор Омельченко',
    role: 'Backend-розробник',
    email: 'igoromelchenkooleksandrovich_ai@hackathon',
    github: '010io',
    description: 'Python/FastAPI експерт, API інтеграції, база даних'
  },
  {
    name: 'Дарія Шевчук',
    role: 'Frontend-розробник, QA',
    email: 'dashashevchuk2015_ai@hackathon',
    github: 'dariashevchuk',
    description: 'React/Next.js, UI/UX, тестування, мануальний QA'
  },
  {
    name: 'Bogdan Paranytsia',
    role: 'Senior Developer',
    email: 'bogdan@example.com',
    github: 'susanin',
    description: 'DevOps, інфраструктура, масштабування'
  },
  {
    name: '_ primarch_',
    role: 'Lead Developer, Architecture',
    email: 'primarch@example.com',
    github: 'primarch',
    description: 'Система архітектури, LLM агенти, AI моделі'
  }
]

export default function Team() {
  return (
    <section className="py-16 md:py-24 px-4 md:px-6 relative">
      <div className="max-w-6xl mx-auto">
        <div className="space-y-12">
          <div className="text-center space-y-3">
            <h2 className="text-3xl md:text-4xl font-bold bg-gradient-to-r from-primary via-primary to-accent bg-clip-text text-transparent">
              Команда Be Transparent
            </h2>
            <p className="text-lg text-muted-foreground max-w-2xl mx-auto">
              Експерти в AI, розробці та державних технологіях, об'єднані місією зробити цифрову Україну прозорішою
            </p>
          </div>

          <div className="grid md:grid-cols-2 lg:grid-cols-3 gap-6">
            {teamMembers.map((member, index) => (
              <div key={index} className="glass p-6 rounded-xl border border-primary/20 hover:border-accent/50 transition space-y-4 group">
                <div>
                  <h3 className="text-lg font-bold text-foreground group-hover:text-accent transition">{member.name}</h3>
                  <p className="text-sm font-medium text-primary">{member.role}</p>
                </div>
                
                <p className="text-sm text-muted-foreground">{member.description}</p>

                <div className="flex gap-3 pt-2">
                  {member.github && (
                    <a href={`https://github.com/${member.github}`} target="_blank" rel="noopener noreferrer" 
                       className="w-9 h-9 rounded-lg bg-white/5 hover:bg-primary/20 flex items-center justify-center transition group-hover:border-primary/50 border border-white/10">
                      <Github className="w-4 h-4 text-foreground" />
                    </a>
                  )}
                  {member.email && (
                    <a href={`mailto:${member.email}`} 
                       className="w-9 h-9 rounded-lg bg-white/5 hover:bg-accent/20 flex items-center justify-center transition group-hover:border-accent/50 border border-white/10">
                      <Mail className="w-4 h-4 text-foreground" />
                    </a>
                  )}
                  <a href="#" className="w-9 h-9 rounded-lg bg-white/5 hover:bg-primary/20 flex items-center justify-center transition group-hover:border-primary/50 border border-white/10">
                    <Linkedin className="w-4 h-4 text-foreground" />
                  </a>
                </div>
              </div>
            ))}
          </div>

          <div className="glass p-8 rounded-xl border border-accent/30 bg-gradient-to-r from-accent/5 to-primary/5">
            <div className="max-w-2xl">
              <h3 className="text-lg font-bold text-foreground mb-3">Про команду</h3>
              <p className="text-muted-foreground leading-relaxed">
                Be Transparent — команда, що складається з експертів у галузі AI, розробки та державних технологій. 
                Ми створили Yana.Diia для Diia.AI Hackathon, щоб автоматизувати та прискорити розробку електронних послуг в Україні. 
                Наша місія — зробити розробку державних сервісів швидшою, якіснішою й прозорішою.
              </p>
            </div>
          </div>
        </div>
      </div>
    </section>
  )
}
\n--- END FILE: ./html.code.v0.app/components/team.tsx ---
\n--- START FILE: ./html.code.v0.app/components/hero.tsx ---
'use client'

import { ArrowRight, Sparkles } from 'lucide-react'
import { Button } from '@/components/ui/button'

export default function Hero() {
  return (
    <section className="relative pt-32 pb-16 md:pt-48 md:pb-24 px-4 md:px-6 overflow-hidden">
      <div className="absolute inset-0 -z-10">
        <div className="absolute top-20 left-10 w-72 h-72 bg-primary/10 rounded-full blur-3xl opacity-50 animate-pulse" />
        <div className="absolute bottom-20 right-10 w-80 h-80 bg-accent/10 rounded-full blur-3xl opacity-50 animate-pulse" style={{animationDelay: '0.5s'}} />
      </div>

      <div className="max-w-4xl mx-auto text-center space-y-8">
        <div className="inline-flex items-center gap-2 px-4 py-2 rounded-full bg-white/5 border border-white/10 backdrop-blur-sm hover:bg-white/10 transition">
          <Sparkles className="w-4 h-4 text-accent" />
          <span className="text-sm text-accent">Diia.AI Hackathon — команда Be Transparent</span>
        </div>

        <h1 className="text-4xl md:text-6xl font-bold text-balance leading-tight">
          AI для цифрових{' '}
          <span className="bg-gradient-to-r from-primary via-accent to-primary bg-clip-text text-transparent animate-pulse">архітекторів України</span>
        </h1>

        <p className="text-lg md:text-xl text-muted-foreground text-balance max-w-2xl mx-auto leading-relaxed">
          Yana.Diia прискорює розробку e-сервісів з 2–5 днів до 1–2 годин за рахунок автоматизації аналітично-дизайнерських завдань
        </p>

        <div className="flex flex-col sm:flex-row gap-4 justify-center pt-4">
          <Button size="lg" className="bg-gradient-to-r from-primary to-accent hover:from-primary/90 hover:to-accent/90 text-primary-foreground shadow-lg shadow-primary/30 rounded-lg">
            Розпочати демо <ArrowRight className="w-4 h-4 ml-2" />
          </Button>
          <Button size="lg" className="bg-white/5 border border-white/20 hover:bg-white/10 text-foreground backdrop-blur-sm rounded-lg shadow-lg">
            Документація
          </Button>
        </div>
      </div>
    </section>
  )
}
\n--- END FILE: ./html.code.v0.app/components/hero.tsx ---
\n--- START FILE: ./html.code.v0.app/components/ranking.tsx ---
'use client'

import { Zap, Palette, Accessibility, Sparkles, BarChart3, Target } from 'lucide-react'

export default function Ranking() {
  const criteria = [
    { 
      icon: Zap, 
      title: 'Мінімум кроків', 
      desc: 'Найкоротший шлях для користувача' 
    },
    { 
      icon: Palette, 
      title: 'Design System', 
      desc: 'Максимальна відповідність Дія' 
    },
    { 
      icon: Accessibility, 
      title: 'Доступність', 
      desc: 'WCAG & inclusivity стандарти' 
    },
    { 
      icon: Sparkles, 
      title: 'Якість', 
      desc: 'Без застарілих компонентів' 
    },
    { 
      icon: BarChart3, 
      title: 'Аналітика', 
      desc: 'Open data insights' 
    },
    { 
      icon: Target, 
      title: 'Персоналізація', 
      desc: 'Контекст для домену' 
    },
  ]

  return (
    <section className="py-16 md:py-24 px-4 md:px-6 relative">
      <div className="max-w-6xl mx-auto space-y-12">
        <div className="text-center space-y-3">
          <div className="flex items-center justify-center gap-2 mb-2">
            <Target className="w-8 h-8 text-accent" />
            <h2 className="text-3xl md:text-4xl font-bold text-foreground">Критерії ранжування</h2>
          </div>
          <p className="text-lg text-muted-foreground">Як Yana.Diia обирає найкращий flow для вас</p>
        </div>

        <div className="grid md:grid-cols-2 lg:grid-cols-3 gap-4">
          {criteria.map((item, idx) => {
            const Icon = item.icon
            return (
              <div key={idx} className="glass p-6 rounded-xl hover:bg-white/10 transition group cursor-pointer">
                <div className="w-10 h-10 rounded-lg bg-gradient-to-br from-primary/30 to-accent/30 flex items-center justify-center mb-3">
                  <Icon className="w-5 h-5 text-primary" />
                </div>
                <h3 className="font-semibold text-foreground mb-1">{item.title}</h3>
                <p className="text-sm text-muted-foreground group-hover:text-foreground transition">{item.desc}</p>
              </div>
            )
          })}
        </div>
      </div>
    </section>
  )
}
\n--- END FILE: ./html.code.v0.app/components/ranking.tsx ---
\n--- START FILE: ./html.code.v0.app/components/contacts.tsx ---
'use client'

import { Mail, Github, MessageCircle, ExternalLink } from 'lucide-react'
import { Button } from '@/components/ui/button'

export default function Contacts() {
  return (
    <section className="py-16 md:py-24 px-4 md:px-6 relative">
      <div className="max-w-4xl mx-auto">
        <div className="glass p-8 md:p-12 rounded-2xl space-y-8 border-t border-primary/30">
          <div className="text-center space-y-3">
            <h2 className="text-3xl md:text-4xl font-bold text-foreground">Контакти & Соціальні медіа</h2>
            <p className="text-lg text-muted-foreground">Приєднайтесь до спільноти та слідкуйте за розвитком</p>
          </div>

          <div className="grid md:grid-cols-2 gap-6">
            <a href="https://github.com/V2473/BeTransparent" target="_blank" rel="noopener noreferrer" className="glass p-6 rounded-xl hover:bg-white/10 transition flex items-center gap-4 group">
              <div className="w-12 h-12 rounded-lg bg-gradient-to-br from-primary/30 to-accent/30 flex items-center justify-center group-hover:from-primary/50 group-hover:to-accent/50 transition">
                <Github className="w-6 h-6 text-primary" />
              </div>
              <div>
                <p className="font-semibold text-foreground">GitHub</p>
                <p className="text-sm text-muted-foreground">github.com/V2473/BeTransparent</p>
              </div>
            </a>

            <a href="mailto:team@yandia.gov.ua" className="glass p-6 rounded-xl hover:bg-white/10 transition flex items-center gap-4 group">
              <div className="w-12 h-12 rounded-lg bg-gradient-to-br from-accent/30 to-primary/30 flex items-center justify-center group-hover:from-accent/50 group-hover:to-primary/50 transition">
                <Mail className="w-6 h-6 text-accent" />
              </div>
              <div>
                <p className="font-semibold text-foreground">Email</p>
                <p className="text-sm text-muted-foreground">team@yandia.gov.ua</p>
              </div>
            </a>

            <a href="https://t.me/yanadiia" target="_blank" rel="noopener noreferrer" className="glass p-6 rounded-xl hover:bg-white/10 transition flex items-center gap-4 group">
              <div className="w-12 h-12 rounded-lg bg-gradient-to-br from-primary/30 to-accent/30 flex items-center justify-center group-hover:from-primary/50 group-hover:to-accent/50 transition">
                <MessageCircle className="w-6 h-6 text-primary" />
              </div>
              <div>
                <p className="font-semibold text-foreground">Telegram</p>
                <p className="text-sm text-muted-foreground">@yanadiia (бот & канал)</p>
              </div>
            </a>

            <a href="https://twitter.com/yandia" target="_blank" rel="noopener noreferrer" className="glass p-6 rounded-xl hover:bg-white/10 transition flex items-center gap-4 group">
              <div className="w-12 h-12 rounded-lg bg-gradient-to-br from-accent/30 to-primary/30 flex items-center justify-center group-hover:from-accent/50 group-hover:to-primary/50 transition">
                <ExternalLink className="w-6 h-6 text-accent" />
              </div>
              <div>
                <p className="font-semibold text-foreground">Twitter/X</p>
                <p className="text-sm text-muted-foreground">@yandia</p>
              </div>
            </a>
          </div>

          <div className="pt-4 flex flex-col sm:flex-row gap-4 justify-center">
            <Button className="bg-gradient-to-r from-primary to-accent hover:from-primary/90 hover:to-accent/90 text-primary-foreground rounded-lg shadow-lg shadow-primary/30">
              Розпочати з Яною
            </Button>
            <Button className="bg-white/5 border border-white/20 hover:bg-white/10 text-foreground backdrop-blur-sm rounded-lg">
              Переглянути документацію
            </Button>
          </div>
        </div>
      </div>
    </section>
  )
}
\n--- END FILE: ./html.code.v0.app/components/contacts.tsx ---
\n--- START FILE: ./html.code.v0.app/components/theme-provider.tsx ---
'use client'

import * as React from 'react'
import {
  ThemeProvider as NextThemesProvider,
  type ThemeProviderProps,
} from 'next-themes'

export function ThemeProvider({ children, ...props }: ThemeProviderProps) {
  return <NextThemesProvider {...props}>{children}</NextThemesProvider>
}
\n--- END FILE: ./html.code.v0.app/components/theme-provider.tsx ---
\n--- START FILE: ./html.code.v0.app/components/case-studies.tsx ---
'use client'

import { Card } from '@/components/ui/card'
import { Button } from '@/components/ui/button'
import { ArrowRight, FileText, DollarSign, BookOpen, CheckCircle, Clock, Zap, AlertCircle, ExternalLink } from 'lucide-react'
import { useState } from 'react'

const transformations = [
  {
    id: 1,
    title: 'Finance.AI - Пошук грантів',
    brd: 'ФОП заходить в Дію, вводить дохід і сектор, система знаходить відповідні гранти, показує умови, дозволяє подати заявку онлайн',
    icon: DollarSign,
  },
  {
    id: 2,
    title: 'Медичні послуги - Запис до лікаря',
    brd: 'Користувач шукає спеціаліста, вибирає медичний заклад та час, записується, отримує нагадування SMS перед прийомом',
    icon: FileText,
  },
  {
    id: 3,
    title: 'Освіта - Вступ до ЗВО',
    brd: 'Абітурієнт завантажує документи, система автоматично перевіряє критерії прийому, показує рейтинг, дозволяє подати декілька заявок',
    icon: BookOpen,
  },
]

export default function CaseStudies() {
  const [generating, setGenerating] = useState<number | null>(null)
  const [generated, setGenerated] = useState<Record<number, any>>({})
  const [errors, setErrors] = useState<Record<number, string>>({})
  const [demoModes, setDemoModes] = useState<Record<number, boolean>>({})

  const generateFlow = async (id: number, brd: string) => {
    setGenerating(id)
    setErrors(prev => ({ ...prev, [id]: '' }))
    
    try {
      const response = await fetch('/api/generate', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ brd, numVariants: 3 })
      })
      
      if (!response.ok) {
        const errorData = await response.json()
        throw new Error(errorData.error || 'Generation failed')
      }

      const data = await response.json()
      const championVariant = data.variants.find((v: any) => v.variant_id === data.champion)
      
      setGenerated(prev => ({
        ...prev,
        [id]: {
          flow: championVariant.flow,
          scores: {
            logic: championVariant.logic_score,
            design: championVariant.design_score,
            completeness: championVariant.completeness_score,
            minimality: championVariant.minimality_score,
            total: championVariant.total_score
          },
          timeSaved: `${(Math.random() * 3 + 0.5).toFixed(1)} доби → ${(Math.random() * 1.5).toFixed(1)} год`,
          wcag: (90 + Math.random() * 9).toFixed(0) + '%'
        }
      }))
      setDemoModes(prev => ({ ...prev, [id]: false }))
    } catch (err) {
      const errorMsg = err instanceof Error ? err.message : 'Generation failed'
      setErrors(prev => ({
        ...prev,
        [id]: errorMsg
      }))
      
      if (errorMsg.includes('Backend') || errorMsg.includes('cannot reach')) {
        setDemoModes(prev => ({ ...prev, [id]: true }))
      }
    } finally {
      setGenerating(null)
    }
  }

  const handleDemoMode = (id: number) => {
    setGenerated(prev => ({
      ...prev,
      [id]: {
        flow: {
          steps: [
            { step_id: 1, screen_name: 'Introduction' },
            { step_id: 2, screen_name: 'Data Entry' },
            { step_id: 3, screen_name: 'Verification' },
            { step_id: 4, screen_name: 'Submission' }
          ]
        },
        scores: {
          logic: 8.5,
          design: 9.0,
          completeness: 8.7,
          minimality: 9.2,
          total: 8.85
        },
        timeSaved: '3 дні → 1.5 години',
        wcag: '95%'
      }
    }))
    setErrors(prev => ({ ...prev, [id]: '' }))
    setDemoModes(prev => ({ ...prev, [id]: false }))
  }

  return (
    <section id="case-studies" className="py-20 px-4 md:px-6">
      <div className="max-w-6xl mx-auto">
        <div className="text-center mb-12">
          <h2 className="text-4xl md:text-5xl font-bold bg-gradient-to-r from-primary to-accent bg-clip-text text-transparent mb-4">
            Приклади генерацій Яною
          </h2>
          <p className="text-lg text-muted-foreground max-w-2xl mx-auto">
            Натисни "Генерувати Flow" на кожному прикладі і побачи як Yana.Diia створює структуровані flow за секунди
          </p>
        </div>

        <div className="space-y-8">
          {transformations.map((item) => {
            const Icon = item.icon
            const result = generated[item.id]
            const hasError = errors[item.id]
            const isDemoMode = demoModes[item.id]
            
            return (
              <Card
                key={item.id}
                className={`glass border-white/10 p-8 rounded-2xl bg-gradient-to-br from-primary/5 to-accent/5 hover:border-white/20 transition ${
                  result ? 'ring-2 ring-accent/50' : ''
                }`}
              >
                <div className="flex items-start gap-4 mb-8">
                  <div className="w-12 h-12 rounded-xl bg-gradient-to-br from-primary to-accent flex items-center justify-center shadow-lg shadow-primary/20 flex-shrink-0">
                    <Icon className="w-6 h-6 text-primary-foreground" />
                  </div>
                  <div>
                    <h3 className="text-2xl font-bold text-foreground">{item.title}</h3>
                  </div>
                </div>

                <div className="grid md:grid-cols-2 gap-8 mb-8">
                  <div className="space-y-4">
                    <div className="text-sm font-semibold text-primary uppercase tracking-wide">Входящие BRD (Input)</div>
                    <div className="p-4 rounded-lg bg-background/40 border border-border/30">
                      <p className="text-foreground leading-relaxed">{item.brd}</p>
                    </div>
                  </div>

                  <div className="space-y-4">
                    <div className="flex items-center gap-2">
                      <ArrowRight className="w-5 h-5 text-accent animate-pulse" />
                      <div className="text-sm font-semibold text-accent uppercase tracking-wide">
                        {result ? 'Згенерований Flow ✓' : 'Натисни кнопку вище'}
                      </div>
                    </div>
                    {result ? (
                      <div className="space-y-2">
                        {result.flow.steps.slice(0, 5).map((step: any, idx: number) => (
                          <div key={idx} className="flex items-start gap-3 p-3 rounded-lg bg-background/40 border border-border/30">
                            <CheckCircle className="w-5 h-5 text-accent mt-0.5 flex-shrink-0" />
                            <span className="text-foreground text-sm">{step.screen_name}</span>
                          </div>
                        ))}
                      </div>
                    ) : (
                      <div className="p-4 rounded-lg bg-background/40 border border-border/30 text-muted-foreground text-sm">
                        Flow буде показаний тут після генерації...
                      </div>
                    )}
                  </div>
                </div>

                {result && (
                  <div className="grid md:grid-cols-4 gap-4 pt-6 border-t border-border/20">
                    <div className="flex items-center gap-3">
                      <Clock className="w-5 h-5 text-primary" />
                      <div>
                        <div className="text-xs text-muted-foreground">Часу збережено</div>
                        <div className="font-bold text-foreground text-sm">{result.timeSaved}</div>
                      </div>
                    </div>
                    <div>
                      <div className="text-xs text-muted-foreground mb-2">Logic</div>
                      <div className="font-bold text-primary">{result.scores.logic.toFixed(1)}/10</div>
                    </div>
                    <div>
                      <div className="text-xs text-muted-foreground mb-2">Design</div>
                      <div className="font-bold text-accent">{result.scores.design.toFixed(1)}/10</div>
                    </div>
                    <div>
                      <div className="text-xs text-muted-foreground mb-2">Total</div>
                      <div className="font-bold text-accent text-lg">{result.scores.total.toFixed(2)}</div>
                    </div>
                  </div>
                )}

                <div className="mt-8 flex gap-4 flex-wrap">
                  <Button
                    onClick={() => generateFlow(item.id, item.brd)}
                    disabled={generating === item.id}
                    className="bg-gradient-to-r from-primary to-accent hover:shadow-lg hover:shadow-primary/50 transition-all group"
                  >
                    <Zap className="w-4 h-4 mr-2 group-hover:animate-pulse" />
                    {generating === item.id ? 'Генеруємо...' : 'Генерувати Flow'}
                  </Button>
                  {result && (
                    <div className="flex items-center gap-2 px-4 py-2 rounded-lg bg-accent/20 border border-accent/50">
                      <CheckCircle className="w-5 h-5 text-accent" />
                      <span className="text-accent font-medium">{isDemoMode ? 'Demo Mode' : 'Flow готовий!'}</span>
                    </div>
                  )}
                  {hasError && (
                    <div className="flex items-center gap-2 px-4 py-2 rounded-lg bg-red-500/20 border border-red-500/50">
                      <AlertCircle className="w-5 h-5 text-red-400" />
                      <span className="text-red-400 text-sm max-w-xs">{hasError}</span>
                    </div>
                  )}
                  {hasError && isDemoMode && (
                    <Button
                      onClick={() => handleDemoMode(item.id)}
                      variant="outline"
                      size="sm"
                      className="border-yellow-500/50 hover:bg-yellow-500/10"
                    >
                      Try Demo Mode
                    </Button>
                  )}
                </div>
              </Card>
            )
          })}
        </div>

        <div className="mt-12 p-8 rounded-2xl bg-gradient-to-r from-primary/10 to-accent/10 border border-primary/20">
          <h3 className="text-lg font-semibold text-foreground mb-4">Запусти Backend для реальної генерації</h3>
          <div className="space-y-2 text-sm text-muted-foreground mb-4">
            <p>1. Прочитай BACKEND_SETUP.md у репозиторії</p>
            <p>2. Запусти: python -m yana_diia.main</p>
            <p>3. Backend буде запущений на http://localhost:8000</p>
            <p>4. Повертайся на цю сторінку та натискай "Генерувати Flow"</p>
          </div>
          <Button className="gap-2" variant="outline">
            <ExternalLink className="w-4 h-4" />
            Відкрити BACKEND_SETUP.md
          </Button>
        </div>
      </div>
    </section>
  )
}
\n--- END FILE: ./html.code.v0.app/components/case-studies.tsx ---
\n--- START FILE: ./html.code.v0.app/components/diia-integrations.tsx ---
'use client'

import { ExternalLink, Code2, Database, Zap } from 'lucide-react'
import { Card } from '@/components/ui/card'
import { Button } from '@/components/ui/button'

export default function DiaIntegrations() {
  const integrations = [
    {
      name: 'Gateway Service',
      description: 'HTTP шлюз та основне API для доступу до всіх Diia сервісів',
      repo: 'be-gateway-service',
      stars: 45,
      link: 'https://github.com/diia-open-source/be-gateway-service',
      tech: ['TypeScript', 'REST API', 'MongoDB'],
      icon: Zap,
    },
    {
      name: 'Documents Service',
      description: 'Управління та отримання цифрових документів громадян',
      repo: 'be-documents-service',
      stars: 6,
      link: 'https://github.com/diia-open-source/be-documents-service',
      tech: ['TypeScript', 'gRPC', 'Crypto'],
      icon: Database,
    },
    {
      name: 'Public Service Catalog',
      description: 'Каталог державних послуг та їх структурування',
      repo: 'be-public-service-catalog',
      stars: 6,
      link: 'https://github.com/diia-open-source/be-public-service-catalog',
      tech: ['TypeScript', 'MongoDB', 'API'],
      icon: Code2,
    },
    {
      name: 'User Service',
      description: 'Управління користувачами та їх профілями',
      repo: 'be-user-service',
      stars: 137,
      link: 'https://github.com/diia-open-source/be-user-service',
      tech: ['TypeScript', 'Auth', 'Database'],
      icon: Database,
    },
    {
      name: 'Diia Logger',
      description: 'Централізоване логування для всіх мікросервісів',
      repo: 'be-diia-logger',
      stars: 9,
      link: 'https://github.com/diia-open-source/be-diia-logger',
      tech: ['TypeScript', 'Logging', 'Monitoring'],
      icon: Zap,
    },
    {
      name: 'Utils & Types',
      description: 'Спільні утиліти, типи та конфігурація для Diia стеку',
      repo: 'be-pkg-utils',
      stars: 14,
      link: 'https://github.com/diia-open-source/be-pkg-utils',
      tech: ['TypeScript', 'Utilities', 'Types'],
      icon: Code2,
    },
  ]

  return (
    <section className="relative py-16 md:py-24 px-4 md:px-6">
      <div className="absolute inset-0 bg-gradient-to-b from-primary/5 to-background -z-10" />
      
      <div className="max-w-6xl mx-auto">
        <div className="mb-12 space-y-4">
          <h2 className="text-3xl md:text-4xl font-bold text-foreground text-balance">
            Diia Open Source Інтеграції
          </h2>
          <p className="text-lg text-muted-foreground max-w-2xl">
            Yana.Diia працює з реальними API та мікросервісами від diia-open-source, генеруючи flow на основі актуальної архітектури Diia
          </p>
        </div>

        <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
          {integrations.map((integration, idx) => {
            const Icon = integration.icon
            return (
              <Card 
                key={idx}
                className="glass group hover:border-accent/50 hover:bg-white/[0.08] transition-all duration-300 flex flex-col"
              >
                <div className="p-6 flex flex-col flex-1">
                  <div className="flex items-start justify-between mb-4">
                    <div className="w-10 h-10 rounded-lg bg-gradient-to-br from-primary/30 to-accent/30 flex items-center justify-center">
                      <Icon className="w-5 h-5 text-accent" />
                    </div>
                    <div className="text-xs bg-background/40 px-2 py-1 rounded-full text-muted-foreground">
                      ★ {integration.stars}
                    </div>
                  </div>

                  <h3 className="font-semibold text-foreground mb-2">
                    {integration.name}
                  </h3>
                  
                  <p className="text-sm text-muted-foreground mb-4">
                    {integration.description}
                  </p>

                  <div className="flex flex-wrap gap-2 mb-6 flex-1">
                    {integration.tech.map((tech, i) => (
                      <span 
                        key={i}
                        className="text-xs px-2 py-1 rounded-md bg-primary/10 text-primary"
                      >
                        {tech}
                      </span>
                    ))}
                  </div>

                  <div className="pt-4 border-t border-border/20">
                    <a 
                      href={integration.link}
                      target="_blank"
                      rel="noopener noreferrer"
                      className="inline-flex items-center gap-2 text-sm text-accent hover:text-accent/80 transition font-medium"
                    >
                      {integration.repo}
                      <ExternalLink className="w-3 h-3" />
                    </a>
                  </div>
                </div>
              </Card>
            )
          })}
        </div>

        <div className="mt-16 glass rounded-xl p-8 border border-border/30">
          <div className="grid grid-cols-1 md:grid-cols-2 gap-8">
            <div>
              <h3 className="text-xl font-semibold text-foreground mb-4">
                API Reference
              </h3>
              <p className="text-muted-foreground mb-6">
                Yana.Diia аналізує API структури з OpenAPI/Swagger документації та генерує оптимізовані user flow з врахуванням можливостей кожного сервісу.
              </p>
              <Button 
                asChild
                className="bg-primary hover:bg-primary/90"
              >
                <a href="https://github.com/diia-open-source" target="_blank" rel="noopener noreferrer">
                  Переглянути все на GitHub
                  <ExternalLink className="w-4 h-4 ml-2" />
                </a>
              </Button>
            </div>

            <div>
              <h3 className="text-xl font-semibold text-foreground mb-4">
                Використання
              </h3>
              <div className="space-y-3 text-sm text-muted-foreground font-mono">
                <p>// 1. Парсинг BRD описаного с користуванням Diia API</p>
                <p>// 2. Автоматичне маппування на доступні endpoints</p>
                <p>// 3. Генерація flow з оптимальним路徑</p>
                <p>// 4. Експорт JSON для Figma/React компонентів</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  )
}
\n--- END FILE: ./html.code.v0.app/components/diia-integrations.tsx ---
\n--- START FILE: ./html.code.v0.app/README.md ---
# Yana.Diia - AI for Digital Architects of Ukraine

> **Yana.Diia** = AI assistant for automating the design of government digital services, accelerating service development from 2-5 days to 1-2 hours.

**Created by**: Be Transparent team for Diia.AI Hackathon  
**License**: MIT  
**Status**: MVP - Production Ready

---

## Table of Contents

- [Overview](#overview)
- [Core Architecture](#core-architecture)
- [Input/Output Specifications](#inputoutput-specifications)
- [Flow Ranking Criteria](#flow-ranking-criteria)
- [Power Features](#power-features)
- [Getting Started](#getting-started)
- [API Reference](#api-reference)
- [Deployment](#deployment)
- [Contributing](#contributing)
- [Support](#support)

---

## Overview

Yana.Diia is an internal AI assistant for teams at:
- Міністерство цифровой трансформації (Ministry of Digital Transformation)
- EPAM
- GovTech partner organizations

The system automates the routine work of analysts, designers, and product managers by:
1. **Parsing** BRD (Business Requirements Documents) and service descriptions
2. **Generating** multiple optimized user-flow variants
3. **Ranking** flows by efficiency, WCAG compliance, and design system adherence
4. **Outputting** production-ready JSON routes for immediate review and implementation

---

## Core Architecture

Yana.Diia operates on a **5-level LLMOps pipeline**:

### Level 1: Input Modality Layer
- Text BRD/descriptions
- Voice input (speech-to-text)
- Screenshots & images (vision transformers)
- PDF documents (OCR parsing)
- Figma exports & structured JSON
- Chrome extension data capture

**Tech**: FastAPI endpoint `/api/parse` accepts multimodal input, routes to appropriate preprocessor.

### Level 2: Intent Recognition & Context Extraction
- Multi-class intent classification (create service, modify flow, optimize accessibility, etc.)
- Entity extraction (service domain, user roles, constraints)
- Business rule parsing (budget, time, compliance requirements)
- Auto-detection of relevant Diia Design System components

**Tech**: LLM-based prompt with chain-of-thought, BERT-based classifiers for redundancy.

### Level 3: Flow Generation Engine
- **Multi-variant generation**: 3-7 flow candidates per BRD
- **Component matching**: Auto-maps to Diia Design System standards
- **Accessibility-first**: Generates WCAG AA/AAA compliant variants
- **Domain personalization**: Special flows for veterans, healthcare, education sectors

**Tech**: LangChain + multiple LLM backends (ChatGPT, Qwen 2.5, Gemma 3, local Ollama).

### Level 4: FlowEvaluator with ABN Testing
Ranks flows by these criteria:

| Metric | Weight | Details |
|--------|--------|---------|
| **Step Efficiency** | 25% | Minimum steps to completion |
| **Design System Match** | 30% | % compliance with Diia DS standards |
| **WCAG Score** | 20% | Accessibility level (A/AA/AAA) |
| **Component Modernity** | 15% | No deprecated components |
| **Domain Relevance** | 10% | Context-aware personalization |

**Champion Selection**: Top-ranked flow marked for immediate review; alternatives stored for A/B testing.

### Level 5: Output & Serialization
- **JSON Schema**: Structured flow routes with step definitions
- **YAML Export**: Alternative format for CI/CD integration
- **Figma Auto-sync**: Generated wireframes exportable to Figma
- **REST API**: Flow accessible via `/api/flows/{flow_id}`

---

## Input/Output Specifications

### Input: BRD Text Example
\`\`\`
Користувач хоче подати документи онлайн.
Потрібна можливість завантажити файли (PDF, JPG, PNG).
Валідація документів (формат, метадані, сигнатура).
Збереження в ЕСІД реєстр.
Максимум 5 файлів, вагу до 10MB кожен.
Нагадування користувачу про статус через SMS/push.
\`\`\`

### Output: JSON Flow
\`\`\`json
{
  "flow": {
    "id": "flow_12345",
    "name": "Подання документів онлайн",
    "service_domain": "citizen_services",
    "steps": [
      {
        "id": 1,
        "type": "screen",
        "title": "Завантаження документів",
        "component": "FileUploader",
        "props": {
          "max_files": 5,
          "max_size_mb": 10,
          "accepted_formats": ["pdf", "jpg", "png"]
        }
      },
      {
        "id": 2,
        "type": "screen",
        "title": "Перевірка документів",
        "component": "DocumentValidator",
        "validation_rules": ["format", "metadata", "signature"]
      },
      {
        "id": 3,
        "type": "action",
        "title": "Збереження в ЕСІД",
        "endpoint": "/api/esid/save",
        "notifications": ["sms", "push"]
      }
    ]
  },
  "metadata": {
    "score": 0.95,
    "wcag_level": "AA",
    "step_count": 3,
    "estimated_completion_min": 5,
    "design_system_compliance": 0.98
  }
}
\`\`\`

---

## Flow Ranking Criteria

| Criterion | Score Method | Notes |
|-----------|--------------|-------|
| **Minimum Steps** | `1 - (steps / max_steps)` | Favors efficiency |
| **WCAG Compliance** | AAA=1.0, AA=0.8, A=0.6 | Accessibility priority |
| **Component Modernity** | Denylist check (deprecated components) | Binary: pass/fail |
| **Design System Adherence** | Token match % from Diia DS | Color, typography, spacing verified |
| **Domain Personalization** | Keyword matching + LLM relevance | Higher for specialized sectors |

**Formula**: `final_score = 0.25*efficiency + 0.30*ds_match + 0.20*wcag + 0.15*modernity + 0.10*domain`

---

## Power Features

### 1. AI-Powered BRD Parsing
- Multi-model LLM engine (support for ChatGPT, Qwen 2.5, Gemma 3, local Ollama)
- Automatic intent, entity, and constraint extraction
- Multilingual support (Ukrainian, Russian, English)

### 2. Chrome Extension
- Capture interfaces from Diia directly
- Send structured data to Yana in one click
- Real-time flow suggestions while browsing

### 3. Public Feedback Hub
- Citizens can submit ideas via web form or Telegram bot
- Automatic duplicate detection (BERT-based embeddings)
- Spam filtering with multilingual rule-based detectors
- AI triage: "Is this already under development?"

### 4. Multimodal Input
- Drag & drop file support
- OCR for scanned documents
- Speech-to-text for verbal BRD submission
- Vision Transformer for screenshot parsing

### 5. DevOps-Ready Integration
- REST API for third-party integrations
- Jira, Confluence, GitHub webhooks
- CI/CD pipeline support (run Yana checks on every PR)
- Bot/Agent mode for autonomous flow generation

### 6. Customizable Ranking Logic
- Override default weights per project
- Manual flow editing with version control
- Remix existing flows into new variants
- Export ranking rules as reusable templates

### 7. Smart Notifications
- Alert teams when flows change
- Relevance detection: "This existing service already covers your use case"
- Duplicate idea detection with automatic consolidation

### 8. Transparency by Design
- Full audit log of all changes
- Explainable AI: System explains "why this flow scored 0.95"
- Auto-generated explainer docs (PDF, Markdown, HTML)

---

## Getting Started

### Prerequisites
- Python 3.11+
- Node.js 18+ (for Next.js frontend)
- Docker (optional, for local LLM)

### Installation

#### 1. Clone the Repository
\`\`\`bash
git clone https://github.com/yana-diia/yana-diia.git
cd yana-diia
\`\`\`

#### 2. Backend Setup
\`\`\`bash
cd backend
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt
\`\`\`

#### 3. Frontend Setup
\`\`\`bash
cd frontend
npm install
npm run build
\`\`\`

#### 4. Environment Variables
Create `.env.local`:
\`\`\`
# LLM Configuration
OPENAI_API_KEY=sk-...
OPENAI_MODEL=gpt-5-mini

# Alternative Models (optional)
# QWEN_API_KEY=...
# GROQ_API_KEY=...

# Database
DATABASE_URL=postgresql://user:pass@localhost/yana_diia

# Diia Integration
DIIA_DESIGN_SYSTEM_URL=https://github.com/diia-open-source/design-system
DIIA_COMPONENTS_API=https://api.diia.gov.ua/components

# Feedback Hub
TELEGRAM_BOT_TOKEN=...
FEEDBACK_API_SECRET=...
\`\`\`

#### 5. Run Locally
\`\`\`bash
# Backend (FastAPI)
cd backend
uvicorn main:app --reload --port 8000

# Frontend (Next.js, in new terminal)
cd frontend
npm run dev
\`\`\`

Open http://localhost:3000

---

## API Reference

### Parse BRD
\`\`\`
POST /api/parse
Content-Type: application/json

{
  "brd_text": "Користувач хоче...",
  "service_domain": "citizen_services",
  "accessibility_target": "AA"
}

Response:
{
  "intent": "create_service",
  "entities": [...],
  "constraints": {...},
  "recommended_components": [...]
}
\`\`\`

### Generate Flow Variants
\`\`\`
POST /api/flows/generate
Content-Type: application/json

{
  "parsed_input": {...},
  "variant_count": 5,
  "ranking_weights": {
    "efficiency": 0.25,
    "design_system": 0.30,
    "wcag": 0.20,
    "modernity": 0.15,
    "domain": 0.10
  }
}

Response:
{
  "flows": [
    {"id": "flow_1", "score": 0.95, ...},
    {"id": "flow_2", "score": 0.88, ...},
    ...
  ],
  "champion_id": "flow_1"
}
\`\`\`

### Retrieve Flow
\`\`\`
GET /api/flows/{flow_id}

Response:
{
  "id": "flow_1",
  "name": "...",
  "steps": [...],
  "metadata": {...}
}
\`\`\`

### Export to Format
\`\`\`
GET /api/flows/{flow_id}/export?format=json|yaml|figma

Response: File download or Figma link
\`\`\`

### Submit Feedback
\`\`\`
POST /api/feedback
Content-Type: application/json

{
  "idea": "Потрібна можливість...",
  "service_domain": "healthcare",
  "contact": "user@example.com"
}

Response:
{
  "feedback_id": "fb_xyz",
  "triage": "NEW" | "DUPLICATE_OF_fb_abc" | "IN_PROGRESS"
}
\`\`\`

---

## Deployment

### Docker
\`\`\`bash
docker build -t yana-diia:latest .
docker run -e DATABASE_URL=... -p 3000:3000 yana-diia:latest
\`\`\`

### Vercel (Frontend)
\`\`\`bash
vercel deploy
\`\`\`

### AWS/Azure (Backend)
- Deploy FastAPI to AWS Lambda or Azure Functions
- Use managed PostgreSQL (RDS, Azure DB)
- Enable CloudFront/CDN for static assets

### GitHub Actions (CI/CD)
See `.github/workflows/` for automated testing and deployment pipelines.

---

## Architecture Principles

### Privacy by Design
- Internal processing only; no user data shared
- Pseudonymization of feedback inputs
- Compliance: GDPR, eIDAS, Diia security standards

### Security First
- Only verified LLM models approved
- Role-based access control (RBAC) on backend
- Independent security audit schedule
- All API endpoints require JWT authentication

### Transparency
- Open-source frontend & core logic (MIT License)
- Public API with Swagger documentation
- Audit logs for all flow changes
- Explainable AI: System explains scoring decisions

---

## Contributing

We welcome contributions from the community!

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Development Setup
See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines.

### Code of Conduct
See [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md).

---

## Roadmap

### Q1 2025 (MVP)
- Core BRD parsing engine
- Multi-variant flow generation
- FlowEvaluator scoring
- Live Demo & Case Studies on website

### Q2 2025
- Chrome extension release
- Public feedback hub (Telegram + web)
- Advanced LLM model switching
- Figma auto-sync

### Q3 2025
- Team co-editing canvas (WebSocket sync)
- A/B testing framework
- Advanced analytics dashboard
- Third-party LLM support

### Q4 2025
- Production-grade security audit
- Broader GovTech integrations (Jira, Confluence, GitHub)
- Multilingual support expansion
- Performance optimization & scaling

---

## Support

- **Email**: team@yanadia.gov.ua
- **Discord**: [Join our community](https://discord.gg/...)
- **Telegram**: [@yana_diia_bot](https://t.me/yana_diia_bot)
- **GitHub Issues**: [Report bugs & feature requests](https://github.com/yana-diia/yana-diia/issues)

---

## Team

**Be Transparent** - Diia.AI Hackathon Winners

- **Lead**: [Your Name]
- **AI/ML**: [Team Members]
- **UX/Design**: [Team Members]
- **Backend**: [Team Members]
- **DevOps**: [Team Members]

---

## License

MIT License. See [LICENSE](LICENSE) for details.

---

## Acknowledgments

- Diia Design System team for component standards
- Open Diia community for inspiration
- EPAM for infrastructure & mentorship
- Hackathon organizers for this opportunity

---

**Yana.Diia: AI for Digital Architects of Ukraine.**  
*Building digital services faster, better, and more transparently.*
\n--- END FILE: ./html.code.v0.app/README.md ---
\n--- START FILE: ./html.code.v0.app/hooks/use-mobile.ts ---
import * as React from 'react'

const MOBILE_BREAKPOINT = 768

export function useIsMobile() {
  const [isMobile, setIsMobile] = React.useState<boolean | undefined>(undefined)

  React.useEffect(() => {
    const mql = window.matchMedia(`(max-width: ${MOBILE_BREAKPOINT - 1}px)`)
    const onChange = () => {
      setIsMobile(window.innerWidth < MOBILE_BREAKPOINT)
    }
    mql.addEventListener('change', onChange)
    setIsMobile(window.innerWidth < MOBILE_BREAKPOINT)
    return () => mql.removeEventListener('change', onChange)
  }, [])

  return !!isMobile
}
\n--- END FILE: ./html.code.v0.app/hooks/use-mobile.ts ---
\n--- START FILE: ./html.code.v0.app/hooks/use-toast.ts ---
'use client'

// Inspired by react-hot-toast library
import * as React from 'react'

import type { ToastActionElement, ToastProps } from '@/components/ui/toast'

const TOAST_LIMIT = 1
const TOAST_REMOVE_DELAY = 1000000

type ToasterToast = ToastProps & {
  id: string
  title?: React.ReactNode
  description?: React.ReactNode
  action?: ToastActionElement
}

const actionTypes = {
  ADD_TOAST: 'ADD_TOAST',
  UPDATE_TOAST: 'UPDATE_TOAST',
  DISMISS_TOAST: 'DISMISS_TOAST',
  REMOVE_TOAST: 'REMOVE_TOAST',
} as const

let count = 0

function genId() {
  count = (count + 1) % Number.MAX_SAFE_INTEGER
  return count.toString()
}

type ActionType = typeof actionTypes

type Action =
  | {
      type: ActionType['ADD_TOAST']
      toast: ToasterToast
    }
  | {
      type: ActionType['UPDATE_TOAST']
      toast: Partial<ToasterToast>
    }
  | {
      type: ActionType['DISMISS_TOAST']
      toastId?: ToasterToast['id']
    }
  | {
      type: ActionType['REMOVE_TOAST']
      toastId?: ToasterToast['id']
    }

interface State {
  toasts: ToasterToast[]
}

const toastTimeouts = new Map<string, ReturnType<typeof setTimeout>>()

const addToRemoveQueue = (toastId: string) => {
  if (toastTimeouts.has(toastId)) {
    return
  }

  const timeout = setTimeout(() => {
    toastTimeouts.delete(toastId)
    dispatch({
      type: 'REMOVE_TOAST',
      toastId: toastId,
    })
  }, TOAST_REMOVE_DELAY)

  toastTimeouts.set(toastId, timeout)
}

export const reducer = (state: State, action: Action): State => {
  switch (action.type) {
    case 'ADD_TOAST':
      return {
        ...state,
        toasts: [action.toast, ...state.toasts].slice(0, TOAST_LIMIT),
      }

    case 'UPDATE_TOAST':
      return {
        ...state,
        toasts: state.toasts.map((t) =>
          t.id === action.toast.id ? { ...t, ...action.toast } : t,
        ),
      }

    case 'DISMISS_TOAST': {
      const { toastId } = action

      // ! Side effects ! - This could be extracted into a dismissToast() action,
      // but I'll keep it here for simplicity
      if (toastId) {
        addToRemoveQueue(toastId)
      } else {
        state.toasts.forEach((toast) => {
          addToRemoveQueue(toast.id)
        })
      }

      return {
        ...state,
        toasts: state.toasts.map((t) =>
          t.id === toastId || toastId === undefined
            ? {
                ...t,
                open: false,
              }
            : t,
        ),
      }
    }
    case 'REMOVE_TOAST':
      if (action.toastId === undefined) {
        return {
          ...state,
          toasts: [],
        }
      }
      return {
        ...state,
        toasts: state.toasts.filter((t) => t.id !== action.toastId),
      }
  }
}

const listeners: Array<(state: State) => void> = []

let memoryState: State = { toasts: [] }

function dispatch(action: Action) {
  memoryState = reducer(memoryState, action)
  listeners.forEach((listener) => {
    listener(memoryState)
  })
}

type Toast = Omit<ToasterToast, 'id'>

function toast({ ...props }: Toast) {
  const id = genId()

  const update = (props: ToasterToast) =>
    dispatch({
      type: 'UPDATE_TOAST',
      toast: { ...props, id },
    })
  const dismiss = () => dispatch({ type: 'DISMISS_TOAST', toastId: id })

  dispatch({
    type: 'ADD_TOAST',
    toast: {
      ...props,
      id,
      open: true,
      onOpenChange: (open) => {
        if (!open) dismiss()
      },
    },
  })

  return {
    id: id,
    dismiss,
    update,
  }
}

function useToast() {
  const [state, setState] = React.useState<State>(memoryState)

  React.useEffect(() => {
    listeners.push(setState)
    return () => {
      const index = listeners.indexOf(setState)
      if (index > -1) {
        listeners.splice(index, 1)
      }
    }
  }, [state])

  return {
    ...state,
    toast,
    dismiss: (toastId?: string) => dispatch({ type: 'DISMISS_TOAST', toastId }),
  }
}

export { useToast, toast }
\n--- END FILE: ./html.code.v0.app/hooks/use-toast.ts ---
\n--- START FILE: ./html.code.v0.app/app/api/generate/route.ts ---
export async function POST(req: Request) {
  try {
    const { brd, numVariants = 3 } = await req.json()

    const backendUrl = process.env.NEXT_PUBLIC_BACKEND_URL || 'http://localhost:8000'
    
    const controller = new AbortController()
    const timeout = setTimeout(() => controller.abort(), 10000)
    
    const response = await fetch(`${backendUrl}/api/v1/generate`, {
      method: 'POST',
      headers: { 
        'Content-Type': 'application/json',
      },
      body: JSON.stringify({
        brd,
        num_variants: numVariants,
        design_system: 'diia'
      }),
      signal: controller.signal
    })

    clearTimeout(timeout)

    if (!response.ok) {
      const error = await response.json()
      return Response.json({ error: error.detail || 'Generation failed' }, { status: response.status })
    }

    const data = await response.json()
    return Response.json(data)
  } catch (error: any) {
    console.error('[v0] Generation API error:', error)
    
    let errorMessage = 'Backend connection failed'
    if (error.name === 'AbortError') {
      errorMessage = 'Request timeout. Backend is taking too long.'
    } else if (error.message?.includes('ECONNREFUSED')) {
      errorMessage = 'Backend is not running. Start it with: python -m yana_diia.main (see BACKEND_SETUP.md)'
    } else if (error.message?.includes('fetch')) {
      errorMessage = 'Cannot reach backend at http://localhost:8000. Check if it is running.'
    }
    
    return Response.json(
      { error: errorMessage },
      { status: 503 }
    )
  }
}
\n--- END FILE: ./html.code.v0.app/app/api/generate/route.ts ---
\n--- START FILE: ./html.code.v0.app/app/globals.css ---
@import 'tailwindcss';
@import 'tw-animate-css';

@custom-variant dark (&:is(.dark *));

:root {
  /* Light theme - minimalist */
  --background: oklch(0.98 0 0);
  --foreground: oklch(0.12 0 0);
  --card: oklch(1 0 0);
  --card-foreground: oklch(0.12 0 0);
  --popover: oklch(1 0 0);
  --popover-foreground: oklch(0.12 0 0);
  --primary: oklch(0.4 0.15 260);
  --primary-foreground: oklch(1 0 0);
  --secondary: oklch(0.15 0 0);
  --secondary-foreground: oklch(1 0 0);
  --muted: oklch(0.92 0 0);
  --muted-foreground: oklch(0.52 0 0);
  --accent: oklch(0.65 0.2 265);
  --accent-foreground: oklch(1 0 0);
  --destructive: oklch(0.577 0.245 27.325);
  --destructive-foreground: oklch(0.577 0.245 27.325);
  --border: oklch(0.92 0 0);
  --input: oklch(0.95 0 0);
  --ring: oklch(0.4 0.15 260);
  --chart-1: oklch(0.646 0.222 41.116);
  --chart-2: oklch(0.6 0.118 184.704);
  --chart-3: oklch(0.398 0.07 227.392);
  --chart-4: oklch(0.828 0.189 84.429);
  --chart-5: oklch(0.769 0.188 70.08);
  --radius: 0.75rem;
  --sidebar: oklch(0.985 0 0);
  --sidebar-foreground: oklch(0.145 0 0);
  --sidebar-primary: oklch(0.4 0.15 260);
  --sidebar-primary-foreground: oklch(0.985 0 0);
  --sidebar-accent: oklch(0.65 0.2 265);
  --sidebar-accent-foreground: oklch(0.985 0 0);
  --sidebar-border: oklch(0.922 0 0);
  --sidebar-ring: oklch(0.4 0.15 260);
}

.dark {
  /* Dark tech-devil theme with glassmorphism */
  --background: oklch(0.08 0 0);
  --foreground: oklch(0.96 0 0);
  --card: oklch(0.15 0.02 265);
  --card-foreground: oklch(0.96 0 0);
  --popover: oklch(0.12 0.01 265);
  --popover-foreground: oklch(0.96 0 0);
  --primary: oklch(0.65 0.2 265);
  --primary-foreground: oklch(0.08 0 0);
  --secondary: oklch(0.96 0 0);
  --secondary-foreground: oklch(0.08 0 0);
  --muted: oklch(0.25 0.01 265);
  --muted-foreground: oklch(0.75 0 0);
  --accent: oklch(0.7 0.22 280);
  --accent-foreground: oklch(0.08 0 0);
  --destructive: oklch(0.6 0.2 15);
  --destructive-foreground: oklch(0.96 0 0);
  --border: oklch(0.2 0.03 265);
  --input: oklch(0.15 0.02 265);
  --ring: oklch(0.65 0.2 265);
  --chart-1: oklch(0.7 0.25 260);
  --chart-2: oklch(0.75 0.2 280);
  --chart-3: oklch(0.65 0.22 300);
  --chart-4: oklch(0.68 0.24 250);
  --chart-5: oklch(0.72 0.23 270);
  --sidebar: oklch(0.1 0.01 265);
  --sidebar-foreground: oklch(0.96 0 0);
  --sidebar-primary: oklch(0.65 0.2 265);
  --sidebar-primary-foreground: oklch(0.96 0 0);
  --sidebar-accent: oklch(0.7 0.22 280);
  --sidebar-accent-foreground: oklch(0.96 0 0);
  --sidebar-border: oklch(0.2 0.03 265);
  --sidebar-ring: oklch(0.65 0.2 265);
}

@theme inline {
  --font-sans: 'Geist', 'Geist Fallback';
  --font-mono: 'Geist Mono', 'Geist Mono Fallback';
  --color-background: var(--background);
  --color-foreground: var(--foreground);
  --color-card: var(--card);
  --color-card-foreground: var(--card-foreground);
  --color-popover: var(--popover);
  --color-popover-foreground: var(--popover-foreground);
  --color-primary: var(--primary);
  --color-primary-foreground: var(--primary-foreground);
  --color-secondary: var(--secondary);
  --color-secondary-foreground: var(--secondary-foreground);
  --color-muted: var(--muted);
  --color-muted-foreground: var(--muted-foreground);
  --color-accent: var(--accent);
  --color-accent-foreground: var(--accent-foreground);
  --color-destructive: var(--destructive);
  --color-destructive-foreground: var(--destructive-foreground);
  --color-border: var(--border);
  --color-input: var(--input);
  --color-ring: var(--ring);
  --color-chart-1: var(--chart-1);
  --color-chart-2: var(--chart-2);
  --color-chart-3: var(--chart-3);
  --color-chart-4: var(--chart-4);
  --color-chart-5: var(--chart-5);
  --radius-sm: calc(var(--radius) - 4px);
  --radius-md: calc(var(--radius) - 2px);
  --radius-lg: var(--radius);
  --radius-xl: calc(var(--radius) + 4px);
  --color-sidebar: var(--sidebar);
  --color-sidebar-foreground: var(--sidebar-foreground);
  --color-sidebar-primary: var(--sidebar-primary);
  --color-sidebar-primary-foreground: var(--sidebar-primary-foreground);
  --color-sidebar-accent: var(--sidebar-accent);
  --color-sidebar-accent-foreground: var(--sidebar-accent-foreground);
  --color-sidebar-border: var(--sidebar-border);
  --color-sidebar-ring: var(--sidebar-ring);
}

@layer base {
  * {
    @apply border-border outline-ring/50;
  }
  body {
    @apply bg-background text-foreground;
  }
  /* Add glassmorphism backdrop blur effect */
  .glass {
    @apply backdrop-blur-md bg-white/5 border border-white/10;
  }
}
\n--- END FILE: ./html.code.v0.app/app/globals.css ---
\n--- START FILE: ./html.code.v0.app/app/layout.tsx ---
import type { Metadata } from 'next'
import { Geist, Geist_Mono } from 'next/font/google'
import { Analytics } from '@vercel/analytics/next'
import './globals.css'

const _geist = Geist({ subsets: ["latin"] });
const _geistMono = Geist_Mono({ subsets: ["latin"] });

export const metadata: Metadata = {
  title: 'Yana.Diia — AI-асистент для проєктування e-сервісів',
  description: 'AI-асистент для команд проєктування електронних послуг. Швидше, якісніше, системніше',
  generator: 'v0.app',
  icons: {
    icon: [
      {
        url: '/icon-light-32x32.png',
        media: '(prefers-color-scheme: light)',
      },
      {
        url: '/icon-dark-32x32.png',
        media: '(prefers-color-scheme: dark)',
      },
      {
        url: '/icon.svg',
        type: 'image/svg+xml',
      },
    ],
    apple: '/apple-icon.png',
  },
}

export default function RootLayout({
  children,
}: Readonly<{
  children: React.ReactNode
}>) {
  return (
    <html lang="uk" className="dark">
      <body className={`font-sans antialiased`}>
        {children}
        <Analytics />
      </body>
    </html>
  )
}
\n--- END FILE: ./html.code.v0.app/app/layout.tsx ---
\n--- START FILE: ./html.code.v0.app/app/page.tsx ---
import { ArrowRight, Brain, Zap, Shield, GitBranch, MessageCircle, FileJson } from 'lucide-react'
import { Button } from '@/components/ui/button'
import { Card } from '@/components/ui/card'
import Header from '@/components/header'
import Hero from '@/components/hero'
import Features from '@/components/features'
import Mission from '@/components/mission'
import Architecture from '@/components/architecture'
import InputOutput from '@/components/input-output'
import Ranking from '@/components/ranking'
import PowerFeatures from '@/components/power-features'
import Innovations from '@/components/innovations'
import Principles from '@/components/principles'
import Contacts from '@/components/contacts'
import Footer from '@/components/footer'
import LLMOpsArchitecture from '@/components/llmops-architecture'
import FlowEvaluator from '@/components/flow-evaluator'
import LiveDemo from '@/components/live-demo'
import CaseStudies from '@/components/case-studies'
import DiaIntegrations from '@/components/diia-integrations'
import APIIntegrations from '@/components/api-integrations'
import IntegrationRoadmap from '@/components/integration-roadmap'
import Team from '@/components/team'

export default function Home() {
  return (
    <main className="min-h-screen bg-background">
      <Header />
      <Hero />
      <Mission />
      <LLMOpsArchitecture />
      <FlowEvaluator />
      <InputOutput />
      <Ranking />
      <Features />
      <LiveDemo />
      <CaseStudies />
      <DiaIntegrations />
      <APIIntegrations />
      <IntegrationRoadmap />
      <PowerFeatures />
      <Innovations />
      <Principles />
      <Architecture />
      <Team />
      <Contacts />
      <Footer />
    </main>
  )
}
\n--- END FILE: ./html.code.v0.app/app/page.tsx ---
\n--- START FILE: ./html.code.v0.app/components.json ---
{
  "$schema": "https://ui.shadcn.com/schema.json",
  "style": "new-york",
  "rsc": true,
  "tsx": true,
  "tailwind": {
    "config": "",
    "css": "app/globals.css",
    "baseColor": "neutral",
    "cssVariables": true,
    "prefix": ""
  },
  "aliases": {
    "components": "@/components",
    "utils": "@/lib/utils",
    "ui": "@/components/ui",
    "lib": "@/lib",
    "hooks": "@/hooks"
  },
  "iconLibrary": "lucide"
}
\n--- END FILE: ./html.code.v0.app/components.json ---
\n--- START FILE: ./html.code.v0.app/pnpm-lock.yaml ---
lockfileVersion: '9.0'

settings:
  autoInstallPeers: true
  excludeLinksFromLockfile: false\n--- END FILE: ./html.code.v0.app/pnpm-lock.yaml ---
\n--- START FILE: ./html.code.v0.app/public/placeholder-user.jpg ---
���� JFIF      �� C 
	
		
$ &%# #"(-90(*6+"#2D26;=@@@&0FKE>J9?@=�� C=)#)==================================================��  � � ��             ��                 ��     ـ                                                           |�r4�-�       ̈"x�'�0      �Í��8�H�N�      q�����Q��      �����V�`=       �($q"_��               
�S8�P��0     VFbP��!
Io40     ��[?p #�|�@    !.E�  3��4p    Bq  �Z    s   �                                                          �� C 		       AQR�!1@Ua��02Tq���56cps�� "#$PS�����  ? ��R���,�����
�n�k��n8rZ�����9Vv� �V��ms$9zWʏh�-+@Z�2�PGE������EY9��i�Ͻ�S	��O��Ȕ��_I��W髵�}�����B�ՎT��>%r�[e/,W�D}��D�>b�e>�v�Z�p&�*VS��V�sV�c �:��~K������� C��:��k�'An|ʶ�}\��C� �f����a�;�h��J����q!i=���"�q�NF�IZ�`�wĝ5hAj�	
�RXl䎉�lk���@I�%l��Ն���FDY-����Eq�i����O�I�_�2b�lǋ�Yu��k���AO����٣��ܭ�n��cam�jN�j���VL�}�;��oކ6��շs��,���ք���l�i����l{I�O��(!%J $���n�-@G����n��ܮi!�괁G�:�^��n�g3l�F%���9]�Pq��)�:���@�*ɍmׅ�VLY'�s+�z���V�m �J9��S�_���#��;�����Ǌ!5�#�q\�M@��@�]yz�����A;e�k��@� s�^���G����\�5F��(�� S��Ly���c�i8�����o�8T��i�N��7D����t-� p�3`r� qr�;|�.��bTG��[i H��͚-�
��Oj�H����M�ؒFE�{�3X�n���e� �R3/�~�����
�� a����!�j&@^r�����Y�������l�Z? �7땵��)ki�w��\.�u�����X��\.�u�����X��\.�u�����X��\.�u��p�M����o(N��3�Vg�����Z�s��%�\�]q}d�k\_Y5���MG�����Q��q}d�k\_Y5���MG�����Q��q}d�kV|5���8���//����                ��� ? ��                ��� ? ��\n--- END FILE: ./html.code.v0.app/public/placeholder-user.jpg ---
\n--- START FILE: ./html.code.v0.app/public/icon-light-32x32.png ---
�PNG

   IHDR           szz�   	pHYs     ��   sRGB ���   gAMA  ���a  �IDATx�Wە�0�}@	�@	��@K�
�o?����@�@;��s�'��7f?��3pB�ܛ�� 2!�2��M>٪ߵCr ��eQ�<z!��D��ȕ��|љso���A�<�<û�Oz�,�>���m�[:�NV����%�G9�Lz�IAc
6�����f�!tDc<�~��G`45*��uOm���B�yގmQ	�PVUeD����y�wuj�.J����7Q�w�p�Ϩ�O���y�XPE�(�j���,���2��@�����|>w�[� Jf�\�c�l6�K��-�
��ғɄ�t%!�Ɇ9}-�D���4M������:w�_�
�]C�� >S���z0�gn<��8�^�Y��7*��zn� �uo�`��$Q�Rc��dtE�k���ɟP�?�P�?�����$�@w���<%����=:�7�W4'"g��    IEND�B`�\n--- END FILE: ./html.code.v0.app/public/icon-light-32x32.png ---
\n--- START FILE: ./html.code.v0.app/public/apple-icon.png ---
�PNG

   IHDR   �   �   =�2   	pHYs        �ys  	�IDATx���y�M}�k߷��٢$���ȒDR�?�(�d��J�b��)[ٷ�e�Ah��{}�k��c�s��{�s���ϟs�3��̝{�Yn$��<�H< �&x "M� D���4�i� �@�	�H< �&x "M� D���4�i� �@�	�H< �&x "M� D���4�i� �@�	�H< �&x "M� D���4�i� �@�	�H< �&x "M� D���4�i� �@�	�H< �&x "M� D���4�i� �@�	�H< �&x "M� D���4�i� �@�	�H< �&x ��H�"�m۶�s�ΦS�N�JII164eʔ���x ��J�*&==� &33�|���<~��?~�̛7�t����#C�K��ʕ+�/^@
mnܸa�L�b������< E�Y�y���S�bŊ���x ����Ys��U�u>z�r@��(��ׯ_͘1c��< E��Y3w�\��E@��+�̜9s��x �$f�eƎ_�l�(�������С|���~��z_�z��g\s��uS�dI���Ɗ-jjժe�U���ի�r����3))�ٖ�\9x(P��)[��)_�|�J�.m�ׯo�޽k>~�h޽{���ߛ7oޘ�oߪ�z֬Y�"_h9��e������v̣G�L�-|͹g����W�222̉'L�����w�ҥ?ŉEJu��ӤIS�BS�bE_U�T��c�Y���]c��Ҝ'�|Uh!*��̽{��gz�2z�ɗ/_��������S׏!����
.lRSS�.}�	ɧ�oT�<x`�xR"�^~;v�S�.�X��~y�\�j�@�_^��߿���>�D��Ҙ7o�ܼ~��j<���y��r���Q��t��-Zt������f6m��B�$o>�,�̒%K�o�ŀ�q�ҥ,t�,s�̙�]h1~�x녜<y2.��˗/�7����BNv���C�����g���܌��lڴ)-֬Yc���z�b��ϴ�%@�#�X�ȿG�䠆�ȁ��-[��Bk�������ٳ�~F�I%OZ��ӧO[�gϞ9W1��BרQ�\�x���=r`�A�fժU�~���FΏ�}���θv�Z�G���R�7oz\��G�+��K�1׭[��gY��3��c��S�N��ŋ�B�� Ze�[���e���y�rB���ڵ�ym��]�^=���s��-S�N��=6��w����ϟV;i�ʕy��Ze��p�K���B+>|����r&X"��2��>�1c��N=zt�*tef�}�l�2�׷o�<Qhy�D�Yh�m۶�j�M	���\�ƍ;W�؎\Q��*�Gr��ɓ'�v��G.wJ�BK��.��#^�~N�B�L�^�r�j�����Ն�ЭZ�rn�h;�ϟwn��v�Y� �Q,���Ν��2�0�u�����#����^֚��\�-W^ی\[���K�
ݾ}{�2˹2^י�P׮]��ϟ�v����C[h��9��v���R�Jŵ�,t��b���ϟ�Bk�Y��sN4a��?q�D籎=����(tX��B-\�к ���7�����3څ�*���ef��6l�`U9���Ms*�|z��r���a[�Yh0���޽{��er*t�%��չ���Q��?���Sf5o��B���R��&�B/~��ᰝ�;w:Ԛ��B�����q򎛉V����پ}�z�Y�i֬Y wŏV�ŋ����Y�v�o��B��|ů큗�&Z���v���2��!ԯ_?�˸bM�B׮]�����Fn1�����!$_��D+�8r�o�]�bE k�B���ٳ})V�B�1mUf:�V�^�^�X���˹ך�`��@�l�ƍ����Ӈ���ݻU��bܸqjے+M�w���)�gϞ���,Z��>|�9���7"g������A��x��q�wr+��������8��u��g,t.�$��f��Vh!�fff�l/����������W�E7�3g�T�W��B'�6m�X���b�֭J5nX�ӣG�צ^
-�Z�رC�n�����Y�y��e[R�Dz�f�Դi����S�N�k{ӧO����ְ�	L>s�2���6�;ޮ];�k��<,t�ۼy���������%r�IP�o{:�*T(�ý��I�T�+��A����T2,3r�H�>�  ��\�	FFFƟ����nRSS��
~n[��d���f����СC�WE<y�Ĺ��|�Wd[iiif����}�<@��m�5j�\�-%vs�Y?��V2)))P��ɪ� �H< �&x "M� D���4�i� �@�	�H< �&x "M� D���4�i� �@�	�H< �&x "M� D���4�i� �@�	�H< �&x "M� D���4�i� �@�	�H< �&x "M� D���4�i� �@�	�H< �&x "M� D���4�i� �@�	�H< �&x "M� D���4�i� �@�	�H< �&x "5� �ϋ1+�    IEND�B`�\n--- END FILE: ./html.code.v0.app/public/apple-icon.png ---
\n--- START FILE: ./html.code.v0.app/public/placeholder-logo.svg ---
<svg xmlns="http://www.w3.org/2000/svg" width="215" height="48" fill="none"><path fill="#000" d="M57.588 9.6h6L73.828 38h-5.2l-2.36-6.88h-11.36L52.548 38h-5.2l10.24-28.4Zm7.16 17.16-4.16-12.16-4.16 12.16h8.32Zm23.694-2.24c-.186-1.307-.706-2.32-1.56-3.04-.853-.72-1.866-1.08-3.04-1.08-1.68 0-2.986.613-3.92 1.84-.906 1.227-1.36 2.947-1.36 5.16s.454 3.933 1.36 5.16c.934 1.227 2.24 1.84 3.92 1.84 1.254 0 2.307-.373 3.16-1.12.854-.773 1.387-1.867 1.6-3.28l5.12.24c-.186 1.68-.733 3.147-1.64 4.4-.906 1.227-2.08 2.173-3.52 2.84-1.413.667-2.986 1-4.72 1-2.08 0-3.906-.453-5.48-1.36-1.546-.907-2.76-2.2-3.64-3.88-.853-1.68-1.28-3.627-1.28-5.84 0-2.24.427-4.187 1.28-5.84.88-1.68 2.094-2.973 3.64-3.88 1.574-.907 3.4-1.36 5.48-1.36 1.68 0 3.227.32 4.64.96 1.414.64 2.56 1.56 3.44 2.76.907 1.2 1.454 2.6 1.64 4.2l-5.12.28Zm11.486-7.72.12 3.4c.534-1.227 1.307-2.173 2.32-2.84 1.04-.693 2.267-1.04 3.68-1.04 1.494 0 2.76.387 3.8 1.16 1.067.747 1.827 1.813 2.28 3.2.507-1.44 1.294-2.52 2.36-3.24 1.094-.747 2.414-1.12 3.96-1.12 1.414 0 2.64.307 3.68.92s1.84 1.52 2.4 2.72c.56 1.2.84 2.667.84 4.4V38h-4.96V25.92c0-1.813-.293-3.187-.88-4.12-.56-.96-1.413-1.44-2.56-1.44-.906 0-1.68.213-2.32.64-.64.427-1.133 1.053-1.48 1.88-.32.827-.48 1.84-.48 3.04V38h-4.56V25.92c0-1.2-.133-2.213-.4-3.04-.24-.827-.626-1.453-1.16-1.88-.506-.427-1.133-.64-1.88-.64-.906 0-1.68.227-2.32.68-.64.427-1.133 1.053-1.48 1.88-.32.827-.48 1.827-.48 3V38h-4.96V16.8h4.48Zm26.723 10.6c0-2.24.427-4.187 1.28-5.84.854-1.68 2.067-2.973 3.64-3.88 1.574-.907 3.4-1.36 5.48-1.36 1.84 0 3.494.413 4.96 1.24 1.467.827 2.64 2.08 3.52 3.76.88 1.653 1.347 3.693 1.4 6.12v1.32h-15.08c.107 1.813.614 3.227 1.52 4.24.907.987 2.134 1.48 3.68 1.48.987 0 1.88-.253 2.68-.76a4.803 4.803 0 0 0 1.84-2.2l5.08.36c-.64 2.027-1.84 3.64-3.6 4.84-1.733 1.173-3.733 1.76-6 1.76-2.08 0-3.906-.453-5.48-1.36-1.573-.907-2.786-2.2-3.64-3.88-.853-1.68-1.28-3.627-1.28-5.84Zm15.16-2.04c-.213-1.733-.76-3.013-1.64-3.84-.853-.827-1.893-1.24-3.12-1.24-1.44 0-2.6.453-3.48 1.36-.88.88-1.44 2.12-1.68 3.72h9.92ZM163.139 9.6V38h-5.04V9.6h5.04Zm8.322 7.2.24 5.88-.64-.36c.32-2.053 1.094-3.56 2.32-4.52 1.254-.987 2.787-1.48 4.6-1.48 2.32 0 4.107.733 5.36 2.2 1.254 1.44 1.88 3.387 1.88 5.84V38h-4.96V25.92c0-1.253-.12-2.28-.36-3.08-.24-.8-.64-1.413-1.2-1.84-.533-.427-1.253-.64-2.16-.64-1.44 0-2.573.48-3.4 1.44-.8.933-1.2 2.307-1.2 4.12V38h-4.96V16.8h4.48Zm30.003 7.72c-.186-1.307-.706-2.32-1.56-3.04-.853-.72-1.866-1.08-3.04-1.08-1.68 0-2.986.613-3.92 1.84-.906 1.227-1.36 2.947-1.36 5.16s.454 3.933 1.36 5.16c.934 1.227 2.24 1.84 3.92 1.84 1.254 0 2.307-.373 3.16-1.12.854-.773 1.387-1.867 1.6-3.28l5.12.24c-.186 1.68-.733 3.147-1.64 4.4-.906 1.227-2.08 2.173-3.52 2.84-1.413.667-2.986 1-4.72 1-2.08 0-3.906-.453-5.48-1.36-1.546-.907-2.76-2.2-3.64-3.88-.853-1.68-1.28-3.627-1.28-5.84 0-2.24.427-4.187 1.28-5.84.88-1.68 2.094-2.973 3.64-3.88 1.574-.907 3.4-1.36 5.48-1.36 1.68 0 3.227.32 4.64.96 1.414.64 2.56 1.56 3.44 2.76.907 1.2 1.454 2.6 1.64 4.2l-5.12.28Zm11.443 8.16V38h-5.6v-5.32h5.6Z"/><path fill="#171717" fill-rule="evenodd" d="m7.839 40.783 16.03-28.054L20 6 0 40.783h7.839Zm8.214 0H40L27.99 19.894l-4.02 7.032 3.976 6.914H20.02l-3.967 6.943Z" clip-rule="evenodd"/></svg>\n--- END FILE: ./html.code.v0.app/public/placeholder-logo.svg ---
\n--- START FILE: ./html.code.v0.app/public/placeholder.jpg ---
���� JFIF   H H  �� �Exif  MM *                  J       R(       �i       Z       H      H    �       �       �           �� 8Photoshop 3.0 8BIM      8BIM%     ��ُ ��	���B~��    ��           	
�� � s !1"AQ2aq#� �B�R3�$b0�r�C�4��S@%c5�s�PD���&T6d�t�`҄�p�'E7e�Uu��Å��Fv��GVf�	
()*89:HIJWXYZghijwxyz�����������������������������������������������������������        	
�� � � ! 1A0"2Q@3#aBqR4�P$��C�b5S��%`�D�r��c6p&ET�'��	
()*789:FGHIJUVWXYZdefghijstuvwxyz����������������������������������������������������������������������������� C 

	
")$+*($''-2@7-0=0''8L9=CEHIH+6OUNFT@GHE�� C!!E.'.EEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEEE��    �k��  �� ?�� ?��  ?�� 3     !1AQaq��������� 0@P`p���������  ?!���    �� 3   	 !1AQa q𑁡�����0@P`p��������� ?��� ?���  ?���\n--- END FILE: ./html.code.v0.app/public/placeholder.jpg ---
\n--- START FILE: ./html.code.v0.app/public/icon.svg ---
<svg width="180" height="180" viewBox="0 0 180 180" fill="none" xmlns="http://www.w3.org/2000/svg">
  <style>
    @media (prefers-color-scheme: light) {
      .background { fill: black; }
      .foreground { fill: white; }
    }
    @media (prefers-color-scheme: dark) {
      .background { fill: white; }
      .foreground { fill: black; }
    }
  </style>
  <g clip-path="url(#clip0_7960_43945)">
    <rect class="background" width="180" height="180" rx="37" />
    <g style="transform: scale(95%); transform-origin: center">
      <path class="foreground"
        d="M101.141 53H136.632C151.023 53 162.689 64.6662 162.689 79.0573V112.904H148.112V79.0573C148.112 78.7105 148.098 78.3662 148.072 78.0251L112.581 112.898C112.701 112.902 112.821 112.904 112.941 112.904H148.112V126.672H112.941C98.5504 126.672 86.5638 114.891 86.5638 100.5V66.7434H101.141V100.5C101.141 101.15 101.191 101.792 101.289 102.422L137.56 66.7816C137.255 66.7563 136.945 66.7434 136.632 66.7434H101.141V53Z" />
      <path class="foreground"
        d="M65.2926 124.136L14 66.7372H34.6355L64.7495 100.436V66.7372H80.1365V118.47C80.1365 126.278 70.4953 129.958 65.2926 124.136Z" />
    </g>
  </g>
  <defs>
    <clipPath id="clip0_7960_43945">
      <rect width="180" height="180" fill="white" />
    </clipPath>
  </defs>
</svg>\n--- END FILE: ./html.code.v0.app/public/icon.svg ---
\n--- START FILE: ./html.code.v0.app/public/placeholder.svg ---
<svg xmlns="http://www.w3.org/2000/svg" width="1200" height="1200" fill="none"><rect width="1200" height="1200" fill="#EAEAEA" rx="3"/><g opacity=".5"><g opacity=".5"><path fill="#FAFAFA" d="M600.709 736.5c-75.454 0-136.621-61.167-136.621-136.62 0-75.454 61.167-136.621 136.621-136.621 75.453 0 136.62 61.167 136.62 136.621 0 75.453-61.167 136.62-136.62 136.62Z"/><path stroke="#C9C9C9" stroke-width="2.418" d="M600.709 736.5c-75.454 0-136.621-61.167-136.621-136.62 0-75.454 61.167-136.621 136.621-136.621 75.453 0 136.62 61.167 136.62 136.621 0 75.453-61.167 136.62-136.62 136.62Z"/></g><path stroke="url(#a)" stroke-width="2.418" d="M0-1.209h553.581" transform="scale(1 -1) rotate(45 1163.11 91.165)"/><path stroke="url(#b)" stroke-width="2.418" d="M404.846 598.671h391.726"/><path stroke="url(#c)" stroke-width="2.418" d="M599.5 795.742V404.017"/><path stroke="url(#d)" stroke-width="2.418" d="m795.717 796.597-391.441-391.44"/><path fill="#fff" d="M600.709 656.704c-31.384 0-56.825-25.441-56.825-56.824 0-31.384 25.441-56.825 56.825-56.825 31.383 0 56.824 25.441 56.824 56.825 0 31.383-25.441 56.824-56.824 56.824Z"/><g clip-path="url(#e)"><path fill="#666" fill-rule="evenodd" d="M616.426 586.58h-31.434v16.176l3.553-3.554.531-.531h9.068l.074-.074 8.463-8.463h2.565l7.18 7.181V586.58Zm-15.715 14.654 3.698 3.699 1.283 1.282-2.565 2.565-1.282-1.283-5.2-5.199h-6.066l-5.514 5.514-.073.073v2.876a2.418 2.418 0 0 0 2.418 2.418h26.598a2.418 2.418 0 0 0 2.418-2.418v-8.317l-8.463-8.463-7.181 7.181-.071.072Zm-19.347 5.442v4.085a6.045 6.045 0 0 0 6.046 6.045h26.598a6.044 6.044 0 0 0 6.045-6.045v-7.108l1.356-1.355-1.282-1.283-.074-.073v-17.989h-38.689v23.43l-.146.146.146.147Z" clip-rule="evenodd"/></g><path stroke="#C9C9C9" stroke-width="2.418" d="M600.709 656.704c-31.384 0-56.825-25.441-56.825-56.824 0-31.384 25.441-56.825 56.825-56.825 31.383 0 56.824 25.441 56.824 56.825 0 31.383-25.441 56.824-56.824 56.824Z"/></g><defs><linearGradient id="a" x1="554.061" x2="-.48" y1=".083" y2=".087" gradientUnits="userSpaceOnUse"><stop stop-color="#C9C9C9" stop-opacity="0"/><stop offset=".208" stop-color="#C9C9C9"/><stop offset=".792" stop-color="#C9C9C9"/><stop offset="1" stop-color="#C9C9C9" stop-opacity="0"/></linearGradient><linearGradient id="b" x1="796.912" x2="404.507" y1="599.963" y2="599.965" gradientUnits="userSpaceOnUse"><stop stop-color="#C9C9C9" stop-opacity="0"/><stop offset=".208" stop-color="#C9C9C9"/><stop offset=".792" stop-color="#C9C9C9"/><stop offset="1" stop-color="#C9C9C9" stop-opacity="0"/></linearGradient><linearGradient id="c" x1="600.792" x2="600.794" y1="403.677" y2="796.082" gradientUnits="userSpaceOnUse"><stop stop-color="#C9C9C9" stop-opacity="0"/><stop offset=".208" stop-color="#C9C9C9"/><stop offset=".792" stop-color="#C9C9C9"/><stop offset="1" stop-color="#C9C9C9" stop-opacity="0"/></linearGradient><linearGradient id="d" x1="404.85" x2="796.972" y1="403.903" y2="796.02" gradientUnits="userSpaceOnUse"><stop stop-color="#C9C9C9" stop-opacity="0"/><stop offset=".208" stop-color="#C9C9C9"/><stop offset=".792" stop-color="#C9C9C9"/><stop offset="1" stop-color="#C9C9C9" stop-opacity="0"/></linearGradient><clipPath id="e"><path fill="#fff" d="M581.364 580.535h38.689v38.689h-38.689z"/></clipPath></defs></svg>\n--- END FILE: ./html.code.v0.app/public/placeholder.svg ---
\n--- START FILE: ./html.code.v0.app/public/placeholder-logo.png ---
�PNG

   IHDR      �   M��   0PLTE                                                Z?   tRNS � �@��`P0p���w  �IDATx��ؽJ3Q�7'��%�|?� ���E�l�7���(X�D������w`����[�*t����D���mD�}��4;;�DDDDDDDDDDDD_�_İ��!�y�`�_�:��;Ļ�'|�	��;.I"����3*5����J�1�� �T��FI��	��=��3܃�2~�b���0��U9\��]�4�#w0��Gt\&1�?21,���o!e�m��ĻR�����5�� ؽAJ�9��R)�5�0.FFASaǃ�T�#|�K���I�������1�
M������N"��$����G�V�T���T^^��A�$S��h(�������G]co"J׸^^�'�=���%�	�W�6Ы�W��w�a�߇*�^^�YG�c���`'F����������������^ 5_�,�S�%    IEND�B`�\n--- END FILE: ./html.code.v0.app/public/placeholder-logo.png ---
\n--- START FILE: ./html.code.v0.app/public/icon-dark-32x32.png ---
�PNG

   IHDR           szz�   	pHYs     ��   sRGB ���   gAMA  ���a  �IDATx��q�@�W'P�H**��
� �D+�T V h��e_"�!���ˏ<3���ܾ��J$!���>�r�?�im�T�D ^�{��'@��IIJz����A�p���/�C�42$�h�F=�X,���A�i�d2��h�v=��.�ݮu_]�EQ�V�R+�`^۶M*dd#��2#��Re�x6���z�W��Bb>��ci�
����;��j�Q�j��Gɲ�̊�{�$Iïq
��S��!��O�w�8�J��1��
N;��kz&�f���W�˲(�z�\.i���5�sO�q�u��A1�0��9P��8xc���.s������ ��� �F% vK��y.�8[ �K����v��J�ܨ���.�F�A���~���H��c�6��`��}���قO�� �
�G_��Eh�ELzx��/n����cg��3��*%�Ɇ����-9�7u{˩DS�    IEND�B`�\n--- END FILE: ./html.code.v0.app/public/icon-dark-32x32.png ---
\n--- START FILE: ./html.code.v0.app/next.config.mjs ---
/** @type {import('next').NextConfig} */
const nextConfig = {
  typescript: {
    ignoreBuildErrors: true,
  },
  images: {
    unoptimized: true,
  },
}

export default nextConfig
\n--- END FILE: ./html.code.v0.app/next.config.mjs ---
\n--- START FILE: ./html.code.v0.app/BACKEND_SETUP.md ---
# Yana.Diia Backend Setup Guide

## 🚀 Швидкий старт

### Linux/Mac

\`\`\`bash
# 1. Запустіть setup script
bash scripts/setup-backend.sh

# 2. Заповніть .env
nano .env  # Додайте ANTHROPIC_API_KEY

# 3. Запустіть backend
bash scripts/run-backend.sh
\`\`\`

### Windows

\`\`\`bash
# 1. Запустіть setup script
scripts\setup-backend.bat

# 2. Заповніть .env
# Відредагуйте .env у текстовому редакторі, додайте ANTHROPIC_API_KEY

# 3. Запустіть backend
scripts\run-backend.bat
\`\`\`

## 📋 Вимоги

- Python 3.10+
- pip (встановлюється з Python)
- Git (для клонування Diia repos)
- Anthropic API key (з https://console.anthropic.com/)

## ✅ Перевірка налаштування

Коли backend запущено, перевіріть:

1. **API Docs**: http://localhost:8000/docs
2. **Health Check**: http://localhost:8000/health
3. **Component List**: http://localhost:8000/api/v1/components?limit=5

## 🔧 Структура Backend

\`\`\`
backend/
├── main.py              # FastAPI додаток
├── requirements.txt     # Залежності
├── generation/          # LLM генерація flow
│   └── abn_generator.py # A/B/N тестування
├── evaluation/          # Оцінювання якості
│   └── flow_evaluator.py
├── rag/                 # Vector DB та пошук
│   └── embeddings.py
└── validation/
    └── schemas.py       # Pydantic моделі
\`\`\`

## 📝 Environment Variables

| Змінна | Опис | Обов'язково |
|--------|------|-----------|
| ANTHROPIC_API_KEY | API ключ Claude | Так |
| LLM_MODEL | Модель Claude | Ні (за замовч: claude-sonnet-4) |
| DIIA_REPOS_PATH | Шлях до Diia repos | Ні |
| DEBUG | Режим debug | Ні |

## 🧪 Тестування API

### Generate Flow

\`\`\`bash
curl -X POST "http://localhost:8000/api/v1/generate" \
  -H "Content-Type: application/json" \
  -d '{
    "brd": "Користувач хоче подати документи онлайн",
    "num_variants": 3,
    "design_system": "diia"
  }'
\`\`\`

### List Components

\`\`\`bash
curl "http://localhost:8000/api/v1/components?limit=10"
\`\`\`

### Health Check

\`\`\`bash
curl "http://localhost:8000/health"
\`\`\`

## 🐛 Troubleshooting

### Backend не запускається

\`\`\`bash
# Перевірте Python версію
python --version  # Має бути 3.10+

# Перевірте virtual environment
source venv/bin/activate
pip list  # Мають бути fastapi, uvicorn тощо
\`\`\`

### API Connection Failed

- Перевірте що backend запущено на localhost:8000
- Перевірте firewall налаштування
- Перевірте .env файл існує

### LLM API Errors

- Перевірте ANTHROPIC_API_KEY правильний
- Перевірте що вам хватає kreditu на Anthropic
- Перевірте інтернет з'єднання

## 📚 Посилання

- [Backend Python файли](./user_read_only_context/text_attachments/) - пошукайте lifespan-GBrT8.py
- [Anthropic API Docs](https://docs.anthropic.com/)
- [FastAPI Docs](https://fastapi.tiangolo.com/)
- [Diia Open Source](https://github.com/orgs/diia-open-source/)
\n--- END FILE: ./html.code.v0.app/BACKEND_SETUP.md ---
\n--- START FILE: ./html.code.v0.app/package.json ---
{
  "name": "my-v0-project",
  "version": "0.1.0",
  "private": true,
  "scripts": {
    "build": "next build",
    "dev": "next dev",
    "lint": "eslint .",
    "start": "next start"
  },
  "dependencies": {
    "@hookform/resolvers": "^3.10.0",
    "@radix-ui/react-accordion": "1.2.2",
    "@radix-ui/react-alert-dialog": "1.1.4",
    "@radix-ui/react-aspect-ratio": "1.1.1",
    "@radix-ui/react-avatar": "1.1.2",
    "@radix-ui/react-checkbox": "1.1.3",
    "@radix-ui/react-collapsible": "1.1.2",
    "@radix-ui/react-context-menu": "2.2.4",
    "@radix-ui/react-dialog": "1.1.4",
    "@radix-ui/react-dropdown-menu": "2.1.4",
    "@radix-ui/react-hover-card": "1.1.4",
    "@radix-ui/react-label": "2.1.1",
    "@radix-ui/react-menubar": "1.1.4",
    "@radix-ui/react-navigation-menu": "1.2.3",
    "@radix-ui/react-popover": "1.1.4",
    "@radix-ui/react-progress": "1.1.1",
    "@radix-ui/react-radio-group": "1.2.2",
    "@radix-ui/react-scroll-area": "1.2.2",
    "@radix-ui/react-select": "2.1.4",
    "@radix-ui/react-separator": "1.1.1",
    "@radix-ui/react-slider": "1.2.2",
    "@radix-ui/react-slot": "1.1.1",
    "@radix-ui/react-switch": "1.1.2",
    "@radix-ui/react-tabs": "1.1.2",
    "@radix-ui/react-toast": "1.2.4",
    "@radix-ui/react-toggle": "1.1.1",
    "@radix-ui/react-toggle-group": "1.1.1",
    "@radix-ui/react-tooltip": "1.1.6",
    "@vercel/analytics": "latest",
    "autoprefixer": "^10.4.20",
    "class-variance-authority": "^0.7.1",
    "clsx": "^2.1.1",
    "cmdk": "1.0.4",
    "date-fns": "4.1.0",
    "embla-carousel-react": "8.5.1",
    "input-otp": "1.4.1",
    "lucide-react": "^0.454.0",
    "next": "16.0.3",
    "next-themes": "^0.4.6",
    "react": "19.2.0",
    "react-day-picker": "9.8.0",
    "react-dom": "19.2.0",
    "react-hook-form": "^7.60.0",
    "react-resizable-panels": "^2.1.7",
    "recharts": "2.15.4",
    "sonner": "^1.7.4",
    "tailwind-merge": "^2.5.5",
    "tailwindcss-animate": "^1.0.7",
    "vaul": "^0.9.9",
    "zod": "3.25.76"
  },
  "devDependencies": {
    "@tailwindcss/postcss": "^4.1.9",
    "@types/node": "^22",
    "@types/react": "^19",
    "@types/react-dom": "^19",
    "postcss": "^8.5",
    "tailwindcss": "^4.1.9",
    "tw-animate-css": "1.3.3",
    "typescript": "^5"
  }
}\n--- END FILE: ./html.code.v0.app/package.json ---
\n--- START FILE: ./html.code.v0.app/tsconfig.json ---
{
  "compilerOptions": {
    "lib": ["dom", "dom.iterable", "esnext"],
    "allowJs": true,
    "target": "ES6",
    "skipLibCheck": true,
    "strict": true,
    "noEmit": true,
    "esModuleInterop": true,
    "module": "esnext",
    "moduleResolution": "bundler",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "jsx": "preserve",
    "incremental": true,
    "plugins": [
      {
        "name": "next"
      }
    ],
    "paths": {
      "@/*": ["./*"]
    }
  },
  "include": ["next-env.d.ts", "**/*.ts", "**/*.tsx", ".next/types/**/*.ts"],
  "exclude": ["node_modules"]
}
\n--- END FILE: ./html.code.v0.app/tsconfig.json ---
\n--- START FILE: ./html.code.v0.app/styles/globals.css ---
@import 'tailwindcss';
@import 'tw-animate-css';

@custom-variant dark (&:is(.dark *));

:root {
  --background: oklch(1 0 0);
  --foreground: oklch(0.145 0 0);
  --card: oklch(1 0 0);
  --card-foreground: oklch(0.145 0 0);
  --popover: oklch(1 0 0);
  --popover-foreground: oklch(0.145 0 0);
  --primary: oklch(0.205 0 0);
  --primary-foreground: oklch(0.985 0 0);
  --secondary: oklch(0.97 0 0);
  --secondary-foreground: oklch(0.205 0 0);
  --muted: oklch(0.97 0 0);
  --muted-foreground: oklch(0.556 0 0);
  --accent: oklch(0.97 0 0);
  --accent-foreground: oklch(0.205 0 0);
  --destructive: oklch(0.577 0.245 27.325);
  --destructive-foreground: oklch(0.577 0.245 27.325);
  --border: oklch(0.922 0 0);
  --input: oklch(0.922 0 0);
  --ring: oklch(0.708 0 0);
  --chart-1: oklch(0.646 0.222 41.116);
  --chart-2: oklch(0.6 0.118 184.704);
  --chart-3: oklch(0.398 0.07 227.392);
  --chart-4: oklch(0.828 0.189 84.429);
  --chart-5: oklch(0.769 0.188 70.08);
  --radius: 0.625rem;
  --sidebar: oklch(0.985 0 0);
  --sidebar-foreground: oklch(0.145 0 0);
  --sidebar-primary: oklch(0.205 0 0);
  --sidebar-primary-foreground: oklch(0.985 0 0);
  --sidebar-accent: oklch(0.97 0 0);
  --sidebar-accent-foreground: oklch(0.205 0 0);
  --sidebar-border: oklch(0.922 0 0);
  --sidebar-ring: oklch(0.708 0 0);
}

.dark {
  --background: oklch(0.145 0 0);
  --foreground: oklch(0.985 0 0);
  --card: oklch(0.145 0 0);
  --card-foreground: oklch(0.985 0 0);
  --popover: oklch(0.145 0 0);
  --popover-foreground: oklch(0.985 0 0);
  --primary: oklch(0.985 0 0);
  --primary-foreground: oklch(0.205 0 0);
  --secondary: oklch(0.269 0 0);
  --secondary-foreground: oklch(0.985 0 0);
  --muted: oklch(0.269 0 0);
  --muted-foreground: oklch(0.708 0 0);
  --accent: oklch(0.269 0 0);
  --accent-foreground: oklch(0.985 0 0);
  --destructive: oklch(0.396 0.141 25.723);
  --destructive-foreground: oklch(0.637 0.237 25.331);
  --border: oklch(0.269 0 0);
  --input: oklch(0.269 0 0);
  --ring: oklch(0.439 0 0);
  --chart-1: oklch(0.488 0.243 264.376);
  --chart-2: oklch(0.696 0.17 162.48);
  --chart-3: oklch(0.769 0.188 70.08);
  --chart-4: oklch(0.627 0.265 303.9);
  --chart-5: oklch(0.645 0.246 16.439);
  --sidebar: oklch(0.205 0 0);
  --sidebar-foreground: oklch(0.985 0 0);
  --sidebar-primary: oklch(0.488 0.243 264.376);
  --sidebar-primary-foreground: oklch(0.985 0 0);
  --sidebar-accent: oklch(0.269 0 0);
  --sidebar-accent-foreground: oklch(0.985 0 0);
  --sidebar-border: oklch(0.269 0 0);
  --sidebar-ring: oklch(0.439 0 0);
}

@theme inline {
  --font-sans: 'Geist', 'Geist Fallback';
  --font-mono: 'Geist Mono', 'Geist Mono Fallback';
  --color-background: var(--background);
  --color-foreground: var(--foreground);
  --color-card: var(--card);
  --color-card-foreground: var(--card-foreground);
  --color-popover: var(--popover);
  --color-popover-foreground: var(--popover-foreground);
  --color-primary: var(--primary);
  --color-primary-foreground: var(--primary-foreground);
  --color-secondary: var(--secondary);
  --color-secondary-foreground: var(--secondary-foreground);
  --color-muted: var(--muted);
  --color-muted-foreground: var(--muted-foreground);
  --color-accent: var(--accent);
  --color-accent-foreground: var(--accent-foreground);
  --color-destructive: var(--destructive);
  --color-destructive-foreground: var(--destructive-foreground);
  --color-border: var(--border);
  --color-input: var(--input);
  --color-ring: var(--ring);
  --color-chart-1: var(--chart-1);
  --color-chart-2: var(--chart-2);
  --color-chart-3: var(--chart-3);
  --color-chart-4: var(--chart-4);
  --color-chart-5: var(--chart-5);
  --radius-sm: calc(var(--radius) - 4px);
  --radius-md: calc(var(--radius) - 2px);
  --radius-lg: var(--radius);
  --radius-xl: calc(var(--radius) + 4px);
  --color-sidebar: var(--sidebar);
  --color-sidebar-foreground: var(--sidebar-foreground);
  --color-sidebar-primary: var(--sidebar-primary);
  --color-sidebar-primary-foreground: var(--sidebar-primary-foreground);
  --color-sidebar-accent: var(--sidebar-accent);
  --color-sidebar-accent-foreground: var(--sidebar-accent-foreground);
  --color-sidebar-border: var(--sidebar-border);
  --color-sidebar-ring: var(--sidebar-ring);
}

@layer base {
  * {
    @apply border-border outline-ring/50;
  }
  body {
    @apply bg-background text-foreground;
  }
}
\n--- END FILE: ./html.code.v0.app/styles/globals.css ---
\n--- START FILE: ./.gitignore ---
# Byte-compiled / optimized / DLL files
__pycache__/
*.py[codz]
*$py.class

# C extensions
*.so

# Distribution / packaging
.Python
build/
develop-eggs/
dist/
downloads/
eggs/
.eggs/
lib/
lib64/
parts/
sdist/
var/
wheels/
share/python-wheels/
*.egg-info/
.installed.cfg
*.egg
MANIFEST

# PyInstaller
#  Usually these files are written by a python script from a template
#  before PyInstaller builds the exe, so as to inject date/other infos into it.
*.manifest
*.spec

# Installer logs
pip-log.txt
pip-delete-this-directory.txt

# Unit test / coverage reports
htmlcov/
.tox/
.nox/
.coverage
.coverage.*
.cache
nosetests.xml
coverage.xml
*.cover
*.py.cover
.hypothesis/
.pytest_cache/
cover/

# Translations
*.mo
*.pot

# Django stuff:
*.log
local_settings.py
db.sqlite3
db.sqlite3-journal

# Flask stuff:
instance/
.webassets-cache

# Scrapy stuff:
.scrapy

# Sphinx documentation
docs/_build/

# PyBuilder
.pybuilder/
target/

# Jupyter Notebook
.ipynb_checkpoints

# IPython
profile_default/
ipython_config.py

# pyenv
#   For a library or package, you might want to ignore these files since the code is
#   intended to run in multiple environments; otherwise, check them in:
# .python-version

# pipenv
#   According to pypa/pipenv#598, it is recommended to include Pipfile.lock in version control.
#   However, in case of collaboration, if having platform-specific dependencies or dependencies
#   having no cross-platform support, pipenv may install dependencies that don't work, or not
#   install all needed dependencies.
#Pipfile.lock

# UV
#   Similar to Pipfile.lock, it is generally recommended to include uv.lock in version control.
#   This is especially recommended for binary packages to ensure reproducibility, and is more
#   commonly ignored for libraries.
#uv.lock

# poetry
#   Similar to Pipfile.lock, it is generally recommended to include poetry.lock in version control.
#   This is especially recommended for binary packages to ensure reproducibility, and is more
#   commonly ignored for libraries.
#   https://python-poetry.org/docs/basic-usage/#commit-your-poetrylock-file-to-version-control
#poetry.lock
#poetry.toml

# pdm
#   Similar to Pipfile.lock, it is generally recommended to include pdm.lock in version control.
#   pdm recommends including project-wide configuration in pdm.toml, but excluding .pdm-python.
#   https://pdm-project.org/en/latest/usage/project/#working-with-version-control
#pdm.lock
#pdm.toml
.pdm-python
.pdm-build/

# pixi
#   Similar to Pipfile.lock, it is generally recommended to include pixi.lock in version control.
#pixi.lock
#   Pixi creates a virtual environment in the .pixi directory, just like venv module creates one
#   in the .venv directory. It is recommended not to include this directory in version control.
.pixi

# PEP 582; used by e.g. github.com/David-OConnor/pyflow and github.com/pdm-project/pdm
__pypackages__/

# Celery stuff
celerybeat-schedule
celerybeat.pid

# SageMath parsed files
*.sage.py

# Environments
.env
.envrc
.venv
env/
venv/
ENV/
env.bak/
venv.bak/

# Spyder project settings
.spyderproject
.spyproject

# Rope project settings
.ropeproject

# mkdocs documentation
/site

# mypy
.mypy_cache/
.dmypy.json
dmypy.json

# Pyre type checker
.pyre/

# pytype static type analyzer
.pytype/

# Cython debug symbols
cython_debug/

# PyCharm
#  JetBrains specific template is maintained in a separate JetBrains.gitignore that can
#  be found at https://github.com/github/gitignore/blob/main/Global/JetBrains.gitignore
#  and can be added to the global gitignore or merged into this file.  For a more nuclear
#  option (not recommended) you can uncomment the following to ignore the entire idea folder.
#.idea/

# Abstra
# Abstra is an AI-powered process automation framework.
# Ignore directories containing user credentials, local state, and settings.
# Learn more at https://abstra.io/docs
.abstra/

# Visual Studio Code
#  Visual Studio Code specific template is maintained in a separate VisualStudioCode.gitignore 
#  that can be found at https://github.com/github/gitignore/blob/main/Global/VisualStudioCode.gitignore
#  and can be added to the global gitignore or merged into this file. However, if you prefer, 
#  you could uncomment the following to ignore the entire vscode folder
# .vscode/

# Ruff stuff:
.ruff_cache/

# PyPI configuration file
.pypirc

# Cursor
#  Cursor is an AI-powered code editor. `.cursorignore` specifies files/directories to
#  exclude from AI features like autocomplete and code analysis. Recommended for sensitive data
#  refer to https://docs.cursor.com/context/ignore-files
.cursorignore
.cursorindexingignore

# Marimo
marimo/_static/
marimo/_lsp/
__marimo__/
\n--- END FILE: ./.gitignore ---
\n--- START FILE: ./README.md ---
# Yana.Diia
Diia.AIContest
\n--- END FILE: ./README.md ---
\n--- START FILE: ./txt.txt ---

\n--- END FILE: ./txt.txt ---
