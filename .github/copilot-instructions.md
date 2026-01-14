<!-- Copilot instructions for contributors and AI agents -->
# Copilot / AI-Agent Quick Guide

This repository is a single SQL dump representing Vietnam administrative units updated to 2025. The primary artifact is the SQL file and the README explains usage. Keep instructions short and actionable.

- **Primary files**: [README.md](README.md) and [database_tinh_thanh_vietnam_update_2025.sql](database_tinh_thanh_vietnam_update_2025.sql)

- **Big picture**: This project is a data artifact (MySQL/MariaDB dump created by phpMyAdmin) containing four main tables: `mien_vung`, `loai_don_vi`, `tinh_thanh`, `phuong_xa`. Treat code changes as data updates, not application logic.

- **Database conventions**:
  - Tables use snake_case; columns commonly include `code`, `name`, `full_name`, `name_en`, `code_name`, `province_code`, `unit_id`.
  - Charset is `utf8mb4` and collate `utf8mb4_general_ci`. Preserve these when importing/exporting.
  - Engine: `InnoDB` (see SQL header produced by phpMyAdmin / MariaDB).

- **How to import locally** (documented in README):
  - Import into MySQL/MariaDB: `mysql -u <user> -p < database_tinh_thanh_vietnam_update_2025.sql` (README example).
  - The dump's original database name is `2025_shopee` (see SQL header); do not rely on that name in downstream code — use the schema as-is.

- **How to regenerate or update the dump** (follow existing patterns):
  - Use `mysqldump` or phpMyAdmin to export with `--default-character-set=utf8mb4 --single-transaction --routines --triggers` so charset, transactions and table drops are preserved.
  - Recommended filename pattern: `database_tinh_thanh_vietnam_update_YYYY.sql` with YYYY year in name.

- **When editing this repo**:
  - Changes should be data-centric: add/update rows or replace the dump. Keep `CREATE TABLE` definitions intact (preserve types, charset, collate, engine).
  - If adding derived scripts (e.g., transformation scripts), include a small README and an example query showing the intended use.

- **Query patterns & examples** (useful when generating SQL snippets):
  - Lookup wards by province: `SELECT * FROM phuong_xa WHERE province_code = '01';` (from README)
  - Join region name: use `mien_vung` and `tinh_thanh` relationships; prefer explicit JOINs.

- **Pull requests & commit messages**:
  - Treat updates as data releases. Suggested commit message prefix: `data:`. Example: `data: update provinces dump to 2025 (phpMyAdmin export)`.
  - Include a short changelog in the PR description listing the high-level changes (rows added/removed, source references).

- **What not to do**:
  - Do not refactor table names or change column types in the dump without documenting compatibility consequences.
  - Avoid manual edits to large INSERT blocks; prefer regenerating the dump from a controlled database instance.

If anything in this guide is unclear, tell me which part you want expanded (import commands, export flags, or sample queries) and I will update it.
