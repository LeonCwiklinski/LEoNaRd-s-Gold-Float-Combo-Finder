# 🧮 LEoNaRd’s Gold Float Combo Finder

**LEoNaRd’s Gold Float Combo Finder** is a web-based tool designed to find combinations of skin floats that yield a specific **trade-up float** (for example, when crafting CS2 Gold items).

---

## ⚙️ Core Functionality

- 🔢 **Converts a desired float** into the actual IEEE754-style value used internally.
- 🎯 **Computes the target average float** needed to hit a desired output float (normalized between 0–1).
- 🧮 **Adjusts for float caps** — every skin has a lower and upper cap (e.g., `0.06–0.8`), and the tool correctly applies these to normalize or denormalize floats.
- 📋 **Parses marketplace pages** (Steam, Buff, etc.) to automatically extract all floats on the page.
- 🧩 **Finds 5-float combinations** that result in the target float, considering each item’s cap range and showing how close each combo is to the desired value.
- ⚗️ **Mix-and-match support** — the calculator can handle skins with completely different float caps in the same combination.

---

## 🧠 How It Works (Math Explainer)

Every CS2 skin has its own **float range** defined by:
\[
\text{lower cap} = L, \quad \text{upper cap} = U
\]

When you see a **desired float** (normalized between 0 and 1), it must be converted to the **real float** that actually corresponds to that skin’s range.

### Forward Conversion (used in the main calculator)
To compute the *real float* from a normalized float \( f \):
\[
f_{\text{real}} = L + (U - L) \times f
\]

Example:
If a skin has a cap range of `0.06–0.80` and the desired float is `0.666`,  
then:
\[
f_{\text{real}} = 0.06 + (0.80 - 0.06) \times 0.666 = 0.54884
\]

### Inverse Conversion (used when displaying results)
When showing results, the tool also applies the reverse operation to display how the **average real float** would map back to the normalized (0–1) scale for consistency.

---

## 💡 Usage Guide

1. **Paste a marketplace page** into the “Extract Floats” box.  
   - Optionally, input float caps (`Low Cap` / `High Cap`) if all the listed skins share the same range.
   - Click **Extract Floats** to retrieve all floats — floats will appear like this:  
     ```
     0.123456(0.06-0.80)
     ```
     if you specified caps.

2. **Paste or adjust extracted floats** into the input list.

3. **Set your desired target float** (the final float you want after trade-up).

4. **Click "Find Combos"**  
   - The tool will calculate all valid 5-float combinations that produce an average close to your target.
   - Each combination will show:
     ```
     Desired: <calculated float>
     avg(real): <average of converted real floats>
     diff: <difference from target>
     ```
     Skins with caps display both their **real** and **input** values, like:
     ```
     0.12(0.06)
     ```

---

## ⚠️ Notes

- The displayed **average** is not an exact IEEE754 float — CS2 rounds internally, so actual results may differ slightly.
- Supports arbitrary float caps per skin, such as:
