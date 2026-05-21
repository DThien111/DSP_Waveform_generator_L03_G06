# Máy Phát Sóng Đa Kênh & Máy Phân Tích Phổ Tần Số

Một công cụ tương tác trực quan mô phỏng xử lý tín hiệu số (DSP) trên nền tảng Web, được xây dựng để giả lập cấu trúc của một máy phát sóng phần cứng, dao động ký (oscilloscope) và máy phân tích phổ (spectrum analyzer). Dự án mang lại trải nghiệm nghe - nhìn theo thời gian thực về lý thuyết tín hiệu rời rạc, các nguyên lý viễn thông và các ràng buộc thiết kế phần cứng ngay trên trình duyệt mà không cần cài đặt bất kỳ thư viện bên ngoài nào.

🚀 **Trải nghiệm trực tuyến (Live Demo):** https://dsp-l03-nhom6.netlify.app/

---

## 🌟 Các tính năng cốt lõi

### 1. Phát sóng đa kênh độc lập (CH1 & CH2)
* Hỗ trợ 5 dạng sóng cơ bản trong kỹ thuật: Sin (Sine), Vuông (Square), Tam giác (Triangle), Răng cưa (Sawtooth) và Nhiễu trắng (White Noise).
* Cho phép điều chỉnh thời gian thực các thông số: **Tần số** ($1\text{ Hz} - 20\text{ kHz}$), **Biên độ** ($0\text{ V} - 20\text{ Vpp}$) và **Pha ban đầu** ($0^\circ - 360^\circ$).
* Giao diện thẻ điều khiển (Tab UI) thông minh giúp tối ưu hóa không gian cấu hình tham số cho từng kênh.

### 2. Dao động ký số hai tia (Miền thời gian - Time Domain)
* **Hiển thị đồ thị kép (Dual Trace):** Vẽ và hiển thị đồng thời cả hai đường tín hiệu CH1 (Màu vàng) và CH2 (Màu xanh lá) trên cùng một màn hình nhờ HTML5 Canvas API.
* **Đồng bộ hóa mạch Trigger (Zero-Crossing):** Tích hợp thuật toán phần mềm tìm điểm cắt gốc tọa độ theo kênh CH1, giữ cố định pha của sóng trên đồ thị giúp người dùng quan sát góc lệch pha giữa hai kênh một cách chuẩn xác (ví dụ: minh họa độ lệch pha hình học $90^\circ$).
* Tích hợp các núm chia tỉ lệ Time/Div (Thời gian/Ô) và Volt/Div (Điện áp/Ô) linh hoạt để căn chỉnh dạng sóng.

### 3. Máy phân tích phổ (Miền tần số - Frequency Domain qua FFT)
* **Hiển thị phổ trộn (Mixed FFT):** Tính toán và hiển thị đè phổ tần số của cả hai kênh bằng thuật toán Biến đổi Fourier Nhanh (FFT Radix-2) đã qua tối ưu hóa.
* **Minh họa kỹ thuật ghép kênh viễn thông (FDM):** Mô phỏng trực quan nguyên lý Ghép kênh phân chia theo tần số (Frequency Division Multiplexing), hiển thị rõ ràng các đỉnh phổ (peaks) tách biệt khi các kênh phát ở tần số khác nhau.
* Hỗ trợ quan sát trực quan sự phân bố năng lượng sóng hài và **Hiện tượng Gibbs** (vọt lố/gợn sóng) của các dạng sóng phi sin (Vuông, Tam giác, Răng cưa).

### 4. Bộ trộn âm thanh thời gian thực & Mô phỏng Vật lý
* Tận dụng sức mạnh của **Web Audio API** tích hợp sẵn trong trình duyệt để tổng hợp các phương trình toán học rời rạc thành âm thanh vật lý thực tế phát ra loa.
* **Mô phỏng góc pha rời rạc:** Chuyển đổi góc lệch pha hình học thành độ trễ thời gian thực tế trong luồng tín hiệu thông qua `DelayNode`.
* **Hiện tượng giao thoa sóng âm (Phách - Beating):** Phát đồng thời hai kênh với độ chênh lệch tần số cực nhỏ (ví dụ: $1000\text{ Hz}$ và $1005\text{ Hz}$) để người dùng trực tiếp nghiệm chứng hiện tượng phách (âm thanh to nhỏ tuần hoàn) qua loa.

---

## 🛠️ Công nghệ sử dụng

* **Cấu trúc Frontend:** Thẻ ngữ nghĩa HTML5 (Semantic Elements)
* **Định dạng & Chủ đề:** CSS3 Grid, Flexbox, phong cách thiết kế Cyberpunk Kỹ thuật số / Viễn thông chuyên nghiệp.
* **Logic lõi & Bộ xử lý DSP:** JavaScript thuần (ES6+) không phụ thuộc thư viện ngoài.
* **Luồng tổng hợp âm thanh:** Web Audio API (`AudioContext`, `OscillatorNode`, `GainNode`, `DelayNode`, `AnalyserNode`)
* **Đồ họa & Đồ thị:** HTML5 Canvas API (Vòng lặp render hiệu suất cao sử dụng `requestAnimationFrame`)

---

## 📐 Nguyên lý DSP & Phần cứng được áp dụng

* **Chống chồng phổ bằng thiết kế (Anti-Aliasing by Design):** Để triệt tiêu hoàn toàn nhiễu chồng phổ (aliasing) mà không cần đến các bộ lọc phần cứng tương tự (analog), ứng dụng giới hạn cứng tần số tín hiệu đầu vào của thanh trượt ở mức tối đa là $20\text{ kHz}$ (ngưỡng thính giác con người). Kết hợp với việc card âm thanh tự động lấy mẫu ở mức cao ($44.1\text{ kHz}$ đến $96\text{ kHz}$), hệ thống luôn thỏa mãn tuyệt đối **Định lý lấy mẫu Nyquist-Shannon** ($f_s \ge 2f_{max}$), đảm bảo tín hiệu khôi phục đạt độ sạch toán học 100%.
* **Độ ổn định hệ thống (Sample Rate Fallback):** Mã nguồn xây dựng cấu trúc bọc ngoại lệ (`try-catch`) khi khởi tạo âm thanh. Nếu phần cứng của người dùng không hỗ trợ luồng xử lý tần số cao $96\text{ kHz}$, hệ thống sẽ tự động fallback (lùi về) tần số lấy mẫu mặc định của máy tính ($44.1\text{ kHz}$ hoặc $48\text{ kHz}$) để đảm bảo ứng dụng luôn chạy ổn định và không bị crash ngầm.

---

## 📦 Hướng dẫn chạy cục bộ (Offline)

Vì dự án được đóng gói toàn vẹn dưới dạng một ứng dụng web tĩnh dung lượng nhẹ, quá trình triển khai và nghiệm thu không đòi hỏi bất kỳ cấu hình máy chủ nào phức tạp:

1. Tải file ZIP hoặc sử dụng lệnh Clone để tải kho lưu trữ này về máy tính.
2. Đảm bảo tất cả các tệp tài nguyên cấu trúc bao gồm tệp `index.html`, ảnh `logo.png` và ảnh `background.jpg` đều nằm chung trong cùng một thư mục gốc.
3. Kích đúp để mở trực tiếp tệp `index.html` bằng bất kỳ trình duyệt web hiện đại nào (Chrome, Edge, Firefox, Safari). **Hệ thống hoạt động ngay mà không cần thiết lập Web Server cục bộ!**
