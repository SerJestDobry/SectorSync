# 🌐 SectorSync


Plugin do Spigota/Paper (Minecraft 1.21.6), który dzieli graczy pomiędzy wiele instancji serwera ("sektorów") i synchronizuje ich dane (ekwipunek, statystyki, lokalizację) przez Redis.

---

> [!WARNING]
> **Projekt jest obecnie aktywnie rozwijany.**
>
> ⚠️ Niektóre funkcje mogą być niekompletne lub niestabilne.
> 
> ❌ Nie używaj tej wersji na głównym/produkcyjnym serwerze.


---

## ✨ Funkcję

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

## 🛠️ Konfiguracja (`messagess.yml`)

```yaml
usage:
  main: '&cUżycie: /sectors <list|info|send|remove>'
  unknown-command: '&cNieznana komenda. Dostępne: list, info, send, remove'
  info: '&cUżycie: /sectors info <nazwa sektoru>'
  send: '&cUżycie: /sectors send <gracz> <nazwa sektoru>'
  remove: '&cUżycie: /sectors remove <nazwa sektora>'

errors:
  no-permission: '&cNie masz uprawnień!'
  send-failed: '&cNie udało się przenieść gracza!'
  remove-failed: '&cNie udało się usunąć sektora! Upewnij się że sektor istnieje i nie ma aktywnych graczy.'

list:
  header: '&6Lista sektorów (&a{count}&6):'
  entry: '&e- {sector} &7(Graczy: {count})'

info:
  header: '&6=== Informacje o sektorze &e{sector}&6 ==='
  status: '&7Status: &a{status}'
  tps: '&7TPS: &a{tps}'
  players-online: '&7Graczy online: &a{count}'
  last-update: '&7Ostatnia aktywność: &a{time}'
  players-header: '&7Gracze online:'
  players-entry: '&e- {player}'
  players-more: '&7... i {count} więcej'

success:
  send: '&aPomyślnie przeniesiono gracza {player} do sektora {sector}'
  remove: '&aSektor {sector} został usunięty!'
```

---

## 🎮 Komendy i uprawnienia

| Komenda | Opis | Uprawnienie |
|---|---|---|
| `/sectors list` | Lista wszystkich zarejestrowanych sektorów |  `sectors.list`  |
| `/sectors info <sektor>` | Szczegóły sektora (status, TPS, gracze) |  `sectors.info`  |
| `/sectors send <gracz> <sektor>` | Przeniesienie gracza do innego sektora | `sectors.admin` |
| `/sectors remove <sektor>` | Usunięcie pustego sektora | `sectors.admin` |

---

## 🗺️ Roadmap

- [ ] Transfer graczy między fizycznie osobnymi serwerami (BungeeCord/Velocity)
- [ ] Watchdog wykrywający awarię sektora i automatyczny failover graczy
- [ ] Dokładniejszy pomiar TPS

---

## 📄 Licencja
