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
