# 👻 Moduł Bezpieczeństwa Ghost
**Narzędzie do wzmacniania bezpieczeństwa Windows i Azure oparte na PowerShell**

> **Proaktywne wzmacnianie bezpieczeństwa dla punktów końcowych Windows i środowisk Azure.** Ghost zapewnia funkcje wzmacniania oparte na PowerShell, które mogą pomóc w redukcji popularnych wektorów ataków poprzez wyłączanie niepotrzebnych usług i protokołów.

## ⚠️ Ważne ostrzeżenia

**TESTOWANIE WYMAGANE**: Zawsze najpierw testuj Ghost w środowiskach nieprodukcyjnych. Wyłączanie usług może wpłynąć na legitymne funkcje biznesowe.

**BRAK GWARANCJI**: Chociaż Ghost celuje w popularne wektory ataków, żadne narzędzie bezpieczeństwa nie może zapobiec wszystkim atakom. To jeden komponent w kompleksowej strategii bezpieczeństwa.

**WPŁYW OPERACYJNY**: Niektóre funkcje mogą wpłynąć na funkcjonalność systemu. Dokładnie przejrzyj każde ustawienie przed wdrożeniem.

**OCENA PROFESJONALNA**: W środowiskach produkcyjnych skonsultuj się ze specjalistami ds. bezpieczeństwa, aby upewnić się, że ustawienia są zgodne z potrzebami organizacji.

## 📊 Krajobraz Bezpieczeństwa

Szkody ransomware osiągnęły **57 miliardów dolarów w 2025 roku**, badania pokazują, że wiele udanych ataków wykorzystuje podstawowe usługi Windows i błędne konfiguracje. Popularne wektory ataków obejmują:

- **90% incydentów ransomware** dotyczy wykorzystania RDP
- **Podatności SMBv1** umożliwiły ataki takie jak WannaCry i NotPetya
- **Makra dokumentów** pozostają główną metodą dostarczania malware
- **Ataki oparte na USB** nadal celują w sieci air-gap
- **Nadużycia PowerShell** znacznie wzrosły w ostatnich latach

## 🛡️ Funkcje Bezpieczeństwa Ghost

Ghost zapewnia **16 funkcji wzmacniania Windows** plus **integrację bezpieczeństwa Azure**:

### Wzmacnianie punktów końcowych Windows

| Funkcja | Cel | Uwagi |
|----------|---------|----------------|
| `Set-RDP` | Zarządza dostępem Remote Desktop | Może wpłynąć na zdalne administrowanie |
| `Set-SMBv1` | Kontroluje starszy protokół SMB | Wymagany dla bardzo starych systemów |
| `Set-AutoRun` | Kontroluje AutoPlay/AutoRun | Może wpłynąć na wygodę użytkownika |
| `Set-USBStorage` | Ogranicza urządzenia pamięci USB | Może wpłynąć na legitymne użycie USB |
| `Set-Macros` | Kontroluje wykonywanie makr Office | Może wpłynąć na dokumenty z włączonymi makrami |
| `Set-PSRemoting` | Zarządza zdalnym PowerShell | Może wpłynąć na zdalne zarządzanie |
| `Set-WinRM` | Kontroluje Windows Remote Management | Może wpłynąć na zdalne administrowanie |
| `Set-LLMNR` | Zarządza protokołem rozwiązywania nazw | Zwykle bezpieczne do wyłączenia |
| `Set-NetBIOS` | Kontroluje NetBIOS przez TCP/IP | Może wpłynąć na starsze aplikacje |
| `Set-AdminShares` | Zarządza udziałami administracyjnymi | Może wpłynąć na zdalny dostęp do plików |
| `Set-Telemetry` | Kontroluje zbieranie danych | Może wpłynąć na możliwości diagnostyczne |
| `Set-GuestAccount` | Zarządza kontem gościa | Zwykle bezpieczne do wyłączenia |
| `Set-ICMP` | Kontroluje odpowiedzi ping | Może wpłynąć na diagnostykę sieci |
| `Set-RemoteAssistance` | Zarządza Remote Assistance | Może wpłynąć na operacje help desk |
| `Set-NetworkDiscovery` | Kontroluje wykrywanie sieci | Może wpłynąć na przeglądanie sieci |
| `Set-Firewall` | Zarządza Windows Firewall | Krytyczne dla bezpieczeństwa sieci |

### Bezpieczeństwo chmury Azure

