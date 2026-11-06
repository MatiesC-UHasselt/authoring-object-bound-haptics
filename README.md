# Authoring Object-Bound Haptics

Papersite voor MUM 2026, met een lokale Git-repository en automatische publicatie via GitHub Pages.
De vier bestaande Sites-versies zijn bewaard in de Git-geschiedenis.

- Repository: <https://github.com/MatiesC-UHasselt/authoring-object-bound-haptics>
- GitHub Pages-adres: <https://matiesc-uhasselt.github.io/authoring-object-bound-haptics/>
- Beoogd eigen domein: `matiesclaesen.be` (registratie en DNS-koppeling nog af te werken).

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

## GitHub-koppeling

De openbare repository is aangemaakt onder **MatiesC-UHasselt**. De lokale `main`-branch volgt `origin/main` en de bestaande versiegeschiedenis is geüpload.

In **Settings → Pages** staat de publicatiebron op **GitHub Actions**. Een push naar `main` start automatisch de workflow **Publish website**. Onder **Actions** kun je de status bekijken en de workflow eventueel handmatig starten.

Wil je GitHub Desktop gebruiken, voeg deze bestaande map toe via **File → Add Local Repository**. De remote is al ingesteld; maak geen tweede online repository aan.

## Domein en HTTPS koppelen

Zodra `matiesclaesen.be` geregistreerd is:

1. Verifieer het domein bij GitHub via **Settings → Pages** van je account en voeg het gevraagde TXT-record toe bij OVH.
2. Stel in **Settings → Pages** van de repository **Custom domain** in op `matiesclaesen.be`. Bij een Actions-publicatie moet dit expliciet in de instellingen; het CNAME-bestand alleen volstaat niet.
3. Stel bij OVH de volgende records voor de website in. Bewaar records voor e-mail en domeinverificatie.

   | Type | Naam | Waarde |
   | --- | --- | --- |
   | A | @ | 185.199.108.153 |
   | A | @ | 185.199.109.153 |
   | A | @ | 185.199.110.153 |
   | A | @ | 185.199.111.153 |
   | CNAME | www | matiesc-uhasselt.github.io |

   Vervang conflicterende website-records; laat geen oude A- of AAAA-records naar OVH staan voor dezelfde naam.
4. Wacht op een geslaagde DNS-controle en het certificaat; schakel daarna **Enforce HTTPS** in.

De absolute metadata in `dist/index.html` gebruikt voorlopig het werkende GitHub Pages-adres.
Pas na het koppelen van het domein `og:image` en `citation_pdf_url` aan naar `https://matiesclaesen.be/assets/…`. `dist/CNAME` bevat al het beoogde domein.

## Updates publiceren

Pas de bestanden aan, maak een commit en kies **Push origin** in GitHub Desktop.
GitHub Actions publiceert daarna de nieuwe versie. Bewerkingen in Sites worden niet automatisch overgenomen.

Vanuit een terminal in deze map kan hetzelfde met:

```sh
git add dist
git commit -m "Update website"
git push
```

## Documentatie

- [GitHub Pages instellen](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)
- [Eigen domein koppelen](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)
- [HTTPS inschakelen](https://docs.github.com/en/pages/getting-started-with-github-pages/securing-your-github-pages-site-with-https)
