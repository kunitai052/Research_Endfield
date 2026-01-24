---
aliases:
- Cơ chế chiêu mộ nhân vật Endfield
date-created: Fri, 23/01/2026 | 14:34:16 (GMT+07:00)
status:
- Đã hoàn thành
tags:
- Self-Research
- Arknight
- Endfield
---

# GIỚI THIỆU VỀ CƠ CHẾ CHIÊU MỘ NHÂN VẬT CỦA TRÒ CHƠI `ARKNIGHT: ENDFIELD`

 > 
 > *Đây là một bài viết để giải thích về cơ chế "gacha" của `Endfield` tới từ một người chưa từng động tay chơi 1 game gacha nào ngoài mấy con mì ăn liền như Rise Of Kingdoms~*

Nội dung trong bài được tham khảo phần lớn từ bài viết ["Arknight: Giải thích chi tiết về logic của Thuật toán rút thẻ"](https://github.com/mark9804/endfield-gacha-calculator/tree/main/src/utils) của **một fap sư tung của** 🙏

* *Cảm ơn Kimiku (`@yuuki.music.chill`) đã nói cho tui về cơ chế "lệch 50-50"* 🫂
* *Cảm ơn Hikari (`@hitori.hikari`) đã giải thích cho tui hiểu về "2 nhân vật phụ của 1 banner giới hạn"* 🫂
* *Cảm ơn Wang (`@roadto300k`) đã cho tui thấy bản thân mình rảnh háng như thế nào* 🫠

 > [!CAUTION]
 > Bài viết này được dựa trên dữ liệu thu thập được từ giai đoạn **beta-test** của `Endfield`, các cơ chế được nêu ở đây có thể **đã bị thay đổi** khi trò chơi ra mắt chính thức.  
 > Mọi thông tin chỉ mang tính chất tham khảo.

# 1. CƠ CHẾ CHIÊU MỘ CỦA TRÒ CHƠI 💳

 > 
 > Các nội dung bên dưới đang nói tới **Vòng quay Giới hạn (Limited Banner)**, một dạng chiêu mộ nhân vật chỉ tồn tại trong **1 khoảng thời gian nhất định**. Mỗi vòng quay giới hạn sẽ có một **nhân vật đại diện**, là nhân vật 6 sao người chơi **chắc chắn** nhận được khi đạt các điều kiện của các [cơ chế đặc biệt](#12-các-cơ-chế-đặc-biệt-).

## 1.1 Tỉ lệ Cơ bản và Hệ thống Bảo hiểm 💸

* **Mỗi lần quay** tốn: 500 Crystalline Jade.
* Tỉ lệ nổ **nhân vật 6 sao** gốc: 0.8%.
* **Bảo hiểm Mềm** (Soft Pity): Bắt đầu từ lần quay **thứ 66**, tỉ lệ nổ 6 sao sẽ **tăng thêm 5% cho mỗi lần quay xịt**.
* **Bảo hiểm Cứng** (Hard Pity): Tỉ lệ Bảo hiểm **đạt mốc tối đa** tại lần quay **thứ 80** (ước tính là 75.8% + 0.8% = 83.6%).
  * Tỉ lệ cho lần thứ 79 là: $`0.8\% + (79 - 66) \times 5\% = 75.8\%`$
  * Tỉ lệ áp dụng cho lần thứ 80 trở đi, thay vì tiếp tục +5% thì chỉ được +0.8%
* **Nổ trúng** (Rate Up): Khi nổ 6 sao, chỉ có 50% **nổ trúng banner** (nhân vật **đại diện** của vòng quay) 50% còn lại sẽ là một nhân vật 6 sao khác (lúc này gọi là **"nổ lệch" hay "lệch rate"**).
* Khi nổ 6 sao (**bất kể nổ trúng hay lệch**), Bảo hiểm sẽ bị xóa, tỉ lệ nổ 6 sao sẽ bị **đặt lại về 0.8%**.

## 1.2. Các Cơ chế Đặc biệt ✨

## 1.2.1. Nổ 120 🧧

Nếu sau **119 lượt quay** mà vẫn chưa nổ **nhân vật đại diện**, lần thứ 120 sẽ **chắc chắn nổ ra nhân vật này**.

=======
* Cơ chế chỉ áp dụng **1 lần** cho **mỗi vòng quay giới hạn**. Nếu người chơi đã nổ nhân vật đại diện trong vòng quay này (bất kể bằng cơ chế `Nổ 120` hay [cơ chế thường](#11-Tỉ-lệ-Cơ-bản-và-Hệ-thống-Bảo-hiểm-)), `Nổ 120` vẫn sẽ bị **vô hiệu hóa đến hết vòng quay**.
>>>>>>> origin/main

## 1.2.2. Nổ tích lũy 240 ↗️

Cứ **mỗi 240 lần quay trong 1 vòng quay** (lần quay thứ 240, 480...), người chơi **chắc chắn nổ nhân vật đại diện của vòng quay này**.

 > [!NOTE]
 > Đây là một **cơ chế đặc biệt**, khi kích hoạt sẽ **không đặt lại** tỉ lệ bảo hiểm đã tích lũy của người chơi.

# 2. Tính Xác suất Nổ 6 sao 🧮

## 2.1 Trường hợp 1: Nổ trong Vòng quay Giới hạn 🎡

Các cơ chế đặc biệt có thể áp dụng trong trường hợp này:

* `Nổ 120`
* `Nổ tích lũy 240`

$\Rightarrow$ `Nổ 6 sao = Tỉ lệ Nổ (+ Tỉ lệ Bảo hiểm) * Tỉ lệ Nổ trúng (50%) + Cơ chế đặc biệt`.

## 2.2 Trường hợp 2: Nổ ngoài Vòng quay Giới hạn 💥

Khi hết vòng quay giới hạn, nhân vật đại diện của vòng quay đó sẽ **còn được xuất hiện** trong **vòng quay giới hạn tiếp theo** (*trong... 1 khoảng thời gian giới hạn :v*). Nếu người chơi có thể chiêu mộ được họ lúc này, lần quay đó sẽ được gọi là **"Nổ hù" (Spook)**.

* Tại một thời điểm, trong `Endfield` sẽ có **2 nhân vật 6 sao đại diện gần nhất** (*?*) có thể được chiêu mộ từ một vòng quay giới hạn.
  * Ngoài ra, lúc này họ bị **gom chung** với các **nhân vật 6 sao vĩnh viễn** (*là các nhân vật 6 sao **luôn tồn tại trong các vòng quay giới hạn***) nên không còn được hưởng các [cơ chế đặc biệt](#1-2-cac-co-che-dac-biet-) nữa.
  * *Bạn hiểu vấn đề rồi đúng k, để quay được 1 nhân vật đại diện trong một vòng quay giới hạn mà họ không phải là đại diện, ta phải **nổ lệch*** 🤡

Giờ ta hãy tính xác suất nổ được nhân vật ta cần trong trường hợp này nào:

* Như đã nói từ nãy, xác suất **nổ lệch** trong **1 lần nổ 6 sao** là 50%
* Giả sử vòng quay thường có $N$ nhân vật 6 sao vĩnh viễn, xác suất để **1 lần nổ lệch 6 sao ra đúng nhân vật đại diện ta cần** sẽ là $\frac{1}{N + 2}$.

$`\Rightarrow \text{Vậy xác suất sẽ là: Xác suất nổ 6 sao} \times 50\% \times \frac{1}{N+2}`$

# 3. TÍNH XÁC SUẤT ĐỂ LÀM GÌ

 > 
 > *Oke, mình nghĩ tới đây chắc mng sẽ hỏi Chin-su viết cái bày này để làm gì đúng k. Mình sẽ liệt kê ra một số lí do mà (mình nghĩ là) sẽ thuyết phục được mọi người:*
 > 
 > *1. Ờm... mình... bị rảnh đấy -\_-*
 > 
 > *2. Từ công thức này, mọi người có thể thiết kế được một **máy tính tỉ lệ nổ nhân vật**, như [anh fap sư này](https://endfield-gacha-calculator.vercel.app/)*
 > 
 > *3. Từ những gì ta đã thảo luận, mng sẽ thấy **mọi tỉ lệ chỉ là tương đối**, chỉ có `Nổ 120` và `Nổ tích lũy 240` mới là **chân ái**, là thứ ta hướng tới trong mỗi lần chiêu mộ nhân vật. Hãy tỉnh táo, đừng để bị rơi vào cạm bẫy của tư bản nhé :3*

Bài viết tới đây là kết thúc, cảm ơn mọi người đã dành thời gian để đọc, chúc mọi người chơi `Endfield` thật lành mạnh nhé ❤️

# 🖇️ CÁC NGUỒN THAM KHẢO

1. https://github.com/mark9804/endfield-gacha-calculator/tree/main/src/utils
1. https://www.reddit.com/r/gachagaming/comments/gm6vpk/what_are_some_general_gacha_gaming_terms_and/
1. https://cellphones.com.vn/sforum/genshin-impact-toan-tap-ve-quy-tac-gacha-lech-rate-bao-hiem-va-dinh-chuan

# 📃 NHẬT KÝ THAY ĐỔI

* Fri, 23/01/2026: Đã tạo bài viết

\- *Chin-su* -
