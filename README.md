# Scoreboard

A live sports scoreboard for a TV or monitor. It rotates through leagues on a big board, scrolls recent results and headlines along the bottom, and lets you click into any game for full stats.

It is a single HTML file with no build step and no server. Built to run full screen in a browser on a Fire TV Stick, but it works in any modern browser.

**Live page:** https://reddevilrooney.github.io/Rick-s-Scoreboard-project/

## What it shows

- **Scoreboard:** live and upcoming games, one league per page, rotating every 12 seconds. Leagues with live games come first, and leagues with nothing on are skipped.
- **Results band:** live scores first, then games that finished in the last day.
- **News band:** headlines from the leagues that have games on.
- **Game stats:** click a game (or focus it and press Enter) and a panel opens on the right with the score by period, team stats, leaders, scoring plays and player stats. The panel scrolls slowly by itself and loops, and it pauses while the mouse is over it or you scroll it by hand. Click another game to switch the panel to it. Click **Back to scores**, click the same game again, or press Escape to close it and get the full board back.
- **Settings:** choose which leagues to show, and optionally set a daily time window for each one.

Scores refresh every minute. Headlines refresh every 10 minutes.

## Where to watch

Each game that is live or coming up has a line under it showing the national channels in the US, Canada and the UK.

- **US:** shown for each game, straight from the data feed. Only national networks and subscription services are listed (up to three), such as ESPN, ABC or Peacock. Regional channels are left out.
- **Canada and UK:** the usual broadcasters for that league, taken from a list near the top of the script (`CHANNELS`). The feed has no data for these countries, so this is by league rather than by game. Some games are on a different channel, and rights change, so edit the list when you notice a difference. Leagues without an entry show nothing for that country.

Finished games don't show a channel line.

## Leagues

| Group | Leagues |
| --- | --- |
| North America | NFL, CFL, NBA, NHL, MLB, WNBA, MLS, college football, college basketball |
| Soccer | Premier League, Championship, FA Cup, League Cup, Scottish Premiership, Champions League, Europa League, Conference League, La Liga, Bundesliga, Serie A, Ligue 1, Liga MX, World Cup, Euros, Nations League, international friendlies |
| Other | Cricket (best effort, may show nothing) |

Darts, golf, F1, tennis, rugby and boxing are not included. The data source does not cover them.

## Set it up on GitHub Pages

1. Create a public repository and upload the HTML file, named exactly `index.html`.
2. Go to **Settings → Pages**. Under **Build and deployment**, choose **Deploy from a branch**, pick `main` and `/ (root)`, then save.
3. After a minute or two the site is live at `https://YOURUSERNAME.github.io/REPONAME/`.

To update it later, upload a new `index.html` with the same name and refresh the page with Ctrl+F5 to skip the cached copy.

## Use it on a Fire TV Stick

1. Open the page address in the Silk browser and bookmark it. Fully Kiosk Browser also works if you want it full screen without the address bar.
2. Use the remote's cursor mode to click the **Settings** button or a game card.
3. Choose your leagues in **Settings** once. They are saved in that browser, so settings made on another device do not carry over.

The Firestick needs its own internet connection. If you plug it into a Cisco DX80, the DX80 must be registered before it will show the Firestick's picture.

## Options in the page address

Add these to the end of the address.

| Option | Example | What it does |
| --- | --- | --- |
| `demo` | `?demo` | Shows sample games and headlines, handy for checking the layout |
| `page` | `?page=20` | Seconds each page stays on screen (default 12) |
| `leagues` | `?leagues=nhl,nba,epl` | Only load these leagues |

Combine them with `&`, for example `?leagues=nhl,nba&page=20`.

League IDs: `nfl`, `cfl`, `nba`, `nhl`, `mlb`, `wnba`, `mls`, `ncaaf`, `ncaam`, `epl`, `champ`, `fa`, `efl`, `spl`, `ucl`, `uel`, `uecl`, `laliga`, `bund`, `seriea`, `ligue1`, `ligamx`, `wc`, `euro`, `nations`, `friend`, `cricket`.

## Settings and time windows

Open **Settings** to untick any league you do not want. For each league you can also set **From** and **To** times so it only appears at certain times of day. Leave both on Any to show it all day. A From time later than the To time means overnight, so 10:00 PM to 2:00 AM works.

## Troubleshooting

- **The page shows a 404 from GitHub.** Pages is not switched on, the repository is private, or the file is not named `index.html`.
- **The board is empty.** Look at the line under the clock. It says how many leagues loaded and shows the first error, for example `12 of 27 leagues loaded (nhl HTTP 403)`.
- **Scores or headlines stop loading.** The data source may be refusing requests for a while, or your network may block it. Wait a few minutes, or try a different network.
- **Changes do not appear after uploading.** Press Ctrl+F5, or add `?v=2` to the address to skip the cached copy.

## Data and limits

Scores, stats and headlines come from ESPN's public web feed. It is not an official or documented API, so it can change or stop working without notice. This project is not affiliated with or endorsed by ESPN or any league. Team names and logos belong to their owners. Do not use it for betting decisions, since scores can be late or wrong.

## Technical notes

- One file of HTML, CSS and JavaScript, with no libraries. The only outside resource is the Barlow font from Google Fonts, with a fallback if it cannot load.
- Settings are stored in the browser's `localStorage` under `scoreboard.settings`.
- Requests to the data source are made a few at a time with short pauses, so it is not hit with dozens at once.
