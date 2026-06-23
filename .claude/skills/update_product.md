---
name: update_product
description: Scan docs/product/ folder structure and auto-generate product index pages (product/index.md and each category's index.md)
---

# update_product

Scan the `docs/product/` directory, extract product information from each product type folder, and regenerate all index pages automatically.

## Configuration

### Section Mapping

Each product category folder maps to a section on the product index page.
When adding a new category, add its folder name prefix here.

```
Section: 硬件产品 (Hardware Products)
  01.飞行控制计算机
  03.大气数据计算机
  05.地面差分基准站

Section: 软件产品 (Software Products)
  06.飞行仿真模拟训练系统

Section: 无人机平台 (Drone Platform)
  10.无人机平台
```

### Material Icons per Section

| Section | Icon |
|---------|------|
| 硬件产品 | `:material-chip:` |
| 软件产品 | `:material-monitor-dashboard:` |
| 无人机平台 | `:material-drone:` |

### Material Icons per Category (used in card titles)

| Category Folder | Icon |
|----------------|------|
| 01.飞行控制计算机 | `:material-memory:` |
| 03.大气数据计算机 | `:material-gauge:` |
| 05.地面差分基准站 | `:material-antenna:` |
| 06.飞行仿真模拟训练系统 | `:material-monitor-dashboard:` |
| 10.无人机平台 | `:material-drone:` |

## Procedure

### Step 1: Scan Folder Structure

Use Glob to list all numbered directories under `docs/product/`:
```
Glob: docs/product/[0-9]*/ (only directories)
```

For each category folder found, list its contents:
- Find `index.md` (category index page) — note if it exists
- Find all other `.md` files (product detail pages)
- Find image files in `imgs/` subdirectory

### Step 2: Extract Product Information

For each product `.md` file in each category, read the file and extract:
- **Product name**: The first `#` heading (H1)
- **Short description**: The first 1-2 sentences after the `## 简介` heading. Keep it to one concise sentence (~30-50 characters) that captures the essence.
- **Key features**: Read the product's feature list or description to distill 4-5 core selling points for the category `index.md` table.

For each category, pick a **display image** for the card:
- Priority 1: `imgs/标识-*.png` (logo/identity image, usually a render with transparent background)
- Priority 2: `imgs/产品图-*.png` (product photo)
- Priority 3: Any `.png` or `.jpg` in `imgs/` (first found)
- If no image exists, note that the card will use an icon placeholder instead.

### Step 3: Generate `docs/product/index.md`

Read the current `docs/product/index.md` to understand the existing structure, then regenerate it using the template below.

**Template:**

```markdown
# 产品中心

NextPilot 提供一系列高性能、高可靠性的无人系统核心组件，覆盖飞行控制、大气传感、差分定位、仿真训练与无人机机体五大领域。

---

## <SECTION_NAME_1>

<div class="grid cards" markdown>

-   ![<CATEGORY_NAME>](<IMAGE_PATH>){: style="height:160px;margin-bottom:0.5rem" }

    ## <ICON> <CATEGORY_NAME>

    ---

    <CATEGORY_DESCRIPTION_ONE_LINE>

    **型号**

    - [<PRODUCT_MODEL>](<PRODUCT_FILE_PATH>)

    [:octicons-arrow-right-24: 查看详情](<CATEGORY_INDEX_PATH>)

</div>

---

## <SECTION_NAME_2>

...
```

**Rules:**
- Each `<div class="grid cards">` block represents one section/row.
- If a section has 3+ cards, they appear in a single 3-column grid row.
- If a section has 1-2 cards, each card takes proportionally more width.
- Section headings use `##` (H2).
- Card titles inside cards use `##` (H2 within the card context) and must include the configured Material icon.
- Between the `---` separator and the `**型号**` list, include a one-line description of the category.
- List each product under `**型号**` as a bullet link to the product `.md` file.
- The "查看详情" link at the bottom of each card should point to the category's `index.md`.
- **Exception**: If a category has NO index.md and only ONE product, link "查看详情" directly to the product `.md` file.
- Image path is relative from `docs/product/index.md` to the category's `imgs/` folder.
- Use `{: style="height:160px;margin-bottom:0.5rem" }` on all card images for visual consistency.

### Step 4: Generate Category `index.md` Files

For each category folder, generate (or update) its `index.md`.

**Template:**

```markdown
# <CATEGORY_NAME>

<ONE_PARAGRAPH_INTRO>

## 产品列表

| 型号 | 核心特点 |
|:-----|:---------|
| [<PRODUCT_MODEL>](<PRODUCT_FILE.md>) | <KEY_FEATURES_SUMMARY> |
```

**Rules:**
- The intro paragraph should be 1-2 sentences describing this product category.
- For categories with a single product, distill the product's description.
- For categories with multiple products, write a general category-level description.
- The "核心特点" column should be a concise, comma-separated list of 3-5 key selling points.
- **Exception**: For `10.无人机平台`, use `## 平台列表` instead of `## 产品列表` since it lists drone platforms.

### Step 5: Report Summary

After generation, report a summary table:

| File | Action | Products Found |
|------|--------|---------------|
| `product/index.md` | regenerated | N categories, M products |
| `01.xxx/index.md` | updated | 1 product |
| ... | ... | ... |

Also mention any issues encountered (missing images, empty categories, etc.).

## Edge Cases

### Empty Category (no product .md files)
- Still include the card in `product/index.md` but mark it as "即将推出" with an icon placeholder.
- Create a minimal `index.md` with "即将推出" message.

### Category with No Images
- Use a large Material icon as placeholder in the card:
  ```markdown
  <ICON>{ style="font-size:120px;display:block;text-align:center;padding:20px 0;color:var(--md-default-fg-color--lightest)" }
  ```

### Multiple Products in One Category
- List all products under `**型号**` as separate bullet items.
- In the category `index.md`, add one row per product in the table.

### Renamed Folders
- If an old category folder no longer exists, remove its card from `product/index.md`.
- The skill regenerates from scratch each time, so renamed/moved folders are handled naturally.

### Non-Product .md Files
- Ignore `index.md` when scanning for product files.
- Only consider `.md` files whose first line is a `#` heading as product files.
