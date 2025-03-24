# Specifikacija: Sustav za planiranje avionskih ruta

## Pregled
Sustav za planiranje avionskih ruta osmišljen je za optimizaciju zračnih ruta pomoću algoritama grafova, koristeći JanusGraph za modeliranje zračnih luka i ruta. Podaci o putnicima i rezervacijama upravljaju se putem PostgreSQL-a radi osiguranja učinkovite i pouzdane prodaje karata.

## Arhitektura sustava

### Korištene tehnologije
- **JanusGraph**: Pohranjuje i modelira zračne luke i rute kao graf.
- **PostgreSQL**: Upravljanje podacima o putnicima i rezervacijama.
- **Algoritmi grafova**: Koriste se za pronalaženje najkraćeg puta, optimalnih ruta i alternativnih prijedloga ruta.
- **Backend**: Implementira poslovnu logiku i obradu podataka.
- **Frontend (opcionalno)**: Omogućuje sučelje za upite o rutama i upravljanje rezervacijama.

## Funkcionalni zahtjevi

### Planiranje ruta
1. **Dodavanje zračne luke**: Sustav mora omogućiti dodavanje zračnih luka kao čvorova u JanusGraph.
2. **Definiranje ruta**: Rute se pohranjuju kao veze između čvorova zračnih luka.
3. **Pronalaženje optimalne rute**: Implementacija algoritama najkraćeg puta (npr. Dijkstra, A*).
4. **Alternativne rute**: Pružanje alternativnih ruta u slučaju kašnjenja ili ograničenja.

### Sustav rezervacija
1. **Registracija putnika**: Pohrana podataka o putnicima u PostgreSQL.
2. **Kreiranje rezervacija**: Povezivanje putnika s letovima.
3. **Dohvat rezervacija**: Upit za prošle i buduće rezervacije.
4. **Otkazivanje/izmjena rezervacija**: Omogućavanje izmjena i otkazivanja rezervacija.

## Nefunkcionalni zahtjevi
- **Skalabilnost**: Sustav treba podržavati tisuće letova i rezervacija.
- **Performanse**: Upiti moraju biti optimizirani za rad u stvarnom vremenu.
- **Sigurnost**: Siguran pristup podacima o putnicima i rezervacijama.
- **Integritet podataka**: Osiguravanje dosljednosti između JanusGraph-a i PostgreSQL-a.

## API krajnje točke (primjer)

### Upravljanje rutama (Graf baza podataka)
- `POST /airports` – Dodavanje zračne luke
- `POST /routes` – Definiranje rute između zračnih luka
- `GET /routes?from=<airport>&to=<airport>` – Dohvaćanje najbolje rute

### Upravljanje rezervacijama (SQL baza podataka)
- `POST /passengers` – Registracija putnika
- `POST /bookings` – Kreiranje rezervacije
- `GET /bookings?passenger_id=<id>` – Dohvaćanje rezervacija
- `DELETE /bookings/<id>` – Otkazivanje rezervacije

## Modeli podataka

### JanusGraph (Shema grafa)
#### Tipovi čvorova:
- **Zračna luka** (`id`, `naziv`, `lokacija`)
#### Tipovi veza:
- **Ruta** (`udaljenost`, `aviokompanija`, `trajanje`)

### PostgreSQL (Relacijska shema)
#### Tablice:
- **Putnici** (`id`, `ime`, `email`)
- **Rezervacije** (`id`, `passenger_id`, `flight_id`, `status`)

## Buduća poboljšanja
- Integracija s ažuriranjem statusa letova u stvarnom vremenu.
- Prediktivna analitika za kašnjenja letova.
- Strojno učenje za optimizaciju ruta.

---
Ovaj dokument služi kao temeljna specifikacija za razvoj Sustava za planiranje avionskih ruta, osiguravajući strukturiranu implementaciju i skalabilnost.

