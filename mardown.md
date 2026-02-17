
## 1. Architektura Systemu (Backend & Baza Danych)

Zamiast trzymać dane o filmach w kodzie JavaScript, stworzymy relacyjną bazę danych.

* **MySQL (Baza danych):** Potrzebujesz przynajmniej dwóch głównych tabel:
* `videos`: (id, title, description, thumbnail_url, video_url, category, views, upload_date).
* `search_history`: (id, query, timestamp) – dla funkcji zapamiętywania wyszukiwań.


* **PHP (Silnik):** Będzie pośrednikiem. Skrypt PHP połączy się z bazą danych, pobierze listę 100+ filmów i "wypluje" je do Twojego frontendu w formacie gotowym do wyświetlenia.

---

## 2. Funkcjonalności Frontendu (HTML, CSS, JS)

Skupimy się na tym, aby strona wyglądała i działała jak oryginał:

* **Dynamiczny Grid:** Za pomocą CSS Grid lub Flexbox stworzysz responsywną siatkę filmów. JavaScript będzie pobierać dane z PHP i generować karty filmów automatycznie.
* **Odtwarzacz (Video Player):** Własny kontener na wideo z niestandardowymi kontrolkami (play/pause, pasek postępu) napisanymi w JS.
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
3. **Wyszukiwanie "Live":** Wyniki wyszukiwania zmieniają się już w trakcie pisania (podpowiedzi).



## 6. Interakcje Użytkownika (Co można robić?)
Aby Twoja „podróba” była angażująca, użytkownik musi mieć realny wpływ na to, co widzi. Oto 5 kluczowych akcji:

 * System Polubień (Lajki): Użytkownik może kliknąć „kciuk w górę”. Dzięki PHP i MySQL, liczba lajków zostanie zapisana w bazie danych i nie zniknie po odświeżeniu strony.
  
 * Sekcja Komentarzy: Pod każdym z 100+ filmów użytkownik może zostawić komentarz. PHP będzie odbierać tekst z formularza i dopisywać go do tabeli comments w bazie.
  
 * Dynamiczne Filtrowanie: Użytkownik klika w „tagi” na górze strony (np. Muzyka, Sport, Kodowanie), a JavaScript bez przeładowania strony (AJAX) prosi PHP o filmy tylko z tej kategorii.
  
 * Tryb Kinowy / Ciemny: Przełącznik w JS, który zmienia style CSS (z jasnego na ciemny) i zapamiętuje wybór użytkownika w localStorage.

 * Licznik Wyświetleń: Za każdym razem, gdy ktoś wejdzie w dany film, skrypt PHP wykona polecenie UPDATE, zwiększając licznik o jeden.