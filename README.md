# BUILD LLM MODEL — Zero to Hero

> **Từ nền tảng Machine Learning đến tự xây dựng, huấn luyện, fine-tuning, đánh giá, tối ưu và vận hành LLM.**
>
> Lộ trình học theo dự án (project-first) hướng tới năng lực **LLM Research Engineer**.

[![Roadmap](https://img.shields.io/badge/Roadmap-v1.0-blue)](docs/roadmap/ROADMAP_V1.md) [![Project](https://img.shields.io/badge/Status-Planning-yellow)](docs/roadmap/ROADMAP_V1.md) [![Language](https://img.shields.io/badge/Docs-Ti%E1%BA%BFng%20Vi%E1%BB%87t-green)](AGENTS.md)

## 1. Giới thiệu

**BUILD LLM MODEL** là không gian học tập, nghiên cứu và thực nghiệm có hệ thống về **Large Language Models (LLMs)**. Mục đích không chỉ là chạy một model có sẵn, mà còn hiểu **model biểu diễn văn bản, tính attention, cập nhật trọng số, học từ dữ liệu, khái quát hóa, và được đánh giá/vận hành như thế nào**.

Hướng tiếp cận: **xây dựng → đo lường → giải thích → cải tiến → kiểm thử lại**. Các ví dụ được triển khai từ đơn giản đến phức tạp, tránh đưa framework/kiến trúc hạ tầng vào trước khi có nhu cầu thực tế.

Dự án được thiết kế để lưu cả **mã nguồn thực hành**, **tài liệu học tập**, **sổ tay thực nghiệm**, **báo cáo đánh giá** và **quyết định kỹ thuật**. Đây là repository học tập cá nhân, **không phải hệ thống LLM đã được kiểm chứng để sử dụng production**.

## 2. Hồ sơ học tập và giới hạn

| Hạng mục | Baseline kế hoạch |
|---|---|
| Định hướng | LLM Research Engineer: hiểu sâu, tự xây dựng, cải tiến và vận hành model |
| Xuất phát điểm | Biết Python, viết script/API; bắt đầu từ nền tảng toán ML và Deep Learning |
| Phương pháp | Project-first, giải thích dễ hiểu rồi tăng dần độ sâu toán học |
| Thời lượng | **8–10 giờ/tuần**, linh hoạt theo kết quả thực tế |
| Thiết bị chính | **Apple Silicon M1, 32 GB unified memory** |
| Môi trường | macOS local-first; thông tin phiên bản macOS và dung lượng SSD sẽ xác nhận tại WP-00 |
| Python dự kiến | Python **3.11**, native `arm64`, dùng `.venv` độc lập; chưa khóa phiên bản dependency |
| Ngân sách | Chưa cần chi phí cloud ở giai đoạn đầu; đầu tư khi có benchmark và đề xuất được duyệt |
| Trạng thái | **Roadmap v1.0 đã chốt; WP-00 chờ phê duyệt triển khai** |

**Giới hạn cần hiểu:** Mac M1 32 GB phù hợp cho neural network nhỏ, GPT giáo dục và thử nghiệm fine-tuning trên các model nhỏ/tương thích. Không mặc định rằng máy đáp ứng pretraining LLM hàng tỷ tham số hay fine-tuning mọi model. Tốc độ, RAM và tương thích phải được xác minh bằng benchmark.

## 3. Mục tiêu đầu ra

### Mốc 12 tuần (PoC học tập)

1. **GPT From Scratch:** hiểu tokenization, embedding, causal self-attention, Transformer decoder; tự huấn luyện một GPT nhỏ từ khởi tạo ngẫu nhiên, lưu/tải checkpoint và sinh token.
2. **Fine-tuning:** chọn một pretrained open-weight model tương thích, thiết kế dataset nhỏ và fine-tune bằng LoRA trên môi trường phù hợp; đo trước/sau trên cùng tập kiểm thử độc lập.
3. **Năng lực giải thích:** tự trình bày cơ chế gradient, loss, backpropagation, train/validation/test, overfitting và giới hạn của từng kết quả.

**Đây là mục tiêu kế hoạch, không phải cam kết đạt độ chính xác cụ thể hay đảm bảo chạy được mọi model trên M1.**

### Mốc 28 tuần (LLM Engineering Capstone)

- Có thể xây dựng, huấn luyện, đánh giá và cải tiến mô hình theo một quy trình tái lập được.
- Có baseline về chất lượng, thời gian suy luận, thông lượng, bộ nhớ và chi phí/tài nguyên.
- Có một API model-serving phục vụ nghiên cứu, kèm kiểm thử, log cơ bản, tài liệu giới hạn và báo cáo nghiệm thu.
- Có báo cáo capstone mô tả giả thuyết, phương pháp, kết quả, thất bại, hạn chế và hướng nghiên cứu tiếp.

## 4. Lộ trình 28 tuần

| WP | Tuần | Trọng tâm | Sản phẩm chính |
|---|---:|---|---|
| [WP-00](docs/roadmap/ROADMAP_V1.md#wp-00--research-environment--baseline-tuần-1) | 1 | Environment và baseline | Hardware inventory, tiny neural network, benchmark CPU/MPS |
| [WP-01](docs/roadmap/ROADMAP_V1.md#wp-01--math-ml--pytorch-foundation-tuần-24) | 2–4 | Math, ML, PyTorch | Neural network, giải thích training loop |
| [WP-02](docs/roadmap/ROADMAP_V1.md#wp-02--tokenizer-attention--transformer-tuần-56) | 5–6 | Transformer internals | Causal attention, decoder block và unit tests |
| [WP-03](docs/roadmap/ROADMAP_V1.md#wp-03--gpt-from-scratch-tuần-79) | 7–9 | GPT từ đầu | GPT nhỏ pretrained, checkpoint, generation |
| [WP-04](docs/roadmap/ROADMAP_V1.md#wp-04--fine-tuning-open-weight-llm-tuần-1012) | 10–12 | SFT, LoRA | Adapter và báo cáo trước/sau fine-tuning |
| [WP-05](docs/roadmap/ROADMAP_V1.md#wp-05--data-engineering--evaluation-tuần-1316) | 13–16 | Dataset và đánh giá | Evaluation harness, provenance, error analysis |
| [WP-06](docs/roadmap/ROADMAP_V1.md#wp-06--llm-optimization-tuần-1720) | 17–20 | Hiệu năng | Benchmark và trade-off quality/latency/memory |
| [WP-07](docs/roadmap/ROADMAP_V1.md#wp-07--model-serving--llmops-tuần-2124) | 21–24 | Vận hành | Model API, logging, health, smoke tests |
| [WP-08](docs/roadmap/ROADMAP_V1.md#wp-08--capstone--research-report-tuần-2528) | 25–28 | Capstone | Báo cáo nghiên cứu và sản phẩm minh chứng |

**Chi tiết mục tiêu, deliverables, lịch 28 tuần, các cổng nghiệm thu và giáo án WP-00:** xem **[ROADMAP_V1.md](docs/roadmap/ROADMAP_V1.md)**.

## 5. Công nghệ định hướng (chưa phải dependency đã cài)

| Lớp | Công nghệ đề xuất | Nguyên tắc sử dụng |
|---|---|---|
| Core | Python 3.11, NumPy khi cần | Dùng bản native Apple Silicon |
| Deep Learning | PyTorch, MPS | Học nền tảng và GPT tự xây dựng |
| Local LLM | Apple MLX / MLX-LM | Thử inference / LoRA khi đến WP-04 |
| Model ecosystem | Hugging Face Tokenizers, Datasets, Transformers | Chọn theo yêu cầu từng WP, không cài toàn bộ từ đầu |
| Inference | MLX-LM hoặc llama.cpp (khi phù hợp) | Benchmark thực tế, không giả định có GPU NVIDIA |
| Serving | FastAPI, runtime phù hợp | Chỉ bổ sung khi đến WP-07 |
| Experiment tracking | Markdown + JSON/CSV | Chưa cần MLflow server, database hay hạ tầng phân tán |

Nguồn tham khảo chính thức:

- [PyTorch MPS Backend](https://docs.pytorch.org/docs/stable/notes/mps.html)
- [PyTorch Beginner Basics](https://pytorch.org/tutorials/beginner/basics/intro.html)
- [Hugging Face LLM Course](https://huggingface.co/learn/llm-course/chapter1/1)
- [Training a causal language model from scratch](https://huggingface.co/learn/llm-course/chapter7/6)
- [Apple MLX-LM](https://github.com/ml-explore/mlx-lm) và [LoRA/QLoRA Guide](https://github.com/ml-explore/mlx-lm/blob/main/mlx_lm/LORA.md)

Các đường dẫn là tài liệu tham khảo; mỗi lần triển khai cần kiểm tra phiên bản và yêu cầu tương thích hiện hành.

## 6. Cấu trúc repository dự kiến

> Đây là **cấu trúc mục tiêu, chưa khẳng định các file/thư mục đã tồn tại**. Tạo dần theo WP đã được duyệt, không scaffold toàn bộ dự án ngay.

```text
build-llm-model/
├── README.md
├── AGENTS.md
├── docs/
│   ├── roadmap/
│   │   └── ROADMAP_V1.md
│   ├── lessons/              # tạo khi có bài học
│   └── research-notes/       # tạo khi có thực nghiệm
├── work-packages/           # tạo từng WP khi được duyệt
│   ├── WP-00-environment/
│   └── ...
├── experiments/             # metadata và kết quả nhỏ, an toàn
├── tests/                   # kiểm thử tương ứng source
└── datasets/                # chỉ mô tả/manifest; không commit dữ liệu lớn/nhạy cảm
```

## 7. Quy trình làm việc và tiêu chí hoàn thành

1. **Đề xuất WP:** mục tiêu, phạm vi, thiết kế, rủi ro, tài nguyên và acceptance criteria (AC).
2. **Phê duyệt:** chỉ triển khai source/test trong phạm vi đã duyệt; Git, dependency, migration, cloud spend, triển khai production cần phê duyệt riêng.
3. **Thực nghiệm:** lưu cấu hình, seed (nếu có), tập dữ liệu, phiên bản, chỉ số, kết quả lỗi và cách tái hiện.
4. **Nghiệm thu:** báo cáo tiếng Việt với lệnh test, output thực tế, kết quả PASS/FAIL/BLOCKED; phân biệt số liệu đo được và kỳ vọng.
5. **Bàn giao:** chỉ commit/push/merge/deploy sau khi có quyền tương ứng.

Quy ước đầy đủ trong **[AGENTS.md](AGENTS.md)**. Chưa đạt AC thì không tự tuyên bố WP hoàn thành.

## 8. Quy tắc dữ liệu và an toàn

- Chỉ sử dụng dữ liệu công khai có giấy phép/quyền sử dụng phù hợp hoặc dữ liệu giả lập trong các bài học đầu.
- **Repository hiện được xác nhận là Public (09/11/2026):** không commit bí mật, `.env`, tokens, credentials, thông tin cá nhân hoặc dữ liệu nội bộ chưa được phép công bố.
- Không tự động gửi dữ liệu doanh nghiệp lên cloud/Hugging Face/telemetry không được phê duyệt.
- Không commit weights/checkpoints/datasets lớn chỉ để lưu lịch sử; ưu tiên manifest, checksum, nguồn và cách tái tạo.
- Mô hình học tập không được coi là đáng tin cậy cho quyết định quan trọng nếu chưa có kiểm định, guardrails và phê duyệt thích hợp.

## 9. Bắt đầu từ đâu?

**Bắt đầu bằng [WP-00 — Research Environment & Baseline](docs/roadmap/ROADMAP_V1.md#wp-00--research-environment--baseline-tuần-1)**: khảo sát Mac M1, thiết lập môi trường sau phê duyệt, huấn luyện mạng neural nhỏ, đo CPU/MPS, hoàn thiện báo cáo nghiệm thu.

**Trạng thái sau cập nhật tài liệu nền tảng:** tài liệu được đưa lên branch riêng theo phê duyệt; **chưa triển khai WP-00**, chưa thay đổi môi trường máy cá nhân.

---

**Phiên bản tài liệu:** 1.0 · **Ngày chốt:** 09/11/2026 · **Ngôn ngữ tài liệu:** Tiếng Việt · **Code identifiers:** English.