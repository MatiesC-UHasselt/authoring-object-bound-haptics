# Authoring Object-Bound Haptics

Lokale Git-repository van de papersite voor MUM 2026, klaar voor GitHub Pages.
De vier bestaande Sites-versies zijn bewaard in de Git-geschiedenis.

## Bestanden aanpassen

- `dist/index.html`: de pagina, opmaak en interacties. Dit is het bewerkbare bronbestand; er is geen bouwstap.
- `dist/assets/`: afbeeldingen, lettertypen, het paper en de BibTeX-citatie.
- `.github/workflows/pages.yml`: publiceert `dist/` na een push naar `main`.
- `dist/CNAME`: het beoogde domein, `matiesclaesen.be`.

Er zijn geen npm-pakketten, database, API-sleutels of aparte server nodig.
De `.openai/hosting.json` is meegekomen met de export van Sites; de GitHub Pages-workflow gebruikt die niet.

## Lokaal bekijken

Open een terminal in deze map en start:

```sh
python3 -m http.server 8000 --bind 127.0.0.1 --directory dist
```

Open daarna <http://localhost:8000>. Stop de lokale server met Ctrl+C.

## Eenmalig op GitHub zetten

Er is nog geen GitHub-remote ingesteld of online repository aangemaakt.

1. Voeg deze bestaande lokale repository toe in GitHub Desktop via **File → Add Local Repository**.
2. Kies **Publish repository**. Een openbare repository kan GitHub Pages gebruiken met GitHub Free.
3. Open de repository op GitHub: **Settings → Pages → Build and deployment → Source → GitHub Actions**.
4. Start onder **Actions → Publish website → Run workflow** de eerste publicatie. Latere pushes naar `main` publiceren automatisch.

Je kunt ook een lege GitHub-repository maken zonder README of andere bestanden en de aangegeven bestaande-repository-instructies volgen.

## Domein en HTTPS koppelen

Deze lokale voorbereiding koopt of configureert geen domein. Zodra `matiesclaesen.be` geregistreerd is en de site op GitHub Pages staat:

1. Verifieer het domein bij GitHub via **Settings → Pages** van je account en voeg het gevraagde TXT-record toe bij OVH.
2. Stel in **Settings → Pages** van de repository **Custom domain** in op `matiesclaesen.be`. Bij een Actions-publicatie moet dit expliciet in de instellingen; het CNAME-bestand alleen volstaat niet.
3. Stel bij OVH de volgende records voor de website in. Bewaar records voor e-mail en domeinverificatie.

   | Type | Naam | Waarde |
   | --- | --- | --- |
   | A | @ | 185.199.108.153 |
   | A | @ | 185.199.109.153 |
   | A | @ | 185.199.110.153 |
   | A | @ | 185.199.111.153 |
   | CNAME | www | de GitHub-gebruikersnaam gevolgd door `.github.io` |

   Gebruik voor het CNAME-record de eigenaar van de uiteindelijke GitHub-repository. Vervang conflicterende website-records; laat geen oude A- of AAAA-records naar OVH staan voor dezelfde naam.
4. Wacht op een geslaagde DNS-controle en het certificaat; schakel daarna **Enforce HTTPS** in.

De absolute metadata in `dist/index.html` is voorbereid voor `https://matiesclaesen.be`.
Gebruik je later een ander adres, pas dan ook `og:image`, `citation_pdf_url` en `dist/CNAME` aan.

## Updates publiceren

Pas de bestanden aan, maak een commit en kies **Push origin** in GitHub Desktop.
GitHub Actions publiceert daarna de nieuwe versie. Bewerkingen in Sites worden niet automatisch overgenomen.

## Documentatie

- [GitHub Pages instellen](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)
- [Eigen domein koppelen](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)
- [HTTPS inschakelen](https://docs.github.com/en/pages/getting-started-with-github-pages/securing-your-github-pages-site-with-https)
