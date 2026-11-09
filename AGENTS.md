# AGENTS.md — Project DNA cho BUILD LLM MODEL

> **Phạm vi áp dụng:** Toàn bộ repository `truongnk4365/build-llm-model`, bao gồm người đóng góp, AI coding agents (Codex, Claude, v.v.) và automation thực hiện thay đổi trong repository.
>
> **Ưu tiên:** bảo mật dữ liệu → tính đúng đắn/tái lập được → giá trị học tập → ổn định → tối giản và hiệu năng.
>
> **Trạng thái cập nhật (09/11/2026):** roadmap v1.0 đã chốt. Đã phê duyệt tạo branch và commit/push **ba tài liệu nền tảng**; chưa phê duyệt triển khai source/test WP-00, cài dependency, tạo PR, merge hay deploy.

## 1. Sứ mệnh dự án

BUILD LLM MODEL là một repository **học tập và nghiên cứu LLM theo phương pháp project-first**. Mục tiêu là hiểu rõ và tự xây dựng các thành phần từ neural network đến Transformer/GPT, sau đó học fine-tuning, evaluation, tối ưu inference và model serving.

**Điều quan trọng:** kết quả chạy được chưa đồng nghĩa mô hình đúng, cải thiện, an toàn hay sẵn sàng production. Mỗi experiment cần có baseline và chứng cứ.

**Nguồn sự thật của kế hoạch:** [`docs/roadmap/ROADMAP_V1.md`](docs/roadmap/ROADMAP_V1.md). Không thay đổi scope, mục tiêu tuần, AC hoặc lịch học chỉ vì agent muốn áp dụng best practice mới.

## 2. Quy trình bắt buộc trước mỗi nhiệm vụ

1. Đọc `README.md`, `AGENTS.md`, roadmap và file hướng dẫn cụ thể của WP (nếu có).
2. Khảo sát hiện trạng **read-only** trước; xác nhận branch, file liên quan, framework/version và trạng thái thay đổi chưa commit trước khi đề xuất sửa.
3. Tóm tắt mục tiêu, nguồn dữ liệu, phương án tối thiểu, ảnh hưởng, rủi ro, acceptance criteria và kế hoạch test bằng **tiếng Việt**.
4. Xác nhận **phạm vi đã được phê duyệt** trước khi sửa source/test hoặc thêm/sửa các tài liệu vượt khỏi yêu cầu đã giao.
5. Sau khi được duyệt, triển khai đúng phạm vi; không tự chuyển sang WP khác, không tự mở rộng kiến trúc hoặc nâng cấp phụ thuộc.
6. Chạy kiểm thử phù hợp và xuất báo cáo **bằng chứng thật** (lệnh, kết quả, failure, NOT_RUN/BLOCKED nếu có). Không tuyên bố PASS nếu chưa chạy.
7. Chỉ đề xuất đóng WP khi đáp ứng AC; nếu có blocker, nêu điều kiện và quyết định GO/NO-GO để chủ dự án xem xét.

**Không được suy luận rằng câu “chuẩn bị tài liệu” cho phép `git commit` hoặc `git push`.** Giấy phép thực hiện một hành động không tự mở rộng sang hành động khác.

## 3. Ma trận phê duyệt (không tự suy đoán quyền)

| Hoạt động | Quy tắc |
|---|---|
| Đọc, phân tích, giải thích source/tài liệu/log an toàn | Có thể làm read-only trong phạm vi được truy cập |
| Soạn phương án và tài liệu để rà soát | Được khi có yêu cầu; không tự push lên remote |
| Sửa source hoặc bổ sung/chỉnh test | **Cần duyệt giải pháp và scope trước**; duyệt xong mới thực hiện trong scope đó |
| Thêm/nâng cấp/hạ cấp dependency, đổi lockfile vì cài package | **Phê duyệt riêng** |
| Đổi database schema/migration, thiết lập storage mới | **Phê duyệt riêng** |
| Tạo branch, commit, push, mở PR, merge/rebase/cherry-pick | **Phê duyệt riêng cho loại thao tác Git tương ứng** |
| Deploy, mở port công khai, sửa service production | **Phê duyệt riêng** |
| Dùng cloud GPU/API tính phí, tải dữ liệu lên bên thứ ba | **Phê duyệt rõ về phạm vi/chi phí/dữ liệu** |
| Xóa/reset/overwrite dữ liệu, checkpoint, `.env`, lịch sử Git | **Không tự thực hiện**; chỉ xem xét sau khi có phê duyệt rõ ràng và phương án an toàn |

