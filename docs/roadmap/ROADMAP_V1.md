# BUILD LLM MODEL — Roadmap Zero to Hero v1.0

**Phiên bản:** 1.0  
**Ngày chốt:** 09/11/2026  
**Định hướng:** LLM Research Engineer (project-first)  
**Thời lượng mục tiêu:** 28 tuần × 8–10 giờ/tuần (**224–280 giờ**, trung bình ~252 giờ)  
**Thiết bị nền:** Apple M1, 32 GB unified memory; SSD/macOS chưa xác minh  
**Trạng thái:** Kế hoạch đã chốt; **chưa phê duyệt thực thi WP-00**.

> Mốc tuần là kế hoạch học, không phải cam kết tốc độ training hoặc chất lượng model. Độ khó và tài nguyên thực tế sẽ được hiệu chỉnh sau mỗi WP. Không tự động mua GPU, sử dụng cloud, tạo repo mới, cài đặt dependency hoặc thay đổi source khi chưa có phê duyệt tương ứng.

## 1. Mục tiêu và triết lý nghiên cứu

### 1.1. Mục tiêu 12 tuần đầu

**PoC A — GPT From Scratch:** tự xây tokenizer đơn giản hoặc tích hợp tokenizer có giải thích rõ, decoder-only Transformer, causal attention, model next-token prediction, pretrain GPT giáo dục từ khởi tạo ngẫu nhiên; lưu/tải checkpoint và đánh giá loss/perplexity phù hợp.

**PoC B — Fine-tuned Open-weight LLM:** chọn model nhỏ có giấy phép sử dụng rõ ràng, chạy baseline, chuẩn bị dataset, LoRA fine-tuning trên phần cứng tương thích, đánh giá tập test tách biệt và báo cáo tác động (kể cả khi cải thiện không đạt kỳ vọng).

**Mục tiêu năng lực:** giải thích toán/thuật toán nằm dưới từng bước, chứ không chỉ thực thi thư viện; tự đọc lỗi và đo mức sử dụng tài nguyên.

### 1.2. Mục tiêu tuần 28

Có một capstone thể hiện đủ chu trình **data → model → training/fine-tuning → evaluation → optimization → serving → monitoring/reporting**, ưu tiên vận hành local. Sản phẩm phục vụ học tập/nghiên cứu, không mặc nhiên đáp ứng tiêu chuẩn production doanh nghiệp.

### 1.3. Nguyên tắc điều hành

1. **Project-first:** 30% thời gian lý thuyết định hướng, ~70% thực hành/đo lường; tỷ lệ linh hoạt theo mức độ khó.
2. **Từ nhỏ đến lớn:** NumPy/PyTorch toy examples → tiny GPT → pretrained small LLM → serving.
3. **Cơ sở khoa học:** ghi rõ giả thuyết, baseline, seed, dataset split, metric, kết quả và giới hạn; không lấy một lần chạy làm kết luận chắc chắn.
4. **Bảo toàn dữ liệu:** dataset phải có provenance và quyền sử dụng; chỉ đưa thông tin an toàn lên GitHub Public.
5. **Gating:** chỉ chuyển sang WP tiếp theo khi đã đạt AC hoặc có quyết định GO có điều kiện được ghi nhận.
6. **YAGNI:** không tự thêm K8s, DB, MLflow, distributed training hay microservices trước khi có yêu cầu chứng minh bằng thí nghiệm.

## 2. Phân bổ thời gian 28 tuần

| WP | Tuần | Thời lượng ước tính | Năng lực chính | Artifact/bằng chứng |
|---|---:|---:|---|---|
| WP-00 | 1 | 8–10h | Env, MPS, tiny model, benchmark | Inventory + experiment report |
| WP-01 | 2–4 | 24–30h | Toán ML, neural net, PyTorch | Notebook/script + test + giải thích |
| WP-02 | 5–6 | 16–20h | Tokenizer, attention, Transformer | Module tests, shape/mask tests |
| WP-03 | 7–9 | 24–30h | GPT training from scratch | Checkpoint + loss curve + generation |
| WP-04 | 10–12 | 24–30h | SFT/LoRA pretrained LLM | Adapter + baseline/post comparison |
| WP-05 | 13–16 | 32–40h | Dữ liệu, benchmarking, eval | Dataset card + eval harness + error analysis |
| WP-06 | 17–20 | 32–40h | Inference optimization | Latency/throughput/memory trade-offs |
| WP-07 | 21–24 | 32–40h | Serving & LLMOps | Local API + telemetry + smoke tests |
| WP-08 | 25–28 | 32–40h | Research capstone | Reproducible experiment + technical report |
| **Tổng** | **28** | **224–280h** | | |

### Lịch học từng tuần

| Tuần | Mục tiêu trọng tâm | Minh chứng cuối tuần |
|---:|---|---|
| 01 | Kiểm tra Mac, Python/MPS, huấn luyện tiny neural network, benchmark | WP-00 acceptance report |
| 02 | Vector, ma trận, Tensor, phép nhân và shape | Bài thực hành Tensor có test |
| 03 | Đạo hàm, gradient descent, autograd, loss | Training loop giải thích được từng bước |
| 04 | Generalization, train/validation/test, overfit/underfit | Báo cáo NN baseline và kiểm thử |
| 05 | Text pipeline, tokenization, embeddings, position | Ví dụ encode/decode và embedding dimensions |
| 06 | Scaled dot-product attention, causal mask, decoder block | Unit test attention/mask và shape |
| 07 | Thiết kế GPT mini, sampling, initialization | Model forward pass + kiểm thử |
| 08 | Causal LM training, optimizer, checkpoint | Training run tái lập được |
| 09 | Eval loss, perplexity, generation, error analysis | GPT nhỏ + model card thực nghiệm |
| 10 | Khảo sát model mở, license, benchmark zero-shot | Baseline và lựa chọn model có lý do |
| 11 | Xây dataset SFT nhỏ, format, split, LoRA | Training/validation artifacts |
| 12 | Fine-tune, chạy test set, so sánh chất lượng | Adapter + before/after evaluation |
| 13 | Data provenance, license, dedup, privacy | Dataset card và kiểm tra chất lượng |
| 14 | Tokenization/packing, leakage, filtering | Data processing report |
| 15 | Thiết kế metric tự động và human review rubric | Eval harness version 1 |
| 16 | Phân tích lỗi và ablation nhỏ | Báo cáo evaluation v1 |
| 17 | Precision, quantization, chất lượng sau lượng tử hóa | Benchmark chất lượng/bộ nhớ |
| 18 | KV cache, prefill/decode, context length | Latency analysis |
| 19 | Batching, tokens/s, memory budget | Throughput benchmark |
| 20 | Lựa chọn cấu hình tối ưu theo workload | Optimization report |
| 21 | Thiết kế model server tối thiểu, API contract | API design + local smoke test |
| 22 | Request validation, timeout, concurrency, streaming (nếu cần) | Functional tests |
| 23 | Health, logging, metrics, operational failure | Observability baseline |
| 24 | Reproducible runbook, versioning, security checklist | LLMOps acceptance report |
| 25 | Chốt vấn đề nghiên cứu và giả thuyết | Research plan và dataset freeze |
| 26 | Chạy baseline và biến thể có kiểm soát | Experiment logs |
| 27 | Đối chiếu kết quả, error analysis, giới hạn | Comparative analysis |
| 28 | Tài liệu, demo, nghiệm thu capstone | Báo cáo cuối + lessons learned |

## 3. Chi tiết từng Work Package

### WP-00 — Research Environment & Baseline (Tuần 1)

**Mục tiêu:** xác thực tài nguyên Mac M1 32 GB, thiết lập môi trường Python độc lập nếu được duyệt, huấn luyện tiny neural network, đo CPU/MPS và giải thích training loop.

**Phạm vi:** inventory, Python native arm64, PyTorch CPU/MPS, synthetic dataset, mini training, benchmark, báo cáo. Không fine-tune LLM, không Docker, không cloud.

