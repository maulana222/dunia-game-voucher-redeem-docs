# Folder `docs/`

| Isi | Keterangan |
|-----|------------|
| **`pages/`** | Sumber Markdown untuk MkDocs. |
| **`site/`** | Hasil build — **jangan** diedit manual; diabaikan Git. |
| **`mkdocs.yml`** | Konfigurasi jika Anda menjalankan MkDocs **dari folder `docs/`**. |

## Opsi A — dari folder `docs/` (seperti di terminal Anda)

```bash
cd docs
pip install -r requirements-docs.txt
mkdocs serve
# atau
mkdocs build
```

Output: **`docs/site/`** (folder `site` di samping `pages`).

## Opsi B — dari akar repo `dunia-game/`

Di root ada **`mkdocs.yml`** lain dengan `docs_dir: docs/pages` dan `site_dir: docs/site`:

```bash
cd /path/to/dunia-game
pip install -r requirements-docs.txt
mkdocs serve
```

Jangan mencampur: kalau `cd docs`, pakai `docs/mkdocs.yml` (otomatis). Kalau di root, pakai `mkdocs.yml` di root.

---

## Deploy ke GitHub Pages (tanpa `gh` CLI)

Repo dokumentasi terpisah memakai workflow **`.github/workflows/deploy-pages.yml`**: setiap push ke **`main`** (jika berubah `pages/`, `mkdocs.yml`, dll.) akan menjalankan `mkdocs build` lalu mendorong isi folder **`site/`** ke branch **`gh-pages`**.

### 1. Push workflow ke GitHub

```bash
cd docs
git add .github/workflows/deploy-pages.yml README.md
git commit -m "Add GitHub Pages deploy workflow"
git push origin main
```

### 2. Izinkan Actions menulis ke repo

Di GitHub: **Settings** → **Actions** → **General** → bagian **Workflow permissions** → pilih **Read and write permissions** → Save.

### 3. Aktifkan GitHub Pages

**Settings** → **Pages** → **Build and deployment**:

- **Source:** *Deploy from a branch*
- **Branch:** **`gh-pages`** — folder **`/ (root)`**

Simpan. Setelah workflow pertama selesai (tab **Actions**), URL biasanya:

`https://maulana222.github.io/dunia-game-voucher-redeem-docs/`

(ganti user/repo jika berbeda.)

### 4. Jika branch `gh-pages` belum muncul

Jalankan workflow sekali: tab **Actions** → workflow **Deploy dokumentasi ke GitHub Pages** → **Run workflow**, atau push commit ke `main`. Branch `gh-pages` dibuat otomatis oleh action **peaceiris/actions-gh-pages**.

### Catatan

- Tidak perlu menginstal **`gh`** (GitHub CLI).
- Isi **`site/`** tidak wajib di-commit ke `main` jika pakai Actions; cukup sumber di **`pages/`**.

---

## Kenapa situs tampak seperti README (polos, bukan tema Material)?

GitHub Pages memublikasikan **satu folder** yang Anda pilih. Yang benar untuk MkDocs adalah folder yang berisi **`index.html`** hasil `mkdocs build` (biasanya isi **`site/`**), **bukan** akar repo yang hanya punya `README.md` + `pages/*.md`.

| Salah (tampilan seperti screenshot) | Benar |
|--------------------------------------|--------|
| Source: **main** + folder **/ (root)** atau **/docs** → tidak ada `index.html` di root publikasi → GitHub menampilkan **README.md** polos | Source: branch **`gh-pages`** + **/ (root)** → isinya hasil deploy MkDocs (ada **`index.html`**) |
| Atau Anda buka URL ke path yang bukan `site/` | Atau Source: **main** + folder **`/site`** *hanya jika* Anda commit folder **`site/`** ke `main` |

**Perbaikan:** **Settings → Pages → Build and deployment → Branch: `gh-pages`, folder `/ (root)`**. Tunggu workflow **Actions** selesai membuat branch `gh-pages` dulu.

Pastikan juga **`site_url`** di `mkdocs.yml` sudah mengarah ke `https://USERNAME.github.io/REPO/` (sudah diset untuk repo ini) supaya aset tema tidak putus.
