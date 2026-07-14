# 🌐 SectorSync

Plugin do Spigota/Paper (Minecraft 1.21.6), który dzieli graczy pomiędzy wiele instancji serwera ("sektorów") i synchronizuje ich dane (ekwipunek, statystyki, lokalizację) przez Redis.

---

> [!WARNING]
> **Projekt jest obecnie aktywnie rozwijany.**
>
> ⚠️ Niektóre funkcje mogą być niekompletne lub niestabilne.
> ❌ Nie używaj tej wersji na głównym/produkcyjnym serwerze.
> ✅ Używaj wyłącznie do testów i developmentu.

---

## ✨ Features

- 🟧 Przenoszenie graczy między sektorami z zachowaniem stanu (ekwipunek, HP, XP, efekty)
- 🔵 Synchronizacja danych gracza w czasie rzeczywistym przez Redis
- 🟠 Współdzielone i synchronizowane informacje o sektorach (status, TPS, liczba graczy)
- 💬 Panel administracyjny (`/sectors`) do zarządzania sektorami

---

## 📦 Wymagania

- ☕ Java 21+
- 🧱 Spigot / Paper 1.21.6
- 🗄️ Serwer Redis (lokalny lub w sieci wewnętrznej)

---

## ⚙️ Instalacja

1. Zbuduj plugin (`mvn package` / `gradle build`) lub pobierz gotowy `.jar`.
2. Wrzuć plik `.jar` do folderu `plugins/` na każdym serwerze-sektorze.
3. Uruchom serwer, aby wygenerował się `config.yml`.
4. Skonfiguruj `config.yml` — w szczególności dane Redis i unikalną nazwę sektora dla każdego serwera.
5. Zrestartuj serwer.

---

## 🛠️ Konfiguracja (`config.yml`)

```yaml
sectors:
  name: 'sektor_01'        # unikalna nazwa sektora dla tego serwera
  tps-warning: 15.0        # próg TPS, poniżej którego sektor oznaczany jest jako "warning"
  max-players: 200
  auto-register: true

redis:
  host: 'localhost'
  port: 6379
  password: ''             # zalecane ustawienie hasła w środowisku produkcyjnym
  timeout: 5000
```

> [!CAUTION]
> Redis powinien być zabezpieczony hasłem i niedostępny publicznie (firewall / sieć wewnętrzna). Instancja bez hasła w środowisku produkcyjnym naraża dane wszystkich graczy.

---

## 🎮 Komendy i uprawnienia

| Komenda | Opis | Uprawnienie |
|---|---|---|
| `/sectors list` | Lista wszystkich zarejestrowanych sektorów | brak |
| `/sectors info <sektor>` | Szczegóły sektora (status, TPS, gracze) | brak |
| `/sectors send <gracz> <sektor>` | Przeniesienie gracza do innego sektora | `sectors.admin` |
| `/sectors remove <sektor>` | Usunięcie pustego sektora | `sectors.admin` |

---

## 🗺️ Roadmap

- [ ] Transfer graczy między fizycznie osobnymi serwerami (BungeeCord/Velocity)
- [ ] Watchdog wykrywający awarię sektora i automatyczny failover graczy
- [ ] Dokładniejszy pomiar TPS

---

## 📄 Licencja

Do uzupełnienia (np. MIT).