**Deliverables:** hardware/environment inventory, mã thí nghiệm tiny NN (sau duyệt source), tối thiểu 3 lần benchmark mỗi workload, kết quả test, báo cáo nghiệm thu bằng tiếng Việt.

**Acceptance:** xem [Mục 4](#4-thiết-kế-chi-tiết-wp-00--nghiệm-thu).

### WP-01 — Math, ML & PyTorch Foundation (Tuần 2–4)

**Kiến thức:** đại số tuyến tính vừa đủ dùng (vector, matrix, broadcasting); đạo hàm, chain rule, gradient, backpropagation; tối ưu SGD/Adam ở mức trực quan và công thức cơ bản; overfit/underfit, train/validation/test; PyTorch model, optimizer, autograd.

**Thực hành:** thực hiện regression/classification nhỏ, so sánh cập nhật trọng số thủ công với autograd; train model có khả năng overfit tập mini để kiểm tra pipeline.

**Nghiệm thu:** giải thích được training step; có ít nhất 1 model cải thiện loss trên tập train, có phép đo trên holdout; có test shape và khả năng lưu/tải model; không suy diễn chất lượng từ train loss đơn thuần.

### WP-02 — Tokenizer, Attention & Transformer (Tuần 5–6)

**Kiến thức:** token/ID, vocabulary, BPE ở mức hiểu thuật toán, embedding, positional information, Q/K/V, scaled dot-product attention, causal mask, multi-head attention, normalization, residual connections, Transformer decoder.

**Thực hành:** mô phỏng tokenizer toy và attention bằng Tensor; triển khai decoder block giáo dục có test shape, mask và hành vi chỉ nhìn token quá khứ.

**Nghiệm thu:** test causal mask chứng minh token trước không phụ thuộc token tương lai trong chế độ phù hợp; giải thích đầu vào/đầu ra từng khối; test kích thước và gradient hữu hạn, tránh kiểm thử bằng cảm quan.

### WP-03 — GPT From Scratch (Tuần 7–9)

**Kiến thức:** autoregressive next-token training, cross-entropy, initialization, optimizer, batching, sequence length, checkpoint, text sampling temperature/top-k, validation loss và perplexity (chú ý khác tokenizer không so sánh trực tiếp).

**Thực hành:** xây GPT decoder-only quy mô giáo dục, **mục tiêu tham khảo 1–5 triệu tham số**, tùy baseline phần cứng/dataset; training từ khởi tạo ngẫu nhiên trên dữ liệu công khai có license phù hợp.

**Nghiệm thu:** model train được, loss hợp lý và có baseline; checkpoint save/load tái hiện được output trong chế độ deterministic; generation không lỗi; báo cáo kiến trúc, số tham số, dữ liệu, token count, tài nguyên và failure modes.

**Giới hạn:** GPT vài triệu tham số không được kỳ vọng hội thoại tốt hay có tri thức như mô hình thương mại.

### WP-04 — Fine-tuning Open-weight LLM (Tuần 10–12)

**Kiến thức:** pretrained vs from-scratch, SFT, LoRA, quantization vs QLoRA, trainable parameters, format instruction/response, model license, evaluation leakage.

**Thực hành:** chọn model mở tương thích MLX/MLX-LM với kích thước ban đầu **~0.5–1.5B** nếu bộ nhớ và phần mềm cho phép; xây dataset công khai/giả lập, huấn luyện adapter và đo chất lượng trước/sau bằng rubric/tập test cố định. Nếu mức này không khả thi, giảm model/sequence length hoặc chuyển lựa chọn khi có kết quả WP-00/benchmark.

**Nghiệm thu:** có baseline model, config và dataset card; adapter được save/load; kết quả đánh giá cặp trước/sau có minh chứng; báo cáo cả trường hợp không cải thiện; không huấn luyện trực tiếp dữ liệu nhạy cảm và không giả định QLoRA CUDA chạy được trên Mac.

### WP-05 — Data Engineering & Evaluation (Tuần 13–16)

**Kiến thức:** nguồn dữ liệu, license, de-duplication, train/validation/test split, data leakage, contamination, SFT quality, automated evaluation, human review và uncertainty.

**Thực hành:** dataset manifest/card, pipeline xử lý có thể tái lập, bộ câu hỏi test/metrics, phân tích nhóm lỗi và một ablation nhỏ.

**Nghiệm thu:** dataset có nguồn và điều kiện sử dụng; test split độc lập, chỉ số và rubric phù hợp; lỗi phân loại theo nguyên nhân, không tuyên bố cải thiện từ ví dụ chọn lọc.

### WP-06 — LLM Optimization (Tuần 17–20)

**Kiến thức:** fp32/fp16/bf16 và giới hạn tương thích, quantization, KV cache, prefill/decode, context length, batching, latency (TTFT nếu streaming), tokens/s, memory và trade-off chất lượng.

**Thực hành:** đo workload và cấu hình cố định trước/sau tối ưu trên phần cứng hiện có; đo latency phân vị khi đủ mẫu, throughput, peak memory theo khả năng công cụ, chất lượng trên tập cố định.

**Nghiệm thu:** benchmark có warm-up, đồng bộ thiết bị, nhiều lần chạy, cấu hình và kích thước input/output; có kết luận cải tiến đi kèm trade-off, không bắt buộc GPU luôn nhanh hơn CPU.

### WP-07 — Model Serving & LLMOps (Tuần 21–24)

**Kiến thức:** API model serving, lifecycle của model, request validation, concurrency/queue, timeout, health checks, logging và metrics, deployment runbook, basic model/version registry và safety controls.

**Thực hành:** local API (ví dụ FastAPI + runtime chọn theo phần cứng), smoke/integration tests, request ID, timing và basic monitoring; Docker Compose chỉ thêm nếu môi trường thực tế cần và được duyệt.

**Nghiệm thu:** API chạy trên môi trường mục tiêu, có các ca valid/invalid/timeouts, log không lộ secrets/prompts nhạy cảm, có hướng dẫn khởi động/dừng và báo cáo giới hạn chịu tải.

### WP-08 — Capstone & Research Report (Tuần 25–28)

**Mục tiêu:** giải quyết một bài toán hẹp được xác định từ dữ liệu an toàn, hoặc chứng minh một cải tiến quy trình/model bằng phương pháp khoa học.

**Thực hành:** khóa baseline, phát biểu giả thuyết, chọn 1–2 biến nghiên cứu, chạy thực nghiệm có thể tái lập, so sánh số liệu, phân tích lỗi, demo sản phẩm.

**Nghiệm thu:** source/config/dataset manifest an toàn; report mô tả mục tiêu, phương pháp, baseline, kết quả, giới hạn, threat-to-validity, cách tái tạo; demo hoạt động và trả lời được câu hỏi phản biện kỹ thuật.

## 4. Thiết kế chi tiết WP-00 & nghiệm thu

### 4.1. Metadata và ranh giới

| Thuộc tính | Giá trị |
|---|---|
| ID | WP-00 |
| Tên | Research Environment & Baseline |
| Ưu tiên | P0 |
| Thời lượng | 1 tuần / 9 giờ kế hoạch |
| Target | Mac M1, RAM 32 GB, macOS chưa xác minh |
| Trạng thái | **PENDING IMPLEMENTATION APPROVAL** |
| Quyền đã có | Phê duyệt roadmap và commit/push ba tài liệu nền tảng trên branch riêng; **chưa phê duyệt source/dependency/PR/merge/deploy** |
| Ngoài phạm vi | Fine-tuning model lớn, production deployment, cloud GPU, Docker/K8s, database, thay đổi dữ liệu có sẵn |

### 4.2. Work breakdown

| ID | Nội dung | Giờ | Bằng chứng |
|---|---|---:|---|
| WP00-01 | Hardware & environment inventory (read-only) | 1.0 | Thông số arm64, macOS, RAM, disk, Python |
| WP00-02 | Môi trường Python độc lập sau phê duyệt | 1.5 | `.venv`, dependency versions, cách tái lập |
| WP00-03 | CPU/MPS device & Tensor tests | 1.0 | MPS availability và kết quả phép toán |
| WP00-04 | Tiny Neural Network training | 2.0 | Loss trace, save/reload, small-set overfit |
| WP00-05 | CPU/MPS benchmark | 1.5 | ≥3 run/workload, kết quả trung vị |
| WP00-06 | Giải thích, báo cáo, nghiệm thu | 2.0 | Acceptance evidence và kết luận |
| **Tổng** | | **9.0** | |

**Khảo sát read-only dự kiến:** `uname -m`, `sw_vers`, `sysctl -n hw.memsize`, `df -h "$HOME"`, `python3 --version`. Không yêu cầu thay đổi hệ thống. Chỉ thực thi trên máy sau khi người dùng đồng ý/đích thực thi rõ ràng.

**Nền tảng đề xuất:** Python 3.11 native arm64, `.venv`, PyTorch với MPS nếu khả dụng. Version pin chỉ quyết định sau khi xác minh tương thích macOS; không mặc định PyTorch đã cài hoặc MPS hoạt động.

### 4.3. Mini neural network đầu tiên

**Bài toán:** regression tổng hợp nhỏ (synthetic), hoặc bài toán phi tuyến đơn giản được xác định với train/test split rõ ràng. Sử dụng mạng 2 đầu vào → 2 hidden layers 4 neuron → 1 đầu ra để học forward, loss, backward, optimizer.

**Kiểm chứng kỹ thuật:**

- So sánh với baseline đơn giản (ví dụ dự đoán trung bình hoặc hàm mục tiêu phù hợp).
- Kiểm tra training loss giảm và holdout metric; không đặt ngưỡng chất lượng cứng trước khi có dataset cụ thể.
- Test tiny-set overfit như phép kiểm tra training loop; kiểm tra seed, độ ổn định và checkpoint save/load.
- Cùng workload benchmark trên CPU/MPS. Thực hiện warm-up, đồng bộ MPS trước/sau thời gian đo, 3 lần đo trở lên, log model size/batch size/sequence/input shape.
- Nếu MPS không khả dụng, ghi blocker và nguyên nhân; không tự bật tùy chọn fallback che dấu lỗi hoặc kết luận sai về GPU.

### 4.4. Acceptance Criteria (WP-00)

| AC | Yêu cầu | Điều kiện PASS |
|---|---|---|
| AC-01 | Inventory | Thu được kiến trúc, RAM, OS, disk, Python; không tự suy diễn thông số chưa đo |
| AC-02 | Reproducible env | `.venv` độc lập, có phiên bản dependencies, hướng dẫn tái lập từ môi trường sạch |
| AC-03 | CPU/MPS | PyTorch CPU chạy; MPS được xác minh khả dụng hoặc blocker có bằng chứng/phương án xử lý |
| AC-04 | Tensor correctness | Kiểm tra phép toán trên các backend khả dụng trong sai số xác định và có test |
| AC-05 | Training | Model chạy train, loss giảm so với ban đầu, đánh giá holdout; có log, seed và config |
| AC-06 | Training loop validation | Có tiny-set overfit test và checkpoint save/load xác minh được |
| AC-07 | Benchmark | ≥3 lần đo mỗi cấu hình, có warm-up/sync và báo cáo trung vị; không khẳng định speedup nếu không có số liệu |
| AC-08 | Report & safety | Có báo cáo tiếng Việt, evidence test, dataset an toàn và đề xuất WP-01 |

**Quy tắc GO:** tất cả AC đạt và không còn blocker ảnh hưởng học phần tiếp theo. **GO có điều kiện:** MPS gặp vấn đề được chứng minh, CPU baseline vẫn hoạt động, kế hoạch xử lý được phê duyệt; không kết luận đã đạt khả năng GPU training. **NO-GO:** training loop không đúng, thiếu bằng chứng hoặc môi trường không tái lập được.

### 4.5. Giáo án tuần đầu: 5 buổi × 9 giờ

| Buổi | Giờ | Nội dung | Bài thực hành / tự kiểm tra |
|---|---:|---|---|
| 1 | 1.5 | LLM là gì; phân biệt ML/DL/LLM, training/inference; khảo sát Mac | Giải thích vì sao LLM không phải database chứa sẵn câu trả lời; lập inventory |
| 2 | 2.0 | Vector, matrix, hàm số, đạo hàm, gradient | Tự tính một bước gradient descent cho ví dụ số đơn giản |
| 3 | 2.0 | Tensor, autograd, loss, optimizer, training loop | Train mạng nhỏ trên CPU; giải thích forward → loss → backward → step |
| 4 | 2.0 | MPS, CPU/GPU, phép đo công bằng | Kiểm tra device và benchmark nhiều lượt; hiểu tại sao GPU có thể chậm với bài toán nhỏ |
| 5 | 1.5 | Validation/overfit, báo cáo, nghiệm thu | Kiểm tra log, checkpoint, benchmark; tự trình bày kết quả, giới hạn và đề xuất WP-01 |

**Câu hỏi tự đánh giá:** gradient dùng để làm gì? Vì sao cần tập validation/test? Causal LLM khác một classifier ở mục tiêu dự đoán như thế nào? Tại sao GPU không luôn nhanh hơn CPU?

### 4.6. Định dạng báo cáo WP-00

1. Thông tin môi trường thực tế (hardware, OS, Python, framework, device).
2. Phạm vi và dataset (synthetic/public, provenance).
3. Model architecture, parameter count, batch/lr/seed, train procedure.
4. Lệnh thực thi đã chạy, số lần lặp và log thực tế (che thông tin cá nhân/secret).
5. Bảng CPU/MPS: operation, shape, runs, median, dispersion nếu có, latency, bộ nhớ khi đo được.
6. Kết quả train/holdout, checkpoint, tests, sai lệch và giới hạn.
7. AC-01…AC-08: `PASS` / `FAIL` / `BLOCKED` / `NOT_RUN`, đường dẫn evidence.
8. Kết luận `GO` / `GO_WITH_CONDITIONS` / `NO_GO`, đề xuất WP-01 và điều kiện đi kèm.

## 5. Tiêu chuẩn chung cho experiment

Mỗi experiment phải đủ thông tin để một lần chạy khác có thể tái hiện ở mức hợp lý:

| Trường | Ví dụ / yêu cầu |
|---|---|
| `experiment_id` | `wp03-gpt-mini-001` |
| `hypothesis` | Giả thuyết kiểm chứng, không chỉ ghi “thử model” |
| `code_revision` | Commit SHA **nếu đã có**; không tạo commit chỉ để lấy số |
| `environment` | OS, Python, framework/backend versions, CPU/GPU/RAM |
| `dataset` | Nguồn, giấy phép, phiên bản, checksum/manifest, split và nguy cơ leakage |
| `model` | Kiến trúc, size, tokenizer, checkpoint và giấy phép nếu có |
| `config` | Seed, precision, batch size, LR, steps/epochs, context length |
| `metrics` | Phù hợp tác vụ: loss, perplexity, task accuracy, latency, tokens/s, memory |
| `evidence` | Raw summary logs an toàn, bảng số liệu, câu lệnh chạy, lỗi và giới hạn |
| `conclusion` | So sánh baseline, phân tích trade-off và bước tiếp theo |

**Tối thiểu cho benchmark:** cùng workload, cùng phiên bản model/dataset, warm-up, nhiều lần đo, thống nhất đơn vị và phương pháp. Nếu GPU async phải đồng bộ trước khi lấy elapsed time.

## 6. Phụ thuộc, rủi ro và phương án điều chỉnh

| Rủi ro | Dấu hiệu | Cách xử lý tối thiểu |
|---|---|---|
| MPS/OS không tương thích | `is_available()` false, operation unsupported | Xác minh OS/PyTorch, chạy CPU cho WP nền tảng, ghi rõ blocker |
| Thiếu SSD | Không đủ chỗ cho wheel/model/checkpoint | Đo trước, giảm model/corpus, dùng đường dẫn lưu khác sau phê duyệt |
| 32 GB RAM không đủ cho fine-tuning lựa chọn | OOM, swap mạnh, thời gian chạy bất hợp lý | Giảm model/context/batch, quantized model tương thích, đánh giá cloud GPU có duyệt |
| Cơ sở toán chậm hơn dự kiến | Không giải thích được training loop | Tăng bài tập trực quan, lùi WP-02, không đốt giai đoạn |
| Dataset không hợp pháp hoặc lộ dữ liệu | License thiếu, chứa thông tin nội bộ | Không dùng; thay bằng data giả lập/công khai rõ quyền |
| Đánh giá gây ngộ nhận | Leakage, chỉ xem ví dụ đẹp, train/test trộn | Freeze test, so sánh baseline, phân tích lỗi, report cả thất bại |
| Phạm vi phình to | Cần K8s/DB/MLOps platform quá sớm | Chỉ chấp nhận công nghệ mới khi giải quyết blocker thực tế |

### Điểm ra quyết định (decision gates)

- **Sau WP-00:** xác nhận SSD/OS, hiệu năng MPS; mới chốt phiên bản framework, ngân sách thiết bị và kích thước GPT nhỏ.
- **Sau WP-03:** nếu GPT mini chưa train ổn định, ưu tiên sửa kiến thức/training loop trước fine-tuning.
- **Sau WP-04:** lựa chọn đào sâu model adaptation hay quay lại tối ưu dataset/evaluation tùy bằng chứng.
- **Sau WP-06:** chỉ chọn runtime/serving stack theo benchmark, không theo xu hướng công nghệ.

## 7. Quản trị thay đổi và phê duyệt

- **Được chốt:** roadmap v1.0, cấu trúc tài liệu, mục tiêu 28 tuần và WP-00 thiết kế.
- **Chưa được chốt:** triển khai WP-00, bổ sung dependency, các thao tác Git **ngoài branch và commit/push ba tài liệu nền tảng đã được duyệt** (bao gồm PR/merge), sử dụng cloud và phí phát sinh, triển khai service.
- Mỗi WP bắt đầu bằng design/scope/AC. Sửa source + tests chỉ khi có phê duyệt giải pháp/phạm vi. Thao tác Git ghi lịch sử, thêm dependency, thay đổi DB/migration, triển khai, chi phí cloud phải có phê duyệt riêng.
- Nếu phải đổi số tuần, cấu hình model hoặc AC: ghi lý do, tác động và xin duyệt; không âm thầm sửa kết quả nghiệm thu.
- Không xóa/reset dữ liệu, repo, dataset hoặc checkpoints của người dùng không có sự đồng ý rõ ràng. Tránh ghi đè `.env`.

Xem [AGENTS.md](../../AGENTS.md) để biết quy tắc áp dụng cho người học, cộng tác viên và AI coding agents.

## 8. Tài liệu tham khảo

- [PyTorch tutorials — Learn the Basics](https://pytorch.org/tutorials/beginner/basics/intro.html)
- [PyTorch — MPS Backend](https://docs.pytorch.org/docs/stable/notes/mps.html)
- [Hugging Face — LLM Course](https://huggingface.co/learn/llm-course/chapter1/1)
- [Hugging Face — Training a causal language model from scratch](https://huggingface.co/learn/llm-course/chapter7/6)
- [Apple — MLX-LM](https://github.com/ml-explore/mlx-lm)
- [Apple — MLX-LM LoRA guide](https://github.com/ml-explore/mlx-lm/blob/main/mlx_lm/LORA.md)

> Các đường dẫn là nguồn học. Không pin phiên bản thư viện trong tài liệu học; phiên bản thực tế phải được chọn theo môi trường đã kiểm tra và ghi vào lock/config khi được triển khai.

---

**Roadmap owner:** Chủ repository  
**Tình trạng ban hành:** Nội dung tài liệu chuẩn bị để đưa vào repository; chưa commit/push bởi trợ lý.  
**Quy ước tài liệu:** Tiếng Việt; mã định danh và tên hàm bằng tiếng Anh.