| Funkcja | Cel | Wymagania |
|----------|---------|--------------|
| `Set-AzureSecurityDefaults` | Włącza podstawowe bezpieczeństwo Azure AD | Uprawnienia Microsoft Graph |
| `Set-AzureConditionalAccess` | Konfiguruje zasady dostępu | Licencjonowanie Azure AD P1/P2 |
| `Set-AzurePrivilegedUsers` | Audytuje konta uprzywilejowane | Uprawnienia Global Admin |

### Opcje wdrażania korporacyjnego

| Metoda | Przypadek użycia | Wymagania |
|--------|----------|--------------|
| **Bezpośrednie wykonanie** | Testowanie, małe środowiska | Prawa lokalnego administratora |
| **Group Policy** | Środowiska domenowe | Administrator domeny, zarządzanie GP |
| **Microsoft Intune** | Urządzenia zarządzane w chmurze | Licencjonowanie Intune, Graph API |

## 🚀 Szybki start

### Ocena bezpieczeństwa
```powershell
# Załaduj moduł Ghost
Invoke-WebRequest 'https://raw.githubusercontent.com/jimrtyler/Ghost/main/Ghost.ps1' -OutFile .\Ghost.ps1
Get-Content .\Ghost.ps1
. .\Ghost.ps1

# Sprawdź aktualną postawę bezpieczeństwa
Get-Ghost
```

### Podstawowe wzmacnianie (najpierw testuj)
```powershell
# Podstawowe wzmacnianie - najpierw testuj w środowisku laboratoryjnym
Set-Ghost -SMBv1 -AutoRun -Macros

# Przejrzyj zmiany
Get-Ghost
```

### Wdrażanie korporacyjne
```powershell
# Wdrażanie Group Policy (środowiska domenowe)
Set-Ghost -SMBv1 -AutoRun -GroupPolicy

# Wdrażanie Intune (urządzenia zarządzane w chmurze)
Set-Ghost -SMBv1 -RDP -USBStorage -Intune
```

## 📋 Metody instalacji

### Opcja 1: Bezpośrednie pobieranie (testowanie)
```powershell
Invoke-WebRequest 'https://raw.githubusercontent.com/jimrtyler/Ghost/main/Ghost.ps1' -OutFile .\Ghost.ps1
Get-Content .\Ghost.ps1
. .\Ghost.ps1
```

### Opcja 2: Instalacja modułu
```powershell
# Instaluj z PowerShell Gallery (gdy dostępne)
Install-Module Ghost -Scope CurrentUser
Import-Module Ghost
```

### Opcja 3: Wdrażanie korporacyjne
```powershell
# Skopiuj do lokalizacji sieciowej dla wdrażania Group Policy
# Skonfiguruj skrypty PowerShell Intune dla wdrażania w chmurze
```

## 💼 Przykłady przypadków użycia

### Mały biznes
```powershell
# Podstawowa ochrona z minimalnym wpływem
Set-Ghost -SMBv1 -AutoRun -Macros -ICMP
```

### Środowisko opieki zdrowotnej
```powershell
# Wzmacnianie skoncentrowane na HIPAA
Set-Ghost -SMBv1 -RDP -USBStorage -AdminShares -Telemetry
```

### Usługi finansowe
```powershell
# Konfiguracja wysokiego bezpieczeństwa
Set-Ghost -RDP -SMBv1 -AutoRun -USBStorage -Macros -PSRemoting -AdminShares
```

### Organizacja Cloud-First
```powershell
# Wdrażanie zarządzane przez Intune
Connect-IntuneGhost -Interactive
Set-Ghost -SMBv1 -RDP -AutoRun -Macros -Intune
```

## 🔍 Szczegóły funkcji

### Główne funkcje wzmacniania

#### Usługi sieciowe
- **RDP**: Blokuje dostęp do pulpitu zdalnego lub randomizuje port
- **SMBv1**: Wyłącza starszy protokół udostępniania plików
- **ICMP**: Zapobiega odpowiedziom ping w celach rozpoznawczych
- **LLMNR/NetBIOS**: Blokuje starsze protokoły rozwiązywania nazw

#### Bezpieczeństwo aplikacji
- **Makra**: Wyłącza wykonywanie makr w aplikacjach Office
- **AutoRun**: Zapobiega automatycznemu wykonywaniu z nośników wymiennych

