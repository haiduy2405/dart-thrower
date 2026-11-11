# 🎯 Phi Tiêu Điện Thoại

Phone-as-dart-thrower: màn hình lớn hiện bia, mỗi người quét QR và dùng điện thoại ngắm + vung tay ném. 2–6 người, 3 lượt × 3 phi tiêu.

## Chạy
- **Phải qua HTTPS** (cảm biến điện thoại không chạy trên http/file). Cách nhanh nhất: GitHub Pages.
- Mở `index.html` trên laptop/TV → quét QR bằng điện thoại.
- Màn hình lớn (TV/PC/laptop) **chỉ để xem**, không có nút, không dùng bàn phím hay chuột. Mọi thứ điều khiển trên điện thoại.

## Deploy GitHub Pages
```bash
git init && git add . && git commit -m "Phi Tieu Dien Thoai v0.1"
git branch -M main
git remote add origin https://github.com/haiduy2405/dart-thrower.git
git push -u origin main
```
Repo → Settings → Pages → Branch `main` / root. URL: `https://haiduy2405.github.io/dart-thrower/`

## Điều khiển trên điện thoại
- Vào phòng là điện thoại **tự chuyển toàn màn hình** như một ứng dụng (Android/Chrome). Không bôi đen chữ, không menu giữ lâu, không phóng to khi chạm đúp. iPhone không cho web tự toàn màn hình: bấm Chia sẻ → **Thêm vào Màn hình chính**, rồi mở từ biểu tượng.
- Khi vào phòng, **tâm mang tên bạn** hiện trên màn hình lớn và chạy theo hướng điện thoại. Lệch thì bấm **Căn giữa**.
- **Chủ phòng** = người vào đầu tiên (thoát thì quyền chuyển cho người kế tiếp). Chủ phòng chọn chế độ, số lượt, độ khó, phòng rồi bấm **Bắt đầu**. Màn hình lớn hiện đúng lựa chọn, kèm luật chơi.
- Trong trận, chủ phòng có **Menu**: Tạm dừng / Tiếp tục, Chơi lại, Về sảnh.
- Khi chưa đến lượt, ai cũng có 4 nút **cổ vũ** (Cố lên! / Hụt rồi! / Ngon! / Hú hú!). Chữ bay lên từ tâm của người gửi trên màn hình lớn.
- Hết trận có thưởng vui: Tay run nhất, Thợ săn tâm, Cú ném đỉnh nhất.

## Chế độ chơi
| Chế độ | Luật |
|---|---|
| Cổ điển | Cộng điểm từng phi tiêu, 3/5/8 lượt, nhiều nhất thắng |
| Số May Mắn | Mỗi vòng một số được tô sáng. Trúng số mới có điểm (đơn ×10, kép ×20, ba ×30), trúng tâm +25 |
| Quanh Bia | Ném lần lượt 1 → 20 rồi tâm. Ném kép nhảy 2 số, ném ba nhảy 3 số. Ai xong trước thắng (tối đa 10 lượt) |
| Sinh Tồn | 3 mạng. Mỗi lượt phải ≥ điểm người ném trước, thấp hơn mất 1 mạng. Cần ≥ 2 người, người cuối cùng còn sống thắng |
| 301 | Trừ dần từ 301 về đúng 0. Vượt quá thì mất điểm của lượt đó (tối đa 10 lượt) |

## Cách chơi
1. Điện thoại: nhập tên → **Vào chơi** (iOS sẽ hỏi quyền cảm biến → Cho phép).
2. Cầm như remote TV, hướng vào bia → bấm **Căn giữa**.
3. Đến lượt: viền sáng lên → vung tay như ném phi tiêu. Lực vừa phải (~24 m/s²) bay thẳng; yếu thì rơi thấp, mạnh quá thì bay cao.
4. Máy không có cảm biến: vuốt lên trên màn hình để ném.

## Chỉnh độ nhạy
| Hằng số | File | Ý nghĩa |
|---|---|---|
| `RANGE` | play.html | Độ quay (°) = 1 bán kính bia. Nhỏ hơn = nhạy hơn |
| `TH` | play.html | Ngưỡng gia tốc nhận cú ném. Cao hơn = phải vung mạnh hơn |
| `LOOKBACK` | play.html | Bù trễ (ms) toạ độ ngắm trước cú vung |
| `SWEET` | index.html | Lực chuẩn không rơi/bay cao |
| `DIFF` | index.html | Hệ số rơi & rung tay cho Dễ/Thường/Khó |

## Lưu ý
- Âm thanh trên màn hình lớn: trình duyệt chặn phát tiếng cho đến khi có một lần tương tác. Nếu muốn có tiếng mà không cần chạm, mở Chrome với cờ `--autoplay-policy=no-user-gesture-required`. Không có tiếng thì game vẫn chơi bình thường (điện thoại vẫn rung).
- **Chỉ chơi qua Wi-Fi:** laptop/TV và tất cả điện thoại phải cùng một mạng Wi-Fi (tắt 4G trên điện thoại). Kết nối P2P WebRTC qua PeerJS (signaling cần internet, dữ liệu chơi đi thẳng trong mạng LAN). Nếu router bật "AP/Client isolation" thì các máy không thấy nhau — hãy tắt tuỳ chọn đó.
- Rớt mạng: vào lại bằng cùng tên để nhận lại slot.
