# 🚀 Releases Documentation

## Mục tiêu
Thư mục `releases/` dùng để:
- Ghi lại **lịch sử phát hành** của hệ thống (version, ngày phát hành, nội dung).  
- Truyền đạt cho team & khách hàng nội bộ về **tính năng mới**, **bugfix**, **thay đổi breaking**.  
- Làm cơ sở cho **rollback** hoặc phân tích regression.  

---

## Các thành phần

### 1. [Changelog tổng](./changelog.md)
- Ghi theo timeline (semver: `v1.0.0`, `v1.1.0`, …).
- Dùng format chuẩn:
  - **Added** – Tính năng mới.  
  - **Changed** – Thay đổi behavior.  
  - **Fixed** – Bugfix.  
  - **Removed** – Xóa bỏ/hủy bỏ.  

### 2. Release Notes theo phiên bản
- Ví dụ:  
  - [v1.0.md](./v1.0.md) – release đầu tiên.  
  - [v1.1.md](./v1.1.md) – thêm rate limiter, update Orleans TestCluster.  
- Mỗi file gồm:
  1. **Date** (ngày phát hành)  
  2. **Highlights** (tính năng chính, thay đổi quan trọng)  
  3. **Bugfixes**  
  4. **Known Issues** (vấn đề còn tồn tại)  
  5. **Migration Notes** (nếu có)  

---

## Convention
- Tên file = `v<major>.<minor>.md` (vd: `v1.2.md`).  
- Luôn update `changelog.md` khi có release mới.  
- Link từ PR/ADR → release notes nếu thay đổi quan trọng.  
- Release có breaking change phải **in đậm + highlight** để dev khác chú ý.  

---

## Tổ chức thư mục
```yaml
/docs/releases
│── README.md
│── changelog.md # changelog tổng
│── v1.0.md # release note phiên bản 1.0
└── v1.1.md # release note phiên bản 1.1
```

---

## Best practice
- Dùng **Semantic Versioning**: `MAJOR.MINOR.PATCH`  
  - MAJOR: thay đổi breaking.  
  - MINOR: thêm tính năng backward-compatible.  
  - PATCH: bugfix nhỏ.  
- Mỗi release phải có **tag Git** tương ứng (`git tag v1.1.0`).  
- CI/CD pipeline nên auto-generate changelog từ commit/PR, nhưng vẫn cần file markdown để lưu trong repo.  

---
