# Prompt tối ưu — Phi Tiêu Điện Thoại

```
ROLE: Senior web game developer (vanilla JS, Canvas 2D, WebRTC).

GOAL: Xây "Phi Tiêu Điện Thoại" — game phi tiêu nhiều người chơi chung 1 màn hình lớn.
Điện thoại là tay ném: dùng cảm biến để NGẮM (orientation) và NÉM (gia tốc kế). Người chơi vào phòng bằng QR.

CONSTRAINTS:
- Web tĩnh, không build step, không backend; deploy được lên GitHub Pages (HTTPS).
- 2 file chính: index.html (host/màn hình lớn), play.html (controller điện thoại). CSS/JS inline.
- Realtime: PeerJS 1.5.x (WebRTC, reliable:true). Peer id "phitieu-" + mã phòng 4 ký tự. QR qrcodejs trên cdnjs.
- Giao diện tiếng Việt. Host chạy tốt ở 1080p; controller portrait, nút to, ánh sáng thấp.

FEATURES (bắt buộc):
1. Lobby: QR + mã phòng, danh sách người chơi (tối đa 6, màu riêng), chọn độ khó Dễ/Thường/Khó, nút Bắt đầu.
2. Bia chuẩn: 20 sector đúng thứ tự, Bull 50, 25, Double x2, Triple x3, số vòng ngoài. Toạ độ chuẩn hoá bán kính=1.
3. Luật: 3 lượt x 3 phi tiêu, lần lượt từng người. Tổng điểm cao nhất thắng; hoà → đồng hạng.
4. Ngắm: yaw=alpha, pitch=beta trừ mốc calibrate (nút "Căn giữa"); 20° = 1 bán kính. Host hiển thị tâm ngắm của người đang tới lượt (làm mượt).
5. Ném: devicemotion, ngưỡng 14 m/s², thu đỉnh 130 ms, dùng toạ độ ngắm 90 ms TRƯỚC khi vung (bù trễ). Lực sweet-spot ~24: yếu → rơi thấp, mạnh → bay cao nhẹ. Cooldown 1.5 s.
6. Host là nguồn sự thật: tính điểm, hiệu ứng bay (phối cảnh, vòng cung), phi tiêu cắm lại, popup điểm, bảng điểm, âm thanh WebAudio.
7. Điện thoại: rung khi trúng, hiển thị lượt/điểm/phi tiêu còn lại; iOS requestPermission trong cú chạm "Vào chơi"; wake lock.
8. Rớt mạng: bỏ lượt, cùng tên vào lại nhận lại slot; vào muộn được phép.
9. Fallback: vuốt lên để ném (máy không có cảm biến); "Thử bằng chuột" trên host để test solo.
10. Màn kết quả: xếp hạng + Chơi lại.

QUALITY BAR: không lỗi console; không dùng thư viện ngoài PeerJS & qrcodejs; escape tên người chơi; code gọn, có hằng số chỉnh được (RANGE, TH, SWEET).

DELIVERABLES: index.html, play.html, README.md (cách chạy, deploy Pages, mẹo cầm điện thoại, chỉnh độ nhạy).
```
