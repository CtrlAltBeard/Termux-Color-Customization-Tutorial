# Termux-Color-Customization-Tutorial
A beginner-friendly guide to customize your Termux terminal with a vibrant color scheme featuring a deep purple background, white text, pink username, cyan directories, and green executables.

---
## Final Result

![Screenshot of the completed project](https://github.com/CtrlAltBeard/Termux-Color-Customization-Tutorial/raw/refs/heads/main/Final-result.jpeg)

## What You'll Learn

This tutorial covers:
- Setting up custom colors in **`colors.properties`**
- Customizing your **bash prompt** to show username in pink and directory in white
- Configuring **`LS_COLORS`** to highlight directories (cyan) and executables (green)
- Troubleshooting common issues

**Final result:** A personalized terminal with pink prompts, white text, cyan directories, and green executables on a deep purple background.

---

## Step 1: Create the Colors Configuration File

Navigate to the Termux styling directory and create your colors file:

```bash
mkdir -p ~/.termux
nano ~/.termux/colors.properties
```

Paste the following configuration:

```properties
background=#1a0033
foreground=#ffffff
color0=#1a0033
color1=#ff69b4
color2=#00ff41
color3=#ffff00
color4=#4a9eff
color5=#ff1493
color6=#00ffff
color7=#ffffff
color8=#663399
color9=#ff69b4
color10=#00ff41
color11=#ffff00
color12=#4a9eff
color13=#ff1493
color14=#00ffff
color15=#ffffff
```

**Color breakdown:**
- **Background:** `#1a0033` (Deep purple)
- **Foreground:** `#ffffff` (White)
- **Color1/Color9:** `#ff69b4` (Hot pink — for username in prompt)
- **Color2/Color10:** `#00ff41` (Neon green — for executables)
- **Color6/Color14:** `#00ffff` (Cyan — for directories)

Save with **Ctrl+O**, press **Enter**, then **Ctrl+X**.

---

## Step 2: Customize Your Bash Prompt

Edit your `.bashrc` file to add a custom prompt with pink username and white directory:

```bash
nano ~/.bashrc
```

Add this line at the end of the file:

```bash
export PS1='\033[38;5;205m\u@\h\033[0m:\033[38;5;255m\w\033[0m\$ '
```

**What this does:**
- `\033[38;5;205m` — Pink color for username (`\u`) and hostname (`\h`)
- `\033[38;5;255m` — White color for working directory (`\w`)
- `\033[0m` — Reset color to default

Save with **Ctrl+O**, press **Enter**, then **Ctrl+X**.

---

## Step 3: Configure LS_COLORS for Directory and Executable Highlighting

Still in `.bashrc`, add these lines:

```bash
alias ls='ls --color=auto'
export LS_COLORS='di=36:ex=32:*.sh=32'
```

**What this does:**
- `di=36` — Directories appear in **cyan** (color 6)
- `ex=32` — Executables appear in **green** (color 2)
- `*.sh=32` — `.sh` files also appear in **green**

Save with **Ctrl+O**, press **Enter**, then **Ctrl+X**.

---

## Step 4: Restart Termux

Close Termux completely and reopen it. This ensures all changes are loaded.

Alternatively, you can reload your `.bashrc` without closing:

```bash
source ~/.bashrc
```

---

## Step 5: Test Your Setup

Create a demo directory to see your colors in action:

```bash
mkdir -p ~/demo-public
cd ~/demo-public
mkdir project-files
touch notes.txt README.md config.txt data.json
touch setup.sh deploy.sh backup.sh
chmod +x setup.sh deploy.sh backup.sh
```

Now run:

```bash
ls
```

You should see:
- **Cyan folders:** `project-files/`
- **Green executables:** `setup.sh`, `deploy.sh`, `backup.sh`
- **White files:** `notes.txt`, `README.md`, `config.txt`, `data.json`
- **Pink prompt:** `username@hostname` at the start of each line

---

## Troubleshooting

### Colors not showing after restart?

**Check if `colors.properties` exists:**
```bash
cat ~/.termux/colors.properties
```

If it's empty or missing, re-create it with the configuration from **Step 1**.

### Prompt not showing pink/white?

**Verify your `.bashrc` changes:**
```bash
grep "PS1=" ~/.bashrc
```

Make sure the line from **Step 2** is there. If not, add it again and run `source ~/.bashrc`.

### Directories still white, executables not green?

**Check your `LS_COLORS`:**
```bash
echo $LS_COLORS
```

If it's empty, run:
```bash
source ~/.bashrc
```

If the colors still don't appear, verify your `LS_COLORS` export from **Step 3** is in `~/.bashrc`.

### Colors look different than expected?

Your device might have a different color palette. Try adjusting the hex values in `colors.properties` using a color picker tool.

---

## Finding More Colors

Want to customize with different colors? Visit **[colorhexa.com](https://www.colorhexa.com)** to:
- Search for any color by name (e.g., "sky blue", "coral")
- View hex codes for that color
- Copy the hex code and paste it into `colors.properties`

Simply replace any hex value (like `#ff69b4`) with your chosen color.

---

## References

- **Termux Wiki - Styling:** https://wiki.termux.com/wiki/Termux:Styling
- **Detailed Guide:** https://www.samgalope.dev/2024/08/27/termux-color-customization-tweaking-termux-properties-for-a-personalized-terminal/