Khi không đủ quyền, **dừng ở đề xuất + danh sách việc chờ duyệt**. Không coi sự im lặng là đồng ý. Không chạy lệnh có side effect để “thử xem sao”.

## 4. Ngôn ngữ và phong cách kỹ thuật

- **Tài liệu, comment giải thích nghiệm thu và báo cáo:** tiếng Việt; tên thư viện/thuật ngữ phổ biến có thể giữ tiếng Anh kèm giải thích lần đầu.
- **Code identifiers:** tiếng Anh, có nghĩa rõ ràng (`train_step`, `validation_loss`, `model_config`). Comments trong code theo convention của module; ưu tiên diễn giải lý do hơn là mô tả cú pháp.
- Hướng dẫn cho người mới: bắt đầu bằng trực giác + ví dụ cụ thể; sau đó mới đến công thức toán, code và giới hạn.
- Không sao chép nguyên văn dài từ sách/paper; ghi nguồn, diễn giải và thử nghiệm độc lập.
- Ưu tiên Python idiomatic, modules/functions nhỏ, type hints tại boundary có giá trị; **không overengineering** với class abstractions/factories/service layers không cần thiết.
- Không đặt tên hoặc tuyên bố kết quả “SOTA”, “production-ready”, “faster”, “more accurate” khi chưa được đo và xác nhận.

## 5. Quy ước kiến trúc và cấu trúc repository

### 5.1. Local-first

- Target ban đầu: Apple Silicon **M1 32 GB RAM**, macOS, Python **3.11 native arm64** trong `.venv` dự án.
- PyTorch CPU/MPS để học kiến trúc và training; MLX/MLX-LM chỉ thêm khi đến tác vụ cần và xác minh version/khả năng máy.
- Đo Mac thực tế trước khi chọn batch/context/model size; không mặc định CUDA/NVIDIA có sẵn.
- Tránh cài gói vào Python global hoặc làm hỏng các `.venv` khác; **không xóa/ghi đè `.env`**.
- Không tự thêm Docker/Kubernetes/PostgreSQL/Redis/MLflow/distributed training/cloud trừ khi scope và bằng chứng nhu cầu được duyệt.

### 5.2. Cấu trúc incremental

Giữ các file nền: `README.md`, `AGENTS.md`, `docs/roadmap/ROADMAP_V1.md`. Chỉ tạo `work-packages/WP-XX-...`, `experiments/`, `tests/`, `datasets/` khi có nội dung thực và quyền thực hiện. Không tạo hàng loạt placeholder để trông như đã hoàn thành WP.

- `docs/` — bài học, kế hoạch, báo cáo và quyết định kỹ thuật.
- `work-packages/` — source/thực hành của WP đã được duyệt.
- `experiments/` — metadata/config và bảng kết quả nhỏ, an toàn (không mặc định lưu dữ liệu lớn).
- `tests/` — unit/integration/smoke tests theo đúng bài thực hành.
- `datasets/` — manifest, cách lấy và license; không lưu dataset lớn hoặc nhạy cảm lên Git.

Đây là quy ước định hướng; không bắt buộc tạo folder nếu không có file cần lưu.

## 6. Dữ liệu, quyền sử dụng và an toàn thông tin

**Repository được xác minh đang Public vào 09/11/2026.** Mặc định mọi thứ commit sẽ có thể xem công khai. Tất cả agent phải giả định repository public cho đến khi được xác nhận khác.

**Không bao giờ commit/push:**

- `.env`, API key, access token, SSH key, credential, cookies, license secrets hoặc file chứa thông tin hệ thống nội bộ.
- Thông tin định danh cá nhân, nội dung ticket/log ngân hàng, tài liệu nội bộ hoặc dữ liệu khách hàng, trừ trường hợp đã được đánh giá pháp lý/bảo mật và phê duyệt công khai cụ thể.
- Raw datasets/checkpoints/weights lớn; file bị ràng buộc license; artifacts có dữ liệu không rõ nguồn gốc.
- Path cá nhân, session token, full prompt/response chứa dữ liệu bí mật trong report hoặc commit history.

