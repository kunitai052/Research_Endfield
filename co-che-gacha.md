---
aliases:
  - Cơ chế chiêu mộ nhân vật Endfield
date-created: Fri, 23/01/2026 | 14:34:16 (GMT+07:00)
status:
  - Đang viết/Đã hoàn thiện/Đã hoàn thành 
tags:
  - Self-Research
---
# GIỚI THIỆU VỀ CƠ CHẾ CHIÊU MỘ NHÂN VẬT CỦA TRÒ CHƠI `ARKNIGHT: ENDFIELD`
>*Đây là một bài viết để giải thích về cơ chế "gacha" của `Endfield` tới từ một người chưa từng động tay chơi 1 game gacha nào ngoài mấy con mì ăn liền như Rise Of Kingdoms~*

Nội dung trong bài được tham khảo phần lớn từ bài [Arknight: Giải thích chi tiết về logic của Thuật toán rút thẻ](https://github.com/mark9804/endfield-gacha-calculator/tree/main/src/utils) của **một fap sư tung của** 🙏
- *Cảm ơn Kimiku (`@yuuki.music.chill`) đã nói cho tui về cơ chế "lệch 50-50"* 🫂
- *Cảm ơn Hikari (`@hitori.hikari`) đã giải thích cho tui hiểu về "2 nhân vật phụ của 1 banner giới hạn"* 🫂
- *Cảm ơn Wang (`@roadto300k`) đã cho tui thấy bản thân mình rảnh háng như thế nào* 🫠

>[!Caution] Chú ý
>Bài viết này được dựa trên dữ liệu thu thập được từ giai đoạn **beta-test** của `Endfield`, các cơ chế được nêu ở đây có thể **đã bị thay đổi** khi trò chơi ra mắt chính thức.  
>Mọi thông tin chỉ mang tính chất tham khảo.
# 1. CƠ CHẾ CHIÊU MỘ CỦA TRÒ CHƠI 💳
>Có 2 loại vòng quay chính trong trò chơi: **Vòng quay Giới hạn (Banner Limited)** và **Vòng quay Thường (Banner thường)**
>- Vòng quay Giới hạn, đúng như cái tên, **chỉ tồn tại trong một khoảng thời gian**, trước khi bị thay thế bằng một Vòng quay Giới hạn khác.
>	- Vòng quay Giới hạn **có các cơ chế đặc biệt** như Bảo hiểm, `Nổ 120` hay `Nổ tích lũy 240`, được liệt kê ở dưới.
>- Vòng quay Thường thì ngược lại, **tồn tại vĩnh viễn**. Tuy nhiên, nó không có các cơ chế bảo hộ người chơi (*?*), **thuần đen đỏ**.
## 1.1 Tỉ lệ Cơ bản và Hệ thống Bảo hiểm 💸
- **Mỗi lần quay** tốn: 500 Crystalline Jade.
- Tỉ lệ nổ **nhân vật 6 sao** ($P_{base}$): 0.8%.
- **Bảo hiểm Mềm** (Soft Pity): Bắt đầu từ lần quay **thứ 66**, tỉ lệ nổ 6 sao sẽ **tăng thêm 5% cho mỗi lần quay xịt**.
- **Bảo hiểm Cứng** (Hard Pity): Tỉ lệ bảo hiểm **đạt mốc tối đa** tại lần quay **thứ 80** (đo được là $75.8\% + 0.8\% = 83.6\%$).
	- Tỉ lệ cho lần thứ 79 là: $0.8\% + (79 - 66) \times 5\% = 75\%$
	- Tỉ lệ từ lần thứ 80, thay vì tiếp tục $+5\%$ thì chỉ được $+0.8\%$
- **Nổ trúng** (Rate Up): Khi nổ 6 sao, chỉ có 50% **nổ trúng banner** (nhân vật **đại diện** của vòng quay) 50% còn lại sẽ là một nhân vật 6 sao khác.
	- Khi nổ trúng, tỉ lệ nổ 6 sao sẽ bị **đặt lại về $P_{base}$**
## 1.2. Các Cơ chế Đặc biệt ✨
## 1.2.1. Nổ 120 🧧
Nếu sau **119 lượt quay** mà vẫn chưa nổ **nhân vật 6 sao đại diện**, lần thứ 120 sẽ **chắc chắn nổ ra nhân vật đại diện này**.
- Cơ chế chỉ áp dụng **1 lần** cho **mỗi vòng quay giới hạn**. Nếu người chơi đã nổ 6 sao trong vòng quay này (bất kể bằng cơ chế `Nổ 120` hay [cơ chế thường](#1.1%20Tỉ%20lệ%20Cơ%20bản%20và%20Hệ%20thống%20Bảo%20hiểm)), `Nổ 120` vẫn sẽ bị **vô hiệu hóa đến hết vòng quay**.
## 1.2.2. Nổ tích lũy 240 ↗️
Cứ **mỗi 240 lần quay trong 1 vòng quay** (lần quay thứ 240, 480...), người chơi **chắc chắn nổ nhân vật 6 sao giới hạn của vòng quay này**.

>[!Note]
>Đây là một **cơ chế đặc biệt**, khi kích hoạt sẽ **không đặt lại** tỉ lệ bảo hiểm đã tích lũy của người chơi.
# 2. Tính Xác suất Nổ 6 sao 🧮
## 2.1 Trường hợp 1: Nổ trong Vòng quay Giới hạn 🎡
Các cơ chế đặc biệt có thể áp dụng trong trường hợp này:
- `Nổ 120`
- `Nổ tích lũy 240`

$\Rightarrow$ `Nổ 6 sao = Tỉ lệ Nổ (+ Tỉ lệ Bảo hiểm) * Tỉ lệ Nổ trúng (50%) + Cơ chế đặc biệt`.
## 2.2 Trường hợp 2: Nổ ngoài Vòng quay Giới hạn 💥
Khi hết vòng quay giới hạn, nhân vật chính của vòng quay đó sẽ **được cho xuất hiện** trong **vòng quay thường** (*trong... 1 khoảng thời gian giới hạn :v*). Nếu người chơi có thể chiêu mộ được họ trong vòng quay thường, lần quay đó sẽ được gọi là **"Nổ hù" (Spook)**.
- Tại một thời điểm, sẽ có **2 nhân vật 6 sao giới hạn** (*?*) có thể được chiêu mộ từ vòng quay thường. Giả sử vòng quay thường có $N$ nhân vật 6 sao cố định (*là các nhân vật luôn có thể nổ ra từ vòng quay thường*), xác suất để **1 lần nổ 6 sao ra 1 nhân vật đặc biệt ta cần** từ vòng quay thường sẽ là $\frac{1}{N + 2}$.
- 
    Probability Model: When a 6-star appears in subsequent pools, there is a 50% chance of a spook; if spooked, the target character enters the permanent pool. Assuming the permanent pool contains N characters, plus 2 current support characters, totaling N + 2.

    Expected single pull hit rate: $\text{Six-Star Expected Hit} \div (0.5 \times \frac{1}{N_{std} + 2})$.

3. Algorithm Principles

This calculator offers two algorithms for user selection:


Target Hit Probability via Twist

# 🖇️ CÁC NGUỒN THAM KHẢO
1. https://github.com/mark9804/endfield-gacha-calculator/tree/main/src/utils
# 📃 NHẬT KÝ THAY ĐỔI
- Fri, 23/01/2026: Đã tạo bài viết
\- *Chin-su* \- 