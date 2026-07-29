# Beerslayer Brewing Co. — Website

A static landing page for Beerslayer Brewing Co., built to deploy on **Azure Static Web Apps**
(free tier) with the custom domain `www.beerslayerbrewing.com`.

## Project structure

```
BeerslayerBrewing/
├─ BeerslayerBrewing.sln      # Solution wrapper so this opens cleanly in Visual Studio
├─ README.md
└─ src/                       # Everything in here is the deployable site (app root)
   ├─ index.html
   ├─ staticwebapp.config.json
   ├─ css/
   │  └─ styles.css
   └─ images/
      └─ beerslayer-logo.png
```

## Preview locally

Any static file server works. From the `src` folder:

```bash
npx serve .
# or
python3 -m http.server 8080
```

Then open http://localhost:8080 (or whatever port is printed).

## Deploy to Azure Static Web Apps

1. Push this folder to a GitHub repository.
2. In the Azure Portal, create a new **Static Web App** resource (Free plan).
3. Connect it to your GitHub repo/branch. When prompted for build details, use:
   - **App location:** `src`
   - **Api location:** *(leave blank — no API yet)*
   - **Output location:** *(leave blank — no build step, plain static files)*
4. Azure will commit a GitHub Actions workflow (`.github/workflows/azure-static-web-apps-*.yml`)
   to the repo that builds and deploys automatically on every push to the connected branch.
5. Once deployed, go to the Static Web App resource → **Custom domains** → add
   `www.beerslayerbrewing.com`, and follow the DNS validation steps (CNAME/TXT record)
   at your domain registrar. A free managed SSL certificate is issued automatically.

## Notes

- This deploys as its own independent Azure resource — it does not touch the FomoFleet
  App Service, App Service Plan, or deployment pipeline in any way.
- To add more pages later, just add more `.html` files under `src/` and link to them;
  no server-side code is required for a static site like this.
