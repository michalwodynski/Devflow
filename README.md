# DevFlow — Platforma Q&A i Oferty Pracy (Next.js + TypeScript)

## 🚀 Opis

`DevFlow` to nowoczesna aplikacja webowa zbudowana w oparciu o Next.js (App Router) i TypeScript. Jest to platforma typu Q&A z funkcjami społecznościowymi oraz modułem ofert pracy. Aplikacja oferuje pełen przepływ: rejestracja/logowanie, tworzenie i ocenianie pytań i odpowiedzi, tagowanie, wyszukiwanie oraz integrację z usługami AI do generowania krótkich, sformatowanych odpowiedzi.

Główne funkcje:
- Rejestracja i logowanie (credentials + OAuth: GitHub, Google) przy użyciu `next-auth`.
- Tworzenie pytań i odpowiedzi, głosowanie, tagi i paginacja.
- Endpointy serwerowe w `app/api/*` z walidacją i obsługą błędów.
- Integracja AI (`@ai-sdk/openai` + `ai`) do generowania odpowiedzi.
- Moduł ofert pracy korzystający z RapidAPI.
- Warstwa dostępu do danych: `mongoose` + modele w `database/`.

## 🛠️ Stos Technologiczny

- Framework: **Next.js (App Router)** — `next@15`
- Język: **TypeScript** (`typescript@5`)
- UI: **React 19**, **Tailwind CSS**, **Radix UI**, **Lucide**
- Autoryzacja: **next-auth** (GitHub, Google, credentials)
- Baza danych: **MongoDB** z **mongoose**
- AI / NLP: **@ai-sdk/openai**, **ai**
- Formularze / walidacja: **react-hook-form**, **zod**, **@hookform/resolvers**
- MDX / edytor: **@mdxeditor/editor**, **next-mdx-remote**
- Narzędzia dev: **ESLint**, **Prettier**, **Tailwind CSS**

Zależności i ich wersje znajdują się w `package.json`.

## ⚙️ Konfiguracja (.env)

Aplikacja wymaga kilku zmiennych środowiskowych. Poniżej spis najważniejszych kluczy oraz przykładowy plik ` .env.example`. NIE umieszczaj prawdziwych sekretów w repozytorium.

Wymagane / rekomendowane zmienne środowiskowe:
- `PORT` — (opcjonalne) port aplikacji (domyślnie `3000`).
- `NODE_ENV` — `development` | `production`.
- `MONGODB_URI` — URI połączenia do MongoDB (WYMAGANE). Aplikacja przerwie start, jeśli nie jest ustawione (sprawdzenie w `lib/mongoose.ts`).
- `NEXTAUTH_URL` — publiczny URL aplikacji (np. `http://localhost:3000`).
- `NEXTAUTH_SECRET` — sekret dla `next-auth` (silny losowy string).
- `GITHUB_ID` i `GITHUB_SECRET` — OAuth GitHub (opcjonalne).
- `GOOGLE_ID` i `GOOGLE_SECRET` — OAuth Google (opcjonalne).
- `NEXT_PUBLIC_API_BASE_URL` — (opcjonalne) baza URL dla wywołań API z frontendu (domyślnie `http://localhost:3000/api`).
- `NEXT_PUBLIC_RAPID_API_KEY` — (opcjonalne) klucz RapidAPI używany przez moduł job search (`lib/actions/job.action.ts`).
- `OPENAI_API_KEY` — (opcjonalne) klucz do integracji AI (używany przez `@ai-sdk/openai` lub konfigurację SDK).

Przykładowy plik `.env.example`:

```env
# Serwer
PORT=3000
NODE_ENV=development

# Baza danych
MONGODB_URI=mongodb+srv://username:password@cluster0.mongodb.net/devflow?retryWrites=true&w=majority

# NextAuth
NEXTAUTH_URL=http://localhost:3000
NEXTAUTH_SECRET=replace_with_a_long_random_secret

# OAuth
GITHUB_ID=your_github_client_id
GITHUB_SECRET=your_github_client_secret
GOOGLE_ID=your_google_client_id
GOOGLE_SECRET=your_google_client_secret

# API / 3rd party
NEXT_PUBLIC_API_BASE_URL=http://localhost:3000/api
NEXT_PUBLIC_RAPID_API_KEY=your_rapidapi_key
OPENAI_API_KEY=your_openai_api_key

```

## 🔧 Uruchomienie lokalne

1. Zainstaluj zależności

```bash
npm install
```

2. Skopiuj i uzupełnij plik środowiskowy

```bash
cp .env.example .env
# edytuj .env i wstaw swoje wartości
```

3. Uruchom w trybie deweloperskim

```bash
npm run dev
```

4. Budowanie i uruchomienie produkcyjne

```bash
npm run build
npm run start
```

## ✅ Skrypty (z `package.json`)

- `npm run dev` — uruchamia Next.js w trybie deweloperskim.
- `npm run build` — buduje aplikację do produkcji.
- `npm run start` — uruchamia aplikację po zbudowaniu.
- `npm run lint` — uruchamia ESLint.

## Kontekst Projektu

Ten projekt został stworzony jako część kursu "The Ultimate Next.js Course" autorstwa JS Mastery.

## Struktura projektu (wybrane katalogi)

- `app/` — strony i routing (Next.js App Router).
- `components/` — komponenty UI i moduły (cards, forms, editor itp.).
- `lib/` — pomocnicze moduły: `api.ts`, `mongoose.ts`, `logger.ts`, akcje i handlery.
- `database/` — modele Mongoose (`user.model.ts`, `question.model.ts`, `answer.model.ts` itp.).
- `app/api/` — API routes (serwerowe endpointy Next.js).