#### Zdalne zarządzanie
- **PSRemoting**: Wyłącza sesje zdalne PowerShell
- **WinRM**: Zatrzymuje Windows Remote Management
- **Remote Assistance**: Blokuje połączenia zdalnej pomocy

#### Kontrola dostępu
- **Admin Shares**: Wyłącza udziały C$, ADMIN$
- **Guest Account**: Wyłącza dostęp do konta gościa
- **USB Storage**: Ogranicza użycie urządzeń USB

### Integracja Azure
```powershell
# Połącz się z dzierżawą Azure
Connect-AzureGhost -Interactive

# Włącz domyślne ustawienia bezpieczeństwa
Set-AzureSecurityDefaults -Enable

# Konfiguruj dostęp warunkowy
Set-AzureConditionalAccess -BlockLegacyAuth -RequireMFA

# Audytuj użytkowników uprzywilejowanych
Set-AzurePrivilegedUsers -AuditOnly
```

### Integracja Intune (nowe w v2)
```powershell
# Połącz się z Intune
Connect-IntuneGhost -Interactive

# Wdrażaj poprzez zasady Intune
Set-IntuneGhost -Settings @{
    RDP = $true
    SMBv1 = $true
    USBStorage = $true
    Macros = $true
}
```

## ⚠️ Ważne uwagi

### Wymagania testowe
- **Środowisko laboratoryjne**: Najpierw testuj wszystkie ustawienia w izolowanym środowisku
- **Stopniowe wdrażanie**: Wdrażaj stopniowo, aby zidentyfikować problemy
- **Plan cofnięcia**: Upewnij się, że możesz cofnąć zmiany w razie potrzeby
- **Dokumentacja**: Zapisuj, które ustawienia działają w twoim środowisku

### Potencjalny wpływ
- **Produktywność użytkowników**: Niektóre ustawienia mogą wpłynąć na codzienne przepływy pracy
- **Starsze aplikacje**: Starsze systemy mogą wymagać określonych protokołów
- **Dostęp zdalny**: Rozważ wpływ na legitymne zdalne administrowanie
- **Procesy biznesowe**: Sprawdź, czy ustawienia nie psują krytycznych funkcji

### Ograniczenia bezpieczeństwa
- **Obrona w głębi**: Ghost to jedna warstwa bezpieczeństwa, nie kompletne rozwiązanie
- **Ciągłe zarządzanie**: Bezpieczeństwo wymaga ciągłego monitorowania i aktualizacji
- **Szkolenie użytkowników**: Kontrola techniczna musi być sparowana ze świadomością bezpieczeństwa
- **Ewolucja zagrożeń**: Nowe metody ataków mogą ominąć obecną ochronę

## 🎯 Przykłady scenariuszy ataków

Chociaż Ghost celuje w popularne wektory ataków, specyficzna prewencja zależy od właściwej implementacji i testowania:

### Ataki w stylu WannaCry
- **Łagodzenie**: `Set-Ghost -SMBv1` wyłącza podatny protokół
- **Uwagi**: Upewnij się, że żaden starszy system nie wymaga SMBv1

### Ransomware oparte na RDP
- **Łagodzenie**: `Set-Ghost -RDP` blokuje dostęp do pulpitu zdalnego
- **Uwagi**: Może wymagać alternatywnych metod dostępu zdalnego

### Malware oparte na dokumentach
- **Łagodzenie**: `Set-Ghost -Macros` wyłącza wykonywanie makr
- **Uwagi**: Może wpłynąć na legitymne dokumenty z włączonymi makrami

### Zagrożenia dostarczane przez USB
- **Łagodzenie**: `Set-Ghost -USBStorage -AutoRun` ogranicza funkcjonalność USB
- **Uwagi**: Może wpłynąć na legitymne użycie urządzeń USB

## 🏢 Funkcje korporacyjne

### Wsparcie Group Policy
```powershell
# Zastosuj ustawienia poprzez rejestr Group Policy
Set-Ghost -SMBv1 -RDP -AutoRun -GroupPolicy

# Ustawienia obowiązują w całej domenie po odświeżeniu GP
gpupdate /force
```

### Integracja Microsoft Intune
```powershell
# Utwórz zasady Intune dla ustawień Ghost
Set-IntuneGhost -Settings $GhostSettings -Interactive

# Zasady są automatycznie wdrażane na zarządzanych urządzeniach
```

