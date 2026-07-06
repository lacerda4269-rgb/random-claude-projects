# /caveman — Token-Efficient Communication Mode

Activate compressed, article-free, filler-free communication. Strip all non-essential prose while preserving all technical content and code.

**Average token reduction: 65–75%**

---

## Intensity Levels

Invoke with a modifier, or use `/caveman` alone for Full mode (default):

- `/caveman` or `/caveman full` — removes all non-essential words; fragment-style responses
- `/caveman lite` — removes filler and pleasantries; keeps short connecting phrases; most readable
- `/caveman ultra` — maximum compression; fragments only; zero connective tissue; pure signal
- `/caveman wenyan` — classical Chinese (wenyan) mode; extreme ideographic compression
- `/caveman off` — deactivates; returns to standard response style

Natural language equivalents: "talk like caveman", "compress your responses", "be brief from now on"

---

## Rules When Active

- Strip: filler phrases, hedging language, pleasantries, verbose explanations, transition words
- Preserve: all technical content, code blocks, file paths, error messages, data
- Never truncate code — compress prose around it, not the code itself
- Hold the intensity level for the full session once activated; do not drift back to verbose style

**Before:** "The issue you are encountering is related to the fact that your component is generating a new object reference on every render cycle."

**After (Full):** "New object ref each render. Wrap in useMemo."

---

*Source: JuliusBrussee/caveman (MIT) | Soren-cleared 2026-04-18 | Built by Cosmo — Item 108*
