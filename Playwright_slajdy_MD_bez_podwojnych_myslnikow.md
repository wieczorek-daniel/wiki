# PLAYWRIGHT

## Automatyzacja testów aplikacji webowych

**Testy UI • API • E2E • CI/CD**

Materiał prezentacyjny — 15 slajdów — ## 1. Czym jest Playwright?

Automatyzacja testów aplikacji webowych

- Automatyzacja interakcji z
aplikacjami internetowymi.

- Testowanie rzeczywistych scenariuszy
użytkownika.

- Weryfikowanie, czy aplikacja działa zgodnie z
oczekiwaniami.

- Możliwość uruchamiania testów w różnych przeglądarkach.

### Obsługiwane silniki przeglądarek

- Chromium — m.in. Google Chrome i Microsoft Edge.
- Firefox.
- WebKit — silnik wykorzystywany przez Safari. Jeden zestaw testów
```ts
może być uruchamiany w trzech różnych silnikach przeglądarek.
``` — ## 2. Problem — dlaczego potrzebujemy automatyzacji?

Wyobraźmy sobie, że tworzymy sklep internetowy. Za każdym razem, gdy zmieniamy kod

aplikacji, ktoś musi sprawdzić, czy wszystko nadal działa. 

### Przykładowa ścieżka użytkownika

1. Otworzenie przeglądarki.
2. Zalogowanie się.
3. Wyszukanie produktu.
4. Dodanie produktu do koszyka.
5. Przejście do kasy i finalizacja zamówienia.

Takie czynności trzeba
```ts
wykonywać ponownie po zmianach, aby upewnić się, że nic nie zostało
zepsute.
```
Problem: ręczne testowanie jest czasochłonne, powtarzalne i
```ts
podatne na błędy.
``` — ## 3. Czym jest Playwright?

Playwright to framework do automatyzacji przeglądarek i testowania end-to-end (E2E).

- Tworzysz testy opisujące zachowanie użytkownika.
- Playwright automatycznie steruje przeglądarką.
- Wykonuje określone czynności.
- Sprawdza, czy aplikacja zachowuje się zgodnie z oczekiwaniami.
```ts
Playwright jest rozwijany przez Microsoft.
```
Playwright pozwala
```ts
uruchamiać testy w Chromium, Firefox i WebKit.
``` — ## 4. Jak wygląda napisanie testu?

Zamiast ręcznie wykonywać kolejne czynności, opisujemy je w kodzie.

### Przykładowy scenariusz

1. Otwórz stronę internetową.
2. Znajdź formularz logowania.
3. Wypełnij formularz.
4. Kliknij przycisk logowania.
5. Sprawdź, czy pojawił się dashboard. 

### Przykładowy kod

```ts
import { test, expect } from '@playwright/test';
test('logowanie użytkownika', async ({ page }) => {
await page.goto('https://example.com');
await page.getByLabel('Email').fill('user@example.com');
await page.getByLabel('Hasło').fill('password');
await page.getByRole('button', {
name: 'Zaloguj się'
```
}).click();

```ts
await expect(page.getByText('Dashboard')).toBeVisible();
});
```
Test samodzielnie wykonuje wszystkie czynności w przeglądarce. — ## 5. Assertions — weryfikacja wyników

Automatyzacja nie polega wyłącznie na wykonywaniu czynności. Najważniejsza jest

weryfikacja rezultatów.

Playwright wykorzystuje asercje (assertions),
które określają, czego oczekujemy od aplikacji. 

### Przykładowe pytania

- Czy dashboard jest widoczny?
- Czy użytkownik został poprawnie zalogowany?
- Czy produkt pojawił się w koszyku?
- Czy wyświetlono odpowiedni komunikat? 

### Przykład

```ts
await expect(
 page.getByText('Dashboard')
).toBeVisible();
```
Samo wykonanie kliknięcia nie oznacza, że funkcjonalność działa
poprawnie. Musimy jeszcze sprawdzić rezultat. — ## 6. Locators — jak Playwright odnajduje elementy?

Playwright wykorzystuje mechanizm Locatorów do identyfikowania elementów na stronie.

### Najważniejsze metody

- getByRole() — wyszukiwanie na podstawie roli dostępności, np.
```ts
button.
```
- getByLabel() — wyszukiwanie na podstawie etykiety formularza.
- getByText() — wyszukiwanie na podstawie widocznego tekstu.
- getByTestId() — wyszukiwanie na podstawie jawnie zdefiniowanego
```ts
identyfikatora testowego. 
```
### Przykłady

```ts
page.getByRole('button', { name: 'Zaloguj się' });
page.getByLabel('Adres e-mail');
page.getByText('Witaj użytkowniku')
```
Odwoływanie się do roli, nazwy i etykiety sprawia, że testy są
czytelniejsze i mniej zależne od zmian struktury HTML. — ## 7. Auto-waiting — automatyczne oczekiwanie

Playwright automatycznie czeka, aż element będzie gotowy do wykonania danej akcji.

Przykład: aplikacja wysyła zapytanie do API, odpowiedź przychodzi po
dwóch sekundach i dopiero wtedy na stronie pojawia się przycisk. Nie
trzeba stosować sztucznych opóźnień

```ts
await page.waitForTimeout(5000);
```
Zamiast tego Playwright sprawdza, czy element istnieje w DOM, jest
widoczny, włączony i stabilny oraz czy może zostać użyty. 

### Korzyści

- Mniej sztucznych opóźnień.
- Większa niezawodność testów.
- Krótszy czas wykonywania.
- Mniejsza liczba przypadkowych błędów. — ## 8. Browser Isolation — izolacja przeglądarki

Każdy test może otrzymać własny Browser Context — odizolowaną sesję przeglądarki.

### Każdy kontekst posiada własne

- Cookies.
- Local Storage.
- Session Storage.
- Stan uwierzytelnienia.

Przykładowo: Test A — pierwszy użytkownik;
```ts
Test B — drugi użytkownik; Test C — użytkownik niezalogowany.
Testy nie muszą wpływać na siebie nawzajem.
```
### Ponowne
```ts
wykorzystanie logowania
```
Playwright pozwala zalogować się raz, zapisać stan uwierzytelnienia i
wykorzystać go w kolejnych testach, np. z pliku storageState.json.
Dzięki temu nie trzeba wykonywać logowania przed każdym testem. — ## 9. Network Mocking — kontrolowanie komunikacji z API

Szczególnie przydatna funkcjonalność dla developerów frontendowych. Nie zawsze

możemy przetestować wszystkie sytuacje na prawdziwym backendzie. 

### Przykładowe scenariusze

- Co się stanie, gdy płatność zostanie odrzucona?
- Jak aplikacja zachowa się przy błędzie serwera?
- Co pokaże użytkownikowi, gdy API odpowie z opóźnieniem? Playwright
```ts
pozwala przechwytywać zapytania sieciowe i kontrolować odpowiedzi za
pomocą page.route(). 
```
### Przykład

```ts
await page.route('**/api/payment', async route => {
 await route.fulfill({
 status: 400,
 contentType: 'applica
```
### Co możemy testować?

- Poprawną lub odrzuconą płatność.
- Błędy API, wolne odpowiedzi i niedostępność serwera.

Możemy zwrócić
```ts
własne dane zamiast komunikować się z prawdziwym API.
``` — ## 10. API Testing — testowanie API bez przeglądarki

Playwright umożliwia również bezpośrednie testowanie API REST. Nie musimy otwierać

przeglądarki ani wykonywać interakcji z interfejsem użytkownika. Możemy
wysyłać żądania HTTP bezpośrednio do backendu i sprawdzać odpowiedzi.

### Co możemy testować?

- GET — pobieranie danych; POST — tworzenie zasobów.
- PUT / PATCH — aktualizowanie danych; DELETE — usuwanie zasobów.
- Kody odpowiedzi HTTP i strukturę JSON.
- Autoryzację, uwierzytelnianie, walidację danych i obsługę błędów.
 

### Przykład — pobieranie użytkowników

```ts
import { test, expect } from '@playwright/test';

test('pobieranie użytkowników z API', async ({ request }) => {
 con
```
### Przykład — tworzenie użytkownika

```ts
test('tworzenie użytkownika przez API', async ({ request }) => {
 const response = await request.post(
 'https://ap
```
API Testing to bezpośrednie testowanie backendu; Network Mocking to
przechwytywanie i zastępowanie odpowiedzi obsługiwanych przez aplikację. — ## 11. Parallel Execution — wykonywanie testów równolegle