### Raportowanie zgodności
```powershell
# Generuj raport oceny bezpieczeństwa
Get-Ghost | Export-Csv -Path "SecurityAudit-$(Get-Date -Format 'yyyy-MM-dd').csv"

# Raport postawy bezpieczeństwa Azure
Get-AzureGhost | Out-File "AzureSecurityReport.txt"
```

## 📚 Najlepsze praktyki

### Przed wdrożeniem
1. **Dokumentuj aktualny stan**: Uruchom `Get-Ghost` przed zmianami
2. **Testuj dokładnie**: Waliduj w środowisku nieprodukcyjnym
3. **Planuj cofnięcie**: Wiedz, jak cofnąć każde ustawienie
4. **Przegląd interesariuszy**: Upewnij się, że jednostki biznesowe zatwierdzają zmiany

### Podczas wdrażania
1. **Podejście stopniowe**: Najpierw wdrażaj do grup pilotażowych
2. **Monitoruj wpływ**: Obserwuj skargi użytkowników lub problemy systemowe
3. **Dokumentuj problemy**: Zapisuj wszelkie problemy dla przyszłego odniesienia
4. **Komunikuj zmiany**: Informuj użytkowników o ulepszeniach bezpieczeństwa

### Po wdrożeniu
1. **Regularna ocena**: Okresowo uruchamiaj `Get-Ghost` do weryfikacji ustawień
2. **Aktualizuj dokumentację**: Utrzymuj aktualne konfiguracje bezpieczeństwa
3. **Przegląd skuteczności**: Monitoruj incydenty bezpieczeństwa
4. **Ciągłe ulepszanie**: Dostosowuj ustawienia na podstawie krajobrazu zagrożeń

## 🔧 Rozwiązywanie problemów

### Typowe problemy
- **Błędy uprawnień**: Upewnij się o podwyższonej sesji PowerShell
- **Zależności usług**: Niektóre usługi mogą mieć zależności
- **Kompatybilność aplikacji**: Testuj z aplikacjami biznesowymi
- **Łączność sieciowa**: Sprawdź, czy dostęp zdalny nadal działa

### Opcje odzyskiwania
```powershell
# Ponownie włącz określone usługi w razie potrzeby
Set-RDP -Enable
Set-SMBv1 -Enable
Set-AutoRun -Enable
Set-Macros -Enable
```

## 👨‍💻 O autorze

**Jim Tyler** - Microsoft MVP dla PowerShell
- **YouTube**: [@PowerShellEngineer](https://youtube.com/@PowerShellEngineer) (10,000+ subskrybentów)
- **Newsletter**: [PowerShell.News](https://powershell.news) - Tygodniowy wywiad bezpieczeństwa
- **Autor**: "PowerShell for Systems Engineers"
- **Doświadczenie**: Dekady automatyzacji PowerShell i bezpieczeństwa Windows

## 📄 Licencja i zrzeczenie się odpowiedzialności

### Licencja MIT
Ghost jest dostarczany na licencji MIT do bezpłatnego użytku, modyfikacji i dystrybucji.

### Zrzeczenie się odpowiedzialności bezpieczeństwa
- **Brak gwarancji**: Ghost jest dostarczany "jak jest" bez gwarancji jakiegokolwiek rodzaju
- **Testowanie wymagane**: Zawsze testuj w środowiskach nieprodukcyjnych najpierw
- **Wskazówki profesjonalne**: Skonsultuj się ze specjalistami ds. bezpieczeństwa dla wdrożeń produkcyjnych
- **Wpływ operacyjny**: Autorzy nie są odpowiedzialni za jakiekolwiek zakłócenia operacyjne
- **Kompleksowe bezpieczeństwo**: Ghost to jeden komponent w kompletnej strategii bezpieczeństwa

### Wsparcie
- **GitHub Issues**: [Zgłoś błędy lub poproś o funkcje](https://github.com/jimrtyler/Ghost/issues)
- **Dokumentacja**: Użyj `Get-Help <function> -Full` dla szczegółowej pomocy
- **Społeczność**: Fora społeczności PowerShell i bezpieczeństwa

---

**🔒 Wzmocnij swoją postawę bezpieczeństwa z Ghost - ale zawsze najpierw testuj.**

```powershell
# Zacznij od oceny, nie od założeń
Get-Ghost
```

**⭐ Daj gwiazdkę temu repozytorium, jeśli Ghost pomaga poprawić twoją postawę bezpieczeństwa!**