**Được ưu tiên:** synthetic data hoặc dataset công khai có quyền rõ ràng, nguồn và license được dẫn; file manifest nhỏ với URL, dataset revision/checksum, cách xử lý và điều kiện sử dụng. Đừng cho rằng “trên Internet” nghĩa là có quyền dùng để train hoặc redistrib.

**Trước khi dùng dữ liệu:** lập provenance, kiểm tra quyền sử dụng cho training/redistribution, rà soát PII/secrets, dedup, split và nguy cơ contamination. Không upload dữ liệu lên third-party service khi chưa có phê duyệt.

**Với model nguồn mở/open-weight:** xác minh model license, model card và giới hạn sử dụng; lưu model ID và revision đã dùng trong thí nghiệm. Không tự tải model rất lớn làm đầy ổ đĩa.

## 7. Chuẩn thí nghiệm (reproducibility)

Mỗi thực nghiệm có thể so sánh phải ghi tối thiểu:

```yaml
experiment_id: wpXX-example-001
objective: "Mô tả giả thuyết kiểm chứng"
status: NOT_RUN # NOT_RUN | PASS | FAIL | BLOCKED
code_revision: null # SHA nếu có; không tạo commit chỉ để điền
model:
  name: example
  architecture: null
  parameter_count: null
dataset:
  source: synthetic
  license: not_applicable
  version: null
  split: null
environment:
  platform: macos-arm64
  python: null
  framework: null
  device: cpu
training:
  seed: null
  batch_size: null
  learning_rate: null
  steps: null
metrics:
  train_loss: null
  validation_loss: null
artifacts: []
limitations: []
```

Đây là **ví dụ schema tài liệu**, không phải config thật hay một kết quả đã chạy. Chỉ bổ sung trường cần thiết cho WP thực tế; không biến schema thành hệ thống database/config quá phức tạp.

- Ghi rõ dataset train/validation/test, nguồn, cách split và version. Không dùng tập test để chọn hyperparameter rồi tuyên bố là unseen test.
- Có baseline tương ứng tác vụ. Kết quả tốt hơn phải dựa trên metric/cùng dataset/cùng phương pháp đo, không dùng vài câu trả lời chọn lọc.
- Ghi random seed nếu có, framework versions, device, batch size, LR, số bước training, số tham số và checkpoint reference.
- Loss/perplexity của hai model dùng tokenizer/dataset khác nhau **không tự động so sánh trực tiếp**.
- Benchmark performance: warm-up; đồng bộ GPU async (MPS) khi cần; nhiều lần lặp; báo cáo median, input/output size, precision, device, RAM/VRAM (nếu đo được), TTFT/latency/tokens/s theo workload.
- Kiểm thử kết quả trên tài nguyên thực: không giả lập log/benchmark để báo PASS.

## 8. Kiểm thử tối thiểu theo dạng thay đổi

| Thay đổi | Bằng chứng tối thiểu |
|---|---|
| Math/Tensor utilities | Unit test shape, giá trị và sai số số học |
| Model architecture | Forward/backward test, causal mask, parameter count và deterministic check khi phù hợp |
| Training loop | Tiny-set overfit, loss trace, checkpoint save/load, kiểm tra lỗi resume |
| Dataset processing | Validation schema, split/leakage checks, provenance/permissions |
| Fine-tuning | Baseline/pre-post evaluation trên tập test độc lập, thông số và adapter reload |
| Inference optimization | So sánh latency/throughput/memory và quality, cùng workload |
| Model serving | API contract, valid/invalid requests, timeout, health, smoke/integration tests |
| Documentation-only | Link/path/consistency review; không tạo báo cáo test source nếu chưa chạy |

**Không tự ý tăng dependency để dùng test framework mới.** Chọn `unittest` trong standard library nếu phù hợp; `pytest` chỉ khi đã nằm trong scope/được duyệt.

## 9. Mẫu báo cáo nghiệm thu WP

Mọi báo cáo final của WP phải có:

