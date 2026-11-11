# Phi Tiêu Điện Thoại — Plan

**TL;DR:** Web tĩnh (GitHub Pages) · Host = màn hình lớn vẽ bia phi tiêu · Controller = điện thoại quét QR, dùng cảm biến để ngắm + vung tay ném · Kết nối P2P WebRTC qua PeerJS (không cần server) · 2–6 người, 3 lượt × 3 phi tiêu, tổng điểm cao nhất thắng.

## 1. Kiến trúc
| Thành phần | Chọn | Lý do |
|---|---|---|
| Hosting | GitHub Pages (HTTPS) | Bắt buộc HTTPS để dùng cảm biến |
| Realtime | PeerJS (WebRTC, signaling cloud miễn phí) | 0 server, 0 chi phí |
| QR | qrcodejs (cdnjs) | Nhẹ |
| Render | Canvas 2D, vanilla JS | Không build step |
| Files | `index.html` (host) · `play.html` (controller) | 2 trang, độc lập |

Room code 4 ký tự → peer id `phitieu-XXXX`. QR chứa `play.html?r=XXXX`.

## 2. Giao thức tin nhắn
- Phone→Host: `hello{name}` · `aim{x,y}` (~20Hz) · `throw{x,y,p}`
- Host→Phone: `welcome{color}` · `state{phase,round,myTurn,dartsLeft,cur,score}` · `hit{label,pts}` · `full`
- Toạ độ ngắm chuẩn hoá: bán kính bia = 1, gốc = tâm bia, y hướng xuống.

## 3. Cảm biến (phần khó nhất)
- **Ngắm:** `deviceorientation` — yaw = alpha, pitch = beta, trừ mốc **Căn giữa** (nút calibrate). 20° = 1 bán kính bia.
- **Phát hiện ném:** `devicemotion` gia tốc tuyến tính; vượt ngưỡng 14 m/s² → thu đỉnh trong 130 ms → gửi.
- **Bù trễ:** lưu lịch sử ngắm 600 ms, lấy toạ độ ngắm **90 ms trước** lúc bắt đầu vung (vì cú vung làm lệch tay).
- **Lực:** đỉnh gia tốc. Sweet spot ≈ 24 m/s². Yếu → rơi thấp; mạnh quá → bay cao nhẹ.
- **iOS:** `requestPermission()` gọi trong cú chạm "Vào chơi".
- **Fallback:** vuốt lên trên màn hình điện thoại để ném (máy không có cảm biến); chuột trên host để test solo.
- Chống spam: cooldown 1.5 s, host là nguồn sự thật (authoritative).

## 4. Luật
- 2–6 người, 3 lượt, mỗi lượt 3 phi tiêu. Điểm chuẩn bia: Bull 50, 25, Double ×2, Triple ×3, đơn 1–20.
- Độ khó: Dễ / Thường / Khó (hệ số rơi + rung tay).
- Rớt mạng: bỏ qua lượt; vào lại cùng tên sẽ nhận lại slot.

## 5. Milestones
1. **M1** Host: bia + tính điểm + chuột test
2. **M2** PeerJS lobby + QR + controller join
3. **M3** Cảm biến ngắm + ném + calibrate
4. **M4** Luật lượt/vòng, bảng điểm, màn kết quả
5. **M5** Âm thanh, rung, popup điểm, độ khó
6. **M6** Deploy Pages, test thật trên Android/iOS

## 6. Rủi ro & xử lý
- Cảm biến drift/gimbal → nút Căn giữa luôn hiện; tư thế khuyến nghị: cầm như remote TV.
- PeerJS signaling chậm lần đầu → hiển thị trạng thái kết nối.
- Mạng công ty/4G chặn P2P → (nâng cấp sau) thêm TURN.
- Âm thanh host cần cú chạm → bấm "Bắt đầu" kích hoạt.

## 7. Roadmap sau v1
Chế độ 301/501, Cricket, skin phi tiêu, hiệu ứng trượt nảy, TURN server, lưu điểm cao localStorage.
