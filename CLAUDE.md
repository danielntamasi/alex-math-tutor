# Alex's Awesome Math Tutor

Single-page flashcard app (`index.html`, no build step) served by GitHub Pages at
https://danielntamasi.github.io/alex-math-tutor/. Progress is stored in Supabase
(project `zrdoyjuffrrcwanhldlb`) through RPC functions: `login`, `logout`, `get_all`,
`add_answers`, `save_round`, `reset_set`. The browser never touches tables directly.

## Adding a times table (the usual request)
The user sends photos/PDFs of Eureka Math² sprint sheets (usually Sheet B and Sheet C, 44 cards each).
1. Read every card. Write each as `a×b=c` / `a÷b=c` with `?` for the blank, e.g. `4×?=20`, `?÷4=6`.
2. Add an entry to `SETS` in `index.html`, keyed by a word (`two`, `five`, `four`, …):
   `four:{name:"× and ÷ by 4",tab:"4's",source:"Eureka Math² · Grade 3 Module 2",sheets:{B:[...],C:[...]}}`
3. Check every card with the page's own `solve()` (each must give a whole number ≥ 0) and that each
   sheet has the expected count. Tell the user about any card you couldn't read; don't guess.
4. Nothing changes in Supabase: answers are keyed by `set_key`.
5. Commit to `main` (Pages redeploys in about a minute).

## Rules
- Never commit passwords or the family code. They live only in Supabase as bcrypt hashes.
- The publishable key in `index.html` is meant to be public.
- Look: Minecraft-style blocks; the pixel font is for the title only, numbers use the readable font.
- `.github/workflows/keepalive.yml` pings Supabase daily so the free project doesn't pause.
