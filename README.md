# Habit Tracker — śledzenie nawyków

Aplikacja webowa stworzona w React, która pomaga śledzić codzienne nawyki, monitorować postępy i zdobywać XP za realizację zadań.

## Funkcjonalności

- **Profile użytkowników** — możliwość korzystania z osobnych profili i przechowywania ich danych lokalnie w przeglądarce.
- **Zarządzanie nawykami** — dodawanie i śledzenie zadań.
- **Kalendarz** — przeglądanie aktywności i postępów.
- **Podsumowanie** — analizowanie wykonanych zadań w wybranym dniu.
- **Zapisywanie danych** — wykorzystanie `localStorage`, aby zachować dane po odświeżeniu strony.
- **Tryb jasny i ciemny** — możliwość zmiany motywu z zapamiętywaniem preferencji.
- **Obsługa nowego roku** — archiwizowanie danych z poprzedniego roku i rozpoczęcie nowego okresu śledzenia nawyków.

## Technologie

- React
- JavaScript
- Vite
- CSS
- Bootstrap
- Web Storage API (`localStorage`)

## Struktura projektu

- `src/App.jsx` — główny komponent, zarządzanie stanem aplikacji i zapisywanie danych.
- `src/App.css` — style głównego widoku.
- `src/assets/components/AccountAccess.jsx` — interfejs wyboru lub obsługi profilu.
- `src/assets/components/Tracker.jsx` — część odpowiedzialna za nawyki.
- `src/assets/components/Calendar.jsx` — kalendarz aktywności.
- `src/assets/components/Summary.jsx` — podsumowanie postępów.

## Zrzuty ekranu

<img width="706" height="841" alt="Ekran logowania" src="https://github.com/user-attachments/assets/5e8ed905-8d6e-4b51-8886-9db707420014" />
<img width="735" height="990" alt="Ekran rejestracji" src="https://github.com/user-attachments/assets/76c88d28-52a8-4cd5-990a-e6ef107b5f5d" />
<img width="2517" height="1327" alt="Główny widok aplikacji" src="https://github.com/user-attachments/assets/f95577ad-42d3-407e-8681-269ef7755d4d" />


## Uruchomienie lokalne

1. Sklonuj repozytorium.
2. Otwórz folder projektu w terminalu.
3. Zainstaluj zależności:

   `npm install`

4. Uruchom aplikację:

   `npm run dev`

5. Otwórz adres lokalny podany przez Vite w terminalu.

## Przechowywanie danych

Aplikacja wykorzystuje `localStorage`, dlatego profile i ich dane są przechowywane w przeglądarce na danym urządzeniu. Nie jest to system kont oparty na serwerze, a dane nie synchronizują się automatycznie pomiędzy urządzeniami.



## Wybrane fragmenty kodu

### 1. Zapisywanie danych

Aplikacja zapisuje nawyki w `localStorage`, dzięki czemu pozostają dostępne po odświeżeniu strony.

```jsx
useEffect(() => {
    if (!user || !tasksLoaded) {
        return;
    }

    const key = getStorageKey(user);

    const data = {
        tasks,
        year: getCurrentYear(),
        updatedAt: new Date().toISOString()
    };

    localStorage.setItem(
        key,
        JSON.stringify(data)
    );
}, [tasks, user, tasksLoaded]);
```

### 2. Zmiana motywu

```jsx
useEffect(() => {
    document.body.classList.toggle(
        "light",
        theme === "light"
    );

    localStorage.setItem(THEME_KEY, theme);
}, [theme]);
```

### 3. Podział na komponenty

```jsx
<Tracker tasks={tasks} setTasks={setTasks} />

<Calendar tasks={tasks} />

<Summary
    tasks={tasks}
    summaryDay={summaryDay}
    setSummaryDay={setSummaryDay}
/>
```

### 3. Architektura komponentów

Interfejs został podzielony na komponenty `Tracker`, `Calendar` i `Summary`. Główny komponent przekazuje im potrzebne dane i funkcje za pomocą propsów.

```jsx
<section id="content">
    <div id="tracker">
        <Tracker
            tasks={tasks}
            setTasks={setTasks}
        />
    </div>

    <div id="calendar">
        <Calendar tasks={tasks} />
    </div>

    <div className="summary-container">
        <Summary
            tasks={tasks}
            summaryDay={summaryDay}
            setSummaryDay={setSummaryDay}
        />
    </div>
</section>
```


## Uruchom aplikację

[**Demo:**](https://virucoder.github.io/habit-tracker/)

**Kod źródłowy wybranych komponentów:** dostępny w repozytorium projektu.
