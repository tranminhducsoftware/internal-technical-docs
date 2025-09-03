# 💻 Coding Style (.NET 8, C#)

## General
- Tuân thủ **.editorconfig** trong repo.
- Tên class/interface/namespace: PascalCase.
- Biến/parameter: camelCase.
- Hằng số: UPPER_CASE.
- Không viết tắt khó hiểu (vd: `cust` → ❌, `customer` → ✅).

## C#
- Dùng `record` cho DTO, `class` cho entity/domain aggregate.
- Ưu tiên **immutability** (`init`, `readonly`).
- Exception handling:
  - Throw exception khi business rule fail.
  - Không swallow exception.
- Logging: luôn gắn `TraceId` vào log.

## Project Structure
```bash
/src
/Api
/Application
/Domain
/Infrastructure
/tests
/docs
```
- Không tham chiếu chéo sai hướng (Api không tham chiếu trực tiếp Infrastructure).
