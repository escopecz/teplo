# Heating ROI Calculator (Interactive Web App)

Tento dokument slouží jako zadání pro vytvoření interaktivní webové kalkulačky návratnosti investic do vytápění. Aplikace bude čistě klientská (Client-side JS), bez nutnosti backendu.

## 🛠 Technický zásobník
- **Styling:** Tailwind CSS (přes CDN pro jednoduchost).
- **Logika:** Vanilla JavaScript (ES6+).
- **Grafy:** Chart.js (CDN).
- **Ikony:** Lucide-icons nebo FontAwesome.

---

## 🏗 Fáze 1: UI a Moderní Layout
Vytvořit responzivní a moderní rozhraní s důrazem na přehlednost.

- [ ] **1.1 Layout:** Centrální kontejner s "glassmorphism" efektem.
- [ ] **1.2 Form:** Horní sekce s parametry objektu (grid layout):
    - Plocha (m²) - Input number (Default: 80).
    - Zateplení stropu - Checkbox (Default: false).
    - Zateplení stěn - Checkbox (Default: false).
    - Okna - Toggle (Stará / Trojskla, Default: Trojskla).
    - Horizont (Počet let) - Slider/Number (Default: 10).
- [ ] **1.3 Chart Area:** Velký kontejner pro `canvas` (Chart.js).
- [ ] **1.4 Table Area:** Sekce pod grafem pro detailní numerické srovnání.

---

## 🧮 Fáze 2: Physics Engine (Tepelné ztráty)
Implementovat logiku pro výpočet kW ztráty objektu.

- [ ] **2.1 Součinitelé (U):**
    - Stěna (cihla 45cm): 1.45 | Zateplená: 0.25
    - Strop (původní): 1.20 | Zateplený (vata): 0.18
    - Okna (stará): 2.40 | Trojskla: 0.85
- [ ] **2.2 Výpočetní funkce:**
    - `calculateHeatLoss(params)`: Spočítá ztrátu v kW (uvažuj fixní parametry: výška 2.6m, Plzeň ΔT=32K).
    - `getAnnualEnergyNeed(losskW)`: Přepočet na kWh/rok (uvažuj 20 dní na 22°C + zbytek sezóny temperování na 10°C = cca 1500 topných hodin ekvivalentu plného výkonu).

---

## 💰 Fáze 3: Economic Engine (ROI Logika)
Výpočet kumulativních nákladů pro jednotlivé zdroje.

- [ ] **3.1 Data zdrojů (Defaultní investice):**
    - **Plynový kotel:** 100,000 Kč | Palivo: 2.5 Kč/kWh | Účinnost: 0.95 | Servis: 4,000 Kč/rok.
    - **Elektrokotel:** 30,000 Kč | Palivo: 4.5 Kč/kWh | Účinnost: 0.99 | Servis: 500 Kč/rok.
    - **TČ (Vzduch-Voda):** 269,686 Kč | Palivo: 4.5 Kč/kWh | SCOP: 3.0 | Servis: 2,500 Kč/rok.
    - **Klimatizace + Bojler:** 144,737 Kč | Palivo: 4.5 Kč/kWh | SCOP: 3.1 | Servis: 2,500 Kč/rok.
- [ ] **3.2 Časová řada:**
    - Funkce generující pole pro každý rok: `Cost = Investice + (Roční_spotřeba * Cena_energie * (1.04^rok)) + (Servis * (1.04^rok))`.
    - Započítat růst cen energií (default 4 % p.a.).

---

## 📊 Fáze 4: Interaktivita a Grafy
Propojení vstupů s vizualizací.

- [ ] **4.1 Chart.js integrace:** - Dataset pro každý zdroj.
    - Osa X: Roky, Osa Y: Kč.
- [ ] **4.2 Real-time Update:** Přidat Event Listenery na všechny inputy, aby graf "reagoval" okamžitě bez reloadu.

---

## 📝 Fáze 5: Tabulka a Dynamické Poznámky
Zobrazení výsledků a doporučení.

- [ ] **5.1 Srovnávací tabulka:** Sloupce: Zdroj, Investice, Náklady po X letech, Celkem.
- [ ] **5.2 Chytré poznámky:**
    - Pokud `ceilingInsulated == false` -> "⚠️ Doporučení: Zateplení stropu vatou (cca 15k Kč) zkrátí návratnost TČ o 3 roky."
    - Pokud `heatSource == 'Elektrokotel'` -> "❗ Varování: Elektrokotel je u nezatepleného objektu extrémně rizikový."
- [ ] **5.3 Export:** Tlačítko pro stažení tabulky do CSV.

---

## 🎯 Cílové hodnoty pro validaci (Baseline):
- Objekt 80m², Trojskla, Bez izolace stropu/stěn, 10 let:
    - Klima by měla být kolem 470k Kč.
    - Plyn kolem 550k Kč.
    - TČ kolem 540k Kč (pokud je vč. TUV).
    - Elektrokotel > 680k Kč.
