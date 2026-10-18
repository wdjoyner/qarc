# QARC — Quantitative-Analytic Reports on Chess

**QARC** reports are entirely computer-generated, book-length LaTeX reports that turn a PGN collection into a reproducible, data-backed “game dossier.” They are produced by **CGA (Chess Game Analyzer)**, the script `chess_game_analyzer.py` in the <a href="https://github.com/wdjoyner/chess-animator" target="_blank">chess-animator repository</a>. The same analyzer also drives chess-animator's Manim videos; this repository holds the report side: sample QARC books and the CGA manual.

```
                    PGN
                     │
                     ▼
     chess_game_analyzer.py (CGA): Stockfish + metrics
                     │
         ┌───────────┴───────────┐
         ▼                       ▼
   chess-animator              QARC
   Manim MP4 video      LaTeX/PDF reports (this repo)
```

To generate a QARC book yourself, get `chess_game_analyzer.py` from chess-animator and run, for example:

```bash
python chess_game_analyzer.py berliner-games-1965-world-corr-ch.pgn \
    -o berliner_book.tex --book --book-title "Berliner's Games"
```

## What a QARC report contains

The sample compiles **Hans Berliner’s 16 games from the 5th World Correspondence Championship (ICCF 1965, <a href="https://en.wikipedia.org/wiki/World_Correspondence_Chess_Championship" target="_blank">WCC championships on Wikipedia</a>)** into a single LaTeX book generated from **Stockfish 16** analysis (depth 20), pairing traditional annotation with interpretable engine-derived positional metrics.

Each game is presented as its own chapter with: (1) clean **game metadata** and **player statistics** (accuracy, average centipawn loss, and move-quality counts), (2) an **annotated move-by-move score**, (3) a **critical positions** section with FEN-based diagrams and “instead of / best continuation” recommendations, and (4) a quantitative layer of plots for **evaluation**, **Space**, **Mobility**, **King Safety**, and **Threats**, plus an experimental composite **Fireteam Index** that attempts outcome prediction via sustained-post-opening dominance (raw and smoothed variants). The document also includes a **collection-level prediction summary** (with held-out tests of the Fireteam Index in reports made with the current CGA) and a **methodology appendix** explaining how the underlying metrics are computed (in classical-eval terms for interpretability). Finally, for downstream research (e.g., regression/classification), the QARC output appends **raw per-ply positional data for every game** (SAN, centipawn eval, and all metric components for both sides) in a machine-friendly comment-block format.

### What the Fireteam Index can and can't do

Tests described in the CGA manual (chapter "Testing the Fireteam Index") found that, on these games, the Fireteam Index does not predict results better than simple baselines, and its weightings do not distinguish one player's style from another's. What does hold up is a small preference shared by all the players studied: among near-equal moves, they choose the more active one (higher Threats, Mobility, or King Safety) more often than chance. In short, some rithmomachia principles help with chess and some do not.

Both books were regenerated on 2026-10-18 with the current CGA (Stockfish 16, depth 20). Earlier versions of the Carlsen–Caruana report listed Carlsen as White in all twelve games; the current report, made from `carlsen-caruana-2018.pgn`, has the correct colors.

## Files

| File | Contents |
|---|---|
| `CGA-chess-game-analyzer-manual.pdf` / `.tex` | User manual for CGA |
| `berliner-games-1965-world-corr-ch.pgn` | Source PGN: Berliner's 16 games, 5th ICCF World Championship |
| `berliner-games-1965-world-corr-champ-book.pdf` / `.tex` | QARC book of those games |
| `carlsen-caruana-2018.pgn` | Source PGN: the 12 classical games of the 2018 World Championship, with the correct colors |
| `carlsen-vs-caruana-match_WCC2018-2018-11-london_qarc.pdf` / `.tex` | QARC report of the 12 games of the 2018 World Championship |

For more on CGA and QARC, see <a href="https://yetanothermathblog.com/mathematics-and-chess/medieval-monks-to-modern-metrics/" target="_blank">Medieval monks to modern metrics</a>.
