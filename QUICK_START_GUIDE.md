# 🚀 Quick Start Guide — 3D Print Studio

Пошаговый гайд для быстрого запуска проекта.

---

## 📝 Шаг 1: Подготовка проекта

### 1.1 Склонируй репозиторий

```bash
git clone https://github.com/BrickVrn/3d-print.git
cd 3d-print
```

### 1.2 Изучи документацию

```bash
# Прочитай главные документы
cat README.md
cat KODA.md
```

---

## 🔧 Шаг 2: Инициализация Frontend

```bash
# Создай Next.js приложение
mkdir frontend
cd frontend

npx create-next-app@latest . --typescript --tailwind --eslint

# Установи зависимости
npm install \
  three \
  @react-three/fiber \
  @react-three/drei \
  axios \
  react-hook-form \
  zod \
  @hookform/resolvers

npm install --save-dev @types/three

# Запусти dev server
npm run dev
# http://localhost:3000
```

---

## 🛠️ Шаг 3: Инициализация Backend

```bash
# Вернись в корень
cd ..

# Создай Express приложение
mkdir backend
cd backend

npm init -y

# Установи зависимости
npm install \
  express \
  typescript \
  ts-node \
  pg \
  knex \
  bcryptjs \
  jsonwebtoken \
  dotenv \
  cors \
  helmet

npm install --save-dev \
  @types/express \
  @types/node \
  ts-node-dev

# Создай структуру
mkdir -p src/{config,routes,controllers,models}
touch src/index.ts
```

### Минимальный index.ts

```typescript
// backend/src/index.ts
import express from 'express';
import cors from 'cors';

const app = express();
const PORT = process.env.PORT || 5000;

app.use(cors());
app.use(express.json());

app.get('/api/health', (req, res) => {
  res.json({ status: 'OK' });
});

app.listen(PORT, () => {
  console.log(`Backend running on http://localhost:${PORT}`);
});
```

---

## 💾 Шаг 4: Настройка Database

### Локально (PostgreSQL через Docker)

```bash
# Запусти PostgreSQL контейнер
docker run --name 3d-studio-db \
  -e POSTGRES_PASSWORD=dev_password \
  -e POSTGRES_DB=3d_studio \
  -p 5432:5432 \
  -d postgres:15

# .env для backend
cd backend
echo "DATABASE_URL=postgresql://postgres:dev_password@localhost:5432/3d_studio" > .env
echo "JWT_SECRET=your_random_secret_here" >> .env
```

---

## 🤖 Шаг 5: Первый запрос к Koda

### Исследование требований

```bash
koda research "Проанализируй требование: главная страница лендинга 3D печати 
с героя-секцией (3D сцена Bambu Lab H2S). Какие компоненты нужны?"
```

### Реализация компонента

```bash
koda implementation "Реализуй компонент HeroSection.tsx 
с интерактивной 3D сценой (Three.js + react-three-fiber).
TypeScript типизация, dark/light тема, responsive дизайн."
```

---

## ✅ Чек-лист при старте

- [ ] Git репозиторий склонирован
- [ ] KODA.md изучен
- [ ] Frontend: `npm install` работает
- [ ] Backend: `npm install` работает
- [ ] PostgreSQL БД создана
- [ ] `.env` файлы заполнены
- [ ] Первый Koda запрос выполнен

---

## 🆘 Troubleshooting

### Backend не подключается к БД

```bash
# Проверь CONNECTION STRING
echo $DATABASE_URL

# Проверь что PostgreSQL запущена
docker ps | grep 3d-studio-db

# Тестируй подключение
psql $DATABASE_URL -c "SELECT 1"
```

### Frontend не загружает 3D модель

```bash
# Проверь файл существует
ls -la frontend/public/models/

# Проверь размер (max 5MB)
du -h frontend/public/models/bambu-h2s.glb
```

---

**Good luck! 🚀**
