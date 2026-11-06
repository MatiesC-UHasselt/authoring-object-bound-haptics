# Authoring Object-Bound Haptics

Papersite voor MUM 2026, met een lokale Git-repository en automatische publicatie via GitHub Pages.
De vier bestaande Sites-versies zijn bewaard in de Git-geschiedenis.

- Repository: <https://github.com/MatiesC-UHasselt/authoring-object-bound-haptics>
- Eigen domein: <https://matiesclaesen.be/>
- Alternatief adres: <https://www.matiesclaesen.be/> (verwijst door naar het hoofddomein zodra DNS en het certificaat actief zijn).
- Oorspronkelijk GitHub Pages-adres: <https://matiesc-uhasselt.github.io/authoring-object-bound-haptics/> (GitHub verwijst dit door naar het eigen domein).

## Bestanden aanpassen

- `dist/index.html`: de pagina, opmaak en interacties. Dit is het bewerkbare bronbestand; er is geen bouwstap.
- `dist/assets/`: afbeeldingen, lettertypen, het paper en de BibTeX-citatie.
- `.github/workflows/pages.yml`: publiceert `dist/` na een push naar `main`.
- `dist/CNAME`: het eigen domein, `matiesclaesen.be`.

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

## Domein en HTTPS

Het domein is gekocht bij OVH. In **Settings → Pages** van de repository staat **Custom domain** op `matiesclaesen.be`. De volgende DNS-records zijn bij OVH ingesteld:

| Type | Naam | Waarde |
| --- | --- | --- |
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |
| CNAME | www | matiesc-uhasselt.github.io. |
| TXT | _github-pages-challenge-MatiesC-UHasselt | 7302787a0ec1e2be0042270701187b |

De bestaande NS-, MX- en e-mail-SPF-records zijn behouden. De OVH-welkomstpagina en bijbehorende webverwijzingen zijn vervangen door de verwijzingen naar GitHub. De website-records hebben een TTL van 300 seconden.

De nameservers zijn `dns103.ovh.net` en `ns103.ovh.net`. Bij een nieuwe registratie kan de activering en verspreiding van DNS nog tijd kosten. GitHub vraagt het certificaat aan zodra de DNS-controle slaagt. Controleer **Enforce HTTPS** in de Pages-instellingen zodra het certificaat beschikbaar is.

Verifieer het domein ook onder [je GitHub-accountinstellingen](https://github.com/settings/pages_verified_domains/matiesclaesen.be) zodra het TXT-record publiek zichtbaar is. Laat het verificatierecord daarna staan.

De absolute metadata voor het paper en de deelafbeelding gebruikt `https://matiesclaesen.be`. Als je ooit verhuist, pas dan ook `og:image`, `citation_pdf_url`, `dist/CNAME` en de GitHub Pages-instellingen aan.

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
