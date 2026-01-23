---
aliases:
  - Cơ chế chiêu mộ nhân vật Endfield
date-created: Fri, 23/01/2026 | 14:34:16 (GMT+07:00)
status:
  - Đang viết/Đã hoàn thiện/Đã hoàn thành 
tags:
  - Self-Research
---
# GIỚI THIỆU SƠ BỘ VỀ CƠ CHẾ CHIÊU MỘ NHÂN VẬT CỦA TRÒ CHƠI `ARKNIGHT: ENDFIELD`
Nội dung trong bài viết  được tham khảo phần lớn từ bài [Arknight: Giải thích chi tiết về logic của Thuật toán rút thẻ](https://github.com/mark9804/endfield-gacha-calculator/tree/main/src/utils) của **một fap sư tung của** 🙏
- *Cảm ơn Kimiku (`@yuuki.music.chill`) đã nói cho tui về cơ chế "lệch 50-50"*.
- *Cảm ơn Hikari (`@hitori.hikari`) đã giải thích cho tui hiểu về "2 nhân vật phụ của 1 banner giới hạn*.
- *Cảm ơn Wang (`@roadto300k`) đã cho tui thấy bản thân mình rảnh háng như thế nào* 🫠

>[!Caution] Chú ý
>Bài viết này được dựa trên dữ liệu thu thập được từ giai đoạn **beta-test** của `Endfield`, các cơ chế được nêu ở đây có thể **đã bị thay đổi** khi trò chơi ra mắt chính thức.  
>Mọi thông tin chỉ mang tính chất tham khảo.
# 1. CƠ CHẾ CHIÊU MỘ CỦA TRÒ CHƠI
## 1.1 Tỉ lệ Cơ bản và Hệ thống Bảo hiểm
- **Mỗi lần quay** tốn: 500 Crystalline Jade.
- Tỉ lệ nổ **nhân vật 6 sao** ($P_{base}$): 0.8%.
- **Bảo hiểm Mềm** (Soft Pity): Bắt đầu từ lần quay **thứ 66**, tỉ lệ nổ 6 sao sẽ **tăng thêm 5% cho mỗi lần quay xịt**.
- **Bảo hiểm Cứng** (Hard Pity): Tỉ lệ bảo hiểm **đạt mốc tối đa** tại lần quay **thứ 80** (đo được là $75.8\% + 0.8\% = 83.6\%$).
	- Tỉ lệ cho lần thứ 79 là: $0.8\% + (79 - 66) \times 5\% = 75\%$
	- Tỉ lệ từ lần thứ 80, thay vì tiếp tục $+5\%$ thì chỉ được $+0.8\%$
- **Nổ trúng** (Rate Up): Khi nổ 6 sao, chỉ có 50% **nổ trúng nhân vật được quảng cáo** 50% chance of being the current UP, 50% chance of being non-UP.

Note: This game currently lacks a “Grand Pity” mechanism (where a miss guarantees a hit next time). Each pull is an independent 50/50 event.
1.2 Special Mechanics

These two mechanics only apply to the current gacha pool and trigger based on the user's set “Maximum Spending Limit” for that pool.
1.2.1 120-Pull Spark System

Rule: If no current UP character is obtained within the first 119 pulls of the pool, the 120th pull will guarantee an UP character.

Restriction: This rule activates only once per gacha event. It becomes inactive immediately if the player luckily draws an UP character or triggers this mechanism.

Impact: It truncates the long-tail distribution for unlucky players, providing a hard stop-loss point.
1.2.2 240 Milestone System

Rule: For every 240 cumulative pulls in the current gacha pool (240, 480...), players receive 1 additional potential for the current UP character.

Nature: This is an additional reward that does not consume the current pull result and does not reset the pity counter.
2. Calculation Logic Flow

To address the scenario where “players may stop pulling before reaching the cap to wait for future gacha pools,” we split the calculation logic into two phases:
2.1 Phase One: Current Banner Phase

Condition: Cumulative pulls ≤ User-set Maximum Investment for the current banner.

Logic:

    Receive protection from the 120-pull cap.

    Receive the 240 milestone reward.

    Target Acquisition Sources: Gacha pulls (50% chance) + Mechanism Guarantee + Mechanism Rewards.

2.2 Phase Two: Future Spook Phase

Condition: Current investment has reached the cap, but the target potential remains unmet.

Logic:

    No longer receive 120 wells (new wells from pools go to new characters).

    No longer receive 240 bonus (new bonuses from pools go to new characters).

    Target Source: Rely solely on “spooks”.

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