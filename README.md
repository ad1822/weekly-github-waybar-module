<!-- <div -->
  <h1 align="center">🟩🟩⬛🟩⬛</h1>
<!-- </div> -->

# GitHub Weekly Contributions Widget for Waybar

A terminal or bar integration script that fetches your **GitHub contribution activity for the current week (Sunday to Today)** using the GitHub GraphQL API and renders a **colored heatmap** with detailed tooltips.

Designed for seamless integration with status bars like **Waybar**, **Polybar**, or any custom desktop widget.

---

## Features

- Pulls real-time contribution data from GitHub's GraphQL API.
- Displays a **7-day contribution heatmap** (Sunday–Saturday layout).
- Uses a **color-coded square** (■) system similar to GitHub's own UI.
- Provides a **detailed tooltip** with:
  - Date-wise contribution breakdown.
  - Total contributions in the week.

---

## Color Levels

#### Dark Theme (By Default, If no argv passed)
| Contributions | Color Hex  | Meaning            |
|---------------|------------|--------------------|
| 0             | `#161b22`  | No contributions   |
| 1–3           | `#0e4429`  | Low activity       |
| 4–6           | `#006d32`  | Moderate activity  |
| 7–9           | `#26a641`  | High activity      |
| 10+           | `#39d353`  | Very high activity |

![Dark Theme](Assets/dark.png)

#### Light Theme
| Contributions | Color Hex  | Meaning            |
|---------------|------------|--------------------|
| 0             | `#ebedf0`  | No contributions   |
| 1–3           | `#9be9a8`  | Low activity       |
| 4–6           | `#40c463`  | Moderate activity  |
| 7–9           | `#30a14e`  | High activity      |
| 10+           | `#216e39`  | Very high activity |

![Light Theme](Assets/white.png)


## Example


| Preview                         |
|---------------------------------|
| ![commits](Assets/image.png)    |
|                                 |
| ![whole](Assets/image-2.png)    |
|                                 |
| ![half](Assets/image-1.png)     |


---

## Setup

### 1. Clone the Repository

```bash
git clone https://github.com/ad1822/weekly-github-waybar-module.git
cd weekly-github-waybar-module
````

---

### 2. GitHub Authentication

To make this module work, you need to provide:

* Your **GitHub username**
* A **Fine-Grained Personal Access Token (PAT)**

  * Scope: `Repository access → All repositories`
  * Minimum required permissions for reading contribution data

➡ **Generate your token here:**
[https://github.com/settings/personal-access-tokens/new](https://github.com/settings/personal-access-tokens/new)

---

### 3. Create `.env` File

Inside the project directory, create a `.env` file with the following content:

```env
GITHUB_USERNAME=your_github_username
GITHUB_PAT=ghp_yourGeneratedTokenHere
```
---

### 4. Install Python Dependencies

```bash
pip install -r requirements.txt
```
> Requires Python 3.7 or higher.
> Dependencies: `requests`, `python-dotenv`

---

### 5. Waybar Integration

Add the following block to your Waybar `config.jsonc`:

```jsonc
"custom/gh_heatmap": {
  "exec": "sleep 1 & ~/.config/waybar/scripts/weekly_commits DARK/LIGHT",
  "return-type": "json",
  "interval": 2400,
  "tooltip": true,
  "on-click": "xdg-open https://github.com/<your-github-username>",
  "on-click-right": "~/.config/waybar/scripts/weekly_commits DARK/LIGHT"
}
```
- On `click` of that module, Your github profile open in browser
- On `right-click` of that module, You can refresh module, So it can fetch latest commit data

Then add styling in your `style.css`:

```css
#custom-gh_heatmap {
  color: #39d353;
  background: rgba(30, 30, 46,0.89); // Put your own background color
  border-radius: 6px;
  margin-right: 2px;
  padding: 0px 8px;
}
```

> Ensure the script is executable:
>
> ```bash
> chmod +x ~/.config/waybar/scripts/weekly_commits
> ```

👉 Check out my custom Hyprland dotfiles: [**hyprdots**](https://github.com/ad1822/hyprdots)
If you like it, consider giving it a ⭐ — it helps!