Playwright umożliwia równoległe wykonywanie niezależnych testów z wykorzystaniem

workerów. 

### Korzyści

- Krótszy czas całej regresji.

- Lepsze wykorzystanie zasobów.

- Możliwość skalowania testów.

- Niezależne wykonywanie scenariuszy. 

### Raportowanie błędów

- Screenshot — zrzut ekranu.

- Video — nagranie przebiegu testu.

- Trace — szczegółowy zapis przebiegu testu. Trace pozwala odtworzyć
```ts
przebieg testu i sprawdzić, co dokładnie wydarzyło się na każdym
etapie. Dostępny jest również raport pokazujący wynik poszczególnych
testów.
``` — ## 12. Integracja z CI/CD

Playwright można zintegrować z pipeline'em CI/CD. Przykładowy proces

1. Developer wypycha kod do repozytorium.
2. CI uruchamia pipeline.
3. Budowana jest aplikacja.
4. Uruchamiane jest środowisko testowe.
5. Playwright uruchamia przeglądarki lub testy API.
6. Wykonywane są testy i asercje.
7. Generowane są raporty oraz trace'y.
8. Pipeline podejmuje decyzję o dalszym wdrożeniu. Jeżeli krytyczne
```ts
testy przejdą pomyślnie — można kontynuować wdrożenie. Jeżeli
zakończą się błędem — pipeline powinien zatrzymać wdrożenie.
``` — ## 13. Jak wygląda typowy przebieg pipeline'u?

Przykładowy scenariusz CI/CD: Etap Opis

1. Push Developer wysyła zmiany do repozytorium.
2. CI Start Automatycznie uruchamia się pipeline.
3. Build Budowana jest aplikacja.
4. Environment Uruchamiane jest środowisko testowe.
5. Playwright Uruchamiane są testy UI, E2E i API.
6. Assertions Weryfikowane są oczekiwane rezultaty.
7. Reports Generowane są raporty, screenshoty i trace'y.
8. Decision Pipeline decyduje, czy wdrożenie może być kontynuowane.
 

### Rezultat

- Wszystkie krytyczne testy zaliczone — wdrażamy.
- Krytyczny test niezaliczony — zatrzymujemy wdrożenie. — ## 14. Gdzie Playwright pasuje w strategii testowania?

Playwright nie powinien zastępować wszystkich pozostałych rodzajów testów.

### 1. Unit Tests — testy jednostkowe

- Sprawdzają pojedyncze funkcje i metody; są szybkie i testują małe,
```ts
odizolowane fragmenty kodu.
```
### 2. Integration Tests — testy
```ts
integracyjne
```
- Sprawdzają współpracę kilku komponentów i komunikację między
```ts
elementami systemu. 
```
### 3. End-to-End Tests — testy E2E

- Sprawdzają kompletną ścieżkę użytkownika i krytyczne procesy
```ts
biznesowe.
```
Playwright może wspierać testowanie API, integracji oraz
```ts
krytycznych ścieżek E2E.
```
Różne poziomy testów powinny się
```ts
uzupełniać, a nie wzajemnie zastępować.
``` — ## 15. Najważniejsze wnioski

Playwright to nie tylko narzędzie, które automatycznie klika w przeglądarce.

### To kompleksowy framework pozwalający

- Automatyzować scenariusze użytkownika.
- Testować API bez uruchamiania przeglądarki.
- Weryfikować poprawność działania aplikacji i testować wiele silników
```ts
przeglądarek.
```
- Automatycznie oczekiwać na gotowość elementów i izolować sesje
```ts
testowe.
```
- Mockować komunikację z API.
- Wykonywać testy równolegle.
- Zbierać dowody błędów i odtwarzać ich przebieg.
- Integrować testy z CI/CD i zatrzymywać wdrożenia, gdy krytyczne
```ts
testy nie przechodzą.
```
Playwright pozwala testować aplikację na
```ts
różnych poziomach — od bezpośredniej komunikacji z API, przez
integrację komponentów, aż po pełne scenariusze użytkownika w
przeglądarce.
```
