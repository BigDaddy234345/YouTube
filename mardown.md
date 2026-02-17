## 1. Architektura Systemu (Zgodnie z wytycznymi)
Twoja aplikacja będzie łączyć kilka nowoczesnych podejść, aby działać płynnie i profesjonalnie:

* MVC (Model-View-Controller): To fundament Twojego PHP.

Model: Obsługuje bazę MySQL (pobieranie filmów, zapisywanie lajków).

View: Pliki HTML/CSS wyświetlające interfejs użytkownika.

Controller: Logika w PHP, która decyduje, co zrobić, gdy użytkownik kliknie "szukaj".

* SPA (Single Page Application): Dzięki JavaScript (Fetch API), użytkownik może przełączać filmy bez przeładowywania całej strony. Pasek boczny i wyszukiwarka zostają na miejscu, zmienia się tylko odtwarzacz.

* REST API: Twój backend w PHP będzie działał jako punkt końcowy (endpoint). JavaScript będzie wysyłał zapytania do np. api/get_videos.php, a serwer odpowie danymi, które JS dynamicznie wstawi do HTML.

* SSR (Server Side Rendering): Pierwsze ładowanie strony (np. strona główna z 100 filmami) zostanie wygenerowane bezpośrednio przez PHP, co przyspieszy indeksowanie i start aplikacji.

* Monolit: Całość (frontend i backend) będzie znajdować się w jednym repozytorium/projekcie, co ułatwi Ci zarządzanie bazą MySQL i plikami PHP.



## 2. Funkcjonalności Frontendu (HTML, CSS, JS)

Skupimy się na tym, aby strona wyglądała i działała jak oryginał:

* **Dynamiczny Grid:** Za pomocą CSS Grid lub Flexbox stworzysz responsywną siatkę filmów. JavaScript będzie pobierać dane z PHP i generować karty filmów automatycznie.
* **Pasek boczny (Sidebar):** Składane menu z kategoriami (Muzyka, Gry, Live), które filtrują filmy bez przeładowania całej strony (używając technologii AJAX/Fetch).

---

## 3. Zaawansowane Wyszukiwanie i Historia

Skoro chcesz, aby strona pamiętała wyszukiwania do czasu resetu:

* **Mechanizm działania:** Gdy użytkownik wpisze frazę w wyszukiwarkę, JS wysyła tę informację do bazy danych (przez PHP).
* **Wyświetlanie:** Pod paskiem wyszukiwania pojawi się lista "Ostatnio szukane".
* **Sesja:** Wykorzystamy `session_start()` w PHP. Historia będzie żyła tak długo, jak długo otwarta jest sesja przeglądarki. Po zamknięciu karty lub resecie, historia może zostać wyczyszczona.

---

## 4. Struktura plików projektu

Twój projekt powinien wyglądać mniej więcej tak:

| Plik/Folder | Rola |
| --- | --- |
| `index.php` | Główna struktura HTML i pętla wyświetlająca filmy. |
| `style.css` | Design (tryb ciemny, układ YouTube, animacje). |
| `script.js` | Obsługa wyszukiwarki, historia, interakcje użytkownika. |
| `db_connect.php` | Konfiguracja połączenia z MySQL (PDO lub mysqli). |
| `get_videos.php` | Skrypt PHP zwracający dane o filmach w formacie JSON dla JavaScriptu. |

---

## 5. Co dodać, żeby projekt "urywał głowę"?

1. **System rekomendacji:** Prosty algorytm w PHP, który pokazuje "podobne filmy" na podstawie kategorii aktualnie oglądanego wideo.
2. **Licznik wyświetleń:** Każde kliknięcie w film wysyła zapytanie do MySQL: `UPDATE videos SET views = views + 1`.


## 6. Interakcje Użytkownika (Co można robić?)
Aby Twoja „podróba” była angażująca, użytkownik musi mieć realny wpływ na to, co widzi. Oto 5 kluczowych akcji:

 * System Polubień (Lajki): Użytkownik może kliknąć „kciuk w górę”. Dzięki PHP i MySQL, liczba lajków zostanie zapisana w bazie danych i nie zniknie po odświeżeniu strony.
  
 * Sekcja Komentarzy: Pod każdym z 100+ filmów użytkownik może zostawić komentarz. PHP będzie odbierać tekst z formularza i dopisywać go do tabeli comments w bazie.
  
 * Dynamiczne Filtrowanie: Użytkownik klika w „tagi” na górze strony (np. Muzyka, Sport, Kodowanie), a JavaScript bez przeładowania strony (AJAX) prosi PHP o filmy tylko z tej kategorii.
  
 * Tryb Kinowy / Ciemny: Przełącznik w JS, który zmienia style CSS (z jasnego na ciemny) i zapamiętuje wybór użytkownika w localStorage.

 * Licznik Wyświetleń: Za każdym razem, gdy ktoś wejdzie w dany film, skrypt PHP wykona polecenie UPDATE, zwiększając licznik o jeden.