1. **Metadata:** WP, ngày, môi trường, branch/commit nếu có, người thực hiện.
2. **Scope:** mục tiêu được duyệt, phần làm và phần không làm.
3. **Changes:** files modified/new, dependencies, dữ liệu/migration nếu có.
4. **Evidence:** lệnh chạy thật, thông số, outputs/logs an toàn, metrics, link/path artifacts.
5. **AC Matrix:** từng AC theo `PASS`, `FAIL`, `BLOCKED`, `NOT_RUN`; kèm evidence và lý do.
6. **Security & Risks:** quyền dùng dữ liệu, bí mật, cấu hình phần cứng, rủi ro tồn dư.
7. **Decision recommendation:** `GO` / `GO_WITH_CONDITIONS` / `NO_GO` và điều kiện chuyển WP.
8. **Approvals outstanding:** những hành động tiếp theo chưa được cấp quyền (Git, dependency, deployment, cloud...).

**Mẫu ngắn:**

```markdown
# WP-XX — Acceptance Report
- Scope approved: ...
- Environment / commit: ...
- Tests actually run: ...

| AC | Result | Evidence |
|---|---|---|
| AC-01 | NOT_RUN | Chưa có quyền thực hiện |

- Measured results: ...
- Known limitations: ...
- Recommendation: NO_GO (đang chờ nghiệm thu)
- Pending separate approvals: ...
```

Không ghi “100% pass” nếu chỉ chạy subset test. Kết quả chưa chạy phải có `NOT_RUN`, công cụ/môi trường chưa sẵn sàng ghi `BLOCKED`.

## 10. Git, thay đổi dữ liệu và ranh giới an toàn

- Không tự `git switch -c`, `git add`, `git commit`, `git push`, tạo PR hay merge khi chưa có phê duyệt rõ ràng cho thao tác đó.
- Không force push, reset hard, clean, rebase lịch sử chia sẻ, xóa branch hoặc xóa file/directory khi chưa có phê duyệt rõ, ngay cả khi trông như file tạm.
- Tôn trọng working tree đang có; nếu gặp thay đổi ngoài scope, không ghi đè mà báo cáo.
- Trước khi commit được phép, rà soát staged diff để phát hiện secrets, dữ liệu lớn, thông tin cá nhân và đường dẫn nhạy cảm.
- Không tự chạy lệnh tốn chi phí cloud, training kéo dài, download model lớn, thay đổi quyền truy cập hoặc publish artifact.
- Nếu kết quả thí nghiệm tạo file lớn: giữ ngoài Git, ghi manifest/checksum và đường dẫn lưu trữ an toàn; **không tự bật Git LFS** nếu chưa được duyệt.
- Không tạo CI/workflow tự động huấn luyện model hoặc gọi dịch vụ trả phí trước khi được duyệt.

## 11. Hướng dẫn cộng tác với người học

AI agent phải hỗ trợ người học **hiểu được code**, không chỉ sinh code:

- Trước phần code có mục tiêu, kiến thức tiên quyết và sơ đồ dòng dữ liệu khi cần.
- Trình bày một ví dụ nhỏ, một phép tính tay hoặc hình dung trực quan trước công thức phức tạp.
- Sau mỗi bài có câu hỏi tự giải thích và checklist kiểm tra lỗi thường gặp.
- Báo cáo khác biệt giữa “model train được” và “model tổng quát hóa tốt”.
- Khi người học chưa nắm vững, ưu tiên phân rã bài tập; không thêm thư viện để né phần cần học.
- Mọi đề xuất nâng cấp Project DNA/`AGENTS.md` phải giải thích bài học rút ra, phạm vi tác động và **xin phê duyệt** trước khi thay đổi.

## 12. Definition of Done và nguyên tắc kết thúc

Một WP chỉ được đề xuất nghiệm thu khi:

- Phạm vi, thiết kế và AC đã được duyệt trước thực hiện.
- Code/test tương ứng (nếu nằm trong scope) tồn tại và có thể chạy lại; không có thay đổi ngoài scope.
- Dataset/model/license và bảo mật được kiểm tra, có evidence thực tế.
- Report có status cho từng AC, limitation và next steps.
- Chủ dự án xác nhận kết luận nghiệm thu; **GO kỹ thuật không đồng nghĩa quyền merge hoặc deploy**.

**Ưu tiên cuối cùng:** đơn giản, học được bản chất, kết quả tái lập được, dữ liệu an toàn; mỗi thay đổi đều có lý do và phê duyệt phù hợp.